---
name: go-standards
description: 'Use when writing, reviewing, refactoring, or designing Go services and platforms. Covers clean architecture, domain boundaries, dependency inversion, config-driven monolith or microservice modes, multi-protocol APIs, error handling, events, observability, security, testing, and AI-ready project structure.'
argument-hint: 'Describe the Go service, bounded context, API, or architecture concern'
user-invocable: true
disable-model-invocation: false
---

<!--
    my-skills
    go-standards/SKILL.md    2026-05-01
     ______     __  __     ______     ______     __     __
    /\  ___\   /\ \_\ \   /\  ___\   /\___  \   /\ \  _ \ \
    \ \___  \  \ \  __ \  \ \  __\   \/_/  /__  \ \ \/ ".\ \
     \/\_____\  \ \_\ \_\  \ \_____\   /\_____\  \ \__/".~\_\
      \/_____/   \/_/\/_/   \/_____/   \/_____/   \/_/   \/_/.com

    @link    : https://github.com/shezw/my-skills
    @author  : shezw
    @email   : hello@shezw.com
-->

# Go Standards

## When To Use

- 编写、评审、重构或设计 Go 单体、微服务、平台模块和共享领域代码时。
- 需要统一清洁架构、依赖倒置、配置驱动运行模式和工程治理门槛时。
- 需要给 AI 或新成员提供一套低学习成本、强约定、易推理的 Go 项目结构时。

## What This Skill Produces

- Go 项目编码标准，见 [code standards](./references/code-standards.md)
- 架构与运行模式默认约束，见 [architecture defaults](./references/architecture-defaults.md)
- 编码与评审检查清单，见 [review checklist](./references/review-checklist.md)
- 目录结构示例，见 [project layout example](./assets/project-layout-example.md)
- 与自动生效规则的对应关系说明：真正对 `*.go` 默认生效的规则位于用户级 `go.instructions.md`

## Procedure

1. 先读取 [code standards](./references/code-standards.md)，确认分层、接口边界、错误体系、事件驱动和工程门槛。
2. 若项目还在定型阶段，再读取 [architecture defaults](./references/architecture-defaults.md)，统一单体与微服务的运行方式和协议入口。
3. 在实现或评审时结合 [review checklist](./references/review-checklist.md) 快速核对分层、配置、安全、可观测性和测试。
4. 若需要落具体目录结构或讨论如何组织 bounded context，可参考 [project layout example](./assets/project-layout-example.md)。
5. 若当前任务同时使用通用开发闭环，配合 [agent-baseline](../agent-baseline/SKILL.md) 一起使用。