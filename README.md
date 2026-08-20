# skills

Public repository for agent skills. Skills are specialized tools and workflows
that extend agent capabilities for specific tasks. Install any skill with `npx
skills add`.

## Available Skills

The following skills are available in this repository:

| Skill | Description | Install Command |
| ------- | ------------- | ----------------- |
| `clean-svelte-architecture` | Clean Architecture patterns and best practices for SvelteKit applications | `npx skills add https://github.com/GabrielMartinMoran/skills --skill clean-svelte-architecture` |
| `clean-backend-architecture` | Framework-agnostic Clean Architecture patterns for APIs, workers, jobs, events, and CLI backends | `npx skills add https://github.com/GabrielMartinMoran/skills --skill clean-backend-architecture` |
| `clean-python` | Python quality, tooling, testing, configuration, and application engineering practices | `npx skills add https://github.com/GabrielMartinMoran/skills --skill clean-python` |
| `prompt-optimizer` | Optimize, review, and rewrite prompts for maximum effectiveness across LLM targets | `npx skills add https://github.com/GabrielMartinMoran/skills --skill prompt-optimizer` |
| `clean-code` | Principles and practices for writing clean and maintainable code | `npx skills add https://github.com/GabrielMartinMoran/skills --skill clean-code` |
| `cognitive-writing` | Write and restructure documentation and general text for cognitive accessibility, clarity, focus, and impact | `npx skills add https://github.com/GabrielMartinMoran/skills --skill cognitive-writing` |

## Complementary Skills for clean-svelte-architecture

Use the applicable companions listed below. If a companion is unavailable, run
its dynamic-use command and follow the complete output.

| Skill | Level | Dynamic use |
| --- | --- | --- |
| `clean-architecture` | `recommended` | `npx skills use https://github.com/pproenca/dot-skills --skill clean-architecture` |
| `clean-code` | `recommended` | `npx skills use https://github.com/GabrielMartinMoran/skills --skill clean-code` |
| `svelte-code-writer` | `recommended` | `npx skills use https://github.com/sveltejs/ai-tools --skill svelte-code-writer` |

`clean-backend-architecture` is the framework-agnostic companion for backend
services, workers, jobs, event consumers, and CLI applications.

## Complementary Skills for clean-python

Use the applicable companions listed below. If a companion is unavailable, run
its dynamic-use command and follow the complete output.

| Skill | Level | Dynamic use |
| --- | --- | --- |
| `clean-code` | `required` | `npx skills use https://github.com/GabrielMartinMoran/skills --skill clean-code` |
| `clean-backend-architecture` | `recommended` | `npx skills use https://github.com/GabrielMartinMoran/skills --skill clean-backend-architecture` |

Use `npx skills add` from the Available Skills table when you want a companion
installed persistently instead of loaded dynamically for one task.

## Notes

Skills take effect when the agent's task matches the skill description. After
installation, the agent automatically loads the skill when a relevant task
is detected.
