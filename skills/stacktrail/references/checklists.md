# StackTrail Checklists

Use these checklists as targeted reminders while working inside real application projects. Do not load them as a substitute for reading the actual code and project memory.

## Cross-Layer Feature Checklist

- Restate the request as a business action, data source, UI/API interaction, and output.
- Identify whether the task is frontend only, backend only, database only, deployment only, or cross-layer.
- Trace the path from UI to API helper/client to route/controller to DTO/schema to service/use-case to repository/mapper to storage and back.
- Confirm HTTP method, route, parameter names, auth location, response shape, pagination/count, and frontend field usage.
- Implement the smallest complete path that preserves current contracts.
- Verify the touched layers with compile/build/tests/smoke checks.
- Update project memory with durable facts and useful mistake lessons after completion.

## Frontend And API Contract

- Inspect frontend API helpers or HTTP clients before renaming or moving backend endpoints.
- Check whether auth is sent in headers, cookies, query strings, local storage, or a mixed compatibility style.
- Preserve existing request and response shapes unless the task is explicitly contract cleanup.
- Remember that a successful frontend build does not prove the backend API works.
- Restart or rebuild the frontend when proxy, base URL, public path, or environment config changes.
- For file downloads, make the frontend request a blob/stream when the backend writes raw bytes.
- For uploads, verify `multipart/form-data`, file size limits, storage directory, and returned URL/path shape.

## Backend Layering

- Keep request types, response types, persistence entities, services, and data access separated according to local convention.
- Keep route/controller code thin: map requests, call services/use-cases, return responses.
- Keep business orchestration in services/use-cases.
- Keep SQL-heavy or query-heavy work in the project's established data-access layer.
- Use the project's existing exception and response conventions.
- Preserve unified JSON wrappers for ordinary JSON APIs when the project uses them.
- Do not wrap streamed downloads in a normal JSON response wrapper.

## Data Modeling

- Use master/current tables for current state.
- Use ledger/log/history tables for events that happened in the past.
- Store snapshot fields in ledger rows when historical truth must survive later master-data edits.
- Do not rewrite historical ledger rows after names, units, locations, or models change.
- For statistics, decide source data, date range, grouping field, aggregation field, and top-N rule before coding.
- For sharded or monthly tables, create or route tables through a consistent service/data-access pattern.
- Validate generated table names with a strict whitelist or regex before string substitution in SQL.
- Remember that DDL may have transaction implications; do not assume schema creation rolls back like normal row changes.

## Deployment Troubleshooting

- Check ports and processes before changing config.
- Check logs before guessing: application output, request logs, data/service logs, reverse proxy logs, and service manager logs.
- Separate local development paths from server/container/production paths.
- Configure upload directories, log directories, cache hosts, database hosts, public URLs, and active profiles/environments.
- Confirm the exact runtime command and active environment/profile.
- Distinguish package-manager-installed service paths from manually/source-installed service paths.
- Treat commands that disable protections or kill broad process groups as diagnostic or temporary unless the user explicitly chooses a permanent operations change.

## Error Reflection

- Capture important mistakes, not just successful decisions.
- Record misunderstood requirements, wrong-layer edits, broken API contracts, failed commands, deployment guesses, stale build artifacts, and regressions when they teach a reusable lesson.
- Convert each mistake into a durable note with `Symptom`, `Cause`, `Fix`, and `Rule`.
- Keep raw logs and long stack traces out of project memory unless a short excerpt is necessary.
- Do not blame the tool or user. Record the operational lesson future agents can use.

## Common Mistakes

- Treating a visible UI request as frontend-only before checking the backend/data path.
- Changing backend route names without checking frontend API helpers.
- Replacing local project patterns with heavier frameworks for small fixes.
- Mixing current state with historical ledger/log data.
- Storing binary file data in ordinary business JSON or tables when paths/URLs are enough.
- Writing large query strings in the wrong layer instead of the established data-access layer.
- Using relative upload/log paths that depend on the process working directory.
- Forgetting old build artifacts can mask current source config.
- Mislabeling timing logs as raw SQL/database logs.
- Updating project memory with narrative history instead of durable, actionable facts and mistake lessons.
