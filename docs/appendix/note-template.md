---
title: Note Template
---

# Note Template

Copy this shape when starting a new note in any area. Keep terminology for one concept identical everywhere it appears.

````markdown
# Topic name

One or two plain sentences: what is it, and why does it matter?

## A concrete example

Ground it in something real (an app, a purchase, a conversation, a sentence in the language).

## Details

The actual content. Use a Mermaid diagram or table when it beats a paragraph.

## Key takeaways

- The three to five things worth remembering.

## Practice Questions

??? question "1. A question that tests the whole idea?"

    The answer, written so I could explain it to someone else.
````

## Where a new note goes

| If it is about... | Put it in |
| --- | --- |
| Networks, databases, distributed systems | System Design (`docs/system-design/` links to the existing `chapter-N/` pages) |
| A programming language (C++, JavaScript, Python, Flutter) | `docs/coding/<language>/` |
| Web, backend, security, cloud, Docker | `docs/coding/web/`, `backend/`, `security/`, `cloud/`, or `docker.md` |
| AI and machine learning | `docs/coding/ai/` |
| IT hardware, Microsoft 365, Agile and Scrum | `docs/coding/it/`, `microsoft-365/`, `agile/` |
| Learning a spoken or written language | `docs/languages/` |
| Earning, saving, investing, taxes | `docs/money/` |
| Communication, relationships, teamwork | `docs/people-skills/` |

Then add the page to the `nav:` section of `mkdocs.yml` under the matching tab so it shows in the sidebar.
