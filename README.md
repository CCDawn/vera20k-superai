# vera20k-superai

**vera20k-superai** is the Super AI plugin for [VERA20K](https://github.com/YuriPlanet/vera20k):
a stronger, human-style computer opponent for skirmish. It plays at the command layer as a
virtual player, so determinism and replays stay intact.

## Status

**The plugin crate has landed.** `vera20k-superai` is now a workspace crate on the fork's
`superai/defense-next` branch: the AI lives in `superai/`, reads the engine through public
read-only APIs and emits the same command stream a human sends — the engine itself no longer
knows the AI exists. This repository mirrors that crate (see *Sync* below).

To play today, build the fork — the crate is a plain workspace member, so the usual build
just works:

```sh
git clone -b superai/defense-next https://github.com/CCDawn/vera20k.git
cd vera20k
cargo build --profile fast -p vera20k --bin vera20k
```

That branch also carries the **defense persona**: on wave-defense maps the AI auto-detects
the map form and co-defends — fort lines on the attack routes, a staffed objective ring,
cooperative stances. Screenshots sit on that
branch's [README](https://github.com/CCDawn/vera20k/tree/superai/defense-next#defense-ai-showcase-defense-ai-展示)
and the play guide (中文) in
[docs/defense-ai-install.zh.md](https://github.com/CCDawn/vera20k/blob/superai/defense-next/docs/defense-ai-install.zh.md).

A standalone clone of this repository alone does **not** build: the crate depends on the
engine by path (`vera20k-core = { path = "../src" }`), so it compiles inside the fork's
workspace. Prebuilt releases remain planned for the
[releases page](https://github.com/CCDawn/vera20k-superai/releases).

### Sync

This repository is a subtree mirror of `superai/` in the fork. After changes land there:

```sh
git clone -b superai/defense-next https://github.com/CCDawn/vera20k.git
cd vera20k
git subtree split -P superai -b superai-crate-split
git push https://github.com/CCDawn/vera20k-superai.git superai-crate-split:crate-split
```

…then merge `crate-split` into `main` here (unrelated histories are already recorded).

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

1. ~~**Extract the plugin crate.**~~ **Done** — the crate lives in the fork's `superai/`
   workspace member and is mirrored here.
2. **This repository takes over releases.** The crate as a dependency, plus prebuilt binaries
   for all platforms, published here.
3. **Give back upstream.** A generic virtual-player interface offered to
   [YuriPlanet/vera20k](https://github.com/YuriPlanet/vera20k).

## License

Licensed under the [GNU GPLv3](LICENSE-GPL), like VERA20K itself. This repository contains no
game files.
