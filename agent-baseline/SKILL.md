---
name: agent-baseline
description: 'Use when coding, fixing bugs, refactoring, or validating implementation. 通用开发闭环规范，要求 .agent req/res/todo/logs/tests、results.db、测试回写、日志记录。'
argument-hint: 'Describe the coding scene and target'
user-invocable: true
disable-model-invocation: false
---

# Agent Baseline

## When To Use

- 任何实际编码行为，包括新功能、缺陷修复、重构、配置调整与测试补齐。
- 需要为任务建立可追踪的 `.agent` 过程记录时。
- 需要在开发结束前补齐测试验证、日志、git 检查与默认提交时。

## What This Skill Produces

- 通用的 `.agent` 目录基线与执行顺序说明，见 [workflow reference](./references/workflow.md)
- 测试数据库与结果回写规范，见 [testing reference](./references/testing.md)
- 语言专项规范入口。Rust 见 [rust-standards skill](../rust-standards/SKILL.md)
- 可直接复用的请求、回复、任务、测试、日志模板，见 `./assets/`

## Procedure

1. 确认项目根目录存在 `.agent/req`、`.agent/res`、`.agent/todo`、`.agent/logs`、`.agent/tests`。
2. 若当前任务有对应的语言专项规范，先加载该技能或规则。Rust 使用 [rust-standards](../rust-standards/SKILL.md) 与用户级 `rust.instructions.md`。
3. 按需使用 [request template](./assets/request-template.md) 和 [response template](./assets/response-template.md) 记录输入与分析。
4. 使用 [task template](./assets/task-template.md) 创建或更新 `todo/task-{YMDHMin}.md`。
5. 使用 [results schema](./assets/results-schema.sql) 初始化 `.agent/tests/results.db`，并先写入一条测试记录。
6. 使用 [test template](./assets/test-template.md) 创建 `tests/{scene}-{YMDHMin}-{target}-{id}.md`。
7. 完成开发与验证；失败时更新 `fails`，成功时写入 `passed_time`。
8. 使用 [log template](./assets/log-template.md) 记录阶段结果，并在结束时检查 git 状态。
9. 默认执行提交，提交信息标题概括任务，正文列出核心改动点，可参考 [commit template](./assets/commit-template.md)。若提交被仓库策略或权限阻断，需要在日志中说明原因。

## Outputs

- `.agent/req/req-{YMDHMin}-{topic}.md`
- `.agent/res/res-{YMDHMin}-{question}.md`
- `.agent/todo/task-{YMDHMin}.md`
- `.agent/tests/results.db`
- `.agent/tests/{scene}-{YMDHMin}-{target}-{id}.md`
- `.agent/logs/log-{YMDHMin}.md`