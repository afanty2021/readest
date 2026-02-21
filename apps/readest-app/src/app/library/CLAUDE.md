# 书架模块 (Library)

> 更新时间：2026-02-21 15:08:21

## 相对路径面包屑

`[根目录](../../CLAUDE.md) > [apps/readest-app](../) > **library**

## 模块职责

负责电子书图书馆的管理，包括图书导入、分类、排序、搜索、OPDS 同步、阅读进度跟踪等功能。

## 入口与启动

- **页面入口**: `apps/readest-app/src/app/library/page.tsx`
- **布局入口**: `apps/readest-app/src/app/library/layout.tsx` (如存在)

## 对外接口

### 页面路由
- `/library` - 书架主页
- `/library?status=reading` - 按阅读状态筛选
- `/library?status=completed` - 已完成
- `/library?status=dropped` - 已放弃
- `/library?status=reading` - 在读

### 核心组件
| 组件 | 路径 | 职责 |
|------|------|------|
| Bookshelf | `components/Bookshelf.tsx` | 书架网格布局 |
| BookItem | `components/BookItem.tsx` | 单本书籍卡片 |
| BookshelfItem | `components/BookshelfItem.tsx` | 书架视图项 |
| GroupingModal | `components/GroupingModal.tsx` | 分组管理弹窗 |
| ImportMenu | `components/ImportMenu.tsx` | 导入菜单 |
| SettingsMenu | `components/SettingsMenu.tsx` | 设置菜单 |
| OPDSDialog | `components/OPDSDialog.tsx` | OPDS 订阅弹窗 |
| TransferQueuePanel | `components/TransferQueuePanel.tsx` | 传输队列面板 |

### 核心 Hooks
| Hook | 路径 | 职责 |
|------|------|------|
| useBooksSync | `hooks/useBooksSync.ts` | 书籍同步 |
| useDragDropImport | `hooks/useDragDropImport.ts` | 拖拽导入 |

### 工具函数
- `libraryUtils.ts` - 图书馆工具函数

## 关键依赖

- `@tauri-apps/plugin-fs` - 文件系统访问
- `@tauri-apps/plugin-dialog` - 文件选择对话框
- `@supabase/supabase-js` - 数据同步后端

## 数据模型

### 书籍元数据结构
```typescript
interface Book {
  id: string;
  title: string;
  author?: string;
  cover?: string;
  format: 'epub' | 'mobi' | 'pdf' | 'fb2' | 'cbz' | 'txt';
  filePath: string;
  fileSize: number;
  progress: number;
  status: 'reading' | 'completed' | 'dropped' | 'to-read';
  addedAt: number;
  lastReadAt?: number;
  tags?: string[];
  series?: string;
}
```

## 测试与质量

- **测试文件**: `src/__tests__/utils/libraryUtils.test.ts`
- **测试框架**: Vitest
- **覆盖范围**: 图书数据处理、排序逻辑

## 常见问题 (FAQ)

### 如何导入书籍？
1. 点击右上角导入按钮
2. 支持文件选择器或拖拽导入
3. 支持 OPDS 订阅导入

### 如何同步阅读进度？
通过 Supabase 后端进行跨设备同步

## 相关文件清单

- `store/libraryStore.ts` - 图书馆状态管理
- `services/transferManager.ts` - 文件传输管理
- `services/metadata/` - 元数据获取服务

## 变更记录

### 2026-02-21 - 模块文档创建
- 创建书架模块 CLAUDE.md
- 记录核心组件、Hooks、依赖
