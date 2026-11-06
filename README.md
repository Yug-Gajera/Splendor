# Splendor

A playable browser version of Splendor (Marc André, Space Cowboys) — full base-game
rules, 2–4 seats, any mix of humans and bots, in a single self-contained HTML file.

## Playing it

Open `index.html` in any modern browser. No build step, no dependencies, no server.
The only network request is the Google Fonts stylesheet; the game runs fine offline
with fallback type.

### On a phone

Publish it with GitHub Pages and play from the Home Screen:

1. **Settings → Pages** in this repository
2. Source **Deploy from a branch**, branch `master`, folder `/ (root)`, **Save**
3. After a minute it is live at <https://yug-gajera.github.io/Splendor/>
4. On iPhone, open that in Safari → **Share → Add to Home Screen**. It launches
   full-screen with no browser chrome, using the bundled icon.

On phones the bank, your tray and your purse ride in a dock at the bottom, and the
turn banner sticks to the top, so the whole table fits on one iPhone 13 screen
without scrolling. Gems you take fly into the dock. Verified on emulated iPhone 13
and iPhone SE: no horizontal scrolling, nothing clipped, and taps drive every action.
Text fields are 16 px so Safari never zooms in on them.

## Rules implemented

Everything in the base game:

- **Setup** — 90 development cards (40 / 30 / 20 across levels I–III), 4 face up per
  level, nobles equal to players + 1. Gem supply is 4 / 5 / 7 per colour for
  2 / 3 / 4 players, plus 5 gold.
- **One action per turn** — take 3 different gems; take 2 of one colour (only from a
  pile of 4 or more); reserve a card from the table or the top of a face-down deck,
  taking a gold with it if any remains; or buy a card from the table or your reserve.
- Taking the maximum number of different gems is enforced, and fewer than 3 only when
  fewer colours remain.
- **Bonuses** — each owned card permanently discounts one gem of its colour.
- **Gold** is a wild joker, and can only be obtained by reserving.
- **Reserve limit** of 3, with reserved cards held face down from opponents.
- **Hand limit** of 10 gems, returned down at the end of the turn.
- **Nobles** arrive automatically when bonuses qualify, at most one per turn, with a
  choice when several qualify at once. Worth 3 prestige each.
- **Game end** — reaching 15 prestige triggers the final round so every player has had
  the same number of turns. Most prestige wins; ties go to the player with fewer
  development cards.

## A note on the card data

No authoritative machine-readable card list exists publicly. The deck here is
generated from the published card *structure*: each tier's cost shapes and prestige
values are dealt once per gem colour around the colour wheel, which reproduces the
official composition exactly — 40 / 30 / 20 cards and 5 / 55 / 80 total prestige per
tier, with the same distribution of costs. Which specific colour pairs with which
cost may differ from the physical cards; play balance does not.

Card names ("Lapis mine", "Sable treasury vault") are flavour, not from the original —
the printed cards carry illustrations rather than names.

## Motion

Every move travels across the table, and the state only changes once it lands:

- **Picking gems:** each one hops from its pile into your tray. Tap a tray gem to
  send it back.
- **Taking gems:** they arc from the tray into your purse, one after another.
- **Buying a card:** it lifts from the market and flies to your bonuses while your
  payment arcs back into the bank. A replacement deals out of the deck.
- **Reserving:** the card flies into your hand along with its gold. A bot's reserve
  flips face down in mid-air.
- **Nobles:** the tile travels from the gallery to the merchant who earned it.
- Stacks pop as gems land, and prestige counters jump when they rise.

**Bots get the same treatment.** On its turn a bot first shows what it is reaching
for, with a garnet ring on the piles or the card it chose and a caption in the turn bar.
Then its move plays out with the same flights as yours, so you can follow every turn.
**Pace** (Brisk, Measured or Deliberate, set at setup or from the top bar) scales
both the animations and the bots' thinking time. With *reduce motion* switched on
in the system settings, the flights are skipped, but bots still pause between moves.

## The bots

Three levels, chosen at setup:

| Level | How it plays |
|---|---|
| **Gentle** | Sometimes browses instead of buying, buys whatever catches its eye, rarely blocks you. |
| **Shrewd** | Scores every legal move: prestige, noble progress, and bonuses toward the cards it's aiming at. Reserves only to win, to take a card a rival can already afford, or when a good card is nearly in hand. |
| **Ruthless** | Plays each promising move forward three of its own turns on a copy of the table and keeps the line that scores soonest. It also blocks a rival's winning card. Its lookahead never peeks at the hidden decks: refills come up empty. |

Measured head to head over 60–80 games each, alternating who goes first:
Shrewd beats Gentle **74%** of the time and Ruthless beats Shrewd **67%**.
Ruthless takes about 10 ms per move.

**Hint** in the turn bar asks the Ruthless engine for your best move and sets it up for
you: the gems go in your tray, or the card is selected with Buy and Reserve ready.

## Saving and your record

The game in progress is saved after every turn, so a reload or a closed tab picks up
where it left off. That matters on iPhone, where Home Screen apps get reloaded. *New game*
keeps the save until you deal a new one, and the setup screen offers to resume it.
Games against bots build a record of wins, best score, and results per bot level.
Winning brings a shower of gems.

## Sound

Every sound is synthesised in the browser, with no audio files: gem clinks as they land,
a swish as a card lifts, a chime for a noble, a two-note cue when the bots hand the turn
back to you, and a fanfare for a win. Toggle it from the top bar. On iPhone it follows
the silent switch where Safari supports that.

## Layout

    index.html              the whole game: styles, rules engine, bot, and UI
    manifest.webmanifest    Home Screen name, colours and display mode
    apple-touch-icon.png    180x180 Home Screen icon

`index.html` is a complete standalone document, so it works from GitHub Pages, a file
on disk, or any static host. The copy published as a Claude artifact is the same file
with its `<head>`/`<body>` shell stripped, since that platform supplies its own.

Verified with headless runs of 2-, 3-, and 4-player games: gem and card totals are
conserved every turn, the hand limit and reserve limit always hold, and every game
terminates with a legitimate winner.
