# Postiz (postiz)

Postiz is an open-source social media scheduling and management platform for posting across 30+ social, video, community, and blogging channels from a single calendar. It ships as a free AGPL-licensed self-hosted app and as a paid managed Cloud. The Postiz Public API uses simple API-key auth to list connected channels, upload media, and create, schedule, list, and delete posts.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/postiz/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/postiz/refs/heads/main/apis.yml)

## Tags

- Social Media
- Scheduling
- Open Source
- Content
- Marketing

## Timestamps

- **Created:** 2026-06-25
- **Modified:** 2026-06-25

## APIs

### Postiz Posts API

Create, schedule (draft / schedule / now), list by date range, and delete posts across all connected channels, with per-platform settings selected by a __type discriminator. Served identically by Postiz Cloud and self-hosted instances.

- **Human URL:** [https://docs.postiz.com/public-api](https://docs.postiz.com/public-api)
- **Base URL:** `https://api.postiz.com/public/v1`

#### Tags

- Posts
- Scheduling
- Publishing

#### Properties

- [Documentation](https://docs.postiz.com/public-api)
- [API Reference](https://docs.postiz.com/public-api/introduction)
- [OpenAPI](openapi/postiz-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/postiz.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/postiz.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Postiz Integrations and Channels API

List and manage connected social channels (integrations), list customer groups, fetch OAuth connect URLs, check connection status, and find the next available scheduling slot for a channel.

- **Human URL:** [https://docs.postiz.com/public-api](https://docs.postiz.com/public-api)
- **Base URL:** `https://api.postiz.com/public/v1`

#### Tags

- Integrations
- Channels
- OAuth

#### Properties

- [Documentation](https://docs.postiz.com/public-api)
- [OpenAPI](openapi/postiz-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/postiz.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/postiz.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Postiz Uploads API

Upload media files via multipart form data or by URL, returning a hosted media object whose id and path are referenced as images when creating posts.

- **Human URL:** [https://docs.postiz.com/public-api](https://docs.postiz.com/public-api)
- **Base URL:** `https://api.postiz.com/public/v1`

#### Tags

- Uploads
- Media
- Files

#### Properties

- [Documentation](https://docs.postiz.com/public-api)
- [OpenAPI](openapi/postiz-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/postiz.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/postiz.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Postiz Webhooks

Configure a webhook URL in Postiz to receive an HTTP POST notifying your own systems when a post is published, so you can sync downstream tools such as spreadsheets, Slack, or a CRM. Webhooks are configured in the app rather than through a Public API endpoint.

- **Human URL:** [https://docs.postiz.com/public-api](https://docs.postiz.com/public-api)
- **Base URL:** `https://api.postiz.com/public/v1`

#### Tags

- Webhooks
- Events
- Notifications

#### Properties

- [Documentation](https://docs.postiz.com/public-api)

## Common Properties

- [GitHub Organization](https://github.com/gitroomhq)
- [LinkedIn](https://www.linkedin.com/company/postiz)
- [Website](https://postiz.com)
- [Documentation](https://docs.postiz.com)
- [Plans](plans/postiz-plans-pricing.yml)
- [Rate Limits](rate-limits/postiz-rate-limits.yml)
- [Fin Ops](finops/postiz-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
