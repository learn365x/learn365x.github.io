# ROADMAP: the context file

Read this first at the start of every study session, both me and Claude.
It holds the method, the rules and where things stand. Each topic's own detailed roadmap is in `docs/<area>/<topic>/index.md`.

## About
- Background: several years of CV research and PyTorch.
- Goal: understand systems, CV and LLMs from first principles (be able to predict, explain and rebuild), not just use them.
- Machines: Windows + WSL, and a remote Linux server (VS Code SSH). Labs run on the server.
- Time: 60–90 min every day, first thing. 20-minute minimum on bad days. 30-minute review every week.

## Site
- MkDocs 1.6.1 + Material 9.7.7, pinned in `requirements.txt`. GitHub Actions builds to the `gh-pages` branch, and Pages serves `gh-pages`.
- Use only standard Markdown features (tables, code, math, admonitions, collapsible `???` blocks, tags), so the site can move to another generator later.
- **Spring 2027 (before May):** check whether Zensical (the Material team's successor, which reads `mkdocs.yml`) is stable and supports tags. If yes, migrate.

## Structure
- `docs/index.md`: overview of all learning lines.
- `docs/<area>/<topic>/index.md`: a topic's roadmap (why, materials, plan, points, labs, Now, log). Areas: `books/`, `papers/`, `courses/`.
- `docs/<area>/<topic>/<point-id>.md`: one point.
- `docs/template.md`: page formats (A: topic roadmap, B: point) and the big-picture depth rule.
- **Starting a topic:** create its folder and `index.md` from template A, add a row to the home page table, and add it to `nav` in `mkdocs.yml`.

## Per-point flow
1. Questions first: answer without reading.
2. If stuck: read the exact section of the source, then re-answer.
3. Predict the output, then run the code test. Send code + prediction + output to Claude to check.
4. Summary in my own words, checked by Claude.
5. Big picture: 2–4 links to other fields, one hop only, each with a check question answerable in about 5 minutes. Deeper links go on a "later" list. Mark each link `code` or `analogy`.
6. Mistakes log.

## Rules
- At most 2–3 active topics at once.
- Claude checks every answer and example by running code before giving it.
- Hints only for official course labs. Solutions stay in a private repo.
- Point IDs start with the topic, e.g. `csapp-2-01`.
- 80% learning, at most 20% writing pages.

## Topics
| Topic | Area | Status | Roadmap |
|---|---|---|---|
| CSAPP (3rd ed.) | book | active | `docs/books/csapp/index.md` |

## Now
- 2026-11-18: shell repo set up; CSAPP started (roadmap + chapter 2 point map).
- **Next:** csapp-2-01 Hex notation and data sizes (§2.1.1–2.1.2).

## How a session ends
Update the topic's "Now" and log line, then the "Now" section above. Commit.
