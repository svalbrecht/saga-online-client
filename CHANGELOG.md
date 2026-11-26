# Changelog

What changed in each version of Saga Online, newest first.

## 0.2.1182 (2026-11-26)

### Added

- Players at home can join a server another player hosts at home, with no port opened on
  the router. Players on networks such as a university's still need the host's port opened.
- A star before the name of the player who created a server, in the lobby's player list and
  the player statistics (R). The game information (L) names that player as the host.

### Changed

- Each server is reached through one network port, and a connection is made with one
  network round trip less.
- A server on another network of the same campus or company is reached at its inside address.
- A server's map comes over the server's own port.
- After five wrong passwords for an account, each further login attempt waits a while, from
  2 seconds up to 5 minutes. A saved login always gets through.
- The creator of a server made with Create is told in the lobby whether players elsewhere
  can reach it.
- The root server moved to a new address, 80.69.33.167. The game moves to it by itself at
  its next update, and a saved login is kept.
- The NTU servers are reached from NTU's network or over its VPN.
- Leaving a round goes straight back to the server's lobby, without the server list in between.
  The end menu's button reads Return to lobby.
- A lost network packet delays a join, a return to the lobby or any other request to a server
  by about half a second, where it cost up to 10 seconds.
- The cast key (E) and opening a shop end a walk or an attack started with a click.
- Playing guide: on a Mac on Wi-Fi, AirDrop, AirPlay and Handoff delay packets; how to turn
  them off while playing.

### Fixed

- The saved login was lost when one computer played on two servers, or when a login's
  answer was lost on the network.
- Joining a server could wait 5 seconds when the lobby's player list was lost on the network.

## 0.2.1133 (2026-11-24)

### Added

- Click to move and click to attack, beside the keys: a left click on the map walks
  there, holding the button down steers the walk, and a click on an enemy attacks it
  with the selected ability until it is gone. A yellow ring marks the point walked to,
  a red ring the target attacked. A movement key cancels the click.
- Search box on the server list, filtering by server name or map.
- Bounce stones on Stilthaven's north and south lanes; teleport stones on Menhirmoor,
  Mazeholt, Glimmerdeep and Highcrest.
- *Max. pl.* column on the server list; *Players* shows lobby and round counts.
- Allowed latency for servers (100 ms by default): a player whose connection is too
  slow is turned away at Join or moved back to the lobby. Set on the Create Game Server
  screen; shown in the game information window (L).
- Ping shown in red on the server list where it is above a server's allowed latency.
- Create Game Server: each mode's settings in a block of their own, with info icons
  for the modes, monster homes and mode settings.

### Changed

- Menus and the round's window are 900 pixels wide.
- Lobby player list and character box one row taller.
- Monster Attack is last in the Create Game Server mode list, and asks the map for 4
  monster homes when chosen.
- Ping in the player statistics (R) is the median round trip of the last 20 seconds.
- Playing guide: how a Mac opens the game the first time.

### Fixed

- Joining a round over a VPN or another network that only carries small packets.
- Players in a round briefly rewound when another player joined.
- A player could be dropped about 10 seconds after joining a round.
- Menu text fields no longer make the system's error sound.
- Stray pixels on the castle towers of the menu landscape.

## 0.2.1082 (2026-11-19)

### Added

- Screenshot key on every screen (Cmd+Shift+P on a Mac, Ctrl+Shift+P elsewhere),
  saving to the desktop.

## 0.2.1075 (2026-11-19)

### Fixed

- A game woken late by its computer (a busy machine, a window in the background)
  falling behind the round.
