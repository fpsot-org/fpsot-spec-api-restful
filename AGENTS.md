# Instructions for agents

This repository holds the FPSOT RESTful API specification: the common rules for every HTTP API that an FPSOT specification defines.

- The normative text is in `spec/en/` and `spec/fr/`. Every rule has an ID such as `API-001`.
- Follow `skill/SKILL.md` when you design, describe, build or call an FPSOT API. The spec text wins on any difference.
- Path, field and event type names follow the FPSOT naming specification. Value formats follow the FPSOT data types specification. Do not restate their rules here.
- Every page exists in English and in French, with the same file name and the same IDs.
- Terms and abbreviations come from the term base of `fpsot-spec-writing`. Add a missing term there first.
- Do not copy text from outside standards. Summarize them in your own words and cite the exact version.
- Commits follow Conventional Commits and are signed. Pull requests are squash-merged.
