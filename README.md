# Haven v1

Haven is a single-page fantasy RPG built with HTML, CSS, and vanilla JavaScript. Play in the browser, create heroes, follow a multi-chapter story, battle enemies, explore a six-floor dungeon, train stats, and manage your gear and resources.

## Contents

- [Features](#features)
- [Getting started](#getting-started)
- [How to play](#how-to-play)
- [Progression and rewards](#progression-and-rewards)
- [Saving and accounts](#saving-and-accounts)
- [Project structure](#project-structure)
- [Technical notes](#technical-notes)
- [Limitations](#limitations)

## Features

- **Hero creation and saves:** Create multiple characters with a name, race, and class; select or delete saved heroes.
- **Adventure combat:** Fight Shadow Stalkers using Attack, Defend, and Skill actions.
- **Six-floor dungeon:** Fight three enemies per floor, carry health between waves, earn floor rewards, and unlock floors in order.
- **Story quests:** Complete nine chapters that guide the hero from Haven’s ruins to the Rift Heart.
- **Rank quests:** Take on six repeatable challenge types for each level tier.
- **Training:** Spend Energy to improve Strength, Defense, Speed, or Evasion.
- **Market and inventory:** Buy level-gated gear and consumable potions. Gear bonuses apply when purchased; consumables can be used from Inventory.
- **Merit shop:** Spend merits on permanent stat and resource upgrades, jewels, or temporary boosts.
- **Resource systems:** Health, Energy, and Glory regenerate over time. Rest restores Health and Energy, subject to a cooldown.
- **Progress tracking:** Review combat, dungeon, training, quest, economy, and level records in Stats.
- **Responsive layout:** The interface adjusts for smaller screens and supports reduced-motion preferences.

## Getting started

Open `index.html` in a modern web browser. No build step or server-side service is needed. Haven uses the browser’s `localStorage` for account and character data.

On first load, the character-selection screen is shown. Create a hero to start. You can also create an account from the login screen; see [Saving and accounts](#saving-and-accounts) for details about how this local-only account flow works.

> **Styling note:** The page loads Tailwind CSS from its CDN. An internet connection is needed for the CDN stylesheet; the document also includes custom CSS for the game’s core appearance and layout.

## How to play

### Your first steps

1. Create a character and choose a race and class.
2. Read the welcome guide, or open **Account → What should I do?** later for the adventurer’s guide.
3. Open **Quests**, accept the available story chapter, complete its objective, then return to claim the reward.
4. Use **Adventure** to earn combat rewards and **Training** to improve your stats.
5. Buy useful gear or potions in the **Market** and manage consumables in **Inventory**.
6. Prepare before entering a dungeon: Energy is spent to enter, and Health carries through all three fights.

### Combat

- **Attack** deals a standard attack.
- **Defend** reduces the damage from the enemy’s next attack.
- **Skill** deals a stronger attack.
- Starting an Adventure combat costs 15 Energy. Winning grants Gold and EXP; losing restores the hero to maximum Health.
- Dungeon **Power Strike** costs 5 Energy. Dungeon fights do not offer the same defeat recovery as Adventure combat, so prepare before entering.

### Training and resources

- Training one stat costs 5 Energy. Training all four stats costs 20 Energy.
- Training also drains Glory, up to 5 points per trained stat. The amount of Glory remaining affects the stat gain.
- Health, Energy, and Glory regenerate in 5-point increments every three minutes while the game is open or when it catches up after returning to the page.
- Rest fully restores Health and Energy and starts a 24-hour cooldown. Rest does not restore Glory.

### Dungeons

The dungeon has six floors, each with three consecutive enemies. Floors must be cleared in order. Each floor costs Energy to enter, and the hero’s Health carries between its waves. A defeat ends the attempt without floor rewards and leaves the hero with partial Health. Successful clears award Gold and EXP, with a chance for additional loot or bonus merits.

### Quests and rewards

Story quests unlock sequentially. Accept the current chapter before completing its objective; progress is only tracked for an accepted quest. Claim rewards from the Quests page once the objective is complete. Rank quests are separate challenges organized by level tier and can be accepted from the same page.

## Progression and rewards

- Heroes earn EXP from combat, dungeons, and quests. Each level requires `level × 500` EXP.
- Leveling increases maximum Health and Energy and restores both resources.
- Equipment applies its stat bonus immediately when purchased; it is recorded in the inventory as owned gear, not equipped or removed from stats later.
- Market items have level requirements. Potions are consumed on use and cannot be used during an active fight.
- Gold and EXP multipliers, and the Combat Power boost, are temporary merit-shop effects. Their durations are tracked using the browser’s clock.

## Saving and accounts

Haven saves data in the browser’s `localStorage` under the `users` key. Character saves include resources, stats, inventory, quest progress, boosts, and lifetime statistics. Resource regeneration can catch up based on elapsed time when the page is revisited.

This is a **local-only demo**, not an online account system:

- Data is stored only in the current browser profile and is not synchronized across devices.
- Clearing browser data can erase saves. Use the same browser profile to continue playing.
- Account passwords are stored in browser storage as plain text. Do not use real or reused passwords.
- The app initializes a local player and opens character selection on load. The register/login UI does not provide server-backed authentication or cloud saves.
- Anyone with access to the browser profile can inspect or modify local save data.

## Project structure

```text
.
├── index.html   # Game markup, styles, interface, and JavaScript logic
└── README.md    # Project documentation
```

The project is intentionally self-contained in `index.html`. It uses inline CSS and JavaScript, with Tailwind CSS referenced from its CDN for utility styles.

## Technical notes

- Built with standard HTML, CSS, and browser JavaScript APIs; there is no framework or package-install step.
- Uses `localStorage`, DOM APIs, timers, and browser events for persistence and gameplay updates.
- Emoji are used for many interface icons.
- The game is designed for a modern browser with JavaScript and local storage enabled.

## Limitations

- There is no backend, multiplayer, account recovery, or cross-device save synchronization.
- Because saves and account information are client-side, they should not be considered secure or tamper-proof.
- The Tailwind CDN dependency may be unavailable offline; custom styles remain embedded in the document.
- Gameplay balance and random outcomes are handled entirely in the browser.
