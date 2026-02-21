# AI 服务目录

> 导航: [readest](../CLAUDE.md) > services > ai

## 目录结构

```
src/services/ai/
├── index.ts                      # 导出入口，公共 API
├── types.ts                      # 类型定义（AIProvider, AISettings, TextChunk 等）
├── constants.ts                  # 常量定义（默认配置、模型定价）
├── logger.ts                     # 日志系统（分模块的调试日志）
├── prompts.ts                    # 系统提示词构建（buildSystemPrompt）
├── ragService.ts                 # RAG 服务（书籍索引、混合搜索）
├── providers/
│   ├── index.ts                  # Provider 工厂函数 getAIProvider()
│   ├── OllamaProvider.ts         # Ollama 本地模型支持
│   ├── AIGatewayProvider.ts      # AI Gateway 云端模型支持
│   └── ProxiedGatewayEmbedding.ts # 浏览器端代理嵌入模型
├── adapters/
│   ├── index.ts                  # 适配器导出
│   └── TauriChatAdapter.ts       # Tauri 聊天适配器（流式响应）
├── storage/
│   └── aiStore.ts                # IndexedDB 存储（向量块、BM25、对话历史）
└── utils/
    ├── chunker.ts                # 文本分块工具（智能段落切分）
    └── retry.ts                  # 重试与超时工具
```

## 支持的 AI 提供商

### Ollama (本地)
- **默认模型**: `llama3.2` (对话), `nomic-embed-text` (嵌入)
- **特点**: 无需认证，完全本地运行
- **健康检查**: 通过 `/api/tags` 检测模型是否存在

### AI Gateway (云端)
- **支持模型**:
  - `google/gemini-2.5-flash-lite`
  - `openai/gpt-5-nano`
  - `meta/llama-4-scout`
  - `xai/grok-4.1-fast-reasoning`
  - `deepseek/deepseek-v3.2`
  - `alibaba/qwen-3-235b`
- **默认嵌入模型**: `openai/text-embedding-3-small`

## Provider 接口

```typescript
export interface AIProvider {
  id: AIProviderName;
  name: string;
  requiresAuth: boolean;
  getModel(): LanguageModel;
  getEmbeddingModel(): EmbeddingModel;
  isAvailable(): Promise<boolean>;
  healthCheck(): Promise<boolean>;
}
```

## RAG 系统

### 索引流程
1. **分块**: 智能文本切分（最大 500 字符，含重叠）
2. **嵌入**: 批量生成向量嵌入
3. **存储**: 向量存储于 IndexedDB，BM25 索引用于全文搜索

### 混合搜索
- 向量搜索: 余弦相似度
- BM25 搜索: 全文关键词匹配
- 融合策略: 加权合并（向量权重 1.0, BM25 权重 0.8）

### 剧透保护
- `spoilerProtection: true` 时，搜索结果限制在当前页之前的内容

## 流式响应

两种流式路径：
1. **AI Gateway 模式**: 通过 `/api/ai/chat` API 路由代理
2. **Ollama 模式**: 直接使用 Vercel AI SDK 的 `streamText()`

## 超时配置

| 操作 | 超时 |
|------|------|
| 单次嵌入 | 30s |
| 批量嵌入 | 2min |
| 聊天响应 | 60s |
| 健康检查 | 5s |
