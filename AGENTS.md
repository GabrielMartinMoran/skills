# Agent instructions

## Skill dependencies

When a skill declares companion skills, use only those relevant to the task.
Prefer a matching skill already available in the agent context. Otherwise run
the exact `Dynamic use` command from the canonical registry, read its complete
output, and follow it for the current task. Resolve relative supporting-file
paths from the directory reported by the command. Do not substitute same-name
skills from another source or install persistently with `skills add`.

Dependency levels are defined as follows:

- `required`: attempt to load whenever the parent skill applies; report failure.
- `recommended`: load when the dependency's scope applies.
- `optional`: load only when explicitly useful.

### Canonical companion registry

The registry below is the source of truth for reproducing companion tables in
individual `SKILL.md` files.

| Skill | Source | Dynamic use |
| --- | --- | --- |
| `clean-architecture` | `https://github.com/pproenca/dot-skills` | `npx skills use https://github.com/pproenca/dot-skills --skill clean-architecture` |
| `clean-code` | `https://github.com/GabrielMartinMoran/skills` | `npx skills use https://github.com/GabrielMartinMoran/skills --skill clean-code` |
| `svelte-code-writer` | `https://github.com/sveltejs/ai-tools` | `npx skills use https://github.com/sveltejs/ai-tools --skill svelte-code-writer` |
| `clean-backend-architecture` | `https://github.com/GabrielMartinMoran/skills` | `npx skills use https://github.com/GabrielMartinMoran/skills --skill clean-backend-architecture` |

### Dependency matrix

Keep the following matrix synchronized with the companion tables in the
dependent skills.

| Parent skill | Companion | Level |
| --- | --- | --- |
| `clean-svelte-architecture` | `clean-architecture` | `recommended` |
| `clean-svelte-architecture` | `clean-code` | `recommended` |
| `clean-svelte-architecture` | `svelte-code-writer` | `recommended` |
| `clean-python` | `clean-code` | `required` |
| `clean-python` | `clean-backend-architecture` | `recommended` |

Each dependent `SKILL.md` must use this table shape:

```md
| Skill | Level | Dynamic use |
| --- | --- | --- |
| `<companion>` | `<required|recommended|optional>` | `npx skills use <source> --skill <name>` |
```

When adding or changing a dependency, update the canonical registry, the
dependency matrix, the dependent `SKILL.md`, and the relevant `README.md`
section in the same change.
