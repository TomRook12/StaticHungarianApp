# Conventions

## File structure

The app is intentionally a single file (`src/App.jsx`). Sections are separated with ASCII banner comments:

```js
// ─── SECTION NAME ──────────────────────────────────────────────────────────
```

Maintain this order: DATA → UTILITIES → ENGINES → HOOKS → QUESTION GENERATORS → STYLES → COMPONENTS → APP.

## Data

- Lesson `id` values are stable and used as keys in `localStorage`. Never reuse or renumber them.
- Add new lessons by appending to `LESSONS[]` with the next sequential `id`.
- Phrase fields: `hu` (Hungarian text), `pr` (pronunciation guide), `en` (English translation). All three are required.
- `aud` is either `"kids"` or `"wife"`. Omitting it is acceptable only for toolkit/reference lessons.

## Components

- Inline styles only — no CSS files, no CSS-in-JS libraries, no Tailwind.
- All colours come from the `C` constants object. Never hardcode a colour outside of `C`.
- Components are functions, not classes.
- Keep components small and co-located in the file. Extract a component when JSX is repeated more than twice.

## State

- Prefer `useState` for UI state, `useCallback` for stable handlers, `useMemo` for derived values.
- All persisted state goes through `useStats`. Don't call `localStorage` directly anywhere else.
- Don't add a new top-level state manager (Redux, Zustand, etc.) without a decision record.

## Naming

- React components: `PascalCase`
- Functions and variables: `camelCase`
- Constants (data arrays, config objects): `SCREAMING_SNAKE_CASE`
- Inline style objects defined at call-site need no naming convention.

## Questions / quiz

- Every question generator (`gen*`) accepts a phrase object and returns a question object with at least `{ type, answer, phrase }`.
- `generateQuestions` is the only place that calls question generators. Don't call them directly from components.

## Accessibility & mobile

- The app targets portrait mobile. Default touch target minimum is 44 × 44 px.
- No hover-only interactions.
- Speech buttons are supplementary; the app must be fully usable without audio.

## Dependencies

Zero production dependencies beyond `react` and `react-dom`. Adding a dependency requires a decision record explaining why the bundle cost is justified.
