---
name: link-review
description: 'link review'
argument-hint: 'Describe the context or task'
user-invocable: true
disable-model-invocation: false
---

# Link Review

## When To Use

link review

## What This Skill Produces

- 功能点或特定需求完整链路调用逻辑和对应的代码位置, 输出到 docs/link-review-${fn}.md

## Steps

1. 通过调用栈分析，找到功能点或特定需求的完整链路调用逻辑。
2. 根据调用栈中的代码位置，定位到对应的代码文件和行数。
3. 分析代码逻辑，理解功能点或特定需求的实现细节。
4. 将分析结果整理成文档，包含功能点或特定需求的完整链路调用逻辑和对应的代码位置。
5. 特别注意，入口函数中包含多个功能点或特定需求时，需要分别分析每个功能点或特定需求的调用逻辑，并在文档中清晰区分。
6. 输出文档到 docs/link-review-${fn}.md，其中 ${fn} 是功能点或特定需求的名称。
7. 同时生成 Mermaid 图表，展示功能点或特定需求的调用链路。