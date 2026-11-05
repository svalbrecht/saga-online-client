<p align="center"><img src="docs/logo.png" alt="Saga Online" width="278"></p>

A 2D top-down multiplayer action-RPG. Warriors and magicians fight with weapons and
abilities across hand-drawn and generated maps, in Deathmatch, Team Deathmatch,
Domination and Monster Attack. Join a game server, or start your own from the game.

This repository holds the game to download and how to play it. It holds no source code.

## Play

1. Install Java 21 or newer ([Adoptium](https://adoptium.net) has installers).
2. Download [saga-client.jar](https://github.com/svalbrecht/saga-online-client/releases/latest/download/saga-client.jar)
   from the [latest release](https://github.com/svalbrecht/saga-online-client/releases/latest).
3. Double-click it, or run `java -jar saga-client.jar`.

The game keeps itself up to date: each time it starts, it fetches a newer version from
its root server if there is one and asks whether to use it. Tick "Don't ask again, always
update" to be asked no more. To keep the version you have without being asked, put a file
`saga-client.properties` beside the jar holding the line `noupdate=1` (from a terminal,
`java -Dsaga.noupdate -jar saga-client.jar` does the same); it then joins only servers of
that version. You need an account on that root server, and a network
that reaches it and its game servers, as [docs/playing.md](docs/playing.md) explains.

| | |
| --- | --- |
| [docs/playing.md](docs/playing.md) | installing and playing, accounts, connection problems, reporting a problem |
| [docs/ADMIN_COMMANDS.md](docs/ADMIN_COMMANDS.md) | the commands of a game server's administrators |
| [NOTICE.md](NOTICE.md) | the licences of what the game is made of |

## Reporting problems

Problems with the game, and suggestions, go in this repository's
[Issues](https://github.com/svalbrecht/saga-online-client/issues). For a crash, a freeze or
a game out of sync, also send a report from the game (Escape, then **Report a problem**):
it carries the logs and a recording an issue cannot, as [docs/playing.md](docs/playing.md#reporting-a-problem)
explains. Problems with the RL package go in [pysaga's Issues](https://github.com/ntu-agents/pysaga/issues).

## Train agents to play it

Saga Online is also a research environment for multi-agent reinforcement learning. The
RL package, its tutorial and its reference are in
[ntu-agents/pysaga](https://github.com/ntu-agents/pysaga). A replay of an
evaluation plays in this game with its pictures and sounds: `java -jar saga-client.jar -replay saga_replay.json`.
