---
name: postiz-audit-channels
description: Audit which social channels a Postiz organization has connected, which are disabled, which customer each belongs to, and resolve platform-specific lookups before scheduling.
api: openapi/postiz-public-api-openapi.json
operations: [isConnected, listGroups, listIntegrations, getIntegrationSettings, triggerIntegrationTool, getIntegrationUrl, getAnalytics, deleteChannel]
generated: '2026-08-13'
method: generated
source: openapi/postiz-public-api-openapi.json + https://docs.postiz.com/public-api/integrations/list
---

# Audit and prepare Postiz channels

## Steps

1. **Check the credential.** `isConnected` (`GET /is-connected`).
2. **List customers.** `listGroups` (`GET /groups`) returns `{id, name}` groups. Agencies use these to segment channels per client.
3. **List channels.** `listIntegrations` (`GET /integrations`), optionally filtered by group id. Each returns `id`, `name`, `identifier` (the platform), `picture`, `disabled` and `customer`. Flag anything with `disabled: true` — those channels will not publish.
4. **Read each channel's contract.** `getIntegrationSettings` (`GET /integration-settings/{id}`) → `rules`, `maxLength`, the settings schema, and a `tools` array of platform helpers, each with `methodName`, `description` and `dataSchema`.
5. **Resolve platform-specific values.** `triggerIntegrationTool` (`POST /integration-trigger/{id}`) executes one of those helpers — list Discord channels, search subreddits, list LinkedIn pages, search Instagram audio for a Reel. Always resolve an **id** here rather than passing a human label into post settings.
6. **Spot-check health.** `getAnalytics` (`GET /analytics/{integration}`) returns follower/impression/engagement series per channel; a flat or empty series on a live channel usually means an expired token.

## Connecting and disconnecting

- `getIntegrationUrl` (`GET /social/{integration}`) generates an OAuth authorization URL to connect a new channel. It returns `400` for integrations that are not OAuth-based (Mastodon and anything needing an external URL) — those must be connected in the app.
- `deleteChannel` (`DELETE /integrations/{id}`) removes a channel **and every scheduled post on it**. This is destructive and unrecoverable through the API — confirm with a human before calling it.

## Rules

- `401` from `triggerIntegrationTool` usually means the channel's platform token expired, not that your API key is wrong. Reconnect the channel.
- `404` on settings or trigger means the integration or the named tool does not exist — re-read `listIntegrations` and the `tools` array rather than guessing a `methodName`.
- The UI calls these "channels"; the API calls them "integrations". Same thing.
