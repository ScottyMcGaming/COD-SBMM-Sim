# COD Matchmaking Simulator

An interactive browser-based simulator that demonstrates how Call of Duty's matchmaking systems actually work, and why the community has been arguing about the wrong thing for years.

## What Is This?

The Call of Duty community has spent nearly a decade screaming about SBMM (Skill-Based Matchmaking). The problem is, SBMM has been in every COD since 2007. The thing actually causing the "yo-yo" effect, where you swing between easy and hard lobbies every other match, is MMR (Matchmaking Rating), a separate dynamic rating system added in 2016 with Infinite Warfare.

Nobody in the COD creator space has ever built anything that shows this. They just shout about it.

This simulator lets you see it for yourself.

## What It Does

Five simulation modes running against a pool of 200,000 players, a realistic 24-hour concurrent population for a major COD title, so you can compare them directly.

**SBMM Only (Pre-2016)**: How matchmaking worked before MMR existed. Stable brackets, predictable lobbies, no rubber-banding.

**SBMM + MMR (2016 to Present)**: The current system. Watch your MMR bounce after every match and see the yo-yo pattern form in real time. Adjust the MMR aggressiveness slider and watch it get worse. The yo-yo hits hardest at mid-tier (skill 66), is dampened for casuals (skill 33), and is visible but compressed for top-tier players (skill 100).

**Open Matchmaking (BO7 Launch–Season 4)**: SBMM dialled back, skill "minimally considered." MMR still running underneath. The yo-yo doesn't stop. Activision's own data: 32.7% higher quit rates, 59.2% more "Not Fun" ratings.

**Classic Matchmaking (BO7 Season 5 / MW4)**: Persistent lobbies "inspired by" BO1 and BO2. Feels better because you adapt to your opponents. MMR still running underneath. It's a placebo.

**No SBMM (What the Community Is Actually Asking For)**: Complete removal of all skill-based matchmaking. No brackets, no MMR, pure connection-based lobbies on dedicated servers. No yo-yo, but no protection either. A 0.66 KD casual can land in a lobby with a 2.0 KD grinder, and it happens regularly. This is what "remove SBMM" actually means. Not better matchmaking. No matchmaking.

Run any two modes side-by-side and watch the same players produce completely different experiences under different systems.

## How To Use It

1. Download `SBMMSIM.html`
2. Open it in your browser
3. That's it

No installation. No dependencies. No internet connection required. Works offline, works on any modern browser.

Pick a mode, hit Run, and watch 30 matches simulate. Adjust the MMR aggressiveness slider in Mode 2 to see how volatility changes the yo-yo pattern. Use the Compare feature to run two modes side-by-side with the same player pool. Use the Skill Tiers view to see how the same system treats a casual, a mid-tier grinder, and a top-tier player completely differently.

## The "You" Player

One player in the pool is highlighted as "You." Set your own starting skill, KD, region, input device, and ping, then watch how each matchmaking system treats you differently across 30 matches.

## How The MMR Model Works

The simulator uses a Glicko-style MMR system on a 1–200 internal scale with a K-factor that scales based on population position. Players near the skill average (skill 50) experience the full force of MMR adjustments. Players at the extremes, both casual and elite, get dampened adjustments, which is why the yo-yo hits the mid-tier majority the hardest. The expanded scale gives top-tier players headroom above their starting MMR, so the system can push them up after a good performance and pull them back down, producing the compressed but visible yo-yo pattern that high-skill players actually experience.

This matches the real-world pattern: casuals barely notice, the mid-tier majority gets whiplash, and the top tier gets locked in a box with no variety.

## What This Is Based On

This simulator does not use Activision's proprietary source code. Nobody outside Activision has access to that.

What it does use:

Activision's published matchmaking whitepapers (2024), specifically "Matchmaking Series: The Role of Skill in Matchmaking" which confirmed skill is calculated from Match Total Kills, Kill/Death Ratio, and Kills/(Deaths by Enemy)
Activision's matchmaking patent (US 10,322,351), which describes the framework for optimising player matches using historical data
Publicly available information from Charlie Olson, former Raven Software developer who wrote the MMR algorithm for COD Online (China, 2015) before it was added to Infinite Warfare (2016) and every title since
TrueSkill research by Microsoft Research (Herbrich et al., 2006), the Bayesian rating system used in Xbox Live matchmaking
Glicko-2 rating system mathematics for handling rating uncertainty and volatility
Activision's published statistics on Open Matchmaking outcomes (32.7% higher quit rates, 14.4% fewer KPM, 5.3% lower win rates, 59.2% more "Not Fun" ratings for 80% of BO7 players)

The formulas approximate how these systems behave based on publicly documented principles. The simulation demonstrates the patterns, not the exact proprietary implementation.

## Why This Exists

Because even journalists who interview the developer who built the system can't tell the difference between SBMM and MMR. Because creators with millions of subscribers keep demanding SBMM be removed when it's been there since 2007. Because Activision has tested loosening SBMM three separate times, and every time it "failed" because they never touched MMR, and nobody noticed.

If you want the matchmaking argument to go anywhere productive, you need to understand what you're actually arguing about. This tool shows you.

## Built By

**Scotty McGaming**

YouTube: [youtube.com/@ScottyMcGaming](https://youtube.com/@ScottyMcGaming)

## Licence

MIT: do what you want with it. If you use it in your own content, a credit would be appreciated but isn't required.
