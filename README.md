# MCP Client + MCP Server 示例项目

本项目展示了如何构建并使用 MCP（Model-Computer Protocol）体系中的 `MCP Client` 与 `MCP Server`，实现从用户提问，到调用工具/服务，再到大模型给出最终答复的完整流程。

## 📁 项目结构

```bash
.
├── .env                          # 环境变量配置文件
├── calculatorMCPServer.py       # 本地 MCP Server 示例：计算器服务
├── calculatorMCPServerTest.py   # 测试 calculatorMCPServer.py 的可用性
├── amapMCPServerTest.py         # 测试高德官方 MCP Server 是否可访问
├── clientChatTest.py            # 主程序，模拟用户问答过程、工具调用和大模型输出
├── servers_config.json          # MCP Server 配置，包括本地与远程服务
├── output.txt                   # 所有工具的描述信息
└── README.md                    # 项目说明文件
```
# 🧠 功能概述
本项目实现以下功能：
1. 搭建本地 MCP Server（如计算器服务）
2. 测试本地/远程 MCP Server 是否连接正常
3. 实现 MCP Client 连接多个 MCP Server 的完整调用流程
4. 用户输入问题 → 自动选择合适工具（MCP Server）→ 返回大模型回答

# 📦 使用说明
1. 环境配置
请在 .env 文件中配置必要的环境变量

2. 运行 MCP Client 主流程
python clientChatTest.py
你将看到以下完整过程：
用户输入一个问题
系统解析调用哪些 MCP Server 工具
通过 servers_config.json 找到目标服务
工具返回结果后由大模型进行融合、总结

# ⚙️ 配置说明
servers_config.json
用于配置 MCP Client 可访问的所有 MCP Server，例如：

json
复制
编辑
{
  "calculator": {
    "command": "python",
    "args": ["calculatorMCPServer.py"],
    "env": {}
  },
  "amap-maps": {
    "command": "npx",
    "args": ["-y", "@amap/amap-maps-mcp-server"],
    "env": {
      "AMAP_MAPS_API_KEY": "${AMAP_MAPS_API_KEY}"
    }
  }
}

# 📝 注意事项
请确保所有 Server 配置项对应可执行命令或服务地址。

.env 中的变量可通过 servers_config.json 中的 ${VAR_NAME} 动态注入。

MCP Client 和 Server 均可本地或远程运行，确保网络可访问。

# 📚 参考
MCP 官方协议说明文档
高德地图 MCP Server：@amap/amap-maps-mcp-server

# 欢迎贡献和交流！

