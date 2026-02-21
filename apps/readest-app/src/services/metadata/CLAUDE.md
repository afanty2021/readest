# 元数据服务目录

> 导航: [readest](../CLAUDE.md) > services > metadata

## 目录结构

```
src/services/metadata/
├── types.ts              # 类型定义
├── service.ts            # MetadataService 主服务类
└── providers/
    ├── base.ts           # BaseMetadataProvider 抽象基类
    ├── googlebooks.ts    # Google Books 提供商
    ├── openlibrary.ts    # Open Library 提供商
    └── index.ts          # 导出入口
```

## 支持的元数据提供商

### Open Library (默认)
- **API**: `https://openlibrary.org`
- **特点**: 免费，无需 API 密钥
- **置信度加成**: 0

### Google Books (可选)
- **API**: `https://www.googleapis.com/books/v1`
- **配置**: 需要 `GOOGLE_BOOKS_API_KEYS` 环境变量
- **特性**: 多 API key 轮换避免限流
- **置信度加成**: +10

## 数据类型

### Metadata
```typescript
interface Metadata {
  title: string;
  subtitle?: string;
  author: string;
  publisher?: string;
  published?: string;
  language?: string;
  identifier?: string;     // ISBN
  subjects?: string[];
  description?: string;
  coverImageUrl?: string;
}
```

### MetadataResult
```typescript
interface MetadataResult {
  metadata: Metadata;
  providerName: string;
  providerLabel: string;
  confidence: number;      // 0-100
}
```

## 置信度计算

基础分 50 分，根据匹配情况加分：

| 匹配类型 | 加分 |
|---------|------|
| ISBN 完全匹配 | +40 |
| 标题相似度 | 最高 +30 |
| 作者相似度 | 最高 +20 |
| 无封面图片 | -20 |
| Google Books 提供商 | +10 |

相似度使用 Levenshtein 距离算法计算。

## 封面图片处理

### Google Books 优先级
extraLarge > large > medium > small > thumbnail > smallThumbnail

### Open Library
`https://covers.openlibrary.org/b/id/{cover_i}-L.jpg`

## 与书架集成

### BookDetailModal
- 书籍详情弹窗，支持元数据查看和编辑

### useMetadataEdit Hook
```typescript
const {
  editedMeta,           // 编辑中的元数据
  fieldSources,         // 字段来源
  lockedFields,         // 锁定的字段
  handleAutoRetrieve,  // 自动获取元数据
  handleSourceSelection, // 选择元数据来源
} = useMetadataEdit(metadata);
```

### SourceSelector 组件
- 显示所有可用的元数据来源
- 显示置信度 (高>=90, 中>=70, 低<70)
