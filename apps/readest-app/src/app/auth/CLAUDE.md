# 认证模块 (Auth)

> 更新时间：2026-02-21 15:08:21

## 相对路径面包屑

`[根目录](../../../../CLAUDE.md) > [apps/readest-app](../) > **auth**

## 模块职责

处理用户认证和授权，支持多种认证方式：Supabase 邮箱登录、Apple Sign In、Google 登录。

## 入口与启动

- **页面入口**: `apps/readest-app/src/app/auth/page.tsx`
- **回调页面**: `app/auth/callback/page.tsx`

## 对外接口

### 页面路由
- `/auth` - 认证首页
- `/auth/callback` - 认证回调处理
- `/auth/recovery` - 密码恢复
- `/auth/update` - 账户更新

### 核心功能
- Supabase 邮箱/密码登录
- Apple Sign In (Tauri 原生 + Web)
- Google 登录
- OAuth 流程处理

### 工具函数
- `appleIdAuth.ts` - Apple ID 认证工具
- `nativeAuth.ts` - 原生认证工具

## 关键依赖

- `@supabase/supabase-js` - Supabase 认证
- `@tauri-apps/plugin-oauth` - OAuth 支持
- `@tauri-apps/plugin-shell` - Apple 认证
- `tauri-plugin-sign-in-with-apple` - Apple 登录

## 变更记录

### 2026-02-21 - 模块文档创建
- 创建认证模块 CLAUDE.md
