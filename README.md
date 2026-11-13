# Awesome-Real-Time-Webhook-Alerting-Event-Hooks

# Awesome Real-Time Webhook Alerting & Event Hooks

> A curated list of top Real-Time Webhook Alerting and Event Hook platforms — both SaaS/Hosted commercial solutions and open-source alternatives for reliably ingesting, routing, and delivering webhook events across your stack.
> 🌟 Star this repo if you find it useful! 🌟

---

## 📋 Table of Contents

- [SaaS / Hosted Platforms](#-saas--hosted-platforms)
  - [Druva Webhooks](#druva-webhooks)
  - [Svix](#svix)
  - [Hookdeck](#hookdeck)
  - [Webhook.site](#webhooksite)
  - [RequestBin](#requestbin)
  - [Zapier Webhooks](#zapier-webhooks)
  - [Make Webhooks](#make-webhooks)
  - [Courier Webhooks](#courier-webhooks)
- [Open-Source Software](#-open-source-software)
  - [Convoy](#convoy)
  - [RelayCore](#relaycore)
  - [webhook (Hookdoo)](#webhook-hookdoo)
- [Comparison at a Glance](#-comparison-at-a-glance)
- [Contributing](#-contributing)

---

## 🟦 SaaS / Hosted Platforms

Commercial, cloud-hosted Real-Time Webhook Alerting and Event Hook platforms. These are not open-source but are included as reference points for feature comparison.

### Druva Webhooks
**Type:** Data protection event streaming to security and IT systems
Druva's Webhooks, located in the Integration Center, post real-time events to a URL you specify — including alerts, unusual data activity, backup jobs, restore jobs, and API access [citation:1]. You can choose the provider (CrowdStrike or Others), set the endpoint URL, and configure authorization via API Key or OAuth 2.0 [citation:1]. This allows security services to consume Druva telemetry for threat detection, ransomware identification, or SIEM ingestion, as demonstrated by the Huntress integration guide requiring the `/raw` endpoint suffix and global "Export Events" toggle [citation:13]. Webhooks are supported exclusively on port 443 [citation:1].
**Best for:** Druva customers wanting to stream data protection events into SIEM, SOAR, or security platforms for real-time alerting and correlation.

### Svix
**Type:** Webhooks-as-a-service with consumer portal and multi-tenancy
Svix is a dedicated webhooks platform providing reliable delivery, retries with exponential backoff, signature verification, and a white-label consumer portal for your customers to self-manage subscriptions [citation:2][citation:14]. The free tier includes 50,000 messages/month with 7-day payload retention, while the Basic tier starts at $20/month with 30-day retention and 200 msgs/sec API rate limit [citation:2]. It supports multiple environments, unlimited consumer applications, and compliance with HIPAA, GDPR, PCI-DSS, and CCPA [citation:2]. Advanced features like custom signature schemes, OpenTelemetry streaming, and additional auth methods are gated to higher tiers [citation:2][citation:14].
**Best for:** SaaS companies wanting to add production-grade, multi-tenant webhooks to their product without building delivery infrastructure and a customer portal from scratch.

### Hookdeck
**Type:** Event gateway with queue, retries, and observability
Hookdeck provides an event gateway that sits between webhook sources and your application, guaranteeing ingestion even during downtime or traffic spikes [citation:3]. The Developer tier is free with 10,000 events, 3-day retention, and 1 user; the Team tier starts at $39/month with 7-day retention, unlimited users, and pay-as-you-go events at ~$0.33 per 100k [citation:3]. The Growth tier ($499/month) adds 30-day retention, SSO/SAML/SCIM, and HIPAA compliance [citation:3]. A 2026 pricing update increased free limits to 100k requests and 100k attempts, and made seats unlimited on all paid plans [citation:15].
**Best for:** Teams wanting a managed gateway that offloads webhook reliability concerns (queueing, retries, replay) to a platform with strong observability.

### Webhook.site
**Type:** Instant webhook inspection with workflow automation
Webhook.site gives you a unique URL and email address immediately for inspecting incoming webhooks, HTTP requests, form submissions, and emails in real time [citation:5]. The free tier gives you 7-day URL expiry and 100 requests, with data publicly viewable by anyone with the URL [citation:5]. Paid accounts unlock **Custom Actions** (visual and code-based workflows that run on every request), Queues for async processing and throttling, Schedules (cron for webhooks), and a managed PostgreSQL-compatible database [citation:5]. It has evolved from a simple inspector into a programmable automation endpoint.
**Best for:** Developers wanting instant webhook debugging plus a path to automating workflows (transform, forward, notify, store) without writing backend code.

### RequestBin
**Type:** Webhook debugging workspace with forwarding rules
RequestBin provides a webhook debugging workspace with named bins, request history, replay, and mock APIs [citation:6]. The Free tier includes 3 bins, 500 requests/bin/day, 100 requests stored per bin, and 5 API keys [citation:6]. The Pro tier ($12/month) unlocks 20 bins, unlimited request history, edit & replay with a full HTTP Requester, 5 forwarding rules, and 20 Mock APIs with 5 rules each [citation:6]. It includes an MCP server for AI IDEs and bulk export capabilities.
**Best for:** Developers and small teams wanting an affordable, organized webhook debugging workspace with request history and forwarding to a live app.

### Zapier Webhooks
**Type:** Webhook triggers and actions within automation
Zapier's Webhooks by Zapier app lets you trigger Zaps from incoming webhooks (Catch Hook) or send webhooks as actions (GET, POST, PUT, or Custom Request for PATCH/DELETE) [citation:7]. It handles automatic data parsing for standard methods, supports JSON/XML/Form/Raw payloads, Basic Auth, and custom headers [citation:7]. The Custom Request option provides raw JSON/XML flexibility for nested arrays, empty values, or specialized headers [citation:7]. It is a lightweight glue layer for connecting webhook-emitting services to 7,000+ apps without code.
**Best for:** Teams wanting no-code automation that consumes or emits webhooks as part of broader multi-app workflows.

### Make Webhooks
**Type:** Custom webhooks within visual automation
Make's Webhooks app lets you create custom webhooks and mailhooks to trigger scenarios instantly from third-party services [citation:8]. Each scenario uses its own unique webhook URL, with optional API Key authentication via the `x-make-apikey` header [citation:8]. You can define a data structure to validate incoming payloads (JSON, form data, multipart with file uploads up to 5 MB) or let Make accept all data without validation [citation:8]. It also supports request headers and JSON pass-through for accessing original payloads [citation:8].
**Best for:** Teams using Make for visual automation who need to receive webhooks as scenario triggers with structured data validation.

### Courier Webhooks
**Type:** Notification delivery via webhook provider
Courier's Webhook integration delivers HTTP requests to a static or dynamic URL as part of its notification orchestration platform [citation:9]. You can set the method, headers, and basic or bearer authentication, and control whether the payload includes limited or expanded profile data [citation:9]. Dynamic destinations let you specify the webhook URL per-recipient via the profile, and provider overrides can replace the URL, method, headers, or body entirely [citation:9]. It is a notification channel rather than a general-purpose webhook gateway.
**Best for:** Teams already using Courier for multi-channel notifications wanting to add webhook delivery as one of their notification channels.

---

## 🟩 Open-Source Software

Self-hosted, community-driven Real-Time Webhook Alerting and Event Hook tools. The open-source ecosystem is **limited but functional**, with Convoy as the most established gateway and newer entrants targeting specific gaps.

### Convoy
**Stack:** Go / PostgreSQL / Redis | **License:** Open Source (per project)
Convoy is an open-source, high-performance **webhooks gateway** designed to manage millions of webhooks end-to-end [citation:4]. It supports both **incoming** projects (receive webhooks from providers with a unique URL per source) and **outgoing** projects (publish events from your systems to customers via API) [from previous context]. Features include retries, filtering, transformations, portal links, and observability. It is the most mature open-source option for teams needing a unified gateway for both inbound and outbound webhook traffic.
**Best for:** Teams needing a self-hosted gateway for both receiving provider webhooks and sending outbound webhooks to customers, with retry and observability built in.

### RelayCore
**Stack:** Go / Redis / Docker | **License:** Open Source (per repository)
RelayCore is a self-hosted **event gateway for webhook routing, verification, deduplication, and delivery** with SOC-grade observability [citation:12]. It ingests webhooks from GitHub, Google Calendar, forms, and any HTTP producer, verifies HMAC-SHA256 signatures, deduplicates events atomically via Redis SET NX, routes based on event type + JSONPath conditions, transforms payloads per destination (GitHub→Slack, GitHub→Discord, Calendar→Database, Form→Email), and delivers with exponential backoff and dead-letter queue support [citation:12]. It includes rate limiting, encrypted credential storage, and a React monitoring dashboard. Deploys via Docker Compose [citation:12].
**Best for:** Teams wanting a focused, self-hosted gateway with signature verification, deduplication, and built-in transformers for common integrations (GitHub to Slack/Discord), accepting a younger project.

### webhook (Hookdoo)
**Stack:** Go | **License:** MIT
`webhook` is a lightweight, single-binary tool that does exactly one thing: it receives HTTP requests, parses headers/payload/query variables, checks if specified rules are satisfied, and passes arguments to a specified command via CLI or environment variables [citation:11]. It is the open-source core behind Hookdoo, which offers a SaaS version with a web interface and additional capabilities [citation:11]. It is not a delivery gateway with retries or a UI—it is a rules-based trigger for executing scripts on incoming webhooks.
**Best for:** Developers and sysadmins wanting a minimal, scriptable webhook receiver that executes shell commands based on incoming request rules, without a database or web UI.

---

## 📊 Comparison at a Glance

| Software | License | Stack | Inbound | Outbound | Retries/Queue | Self-Hosted | Best For |
|----------|---------|-------|---------|----------|---------------|-------------|----------|
| **Druva** | Proprietary | Cloud | ❌ | ✅ Event stream | (Platform) | ❌ | Data protection events to SIEM |
| **Svix** | Proprietary | Cloud | ❌ | ✅ Multi-tenant | ✅ | ❌ | Product webhooks + portal |
| **Hookdeck** | Proprietary | Cloud | ✅ Gateway | ✅ | ✅ Queue | ❌ | Managed reliability gateway |
| **Webhook.site** | Proprietary | Cloud | ✅ Inspector | ✅ Actions | ✅ Queues | ❌ | Debug + workflow automation |
| **RequestBin** | Proprietary | Cloud | ✅ Inspector | ✅ Forwarding | (Pro) | ❌ | Affordable debug + forward |
| **Zapier** | Proprietary | Cloud | ✅ Trigger | ✅ Action | (Zapier) | ❌ | No-code multi-app glue |
| **Make** | Proprietary | Cloud | ✅ Trigger | ✅ | (Scenario) | ❌ | Visual scenario triggers |
| **Convoy** | Open Source | Go/Postgres | ✅ | ✅ | ✅ | ✅ | Unified inbound + outbound |
| **RelayCore** | Open Source | Go/Redis | ✅ | ✅ | ✅ Backoff + DLQ | ✅ | Signature + dedup + routing |
| **webhook (Hookdoo)** | MIT | Go | ✅ | ❌ | ❌ | ✅ | Script trigger on request |

---

## 🤝 Contributing

Contributions are welcome! If you know of an open-source Real-Time Webhook Alerting or Event Hook tool that should be listed here, please open a pull request with:

- Project name and URL
- Brief description (1–2 sentences)
- Stack and license
- Why it stands out

Please ensure the project is actively maintained (releases within the last 12 months) and genuinely open-source. Note that the open-source ecosystem for **production-grade webhook delivery** is very limited. **Convoy** is the most established open-source gateway for managing webhooks end-to-end [citation:4]. **RelayCore** fills a specific gap with signature verification, atomic deduplication, and built-in transformers for common integrations [citation:12]. **webhook (Hookdoo)** is a minimalist script-trigger tool rather than a delivery gateway [citation:11]. Commercial platforms like Svix and Hookdeck remain far more capable for multi-tenant SaaS webhooks, consumer portals, and managed reliability at scale.

---

## 📄 License

This list is released under CC0 1.0 Universal (Public Domain). The software projects listed retain their respective licenses.

---

⭐ **If this list helped you discover a useful tool, please star the repo!** ⭐
