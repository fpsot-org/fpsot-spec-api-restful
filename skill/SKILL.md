---
name: fpsot-api-restful
description: Common rules for FPSOT REST APIs. Use when designing, describing, building, reviewing or calling an HTTP API defined by an FPSOT specification, or when publishing its events.
---

# FPSOT RESTful API

Summary of the FPSOT RESTful API specification. It adds no rules of its own.
The spec text in `spec/` wins on any difference. Each line cites its requirement ID.
Each line keeps the strength of its rule: "must" for MUST, "should" for SHOULD, "may" for MAY.
Path, field and event type names follow the FPSOT naming specification. Dates, money, identifiers and bilingual text follow the FPSOT data types specification.

## Methods and status codes

- Each method must keep its RFC 9110 meaning (API-001). `GET`, `HEAD` and `OPTIONS` must not change state. `PUT` and `DELETE` must be idempotent (API-002).
- `PATCH` must take JSON Merge Patch, `application/merge-patch+json`. JSON Patch may also be accepted (API-003).
- The status code must fit the result, from the table; `428` and `429` come from RFC 6585 (API-004). An error must never get a `2xx` (API-005).
- `201 Created` must carry `Location` and should carry the new item (API-006). Long work should answer `202 Accepted`, which must then carry `Location` to an operation resource (API-007).
- Every item must carry a strong `ETag`. A matching `If-None-Match` must get `304` (API-008).
- `PUT`, `PATCH` and `DELETE` on an item must carry `If-Match`: missing gives `428`, stale gives `412` and no change (API-009).

## Resources

- Paths must be `/v<major>/<plural-collection>` and `/v<major>/<collection>/{<resource>Id}`, with path variables named like the referring field (API-010). The last segment must be the opaque identifier, never a row number (API-011).
- A path should not go deeper than one collection under a top-level item; `/v1/parties/{partyId}/addresses` is fine (API-012).
- A path must not end with a slash or a file extension; the server should redirect such a path with `308` (API-013).
- An action should first become a resource; when none fits, `POST /<collection>/{<resource>Id}/<action>` may be used (API-014).
- Bodies must be JSON objects at the top level (API-015). Names and values must follow the naming and data types specs (API-016).
- Items must carry `id`, and should carry `createdAt` and `updatedAt` (API-017). Responses should omit empty fields; clients must treat absent and `null` alike (API-018).
- A capability may serve its API under a deployment base path (`/registry/v1/...`, `/registry/v1/openapi`), given in the description's server URL; an adapter for an outside specification such as GovStack may follow that specification's paths and must name it (API-019).

## Descriptions

- Every API must have a complete OpenAPI 3.1 description, 3.1.2 or a later 3.1 patch (API-020).
- The domain spec must publish it, and it is normative. Servers must conform to it, and CI should test that (API-021).
- A running server must serve it at `/v<major>/openapi` as JSON (API-022). Schemas must use JSON Schema 2020-12, without `nullable` (API-023).
- Each operation must have a unique `operationId` in field-name form, a summary and a description (API-024).
- Each operation must list every status code, with errors as problem details; requests and success responses should have examples (API-025).
- The text should be in English and French (API-026). CI should lint each description (API-027).

## Errors

- Every `4xx` and `5xx` must be `application/problem+json`, whatever `Accept` says (API-030).
- `type` must be a stable absolute HTTPS URI, never `about:blank`. It is an identifier whether or not a page exists yet, and should lead to a page in English and French (API-031).
- The shared types under `https://fpsot.org/problems/` must be used when they fit. Domain specs must define and publish their own (API-032).
- `title` must be fixed per type and language, and `detail` should explain the occurrence. Both must use the response language (API-033). `status` must equal the status code (API-034).
- `instance` should identify the occurrence, and the server should log the same identifier (API-035).
- Validation faults must go in `errors[]`, each with `detail` and `pointer` or `parameter` (API-036).
- A problem must not reveal stack traces, queries, internal host names, secrets or other people's data (API-037).

## Pages, filters and sorting

- A collection must return a page. Clients may ask for `pageSize`; above the stated maximum it must get `400` (API-040).
- Pages must use an opaque cursor, never an offset or page number. A bad cursor must get `400` with `invalid-cursor` (API-041).
- A page must have `items`, and `next` (absolute URL) when a next page exists. It should also send `Link: rel="next"` (API-042).
- A page should not include a total count unless the client asks (API-043).
- Filters must be `<field>=value`. Ranges must use `<field>From` (inclusive) and `<field>To` (exclusive), suffixes the naming spec allows (API-044).
- An unknown or wrong parameter must get `400` (API-045).
- Free-text search should use `search` (API-046). Clients may sort with `sortBy` and `sortOrder=ascending|descending`, `ascending` by default (API-047).
- Every collection must have a stated default order that ends with `id` (API-048).
- A search or filter on personal information must use `POST /v<major>/<collection>/searches` with the criteria in a JSON body. It must return the same page format, and its cursor must not hold the criteria (API-049).

## Versions

- The major version must be in the path only, never in a header, a parameter or a media type (API-050). A change within a major must not break clients (API-051).
- Clients must ignore unknown fields and headers, and should handle unknown enum values (API-052). `info.version` must be SemVer with the same major (API-053).
- A deprecated operation or version must send `Deprecation` and be marked `deprecated`. It should also send `Link` with `rel="deprecation"` (API-054).
- `Sunset` must be sent once the date is known, at least 12 months after the first `Deprecation`. The old major must stay until then, and an operation must only be removed in a new major (API-055).
- After sunset, requests must get `410` with `version-retired`; `detail` should point to the replacement (API-056).

## Retries

- `Idempotency-Key` must be accepted on `POST` and `PATCH`; a `POST` that creates an item should require it (API-060).
- Clients must send a new key per request, and the same key on retry (API-061).
- Servers must keep keys at least 24 hours: replay gets the stored response, a different body `422`, in progress `409`, missing `400` (API-062).
- Clients should back off with jitter, and must respect `Retry-After` (API-063).

## Formats and languages

- APIs must use JSON in UTF-8 (API-070). Unsupported formats must get `406` or `415` (API-071).
- By default, bilingual fields must return every language as a language map. Where a jurisdiction rule requires it, a server may return only the `Accept-Language` languages, and must then send `Content-Language` and `Vary: Accept-Language` (API-072).
- Server-written text must take its language from the person's profile, then `Accept-Language`, then the deployment default. English and French must be supported (API-073).
- Responses with server-written text must send `Content-Language`, and `Vary: Accept-Language` when the language depends on the request (API-074).

## Security

- Content and requests must use HTTPS only, with TLS 1.2 or 1.3; TLS 1.3 should be offered. Plain HTTP must never serve content or accept requests (API-080).
- A server should not answer plain HTTP at all. Where a binding rule requires it, it may answer with a `301` or `308` redirect to HTTPS, which must carry no content (API-080).
- Every response must send HSTS for at least one year, with `includeSubDomains` (API-081).
- Every response must send `nosniff`; non-public data must send `no-store`; other responses should send an explicit `Cache-Control` (API-082). Servers must not send software or version headers (API-083).
- CORS headers must be sent only when needed, with a fixed origin list, never echoing `Origin`, never `*` with credentials. Open data without credentials may allow `*` (API-084).
- URLs must not carry secrets, tokens or personal data (API-085). Servers must validate input, limit body size with `413`, and ignore or refuse read-only fields (API-086).
- An API that must know its caller must accept OAuth 2.0 bearer tokens (RFC 6750) per RFC 9700, and should use OpenID Connect for people. It must check issuer, audience, expiry and signature (API-090).
- Servers must not accept credentials in query parameters, and an API key alone must not open non-public data (API-091).
- Servers must check access to every item and every field (API-092). They should answer `404` rather than `403` when existence is private (API-093).
- Every API must limit request rates, with `429` and `Retry-After`, and the description must state the limits (API-094).
- Servers should send the `RateLimit` and `RateLimit-Policy` headers of the latest RateLimit Internet-Draft, which can still change (API-095).
- Organizations must keep an inventory of hosts and versions with their descriptions, and must remove versions after sunset (API-096).

## Events

- Events must use CloudEvents 1.0.2, JSON format, structured mode over HTTP (API-100).
- Events must carry `specversion`, `id`, `source`, `type`, `time` and `datacontenttype`, and should carry `subject` and `dataschema` (API-101).
- `data` must follow the resource field rules and hold no secrets. It should hold the state after the change and only the personal data consumers need (API-102).
- Domain specs must list event types with schemas, and a breaking change must use a new type (API-103).
- Consumers must accept duplicates, treat the same `source` and `id` as one event, and ignore unknown attributes (API-104).
