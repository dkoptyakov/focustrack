# FocusTrack

An attention trainer with statistics you can actually read: Schulte tables, dual n-back,
and red-black Gorbov–Schulte tables. Runs in any browser and as a Telegram Mini App.

**Open it:** https://dkoptyakov.github.io/focustrack/ · **In Telegram:** [@focustrack_bot](https://t.me/focustrack_bot)

Interface in English and Russian. No account, no server, no tracking.

## Three exercises, three functions of attention

| Exercise | What it trains | What is measured |
|---|---|---|
| **Schulte tables** (4×4–6×6) | sustained attention, peripheral vision | time, errors, the pause before every number; a series of 5 yields the classic EF / WU / ST indices |
| **Dual n-back** | working memory | per-channel accuracy for position and sound, adaptive level N |
| **Red-black tables** (7×7) | attention switching | time, errors, the pause before every move |

Every exercise keeps its own statistics: day-by-day trend, personal best, average of the
last five attempts with a delta, a heatmap of where your search slows down, and a log of
individual attempts you can prune.

## How to practice

**Schulte tables.** Keep your eyes on the center of the grid (turn on the anchor dot) and
find the numbers in order using peripheral vision, rather than scanning row by row. The
adult norm for a 5×5 grid is roughly 25–40 seconds. *Click mode* is for measurement — it
records errors and the pause on each number. *Gaze mode* is the pure exercise: find every
number with your eyes, then press Finish.

**Dual n-back.** Every 3 seconds a cell lights up and a letter is spoken. Flag a match with
what appeared N steps back — position (`A`) and sound (`L`) independently. A session runs
20 + N² trials, and the level adapts: ≥ 80 % moves you up, three consecutive sessions below
50 % move you down. Session length, thresholds and the probabilities of forced matches and
lures follow [Brain Workshop](https://brainworkshop.sourceforge.net/); the implementation
here was written from scratch, with no code or audio taken from it.

**Red-black tables.** Alternate black ascending with red descending: B1 → R24 → B2 → R23 …
→ B25. Switching between two rules is the whole point of the exercise.

You improve at what you train. Expect gains in visual search, peripheral span and
concentration — not in general intelligence. The app reports what it measured and promises
nothing beyond that.

## Where your data lives

There is no backend and no analytics.

- **In a browser**, history is kept in `localStorage` — on that device only, works offline.
- **In Telegram**, history is kept in Telegram's cloud storage, tied to your account and
  available on every device you use: phone, Telegram Desktop, web.telegram.org.

The two stores are independent. Move history between them with **Export** → **Import**:
records merge by unique id, importing the same file twice adds nothing, and deleted records
are not resurrected by an older export.

## Running your own instance

1. Fork this repository and enable GitHub Pages (branch `main`, root).
2. In [@BotFather](https://t.me/BotFather): `/newbot`, then pick a name and username.
3. `/newapp` → choose the bot → give it your Pages URL and a short name.
4. Optionally `/setmenubutton` to launch the app straight from the bot chat.

## Development

The whole app is a single `index.html`: no build step, no dependencies, opens on a
double click. The only external resource is Telegram's official `telegram-web-app.js`, and
the app degrades to local storage when it is absent.

The file is organised in numbered sections — design tokens, markup, i18n dictionary, pure
logic, storage adapters, exercise controllers, statistics, boot. Game rules, scoring, merge
and migration are DOM-free functions, so they can be exercised straight from the console.

## License

MIT
