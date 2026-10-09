# Project-Centric Intelligence (PCI)

> 项目中心智能：让项目成为长期智能的主体，让 AI 模型成为可替换的智能引擎。

## 一句话定义

PCI 认为长期智能的基本主体不是 AI Agent，而是 Project。项目持续拥有知识、状态、经验、策略和文档，LLM 只是可替换引擎。通过执行—反馈—经验—验证—策略—再执行的闭环，项目不断积累智能、自组织生长，最终从完成单个任务成长为能驱动公司的数字组织。

## 核心命题

- **Project as Subject**：项目是长期主体。
- **Model as Engine**：模型是可替换引擎。
- **Project Continual Intelligence**：项目因过去而改变未来行为。
- **Experience Capitalization**：经验成为项目的数字资本。
- **Dual-Mode Production**：ReAct 探索，Workflow 固化。
- **Self-Evolution**：进化引导文件、工作流和元规则。
- **Documentation as Protocol**：文档是项目智能的接口。
- **Validation as Selection Pressure**：无验证，不入策略。

## 与 Goal 模式区别

```text
Goal：目标 → 执行 → 完成 → 结束。
PCI：Project → Goal → Work → Feedback → Experience → Validation → Strategy → 新 Goal。
```

Goal 是项目当前要做的事；Project 才是长期智能主体。

## 系统循环

1. Load Project Core
2. Generate or Select Goal
3. Plan & Route
4. Execute
5. Observe
6. Reflect
7. Validate
8. Promote / Reject
9. Update Docs & State
10. Next Goal

## 双模生产

- ReAct：探索态，灵活，文档引导，处理新问题。
- Workflow：固化态，快速，稳定，可复制，规模化。
- 结晶：ReAct 成功解法 → 验证 → 固化为 Workflow。
- 退化：Workflow 失效 → 退回 ReAct → 修复 → 重新结晶或废弃。

## 文档体系

```text
.pci/
  constitution/
  strategy/
  org/
  knowledge/
  state/
  goals/
  experience/
  strategies/
  models/
  audit/
  metrics/
```

## 经验 Schema 核心字段

```text
id, type, scope, status, context, action, outcome, evidence, causal_hypothesis, strategy_candidate, confidence, valid_until, source_model, created_at, updated_at
```

## 策略 Schema 核心字段

```text
id, trigger, preconditions, action, validation, rollback, scope, confidence, priority, cost, owner, version, status, evidence, expires
```

## 验证证据等级

- **L0** 日志
- **L1** 单元测试
- **L2** CI/集成测试
- **L3** 人工 review
- **L4** 线上指标
- **L5** A/B、因果推断、回溯测试

## 重要组件

- Project Core
- Document System
- Experience Store
- Strategy Engine
- Goal Generator
- Model Router
- Validation Engine
- Self-Evolution Engine
- ReAct Runtime
- Workflow Runtime
- Audit & Governance
- Metrics Scorecard

## 生长路线

- 0 单任务
- 1 单 repo 自维护
- 2 项目自组织
- 3 多项目迁移
- 4 组织化
- 5 公司 OS

## 快速开始

建 .pci/，写六个文件：

```text
constitution/constitution.md
state/current.yaml
goals/active.yaml
experience/exp-001.yaml
strategies/strat-001.yaml
models/router.yaml
```

## 最小 CLI

```bash
pci run --goal "修复登录超时" --model claude
pci reflect --run 001
pci validate --exp 001
pci promote --exp 001
pci next
```

## 一句话

PCI 让项目成为长期智能主体；ReAct 负责探索，Workflow 负责生产；自进化引擎不断修改两者，使项目从完成单个任务，成长为能自组织、能驱动公司的数字组织。
