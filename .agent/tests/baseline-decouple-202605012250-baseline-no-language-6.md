# 测试用例

- 测试 ID: `6`
- 项目: `skills`
- 场景: `baseline-decouple`
- 目标: `baseline-no-language`
- 创建时间: `2026-05-01 22:50:03`

## 测试验证

1. 搜索 `agent-baseline/**`，确认不再出现 `Rust`、`rust-standards`、`语言专项` 等语言层内容。
2. 检查 `agent-baseline/SKILL.md` 与 `agent-baseline/references/workflow.md` 无诊断问题且仍覆盖流程闭环。
3. 检查 `agent-baseline/references/rust-code-standards.md` 已删除。
4. 检查 `rust-standards/` 目录仍存在，确保语言规范保留在独立技能中。
5. 执行一次实际 git 提交。
6. 读取最新一次提交信息，确认标题概括任务且正文列出核心改动点。

## 结果判定

- 返回值: `true | false`
- 通过条件: baseline 目录已纯流程化，语言规范仍保留在独立技能中，且本次变更已通过符合规范的提交写入 git 历史。
- 失败处理: 将 `results.db` 中 ID 为 `6` 的记录 `fails` 加 `1`。

## 执行记录

- 最近结果: `true`
- 说明: 已验证 baseline 目录中不再包含语言层内容，并确认提交 `52633db40f62efa7899a9eaf73cfb42b8be2f903` 的标题和正文符合默认提交规范。