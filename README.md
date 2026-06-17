# English Billiards Scorer

A self-contained, mobile-first scoreboard for marking up a game of English
Billiards. It runs entirely in the browser from a single HTML file — no build
step, no server-side code, no dependencies to install, and no network
connection required once the page has loaded.

The whole app lives in [`public_html/index.html`](public_html/index.html):
markup, styling and game logic are bundled into one file so it can be dropped
onto any static web host (hence the `public_html` directory) or simply opened
straight from disk.

---

## Purpose

When friends play English Billiards down the pub or in the club room, keeping
score on a chalkboard is fiddly and easy to get wrong. This tool turns a phone,
tablet or laptop into a dedicated marker's board:

- Tap a button each time a player scores and the totals, the current break and
  the high break all update automatically.
- It enforces nothing about *how* you play — it simply does the arithmetic, so
  the players stay in charge of the game.
- At the end it shows a full breakdown of the match: per-player statistics and a
  score-progression chart.

It is designed to feel at home on the table rail: dark green "cloth" styling,
brass accents, big touch targets, and a screen that stays awake while you play.

---

## Scoring rules

The buttons follow standard English Billiards scoring:

| Action            | Points | Notes                                   |
| ----------------- | -----: | --------------------------------------- |
| Pot Red           | **+3** | Potting the red ball                    |
| In-off Red        | **+3** | Cue ball goes in off the red            |
| Pot Cue Ball      | **+2** | Potting the opponent's (white) cue ball |
| In-off Cue Ball   | **+2** | Cue ball goes in off the other cue ball |
| Cannon            | **+2** | Cue ball strikes both other balls       |
| Foul              | **+2** | Awarded to the **opponent**             |

Points accumulate into the striker's **current break** until the break ends
(either by ending the turn or committing a foul). The highest break each player
makes during the match is tracked separately.

The match is won by the first player to reach the agreed target score
(the "finish line"). Targets of 50, 100, 150 or 200 are one tap away, or you can
type any number.

---

## Using the tool

### Opening it

- **Locally:** open `public_html/index.html` in any modern browser
  (double-click it, or drag it onto a browser window).
- **Hosted:** upload the contents of `public_html/` to any static web host
  (the directory is named `public_html` so it works out of the box on most
  shared hosting). Then visit the page.
- **As an app:** on iOS/Android, use *Add to Home Screen* to launch it
  full-screen like a native app.

### Setting up a match

1. Enter each player's name (optional — defaults to "Player 1" / "Player 2").
2. Pick a coloured ball for each player. The colour the opponent picks is shown
   on the cue-ball buttons during play so it's clear which ball is which.
3. Choose the finish line (the score the match is played to).
4. Tap **Start match**.

### During play

- The active player's panel is highlighted and marked **In play**.
- Before any points are scored you can tap the *other* player's panel to swap
  who breaks first.
- Tap a scoring button each time the striker scores; the score, current break
  and high break update immediately.
- Tap **End break & change player** to hand over to the opponent.
- Tap **Foul (+2 opp.)** to award two points to the opponent and pass the turn.
- **Undo** reverses the last action (multiple levels of undo are supported).
- **New match** resets everything (with a confirmation prompt).

### Extras

- **Full screen** — toggle a distraction-free full-screen view.
- **Screen** — a keep-awake toggle so the display doesn't lock mid-frame
  (where the browser supports it).
- **Sounds** — choose a sound pack (Arcade, Sci-Fi, Jazz Age, Darts, Classic)
  or mute entirely. All sounds are synthesised in the browser — no audio files.

### End of the match

When a player reaches the target, an end screen shows:

- The winner and the final score.
- A match summary (scoring strokes, lead changes, best break).
- Per-player statistics: final score, highest break, visits, average per visit,
  cannons, pots, in-offs and fouls conceded.
- A score-progression line chart for both players.

From there you can start a **Rematch** with the same players and settings, or
set up a **New match**.

---

## Technical notes

- **Single file, zero dependencies.** Everything is inline in
  `public_html/index.html`. The only external resources are Google Fonts, which
  are optional — the page falls back to system fonts if they can't load.
- **No data is stored or transmitted.** All state lives in memory for the
  duration of the match; refreshing the page starts over.
- **Progressive enhancement.** Wake-lock, full-screen and the Web Audio API are
  all used only when available and degrade gracefully when they aren't.
- **Responsive.** Layouts are tuned for phones, tablets and landscape displays.

## Repository layout

```
.
├── public_html/
│   └── index.html   # the entire application
└── README.md        # this file
