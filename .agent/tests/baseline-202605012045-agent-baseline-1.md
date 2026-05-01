# 测试用例

- 测试 ID: `1`
- 项目: `skills`
- 场景: `baseline`
- 目标: `agent-baseline`
- 创建时间: `2026-05-01 20:45:00`

## 测试验证

1. 检查 `agent-baseline/SKILL.md`、参考资料与模板文件是否存在。
2. 检查用户级基线指令文件是否存在。
3. 检查 `.agent/req`、`.agent/res`、`.agent/todo`、`.agent/tests/results.db` 是否包含本次任务的记录。
4. 执行 git 状态检查，确认新增产物已经出现在工作区变更中。

## 结果判定

- 返回值: `true | false`
- 通过条件: 关键文件全部存在，`results.db` 中存在 ID 为 `1` 的记录，git 状态能列出本次新增文件。
- 失败处理: 将 `results.db` 中 ID 为 `1` 的记录 `fails` 加 `1`。

## 执行记录

- 最近结果: `true`
- 说明: 已验证关键文件存在、`results.db` 中存在 ID 为 `1` 的记录，且 `git status --short` 已显示本次新增产物。