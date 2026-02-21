# 阅读器模块 (Reader)

> 更新时间：2026-02-21 15:08:21

## 相对路径面包屑

`[根目录](../../../../CLAUDE.md) > [apps/readest-app](../) > **reader**

## 模块职责

Readest 的核心阅读模块，提供沉浸式阅读体验，支持多种阅读模式、标注、笔记、翻译、TTS、RSVP 速读等功能。

## 入口与启动

- **页面入口**: `apps/readest-app/src/app/reader/page.tsx`
- **Reader 组件**: `components/Reader.tsx` - 主阅读器容器

## 对外接口

### 页面路由
- `/reader?id={bookId}` - 打开指定书籍

### 核心组件

#### 阅读核心
| 组件 | 路径 | 职责 |
|------|------|------|
| Reader | `components/Reader.tsx` | 阅读器主容器 |
| ReaderContent | `components/ReaderContent.tsx` | 阅读内容区域 |
| FoliateViewer | `components/FoliateViewer.tsx` | Foliate 渲染器封装 |

#### 标注系统
| 组件 | 路径 | 职责 |
|------|------|------|
| Annotator | `components/annotator/Annotator.tsx` | 标注系统入口 |
| AnnotationPopup | `components/annotator/AnnotationPopup.tsx` | 标注弹窗 |
| AnnotationNotes | `components/annotator/AnnotationNotes.tsx` | 笔记编辑器 |
| HighlightOptions | `components/annotator/HighlightOptions.tsx` | 高亮选项 |
| TranslatorPopup | `components/annotator/TranslatorPopup.tsx` | 翻译弹窗 |
| ProofreadPopup | `components/annotator/ProofreadPopup.tsx` | 校对弹窗 |

#### 侧边栏
| 组件 | 路径 | 职责 |
|------|------|------|
| SideBar | `components/sidebar/SideBar.tsx` | 侧边栏容器 |
| TOCView | `components/sidebar/TOCView.tsx` | 目录视图 |
| SearchResults | `components/sidebar/SearchResults.tsx` | 搜索结果 |
| BooknotesNav | `components/sidebar/BooknotesNav.tsx` | 笔记导航 |

#### 底部栏
| 组件 | 路径 | 职责 |
|------|------|------|
| FooterBar | `components/footerbar/FooterBar.tsx` | 底部栏容器 |
| FontLayoutPanel | `components/footerbar/FontLayoutPanel.tsx` | 字体布局设置 |
| NavigationPanel | `components/footerbar/NavigationPanel.tsx` | 导航面板 |

#### TTS 语音
| 组件 | 路径 | 职责 |
|------|------|------|
| TTSBar | `components/tts/TTSBar.tsx` | TTS 控制栏 |
| TTSPanel | `components/tts/TTSPanel.tsx` | TTS 设置面板 |

#### 速读模式
| 组件 | 路径 | 职责 |
|------|------|------|
| RSVPControl | `components/rsvp/RSVPControl.tsx` | RSVP 控制 |
| RSVPOverlay | `components/rsvp/RSVPOverlay.tsx` | RSVP 覆盖层 |

#### 特殊模式
| 组件 | 路径 | 职责 |
|------|------|------|
| ParagraphBar | `components/paragraph/ParagraphBar.tsx` | 段落模式导航 |
| ParagraphOverlay | `components/paragraph/ParagraphOverlay.tsx` | 段落模式覆盖 |

### 核心 Hooks
| Hook | 路径 | 职责 |
|------|------|------|
| useBookShortcuts | `hooks/useBookShortcuts.ts` | 键盘快捷键 |
| useFoliateEvents | `hooks/useFoliateEvents.ts` | Foliate 事件处理 |
| useTTSControl | `hooks/useTTSControl.ts` | TTS 控制 |
| useProgressSync | `hooks/useProgressSync.ts` | 进度同步 |
| useAnnotationEditor | `hooks/useAnnotationEditor.ts` | 标注编辑 |
| useKOSync | `hooks/useKOSync.ts` | Koreader 同步 |

## 关键依赖

- `foliate-js` - EPUB/PDF 渲染引擎
- `@tauri-apps/plugin-fs` - 文件系统
- `services/tts/*` - 语音合成服务
- `services/translators/*` - 翻译服务
- `services/ai/*` - AI 对话服务

## 数据模型

### 阅读进度
```typescript
interface ReadingProgress {
  bookId: string;
  cfi: string; // EPUB CFI 位置
  percentage: number;
  page?: number;
  scrollTop?: number;
}
```

### 标注
```typescript
interface Annotation {
  id: string;
  bookId: string;
  type: 'highlight' | 'note' | 'bookmark';
  cfiRange?: string;
  text?: string;
  note?: string;
  color?: string;
  createdAt: number;
}
```

## 测试与质量

- **测试框架**: Vitest
- **覆盖范围**: 组件渲染、状态管理、工具函数

## 常见问题 (FAQ)

### 如何使用 TTS 语音阅读？
1. 点击底部栏 TTS 图标
2. 选择语音和语速
3. 开始/暂停朗读

### 如何添加标注？
1. 长按或选择文本
2. 弹出标注工具栏
3. 选择高亮颜色或添加笔记

## 相关文件清单

- `store/readerStore.ts` - 阅读器状态
- `store/bookDataStore.ts` - 书籍数据
- `store/notebookStore.ts` - 笔记本状态
- `services/rsvp/` - RSVP 速读服务
- `services/transformers/` - 文本转换服务

## 变更记录

### 2026-02-21 - 模块文档创建
- 创建阅读器模块 CLAUDE.md
- 记录核心组件、Hooks、功能模块
