# Terms needed in the writing term base

These abbreviations are used by this specification and are missing from `fpsot-spec-writing/termbase/terms.yaml`.
The entries below use the format of that file.
Definitions are FPSOT wording.

French forms were checked in the Grand dictionnaire terminologique (GDT) on 2026-11-03.
TERMIUM Plus refused automated reading on that date, so no TERMIUM record could be checked.

Seven entries have no GDT record: `json`, `rest`, `cors`, `hsts`, `owasp`, `uuid` and `utf-8`.
For them, the French short form and full form keep the English name, as for `csl` and `fpsot`.
No French full form was invented.
A person must confirm these seven in TERMIUM Plus before the release, and replace the source if a record exists.

```yaml
  - id: http
    kind: abbreviation
    en: {short: "HTTP", full: "Hypertext Transfer Protocol", definition: "The protocol that web clients and servers use to send requests and responses."}
    fr: {short: "HTTP", full: "protocole HTTP (Hypertext Transfer Protocol)", definition: "Protocole qu'emploient les clients et les serveurs Web pour échanger des requêtes et des réponses."}
    source: {name: "Grand dictionnaire terminologique", url: "https://vitrinelinguistique.oqlf.gouv.qc.ca/fiche-gdt/fiche/2075739/protocole-http", checked: "2026-11-03"}
  - id: https
    kind: abbreviation
    en: {short: "HTTPS", full: "Hypertext Transfer Protocol Secure", definition: "HTTP sent over an encrypted connection, so that others cannot read or change the exchange."}
    fr: {short: "HTTPS", full: "protocole HTTPS (Hypertext Transfer Protocol Secure)", definition: "Protocole HTTP transmis par une connexion chiffrée, pour que des tiers ne puissent ni lire ni modifier l'échange."}
    source: {name: "Grand dictionnaire terminologique", url: "https://vitrinelinguistique.oqlf.gouv.qc.ca/fiche-gdt/fiche/26558496/protocole-https", checked: "2026-11-03"}
  - id: tls
    kind: abbreviation
    en: {short: "TLS", full: "Transport Layer Security", definition: "The protocol that encrypts a network connection and proves the identity of the server."}
    fr: {short: "TLS", full: "protocole TLS (Transport Layer Security)", definition: "Protocole qui chiffre une connexion réseau et prouve l'identité du serveur."}
    source: {name: "Grand dictionnaire terminologique", url: "https://vitrinelinguistique.oqlf.gouv.qc.ca/fiche-gdt/fiche/26558099/protocole-tls", checked: "2026-11-03"}
  - id: uri
    kind: abbreviation
    en: {short: "URI", full: "uniform resource identifier", definition: "A standard text string that names a resource, by its location or by a lasting name."}
    fr: {short: "URI", full: "adresse URI (uniform resource identifier)", definition: "Chaîne de caractères normalisée qui désigne une ressource, par son emplacement ou par un nom durable."}
    source: {name: "Grand dictionnaire terminologique", url: "https://vitrinelinguistique.oqlf.gouv.qc.ca/fiche-gdt/fiche/26520166/adresse-uri", checked: "2026-11-03"}
  - id: ietf
    kind: abbreviation
    en: {short: "IETF", full: "Internet Engineering Task Force", definition: "The open body that develops and publishes the technical standards of the Internet."}
    fr: {short: "IETF", full: "groupe de travail IETF (Internet Engineering Task Force)", definition: "Organisme ouvert qui élabore et publie les normes techniques d'Internet."}
    source: {name: "Grand dictionnaire terminologique", url: "https://vitrinelinguistique.oqlf.gouv.qc.ca/fiche-gdt/fiche/8874737/groupe-de-travail-ietf", checked: "2026-11-03"}
  - id: json
    kind: abbreviation
    en: {short: "JSON", full: "JavaScript Object Notation", definition: "A text format for structured data, made of objects, arrays, strings, numbers and Boolean values."}
    fr: {short: "JSON", full: "JavaScript Object Notation", definition: "Format texte de données structurées, fait d'objets, de tableaux, de chaînes, de nombres et de valeurs booléennes."}
    source: {name: "RFC 8259 (no GDT record found; TERMIUM Plus not checked)", url: "https://www.rfc-editor.org/rfc/rfc8259", checked: "2026-11-03"}
  - id: rest
    kind: abbreviation
    en: {short: "REST", full: "Representational State Transfer", definition: "An architectural style for web services, where clients act on resources through the standard HTTP methods."}
    fr: {short: "REST", full: "Representational State Transfer", definition: "Style d'architecture de services Web où les clients agissent sur des ressources au moyen des méthodes HTTP normalisées."}
    source: {name: "Fielding, Architectural Styles and the Design of Network-based Software Architectures, chapter 5 (no GDT record found; TERMIUM Plus not checked)", url: "https://ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm", checked: "2026-11-03"}
  - id: cors
    kind: abbreviation
    en: {short: "CORS", full: "cross-origin resource sharing", definition: "The browser mechanism that lets a server allow web pages from other origins to read its responses."}
    fr: {short: "CORS", full: "cross-origin resource sharing", definition: "Mécanisme des navigateurs qui permet à un serveur d'autoriser des pages Web d'autres origines à lire ses réponses."}
    source: {name: "WHATWG Fetch Standard (no GDT record found; TERMIUM Plus not checked)", url: "https://fetch.spec.whatwg.org/#http-cors-protocol", checked: "2026-11-03"}
  - id: hsts
    kind: abbreviation
    en: {short: "HSTS", full: "HTTP Strict Transport Security", definition: "A response header that tells browsers to reach a host only over HTTPS for a set time."}
    fr: {short: "HSTS", full: "HTTP Strict Transport Security", definition: "En-tête de réponse qui demande aux navigateurs de n'accéder à un hôte qu'en HTTPS pendant une durée fixée."}
    source: {name: "RFC 6797 (no GDT record found; TERMIUM Plus not checked)", url: "https://www.rfc-editor.org/rfc/rfc6797", checked: "2026-11-03"}
  - id: owasp
    kind: abbreviation
    en: {short: "OWASP", full: "Open Worldwide Application Security Project", definition: "An open foundation that publishes guides and lists of risks for the security of software."}
    fr: {short: "OWASP", full: "Open Worldwide Application Security Project", definition: "Fondation ouverte qui publie des guides et des listes de risques sur la sécurité des logiciels."}
    source: {name: "OWASP Foundation (no GDT record found; TERMIUM Plus not checked)", url: "https://owasp.org/", checked: "2026-11-03"}
  - id: uuid
    kind: abbreviation
    en: {short: "UUID", full: "universally unique identifier", definition: "A 128-bit identifier that systems create on their own, with no central registry, and that does not repeat."}
    fr: {short: "UUID", full: "universally unique identifier", definition: "Identifiant de 128 bits que les systèmes créent eux-mêmes, sans registre central, et qui ne se répète pas."}
    source: {name: "RFC 9562 (no GDT record found; TERMIUM Plus not checked)", url: "https://www.rfc-editor.org/rfc/rfc9562", checked: "2026-11-03"}
  - id: utf-8
    kind: abbreviation
    en: {short: "UTF-8", full: "Unicode Transformation Format, 8-bit", definition: "The encoding that writes every Unicode character as one to four bytes, and the usual encoding of the web."}
    fr: {short: "UTF-8", full: "Unicode Transformation Format, 8-bit", definition: "Codage qui écrit chaque caractère Unicode sur un à quatre octets, et le codage habituel du Web."}
    source: {name: "RFC 3629 (no GDT record found; TERMIUM Plus not checked)", url: "https://www.rfc-editor.org/rfc/rfc3629", checked: "2026-11-03"}
```
