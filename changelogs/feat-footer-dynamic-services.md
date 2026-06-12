# feat-footer-dynamic-services

## Metadata

- Timestamp: 2026-06-12
- OS: Windows
- Branch: feat/footer-dynamic-services
- Repository: geo-travel-lombok

---

## Summary

Added conditional rendering to Footer Services section based on Firestore collection data availability, matching the pattern already used in Navbar (`useFilteredNavigation`).

## Modified Files

- `src/components/Footer.tsx`

## Created Files

- `.ai/changelogs/feat-footer-dynamic-services.md`

## Deleted Files

- None

## Reuse Analysis

- Reused pattern from `src/hooks/useFilteredNavigation.ts` — `onSnapshot` + `limit(1)` to check collection existence
- Local hook `useCollectionHasData` created inline in Footer (avoids unnecessary abstraction for a single consumer)

## Commands Executed

- `git checkout -b feat/footer-dynamic-services`
- `npx tsc --noEmit`

## Validation

- Type Check: Pass (no Footer-related errors)
- Build: Not run (waiting for user signal)
- Deploy: Not run (waiting for user signal)

---

## Notes

- `hasVehicles` controls both "Airport & Hotel Shuttle" and "Car Rental" items
- `hasScooters` controls "Motorbike Rental" item
- "Mobile Booking & Support" remains unconditional
- Real-time reactive — items appear/disappear immediately when Firestore data changes
