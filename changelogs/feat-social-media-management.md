# feat-social-media-management

## Metadata

- Timestamp: 2026-06-13
- OS: Windows
- Branch: feat/admin-destinations-crud
- Repository: geo-travel-lombok

---

## Summary

- Added Social Media management in admin panel (CRUD)
- Updated Footer to read social links dynamically from Firestore
- Fixed Facebook link bug (was pointing to Instagram URL)

## Modified Files

- `src/types/firestore.ts` — added `SocialData` and `Social` types
- `src/App.tsx` — added route `/admin/socials`
- `src/layouts/menu.ts` — added "Social Media" menu item with Share2 icon
- `firestore.rules` — added `socials` collection with public read / admin write
- `src/components/Footer.tsx` — replaced hardcoded social icons with dynamic Firestore data; added `SocialIcon` component with SVG icons for Instagram, Facebook, Twitter/X, YouTube, TikTok

## Created Files

- `src/lib/firebase/admin/socialAdmin.service.ts` — CRUD service with token auth (following destinationAdmin pattern)
- `src/pages/admin/AdminSocialPage.tsx` — Admin CRUD UI (card grid + modal form, following AdminDestinationPage pattern)

## Reuse Analysis

- Followed exact pattern from `AdminDestinationPage` and `destinationAdmin.service.ts`
- Reused `Modal` from `@/components/ui/DialogScooter`
- Reused token-auth pattern from existing admin services
- Reused existing SVG icons from Footer for Instagram/Facebook

## Commands Executed

- `npx tsc --noEmit`
- `pnpm build`
- `firebase deploy --only hosting`
- `firebase deploy --only firestore:rules`

## Validation

- Type Check: Pass (only pre-existing styled-components false positive)
- Build: Success
- Deploy: Success — hosting + firestore rules

---

## Notes

- Social links displayed in Footer are filtered by `active == true` and sorted by `order` ascending (realtime via `onSnapshot`)
- Platform icons supported: Instagram, Facebook, Twitter/X, YouTube, TikTok — others fallback to `ExternalLink` icon
- Admin can add any platform name (free text), set URL, toggle active/inactive, and reorder
