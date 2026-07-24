# skills

Public repository for agent skills. Skills are specialized tools and workflows
that extend agent capabilities for specific tasks. Install any skill with `npx
skills add`.

## Available Skills

The following skills are available in this repository:

| Skill | Description | Install Command |
|-------|-------------|-----------------|
| `clean-svelte-architecture` | Clean Architecture patterns and best practices for SvelteKit applications | `npx skills add https://github.com/GabrielMartinMoran/skills --skill clean-svelte-architecture` |
| `clean-backend-architecture` | Framework-agnostic Clean Architecture patterns for APIs, workers, jobs, events, and CLI backends | `npx skills add https://github.com/GabrielMartinMoran/skills --skill clean-backend-architecture` |
| `prompt-optimizer` | Optimize, review, and rewrite prompts for maximum effectiveness across LLM targets | `npx skills add https://github.com/GabrielMartinMoran/skills --skill prompt-optimizer` |
| `clean-code` | Principles and practices for writing clean and maintainable code | `npx skills add https://github.com/GabrielMartinMoran/skills --skill clean-code` |

## Complementary Skills for clean-svelte-architecture

These are companion skills recommended for `clean-svelte-architecture` users:

```bash
npx skills add https://github.com/pproenca/dot-skills --skill clean-architecture && \
npx skills add https://github.com/GabrielMartinMoran/skills --skill clean-code && \
npx skills add https://github.com/sveltejs/ai-tools --skill svelte-code-writer
```

`clean-backend-architecture` is the framework-agnostic companion for backend
services, workers, jobs, event consumers, and CLI applications.

## Notes

Skills take effect when the agent's task matches the skill description. After
installation, the agent automatically loads the skill when a relevant task
is detected.
