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

## 更新到最新版

```bash
cd ~/.workbuddy/skills/model-choice-advisor && git pull
```

## 它能做什么

- **任务拆解**：拆成可独立验收的阶段，输出规划总表。
- **按步定模型**：机械活走免费/轻量档，常规走中档，核心推理才上高档，顶档需举证。
- **分阶段执行**：一轮只做一个阶段，做完即停。
- **交接卡**：每阶段给出下一阶段模型 + 自包含提示词，换模型/换会话也能接上。

用法：安装后发 `@skill:model-choice-advisor` 或直接把任务丢给它。

## 文件说明

- `SKILL.md`：技能主逻辑（工作流、交接协议、输出模板）。别改名，加载依赖此文件名。
- `model-catalog.md`：模型候选池（credits 倍率与刷新方法）。产品升级后模型会变，按文件里的「刷新方法」重新采集。

## 注意

- credits 是相对消耗倍率（x0.00 = 免费），来自产品配置快照，非实测账单，随版本可能变。
- 本技能只做任务规划与模型路由建议，不代替你执行外部发布/付款/删除等动作。
- 安装目录名用 `model-choice-advisor`（技能内部 name），仓库名叫 `task-master-skill`，两者不同是正常的。

## License

MIT
