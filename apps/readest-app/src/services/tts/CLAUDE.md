# TTS 服务目录

> 导航: [readest](../CLAUDE.md) > services > tts

## 目录结构

```
src/services/tts/
├── index.ts              # 导出入口
├── types.ts              # 类型定义
├── TTSClient.ts          # TTS 客户端接口
├── TTSController.ts      # TTS 控制器（核心）
├── TTSData.ts            # 静态数据（黑名单、静音数据）
├── TTSUtils.ts           # 工具函数
├── EdgeTTSClient.ts      # Edge TTS 实现
├── WebSpeechClient.ts    # Web Speech API 实现
└── NativeTTSClient.ts   # Native TTS 实现（Android）
```

## 支持的 TTS 引擎

### Edge TTS
- 使用微软 Edge Speech API
- 支持 140+ 语言
- 特性: 音频预加载、LRU 缓存、Safari/iOS 淡出补偿
- 自动回退机制 (wss -> https)

### Web Speech API
- 使用浏览器原生 `window.speechSynthesis`
- 支持所有现代浏览器
- 黑名单过滤奇怪音效语音

### Native TTS
- 使用 Tauri 插件 `native-tts`
- 仅支持 Android
- 支持多种 TTS 引擎 (System, Microsoft, ByteDance, Xiaomi, Azure, Google, Gemini 等)

## 音频控制

```typescript
// 播放控制
- play(): 播放音频
- pause(): 暂停并记录位置
- resume(): 恢复播放
- stop(): 停止并重置
```

### 预加载机制
- 预加载前2个标记
- LRU 缓存 (200条)

## 语音配置

| 参数 | Edge TTS | Web Speech | Native TTS |
|------|----------|------------|------------|
| Rate | 0.5-2.0 | 0.1-10 | 幂运算转换 |
| Pitch | 0.5-1.5 | 0-2 | 自定义 |

## 与阅读器集成

### TTSController 核心类
```typescript
class TTSController extends EventTarget {
  state: 'stopped' | 'playing' | 'paused' | ...
  async init()
  async speak(ssml, oneTime, oneTimeCallback)
  async play(), pause(), resume(), stop()
  async backward(byMark), forward(byMark)
}
```

### React Hook
`app/reader/hooks/useTTSControl.ts` - TTS React Hook

### UI 组件
| 组件 | 职责 |
|------|------|
| TTSControl.tsx | 控制入口、弹出面板定位 |
| TTSPanel.tsx | 设置面板 (语音、语速、超时) |
| TTSIcon.tsx | TTS 图标 |
| TTSBar.tsx | 底部 TTS 控制栏 |

## 特色功能

- SSML 预处理
- 多语言支持
- 朗读目标语言 (源语言/翻译语言)
- 阅读进度跟踪 (CFI)
- 后台播放 (iOS)
- 媒体会话 (锁屏控件)
