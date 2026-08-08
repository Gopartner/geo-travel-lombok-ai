# feat-scooter-card-scale-effect

## Metadata

- Timestamp: 2026-08-08
- OS: Windows
- Branch: feat/scooter-card-scale-effect
- Repository: geo-travel-lombok

---

## Summary

- Applied "scale-effect card" design (Tailwind Tap reference) to `ScooterCard`
- Kept all existing features: daily/weekly/monthly pricing blocks, SAVE/BEST VALUE badges, Reserve button, responsive mobile (horizontal) + desktop (vertical) layout
- Per user decision: "konten nya fitur tetap" (keep features, restyle only)

## Modified Files

- `src/components/ScooterCard.tsx` — restyled to scale-effect card visual language

## Created Files

- None

## Deleted Files

- None

## Reuse Analysis

- Kept existing `Button` from `@/components/ui/button`
- Kept existing `formatRupiah` from `@/utils/currency`
- Reused existing shimmer/bounce-save keyframes (unchanged)

## New Components

- None (inline helper `getInitials` added inside ScooterCard)

## Commands Executed

- `git checkout -b feat/scooter-card-scale-effect`
- `npx tsc --noEmit`

## Validation

- Type Check: Pass (only pre-existing node_modules false positives from goober/styled-components)
- Build: Not run (waiting for user signal)
- Deploy: Not run

---

## Notes

- Card now: `hover:drop-shadow-md` + image `group-hover:scale-125` with delay-200 ease-in-out (reference scale-effect)
- Added avatar initials circle (top-right on image) derived from scooter name — follows reference card pattern
- Added "Scooter Rental" category label (truncate) above the title; title now `line-clamp-2`
- No prop contract changes — `ScooterCard` API unchanged, callers in `src/pages/Home.tsx` untouched
