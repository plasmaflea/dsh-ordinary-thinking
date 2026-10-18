# 仓库状态与接手说明

> 给**下一个会话**看的。权威顺序：`git` 与磁盘 > 本文件 > 任何记忆/摘要。本文件里的哈希与版本会过期，**先用脚本拉一次真实状态**：
>
> ```powershell
> D:\DeepSeek-levelup\dsh-thinking-models\scripts\state.cmd -Repo D:\DeepSeek-levelup\dsh-ordinary-thinking
> ```

---

## 1. 这是什么

一个**研究用**技能：把普通人「先有答案、再补理由」的思考**完整跑出来**，用于研究这种思维**本身**——不追求正确答案。

它与主仓库 [dsh-thinking-models](https://github.com/plasmaflea/dsh-thinking-models) 里的**审计版**是同一个名字下的两种东西，不要混：

| | 审计版（主仓库） | 模拟版（本仓库） |
|---|---|---|
| id | `presupposed-answer-hypothesis-backderivation` | `presupposed-answer-hypothesis-backderivation-simulation` |
| 干什么 | 诊断一段推理有没有走形，产出**诊断报告 + 纠正映射** | 如实**复现**普通人的推理轨迹，产出**轨迹 + 通道归因** |
| 立场 | 反面教材，用来避免 | 观察对象，不评价对错 |
| 关键列 | `H / E+ / E± / 差异 / 反例条件` | `H / E+ / E± / 偏差处置 / 是否仍成立 / 通道标记` |
| 能不能省掉反例条件 | 不行（写不出反例条件 = 不是假设而是叙事） | **必须没有这一列**（普通人压根不写它，替写就污染观察对象） |

核心论点：倒推法**不是错误方向，是低成本探索策略**。它成功走三条通道——**L 运气**（假设恰好为真）／**A 迟到调整**（不改假设改适用边界，等价于推迟的分类讨论）／**R 改题面**（重述成假设能解释的问题）。

## 2. 上传信息

| 项 | 值 |
|---|---|
| 仓库 | https://github.com/plasmaflea/dsh-ordinary-thinking |
| 远端 | `https://github.com/plasmaflea/dsh-ordinary-thinking.git`（origin） |
| 可见性 | PUBLIC |
| 默认分支 | `main`（首次推送曾落在 `master`，已改并删除远端 master） |
| 当前版本 | 见 `VERSION`（0.1.1）／标签 `v0.1.1` |
| topics | ai-agents, confirmation-bias, decision-making, llm, prompt-engineering, reasoning, skills |
| 账号 | GitHub `plasmaflea`；`gh` 已登录（scope: `gist, read:org, repo`） |

## 3. 文件地图

```
presupposed-answer-hypothesis-backderivation-simulation/SKILL.md   技能正文
examples/single-run-lucky-guess.md                                  一次走运猜中的完整轨迹
README.md  CHANGELOG.md  VERSION  STATE.md  LICENSE
```

本仓库**没有** `scripts/`，直接用主仓库的 `state.ps1` + `state.cmd`（已支持 `-Repo` 参数与自动发现技能 id）。

## 4. 安装位与同步

```powershell
$src = 'D:\DeepSeek-levelup\dsh-ordinary-thinking'
$id  = 'presupposed-answer-hypothesis-backderivation-simulation'
$dst = "$env:USERPROFILE\.dsh\skills"
New-Item -ItemType Directory -Force -Path "$dst\$id" | Out-Null
Copy-Item "$src\$id\SKILL.md" "$dst\$id\SKILL.md" -Force
```

⚠️ 两个 id 都以 `presupposed-answer-hypothesis-backderivation` 开头，安装目录名**几乎一样**。复制前先看清是否带 `-simulation` 后缀，否则会用模拟版覆盖审计版。

## 5. 发版流程

```powershell
cd D:\DeepSeek-levelup\dsh-ordinary-thinking
D:\DeepSeek-levelup\dsh-thinking-models\scripts\state.cmd -Repo . -Verify
# 改 CHANGELOG.md + VERSION
git add -A; git commit -m "..."; git tag vX.Y.Z; git push; git push --tags
# 然后到 DSH 设置 → 技能 → 技能仓库 → 重新扫描
```

版本号规则、技能命名约束、`.ps1` 必须走 `.cmd`、`.cmd` 必须 ASCII+CRLF —— 与主仓库 `STATE.md` 第 6、7 节相同，不重复。

## 6. 已知缺口

- `LICENSE` 第 3 行仍是 `Copyright (c) 2026 <AUTHOR>` 占位。
- 三种运行模式（单跑／蒙特卡洛／对撞）**一次都没实际跑过**，`p̂` 与通道分解无实测数据。
- README 的「为什么要单独成仓库」只写了设计与理由，没有结果。

## 7. 与主仓库的关系

主仓库 README 里有一行互链。两仓库**独立发版**；模拟版是主仓库审计器的对照物，两边 SKILL.md 不要互相复制——那会毁掉「三处结构差」这个设计。
