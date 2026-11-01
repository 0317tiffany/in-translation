# Agent 思考格式识别与预处理

不同 agent 产品输出思考的包裹格式与风格不同。翻译前先识别来源、剥离包裹标记，只翻译思考正文。

## 常见格式速查表

| 来源 | 常见包裹 / 标记 | 预处理 |
|---|---|---|
| DeepSeek R1 / V3（thinking 模式） | `<think>...</think>` 标签对 | 剥离标签，只译内容；标签本身不译 |
| Claude（Claude Code / API） | thinking 块；用户复制粘贴后多为纯文本 | 按纯文本直接翻译 |
| OpenAI Codex / o 系列 / GPT（reasoning） | reasoning summary，多为 "Let me..."、"I need to..." 开头的成段文本 | 按纯文本直接翻译 |
| Qwen QwQ / GLM 等 | `<think>...</think>` 或 "Thought:" 行首前缀 | 剥离标记，只译内容 |
| SWE-agent / 各类 agent harness | `THOUGHT:`、`### Thought`、`[thinking]` 等行首或标题标记 | 剥离行首/标题标记，保留正文 |
| 通用粘贴文本 | 无标记 | 直接翻译 |

## 通用剥离规则（未识别格式）

输入不在上表时，按以下特征识别思考标记并剥离，**不因格式未知而拒绝翻译**：

- 成对的语义标签 `<xxx>...</xxx>`（think / reasoning / thought 等）
- 行首前缀：`Thought:` / `Thinking:` / `THOUGHT:` / `Reasoning:`
- 标题行：`### Thinking` / `## Reasoning` 等
- 剥离后若剩余内容为空或无英文思考特征，向用户说明所见内容，不要硬译

## 各家风格要点（影响翻译策略，不改变翻译标准）

- **DeepSeek R1**：思考偏长、自问自答多（"The user wants... So I should..."），可能出现**中英夹杂**——中文片段原样保留，不回译也不删；结尾常有 "So the answer is..." 式总结
- **Claude**：口语化、自我修正频繁（"Wait, actually..."），常引用工具调用、文件路径与代码
- **Codex / OpenAI**：偏精炼、结构化，推理链更线性，术语密度高
- 风格差异只影响口语标记与术语的出现频率；**信达雅标准与术语规则对所有来源一视同仁**

## 来源标注

- 能明确判断输入来自哪个 agent 时，在双语输出头部加一行引用标注，如：`> 来源：DeepSeek R1（用户粘贴）`
- 判断不了就不标注，**不猜测来源**
- 标注只用于帮助读者定位语境，不影响翻译内容
