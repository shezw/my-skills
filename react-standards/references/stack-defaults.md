<!--
    my-skills
    react-standards/references/stack-defaults.md    2026-05-01
     ______     __  __     ______     ______     __     __
    /\  ___\   /\ \_\ \   /\  ___\   /\___  \   /\ \  _ \ \
    \ \___  \  \ \  __ \  \ \  __\   \/_/  /__  \ \ \/ ".\ \
     \/\_____\  \ \_\ \_\  \ \_____\   /\_____\  \ \__/".~\_\
      \/_____/   \/_/\/_/   \/_____/   \/_____/   \/_/   \/_/.com

    @link    : https://github.com/shezw/my-skills
    @author  : shezw
    @email   : hello@shezw.com
-->

# React Stack Defaults

这份文档描述在“没有特别偏好”的前提下，React 项目的默认推荐栈。若现有项目已经有成熟设计系统、框架约束或基础设施，优先尊重既有体系。

## Baseline

- 语言：TypeScript
- UI 组件：`@mantine/core`
- Mantine 生态：`@mantine/hooks`、`@mantine/form`、`@mantine/notifications`、`@mantine/modals`
- 图标：`@tabler/icons-react`
- 服务端状态：TanStack Query（在框架没有更优原生数据层时）
- 表单校验：Zod
- 测试：React Testing Library + Vitest 或 Jest + MSW
- 样式：Mantine theme + CSS Modules

## UI Adoption Rules

- 先看 Mantine 现成组件是否已满足需求，再决定是否包装或自建。
- 主题、间距、字体层级、颜色、圆角等统一收敛到 Mantine theme。
- 通知、模态框、抽屉、表单输入等基础设施默认使用 Mantine 提供方案，避免重复造轮子。
- 图标统一使用 Tabler，避免混入 Material、Heroicons、Lucide 等多套风格，除非项目已有统一标准。

## When To Deviate

- 现有项目已经有成熟设计系统或明确品牌体系。
- Mantine 在核心交互或性能要求上无法满足产品目标。
- 框架原生能力比通用库更自然，例如 Next.js 的路由、数据和图片能力。

## What To Avoid By Default

- 同时引入多个 UI 库。
- 为小项目过早接入重型全局状态库。
- 为简单表单同时混用多套表单和校验方案。
- 在没有设计系统原因的前提下大量自建底层 Button、Input、Modal、Tooltip 等基础组件。