---
name: new-file
description: 'Create new repository files with the project header comment, correct file-type comment syntax, and optional ASCII logo banner. Use when creating source files, Markdown docs, scripts, Mermaid diagrams, or templates in this repository.'
argument-hint: 'Describe the target file path, file type, and whether the ASCII logo banner should be included.'
user-invocable: true
---

<!--
    CNP
    .copilot/skills/new-file SKILL.md    2026-04-30

    @link    : https://github.com/shezw/my-skills
    @author  : shezw
    @email   : hello@shezw.com
-->

# New File

## When to Use

- 在当前项目中创建任何新文件。
- 需要按文件类型自动选择注释语法。

## Procedure

1. 确认目标文件路径、文件类型和逻辑模块。
2. 根据文件类型选择正确的注释风格。
3. 在新文件顶部加入统一头注释，字段内容来自本仓库规则。
4. 除非使用项目级logo，否则加入 personal logo 素材。
5. 如果文件必须以 frontmatter 开头，frontmatter 保持第一段，头注释放在其后。
6. 如果文件格式严格不允许注释，不要写入非法头注释。

## Resources

- [Header templates](./assets/header-templates.md)
- [Personal logo asset](./assets/personal-logo.md)