# FallFlip

**The mirror. Someone self-promotes on your LinkedIn post? Flip it. Proportional response on their post AND yours.**

One HTML file. Opens in any browser. Data on your device. No login, no subscription.

**Live:** https://sjgant80-hub.github.io/fallflip/

---

## The rule

> Only flip when they started it. This is a mirror, not an attack.
> They brought their product to your audience → you bring yours to theirs.
> Fair game. They set the rules. You play by them.

---

## What it does

1. **Paste their comment** + their profile URL + (optional) their latest post topic
2. **FallFlip analyses** — spam level 1-5, archetype, their product, their domain
3. **Generates two responses** — proportional to the spam level
   - **Reply** for YOUR post (kills their promo, redirects to your content)
   - **Counter-comment** for THEIR post (subtly promotes your work on their turf)
4. **Optional DM** — for escalation when level is 4-5 or repeat offender

Copy buttons on each output. Done in under a minute, on a phone, between meetings.

---

## The 5 levels

| Level | Archetype | Example |
|-------|-----------|---------|
| 1 | Subtle nudge | "Interesting that you're working in this space too..." |
| 2 | Soft plug | "We do similar work at..." |
| 3 | Direct promo | "I built X which solves this!" |
| 4 | Spam/irrelevant | "Great post! 🔥 BTW check out my..." |
| 5 | Pure bot | "Nice insight 🔥 visit mylink.com" |

Templates are calibrated per level. Level 1 is generous-but-redirect. Level 5 exposes-and-redirects.

---

## Tone — what FallFlip will and will not do

**Never:**
- aggressive, hostile, personal
- threats to report
- passive-aggressive ("I'm sure you didn't mean to...")
- sarcasm that makes YOU look petty

**Always:**
- professional enough for a CFO to read
- sharp enough that the spammer knows you noticed
- valuable enough that other readers benefit
- specific enough to show you actually know the domain

**The goal:** when someone else reads the exchange, they think *"oh, Simon's tool actually does solve that differently"* — not *"Simon's being petty."*

---

## Examples

**Spam input:**
> "Great insights Simon! 🔥 We've built an AI-powered CRM at SalesBot.io that automates exactly this. Check it out!"

**Reply (on your post):**
> "Appreciate the mention of SalesBot.io. Different approach to the same problem — FallForce is a sovereign CRM: one HTML file, no subscription, data on-device. Worth a look if cloud-hosted doesn't fit the use case."

**Counter (on their post about 'automating sales pipelines'):**
> "Solid take on automating sales pipelines. One angle that doesn't always come up: sovereignty. I've been building FallForce — runs as a single HTML file, data on-device, no subscription. Curious whether your approach handles the offline / regulated-environment edge cases."

The point isn't to "win" the exchange. It's to **redirect attention** while adding genuine value, so readers walk away knowing both tools exist and what makes yours different.

---

## How to use it

### On your phone (Simon's primary use case)

1. Open `https://sjgant80-hub.github.io/fallflip/`
2. Add to home screen — looks like an app, opens in 200ms
3. When you spot a spam comment on LinkedIn:
   - Copy the comment text
   - Copy their profile URL
   - Paste both into FallFlip
   - Tap **Flip it**
   - Copy the reply → paste back on LinkedIn → done
4. Optional: tap the counter, navigate to their latest post, paste it as your comment there
5. Optional: blacklist them if they're a repeat offender — next time uses harsher templates automatically

### First-time setup (Settings → cog icon)

- Set your name (used to personalise)
- Set your LinkedIn profile URL
- Set your **default tool** to mention — choose from FallForce, FallBrief, FallAccount Trades, AudioFabric, GymOS, Apex, FallCore (or which tool fits the spam domain — auto-selected)
- Optional: paste a free Gemini API key for sharper AI-enhanced responses

---

## Sovereignty

- All data lives on your phone (localStorage)
- Spam log, blacklist, whitelist — all on-device
- Export JSON backup anytime
- No server, no telemetry, no signup, no monthly fee
- Works offline once loaded (T0 templates always available)
- Optional Gemini key for AI sharpening — even then, the call goes direct from your phone to Google, never via our infra (because there is no infra)

---

## How it's built (for developers)

### Architecture

- **Single HTML file** — ~52 KB, no build step, no dependencies
- **Vanilla JS** — no React, no Vue
- **localStorage** for persistence
- **BroadcastChannel** `fall-signal` for mesh interop (prime 211)
- **Konomi licence shim** baked in (sovereign tier)
- **Optional Gemini Vision/Text** (T3 cascade)

### 7-layer breakdown (v19 spec)

| Ring | Role | Implementation |
|------|------|----------------|
| L1 FACE | input → analysis → 2 outputs + optional DM | left panel input, right panel output |
| L2 SWARM | Ω + 4 agents | α analyser · β reply · γ counter · δ tone/DM |
| L3 CASCADE | T0 always | template tables per spam level; T3 Gemini optional |
| L4 BLOOM | routing | comment → level + archetype + domain → template lookup |
| L5 PERSIST | localStorage | log · blacklist · whitelist · settings · JSON export |
| L6 SKIN | mobile-first | dark `#1a1a17` + amber `#e8a012` · one-thumb |
| L7 ASS | empty state | "Paste their comment, hit Flip it" — no setup wizard |

Cross-tool interop: `BroadcastChannel('fall-signal')` · prime **211** · hello on boot.

### Files

```
fallflip/
├── index.html        # 52 KB · the deliverable
├── README.md         # this file
├── LICENSE           # MIT
└── .gitignore
```

### Fork & customise

```bash
gh repo fork sjgant80-hub/fallflip --clone=true
cd fallflip
# Customise state.tools array in index.html to YOUR product list
# Update yourName / yourProfile defaults
gh repo edit --enable-pages --pages-branch main
git push
```

### Verify before deploy

```bash
node -e "
const html = require('fs').readFileSync('index.html', 'utf8');
console.log('size:', (html.length/1024).toFixed(1), 'KB');
const code = html.substring(html.lastIndexOf('<script>') + 8, html.lastIndexOf('</script>'));
new Function(code);
console.log('parses: ok');
"
```

---

## Roadmap

- ✅ Core: paste → analyse → reply + counter + optional DM
- ✅ 5-level spam detection (offline regex)
- ✅ Tool auto-selection based on spammer's domain
- ✅ Repeat-offender blacklist
- ✅ Optional Gemini AI sharpening
- ✅ Log + JSON export
- ⬜ Browser extension version (right-click → "Flip this")
- ⬜ Bulk mode (paste a list of recent spam, flip the whole batch)
- ⬜ Stats dashboard (most common spammers, levels over time)
- ⬜ Whitelist auto-conversion (spammer engages genuinely → soften templates)

---

## Licence

MIT — see [LICENSE](LICENSE). Use it, fork it, customise the templates for your voice and your tool list.

---

## Credit

- **Architecture & build:** Simon Gant · [@sjgant80-hub](https://github.com/sjgant80-hub) · [LinkedIn](https://www.linkedin.com/in/simon-gant-295b56180/)

◊·κ=1 · the mirror · proportional · profitable · they brought their product to your audience · you bring yours to theirs · the flip is the moat
