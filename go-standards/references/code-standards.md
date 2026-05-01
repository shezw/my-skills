<!--
    my-skills
    go-standards/references/code-standards.md    2026-05-01
     ______     __  __     ______     ______     __     __
    /\  ___\   /\ \_\ \   /\  ___\   /\___  \   /\ \  _ \ \
    \ \___  \  \ \  __ \  \ \  __\   \/_/  /__  \ \ \/ ".\ \
     \/\_____\  \ \_\ \_\  \ \_____\   /\_____\  \ \__/".~\_\
      \/_____/   \/_/\/_/   \/_____/   \/_____/   \/_/   \/_/.com

    @link    : https://github.com/shezw/my-skills
    @author  : shezw
    @email   : hello@shezw.com
-->

# Go Code Standards

这份文档面向同时支持单体与微服务的 Go 项目，目标是让核心业务逻辑稳定、可测试、可替换，也让 AI 和新成员能快速理解目录结构与依赖边界。

## Goals

- 保持核心业务逻辑纯 Go、低耦合、易测试。
- 用清晰分层、强约定目录和接口边界，让单体与微服务共享同一套领域能力。
- 让错误、配置、事件、追踪和安全默认一致，减少项目级随意发挥。

## Architecture And Layering

- 严格遵循清洁架构：`interfaces` → `application` → `domain` ← `infrastructure`。
- `domain` 只承载实体、值对象、领域服务、领域事件、领域规则，不依赖数据库、HTTP、gRPC、MQ、日志框架或配置库。
- `application` 负责编排用例、事务边界、权限校验入口、领域对象协调，不直接写传输协议细节。
- `interfaces` 负责 handler、DTO、请求解析、协议适配和对外错误映射。
- `infrastructure` 负责 repo、缓存、消息队列、第三方 AI 服务、服务发现、网关适配和配置装配。

## Dependency Inversion And Interfaces

- 所有外部依赖都先定义接口，再由基础设施层实现，例如数据库、缓存、消息总线、AI 推理、对象存储、时钟与 ID 生成器。
- 接口定义放在消费方最接近的位置，避免把所有接口都扔进巨大的 `ports` 或 `contracts` 包。
- 依赖注入优先使用 compile-time 方式，例如 Wire；若项目已有成熟容器，也要保持构造函数显式依赖。
- 用例层只依赖接口契约，不依赖具体实现、全局单例或隐式 service locator。

## Project Structure And Bounded Contexts

- 目录优先按 bounded context 或业务能力拆分，例如 `internal/domain/order`、`internal/application/order`。
- 默认目录深度不超过 3 层，超出时必须有明确的上下文边界或生成代码原因。
- 单体模式和微服务模式共享同一套 `domain` 与 `application` 代码，不复制业务规则。
- `cmd/` 只放启动入口和装配逻辑，业务规则不得堆在 `main.go`。
- `pkg/` 只放确实需要被多个程序或模块复用、且语义稳定的公共能力；不要把内部业务代码提前暴露到 `pkg/`。

## Configuration And Runtime Modes

- 一份代码支持 `mode: monolith` 与 `mode: microservice`，由 `config.yaml` 或环境变量驱动，而不是靠分叉代码路径硬编码。
- 模块启停、端口、服务发现、外部依赖地址、消费组、限流阈值等都由配置决定。
- 配置加载后尽早转换成显式结构体，不在业务代码里到处读取原始环境变量。
- 敏感配置只来自环境变量、密钥管理系统或受控注入，不写入仓库默认值。

## API Gateways And Protocols

- 统一网关层负责认证、限流、请求 ID、trace 透传、审计和通用中间件。
- 外部协议默认通过适配器暴露：REST(JSON)、gRPC(Protobuf)、WebSocket 各自有明确 handler 边界。
- 协议层 DTO 与领域对象分离，避免把 transport schema 直接当作领域模型。
- 同一用例逻辑应被不同协议复用，而不是为每个协议复制一份业务实现。

## Error Model

- 错误必须同时表达业务语义和技术上下文；统一错误码枚举，不使用只靠字符串 message 的松散约定。
- 推荐在业务错误外层叠加带堆栈的包装，例如 `pkg/errors` 或等价方案，但不要丢失结构化错误码。
- 协议层统一输出标准错误格式，例如 `{"code": ..., "msg": "...", "request_id": "..."}`。
- 错误映射要稳定：领域错误、权限错误、参数错误、下游依赖错误要有清晰边界，不要随意返回 500。

## Event-First And Async

- 耗时或解耦价值明显的业务流程优先通过领域事件驱动，例如订单结算、通知分发、设备指令、AI 推理。
- 单体模式可先使用进程内事件总线；微服务模式再替换为 RabbitMQ、Kafka 或等价消息总线，但事件契约和应用层语义保持一致。
- 事件名称、payload、幂等键、重试语义和死信处理要显式设计，避免“先发起来再说”。
- 同步 RPC 只用于必须同步返回结果的场景，避免把系统全部做成链式同步调用。

## AI-Ready Conventions

- 命名遵循 Go 官方风格，避免花哨缩写和无意义前后缀。
- 所有导出类型、函数、接口、常量组都必须有 doc 注释，便于 IDE 和 AI 理解。
- 重复性代码统一交给 `go:generate`、proto 生成、mock 生成或模板产物，不手写大量机械代码。
- 目录结构保持稳定，例如 `internal/domain/{boundedContext}`、`internal/application/{boundedContext}`，让 AI 能基于固定路径生成代码。

## Observability And Security

- 默认集成 OpenTelemetry，统一 trace、metric 和结构化日志。
- 日志至少包含 `trace_id`、`span_id`、`request_id`；若场景允许，还应包含 `user_id`、租户或业务主键。
- 默认启用 JWT 或等价鉴权、输入校验、SQL 注入防护、跨站或来源控制、敏感字段脱敏。
- 所有 handler 和 repo 调用都必须显式传递 `context.Context`，不要丢掉超时、取消和 trace 链路。

## Readability And Package Discipline

- 包名短而稳定，优先小写单词，不用复数和 `_utils` 这类模糊命名。
- 文件按职责命名，例如 `order_handler.go`、`order_usecase.go`、`order_repository.go`，不要塞进 `misc.go`。
- 一个文件只承载一组紧密相关的类型或逻辑，通常控制在 150 到 300 行；超过 400 行默认评估是否职责过多。
- 函数尽量单一职责，避免超长控制流；超过 80 行时优先评估是否需要提取独立逻辑。
- 只在必要时注释，重点解释“为什么这样做”“边界在哪里”“副作用是什么”。

## Transactions, Concurrency, And Context

- 事务边界由 `application` 层控制，不在 handler 或 repo 中随意开启跨用例事务。
- 并发启动 goroutine 时必须明确所有权、退出条件、错误传播和 `context.Context` 生命周期。
- 不允许无上限 goroutine、无超时外部调用和无 backpressure 的生产者逻辑。
- channel 只在确实建模异步协作时使用，不把它当作随手可用的“高级语法糖”。

## Testing And Quality Gates

- `domain` 层以纯单元测试为主；`application` 层测试用例编排、错误映射和事务语义；`interfaces` 层测试协议契约。
- 合约测试、集成测试和端到端测试要分别覆盖 repo、消息、网关和跨协议入口。
- mock、stub 和 fake 优先通过接口契约生成，不手写大段重复假实现。
- 提交前至少执行 `gofmt`、`go test ./...`、`go vet` 与项目规定的 lint；协议生成代码和 mock 产物需保持最新。

## Keep It Pragmatic

- 不为了“上架构”而过度拆服务或过早引入 MQ。
- 不为了“可扩展”而预抽象所有接口；只有在外部依赖、边界替换、测试隔离确有价值时再抽象。
- 在满足统一约束的前提下，允许项目按实际业务规模裁剪复杂度。