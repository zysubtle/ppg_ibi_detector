# Phase A 自审清单

状态：当前有效
用途：供 Architect / Reviewer、Owner 和 Codex 在关键阶段自审使用。

---

## 1. 完全重新开始自审

在任何输出前检查：

- [ ] 是否没有自动沿用旧 Project Brief？
- [ ] 是否没有自动沿用旧 Algorithm Blueprint？
- [ ] 是否没有自动沿用旧 Decision Cards？
- [ ] 是否没有自动沿用旧 M1 包？
- [ ] 是否没有自动沿用旧 Codex 任务？
- [ ] 是否没有把旧对话结论当作当前有效决策？
- [ ] 是否明确当前只处于 Phase A？

---

## 2. M0 自审

M0 输出前检查：

- [ ] 是否只输出问诊表、关键假设、后置问题？
- [ ] 是否没有生成 Project Brief？
- [ ] 是否没有生成 Deep Research Prompt？
- [ ] 是否没有生成 Codex 任务？
- [ ] 是否没有写代码？
- [ ] 问题是否按决策点合并？
- [ ] 是否覆盖 Phase A 特有问题，如 online constraint、truth contract、golden output、Phase A exit gate？

---

## 3. Project Brief 自审

Project Brief 输出前检查：

- [ ] 是否只基于 Owner 本轮回答？
- [ ] 是否区分已确认决策、待确认决策、关键假设和风险？
- [ ] 是否说明是否需要 Deep Research？
- [ ] 是否没有提前生成 Codex 任务？
- [ ] 是否没有把算法路线写成已达标？

---

## 4. Deep Research 自审

生成 Deep Research Prompt 前检查：

- [ ] Owner 是否已接受 Project Brief v0.1？
- [ ] Owner 是否明确要求生成 Deep Research Prompt？
- [ ] Prompt 是否要求 Evidence Traceability？
- [ ] Prompt 是否要求 License / Dependency Risk Review？
- [ ] Prompt 是否要求 Engineering Decision Boundary？
- [ ] Prompt 是否明确 Blueprint 不是 Codex 任务？

---

## 5. Phase A 实现前自审

进入 M1 前检查：

- [ ] Owner 是否接受 Project Brief v0.2 或风险豁免？
- [ ] 是否已经明确 Phase A 只做 Python Reference Simulator？
- [ ] 是否已经明确禁止 C 主算法实现？
- [ ] 是否已经明确数据契约和测试数据策略？
- [ ] 是否已经明确评估协议？
- [ ] 是否已经明确参数治理？
- [ ] 是否已经明确 golden output 规格？

---

## 6. Codex 任务自审

生成或执行 `docs/10_CODEX_NEXT_TASK.md` 前检查：

- [ ] 是否明确当前 Milestone？
- [ ] 是否明确目标分支？
- [ ] 是否明确工作分支？
- [ ] 是否明确允许修改文件？
- [ ] 是否明确禁止事项？
- [ ] 是否明确测试命令？
- [ ] 是否明确 PR 描述要求？
- [ ] 是否明确完成报告要求？
- [ ] 是否明确不得直接实现 C 主算法，除非已进入 Phase B？
- [ ] 是否明确不得提交未确认的人体生理数据？

---

## 7. Phase A Exit 自审

Phase A 结束前检查：

- [ ] Python Reference Simulator 是否能完整运行？
- [ ] 输出字段是否稳定？
- [ ] 评估协议是否稳定？
- [ ] 参数表是否稳定？
- [ ] invalid reason 是否稳定？
- [ ] online constraint 是否通过审查？
- [ ] golden output 是否生成？
- [ ] 错误案例是否审查？
- [ ] 是否记录达标或未达标原因？
- [ ] Owner 是否明确批准进入 Phase B？
