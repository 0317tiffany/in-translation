# 翻译范例 — 输入与成品对照

以下范例展示标准输入与对应的输出成品形态。翻译时对照本文件校准输出格式。

## 范例一：带自我修正的短思考

**输入（英文原文）：**

```
Let me look at the error. The stack trace points to line 42 in parser.py — an
IndexError. Hmm, that usually means the list is empty when we try to access
index 0. Wait, but the user said the file has content... Let me re-check the
file reading logic. Ah, I see it — the file is opened but never read into the
buffer, so `lines` stays empty. That's the bug.
```

**输出（双语成品）：**

````
## 🧠 思考过程（中文）

让我看看这个报错。堆栈信息指向 parser.py 的第 42 行——一个 IndexError。嗯，这通常说明访问索引 0 时列表是空的。等等，但用户说文件是有内容的……让我重新检查文件读取逻辑。啊，找到了——文件被打开了，但从未读入 buffer，所以 `lines` 一直是空的。这就是 bug 所在。

<details>
<summary>📄 查看英文原文</summary>

Let me look at the error. The stack trace points to line 42 in parser.py — an
IndexError. Hmm, that usually means the list is empty when we try to access
index 0. Wait, but the user said the file has content... Let me re-check the
file reading logic. Ah, I see it — the file is opened but never read into the
buffer, so `lines` stays empty. That's the bug.

</details>
````

要点：犹豫词如实翻译（Hmm→嗯）、自我修正保留（等等，但……）、`lines` 与 IndexError 保持原样。

## 范例二：带代码块的思考

**输入（英文原文）：**

```
I need to figure out why the pagination is slow. The query itself looks fine,
so let me check the execution plan:

EXPLAIN SELECT * FROM orders WHERE created_at > '2026-01-01';

The type is ALL — a full table scan, no index being used. So I should create
an index on created_at. But wait, this table gets heavy writes... a plain
B-tree index might slow down every INSERT. Maybe partitioning is better here.
Let me measure the write load before deciding.
```

**输出（双语成品）：**

````
## 🧠 思考过程（中文）

我需要弄清楚分页为什么慢。查询本身看起来没问题，所以让我检查一下执行计划：

```sql
EXPLAIN SELECT * FROM orders WHERE created_at > '2026-01-01';
```

type 是 ALL——全表扫描，没有用到索引。所以我应该在 created_at 上建索引。但等等，这张表写入很频繁……普通的 B-tree 索引可能会拖慢每一次 INSERT。也许这里用分区更合适。决定之前，先测一下写入压力。

<details>
<summary>📄 查看英文原文</summary>

I need to figure out why the pagination is slow. The query itself looks fine,
so let me check the execution plan:

```sql
EXPLAIN SELECT * FROM orders WHERE created_at > '2026-01-01';
```

The type is ALL — a full table scan, no index being used. So I should create
an index on created_at. But wait, this table gets heavy writes... a plain
B-tree index might slow down every INSERT. Maybe partitioning is better here.
Let me measure the write load before deciding.

</details>
````

要点：SQL 语句在中文区与折叠区都原样保留；INSERT、B-tree、buffer 等术语保持英文；"maybe / might" 的不确定性如实翻译（"也许 / 可能"）。

## 范例三：长思考的分组折叠

输入超过约 10 个语义段时，按逻辑章节分组，每组配一个折叠块。结构示意：

````
## 🧠 思考过程（中文）

**分析问题**

[该章节全部段落的中文译文……]

<details>
<summary>📄 查看英文原文 — 分析问题</summary>

[该章节英文原文……]

</details>

**制定方案**

[该章节全部段落的中文译文……]

<details>
<summary>📄 查看英文原文 — 制定方案</summary>

[该章节英文原文……]

</details>

**验证方案**

[该章节全部段落的中文译文……]

<details>
<summary>📄 查看英文原文 — 验证方案</summary>

[该章节英文原文……]

</details>
````

要点：章节标题从思考内容的自然逻辑中提炼（分析 / 方案 / 验证只是常见形态，不是固定模板）；每个折叠块的 summary 带上章节名，方便定位。
