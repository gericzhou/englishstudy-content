# EnglishStudy 在线试卷精读题库

在线地址：`https://raw.githubusercontent.com/gericzhou/englishstudy-content/main/reading.json`

## 使用方式

用户将英语阅读原文、相应的原卷试题和已核对的正确答案发给 ChatGPT。经过校对、拆句和解析后，更新本仓库的 `reading.json` 并递增 `revision`。安装过在线精读客户端的学员只需点「试卷精读 → 在线精读题库 → 检查更新」，无需为新增内容重新编译。

客户端将所有文章、题目与按句解析缓存到本机；离线可阅读、拆句、答题。App 安装此功能的首个版本仍需编译一次。

## 文件结构

`reading.json` 顶层字段：

- `schemaVersion`: 固定 `1`
- `revision`: 从 `1` 起的递增整数，每次发布必须 +1
- `passages`: `ReadingPassage` 数组，每篇必须 `id` 唯一且以 `online-` 开头，`section` 固定 `ONLINE`
- `questionSets`: `ReadingQuestionSet` 数组，每组 `id` 必须与对应文章 `id` 完全相同
- `retiredPassageIDs`: 明确下线且不再出现在 `passages` 中的文章 ID 数组

文章格式与现有 App 内置 `reading_passages.json` 相同，包含 `id`、`section`、`title`、`page`、`source`、`sourceURL`、`examEdition`、`examPart`、`sentences`、`glossary`，以及其他可选的解释字段。每个句子必须预先提供正确的 `sentence`、`targets`（至少 `s`、`v`）、`main`、`meaning`、`analysis` 和 `distractors`（缺省时可传空数组）。
- `studyUnits`（逐句精读的**全句分句与修饰**）：在线题建议每句提供完整数组。每项为 `{ "id":"u01", "kind":"定语", "question":"哪个词修饰 consultant？", "text":"successful", "explanation":"successful 修饰 consultant", "startToken":5, "endToken":5 }`（位置仅为格式示意，发布时应根据原句实际编号计算）。逐项包含确切的起止单词索引，区分重复出现的 `I / she / was` 等。每句先练主干，再逐项分析其余独立分句、完整定语/状语及从句修饰关系，最后理解中文。
- **不得**出现笼统的“找出一个介词短语”这类多解任务；改问“哪部分说明动作发生在何处／修饰哪个名词”，并给出明确对象。精读要覆盖整句话，不得只写第一个分句的主谓、跳过后面的独立分句。`targets` 只对主干、完整从句出选词题，不再让孩子独立圈介词短语、非谓语等小成分；其他语法知识保留于 `roleExplanations`、`grammarSupplements`。

题目格式与 `reading_questions.json` 相同。普通单选 `mode: "single"`，每道题有题号、题干、A/B/C/D 四个选项、0—3 的 `correctIndex`、原文证据 `evidence` 和解题 `explanation`。六选四使用现有 `mode: "insertion"` 和 `sharedOptions` 字段。**禁止凭 AI 猜测原卷答案**；答案须由提供的原卷答案或人工核对支持。

## 发布规则

1. 保留原文中的中文注释和括号释义，例如 `krill（磷虾）`；OCR 后核对中文及特殊符号。
2. 逐句分析先理解整句意思，再找主干，最后标识修饰哪一个主语或宾语；多处可选定语从句时提供 `acceptedTargets` 及对应解析。
3. 每个 `online-...` ID 代表固定的原文。不可在同一 ID 下修改已发布的英文句子、句子 ID、原卷题干或四个选项；此类改动创建新文章 ID。可以纠正译文、答案、解析与词义，发布时递增 `revision`。
4. 尚未获得可核实试题的文章可暂不发布其 `questionSet`，不要编造原卷题目或答案。
5. App 在缓存成功后才替换旧题库，同步失败保留旧内容和学习记录；删除文章须明确加入 `retiredPassageIDs`。
6. 它是公开可读取的学习内容仓库；不得把 API Key、学生姓名或个人记录写入公开 JSON。

## 首次交付

初始 `reading.json` 是空题库。等待用户提供第一篇文章和试题后发布内容。之后增删文章均属于在线内容更新。
