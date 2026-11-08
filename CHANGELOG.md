# Changelog

## 1.1.1 (2026-11-08)

- The optional API key setting has no default value; leave it blank for keyless mode.
- Code examples in the skills take the key from the project's secret store instead of reading environment variables.

## 1.1.0 (2026-11-08)

- Connects the hosted MCP server at https://allratestoday.com/api/mcp instead of starting two local npm servers. Nothing runs on your machine, and it also works on claude.ai.
- The optional API key is asked for when you enable the plugin and kept in your system's credential store. Leave it blank for keyless mode.
- Slash commands pre-approve only Read, Grep and Glob, and fetch rates through the MCP tools.
- Plugin icon and privacy policy link.
