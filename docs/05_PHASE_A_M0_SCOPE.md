# Phase A / M0 项目启动问诊范围

状态：当前有效
用途：约束 Phase A 完全重新开始后的 M0 问诊范围。

---

## 1. M0 目标

M0 只做项目启动问诊，目标是收集生成以下内容所需的信息：

1. Phase A Project Brief v0.1；
2. 是否需要 Deep Research 的判断依据；
3. 后续 Deep Research Prompt 的必要输入；
4. Phase A 范围、边界、风险和工程交付形态；
5. Phase B 启动条件的初步判断。

M0 不生成 Project Brief，不生成 Deep Research Prompt，不生成 Codex 任务，不写代码。

---

## 2. M0 必须覆盖的方向

### 2.1 Phase A 目标定义

需要确认：

1. Python Reference Simulator 的目标；
2. 与 Python Research Prototype 的区别；
3. Phase A 的交付边界；
4. Phase B 的启动边界；
5. 当前是否只做 Python，不做 C。

### 2.2 输入数据条件

需要确认：

1. PPG 或其他输入信号；
2. 通道数、采样率、单位、数值范围；
3. 时间戳；
4. 缺失、饱和、增益变化、乱序等异常；
5. 数据规模；
6. 数据能否提交仓库；
7. 是否包含人体生理敏感信息。

### 2.3 真值契约

需要确认：

1. 真值来源；
2. 是否有 reference event timestamp；
3. 是否有 reference interval；
4. 是否能恢复完整 reference event timeline；
5. 与输入信号是否同步；
6. 是否存在人工标注或参考设备误差。

### 2.4 输出契约

需要确认：

1. 输出事件定义；
2. interval 定义；
3. event timestamp；
4. emit timestamp；
5. latency；
6. valid / invalid；
7. invalid reason；
8. confidence / SQI / state；
9. 是否允许回填；
10. 最大输出延迟。

### 2.5 在线约束

需要确认：

1. Python reference 是否必须模拟实时处理；
2. 是否允许使用未来数据；
3. 允许多少未来数据；
4. 是否禁止全文件统计量；
5. 是否禁止 zero-phase 过滤作为 reference 行为；
6. 是否需要 online constraint audit。

### 2.6 评估协议

需要确认：

1. matching 规则；
2. 误差指标；
3. coverage 定义；
4. invalid 对 coverage 的影响；
5. 漏检 / 误检定义；
6. per-file / per-subject / per-scenario 统计；
7. 错误案例输出；
8. 是否需要可视化。

### 2.7 参数治理

需要确认：

1. 是否要求全局参数；
2. 是否允许 per-file 参数；
3. 是否需要参数表；
4. 是否需要参数 sweep；
5. 如何防止小样本过拟合。

### 2.8 Golden Output 与 Phase B

需要确认：

1. C 移植前是否必须有 golden output；
2. golden output 覆盖哪些场景；
3. Python/C 一致性比较方式；
4. Phase B 是否必须由 Owner 明确批准。

### 2.9 第三方资料与依赖

需要确认：

1. 是否允许参考论文；
2. 是否允许参考开源库；
3. 是否允许使用第三方库做离线 benchmark；
4. 是否禁止复制源码；
5. 是否禁止生产依赖；
6. 许可证边界。

---

## 3. M0 输出格式

M0 阶段只输出三部分：

1. 项目启动问诊表；
2. 需要确认的关键假设；
3. 后置问题。

问诊表格式：

| 编号 | 问题 | 为什么需要这个问题 | 建议回答格式 |
|---|---|---|---|

---

## 4. M0 禁止事项

M0 阶段不得：

1. 进入 M1；
2. 生成 Project Brief；
3. 生成 Deep Research Prompt；
4. 生成 Codex prompt；
5. 生成 `docs/10_CODEX_NEXT_TASK.md` 的可执行内容；
6. 生成项目包；
7. 写 Python 代码；
8. 写 C 代码；
9. 修改仓库文件；
10. 沿用旧 Project Brief 或旧任务作为当前有效决策。
