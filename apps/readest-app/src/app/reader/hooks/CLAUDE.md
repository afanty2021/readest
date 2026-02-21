# Reader Hooks 目录

> 导航: [readest](../CLAUDE.md) > app > reader > hooks

## 目录结构

```
src/app/reader/hooks/
├── useAnnotationEditor.ts      # 标注编辑器
├── useAutoHideScrollbar.ts    # 自动隐藏滚动条
├── useAutoSaveBookCover.ts    # 自动保存封面
├── useBookShortcuts.ts        # 书籍快捷键
├── useBooknotesNav.ts         # 笔记导航
├── useBooksManager.ts         # 书籍管理器
├── useFoliateEvents.ts        # Foliate 事件处理
├── useIframeEvents.ts         # iframe 事件
├── useInstantAnnotation.ts    # 即时标注
├── useKOSync.ts              # KOReader 同步
├── useNotesSync.ts            # 笔记同步
├── useOpenAIInNotebook.ts    # AI 笔记本
├── usePagination.ts          # 分页控制
├── useParagraphMode.ts       # 段落模式
├── useProgressAutoSave.ts    # 进度自动保存
├── useProgressSync.ts        # 进度同步
├── useScrollToItem.ts        # 滚动定位
├── useSearchNav.ts           # 搜索导航
├── useSidebar.ts             # 侧边栏控制
├── useTTSControl.ts          # TTS 控制
├── useTTSMediaSession.ts     # TTS 媒体会话
├── useTextSelector.ts        # 文本选择
└── useTextTranslation.ts     # 文本翻译
```

## 核心 Hooks

| Hook | 职责 |
|------|------|
| useTTSControl | TTS 播放控制、进度跟踪 |
| useTextSelector | 文本选择、标注创建 |
| useTextTranslation | 翻译功能集成 |
| useProgressSync | 阅读进度同步 |
| useSidebar | 侧边栏状态管理 |
| useBooksManager | 书籍加载和管理 |

## 与 Store 集成

- `readerStore` - 阅读器状态
- `bookDataStore` - 书籍数据
- `sidebarStore` - 侧边栏
- `settingsStore` - 系统设置
