# Todo

一个以截止时间为核心的个人任务管理工具。

## 当前状态

项目当前按新的 SPEC 主线推进。

- 当前有效需求基线：`docs/01-requirements-spec.md`
- 详细设计：已完成
- 实施计划：已完成
- 编码实现：待开始

## 当前原则

- 任务以截止时间为核心
- 开始时间表示进入视野时间，不表示持续占用
- 同步按远程优先语义理解
- 当前要求为 Windows 与 Android 双端兼容，允许分阶段实施但不按单端产品设计
- 当前主线技术架构：`Tauri v2 + Vue 3 + TypeScript + Vite + Rust + SQLite + WebDAV`
- 前端整体界面以自定义设计系统为主，复杂日期时间控件例外采用 `Naive UI`

## 文档

- `docs/01-requirements-spec.md`
- `docs/02-detailed-design.md`
- `docs/03-implementation-plan.md`
