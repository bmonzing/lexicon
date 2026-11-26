# Lexicon

A shared vocabulary for AI-assisted coding and software product development, intended for people and AI agents working across projects.

## Glossaries

- [Deterministic Decisions in AI Systems](glossaries/deterministic-ai.md) — deterministic and probabilistic computation, AI architecture, data governance, drift, and reliability. Plain text for agents and API calls: `https://raw.githubusercontent.com/bmonzing/lexicon/main/glossaries/deterministic-ai.md`

## Using the lexicon

Reference this repository from your project documentation or agent instructions. Point agents at the plain-text links above; the github.com pages wrap the files in a web interface. Consult the relevant glossary when interpreting terminology. These definitions establish preferred usage, not necessarily universal industry consensus.

For AI agents, see [AGENTS.md](AGENTS.md).

## Adding terms

Add definitions to the relevant glossary. Use a clear term heading, a concise definition, and optional examples, distinctions, or watch-out notes. Include sources where available. Add a new topical glossary only when useful, and link it here.

## Versions

This is an evolving reference, and `main` always holds the latest definitions. Stable versions are marked with release tags (`v1.0`, `v1.1`, …), and the `version` field at the top of each glossary matches the latest tag that changed it.

When a project needs definitions that won't change under it, link to a tag instead of `main`:

`https://raw.githubusercontent.com/bmonzing/lexicon/v1.0/glossaries/deterministic-ai.md`

When releasing, bump the `version` and `date` fields of each changed glossary, merge, then tag the merge commit. Use a minor version (1.1) for added terms or clarifications, and a major version (2.0) when an existing definition changes meaning.

## License

The lexicon's content is licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE). You may share and adapt it, including commercially, with credit to this repository.
