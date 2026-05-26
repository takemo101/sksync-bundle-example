---
name: sksync
description: Manage Agent Skills with sksync, including finding skills, adding them to target agents, removing them, and installing bundles. Use when the user asks to find, install, sync, remove, or audit Agent Skills across coding agents with sksync or skills.sh.
---

# sksync Skill Management

Use `sksync` as the source of truth for installing and removing Agent Skills across coding agents.

## Quick start

Find candidates with skills.sh, then install the chosen source with explicit target agents:

```sh
npx skills find <query>
sksync add <source> --agent <agent>
```

Example:

```sh
npx skills find code review
sksync add github:example/skills/skills/review#main --agent pi --agent claude-code
```

## Before changing skills

1. Identify scope: project config by default, or global config with `--global`.
2. Identify target agents explicitly. Do not guess.
3. Inspect current state when useful:

```sh
sksync list
sksync doctor
sksync plan
```

## Find and add a skill

1. Search:

```sh
npx skills find <query>
```

2. Read candidate names, descriptions, and source URLs.
3. If multiple candidates match, ask the user which one to install.
4. Install with explicit agents:

```sh
sksync add <source> --agent <agent>
sksync add <source> --agent pi --agent claude-code --agent cursor
```

5. If the source contains multiple skills or the name cannot be inferred, use `--name`:

```sh
sksync add <source> --name <skill-name> --agent <agent>
```

## Install bundles

Bundles install curated sets of skills, but the user still chooses target agents.

```sh
sksync bundle inspect <bundle-source>
sksync bundle add <bundle-source> --agent <agent> --dry-run
sksync bundle add <bundle-source> --agent <agent>
```

Add `--global` for global installation.

## Remove skills

Remove one skill explicitly:

```sh
sksync remove <skill-name>
```

Remove bundle provenance safely when the user wants to remove a whole bundle:

```sh
sksync bundle remove <bundle-name> --dry-run
sksync bundle remove <bundle-name>
```

Use `sksync remove` when the user explicitly wants a specific skill gone regardless of bundle provenance.

## Safety rules

- Never modify agent skill directories manually when sksync can manage the change.
- Prefer `--dry-run`, `sksync plan`, `sksync list`, and `sksync doctor` before risky changes.
- Do not overwrite unmanaged files.
- Preserve bundle provenance when re-adding the same skill source.
- If conflicts or blocked targets appear, stop and explain the next safe command.
