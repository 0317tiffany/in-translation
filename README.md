# In Translation

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

**中文** | [English](#english)

---

## 这是什么

AI agent 的思考过程（thinking / reasoning / extended thinking）大多是英文的，中文用户往往只能"看个大概"。**In Translation** 项目提供一个 agent skill（`translate-agent-reasoning`）：把英文思考过程翻译成**中文在上、英文折叠对照**的双语形式——先流畅地读懂，遇到疑问再展开原文核对。自动识别主流 agent 的思考格式——DeepSeek 的 think 标签、Claude 的 thinking、Codex 的 reasoning summary、各类 harness 的行首标记——粘贴即可翻译。

## 效果展示

> 用户：翻译一下你刚才的思考

**🧠 思考过程（中文）**

让我看看这个报错。堆栈信息指向 parser.py 的第 42 行——一个 IndexError。嗯，这通常说明访问索引 0 时列表是空的。等等，但用户说文件是有内容的……让我重新检查文件读取逻辑。啊，找到了——文件被打开了，但从未读入 buffer，所以 `lines` 一直是空的。这就是 bug 所在。

<details>
<summary>📄 查看英文原文</summary>

Let me look at the error. The stack trace points to line 42 in parser.py — an
IndexError. Hmm, that usually means the list is empty when we try to access
index 0. Wait, but the user said the file has content... Let me re-check the
file reading logic. Ah, I see it — the file is opened but never read into the
buffer, so `lines` stays empty. That's the bug.

</details>

## 翻译标准：信 > 达 > 雅

源自严复的翻译三难，针对技术思考过程做了操作化，优先级固定为 **信 > 达 > 雅**：

| 标准 | 含义 | 操作细则 |
|---|---|---|
| **信** | 忠实原意 | 不增不减不歪曲；模糊保持模糊（might→可能）；代码、命令、路径原样保留 |
| **达** | 通顺流畅 | 中文语序、长句拆短、消除翻译腔、代词落地 |
| **雅** | 清晰精炼 | 仅在信达之内润色，不做文学化修辞 |

两条特色规则：

- **术语按三类规则处理** — API、token、hook、prompt、agent 等开发者通用术语保留英文，常见词正常翻译，有通行译名的领域术语首次标注原文（主要清单与判定规则见 [translation-guide.md](.workbuddy/skills/translate-agent-reasoning/references/translation-guide.md)）
- **保留思考质感** — 独立使用的 "Wait..." 可译作“等等……”，"wait for" 则译作“等待”；hmm 译作“嗯”。自我修正与推理链如实翻译。这些是 agent 推理路径的路标，抹平了就失去了“看 agent 怎么想”的意义

## 安装

### WorkBuddy（项目级）

```bash
git clone https://github.com/0317tiffany/in-translation.git
```

clone 后用 WorkBuddy 打开该项目目录，skill 自动生效（位于 `.workbuddy/skills/translate-agent-reasoning/`）。

### WorkBuddy（用户级，全项目可用）

```bash
cp -r in-translation/.workbuddy/skills/translate-agent-reasoning ~/.workbuddy/skills/
```

### Claude Code（格式兼容）

`SKILL.md` + frontmatter 结构与 Claude Code skills 同构，可直接使用：

```bash
cp -r in-translation/.workbuddy/skills/translate-agent-reasoning ~/.claude/skills/
```

## 使用

三种输入方式，说人话即可触发：

| 输入 | 示例 |
|---|---|
| 会话内可见思考 | "翻译一下你刚才的思考"（仅翻译会话中可见的 reasoning 摘要，不访问不可见的内部思考） |
| 粘贴文本 | "把这段 reasoning 翻成双语" + 粘贴英文思考 |
| 文件 | "翻译 thinking-log.md 里的思考记录" |

翻译结果默认直接显示在对话中；说"保存成文件"即产出双语 `.md` 文档。

## 项目结构

```
in-translation/
├── LICENSE                          # MIT
├── README.md                        # 本文件（双语）
└── .workbuddy/
    └── skills/
        └── translate-agent-reasoning/
            ├── SKILL.md             # skill 主文件：工作流 + 输出模板 + 质量自检
            └── references/
                ├── translation-guide.md   # 信达雅细则 + 术语三类规则
                ├── agent-formats.md       # 主流 agent 思考格式识别与标记剥离
                └── examples.md            # 翻译前后对照范例
```

## 参与贡献

欢迎通过 issue / PR 参与，特别欢迎：

- 补充**术语三类清单**（AI / 前端 / 后端 / 数据等领域的常用术语）
- 报告**未识别的思考格式**（帮助扩充 agent-formats.md 速查表）
- 提供更多**翻译范例**（不同 agent 的真实思考样本）
- 改进翻译细则中不符合你语感的规则

---

<a id="english"></a>

# In Translation

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

[中文](#这是什么) | **English**

## What is this

AI agents mostly think in English, which leaves Chinese-speaking users reading their reasoning "roughly". **In Translation** provides an agent skill (`translate-agent-reasoning`) that renders an agent's English thinking process as **Chinese-first with the English original collapsible underneath** — read it fluently first, expand the original only when you need to verify. It auto-detects thinking formats from major agents — DeepSeek think tags, Claude thinking, Codex reasoning summaries, harness-style prefixes — just paste and translate.

## Translation standard: Faithfulness > Expressiveness > Elegance

Adapted from Yan Fu's classic translation principles, operationalized for technical reasoning with a fixed priority: **Faithfulness > Expressiveness > Elegance**.

Two signature rules:

- **Handle terminology in three tiers** — common developer terms such as API, token, hook, prompt, and agent stay in English; everyday terms are translated; domain terms with established Chinese equivalents are translated and annotated on first use (see the glossary and judgment rules in [translation-guide.md](.workbuddy/skills/translate-agent-reasoning/references/translation-guide.md))
- **Preserve the texture of thinking** — a standalone "Wait..." can become "等等……", while "wait for" means "等待"; translate *hmm* as "嗯". Keep self-corrections and reasoning chains intact. They are the signposts of how the agent actually thinks.

## Install

```bash
# WorkBuddy (project scope): clone and open the project in WorkBuddy
git clone https://github.com/0317tiffany/in-translation.git

# WorkBuddy (user scope) / Claude Code:
cp -r in-translation/.workbuddy/skills/translate-agent-reasoning ~/.workbuddy/skills/   # or ~/.claude/skills/
```

## Usage

Three input modes — just ask naturally:

- "翻译一下你刚才的思考" (translate your latest thinking in this session)
- Paste an English reasoning block and ask for a bilingual version
- Point to a file: "翻译 thinking-log.md 里的思考记录"

Results render inline by default; ask to "save as file" for a standalone bilingual `.md`.

## Contributing

Issues and PRs are welcome — especially glossary additions, real-world thinking samples for the examples, and rules that better match your sense of the language.

## License

[MIT](LICENSE)
