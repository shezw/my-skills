<!--
    my-skills
    react-standards/references/code-standards.md    2026-05-01
     ______     __  __     ______     ______     __     __
    /\  ___\   /\ \_\ \   /\  ___\   /\___  \   /\ \  _ \ \
    \ \___  \  \ \  __ \  \ \  __\   \/_/  /__  \ \ \/ ".\ \
     \/\_____\  \ \_\ \_\  \ \_____\   /\_____\  \ \__/".~\_\
      \/_____/   \/_/\/_/   \/_____/   \/_____/   \/_/   \/_/.com

    @link    : https://github.com/shezw/my-skills
    @author  : shezw
    @email   : hello@shezw.com
-->

# React Code Standards

这份文档沉淀一套偏成熟工程团队风格的 React 规范。默认假设项目以 React + TypeScript 为主，优先使用成熟稳定库，减少自造基础设施。

## Goals

- 保持模块边界清晰、组件职责单一、代码可读且易重构。
- 优先组合成熟库和框架能力，不重复造基础 UI、表单、通知、图标、服务端状态等轮子。
- 用一致的结构、命名、测试和可访问性标准，降低多人协作成本。

## Default Baseline

- 默认使用 React + TypeScript；如果项目已经有成熟框架或现成设计系统，优先遵循现有体系而不是强行替换。
- 绿地项目默认 UI 栈采用 Mantine，图标默认使用 `@tabler/icons-react`。
- 保持模块深度默认不超过 3 层；超出时必须有明确业务或架构理由。

## Project Structure And Module Boundaries

- 优先 feature-first 结构：按业务能力拆目录，而不是按 `components`、`utils`、`types` 全局横切拆分。
- 页面或 route 文件只做页面级组装、数据边界和布局协调，不堆积复杂业务判断。
- 单个 feature 内优先把 `ui`、`hooks`、`api`、`model` 放在同一 feature 边界中，减少跨目录跳转。
- 不要为了“看起来模块化”而创建多层空目录、纯转发组件或无意义 barrel。
- `index.ts` 只建议在 feature 根或公共模块根做受控导出，不要在每一级目录都加 barrel。

## File Size And Split Heuristics

- React 组件文件建议控制在 120 到 220 行；超过 280 行时默认评估是否存在多职责。
- 页面文件可略大，但超过 350 行时应优先拆出独立区块、hooks 或子模块。
- 自定义 hook 建议控制在 40 到 120 行；超过 150 行时评估是否混入多个状态机或副作用源。
- 一个文件默认只放一个主要组件；仅允许放少量紧耦合的私有小组件或常量。
- 不要为了缩短文件而把上下文强相关逻辑拆得过碎，导致阅读必须来回跳文件。

## Component Boundaries

- 页面组件负责路由参数、权限判断、数据装配和大布局，不负责细碎交互细节。
- 业务组件负责一个完整业务意图，例如筛选面板、详情卡片、编辑表单，而不是“一个 div 一个文件”。
- 展示型组件尽量纯粹：通过 props 接收数据和回调，避免直接耦合数据获取。
- 只有当状态逻辑被多个组件复用、或单个组件内部状态机已经明显复杂时，才提取自定义 hook。
- 共享组件先放在 feature 内复用，确认跨多个 feature 稳定复用后再上升到 shared 层。

## Readability And Naming

- 命名优先业务语义，不用 `data`, `item`, `handler`, `temp` 这类低信息量命名充斥核心代码。
- 组件用 `PascalCase`，hooks 用 `camelCase` 且以 `use` 开头，事件处理函数以 `handle` 开头。
- 共享可复用组件与 hooks 优先使用命名导出；默认导出仅保留给路由入口、页面入口或框架约定文件。
- 优先早返回、提早处理空态和异常态，避免把正常路径埋在多层 `if` 中。
- 不要为省几行代码而写难读的三元链、内联匿名大函数或过度链式表达式。

## Comments And Documentation

- route 入口、provider 组合、复杂数据流或特殊缓存边界可以写短文件头说明，讲清职责和边界。
- 共享组件、共享 hooks、复杂工具函数需要有简短 doc comment，说明用途、关键参数和返回约束。
- 对以下内容必须写“为什么”的注释：特殊 memo 化、非直观 effect 依赖、竞态规避、性能取舍、权限或埋点分支、兼容性 workaround。
- 不要用注释重复 JSX 已经清楚表达的结构；优先重命名和拆函数，而不是用注释拯救晦涩代码。

## Hooks, State, And Effects

- 本地状态尽量靠近使用点，避免把临时 UI 状态无意义提升到全局。
- 能从 props 或其他状态直接推导出的值不要再单独存一份 state。
- `useEffect` 只用于与 React 外部系统同步，例如订阅、DOM、定时器、浏览器 API、显式网络触发；不要用 effect 做纯派生计算。
- `useMemo`、`useCallback` 默认不主动添加；只有在性能证据明确、或需要稳定引用语义时才使用。
- 复杂本地交互状态优先考虑 `useReducer` 或封装 hook，而不是堆叠很多耦合的 `useState`。
- 对大列表筛选、搜索联想、复杂切换等交互，可优先考虑 `useDeferredValue`、`startTransition` 等现代 React 手段。

## Data Fetching And Async Boundaries

- 如果框架本身有成熟数据层，优先使用框架原生方案；否则服务端状态默认使用 TanStack Query。
- 数据获取逻辑放在页面边界、feature hook 或 `api` 模块，不直接散落在纯展示组件内部。
- 加载、空态、错误态要成为显式 UI 分支，而不是用一堆可空判断混在同一块 JSX 中。
- 请求参数、响应转换、缓存键和重试策略集中在同一模块管理，避免到处手写 fetch 细节。

## UI And Styling

- 默认优先使用 Mantine 提供的成熟组件、hooks、form、notifications、modals 和 theme 扩展能力。
- 默认图标库使用 `@tabler/icons-react`，不要在一个项目中混用多个图标风格而缺乏统一理由。
- 先扩展 Mantine theme，再做局部样式定制；不要到处硬编码颜色、间距、字号和阴影。
- 复杂局部样式优先用 CSS Modules 或 Mantine 的样式扩展方式；避免在 JSX 中堆积大段内联 style 对象。
- 只有在 Mantine 缺失关键能力或现有抽象确实不适配时，才自建底层 UI 组件。

## Forms And Validation

- 默认表单方案使用 `@mantine/form`，校验优先用 Zod 等结构化 schema。
- 字段定义、默认值、转换和校验逻辑集中管理，不要在 JSX 里临时拼接大量表单逻辑。
- 提交态、脏状态、禁用态和错误提示需要明确，避免用户不知道当前操作结果。

## Accessibility

- 优先使用语义化 HTML 和 Mantine 自带的可访问性能力，不要无理由把按钮写成 `div`。
- 所有交互控件必须可键盘访问，可见焦点态不能被去掉。
- 表单字段必须有可读 label、描述或等价可访问名称。
- 图标按钮必须提供可访问名称；纯装饰图标要标记为装饰用途。
- 颜色对比、错误提示、加载反馈和空态文案都应考虑真实用户可理解性。

## Testing

- 组件和页面测试默认采用 React Testing Library，断言用户可见行为而不是实现细节。
- 测试运行器可使用 Vitest 或 Jest；接口层 mock 优先 MSW。
- 新增行为、边界条件、权限分支、错误态和回归修复必须补测试。
- 不为简单纯展示组件堆砌低价值 snapshot；优先测试关键交互和状态转移。

## Performance

- 路由和大区块优先按页面或功能边界拆分 code splitting。
- 长列表、重量级图表、复杂编辑器等场景尽早评估虚拟化和懒加载。
- 避免无意义全局状态导致大面积重渲染；先解决数据边界，再谈 memo 化。
- 图片、富媒体和重依赖组件优先按框架最佳实践做延迟加载与体积控制。

## Dependencies And Quality Gates

- 优先选择维护活跃、文档完整、API 稳定的成熟库；默认先看 Mantine 是否已覆盖需求。
- 不要同时引入多个同类基础库，例如多个 UI 库、多个表单库、多个服务端状态库。
- TypeScript 应保持严格模式；lint 和 format 规则不应长期被注释绕过。
- 提交前至少执行 lint、类型检查、相关测试；React 项目若无特殊原因，不应跳过 a11y 与 hooks 规则检查。