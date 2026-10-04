---
name: to-plan
description: Create a paired spec.md and detailed plan.md from a software discussion, requirements, or an existing design plus repository evidence. Use when preparing an implementation handoff to another agent or session, especially one that will use Matt Pocock's implement skill. Plan the work; do not implement it or publish tracker tickets.
---

# To Plan

Produce two portable documents that let a new implementer work without the original conversation. The spec owns the required behavior; the plan carries the decisions, interfaces, tests, and sequence needed to build it. Scale detail to the work, not to a fixed task count.

This planning skill is self-contained. Do not invoke `to-spec`, `to-tickets`, `writing-plans`, or their executors. Matt's `implement`, `tdd`, and `code-review` are dependencies of the later implementation session, not prerequisites for writing this plan.

## Ground the plan

1. Extract settled intent from the conversation and any supplied documents. Read referenced requirements and comments when accessible. Distinguish requirements from suggestions; surface contradictory requirements rather than choosing silently.
2. Inspect the repository's instructions, relevant code and callers, glossary, ADRs, test conventions, and configuration. Find existing seams before adding new ones. Record the inspected branch, revision, and relevant uncommitted changes; never invent a revision. Without a repo, explain which paths, interfaces, and commands remain unverified.
3. Look up environmental facts yourself. Ask only unresolved choices that materially change behavior, scope, or architecture. Do not restart an interview already settled in the conversation. Choose routine implementation details from repo conventions and record consequential defaults.

A product decision that blocks the design keeps the plan `blocked`; write the known parts and the specific question instead of filling the gap with an unsupported assumption. After the answer, reconcile both documents.

## Build the documents

Read [references/plan-template.md](references/plan-template.md) when drafting or revising the output. Follow its content contract while omitting irrelevant optional fields.

Use an explicit user location first, an established repo planning location second, and `docs/plans/<feature-slug>/` otherwise. Keep `spec.md` and `plan.md` together with relative links. Do not overwrite an unrelated existing feature. Revise existing documents for the same feature when requested.

Write prose in the user's language and preserve actual code identifiers, paths, and commands. Paths inside the documents are relative to the repository or document as labeled, not machine-specific absolute paths.

### Spec: what must be true

Capture the problem, intended behavior, scope exclusions, constraints, acceptance criteria (`AC-01`, etc.), agreed design decisions, testing seams, and any unresolved questions. Mark each testing seam as proposed or user-confirmed, citing the confirming instruction when present; a planner's recommendation is not user confirmation. A complete plan may await that execution preflight without an unresolved product design. Make criteria observable. Include required failure behavior and edge cases implied by the feature, not an exhaustive speculative catalogue. Keep specific edit locations and step sequences in the plan.

### Plan: how to get there

Break work into small deliverables with task IDs (`T-01`, etc.), real blocking dependencies, and links to acceptance criteria. Prefer narrow complete behavior slices. Include preparatory refactors only when the feature needs them. For wide refactors where isolated slices cannot remain green, explicitly plan a compatible migration or a final integration-and-verification gate; do not promise checks that cannot pass midway.

For each task specify:
- The deliverable, dependencies, and criteria it proves.
- Exact existing files to change and proposed new files, labeled distinctly; nearby symbols are more durable than line numbers.
- Interfaces consumed and produced, with agreed names, arguments, return/error behavior, and data formats where other tasks depend on them. Define shared contracts once and reference them.
- Ordered steps and meaningful behavior tests: test names, setup, input, and expected assertions. Use test code or compact pseudocode when that preserves a decision more precisely than prose; do not prewrite the whole implementation.
- Verification commands, working directory, and semantic pass/fail expectations. Ground them in the actual repo and shell; mark new test targets as future targets. Distinguish commands already run from instructions for later execution.

Decide the approach or algorithm when leaving it open would make the next agent redesign the feature. Leave ordinary idiomatic implementation freedom. Avoid empty directions such as "handle edge cases" or "add appropriate tests".

Record global constraints in the spec and reference them from the plan; do not maintain contradictory copies. Include a compact coverage map and final checks. Tests should exercise external behavior at the agreed seams, including relevant compatibility cases.

For tasks with several cases, list the cases as a coverage checklist but execute one behavior test -> run it -> minimal implementation if needed -> rerun at a time. Missing behavior should fail for the intended reason before its fix. If a valid compatibility test already passes because existing code or an earlier change provides the behavior, record it as regression evidence and continue; never manufacture a failure or promise every listed case will start red. Do not prescribe writing the whole task's test suite before implementing it; Matt's TDD loop is incremental, not a batch of imagined tests.

## Check and hand off

Review the pair against the repo and the settled intent:
- Every acceptance criterion has a task and evidence-producing check; no task invents extra scope.
- Dependencies are acyclic and reference real task IDs. Cross-task names, types, and data formats agree.
- Paths exist unless labeled new, commands fit the repository, and expected failures detect the target symptom rather than an unrelated environment error.
- No consequential decision is hidden behind a placeholder. A fresh session can identify the first task, its inputs, and the check that finishes it.

Keep two separate statements: `Plan readiness: ready | blocked` and `Implementation authorization: not requested | granted by <explicit instruction>`. Writing a complete plan never grants permission to execute it. Do not forget authorization already given in the session; this skill still stops after planning.

Use the template's copyable handoff with Matt `implement` as the selected executor. Include dependency/configuration and testing-seam confirmation preflight for the later session, repository-drift checks, a progress table, and a full-work review contract. Provide both documents and the implementation-start baseline to review. The pinned Matt review uses `<baseline>...HEAD`, which misses uncommitted work: carry the template's explicit working-tree diff instruction as a handoff override, preserving both review axes and review-before-final-commit. Include new files in the review. If the installed review tooling cannot cover the actual changes, report the limitation instead of claiming the review passed.

End by linking both documents, stating readiness and outstanding decisions, and presenting the handoff. Do not publish issues, install skills, edit application code, commit, push, or start an executor as part of `to-plan`.
