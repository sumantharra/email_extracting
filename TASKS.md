# Gmail Email Extractor - Full-Stack Pilot Task Plan

## Phase 0 - Planning and Alignment
- Finalize architecture with TL review
- Confirm pilot scope (email extraction only)
- Confirm team split (3 engineers)
- Validate GitHub issues, labels, milestones
- Define solo execution cadence (daily checkpoint + weekly demo)
- Freeze pilot API contract draft before heavy coding
- Create explicit acceptance criteria per phase issue
- Set simple risk register (OAuth delay, Gmail quota, parsing edge cases)

Deliverable:
- Approved implementation plan.

---

## Phase 1 - Repository and Scaffolding
- Create `backend/` FastAPI scaffold
- Create `frontend/` React + Vite scaffold
- Add environment templates (`.env.example`)
- Add shared coding conventions and lint setup
- Add Python tooling (`ruff`, `black`, `pytest`) baseline config
- Add frontend tooling (`eslint`, `prettier`, `vitest`) baseline config
- Add `Makefile` (or npm scripts) for common local commands
- Add pre-commit hooks for lint/format guardrails
- Add initial CI workflow for lint + unit tests
- Add README setup section for first local run

Deliverable:
- Frontend and backend boot locally.

---

## Phase 2 - Backend Foundation
- Add FastAPI app structure and route modules
- Configure DB layer (SQLite for pilot)
- Add base models and migrations (Alembic)
- Add health endpoint and basic logging
- Add app settings validation (fail fast when env missing)
- Add CORS config for local frontend domain
- Add centralized error handlers and API error schema
- Add request ID middleware for traceability
- Add startup checks (DB connection + migration state)
- Add seed script for local dev smoke testing

Deliverable:
- Stable backend foundation ready for features.

---

## Phase 3 - Gmail OAuth Integration
- Configure Google Cloud project and OAuth credentials
- Implement `/api/gmail/connect`
- Implement `/api/gmail/callback`
- Persist encrypted token metadata
- Add `/api/gmail/status`
- Handle token refresh and expired grant recovery flow
- Add reconnect endpoint/path for revoked tokens
- Add CSRF `state` handling and callback validation
- Store minimal OAuth scopes and last-refresh timestamp
- Add OAuth troubleshooting docs (redirect URI mismatch, consent mode)
- Add integration test for connect -> callback -> status

Deliverable:
- Gmail account can be connected successfully.

---

## Phase 4 - Sync and Extraction Pipeline
- Implement Gmail pagination sync
- Read headers only (`From`, `To`, `Cc`, `Bcc`, `Reply-To`)
- Normalize and validate emails
- Deduplicate and upsert into `emails` table
- Track processed message IDs for idempotency
- Add sync job table with statuses (`queued`, `running`, `done`, `failed`)
- Add incremental sync mode (since last successful sync timestamp)
- Add mailbox scope flags (Inbox/Sent and optional Promotions/Updates)
- Add malformed header handling and dead-letter logging
- Add domain-level allow/deny filter hooks for future extension
- Add parser unit tests for tricky header formats
- Add load-safe batching with backoff for quota/rate limits

Deliverable:
- Backend extracts and stores unique email IDs.

---

## Phase 5 - Contacts API and Export
- Implement `GET /api/contacts` with pagination/filter basics
- Implement `GET /api/export/contacts.csv`
- Implement `GET /api/export/contacts.json`
- Add summary stats response for UI
- Add sort options (email asc/desc, first_seen, last_seen)
- Add filters (domain, source folder/category, validation status)
- Add CSV injection-safe export formatting
- Add streamed export response for larger datasets
- Add deterministic filename format with timestamp
- Add export audit log entry (who, when, row count, format)
- Add endpoint tests for pagination/filter/export correctness

Deliverable:
- Processed email IDs can be viewed and exported via API.

---

## Phase 6 - Frontend Pilot UI
- Add app routes/pages (dashboard, connect, sync, contacts)
- Integrate API client and query state
- Build contacts table and search/filter basics
- Add export buttons (CSV/JSON)
- Add explicit connect/sync state banners (not connected, in progress, failed)
- Add retry actions in UI for failed sync/export
- Add lightweight toaster/alert system for API errors
- Add client-side validation for search/filter params
- Add empty states and loading skeletons/spinners
- Add frontend smoke tests for key user flow
- Keep UX to minimum viable screens for solo delivery

Deliverable:
- End-to-end pilot flow is usable in browser.

---

## Phase 7 - Reliability and Hardening
- Add retries for Gmail API transient failures
- Improve error handling and user-facing messages
- Add run logs and sync progress status
- Add smoke tests for critical flows
- Add timeout and circuit-breaker style guardrails per sync run
- Add rate-limit aware retry policy with jitter
- Add structured logs with sync job IDs and mailbox context
- Add health/readiness checks for API + DB + OAuth config
- Add backup/restore script for SQLite pilot data
- Add security pass (secret handling, token-at-rest checks, dependency audit)
- Add manual disaster recovery checklist

Deliverable:
- Pilot is stable for team usage and demo.

---

## Phase 8 - UAT and Release Readiness
- Run full mailbox test
- Validate output quality and dedupe behavior
- Verify OAuth reconnect and token refresh behavior
- Finalize docs and rollout checklist
- Run test matrix on small/medium/large mailbox samples
- Capture known limitations and deferred post-pilot backlog
- Freeze release tag and changelog for first pilot cut
- Record demo script and validation evidence (screenshots/logs)
- Prepare rollback plan and issue triage template
- Define week-1 post-release monitoring checklist

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

---

## Solo Builder Focus (Important override)

Because current execution is solo, prioritize the smallest end-to-end slice first:
1. Phase 1 minimal scaffold
2. Phase 2 core backend boot
3. Phase 3 OAuth happy path
4. Phase 4 extraction happy path
5. Phase 5 export endpoints
6. Phase 6 minimal UI (connect + sync + list + export)
7. Phase 7/8 hardening and UAT

Defer nice-to-have tasks unless they block pilot acceptance.

---

## Suggested Additional GitHub Issues To Create

1. API contract freeze and versioning notes
2. OAuth callback security (`state`) validation
3. Gmail quota/rate-limit backoff strategy
4. Parser edge-case test suite for header normalization
5. Export security (CSV injection prevention)
6. Sync job observability and structured logs
7. End-to-end smoke test automation
8. Pilot release checklist and rollback playbook
