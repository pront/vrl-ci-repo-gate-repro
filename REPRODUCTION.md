# Repository gate branch-protection reproduction

Source: vectordotdev/vrl pull request 2048, commit 471cd7d0865622a9dce597a1fb4d6c6be4b71fd8.

This test fork reproduces the Test Suite job graph, all four required test/vrl matrix check names, and the other required workflow aggregates. Its disposable target branch mirrors VRL's 12 required checks, GitHub Actions app binding, strict up-to-date checks, and administrator enforcement. Review approval requirements are omitted to isolate check enforcement.

The repository identity in the shared gate is adapted to this fork. Repository variable REPRO_GATE_FAIL injects an exit-1 failure only in the Test Suite gate. REPRO_CLIPPY_FAIL controls a separate required-check failure. Expensive build steps are replaced with no-ops; workflow triggers, names, dependencies, matrix definitions, runner labels, and aggregate checks are preserved. Unrelated workflows are removed from this test branch.

Scenarios:
1. Fresh pull request: the Test Suite gate fails before matrix jobs run.
2. Rerun: the matrix jobs pass, clippy fails, then the whole Test Suite is rerun at the same SHA with a failed gate.
3. Successful control, if needed to validate merge enforcement.

Only branches prefixed pront- in this test fork are pushed or merged. The original pull request and repository settings are unchanged.
