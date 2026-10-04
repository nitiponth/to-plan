# to-plan

Turn a software discussion, requirements, or an existing design into a portable `spec.md` and `plan.md` pair. The documents provide the context, decisions, task order, interfaces, and verification steps needed by an agent in a new session, with a handoff tailored to Matt Pocock's `implement` skill.

## Install

Install into your current project with the [Skills CLI](https://github.com/vercel-labs/skills):

```sh
npx skills add nitiponth/to-plan --skill to-plan
```

Add `--global` to install for your user account instead. The CLI lets you select which supported agents receive the skill.

To list the available skill without installing it:

```sh
npx skills add nitiponth/to-plan --list
```

## Use

Ask your agent to use `to-plan` with your feature discussion or requirements and the relevant repository. For example:

```text
Use to-plan to plan this feature from our discussion and the current repository.
Inspect the code and test conventions before asking unresolved product questions.
Write a spec.md and plan.md pair for handoff to Matt implement in a new session.
```

By default, the documents go in `docs/plans/<feature-slug>/`. An explicit location or an established repository convention takes precedence. Document prose follows your language; code identifiers and commands retain their repository spelling.

The skill creates:

- **spec.md**: intended behavior, scope, constraints, acceptance criteria, design decisions, testing seams, and unresolved questions.
- **plan.md**: tasks, dependencies, concrete file locations, shared interfaces, tests, verification commands, coverage, progress, and a copyable implementation handoff.

The spec is the authority for behavior and scope. The plan supplies the implementation details and sequence. An unresolved product decision keeps the plan blocked. Plan readiness and authorization to implement are recorded separately.

## Implement in another session

Give the receiving agent the repository, both documents, and the handoff at the end of `plan.md`. It checks the current code against the inspected revision, follows task dependencies, records progress and verification evidence, and supplies both documents plus the implementation-start revision to code review.

The planning skill is self-contained. The receiving implementation session needs Matt Pocock's `implement`, `tdd`, and `code-review` skills and the configuration required by their installed versions. Those skills are not bundled here. See [Matt Pocock's skills](https://github.com/mattpocock/skills).

`to-plan` stops after planning. It does not implement application code, publish tracker tickets, install skills, commit, or push as part of its workflow.

## Validation and limits

The current skill was evaluated on three small Python CLI planning cases with independent agents reading the resulting handoffs. That evaluation checked plan completeness and fresh-session comprehension; it did not execute the planned features or Matt's implementation workflow. It does not establish performance for particular Opus or Luna models, or superiority over a complete `to-spec` plus `writing-plans` workflow. Small tasks can produce more documentation than necessary.

## Sources and license

The skill adapts planning ideas from Matt Pocock's `to-spec` and `to-tickets`, and Jesse Vincent's Superpowers `writing-plans`. Anthropic's `skill-creator` supported development and evaluation; its tools are not bundled.

See [attribution](skills/to-plan/ATTRIBUTION.md), [pinned sources](skills/to-plan/sources.json), and [upstream MIT notices](skills/to-plan/LICENSES.txt). Original contributions are available under the [MIT license](LICENSE).
