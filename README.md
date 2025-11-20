# Claude配置切换工具 (ccs-jiang)

一个用于在不同的Claude API配置之间进行切换的命令行工具。

**支持 Windows / macOS / Linux 跨平台使用**

> 基于 [claude-config-switch](https://github.com/canglong/claude-code-switch) 修改，增加了 Windows 系统兼容性支持。

## 安装

```bash
npm i -g ccs-jiang
```

npm 包地址：https://www.npmjs.com/package/ccs-jiang

### 依赖项

- Node.js (>= 12.0.0)
- npm (>= 6.0.0)

## 使用方法

### 配置文件

工具需要配置文件，位于 `~/.claude/` 目录下：

#### 1. apiConfigs.json - API配置列表

存储所有可用的Claude API配置，格式如下：

```json
[
  {
    "name": "config-1",
    "config": {
      "env": {
        "ANTHROPIC_AUTH_TOKEN": "sk-XXXXXXX",
        "ANTHROPIC_BASE_URL": "https://api.example.com",
        "CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC": "1"
      },
      "permissions": {
        "allow": [],
        "deny": []
      },
      "model": "claude-sonnet-4-20250514"
    }
  }
]
```

#### 2. settings.json - 当前激活配置

存储当前使用的配置，切换配置时会自动更新此文件。

### 命令

#### 列出所有配置并选择切换

```bash
ccs list
# 或使用简写
ccs ls
```

使用键盘上下箭头选择配置，按 Enter 确认切换。

#### 打开配置文件

```bash
# 打开API配置文件 (apiConfigs.json)
ccs o api

# 打开设置配置文件 (settings.json)
ccs o setting
```

如果文件不存在，会自动创建包含示例内容的配置文件。

#### 健康检查

```bash
ccs health
```

检查所有配置的API端点可用性和网络延迟。

#### 企微通知

```bash
# 设置企微机器人
ccs notify setup

# 查看通知状态
ccs notify status

# 测试通知
ccs notify test
```

#### 显示帮助

```bash
ccs --help
```

## Windows 兼容性修复

此版本修复了原版在 Windows 系统上的以下问题：

1. **文件打开命令**：使用跨平台方案
   - Windows: `cmd /c start`
   - macOS: `open`
   - Linux: `xdg-open`

2. **Claude CLI 启动**：添加 `shell: true` 支持 Windows 正确找到 npm 全局命令

## 更新日志

### 1.0.0 (ccs-jiang)

- 基于 claude-config-switch 1.7.0
- 添加 Windows 系统兼容性支持
- 修复 `ccs o api/setting` 在 Windows 上无法打开文件的问题
- 修复切换配置后启动 Claude CLI 失败的问题

## 致谢

- 原项目：[claude-config-switch](https://github.com/canglong/claude-code-switch) by canglong

## License

MIT
