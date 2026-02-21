# Store 目录 - 状态管理

> 导航: [readest](../CLAUDE.md) > store

## 目录结构

```
src/store/
├── settingsStore.ts        # 系统设置管理
├── readerStore.ts          # 阅读器视图状态
├── libraryStore.ts         # 书架/图书馆管理
├── bookDataStore.ts        # 书籍数据管理
├── themeStore.ts           # 主题/外观管理
├── sidebarStore.ts         # 侧边栏状态管理
├── notebookStore.ts        # 笔记本/笔记管理
├── aiChatStore.ts          # AI 对话管理
├── deviceStore.ts          # 设备控制管理
├── parallelViewStore.ts    # 并排视图管理
├── proofreadStore.ts       # 校对规则管理
├── customFontStore.ts      # 自定义字体管理
├── customTextureStore.ts   # 自定义纹理管理
├── trafficLightStore.ts    # macOS 窗口控制管理
└── transferStore.ts        # 文件传输管理
```

## 技术方案

**Zustand** - 统一使用 Zustand 作为状态管理方案

## 核心 Store

### settingsStore.ts
- 系统全局设置
- UI 语言管理
- 字体面板视图

### readerStore.ts
- 阅读器视图状态 (FoliateView)
- 阅读进度跟踪
- 视图设置管理

### libraryStore.ts
- 书籍库管理
- 书籍分组
- 同步进度

### bookDataStore.ts
- 书籍持久化数据
- 书籍配置 (BookConfig)
- 笔记管理

### themeStore.ts
- 主题模式 (light/dark/auto)
- 主题色
- 系统 UI 可见性

### sidebarStore.ts
- 侧边栏显示状态
- 搜索导航状态
- 笔记导航状态

### notebookStore.ts
- 笔记本面板
- 笔记编辑状态
- AI 对话标签

### aiChatStore.ts
- AI 对话管理
- 对话历史
- 消息管理

### deviceStore.ts
- 音量键拦截
- 返回键拦截
- 屏幕亮度控制

### transferStore.ts
- 文件传输队列
- 下载/上传进度
- 并发控制

### 其他 Store

| Store | 职责 |
|-------|------|
| parallelViewStore.ts | 多本书并排显示 |
| proofreadStore.ts | 校对规则 |
| customFontStore.ts | 自定义字体 |
| customTextureStore.ts | 自定义纹理 |
| trafficLightStore.ts | macOS 窗口控制 |

## 持久化策略

```
Zustand Stores → AppService Layer → NativeAppService (Tauri/文件系统)
                                → WebAppService (IndexedDB/localStorage)
```

## API 设计模式

```typescript
export const useXxxStore = create<XxxState>((set, get) => ({
  // 状态
  state: value,

  // 同步方法
  setXxx: (value) => set({ xxx: value }),

  // 异步方法
  async actionXxx: async (params) => {
    const result = await doSomething();
    set({ result });
  }
}));
```

## 跨 Store 调用

```typescript
const { library, setLibrary } = useLibraryStore.getState();
const { settings } = useSettingsStore.getState();
```
