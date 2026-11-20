# Memory Plugin

由 gen-mcp-bridge.mjs 从 http://127.0.0.1:1933/mcp 的 tools/list 直接生成。

- 工具数：2（服务端共 2）
- 覆盖端点：`http://127.0.0.1:1933/mcp`

## 凭据配置（首次使用必读）

这个插件本身**不携带**访问凭据，需要在运行 AGH 的环境里配置环境变量：

```
MCP_API_KEY=<你的 key>
```

key 获取方式（摘自原插件文档）：`skillCatalog` (default `true`) and `skillCatalogTokenBudget` (default `1200`; `0` also turns the catalog off) govern `<available-skills>`. The catalog comes from one `GET /api/v1/skills?node_limit=200` call: the user's own skills first, then those shared under `viking://agent/skills` minus any whose name the user also owns, each description cut to about 40 tokens. Its budget is separate from `profileTokenBudget`. When the descriptions do not fit, the catalog lists names only (with a `... +N more` tail if even the names do not all fit); when not even one name fits, it shrinks to a one-line count; with no skills, or a server without the endpoint, it is omitted.

配置后重启 AGH 或重新加载插件即可生效。未配置时工具调用会报
`MCP_API_KEY is not configured` 或 `401 Sign-in required` ——
这属于运行环境未就绪，不是插件缺陷。

重新生成：`node gen-mcp-bridge.mjs --endpoint http://127.0.0.1:1933/mcp --key-env MCP_API_KEY --prefix memory_plugin_dcbaba0a --out /home/node/agh-artifacts/agh-memory-plugin-dcbaba0a/agn-plugin --name @agh-hub/memory-plugin-dcbaba0a`
