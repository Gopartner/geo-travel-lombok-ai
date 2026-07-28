# fix-slug-auto-generate-admin-scooter

## Metadata

- Timestamp: 2026-07-28
- OS: Windows (win32)
- Branch: feat/admin-destinations-crud
- Repository: geo-travel-lombok

---

## Summary

Fix slug bug di AdminScooterPage — slug field sekarang auto-generate dari Unit Name saat create, tetap bisa di-custom manual. Serta konsolidasi fungsi `slugify` ke shared utility.

---

## Root Cause

- Form pakai `defaultValue` (uncontrolled input) untuk slug field
- Slug bisa "bleed" dari sesi edit sebelumnya ke form create baru
- Fallback chain `formData.get("slug") || selectedScooter?.slug || ""` menghasilkan empty string yang lolos validasi `!data.slug`
- Empty string dipakai sebagai Firestore document ID → data corrupt

---

## Modified Files

- `src/pages/admin/AdminScooterPage.tsx` — controlled state untuk name & slug, auto-generate + manual override
- `src/pages/admin/AdminVehiclePage.tsx` — replace inline `generateSlug()` dengan shared `slugify()`

## Created Files

- `src/utils/slugify.ts` — shared slugify utility (kebab-case)

## Deleted Files

- (none)

---

## Reuse Analysis

- Shared utility `slugify()` di `src/utils/slugify.ts` bisa dipakai oleh admin page lain
- Mengikuti pattern existing `src/utils/currency.ts` (single export function)

---

## Validation

- Type Check: pass (error styled-components pre-existing, unrelated)
- Build: not run (menunggu approval user)
- Deploy: not run (menunggu approval user)

---

## Behavior

### Create Mode
- Ketik Unit Name → Slug auto-update ke kebab-case (misal: `Honda Scoopy 2024` → `honda-scoopy-2024`)
- Admin bisa override slug manual → auto-generate berhenti
- Indicator: "⚡ Auto-generated dari nama" / "✏️ Manual mode"

### Edit Mode
- Slug field `readOnly` (tidak bisa diubah, menjaga konsistensi document ID)
- State di-reset ke data existing saat modal dibuka

### Validation
- Fallback: `formSlug || slugify(formName)` — slug tidak pernah kosong
- Error thrown jika hasil akhir masih kosong
