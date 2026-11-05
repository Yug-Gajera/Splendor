# Splendor

A playable browser version of Splendor (Marc André, Space Cowboys) — full base-game
rules, 2–4 seats, any mix of humans and bots, in a single self-contained HTML file.

## Playing it

Open `index.html` in any modern browser. No build step, no dependencies, no server.
The only network request is the Google Fonts stylesheet; the game runs fine offline
with fallback type.

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

## The bots

Each bot scores every legal action and takes the best, with a little noise so games
differ. It values prestige, progress toward nobles, and bonuses that cheapen the cards
it is aiming at; it reserves only to close out a win, to take a card a rival can
already afford, or when a card worth buying is nearly in hand. Pace is adjustable at
setup.

## Layout

    index.html    the whole game: styles, rules engine, bot, and UI

Verified with headless runs of 2-, 3-, and 4-player games: gem and card totals are
conserved every turn, the hand limit and reserve limit always hold, and every game
terminates with a legitimate winner.
