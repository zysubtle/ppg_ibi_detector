# 项目完全重新开始上下文

状态：当前有效
用途：说明当前仓库进入一次完全重新开始的 Phase A 协作流程。

---

## 1. 完全重新开始声明

本仓库当前按照 OAR-M 机制进入一次**完全重新开始**。

除非 Owner 在本轮流程中重新确认，否则以下历史内容均不是当前有效决策：

1. 旧 Project Brief；
2. 旧 Deep Research Prompt；
3. 旧 Algorithm Blueprint；
4. 旧 M0-B 审查；
5. 旧 Algorithm Decision Cards；
6. 旧 M1 包；
7. 旧 `docs/10_CODEX_NEXT_TASK.md`；
8. 旧 PR 说明；
9. 旧对话中的技术结论、参数、算法路线或验收门槛。

历史内容可以作为背景参考，但不能自动进入当前项目决策。

---

## 2. 当前唯一大阶段

当前唯一大阶段是：

> Phase A：Python Reference Simulator

Phase A 的目标是：

> 建立一个可复现、可评估、可作为后续 C99 / MCU 移植依据的 Python reference simulator。

Phase A 不是 C 实现阶段，也不是 MCU 移植阶段。

---

## 3. Phase A 可以包含的内容

Phase A 可以包含：

1. M0：项目启动问诊；
2. Phase A Project Brief；
3. Deep Research / Algorithm Blueprint，若 Owner 确认需要；
4. 数据契约；
5. 真值契约；
6. 评估协议；
7. Python baseline；
8. Python reference simulator；
9. online constraint audit；
10. 参数治理；
11. invalid / confidence / SQI 设计；
12. 回填与延迟定义；
13. 错误案例分析；
14. golden output 规格；
15. Phase A exit report；
16. Phase B 启动条件。

---

## 4. Phase A 禁止事项

Phase A 当前不得包含：

1. C99 主算法实现；
2. MCU core 实现；
3. nRF / 具体芯片移植；
4. 生产依赖集成；
5. 未经确认复制第三方源码；
6. 未经验收就声明算法已经达标；
7. 将 Python research prototype 直接当作 C 移植依据；
8. 在未完成 Phase A exit gate 前启动 Phase B。

---

## 5. Phase B 启动条件

Phase B 是后续 C99 / MCU 实现阶段。

Phase B 只有在以下条件满足后才允许启动：

1. Python reference simulator 已实现并审查；
2. 评估协议稳定；
3. 输出契约稳定；
4. 参数表稳定；
5. invalid reason 稳定；
6. golden output 已生成；
7. Phase A acceptance report 已由 Owner 接受；
8. Owner 明确批准进入 Phase B。

---

## 6. 与 `docs/10_CODEX_NEXT_TASK.md` 的关系

当前没有 Codex 可执行任务。

在 Owner 未确认进入 M1 前，`docs/10_CODEX_NEXT_TASK.md` 只能是“当前无任务”的占位文件，不得承载可执行编码任务。
