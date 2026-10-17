# 普通人的倒推法 / Ordinary Backderivation

主仓库 [dsh-thinking-models](https://github.com/plasmaflea/dsh-thinking-models) 讲的是**怎么想才不丢负边**；这个仓库只做一件事——把普通人「先有答案、再补理由」的思考**完整跑出来、记下来、算清楚它什么时候歪打正着**。

A research counterpart to [dsh-thinking-models](https://github.com/plasmaflea/dsh-thinking-models). That repo asks *how to think without dropping edges*. This one asks *how ordinary people actually think, and why it sometimes works anyway*.

## 为什么要单独成仓库

**普通人不是不能处理问题。** 倒推法在三种情况下也能得出正确结果：

- **L 运气** —— 假设恰好为真（选项少、先验强时概率并不低）
- **A 迟到调整** —— 反例出现后不改假设，改假设的**适用边界**（推迟了的分类讨论）
- **R 改题面** —— 把问题重述成假设能解释的那个问题

所以研究目标不是「证明它错」，而是「量出它错在哪、以及它靠什么对」。

同一套倒推法在主仓库里是**审计器**（判一段推理可不可信，产物是诊断报告 + 纠正映射）；在这里是**模拟器**（把普通人的思考过程跑一遍，产物是思考轨迹 + 通道记账）。目标不同，产物不同，所以分成两个仓库。

## 里面有什么

| 全称 | 简称（产物／动作） | 技能 id | 产物 | 触发 |
|---|---|---|---|---|
| 🧪 预设答案假设倒推法（模拟版） | **倒推图·模拟** ／ **倒推法·模拟** | `presupposed-answer-hypothesis-backderivation-simulation` | 思考轨迹表 + 通道归因（L／A／R） | 「模拟一下普通人的思路」「倒推法凭什么也能对」「研究这个思维模型本身」 |

**命名**：与主仓库一致，id 是中文全称的逐段直译（图名·核心限定·法名），末尾加 `simulation` 表示模拟版——两版可同时安装，`name` 与目录都不冲突。

## 三种运行模式

| 模式 | 干什么 | 产出 |
|---|---|---|
| **单跑** | 复现一次真实思考，逐步记录偏差怎么被处置 | 轨迹表 + 这次靠哪条通道 |
| **蒙特卡洛** | 只随机化「第一轮选了哪支假设」，跑 N≥20 次 | `p̂` 命中率、通道分解、注入硬反例后的掉幅 |
| **对撞** | 同题对照主仓库三张图 | 命中率／步数／可解释性／能否定位漏项 |

## 安装 / Install

技能没有中心化商店，分发单位就是一个目录 + 一份 `SKILL.md`。

```powershell
$dst = "$HOME\.dsh\skills"
Copy-Item -Recurse -Force `
  .\presupposed-answer-hypothesis-backderivation-simulation $dst
```

| 作用域 | 路径 |
|---|---|
| DSH 全局 | `~/.dsh/skills/<skill-id>/SKILL.md` |
| 跨 Agent 共享 | `~/.agents/skills/<skill-id>/SKILL.md` |
| 项目内 | `<project>/.dsh/skills/<skill-id>/SKILL.md` |

也可用 Skills Manager 的「技能仓库」添加本仓库地址，扫描后**逐项**安装；或 `npx skills add plasmaflea/dsh-ordinary-thinking`（该 CLI 面向 Claude Code／Cursor／Codex，不含 DSH）。

## 仓库结构 / Layout

```
.
├── presupposed-answer-hypothesis-backderivation-simulation/SKILL.md  # 🧪 模拟版
├── examples/
│   └── single-run-lucky-guess.md        # 一次"歪打正着"的完整轨迹 + 多跑设计
├── README.md
└── LICENSE
```

## 适用边界（诚实版）

- **它不是「更聪明的技能」**，是研究工具。要答案、要可靠结论，请用主仓库的三张图。
- **单次运行证明不了方法好坏**。N < 20 的命中率只能当轶事。
- **模拟出的「普通人」是模型，不是真人画像**。它是行为假设，可以被证伪。
- **它不能给答案背书**：「这次对了」和「方法可靠」是两件事，产物里必须带这条警告。

## 与主仓库的关系

| | dsh-thinking-models | dsh-ordinary-thinking（本仓库） |
|---|---|---|
| 回答的问题 | 怎么想才对 | 普通人怎么想、为什么有时也对 |
| 技能数 | 3 个作答模型 + 1 个审计器 | 1 个模拟器 |
| 产物 | 林状图／网状图／公式图／诊断报告 | 思考轨迹表 + 通道记账 |
| 使用时机 | 要解决问题 | 要理解「普通思维」这个对象本身 |

## 许可 / License

MIT，见 [LICENSE](LICENSE)。
