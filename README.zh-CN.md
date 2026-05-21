# AI Learning Loop

[English](README.md)

AI Learning Loop 是一个通用的 Agent Skill，帮助你在使用 AI 助手写代码、调试、评审和学习时，不把理解本身外包给 AI。

这个 Skill 受到 Addy Osmani 的文章 [Don't Outsource the Learning](https://addyosmani.com/blog/dont-outsource-learning/) 启发。核心观点很直接：AI 应该帮你更快交付，也应该让你更会思考。如果任务完成了，但你的 mental model 没有变清晰，你就在积累认知债务。

## 它解决什么问题

这个 Skill 会给编码智能体一套轻量的 AI 协作工作流：

- 在向模型要修复方案之前，先形成一个假设。
- 在陌生领域，先解释概念、替代方案和权衡，再生成代码。
- 把 AI 输出当成初级工程师提交的 PR 来审查。
- 要求测试、日志、截图、手动验证等证据。
- 在重要会话结束时，同时检查“是否交付”和“是否学到了东西”。

这个 Skill 故意保持为简单的 Markdown 和少量元数据，方便适配任何支持 `SKILL.md` 约定的智能体。

## 项目结构

```text
ai-learning-loop/
+-- SKILL.md
+-- agents/
|   +-- openai.yaml
+-- LICENSE
+-- README.md
+-- README.zh-CN.md
```

`SKILL.md` 是核心 Skill。其他文件用于打包、元数据或开源说明。

## 安装方式

把整个目录 clone 或复制到你的智能体支持的 Skill 目录即可。

### Claude Code

个人 Skill：

```text
~/.claude/skills/ai-learning-loop/
```

项目级 Skill：

```text
.claude/skills/ai-learning-loop/
```

Claude Code 可以根据 skill description 自动触发，也可以手动调用：

```text
/ai-learning-loop
```

### Codex 和通用 Agent 目录

推荐使用共享 Agent Skills 约定：

```text
.agents/skills/ai-learning-loop/
```

### Cursor

如果你的 Cursor 环境支持 Agent Skills，可以放到：

```text
.cursor/skills/ai-learning-loop/
.agents/skills/ai-learning-loop/
```

如果你的 Cursor 环境只支持 Rules，可以把 `SKILL.md` 正文复制到项目规则文件，例如：

```text
.cursor/rules/ai-learning-loop.mdc
```

### 其他智能体

任何能加载指令目录、规则文件或可复用提示词的智能体，都可以使用 `SKILL.md` 的内容。平台支持 frontmatter 时保留 frontmatter；不支持时，只复制 Markdown 正文即可。

## 示例 Prompt

```text
Use $ai-learning-loop while helping me debug this failing test.
```

```text
Use $ai-learning-loop to explain this framework before writing the implementation.
```

```text
Use $ai-learning-loop to review this AI-generated diff and tell me what I should understand before merging.
```

中文也可以这样说：

```text
使用 $ai-learning-loop 帮我调试这个失败测试，但不要跳过理解过程。
```

```text
使用 $ai-learning-loop 先解释这个框架的关键概念，再开始写实现。
```

```text
使用 $ai-learning-loop 帮我审查这段 AI 生成的 diff，并告诉我合并前必须理解什么。
```

## 什么时候使用

适合用于非平凡的 AI 辅助编码、调试、代码评审、架构决策，以及学习新库、新框架或新代码库。

可以跳过的场景：一次性样板代码、格式调整、临时脚本，或者用户明确表示不需要理解和维护的代码。

## 设计目标

- 可在 Claude Code、Codex、Cursor 和其他智能体工具中复用。
- 足够短，适合频繁加载，不浪费上下文。
- 聚焦智能体行为，而不是写成长篇人类文档。
- 开源、易 fork、易改造。

## 许可证

MIT。见 [LICENSE](LICENSE)。
