---
name: rust-standards
description: 'Use when writing, reviewing, refactoring, or designing Rust projects. Covers module boundaries, file size, comments, documentation, APIs, errors, async, unsafe, testing, linting, and dependency choices.'
argument-hint: 'Describe the Rust crate, module, architecture, or coding question'
user-invocable: true
disable-model-invocation: false
---

<!--
    my-skills
    rust-standards/SKILL.md    2026-05-01
     ______     __  __     ______     ______     __     __
    /\  ___\   /\ \_\ \   /\  ___\   /\___  \   /\ \  _ \ \
    \ \___  \  \ \  __ \  \ \  __\   \/_/  /__  \ \ \/ ".\ \
     \/\_____\  \ \_\ \_\  \ \_____\   /\_____\  \ \__/".~\_\
      \/_____/   \/_/\/_/   \/_____/   \/_____/   \/_/   \/_/.com

    @link    : https://github.com/shezw/my-skills
    @author  : shezw
    @email   : hello@shezw.com
-->

# Rust Standards

## When To Use

- 编写、评审、重构或设计 Rust 项目、crate、模块与公共 API 时。
- 需要统一模块边界、文件规模、注释质量和工程门槛时。
- 需要在落代码前快速核对 Rust 项目应遵循的标准与检查项时。

## What This Skill Produces

- Rust 项目编码标准，见 [code standards](./references/code-standards.md)
- 编码与评审检查清单，见 [review checklist](./references/review-checklist.md)
- 与自动生效规则的对应关系说明：真正对 `*.rs` 默认生效的规则位于用户级 `rust.instructions.md`

## Procedure

1. 先读取 [code standards](./references/code-standards.md)，确认模块边界、文档注释、错误处理、测试和工具链要求。
2. 在实现或评审时结合 [review checklist](./references/review-checklist.md) 做快速核对。
3. 若项目还未决定加严策略，再确认 `unsafe`、`clippy`、async/FFI、workspace crate 拆分等可选约束。
4. 若当前任务同时使用通用开发闭环，配合 [agent-baseline](../agent-baseline/SKILL.md) 一起使用。