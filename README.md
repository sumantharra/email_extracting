# Gmail Email Extractor (Pilot) - Plain Overview

## What this project is

This is a planning repository for a pilot app.  
The goal is to help users who have a large Gmail inbox and want one clean list of email IDs.

## Problem we are solving

- Gmail accounts used for marketing/recruiting contain thousands of emails.
- Important contact email IDs are mixed with promotions, updates, and noise.
- Manual copy/paste is slow and error-prone.

## Proposed solution

Build a simple full-stack app that:
1. Connects securely to Gmail
2. Reads email header fields (sender/receiver IDs)
3. Removes duplicate email IDs
4. Shows the final list in a web page
5. Exports the list as CSV/JSON

## Pilot scope (first version)

### Included
- Gmail connection (secure Google sign-in permission)
- Email ID extraction from Inbox/Sent (optional Promotions/Updates)
- Duplicate removal
- Basic UI to review results
- Export options (CSV/JSON)

### Not included in pilot
- Automatic classification (vendor/recruiter/client)
- Multi-account support
- Advanced analytics

## Current repo status

- This repo currently contains planning docs only:
  - `ARCHITECTURE.md`
  - `TASKS.md`
- Implementation starts after TL review and approval.
- GitHub issues and milestones are already created for execution.

## Software needed later (for implementation)

- Git
- Python 3.11+
- Node.js 20+ and npm

## Quick glossary (non-technical)

- **OAuth**: secure Google permission flow (without sharing Gmail password)
- **API**: a way for two apps/systems to talk
- **Deduplication**: removing repeated/duplicate email IDs
- **Pilot**: first practical version for testing with the team

