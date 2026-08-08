# feat-rental-card-reusable

## Metadata

- Timestamp: 2026-08-09
- OS: Windows
- Branch: feat/scooter-card-scale-effect
- Repository: project-travel-lombok (Next.js App Router workspace)

---

## Summary

- Extracted the "scale-effect card" design from `ScaleEffectPreview` into a reusable, abstract component `RentalCard` (usable for scooter & car/vehicle content)
- Replaced the inline card markup on `/rent-scooter` (`ScooterList`) with `RentalCard`
- Refactored `ScaleEffectPreview` to consume `RentalCard` (removed duplicated card markup)
- Finalized mobile layout: photo & info locked 50/50 via `grid grid-cols-2`; equal card heights via `auto-rows-fr` + `h-full`
- Redesigned Reserve Now button: blue→indigo→violet gradient pill (rounded-sm on mobile, rounded-md on sm+), no WhatsApp icon (modal will come later), works in dark & light mode
- SAVE badge restyled: emerald→teal gradient + `Tag` icon, "Save {n}%" visible on all screens
- Tablet: title/specs wrap dynamically (beside if fits, specs below if long)

## Modified Files

- `src/components/ScooterList.tsx` — replace inline card with `RentalCard`, add `auto-rows-fr`
- `src/components/ScaleEffectPreview.tsx` — refactor to render `RentalCard`, remove inline markup

## Created Files

- `src/components/RentalCard.tsx` — reusable abstract rental card (scooter/car)

## Deleted Files

- None

## Reuse Analysis

- Reused `Button` from `@/components/ui/button`
- Reused `formatRupiah` from `@/utils/currency`, `toTitleCase` from `@/utils/titleCase`
- Reused `PricePeriod` type from `@/types/scooter`
- Reused existing Dialog booking modal in `ScooterList` (unchanged)

## New Components

- `RentalCard` (default export, abstract name — reusable for car/vehicle content)

## Commands Executed

- `npx tsc --noEmit`

## Validation

- Type Check: Pass
- Build: Not run (waiting for user signal)
- Deploy: Not run

---

## Notes

- Card mobile split is now bulletproof 50/50 via CSS grid (`grid grid-cols-2 sm:flex sm:flex-col`)
- Equal card height achieved with `auto-rows-fr` + `h-full`; booking button pinned bottom via `mt-auto`
- Button: gradient + `border-white/30` (light) / `dark:border-white/20` (dark)
- `RentalCard` props: `name`, `image`, `price { day, weekly?, monthly? }`, `specs?`, `onBook`
