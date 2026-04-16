# Issue Execution Order (Serial + Issue Number)

Use this strict sequence for solo execution.

1. **#1** Phase 0: Project initialization
2. **#2** Phase 1: Google Cloud and OAuth setup
3. **#21** Environment and secrets management baseline
4. **#23** API documentation and response contract
5. **#11** API contract freeze and versioning notes
6. **#20** Database schema finalization and Alembic initial migration
7. **#12** OAuth callback security (`state`) validation
8. **#3** Phase 2: Build core Gmail extractor
9. **#4** Phase 3: Add deduplication and sync state
10. **#13** Gmail quota and rate-limit backoff strategy
11. **#14** Parser edge-case test suite for header normalization
12. **#5** Phase 4: Implement CSV and JSON export
13. **#15** Export security: CSV injection prevention
14. **#6** Phase 5: Add filtering and quality controls
15. **#19** Frontend MVP implementation (Connect -> Sync -> Contacts -> Export)
16. **#7** Phase 6: Reliability and error handling
17. **#16** Sync job observability and structured logs
18. **#17** End-to-end smoke test automation
19. **#22** CI pipeline: lint and test checks
20. **#8** Phase 7: Scheduling and maintenance
21. **#9** Final validation: End-to-end run and output audit
22. **#24** UAT sign-off checklist and evidence pack
23. **#18** Pilot release checklist and rollback playbook

---

## Quick Start

Start with: **#1 -> #2 -> #21**.

Do not open a new implementation thread until the current issue acceptance criteria is complete.
