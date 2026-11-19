# learn365x

Learning from first principles, one point at a time. Each learning line is one main work plus its companions, and all lines link into one big picture.

## About
- **Background:** several years of CV research and PyTorch.
- **Goal:** understand systems, CV and LLMs from first principles (be able to predict, explain and rebuild), not just use them.
- **Machines:** Windows + WSL, and a remote Linux server (VS Code SSH). Labs run on the server.
- **Time:** 60–90 min every day, first thing. 20-minute minimum on bad days. 30-minute review every week.

## Learning lines
Books and courses are learning lines. Each line has one folder, `docs/<line>/`, and its `index.md` is that line's roadmap. Categories are [tags](tags.md), not folders.

| Line | Tags | Started | Status |
|---|---|---|---|
| [CSAPP: Computer Systems: A Programmer's Perspective](csapp/index.md) (+ CMU 15-213) | systems, programming, architecture | 2026-11-18 | active |

Status: `planned` → `active` → `paused` / `done`.

**Papers** are not lines: each is one page in [Papers](papers/index.md), whatever its field.

| Collection | Tags | Started | Status |
|---|---|---|---|
| [Papers](papers/index.md) (1 paper) | cv, deep-learning | 2026-03-18 | active |

## Now
- 2026-11-18: site set up; CSAPP started (roadmap + chapter 2 point map).
- **Next:** csapp-2-01 Hex notation and data sizes (§2.1.1–2.1.2).

## Layout
```
docs/index.md                       ← this page: all lines, flow, rules
docs/<line>/index.md                ← a line's roadmap (sources, plan, Now, log)
docs/<line>/chNN/index.md           ← a unit's point map
docs/<line>/chNN/<id>-<name>.md     ← one point, e.g. csapp/ch02/csapp-2-01-hex.md
docs/papers/<year>-<name>.md        ← one paper, e.g. papers/2012-alexnet.md
docs/tags.md                        ← tag index (generated)
docs/timeline.md                    ← when each idea appeared
docs/template.md                    ← page formats
labs/                               ← my own small labs
```

**Starting a line:** create `docs/<line>/index.md` from [template A](template.md#a-line-roadmap), add a row to the table above, and add it to `nav` in `mkdocs.yml`.

## How each point works
The same for every line:

1. **Questions first**: answer without reading anything.
2. **If stuck**: read the exact section of the source, then re-answer.
3. **Predict, then run**: write down the expected output, then run the code test. Code + prediction + output go to Claude to check.
4. **Summary**: in my own words, checked by Claude.
5. **Big picture**: 2–4 links to other fields, one hop only, each with a check question answerable in about 5 minutes. Deeper links go on a "later" list. Each link is marked `code` or `analogy`.
6. **Mistakes log**: what I got wrong, and why.

Status of each point: `seen` → `can answer` → `can apply`.

## Rules
- At most 2–3 active lines at once.
- Every answer and example is checked by running code.
- Hints only for official course labs, never solutions. Solutions stay in a private repo.
- Point IDs start with the line, e.g. `csapp-2-01`.
- 80% learning, at most 20% writing pages.

## How a session ends
Update the line's "Now" and log, then the "Now" section above. Commit.

## Site
- MkDocs 1.6.1 + Material 9.7.7, pinned in `requirements.txt`. GitHub Actions builds to the `gh-pages` branch, and Pages serves it.
- Only standard Markdown features (tables, code, math, admonitions, collapsible `???` blocks, tags), so the site can move to another generator later.
- **Spring 2027 (before May):** check whether Zensical (the Material team's successor, which reads `mkdocs.yml`) is stable and supports tags. If yes, migrate.

See [How pages work](template.md) for the page formats.
