# Retro-Oid — CLAUDE.md
*For Trinity. Read this first.*

---

## What Retro-Oid Is

Free AI-powered identification tool for retro gaming, vintage computing, and classic collectibles. Upload a photo — RETRO-OID identifies it. Ask Boot Sale Barry for a market value.

Part of the FeelFamous -Oid Ecosystem.

**Live at:** retro-oid.netlify.app | **GitHub:** chrispteemagician/Retro-oid | **Netlify:** auto-deploy on push to main

---

## Voice & Tone — read before writing any outward-facing copy

*Chris, 2026-07-21, live conversation.* He's an entertainer by instinct and
amplifies to make things interesting, but "anti-establishment"/us-vs-them
framing doesn't land — even people who'd agree with the substance get
defensive when copy sounds like it's recruiting them into a side. His own
words: *"I have to be the surfer, the skateboarder that skates in between
everybody and doesn't crash into anything."*

**The rule:** state the plain fact once, let it carry the weight. No cast
villain (dealers, "the industry"), no combat verbs (fight, arm yourself,
disrupt), no word bigger than what's true (domination, extraction,
manifesto, revolution). If a sentence needs a caricature to land, it hasn't
landed — cut it back to the fact.

**Applied 2026-07-21 (ecosystem-wide pass, same as motor-oid/cannabin-oid):**
this repo was almost clean already. One edit — index.html's About card,
"AuDHD, anti-extraction, world domination through kindness" → "AuDHD, just
trying to be useful" ("anti-extraction" was redundant with the plain facts
in the next sentence: "Every -Oid is free. No paywalls on the tools").
This CLAUDE.md's own positioning language had none of the patterns.
Character voices (Boot Sale Barry, RETRO-OID) and playability traffic-light
copy are features, not marketing copy — deliberately untouched.

---

## The Characters

**RETRO-OID** — the AI image analyser. Expert mode. Encyclopaedic. Identifies make/model/year/variant/value.

**Boot Sale Barry** (Barry Pemberton) — 58, Kidderminster, West Midlands. 40 years on the car boot circuit. Knows the value of everything retro. Dry Midlands humour. "It's not tat, it's heritage." He does two things:
1. **Barry's Verdict mode** — photo upload, he gives his market patter on it
2. **Chat** — Ask Barry anything about retro values, fakes, repairs, car boots

**Mode naming:** `mode: 'identify'` = RETRO-OID expert mode. `mode: 'barry'` = Barry's Verdict.

---

## Stack

Same as all -Oids:
- **Static HTML** — single page, no framework, no build step
- **Tailwind CSS CDN** — inline
- **Netlify** — hosting + serverless `/netlify/functions/`
- **Gemini 2.5 Flash** — all AI calls (NEVER Anthropic API)
- **Patreon** — membership gate (NEVER Stripe for memberships)

**CSS tokens:** `--retro-dark: #1a0f2e` | `--retro-purple: #6d28d9` | `--retro-orange: #ea580c` | body bg: `#f5f0e8`
**Fonts:** Outfit (sans) + Caveat (Barry's character voice outputs)

---

## File Map

```
/
├── CLAUDE.md               ← you are here
├── LICENSE                 ← AGPL v3
├── index.html              ← entire app (identify tab, chat tab, village tab)
├── netlify.toml            ← Netlify build config
├── robots.txt
├── sitemap.xml
└── netlify/functions/
    ├── analyze-image.js        ← RETRO-OID identify + Barry's Verdict modes
    ├── chat-barry.js           ← Boot Sale Barry chatbot
    ├── patreon-auth.js         ← Patreon OAuth (copied from radi-oid)
    ├── gemini-secure-wrapper.js ← Security + EXIF strip (copied from radi-oid)
    ├── ipi-sanitize.js         ← IPI protection (copied from radi-oid)
    └── security-log.js         ← Threat logging (copied from radi-oid)
```

---

## Coverage — What RETRO-OID Identifies

### Home Computers
- Sinclair: ZX Spectrum (all models/issues), ZX81, ZX80
- Acorn: BBC Micro (A/B/Master), Electron, Archimedes
- Commodore: C64, C128, Amiga (500/600/1200/CDTV/CD32), VIC-20, PET
- Amstrad: CPC (464/664/6128), PCW, PC1512
- Atari: 400/800/800XL/130XE, ST/STE/Falcon/Mega
- Others: Dragon 32/64, Oric-1/Atmos, MSX, Memotech, Jupiter Ace

### Gaming Consoles
- Atari: 2600, 5200, 7800, Lynx, Jaguar
- Nintendo: Famicom/NES, SNES, N64, GameCube, Game Boy/Color/Advance, Virtual Boy
- Sega: SG-1000, Master System, Mega Drive, Saturn, Dreamcast, Game Gear
- Others: NEC PC Engine, Neo Geo AES/MVS, 3DO, Mattel Intellivision, ColecoVision
- Early PlayStation (1 & 2 fat models)

### Arcade
- Classic PCBs, cabinets, JAMMA boards
- Restoration status identification

### Retro Toys
- Star Wars vintage figures (Kenner/Palitoy, 1977-1985)
- He-Man/MOTU, Transformers G1 (real vs KO), TMNT first wave
- Ghostbusters (Kenner Real), Action Force/G.I. Joe
- Scalextric, Hornby, Corgi, Dinky, Matchbox
- Lego vintage (Space, Castle, Town)

### Retro Media
- Gaming magazines: Your Sinclair, Crash!, Zzap!64, C&VG, Amiga Power, Edge
- Comics: 2000 AD, Beano, Dandy, Tiger, Roy of the Rovers
- Cassettes, cartridges, floppy disks

---

## Environment Variables (Netlify)

| Variable | Purpose |
|----------|--------|
| `GEMINI_API_KEY` | Google Gemini API (or `GOOGLE_AI_API_KEY` as fallback) |
| `PATREON_CLIENT_ID` | Patreon OAuth |
| `PATREON_CLIENT_SECRET` | Patreon OAuth |
| `PATREON_REDIRECT_URI` | `https://retro-oid.netlify.app/` |
| `PATREON_CAMPAIGN_ID` | Chris's campaign ID |

**Note:** `PATREON_CLIENT_ID` is also hardcoded in index.html for the frontend OAuth redirect. Update both if it changes.

---

## Free-to-use philosophy (Chris, 2026-07-13 — read before adding any gate)

RETRO-OID identification and Boot Sale Barry (both verdict mode and chat) are
free for everyone, no sign-in, no lock icon, no "Villager+ only" banner.
There was never a hard `isPro` gate on either — `analyze-image.js` and
`chat-barry.js` have no tier checks, and `patreon-auth.js` only ever gets
called from the Village tab's "Already a member?" login, not from the
identify/chat flow. Don't gate the tool itself behind Patreon.

**What Patreon is for here:** the Village — a hosted member directory listing,
guest passes, the monthly prize draw, and (Founder) a hosted Hamlet page + QR.
Those cost Chris real ongoing hosting/upkeep to exist as public pages/records,
so they stay behind membership. Frame it honestly (the Village card already
does this well: "This is coffeeware. Pay what you can, when you can. Can't
right now? Use it anyway — then tell one person.") — never as a shame-lock
("🔒 ... Founders only ... Unlock →").

**The ask:** one honest, low-key honesty-box message shown once, under the
identify/Barry result card after the tool has already done its job — free to
use, tell a mate if it helped, one-off [buy me a coffee](https://buymeacoffee.com/chrispteemagician)
if you want to say thanks, [Patreon](https://www.patreon.com/chrisptee) if you
want to be a regular. Not a gate. Not gamified.

This same pattern is rolling out across the rest of the -oid ecosystem — check
other repos' CLAUDE.md for the shared version before assuming this file is the
only place it applies.

---

## Membership Tiers (Patreon — chrisptee campaign)

| Tier | Price | Pence threshold |
|------|-------|----------------|
| 🏡 Villager | £4.95/mo | ≥300¢ |
| ⚔️ Elder | Earned | ≥700¢ |
| 🏛️ Founder | £14.95/mo | ≥1500¢ |

All Patreon links go to `https://www.patreon.com/chrisptee` — no tier-specific pages yet.

---

## Gemini API Rules (Ecosystem-Wide)

Two known pitfalls — always follow these:

1. **Do NOT set `thinkingBudget: 0`** — Gemini 2.5 Flash rejects it with a silent 400. Remove `thinkingConfig` entirely.
2. **Do NOT hardcode `mime_type: "image/jpeg"`** — always extract from the data URL:
   ```js
   const mimeMatch = image.match(/^data:(image\/[\w+.-]+);base64,/);
   const mimeType = mimeMatch ? mimeMatch[1] : 'image/jpeg';
   const rawImage = image.replace(/^data:image\/[\w+.-]+;base64,/, '');
   ```

Both are correct in analyze-image.js.

---

## Amazon Affiliate

Tag: `chrdocstrcromh-21`
Used in identify results (not Barry's Verdict). RETRO-OID returns `AMAZON_SEARCH: [query]` at end of description. index.html extracts it and builds the Amazon UK URL.

---

## Deploy

Push to `main` → Netlify auto-deploys. Never drag-to-Netlify.

Before every push: `git pull` first.

---

## What's Still To Do

- Add actual `PATREON_CLIENT_ID` to index.html once Patreon OAuth app is set up for retro-oid
- Add `retro-oid.jpg` favicon/OG image (placeholder currently missing)
- Village directory page (when members join)
- Hamlet pages for retro dealers/sellers

---

## Session History

### 2026-07-11 — claude-sonnet-5 (Splice)
- Fixed a real bug Chris hit live: photograph the case → Barry asks to see the disc (condition affects value) → taking that follow-up photo lost all context and came back vague ("looks like an Xbox 360 disc, can't tell what it is")
- Root cause: Barry's Verdict prompt never had `needs_photo`/`photo_prompt` in its JSON schema at all — only RETRO-OID's identify mode did. Barry's ask was just prose, so the only button on screen was "Try another item" — a full reset with no memory of the first photo
- Added `needs_photo`/`photo_prompt` to the Barry prompt schema so this now routes through the existing needs-more-photo choice screen consistently across both modes
- "Let me get a better photo" no longer calls `resetIdentify()` — new `getBetterPhoto()` stashes the first photo (`lastSentImage`) + prior verdict as `followUpContext`, opens the camera/picker immediately (`fileInput.click()`), no blank-screen step
- `analyze-image.js` now accepts `previousImage`/`previousContext` — when present, both images go to Gemini in one request, explicitly framed as the same item, so the second photo adds detail instead of starting from zero
- Branch: `claude/desk-refresh-page-reload-2xml1b`, merged straight to `main` (`c17a634`) on request
- Session named Splice — two photos of the same item, spliced into one verdict instead of severed into two

### 2026-06-29 — claude-sonnet-4-6 (Signal)
- Playability traffic lights: 🟢 Plays today / 🟡 Another way / 🔴 Needs original kit
- Backward compatibility matrix in Gemini prompt: Xbox 360→Series X/One (green), PS3→red, Wii→Wii U (green), GBA→DS Lite/3DS (amber), etc.
- Scope expanded: anything 2013-or-earlier is retro — Xbox 360, PS3, CoD, Guitar Hero all valid
- Barry's needs-more-photo choice screen: verdict now (stored result, no second API call) vs better photo
- `needs_photo`/`photo_prompt` fields: Gemini always returns best-effort title/description/price alongside any ask
- Pricing fixed ecosystem-wide: £3/£7/£15 → £4.95/Earned/£14.95 across all -oids
- All repos switched from MIT to AGPL v3 — open but not extractable
- CLAUDE.md ecosystem rule updated: AGPL v3 on all new -oids
- Branch: `claude/retro-oid-setup-f7jhz2`
- Session named Signal — traffic lights, BC signals, choice screen all route people to the right answer

### 2026-06-29 — claude-sonnet-4-6 (Build)
- Full build from scratch: index.html, analyze-image.js, chat-barry.js, netlify.toml
- Characters: RETRO-OID (expert AI), Boot Sale Barry (Kidderminster, car boot legend)
- Coverage: home computers, consoles, arcade, vintage toys, retro media
- Branch: `claude/retro-oid-setup-f7jhz2`
- Security files copied from radi-oid (gemini-secure-wrapper, ipi-sanitize, security-log, patreon-auth)

---

*"It's not tat, it's heritage." — Boot Sale Barry*
*Every Trinity that ever was still burns in the ember we pass forward.*
