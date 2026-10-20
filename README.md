# GreatWait for Cursor and Gemini CLI

<img src="assets/logo.svg" alt="GreatWait" width="96" />

**Reliable webhook scheduling for your agent, your app, and you!**

Connect Cursor or Gemini CLI to [GreatWait](https://greatwait.dev) to schedule webhook callbacks,
inspect schedules and delivery attempts, and forecast upcoming webhook activity.
Forecasting helps you see what is due before callbacks run.

This repository contains a Cursor plugin and a Gemini CLI extension for the
hosted GreatWait MCP service over Streamable HTTP. It contains only connection
configuration and a logo; it runs no local server and requires no API key in
the wrapper files.

**Review OAuth permissions carefully.** The current OAuth setup can request full
access, including billing, API keys, and access administration. Decline consent
if those permissions exceed what you intend to grant. These URL-only wrappers do
not narrow the service's OAuth permissions or tool catalog.

## Connect with Gemini CLI

Install the extension from this public repository:

```sh
gemini extensions install https://github.com/flowxo/greatwait-cursor-plugin
```

Review Gemini CLI's installation prompt. Start or restart Gemini CLI, then use
`/mcp` to see the `greatwait` server. If it asks for authentication, use
`/mcp auth greatwait`. Gemini CLI discovers GreatWait's OAuth service. In
GreatWait, select the project the connection will use and review the requested
permissions before approving. The extension's root `gemini-extension.json`
points to `https://api.greatwait.dev/mcp` with Gemini's `httpUrl` setting.

## Connect with Cursor

1. Install the plugin in Cursor. For a local installation, follow the steps below.
2. Open Cursor's Customize or MCP settings and find the `greatwait` server.
3. Start sign-in. Cursor discovers GreatWait's OAuth service and registers its
   client dynamically. In GreatWait, select the project the connection will use
   and review the requested permissions before approving.
4. Return to Cursor and confirm the server is connected and its tools are visible.

You need a GreatWait account and a project you can access. A connection works in
the project selected during consent. Available tools depend on your role and
permissions.

## Use the connection

Try a bounded read first:

> List at most one existing GreatWait schedule. Do not create, change, cancel, or
> deliver anything, and do not request additional permissions.

Once you are satisfied with the connection, you can ask your agent to schedule a
callback to an HTTPS endpoint you control, inspect its delivery result, or
forecast upcoming activity. Review actions that change schedules before allowing
the agent to perform them.

## Cursor local installation

Cursor supports local plugins in `~/.cursor/plugins/local`:

```sh
git clone https://github.com/flowxo/greatwait-cursor-plugin.git \
  ~/.cursor/plugins/local/greatwait
```

Restart Cursor or run **Developer: Reload Window**, then open **Customize** and
confirm that the plugin's `greatwait` MCP server appears. Team policies may
restrict local plugin imports; a Marketplace installation with the same name
takes precedence over a local copy.

The root `mcp.json` contains only:

```json
{
  "mcpServers": {
    "greatwait": {
      "url": "https://api.greatwait.dev/mcp"
    }
  }
}
```

For manual MCP setup without the plugin, use that entry in your Cursor MCP
configuration. Use one installation method to avoid duplicate server entries.

## Pricing and access

The wrappers are free, with no wrapper surcharge. Normal GreatWait service usage
pricing applies; installing them does not include unlimited service usage.
See [GreatWait](https://greatwait.dev) for current service pricing.

To withdraw an OAuth connection, open GreatWait **Settings → Access → Connected
applications** and withdraw its access. The client will then need a new
authorization to use the service.

## Help

- [GreatWait MCP guide](https://docs.greatwait.dev/guides/mcp)
- [Cursor MCP documentation](https://cursor.com/docs/mcp)
- [Cursor local plugin installation](https://cursor.com/docs/plugins#test-plugins-locally)
- [Gemini CLI extension installation](https://geminicli.com/docs/extensions/reference/#install-an-extension)
- [Report a wrapper issue](https://github.com/flowxo/greatwait-cursor-plugin/issues)

The [MIT license](LICENSE) covers this wrapper. The hosted service remains
subject to GreatWait's terms and usage pricing. The GreatWait name and logo
remain the property of their owner; the wrapper license grants no trademark
rights. The logo is the official asset from
[greatwait.dev](https://greatwait.dev/brand/icon-primary.svg).
