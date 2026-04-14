# Gmail Email Extractor - End-to-End Project Blueprint

## 1) Purpose of this file

This document is the complete implementation blueprint for the full-stack pilot project.  
It explains:
- what the architecture looks like
- what files/folders will be created
- in what order they will be created
- how the final project tree will look

This is a planning document only.

---

## 2) Project goal (pilot)

Build a full-stack app that:
1. Connects Gmail securely (Google OAuth)
2. Scans email headers from selected categories
3. Extracts and deduplicates email IDs
4. Shows results in a web UI
5. Exports results to CSV and JSON

---

## 3) High-level architecture

```text
[ React Frontend ]
       |
       v
[ FastAPI Backend ] -----> [ Export Service ]
       |
       +-----> [ Gmail OAuth + Gmail API ]
       |
       +-----> [ SQLite Database ]
```

### Simple data flow
1. User clicks Connect Gmail in frontend.
2. Backend completes OAuth and stores token.
3. User starts sync.
4. Backend fetches Gmail messages in batches.
5. Backend extracts email IDs from headers.
6. Backend removes duplicates and stores results.
7. Frontend shows results table.
8. User exports CSV/JSON.

---

## 4) Implementation phases and files created

## Phase 0 - Base setup

Files:
- `README.md`
- `ARCHITECTURE.md`
- `TASKS.md`
- `PROJECT_BLUEPRINT.md`
- `.gitignore`
- `.env.example`
- `requirements.txt`

## Phase 1 - Backend scaffold

Folders:
- `backend/app/api/routes/`
- `backend/app/core/`
- `backend/app/db/`
- `backend/app/models/`
- `backend/app/schemas/`
- `backend/app/services/`
- `backend/app/workers/`
- `backend/alembic/`

Files:
- `backend/requirements.txt`
- `backend/.env.example`
- `backend/app/main.py`
- `backend/app/core/config.py`
- `backend/app/core/security.py`
- `backend/app/db/session.py`
- `backend/app/db/base.py`
- `backend/app/api/routes/health.py`
- `backend/app/api/routes/auth.py`
- `backend/app/api/routes/gmail.py`
- `backend/app/api/routes/sync.py`
- `backend/app/api/routes/contacts.py`
- `backend/app/api/routes/export.py`

## Phase 2 - Backend data model

Files:
- `backend/app/models/user.py`
- `backend/app/models/gmail_account.py`
- `backend/app/models/sync_job.py`
- `backend/app/models/email_message.py`
- `backend/app/models/email_participant.py`
- `backend/app/models/contact.py`
- `backend/app/models/__init__.py`
- `backend/alembic.ini`
- `backend/alembic/env.py`
- `backend/alembic/versions/0001_initial.py`

## Phase 3 - Gmail integration and extraction

Files:
- `backend/app/services/gmail/oauth_service.py`
- `backend/app/services/gmail/gmail_client.py`
- `backend/app/services/gmail/sync_service.py`
- `backend/app/services/gmail/parser.py`
- `backend/app/services/contacts/deduper.py`
- `backend/app/services/contacts/extractor.py`

## Phase 4 - Export and API completion

Files:
- `backend/app/services/export/exporter.py`
- `backend/app/schemas/contacts.py`
- `backend/app/schemas/gmail.py`
- `backend/app/schemas/sync.py`
- `backend/app/schemas/export.py`

## Phase 5 - Frontend scaffold

Folders:
- `frontend/src/api/`
- `frontend/src/components/`
- `frontend/src/features/auth/`
- `frontend/src/features/gmail/`
- `frontend/src/features/sync/`
- `frontend/src/features/contacts/`
- `frontend/src/features/export/`
- `frontend/src/hooks/`
- `frontend/src/pages/`
- `frontend/src/store/`
- `frontend/src/types/`
- `frontend/src/utils/`

Files:
- `frontend/package.json`
- `frontend/tsconfig.json`
- `frontend/vite.config.ts`
- `frontend/index.html`
- `frontend/src/main.tsx`
- `frontend/src/App.tsx`
- `frontend/src/api/client.ts`

## Phase 6 - Frontend pages

Files:
- `frontend/src/pages/LoginPage.tsx`
- `frontend/src/pages/DashboardPage.tsx`
- `frontend/src/pages/ConnectGmailPage.tsx`
- `frontend/src/pages/SyncStatusPage.tsx`
- `frontend/src/pages/ContactsPage.tsx`
- `frontend/src/pages/ExportPage.tsx`
- `frontend/src/components/ContactsTable.tsx`
- `frontend/src/components/SyncProgress.tsx`

## Phase 7 - Runtime and deployment basics

Files:
- `docker-compose.yml`
- `backend/Dockerfile`
- `frontend/Dockerfile`
- `.env`

---

## 5) Final target folder tree

```text
email_extracting/
├── README.md
├── ARCHITECTURE.md
├── TASKS.md
├── PROJECT_BLUEPRINT.md
├── .gitignore
├── .env.example
├── requirements.txt
├── docker-compose.yml
│
├── backend/
│   ├── .env.example
│   ├── requirements.txt
│   ├── Dockerfile
│   ├── alembic.ini
│   ├── alembic/
│   │   ├── env.py
│   │   └── versions/
│   │       └── 0001_initial.py
│   └── app/
│       ├── main.py
│       ├── api/
│       │   └── routes/
│       │       ├── health.py
│       │       ├── auth.py
│       │       ├── gmail.py
│       │       ├── sync.py
│       │       ├── contacts.py
│       │       └── export.py
│       ├── core/
│       │   ├── config.py
│       │   └── security.py
│       ├── db/
│       │   ├── base.py
│       │   └── session.py
│       ├── models/
│       │   ├── user.py
│       │   ├── gmail_account.py
│       │   ├── sync_job.py
│       │   ├── email_message.py
│       │   ├── email_participant.py
│       │   ├── contact.py
│       │   └── __init__.py
│       ├── schemas/
│       │   ├── gmail.py
│       │   ├── sync.py
│       │   ├── contacts.py
│       │   └── export.py
│       ├── services/
│       │   ├── gmail/
│       │   │   ├── oauth_service.py
│       │   │   ├── gmail_client.py
│       │   │   ├── sync_service.py
│       │   │   └── parser.py
│       │   ├── contacts/
│       │   │   ├── extractor.py
│       │   │   └── deduper.py
│       │   └── export/
│       │       └── exporter.py
│       └── workers/
│           └── jobs.py
│
└── frontend/
    ├── package.json
    ├── tsconfig.json
    ├── vite.config.ts
    ├── Dockerfile
    ├── index.html
    └── src/
        ├── main.tsx
        ├── App.tsx
        ├── api/
        │   └── client.ts
        ├── components/
        │   ├── ContactsTable.tsx
        │   └── SyncProgress.tsx
        ├── pages/
        │   ├── LoginPage.tsx
        │   ├── DashboardPage.tsx
        │   ├── ConnectGmailPage.tsx
        │   ├── SyncStatusPage.tsx
        │   ├── ContactsPage.tsx
        │   └── ExportPage.tsx
        ├── features/
        │   ├── auth/
        │   ├── gmail/
        │   ├── sync/
        │   ├── contacts/
        │   └── export/
        ├── hooks/
        ├── store/
        ├── types/
        └── utils/
```

---

## 6) What this means for TL review

- This blueprint is the agreed structure for full-stack implementation.
- Team can estimate effort per phase/file group clearly.
- No code assumptions are hidden; all main files are listed upfront.
- After TL approval, implementation starts phase-by-phase from this file.
