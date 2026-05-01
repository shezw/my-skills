<!--
    my-skills
    go-standards/assets/project-layout-example.md    2026-05-01
     ______     __  __     ______     ______     __     __
    /\  ___\   /\ \_\ \   /\  ___\   /\___  \   /\ \  _ \ \
    \ \___  \  \ \  __ \  \ \  __\   \/_/  /__  \ \ \/ ".\ \
     \/\_____\  \ \_\ \_\  \ \_____\   /\_____\  \ \__/".~\_\
      \/_____/   \/_/\/_/   \/_____/   \/_____/   \/_/   \/_/.com

    @link    : https://github.com/shezw/my-skills
    @author  : shezw
    @email   : hello@shezw.com
-->

# Project Layout Example

下面是一个兼顾单体与微服务的 Go 项目目录示例。目标是保持领域代码稳定、目录约定清晰，而不是为了“支持微服务”先把仓库拆碎。

```text
cmd/
  gateway/
    main.go
  order-service/
    main.go
internal/
  domain/
    order/
      entity.go
      event.go
      service.go
  application/
    order/
      usecase.go
      command.go
      query.go
  interfaces/
    http/
      order_handler.go
    grpc/
      order_service.go
    websocket/
      order_hub.go
  infrastructure/
    persistence/
      order_repository.go
    messaging/
      event_bus.go
    ai/
      inference_client.go
  bootstrap/
    wire.go
pkg/
  errs/
  tracing/
api/
  proto/
configs/
  config.yaml
```

## Notes

- `cmd/` 只负责启动装配和运行模式选择。
- `internal/domain` 与 `internal/application` 是单体和微服务都应尽量共享的核心。
- `interfaces` 负责协议适配，`infrastructure` 负责具体外部实现。
- 默认深度不超过 3 层；若 bounded context 很大，再考虑细化子目录。