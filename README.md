# 我们不需要臃肿的清理软件！

# C Drive Cleaner neo

Win11 风格 C 盘清理工具 —— 基于 [C Drive Cleaner](https://github.com/ALingStudio/C-Drive-Cleaner) v2.9 从底层全面重构的 neo 架构版本。

## 特性

- **Win11 Fluent 风格 GUI**：原生 WebView2 渲染，不捆绑 Chromium，单文件便携 EXE 约 9 MB，秒开
- **清理逻辑零改动**：原版 v2.9 脚本原样内置，全部清理命令运行时逐字取出执行（SHA-256 校验一致）
- **neo 高速引擎**：大文件查找采用原生 Go 多线程并发扫描 + 实时进度条，替代旧版 PowerShell 方案
- **16 国语言**：界面多语言，自动跟随系统语言，可手动切换
- **开箱即用**：启动自动检测 C 盘剩余空间，全局日志默认开启（`C:\Log\CleanLog.txt`）

## 下载

从 [Releases](https://github.com/ALingStudio/C-Drive-Cleaner-Neo/releases) 获取最新版：

- `C-Drive-Cleaner-neo-*-Win64.exe` —— 主程序（右键"以管理员身份运行"）
- `*-with-source.zip` —— 主程序 + 完整源代码

> EXE 未做代码签名，若 SmartScreen 提示"未知发布者"，点击"更多信息 → 仍要运行"。

## 构建

依赖：Go 1.22+、[Wails CLI](https://wails.io) v2.9.2、mingw-w64（Linux 交叉编译时需要）

```bash
wails build -platform windows/amd64 -o C-Drive-Cleaner-neo-1.0-Win64.exe
```

产物位于 `build/bin/`。

## 目录结构

```
├── main.go / app.go          # Wails 入口与后端逻辑
├── hide_windows.go           # Windows 窗口隐藏
├── internal/
│   ├── batparse/             # 原版 bat 解析器（含测试）
│   ├── runner/               # 工作脚本生成器（命令逐字取自原版）
│   └── scan/                 # neo 高速大文件扫描器（含测试）
├── frontend/                 # 界面（HTML/CSS/JS + 16 语言包 i18n.js）
├── resources/                # 内置原版 bat（未修改）
└── build/windows/            # EXE 清单（requireAdministrator）与图标
```

## 许可证

MIT（与原版一致）。原版版权归 ALing 所有。
