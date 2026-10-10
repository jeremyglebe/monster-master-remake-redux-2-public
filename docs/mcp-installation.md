# Monster Master MCP + play skill

Play [Monster Master](https://monstermaster.fans/) against an assistant through multiplayer API tools. You use the game's normal Multiplayer screen; the assistant gets its own guest seat and only player-visible information. The package includes a `play-monster-master` Agent Skill for chatty, continued play.

**Release:** [MCP 0.1.0](https://github.com/jeremyglebe/monster-master-remake-redux-2-public/releases/tag/mcp-v0.1.0) is distributed alongside the game in its public release repository. The package includes the server, play skill and this guide. It is installed from GitHub; npm registry publication is optional and has not happened.

## Install the package

Requires Node.js 22.12 or newer on Windows, macOS or Linux. Install directly from the release:

```sh
npm install --global https://github.com/jeremyglebe/monster-master-remake-redux-2-public/releases/download/mcp-v0.1.0/monster-master-mcp-0.1.0.tgz
monster-master-mcp --version
npm root --global
```

Alternatively, download the [package](https://github.com/jeremyglebe/monster-master-remake-redux-2-public/releases/download/mcp-v0.1.0/monster-master-mcp-0.1.0.tgz) and [SHA-256 checksum](https://github.com/jeremyglebe/monster-master-remake-redux-2-public/releases/download/mcp-v0.1.0/monster-master-mcp-0.1.0.tgz.sha256), verify the file, then run `npm install --global /absolute/path/to/monster-master-mcp-0.1.0.tgz`. In PowerShell, `Get-FileHash ./monster-master-mcp-0.1.0.tgz -Algorithm SHA256` prints the hash; on macOS/Linux, use `shasum -a 256 ./monster-master-mcp-0.1.0.tgz`. Compare it with the checksum file. Developers can build the same artifacts with `npm run package:mcp` in the development checkout (output: `release-artifacts/mcp/`).

The last command locates your installed packages. The MCP entry point is `<global-root>/monster-master-mcp/bin/monster-master-mcp.mjs`. Substitute its **absolute path** in the examples below. On Windows, forward slashes in JSON paths work; otherwise escape backslashes as `\\`. If a desktop app cannot find Node, use its absolute executable path instead of `node`.

The package includes compiled game/player code and public card data. It needs no private source checkout, Vite, TypeScript compiler, browser build or backend deployment. Runtime dependencies are installed by npm. Public backend defaults are embedded; no user API key is required.

## Install the companion skill

Choose a skills directory supported by your client:

| Client            | Personal skill directory |
| ----------------- | ------------------------ |
| Codex             | `~/.agents/skills`       |
| Claude Code       | `~/.claude/skills`       |
| Cursor            | `~/.cursor/skills`       |
| VS Code / Copilot | `~/.copilot/skills`      |

For example, for Codex (works in PowerShell and macOS/Linux shells):

```sh
monster-master-mcp --install-skill "$HOME/.agents/skills"
```

Replace the directory for your client. The installer copies `play-monster-master/SKILL.md` and its metadata, leaves unrelated skills alone, and refuses to overwrite a different existing version. Reload your client's skills or start a new session. Registering the MCP server is a separate step below.

These locations follow the clients' current documentation: [Codex](https://developers.openai.com/codex/skills), [Claude Code](https://code.claude.com/docs/en/skills), [Cursor](https://prod.cursor.com/docs/skills), and [VS Code](https://code.visualstudio.com/docs/agent-customization/agent-skills). Other clients may accept the same Agent Skill folder through their own skill importer. A client without skill support can still use the MCP's server instructions; continued play depends on that client's tool loop.

## Codex

```sh
codex mcp add monster-master -- node "/absolute/path/to/monster-master-mcp/bin/monster-master-mcp.mjs"
codex mcp get monster-master
```

In the desktop app, use Settings → MCP servers to restart the connection. In the CLI, `/mcp` shows connected servers. Select or mention `play-monster-master`, or simply ask to play a match after installing the skill. See [Codex MCP configuration](https://developers.openai.com/codex/extend/mcp).

## Claude Code

```sh
claude mcp add --transport stdio --scope user monster-master -- node "/absolute/path/to/monster-master-mcp/bin/monster-master-mcp.mjs"
claude mcp get monster-master
```

Install the skill under `~/.claude/skills`, then invoke `/play-monster-master` with your invitation or ask to play normally. See [Claude Code MCP configuration](https://code.claude.com/docs/en/mcp).

## Claude Desktop

Open Settings → Developer → Edit Config and merge this entry into `mcpServers` (preserve your existing servers):

```json
{
  "mcpServers": {
    "monster-master": {
      "command": "node",
      "args": [
        "/absolute/path/to/monster-master-mcp/bin/monster-master-mcp.mjs"
      ]
    }
  }
}
```

Restart the app. Configuration lives at `%APPDATA%/Claude/claude_desktop_config.json` on Windows or `~/Library/Application Support/Claude/claude_desktop_config.json` on macOS. See the [official local-server setup guide](https://modelcontextprotocol.io/docs/develop/connect-local-servers). Claude Desktop's local MCP setup is independent of Claude Code's skill directory; use the skill importer offered by your desktop version, if available, or rely on server instructions. This setup guide does not promise indefinite turn continuation in every client.

## Cursor

Merge the same `mcpServers` JSON above into `~/.cursor/mcp.json` for personal use, or `.cursor/mcp.json` in a project. Install the skill under `~/.cursor/skills`, reload, and use Agent mode. See [Cursor MCP configuration](https://prod.cursor.com/help/customization/mcp).

## VS Code / GitHub Copilot

Use **MCP: Open User Configuration**, or create `.vscode/mcp.json` in a workspace. Its wrapper is `servers`, rather than `mcpServers`:

```json
{
  "servers": {
    "monster-master": {
      "type": "stdio",
      "command": "node",
      "args": [
        "/absolute/path/to/monster-master-mcp/bin/monster-master-mcp.mjs"
      ]
    }
  }
}
```

Install the skill under `~/.copilot/skills`, start the server, and use an agent with MCP tools enabled. See [VS Code MCP configuration](https://code.visualstudio.com/docs/agents/reference/mcp-configuration).

## Play

Create a room in the game's Multiplayer menu, copy the **full invitation URL**, and say:

> Play Monster Master with me: [full invitation URL].

The installed skill supplies the play loop, fair-play rules and conversation guidance. The bot marks Ready; you mark Ready and start as host. It reacts briefly to meaningful moves, comments while playing, gives a handoff comment, and waits again until the result or you stop it. Conversation stays in the assistant chat. You can also ask it to host and share its invitation.

Concealed opponent cards, deck order, seed/RNG and credentials are excluded from tool output. An explicit in-game reveal effect permits the same information a human player would see. The public rules/catalogue are available to all players.

## Profiles and troubleshooting

The guest identity and pending moves are stored locally under `%LOCALAPPDATA%/MonsterMaster/mcp/<backend-hash>` on Windows or `~/.local/share/MonsterMaster/mcp/<backend-hash>` elsewhere. Preserve that profile to recover your seat. One active game server uses each profile; set `MONSTER_MASTER_MCP_STATE_DIR` in a server's `env` for an independent bot or concurrent client. No credentials appear in game tool output.

Optional `MONSTER_MASTER_MCP_URL` and `MONSTER_MASTER_MCP_KEY` overrides select another backend using its public publishable/anon key. Secret service keys are rejected. Set both when changing backends.

The ten tools are `get_rules`, `join_game`, `create_game`, `get_game`, `ready_game`, `start_game`, `play_action`, `retry_action`, `wait_for_turn` and `leave_game`. Waits last at most 30 seconds and wake on opponent actions, turn/lobby changes or game end; configure a tool timeout of at least 60 seconds if your client exposes that setting. A lost move response is retried with the same command ID, including across restarts. Do not start a new identity to recover an occupied seat.

If the skill appears but tools do not, check the server configuration and restart it. If the server appears but the skill does not, check the client's skill directory. A local stdio server works in clients that can start a local Node process; a cloud-only chat needs a separate hosted MCP integration, which this package does not provide.
