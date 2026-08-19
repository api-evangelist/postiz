---
name: postiz-reconcile-published-posts
description: Find Postiz posts whose releaseId came back "missing", reconnect them to the real published content, and pull analytics once they resolve.
api: openapi/postiz-public-api-openapi.json
operations: [listPosts, getMissingContent, updateReleaseId, getPostAnalytics, getAnalytics, changePostStatus]
generated: '2026-08-13'
method: generated
source: openapi/postiz-public-api-openapi.json + https://docs.postiz.com/public-api/posts/missing-content
---

# Reconcile published Postiz posts

When a post publishes but the platform does not return a usable post id, Postiz sets `releaseId` to `"missing"`. Analytics stay dark until it is reconnected. This is the repair loop.

## Steps

1. **Sweep the window.** `listPosts` (`GET /posts?startDate=…&endDate=…`) over the range you published in. Each item carries `id`, `state` (`QUEUE`, `DRAFT`, `PUBLISHED`, `ERROR`), `publishDate`, `releaseURL`, `group`, and its `integration`.
2. **Select candidates.** Take posts in `PUBLISHED` state whose release id is `"missing"` (no usable `releaseURL`).
3. **Fetch candidates from the provider.** `getMissingContent` (`GET /posts/{id}/missing`) returns recent content from the connected platform as `{id, url}` items.
4. **Match, then reconnect.** Pick the item that matches the post's content and publish time and call `updateReleaseId` (`PUT /posts/{id}/release-id`). Only match on strong evidence — a wrong reconnection permanently attributes someone else's content to this post.
5. **Confirm analytics flow.** `getPostAnalytics` (`GET /analytics/post/{postId}`) should now return series. Channel-level numbers come from `getAnalytics` (`GET /analytics/{integration}`).

## Rules

- Only run step 4 on posts you published. `403` means the post belongs to another organization.
- `changePostStatus` (`PUT /posts/{id}/status`) moves a post between `draft` and `schedule` — it is not part of this repair loop and will not fix a missing release id.
- A `500` from a delete **can** mean "already gone" because of a known Postiz issue where a missing post id surfaces as 500 instead of 404. Treat every other `500` as a real server error: log it, back off, retry, do not silently suppress.
- Analytics fields vary by platform. Do not assume a metric exists across channels.
