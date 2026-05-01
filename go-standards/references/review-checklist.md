<!--
    my-skills
    go-standards/references/review-checklist.md    2026-05-01
     ______     __  __     ______     ______     __     __
    /\  ___\   /\ \_\ \   /\  ___\   /\___  \   /\ \  _ \ \
    \ \___  \  \ \  __ \  \ \  __\   \/_/  /__  \ \ \/ ".\ \
     \/\_____\  \ \_\ \_\  \ \_____\   /\_____\  \ \__/".~\_\
      \/_____/   \/_/\/_/   \/_____/   \/_____/   \/_/   \/_/.com

    @link    : https://github.com/shezw/my-skills
    @author  : shezw
    @email   : hello@shezw.com
-->

# Go Review Checklist

## Layering

- handler、usecase、domain、repo 或 adapter 是否职责清晰。
- `domain` 是否仍保持纯 Go，不依赖协议、数据库或框架。
- 事务、权限和编排逻辑是否位于 `application` 层，而不是散落在 handler 或 repo。

## Interfaces And DI

- 外部依赖是否通过接口隔离。
- 接口是否定义在消费方附近，而不是堆在全局大包里。
- 构造函数依赖是否显式，是否避免了全局单例和隐藏依赖。

## Config And Runtime

- 运行模式是否由配置驱动，而不是硬编码分支。
- 模块启停、端口、服务发现和外部依赖地址是否都可配置。
- 敏感配置是否通过环境变量或密钥系统注入。

## APIs And Errors

- REST、gRPC、WebSocket 是否通过 adapter 暴露，而不是复制业务逻辑。
- 错误码、错误包装和对外错误响应是否统一。
- 请求 ID、trace 信息和日志字段是否可贯穿链路。

## Events And Concurrency

- 耗时流程是否优先事件驱动，而不是全部走同步链路。
- goroutine、channel、超时和取消语义是否清晰。
- 事件是否定义了幂等、重试和监控边界。

## AI-Ready And Readability

- 导出标识符是否有 doc 注释。
- 目录和文件命名是否强约定、低歧义。
- 生成代码是否通过 `go:generate` 或既有工具产出，而不是手写机械代码。
- 文件和函数是否保持在可读范围内，注释是否说明“为什么”。

## Security And Testing

- 是否有输入校验、鉴权、参数化查询和敏感信息保护。
- `context.Context` 是否在关键链路中完整传递。
- 是否为领域规则、错误路径、repo 契约、消息处理和协议适配补了对应测试。
- 是否计划执行 `gofmt`、`go test ./...`、`go vet` 和项目 lint。