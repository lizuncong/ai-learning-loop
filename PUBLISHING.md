# Publishing

This project is already a valid root-level Agent Skill: the repository root contains `SKILL.md`.

For broad discovery, publish it to GitHub first, then submit the GitHub repository to skill registries and marketplaces.

## Pre-Publish Checklist

- `SKILL.md` has valid frontmatter:
  - `name: ai-learning-loop`
  - `description: ...`
  - `license: MIT`
- `README.md` explains installation in English.
- `README.zh-CN.md` explains installation in Chinese.
- `LICENSE` is present.
- No scripts are bundled, so there are no executable supply-chain risks to disclose.

## Recommended GitHub Repository Settings

Suggested repository name:

```text
ai-learning-loop
```

Suggested description:

```text
A portable Agent Skill for making AI assistants guide user thinking while they execute.
```

Suggested topics:

```text
agent-skills
skill-md
claude-code
codex
cursor
github-copilot
ai-learning
ai-assisted-engineering
cognitive-debt
```

## Publish With GitHub CLI

GitHub CLI 2.90.0 or later includes `gh skill` commands in public preview.

Validate locally without publishing:

```bash
gh skill publish --dry-run
```

Publish a release:

```bash
gh skill publish --tag v0.1.0
```

The publish command validates Agent Skills metadata, adds the `agent-skills` topic, and creates a GitHub release.

## Manual GitHub Release

If `gh skill publish` is unavailable, create a normal GitHub release:

```bash
git tag v0.1.0
git push origin v0.1.0
```

Then create a GitHub Release for `v0.1.0` with release notes such as:

```text
Initial public release of ai-learning-loop.

- Adds the AI Learning Loop skill.
- Supports Claude Code, Codex, Cursor, GitHub Copilot, and other SKILL.md-compatible agents.
- Includes English and Chinese README files.
```

## Marketplace Submission Copy

Use this copy when submitting to registries such as SkillsMD or SkillUse.

Skill name:

```text
ai-learning-loop
```

Short description:

```text
Guide user thinking while AI executes.
```

Long description:

```text
AI Learning Loop is a portable Agent Skill for AI-assisted engineering. It makes coding agents ask for the user's current thought, diagnosis, or tradeoff preference before solving non-trivial work, then teach unfamiliar concepts, APIs, architectures, design patterns, principles, sources, and tradeoffs while the AI executes.
```

Install command examples:

```bash
gh skill install lizuncong/ai-learning-loop ai-learning-loop
```

```text
$skill-installer install https://github.com/lizuncong/ai-learning-loop
```

## Registry Targets

### GitHub / Copilot skill ecosystem

Publish with:

```bash
gh skill publish --tag v0.1.0
```

Users can preview before installing:

```bash
gh skill preview lizuncong/ai-learning-loop ai-learning-loop
```

Users can install with:

```bash
gh skill install lizuncong/ai-learning-loop ai-learning-loop
```

### Codex

Users can install from the GitHub URL with Codex's `$skill-installer`.

```text
$skill-installer install https://github.com/lizuncong/ai-learning-loop
```

For inclusion in the OpenAI skills catalog, open a PR or issue against `openai/skills` and follow that repository's current contribution process.

### SkillsMD

Submit the public GitHub repository at:

```text
https://skillsmd.dev/
```

Use:

- Repository: `lizuncong/ai-learning-loop`
- Skill Name: `ai-learning-loop`
- Description: the short description above

### SkillUse

After publishing the repo, SkillUse users can add the repository and install the skill.

```bash
skilluse repo add lizuncong/ai-learning-loop
skilluse skill install ai-learning-loop
```

If publishing through SkillUse directly:

```bash
skilluse publish --version 0.1.0
```

## Versioning

Use semantic versioning:

- `v0.1.0` for the first public release.
- Patch releases for wording, metadata, or docs improvements.
- Minor releases for meaningful workflow changes.
- Major releases only if the triggering behavior or expected output shape changes substantially.
