# domain-separated-self-boot-agent-runtime

> **BaijiMind · 白鳍智章（别称 DolphinMind · 海豚智章）— 分域受控自举智能体运行时**
> Domain-Separated Controlled Self-Boot Agent Architecture · Trust-domain isolation, privileged governance domain, plugin-based self-boot · MIT License

中文 | [English](README-en.md)

⚠️ 提示：本项目目前为 **v0.1 版本**，用于验证分域受控自举智能体架构，尚未经过大规模生产环境验证，上线使用请自行评估风险。演进路径见文末 [Roadmap](#-roadmap)。

📌 当前状态：概念与架构文档阶段，代码实现推进中——仓库当前核心是[架构白皮书](docs/original-2026-paradigm.md)。

## 简介

本项目以**分域受控自举智能体架构**为设计目标，核心命题是：**如何组织生产，才能让人与 AI 协调配合、各司其职，既支持大规模自主生产、高速自举进化，又全程可控、永不失控？**

系统以可信安全分域作为基础模型，特权管控域是分域体系中的特殊可信域；
v0.1采用「特权管控域 + 若干业务分域」最简实现，架构本身**不强制固定域数量**，支持按需扩展、收缩分域。

面向企业研发场景，对接 IM 与邮件系统，把产品、前端、后端、测试、部署完整研发流程编排为可流转的工作流（可编排、可自组织）；
AI生成插件/代码制品，工作台仅输出产物，禁止直接操作生产域。

整套架构围绕**受控自举**展开：AI 大胆自举、自产工具与工作流，但所有自举须经审批晋升、版本化、可回滚；治理锚点统一把守规则与边界，人在环中审批与定界。

## 🧭 架构总览

核心思想一句话：**如何组织生产，才能让人与 AI 协调配合、各司其职，既支持大规模自主生产、高速自举进化，又全程可控、永不失控？**

愿景：**智能自由生长，秩序永久可控** —— 打造「可控自由」的企业级智能体运行时。

```mermaid
flowchart TD
    subgraph GOV[特权管控域 · 系统安全根]
        direction LR
        P[权限 / 风险校验] --> A[审计日志]
        A --> L[版本锁定]
    end

    IM[IM / 邮件] -->|消息转为需求和企业知识库| WB[工作台 Workbench]

    subgraph BIZ[业务分域 · 互相隔离 · 可演化]
        direction LR
        D1[产品域] --- D2[编码域] --- D3[测试域] --- D4[部署域]
    end

    WB -->|编排研发工作流| BIZ
    BIZ -->|产出代码 / 插件制品| GIT[(制品 / Git)]

    WB -. AI 自产工具（harness）需审批 .-> GOV
    BIZ -. 工作流自举（WASM）需审批 .-> GOV
    GOV -. 统一下发安全规则 .-> BIZ
    WB --x|只出制品、禁止直连生产| PROD[(生产环境)]
```

> 读图要点：特权管控域统一校验安全；业务分域互相隔离、可独立演化；编码工具（harness）与工作流（WASM）自举均需审批；工作台只出制品，不碰生产。

## ✨ 主要特性

- 分域安全隔离模型，特权管控域统一做权限、版本、风险校验
- 对接 IM / 邮件机器人，消息与上传文档转为需求与知识库，AI 持续获取项目上下文
- 内置轻量可视化工作流编排，可配置产品、编码、测试、部署阶段
- 对接多种大模型编码能力，产出插件代码，人工二次修改后提交Git
- **受控自举**：AI 自产工具 / 工作流经审批晋升、版本化、可回滚——自由进化与治理受控一体两面
- 人在环中：自举晋升 / 流程推进 / 规则修订 / 制品合并均有审批把关；责任当前归于人，随 AI 能力提升可转移
- **目标与评估**：任务/目标声明可测完成条件，配与执行者分离的独立评估者判定达成——生成/评估分离，达成才晋升
- 支持对接外部知识库、RAG、图数据库、对象存储
- 可按需新增业务分域，支持后续向分布式集群场景演进

## 📄 文档

- [架构白皮书](docs/original-2026-paradigm.md) ｜范式完整定义、产品定位与双栈技术体系，IP归档文档
- [Architecture Whitepaper (English)](docs/original-2026-paradigm-en.md) ｜英文对照译本，内容与中文原文一致
- [v0.1 实现计划](docs/v0.1-implementation-plan.md) ｜第一版实现计划：关键流程、模块总表、技术决策摘要、实施阶段
- [v0.1 架构决策记录（ADR）](docs/v0.1-key-decisions.md) ｜第一版 16 条关键架构决策与风险清单
- **白鳍智章（BaijiMind）** ｜产品与阐述本范式的文章共用此品牌名——中文名白鳍智章、代号 BaijiMind、别称海豚智章（DolphinMind）
- [项目说明](docs/about-note.md) ｜设计启发、开发说明、未来规划
- [Project Note (English)](docs/about-note-en.md) ｜英文对照版本

> 随着项目演进，此处将陆续补充安全模型、更多架构决策记录（ADR）等文档。

## 🛠 技术栈

> 单 Java 模块化单体，可集群部署，详见[范式白皮书 §8 工程落地](docs/original-2026-paradigm.md#8-工程落地单-java-模块化单体-wasm-沙箱)

- **单 Java 模块化单体**：Spring Boot 3.5 + Java 17，一个进程承载治理/业务/执行/编排/RAG/IM 全部能力，可集群横向扩容
- **自举机制（代码制度）**：编码工具经 **harness 热插拔**；AI 产真实代码（Go）→ TinyGo 编译 WASM → 审批 → **Extism + Endive 沙箱热插拔**（一期纯 Java、零原生依赖）
- 存储：OLTP、OLAP、文档库、Neo4j图库、MinIO对象存储
- LLM 成本 / 用量管理：模型路由、key 池、token 统计、成本报表（承载白皮书 §3.1.4 使用成本）
- 集成：IM / 邮件系统、RAG、Git、大模型API、Penpot（开源 UI 设计）

## 🚧 Roadmap

- v0.1：验证架构，基础域模型、工作流、审批式自举、IM机器人对接
- v0.2：完善RAG、知识库目录绑定、模板管理
- v1.0：稳定性加固，生产环境适配

## 📃 License

This project is under the MIT License - see [LICENSE](./LICENSE) file for details.
