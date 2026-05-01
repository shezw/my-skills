# 测试用例

- 测试 ID: `8`
- 项目: `skills`
- 场景: `go-guidelines`
- 目标: `go-standards`
- 创建时间: `2026-05-01 23:22:47`

## 测试验证

1. 检查 `go-standards/SKILL.md`、`go-standards/references/` 和 `go-standards/assets/project-layout-example.md` 是否存在且无诊断问题。
2. 检查用户级 `go.instructions.md` 是否存在，且 `applyTo` 覆盖 Go 文件。
3. 搜索规范文本，确认包含清洁架构、Wire、`config.yaml`、`mode: monolith`、`mode: microservice`、REST、gRPC、WebSocket、错误码、`request_id`、`pkg/errors`、事件总线、RabbitMQ、Kafka、`go:generate`、OpenTelemetry、JWT、validator、SQL 防护、Vault 和 `context.Context` 等关键条目。
4. 执行一次实际 git 提交。
5. 读取最新一次提交信息，确认标题概括任务且正文列出核心改动点。

## 结果判定

- 返回值: `true | false`
- 通过条件: Go 规范技能、自动生效规则层和关键条目都已落地，且本次变更已通过符合规范的提交写入 git 历史。
- 失败处理: 将 `results.db` 中 ID 为 `8` 的记录 `fails` 加 `1`。

## 执行记录

- 最近结果: `true`
- 说明: 已验证 Go 规范技能与自动生效规则层完整落地，并确认提交 `92f5a53d61a9a70f527679ed70975288f238e5ea` 的标题和正文符合默认提交规范。