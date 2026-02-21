# 同步服务目录

> 导航: [readest](../CLAUDE.md) > services > sync

## 同步系统概览

Readest 支持两种同步协议：

| 协议 | 客户端 | 用途 |
|------|--------|------|
| **KOReader Sync** | `KOSyncClient.ts` | 与 KOReader 阅读器同步 |
| **Cloud Sync** | `libs/sync.ts` | Readest 自有云同步 |

## KOReader Sync

### 目录位置
```
src/services/sync/
└── KOSyncClient.ts        # KOReader Sync 客户端
```

### API 端点
```
GET  /users/auth           # 用户认证
POST /users/create         # 用户注册
GET  /syncs/progress/{hash} # 获取阅读进度
PUT  /syncs/progress      # 更新阅读进度
```

### 认证机制
- `X-Auth-User`: 用户名
- `X-Auth-Key`: MD5 密码哈希
- 媒体类型: `application/vnd.koreader.v1+json`

### 同步策略
| 策略 | 代码 | 说明 |
|------|------|------|
| 提示 | `prompt` | 冲突时弹出对话框选择 |
| 静默 | `silent` | 远程较新则自动接收 |
| 发送 | `send` | 只推送，不接收 |
| 接收 | `receive` | 只接收，不推送 |

### 冲突解决
- 冲突阈值: `0.0001` (0.01%)
- 比较阅读进度的百分比差异

## Cloud Sync (Supabase)

### 目录位置
```
src/libs/sync.ts           # 云同步客户端
src/pages/api/sync.ts      # API 路由
```

### 数据类型
- `books` - 书籍信息
- `configs` - 书籍配置
- `notes` - 书籍笔记

### 冲突解决
- Last-Writer-Wins 策略
- 基于时间戳比较 (`clientDeletedAt`, `clientUpdatedAt`)

## 数据模型

### KoSyncProgress
```typescript
interface KoSyncProgress {
  document?: string;      // 文档哈希
  progress?: string;     // 进度位置 (CFI/XPointer)
  percentage?: number;   // 完成百分比 (0-1)
  timestamp?: number;    // 更新时间戳
  device?: string;       // 设备名称
}
```

## 相关 Hooks

| Hook | 职责 |
|------|------|
| useKOSync | KOReader 同步核心逻辑 |
| useProgressSync | 阅读进度同步 |
