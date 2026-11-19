# Recorded play data

Some Saga Online servers record their rounds for research. This page says why, what is
recorded, where it is kept, and how to have your recordings removed.

## Which servers record

Only servers that say so. A server that records is marked with a disk icon in the server
list, and its tooltip reads *Records its rounds for research*. The first time you join such
a server, the game asks whether you agree to your play being recorded. If you say no, you
are not joined, and nothing is recorded. Servers without the icon record nothing.

Your answer is kept with your account, so you are asked once. To withdraw it, see
[Removing your recordings](#removing-your-recordings).

When you start a server yourself with **Record play data** ticked, the same applies to
every player who joins it, you included.

## Why we record

We study how artificial agents can learn to play from people: to imitate how human players
move and fight, to play alongside them, and to play against them. Recordings of real rounds
are what such agents learn from. We may publish the recordings as a dataset, so that other
researchers can train and compare agents on the same play.

## What is recorded

For each round on a recording server, the game records:

- **Every player's inputs and choices**, step by step: movement, abilities cast, items used,
  bought and sold, abilities learned and placed, skill points spent, team and spawn point
  changes. This covers every player in the round, not only you.
- **The state of the game** often enough to replay the round exactly: positions, health,
  the abilities in flight, and so on.
- **When each step happened on each player's computer**, so that the effect of network
  delay can be studied. In published data these times count from the player's start of the
  round, with no date or time of day.
- **The round's facts**: the map, the mode, the round's number, the game's version and the
  server's name.
- **Each player's account name**, which ties a player's inputs together within the round.

The following are **not** recorded: chat, your password, your IP address, and anything from
your computer other than the game's own inputs.

## Where it is stored

Each player's game sends its recording to the game's root server in parts while the round
is played. The root server runs on a machine at Nanyang Technological University (NTU),
Singapore, and keeps the recordings there in a folder of its own. They are not shared
outside the research team, except as the published dataset described below.

Before a recording is published as part of a dataset, every account name is replaced with a
pseudonym (`player-0001`, `player-0002`, ...). The table linking pseudonyms to account names
stays on the server and is not published.

## Ethics approval

*[Placeholder: details of the approval by NTU's Institutional Review Board, with its
reference number, will be added here once granted.]*

## Removing your recordings

You can ask at any time for your recordings to be removed. When we act on it:

- every recorded round you played in is deleted from the server, for all players in it,
  since each round is one recording of everyone in it;
- your agreement is withdrawn, so the game asks you again before you next join a recording
  server.

Removal applies to every dataset published after your request. A dataset that was already
published cannot be recalled.

## Contact

Stefano V. Albrecht leads this research. To ask a question or have your recordings removed,
use the contact details on his page:
[agents-lab.org/stefano-albrecht](https://agents-lab.org/stefano-albrecht/).
