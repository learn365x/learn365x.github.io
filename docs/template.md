# How pages work

**Books and courses are learning lines:** one main work plus its companions, e.g. a book and the course that follows it (CSAPP + CMU 15-213). Each line has a roadmap and one flat folder under `docs/`.

**Papers are single pages in `docs/papers/`**, named `<year>-<short-name>.md` (e.g. `2012-alexnet.md`), whatever their field. A paper is short and self-contained, so it gets no roadmap and no folder. If a paper ever grows into a months-long study, turn it into its own line.

 Categories (systems, CV, LLMs, ...) are **tags**, not folders; see [Tags](tags.md).

There are four kinds of page: a **line roadmap** (one per line), a **unit point map** (one per unit), a **point** (many per unit) and a **paper page** (one per paper).

```
docs/<line>/index.md                ← line roadmap
docs/<line>/chNN/index.md           ← unit point map
docs/<line>/chNN/<id>-<name>.md     ← points
docs/papers/index.md                ← table of papers + reading orders
docs/papers/<year>-<name>.md        ← one paper
```

**Units follow the main source's structure:** chapters for a book (`ch02/`), sections for a paper, lectures or modules for a course. Example: `docs/csapp/index.md`, `docs/csapp/ch02/index.md` and `docs/csapp/ch02/csapp-2-01-hex.md`.

**Starting a new line:** create its folder and `index.md` from template A, add a row to the home page table, and add it to `nav` in `mkdocs.yml`. Create a unit folder only when you reach that unit.

## A. Line roadmap

````markdown
---
title: "<Line name>"
line: <short-id>           # folder name and prefix of point IDs
source: "<main work: authors, edition / venue, year>"
companions: []             # e.g. ["CMU 15-213"]
status: planned            # planned | active | paused | done
started:
tags:
  - domain/<domain>        # e.g. domain/systems, domain/cv, domain/llm
---

# <Line name>

**Why I'm learning this:** <one or two sentences>

**Materials:** <main work (edition, link), companion sources, labs>

**Plan:** <units in order, time estimate, how labs/projects fit in>

## Units
| # | Unit | Lab | Est. | Status |
|---|---|---|---|---|
| 1 | [<unit>](ch01/index.md) | | | |

## Labs / projects
- [ ] ...

## Now
**Current point:** ...

## Log
- yyyy-mm-dd: what I did, what I got wrong, what's next.
````

## B. Point

````markdown
---
title: "<a claim, not a topic>"
id: <line>-<unit>-01
type: concept            # concept | paper | technique | tool
source: "<book §x.y / paper §z>"
year:                    # when the idea appeared (history of the field)
learned:                 # when I studied it (history of my learning)
status: seen             # seen | can answer | can apply
needs: []
unlocks: []
tags:
  - domain/systems       # e.g. domain/cv, domain/llm-infra, domain/signal, domain/comm
  - layer/bits           # bits | hardware | os | compiler | framework | model
---

# <title>

## 1. Questions
Answer first, without reading. No answers are written in advance: I send mine to Claude, who checks them by running code. What I got wrong goes in the mistakes log.

1. <question>

## 2. If stuck, read
- <exact section>. Then re-answer the questions above.

## 3. Predict, then run
**My prediction:** ...

```python
# code test
```

**Actual output:** ...
**Prediction right?** yes / no, and why

## 4. Summary (my own words)
- ...

## 5. Big picture
**Shared principle:** <one sentence>

| Field | Same principle there | Check question | Verified? |
|---|---|---|---|
| | | | code / analogy |

## 6. Mistakes log
- yyyy-mm-dd: I thought ___, actually ___.
````

## C. Paper page
The point format, inside one page: each key design choice is a short section. Add a row to `docs/papers/index.md` when starting a paper.

````markdown
---
title: "<Paper title>"
id: <short-name>
source: "<authors, venue, year>"
year: <year>
status: planned            # planned | reading | done
learned:
tags:
  - domain/<domain>        # e.g. domain/cv, domain/llm, domain/systems (several are fine)
---

# <Short name> (<year>)

**Paper:** <full citation, link>

**Why I'm reading it:** <one sentence>

**Code:** <link, if any>

## Key points

### <Design choice 1>
*Paper §x.y*

**Questions**

1. ...

**Check** (prediction, then run)

**Summary** (my own words)

**Big picture**

## Mistakes log
- yyyy-mm-dd: I thought ___, actually ___.
````

## How deep do big-picture links go?

**One hop, at the level of the shared principle.** A link shows that the *same idea* appears in another field. It doesn't teach that field.

- **2–4 links per point**, only where the link is real.
- **One hop only:** link from this point to another field, never from that field on to a third.
- **Each link gets one check question I can answer in about 5 minutes** from this point plus what I already know. If answering it needs a concept I haven't learned, the link is too deep.
- **Too deep? Don't follow it now.** Write it in a "later" list. It can become its own point when that line is active.
- **Mark each link** `code` (I checked it by running something) or `analogy` (understood, not verified).
