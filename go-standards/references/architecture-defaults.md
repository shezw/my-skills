<!--
    my-skills
    go-standards/references/architecture-defaults.md    2026-05-01
     ______     __  __     ______     ______     __     __
    /\  ___\   /\ \_\ \   /\  ___\   /\___  \   /\ \  _ \ \
    \ \___  \  \ \  __ \  \ \  __\   \/_/  /__  \ \ \/ ".\ \
     \/\_____\  \ \_\ \_\  \ \_____\   /\_____\  \ \__/".~\_\
      \/_____/   \/_/\/_/   \/_____/   \/_____/   \/_/   \/_/.com

    @link    : https://github.com/shezw/my-skills
    @author  : shezw
    @email   : hello@shezw.com
-->

# Go Architecture Defaults

## Runtime Modes

- `mode: monolith` 时启动所有核心模块、统一网关和本地事件总线。
- `mode: microservice` 时按配置启动指定 bounded context、协议入口和消息消费者。
- 运行模式切换不应要求复制领域代码或改写业务用例。

## Dependency Injection

- 默认优先使用 Wire 进行 compile-time 依赖注入。
- 依赖装配集中在 `cmd/` 或 `bootstrap/`，避免到处 new 实现对象。
- 构造函数签名要显式，便于测试和 AI 生成代码时直接补全依赖。

## Recommended Core Libraries

- 配置：Viper 或等价成熟方案，但最终都映射到显式结构体。
- 日志：支持结构化日志和字段输出的成熟库。
- 追踪与指标：OpenTelemetry。
- 验证：validator 或等价方案。
- 协议：REST、gRPC、WebSocket 通过独立 adapter 暴露。

## Error And Response Shape

- 统一响应错误载荷：`code`、`msg`、`request_id` 为最小必备字段。
- 服务间错误码映射要稳定；不要把底层数据库错误直接透出到接口层。

## Event Bus Defaults

- 单体默认使用进程内事件总线，适合先验证业务流程和事件契约。
- 微服务默认切换到 RabbitMQ、Kafka 或现有消息基础设施，但应用层只依赖事件接口。
- 事件消费者必须具备幂等、重试和监控能力。

## Security Baseline

- 鉴权默认启用 JWT 或等价令牌机制。
- 输入校验默认开启，DTO 与领域对象映射时做白名单转换。
- 数据访问必须使用参数化查询或 ORM 安全接口，不拼接 SQL。
- 敏感配置通过环境变量、Vault 或等价密钥管理系统注入。