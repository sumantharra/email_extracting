# Gmail Email Extractor - Pilot Architecture (Plain Language)

## 1) Goal

Create a pilot web app that helps users pull all unique email IDs from Gmail and download them as a file.

## 2) What the user will do

1. Open the app
2. Connect Gmail securely
3. Click sync
4. See a clean list of unique email IDs
5. Export the list as CSV or JSON

## 3) What the system will do behind the scenes

- Read email header fields (like sender/receiver)
- Collect email IDs from those fields
- Remove duplicates
- Save results in a local database
- Serve results to the UI
- Generate downloadable files

## 4) High-level architecture

```text
[ Web UI (Frontend) ]
        |
        v
[ Backend API ]
   |       \
   |        \--> [ Export Generator ]
   |
   +--> [ Gmail OAuth + Gmail API ]
   |
   +--> [ Local Database (SQLite) ]
```

## 5) Main parts and responsibility

### Frontend (what users see)
- Connect Gmail button
- Start sync button
- Results table
- Export buttons (CSV/JSON)

### Backend (business logic)
- Handles Gmail connect/callback flow
- Runs extraction process
- Stores and reads extracted IDs
- Exposes APIs for UI and export

### Database
- Stores unique email IDs
- Tracks processed message IDs to avoid duplicates on rerun

## 6) Pilot scope

### Included
- Gmail connection
- Email ID extraction
- Duplicate removal
- UI review page
- CSV/JSON export

### Not included now
- Vendor/recruiter/client auto-classification
- Multi-account support
- Advanced analytics and enrichment

## 7) Data flow (simple)

1. User connects Gmail
2. App gets permission via Google OAuth
3. App reads selected mailbox categories
4. App extracts IDs from headers
5. App removes duplicates and stores clean list
6. User views and exports results

## 8) Current repository status

- Docs-first state for review:
  - `README.md`
  - `ARCHITECTURE.md`
  - `TASKS.md`
- Implementation starts after approval.

## 9) Done criteria for pilot

- App connects to Gmail successfully
- Sync extracts unique email IDs
- IDs are visible in UI
- CSV and JSON downloads work
