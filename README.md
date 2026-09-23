# i-have-adhd

> ADHD-friendly output instructions for AI agents.
>
> 面向 ADHD 读者的 AI 输出规范，让回复更容易理解、开始和完成。

[English](#english) · [中文](#中文)

---

## English

### What it is

`i-have-adhd` is a reusable skill for AI agents. It shapes responses around the way many ADHD readers process information:

- start with a concrete next action;
- turn multi-step work into short, numbered steps;
- keep current state visible across turns;
- suppress tangents until the main task is complete;
- use concrete time estimates;
- make completed work and verification results easy to see.

The skill changes the structure and presentation of an answer. It does not replace the host agent's reasoning, tools, permissions, or safety policies.

### Why it helps

A response can be accurate and still be hard to act on. Important details may be buried in a long introduction, several actions may be mixed into one paragraph, or the next step may be unclear. This skill reduces that execution friction while preserving depth when a task needs explanation.

### Core behavior

1. **Lead with the next action.** Put the command, path, conclusion, or immediate action first.
2. **Number multi-step work.** Keep each step bounded and easy to complete.
3. **Externalize state.** Show what is done, what remains, and the next step.
4. **Control scope.** Finish the current issue before opening side topics.
5. **Use concrete estimates.** Say `15 minutes`, `two hours`, or `this afternoon` instead of vague effort labels.
6. **Show the result.** State what now works and how to verify it.
7. **Explain errors directly.** Identify the location, cause, and fix.
8. **Keep lists short.** Split long lists into ranked groups such as “Do now” and “Later”.

### Example

Without the skill:

> There are a few things to consider before changing the authentication flow. You may want to inspect the configuration, update the handler, and then run the tests.

With the skill:

```text
1. Open src/auth.ts.
2. Replace verifyToken with the updated function.
3. Run npm test -- auth.spec.ts.

Next: paste the first failing line if the test still fails.
```

### Installation

#### Codex / OpenAI

Copy the skill directory into the Codex global skills directory:

```bash
mkdir -p ~/.codex/skills/i-have-adhd/agents
cp i-have-adhd/SKILL.md ~/.codex/skills/i-have-adhd/SKILL.md
cp i-have-adhd/agents/openai.yaml ~/.codex/skills/i-have-adhd/agents/openai.yaml
```

The included OpenAI metadata enables implicit invocation, so the skill can shape every response automatically. To return to the default response style for the current session, say:

```text
stop adhd mode
```

or:

```text
normal mode
```

#### Gemini CLI

Install the command file:

```bash
mkdir -p ~/.gemini/commands
cp i-have-adhd/agents/gemini.toml ~/.gemini/commands/i-have-adhd.toml
```

Enable it in a Gemini CLI session with:

```text
/i-have-adhd
```

### When to use it

This skill works well for coding, debugging, research notes, planning, writing, learning, project management, and everyday questions. It is especially useful when a task has several steps, requires multiple rounds of collaboration, or is easy to postpone because the starting point is unclear.

### Safety and boundaries

The skill only changes response style. The host agent's safety rules still apply. Destructive actions, permission changes, credential handling, and other high-impact operations must follow the confirmation requirements of the host environment.

### Files

```text
i-have-adhd/
├── SKILL.md                 # Core behavior and rules
├── agents/
│   ├── openai.yaml          # Codex / OpenAI metadata
│   └── gemini.toml          # Gemini CLI command
```

### License

MIT. See the [LICENSE](LICENSE) file when included by your distribution.

---

## 中文

### 这是什么

`i-have-adhd` 是一套可复用的 AI Agent Skill，专门调整回复的组织方式，让 ADHD 读者更容易理解、开始和完成任务。

它重点处理以下阅读和执行摩擦：

- 重点隐藏在长段落里；
- 多个动作混在同一步里；
- 对话进行几轮后，当前状态变得模糊；
- 旁支信息过多，主任务难以收敛；
- 时间规模表达过于模糊；
- 已完成的工作和验证结果不够明显。

这套 Skill 负责调整表达结构和呈现方式，同时保留复杂任务所需的解释深度。模型判断、工具权限和安全规则仍由宿主 Agent 负责。

### 核心行为

1. **先给下一步动作。** 第一行优先放命令、路径、结论或可以立即执行的操作。
2. **多步骤任务编号。** 每一步保持边界清晰，方便逐项完成。
3. **持续显示状态。** 说明已完成内容、剩余事项和紧接着的动作。
4. **控制信息范围。** 先完成当前问题，再处理额外议题。
5. **给出具体时间。** 使用“15 分钟”“两小时”“今天下午”等明确表达。
6. **让成果可见。** 说明当前已经实现的结果，以及验证方式。
7. **直接说明错误。** 指出发生位置、原因和修复动作。
8. **保持列表短小。** 列表较长时拆成“现在做”和“稍后做”等有顺序的分组。

### 使用示例

普通回复可以直接从行动开始：

```text
1. 打开 src/auth.ts。
2. 用新版函数替换 verifyToken。
3. 运行 npm test -- auth.spec.ts。

下一步：如果测试仍然失败，粘贴第一条失败信息。
```

当用户要求“解释”或“带我过一遍”时，Skill 会保留完整解释，并使用标题和段落帮助定位。遇到删除数据、强制推送、权限变更等高风险操作，仍然遵守宿主环境的确认要求。

### 安装方式

#### Codex / OpenAI

将 Skill 文件复制到 Codex 全局目录：

```bash
mkdir -p ~/.codex/skills/i-have-adhd/agents
cp i-have-adhd/SKILL.md ~/.codex/skills/i-have-adhd/SKILL.md
cp i-have-adhd/agents/openai.yaml ~/.codex/skills/i-have-adhd/agents/openai.yaml
```

随附的 OpenAI 配置允许自动触发，新的回复会默认采用这套输出方式。当前会话需要恢复普通回复时，可以说：

```text
stop adhd mode
```

或：

```text
normal mode
```

#### Gemini CLI

复制命令文件：

```bash
mkdir -p ~/.gemini/commands
cp i-have-adhd/agents/gemini.toml ~/.gemini/commands/i-have-adhd.toml
```

在 Gemini CLI 会话中输入：

```text
/i-have-adhd
```

### 适用场景

这套 Skill 适合编程、调试、资料整理、项目规划、写作、学习、项目管理和日常问答。任务步骤较多、需要多轮协作，或启动点不够明确时，使用效果尤其明显。

### 文件结构

```text
i-have-adhd/
├── SKILL.md                 # 核心规则
├── agents/
│   ├── openai.yaml          # Codex / OpenAI 配置
│   └── gemini.toml          # Gemini CLI 命令
```

### GitHub

仓库地址：[AAAAAAAJ/i-have-adhd](https://github.com/AAAAAAAJ/i-have-adhd)

### 许可证

MIT。发布包包含许可证文件时，请同时遵守 [LICENSE](LICENSE) 中的条款。

---

## Contributing / 参与改进

Issues and pull requests are welcome. Keep changes focused on making AI output easier to understand and act on, and include a short example when changing a rule.

欢迎提交 Issue 和 Pull Request。修改规则时，请围绕“让 AI 回复更容易理解和执行”这一目标，并附上简短示例，方便评估变化效果。
