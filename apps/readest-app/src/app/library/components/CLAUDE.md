# Library Components 书架组件

> 导航: [readest](../CLAUDE.md) > app > library > components

## 目录结构

```
src/app/library/components/
├── BookItem.tsx           # 书籍项
├── Bookshelf.tsx         # 书架容器
├── BookshelfItem.tsx     # 书架书籍项
├── GroupHeader.tsx       # 分组标题
├── GroupItem.tsx         # 分组项
├── GroupingModal.tsx     # 分组管理弹窗
├── ImportMenu.tsx       # 导入菜单
├── LibraryHeader.tsx    # 书架头部
├── MigrateDataWindow.tsx # 数据迁移窗口
├── OPDSDialog.tsx       # OPDS 订阅对话框
├── ReadingProgress.tsx  # 阅读进度
├── SelectModeActions.tsx # 多选操作栏
├── SetStatusAlert.tsx   # 设置状态提示
├── SettingsMenu.tsx    # 设置菜单
├── StatusBadge.tsx     # 状态徽章
├── TransferQueuePanel.tsx # 传输队列面板
└── ViewMenu.tsx        # 视图菜单
```

## 核心组件

| 组件 | 职责 |
|------|------|
| Bookshelf | 书架主容器，管理书籍列表和布局 |
| BookItem | 单本书籍展示（封面、标题、进度） |
| ImportMenu | 导入书籍菜单 |
| OPDSDialog | OPDS 订阅源管理 |
| TransferQueuePanel | 下载/上传队列显示 |

## 与 Store 集成

- `libraryStore` - 书架数据、分组、同步进度
- `transferStore` - 文件传输队列
