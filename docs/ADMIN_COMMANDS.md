# Admin commands

A game server's administrators control it by typing commands into the chat. This page
lists every command the server understands, what it does and what it takes.

The descriptions are read from the game server's source code (`saga.gs.cmd`, October
2026). Commands marked **(tested)** were run against a live server on 2026-10-06 or are
used by the test harness every day; the others were checked against the code only.

## How commands work

- **Who is an admin.** Every name in `admins.txt`, a text file in the game server's own
  folder, one name a line. The folder is `-Dsaga.serverdir` (the working directory when
  unset): `~/.saga-online/local/gs-<slot>/` on the development stack, and
  `~/.saga-online/server/` for a server started from the Create Game Server screen. Matching ignores upper and lower case. A `*` at the start, at
  the end or at both ends of an entry matches any text there: `test*` covers `test` and
  `test2`, and `*` alone covers everyone. The list is read every time a command arrives,
  so a change to it -- by command, or by hand and then `/reload adminlist` -- holds at
  once, for players already connected too.
- **The creator is an admin.** A server started from the Create Game Server screen makes
  the player who created it an admin besides the list (the game starts it with
  `-admin <account>`): a server just created has no list, and its creator could not
  otherwise give a command. `/get adminlist` names them first; `/clear` and `/reload`
  do not take their rights.
- **Names are real.** A player's name is the one they logged in with: a joining game
  sends its login session, and the game server asks the root server whose it is. Nobody
  can join under another player's name, an administrator's included. Login sessions live
  in the root server's memory, so after the root server restarts, players must log in
  again before they can join a game: until then a join answers *The server could not
  confirm your login.*
- **How to send one.** Start a chat line with `/` in the lobby chat or in the round's
  chat (to all or to the team). The server runs the command and shows the line to nobody
  else. From anyone who is not an admin, a line starting with `/` is ordinary chat.
- **Format.** `/command argument`. The line is split at the first space: everything after
  it is the argument, spaces included (`/message Round restarts in a minute`). Command
  names ignore case; type arguments in lower case.
- **Replies.** The answer comes back to you alone, as a chat line. Commands that change
  something for players (a kick, a mute) also announce it to everyone in the chat.
  An unknown command answers `Unknown command "...".`
- **Names in commands.** A player name must be typed in full, and ignores case. Only
  `/kick` and `/ban` accept `*` patterns.
- **Without the chat.** The server's own console takes the same commands without the `/`
  (started with `-t`). On the development stack: `./run-local.sh cmd 'server status'`.
- **Logs.** The server's output names every command an admin sends from the chat, by its
  name alone (`Admin: test runs /setpwd`), since an argument may be a password. Chat is
  not logged (the 2010 `-l` chat log, which recorded passwords, is gone).

## Quick reference

| Command | Argument | What it does |
| --- | --- | --- |
| `/get` | `adminlist`, `banlist`, `commandlist`, `maplist`, `playerlist` | Shows a list |
| `/server` | `status`, `restartround`, `unsubscribe`, `resubscribe`, `stop` | Server status and control |
| `/message` | text | Announces the text to everyone |
| `/kick` | name, pattern or `all` | Kicks players off the server |
| `/lock`, `/unlock` | name | Holds a player in the round still, or releases them |
| `/disablechat`, `/enablechat` | name | Mutes or unmutes a player |
| `/addadmin`, `/removeadmin` | name or pattern | Edits the admin list |
| `/ban`, `/unban` | name or pattern | Edits the ban list (adding also kicks) |
| `/clear` | `adminlist` or `banlist` | Empties a list |
| `/reload` | `adminlist`, `banlist` or `maplist` | Reads a list again from its file |
| `/changemap` | map name | Restarts the round on another map |
| `/setroundmode` | `dm`, `tdm`, `dom` or `ma` | Mode of the next round |
| `/setteamcount` | 2 to 4 | Team count of the next round |
| `/setmonsters` | 0 to 16 | How many of the map's monster homes the next round fills |
| `/setscorelimit` | 0 to 10000 | The score a domination or Monster Attack round is won at; 0 plays to the clock |
| `/setspawninterval` | 1 to 60 seconds | Monster Attack: how often a monster spawns |
| `/setmonstercap` | 1 to 16 | Monster Attack: how many monsters may be up at once |
| `/setmegachance` | 0 to 100 percent | Monster Attack: how many of the spawns are Mega Monsters |
| `/setbotkits` | `on` or `off` | Whether a bot may hold the abilities its policy was trained with |
| `/setbots` | `on` or `off` | Whether bots may join at all |
| `/setroundtime` | minutes, at least 5 | Length of the next round |
| `/setplayercount` | number | Most players in the round (at most 16) |
| `/autobalancing` | `on`, `off`, `setpause <s>`, `setpuffer <n>` | Automatic team balancing |
| `/setservername` | name | Name in the server list |
| `/setpwd`, `/getpwd` | password, nothing / none | Sets, removes or shows the join password |
| `/enablepwd`, `/disablepwd` | none | Turns the join password on or off |
| `/gsynch` | none | Resynchronises everyone in the round |

## Information

### `/get <list>` **(tested)**

- `adminlist`, `banlist` -- the entries of each list file.
- `commandlist` -- the name of every command on this page.
- `maplist` -- the maps in the server's `Maps` folder, the names `/changemap` accepts.
- `playerlist` **(tested)** -- every player in the round (not the lobby), with their team
  and the last five round trips the server measured to them (least, mean and most), or
  `no ping yet`.

### `/server status` **(tested)**

One line: the server's build and version, when it started, when the round started (`-`
until a player enters it), the round's length, whether it is listed with the root server
(assumed, not checked), the traffic in packets a second, memory, players in the round
against the maximum with team count and mode (`2/16 (2 teams, tdm mode)`), players in the
lobby against 126, the map, and whether auto-balancing is on.

## Players

### `/message <text>` **(tested)**

Shows the text as a server line in every lobby chat and every round chat.

### `/kick <name | pattern | all>` **(tested)**

An admin's game offers it without typing: the red cross after the icons of each row of the
lobby's player list, and *Kick player* in the menu a right click on another player opens
in the round (*Ban player* there runs `/ban`). Both show only while the player holds an
admin's rights, which the server tells the game at the lobby's entry and on every change.

Kicks players: the server lets them go, their game returns to the server list and shows
*An administrator kicked you from the server.*, and everyone is told *Player "x" got
kicked by admin "y"*. The player may join again; `/ban` keeps them out.

- A full name kicks that player, in the lobby or the round.
- `abc*`, `*abc` or `*abc*` kicks every name starting with, ending with or containing
  `abc`. A pattern that matches nobody answers nothing.
- `all` or `*` kicks everyone.
- A pattern or `all` never kicks you.

### `/lock <name>` and `/unlock <name>`

Holds a player in the round still: they cannot walk or use their attack and ability keys
until `/unlock`, or until they leave the round. Everyone is told. Players in the lobby
are not found. The held player's own game shows them in the attack pose.

### `/disablechat <name>` and `/enablechat <name>` **(tested)**

Mutes a player, or unmutes them. Everyone is told. The server keeps the mute: whatever
the muted player says, in the lobby or the round, reaches nobody, and their game shows
*An administrator has muted your chat.* A mute lasts until `/enablechat` or until the
server is restarted, through rounds and reconnections. `/disablechat` needs the player
connected; `/enablechat` takes any name that is muted, connected or not.

## Admins and bans

Both lists are saved to their files (`admins.txt`, `bans.txt`) as soon as they
change, and read again at the start of every round.

### `/addadmin <name | pattern>` **(tested)**

Adds an entry to the admin list. Every connected player it covers is an admin at once,
patterns included, and everyone is told who was upgraded. If an entry already covers the
name, nothing is added: *Admin list already contains the value*.

### `/removeadmin <name>` **(tested)**

Removes the first entry that covers the name. That may be a pattern: with `b*` on the
list, `/removeadmin bob` deletes `b*`. Everyone it took rights from loses them at once,
and everyone is told.

### `/ban <name | pattern>` **(tested)**

Adds an entry to the ban list and kicks every connected player it covers (never you). A
banned player is refused when connecting. `/ban *` bans every player, you included,
the next time you connect.

### `/unban <name>` **(tested)**

Removes the first entry of the ban list that covers the name, as `/removeadmin` does.

### `/clear <adminlist | banlist>`

Empties the list and its file. Clearing the admin list takes everybody's rights at once,
yours included -- only the server's console can then give them back.

### `/reload <adminlist | banlist | maplist>`

Reads the list again after its file was edited by hand, or the `Maps` folder after a map
was added. A reloaded admin list holds at once and its changes are announced; a reloaded
ban list kicks every connected player it now covers.

## Round and map

Mode, team count and round time apply to the **next** round: send `/server restartround`
to start it.

### `/changemap <map>`

Ends the round and starts a new one on that map (a name from `/get maplist`). Every
connected player, in the lobby or the round, is reconnected and lands in the lobby, and
their game fetches the map if it lacks it. If the round has not stopped after ten
seconds, the command gives up and says so.

### `/server restartround` **(tested)**

The same as `/changemap` with the current map. It starts the next round with the
settings below.

### `/setroundmode <mode>` **(tested)**

- `dm` or `deathmatch` -- every player for themselves. Deathmatch has no teams, and this
  also turns auto-balancing off.
- `tdm` or `teamdeathmatch` -- teams score kills.
- `dom` or `domination` -- teams score by holding capture points. A point falls after
  five seconds with exactly one team on it, and pays its team a point a second; a team
  at the score limit (`/setscorelimit`) wins the round.
- `ma` or `monsterattack` -- Monster Attack: every player on one team, against monsters
  that spawn at the map's monster homes and hunt the players. Each monster picks a
  player, favouring the least hunted, and keeps after it until one of the two dies. The
  team scores a point per monster killed. The map needs monster homes; the team count is
  one, and auto-balancing is turned off.

### `/setteamcount <2..4>` **(tested)**

How many teams the next round has. It matters in team deathmatch and domination only;
Monster Attack always has one.

### `/setmonsters <0..16>` **(tested)**

How many of the map's monster homes the next round fills -- monsters that notice a player
near them, chase and bite, can be killed and come back. A map declares where monsters
may stand; none are out unless this, the `-monsters` argument or the Create Game Server
screen asks for them. More than the map has becomes as many as it has, and the next round
says so. `/server status` shows `Monsters: <filled>/<homes> homes`. Like the team count,
it takes effect when the round restarts.

### `/setscorelimit <0..10000>` **(tested)**

The score a domination round is won at: a team holding that many points wins, and the
round ends at once -- every player's game counts the score and tells the server, which
ends the round on the first report and says *Team 2 wins with 300 points*. 0 plays the
round to its clock. The `-score` argument and the Create Game Server screen's *Score
limit* (300 by default) set it too. `/server status` shows `Score limit: <n>`. Like the
team count, it takes effect when the round restarts. In Monster Attack it counts the
monsters the team has killed; in deathmatch and team deathmatch it does nothing.

### `/setspawninterval <1..60>`, `/setmonstercap <1..16>`, `/setmegachance <0..100>` **(tested)**

Monster Attack's spawner: a monster every so many seconds (6 by default), at most so
many up at once (4), and that percent of them Mega Monsters (10) -- twice the size, three
times the health, twice the strength and four times the coins and experience of their
kind. The `-spawn`, `-monstercap` and `-mega` arguments and the Create Game Server screen
set them too. `/server status` shows `Monster Attack: a monster every 6 s, 4 at most, 10%
Mega`. Like the team count, they take effect when the round restarts; outside Monster
Attack they do nothing.

### `/setbotkits on|off` **(tested)**

Whether a bot -- a client whose character a trained policy plays -- may hold the
abilities its policy was trained with. A bot asks for them when it joins; with `on` (the
default) it gets them, with `off` it plays with the weapon strike, as a player starts. A
human enters a round with the strike alone, so trained abilities are a handicap for the
humans: fine for research, unfair in open play. The `-botkits on|off` argument sets it
when the server starts. It holds for the next bot to join: a bot already in the round
keeps what it has. `/server status` shows `Bot kits: on`. A bot whose game deals it a
kit anyway is removed from the server.

### `/setbots on|off` **(tested)**

Whether bots may join the server at all. With `on` (the default) any player may add a bot
of their own from the lobby's *Add bot*, and a bot started with a bot key joins as well;
with `off` a bot's join is refused (*This server lets in no bots.*) and the lobby greys
*Add bot* for a player who joins after the change -- a lobby already open keeps its button
until it is shown again, and the bot it starts is then refused. The `-bots on|off`
argument sets it when the server starts. A bot already playing stays: kick it
(`/kick Owner#N`). `/server status` shows `Bots: on`.

### `/setroundtime <minutes>`

Length of the next round, at least 5 minutes.

### `/setplayercount <number>`

The most players allowed in the round, from now on; players already in it stay. The game
holds at most 16, so a larger number is set to 16, and the reply says the number
actually set. `0` lets nobody enter the round. The lobby has its own limit of 126.

### `/autobalancing <on | off | setpause seconds | setpuffer number>` **(tested)**

Off unless switched on, and not available in deathmatch. While on, every `setpause`
seconds (30 by default) it checks whether the largest team has more than `setpuffer`
players (2 by default) more than the smallest. If so, it moves one player: the one of the
largest team who joined it last goes to the smallest. The move is an ordinary team
change, made by that player's own game at once, with the death and respawn every team
change has; their screen says *Auto-balancing: you change to ...*. The next check, a
`setpause` later, moves another if the gap is still too large.

## The server

### `/server unsubscribe` and `/server resubscribe` **(tested)**

Takes the server off the server list, or puts it back -- after a root server restart,
`resubscribe` lists it again. Players already connected stay. The server's listener makes
the request between two connections; if it has not within 30 seconds, the command says
so.

### `/server stop`

Takes the server off the list, counts down three seconds in the chat, disconnects
everyone (*An administrator stopped the server.*) and ends the server program. It must
be started again on its machine.

### `/setservername <name>` **(tested)**

The name shown in the server list from its next refresh. Up to 100 characters -- a
longer one is cut there; `%` is removed, and an empty name gives `Saga Online`.

### Join password: `/setpwd`, `/getpwd`, `/enablepwd`, `/disablepwd`

- `/setpwd <password>` stores a password, but does not turn it on. **(tested)**
- `/setpwd` with nothing after it removes the password, and turns it off. **(tested)**
- `/enablepwd` turns it on: players must then type it to join, and the server list
  marks the server as locked. It refuses while no password is stored.
- `/disablepwd` turns it off and keeps it stored.
- `/getpwd` shows the stored password and whether it is on. **(tested)**

Nothing is kept across a restart. A server started with `-pwd <password>`, or `-pwdin` and the password as
the first line of its standard input (what the Create screen does, since a command line
shows in every user's process listing), starts with it stored and on.

## Resynchronising

### `/gsynch` **(tested)**

Resynchronises everyone in the round: one player's game state is copied to every other,
which holds all players still for about a tenth of a second. Use it if players report
seeing different things. The games also repair themselves when they notice they
disagree.
