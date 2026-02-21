# 文本转换器目录

> 导航: [readest](../CLAUDE.md) > services > transformers

## 目录结构

```
src/services/transformers/
├── index.ts           # 转换器导出入口
├── types.ts           # Transformer 接口定义
├── footnote.ts        # EPUB 脚注转换
├── language.ts        # 语言检测与 HTML lang 设置
├── punctuation.ts     # 标点符号转换（简繁竖排）
├── sanitizer.ts       # HTML 清理与安全处理
├── simplecc.ts        # 简繁中文转换
├── style.ts           # CSS 样式转换
├── whitespace.ts      # 空白字符处理
└── proofread.ts       # 文本校对规则引擎
```

## 转换器列表

| 转换器 | 功能 |
|--------|------|
| punctuationTransformer | 标点符号简繁/竖排转换 |
| footnoteTransformer | EPUB 脚注标准化 |
| languageTransformer | 语言检测与 lang 属性 |
| styleTransformer | CSS 响应式布局转换 |
| whitespaceTransformer | 空白字符规范化 |
| sanitizerTransformer | HTML XSS 清理 |
| simpleccTransformer | 简繁中文转换 |
| proofreadTransformer | 文本校对规则 |

## simpleccTransformer (简繁转换)

支持转换类型：
- `s2t` / `t2s` - 简体 ↔ 繁体
- `s2h` / `s2hk` / `s2tw` / `s2twp` - 简体 → 各地繁体
- `tw2s` / `hk2s` - 各地繁体 → 简体

## punctuationTransformer (标点转换)

- 简繁标点互换 (`"` ↔ `"`)
- 竖排标点转换

## proofreadTransformer (校对规则)

```typescript
interface ProofreadRule {
  scope: 'selection' | 'book' | 'library';
  pattern: string;
  replacement: string;
  isRegex: boolean;
  onlyForTTS?: boolean;
}
```

支持三种作用域：选区、书籍、全局

## sanitizerTransformer (安全清理)

- 使用 DOMPurify 清理 HTML
- 禁止 `<script>` 标签
- 白名单 URI 协议

## 转换流水线

```typescript
const transformed = await transformContent(ctx);
// 按配置顺序依次执行转换器
// 单个失败不影响其他
```

## 与阅读器集成

- `transformService.ts` - 通用转换入口
- `useTTSControl.ts` - TTS 文本预处理（调用 proofreadTransformer）
