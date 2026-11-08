# Kit (ConvertKit) MCP server

Find subscribers and explicitly create an inactive subscriber record without activating a subscription.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `KIT_API_KEY`



Credential help: https://developers.kit.com/api-reference/v4.json

## Provider setup

Use your own Kit v4 API key (X-Kit-Api-Key). Creating an inactive record does not establish consent or subscribe the person; review downstream Kit automation before writes.

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call kit_list_subscribers '{"per_page":10}'
```

## Use with an MCP client

Launch `node /absolute/path/kit-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| kit_list_subscribers | Read | Read a page of subscribers with optional email filtering. |
| kit_create_inactive_subscriber | Explicit approval required | Create an inactive subscriber; this does not subscribe them to email marketing. |

## Concrete workflow

Find subscribers and explicitly create an inactive subscriber record without activating a subscription.

1. kit_list_subscribers
2. kit_create_inactive_subscriber

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Activate with PipMCP](https://pipmcp.com/github/start?app=kit&integration=kit-mcp&utm_source=github&utm_campaign=github-kit-mcp&utm_content=readme) when you want the hosted service.  Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/kit/).

## Provenance and maintenance

- https://developers.kit.com/api-reference/v4.json

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.
