# Hungarian localization notes

This repository contains a Hungarian localization that keeps the original professional English terminology visible.

## Structure

- `README.md` remains the original generated English dictionary.
- `README.hu.md` is the generated Hungarian edition.
- `dictionary/` remains the original English source.
- `dictionary-hu/` contains the Hungarian localized entries using the same file names as the English source.
- `internal/Curriculum.hu.md` defines the Hungarian README structure.
- `internal/README.template.hu.md` contains the Hungarian README intro.
- `internal/generate-readme.hu.js` generates `README.hu.md`.

## Style rule

The localization translates explanations into Hungarian, but keeps load-bearing AI/coding terms in English:

- model
- agent
- prompt
- system prompt
- context
- context window
- token
- inference
- training
- tool
- tool call
- tool result
- sandbox
- harness
- cache tokens
- prefix cache
- stateless
- stateful
- handoff

The goal is not literal translation. The goal is Hungarian comprehension without erasing the terminology developers will meet in docs, issues, PRs, tools, and team communication.
