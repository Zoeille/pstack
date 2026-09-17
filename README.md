# pstack — Hermes Plugin

Poteto's engineering rigor stack, adapted for [Hermes Agent](https://hermes-agent.nousresearch.com).

Fork of [pstack](https://github.com/cursor/plugins/tree/main/pstack) by poteto (Meta/Netflix/Cursor, React core team). Originally built as a Cursor plugin, rebuilt here as a Hermes plugin with native skills, delegate_task orchestration, and playbook routing.

## What it does

One orchestrator skill (`poteto-mode`) that routes tasks to playbooks and enforces principles. Five satellite skills for specific capabilities.

| Skill | Purpose |
|-------|---------|
| `pstack:poteto-mode` | Orchestrator. Task → playbook routing, principles, autonomy rules, delegation patterns. |
| `pstack:how` | Codebase exploration. "How does X work?" with explain/critique modes. |
| `pstack:architect` | Design types and module boundaries before implementing. "Design it twice." |
| `pstack:interrogate` | Multi-reviewer adversarial code review via parallel delegates. |
| `pstack:swarm` | Fan out N parallel workers, drain, report. |
| `pstack:unslop` | Strip AI writing patterns. Apply to all prose. |

## Playbooks

Loaded via `skill_view(name='pstack:poteto-mode', file_path='playbooks/<name>.md')`:

- `investigation.md` — read-only question, trace behavior
- `bug-fix.md` — reproduce, root-cause, fix with evidence
- `feature.md` — plan, design, delegate, verify
- `perf-issue.md` — measure, profile, fix, measure again
- `refactoring.md` — behavior-preserving restructuring
- `autonomous-run.md` — long task with falsifiable exit predicate
- `figure-it-out.md` — large/cross-cutting work, design your own workflow

## Install

Symlink or copy into your Hermes profile plugins directory:

```bash
ln -s /path/to/pstack ~/.hermes/profiles/<profile>/plugins/pstack
```

Hermes loads it on next session start.

## License

MIT
