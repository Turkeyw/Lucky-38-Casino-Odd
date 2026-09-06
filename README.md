# Lucky 38 Casino — Odds & Fairness

The complete math behind every game. The short version: **no game is rigged.** Every roll, card, mine, and horse is decided by plain randomness before or during play — the house earns its edge by paying slightly below true odds, exactly like a real casino, never by touching the outcome.

| | |
|---|---|
| **Games** | 5 |
| **House edge (most games)** | 5% |
| **Blackjack edge** | ~1% (rules-based) |
| **Outcomes altered after the fact** | 0 |

> **How the house edge works**
>
> Every payout in this document is the mathematically fair payout multiplied by **0.95** (or the rules-based equivalent for blackjack). The randomness itself is never weighted. If a game says you have a 1-in-5 chance, you have exactly a 1-in-5 chance — the win simply pays 4.75x instead of 5x.

---

## Blackjack

Standard rules: 6-deck shoe, dealer stands on all 17s, aces auto-score as 1 or 11 (whichever keeps you alive), double down on your first two cards.

| Outcome | Payout |
|---|---|
| Win (closer to 21 than dealer) | 2x your bet (1:1) |
| Blackjack (natural 21 on the deal) | 2.5x your bet (3:2) |
| Push (tie with dealer) | Bet refunded |
| Bust / dealer wins | Bet lost |
| Double down (first two cards) | Bet doubled, one card, forced stand |

*House edge comes from the rules themselves, not the payouts: when you bust, you lose immediately — even if the dealer would have busted too. That single rule gives the house roughly 1% over time, the same as a real casino table.*

---

## Horse Race

Five horses, identical movement odds every tick (0–3 steps: 10% / 35% / 35% / 20%). Every horse has an exactly equal **20% chance** to win — there is no favorite, and dead heats at the line are settled by a coin flip.

| Mode | Payout |
|---|---|
| Solo — your horse wins (1 in 5) | 2.25x your bet |
| Party — winner takes the pot | Pot minus 5% rake |
| Party — a riderless horse wins | House takes the pot |

*Solo EV: 20% chance × 2.25x payout = 0.45. Solo mode is priced as a high-variance jackpot bet — party mode (5% rake) is the fair-odds way to race.*

---

## Dice Roll

Two six-sided dice are rolled; you bet on the exact sum (2–12). Each sum pays its true odds (36 divided by the number of ways to roll it) multiplied by 0.95 — so every number on the board carries the same 5% house edge, and no pick is secretly better or worse than another.

| Sum | Ways to roll | Chance | Payout |
|---|---|---|---|
| 2 or 12 | 1 of 36 | 2.78% | 34.2x |
| 3 or 11 | 2 of 36 | 5.56% | 17.1x |
| 4 or 10 | 3 of 36 | 8.33% | 11.4x |
| 5 or 9 | 4 of 36 | 11.11% | 8.55x |
| 6 or 8 | 5 of 36 | 13.89% | 6.84x |
| 7 | 6 of 36 | 16.67% | 5.7x |

*EV check: (ways / 36) × (36 / ways) × 0.95 = 0.95 for every single number.*

---

## Crab Games

Simplified craps with two dice. Overall chance to win a round: **51.6%**.

| Stage | Probability | Result |
|---|---|---|
| Come-out roll: 7 or 11 | 22.2% (8 of 36) | Instant win — 1.84x |
| Come-out roll: 2, 3 or 12 | 11.1% (4 of 36) | Instant loss |
| Come-out roll: 4, 5, 6, 8, 9, 10 | 66.7% (24 of 36) | Point set — smaller die rerolled up to 2x for a 7 or 11 |
| Point phase | 44.1% to win | Win — 1.84x, otherwise house wins |

*EV: 51.6% × 1.84x = 0.95 — the same 5% house edge as every other game.*

---

## Mines

A 5x5 board hides your chosen number of mines. **All mine positions are generated when the game starts — before your first click — and are never moved.** Each diamond raises your multiplier by the true survival odds of that pick, minus a small per-pick house cut that scales with mine count.

### Multiplier by safe picks

| Board | 1 pick | 3 picks | 5 picks | 10 picks |
|---|---|---|---|---|
| 1 mine | 1.01x | 1.04x | 1.07x | 1.23x |
| 2 mines | 1.02x | 1.08x | 1.16x | 1.54x |
| 3 mines | 1.04x | 1.13x | 1.27x | 2.01x |
| 5 mines | 1.15x | 1.57x | 2.26x | 7.69x |
| 7 mines | 1.29x | 2.25x | 4.27x | 35.38x |
| 10 mines | 1.57x | 4.20x | 12.98x | 586.28x |
| 15 mines | 2.40x | 16.96x | 171.91x | 2,173,178x |
| 20 mines | 4.90x | 216.47x | 48,025x | — |
| 24 mines | 24.50x | — | — | — |

### Per-pick house cut

| Mines on board | Cut per pick |
|---|---|
| 1 mine | 3.0% |
| 2 mines | 6.0% |
| 3 mines | 8.8% |
| 5 mines | 8.0% |
| 7 mines | 7.2% |
| 10 mines | 6.0% |
| 15 mines | 4.0% |
| 20 / 24 mines | 2.0% (floor) |

*The cut is capped at 0.75 × mines / 25 so a diamond can never lower your multiplier — every safe pick always pays more than the last.*

---

## Fairness Guarantees

- Mines are placed **before your first click** and revealed in full when the game ends.
- Horse positions, dice, and cards are drawn live from unweighted randomness.
- Bets are deducted up front; abandoned games refund automatically (dice 60s, mines 5 min, horse lobby 5 min).
- If a race message is deleted mid-game, every rider is refunded in full.
- Your lifetime winrate is tracked on `/balance` — you can audit your own results against these tables any time.

---

*Source: Lucky 38 game handlers · September 2026*
