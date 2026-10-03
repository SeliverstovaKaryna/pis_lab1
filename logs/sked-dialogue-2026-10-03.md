# SKED Dialogue Log

## Sports Activity Control Information System

| Field | Value |
|---|---|
| Author | user12345 |
| Date | 2026-10-03 |
| Artifact Type | Dialogue summary and requirements decision log |
| Context | Clarification of unresolved requirements before formal SRS update. |

---

## Confirmed Decisions

| Topic | Decision |
|---|---|
| Scope | The system stores activity history and calculates activity minutes. Existing inclusions and exclusions from SRS section 2 remain valid. |
| Activity Entry | One Activity Entry represents one performed Exercise. Complex multi-exercise sessions are out of scope. |
| Exercise names | Exercise names are selected from a fixed catalog and are written in English. |
| Exercise catalog | Users cannot add custom exercises. The initial fixed catalog is stored in `docs/exercise-catalog.md`. |
| Notes | Notes are optional. Empty string, spaces, and line breaks are allowed. Maximum length is 1000 characters. |
| Date rule | A record may be created only for the current date in the configured application time zone. Past and future dates are forbidden. |
| Time zone | The application time zone is configured with the `.env` variable `APP_TIMEZONE`. |
| Duration | Duration is required and must be an integer from 1 to 1440 minutes inclusive. |
| Weekly totals | A week is a calendar week from Monday to Sunday. |
| Monthly and yearly totals | Month and year totals are calendar-based. |
| Filtering | Exercise-name filtering uses case-insensitive substring matching. |
| Summary filters | Summary output supports simultaneous filtering by exercise name and by date or inclusive date period. |
| Summary output | Summary output includes minutes per exercise and total daily activity minutes. |
| Account access | Registration uses login and password. Only login and registration pages are available before authentication. |
| Account features | Logout, password recovery, and account deletion are out of scope. |
| Delete behavior | Delete is permanent. No confirmation and no recovery are required. |
| Interface language | All application UI text and exercise names are in English. |
| Target use | The system is intended for real use by a small number of users. Only desktop UI is required at this stage. |
| Performance requirements | The previous 2-second listing and 1-second saving requirements are deferred for now. |
| Current stage | The project is currently documenting requirements and planning code structure, not implementing the application. |

---

## Open Items

| ID | Question |
|---|---|
| OI-001 | Should direct editing/deleting of another user's record still return HTTP 403, or should unauthorized users be redirected/hidden from those routes at UI level only? |
| OI-002 | Should the date field be visible and fixed to today's date, or omitted from the create form and assigned automatically by the system? |
| OI-003 | Should the system keep the existing bcrypt cost requirement from the SRS while implementation details are otherwise deferred? |
