# Private Query Configuration — LOCAL ONLY

Copy this file to `inputs/query-config.local.md` and fill in values **locally**.
Do not commit `inputs/query-config.local.md` or real internal Jira/Zephyr URLs or identifiers.

## Report: hc_uk_ideation_v2
- ZQL: TODO — exact test cycle and fixVersion for this report
- JQL: TODO — outstanding bugs query scoped to this report
- Jira dashboard URL: TODO (optional)

## Query syntax

ZQL contains the query expression only; `offset`, `maxRecords`, and `expand=executionStatus` are API parameters.
For every report, obtain all pages, deduplicate executions by stable execution ID, verify totals, and report incomplete results rather than publishing them as final.
Do not reuse one cycle's execution results for a different environment/purpose without explicit mapping.
