# 工具函数目录

> 导航: [readest](../CLAUDE.md) > utils

## 目录结构

```
src/utils/
├── debounce.ts          # 防抖函数
├── throttle.ts          # 节流函数
├── lru.ts               # LRU 缓存
├── fetch.ts             # HTTP 请求封装
├── lang.ts              # 语言检测与处理
├── simplecc.ts          # 简繁转换 (WASM)
├── book.ts              # 书籍元数据工具
├── cfi.ts               # CFI 解析与处理
├── ttsTime.ts           # TTS 时间估算
├── note.ts              # 笔记模板渲染
├── style.ts             # CSS 样式转换
├── supabase.ts          # Supabase 客户端
├── access.ts            # 认证与授权
├── storage.ts           # 存储类型定义
├── os.ts                # 系统检测
├── path.ts              # 路径处理
├── file.ts              # 文件操作
└── ...
```

## 核心工具

| 工具 | 功能 |
|------|------|
| debounce/throttle | 函数控制 |
| lru | LRU 缓存实现 |
| fetch | 超时请求封装 |
| lang | 语言检测、CJK 判断 |
| simplecc | 简繁转换 (需先 init) |
| book | 作者/标题格式化 |
| cfi | EPUB CFI 定位 |
| ttsTime | 估算剩余阅读时间 |
| note | Nunjucks 模板渲染 |

## 使用示例

```typescript
import { debounce, throttle } from '@/utils/debounce';
import { detectLanguage } from '@/utils/lang';
import { formatAuthors } from '@/utils/book';

const lang = detectLanguage('中文文本');
const authors = formatAuthors(contributors);
```
