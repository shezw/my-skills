# 测试用例

- 测试 ID: `5`
- 项目: `skills`
- 场景: `rust-skill-structure`
- 目标: `rust-standards-skill`
- 创建时间: `2026-05-01 22:44:38`

## 测试验证

1. 检查 `rust-standards/SKILL.md`、`rust-standards/references/code-standards.md`、`rust-standards/references/review-checklist.md` 是否存在且无诊断问题。
2. 检查 `agent-baseline/SKILL.md` 与 `agent-baseline/references/workflow.md` 是否显式引用 `rust-standards`。
3. 检查 `agent-baseline/references/rust-code-standards.md` 是否已变为兼容转向页。
4. 检查用户级 `rust.instructions.md` 是否说明其与 `rust-standards` 技能的对应关系。
5. 执行一次实际 git 提交。
6. 读取最新一次提交信息，确认标题概括任务且正文列出核心改动点。

## 结果判定

- 返回值: `true | false`
- 通过条件: Rust 规范已迁移为独立技能，基线技能已暴露该入口，兼容转向页存在，且本次变更已通过符合规范的提交写入 git 历史。
- 失败处理: 将 `results.db` 中 ID 为 `5` 的记录 `fails` 加 `1`。

## 执行记录

- 最近结果: `true`
- 说明: 已验证 Rust 规范迁移为独立 `rust-standards` 技能，并确认提交 `7ab8d11d92cb4d9745c236839be90ad17eceae14` 的标题和正文符合默认提交规范。