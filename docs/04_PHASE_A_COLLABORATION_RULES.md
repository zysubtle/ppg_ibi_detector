# Phase A 协作规则：Python Reference Simulator

状态：当前有效
用途：定义 Phase A 的边界、核心概念和防错规则。

---

## 1. Phase A 目标

Phase A 的目标是建立 Python Reference Simulator，而不是直接实现 C / MCU 算法。

Python Reference Simulator 应用于：

1. 明确算法行为；
2. 固化评估协议；
3. 验证数据契约和真值契约；
4. 进行错误案例分析；
5. 进行参数收敛；
6. 生成后续 C 移植所需的 golden output；
7. 为 Phase B 提供行为基准。

---

## 2. 两类 Python 代码必须区分

### 2.1 Python Research Prototype

Python Research Prototype 用于快速试验、画图、参数 sweep、错误分析和第三方 benchmark。

它可以更灵活，但其结果不能直接作为 C 移植依据。

### 2.2 Python Reference Simulator

Python Reference Simulator 是后续 C 实现的行为规范来源。

它必须满足：

1. streaming 语义清晰；
2. 不使用超出允许延迟的未来数据；
3. 参数集中管理；
4. 输出字段稳定；
5. 状态机稳定；
6. invalid reason 稳定；
7. 能生成 golden output；
8. 能由 C99 streaming core 复现。

---

## 3. online constraint 规则

Python Reference Simulator 不得使用无法在实时系统中获得的信息。

除非 Owner 后续确认，否则应默认遵守：

1. 不使用全文件未来信息；
2. 不使用 zero-phase 过滤作为 reference 行为；
3. 不使用全文件均值、方差、最大值或最小值作为在线阈值；
4. 不使用完整文件 peak list 再反推实时输出；
5. 每个输出必须记录实际事件时间和输出时间；
6. 任何有效输出都必须能验证延迟约束。

Research Prototype 可以使用离线方法做参考，但必须明确标注为 research-only。

---

## 4. 时间戳与回填规则

Phase A 必须在问诊和后续 Project Brief 中确认以下概念：

1. event timestamp：事件真实发生时间；
2. emit timestamp：算法确认并输出结果的时间；
3. latency：emit timestamp 与 event timestamp 的差值；
4. previous event timestamp：上一个有效事件时间；
5. interval：当前事件与上一个有效事件之间的间隔。

如果允许回填，必须明确：

1. 回填结果使用哪个事件时间；
2. 输出时间如何记录；
3. 最大允许延迟如何验证；
4. 回填是否影响评估匹配。

---

## 5. 真值契约

Phase A 必须确认真值数据是否包含：

1. reference event timestamp；
2. reference interval；
3. reference event quality；
4. 可评估区间；
5. 与 PPG 数据的时间基准关系。

若只有 interval 而没有 reference event timestamp，必须评估是否能唯一恢复 reference event timeline。

真值契约未确认前，不得宣称评估协议稳定。

---

## 6. motion / gating 契约

若存在外部运动标志、质量标志或 gating 信号，必须确认：

1. 时间粒度；
2. 与 PPG 是否同步；
3. 缺失值处理；
4. 是否进入可评估区间定义；
5. 是否直接触发 invalid；
6. 是否进入 coverage 分母。

若当前数据没有运动标志，但 Owner 声明数据场景为静息 / 睡眠，是否允许生成全静止标志，必须由 Owner 明确确认。

---

## 7. 评估协议治理

Phase A 必须明确：

1. matching 规则；
2. 误差计算公式；
3. coverage 分母；
4. invalid 对 coverage 的影响；
5. 漏检定义；
6. 误检定义；
7. per-file 统计；
8. 汇总统计；
9. 错误案例输出字段；
10. 小样本结果不得夸大为泛化结论。

---

## 8. 参数治理

Phase A 必须要求所有核心参数集中管理。

每个参数至少应记录：

1. 参数名；
2. 默认值；
3. 单位；
4. 合法范围；
5. 是否进入 C；
6. 来源；
7. 对准确性和 coverage 的影响；
8. 是否允许后续调参。

禁止 magic number 分散在算法函数中。

---

## 9. Golden Output 规则

Phase A 结束前应生成 golden output，用于 Phase B 的 Python/C 一致性验证。

Golden output 应至少覆盖：

1. 正常片段；
2. 启动阶段；
3. 回填输出；
4. 低质量片段；
5. 无事件片段；
6. 数据缺失；
7. 饱和或异常值；
8. gating 信号触发 invalid；
9. invalid reason；
10. 边界时间戳。

C 实现阶段应以 golden output 作为行为一致性检查依据。

---

## 10. Phase A Exit Gate

Phase A 完成不等于“Python 代码能运行”。

Phase A exit gate 至少应包含：

1. Python reference simulator 能完整运行；
2. 输出字段稳定；
3. 评估协议稳定；
4. 参数表稳定；
5. per-file 结果已生成；
6. 错误案例已审查；
7. online constraint 已审查；
8. golden output 已生成；
9. 若未达标，原因和风险已记录；
10. Owner 明确确认是否允许进入 Phase B。
