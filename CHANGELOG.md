# Changelog

All notable changes to this specification are listed here.
The format follows [Keep a Changelog 1.1.0](https://keepachangelog.com/en/1.1.0/),
and versions follow [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.2.0] - 2026-11-07

### Added

- API-019: a capability may serve its API under a base path that a deployment sets, so several capabilities can run in one application. An adapter that implements an outside specification, such as GovStack, may follow that specification's paths.
- API-020: a new description should use OpenAPI 3.2 (3.2.1 or later). OpenAPI 3.1 stays allowed while common generators, such as Quarkus's, still write it.

### Fixed

- API-090 now links "OAuth 2.0 bearer tokens" to RFC 6750, and RFC 6750 joins the references. The skill names RFC 6750 too.
- The French security page links the French page of the federal configuration requirements for web sites, with an archived copy.
- Each RFC archived copy is now a snapshot of the `/info/` page that the text links, instead of the `/rfc/` page.

## [0.1.1] - 2026-11-04

### Changed

- Each RFC and other outside standard named in the text now links to its source.
- Each page that cites outside sources has a References section, with archived copies where one exists.
- English text uses US spelling, such as "license" and "misspelled".
- The repository turns on the references and US spelling checks.

## [0.1.0] - 2026-11-04

### Added

- Methods and status codes, API-001 to API-009: RFC 9110 methods, JSON Merge Patch, a fixed list of status codes, `ETag` and required `If-Match`.
- Resources, API-010 to API-018: plural kebab-case paths under `/v<major>/`, opaque identifiers, JSON object bodies, field rules from the naming and data types specifications.
- Descriptions, API-020 to API-027: a complete, published OpenAPI 3.1 description with JSON Schema 2020-12, served at `/v<major>/openapi`.
- Errors, API-030 to API-037: problem details (RFC 9457) with stable `type` URIs, a shared set of types, translated titles and field-level `errors`.
- Pages, filters and sorting, API-040 to API-049: opaque cursors, a `next` member and `Link` header, field filters, `sortBy` and `sortOrder`, and `POST` searches for personal information.
- Versions, API-050 to API-056: major version in the path, no breaking change within a major, `Deprecation` and `Sunset` headers, 12 months of notice.
- Retries, API-060 to API-063: the `Idempotency-Key` header and client back-off.
- Formats and languages, API-070 to API-074: JSON in UTF-8, full bilingual fields by default, a fixed order to choose the language of server-written text.
- Security, API-080 to API-096: no content over plain HTTP, HSTS, security headers, CORS, OAuth 2.0 and OpenID Connect, object-level access checks, rate limits, inventory.
- Events, API-100 to API-104: CloudEvents 1.0.2 in JSON, required attributes, duplicate-safe consumers.
- Comparison data for the international baseline, Canada and Québec.
- A how-to guide, the agent skill, `llms.txt` and the book in both languages.

[Unreleased]: https://github.com/fpsot-org/fpsot-spec-api-restful/compare/v0.1.1...HEAD
[0.1.1]: https://github.com/fpsot-org/fpsot-spec-api-restful/compare/v0.1.0...v0.1.1
[0.1.0]: https://github.com/fpsot-org/fpsot-spec-api-restful/releases/tag/v0.1.0
