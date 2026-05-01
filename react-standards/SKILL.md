---
name: react-standards
description: 'Use when writing, reviewing, refactoring, or designing React applications. Covers project structure, component boundaries, readability, hooks, state, testing, accessibility, performance, and default UI stack choices such as Mantine and @tabler/icons-react.'
argument-hint: 'Describe the React app, feature, page, or component concern'
user-invocable: true
disable-model-invocation: false
---

<!--
    my-skills
    react-standards/SKILL.md    2026-05-01
     ______     __  __     ______     ______     __     __
    /\  ___\   /\ \_\ \   /\  ___\   /\___  \   /\ \  _ \ \
    \ \___  \  \ \  __ \  \ \  __\   \/_/  /__  \ \ \/ ".\ \
     \/\_____\  \ \_\ \_\  \ \_____\   /\_____\  \ \__/".~\_\
      \/_____/   \/_/\/_/   \/_____/   \/_____/   \/_/   \/_/.com

    @link    : https://github.com/shezw/my-skills
    @author  : shezw
    @email   : hello@shezw.com
-->

# React Standards

## When To Use

- 编写、评审、重构或设计 React 应用、页面、组件、hooks 和前端模块时。
- 需要统一模块边界、可读性、UI 选型和工程门槛时。
- 需要在绿地项目中快速得到一套成熟、稳定、优先使用现成优质库的默认规范时。

## What This Skill Produces

- React 项目编码标准，见 [code standards](./references/code-standards.md)
- 默认 UI 与工程栈建议，见 [stack defaults](./references/stack-defaults.md)
- 编码与评审检查清单，见 [review checklist](./references/review-checklist.md)
- 目录拆分示例，见 [feature layout example](./assets/feature-layout-example.md)
- 与自动生效规则的对应关系说明：真正对 React 组件文件默认生效的规则位于用户级 `react.instructions.md`

## Procedure

1. 先读取 [code standards](./references/code-standards.md)，确认模块边界、组件拆分、状态处理、测试与性能要求。
2. 若是新项目或还未定栈，再读取 [stack defaults](./references/stack-defaults.md)，优先使用默认的 Mantine 与 Tabler Icon 方案。
3. 在实现或评审时结合 [review checklist](./references/review-checklist.md) 快速核对结构、a11y、测试和依赖选择。
4. 若需要落具体目录结构或讨论如何拆 feature，可参考 [feature layout example](./assets/feature-layout-example.md)。
5. 若当前任务同时使用通用开发闭环，配合 [agent-baseline](../agent-baseline/SKILL.md) 一起使用。