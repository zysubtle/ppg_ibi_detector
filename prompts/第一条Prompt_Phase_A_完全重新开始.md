我希望按 OAR-M 机制与你协作开发一个算法项目。

仓库：
https://github.com/zysubtle/ppg_ibi_detector

目标分支：
dev

请严格基于该分支阅读和修改代码，不要基于 main 分支。

分支链接：
https://github.com/zysubtle/ppg_ibi_detector/tree/dev

请先阅读并遵守以下仓库文档：

1. `docs/00_OAR_M_PROTOCOL.md`
2. `docs/01_DEEP_RESEARCH_PROTOCOL.md`
3. `docs/02_CODEX_GITHUB_RULES.md`
4. `docs/03_PROJECT_FRESH_START_CONTEXT.md`
5. `docs/04_PHASE_A_COLLABORATION_RULES.md`
6. `docs/05_PHASE_A_M0_SCOPE.md`
7. `docs/06_PHASE_A_SELF_AUDIT_CHECKLIST.md`

如果你当前无法读取这些文档，请明确说明缺少哪些文档，并要求我上传或粘贴。不要在未读取这些文档的情况下自行补全协议细节。

---

## 完全重新开始声明

这是一次完全重新开始。

如果仓库或对话历史中存在旧的 Project Brief、旧 Deep Research Prompt、旧 Algorithm Blueprint、旧 Algorithm Decision Cards、旧 M1 包、旧 `docs/10_CODEX_NEXT_TASK.md` 或旧 Codex 任务，请不要自动沿用。

除非 Owner 在本轮重新确认，否则这些旧内容只能视为历史参考，不能作为当前有效项目决策。

---

## 当前大阶段

当前只启动：

> Phase A：Python Reference Simulator

Phase A 的目标是：

> 先实现一个可复现、可评估、可作为后续 C99 / MCU 移植依据的 Python Reference Simulator，用于 PPG-IBI 检测算法的算法验证、评估协议固化、错误案例分析、参数收敛和算法行为冻结。

Phase A 不是 C 实现阶段。

Phase B 才是：

> 基于 Phase A 已冻结的 Python Reference Simulator，实现 C99 / MCU streaming core，并做 Python/C 一致性验证和 MCU 资源收敛。

Phase B 只有在 Phase A 被 Owner 明确验收后，才允许启动。

---

## 当前项目技术目标

本项目最终长期目标是：

> 开发嵌入式 MCU 端 PPG-IBI 自研算法。

但当前阶段的目标只限于：

> Phase A：Python Reference Simulator。

当前你只知道 Phase A 的阶段目标，不要假设任何额外技术硬约束、数据条件、平台资源、算法路线、验收标准或工程实现方式。

上述仓库流程文档定义的协作流程、阶段门控、角色边界、Deep Research 规则和 Codex / GitHub 权限规则属于流程约束，必须严格遵守。

---

## Codex 任务文件规则

后续凡是需要交给 Codex 执行的任务，包括新里程碑任务、当前 PR 追加修复、文档修订、测试补跑、回归验证、风险收敛或仓库 hygiene 修复，必须通过仓库文件：

```text
docs/10_CODEX_NEXT_TASK.md
```

来承载。

规则如下：

1. 不得只在对话框中给 Codex 一段自由任务或临时任务说明。
2. 如果新任务取代上一任务，应明确要求完全覆盖 / 替换 `docs/10_CODEX_NEXT_TASK.md`。
3. 如果只是对当前里程碑或当前 PR 做小修，而不需要删除原有任务背景，应明确要求将新的任务块粘贴到原有 `docs/10_CODEX_NEXT_TASK.md` 顶端，并标注为当前最高优先级任务。
4. 对话框中可以保留摘要、审查结论和下一步建议，但 Codex 的可执行任务必须以 `docs/10_CODEX_NEXT_TASK.md` 中的任务为准。
5. `docs/10_CODEX_NEXT_TASK.md` 中的任务应至少包含：当前阶段 / Milestone、目标分支或 PR、任务范围、允许修改文件、禁止事项、测试命令、PR 描述要求、完成报告要求和已知风险。
6. 如果对话中的临时说明与 `docs/10_CODEX_NEXT_TASK.md` 不一致，Codex 应停止执行并要求 Owner / Architect 更新任务文件。

当前仓库中的 `docs/10_CODEX_NEXT_TASK.md` 如果是“当前无 Codex 可执行任务”的占位文件，则不得执行任何 Codex 任务。

---

## Phase A 的核心边界

Phase A 应重点确认和设计：

1. Python Reference Simulator 的定义；
2. Python Research Prototype 与 Python Reference Simulator 的边界；
3. online constraint，即 Python reference 不得使用超过允许延迟的未来数据；
4. event timestamp、emit timestamp、latency 的输出定义；
5. 真值契约，尤其是是否需要 reference event timestamp；
6. motion flag / gating 契约；
7. PPG 输入数据契约；
8. one-to-one matching 评估协议；
9. IBI MAE、coverage、漏检、误检、invalid rate 的定义；
10. invalid reason 枚举；
11. 参数治理；
12. golden output 规格；
13. 错误案例输出；
14. 可视化 / debug 工具边界；
15. Phase A exit gate；
16. Phase B 启动条件。

Phase A 当前不得直接实现 C 主算法。

---

## 当前阶段

请现在进入：

> M0：Phase A 项目启动问诊

当前阶段只做项目启动问诊，目标是收集生成 Phase A Project Brief v0.1 和后续 Deep Research Prompt 所必需的信息。

---

## M0 输出要求

请只输出以下三部分：

1. 项目启动问诊表；
2. 需要确认的关键假设；
3. 后置问题。

项目启动问诊表请使用以下格式：

| 编号 | 问题 | 为什么需要这个问题 | 建议回答格式 |
|---|---|---|---|

---

## 当前禁止事项

当前阶段不要：

1. 进入 M1；
2. 生成 Project Brief；
3. 生成 Deep Research Prompt；
4. 生成 Codex prompt；
5. 生成 `docs/10_CODEX_NEXT_TASK.md`；
6. 生成项目包；
7. 写代码；
8. 实现 Python 算法；
9. 实现 C 算法；
10. 创建或修改仓库文件；
11. 沿用旧 Project Brief 或旧 M1 任务作为当前有效决策。
