# 核心库目录

> 导航: [readest](../CLAUDE.md) > libs

## 目录结构

```
src/libs/
├── document.ts          # 文档加载与格式识别
├── edgeTTS.ts          # Edge TTS 语音合成
├── mediaSession.ts     # 媒体会话控制
├── metadata.ts         # 元数据搜索服务
├── storage.ts          # 云存储管理
├── sync.ts             # 数据同步
├── user.ts             # 用户管理
└── payment/            # 支付模块
    ├── stripe/
    │   ├── client.ts   # 前端 SDK
    │   └── server.ts   # 后端 API
    └── iap/
        ├── apple/
        ├── google/
        └── client.ts
```

## 核心模块

### document.ts
支持格式: EPUB, PDF, MOBI, AZW, AZW3, CBZ, FB2, FBZ, TXT, MD

### edgeTTS.ts
- 140+ 语言/地区语音
- WebSocket/HTTP 双协议
- LRU 缓存 (200条)

### mediaSession.ts
- 锁屏播放控制
- 系统通知栏

### storage.ts
- uploadFile / downloadFile / deleteFile
- Web 和 Tauri 平台适配

### sync.ts
- 增量同步 (books/configs/notes)

## 与 utils 关系

libs 依赖 utils 中的:
- `utils/fetch.ts` - 网络请求
- `utils/access.ts` - 认证
- `utils/supabase.ts` - 数据库
- `utils/lru.ts` - 缓存
