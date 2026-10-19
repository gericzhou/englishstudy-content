# EnglishStudy · 公开在线练习题库

这是英语补习 iOS App 的**只读题目内容仓库**，不包含 App 源码、API 密钥、学生身份或学习进度。

**在线 JSON 接口（HTTPS）**
https://raw.githubusercontent.com/gericzhou/englishstudy-content/main/lessons.json

## 更新题库

`lessons.json` 为版本化的 JSON 数据文件，顶层字段为 `schemaVersion`、`revision` 和 `lessons`。发布新题时：

1. 新增题目到 `lessons`，使用从 **10000** 开始的全局唯一数字 `id`，不能使用已经发布的 ID，也不能修改旧题英语原句、答案或对应难度。
2. 将 `revision` 加 1，保持 `schemaVersion` 为 1。
3. 每题必须包含 `id`、`level`（1～4）、`title`、`sentence`、`targets`、`main`、`meaning`、`analysis`、三项 `distractors` 和 `words`（可为空数组），复杂句可增加 `roleExplanations` 与 `grammarSupplements`。
4. 特别核对主谓宾、并列谓语、表语、介宾、宾补等角色的句法和原文选区；练习的解释必须和句子意思相符。
5. 推送到 main 后，**安装了在线题库功能的新版 App** 会在打开时自动检查（每 6 小时最多一次），也支持手动立即同步。缓存过的题离线可用。

App 继续内置基础练习题；在线题使用独立 ID，不覆盖已完成、错题或书签记录。发布后的内容可能被任何人读取，请勿上传个人信息、证书、密钥或未经授权的整篇第三方文章。

最初的两题 `10001`、`10002` 是接口连通测试用基础题，后续可以直接追加真正的每周练习题，不必重新打包 App。第一次使用仍需安装包含在线同步代码的新版 App。
