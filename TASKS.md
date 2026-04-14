# Gmail Email Extractor - Full-Stack Pilot Task Plan

## Phase 0 - Planning and Alignment
- Finalize architecture with TL review
- Confirm pilot scope (email extraction only)
- Confirm team split (3 engineers)
- Validate GitHub issues, labels, milestones

Deliverable:
- Approved implementation plan.

---

## Phase 1 - Repository and Scaffolding
- Create `backend/` FastAPI scaffold
- Create `frontend/` React + Vite scaffold
- Add environment templates (`.env.example`)
- Add shared coding conventions and lint setup

Deliverable:
- Frontend and backend boot locally.

---

## Phase 2 - Backend Foundation
- Add FastAPI app structure and route modules
- Configure DB layer (SQLite for pilot)
- Add base models and migrations (Alembic)
- Add health endpoint and basic logging

Deliverable:
- Stable backend foundation ready for features.

---

## Phase 3 - Gmail OAuth Integration
- Configure Google Cloud project and OAuth credentials
- Implement `/api/gmail/connect`
- Implement `/api/gmail/callback`
- Persist encrypted token metadata
- Add `/api/gmail/status`

Deliverable:
- Gmail account can be connected successfully.

---

## Phase 4 - Sync and Extraction Pipeline
- Implement Gmail pagination sync
- Read headers only (`From`, `To`, `Cc`, `Bcc`, `Reply-To`)
- Normalize and validate emails
- Deduplicate and upsert into `emails` table
- Track processed message IDs for idempotency

Deliverable:
- Backend extracts and stores unique email IDs.

---

## Phase 5 - Contacts API and Export
- Implement `GET /api/contacts` with pagination/filter basics
- Implement `GET /api/export/contacts.csv`
- Implement `GET /api/export/contacts.json`
- Add summary stats response for UI

Deliverable:
- Processed email IDs can be viewed and exported via API.

---

## Phase 6 - Frontend Pilot UI
- Add app routes/pages (dashboard, connect, sync, contacts)
- Integrate API client and query state
- Build contacts table and search/filter basics
- Add export buttons (CSV/JSON)

Deliverable:
- End-to-end pilot flow is usable in browser.

---

## Phase 7 - Reliability and Hardening
- Add retries for Gmail API transient failures
- Improve error handling and user-facing messages
- Add run logs and sync progress status
- Add smoke tests for critical flows

Deliverable:
- Pilot is stable for team usage and demo.

---

## Phase 8 - UAT and Release Readiness
- Run full mailbox test
- Validate output quality and dedupe behavior
- Verify OAuth reconnect and token refresh behavior
- Finalize docs and rollout checklist

Deliverable:
- Pilot approved for internal usage.

---

## Critical Dependency Chain
`Phase 1 -> Phase 2 -> Phase 3 -> Phase 4 -> Phase 5 -> Phase 6 -> Phase 8`

Parallel-friendly:
- Phase 6 UI shell can start after Phase 2
- Phase 7 hardening can start once Phase 4 is functional

---

## Definition of Done
- Full-stack app runs locally (frontend + backend)
- Gmail OAuth and sync work on real account
- Unique email IDs are extracted and shown in UI
- CSV and JSON exports are downloadable
- Pilot documentation is complete and reviewed
