# Bee Garden

A first taste of coding for young kids. A bumblebee wants to reach the flowers in a little fenced garden. You don't
steer her. Instead you lay down arrow cards to make a plan, press Go, and watch her follow it card by card. It works
like the floor robots used in kindergartens, on a phone or tablet.

Twelve gardens, everything built in code (no picture files), synthesized sounds. Play it at
[tb-x.github.io/bee-garden](https://tb-x.github.io/bee-garden/).

It works offline and can be added to the Home Screen: the first visit stores everything it needs, and later visits
start without internet.

## How it plays

- The garden is a grid of squares in two shades of green, so the steps are easy to count. The bee starts on a
  honeycomb mat. Bushes, rocks and a toadstool are in the way.
- Tap the arrow buttons to add cards to the plan strip (up to 12). Each card plays a note that goes up the scale, so
  a longer plan sounds like a little tune. Tap a card in the strip to take it out, or use the back button to remove
  the last one.
- Press the big green Go button. The bee buzzes along her plan, and the card she's on lights up.
- Every flower she flies over gets sipped: it grows, its petals spin and sparkles fly. When every flower in the
  garden is sipped, she does a happy loop and the "Yum!" card shows the next garden.
- **Gentle failing.** If a card sends her into a bush or the fence, she bumps, gets dizzy stars, and that card
  shakes red. If the plan runs out before all the flowers, she shrugs. Either way she flies back to her mat, and the
  plan stays so it can be fixed.
- After three tries a light bulb appears. Tapping it shows the shortest way as a trail of honey drops (but not
  which cards to use).
- **Gardens 1–6** use screen arrows (up, down, left, right). **Gardens 7–12** switch to robot cards: forward, turn
  left and turn right. Here the bee turns on the spot, and a white chevron on the ground shows which way she's facing.
  This is the harder idea, the one Bee-Bot style toys teach.
- The level dots at the top jump back to any garden already reached. Progress and the mute setting are remembered.

## Running it

```bash
python -m http.server 5231
```

Then open `http://localhost:5231/` (or use the `bee-garden` entry in the root launch config). Opening `index.html`
straight from disk mostly works too.

## Tuning knobs

At the top of the script in `index.html`:

| Knob | What it does | Now |
| --- | --- | --- |
| `MAX_CARDS` | longest plan the bee will follow | 12 |
| `STEP_MS` | time for one hop to the next square | 520 ms |
| `TURN_MS` | time for a quarter turn on the spot | 340 ms |
| `HINT_AFTER_FAILS` | tries before the hint bulb shows up | 3 |
| `CAM_ELEVATION` | how steeply the camera looks down | 54° |
| `LEVELS` | the gardens, drawn as little text maps (`B` bee, `F` flower, `#` bush, `o` rock, `m` toadstool), which card set they use, and where the bee faces | 12 gardens |

On load, the page checks that every garden can be solved within `MAX_CARDS` and warns in the console if one can't.
`window.__par` lists the shortest plan for each one: 2, 3, 4, 5, 6, 6 cards for the arrow gardens and 3, 5, 8, 9,
11, 11 for the turn gardens.

## Ideas for the next version

- Is the jump from arrows to turning too big? A garden or two that mixes them in, or a short demo of "turn means turn
  on the spot", might help.
- The later turn gardens need 11 cards, which is a lot for a 5-year-old. A "repeat ×2" card would teach loops and
  shorten the plans.
- More things to do on the way: pollen to carry back to the hive, flowers that must be visited in colour order, a
  spider web that sends her back.
- The name avoids "Bee-Bot", which is a trademarked toy.
