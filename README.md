# Turnout

**Everyone takes a turn hosting.** A rotating-host community for real-life gatherings: fair turns, themed ideas where everyone contributes, shared costs so the host isn't footing the bill, and a guest list that mixes friends with friends-of-friends.

**Live demo:** https://mindy-portfolio.vercel.app/turnout.html
Part of [Mindy's portfolio](https://mindy-portfolio.vercel.app).

> The **sample circle** runs entirely in your browser (saved to `localStorage`, simulated members, no API calls). An optional **cloud layer** (Supabase) adds email sign-in, real circles with invite links and owner approval, and a server-run rotation, party planning, RSVP, rating and points. It is only active when you sign in; see [`docs/backend.md`](docs/backend.md).

## Why

In-person hosting has become rarer while loneliness has become a bigger problem. A lot of that is the activation energy: someone has to host, and the cost and effort fall on one person. Turnout makes hosting a shared, scheduled habit.

## What the demo does

- **Circle:** a fair rotation wheel (nobody hosts twice until everyone has once), claim-a-month scheduling, skip-this-month, adjustable circle size.
- **Party:** themed ideas (charcuterie, blind wine tasting, bagel spread-off, chili cook-off, dumpling folding and more, plus "Move" previews like pilates and park yoga). Each says what the host brings, what each guest brings, and the game.
- **Money:** a host-cost model with budget tiers and a small circle pot that reimburses the host. It shows the host's worst-month cost with and without sharing, and flags when the pot is too small.
- **After:** rate the party, "lock in" the new people you met, and watch your network grow.
- **Me:** points, a leaderboard, your vibe matches, and what the matcher has learned.
- **Look:** a disco-ball entrance, with a day mode (sage green and butter yellow) and a night mode (soft orange on navy).

## The machine learning (all on-device)

The sample sizes here are tiny, so these are small models that learn from feedback, not deep networks.

| Piece | Method |
|---|---|
| Idea ranking | Collaborative filtering (Pearson similarity over idea ratings) blended with a logistic regression trained online on post-party ratings |
| Guest matching | Pair-compatibility logistic regression over vibe-dimension closeness, "has what you look for", and shared interests; retrained from who you actually lock in |
| Room composition | Hill-climbing optimiser balancing known vs new people, making sure nobody is isolated, with attendance fairness and capped points |

Points raise invite priority, capped at 250, with a boost for people who've never attended. Host rotation ignores points.

## Run it

It's one static file.

```bash
python3 -m http.server 8080   # then open http://localhost:8080
```

## Roadmap

See [`docs/backend.md`](docs/backend.md) and [`docs/schema.sql`](docs/schema.sql): phone sign-in, moving matching fully server-side so members' answers stay private, live updates, and safety features (report and block, address reveal) before strangers meet at homes.

First-month goals: at least four communities created, each hosting at least one party, and 100 sign-ups or installs.

## Notes

All rights reserved for now. Not yet licensed for reuse.
