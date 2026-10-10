# Monster Master · remake

Latest stable release: [1.3.4](https://github.com/jeremyglebe/monster-master-remake-redux-2-public/releases/tag/v1.3.4).

[Play Monster Master](https://monstermaster.fans/) · [Download releases](https://github.com/jeremyglebe/monster-master-remake-redux-2-public/releases)

An HTML5 remake of Matthew Stradwick (Moonkey)'s original Monster Master,
published by Crazy Monkey Games.

Play against the computer, watch two computers, or share a device for local
two-player games. Choose your characters, names, deck strengths or custom decks
made from the original cards. Phones and touch tablets default to Mobile; desktop
players start in Classic. Settings offers Classic, Modern and Mobile, preserving
the same match when switching. Mobile uses the Classic burgundy/cream/gold
palette, tap-to-inspect cards, highlighted targets, scrolling hands and fields,
and large turn controls.

Online multiplayer uses private invitation rooms: choose Multiplayer, share a
room link, mark Ready, then start. Guests need no account, and all three
interfaces can play together.

This repository distributes **built releases**. The game's development source,
original Flash file and reference archives remain private. JavaScript and CSS in
the downloads are minified, without source maps. Original artwork and other
materials retain their original ownership; publication grants no new license.

## Downloads

Use the `browser.zip` asset for a static web server at its root. Extract the ZIP
and serve that folder over HTTP. The `pages.zip` asset is prepared for this
repository's GitHub project path. `SHA256SUMS.txt` lists archive checksums.

## Play against an assistant

[MCP 0.1.0](https://github.com/jeremyglebe/monster-master-remake-redux-2-public/releases/tag/mcp-v0.1.0) lets an assistant play a multiplayer seat through API calls. The package includes the `play-monster-master` skill, which guides ongoing, chatty play using only player-visible information.

See the [installation guide](docs/mcp-installation.md) for Codex, Claude Code/Desktop, Cursor and VS Code/Copilot. Requires Node.js 22.12 or newer; install the package, install the companion skill, and register the MCP server in your client. Then share a full invitation URL from the game's Multiplayer menu. Conversation stays in the assistant chat. The MCP has its own version and does not update the hosted game.

## Website updates

Publishing a stable release with a Pages archive triggers the deployment
workflow. It downloads the latest stable release and deploys its built files to
GitHub Pages. The workflow can also be run manually to redeploy the latest
release. Repository files contain only distribution documentation and hosting
configuration; the workflow has no access to the private source repository.

The custom domain `monstermaster.fans` belongs to this repository's Pages site.
