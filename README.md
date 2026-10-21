# EnglishStudy · 公开在线练习题库

这是英语补习 iOS App 的**只读题目内容仓库**，不包含 App 源码、API 密钥、学生身份或学习进度。

**在线 JSON 接口（HTTPS）**
https://raw.githubusercontent.com/gericzhou/englishstudy-content/main/lessons.json

## 更新题库

`lessons.json` 为版本化的 JSON 数据文件，顶层字段为 `schemaVersion`、`revision` 和 `lessons`。发布新题时：

1. 新增题目到 `lessons`，使用从 **10000** 开始的全局唯一数字 `id`，不能使用已经发布的 ID，也不能修改旧题英语原句、答案或对应难度。
2. 将 `revision` 加 1，保持 `schemaVersion` 为 1。
3. 每题必须包含 `id`、`level`（2～4：基础／进阶／挑战）、`title`、`sentence`、`targets`、`main`、`meaning`、`analysis`、三项 `distractors` 和 `words`（可为空数组），复杂句可增加 `roleExplanations` 与 `grammarSupplements`。
4. 特别核对主谓宾、并列谓语、表语、介宾、宾补等角色的句法和原文选区；练习的解释必须和句子意思相符。
5. 推送到 main 后，**安装了在线题库功能的新版 App** 会在打开时自动检查（每 6 小时最多一次），也支持手动立即同步。缓存过的题离线可用。

App 继续内置基础练习题；在线题使用独立 ID，不覆盖已完成、错题或书签记录。发布后的内容可能被任何人读取，请勿上传个人信息、证书、密钥或未经授权的整篇第三方文章。

先前的两道过易连接测试题 `10001`、`10002` 已从在线修订版 2 撤下；当前远端 `lessons` 暂为空，App 仍内置基础／进阶／挑战各20题，避免把被删除的热身题重新同步回来。后续的在线新题从未使用的 ID 开始加入即可。首次使用仍需安装包含在线同步代码的新版 App。

## 内置题库勘误（基础／进阶／挑战）

自新版 App 支持 `bundledCorrections` 后，同一份 `lessons.json` 可以同时提供新题和**已有内置题目的修订版**。这是一组完整的 `Lesson` 对象，保留旧题 `id`、`level`、`title` 和英文 `sentence` 不变，只修订经过复核的答案范围、解析等。更新 `revision` 后，用户在「拆句训练 → 在线题库 → 立即检查新增题目」一次即可拉取所有校正，旧的已完成记录、错题记录和书签仍绑定原题号，离线缓存也会保存勘误。

**兼容性：** 在加入这个功能之前编译的 App 只能更新 id ≥ 10000 的在线新增题，会忽略 `bundledCorrections`。必须先通过 TestFlight 安装支持内置题校正的新版本一次；此后题目内容的再修订才无需重新编译。
