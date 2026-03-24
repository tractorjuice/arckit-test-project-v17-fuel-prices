# Government Code Search Report: UK Fuel Price Transparency Service

> **Template Origin**: Official | **ArcKit Version**: 4.5.1 | **Command**: `/arckit.gov-code-search`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-GCSR-003-v1.0 |
| **Document Type** | Government Code Search Report |
| **Project** | UK Fuel Price Transparency Service (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 1.0 |
| **Created Date** | 2026-03-24 |
| **Last Modified** | 2026-03-24 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-06-24 |
| **Owner** | CMA Digital Lead (Product Owner) |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | CMA Digital, Delivery Team, Architecture Review Board |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 1.0 | 2026-03-24 | ArcKit AI | Initial creation from `/arckit.gov-code-search` agent -- GOV.UK Notify bulk messaging patterns | PENDING | PENDING |

---

## Executive Summary

### Search Query

**Original Query**: `GOV.UK Notify bulk messaging patterns`

**Query Variations Used**:

- `notifications API client sending bulk email and SMS to citizens`
- `GOV.UK Notify integration service email templates batch sending`
- `notify callback delivery status webhook retry queue processing`
- `compliance reminder email service government regulatory enforcement notifications`
- `batch notification processing scheduled messages registered users queue worker`
- `Celery SQS notification worker queue dead letter government service asynchronous`

**Platforms Searched**: govreposcrape (approximately 24,500 UK government repositories indexed), GitHub (alphagov, DFE-Digital, hmrc organisations via direct WebFetch verification)

### Results Found

**Total Repositories Scanned via govreposcrape**: 102 results across 7 query variations (before deduplication)

**Unique Repositories from govreposcrape (deduplicated)**: 48

**High Relevance Results (from direct GitHub verification)**: 10

**Medium Relevance Results**: 4

**Low Relevance / Excluded**: 48 (exclusively local council repositories with no GOV.UK Notify integration code)

### Top Results

| # | Repository | Organisation | Relevance | Language | Last Active |
|---|------------|--------------|-----------|----------|-------------|
| 1 | [notifications-api](https://github.com/alphagov/notifications-api) | GDS (alphagov) | High | Python | 2026-03 |
| 2 | [notifications-admin](https://github.com/alphagov/notifications-admin) | GDS (alphagov) | High | Python | 2026-03 |
| 3 | [email-alert-api](https://github.com/alphagov/email-alert-api) | GDS (alphagov) | High | Ruby | 2026-03 |
| 4 | [notifications-python-client](https://github.com/alphagov/notifications-python-client) | GDS (alphagov) | High | Python | 2026-03 |
| 5 | [notifications-utils](https://github.com/alphagov/notifications-utils) | GDS (alphagov) | High | Python | 2026-03 |

---

## Search Results

### High Relevance Results

#### notifications-api

| Attribute | Value |
|-----------|-------|
| **Organisation** | Government Digital Service (GDS) -- alphagov |
| **Repository URL** | https://github.com/alphagov/notifications-api |
| **Description** | The public-facing REST API for GOV.UK Notify, alongside internal management APIs and asynchronous Celery workers for processing and sending notifications across email, SMS, and letter channels |
| **Language** | Python 3.13 (99.5%) |
| **License** | MIT |
| **Last Activity** | 2026-03 (12,065 commits, 609 tags, 32 open PRs -- actively maintained) |
| **Stars** | 74 |

**Why Relevant**: This is the core backend of GOV.UK Notify itself. It reveals the authoritative patterns for how bulk messaging is processed internally, including queue-based architecture, batch splitting, rate limiting, and delivery orchestration. Understanding these internals is essential for designing a high-volume consumer service like Fuel Finder.

**Key Patterns**:

- **Celery task queue architecture**: Notifications are processed asynchronously through dedicated queues (JOBS, DATABASE, SEND_SMS, SEND_EMAIL, CALLBACKS), providing isolation between ingestion and delivery
- **Adaptive batch splitting via `shatter-job-rows`**: Large CSV uploads are split into batches of 32 rows; if a message exceeds SQS limits, the batch recursively subdivides by half until processable
- **Rate limit enforcement**: Sending limits are checked per-service before job processing via `__sending_limits_for_job_exceeded()`; failed validations trigger status updates rather than retries
- **Retry with exponential backoff**: Tasks implement `max_retries=5, default_retry_delay=300` seconds; duplicate detection prevents reprocessing via notification ID existence checks
- **FIFO queue semantics**: `MessageGroupId` ensures ordering guarantees across queue operations

---

#### notifications-admin

| Attribute | Value |
|-----------|-------|
| **Organisation** | Government Digital Service (GDS) -- alphagov |
| **Repository URL** | https://github.com/alphagov/notifications-admin |
| **Description** | GOV.UK Notify admin application -- enables users to register and manage services, create templates, send batch communications via CSV upload, and view notification history |
| **Language** | Python 3.13 (70.7%), HTML (17.2%), JavaScript (9.4%), SCSS (2.4%) |
| **License** | MIT |
| **Last Activity** | 2026-03 (18,303 commits -- actively maintained) |
| **Stars** | 45 |

**Why Relevant**: Demonstrates the user-facing bulk messaging workflow -- CSV upload, template management, batch sending, and notification history tracking. The CSV-to-bulk-send pattern is directly applicable to how Fuel Finder would send compliance reminders to approximately 8,500 retailers.

**Key Patterns**:

- **CSV-based bulk upload**: The primary mechanism for batch messaging -- users upload a CSV with recipient details and personalisation values, which the admin app processes into individual notification requests
- **Template management UI**: Flask-based interface for creating, editing, and versioning notification templates with personalisation placeholders
- **Notification history and tracking**: Dashboard for viewing delivery status of sent notifications, searchable by service, template, and time period
- **Service-level administration**: Each government service gets its own isolated configuration with separate API keys, rate limits, and templates

---

#### email-alert-api

| Attribute | Value |
|-----------|-------|
| **Organisation** | Government Digital Service (GDS) -- alphagov |
| **Repository URL** | https://github.com/alphagov/email-alert-api |
| **Description** | Sends emails to users that subscribe to specific GOV.UK email alerts -- provides a consistent internal interface to external email notification services |
| **Language** | Ruby (99.9%) |
| **License** | MIT |
| **Last Activity** | 2026-03 (release v579, 6,153 commits, 510 total releases -- actively maintained) |
| **Stars** | 18 |

**Why Relevant**: This is the most important pattern reference for Fuel Finder's notification architecture. It demonstrates how a high-volume government service (GOV.UK publishing platform) wraps GOV.UK Notify as a downstream dependency, managing subscriber lists, digest batching, and abstracted delivery. The Fuel Finder service needs an analogous abstraction layer for compliance reminders and enforcement notifications.

**Key Patterns**:

- **Abstraction layer over Notify**: Provides "a consistent internal interface to external email notification services" -- the service does not call Notify directly from business logic but through an abstracted notification service
- **Digest run batching**: Daily and weekly digest batches with defined start/end times and specific recipient sets -- directly applicable to Fuel Finder's daily compliance reminder use case
- **Subscriber list management**: Subscription lists with filtering criteria (e.g., "all publications by HMRC") -- applicable to Fuel Finder's retailer notification categories (compliance reminders, enforcement notices, account events)
- **Content change triggers**: Two notification types -- content-change-driven and standalone messages -- mapping to Fuel Finder's submission-driven confirmations and officer-initiated enforcement notices

---

#### notifications-python-client

| Attribute | Value |
|-----------|-------|
| **Organisation** | Government Digital Service (GDS) -- alphagov |
| **Repository URL** | https://github.com/alphagov/notifications-python-client |
| **Description** | Official Python client library for the GOV.UK Notify API -- supports email, SMS, and letter delivery with template personalisation |
| **Language** | Python (95.1%) |
| **License** | MIT |
| **Last Activity** | 2026-03 (830 commits) |
| **Stars** | 24 |

**Why Relevant**: The primary integration library for Python-based services consuming GOV.UK Notify. Given Fuel Finder's likely Python/Node.js tech stack, this client demonstrates the canonical integration pattern including template personalisation, error handling, and rate-limit-aware sending loops.

**Key Patterns**:

- **Sequential bulk sending**: No native batch API -- the official documentation states: "You cannot use a single API call to send messages in bulk." Consumers must iterate over recipients: `for recipient in recipients: client.send_email_notification(email_address=recipient, template_id=...)`
- **Template personalisation**: Double-bracket placeholders `((variable_name))` with support for strings, lists (rendered as bullet points), and file attachments via `prepare_upload()`
- **Error handling by status code**: 400 (do not retry -- validation error), 429 (rate limit exceeded -- exponential backoff), 500-599 (safe to retry) -- with `HTTPError` exception providing structured error messages
- **Delivery status polling**: `get_all_notifications()` with filters by template_type, status, and reference; `get_all_notifications_iterator()` for paginated traversal of large result sets
- **Smoke testing**: Designated test numbers (07700900000, 07700900111, 07700900222) and addresses (simulate-delivered@notifications.service.gov.uk) validate requests without sending or persisting records

---

#### notifications-utils

| Attribute | Value |
|-----------|-------|
| **Organisation** | Government Digital Service (GDS) -- alphagov |
| **Repository URL** | https://github.com/alphagov/notifications-utils |
| **Description** | Shared Python code for GOV.UK Notify applications -- standardises logging, rendering message templates, parsing spreadsheets, talking to external services and more |
| **Language** | Python (98.2%), Jinja (1.6%) |
| **License** | MIT |
| **Last Activity** | 2026-03 (3,476 commits) |
| **Stars** | 14 |

**Why Relevant**: Contains the reusable building blocks for template rendering and CSV/spreadsheet parsing that power the bulk messaging pipeline. This library is a dependency of 6+ Notify applications (API, Admin, Document Download, Template Preview, Email Stub) and demonstrates shared utility patterns for notification processing.

**Key Patterns**:

- **Template rendering engine**: Standardised rendering of message templates with personalisation variable substitution via Jinja
- **Spreadsheet parsing**: CSV and spreadsheet validation for bulk recipient lists -- validates column headers, data types, and required fields
- **Redis client wrapper**: `notifications_utils.redis_client.RedisClient` for caching and rate-limit tracking across the platform
- **Shared logging standards**: Consistent structured logging across all Notify microservices

---

#### notifications-node-client

| Attribute | Value |
|-----------|-------|
| **Organisation** | Government Digital Service (GDS) -- alphagov |
| **Repository URL** | https://github.com/alphagov/notifications-node-client |
| **Description** | Node client for the GOV.UK Notify API -- enables sending emails, text messages, and letters |
| **Language** | JavaScript (88.3%), TypeScript (8.6%) |
| **License** | MIT |
| **Last Activity** | 2026 (557 commits, 21 watchers) |
| **Stars** | 18 |

**Why Relevant**: Alternative integration client for Node.js-based services. Relevant if Fuel Finder uses Node.js for any backend components or microservices. Available as `notifications-node-client` on npm.

**Key Patterns**:

- **npm package distribution**: `npm install notifications-node-client` for straightforward integration
- **TypeScript support**: 8.6% TypeScript coverage provides type definitions for improved developer experience
- **Consistent API surface**: Mirrors the Python client's API patterns -- same endpoints, same personalisation model, same error handling approach

---

#### notifications-java-client

| Attribute | Value |
|-----------|-------|
| **Organisation** | Government Digital Service (GDS) -- alphagov |
| **Repository URL** | https://github.com/alphagov/notifications-java-client |
| **Description** | Official Java client library for the GOV.UK Notify API |
| **Language** | Java (98.8%) |
| **License** | MIT |
| **Last Activity** | 2026 (741 commits) |
| **Stars** | 8 |

**Why Relevant**: Java integration path. Actively maintained with 741 commits. Available on Maven Central at `uk.gov.service.notify/notifications-java-client`.

**Key Patterns**:

- **Maven Central distribution**: Standard Java dependency management
- **Docker and CI/CD integration**: GitHub Actions pipeline for automated testing and deployment
- **Consistent API surface**: Same patterns as other language clients

---

#### notifications-net-client

| Attribute | Value |
|-----------|-------|
| **Organisation** | Government Digital Service (GDS) -- alphagov |
| **Repository URL** | https://github.com/alphagov/notifications-net-client |
| **Description** | Official .NET client library for the GOV.UK Notify API |
| **Language** | C# (98.5%) |
| **License** | MIT |
| **Last Activity** | 2021-03 (v2.9.0 release, 524 commits) |
| **Stars** | 25 |

**Why Relevant**: .NET integration path for Notify. Less actively maintained than Python/Ruby/Node clients (last release March 2021), which is a consideration if the Fuel Finder service uses .NET components.

**Key Patterns**:

- **NuGet distribution**: Available as `GovukNotify` on NuGet
- **Consistent API design**: Same integration patterns as other language clients
- **Note**: Less recent activity compared to Python/Node clients -- verify compatibility with latest Notify API version before adoption

---

#### email-alert-service

| Attribute | Value |
|-----------|-------|
| **Organisation** | Government Digital Service (GDS) -- alphagov |
| **Repository URL** | https://github.com/alphagov/email-alert-service |
| **Description** | Message queue consumer that triggers email alerts when documents are published with a major change on GOV.UK |
| **Language** | Ruby (99.2%) |
| **License** | MIT |
| **Last Activity** | 2026-03 (release v313, 1,927 commits) |
| **Stars** | 4 |

**Why Relevant**: Demonstrates the event-driven notification pattern -- subscribing to a message queue (RabbitMQ `published_documents` exchange) and triggering notifications via the email-alert-api. This pattern maps to Fuel Finder's need to trigger compliance reminders based on data events (e.g., "no submission received in 24 hours").

**Key Patterns**:

- **Event-driven architecture**: Uses `govuk_message_queue_consumer` to subscribe to a RabbitMQ exchange -- notifications triggered by events rather than scheduled batch jobs
- **Separate processing pipelines**: Major change consumer and unpublishing consumer run as separate rake tasks, providing isolation between notification types
- **Queue-based asynchronous processing**: Message queues created via `bundle exec rake message_queues:create_queues` -- ensuring reliable, decoupled processing

---

### Medium Relevance Results

#### notifications-template-preview

| Attribute | Value |
|-----------|-------|
| **Organisation** | Government Digital Service (GDS) -- alphagov |
| **Repository URL** | https://github.com/alphagov/notifications-template-preview |
| **Description** | Generates PNG and PDF previews of letter templates created in the GOV.UK Notify admin app |
| **Language** | Python (95.3%) |
| **License** | MIT |
| **Last Activity** | 2026-03 (1,721 commits) |
| **Stars** | 3 |

**Why Relevant**: Template preview capability for validating notification content before sending. Useful reference if Fuel Finder needs template preview functionality for CMA officers reviewing enforcement notice templates.

**Key Patterns**:

- **Asynchronous PDF generation**: Uses Celery for PDF sanitisation tasks
- **Template rendering pipeline**: Converts template designs to PNG and PDF for visual validation
- **Flask and Docker**: Consistent with the Notify platform's technology choices

---

#### hmrc-email-renderer

| Attribute | Value |
|-----------|-------|
| **Organisation** | HMRC |
| **Repository URL** | https://github.com/hmrc/hmrc-email-renderer |
| **Description** | Renders parameterised email body content in HTML or plain text given a template -- backend rendering engine for HMRC Digital Contact team |
| **Language** | HTML (57.8%), Scala (42.2%) |
| **License** | Apache 2.0 |
| **Last Activity** | 2026-03 (v3.95.0, 1,930 commits, 1,155 releases) |
| **Stars** | 5 |

**Why Relevant**: Alternative approach to email templating at government scale. HMRC uses its own template rendering service rather than GOV.UK Notify's built-in templates, which is relevant as a comparison point for Fuel Finder's architecture decision on where to render notification content.

**Key Patterns**:

- **Separate rendering microservice**: Dedicated service for template rendering (POST `/templates/:templateId`) decoupled from delivery
- **Bilingual support**: English and Welsh template selection via preferences service integration
- **Developer preview mode**: Local preview on port 8950 during development -- addresses the challenge of testing templates without sending live messages

---

#### notifications-php-client

| Attribute | Value |
|-----------|-------|
| **Organisation** | Government Digital Service (GDS) -- alphagov |
| **Repository URL** | https://github.com/alphagov/notifications-php-client |
| **Description** | Official PHP client library for the GOV.UK Notify API |
| **Language** | PHP (97.8%) |
| **License** | MIT |
| **Last Activity** | 2026 (371 commits) |
| **Stars** | 11 |

**Why Relevant**: Completes the client library landscape. Demonstrates that GOV.UK Notify supports six official client languages (Python, Ruby, Node.js, Java, .NET, PHP) plus direct REST API access.

**Key Patterns**:

- **Packagist distribution**: Standard PHP package management
- **Consistent API surface**: Same integration model across all official clients

---

#### teaching-vacancies (DFE-Digital)

| Attribute | Value |
|-----------|-------|
| **Organisation** | Department for Education (DFE-Digital) |
| **Repository URL** | https://github.com/DFE-Digital/teaching-vacancies |
| **Description** | Free job-listing service from the Department for Education -- teachers search and apply for jobs, save jobs, and set up job alerts |
| **Language** | Ruby (78.7%), Slim (14.7%) |
| **License** | MIT |
| **Last Activity** | 2026-03 (19,050 commits) |
| **Stars** | 25 |

**Why Relevant**: Active DfE service integrating with GOV.UK Notify for job alert notifications to subscribers. Demonstrates a typical government service consumer pattern with subscriber management, alert notifications, and Rails-based architecture.

**Key Patterns**:

- **GOV.UK One Login integration**: Modern authentication approach for user-facing services
- **Ruby on Rails architecture**: Standard GDS technology choice for web services
- **Multi-audience notification routing**: Different authentication for publishers (DSI) vs jobseekers (GOV.UK One Login) -- demonstrates multi-audience notification patterns

---

## Code Patterns Identified

| Pattern | Repositories Using It | Description |
|---------|----------------------|-------------|
| Sequential bulk sending (no batch API) | notifications-api, notifications-python-client, notifications-node-client, notifications-ruby-client, notifications-java-client | GOV.UK Notify does not support a single API call for bulk sends -- consumers must iterate over recipients, sending one notification per API call, while respecting the 3,000 messages per 60-second rolling rate limit |
| CSV upload for batch messaging | notifications-admin, notifications-api | The admin UI accepts CSV uploads with recipient details and personalisation values; the API processes these as "jobs" using the `shatter-job-rows` task to split large uploads into manageable batches of 32 rows |
| Celery/queue-based async processing | notifications-api, notifications-template-preview, email-alert-service | Asynchronous task processing via Celery (Python) or message queues (RabbitMQ for Ruby services) ensures notification delivery does not block the submitting application |
| Abstraction layer over Notify | email-alert-api | High-volume services do not call Notify directly from business logic -- they wrap it in an abstraction layer that manages subscriber lists, digest batching, and delivery status tracking |
| Template personalisation with placeholders | All client libraries | Double-bracket placeholder syntax `((variable_name))` with support for strings, lists (rendered as bullet points), and file attachments -- consistent across all 6 official client libraries |
| JWT authentication | All client libraries, REST API | API keys encode service ID and secret; clients generate short-lived (30-second) JWTs for each request -- standard pattern across all integrations |
| Delivery status callbacks | notifications-api, REST API | Webhook-based delivery status updates (POST to configured URL) with retry policy of every 5 minutes up to 5 attempts -- enables asynchronous delivery tracking without polling |
| Three-tier API key model | All client libraries | Test (simulated delivery), Team and Guest List (limited real delivery), and Live (full production) keys provide progressive testing capability |

**Observations**: GOV.UK Notify's architecture is fundamentally designed around single-message API calls with client-side iteration for bulk sends. This is a deliberate design choice that pushes rate-limiting and batch management responsibility to the consumer service. The most successful high-volume integrations (like email-alert-api) build an abstraction layer that handles queuing, batching, retry logic, and subscriber management internally, treating Notify purely as a delivery provider.

The Celery-based queue architecture within Notify itself (JOBS -> DATABASE -> SEND_SMS/SEND_EMAIL -> CALLBACKS) demonstrates a mature pattern for decoupling ingestion from delivery. Consumer services should mirror this pattern by maintaining their own internal queue between business logic and the Notify API call.

---

## Implementation Approaches Compared

| Approach | Used By | Pros | Cons |
|----------|---------|------|------|
| **Direct API iteration** (loop over recipients, call Notify per message) | notifications-python-client examples, small services | Simple to implement; no additional infrastructure; works for low volumes ( < 3,000/min) | No resilience to failures mid-batch; no retry without custom code; blocks calling thread; hard to track batch completion |
| **CSV upload via admin UI** (manual bulk send) | notifications-admin | No code required; built-in template preview and validation; audit trail in Notify dashboard; supports up to 250,000 messages/day | Manual process; not suitable for automated/scheduled sends; requires human operator; no API-level control |
| **Abstraction layer with internal queue** (service wraps Notify behind queue + worker) | email-alert-api, email-alert-service | Resilient to Notify outages (queue buffers); automatic retry; batch management; subscriber list control; decoupled from delivery timing | More infrastructure (queue, worker, database); more complex to build and operate; requires monitoring of queue depth and delivery rates |
| **Event-driven triggers** (message queue consumer triggers notifications) | email-alert-service | Reactive to business events; decoupled from event producer; easy to add new notification types; natural fit for "no submission in 24h" triggers | Requires message broker infrastructure; more complex debugging; event ordering considerations; need dead-letter queue handling |
| **Separate rendering service** (custom template engine + Notify for delivery only) | hmrc-email-renderer | Full control over template rendering; bilingual support; preview without sending; complex formatting beyond Notify's capabilities | Additional microservice to maintain; diverges from Notify's template management; harder to use Notify's built-in personalisation features |

**Recommended Approach for This Project**: **Abstraction layer with internal queue + event-driven triggers** -- The Fuel Finder service should implement a notification service that wraps GOV.UK Notify behind an internal queue (e.g., SQS or Redis-backed Celery). This approach:

1. Handles the projected approximately 50,000 emails/month during retailer onboarding (per assumption A-2 in requirements)
2. Provides resilience when Notify is unavailable (requirement: "If GOV.UK Notify is unavailable: notifications are queued and retried; submissions are not blocked")
3. Supports event-driven triggers for compliance reminders ("no submission in 24 hours" triggers)
4. Enables circuit breaker pattern required by NFR-A-3 ("circuit breaker for all external dependencies including Notify")
5. Manages delivery status callbacks for enforcement action tracking (notification_id in enforcement_action entity)

---

## Project Relevance Mapping

| Repository | Relevant Requirements | How It Helps | Quick Start |
|---|---|---|---|
| [alphagov/notifications-python-client](https://github.com/alphagov/notifications-python-client) | INT-003, FR-009 | Official Python client for sending compliance reminders, submission confirmations, and enforcement notices via Notify API | `pip install notifications-python-client` |
| [alphagov/notifications-node-client](https://github.com/alphagov/notifications-node-client) | INT-003, FR-009 | Alternative client if Fuel Finder uses Node.js backend components | `npm install notifications-node-client` |
| [alphagov/notifications-api](https://github.com/alphagov/notifications-api) | INT-003, NFR-A-3 | Reference architecture for queue-based async processing, rate limiting, retry patterns, and batch splitting -- informs Fuel Finder's notification service design | `git clone https://github.com/alphagov/notifications-api.git` |
| [alphagov/notifications-admin](https://github.com/alphagov/notifications-admin) | FR-006, FR-009 | Template management and CSV bulk send patterns -- informs CMA officer workflow for sending enforcement notices to multiple retailers | `git clone https://github.com/alphagov/notifications-admin.git` |
| [alphagov/email-alert-api](https://github.com/alphagov/email-alert-api) | FR-009, NFR-A-3, INT-003 | Primary pattern reference for building a notification abstraction layer with subscriber management, digest batching, and delivery status tracking | `git clone https://github.com/alphagov/email-alert-api.git` |
| [alphagov/email-alert-service](https://github.com/alphagov/email-alert-service) | FR-009, FR-012 | Event-driven notification trigger pattern -- applicable to "no submission in 24 hours" compliance reminder trigger | `git clone https://github.com/alphagov/email-alert-service.git` |
| [alphagov/notifications-utils](https://github.com/alphagov/notifications-utils) | INT-003, FR-009 | Shared utilities for template rendering and CSV parsing -- reusable patterns for Fuel Finder's notification module | `pip install notifications-utils` (or clone for reference) |

---

## Search Effectiveness Assessment

### Coverage

The search achieved **strong coverage for the GOV.UK Notify platform itself** (core platform repositories, all 6 official client libraries, administrative interface, utility libraries, and template preview service) and **good coverage for the email-alert ecosystem** (the highest-volume Notify consumer on GOV.UK).

However, the search revealed a **significant gap in the govreposcrape index**: none of the 102 results from 7 govreposcrape queries returned any central government organisation repository (alphagov, hmrc, dwp, moj, dfe, cabinetoffice, NHSDigital, govuk-one-login). All govreposcrape results were from local council organisations (Dorset-Council-UK, east-sussex-county-council, BathnesDevelopment, BristolCityCouncil, BracknellForestCouncil, CamdenCouncil, brighton-hove-gov-uk, DundeeCityCouncil, CityOfYork). None of these local council repos contained GOV.UK Notify integration code.

### Gaps

| Gap Area | Alternative Search Strategy |
|----------|---------------------------|
| **Consumer service integration patterns** (how DWP, HMRC, MoJ services integrate Notify) | Search directly: `https://github.com/search?q=org%3Adwp+notify&type=code` or `https://github.com/search?q=org%3Ahmrc+notify&type=code` |
| **High-volume sending patterns** (services sending > 100,000 notifications/month) | Contact GOV.UK Notify team directly via `https://www.notifications.service.gov.uk/support` -- they maintain a list of high-volume consumers |
| **Compliance/enforcement notification patterns** (how regulators use Notify for enforcement) | Search: `https://github.com/search?q=org%3Aalphagov+enforcement+notify&type=code` and check CMA, Ofcom, Ofgem GitHub organisations |
| **Queue architecture patterns for Notify consumers** | WebSearch: `site:github.com alphagov celery notify queue` or `site:github.com dwp sqs notify` |

### Index Limitations

The govreposcrape index is **heavily biased toward local council repositories** and does not appear to include the most important central government GitHub organisations (alphagov alone has approximately 2,000 public repositories). This means any search for central government platform patterns (GOV.UK Notify, GOV.UK One Login, GOV.UK Pay, GOV.UK Design System core) will return zero directly relevant results from govreposcrape. All high-relevance results in this report were found through direct GitHub WebFetch of known central government repositories, not through the govreposcrape search index.

Users should be aware that a "no results" finding from govreposcrape does **not** mean no government team has built the capability being searched for -- it means the index does not cover the relevant organisations.

---

## GOV.UK Notify Platform Reference

### Rate Limits (as of 2026-03)

| Limit Type | Value | Scope |
|------------|-------|-------|
| Per-minute request limit | 3,000 messages per 60-second rolling window | Per API key type |
| Daily email limit (live) | 250,000 | Per service |
| Daily SMS limit (live) | 250,000 | Per service |
| Daily letter limit (live) | 20,000 | Per service |
| Trial mode limit | 50 messages combined | Team and guest list key |
| Phone network constraint | 20 identical messages or 100 total per hour | Per recipient number |
| International SMS default | 100 per day | Per service (increase available on request) |
| Email message size limit | 2,000,000 bytes | Per message |
| File attachment limit | 2MB | Per attachment |
| File retention default | 26 weeks | Configurable 1-78 weeks |

### API Key Types

| Key Type | Purpose | Delivery | Counts Against Limit |
|----------|---------|----------|---------------------|
| Test | Performance and integration testing | Simulated (no real send) | No |
| Team and Guest List | Trial mode for team + 5 others | Real messages | Yes |
| Live | Production sending to any recipient | Real messages | Yes |

### Delivery Status Values

| Status | Channel | Meaning |
|--------|---------|---------|
| `created` | All | Notification placed in queue |
| `sending` | All | Notification sent to provider |
| `delivered` | Email, SMS | Successfully delivered to recipient |
| `permanent-failure` | Email, SMS | Address/number does not exist |
| `temporary-failure` | Email, SMS | Inbox full, phone off -- will retry |
| `technical-failure` | All | Notify or provider system error |
| `accepted` | Letter | Letter accepted for printing |
| `received` | Letter | Letter delivered by Royal Mail |
| `cancelled` | Letter | Letter cancelled before printing |
| `pending` | SMS | Provider has accepted but not yet confirmed delivery |
| `sent` | SMS | Message sent to international number (no delivery receipt available) |
| `pending-virus-check` | Precompiled Letter | Attachment awaiting virus scan |
| `virus-scan-failed` | Precompiled Letter | Attachment failed virus scan |
| `validation-failed` | Precompiled Letter | Attachment failed format validation |

### Callback Retry Policy

Failed callback deliveries are retried every 5 minutes, up to a maximum of 5 attempts. Callbacks include: notification ID, status, recipient, timestamps, template ID, and template version.

### Smoke Testing Addresses

| Channel | Test Value | Simulated Result |
|---------|-----------|-----------------|
| SMS | 07700900000 | delivered |
| SMS | 07700900111 | permanent-failure |
| SMS | 07700900222 | temporary-failure |
| Email | simulate-delivered@notifications.service.gov.uk | delivered |
| Email | simulate-delivered-2@notifications.service.gov.uk | delivered |
| Email | simulate-delivered-3@notifications.service.gov.uk | delivered |

### Performance Commitments

- 95% of emails and text messages sent within 10 seconds
- Letters printed and posted by 3pm the next working day

### Pricing

- Email: Free (unlimited)
- SMS: Thousands of free messages included (volume-based beyond free tier)
- Letters: Tiered postage options (first class, second class, economy for international)

---

## Recommendations

### Immediate Next Steps

1. **Clone and Review**: [alphagov/email-alert-api](https://github.com/alphagov/email-alert-api) -- Examine the `/docs` directory and `app/models/` for subscriber list management patterns, digest run implementation, and Notify abstraction layer design
2. **Install Client Library**: `pip install notifications-python-client` (or `npm install notifications-node-client`) -- Begin spike integration with a Notify test API key to validate template personalisation for enforcement notice and compliance reminder templates
3. **Capacity Planning**: Engage GOV.UK Notify team to confirm capacity for approximately 50,000 emails/month during onboarding phase (validates assumption A-2); request rate limit increase if needed beyond the standard 3,000 messages/60 seconds
4. **Architecture Spike**: Prototype the notification abstraction layer pattern from email-alert-api, adapted for Fuel Finder's three notification types: (a) compliance reminders (scheduled/event-driven), (b) submission confirmations (transactional), (c) enforcement notices (officer-triggered)
5. **Template Design**: Create GOV.UK Notify templates for the three notification types using the admin UI, with personalisation placeholders for retailer name, forecourt address, submission date, and enforcement action type

### Search Refinements

If further searching is needed, consider these refined queries:

- `GOV.UK Notify rate limit handling exponential backoff resilience patterns` -- Would surface implementations dealing specifically with rate-limit-aware sending at scale
- `government service compliance monitoring scheduled task cron automated alerts` -- Would surface services with scheduled compliance reminder patterns similar to Fuel Finder's needs
- `Celery SQS notification worker queue dead letter retry government service` -- Would surface queue architecture patterns for notification processing

### Related ArcKit Commands

- Run `/arckit:gov-reuse` for a full reusability assessment of the shortlisted repositories (particularly email-alert-api and notifications-python-client)
- Run `/arckit:research` for a deeper technology research report on notification queue architectures (SQS vs Redis/Celery vs RabbitMQ) for the Fuel Finder notification service

---

## External References

| Document | Type | Source | Key Extractions | Path |
|----------|------|--------|-----------------|------|
| GOV.UK Notify Python Documentation | API Reference | GDS | Rate limits, personalisation patterns, error handling, bulk sending guidance, smoke testing addresses | https://docs.notifications.service.gov.uk/python.html |
| GOV.UK Notify REST API Documentation | API Reference | GDS | Endpoint specifications, JWT authentication, callback format, status values, daily limits | https://docs.notifications.service.gov.uk/rest-api.html |
| GOV.UK Notify Features | Platform Overview | GDS | Channel support, performance commitments (95% within 10 seconds), pricing model | https://www.notifications.service.gov.uk/features |
| ARC-001-REQ-v2.0 | Requirements | Project 001 | INT-003 (Notify integration), FR-009 (retailer notifications), NFR-A-3 (circuit breaker for Notify), A-2 (50K emails/month capacity) | projects/001-uk-fuel-price-transparency-service/ARC-001-REQ-v2.0.md |

---

**Generated by**: ArcKit `/arckit.gov-code-search` agent
**Generated on**: 2026-03-24
**ArcKit Version**: 4.5.1
**Project**: UK Fuel Price Transparency Service (Project 001)
**AI Model**: Claude Opus 4.6 (1M context)
