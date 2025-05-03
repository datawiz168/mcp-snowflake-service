[![MseeP.ai Security Assessment Badge](https://mseep.net/pr/datawiz168-mcp-snowflake-service-badge.png)](https://mseep.ai/app/datawiz168-mcp-snowflake-service)

A Model Context Protocol (MCP) server that provides Claude access to Snowflake databases. / 一个为 Claude 提供 Snowflake 数据库访问能力的 MCP (模型上下文协议) 服务器。

![GitHub Stars](https://img.shields.io/github/stars/datawiz168/mcp-snowflake-service?style=social)
[![Smithery Badge](https://smithery.ai/badge/@datawiz168/mcp-service-snowflake)](https://smithery.ai/server/@datawiz168/mcp-service-snowflake)

This server implements the Model Context Protocol to allow Claude to:
- Execute SQL queries on Snowflake databases
- Automatically handle database connection lifecycle (connect, reconnect on timeout, close)
- Handle query results and errors
- Perform database operations safely

此服务器实现了模型上下文协议，使 Claude 能够：
- 在 Snowflake 数据库上执行 SQL 查询
- 自动管理数据库连接生命周期（连接创建、超时重连、连接关闭）
- 处理查询结果和错误
- 安全地执行数据库操作

## Installation / 安装

### Installing via Smithery

To install mcp-service-snowflake for Claude Desktop automatically via [Smithery](https://smithery.ai/server/@datawiz168/mcp-service-snowflake):

```bash
npx -y @smithery/cli install @datawiz168/mcp-service-snowflake --client claude
```

### Manual Installation
1. Clone this repository / 克隆此仓库
```bash
git clone https://github.com/datawiz168/mcp-snowflake-service.git
```

2. Install dependencies / 安装依赖
```bash
pip install -r requirements.txt
```

## Configuration / 配置说明

### MCP Client Configuration Example / MCP 客户端配置示例

Add the following configuration to `claude_desktop_config.json` / 在 `claude_desktop_config.json` 中添加配置:

```json
{
  "mcpServers": {
    "snowflake": {
      "command": "C:\\Users\\K\\anaconda3\\envs\\regular310\\python.exe",
      "args": ["D:\\tools\\mcp-snowflake\\server.py"]
    }
  }
}
```

Configuration parameters / 配置参数说明:
- `command`: Full path to your Python interpreter. Please modify this according to your Python installation location. / Python 解释器的完整路径，请根据您的 Python 安装位置进行修改。
- `args`: Full path to the server script. Please modify this according to where you cloned the repository. / 服务器脚本的完整路径，请根据您克隆仓库的位置进行修改。

Example paths for different operating systems / 不同操作系统的路径示例:

Windows:
```json
{
  "mcpServers": {
    "snowflake": {
      "command": "C:\\Users\\YourUsername\\anaconda3\\python.exe",
      "args": ["C:\\Path\\To\\mcp-snowflake\\server.py"]
    }
  }
}
```

MacOS/Linux:
```json
{
  "mcpServers": {
    "snowflake": {
      "command": "/usr/bin/python3",
      "args": ["/path/to/mcp-snowflake/server.py"]
    }
  }
}
```

### Snowflake Configuration / Snowflake 配置

Create a `.env` file in the project root directory and add the following configuration / 在项目根目录下创建 `.env` 文件，添加以下配置：

```env
SNOWFLAKE_USER=your_username      # Your username / 您的用户名
SNOWFLAKE_PASSWORD=your_password  # Your password / 您的密码
SNOWFLAKE_ACCOUNT=NRB18479.US-WEST-2    # Example: NRB18479.US-WEST-2 / 示例: NRB18479.US-WEST-2
SNOWFLAKE_DATABASE=your_database  # Your database / 您的数据库
SNOWFLAKE_WAREHOUSE=your_warehouse # Your warehouse / 您的数据仓库
```

## Connection Management / 连接管理

The server provides automatic connection management features / 服务器提供以下自动连接管理功能：

- Automatic connection initialization / 自动初始化连接
  - Creates connection when first query is received / 首次查询时自动创建连接
  - Validates connection parameters / 验证连接参数

- Connection maintenance / 连接维护
  - Keeps track of connection state / 跟踪连接状态
  - Handles connection timeouts / 处理连接超时
  - Automatically reconnects if connection is lost / 连接断开时自动重连

- Connection cleanup / 连接清理
  - Properly closes connections when server stops / 服务器停止时正确关闭连接
  - Releases resources appropriately / 适当释放资源

## Usage / 使用说明

The server will start automatically with the Claude Desktop client. No manual startup is required. Once the server is running, Claude will be able to execute Snowflake queries. / 服务器会随 Claude Desktop 客户端自动启动，无需手动运行。服务器启动后，Claude 将能够执行 Snowflake 查询。

For development testing, you can start the server manually using / 如果需要单独启动服务器进行测试，可以使用以下命令:

```bash
python server.py
```

Note: Manual server startup is not needed for normal use. The Claude Desktop client will automatically manage server startup and shutdown based on the configuration. / 注意：正常使用时无需手动启动服务器，Claude Desktop 客户端会根据配置自动管理服务器的启动和停止。

## Features / 功能

- Secure Snowflake database access / 安全的 Snowflake 数据库访问
- Robust error handling and reporting / 健壮的错误处理和报告机制
- Automatic connection management / 自动连接管理
- Query execution and result processing / 查询执行和结果处理

## Development / 开发

To contribute code or report issues / 要贡献代码或报告问题，请:

1. Fork this repository / Fork 此仓库
2. Create your feature branch / 创建您的功能分支 (`git checkout -b feature/AmazingFeature`)
3. Commit your changes / 提交您的更改 (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch / 推送到分支 (`git push origin feature/AmazingFeature`)
5. Open a Pull Request / 开启一个 Pull Request

## notes / 备注
mcp‑server‑snowflake controls database access rights precisely by way of database users. If you only need to read data, just assign a user with read‑only database permissions./
mcp-server-snowflake 控制数据库访问权限，是通过数据库用户来精准实现的。如果你只想读取数据，给个只有读取数据库权限的用户就行了。

## License / 许可
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This project is licensed under the [MIT License](LICENSE).

此项目采用 [MIT 许可证](LICENSE)。
