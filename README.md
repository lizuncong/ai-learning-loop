# AI Learning Loop

[中文](README.zh-CN.md)

AI Learning Loop is a portable Agent Skill for making AI assistants guide the user's thinking instead of merely outputting answers.

It is inspired by Addy Osmani's essay [Don't Outsource the Learning](https://addyosmani.com/blog/dont-outsource-learning/). The core idea is simple: the human practices judgment, the AI explains and executes. When the user asks "how should I do this?", reports a failed click, or asks for a solution, the AI should first invite the user to share their guess, diagnosis, or tradeoff preference. When the AI introduces an unfamiliar API, architecture, design pattern, best practice, or principle, it should explain what it is, where the guidance comes from, why it applies, and what tradeoffs it has.

## What It Does

This skill gives coding agents a lightweight workflow for AI-assisted engineering:

- Ask the user for their current thought, diagnosis, or preference before solving non-trivial work.
- Surface unfamiliar concepts, APIs, patterns, and best practices.
- Explain what they mean, where the guidance comes from, and why they apply.
- Name architectures, design patterns, and principles when they are used.
- Treat AI output like a pull request from a junior engineer.
- Require evidence such as tests, logs, screenshots, or manual verification.
- End substantial sessions with both a shipping checkpoint and a learning checkpoint.

The skill is intentionally plain Markdown with minimal metadata so it can work across agents that support the `SKILL.md` convention.

## Repository Structure

```text
ai-learning-loop/
+-- SKILL.md
+-- agents/
|   +-- openai.yaml
+-- LICENSE
+-- README.md
+-- README.zh-CN.md
```

`SKILL.md` is the canonical skill. Other files are packaging or platform metadata.

## Installation

Clone or copy this directory into the skill location used by your agent.

GitHub repository:

```text
https://github.com/lizuncong/ai-learning-loop
```

### Claude Code

Personal skill:

```text
~/.claude/skills/ai-learning-loop/
```

Project skill:

```text
.claude/skills/ai-learning-loop/
```

Claude Code can invoke it automatically when the request matches the skill description, or manually with:

```text
/ai-learning-loop
```

### Codex and Shared Agent Setups

Use the shared agent skills convention:

```text
.agents/skills/ai-learning-loop/
```

Codex can also install from the GitHub URL:

```text
$skill-installer install https://github.com/lizuncong/ai-learning-loop
```

### Cursor

If your Cursor setup supports Agent Skills, use either:

```text
.cursor/skills/ai-learning-loop/
.agents/skills/ai-learning-loop/
```

If your setup only supports Cursor Rules, copy the body of `SKILL.md` into a project rule such as:

```text
.cursor/rules/ai-learning-loop.mdc
```

### Other Agents

Any agent that can load instruction folders or reusable rules can use the content of `SKILL.md`. Keep the frontmatter when the platform supports it; otherwise copy the Markdown body into that platform's rule or instruction format.

## Example Prompts

```text
Use $ai-learning-loop while helping me debug this failing test.
```

```text
Use $ai-learning-loop to explain this framework before writing the implementation.
```

```text
Use $ai-learning-loop to review this AI-generated diff and tell me what I should understand before merging.
```

## When To Use It

Use this skill for non-trivial AI-assisted coding, debugging, reviewing, architecture decisions, and learning new libraries or codebases. It is especially useful when the user asks for a solution, reports a failure, compares approaches, or when the answer depends on unfamiliar knowledge, external documentation, architecture, design patterns, principles, or best practices.

Skip it for disposable boilerplate, formatting chores, one-off scripts, or code the user explicitly does not need to understand.

## Design Goals

- Portable across Claude Code, Codex, Cursor, and other agent tools.
- Small enough to load often without wasting context.
- Focused on agent behavior rather than human-facing documentation.
- Open source and easy to fork.

## Publishing

Maintainers can publish this skill through GitHub releases, `gh skill publish`, and skill registries. See [PUBLISHING.md](PUBLISHING.md).

## License

MIT. See [LICENSE](LICENSE).
