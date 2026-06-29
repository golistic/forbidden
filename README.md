# Forbidden

Guard a gate. Let your side in, drop the other side into the void. A small LCD-style
arcade game in Go, ripped off (lovingly) from a 1981 handheld.

Working name, might rename it before it's done. It comes from HTTP 403 — every enemy you
turn away gets a Forbidden.

## Where this came from

It began with a hunt for a handheld LCD game, half-remembered from a 1980s childhood in
Belgium: figures coming in from the left toward a castle, and you work a drawbridge to let
the good ones in while the bad ones drop in the moat. Finding it again meant digging through
thousands of photos in the handheld archives.

It's Gakken's Trojan Horse, 1981 (sold as Cheval de Troie in French).

You're defending Troy. People come off a ship and walk toward the city walls. Some are
Greek soldiers attacking, some are civilians trying to get in. You raise the bridge so the
soldiers fall in the moat, lower it to let civilians through. There's a wooden horse that
turns up now and then. The catch: you can't win. Troy always falls. You're just playing to
see how long you last.

That gate loop is the whole thing this project rebuilds.

## What it is

Same loop, tech theme.

Stuff comes in from one side. You open and close the gate. Let your team through, drop the
enemy. Letting an enemy in is bad, dropping one of your own is bad, surviving gets points.

You pick a side at the start, and that decides who's the hero and who's the monster. Same
sprite, drawn cute when it's yours and nasty when it's the enemy's. Saves art, and it's
kind of the joke anyway — everyone thinks the other language is the cursed one.

### Ideas to try (not committed to any of it)

Teams: language mascots fighting. Go's gopher vs Rust's Ferris, Python vs Ruby, the browser
wars, vim vs emacs, whatever.

The gate doesn't have to be a drawbridge. A CD-ROM tray. A sci-fi door that opens the wrong
way half the time. A server bay. A firewall. A USB port that's never the right way up.

Where rejected enemies go: /dev/null, the recycle bin, the backlog.

Power-ups and hazards as jokes: caffeine for speed, rubber duck for slow-mo, segfault
glitches the screen, kernel panic flips it, stack overflow piles enemies up, merge conflict,
hotfix repairs the gate, a Heisenbug.

Bosses: Internet Explorer (slow, won't die), a COBOL mainframe, "manager wants a sync".

HTTP codes as enemy types: 403 turned away, 404 vanishes, 418 teapot, 429 a rush wave, 500
crashes the gate, 200 gets in fine.

A Trojan Horse enemy, since that's where this all started. Looks like one of yours, isn't.

The unwinnable thing from the original stays. It just gets harder until you lose, then it
shows you a fake post-mortem / incident report. Prod always goes down eventually.

## Tech

Go + Fyne (v2).

It's basically a state machine with sprites that swap around, so no real game engine needed.

- `canvas.Image` sprites that snap to fixed lane positions (gives it that chunky LCD look)
- `time.Ticker` for the loop
- updates go through `fyne.Do` / `fyne.DoAndWait`, not straight from the loop goroutine

Fixed slots per lane should feel the most like the old game.

## License

Copyright (C) 2026 Geert JM Vanderkelen.

Split license, because code and art aren't the same thing:

- **Code** — GNU General Public License v3.0 ([`LICENSE`](LICENSE)). Fork it, change it, share
  it; anything you ship built on it has to stay GPL too.
- **Art, sprites, sound and other assets** — Creative Commons Attribution-NonCommercial 4.0
  ([`LICENSE-ASSETS`](LICENSE-ASSETS)). Use and remix with credit, but **not commercially**.

So you can read, learn from and tinker with all of it, but you can't repackage the game and
sell it (on a console store or anywhere else) — the assets block that. Want to do something
commercial with it? Ask: geert@vanderkelen.org.

### Don't-get-sued notes

- The mechanic is fine to copy. You can't copyright game rules. Just not Gakken's actual
  art or sounds.
- Ferris (the Rust crab) is public domain, CC0. Use it however.
- The Go gopher is Renée French's, under CC BY, so using her art means crediting her.
  Easier to just draw a new gopher.
- "Go" and "Rust" and their logos are trademarks. Use the mascots as characters, not as the
  game's logo, don't pretend it's official, and put an "unofficial, not affiliated" line
  somewhere.

## Roadmap

### Phase 0 — setup

- [ ] Go module + repo (pick a stable module path; title is just a string)
- [ ] Fyne window up, fixed size, draws a static gate

### Phase 1 — make it a game

- [ ] one matchup, two lanes, fixed slots
- [ ] spawn friends and enemies from one side
- [ ] gate open/close on input
- [ ] scoring: enemy in = bad, ally dropped = bad, enemy dropped = good
- [ ] health/lives, lose condition, game over screen

### Phase 2 — make it feel right

- [ ] chunky LCD-style movement
- [ ] sound
- [ ] gets harder over time
- [ ] post-mortem end screen

### Phase 3 — content

- [ ] side-select screen
- [ ] more matchups
- [ ] different gates per matchup
- [ ] mascots (custom gopher + Ferris)
- [ ] HTTP-code enemies
- [ ] power-ups, hazards, bosses
- [ ] the Trojan Horse enemy

### Phase 4 — ship it

- [ ] final name + IP disclaimer
- [ ] settings, save high score
- [ ] desktop builds, itch.io page

## Links

- Gakken Trojan Horse: http://handheldempire.com/game.jsp?game=805
- write-up on the game: https://link.springer.com/chapter/10.1007/978-3-319-73380-7_5
- gameplay video: https://www.youtube.com/watch?v=jLlK8mgdOcc
- Go gopher: https://go.dev/blog/gopher and https://go.dev/brand
- Ferris: https://rustacean.net and https://ferris.rs/blogs/guides/can-you-use-ferris
- Fyne: https://fyne.io
