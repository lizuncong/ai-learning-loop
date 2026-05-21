# AI Learning Loop

[English](README.md)

AI Learning Loop 是一个通用的 Agent Skill，让 AI 助手引导用户参与思考，而不是只输出答案。

这个 Skill 受到 Addy Osmani 的文章 [Don't Outsource the Learning](https://addyosmani.com/blog/dont-outsource-learning/) 启发。核心观点很直接：人负责练习判断，AI 负责解释和执行。当用户问“这个怎么做”、反馈“按钮点击失败”、或者询问方案时，AI 应该先邀请用户说出自己的思路、判断或取舍偏好。当 AI 引入陌生 API、架构、设计模式、最佳实践或原理时，它应该解释这是什么、依据来自哪里、为什么适用于这里，以及有什么权衡。

## 它解决什么问题

这个 Skill 会给编码智能体一套轻量的 AI 协作工作流：

- 在解决非平凡问题前，先询问用户当前的思路、判断或偏好。
- 主动暴露陌生概念、API、模式和最佳实践。
- 解释它们是什么意思、依据来自哪里、为什么适用于当前任务。
- 使用架构、设计模式或原理时，明确命名并讲清楚。
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

GitHub 仓库：

```text
https://github.com/lizuncong/ai-learning-loop
```

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

Codex 也可以通过 GitHub URL 安装：

```text
$skill-installer install https://github.com/lizuncong/ai-learning-loop
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

适合用于非平凡的 AI 辅助编码、调试、代码评审、架构决策，以及学习新库、新框架或新代码库。尤其适合用户询问方案、反馈失败、比较不同做法，或者答案依赖陌生知识、外部文档、架构、设计模式、原理或最佳实践的场景。

可以跳过的场景：一次性样板代码、格式调整、临时脚本，或者用户明确表示不需要理解和维护的代码。

## 设计目标

- 可在 Claude Code、Codex、Cursor 和其他智能体工具中复用。
- 足够短，适合频繁加载，不浪费上下文。
- 聚焦智能体行为，而不是写成长篇人类文档。
- 开源、易 fork、易改造。

## 发布到市场

维护者可以通过 GitHub Release、`gh skill publish` 和各类 Skill registry 发布这个 Skill。见 [PUBLISHING.md](PUBLISHING.md)。

## 许可证

MIT。见 [LICENSE](LICENSE)。
