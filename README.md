# Evidence First Skill

> 中文 / English

Evidence First is a portable Codex skill for working in a Fable5-like mode: intent first, evidence before claims, conclusion first, and explicit verification before calling work done.

Evidence First 是一个可移植的 Codex skill，用来复刻 Fable5 式工作模式：先理解意图，再拿证据支撑结论；结论放第一句；没有实际验证就不说完成。

## Keywords / 关键词

agent skills, Codex skills, npx skills, skills CLI, AI agents, prompt engineering, evidence-based workflow, verification-first delivery, adversarial review, portable agent methodology, Fable5-like workflow

agent skill、Codex skill、npx skills、skills CLI、AI agent、提示词工程、证据优先、验证优先、敌对评审、可移植 agent 方法论、Fable5 式工作流

## 中文说明

### 它解决什么问题

这个 skill 面向调研、分析、排查、写方案、写文档、编码等非琐碎任务，尤其适合以下场景：

- 时间很紧，但仍然不能牺牲事实准确性。
- 信息来源互相矛盾，需要判断哪些可信。
- 输出会被别人拿去做决策，需要每个结论都有出处。
- 想把同一套工作方法移植到其他模型或 agent。

### 它会强制什么

- 先核对用户请求里的事实前提，再动手。
- 每个事实、数字、路径、命令、配置值都要能说出来源。
- 输出第一句话就是结论，然后才是论据和细节。
- 模糊词要换成数字、对比、例子，或明确写成待确认。
- 没有真实运行验证，就不能说测试通过或工作完成。
- 每次交付都使用五字段：结论、前提核对、验证方式、相邻发现、待确认。

### 用 npx 安装

先查看仓库里可安装的 skill：

```bash
npx skills add yinguangyao/evidence-first-skill --list
```

安装到 Codex 的全局 skills 目录：

```bash
npx skills add yinguangyao/evidence-first-skill --skill evidence-first --agent codex --global
```

非交互安装：

```bash
npx skills add yinguangyao/evidence-first-skill --skill evidence-first --agent codex --global --yes
```

安装后，开启一个匹配描述的任务，或明确要求 Codex 使用 `evidence-first`。

### 手动安装

也可以直接 clone 到 Codex skills 目录：

```bash
mkdir -p ~/.codex/skills
git clone git@github.com:yinguangyao/evidence-first-skill.git ~/.codex/skills/evidence-first
```

### 移植到其他模型

1. 把 `methodology.md` 的完整内容放进目标模型的 system prompt 或第一条消息。
2. 布置任务时要求它显式输出“侦察发现”和“验证方式”。
3. 产出后新开一个上下文，把 `review.md` 和产出物一起交给模型做敌对评审。
4. 抽查每个论断的来源；标不出来源的，一律改写为“待确认”。

## English

### What It Is For

This skill is for non-trivial work such as research, analysis, debugging, planning, writing, and code delivery. It is useful when:

- Time is tight, but factual accuracy still matters.
- Sources disagree and claims need to be downgraded or verified.
- The output will be used as decision-making material.
- You want to port the same working style to another model or agent.

### What It Enforces

- Check factual premises in the user's request before acting.
- Attach evidence to every factual claim, number, path, command, or config value.
- Put the conclusion in the first sentence, then support it.
- Replace vague language with numbers, comparisons, examples, or explicit uncertainty.
- Never claim tests passed or work is complete unless verification actually ran.
- Always deliver with five fields: conclusion, premise check, verification, adjacent findings, and pending confirmations.

### Install With npx

List the available skills in this repository:

```bash
npx skills add yinguangyao/evidence-first-skill --list
```

Install globally for Codex:

```bash
npx skills add yinguangyao/evidence-first-skill --skill evidence-first --agent codex --global
```

Install non-interactively:

```bash
npx skills add yinguangyao/evidence-first-skill --skill evidence-first --agent codex --global --yes
```

After installation, start a task that matches the skill description, or explicitly ask Codex to use `evidence-first`.

### Manual Install

You can also clone the repository into your Codex skills directory:

```bash
mkdir -p ~/.codex/skills
git clone git@github.com:yinguangyao/evidence-first-skill.git ~/.codex/skills/evidence-first
```

### Portable Use

For another model or agent:

1. Paste the full contents of `methodology.md` into the system prompt or first message.
2. Ask the model to expose scout findings and verification in the deliverable.
3. After it produces output, open a fresh context and paste `review.md` plus the output for adversarial review.
4. Treat every unsupported claim as pending confirmation.

## Files

- `SKILL.md`: Codex skill entry point.
- `methodology.md`: Portable rules that can be pasted into another model's system prompt or first message.
- `phases.md`: Templates for splitting long work into clarify, scout, plan, execute, and deliver phases.
- `review.md`: Adversarial review prompt for a fresh context after producing the deliverable.

## Maintenance Contract

The core rules are duplicated in `SKILL.md` and `methodology.md` so Codex gets the rules immediately while the portable version stays easy to copy. If you change any rule, update both files. `methodology.md` is the source of truth.

核心规则在 `SKILL.md` 和 `methodology.md` 中各保留一份，方便 Codex 加载，也方便复制到其他模型。修改任何规则时必须同步更新两处；`methodology.md` 是基准。
