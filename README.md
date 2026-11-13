# COD Matchmaking Simulator

An interactive browser-based simulator that demonstrates how Call of Duty's matchmaking systems actually work, and why the community has been arguing about the wrong thing for years.

## What Is This?

The Call of Duty community has spent nearly a decade screaming about SBMM (Skill-Based Matchmaking). The problem is, SBMM has been in every COD since 2007. The thing actually causing the "yo-yo" effect, where you swing between easy and hard lobbies every other match, is MMR (Matchmaking Rating), a separate dynamic rating system added in 2016 with Infinite Warfare.

Nobody in the COD creator space has ever built anything that shows this. They just shout about it.

This simulator lets you see it for yourself.

## What It Does

Five simulation modes running against a pool of up to 2,000,000 players so you can compare them directly. Scale the pool down to 100,000 to see what happens at off-peak hours.

**SBMM Only (Pre-2016)**: How matchmaking worked before MMR existed. Stable brackets, predictable lobbies, no rubber-banding. Connection is king here, ping gets priority over skill matching.

**SBMM + MMR (2016 to Present)**: The current system. Watch your MMR bounce after every match and see the yo-yo pattern form in real time. Adjust the MMR aggressiveness slider and watch it get worse. The yo-yo hits hardest at mid-tier (skill 66), is dampened for casuals (skill 33), and is visible but compressed for top-tier players (skill 100). Connection quality takes a back seat to skill matching, which is why you end up in 80-90ms lobbies when the algorithm is chasing your MMR target.

**Open Matchmaking (BO7 Launch to Season 4)**: SBMM dialled back, skill "minimally considered." MMR still running underneath. The yo-yo doesn't stop. Activision's own data: 32.7% higher quit rates, 59.2% more "Not Fun" ratings.

**Classic Matchmaking (BO7 Season 5 / MW4)**: Persistent lobbies "inspired by" BO1 and BO2. Feels better because you adapt to your opponents. MMR still running underneath. It's a placebo.

**No SBMM (What the Community Is Actually Asking For)**: Complete removal of all skill-based matchmaking. No brackets, no MMR, pure connection-based lobbies on dedicated servers. No yo-yo, but no protection either. A 0.66 KD casual can land in a lobby with a 2.0 KD grinder, and it happens regularly. This isn't better matchmaking. It's no matchmaking.

Run any two modes side-by-side and watch the same players produce completely different experiences under different systems.

## System Settings

**Persistent Lobbies**: Toggle lobby persistence on for any mode. When enabled, lobbies carry players between matches instead of disbanding and rebuilding from scratch every time. Mode 4 (Classic) always has this on. With persistence off in MMR modes, the matchmaker rebuilds all 12 players every match, which drives queue times up and lets the algorithm re-optimise your lobby around your latest rating. With persistence on, it backfills a few empty slots and leaves the rest alone. Faster queues, familiar faces, but the lobby composition reflects where you were, not where the system thinks you are now.

**6-Stack Party**: Queue as a full party of six. Your five teammates are matched to your MMR and stay with you across all 30 matches. Works with or without persistent lobbies, because your party is your party regardless of what happens to the other six players in the lobby.

**MMR Aggressiveness**: Controls how hard the rating system reacts to each match result. Higher values produce bigger swings and a more violent yo-yo. Affects Modes 2, 3, and 4 only. Modes 1 and 5 have no MMR.

**Player Pool**: Scale the population from 2,000,000 down to 100,000. Smaller pools produce longer queue times, wider skill ranges in lobbies, and worse ping spread, especially in strict MMR modes where the algorithm has fewer valid candidates to pull from.

## Queue Time Model

Queue times aren't flat estimates anymore. They factor in pool size, mode strictness, lobby persistence, and how far your skill sits from the centre of the bell curve. In Mode 2 at skill 50 with a full pool, you're looking at around 15 seconds. Push that skill to 90 and it climbs past 30. Drop the pool to 250,000 at skill 90 and you're waiting minutes. That's the 2am experience. Persistent lobbies cut queue times because the system is backfilling slots, not rebuilding from nothing.

## Ping and Connection Model

The ping distribution across the player pool reflects real-world connection quality. 15% of players sit under 25ms on good fibre near a data centre. 40% are between 25 and 60ms on decent broadband. 25% sit at 55 to 100ms. The rest tail out past 130ms for rural connections and bad ISP routing. Cross-region matchmaking adds 80 to 140ms on top.

How much the matchmaker cares about ping depends on the mode. Mode 1 (SBMM Only) prioritises connection heavily. Mode 2 (SBMM + MMR) sacrifices connection quality to chase skill targets, which is why you end up in high-ping lobbies when your MMR narrows the candidate pool. The ping spread stat measures the average within-lobby standard deviation, showing how mixed the connections are in your actual matches.

## The "You" Player

One player in the pool is highlighted as "You." Set your own starting skill, KD, region, input device, and ping, then watch how each matchmaking system treats you differently across 30 matches.

## How The MMR Model Works

The simulator uses a Glicko-style MMR system on a 1 to 200 internal scale with a K-factor that scales based on population position. Players near the skill average (skill 50) experience the full force of MMR adjustments. Players at the extremes, both casual and elite, get dampened adjustments, which is why the yo-yo hits the mid-tier majority the hardest. The expanded scale gives top-tier players headroom above their starting MMR, so the system can push them up after a good performance and pull them back down, producing the compressed but visible yo-yo pattern that high-skill players actually experience.

This matches the real-world pattern: casuals barely notice, the mid-tier majority gets whiplash, and the top tier gets locked in a box with no variety.

## How To Use It

1. Download `SBMMSIM.html`
2. Open it in your browser
3. That's it

No installation. No dependencies. No internet connection required. Works offline, works on any modern browser.

Pick a mode, hit Run, and watch 30 matches simulate. Adjust the MMR aggressiveness slider in Mode 2 to see how volatility changes the yo-yo pattern. Toggle persistent lobbies to see how lobby carry-over affects queue times, fairness perception, and player retention. Use the Compare feature to run two modes side-by-side with the same player pool. Use the Skill Tiers view to see how the same system treats a casual, a mid-tier grinder, and a top-tier player completely differently.

## What This Is Based On

This simulator doesn't use Activision's proprietary source code. Nobody outside Activision has access to that.

What it does use:

- Activision's published matchmaking whitepapers (2024), specifically "Matchmaking Series: The Role of Skill in Matchmaking" which confirmed skill is calculated from Match Total Kills, Kill/Death Ratio, and Kills/(Deaths by Enemy)
- Activision's matchmaking patent (US 10,322,351), which describes the framework for optimising player matches using historical data
- Publicly available information from Charlie Olson, former Raven Software developer who wrote the MMR algorithm for COD Online (China, 2015) before it was added to Infinite Warfare (2016) and every title since
- TrueSkill research by Microsoft Research (Herbrich et al., 2006), the Bayesian rating system used in Xbox Live matchmaking
- Glicko-2 rating system mathematics for handling rating uncertainty and volatility
- Activision's published statistics on Open Matchmaking outcomes (32.7% higher quit rates, 14.4% fewer KPM, 5.3% lower win rates, 59.2% more "Not Fun" ratings for 80% of BO7 players)

The formulas approximate how these systems behave based on publicly documented principles. The simulation demonstrates the patterns, not the exact proprietary implementation.

## Why This Exists

Because even journalists who interview the developer who built the system can't tell the difference between SBMM and MMR. Because creators with millions of subscribers keep demanding SBMM be removed when it's been there since 2007. Because Activision has tested loosening SBMM three separate times, and every time it "failed" because they never touched MMR, and nobody noticed.

If you want the matchmaking argument to go anywhere productive, you need to understand what you're actually arguing about. This tool shows you.

## Built By

**Scotty McGaming**

YouTube: [youtube.com/@ScottyMcGaming](https://youtube.com/@ScottyMcGaming)

## Licence

MIT. Do what you want with it. If you use it in your own content, a credit would be appreciated but isn't required.
