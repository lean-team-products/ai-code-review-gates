# Slop filter

AI agents write code fast. These are the mistakes they make most often. Check every AI-assisted diff against this list before it merges.

| # | Slop pattern | How to spot it | What to do |
|---|---|---|---|
| 1 | **Invented APIs** | Calls to functions, methods, flags or packages that don't exist in your dependency versions | Search the codebase and the library's docs for each unfamiliar call. Delete or replace anything you can't find. |
| 2 | **Duplicate helpers** | A new utility that does what an existing one already does | Search for similar names and logic. Reuse the existing helper. |
| 3 | **Narrating comments** | Comments like `// increment counter` or `# loop through users` | Delete them. Keep only comments that explain why. |
| 4 | **Dead code** | Unused imports, variables, parameters, functions or commented-out blocks | Delete. Run the linter's unused-code checks. |
| 5 | **Scope creep** | Reformatted files, renamed variables or "improvements" unrelated to the task | Revert everything outside the task. |
| 6 | **Swallowed errors** | Empty `catch` blocks, `except: pass`, or errors logged and then ignored | Handle the error, rethrow it, or document why ignoring it is safe. |
| 7 | **Fake tests** | Tests with no assertions, tests that assert a mock was called and nothing else, or tests that mirror the implementation | Rewrite them to assert observable behavior. |
| 8 | **Hard-coded values** | Magic numbers, URLs, file paths or credentials inline | Move to configuration or named constants. |
| 9 | **Over-engineering** | New interfaces, factories or abstraction layers for a single use | Inline it. Abstract when there is a second real use. |
| 10 | **Confident wrong summaries** | The agent says tests pass or a bug is fixed but shows no output | Re-run the command yourself and read the output. |
| 11 | **Dependency drift** | New packages added for small tasks, or versions bumped without reason | Remove them unless the team agrees the dependency is worth it. |
| 12 | **Silent behavior changes in "refactors"** | Changed defaults, error messages, log lines or ordering inside a refactor | Split behavior changes into their own commit with a test. |

## The one-question test

Before merging, ask: **"Would I be comfortable defending this diff in review if I had written every line myself?"** If not, it isn't ready.
