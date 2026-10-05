> **Portfolio showcase** — the complete implementation is private. This public repository intentionally contains documentation only. A live demo or controlled private review is available for serious project discussions.

# Frankie CRM

Frankie is a production-grade CRM and operations platform built by heavily extending the open-source Twenty CRM foundation for a real ecommerce and service workflow.

This public repository is a **sanitized portfolio edition**. Customer identities, production records, credentials, private infrastructure details, proprietary catalog data and commercially sensitive rules are not published. The included source files are representative, anonymized modules from the larger system.

## What Frankie covers

### CRM and customer operations
- customer and contact records
- sales ownership and assignment
- related orders, offers, documents, tasks and service cases
- searchable operational views and custom record widgets
- internal notes, attachments and activity history

### Sales and quotation workflow
- multi-step quotation builder
- configurable product alternatives per step
- optional components and grouped component variants
- per-offer manual naming and pricing without modifying the master catalog
- technical specification blocks
- customer-specific offer layouts
- automatic calculations and validation
- offer-to-order conversion
- generated sales documents and customer-facing output

### Orders and ecommerce synchronization
- inbound and outbound order synchronization
- product synchronization
- status mapping between systems
- marketplace-originated order handling
- retry-safe update flows
- duplicate and replay protection
- reconciliation after partial failures

### Accounting and document automation
- invoice and receipt workflows
- sales and purchase document synchronization
- PDF/document attachment handling
- document matching to CRM orders
- safeguards against duplicate document creation
- durable operation markers for non-reversible actions
- recovery logic after timeouts or interrupted writes

### Products, suppliers and purchasing
- product catalog extensions
- supplier relationships
- purchase-order workflows
- purchasing data and cost handling
- inventory-related synchronization
- product pricing synchronization
- supplier-oriented operational views

### Demand and purchasing forecast
- historical purchase analysis
- consumption-rate calculations
- seasonal adjustment
- product grouping
- purchase reconciliation
- purchasing recommendations based on operational history

### Service, complaints and field workflows
- service-case handling
- warranty and complaint workflows
- field-service integration
- service photos and documents
- validation of dates and operational states

### Communication
- internal company chat
- mentions and notification rules
- synchronized email workflow
- customer-linked communication
- task and notification counters
- operational alerts

### Integration health and observability
- health state for background integrations
- stale-run detection
- consecutive-failure tracking
- recovery events
- health dashboards inside the CRM
- email alerts after configurable failure thresholds
- disk/worker monitoring
- reconciliation reports
- protection against the dangerous case where "no alert" is mistaken for "everything works"

## Reliability patterns used in the project

### Idempotency and duplicate prevention
External APIs can accept an operation and still time out before returning a response. Frankie does not blindly retry irreversible actions. Critical flows use durable markers, source-side identifiers, lookup-before-create strategies and reconciliation.

### Failure isolation
Background bridges are designed so a temporary failure in one external system does not silently corrupt another workflow.

### Observable background jobs
A running container is not automatically treated as a healthy integration. Workers persist success/failure timestamps and surface them in a dedicated system-health view.

### Business rules as testable code
Pricing, tax, document, product-selection and order rules are implemented as explicit domain functions with regression tests rather than only as UI conditions.

## Architecture

Typical flow:

```text
React / TypeScript CRM UI
          |
          v
Twenty CRM / GraphQL
          |
          +---- sales & quotation logic
          +---- documents / orders / service
          +---- internal communication
          |
          v
Node.js integration workers
          |
          +---- ecommerce / marketplace APIs
          +---- accounting systems
          +---- supplier / service integrations
          +---- monitoring and reconciliation
```

The production environment uses containerized workers and explicit health/recovery mechanisms.

## Technology

- React
- TypeScript
- Twenty CRM
- GraphQL
- Node.js
- Docker / Compose
- external REST APIs
- automated unit and regression tests
- background integration workers

## Related project

The **Bacteria Run** gamification module originally lived inside the larger Frankie application. Its game engine and public-safe assets are published separately as the `bacteria-run` portfolio repository.

## Portfolio note

Frankie is shown here to demonstrate the scale of the delivered system, architecture decisions and production automation patterns without exposing customer data or proprietary production material.

## Source access

The complete implementation is kept in a private source archive. For serious commercial discussions, a live walkthrough, architecture review, or controlled private code review can be arranged.

## Usage and licensing

This repository is source-available for portfolio evaluation. You may inspect the code and run an unmodified local copy for evaluation, but commercial use, redistribution, republishing and derivative distribution are not permitted without written permission. See [PROPRIETARY-NOTICE.md](PROPRIETARY-NOTICE.md).
