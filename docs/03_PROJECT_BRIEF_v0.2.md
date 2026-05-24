# Project Brief v0.2：PPG-IBI Detector

Status: Owner accepted
Stage: M1 input
Target repository: `zysubtle/ppg_ibi_detector`
Target branch: `dev`

---

## 1. Project Goal

开发一个面向 nRF54L15 / C99 / Keil 的嵌入式 MCU 端单通道腕部 PPG-IBI 自研算法。

IBI 定义：

> 相邻 PPG 主峰之间的时间间隔，单位 ms。

首版输出逐搏 IBI，不输出 HR。

---

## 2. Runtime Input

| Input | v0.2 Definition |
|---|---|
| PPG | 单通道 raw PPG，50 Hz，范围 0–1，已扣环境光 |
| timestamp | 必须有，单位在 `docs/05_DATA_CONTRACT.md` 固定 |
| motion flag | 逐采样点 binary，同步；`1`=运动，`0`=静止；缺失按运动处理 |
| ECG RRI | 仅作为评估真值，不进入 MCU runtime |

Known PPG anomalies:

- dropout / 丢点；
- saturation / 饱和；
- gain jump / 增益突变；
- low perfusion / 低灌注；
- loose wearing / 轻度佩戴松动；
- contact loss / 接触失效。

---

## 3. Runtime Output

首版建议输出字段：

| Field | Description |
|---|---|
| `valid` | 是否输出有效 IBI |
| `ibi_ms` | 有效时输出主峰-主峰 IBI |
| `peak_timestamp_ms` | 当前主峰实际时间戳 |
| `prev_peak_timestamp_ms` | 上一有效主峰实际时间戳 |
| `confidence` | 0–1 或 0–100，接口阶段固定 |
| `sqi` | 当前 beat / 短窗信号质量 |
| `state` | 算法状态 |
| `invalid_reason` | invalid 原因枚举 |

Initial invalid reason enum:

```text
startup
motion_flag
motion_flag_missing
dropout
timestamp_gap
saturation
gain_jump
low_sqi
no_peak_candidate
unstable_interval
wear_loose_or_contact_loss
out_of_range_ibi
internal_state_not_ready
```

---

## 4. Supported and Unsupported Scenarios

| Type | v0.2 Definition |
|---|---|
| Supported | 静息、睡眠、`motion_flag=0` 的日常轻微活动、低灌注、轻度佩戴松动 |
| Unsupported | 走路、跑步、强运动、`motion_flag=1`、motion flag 缺失、明显佩戴松动、接触失效 |
| Unsupported output | `invalid` |

运动场景不纳入首版验收。

---

## 5. Realtime Requirements

| Requirement | Value |
|---|---|
| Processing mode | 实时 / streaming |
| Window | 8 s |
| Sampling rate | 50 Hz |
| Output cadence | 逐搏 |
| Startup delay | 5 s |
| Max output delay | ≤ 2 s |
| Future samples | 允许 |
| Backfill | 允许，使用实际峰时间戳 |

---

## 6. Evaluation Targets

| Metric | v0.2 Definition |
|---|---|
| IBI MAE | one-to-one 匹配成功的 valid IBI 与 ECG RRI 的绝对误差均值 |
| Coverage | evaluable period 内，成功匹配且输出 valid IBI 的数量 / ECG RRI beat 数 |
| Matching tolerance | ±100 ms |
| Statistics | per-file |
| Target | per-file IBI MAE < 60 ms；per-file coverage > 90% |
| Error cases | 必须输出 beat-level error CSV |

Evaluable period 暂定为：

> 验收场景 ∩ `motion_flag=0` ∩ motion flag 存在 ∩ 非严重输入故障时段。

---

## 7. Accepted Algorithm Direction

Owner 已接受以下候选主路线进入工程验证：

> 低阶带通 + ERMA 风格候选增强 + 局部导数 / upslope 辅助主峰定位 + 逐搏 SQI + template/morphology consistency + 生理间期门控 + 外部运动 hard invalid + ≤2 s 回填确认。

Boundary:

1. MSPTDfast / ppg-beats 只作为 PC 离线强基线 / research-only 上界参考，不作为 MCU 首版主干。
2. SPAR 只作为 ambiguous peak 研究对照，不作为首版。
3. 深度学习、小模型、重型频域算法不进入首版。
4. 不复制第三方源码，不引入生产依赖。
5. M1 不直接实现 MCU 主算法，只建立文档、数据契约、评估协议和 Python baseline / CLI 骨架。

---

## 8. Target Platform

| Item | Value |
|---|---|
| MCU | nRF54L15 |
| RAM budget | 15 KB |
| Flash budget | 30 KB |
| FPU | Unknown |
| float | Allowed, but fixed-point fallback should remain possible |
| Dynamic memory | Forbidden |
| C standard | C99 |
| Compiler | Keil |

---

## 9. Delivery Path

1. PC / Python offline validation;
2. C99 streaming implementation;
3. MCU porting and resource profiling.

M1 only creates the foundation for step 1.

---

## 10. Product Wording Boundary

Product positioning: medical-grade engineering quality, but no medical claims.

禁止表述：诊断级、临床达标、可用于诊断 / 筛查 / 治疗、医学疗效承诺。

允许表述：更严格的工程质量要求、更严格的错误案例分析、不作为医学诊断、治疗、筛查依据。
