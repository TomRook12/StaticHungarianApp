# Decision: Keep App.jsx as a single file beyond 1,500 lines

> **Date:** 2026-04-16
> **Status:** Accepted

## Context

After completing Milestones 1–5 (including the engine-depth spec), `src/App.jsx` has grown to ~1,937 lines — well beyond the 1,500-line soft limit noted in the project constitution. The spec required a decision record before considering a file split.

The app is a family-use PWA deployed to GitHub Pages. The single-file constraint was adopted deliberately: it eliminates module wiring complexity, makes the whole app greppable in one place, and means any contributor can understand the entire codebase by reading one file.

## Decision

Keep `App.jsx` as a single file. Do not split it at this point.

Rationale:
- The file is long but not complex — most of the growth is lesson data (constant arrays). The actual component and logic code is around 400–500 lines.
- All section banners (`// ─── NAME`) make navigation trivial with grep. `docs/app-map.md` provides a structural index without opening the file.
- Splitting would require a decision about module boundaries (data vs. components vs. logic), a migration, and ongoing discipline to keep imports correct — all overhead that adds no user value.
- The zero-dependency constraint and single-file rule are central to this app's maintenance philosophy: it must be understandable and deployable by a non-developer parent in the future.

Revisit this decision if App.jsx exceeds 3,000 lines or if a clear, stable module boundary emerges (e.g., STORIES data is large enough to warrant its own file).

## Alternatives considered

| Option | Why rejected |
|--------|-------------|
| Split into `data.js` + `App.jsx` | Data and components reference each other frequently; a data module would need to export ~200 constants |
| Split into feature modules (`StoryView.jsx`, etc.) | Adds import overhead; makes the "read one file" property false; requires decision about shared state |
| Lazy-load lesson data | Unnecessary complexity; data is ~1,200 lines of static arrays, not a performance concern |

## Consequences

- `App.jsx` will continue to grow as lessons are added. This is acceptable — each lesson is ~15 lines.
- Editors with poor large-file performance may slow down. The `docs/app-map.md` grep-based workflow mitigates this.
- The convention-reviewer agent should continue to flag any structural changes that deserve discussion.
