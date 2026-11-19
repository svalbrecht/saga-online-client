<p align="center"><img src="docs/logo.png" alt="Saga Online" width="278"></p>

A 2D top-down multiplayer action-RPG developed in Java. Warriors and magicians fight with weapons and
abilities across generated maps. Gain experience points, level up, learn powerful abilities, and trade equipment in shops. Five elements (Neutral, Earth, Fire, Ice, Wind - the orbs in the logo) run through the abilities and weapons: Earth beats Fire, Fire beats Ice, Ice beats Wind, and Wind beats Earth. Game modes include Deathmatch, Team Deathmatch, Domination, Monster Attack, and Capture the Flag. Join a game server or start your own server from the game.

## Play

1. Install Java 21 or newer ([Adoptium](https://adoptium.net) has installers).
2. Download [saga-client.jar](https://github.com/svalbrecht/saga-online-client/releases/latest/download/saga-client.jar)
   from the [latest release](https://github.com/svalbrecht/saga-online-client/releases/latest).
3. Double-click it, or run `java -jar saga-client.jar`.

The game keeps itself up to date. Each time it starts, it fetches the latest version from
the root server.


| | |
| --- | --- |
| [docs/playing.md](docs/playing.md) | installing and playing, accounts, connection problems, reporting a problem |
| [docs/ADMIN_COMMANDS.md](docs/ADMIN_COMMANDS.md) | the commands of a game server's administrators |
| [NOTICE.md](NOTICE.md) | the licences of what the game is made of |

## Reporting problems

If you experience any problems while playing the game (such as a crash, game out of sync, something looking wrong), please send a report from the game: press ESC key, then click **Report a problem**. The report carries the game's logs and a recording of the round, as [docs/playing.md](docs/playing.md#reporting-a-problem) explains.

Feel free to post suggestions or other issues in this repository's
[Issues](https://github.com/svalbrecht/saga-online-client/issues).

## Train agents to play the game

Saga Online is also a research environment for [multi-agent reinforcement learning](https://en.wikipedia.org/wiki/Multi-agent_reinforcement_learning) (MARL).
The [pySaga](https://github.com/ntu-agents/pysaga) Python package lets you train policies for bots in Saga Online using MARL algorithms. To get started, see the [quickstart guide](https://github.com/ntu-agents/pysaga/blob/main/docs/rl-quickstart.md).

If you would like to learn more about MARL, and AI research in general, check out these books:

* [Multi-Agent Reinforcement Learning: Foundations and Modern Approaches](https://www.marl-book.com/) (MIT Press, free download)
* [Becoming an AI Researcher: Practical Advice for Graduate Students](https://phd-in-ai.com/) (Cambridge University Press)
