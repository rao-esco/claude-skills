# Claude Skills

Agent skills for Claude Code and claude.ai. Each skill teaches the agent a workflow it
wouldn't follow on its own, so you get the result you want without explaining the
process every time.

## Install

```bash
npx skills@latest add rao-esco/claude-skills
```

## Why use it?

Left alone, an agent takes the shortest path to "done". Asked to redesign a screen, it
reads the current one and hands back a reskin of the same layout. These skills give it
the steps a careful person would take: understand the problem first, keep its own
judgement out of the places it biases the result, check the work, and leave you an easy
way back.

## Reference

| Skill | What it does |
|---|---|
| [fresh-ui-take](skills/fresh-ui-take/SKILL.md) | Redesigns an existing dialog, panel, page section or component without anchoring on how it looks today. It breaks down what the UI does, writes a layout-free brief for a design agent that never sees the old files, puts the result in place of the old component, and keeps data changes temporary until you approve. Git keeps the old version so going back is one restore. |
