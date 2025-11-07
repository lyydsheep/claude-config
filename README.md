# Claude 配置管理器

这是一个用于管理 Claude AI 助手配置的命令行工具。该工具允许用户轻松修改 Claude 相关的配置文件，包括模型选择、API 基础 URL 和认证令牌等。

## 功能特性

- **模型切换**: 一键更新所有 ANTHROPIC_MODEL 相关配置
- **API URL 修改**: 快速更改 API 基础 URL 配置
- **令牌管理**: 安全更新认证令牌
- **配置查看**: 显示当前有效的环境配置
- **数据安全**: 所有修改操作前自动创建配置文件备份
- **注释支持**: 能够处理包含注释的 JSON 配置文件

## 目录结构

```
├── claude_config.sh  # 主要配置管理脚本
└── README.md         # 项目说明文档
```

## 安装说明

1. 克隆本仓库：
   ```bash
   git clone https://github.com/lyydsheep/claude-config.git
   cd claude-config
   ```

2. 确保脚本具有执行权限：
   ```bash
   chmod +x claude_config.sh
   ```

3. （可选）将脚本移动到系统路径以便全局使用：
   ```bash
   mv claude_config.sh /usr/local/bin/claude-config
   ```

## 使用方法

脚本默认管理位于 `$HOME/.claude/settings.json` 的配置文件。支持以下命令：

### 1. 显示帮助信息

```bash
./claude_config.sh help
```

### 2. 查看当前配置

```bash
./claude_config.sh show
```
显示当前配置文件中所有有效的环境配置（自动过滤注释行）。

### 3. 更新模型配置

```bash
./claude_config.sh model claude-3-opus-20240229
```
将所有以 ANTHROPIC_ 开头且包含 MODEL 的配置项更新为指定的值。

### 4. 更新 API 基础 URL

```bash
./claude_config.sh baseurl https://api.anthropic.com
```
更新 ANTHROPIC_BASE_URL 配置项。

### 5. 更新认证令牌

```bash
./claude_config.sh token sk-ant-XXXXXXXXXX
```
更新 ANTHROPIC_AUTH_TOKEN 配置项。

## 配置文件格式

脚本支持的配置文件为 JSON 格式，且包含注释行，例如：

```json
{
  "env": {
    # 这是一个注释行
    "ANTHROPIC_MODEL": "claude-3-opus-20240229",
    "ANTHROPIC_BASE_URL": "https://api.anthropic.com",
    "ANTHROPIC_AUTH_TOKEN": "sk-ant-XXXXXXXXXX"
  }
}
```

## 安全说明

- 所有修改操作都会自动创建配置文件的备份，备份文件包含时间戳和操作类型
- 备份文件保存在与原配置文件相同的目录中
- 在更新令牌时，脚本会显示令牌长度但不会显示完整令牌内容

## 依赖要求

- bash
- jq（用于处理 JSON 数据）

## 版本历史

- **版本 1.5**：最终版，支持所有基本功能