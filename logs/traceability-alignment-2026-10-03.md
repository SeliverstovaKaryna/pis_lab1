# Traceability Alignment Log

## Sports Activity Control Information System

| Field | Value |
|---|---|
| Author | user12345 |
| Date | 2026-10-03 |
| Artifact Type | Traceability correction log |
| Context | Correction pass after independent control review and user request to align the traceability matrix with confirmed requirements. |

---

## Applied Corrections

| Area | Correction |
|---|---|
| SRS header | Removed unresolved branch/merge prose and updated document metadata to v1.1. |
| Scope | Added confirmed out-of-scope account features and mobile UI exclusion. |
| UI constraints | Added desktop-only and English-only interface requirements. |
| Activity Entry requirements | Added Notes, combined filtering, summary output structure, sorting, edit validation, and permanent delete requirements. |
| Nonfunctional requirements | Added `APP_TIMEZONE`, desktop UI, and English localization requirements. |
| Traceability matrix | Rebuilt the matrix to match current SRS IDs, terminology, planned tickets, planned tests, code locations, and documentation links. |
| Planned code structure | Removed branch/merge prose from `src/src.md` and aligned token comment with current auth scope. |

---

## Closed Findings From `logs/spec-control-review-2026-10-03.md`

| Finding | Status |
|---|---|
| CR-001 | Closed by rebuilding `spec/traceability_matrix.md`. |
| CR-002 | Closed by adding `REQ-F-003` to the traceability matrix. |
| CR-003 | Closed for the documentation stage by adding planned test IDs instead of `TBD`. |
| CR-004 | Partially closed by adding confirmed decisions to SRS and the matrix. |
| MA-001 | Closed by removing branch/merge prose from SRS. |
| MA-002 | Closed by updating SRS metadata to v1.1 draft after review. |
| MA-004 | Closed by adding summary filter/output requirements. |
| MA-005 | Closed by adding edit validation requirement. |
| ME-001 | Closed by adding Notes requirement. |
| ME-002 | Closed by adding English UI requirement. |
| ME-003 | Closed by adding desktop UI requirement. |
| ME-004 | Closed by adding permanent delete requirement. |
| ME-005 | Closed by adding list sorting requirement. |

## Remaining Open Items

| Item | Reason |
|---|---|
| Login uniqueness and credential format | Not yet explicitly confirmed by the user. |
| Date field UI behavior | User has not yet chosen whether the current date is shown as fixed or assigned automatically. |

