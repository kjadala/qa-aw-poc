<details>
<summary>MCP Gateway</summary>

- ✓ **startup** MCPG Gateway version: v0.2.17
- ✓ **startup** Starting MCPG with config: stdin, listen: 0.0.0.0:80, log-dir: /tmp/gh-aw/mcp-logs/
- ✓ **startup** Loaded 3 MCP server(s): [github rpdevops safeoutputs]
- ✓ **startup** Guards sink server ID logging enrichment disabled
- ✓ **backend**
  ```
  Successfully connected to MCP backend server, command=docker
  ```
- 🔍 rpc **github**→`tools/list`
- 🔍 rpc **github**←`resp` `{"jsonrpc":"2.0","id":1,"result":{"tools":[{"annotations":{"readOnlyHint":true,"title":"Get commit details"},"description":"Get details for a commit from a GitHub repository","inputSchema":{"properties":{"include_diff":{"default":true,"description":"Whether to include file diffs and stats in the response. Default is true.","type":"boolean"},"owner":{"description":"Repository owner","type":"string"},"page":{"description":"Page number for pagination (min 1)","minimum":1,"type":"number"},"perPage":{"descriptio...`
- ✗ **backend**
  ```
  MCP backend stderr output:
npm error code E403
npm error 403 403 Forbidden - GET https://artifacts.realpage.com/artifactory/api/npm/npm-virtual/@architecture%2fmcp-server-azuredevops
npm error 403 In most cases, you or one of your dependencies are requesting
npm error 403 a package version that is forbidden by your security policy, or
npm error 403 on a server you do not have access to.
npm error A complete log of this run can be found in: /root/.npm/_logs/2026-04-16T03_30_20_643Z-debug-0.log
npm notice
npm notice New minor version of npm available! 11.11.0 -> 11.12.1
npm notice Changelog: https://github.com/npm/cli/releases/tag/v11.12.1
npm notice To update run: npm install -g npm@11.12.1
npm notice
  ```
- ✗ **backend**
  ```
  MCP backend connection/protocol error, command=docker
  ```
- ✗ **backend**
  ```
  MCP backend connection/protocol error, command=docker
  ```
- 🔍 rpc **safeoutputs**→`tools/list`
- 🔍 rpc **safeoutputs**←`resp` `{"jsonrpc":"2.0","id":1,"result":{"tools":[{"description":"Create a new GitHub issue for tracking bugs, feature requests, or tasks. Use this for actionable work items that need assignment, labeling, and status tracking. For reports, announcements, or status updates that don't require task tracking, use create_discussion instead. CONSTRAINTS: Maximum 1 issue(s) can be created. Title will be prefixed with \"[US-Eval] \". Labels [\"user-story-evaluation\" \"automated\"] will be automatically added.","inputSche...`
- ✓ **startup** Starting in ROUTED mode on 0.0.0.0:80
- ✓ **startup** Routes: /mcp/<server> for servers: [github rpdevops safeoutputs]
- ✗ **backend**
  ```
  MCP backend stderr output:
npm error code E403
npm error 403 403 Forbidden - GET https://artifacts.realpage.com/artifactory/api/npm/npm-virtual/@architecture%2fmcp-server-azuredevops
npm error 403 In most cases, you or one of your dependencies are requesting
npm error 403 a package version that is forbidden by your security policy, or
npm error 403 on a server you do not have access to.
npm error A complete log of this run can be found in: /root/.npm/_logs/2026-04-16T03_30_52_617Z-debug-0.log
npm notice
npm notice New minor version of npm available! 11.11.0 -> 11.12.1
npm notice Changelog: https://github.com/npm/cli/releases/tag/v11.12.1
npm notice To update run: npm install -g npm@11.12.1
npm notice
  ```
- ✗ **backend**
  ```
  MCP backend connection/protocol error, command=docker
  ```
- ✗ **backend**
  ```
  MCP backend connection/protocol error, command=docker
  ```
- 🔍 rpc **safeoutputs**→`tools/call` `missing_tool`
  
  ```json
  {"params":{"arguments":{"alternatives":"Ensure the rpdevops MCP server is configured and the AZDO_PAT secret is set in the repository with read access to the Consumer Solutions project on tfs.realpage.com.","reason":"The rpdevops MCP server required to fetch Azure DevOps work item #1727233 is not available in this environment. Cannot retrieve work item content to perform evaluation.","tool":"rpdevops MCP server (wit_get_work_item)"},"name":"missing_tool"}}
  ```
- 🔍 rpc **safeoutputs**←`resp`
  
  ```json
  {"id":1,"result":{"content":[{"text":"{\"result\":\"success\"}","type":"text"}]}}
  ```
- 🔍 rpc **safeoutputs**→`tools/call` `{"jsonrpc":"2.0","method":"tools/call","params":{"arguments":{"body":"## Work Item Fetch Failed\n\n**Work Item ID:** [#1727233](https://tfs.realpage.com/tfs/Realpage/Consumer%20Solutions/_workitems/edit/1727233)\n**Date:** 2026-04-16\n**Workflow Run:** [24490455707](https://github.com/kjadala/qa-aw-poc/actions/runs/24490455707)\n\n---\n\n## Error Details\n\nThe automated User Story Evaluation workflow could not retrieve work item **#1727233** from Azure DevOps because the **rpdevops MCP server** was not ava...`
- 🔍 rpc **safeoutputs**←`resp`
  
  ```json
  {"id":1,"result":{"content":[{"text":"{\"result\":\"success\"}","type":"text"}]}}
  ```
