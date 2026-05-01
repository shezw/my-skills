# 测试用例

- 测试 ID: `2`
- 项目: `skills`
- 场景: `commit-baseline`
- 目标: `default-commit`
- 创建时间: `2026-05-01 21:47:05`

## 测试验证

1. 搜索 `agent-baseline` 技能和用户级基线指令，确认不再保留“仅在明确要求时提交”的旧规则。
2. 检查 `agent-baseline/assets/commit-template.md` 和 `agent-baseline/assets/log-template.md`，确认已定义提交标题与核心改动点记录方式。
3. 执行一次实际 git 提交。
4. 读取最新一次提交信息，确认标题概括任务，正文包含“核心改动点”及对应要点。

## 结果判定

- 返回值: `true | false`
- 通过条件: 新规则文本存在，提交模板存在，且最新一次提交信息包含标题和“核心改动点”正文。
- 失败处理: 将 `results.db` 中 ID 为 `2` 的记录 `fails` 加 `1`。

## 执行记录

- 最近结果: `pending`
- 说明: 待执行。