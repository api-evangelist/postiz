---
name: postiz-schedule-post-with-media
description: Upload media to Postiz, discover a channel's real settings schema, and schedule a post to it without tripping the silent-discard failure mode.
api: openapi/postiz-public-api-openapi.json
operations: [isConnected, listIntegrations, getIntegrationSettings, uploadFile, uploadFromUrl, findSlot, createPost, listPosts]
generated: '2026-08-13'
method: generated
source: openapi/postiz-public-api-openapi.json + https://docs.postiz.com/public-api/introduction
---

# Schedule a Postiz post with media

Base URL `https://api.postiz.com/public/v1` (Cloud) or `{NEXT_PUBLIC_BACKEND_URL}/public/v1` (self-hosted).
Auth: the raw API key or a `pos_` OAuth token as the **entire** `Authorization` header value — no `Bearer` prefix on the Public API.

## Steps

1. **Verify the key.** `isConnected` (`GET /is-connected`). A 401 means the header is missing or the key is unrecognised; stop rather than retrying.
2. **List channels.** `listIntegrations` (`GET /integrations`). Optionally filter to one customer by first calling `listGroups` (`GET /groups`) and passing the group id. Keep the `id` (use when scheduling) and the `identifier` (the platform, e.g. `x`, `linkedin`, `tiktok`).
3. **Read the channel's real rules — do not skip this.** `getIntegrationSettings` (`GET /integration-settings/{id}`) returns `rules`, `maxLength`, the settings JSON schema, and the `tools` array. **A setting that does not apply to the chosen posting method or media type is silently discarded and the post still reports success**, so this call is your only chance to catch a mis-shaped payload.
4. **Upload media first.** `uploadFile` (`POST /upload`, multipart `file`) or `uploadFromUrl` (`POST /upload-from-url`, JSON `{"url": …}`). Keep the returned `id` and `path`. Raw filesystem paths and third-party URLs are rejected by the publishing pipeline — only a Postiz-hosted `path` works. Never base64-inline an image into the post body: `/posts` caps at 50 MB and returns `413`.
5. **Pick a slot (optional).** `findSlot` (`GET /find-slot/{id}`) returns the next available posting time for that channel.
6. **Create the post.** `createPost` (`POST /posts`) with `type` = `schedule`, `now`, or `draft`; a UTC ISO `date`; and `posts[]` each carrying `integration.id`, `value[].content` and `value[].image[]`, plus a `settings` object whose `__type` matches the channel's platform identifier.
   - Content is **HTML with a restricted tag set**: `<p>`, `<h1>`–`<h3>`, `<strong>`, `<u>`, `<ul>`, `<li>`. Wrap every line in `<p>`. Never combine `<u>` and `<strong>` in one element.
   - On thread platforms (X, Threads, Bluesky) each `value[]` item becomes a thread item; on LinkedIn and Facebook the first is the post and the rest are comments.
   - On TikTok set `content_posting_method` to `"DIRECT_POST"` unless the user explicitly wants to finish in the TikTok app — `"UPLOAD"` reports success but only drops the media into the account inbox.
7. **Verify.** `listPosts` (`GET /posts?startDate=…&endDate=…`) over the window you targeted and confirm the post exists in `QUEUE` or `PUBLISHED` state.

## Rules

- **No idempotency key exists.** On a timeout or 5xx after `createPost`, do **not** blindly retry: call `listPosts` for the target window and match first, or you will duplicate the post.
- Batch. The per-hour limit (90, 100 on Cloud) counts **requests on the create-post endpoint**, not posts — schedule many posts in one `createPost` call.
- `429` carries no `Retry-After` and no `RateLimit-*` headers. Back off exponentially with jitter.
- `403` means the resource belongs to another organization. Do not retry.
- Rollback is `deletePost` (`DELETE /posts/{id}`), which removes every post in the same group; a `404` means it is already gone and is safe to ignore.
