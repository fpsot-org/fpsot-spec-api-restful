---
name: fpsot-api-restful
description: Common rules for FPSOT REST APIs. Use when designing, describing, building, reviewing or calling an HTTP API defined by an FPSOT specification, or when publishing its events.
---

# FPSOT RESTful API

Summary of the FPSOT RESTful API specification. It adds no rules of its own.
The spec text in `spec/` wins on any difference. Each line cites its requirement ID.
Path, field and event type names follow the FPSOT naming specification. Dates, money, identifiers and bilingual text follow the FPSOT data types specification.

## Methods and status codes

- Use each method with its RFC 9110 meaning (API-001). `GET`, `HEAD`, `OPTIONS` change nothing. `PUT` and `DELETE` are idempotent (API-002).
- `PATCH` takes JSON Merge Patch, `application/merge-patch+json` (API-003).
- Use the status codes of the table (API-004). Never answer an error with `2xx` (API-005).
- `201 Created` carries `Location` and should carry the new item (API-006). Long work answers `202 Accepted` with `Location` to an operation resource (API-007).
- Every item has a strong `ETag`. `If-None-Match` gives `304` (API-008).
- `PUT`, `PATCH` and `DELETE` on an item need `If-Match`: missing gives `428`, stale gives `412` (API-009).

## Resources

- Paths: `/v1/<plural-collection>` and `/v1/<collection>/{<resource>Id}`, path variables named like the referring field (API-010). The id is the opaque identifier, never a row number (API-011).
- At most one collection under an item (API-012). No trailing slash, no file extension (API-013).
- Model an action as a resource first; else `POST /<collection>/{<resource>Id}/<action>` (API-014).
- Bodies are JSON objects at the top level (API-015). Names and values follow the naming and data types specs (API-016).
- Items carry `id`, and should carry `createdAt` and `updatedAt` (API-017). Omit empty fields; treat absent and `null` alike (API-018).

## Descriptions

- Every API has a complete OpenAPI 3.1 description (API-020). The domain spec publishes it and it is normative (API-021).
- Serve it at `/v<major>/openapi` (API-022). Schemas use JSON Schema 2020-12, no `nullable` (API-023).
- Each operation has `operationId`, summary and description (API-024), and lists every status code, errors as problem details (API-025).
- Give the text in English and French (API-026). Lint descriptions in CI (API-027).

## Errors

- Every `4xx` and `5xx` is `application/problem+json` (API-030).
- `type` is a stable absolute HTTPS URI, never `about:blank` (API-031). Use the shared types under `https://fpsot.org/problems/` when they fit (API-032).
- `title` is fixed per type and language; `title` and `detail` follow the negotiated language (API-033). `status` equals the status code (API-034).
- `instance` identifies the occurrence, also logged (API-035).
- Validation faults go in `errors[]` with `detail` and `pointer` or `parameter` (API-036).
- No stack traces, internal names, secrets or other people's data (API-037).

## Pages, filters and sorting

- Collections always return a page; `pageSize` up to a stated maximum, else `400` (API-040).
- Opaque cursor, never offset or page number; bad cursor gives `invalid-cursor` (API-041).
- Page body: `items` and `next` (absolute URL); also `Link: rel="next"` (API-042). No total count unless asked (API-043).
- Filters: `<field>=value`, ranges `<field>From` (inclusive) and `<field>To` (exclusive) (API-044). Unknown parameter gives `400` (API-045).
- Free text: `search` (API-046). Sorting: `sortBy` and `sortOrder=asc|desc` (API-047). Every order ends with `id` (API-048).

## Versions

- Major version in the path only (API-050). No breaking change within a major (API-051).
- Clients ignore unknown fields and handle unknown enum values (API-052). `info.version` is SemVer, same major (API-053).
- Deprecated: send `Deprecation` and mark `deprecated` (API-054). `Sunset` at least 12 months later, old major kept until then (API-055).
- After sunset: `410` with `version-retired` (API-056).

## Retries

- Accept `Idempotency-Key` on `POST` and `PATCH` (API-060). Clients send a new key per request, the same key on retry (API-061).
- Keep keys 24 hours at least: replay gives the stored response, different body `422`, in progress `409`, missing `400` (API-062).
- Clients back off with jitter and respect `Retry-After` (API-063).

## Formats and languages

- JSON in UTF-8 (API-070). `406` and `415` for unsupported formats (API-071).
- Bilingual fields always return every language as a language map (API-072).
- Server-written text follows `Accept-Language`; English and French are required (API-073). Send `Content-Language` and `Vary: Accept-Language` (API-074).

## Security

- HTTPS only, TLS 1.2 or 1.3, no plain HTTP, not even a redirect (API-080). HSTS one year with `includeSubDomains` (API-081).
- `nosniff`, `no-store` on non-public data (API-082). No server version headers (API-083).
- CORS only when needed, fixed origin list, never `*` with credentials (API-084).
- No secrets or personal data in URLs (API-085). Validate input, limit body size, refuse read-only fields (API-086).
- OAuth 2.0 bearer tokens per RFC 9700, OpenID Connect for people; check every token (API-090). No credentials in query parameters (API-091).
- Check access to every item and every field (API-092). Prefer `404` to `403` when existence is private (API-093).
- Rate limit with `429` and `Retry-After` (API-094); send `RateLimit` and `RateLimit-Policy` (API-095).
- Keep an inventory of hosts and versions; remove sunset versions (API-096).

## Events

- CloudEvents 1.0.2, JSON format, structured mode over HTTP (API-100).
- Required: `specversion`, `id`, `source`, `type`, `time`, `datacontenttype`; should add `subject` and `dataschema` (API-101).
- `data` follows the resource field rules, no secrets, minimal personal data (API-102).
- Domain specs list event types with schemas; a breaking change needs a new type (API-103).
- Consumers deduplicate on `source` and `id`, and ignore unknown attributes (API-104).
