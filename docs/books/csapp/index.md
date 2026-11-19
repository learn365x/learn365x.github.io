---
title: "CSAPP: Computer Systems: A Programmer's Perspective"
topic: csapp
area: book
source: "Bryant & O'Hallaron, 3rd ed. (Global Edition), 2016"
status: active
started: 2026-11-18
---

# CSAPP: Computer Systems: A Programmer's Perspective

**Why I'm learning this:** to understand what actually happens under the code I write in Python and PyTorch: data representation, machine code, memory, processes. Then I can predict performance and bugs instead of guessing.

## Materials
- **Book:** 3rd edition, Global Edition. Read the chapter text from it, but **skip its practice and homework problems**: the authors say that edition's problem set has many errors. Questions on this site are written separately and checked by running code. Sections are referenced by number (e.g. §2.1.3), not by page.
- **Book site** (errata, self-study lab handouts): <https://csapp.cs.cmu.edu/3e/>
- **CMU 15-213** (slides, schedule), as a second explanation: <https://www.cs.cmu.edu/~213/>
- **Machine for labs:** the remote Linux server (x86-64).
- **Lab solutions** go in a private repo, not here.

## Plan
Order follows CMU 15-213. Chapter 4 is skipped on the first pass. Estimate: 7–9 months at 60–90 min a day.

| # | Chapter | Official lab | Est. | Status |
|---|---|---|---|---|
| 1 | Ch1 A tour of computer systems | – | 2 days | |
| 2 | [Ch2 Representing and manipulating information](ch02/index.md) | datalab | 3–4 wk | next |
| 3 | Ch3 Machine-level representation of programs | bomblab, attacklab | 5–6 wk | |
| 4 | Ch6 The memory hierarchy | cachelab | 3 wk | |
| 5 | Ch5 Optimizing program performance | – | 2–3 wk | |
| ★ | **Project:** speed up a CV/ML step and explain why, using Ch5–6 | – | 1–2 wk | |
| 6 | Ch7 Linking | – | 2 wk | |
| 7 | Ch8 Exceptional control flow | shelllab | 3–4 wk | |
| 8 | Ch9 Virtual memory | malloclab | 4–5 wk | |
| 9 | Ch10 System-level I/O | – | 1 wk | |
| 10 | Ch11 Network programming | proxylab | 2 wk | |
| 11 | Ch12 Concurrent programming | proxylab | 2–3 wk | |
| – | Ch4 Processor architecture | archlab | later | |

Chapter status: blank → `next` → `in progress` → `done` (all points at least `can answer`, lab passed).

## How this topic works
- Each chapter gets a folder (`ch02/`, `ch03/`, …) when I reach it, with a point map in its `index.md`.
- One point ≈ one session. Point pages are `chNN/<id>-<short-name>.md`, IDs like `csapp-2-01`.
- A chapter's official lab comes after the points it needs. The point map says where.

## Now
**Current point:** csapp-2-01 Hex notation and data sizes (§2.1.1–2.1.2)

## Log
- 2026-11-18: set up the CSAPP roadmap and the chapter 2 point map.
