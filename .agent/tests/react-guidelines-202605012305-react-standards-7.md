# 测试用例

- 测试 ID: `7`
- 项目: `skills`
- 场景: `react-guidelines`
- 目标: `react-standards`
- 创建时间: `2026-05-01 23:05:35`

## 测试验证

1. 检查 `react-standards/SKILL.md`、`react-standards/references/` 和 `react-standards/assets/feature-layout-example.md` 是否存在且无诊断问题。
2. 检查用户级 `react.instructions.md` 是否存在，且 `applyTo` 覆盖 React 组件文件。
3. 搜索规范文本，确认包含 Mantine、`@tabler/icons-react`、feature 拆分、hooks、表单、测试、可访问性和性能等关键条目。
4. 执行一次实际 git 提交。
5. 读取最新一次提交信息，确认标题概括任务且正文列出核心改动点。

## 结果判定

- 返回值: `true | false`
- 通过条件: React 规范技能、自动生效规则层和关键条目都已落地，且本次变更已通过符合规范的提交写入 git 历史。
- 失败处理: 将 `results.db` 中 ID 为 `7` 的记录 `fails` 加 `1`。

## 执行记录

- 最近结果: `true`
- 说明: 已验证 React 规范技能与自动生效规则层完整落地，并确认提交 `f8216754517173f549c7061dc4b80a1c2a324ac4` 的标题和正文符合默认提交规范。