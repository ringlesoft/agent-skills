# Agent Skills

Reusable AI agent skills for coding and product work.

## What This Repository Is

This repository contains skills that can be installed or copied into an agent's skills directory so the agent can perform specialized tasks with better workflow guidance, sharper trigger conditions, and less repeated prompting.

Each skill is a self-contained folder with a required `SKILL.md` file and optional supporting resources such as references, scripts, or assets.

## Repository Structure

```text
skills/
  <skill-name>/
    SKILL.md
    references/
    scripts/
    assets/
    agents/
```

## Installation

Install a skill with the skills CLI:

```bash
npx skills add ringlesoft/agent-skills <skill>
```

Examples:

```bash
npx skills add ringlesoft/agent-skills <skill>
```

If the target environment does not use the CLI, copy or symlink the desired skill folder into that agent's skills directory instead.

## Available Skills

This table should be updated as new skills are added.

| Skill | Status | Purpose |
| --- | --- | --- |
| `ariakit` | Ready | Guidance for building accessible React UI with Ariakit headless components and correct store/provider wiring. |
| `mantine-ui` | In progress | Reserved for Mantine UI skill content. |

## Skill Format

Every skill should follow the standard agent-skill shape:

1. `SKILL.md` starts with YAML frontmatter.
2. Frontmatter includes:
   - `name`
   - `description`
3. The body explains:
   - when the skill should trigger
   - how the agent should execute the work
   - what guardrails or constraints matter
   - which supporting files to read only when needed

The body should stay lean. Detailed reference material belongs in `references/`, not in the main skill file.

## Authoring Principles

- Write for an agent, not for an end user.
- Optimize for triggering accuracy.
- Prefer workflows and decision rules over long explanations.
- Use progressive disclosure: keep `SKILL.md` concise and move bulky details into supporting files.
- Include only files that directly help the agent do the job.

## Using a Skill

1. Install the skill with `npx skills add ringlesoft/agent-skills <skill-source>` or copy it into the target skills directory.
2. Ensure the folder name matches the skill name.
3. Keep the `description` specific enough that the agent knows when to activate it.

## Contributing

When adding or updating a skill:

1. Define the concrete jobs the skill should handle.
2. Write a trigger-focused `description`.
3. Keep `SKILL.md` operational and concise.
4. Add references or scripts only when they reduce ambiguity or repeated work.
5. Validate the skill against a realistic prompt before considering it done.
