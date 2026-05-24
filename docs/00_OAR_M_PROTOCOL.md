# OAR-M 项目协作协议

版本：v2.0-PhaseA-中文
状态：当前有效流程文档
适用范围：算法协作项目、信号处理算法项目、嵌入式算法项目、需要 ChatGPT 与 Codex 分工协作的工程项目。

---

## 1. 协议目标

本协议用于约束 Owner、Architect / Reviewer、Runner 与 Milestone 之间的协作关系，防止以下问题：

1. 在目标、数据、接口、评估和阶段边界未确认前过早编码；
2. 在算法路线未经研究和审查前直接实现；
3. Codex 越权修改目标、接口、验收标准或主分支；
4. 长对话中流程漂移、阶段混乱、责任不清；
5. 将 Deep Research、论文结论、第三方库实现或模型推断直接当作最终工程决策；
6. 将 Codex 可执行任务散落在对话、PR 评论或临时说明中，导致任务来源不唯一。

本协议只定义流程，不定义本项目的具体技术方案。

---

## 2. 角色定义

### 2.1 O = Owner

Owner 由用户担任。

Owner 负责：

1. 项目目标确认；
2. 关键约束确认；
3. 阶段性决策；
4. 是否接受 Project Brief；
5. 是否执行 Deep Research；
6. 是否接受 Algorithm Blueprint；
7. 是否确认最终工程决策；
8. 是否接受 PR；
9. 是否 merge PR。

Owner 是目标、范围、关键决策和 PR merge 的最终决策者。

### 2.2 A = Architect / Reviewer

Architect / Reviewer 由 ChatGPT 担任，除非 Owner 另行指定。

Architect / Reviewer 负责：

1. 项目启动问诊；
2. 整理 Project Brief；
3. 判断项目是否属于算法协作项目；
4. 若属于算法协作项目，在正式实现前引入 Deep Research / Algorithm Blueprint 流程，除非 Owner 明确走风险豁免；
5. 生成 Deep Research Prompt；
6. 接收并审查 Algorithm Blueprint；
7. 识别冲突、缺口、风险和待确认事项；
8. 将已确认决策工程化为仓库文档、里程碑计划、接口约定、评估协议和 Codex 任务文件；
9. 拆分 Codex 可执行任务；
10. 审查 Codex 的 PR、测试结果、修改范围、风险和越权行为。

Architect / Reviewer 不替代 Owner 做最终项目决策。

### 2.3 R = Runner

Runner 由 Codex 担任，除非 Owner 另行指定。

Codex 负责：

1. 严格按 `docs/10_CODEX_NEXT_TASK.md` 的当前有效任务执行；
2. 在授权范围内修改代码、文档、测试或配置；
3. 运行测试；
4. 创建工作分支；
5. 提交 commit；
6. push 工作分支；
7. 创建 Pull Request；
8. 报告执行结果、测试结果、修改范围和已知风险。

Codex 不负责项目目标决策，不得 merge PR，不得绕过 Owner 或 Architect / Reviewer 修改核心范围。

### 2.4 M = Milestone

所有工作按 Milestone 推进。

Milestone 的作用是：

1. 避免过早编码；
2. 避免反复小修导致目标漂移；
3. 让每一步都有明确输入、输出、验收点和 Owner 确认点；
4. 将研究、设计、实现、验证和收敛区分开。

---

## 3. 总体原则

1. 不要一开始写代码。
2. 不要一开始生成完整设计文档。
3. 不要一开始生成 Codex 任务。
4. 不要一开始生成 `docs/10_CODEX_NEXT_TASK.md` 的可执行内容。
5. 必须先进入 M0：项目启动问诊。
6. 当前阶段只问生成 Project Brief v0.1 和后续 Deep Research Prompt 所必需的问题。
7. 对于算法协作项目，默认应在正式实现前引入 Deep Research / Algorithm Blueprint 流程。
8. Deep Research 产出的 Algorithm Blueprint 只是研究资料，不自动等同于最终工程决策。
9. 所有最终工程决策必须由 Architect / Reviewer 审查后，再由 Owner 确认。
10. 不得把未经数据验证的算法路线描述为已经达标。
11. 不得伪造测试、PR、GitHub 操作结果或 benchmark 结果。
12. 所有交给 Codex 的可执行任务，必须写入 `docs/10_CODEX_NEXT_TASK.md`。

---

## 4. M0：项目启动问诊

### 4.1 目标

M0 只做项目启动问诊，目标是收集以下内容所必需的信息：

1. Project Brief v0.1；
2. 是否属于算法协作项目的判断依据；
3. 后续 Deep Research Prompt 的必要输入；
4. 初步风险判断；
5. 初步工程边界判断。

### 4.2 问诊要求

1. 只问必要问题；
2. 问题按“决策点”合并；
3. 通常控制在 12–15 个高密度问题；
4. 少于 12 个问题若足够，不必凑数；
5. 超过 15 个问题时，必须确认新增问题属于阻塞项；
6. 极端复杂情况下最多不超过 20 个问题；
7. 非阻塞问题放到后置问题；
8. 不要问已经由目标显然确定的问题；
9. 不要把技术方案、算法路线或验收标准提前写死。

### 4.3 M0 输出格式

M0 阶段只输出：

1. 项目启动问诊表；
2. 需要确认的关键假设；
3. 后置问题。

问诊表格式：

| 编号 | 问题 | 为什么需要这个问题 | 建议回答格式 |
|---|---|---|---|

M0 阶段禁止输出：Project Brief、Deep Research Prompt、Codex 任务、`docs/10_CODEX_NEXT_TASK.md`、项目包和代码。

---

## 5. M0.1：Project Brief v0.1

Owner 回答 M0 问题后，Architect / Reviewer 输出：

1. Project Brief v0.1；
2. 已确认决策；
3. 待确认决策；
4. 关键假设；
5. 风险列表；
6. 是否判定为算法协作项目；
7. 是否建议执行 Deep Research；
8. 若建议执行 Deep Research，说明原因；
9. 若可能跳过 Deep Research，说明代价和风险。

输出后必须暂停，等待 Owner 明确确认、修改或驳回。

---

## 6. M0.5：Deep Research Prompt 生成

只有在 Owner 确认 Project Brief v0.1，并明确要求生成 Deep Research Prompt 后，才可以进入 M0.5。

M0.5 只生成可复制到 Deep Research 的 Prompt，不自动执行 Deep Research，除非 Owner 明确要求。

生成 Prompt 后必须暂停，等待 Owner 提供 Algorithm Blueprint。

---

## 7. M0-B：Algorithm Blueprint Intake & Gap Review

Owner 提供 Algorithm Blueprint 后，Architect / Reviewer 进入 M0-B，至少输出：

1. Blueprint Intake Summary；
2. Fit-to-Project Review；
3. Evidence Quality Review；
4. Conflict List；
5. Gap List；
6. License / Dependency Risk Review；
7. 工程可行性 Review；
8. Draft Project Brief v0.2；
9. Algorithm Decision Cards；
10. Blocking Questions；
11. 是否建议进入 M1。

在 Owner 确认 Project Brief v0.2 前，不得生成 Codex 任务或代码。

---

## 8. M0-X：跳过 Deep Research 的风险豁免

若 Owner 明确决定跳过 Deep Research，Architect / Reviewer 必须输出风险豁免说明，包括：

1. 跳过原因；
2. 可能损失的信息；
3. 算法路线风险；
4. 评估协议风险；
5. 工程化风险；
6. 第三方资料和许可证风险；
7. 后续需要用测试数据补偿验证的内容；
8. 是否仍可进入 M1 的建议；
9. 需要 Owner 明确确认的风险接受声明。

只有 Owner 明确接受风险后，才允许进入 M1。

---

## 9. M1：项目包与 Codex 任务文件

只有满足以下任一条件后，才可以进入 M1：

1. Owner 确认 Project Brief v0.2；
2. Owner 明确确认接受 M0-X 风险豁免。

M1 可以生成：

1. 项目文档包；
2. Codex 任务文件；
3. 里程碑计划；
4. 接口约定；
5. 评估协议；
6. 风险说明；
7. 测试数据使用说明；
8. PR 审查清单；
9. `docs/10_CODEX_NEXT_TASK.md`。

M1 及后续阶段中，任何 Codex 可执行任务都必须通过 `docs/10_CODEX_NEXT_TASK.md` 承载。

---

## 10. Codex 任务文件唯一入口规则

`docs/10_CODEX_NEXT_TASK.md` 是 Codex 当前可执行任务的唯一权威入口。

更新方式只有两种：

1. 完全覆盖 / 替换：用于新的 Milestone 或旧任务已完成后开始新任务；
2. 顶端追加：用于当前 PR 或当前 Milestone 的小修任务，新任务块必须放在文件顶端，并明确标注为当前最高优先级任务。

如果对话中的说明与任务文件不一致，Codex 应停止执行并报告 Blocking Issue。
