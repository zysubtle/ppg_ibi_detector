# PPG-IBI Detector M1 Package

本包用于 OAR-M 流程中的 M1：项目文档包与 Codex 任务文件。

## 使用方式

1. 将本包中的 `docs/*.md` 放入仓库根目录的 `docs/` 下。
2. 对 `docs/10_CODEX_NEXT_TASK.md` 采用 **完全覆盖 / 替换**。
3. 让 Codex 严格执行仓库中的 `docs/10_CODEX_NEXT_TASK.md`。
4. Codex 应从 `dev` 创建工作分支，PR 目标分支为 `dev`，不得 merge。

## 本包范围

本包只包含 M1 文档与 Codex 任务文件，不包含生产算法实现代码。M1 的 Codex 任务范围是：

- 项目文档落库；
- 数据契约；
- 评估协议；
- 接口草案；
- Python baseline / CLI 骨架；
- 合成 fixture 与 smoke test；
- 不实现 MCU 主算法；
- 不复制第三方源码；
- 不提交真实人体生理数据，除非 Owner 另行明确确认。
