# Postiz (postiz)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
