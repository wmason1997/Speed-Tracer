# Tracer

A Qix-style territory capture game built as a single HTML file, wrapped in [Capacitor](https://capacitorjs.com/) for Android and iOS deployment.

## Gameplay

Draw a path across the open field and return to safe ground (the border or already-filled area) to claim the enclosed territory. Avoid the bouncing predators — if one touches your trail, or you cross your own trail, you lose a life. Fill enough of the field to clear the level.

**Power-ups** spawn on the field and can be collected by running over them or enclosing them:

| Icon | Power-up | Effect |
|------|----------|--------|
| ⚡ | Speed | Doubles movement speed for 5 seconds |
| ❄️ | Freeze | Freezes all predators for 4 seconds |
| 🛡️ | Shield | Protects your trail from predators for 3 seconds |

**Bonus lives** — fill 10% above the target in a single level, or clear every 5th level, to earn an extra life.

## Modes

### Classic (Free — Levels 1–3)
Progress through levels of increasing difficulty. Each level adds predators, raises their speed, and increases the fill target. Completing a level advances to the next; losing all lives ends the run. Progress is saved — returning to the menu resumes from the highest level reached.

| Level | Predators | Speed | Target |
|-------|-----------|-------|--------|
| 1 | 1 | 5.5 | 75% |
| 2 | 2 | 6.5 | 78% |
| 3 | 2 | 7.5 | 80% |
| 4 ★ | 3 | 8.0 | 83% |
| 5 ★ | 3 | 9.0 | 85% |
| 6 ★ | 4 | 9.5 | 88% |
| 7 ★ | 4 | 10.5 | 90% |
| 8 ★ | 5 | 11.0 | 92% |
| 9 ★ Master | 5 | 12.0 | 95% |

★ Requires Premium unlock.

### Timed Mode (Premium)
Claim as much territory as possible in 90 seconds. No lives — dying respawns you immediately but resets your combo multiplier. Consecutive enclosures build a combo (1× → 4× max, +0.5× per fill). Score = cells filled × current multiplier. High scores are saved to the device.

## Freemium

- Levels 1–3 and Classic mode are free.
- Levels 4–9 and Timed Mode require a one-time **Premium** unlock ($1.99).
- After clearing Level 3, non-premium players see the upgrade prompt.
- Premium status is stored in `localStorage` under `isPremium`.

### IAP Integration

`triggerPurchase()` and `restorePurchase()` are stubbed in `www/index.html` with `TODO` comments marking the integration points for `@capacitor-community/in-app-purchases`. The product ID is `com.williammason.tracer.premium`. On a successful purchase or restore, call `grantPremium()`.

## Controls

An 8-direction drag wheel sits at the bottom of the screen. Press and drag in any direction to move the ship. Drag further from the center for higher speed. Release to stop.

## Project Structure

```
www/
  index.html        — entire game: HTML, CSS, and JS in one file
capacitor.config.json
android/            — Android project (Capacitor)
ios/                — iOS project (Capacitor)
```

All game logic, rendering, and UI live in `www/index.html`. There is no build step for the web layer.

## Local Development

Open `www/index.html` directly in a browser, or use any static file server:

```bash
npx serve www
```

## Android Build

```bash
npx cap sync android
npx cap open android
```

Then build and run from Android Studio.

## iOS Build

```bash
npx cap sync ios
npx cap open ios
```

Then build and run from Xcode.

## localStorage Keys

| Key | Type | Description |
|-----|------|-------------|
| `isPremium` | boolean string | Whether the user has unlocked premium |
| `highestLevel` | number string | Furthest Classic level reached |
| `timedHighScore` | number string | All-time best Timed Mode score |

## Tech Stack

- Vanilla JavaScript, Canvas 2D API — no frameworks, no build system
- [Capacitor 8](https://capacitorjs.com/) for native Android / iOS wrapping
