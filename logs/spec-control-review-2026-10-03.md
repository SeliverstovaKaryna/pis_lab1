# SPEC-CONTROL Review

## Sports Activity Control Information System

| Field | Value |
|---|---|
| Author | user12345 |
| Review Date | 2026-10-03 |
| Review Type | Independent control review of requirements specification |
| Reviewed Artifacts | `spec/srs.md`, `spec/traceability_matrix.md`, `spec/concept.md`, `docs/exercise-catalog.md`, `logs/sked-dialogue-2026-10-03.md` |
| Result | FAILED |

---

## Review Summary

The specification is not ready to be treated as a controlled baseline. The current SRS contains several useful updates from the dialogue, but traceability and acceptance coverage are inconsistent with the current requirements. Some confirmed decisions exist only in dialogue logs and have not yet been reflected in the SRS.

---

## Blocking Findings

| ID | Finding | Evidence | Required Action |
|---|---|---|---|
| CR-001 | The traceability matrix is outdated and contradicts the current glossary and SRS wording. | `spec/traceability_matrix.md` still uses "спортивна справа", "назва вправи", "дата в майбутньому", "вивід", and active 2s/1s performance requirements, while `spec/srs.md` now uses Activity Entry, fixed Exercise Catalog, current-date-only rule, display terminology, and deferred performance requirements. | Update `spec/traceability_matrix.md` to match current SRS requirement wording. |
| CR-002 | `REQ-F-003` exists in SRS but is missing from the traceability matrix. | `spec/srs.md` contains `REQ-F-003`, while `spec/traceability_matrix.md` jumps from `REQ-F-002` to `REQ-F-004`. | Add `REQ-F-003` to the traceability matrix. |
| CR-003 | The SRS process rule requires test coverage for every functional requirement, acceptance criterion, and BDD scenario, but the matrix leaves all test links as `TBD`. | `spec/srs.md` section 6 requires coverage; `spec/traceability_matrix.md` has `TBD` in the Test column for all rows. | Either mark this as planned pre-implementation coverage or add planned test IDs for each requirement. |
| CR-004 | Confirmed October decisions are not fully reflected in SRS. | `logs/sked-dialogue-2026-10-03.md` confirms account features out of scope, desktop-only UI, English UI, permanent delete without confirmation, simultaneous summary filters, and per-exercise plus daily total summaries; SRS only partially captures these. | Add or revise SRS requirements and constraints for all confirmed decisions. |

---

## Major Findings

| ID | Finding | Evidence | Required Action |
|---|---|---|---|
| MA-001 | SRS contains unresolved branch/merge prose at the top of the document. | `spec/srs.md` begins with non-requirement text before and after the title. | Remove branch/merge artifacts from the controlled SRS. |
| MA-002 | Document status is ambiguous. | Metadata says `Draft — затверджено в ітеративному SKED-діалозі`; the current review result is failed and newer decisions were added after the document date. | Set a clear status such as `Draft — under review` or update version/date after corrections. |
| MA-003 | Open decisions conflict with fixed SRS requirements. | `logs/sked-dialogue-2026-10-03.md` keeps `HTTP 403` and bcrypt as open items, while SRS already states them as requirements. | Confirm whether `HTTP 403` and bcrypt cost `>= 10` are accepted requirements or still open questions. |
| MA-004 | Summary behavior is underspecified in SRS. | SRS mentions day/week/month/year summary but does not fully define simultaneous filters, inclusive period boundaries, per-exercise totals, and total daily activity minutes. | Expand `REQ-F-023` or add separate requirements for summary filtering and output structure. |
| MA-005 | Edit validation is underspecified. | SRS allows editing own records but does not explicitly state that the same validation rules apply on edit as on create. | Add a requirement that edit operations must enforce Exercise Catalog, duration, date, ownership, and notes constraints. |
| MA-006 | Account model lacks uniqueness and credential validation rules. | SRS states registration with users but does not specify whether login is unique, allowed length/format, or behavior for duplicate login. | Add registration validation rules and acceptance criteria for duplicate login and invalid credentials. |

---

## Medium Findings

| ID | Finding | Evidence | Required Action |
|---|---|---|---|
| ME-001 | Notes are defined in the glossary and constraints but not represented as a functional requirement. | SRS section 7.2 has required Exercise, Duration, and Performed Date, but no requirement for optional Notes with 1000-character limit. | Add a Notes requirement or explicitly keep it as a constraint only. |
| ME-002 | The UI language requirement is absent from SRS. | Dialogue confirms all UI text is English; SRS does not state this. | Add a nonfunctional/UI constraint for English-only UI. |
| ME-003 | Desktop-only support is absent from SRS. | Dialogue confirms only desktop version is required at this stage; SRS says only "web interface". | Add target device/browser scope. |
| ME-004 | Delete behavior is incomplete. | Dialogue confirms permanent delete without confirmation or recovery; SRS only says the system allows deletion. | Add delete behavior and acceptance criteria. |
| ME-005 | Sort order for record lists is not defined. | SRS requires displaying all records but does not define default order. | Define default sorting, for example by performed date descending and creation time descending. |
| ME-006 | Date input behavior remains unresolved. | The system allows only current date, but it is still open whether the create form shows a fixed date field or assigns it automatically. | Resolve or keep as explicit open item outside the baseline. |

---

## Traceability Coverage Check

| Requirement Area | Status |
|---|---|
| User registration/login | Partially covered; missing acceptance criteria for duplicate login, wrong password, and unauthenticated access exception for login/register pages. |
| User data isolation | Partially covered; ownership rule and HTTP 403 exist, but open decision status must be resolved. |
| Activity Entry creation | Partially covered; current date, duration, and catalog rules exist, but Notes and edit validation require clearer traceability. |
| Activity Entry display/filtering | Partially covered; search behavior is defined, but sorting and summary filter details are incomplete. |
| Activity Summary | Under-specified; day/week/month/year exists, but output structure and filter combination need requirements and AC. |
| Edit/delete | Partially covered; permanent delete and no confirmation are not yet in SRS. |
| Nonfunctional requirements | Inconsistent; performance is deferred, security requirements need confirmation. |

---

## Gate Decision

The specification fails the independent control review. The next correction pass should update the traceability matrix first, then revise the SRS so that every confirmed SKED decision is either represented as a requirement/constraint or explicitly listed as an open item.

