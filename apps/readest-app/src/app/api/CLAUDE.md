# API 路由目录

> 导航: [readest](../CLAUDE.md) > app > api

## 目录结构

```
src/app/api/
├── ai/
│   ├── chat/route.ts       # AI 对话流式响应
│   └── embed/route.ts      # 嵌入向量生成
├── apple/iap-verify/route.ts   # Apple IAP 验证
├── google/iap-verify/route.ts  # Google IAP 验证
├── metadata/search/route.ts    # 图书元数据搜索
├── opds/proxy/route.ts         # OPDS 订阅源代理
├── stripe/
│   ├── plans/route.ts      # 订阅计划列表
│   ├── checkout/route.ts  # Stripe 结账会话
│   ├── check/route.ts     # 结账状态检查
│   ├── portal/route.ts    # 客户门户
│   └── webhook/route.ts   # Webhook 处理
└── tts/edge/route.ts      # Edge TTS 语音合成
```

## API 端点

| 端点 | 功能 | 认证 |
|------|------|------|
| `/api/ai/chat` | AI 对话流式响应 | Bearer |
| `/api/ai/embed` | 嵌入向量生成 | Bearer |
| `/api/metadata/search` | 元数据搜索 | Bearer |
| `/api/opds/proxy` | OPDS 代理 | Bearer |
| `/api/stripe/plans` | 订阅计划 | 公开 |
| `/api/stripe/checkout` | 创建结账 | Bearer |
| `/api/tts/edge` | TTS 语音合成 | Bearer |
| `/api/apple/iap-verify` | Apple IAP | Bearer |
| `/api/google/iap-verify` | Google IAP | Bearer |

## 认证机制

统一使用 Supabase JWT Token:
```typescript
const { user, token } = await validateUserAndToken(authHeader);
```

## 遗留 Pages API

| 路径 | 功能 |
|------|------|
| `/api/deepl/translate` | DeepL 翻译代理 |
| `/api/storage/*` | 文件存储操作 |
| `/api/sync` | 数据同步 |
| `/api/kosync` | KOReader 同步 |
