# Vault Schema

Personal knowledge management vault organized as a Zettelkasten/PARA hybrid.
Process: capture → refine → link, with the LLM handling maintenance.

## Structure

| Folder | Contents | Role |
|---|---|---|
| `1- Rough-notes/` | Core-dump, Ideas, Prompts, GPT answers | **Inbox** — fleeting notes to be processed by LLM |
| `2- Source-material/` | Books, YouTube, Blog, Clippings, Projects | **Source documents** — immutable references |
| `3- Tags/` | 37 single-concept files (e.g. `LLM.md`, `Startups.md`) | **Reference system** — each page documents a topic that atomic notes relate to via `[[wikilinks]]` in the body |
| `4- Indexes/` | 5 MOC notes (AI, Marketing, Business, Electronics, Web apps) | **Entry points** — topical tables of content |
| `5- Templates/` | Daily note, Full-note, Index, Links | **Templates** — consistent note creation |
| `6- Atomic-notes/` | 85 permanent notes with clean filenames | **Knowledge graph** — the core |

## Tags (Mastery Level)

The `tags` field in YAML frontmatter tracks **proficiency level** with the subject.
Three tiers:

```yaml
---
tags: [noob]    # Learning — just started, rough understanding
tags: [user]    # Comfortable — can use it, know the basics
tags: [root]    # Deep — mastered, can teach or build with it
tags: [noob, user]  # Can combine if topic spans levels
```

The LLM updates this tag when it processes notes — if you clearly understand
something, the tag gets promoted.

## Graph Coloring (Domain)

The `domain` field exists **only** for Obsidian's graph view — it color-codes
nodes so you can see clusters at a glance.

```yaml
---
domain: sales
---
```

Cross-domain notes use an array:
```yaml
---
domain: [AI, business]
---
```

### Domain values

| Domain | Graph color | Applies to |
|---|---|---|
| `sales` | (auto) | Sales, B2B, conversion, customer acquisition |
| `business` | (auto) | Strategy, planning, business models, startups |
| `webapps` | (auto) | Web development, databases, system design |
| `elec` | (auto) | Electronics, voltage, circuits |
| `ai` | (auto) | AI, ML, DL, LLMs, agents |
| `net` | (auto) | Networking, protocols, infrastructure |
| `cpp` | (auto) | C++ programming |
| `general` | (auto) | Cross-domain or uncategorized |

## Atomic Note Structure

Follow the `5- Templates/Full-note.md` template. A well-formed atomic note has:

```markdown
---
title: "Short Title"
domain: <domain>
tags: [noob]           # Mastery: noob / user / root
created: YYYY-MM-DD
updated: YYYY-MM-DD
---
Tags: [[TagName]] [[AnotherTag]]
# Title
## Summary
One paragraph capturing the core idea.
## Key Points
- Bullet explaining one aspect
- Second key point
- Third key point
## Connections
- Related to: [[6- Atomic-notes/Related Note]]
- Builds on: [[6- Atomic-notes/Foundation Note]]
- Leads to: [[6- Atomic-notes/Next Note]]
## References
- [Source Title](https://actual.url)
## Quotes
> Memorable or important excerpt.
```

Required sections: Summary, Key Points, Connections, References.
Remove empty sections instead of leaving placeholders.
The `Tags:` line uses `[[wikilinks]]` to `3- Tags/` for topic association.

> **Note:** Notes use clean filenames with `domain:` frontmatter for graph coloring.
> The `domain:` field replaces the old `Prefix__` naming convention.

## Operations

### Ingest
New source arrives in `2- Source-material/`. LLM reads it, updates relevant
atomic notes in `6- Atomic-notes/`, cross-references tag notes in `3- Tags/`,
and refreshes indexes in `4- Indexes/`.

### Query
LLM scans `4- Indexes/` and `3- Tags/` to locate relevant pages in
`6- Atomic-notes/`, then synthesizes an answer with citations.

### Lint
Health check against the Full-note template: frontmatter completeness,
missing sections, empty placeholder content, dead wikilinks, orphan notes,
domain consistency, mastery tag accuracy, stale rough notes.
`_meta/lint-report.md` captures results.
