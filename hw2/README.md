# 软工第二次作业-电商分析师



# Quick Start

不使用网关：

- 首先启动 [MCP-Tools](https://github.com/FZU-YOROZUYA/MCP-Tools/tree/mcp-server) 的 mcp-server 分支下

  使用 `docs/create_tables.sql` 先建好 SQL 表

- 接着启动 [MCP-Client](https://github.com/FZU-YOROZUYA/MCP-Client)

  - 启动 MCP-Client 时需要配置四个 API_KEY 到你的环境变量，分别为
    - ACCESS_KEY_ID：你的阿里云 OSS 的 KEY
    - ACCESS_KEY_SECRET：你的阿里云 OSS 的 SECRET
    - API_KEY_DEEPSEEK：DEEPSEEK 的 API_KEY
    - API_KEY_QWEN：千问的 API_KEY

- 最后进入 **[MCP-Frontend](https://github.com/FZU-YOROZUYA/MCP-Frontend)** 仓库按照要求启动前端服务
  - 运行 `npm install`
  - 运行 `npm run dev`

 

最后访问 127.0.0.1:5175 即可访问



使用网关：

修改 MCP-Client 项目下的 `package com.example.mcp_client_demo.common.McpCaller` 文件，替换

```java
private static final McpTransport transport = new HttpMcpTransport.Builder()
    .sseUrl("http://localhost:8087/sse")
    .logRequests(true)
    .logResponses(true)
    .build();
```

为

```java
private static final McpTransport transport = new HttpMcpTransport.Builder()
        .sseUrl("http://localhost:9195/api/product/sse")
        .logRequests(true)
        .logResponses(true)
        .build();
```



进入[MCP-Server](https://github.com/FZU-YOROZUYA/Mcp-Server) 下，按照要求修改目前 2.7.0.2 Shenyu 目前存在的 MCP 的 BUG，按照要求启动

- shenyu-admin
- shenyu-bootstrap

然后可以登录 127.0.0.1:9195 配置你的 MCP-Tools

最后同上，启动其他的 MCP 服务



