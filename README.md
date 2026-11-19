# WorkBuddy 任务大师（Task Master）

> 一个 WorkBuddy Skill：收到任务先拆分规划，按难度给每个步骤分配高性价比模型（含内置模型 + 自定义模型），逐阶段执行，每阶段结束输出「交接卡」——下一阶段推荐模型 + 可直接复制的自包含提示词。

起因：长任务全程用单一贵档，一轮烧掉十几块，但真正需要深度推理的只有少数步骤。任务大师把「选模型」变成「编排任务 + 省钱 + 阶段交接」。

## 它能做什么

- **任务拆解**：把一个任务拆成可独立验收的阶段，输出规划总表。
- **按步定模型**：机械活走免费/轻量档，常规走中档，核心推理才上高档，顶档需举证。
- **分阶段执行**：一轮只做一个阶段，做完即停。
- **交接卡**：每阶段结束给出下一阶段推荐模型 + 自包含提示词，换模型/换会话也能接上。

调用方式（安装后）：在对话里说 `@skill:model-choice-advisor` 或直接发任务，它会先给规划总表。

## 安装（选一种）

### 方式 A · 一条命令（推荐，macOS / Linux）

```bash
git clone https://github.com/425794391-max/task-master-skill.git ~/.workbuddy/skills/model-choice-advisor
```

装完即可用，无需重启 WorkBuddy（新会话自动加载）。

### 方式 B · 手动下载

1. 打开 <https://github.com/425794391-max/task-master-skill>，点绿色 **Code → Download ZIP**。
2. 解压，把里面的 `skills/model-choice-advisor` 整个文件夹拷贝到：

   | 系统 | 目标目录 |
   |---|---|
   | macOS / Linux | `~/.workbuddy/skills/model-choice-advisor` |
   | Windows | `%USERPROFILE%\.workbuddy\skills\model-choice-advisor` |

3. 确认目录里能看到 `SKILL.md` 和 `model-catalog.md` 两个文件。

## 验证安装

目录结构应是这样：

```
~/.workbuddy/skills/model-choice-advisor/
├── SKILL.md            # 必需：技能定义
└── model-catalog.md    # 模型候选清单（内置 + 自定义）
```

在 WorkBuddy 新开一个会话，输入：

```
@skill:model-choice-advisor 帮我把 XX 任务拆分规划
```

如果它先给出「任务大师 · 规划」表格，说明装好了。

## 更新到最新版

```bash
cd ~/.workbuddy/skills/model-choice-advisor && git pull
```

## 文件说明

- `SKILL.md`：技能主逻辑，含工作流、交接协议、输出模板。别改名（Skill 加载依赖此文件名）。
- `model-catalog.md`：模型候选池，含 credits 倍率与刷新方法。产品版本升级后模型清单会变，按文件里的「刷新方法」重新采集。

## 注意

- 清单里的 credits 是相对消耗倍率（x0.00 = 免费），来自产品配置快照，非实测账单，可能随版本变化。
- 本技能只做任务规划与模型路由建议，不代替你执行外部发布/付款/删除等动作。
- 安装目录名用 `model-choice-advisor`（技能内部 name），仓库名叫 `task-master-skill`，两者不同是正常的。

## License

MIT
