# OPDS 模块 (OPDS)

> 更新时间：2026-02-21 15:08:21

## 相对路径面包屑

`[根目录](../../../../CLAUDE.md) > [apps/readest-app](../) > **opds**

## 模块职责

提供 OPDS (Open Publication Distribution System) 支持，允许用户订阅在线图书馆、Calibre 服务器、以及其他 OPDS 兼容的图书源。

## 入口与启动

- **页面入口**: `apps/readest-app/src/app/opds/page.tsx`

## 对外接口

### 页面路由
- `/opds` - OPDS 订阅管理页面

### 核心组件
| 组件 | 路径 | 职责 |
|------|------|------|
| FeedView | `components/FeedView.tsx` | OPDS 内容视图 |
| Navigation | `components/Navigation.tsx` | 导航栏 |
| PublicationCard | `components/PublicationCard.tsx` | 出版物卡片 |
| PublicationView | `components/PublicationView.tsx` | 出版物详情 |
| SearchView | `components/SearchView.tsx` | 搜索视图 |
| CatalogManager | `components/CatelogManager.tsx` | 订阅目录管理 |

### 工具函数
- `opdsReq.ts` - OPDS 请求处理
- `opdsUtils.ts` - OPDS 数据转换

## 关键依赖

- `@tauri-apps/plugin-http` - HTTP 请求
- `@tauri-apps/plugin-fs` - 文件系统访问

## 数据模型

### OPDS 订阅源
```typescript
interface OPDSFeed {
  id: string;
  title: string;
  url: string;
  type: 'navigation' | 'acquisition';
  icon?: string;
}
```

## 相关文件清单

- `app/library/components/x` - OPDSDialog.ts书架中的订阅弹窗

## 变更记录

### 2026-02-21 - 模块文档创建
- 创建 OPDS 模块 CLAUDE.md
