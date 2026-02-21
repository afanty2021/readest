# Types 类型定义目录

> 导航: [readest](../CLAUDE.md) > types

## 目录结构

```
src/types/
├── annotator.ts       # 标注相关类型
├── book.ts            # 书籍数据类型
├── error.ts           # 错误类型
├── kosync.ts          # KOReader 同步类型
├── misc.ts            # 杂项类型
├── opds.ts            # OPDS 类型
├── payment.ts         # 支付相关类型
├── quota.ts           # 配额类型
├── records.ts         # 记录类型
├── settings.ts        # 设置类型
├── system.ts          # 系统类型
└── view.ts           # 视图类型
```

## 核心类型

### book.ts
- `BookConfig` - 书籍配置
- `BookMetadata` - 书籍元数据
- `BookProgress` - 阅读进度
- `Bookmarks` - 书签

### settings.ts
- `UserSettings` - 用户设置
- `ViewSettings` - 视图设置

### annotator.ts
- `Annotation` - 标注
- `Highlight` - 高亮
- `Note` - 笔记

### payment.ts
- `UserPlan` - 用户计划
- `Subscription` - 订阅信息

## 类型导出模式

```typescript
// 统一从 index.ts 导出
export * from './book';
export * from './settings';
// ...
```
