# Deep Research 与 Algorithm Blueprint 协议

版本：v2.0-PhaseA-中文
状态：当前有效流程文档
适用范围：算法协作项目、信号处理项目、嵌入式算法项目、数据驱动算法项目。

---

## 1. 协议目标

Deep Research 的目标不是直接产出最终工程决策，而是提供可审查、可追溯、可比较的算法研究资料，供 Architect / Reviewer 审查，并由 Owner 最终确认。

Algorithm Blueprint 不能自动成为 Codex 可执行任务。若后续需要工程实现，必须先完成 M0-B 审查，并在 Owner 确认后转化为 `docs/10_CODEX_NEXT_TASK.md`。

---

## 2. 适用条件

满足以下任一条件的项目，默认应视为算法协作项目，并在正式实现前引入 Deep Research / Algorithm Blueprint 流程：

1. 需要选择或设计核心算法路线；
2. 需要参考论文、公开 benchmark、第三方库或工具箱；
3. 涉及信号处理、统计建模、机器学习、传感器融合或医学 / 生理数据分析；
4. 算法效果依赖数据分布、真值定义、评估协议或边界条件；
5. 存在嵌入式资源、实时性或功耗约束；
6. 存在许可证、第三方代码或生产依赖风险；
7. 需要在正式工程实现前比较 baseline 与候选方案。

若 Owner 明确决定跳过 Deep Research，必须走 OAR-M 协议中的风险豁免流程。

---

## 3. Deep Research 执行边界

Deep Research 默认由 Owner 通过以下方式之一执行：

1. 单独的 Deep Research 工具；
2. 单独的新对话；
3. Owner 自行组织的人工调研流程；
4. Owner 指定的其他研究流程。

Architect / Reviewer 在 M0.5 阶段只负责生成 Deep Research Prompt，不自动执行 Deep Research，除非 Owner 明确要求。

生成 Deep Research Prompt 后必须暂停，等待 Owner 提供 Algorithm Blueprint。

---

## 4. Deep Research Prompt 应覆盖的内容

Deep Research Prompt 应要求输出 Algorithm Blueprint，并至少覆盖：

1. 项目目标与约束回顾；
2. 输入、输出、场景和边界条件；
3. 相关论文调研；
4. 相关第三方库 / 工具箱调研；
5. 候选算法路线对比；
6. 推荐主算法路线；
7. 推荐 baseline；
8. 预处理方案；
9. 核心检测 / 估计流程；
10. 结果计算策略；
11. SQI 或质量控制策略；
12. 异常处理与 invalid 机制；
13. 后处理策略；
14. confidence 或可靠性评分；
15. 评估协议；
16. 参数初值建议；
17. 计算量、内存、实时性风险；
18. 目标平台工程化风险；
19. 许可证风险；
20. 不建议采用的算法及原因；
21. 推荐里程碑计划；
22. Open Questions；
23. References；
24. Evidence Traceability；
25. Evidence Strength；
26. Reproducibility Notes；
27. Engineering Decision Boundary。

上述内容可按项目复杂度合并章节，但不得删除关键风险项。

---

## 5. Evidence Traceability 要求

Algorithm Blueprint 对每个关键建议必须标注依据来源。

来源类型至少包括：

1. 论文；
2. 标准、指南或官方文档；
3. 开源库；
4. 工具箱；
5. 公开 benchmark；
6. 工程经验；
7. 作者推断；
8. 待验证假设。

不得把“作者推断”或“工程经验”描述为已被论文或数据验证的事实。

---

## 6. Evidence Strength 分级

建议使用以下分级：

| 等级 | 含义 |
|---|---|
| Strong | 有高相关论文、公开实现、公开 benchmark 或多来源一致支持 |
| Moderate | 有相关论文或工程实现支持，但与当前项目约束不完全一致 |
| Weak | 主要来自有限经验、类比或非完全匹配资料 |
| Assumption | 工程假设，需要后续数据验证 |
| Unknown | 证据不足，必须列为风险或 Open Question |

---

## 7. 第三方资料、benchmark、依赖与源码规则

必须区分以下四类行为：

1. 参考第三方资料；
2. 使用第三方工具做离线 benchmark；
3. 引入第三方代码作为生产依赖；
4. 复制或改写第三方源码。

规则如下：

1. Deep Research 可以调研、总结和引用论文、第三方库、工具箱、公开 benchmark 和非目标语言实现；
2. 使用第三方工具做离线 benchmark 必须标明工具名称、用途、许可证和是否仅用于研究验证；
3. 引入第三方代码作为生产依赖，必须经过 Owner 明确确认；
4. 复制或改写第三方源码，必须经过 Owner 明确确认，并明确许可证、来源、版权和合规风险；
5. 对许可证不清楚、来源不清楚或用途不清楚的第三方代码，不得进入工程实现。

---

## 8. M0-B 审查要求

Architect / Reviewer 在接收 Algorithm Blueprint 后，必须执行 M0-B：Algorithm Blueprint Intake & Gap Review。

M0-B 输出至少包括：

1. Blueprint Intake Summary；
2. Fit-to-Project Review；
3. Evidence Quality Review；
4. Conflict List；
5. Gap List；
6. License / Dependency Risk Review；
7. 目标平台 Feasibility Review；
8. Draft Project Brief v0.2；
9. Algorithm Decision Cards；
10. Blocking Questions；
11. 是否建议进入 M1。

如果 M0-B 后建议进入 M1，也只能提出建议；在 Owner 确认 Project Brief v0.2 前，不得生成 `docs/10_CODEX_NEXT_TASK.md` 或任何 Codex 可执行任务。

---

## 9. 禁止事项

在 Owner 确认前，不得：

1. 把 Deep Research 结论当作最终工程决策；
2. 把未经验证的算法路线描述为已经达标；
3. 将第三方源码复制进工程；
4. 引入新的生产依赖；
5. 改变核心接口、验收标准或里程碑范围；
6. 生成正式实现任务；
7. 跳过 Evidence Quality Review；
8. 忽略许可证风险或数据验证风险；
9. 将 Algorithm Blueprint、M0-B 审查意见或聊天中的临时说明直接当作 Codex 可执行任务。
