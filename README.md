# Animal Checklist MCP

Animal Checklist offers two remote MCP servers over Streamable HTTP.

| Server | URL | Access |
| --- | --- | --- |
| Species catalogue | `https://animalchecklist.com/mcp` | Public, read only |
| Your account | `https://animalchecklist.com/mcp/account` | Personal MCP key |

The public server searches animal species and returns these details:

- Names.
- Habitats.
- Countries.
- Photos.
- Source credits.

The account server also reads your synced sightings. A read-write key can mark a catalogue species seen.

Create a personal key on [your Account page](https://animalchecklist.com/account). Choose a read key unless your MCP app must mark animals seen. Copy the key when it appears; Animal Checklist shows it only once. Remove it from the same page when you no longer use the app. Keys expire after 90 days.

Configure the account server with this HTTP header:

```text
Authorization: Bearer YOUR_MCP_KEY
```

Keep the key in your MCP client's secret store. Do not commit it to a repository. The public `mcp.json` contains only the keyless catalogue server because the Agent Plugins 1.0.0 format does not define portable secret references.

Both endpoints support MCP `2026-07-28` with per-request metadata and matching HTTP headers. Legacy clients retain initialization and result shapes.
The authenticated account endpoint can expose `checklist.sighting_changed` after the operator enables its safe relay.
Check `server/discover` with your key for Events readiness. The keyless catalogue has no Events capability.
See the [Events contract](https://animalchecklist.com/mcp-events.md).

The `server.json` and `server-account.json` files describe both servers for the [official MCP Registry](https://registry.modelcontextprotocol.io/). The [`mcp.json`](mcp.json) file provides a portable public-server connection. See the [developer guide](https://animalchecklist.com/developers) for tool details and a client config example.
