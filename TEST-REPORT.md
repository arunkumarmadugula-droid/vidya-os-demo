# Vidya final release test report

Release: `2026-08-11`  
Package: `Vidya-OS-FINAL-WEB-APP-2026-08-11`

## Passed

- JavaScript syntax checks: `app.js`, `auth.js`, and `sw.js`.
- HTML ID uniqueness and required service-worker asset presence.
- First-run vault creation, recovery-key creation, manual lock, reload lock, correct-password unlock, and wrong-password rejection.
- Encrypted persistence for app state and Library documents; no plaintext task/chat/document state is intentionally stored after migration.
- Mobile website at 320 x 568 and 390 x 844 with no horizontal Library overflow.
- Mobile source details dialog buttons remain inside the viewport.
- Desktop website at 1440 x 900.
- Library search, subject filter, type filter, sorting, source selection, and passage-count wording.
- Interest Hub: 48 topics in eight groups, search, Follow, and the five-Core limit.
- Interest-aware Brief ranking and rotating live-research topic selection.
- `@Subject` plus `#tag` task capture from Coach to Today.
- Encrypted backup export/restore controls, password change, local reset, install guidance, and offline status UI.
- User guide accessibility audit: zero high-, medium-, or low-severity findings.
- User guide visual preview: 14 pages reviewed with no visible clipping or overflow.

## Device test still required

The real iPhone biometric ceremony cannot be automated in the desktop test browser. After GitHub Pages is live over HTTPS, test **Unlock with this device** in Safari and the installed Home Screen app. iOS may present Face ID, Touch ID, or the device passcode. Vidya never receives or stores biometric data.

## Security boundary

This release is an encrypted, browser-local personal beta. It is not yet a cross-device cloud account. Confidential multi-device use, reliable closed-app reminders, and server-protected AI require the Supabase/Auth/RLS/Storage/Edge Function upgrade described in the user guide. Do not place Supabase service-role keys or production AI keys in browser code.
