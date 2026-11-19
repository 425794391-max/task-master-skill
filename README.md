# WorkBuddy 任务大师（Task Master）

> 收到任务先拆分规划，按难度给每步配性价比最高的模型（内置 + 自定义），逐阶段执行，每步结束交出「交接卡」——下一阶段推荐模型 + 可直接复制的自包含提示词。

起因：长任务全程用单一贵档，一轮烧掉十几块，但真正需要深度推理的只有少数步骤。任务大师把「选模型」变成「编排任务 + 省钱 + 阶段交接」。

## 一条命令安装（Windows / macOS 通用）

```bash
git clone https://github.com/425794391-max/task-master-skill.git ~/.workbuddy/skills/model-choice-advisor
```

- macOS / Linux：在「终端」里运行。
- Windows：在 **PowerShell** 里运行（`~` 会自动展开到你的用户目录）。
- 前提：装了 Git。没有先装 <https://git-scm.com>。
- 装完新开一个 WorkBuddy 会话即可用，不用重启。

装好后的目录长这样（`SKILL.md` 必须直接在这一层）：

```
~/.workbuddy/skills/model-choice-advisor/
├── SKILL.md
└── model-catalog.md
```

## 验证安装

新开会话输入：

```
@skill:model-choice-advisor 帮我把 XX 任务拆分规划
```

它若先给出「任务大师 · 规划」表格，就成了。

## 手动安装（不想用 Git）

1. 打开 <https://github.com/425794391-max/task-master-skill>，点 **Code → Download ZIP**，解压。
2. 把解压出的 **`SKILL.md` 和 `model-catalog.md` 两个文件**拷到：

   | 系统 | 目标目录 |
   |---|---|
   | macOS / Linux | `~/.workbuddy/skills/model-choice-advisor` |
   | Windows | `C:\Users\你的用户名\.workbuddy\skills\model-choice-advisor` |

3. 目录里要能直接看到这两个文件，不要多套一层文件夹。

## 已安装的人怎么更新到最新版

**不会自动更新。** 之前 clone 的是静态副本，仓库改了本地不会变，需要手动拉一次。在 WorkBuddy 对话框粘贴：

```
请帮我把已安装的「任务大师」skill 更新到最新版。执行：
cd ~/.workbuddy/skills/model-choice-advisor && git pull
如果提示不是 git 仓库（当初是手动下载 ZIP 装的），就删掉该目录后重新克隆：
rm -rf ~/.workbuddy/skills/model-choice-advisor && git clone https://github.com/425794391-max/task-master-skill.git ~/.workbuddy/skills/model-choice-advisor
装完确认 SKILL.md 在 ~/.workbuddy/skills/model-choice-advisor/ 根目录，然后告诉我更新好了，我会新开会话生效。
```

更新完**新开一个会话**才加载新版本。

## 它能做什么

- **任务拆解**：拆成可独立验收的阶段，输出规划总表。
- **按步定模型**：机械活走免费/轻量档，常规走中档，核心推理才上高档，顶档需举证。
- **分阶段执行**：一轮只做一个阶段，做完即停。
- **交接卡**：每阶段给出下一阶段模型 + 自包含提示词，换模型/换会话也能接上。

用法：安装后发 `@skill:model-choice-advisor` 或直接把任务丢给它。

## 使用说明（完整流程）

### 1. 怎么触发
新开会话，直接把任务描述发给它，或明确说：
```
@skill:model-choice-advisor 我要做 XX 任务，帮我规划
```

### 2. 它会先摸底本机模型（这一步是硬性前置）
因为每个人的 WorkBuddy 可用模型不同，它会先读你这台机器上真实可选的模型，告诉你有哪些、各档位（免费/轻量/中/高/顶）分别是什么、相对价格多少。确认后才往下走——这样它推荐的模型一定是你能选到的，不会推荐别人机器上才有的私有模型。你也可以补一句"我还能选 XX 模型"让它纳入。

### 3. 看规划表，确认拆分
它会把任务拆成几个阶段，列出：每阶段目标、性质（机械/中等/核心推理）、用什么模型、验收标准、预估成本。你确认方向对，它才开始做；想调整拆分或某步的模型，直接说。

### 4. 一次只做一个阶段，做完停下交接
它做完当前阶段会停下来，给出一张「交接卡」：
- 本阶段结果和验收证据
- 下一阶段用什么模型、为什么
- **一段可直接整段复制的提示词**

### 5. 衔接下一阶段（关键动作）
把交接卡里那段提示词整段复制，切到它推荐的模型（或新开一个会话），直接发过去——新的一轮就能接着做，不用重新交代背景。换机器/换人执行时，它会先重新摸底那台机器的模型再选同档位的，不用担心模型对不上。

### 6. 成本怎么控制
默认省钱：机械活（加列、跑脚本、格式转换、清理）走免费/轻量档，常规活走中档，只有核心算法和关键决策才用高档，顶档要你点头。想更省可以直接说"用便宜的"，想某步用最强可以点名。

一句话记法：**发任务 → 看摸底 → 确认规划 → 做一步 → 复制交接提示词 → 换模型接着做**，循环到交付。

## 文件说明

- `SKILL.md`：技能主逻辑（工作流、交接协议、输出模板）。别改名，加载依赖此文件名。
- `model-catalog.md`：模型候选池（credits 倍率与刷新方法）。产品升级后模型会变，按文件里的「刷新方法」重新采集。

## 注意

- credits 是相对消耗倍率（x0.00 = 免费），来自产品配置快照，非实测账单，随版本可能变。
- 本技能只做任务规划与模型路由建议，不代替你执行外部发布/付款/删除等动作。
- 安装目录名用 `model-choice-advisor`（技能内部 name），仓库名叫 `task-master-skill`，两者不同是正常的。

## License

MIT
