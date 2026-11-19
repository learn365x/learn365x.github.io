# How pages work

There are two kinds of page: a **topic roadmap** (one per topic) and a **point** (many per topic).

```
docs/<area>/<topic>/index.md        ← topic roadmap
docs/<area>/<topic>/<point-id>.md   ← points
```

Areas are `books/`, `papers/` and `courses/`. Example: `docs/books/csapp/index.md` and `docs/books/csapp/2-01-hex.md`.

**Starting a new topic:** create its folder and `index.md` from template A, add a row to the home page table, and add it to `nav` in `mkdocs.yml`.

## A. Topic roadmap

````markdown
---
title: "<Topic name>"
topic: <short-id>          # used as the prefix of point IDs
area: book                 # book | paper | course
source: "<authors, edition / venue, year>"
status: planned            # planned | active | paused | done
started:
---

# <Topic name>

**Why I'm learning this:** <one or two sentences>

**Materials:** <book edition, paper link, course site, labs>

**Plan:** <order, time estimate, how labs/projects fit in>

## Points
| ID | Point | Source section | Needs | Status |
|---|---|---|---|---|
| <id>-01 | | | – | |

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
id: <topic>-01
type: concept            # concept | paper | technique | tool
source: "<book §x.y / paper §z>"
year:                    # when the idea appeared (history of the field)
learned:                 # when I studied it (history of my learning)
status: seen             # seen | can answer | can apply
needs: []
unlocks: []
tags:
  - domain/cs-systems    # e.g. domain/cv, domain/llm-infra, domain/signal, domain/comm
  - layer/bits           # bits | hardware | os | compiler | framework | model
---

# <title>

## 1. Questions
Answer first, without reading.

1. <question>

    ??? answer
        <answer + why>

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

## How deep do big-picture links go?

**One hop, at the level of the shared principle.** A link shows that the *same idea* appears in another field. It doesn't teach that field.

- **2–4 links per point**, only where the link is real.
- **One hop only:** link from this point to another field, never from that field on to a third.
- **Each link gets one check question I can answer in about 5 minutes** from this point plus what I already know. If answering it needs a concept I haven't learned, the link is too deep.
- **Too deep? Don't follow it now.** Write it in a "later" list. It can become its own point when that topic is active.
- **Mark each link** `code` (I checked it by running something) or `analogy` (understood, not verified).
