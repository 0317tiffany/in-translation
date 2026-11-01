# 翻译标准细则 — 信达雅操作手册

本文件是 translate-agent-reasoning skill（In Translation 项目）的翻译质量标准，翻译任何思考过程前必读。

## 优先级裁决：信 > 达 > 雅

三条标准冲突时，永远牺牲低优先级的一方：

- 为"达"调整语序可以，但不能改变原意（信）
- 为"雅"润色用词可以，但不能牺牲通顺（达）
- 例：原文 "This might fail" 译"这可能失败"（信），不得为流畅译成"这会失败"（丢失 might 的不确定性）

## 信（Faithfulness）— 忠实原意

- **不增不减**：不补充原文没有的信息，不省略原文的信息
- **精确要素**：数字、单位、版本号、行号、文件名逐一核对
- **逻辑关系不变**：因果（because→因为）、条件（if→如果）、转折（but→但）不能错位
- **模糊保持模糊**：might→"可能"、seems→"似乎"、I guess→"我猜"，不得译成确定语气
- **不译内容原样**：代码块、行内代码、命令、路径、URL、变量/函数/类名、结构化数据

## 达（Expressiveness）— 通顺流畅

- **语序中文化**：英文后置的从句、插入语按中文习惯前置或拆分
- **长句拆短**：一句超过两个逗号层次时拆成多句
- **消除翻译腔**："进行一个 X 的操作"→"执行 X"；"基于……的基础之上"→"基于……"
- **代词落地**：it / this / that 指代前文具体事物时，译出该事物名（如"这个方案"），避免"它"满天飞
- **被动改主动**：开发者语境优先主动语态，必要时保留被动

## 雅（Elegance）— 润色边界

- 仅在信、达达成后润色
- 技术文本的"雅"是**清晰、干净、精炼**，不是文学化修辞
- 禁止：堆砌成语、过度比喻、文言混用

## 术语三类处理清单

判定标准（按顺序问）：

1. 中文开发者口语中通常直接说英文吗？→ **保留英文**
2. 译名唯一且通行的常用词吗？→ **正常翻译**
3. 有通行译名、但英文原词同样高频吗？→ **翻译 + 首次标注**

### 一律保留英文（不翻译）

- **协议与格式**：API, SDK, CLI, IDE, LSP, MCP, HTTP, REST, GraphQL, JSON, YAML, XML, SQL
- **工具链**：Git, Docker, Nginx, Webpack, Vite, ESLint
- **AI / agent 领域**：agent, prompt, system prompt, token, context window, few-shot, RAG, fine-tuning, embedding, hallucination, tool call
- **开发通用**：hook, callback, middleware, refactor, debug, deploy, rollback, commit, merge, rebase, pipeline, workflow, framework, library, bug, log, cache, shard
- **所有命名标识**：变量名、函数名、类名、参数名、文件名（如 `parse_config()`、`app.py`）

### 正常翻译的常用词

file→文件，server→服务器，database→数据库，request→请求，response→响应，
index→索引，query→查询，table→表，field→字段，error→错误，warning→警告，
test→测试，build→构建，release→发布，branch→分支，tag→标签

### 翻译 + 首次标注的领域术语

有通行中文译名、但英文原词在社区同样高频的术语：首次出现时译成中文并括号附英文原词，同一文档后续出现时只用中文。此类术语**不属于**保留英文清单。如：思维链（chain-of-thought）、竞态条件（race condition）、过拟合（overfitting）、注意力机制（attention mechanism）。

## 思考质感处理

思考过程的口语化标记是推理路径的"路标"，必须保留；但每个句子内部的语言要润色通顺（保留结构 + 润色语言）：

| 特征 | 原文示例 | 译法 |
|---|---|---|
| 犹豫词 | hmm / let me think / okay | 嗯 / 让我想想 / 好 |
| 自我修正 | Wait, that's not right... | 等等，这不对…… |
| 推演推进 | Let me check... First... Now... | 让我查一下……首先……现在…… |
| 假设验证 | If X, then... but actually... | 如果 X，那么……但实际上…… |
| 发现标记 | Ah, I see / There it is | 啊，明白了 / 找到了 |
| 结论标记 | So the answer is... / That's the bug | 所以答案是…… / 这就是问题所在 |
| 换思路 | Alternatively... / On second thought | 或者换个思路…… / 再想想 |

省略号（...）是思考停顿的标志，如实保留为中文省略号（……）。

**wait 按语境处理，不做机械替换**：独立表犹豫的 "Wait..." / "Wait, but..." 译作"等等……"；表动作的 wait for 译作"等待"（wait for the build to finish→等待构建完成）。

## 特殊内容处理

- **代码块**：原样保留，包括缩进与注释（注释也不译，保持代码完整性）
- **数学公式**：原样
- **报错信息 / 日志**：原样，仅翻译其前后的说明文字
- **引号内的用户原话**：翻译，但保留引号
