# WorkBuddy 模型候选清单（内置 + 自定义）

> 用途：任务大师分配模型时的候选池。credits 是相对消耗倍率（x0.00 = 免费），来自产品配置，非实测账单。
> 采集日期：2026-11-19。数据快照：`~/.workbuddy/cache/acc-product-config-v3-88630-*.json` + `~/.workbuddy/models.json`。
> **刷新方法**：缓存文件名带哈希、会随版本变化。重新采集时执行——
> `python3 -c "import json,glob; d=json.load(open(sorted(glob.glob('$HOME/.workbuddy/cache/acc-product-config-v3-*.json'))[-1])); ..."`，
> 从含 `models` 数组（长度 >20）的节点提取 `id/name/credits/supportsToolCall/supportsImages/reasoning/maxInputTokens`；
> 再合并 `~/.workbuddy/models.json` 的自定义模型。若读不到，降级用下表并注明"清单可能过期"。

## A. 性价比分层（任务大师默认路由优先用这些）

### 免费档（x0.00）——机械活首选，别放过
| 模型 | ID | credits | 上下文 | 推理 | 备注 |
|---|---|---|---|---|---|
| Hy4 flash | `hy4flash-free` | x0.00 | 960k | high | **免费 + 强推理 + 大上下文，机械活/批量首选** |
| Hy3 | `hy3-b` / `hy3-c` | x0.00 | 192k | high | 免费推理档，短平快任务 |

### 轻量档（x0.07–0.19）——机械活、格式化、批量
| 模型 | ID | credits | 上下文 | 推理 |
|---|---|---|---|---|
| 自定义 DeepSeek-V4.1-Flash | `custom-local:DeepSeek-V4.1-Flash` | x0.07 | 1M | medium |
| GLM-5.3-Flash | `glm-5.3-flash` | x0.08 | 1M | high |
| 自定义 极速 | `custom-local:极速` | x0.09 | 1M | medium |
| DeepSeek-V4.1-Flash | `deepseek-v4.1-flash` | x0.11 | 1M | high |
| Xiaomi MiMo-V2.6-Pro | `mimo-v2.6-pro` | x0.13 | 1M | high |
| 内置 快速 | `fast-model` | x0.15 | 300k | medium |
| Deepseek-V4-Flash | `deepseek-v4-flash` | x0.17 | 1M | high |
| MiniMax-M2.5 | `minimax-m2.5` | x0.18 | 200k | medium |
| GLM-5.3-FlashX | `glm-5.3-flashx` | x0.19 | 1M | high |

### 中档（x0.20–0.55）——常规代码、写作、一般推理
| 模型 | ID | credits | 上下文 | 推理 |
|---|---|---|---|---|
| 自定义 DeepSeek-V4-Pro | `custom-local:DeepSeek-V4-Pro` | x0.20 | 1M | high |
| 自定义 均衡 | `custom-local:均衡` | x0.23 | 1M | medium |
| Kimi-K2.5 | `kimi-k2.5` | x0.45 | 256k | medium |
| 自定义 GPT-6.2-Sol | `custom-local:GPT-6.2-Sol` | x0.50 | 1M | medium |
| 内置 均衡 | `balanced-model` | x0.50 | 300k | medium |
| DeepSeek-V4-Pro | `deepseek-v4-pro` | x0.51 | 1M | high |

### 高档（x0.69–1.62）——核心算法、关键决策、终稿
| 模型 | ID | credits | 上下文 | 推理 |
|---|---|---|---|---|
| GLM-5.3 | `glm-5.3` | x0.69 | 1M | high |
| 自定义 GPT-6.2-Astra | `custom-local:GPT-6.2-Astra` | x0.80 | 1M | medium(max effort) |
| Kimi-K3.1-Pro | `kimi-k3.1-pro` | x0.97 | 1M | high |
| 内置 极致 | `deep-model` | x1.00 | 300k | medium |
| 自定义 GPT-6-Astra | `custom-local:GPT-6-Astra` | x1.00 | 1M | medium(max effort) |
| 自定义 Claude-Sonnet-5.5 | `custom-local:Claude-Sonnet-5.5` | x1.25 | 1M | medium |
| Kimi-K3 | `kimi-k3-2` | x1.62 | 1M | high |
| Kimi-K3.1-Pro-Highspeed | `kimi-k3.1-pro-highspeed` | x1.56 | 1M | high |

### 顶档（x2.00+）——仅不可重试的关键决策，需举证
| 模型 | ID | credits | 上下文 |
|---|---|---|---|
| 自定义 Claude-Opus-5.5 | `custom-local:Claude-Opus-5.5` | x2.00 | 1M |
| 自定义 Claude-Fable-5.2 | `custom-local:Claude-Fable-5.2` | x3.75 | 1M |

## B. 专用模型（按模态触发，不参与通用排序）
- **视觉/图片**：GLM-4.6V `glm-4.6v`（x0.11, 128k）、GPT-Image2.5-Flare / Sunburst（图片生成，无推理）
- **视频**：Kling-Video-V3、MiniMax-H3
- **图像生成**：Hunyuan Image Alpha、Hunyuan-Image-V3
- **代码补全（非对话）**：codewise-* 、hunyuan-3b/7b —— 编辑器内联补全，不作为任务执行模型

## C. 成本速查（默认路由心智）
机械活 → 免费档 Hy4 flash / 轻量档 GLM-5.3-Flash；常规 → 中档 DeepSeek-V4-Pro / GPT-6.2-Sol；
核心推理 → 高档 GPT-6.2-Astra / Kimi-K3.1-Pro；顶档 Claude-Opus-5.5 需举证。
**能免费的绝不花钱，能用便宜档的绝不上贵档。**
