<!--
    my-skills
    rust-standards/references/review-checklist.md    2026-05-01
     ______     __  __     ______     ______     __     __
    /\  ___\   /\ \_\ \   /\  ___\   /\___  \   /\ \  _ \ \
    \ \___  \  \ \  __ \  \ \  __\   \/_/  /__  \ \ \/ ".\ \
     \/\_____\  \ \_\ \_\  \ \_____\   /\_____\  \ \__/".~\_\
      \/_____/   \/_/\/_/   \/_____/   \/_____/   \/_/   \/_/.com

    @link    : https://github.com/shezw/my-skills
    @author  : shezw
    @email   : hello@shezw.com
-->

# Rust Review Checklist

## Structure

- 模块职责是否单一且边界清晰。
- 模块深度是否保持在默认 3 层以内。
- `main.rs` 或 `lib.rs` 是否保持薄入口。
- 是否存在只为凑模块化而增加的空转发层。

## Size

- 文件是否仍在可维护范围内。
- 过长函数是否真的无法进一步提炼。
- 拆分后的代码是否仍保留上下文可读性。

## Documentation

- crate 根和关键模块是否有 `//!`。
- 公共类型、函数、trait、宏是否有 `///`。
- 文档是否覆盖参数、返回值、错误、panic 和必要示例。
- 易分歧点、性能取舍、所有权边界、锁顺序、`unsafe` 不变量是否有解释。

## API And Errors

- 是否控制了 `pub` 暴露面。
- 是否避免了过早抽象、无意义 trait 和泛型。
- 错误类型是否与层次匹配，是否避免用 `anyhow` 污染底层模块。
- 是否避免了生产路径中的 `unwrap` 和 `expect`。

## Safety And Runtime

- `unsafe` 是否已经收缩边界并写明 `Safety`。
- async 路径是否避免阻塞调用。
- 并发共享状态、取消语义、超时和重试策略是否清晰。

## Verification

- 是否为新增行为、边界条件、错误路径或 bug fix 补了测试。
- 是否计划执行 `cargo fmt`、`cargo clippy --all-targets --all-features -D warnings` 和相关测试。
- 对 lint `allow`、新依赖、feature flag 的引入是否有明确理由。

## Confirm With Project Owner

- 是否将 `unsafe` 升级为 `#![forbid(unsafe_code)]`。
- 是否将 `clippy` 零 warning 设为硬规则。
- 是否需要补 async、FFI、workspace 多 crate 拆分的专项规则。