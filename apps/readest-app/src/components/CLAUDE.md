# Components 组件目录

> 导航: [readest](../CLAUDE.md) > components

## 目录结构

```
src/components/
├── assistant/               # AI 对话助手 UI
│   ├── MarkdownText.tsx     # Markdown 渲染
│   ├── Thread.tsx           # 对话线程
│   └── TooltipIconButton.tsx
├── command-palette/         # 命令面板 (Cmd+Shift+P)
│   ├── CommandPalette.tsx
│   ├── CommandPaletteProvider.tsx
│   └── HighlightChars.tsx
├── metadata/                # 图书元数据管理
│   ├── BookDetailModal.tsx
│   ├── BookDetailView.tsx
│   ├── BookDetailEdit.tsx
│   └── SourceSelector.tsx
├── primitives/             # 基础 UI 原语 (@/components/ui/*)
│   ├── button.tsx, dialog.tsx
│   ├── dropdown-menu.tsx
│   ├── select.tsx, tooltip.tsx
│   └── ...
├── settings/                # 设置面板系统
│   ├── SettingsDialog.tsx   # 7 标签页主容器
│   ├── FontPanel.tsx, LayoutPanel.tsx
│   ├── ColorPanel.tsx, ControlPanel.tsx
│   └── color/               # 颜色子组件
├── AboutWindow.tsx          # 关于窗口
├── Alert.tsx               # 确认对话框
├── BookCover.tsx           # 图书封面 (memo 优化)
├── CachedImage.tsx         # 带缓存的图片
├── Dialog.tsx              # 核心对话框
├── Dropdown.tsx            # 下拉菜单
├── Menu.tsx/MenuItem.tsx   # 菜单系统
├── Slider.tsx              # 自定义滑块
├── Toast.tsx               # 全局通知
├── WindowButtons.tsx       # 窗口控制按钮
└── ...
```

## 组件复用模式

### 双层架构
- **primitives/**: Radix UI 原语封装 (@/components/ui/*)
- **顶层组件**: DaisyUI + Tailwind 业务组件

### 核心复用组件
| 组件 | 被消费于 |
|------|----------|
| Dialog | AboutWindow, UpdaterWindow, BookDetailModal, SettingsDialog |
| Dropdown + MenuItem | 各工具栏、设置面板 |

## 与 Store 集成

| Store | 使用组件 |
|-------|----------|
| settingsStore | SettingsDialog, FontPanel, ColorPanel 等 |
| themeStore | Providers, Dialog, Toast |
| readerStore | FontPanel, LayoutPanel |
| deviceStore | Dialog (Android 返回键拦截) |

## 性能优化

- **React.memo**: BookCover, CachedImage
- **内存缓存**: CachedImage (Map + Promise 去重)
- **forwardRef**: TextEditor 暴露 imperative API
