# 测试与结果回写规范

## 数据库

`.agent/tests/results.db` 使用 SQLite，表结构如下：

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| `id` | `INTEGER PRIMARY KEY AUTOINCREMENT` | 测试记录主键 |
| `project` | `TEXT` | 项目名称 |
| `scene` | `TEXT` | 测试场景 |
| `target` | `TEXT` | 测试目标 |
| `create_time` | `DATETIME` | 记录创建时间 |
| `fails` | `INTEGER` | 失败次数，默认 `0` |
| `passed_time` | `DATETIME` | 最近一次通过时间 |

## 推荐流程

1. 创建任务时先向 `results.db` 插入一条记录。
2. 取回 `id` 后，再创建测试说明文档，保证文件与数据库存在稳定映射。
3. 测试文档中必须写清楚：
   - 测试准备
   - 测试步骤
   - 布尔判定规则
   - 最近一次执行结果
4. 验证失败时执行：`fails = fails + 1`。
5. 验证通过时执行：`passed_time = CURRENT_TIMESTAMP`。

## 文件命名

为保证文档与数据库一一对应，测试文件名采用：

`{scene}-{YMDHMin}-{target}-{id}.md`

其中：

- `{scene}`: 当前任务场景，如 `baseline`
- `{YMDHMin}`: 任务时间戳，如 `202605012045`
- `{target}`: 测试目标，如 `agent-baseline`
- `{id}`: `results.db` 中插入记录后的主键