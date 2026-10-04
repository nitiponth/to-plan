# Output contract

Use the following structure as a compact starting point, not a request to fill empty sections. Replace example placeholders with the actual decisions. Spec and plan form one handoff; do not duplicate the complete requirements in both.

## spec.md

```markdown
# <Feature> — Spec

Implementation plan: [plan.md](plan.md)

## Goal and problem
<Who needs what behavior, and why.>

## Required behavior and constraints
<Normal flow, required failure behavior, compatibility, and exact agreed values.>

## Acceptance criteria
- AC-01: <Observable input/action and expected result.>

## Out of scope
<Meaningful exclusions that prevent accidental extra work.>

## Decisions and testing seams
<Agreed architecture, domain terms, important defaults and reasons.>
<Which existing public seam proves each behavior and why it reaches the real case.>
<For each seam: proposed or user-confirmed; cite actual confirmation if present.>

## Open decisions
<Questions blocking the plan, or “None”.>
```

## plan.md

```markdown
# <Feature> — Implementation Plan

Spec: [spec.md](spec.md)
Executor: Matt Pocock's implement
Plan readiness: <ready | blocked, with reason>
Implementation authorization: <not requested | granted by explicit instruction>

## Repository context
- Branch and inspected revision: <observed values, or unavailable with reason>
- Relevant uncommitted changes: <observed state>
- Working directory for commands: <repo-relative>
- Runtime/test tooling: <from actual config; no machine-specific executable paths>
- Existing conventions and instructions: <short references>
- Existing checks run while planning: <command, observed result; or not run>

## Agreed contracts and constraints
<Define shared signatures/data shapes once, if needed. Reference spec constraints.>

## Tasks

### T-01: <Deliverable>
- Covers: AC-01
- Blocked by: None
- Files: Modify `<existing path>` at `<symbol>`; Create `<new path>`; Test `<test path>`
- Consumes / produces: <exact shared interfaces or reference to contract above>

Coverage cases: <name, setup/input and expected assertion for each needed behavior>.

For each case, complete this cycle before writing the next behavior test:
1. Write <one test name> at <confirmed seam>, with <input/setup> asserting <exact required behavior>.
2. Run `<targeted command>` from <directory>. For missing behavior, expect <target failure>. If the required behavior already passes, record regression evidence and skip the unnecessary fix; do not manufacture a failure.
3. When needed, make <specific change with settled approach and values>.
4. Run `<targeted command>`. Expected: <same behavior assertion passes>.
5. Run <other checks justified by this change>; record actual results in Progress.

<Use TDD steps for testable behavior. For tasks that do not benefit from that shape,
write appropriate steps and an evidence-producing check rather than fake tests.>

## Coverage and final verification
| Criterion | Task | Behavior check |
|---|---|---|
| AC-01 | T-01 | <test/observable check> |

<Actual full-suite/typecheck commands; compatibility/integration checks if needed.>
<Important review focus that tests cannot fully cover.>

## Progress
Implementation-start branch/revision: Not started

| Task | Status | Evidence / commands / result | Deviation and reason |
|---|---|---|---|
| T-01 | Not started | — | — |

## Implementation-session preflight
- Locate and read the installed Matt `implement`, `tdd`, and `code-review` skills.
- Check configuration required by their installed versions, including issue-tracker
  configuration if required. Supply this spec explicitly to the review.
- Confirm proposed testing seams with the user before writing tests. Reuse actual
  prior user confirmation when recorded; do not ask the same question again.
- If something is unavailable, identify it and ask how to proceed; do not silently
  substitute another workflow or claim a Matt review ran. Do not install implicitly.
- Confirm the intended checkout/branch and record the implementation-start revision
  before editing. Inspect relevant drift from the planning revision and any existing
  working-tree changes. Preserve unrelated user work.
- Set a review baseline for the entire work, not just the most recent task/commit.
- Matt's pinned code-review uses `<baseline>...HEAD`, which omits pending changes.
  For review-before-final-commit, supply this explicit diff override: stage only this
  work's new files when authorized, then use `git diff <implementation-start-revision>`
  plus `git log <implementation-start-revision>..HEAD --oneline` and the file list.
  This includes tracked staged/unstaged edits and earlier feature commits. Exclude
  unrelated pre-existing user changes; never stage them merely to collect the diff.
  Preserve both Standards and Spec review axes. If this override cannot be honored,
  report the incompatibility and agree an alternative instead of claiming success.

## Copyable handoff
Use Matt implement to execute this plan, reading the linked spec first. The spec
controls behavior and scope; the plan controls sequence and agreed implementation
details. Start with the implementation-session preflight. Work in dependency order
and use TDD at user-confirmed seams, completing one behavior test and its run/change/rerun
cycle before writing the next test. Observe the target failure for missing behavior;
record already-green compatibility cases as regression evidence without forcing a change.
Update Progress with completed tasks, commands,
results, and deviations so another session can resume from evidence.

Recheck relevant repository changes since the planning revision. Record routine
adjustments with reasons. Ask before changing agreed behavior, scope, or architecture;
do not silently resolve contradictory requirements. Report missing tools or access.

Run applicable typechecks, targeted tests, and the final suite. Give code-review both
spec.md and plan.md, plus the implementation-start baseline. Use the preflight's
explicit working-tree diff override when commits are pending; an empty committed diff
does not prove uncommitted work was reviewed. Include this work's new files without
including unrelated user edits. Fix actionable findings and verify fixes
before the final commit. Follow the user's branch/commit instructions. Stop after the
requested implementation; this handoff does not authorize push, merge, or deployment.
```

Localize the headings and handoff prose to the user's language when appropriate.
Keep the readiness and authorization meanings distinct even when labels are translated.
An unresolved design may have a useful partial plan, but its handoff must explicitly
say not to start the blocked work before those decisions are answered.
