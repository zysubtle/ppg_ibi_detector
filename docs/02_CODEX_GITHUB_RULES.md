# Codex 与 GitHub 协作规则

版本：v2.0-PhaseA-中文
状态：当前有效流程文档
适用范围：使用 Codex 作为 Runner，在 GitHub 仓库中编码、测试、提交分支、创建 PR 的协作项目。

---

## 1. 协议目标

本协议用于约束 Codex 在仓库中的执行权限，防止以下问题：

1. 直接修改 main / master；
2. 未经审查合并 PR；
3. force push 或覆盖历史；
4. 未经确认改变项目目标、接口或验收标准；
5. 未经确认引入第三方依赖或许可证风险；
6. 提交 secrets、隐私数据、受限数据或人体生理敏感数据；
7. 伪造测试结果、PR 链接或 benchmark 结果；
8. Codex 根据聊天中的临时说明执行，而不是根据 `docs/10_CODEX_NEXT_TASK.md` 的当前有效任务执行。

---

## 2. Codex 运行前提

Codex 可以在满足运行环境条件的前提下执行 GitHub 协作操作。

运行环境条件包括：

1. 当前目录是有效 Git 仓库；
2. 已配置正确 remote；
3. 当前环境具备必要 Git 权限；
4. 当前环境具备 GitHub 访问权限；
5. 如需使用 GitHub CLI，则 GitHub CLI 已安装且已登录；
6. 网络访问可用；
7. 仓库分支保护规则允许创建分支和 PR。

如果上述条件不满足，Codex 必须报告缺失条件，不得伪造 push、PR 或测试结果。

---

## 3. Codex 可以执行的操作

在 `docs/10_CODEX_NEXT_TASK.md` 的当前有效任务明确授权范围内，Codex 可以：

1. 基于任务要求自行创建新的工作分支；
2. 在工作分支上修改代码、文档、测试或配置；
3. 运行必要的测试、构建、静态检查或 smoke test；
4. 创建 commit；
5. 将工作分支 push 到远程仓库；
6. 基于该分支创建 Pull Request；
7. 在 PR 描述中报告执行结果。

Codex 的执行必须受以下内容约束：

1. `docs/00_OAR_M_PROTOCOL.md`；
2. `docs/01_DEEP_RESEARCH_PROTOCOL.md`；
3. `docs/02_CODEX_GITHUB_RULES.md`；
4. `docs/10_CODEX_NEXT_TASK.md`；
5. Owner 明确确认的 Project Brief；
6. Owner 明确确认的接口、评估协议和验收标准。

---

## 4. `docs/10_CODEX_NEXT_TASK.md` 任务文件规则

`docs/10_CODEX_NEXT_TASK.md` 是 Codex 当前可执行任务的唯一权威入口。

Codex 不得仅根据以下来源执行任务：

1. 聊天对话中的临时说明；
2. PR 评论中的临时要求；
3. 未落入仓库的外部文档；
4. 口头摘要或审查结论。

如果 Owner 或 Architect / Reviewer 在对话中提出新任务，但没有更新 `docs/10_CODEX_NEXT_TASK.md`，Codex 必须要求先更新任务文件，不得自行执行。

---

## 5. 任务文件更新方式

`docs/10_CODEX_NEXT_TASK.md` 可以通过两种方式更新：

1. 完全覆盖 / 替换：用于新的 Milestone 或旧任务已完成后开始新任务；
2. 顶端追加：用于当前 PR 或当前 Milestone 的小修任务，新任务块必须放在文件顶端，并明确标注为当前最高优先级任务。

如果采用顶端追加方式，Codex 应以最上方的当前最高优先级任务为准；旧任务只能作为背景，不能覆盖当前任务。

---

## 6. 执行前检查

Codex 开始执行前必须检查：

1. 当前分支是否符合任务文件要求；
2. 任务是要求新建分支，还是要求在当前 PR 分支追加 commit；
3. 允许修改哪些文件；
4. 禁止修改哪些文件；
5. 是否允许算法逻辑变更；
6. 是否允许接口 / IO Contract 变更；
7. 是否允许数据格式变更；
8. 是否允许新增依赖；
9. 是否允许提交 fixture 或数据文件；
10. 需要运行哪些测试和检查。

如果任务文件缺少关键信息或与协议冲突，Codex 必须停止并报告 Blocking Issue。

---

## 7. 分支规则

Codex 不得在 main / master 分支上编码。

每个里程碑或明确任务应创建独立工作分支。

推荐分支命名：

```text
feature/m{milestone}-{short-name}
fix/m{milestone}-{short-name}
docs/m{milestone}-{short-name}
test/m{milestone}-{short-name}
```

如仓库已有分支命名规范，应优先遵守仓库规范。

---

## 8. PR 描述要求

Codex 创建 PR 时，PR 描述必须包含：

```markdown
## 摘要

## 修改文件

## 是否改变算法逻辑
- 是 / 否
- 说明：

## 是否改变接口 / IO Contract
- 是 / 否
- 说明：

## 是否改变依赖
- 是 / 否
- 说明：

## 是否改变数据格式
- 是 / 否
- 说明：

## 是否改变测试协议
- 是 / 否
- 说明：

## 测试命令和结果

## 未运行的测试及原因

## 已知风险

## 建议 Reviewer 重点检查

## 超出范围的事项
```

如果未能运行测试，必须说明原因。不得声称测试通过，除非实际执行过对应测试。

---

## 9. Codex 绝对禁止的操作

Codex 绝对禁止：

1. 直接在 main / master 分支上编码；
2. 直接 push 到 main / master；
3. merge PR；
4. 执行任何形式的 PR merge；
5. 启用 auto-merge；
6. 覆盖主分支历史；
7. force push；
8. 未经 Owner 明确确认，修改项目目标；
9. 未经 Owner 明确确认，修改里程碑范围；
10. 未经 Owner 明确确认，修改核心接口约定；
11. 未经 Owner 明确确认，修改 IO Contract；
12. 未经 Owner 明确确认，修改验收标准；
13. 未经 Owner 明确确认，引入新的第三方生产依赖；
14. 未经 Owner 明确确认，引入许可证风险不明的代码；
15. 未经 Owner 明确确认，提交原始大数据集；
16. 未经 Owner 明确确认，提交隐私数据、受限数据或人体生理敏感数据；
17. 提交密钥、token、证书、账号凭据或任何 secrets；
18. 伪造测试结果；
19. 伪造 benchmark 结果；
20. 伪造 PR 链接；
21. 声称完成但未实际执行；
22. 在未更新 `docs/10_CODEX_NEXT_TASK.md` 的情况下，仅凭聊天或 PR 评论执行新任务。

PR 的最终 review、是否接受、是否 merge，只能由 Owner 决定。

---

## 10. 测试数据与 fixture 规则

如果项目涉及真实数据、人体数据、生理数据、设备数据或受限数据，必须遵守：

1. 不得未经 Owner 明确确认提交原始完整数据集；
2. 不得未经 Owner 明确确认提交隐私数据、受限数据或人体生理敏感数据；
3. 不得提交密钥、token、证书、账号凭据或任何 secrets；
4. 允许提交经过 Owner 明确确认的、脱敏的小型 fixture 数据，用于单元测试、smoke test 或 CI；
5. fixture 数据应尽量小、可复现、用途明确，并在文档中说明来源、用途和限制；
6. 如果不能提交真实 fixture，应使用合成数据或最小模拟数据进行测试；
7. 不得把 fixture 测试结果夸大为真实数据集评估结果。
