# 翻译服务目录

> 导航: [readest](../CLAUDE.md) > services > translators

## 目录结构

```
src/services/translators/
├── index.ts           # 主入口，导出类型和函数
├── types.ts           # TypeScript 类型定义
├── cache.ts           # 缓存实现（IndexedDB + 内存）
├── polish.ts          # 翻译后文本润色
├── preprocess.ts      # 翻译前文本预处理
├── utils.ts           # 工具函数（配额管理）
└── providers/        # 翻译提供商
    ├── index.ts       # 提供商注册与导出
    ├── deepl.ts      # DeepL 翻译服务
    ├── google.ts      # Google Translate
    ├── yandex.ts     # Yandex Translate
    └── azure.ts      # Azure Translator
```

## 支持的翻译提供商

| 提供商 | 认证要求 | 说明 |
|--------|----------|------|
| **DeepL** | 需要 API Token | 主要翻译服务，通过后端代理 |
| **Google Translate** | 不需要 | 免费服务，直接调用 |
| **Yandex Translate** | 不需要 | 通过 translate.toil.cc 代理 |
| **Azure Translator** | 不需要 | 免费服务，需要获取临时 Token |

### 每日翻译配额

| 用户计划 | 每日配额 |
|----------|----------|
| free | 10K 字符 |
| plus | 100K 字符 |
| pro | 500K 字符 |
| purchase | 无限制 |

## 核心接口

```typescript
export interface TranslationProvider {
  name: string;
  label: string;
  authRequired?: boolean;
  translate: (
    texts: string[],
    sourceLang: string,
    targetLang: string,
    token?: string | null,
    useCache?: boolean,
  ) => Promise<string[]>;
}
```

## 缓存策略

### 双层缓存架构
1. **内存缓存** - 快速访问
2. **IndexedDB 缓存** - 持久化存储

### 缓存管理
- 预加载：启动时加载最近 30 天内 10000 条缓存
- 自动清理：每 60 分钟执行一次
- 最大年龄：90 天
- 最大条目：100,000
- 最大大小：10 MB

## 文本预处理与润色

### 预处理 (preprocess.ts)
- 替换特殊占位符 (Cover, Dedication 等)

### 润色 (polish.ts)
- 中文：修复标点符号间距
- 西班牙语：修复问号/感叹号后空格
- 法语：修复标点符号间距
- 日语：修复标点符号间距

## 与阅读器集成

### 核心 Hook
- `useTranslator` - 通用翻译 Hook
- `useTextTranslation` - 阅读器翻译 Hook

### 翻译流程
1. IntersectionObserver 监听视口内文本节点
2. 懒加载翻译（预翻译后续2个元素）
3. 创建 `.translation-target` 元素注入翻译
4. 缓存检查和存储

### 翻译触发场景
- 滚动到新段落
- 切换翻译提供商/目标语言
- 启用/禁用翻译
- 阅读进度跳转
