# Nookal (nookal)

Nookal is Australian-built practice management software for allied health clinics - physiotherapy, chiropractic, podiatry, psychology, and similar disciplines - covering online bookings, multi-practitioner scheduling, patient and case records, treatment notes, invoicing, bulk billing, and clinic reporting. Nookal exposes a documented REST API that lets integrators read and write patients, cases, appointments, class bookings, availabilities, practitioners, locations, treatment notes, files, and invoices.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/nookal/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/nookal/refs/heads/main/apis.yml)

## Access Model (Read First)

- **Base URL:** `https://api.nookal.com/production/v2/` (confirmed live 2026-07-12).
- **Authentication:** account-issued **API key**, passed as the `api_key` parameter - in the query string for GET requests and as a form field for POST requests. The key is created inside the Nookal application (Setup / Integrations) with a configurable access level. There is no OAuth flow and no Authorization header; the API key is the sole credential. Confirmed live: calling `/verify` without a key returns `{"status":"failure","details":{"errorCode":"L000_1","alerts":["Missing variable: api_key"]}}`.
- **Plan gating:** API access is available on the paid **Professional** and **Enterprise** plans. It is **not** included in the entry-level Essentials tier. Getting a key is self-serve for an account admin on a qualifying plan.
- **Format:** JSON, using a common envelope `{"status":"success"|"failure","data":{...},"details":{...}}`. Read endpoints paginate via `page`/`page_length` and support a `last_modified` incremental filter; `details` reports `totalItems`, `currentItems`, `currentPage`, and `nextPage`.
- **Transport:** REST over HTTPS only. **No public WebSocket API** is documented (see `review.yml`).

## Real vs Modeled

- **Confirmed live** against the production host (`verify`, `getLocations`, `getPatients`) - base URL and the `api_key` auth requirement were verified by direct probes.
- **Documented** paths, methods, and parameters for the remaining endpoints are taken from Nookal's public API reference at `https://api.nookal.com/dev/reference/*`. Nookal does **not** publish a machine-readable OpenAPI document, so the request/response body **shapes** in `openapi/nookal-openapi.yml` are **modeled** from the documented object reference and the confirmed live envelope. Verify field-level schemas against a live account before production use.

## Tags

- Practice Management
- Healthcare
- Allied Health
- Appointments
- Scheduling
- Patients
- Clinics
- Bookings
- Physiotherapy
- SaaS

## Timestamps

- **Created:** 2026-07-12
- **Modified:** 2026-07-12

## APIs

### Nookal Patients API

Read and write patient records, cases, treatment notes, and patient files - list and search patients, add and edit patients, manage cases, retrieve and add treatment notes, upload and fetch files, and update Medicare / DVA details.

- **Human URL:** [https://api.nookal.com/dev/reference/patient](https://api.nookal.com/dev/reference/patient)
- **Base URL:** `https://api.nookal.com/production/v2`

#### Tags

- Patients
- Cases
- Treatment Notes

#### Properties

- [Documentation](https://api.nookal.com/developers)
- [API Reference](https://api.nookal.com/dev/reference/patient)
- [OpenAPI](openapi/nookal-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/nookal.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/nookal.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Nookal Appointments API

Retrieve appointments and query appointment and class availabilities, then create, update, cancel, and rebook appointment and class bookings. Also read class participants, class and service redemptions, and the waiting list.

- **Human URL:** [https://api.nookal.com/dev/reference/appointment](https://api.nookal.com/dev/reference/appointment)
- **Base URL:** `https://api.nookal.com/production/v2`

#### Tags

- Appointments
- Bookings
- Scheduling

#### Properties

- [Documentation](https://api.nookal.com/developers)
- [API Reference](https://api.nookal.com/dev/reference/appointment)
- [OpenAPI](openapi/nookal-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/nookal.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/nookal.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Nookal Clinic API

Retrieve clinic reference data - locations and logos, practitioners and photos, appointment types, class types, and the stock list - used to resolve the identifiers referenced across the Patients, Appointments, and Invoices APIs.

- **Human URL:** [https://api.nookal.com/dev/reference/location](https://api.nookal.com/dev/reference/location)
- **Base URL:** `https://api.nookal.com/production/v2`

#### Tags

- Locations
- Practitioners
- Reference Data

#### Properties

- [Documentation](https://api.nookal.com/developers)
- [API Reference](https://api.nookal.com/dev/reference/location)
- [OpenAPI](openapi/nookal-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/nookal.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/nookal.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Nookal Invoices API

Create and read invoices and their line items, payments, credits, discounts, refunds, and adjustments. Add and delete invoice items and payments, add account credit, and retrieve financial breakdowns for billing and reconciliation.

- **Human URL:** [https://api.nookal.com/dev/reference/invoices](https://api.nookal.com/dev/reference/invoices)
- **Base URL:** `https://api.nookal.com/production/v2`

#### Tags

- Invoices
- Payments
- Billing

#### Properties

- [Documentation](https://api.nookal.com/developers)
- [API Reference](https://api.nookal.com/dev/reference/invoices)
- [OpenAPI](openapi/nookal-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/nookal.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/nookal.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Nookal Verification API

Verify that an API key is valid and connected to a Nookal account before making further calls. Confirmed live at `/verify`, which returns a JSON status envelope and reports a missing or invalid `api_key`.

- **Human URL:** [https://api.nookal.com/dev/reference/verify](https://api.nookal.com/dev/reference/verify)
- **Base URL:** `https://api.nookal.com/production/v2`

#### Tags

- Verification
- Authentication
- API Key

#### Properties

- [Documentation](https://api.nookal.com/developers)
- [API Reference](https://api.nookal.com/dev/reference/verify)
- [OpenAPI](openapi/nookal-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/nookal.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/nookal.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [Domain Security](security/nookal-domain-security.yml)
- [Authentication](authentication/nookal-authentication.yml)
- [Website](https://www.nookal.com)
- [Documentation](https://api.nookal.com/developers)
- [Sign Up](https://www.nookal.com/signup)
- [Plans](plans/nookal-plans-pricing.yml)
- [Pricing](https://www.nookal.com/pricing)
- [Rate Limits](rate-limits/nookal-rate-limits.yml)
- [Fin Ops](finops/nookal-finops.yml)
- [LinkedIn](https://www.linkedin.com/company/nookal)
- [Support](https://support.nookal.com)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
