<!--
    my-skills
    react-standards/assets/feature-layout-example.md    2026-05-01
     ______     __  __     ______     ______     __     __
    /\  ___\   /\ \_\ \   /\  ___\   /\___  \   /\ \  _ \ \
    \ \___  \  \ \  __ \  \ \  __\   \/_/  /__  \ \ \/ ".\ \
     \/\_____\  \ \_\ \_\  \ \_____\   /\_____\  \ \__/".~\_\
      \/_____/   \/_/\/_/   \/_____/   \/_____/   \/_/   \/_/.com

    @link    : https://github.com/shezw/my-skills
    @author  : shezw
    @email   : hello@shezw.com
-->

# Feature Layout Example

下面是一个偏干净、不过度拆分的 React 目录示例。目标是保持 feature 自洽，而不是把所有东西扔进全局 `components/`、`hooks/`、`utils/`。

```text
src/
  app/
    providers/
    router/
    theme/
  pages/
    OrdersPage.tsx
  features/
    orders/
      ui/
        OrdersTable.tsx
        OrderFilters.tsx
      hooks/
        useOrderFilters.ts
      api/
        orders.query.ts
      model/
        order.types.ts
        order.schema.ts
      index.ts
  shared/
    ui/
      PageSection.tsx
    lib/
      formatCurrency.ts
```

## Notes

- 页面入口放在 `pages/` 或框架对应的 route 目录中。
- 单个 feature 内部尽量把 UI、数据、模型和 hooks 收拢在一起。
- `shared/` 只放真正跨 feature 复用且已经稳定的内容。
- 不要轻易继续下钻到 `ui/internal/components/...` 这种层级，默认深度不超过 3 层。