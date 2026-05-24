# Algorithm Decision Cards v0.2

Status: Owner accepted
Stage: M1 input

---

## D1：首版主算法路线

| Item | Content |
|---|---|
| Decision Topic | 首版 MCU 主算法路线 |
| Candidate Options | 简单时域峰检；ERMA/HeartPy-like；MSPTDfast-like；SPAR；DL |
| Recommended Option | 轻量 hybrid：低阶带通 + ERMA 候选 + upslope 主峰定位 + SQI/template/interval 门控 |
| Rationale | 匹配 50 Hz、单通道、≤2 s、15 KB RAM、30 KB Flash、无生产依赖 |
| Evidence Strength | Moderate |
| Risks | 50 Hz 主峰量化、双峰/肩峰、低灌注、轻度松动 |
| Validation Required | Python baseline + per-file 误例分析 |
| Engineering Decision | Accept with validation |

---

## D2：MSPTDfast / ppg-beats 定位

| Item | Content |
|---|---|
| Decision Topic | MSPTDfast 是否进入首版 |
| Candidate Options | MCU 主干 / PC 强基线 / 不使用 |
| Recommended Option | PC research-only 强基线，不进入 MCU 主干 |
| Rationale | 准确性强，但实现和许可证复杂度高 |
| Evidence Strength | Strong for benchmark relevance；license risk high |
| Risks | ppg-beats 是 mixed-license per-file，不可整体视为 MIT |
| Validation Required | per-file license review；只作离线对照 |
| Engineering Decision | Accept as research-only |

---

## D3：SQI / invalid 策略

| Item | Content |
|---|---|
| Decision Topic | 是否将 SQI/invalid 作为首版核心能力 |
| Candidate Options | 始终输出 / 低质量 invalid / hold-predict |
| Recommended Option | 低质量 invalid，且输出 invalid_reason |
| Rationale | Wrist PPG、低灌注、轻度松动、无 ACC 条件下，错误 valid 比 invalid 更危险 |
| Evidence Strength | Strong for quality gating；thresholds need validation |
| Risks | 过度 invalid 导致 coverage < 90% |
| Validation Required | SQI threshold sweep；coverage-MAE tradeoff 曲线 |
| Engineering Decision | Accept |

---

## D4：评估协议

| Item | Content |
|---|---|
| Decision Topic | IBI MAE / coverage 评估协议 |
| Candidate Options | 最近邻匹配 / one-to-one greedy / ordered matching |
| Recommended Option | one-to-one ordered matching，±100 ms 容忍 |
| Rationale | 与 Owner 已确认规则一致，可记录漏检/误检 |
| Evidence Strength | Moderate |
| Risks | ECG RRI 与 PPG 主峰不是同一事件，matching 语义必须固定 |
| Validation Required | 用小 fixture 验证 corner cases |
| Engineering Decision | Accept |

---

## D5：第三方依赖与源码

| Item | Content |
|---|---|
| Decision Topic | 第三方库使用边界 |
| Candidate Options | 引入依赖 / 只作 benchmark / 只读论文 |
| Recommended Option | Python 阶段可 research-only；生产 C 不引入依赖、不复制源码 |
| Rationale | 符合 Owner 已确认许可证边界和 Codex 规则 |
| Evidence Strength | Strong |
| Risks | ppg-beats mixed license；GPL 工具污染生产代码 |
| Validation Required | M1 license appendix |
| Engineering Decision | Accept |

---

## D6：MCU 实现策略

| Item | Content |
|---|---|
| Decision Topic | float / fixed-point / buffer 策略 |
| Candidate Options | 全 float / fixed-point only / float reference + fixed-point fallback |
| Recommended Option | float reference + fixed-point fallback 预留 |
| Rationale | FPU 未知，float 允许但不能假设最终成本 |
| Evidence Strength | Assumption |
| Risks | 15 KB / 30 KB 估算可能低估 |
| Validation Required | C map 文件、RAM 静态表、cycle/profile |
| Engineering Decision | Accept with profiling |

---

## D7：数据提交策略

| Item | Content |
|---|---|
| Decision Topic | 5 个真实文件是否进入仓库 |
| Candidate Options | 全量提交 / 小 fixture / 合成数据 |
| Recommended Option | Owner 再确认脱敏与仓库可见性后再决定；M1 默认只提交合成 fixture |
| Rationale | 生理数据存在敏感性，Codex 规则要求明确确认 |
| Evidence Strength | Strong protocol requirement |
| Risks | 原始生理数据、隐私字段、公开仓库风险 |
| Validation Required | 数据字段审计 |
| Engineering Decision | Accept：M1 不提交真实人体生理数据 |
