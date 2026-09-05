# Fall 2027 Coursework — LLM Wiki

This repo follows Andrej Karpathy's ["LLM Wiki" pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f):
instead of re-reading raw notes/PDFs from scratch every time a question comes up (plain RAG), Claude
incrementally builds and maintains a persistent markdown wiki under `wiki/`. The wiki is compiled once
from sources and kept current — read it before re-deriving something from raw files.

## Layers

1. **Raw sources** (immutable) — course folders: `COP2274/`, `EAS4200/`, `EAS4300/`, `EAS4700/`,
   `EML4140/`. Lecture slides, readings, problem sets, notes, syllabi. Never edit these except to add
   new material — they are the ground truth the wiki is compiled from.
   - **Note:** some course folders currently live one level up, in `../` (the `Documents/` folder),
     rather than inside this repo. EAS4300's real source folder is `../EAS4300/`. Check both locations
     before concluding a source is missing. Per-course source paths are recorded on each course page.
2. **The wiki** (`wiki/`) — LLM-maintained markdown. Summaries, per-course pages, cross-cutting concept
   pages, and links back to the source file each claim came from.
3. **This schema** (this file) — defines the structure and the three operations below.

## Wiki structure

- `wiki/index.md` — catalog of every wiki page with a one-line summary. Update this whenever a page is
  added or its scope changes.
- `wiki/log.md` — append-only chronological record of ingests, queries answered, and lint passes. Never
  edit past entries; append new ones with a date.
- `wiki/courses/<CODE>.md` — hub page per course (e.g. `wiki/courses/EAS4300.md`). Overview, logistics,
  grading, full schedule, exam dates, a lecture index, and a source list linking back to files in the
  course's raw-source folder.
- `wiki/courses/<CODE>/L##-<slug>.md` — one page per lecture/topic, when a course has enough material to
  warrant it. Numbered by the **syllabus's own topic number** so the filename greps against the
  schedule. Each lecture page carries a metadata header (topic no., dates, book sections, tags), then
  concepts explained in prose, key equations, worked logic, pitfalls, and an exam checklist.
  - **Display equations go in `$$ ... $$` blocks**, with the `$$` on their own lines. **Inline math uses
    single `$ ... $`.** This is Obsidian/MathJax syntax — the wiki is read in Obsidian, which typesets
    these as real equations. Keep this convention for all courses.
    - Do **not** use ` ```latex ` code fences — Obsidian renders those as gray code boxes, not math.
    - Plain ` ``` ` fences are still correct for ASCII schematics (engine layouts, block diagrams).
    - Avoid blank lines inside a `$$` block; they break MathJax rendering.
- `wiki/courses/<CODE>/exam-*.md` — scope/prep pages per exam, listing which lecture pages are in play.
- `wiki/concepts/<slug>.md` — cross-cutting concept pages when the same idea shows up in more than one
  course (e.g. a stats concept used in both EAS4200 and EML4140). Link to and from the relevant course
  pages.

## Operations

**Ingest** — when new material lands in a course folder (or the user pastes/describes something):
1. Read the source.
2. Update the relevant `wiki/courses/<CODE>.md` page (or create it) — extract what matters, don't just
   copy the source. Cite the source file/section.
3. If the material introduces a concept relevant to another course, create/update a
   `wiki/concepts/<slug>.md` page and cross-link it from both course pages.
4. Update `wiki/index.md` if a page was added or its summary changed.
5. Append a one-line entry to `wiki/log.md`: date, what was ingested, what pages changed.

**Query** — when the user asks a question:
1. Check `wiki/index.md` first to see if it's already covered.
2. Answer from the wiki pages, not by re-reading raw sources, unless the wiki is missing the answer —
   in that case read the raw source, answer, and consider ingesting the gap.
3. If the answer is likely to be asked again (e.g. a good exam-prep synthesis), save it as a new or
   updated wiki page rather than letting it live only in chat.

**Lint** — periodically, or when asked to "clean up the wiki":
1. Look for contradictions between pages, orphan pages not listed in `index.md`, stale claims (e.g. an
   assignment page that never got exam results added), and missing cross-links between related
   concept/course pages.
2. Fix what you can directly; flag the rest in `wiki/log.md`.

## Notes

- Course names/topics are intentionally left as `TBD` in the stub pages below — fill them in on first
  ingest rather than guessing.
- This is a personal study tool, not a citation-grade source — always double check against the actual
  syllabus/lecture material before relying on a wiki page for something graded.
