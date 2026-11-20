## What this changes

<!-- One or two sentences. Link the ticket. -->

### The change

- [ ] The pull request does one thing. Unrelated changes are split out.
- [ ] I can explain every line of the diff. Nothing was merged just because an agent wrote it.
- [ ] Acceptance criteria from the ticket are met and listed in the description.

### Tests

- [ ] New behavior has tests that would fail if the behavior broke.
- [ ] Bug fixes include a test that reproduces the bug.
- [ ] The full test suite passes locally or in CI. No tests were skipped or deleted to get there.
- [ ] No sleeps or timing-dependent tests were added.

### Safety

- [ ] No secrets, tokens or credentials in code, config, tests or logs.
- [ ] No personal or customer data written to logs.
- [ ] Inputs from users or other services are validated.
- [ ] Database migrations are reversible or have a written rollback plan.
- [ ] Risky behavior is behind a feature flag where the team uses flags.

### Operability

- [ ] Errors are logged once, at the right level, with a request or trace ID.
- [ ] No new log lines in hot paths at info level or above.
- [ ] New configuration has a default and is documented.

### Slop filter

- [ ] The diff passes every item in `gates/slop-filter.md`.

### Docs

- [ ] README, runbook or API docs are updated if behavior, setup or configuration changed.
