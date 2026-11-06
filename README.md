# vera20k-superai

**vera20k-superai** is the Super AI plugin for [VERA20K](https://github.com/YuriPlanet/vera20k):
a stronger, human-style computer opponent for skirmish. It plays at the command layer as a
virtual player, so determinism and replays stay intact.

## Status

**The plugin crate is in preparation.** Phase 1 — extracting Super AI out of the engine into a
plugin crate — is underway on the fork's `superai` line.

Until the crate lands, you can play Super AI today by building the fork:

- Clone [CCDawn/vera20k](https://github.com/CCDawn/vera20k) (its default branch is
  `superai/base`) and follow the [quick start in SUPERAI.md](https://github.com/CCDawn/vera20k/blob/superai/base/SUPERAI.md).
- The same fork's `superai/defense-next` branch adds the **defense persona**: on
  wave-defense maps the AI auto-detects the map form and co-defends — fort lines on the
  attack routes, a staffed objective ring, cooperative stances. Screenshots sit on that
  branch's [README](https://github.com/CCDawn/vera20k/tree/superai/defense-next#defense-ai-showcase-defense-ai-展示)
  and the play guide (中文) in
  [docs/defense-ai-install.zh.md](https://github.com/CCDawn/vera20k/blob/superai/defense-next/docs/defense-ai-install.zh.md).

When this repository takes over, it will offer:

1. **A plugin crate** — add Super AI to your VERA20K build as a dependency.
2. **Prebuilt releases** — ready-to-run builds for Windows, Linux and macOS on the
   [releases page](https://github.com/CCDawn/vera20k-superai/releases).

## What it is

Super AI is a **command-layer virtual player**. It observes the match through a read-only view
and issues the same command stream a human player would — it never writes simulation state
directly, so **determinism and replays stay intact**.

The stock computer opponents (**Easy**, **Normal**, **Hard**) are completely untouched: an
ordinary computer slot keeps the native AI. Super AI is strictly **opt-in** — a match uses it
only when you pick a Super AI row in the lobby.

The design notes live in
[docs/superai.md](https://github.com/CCDawn/vera20k/blob/superai/base/docs/superai.md) on the
fork: positioning, the determinism contract, the engine hooks and upstream sync.

## Difficulty tiers

| Tier | Strength | Lobby row |
|------|----------|-----------|
| **Fair** | Zero subsidies. Pure decisions only — the baseline for win-rate measurement. | — |
| **Brutal** | Fair + the native Hard AI's opening subsidy + a recurring +1,000 credits drip. | — |
| **Super** | Brutal + build times scaled ×0.5. | **Super AI** |
| **Unlimited** | Super + a per-tick wallet floor topped up to 1,000,000 credits. A spectacle tier for watching; do not cite it for strength claims. | **Super AI MAX** |

The lobby exposes only the **Super AI** (Super) and **Super AI MAX** (Unlimited) rows. **Fair**
and **Brutal** are benchmark-only tiers, used as measurement baselines by the headless win-rate
bench.

## Roadmap

1. **Extract the plugin crate.** A virtual-player interface on the fork, so Super AI can leave
   the engine tree.
2. **This repository takes over releases.** The crate as a dependency, plus prebuilt binaries
   for all platforms, published here.
3. **Give back upstream.** A generic virtual-player interface offered to
   [YuriPlanet/vera20k](https://github.com/YuriPlanet/vera20k).

## License

Licensed under the [GNU GPLv3](LICENSE-GPL), like VERA20K itself. This repository contains no
game files.
