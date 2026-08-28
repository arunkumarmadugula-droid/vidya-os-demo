# Vidya completion test report

Tested: August 27, 2026  
Build cache: `vidya-library-complete-2026-08-27-v4`

## Outcome

- Browser regression: **47/47 passed**
- Backend/security contract: **28/28 passed**
- JavaScript syntax: **app.js, assistant.js and auth.js passed**
- Uncaught browser errors: **0**
- Viewports: **390×844 phone, 820×1180 iPad portrait, 1180×820 iPad landscape**

The tests used a fresh encrypted vault and synthetic files. No personal document
or production credential was used.

## Problems reproduced and fixed

| Problem | Cause | Correction | Result |
|---|---|---|---|
| New subject disappeared | Tabs were built only from subjects that already had files | Tabs now include durable subjects and file subjects | Fixed |
| Mobile could not filter by file type | CSS hid the type selector below 900 px | Reflowed search, type and sort controls for phone/iPad | Fixed |
| It was unclear where an upload went | `All` silently mapped files to Inbox | Inbox is explained; rows display `@Subject` and generated `#tags` | Fixed |
| Could not organize Inbox | No obvious move workflow in the shipped view | Source details include **Stored in subject** | Fixed |
| Mixed uploads hid failures | Last success toast replaced earlier errors | One result now reports added and skipped items; file input resets | Fixed |
| Duplicate/unsupported files looked ignored | Error feedback was transient and overwritten | Explicit `Nothing added` / `skipped` result | Fixed |
| More than five Coach sources failed silently | Form sliced the selection only at submit | Sixth selection is rejected immediately with explanation | Fixed |
| A long file could monopolize a comparison | Passage ranking did not guarantee one result per selected source | Retrieval now represents every selected file before adding extra passages | Fixed |
| Source removal was too easy | Delete had no confirmation | Destructive confirmation names the file and backup boundary | Fixed |
| Empty search was a dead end | No action restored filters | Added **Clear filters** | Fixed |
| Installed build could remain stale | Static asset URLs did not change | Versioned CSS/JS URLs plus new service-worker cache | Fixed |
| API setup lived only in a separate document | Settings had no setup path | Added seven-step in-app **API setup guide** | Fixed |
| Scheduled-brief copy overstated push | Backend stores briefs but Web Push is not included | Settings now states that lock-screen delivery is a separate phase | Fixed |

## Browser functionality verified

### Vault and Library

- Encrypted vault creation and unlock.
- Demo source is explicitly named as demonstration material.
- TXT, Markdown, CSV, JSON, DOCX and PDF ingestion.
- `All` uploads enter `@Inbox`; upload under a selected subject stays there.
- Custom subject remains selectable before it contains a file.
- Duplicate and unsupported-file handling.
- File input resets, allowing the same file picker to be used again.
- Search across filename, subject, keywords and summary.
- File-type filter, A–Z sort and filter reset.
- Generated tags visible on source rows.
- Source details, searchable passages and move-to-subject.
- Follow-up task prefill and destructive confirmation.

### Coach and retrieval

- **Ask** attaches the exact file and leaves the question field empty.
- Local no-API answer retrieved the real owner, threshold, deadline and risk.
- Local citations open their stored source.
- Five-file comparison context and immediate maximum enforcement.
- Five-file local and secure retrieval represent five distinct selected sources.
- Secure-engine mock received selected Library excerpts.

### Rest of app

- Smart task capture parsed `@Work`, `#release`, date, time, estimate and priority.
- Expanded interest search.
- Seven-step API guide opens from Settings.
- Secure-engine health check and AI command-brief request.
- Secure Coach request includes selected Library excerpts; schedule update reaches the backend.
- Theme switching and Cost Monitor secure-usage estimate.
- All four command-brief lanes visible on phone.
- Scribe Write, Scan, Sketch and outcome selection; Write saves to Library.
- Encrypted backup contains no Library plaintext.
- No horizontal Library spread on phone or either iPad orientation.

## Backend/security contract verified statically

- Owner-token, Supabase JWT and separate Cron authentication paths.
- Exact-origin CORS fails closed; wildcard origins are rejected.
- Request, snapshot and hourly request limits.
- Private-reference prompt-injection boundary.
- Gemini 3.5 Flash-Lite / Gemini 3.7 Flash routing.
- `health`, `coach`, `visual`, `brief.generate`, `brief.latest`,
  `schedule.update` and `usage.summary` operations.
- Usage logs exclude prompt-text fields.
- RLS and private grants on user tables.
- Daily and five-hour Cron definitions use Supabase Vault.
- Example environment file contains placeholders, not live keys.
- Client sends selected excerpts, encrypts the engine token and removes it from
  backups.

## Remaining boundaries

These are product boundaries, not hidden working features:

1. The cloud function was tested through a strict mock and static contract
   checks. A real end-to-end Supabase/Gemini test requires the owner's project
   URL and secrets after deployment.
2. Local retrieval is lexical passage search. Large semantic RAG, OCR for
   image-only PDFs and cross-device Library sync are future backend phases.
3. GitHub Pages cannot run closed-app background work. Supabase Cron generates
   stored briefs; lock-screen delivery still needs Web Push subscription/server
   delivery.
4. First-class Siri App Intents, iPad Pencil squeeze and a system share
   extension require a small native iOS companion. Apple Shortcuts remains the
   web-app bridge.
5. Browser data belongs to its exact origin. `file://`, localhost and the
   GitHub HTTPS site do not share a Library. Use encrypted export/restore.

## Release acceptance

This build is suitable for a personal beta after:

1. Deploying the included migrations and Edge Function.
2. Adding server-side secrets.
3. Testing the real `health` response.
4. Asking a non-confidential selected file one question.
5. Generating one command brief and verifying Cost Monitor.
6. Exporting and restoring one encrypted backup.

See `Documentation/CLOUD-AI-SETUP.md` for the production procedure.
