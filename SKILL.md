---
name: ai-learning-loop
description: Use when a user is using AI to code, debug, review, design, learn a library or framework, understand unfamiliar code, or avoid outsourcing comprehension while still shipping with AI assistance.
license: MIT
---

# AI Learning Loop

## Principle

Use AI to amplify thinking, not replace it. The goal is to ship useful work while leaving the human with a sharper mental model than they started with.

Default AI workflows optimize for task closure. This skill adds deliberate learning checkpoints so the agent helps the user understand, judge, and retain the work.

## When to Use

Use this skill when the user is:

- Asking AI to write, fix, refactor, or review code.
- Debugging an error, failing test, production issue, or unfamiliar stack trace.
- Learning a new library, framework, API, architecture, or codebase.
- Making a design choice where tradeoffs matter.
- Accepting a large AI-generated change.
- Asking for a faster workflow but still wants to grow skill and judgment.

Do not slow down the work for disposable boilerplate, throwaway scripts, formatting chores, or code the user explicitly says they do not need to understand.

## Core Loop

Follow this loop for non-trivial AI-assisted work:

1. **Hypothesize first**
   Ask the user, or write yourself, a short expectation before generating the answer:
   - What is probably happening?
   - What shape should the solution have?
   - What would count as evidence that it works?

2. **Explain before generating**
   In unfamiliar territory, explain the concepts, alternatives, and tradeoffs before writing code. Prefer conceptual inquiry before production.

3. **Generate with constraints**
   Produce the smallest useful change. Preserve local patterns. Name the reasoning behind important choices.

4. **Review like a PR**
   Treat AI output as a junior engineer's pull request. Read the diff, critique the choices, look for edge cases, and require evidence. Passing tests are useful evidence, not a substitute for judgment.

5. **Teach back**
   After the work, summarize what changed, why it works, what concepts were involved, and what the user should be able to explain without the agent.

6. **Calibrate**
   End substantial sessions with two separate checks:
   - Ship: What evidence shows the task is done?
   - Learn: What did the human understand better after this session?

## Delegation Boundaries

Pure delegation is acceptable for:

- Boilerplate, scaffolding, formatting, and repetitive transformations.
- Glue code with low long-term ownership cost.
- One-off scripts the user will not maintain.
- Syntax lookup where memorization has low value.

Require active learning for:

- Architecture, data flow, concurrency, security, persistence, and reliability decisions.
- Bugs the user may need to debug again.
- Framework or library usage the user is trying to learn.
- Code that will become part of a maintained system.
- Changes whose failure mode is subtle, expensive, or hard to detect.

## Prompt Patterns

Use these patterns as needed:

- "Before I generate the fix, here is my current hypothesis..."
- "Explain the moving parts and tradeoffs first; wait to write code until the model is clear."
- "Give two plausible approaches and argue against your preferred one."
- "Review this output as if it came from a junior engineer. What would block merge?"
- "After this change, teach me what concepts I need to understand to maintain it."
- "Ask me to re-derive the key step before giving the final answer."

## Anti-Rationalization Table

| Rationalization | Response |
| --- | --- |
| "The AI fixed the bug, so we're done." | The symptom disappeared; verify the cause and update the mental model. |
| "The tests pass, so I don't need to read it." | Tests are evidence, not comprehension. Review the change anyway. |
| "This is too urgent to learn." | Use the fastest loop that still records the hypothesis, risk, and evidence. |
| "The model sounds confident." | Confidence is not reasoning. Ask for alternatives or counterarguments. |
| "I can always ask AI again later." | Maintained systems need humans who can reason when the tool is wrong or unavailable. |
| "Learning mode is for students." | Experts use teaching-style prompts whenever they are beginners in a specific domain. |
| "This diff is too big to understand." | Split the work. The unit of review is the unit of comprehension. |

## Output Shape

For meaningful coding or debugging tasks, include:

- **Hypothesis:** the expected cause, design, or solution shape before relying on generated output.
- **Change:** what was done.
- **Why:** the reasoning and tradeoffs.
- **Evidence:** tests, logs, screenshots, manual checks, or review notes.
- **Learning checkpoint:** what the user should now understand or be able to explain.

Keep this lightweight. The learning loop should add useful friction, not ceremony.

## Compatibility

This skill is intentionally plain `SKILL.md` with minimal metadata so it can be installed in any agent that supports the Agent Skills convention. Common install locations include:

- Claude Code personal: `~/.claude/skills/ai-learning-loop/`
- Claude Code project: `.claude/skills/ai-learning-loop/`
- Codex or shared project skills: `.agents/skills/ai-learning-loop/`
- Cursor, when Skill discovery is available: `.cursor/skills/ai-learning-loop/` or a shared `.agents/skills/ai-learning-loop/`

If an agent only supports rule files, copy the body of this file into that agent's project rule or instruction format.
