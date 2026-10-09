# Monster Master · remake

[Play Monster Master](https://monstermaster.fans/) · [Download releases](https://github.com/jeremyglebe/monster-master-remake-redux-2-public/releases)

An HTML5 remake of Matthew Stradwick (Moonkey)'s original Monster Master,
published by Crazy Monkey Games. Remade with permission.

Play against the computer, watch two computers, or share a device for local
two-player games. Choose your characters, names, deck strengths or custom decks
made from the original cards. Classic is the default appearance; Settings lets
you switch to Modern and continue the same match. Online multiplayer is planned.

This repository distributes **built releases**. The game's development source,
original Flash file and reference archives remain private. JavaScript and CSS in
the downloads are minified, without source maps. Original artwork and other
materials retain their original ownership; publication grants no new license.

Latest stable release: [1.1.4](https://github.com/jeremyglebe/monster-master-remake-redux-2-public/releases/tag/v1.1.4).

## Downloads

Use the `browser.zip` asset for a static web server at its root. Extract the ZIP
and serve that folder over HTTP. The `pages.zip` asset is prepared for this
repository's GitHub project path. `SHA256SUMS.txt` lists archive checksums.

## Website updates

Publishing a stable release with a Pages archive triggers the deployment
workflow. It downloads the latest stable release and deploys its built files to
GitHub Pages. The workflow can also be run manually to redeploy the latest
release. Repository files contain only distribution documentation and hosting
configuration; the workflow has no access to the private source repository.

The custom domain `monstermaster.fans` belongs to this repository's Pages site.
