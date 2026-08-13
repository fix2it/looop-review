# Looop Review

Two interactive [Agent Skills](https://agentskills.io) for iterative review with a user-selected severity scope:

- `loop-code-review-3` reviews task-scoped active code changes.
- `loop-plan-review-3` reviews implementation plans and specifications.

Both skills ask how strict the review should be **before reading the target**, then use fresh independent reviewer agents and loop only on the selected classes of findings.

## Why

Powerful review models can spend substantial time and tokens on low-impact polish. Looop Review makes review depth an explicit product choice: search only for release blockers, include medium risks, or inspect every level when the situation warrants it.

## Severity levels

Each skill presents a domain-specific version of the same scale:

1. **Blockers** — work cannot safely proceed or be released.
2. **Critical** — catastrophic security, privacy, payment, or data-loss risk.
3. **Serious** — an important flow or implementation path is likely to fail.
4. **Medium** — meaningful edge cases, recovery, accessibility, performance, rollout, or validation gaps.
5. **Minor** — low-impact maintainability or clarity friction.
6. **Preferences / optional polish** — subjective style or alternative organization.
7. **All levels** — review levels 1 through 6.

For ordinary product work, levels `1-3` are the recommended practical default.

## Skills

### `loop-code-review-3`

Reviews only the active Git changes owned by the current task. It checks the selected severity levels across correctness, security, privacy, data integrity, UX, operational behavior, tests, architecture, reuse, and maintainability.

Unselected lower-severity findings do not reduce the score, trigger fixes, or cause another review round.

### `loop-plan-review-3`

Reviews a plan or specification for execution readiness at the selected severity levels. It verifies repository claims, ordering, dependencies, ownership, acceptance criteria, validation, rollout, rollback, and fallback behavior.

It keeps plans at the right altitude: runtime uncertainty becomes a hypothesis, early experiment, threshold, and fallback—not speculative implementation detail.

## Shared behavior

- Mandatory severity selection before reading or reviewing.
- Fresh independent reviewer context for every scoring pass.
- Reviewer reasoning effort exactly matches the orchestrator's effort.
- Exact runtime reviewer model is shown in every score row.
- Scoped scores: `9.5/10` applies only to the selected severity levels.
- At most five scoring passes by default; exhaustion is incomplete, not success.
- Score trajectory is shown in the user's language and mirrored to the Codex status line.
- Unmistakable catastrophic safety risks may be surfaced once even when outside the chosen scope.

## Install

Clone the repository:

```sh
git clone https://github.com/tablesguru/looop-review.git
cd looop-review
```

For Codex:

```sh
mkdir -p ~/.agents/skills
cp -R loop-code-review-3 loop-plan-review-3 ~/.agents/skills/
```

For Claude Code:

```sh
mkdir -p ~/.claude/skills
cp -R loop-code-review-3 loop-plan-review-3 ~/.claude/skills/
```

You can also install either folder at project scope using the skill directory supported by your agent runtime.

## Use

In Codex:

```text
$loop-code-review-3
$loop-plan-review-3 path/to/plan.md
```

In Claude Code:

```text
/loop-code-review-3
/loop-plan-review-3 path/to/plan.md
```

The skill first asks which severity levels to search and waits for an explicit answer.

## Repository structure

```text
looop-review/
├── loop-code-review-3/
│   ├── SKILL.md
│   └── agents/openai.yaml
├── loop-plan-review-3/
│   ├── SKILL.md
│   └── agents/openai.yaml
├── LICENSE
└── NOTICE.md
```

## Attribution and license

The code-review workflow is derived from Dima Sukharev's MIT-licensed [`loop-code-review-skill`](https://github.com/di-sukharev/loop-code-review-skill). See [NOTICE.md](NOTICE.md) for details.

This repository is licensed under the [MIT License](LICENSE).
