# Anthropic 开源！23页官方指南：用Claude Code搞定几乎一切工作！

> **Anthropic 内部团队如何使用 Claude Code —— 变革工作流：从开发人员到非技术人员的实战案例**

📄 **[点击查看完整PDF指南](./Inside_Anthropic_Claude_Code.pdf)**

---

## 概述

这是 Anthropic 官方发布的内部案例研究合集，揭示了 Anthropic 内部团队如何利用 Claude Code 改造工作流程。不仅仅是代码助手，而是**工作方式的全面转型**——使开发人员和非技术人员都能处理复杂项目，并填补此前限制生产力的技能空白。

**三大核心价值：**
- **自动化 (Automation)** —— 处理重复性任务
- **填补技能缺口 (Bridging Skill Gaps)** —— 赋能非技术人员
- **复杂项目 (Complex Projects)** —— 加速工程开发

---

## 目录

- [第一部分：数据与基础设施](#第一部分数据与基础设施)
- [第二部分：产品开发与工程](#第二部分产品开发与工程)
- [第三部分：数据科学与 API](#第三部分数据科学与-api)
- [第四部分：增长、设计与法律](#第四部分增长设计与法律)
- [跨团队核心洞察](#跨团队核心洞察)

---

## 第一部分：数据与基础设施

> 自动化核心流程与民主化数据访问

### 案例 1：Kubernetes 调试 — 自动化运维

- **痛点：** 集群故障，Pod 无法调度，通常需要网络专家介入
- **做法：** 将仪表盘截图发送给 Claude Code → Claude 引导浏览 Google Cloud UI → 发现 IP 地址耗尽 → Claude 提供创建新 IP 池的精确命令
- **成果：** 无需专家介入即可解决，大幅缩短故障排除时间

### 案例 2：财务工作流自动化 — 赋能财务团队

- **背景：** 针对无代码经验的财务人员
- **工作流：** 财务人员编写纯文本 (Plain text) 描述需求 → Claude Code 自动执行"查询此仪表盘，运行这些查询，生成 Excel"
- **影响：** 财务团队无需编码经验即可独立执行复杂工作流（Self-Service）
- **亮点：** 在多个代码库实例之间切换时，保持完整的上下文记忆（No context loss）

### 案例 3：文档持续改进循环 (The Documentation Loop)

- **流程：** 新员工入职（读取 Claude.md）→ 解释数据管道 → 会话结束（总结工作）→ 提议改进 Claude.md → 持续优化
- **专家建议：** 编写详细的 `Claude.md` 文件；建议使用 MCP 服务器而非 CLI 处理敏感数据以确保安全

---

## 第二部分：产品开发与工程

> 构建自给自足的开发循环

### 案例 4：Auto-accept Mode（自动接受模式）— 快速原型与核心功能开发

- **工作流：** 启用 Shift+Tab → Claude 编写代码、运行测试、持续迭代 → 工程师审查 **80% 完成** 的解决方案
- **前提条件：** 从干净的 git 状态开始，定期提交 checkpoint
- **适用场景：** 核心业务逻辑的同步编码（Synchronous Coding），工程师提供详细 Prompt → 实时监控代码质量与风格 → Claude 处理重复性编码工作

### 案例 5：Vim Mode — 异步开发的自主实现

- **场景：** 异步项目，非优先级功能
- **成果：** **70%** 的最终实现代码由 Claude 自主完成
- **影响领域：**
  - **Test Generation（测试生成）：** 实现功能后自动编写全面测试 → 利用 GitHub Actions 处理 PR 评论
  - **Codebase Exploration（代码库探索）：** 在单体仓库 (Monorepo) 中快速理解陌生代码，无需等待同事回复 Slack
- **顶级建议：** 建立自给自足的循环 — 要求 Claude 在写代码前先生成测试，并让它运行构建和 Lint 检查来验证自己的工作

### 案例 6：Security Engineering — 缩短事件响应时间

- **核心用例：**
  - **Infrastructure Debugging（基础设施调试）：** 输入堆栈跟踪 (Stack traces) → Claude 追踪控制流 → 快速定位生产环境问题
  - **Terraform Review（Terraform 审批）：** 将 Terraform 计划复制给 Claude → 询问 "What's this going to do? Am I going to regret this?" → 加速安全审批
- **效率提升：** 手动代码扫描 15 分钟 → Claude 诊断仅需 **5 分钟**
- **专家建议：** 让 Claude "边做边提交" (commit your work as you go)，而不是只问代码片段的问题

### 案例 7：Inference 团队 — 跨越机器学习的知识鸿沟

- **效率提升：** 研究时间减少 **80%**
- **Knowledge Bridging（知识桥接）：**
  - **Concept Explanation（概念解释）：** 解释模型特定函数和设置，原本 1 小时 Google 搜索 → 现在 10-20 分钟 Claude 解释
  - **Cross-language Translation（跨语言翻译）：** 描述意图 → Claude 用 Rust 编写逻辑 → 无需学习新语言
- **Kubernetes Management：** 询问"如何获取所有 pod" → 接收编切命令 → 无需记忆复杂语法

### 案例 8：RL Engineering — 监督下的自主性与实验文化

- **工作流策略：Try and Rollback**
  - 频繁提交 Checkpoints → 测试 Claude 的自主实现 → 鼓励实验性开发
  - 失败 → Rollback；成功 → Commit
- **用例：**
  - **Feature Dev（功能开发）：** 编写中小规模功能（如权重传输组件）
  - **Documentation（文档）：** 自动添加注释，加速文档编写
- **现实检验：** 首次尝试成功率约为 **1/3**
- **建议：** 在 `Claude.md` 中添加指令防止重复工具调用（'Just use the right path'）

---

## 第三部分：数据科学与 API

> 构建持久化工具与上下文理解

### 案例 9：Data Science — 从"一次性脚本"到"持久化应用"

- **转变：**
  - **Before（之前）：** 废弃的 Jupyter Notebooks（一次性使用）
  - **After（之后）：** 可复用的 React 仪表盘（Persistent React Dashboards）
- **影响：** 即使"不懂 JavaScript/TypeScript"，也能构建 **5,000 行** 代码的应用程序
- **"老虎机方法" (The Slot Machine Method)：** 保存状态 → 让 Claude 自主工作 30 分钟 → 接受结果或重新开始（比修复错误更高效）
- **深层价值：** 深入理解模型训练性能，而不仅仅是看单个数字的变化

### 案例 10：API Knowledge — 消除上下文切换成本

- **增强信心 (Increased Confidence)：** 团队成员可以独立调试陌生代码库中的 bug，无需询问他人
- **Dogfooding：** 自动使用最新的研究模型快照 (Research model snapshots) → 在开发中直接体验模型行为变化
- **工作流转变：**
  - **旧方式：** 复制粘贴代码片段 → 拖拽文件到 Claude.ai → 耗费脑力整理上下文
  - **新方式：** 直接在终端问 → 自动获取 Monorepo 上下文 → "First stop"（任务的第一站）

---

## 第四部分：增长、设计与法律

> 创意自动化与非技术人员赋能

### 案例 11：Growth Marketing — 自动化创意生成 (10x Output)

- **创意产出提升 10 倍**
- **Google Ads Automation：** 处理 CSV → 识别表现不佳的广告 → 生成数百个符合字符限制 (30/90 chars) 的新变体
- **Figma Plugin：** 编程生成 100+ 广告变体 → 替换标题和描述 → 半秒钟完成一小时的工作
- **Meta Ads MCP：** 直接在 Claude Desktop 中查询广告支出和效果，无需切换平台
- **战略转变：** 从手动执行转向构建 Agentic Automation（代理自动化）

### 案例 12：Product Design — 设计与工程的无缝融合

- **核心工作流：Image Pasting for Prototyping**
  - 粘贴截图 → Claude 生成功能性原型 → 工程师直接理解交互意图，取代静态的 Figma 设计图
- **Frontend Polish（前端打磨）：** 设计师直接修改字体、颜色、间距 (Visual tweaks) → 无需与工程师反复沟通
- **两种体验：**
  - 开发者："强力工作流"
  - 非技术用户："Holy crap, I'm a developer"（天哪，我成了开发者）
- **建议：** 明确告诉 Claude "我是设计师，不懂代码"，要求它逐步解释

### 案例 13：Legal — 法律部门的无代码原型与自动化

- **原型驱动创新 (Prototype-driven Innovation)：**
  - **Accessibility Tools：** 为有语言障碍的家庭成员构建语音应用（1小时内完成）
  - **Workflow Automation：** 构建 'Phone tree' 原型 → 帮助员工联系合适的律师
  - **Compliance：** 快速构建合规工具，平衡创新与风险管理
- **工作模式：**
  - **Planning（规划）：** 在 Claude.ai 中进行头脑风暴
  - **Building（构建）：** 在 Claude Code 中逐步实现

---

## 跨团队核心洞察

| 洞察 | 描述 |
|------|------|
| **Documentation is Code** | 编写详细的 `Claude.md` 是让 Claude 变聪明的关键（Data Infra 团队经验） |
| **Iterative Partnership** | 把 Claude 当作合作伙伴而非一次性解决方案；建立自给自足的测试循环（Product Dev 团队经验） |
| **Context First** | 利用 MCP 服务器和自动上下文获取，减少手动复制粘贴（Security/API 团队经验） |
| **Don't Fear the Code** | 非技术人员应利用截图和自然语言大胆尝试原型设计（Design/Legal 团队经验） |

> **从 10x 营销产出到 5 分钟的安全调试，Claude Code 正在重新定义"谁可以构建软件"。**

---

## 关于本指南

本文件为 Anthropic 官方发布的内部案例研究合集（Internal Case Study Anthology），基于对内部深度用户的访谈整理。涵盖工程、数据基础设施、产品开发、安全、机器学习推理、数据科学、增长营销、产品设计和法律等多个部门的真实使用场景。

**变革已经开始。Anthropic 内部团队正在定义人机协作的未来。**

---

*由 NotebookLM 整理呈现*
