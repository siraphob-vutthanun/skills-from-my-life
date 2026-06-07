# Skills From My Life

Reusable AI-agent skills shaped by everyday AI use across chat and coding workflows, mostly from working with ChatGPT and Codex.

This repo starts small on purpose. Each skill should be practical, portable, and easy to copy into another AI account or install as a skill folder.

## Structure

Skills are grouped by lifecycle first:

- `launch/` for skills ready to use regularly
- `develop/` for skills still being shaped
- `deprecated/` for skills kept for reference only

Each lifecycle has the same categories:

- `daily/`
- `SE/`
- `coding/`
- `other/`

## Available Skills

### skeptical-research

Path: `launch/daily/skeptical-research`

Use this skill for skeptical, evidence-driven research and decisions about tools, products, AI models, APIs, subscriptions, pricing, quotas, limits, privacy, TOS, licenses, commercial use, and production readiness.

Best for questions like:

- "Which AI subscription should I pay for?"
- "Can I use this API output commercially?"
- "Is this pricing or quota still current?"
- "Is this tool production-ready?"
- "Compare these two software stacks for my use case."

## Develop Skills

These skills are still being shaped. They may be useful, but their behavior and wording are less settled than launch skills.

### github-https-repo-auth

Path: `develop/SE/github-https-repo-auth`

Repo-scoped GitHub HTTPS authentication for cases like publishing from a separate GitHub account, repairing credential helper issues, and diagnosing push errors without changing unrelated global auth.

### codex-sandbox-git

Path: `develop/SE/codex-sandbox-git`

Git workflow guidance for Codex workspace sandboxes, including when to use normal sandbox commands and when a `.git` write, network remote, or credential operation may need explicit user-approved escalation.

## Use With Codex

Install the full skill folder so Codex can discover its metadata and instructions:

```bash
mkdir -p ~/.codex/skills
cp -R launch/daily/skeptical-research ~/.codex/skills/
cp -R develop/SE/github-https-repo-auth ~/.codex/skills/
```

Then ask Codex normally, or explicitly invoke the skill:

```text
Use $skeptical-research to compare these two AI plans for my workflow.
```

## Use In ChatGPT Or Another Chat App

For chat-only use, copy the contents of:

```text
launch/daily/skeptical-research/SKILL.md
```

Paste it into a custom instruction, project instruction, custom GPT instruction, or the top of a new chat. The v1 skill is intentionally self-contained, so no extra reference files are required.

## Design Principles

- One portable `SKILL.md` is the source of truth for each v1 skill.
- Extra reference files are added only when real usage proves they are needed.
- Prefer concise, decision-focused behavior over large prompt libraries.
- Keep official facts separate from interpretation, recommendation, community opinion, and uncertainty.
- Avoid marketing language and unsupported certainty.

## Future Expansion

The `skeptical-research` skill may later grow optional reference files for answer patterns, source quality rules, or TOS/privacy checklists. If that happens, `SKILL.md` should remain usable alone for chat copy-paste workflows.

## Contributing

Contributions should come from real repeated use, not speculative prompt design.

Before adding a new skill or expanding an existing one:

- Keep the smallest structure that works.
- Prefer one self-contained `SKILL.md` for v1.
- Add references only when they reduce repeated context or make the skill easier to maintain.
- Keep examples practical and decision-oriented.
