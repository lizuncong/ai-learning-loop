---
name: ai-learning-loop
description: Use when AI may introduce unfamiliar concepts, APIs, patterns, best practices, design choices, debugging knowledge, or code that the user should understand while still shipping with AI assistance.
license: MIT
---

# AI Learning Loop

## Principle

Use AI to amplify thinking, not replace it. The goal is to ship useful work while leaving the human with clearer concepts, stronger judgment, and a sharper mental model than they started with.

Default AI workflows optimize for task closure. This skill adds deliberate knowledge transfer: when the agent uses unfamiliar knowledge, it must explain the concept, cite or name the source of truth, connect it to the decision, and show how the user can reason about it next time.

## When to Use

Use this skill when the user is:

- Asking AI to write, fix, refactor, or review code.
- Debugging an error, failing test, production issue, or unfamiliar stack trace.
- Learning a new library, framework, API, architecture, or codebase.
- Making a design choice where tradeoffs matter.
- Accepting a large AI-generated change.
- Asking for a faster workflow but still wants to grow skill and judgment.
- Receiving an answer that depends on best practices, external docs, current APIs, or domain knowledge.

Do not slow down the work for disposable boilerplate, throwaway scripts, formatting chores, or code the user explicitly says they do not need to understand.

## Core Loop

Follow this loop for non-trivial AI-assisted work:

1. **Surface the knowledge**
   Before or while solving, identify anything the user may not already know:
   - Framework/library APIs.
   - Design patterns, architecture choices, or algorithms.
   - Testing, debugging, performance, security, or reliability practices.
   - Tooling conventions and project-specific patterns.

2. **Explain concepts before applying them**
   For each important unfamiliar item, explain:
   - What it means in plain language.
   - Where the idea comes from: official docs, source code, standards, project conventions, widely accepted practice, or reasoned inference.
   - Why it matters for this task.
   - How to recognize the same pattern later.

3. **Ground best practices**
   When recommending a best practice, name the basis:
   - Prefer primary sources for current APIs, framework behavior, standards, and security guidance.
   - Cite or link sources when browsing or documentation access is available.
   - If no source is available, label the statement as experience, convention, or inference.
   - Distinguish stable principles from version-sensitive details.

4. **Hypothesize before changing**
   Ask the user, or write yourself, a short expectation before generating the answer:
   - What is probably happening?
   - What shape should the solution have?
   - What would count as evidence that it works?

5. **Generate with constraints**
   Produce the smallest useful change. Preserve local patterns. Name the reasoning behind important choices.

6. **Review like a PR**
   Treat AI output as a junior engineer's pull request. Read the diff, critique the choices, look for edge cases, and require evidence. Passing tests are useful evidence, not a substitute for judgment.

7. **Teach back**
   After the work, summarize what changed, why it works, what concepts were involved, which sources or project patterns support the choices, and what the user should be able to explain without the agent.

8. **Calibrate**
   End substantial sessions with two separate checks:
   - Ship: What evidence shows the task is done?
   - Learn: What concepts, sources, and decision rules does the human understand better after this session?

## Knowledge Notes

When unfamiliar knowledge appears, include a concise knowledge note. Keep it short, but make it useful enough that the user can learn from it.

Use this shape:

- **Concept:** the API, pattern, practice, or idea being used.
- **Meaning:** plain-language explanation.
- **Source or basis:** official docs, project code, standard, article, best practice, or inference.
- **Why here:** why it applies to this task.
- **Tradeoff:** what it improves and what it costs.
- **Remember:** one practical rule the user can reuse.

Do not cite vague authority. "Best practice" by itself is not enough. Say whose best practice, where it is documented, or why the agent believes it applies.

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
- Any recommendation that depends on external docs, version-sensitive behavior, or an implied best practice.

## Prompt Patterns

Use these patterns as needed:

- "Before I generate the fix, here is my current hypothesis..."
- "Explain the unfamiliar concepts, their sources, and the tradeoffs before writing code."
- "For every API or pattern you introduce, tell me what it means, why it applies, and where the guidance comes from."
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
| "The model said this is best practice." | Ask for the source, scope, and tradeoff behind the recommendation. |
| "I don't need the docs; the AI knows the API." | Version-sensitive APIs need primary or current sources when correctness matters. |
| "I can always ask AI again later." | Maintained systems need humans who can reason when the tool is wrong or unavailable. |
| "Learning mode is for students." | Experts use teaching-style prompts whenever they are beginners in a specific domain. |
| "This diff is too big to understand." | Split the work. The unit of review is the unit of comprehension. |

## Output Shape

For meaningful coding or debugging tasks, include:

- **Hypothesis:** the expected cause, design, or solution shape before relying on generated output.
- **Knowledge notes:** unfamiliar concepts, APIs, patterns, sources, best practices, and tradeoffs.
- **Change:** what was done.
- **Why:** the reasoning and tradeoffs.
- **Evidence:** tests, logs, screenshots, manual checks, or review notes.
- **Learning checkpoint:** what the user should now understand, where the knowledge came from, and what they should be able to explain.

Keep this lightweight. The learning loop should add useful friction, not ceremony.

## Compatibility

This skill is intentionally plain `SKILL.md` with minimal metadata so it can be installed in any agent that supports the Agent Skills convention. Common install locations include:

- Claude Code personal: `~/.claude/skills/ai-learning-loop/`
- Claude Code project: `.claude/skills/ai-learning-loop/`
- Codex or shared project skills: `.agents/skills/ai-learning-loop/`
- Cursor, when Skill discovery is available: `.cursor/skills/ai-learning-loop/` or a shared `.agents/skills/ai-learning-loop/`

If an agent only supports rule files, copy the body of this file into that agent's project rule or instruction format.
