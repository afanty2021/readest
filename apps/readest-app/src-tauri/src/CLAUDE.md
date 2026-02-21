# Rust 后端核心

> 导航: [readest](../CLAUDE.md) > src-tauri > src

## 目录结构

```
src-tauri/src/
├── main.rs                    # 应用入口点
├── lib.rs                     # 主库文件，Tauri 应用构建
├── dir_scanner.rs             # 目录扫描模块
├── transfer_file.rs           # 文件传输模块（下载/上传）
├── discord_rpc.rs             # Discord Rich Presence 集成
├── macos/                     # macOS 平台特定模块
│   ├── mod.rs
│   ├── menu.rs                # 菜单栏配置
│   ├── traffic_light.rs       # 窗口红绿灯按钮控制
│   ├── safari_auth.rs         # Safari 认证
│   └── apple_auth.rs          # Apple Sign-In
├── windows/                   # Windows 平台特定模块
│   └── mod.rs
├── android/                   # Android 平台特定模块
│   ├── mod.rs
│   └── eink.rs                # E-ink 设备检测
└── plugins/                   # Tauri 插件
    ├── tauri-plugin-native-bridge/
    └── tauri-plugin-native-tts/
```

## Tauri Commands

### dir_scanner.rs
| 命令 | 功能 |
|------|------|
| `read_dir` | 递归/非递归扫描目录，支持文件扩展名过滤 |

### transfer_file.rs
| 命令 | 功能 |
|------|------|
| `download_file` | HTTP 下载，支持多线程分片下载和进度回调 |
| `upload_file` | HTTP 上传文件，支持 POST/PUT 方法 |

### discord_rpc.rs
| 命令 | 功能 |
|------|------|
| `update_book_presence` | 更新阅读状态到 Discord |
| `clear_book_presence` | 清除 Discord 状态 |

### macos 模块
- `safari_auth::auth_with_safari` - Safari OAuth 认证
- `apple_auth::start_apple_sign_in` - Apple Sign-In
- `traffic_light::set_traffic_lights` - 窗口红绿灯控制

## 与前端通信

1. **Tauri Commands** - `#[tauri::command]` 宏暴露 Rust 函数
2. **事件发射** - `window.emit()` 向前端发送事件
3. **Channel** - 服务端推送进度
4. **State 管理** - `tauri::State` 共享状态

## 平台特定功能

### macOS
- 窗口红绿灯按钮自定义
- Apple Sign-In
- Safari OAuth 认证

### Windows
- 窗口阴影和装饰控制
- Deep Link (`readest://` 协议)

### Android
- E-ink 设备检测 (BOOX, Kindle, Kobo, reMarkable)
- 后台音频
- 屏幕方向锁定

### iOS
- Apple Sign-In
- 触觉反馈

## 关键依赖

- **tauri** 2.x
- **tokio** - 异步运行时
- **reqwest** - HTTP 客户端
- **cocoa/objc/objc2** - macOS 互操作
- **discord-rich-presence** - Discord RPC
