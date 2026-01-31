# Masked Garden

Game jam project - theme: **mask**

Domain: [masked.garden](https://masked.garden)

## Quick Start

```bash
pnpm install
pnpm dev
```

Open http://localhost:3000

## Routes

| Route | Purpose |
|-------|---------|
| `/` | Landing page |
| `#demo` | Demo index |
| `#demo/game` | Main game |
| `#demo/sound` | Sound team workspace |
| `#demo/art` | Art direction (TODO) |
| `#demo/particles` | Shader effects (TODO) |
| `#demo/assets` | Asset browser (TODO) |

Demo pages use additative registry pattern - see `ent/web/app/demos/reg.ts`

## Architecture

```
Pure TS Data Layer = Source of Truth
         |
    +----+----+
    |         |
    v         v
Three.js   Jotai Atoms
(reads     (reflects)
 per-frame)    |
               v
           React UI
           (subscribes)
```

**Rules:**
- Never flow data React → Three.js
- Three.js reads raw data directly (imperative, per-frame)
- React reads via Jotai atoms (reactive, on-change)
- All mutations go through actions

See [data-flow.md](data-flow.md) for full architecture.

## Structure

```
env/
  ts/lib/        # pure TS utilities
  game/          # game logic (no react, no three)
    state/       # jotai atoms + actions
    lib/         # masks, zones, etc
  three/lib/     # three.js rendering
  react_web/lib/ # react hooks + components

ent/web/         # entrypoints
public/assets/   # drop zone for team
```

## Patterns & Docs

| Doc | Purpose |
|-----|--------|
| [data-flow.md](data-flow.md) | Clean data flow architecture |
| [stable-randomness.md](stable-randomness.md) | Seeded world generation |
| [graceful-degradation.md](graceful-degradation.md) | Load handling & throttling |
| [ts-refactoring-patterns.md](ts-refactoring-patterns.md) | TypeScript patterns |
| [react-patterns.md](react-patterns.md) | React patterns |
| [SPEC.rim](SPEC.rim) | Full architecture spec |
