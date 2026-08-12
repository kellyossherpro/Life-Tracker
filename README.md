# The Life Index

A private, phone-first app to track **everything** in one place — foods & recipes,
personal reference info (medical aid, insurance, rent, car, ID), your body, and your
money. Built to run for **R0/month** on free tiers, with your sensitive data
encrypted on-device before it ever syncs.

> 📄 **Read the full blueprint:** [`docs/blueprint.html`](docs/blueprint.html) —
> open it in a browser (or view the hosted version shared in chat) for the designed,
> phone-friendly version.

---

## The decisions (locked)

| Question | Decision |
| --- | --- |
| Where it lives | **Progressive Web App (PWA)** — "Add to Home Screen", works offline, no App Store |
| Cost | **R0/month** — entirely on free tiers |
| Data | **On-device first**, auto-synced to a **free private cloud** for backup + multi-device |
| Sensitive fields | **Encrypted on the phone** (passphrase only Kelly knows) before syncing |
| Currency | **South African Rand (R)** |
| Reminders | **On** — driven by due dates (rent, renewals, cycle, weigh-ins) |
| Start with | **Foods & Recipes** + **Personal Info Vault** |

## Proposed stack (all free)

| Piece | Choice | Why |
| --- | --- | --- |
| App / UI | React + Vite + PWA plugin | Installable, offline, easy to grow module-by-module |
| On-device storage | IndexedDB (via Dexie) | Instant saves, works with no signal |
| Cloud sync + login | Supabase free tier (Postgres + Auth + row-level security) | Generous free tier; each user only sees their own rows |
| Encryption | Web Crypto API (AES-GCM), key derived from a passphrase | Vault fields are unreadable to the server |
| Hosting | GitHub Pages / Netlify / Vercel free tier | Static PWA, R0 |

*(Stack is a recommendation, not yet committed — confirm before Phase 0.)*

## Roadmap

- **Phase 0 — Foundation:** installable app shell, navigation, offline storage, login, encrypted sync.
- **Phase 1 — Week-one modules:** Foods & Recipes (ingredients → auto cost & time, favorites, shops) + Personal Info Vault (locked sensitive fields, renewal reminders).
- **Phase 2 — Body:** Period & Cycle (log, symptoms, predictions) + Weight (trends).
- **Phase 3 — Money & time:** bank-statement import (CSV then PDF) + budgets + Time/Habits + Home Dashboard.

## Data models (Phase 1)

### Foods & Recipes
`name`, `photo`, `favourite`, `ingredients[] {name, quantity, unit, cost, shop}`,
`prep_time`, `cook_time`, `servings`, `total_cost` (auto), `steps`, `rating`, `last_made`

### Personal Info Vault
`category` (Medical Aid · Insurance · Internet · Rent · Car · ID & Docs · Utilities · Subscriptions),
`title`, `provider`, `account_no` 🔒, `id_number` 🔒, `monthly_cost`, `renewal_date`,
`documents`, `notes` — fields marked 🔒 are encrypted on-device before sync.

## Status

Blueprint approved-in-progress. Next step: build **Phase 0 + Phase 1** (pending Kelly's go-ahead).
