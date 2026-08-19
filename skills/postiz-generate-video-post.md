---
name: postiz-generate-video-post
description: Discover Postiz video generator options, resolve their dynamic parameters, generate a video, and schedule it to a video channel.
api: openapi/postiz-public-api-openapi.json
operations: [videoFunction, generateVideo, listIntegrations, getIntegrationSettings, uploadFromUrl, createPost]
generated: '2026-08-13'
method: generated
source: openapi/postiz-public-api-openapi.json + https://docs.postiz.com/public-api/video/generate
---

# Generate a video and post it with Postiz

Video generation is a 2026 addition to the Public API and is **not** covered by the `@postiz/node` SDK (last published 2025-07-27). Call it over HTTP or through the MCP tools `generateVideoOptions` / `videoFunctionTool` / `generateVideoTool`.

## Steps

1. **Discover generator options.** The video type catalogue lists each `type` identifier (e.g. `image-text-slides`, `veo3`), supported `output` orientations (`vertical` / `horizontal`), a `tools` array of helper functions, and a `customParams` JSON schema. Over MCP this is `generateVideoOptions`; over REST it is reached through `videoFunction` (`POST /video/function`).
2. **Resolve dynamic parameters.** `videoFunction` (`POST /video/function`) with the video type `identifier` and a `functionName` from that type's `tools` array — for example loading the available voices before choosing one.
3. **Generate.** `generateVideo` (`POST /generate-video`) with `type` (the identifier), `output`, and `customParams` filled from the schema in step 1. It returns the URL of the generated video.
4. **Bring the media into Postiz.** `uploadFromUrl` (`POST /upload-from-url`) with the generated video URL, so the post references a Postiz-hosted `path`. External URLs are rejected by the publishing pipeline.
5. **Check the target channel's rules.** `listIntegrations` then `getIntegrationSettings` for the video channel. YouTube needs `title`, `type`, `selfDeclaredMadeForKids`, optional `thumbnail` and `tags`. TikTok needs `privacy_level` and — critically — `content_posting_method: "DIRECT_POST"` to actually publish; `duet`/`stitch` are video-only and `autoAddMusic` is photo-only, and any setting that does not apply is silently discarded.
6. **Schedule.** `createPost` (`POST /posts`) with the uploaded media in `value[].image[]` and the platform `settings.__type`.

## Rules

- AI video is metered by plan (3/month on Standard up to 60/month on Ultimate) — a quota failure is a plan limit, not a rate limit.
- Generation is slow relative to a normal API call. Do not treat a long response as a failure and retry; there is no idempotency key, so a retry can burn a second video from the quota.
- Verify with `listPosts` over the target window before reporting success.
