# Flow Automation — design reference

Two sources, deliberately split:

- **Layout, geometry, and type** come from **https://replymer.com/**, extracted with dembrandt
  on 2026-08-24 — pill controls, 14px cards, hairline borders, soft elevation, Poppins 800
  display, and the section rhythm.
- **Colour and artwork** come from **the extension itself** —
  `extension/src/ui/side-panel/styles.css` and `store/chrome/generated-assets/` in
  `D:\Code Project\Extensions\Google Flow Automation`.

Everything is implemented in [`assets/site.css`](assets/site.css).

## Colour

Light surfaces use the extension's **light theme**; dark bands use its **dark theme**.

| Token | Value | Source | Use |
| --- | --- | --- | --- |
| `--white` | `#ffffff` | ext light `--surface` | Page surface |
| `--soft` | `#f7f4ee` | ext light `--background` | Alternating section band |
| `--soft-2` | `#f0ebdf` | ext light `--surface-2` | Inline code, FAQ badge |
| `--edge` | `#ebe4d6` | ext light `--muted` | Hard dividers |
| `--line` | `rgba(36,31,22,.12)` | ext light `--line-soft` | Every card/button border |
| `--ink` | `#241f16` | ext light `--foreground` | Headings |
| `--body` | `#585044` | ext light `--foreground-2` | Body copy (7.0:1 on white) |
| `--muted` | `#867c6a` | ext light `--muted-fg` | Meta / captions |
| `--primary` | `#008a76` | ext light `--primary` | Buttons, links, eyebrows on light |
| `--primary-700` | `#00705f` | derived | Primary hover |
| `--primary-fg` | `#f4fffc` | ext light `--primary-fg` | Text on primary |
| `--teal` | `#00e3c0` | ext `--brand-teal` | Glow + accents **on dark only** |
| `--teal-soft` | `#00d3b3` | ext `--brand-teal-soft` | Glow hover |
| `--sky` | `#38bdf8` | ext `--sky` | Running state |
| `--pop` | `#a78bfa` | ext `--pop` | Tertiary accent |
| `--success` | `#4ade80` | ext `--success` | Success |
| `--warning` | `#ffb020` | ext `--warning` | Window dot |
| `--coral` | `#ef4444` | ext `--danger` | Window dot, campaign emphasis |
| `--night` | `#060607` | ext `--background` | Footer, closing CTA |
| `--night-2` | `#0a0a0d` | ext `--surface` | Dark surface fill |
| `--night-3` | `#0e0e11` | ext `--surface-2` | Dark gradient end |
| `--night-fg` | `#eeeef1` | ext `--foreground` | Text on dark |
| `--night-fg-2` | `#c6c7ce` | ext `--foreground-2` | Secondary text on dark |
| `--night-muted` | `#9a9aa6` | ext `--muted-fg` | Meta on dark |

Composites: `--grad-brand` `linear-gradient(96deg,#008a76,#00c4a6)` (light),
`--grad-glow` `linear-gradient(96deg,#00e3c0,#38bdf8)` (dark),
`--tint-teal` `linear-gradient(160deg,#edfbf7,#fff)`,
`--tint-warm` `linear-gradient(160deg,#fbf7ef,#fff)`,
`--dark` `linear-gradient(140deg,#060607,#0e0e11)`.

**The one rule that matters:** `#00e3c0` is the brand teal but measures ~1.6:1 on white — it
is a *dark-surface* colour only. On light surfaces always use `--primary` `#008a76`
(4.9:1 on white, AA for normal text, and 4.7:1 white-on-teal for button labels). This is the
same split the extension itself makes between its dark and light themes.

## Type

Poppins (Google Fonts, variable) with an `-apple-system` fallback stack. Panel/mono details
use the extension's stack: `ui-monospace, "JetBrains Mono", "Cascadia Mono", Menlo`.

| Role | Size | Weight | Tracking | Leading |
| --- | --- | --- | --- | --- |
| `.display` | `clamp(2.4rem, 5.2vw, 4.4rem)` | 800 | `-0.035em` | 1.06 |
| `.h2` | `clamp(1.85rem, 3.4vw, 2.5rem)` | 800 | `-0.02em` | 1.2 |
| `.h3` | `1.45rem` | 700 | `-0.02em` | 1.35 |
| `.lead` | `1.13rem` | 400 | — | 1.6 |
| body | `1.03rem` | 400 | — | 1.6 |
| `.eyebrow` | `0.72rem` | 700 | `0.06em`, uppercase | — |

## Surfaces

- Container: `.wrap` is **1120px** with `24px` side padding — the reference's exact width.
- Radii: `10px` step badges, `14px` cards, `16px` tour shots, `18px` the lead shot, `100px` pills.
- Borders: a single `1px solid rgba(36,31,22,.12)` on light, `rgba(154,154,166,.20)` on dark.
- Elevation: `0 2px 12px rgba(36,31,22,.06)` at rest, `0 18px 44px rgba(36,31,22,.14)` on
  hover, `0 30px 70px -30px rgba(6,6,7,.55)` under dark frames, plus a teal bloom
  `0 24px 60px -20px rgba(0,227,192,.28)` on the lead panel mockup.
- Spacing: 8px scale; sections `84px` desktop → `64px` under 820px.

## Assets

Sourced from the extension repo and converted for the web with ffmpeg.

| File | Source | Notes |
| --- | --- | --- |
| `assets/logo-128.png` | `logo_128x128.png` | Nav + footer brand mark, favicon, apple-touch-icon (6.5 KB) |
| `assets/flowbot.webp` | `store/.../final/flowbot-mascot.png` | Closing-CTA mascot, transparent, 620px wide (54 KB from 1.0 MB) |
| `assets/shots/1–5-*.webp` | `store/.../final/screenshots-1280x800/` | 1 lead shot + 4 tour shots, native 1280px (~95 KB each from ~1.5 MB) |
| `assets/shots/dashboard-concept.webp` | Codex-generated mockup | **Lead hero shot.** Concept dashboard, 1672x941 (16:9, renders 978x551 — matches the reference's 978x546). Concept UI branded "Automator"; the metrics shown are illustrative, not live product data. |
| `assets/avatars/*.webp` | randomuser.me | **Placeholder** portraits for the avatar stack — replace before launch |
| `assets/family/*.webp` | sibling site + extension icons | Family pills (24px) and avatar stack (46px) in the hero |
| `assets/chrome-logo.svg`, `assets/edge-logo.svg` | `extension/src/assets/` | Real browser marks in the hero rail (22px) and store buttons (28px) |
| `assets/og-marquee.jpg` | `store/.../final/promo/marquee-promo-tile-1400x560.png` | `og:image` / `twitter:image` (165 KB from 1.0 MB) |

Regenerate with `ffmpeg -i <src> -vf "scale=<w>:-1:flags=lanczos" -c:v libwebp -q:v 80 -preset picture <dst>`
(drop `-vf` for the screenshots — they ship at their native 1280px so wide viewports never upscale).

## Motion

Buttons and cards lift `translateY(-2px … -3px)` on hover; the closing-CTA Flowbot floats on
a 6s loop. Section content fades up via `.reveal` + IntersectionObserver, with a 1.6s failsafe so
content can never stay at opacity 0. Everything stops under `prefers-reduced-motion: reduce`.

## Breakpoints

`1100px` (3-col → 2-col) · `900px` (nav links hide, store buttons stack) · `820px` (section
padding drops) · `640px` (grids single-column) · `480px` (compact padding, steps stack).

## Page structure

`index.html` copies Replymer's section order **and its measured layout**, minus the parts Flow
Automation has no honest content for (no testimonials, no customer logos, no pricing —
listings are still in review):

1. Sticky nav — logo · centred links · Contact + primary CTA
2. Hero — **single centred column, text only**: chip → headline → sub → CTAs → family pills →
   avatars → proof line. One row per slot, same as the reference. No image beside the text.
3. `.browser` — one lead shot (`dashboard-concept.webp`), **980px wide**, `18px` radius,
   `0 40px 100px rgba(6,6,7,.18)`, hairline border, `overflow: hidden`
4. Workflows (warm band) — 3 mode cards
5. Features — 6 icon cards
6. How it works — `.tour`, copied from the reference (see below)
7. Privacy — near-black band, stacked single column: heading → copy → bulleted list → CTA
8. FAQ (warm band) — `<details>` accordion
9. Closing CTA — near-black with teal bloom, Flowbot, 2 store buttons (Chrome, Edge)
10. Near-black 4-column footer

## The tour (measured off replymer.com, 1440px viewport)

This is the part that matters, and the numbers are theirs, not approximations:

```
.tour       flex column, gap 72px
.tour-row   grid, columns 1fr 0.654fr (text 617 / shot 403), gap 52px, align-items center
.tour-row.flip   columns 0.654fr 1fr; .tour-text { order: 2 }  .tour-shot { order: 1 }
.tour-text  .n badge → h3 → p
.n          34×34, radius 10px (rounded square, not a circle), accent fill, 16px/700, 16px below
h3          23.2px / 700 / -0.02em / 1.6, 10px below
p           15.52px / 1.6
.tour-shot  radius 16px, 0.8px hairline border, 0 30px 70px -30px shadow, overflow hidden
```

Rows alternate: text-left/shot-right, then shot-left/text-right.

**One deliberate divergence from the reference.** Replymer keeps its column template fixed at
`0.654fr 1fr`, so its shots render at 615px on normal rows and 402px on flipped rows — a
different size every other row. We flip the template as well, so **every tour shot is the same
402×251**, the smaller of the two. Same alternating rhythm, consistent image size.

Under 900px every row collapses to one column and `order` resets to `0`.

`privacy.html`, `terms.html`, and `contact.html` reuse the same nav/footer with the `.doc`
prose layout.

## Store status

Chrome is **live**: https://chromewebstore.google.com/detail/kfkojfkfjlmaemjocdidplabaaglgggi (v1.0.1). The nav CTA, hero CTA, FAQ, first store button, footer,
`installUrl`/`downloadUrl` in the `SoftwareApplication` JSON-LD, `index.md`, and
`llms-full.txt` all point at it. Edge is still in review and remains the one `mailto:`
waitlist link on the page — swap it when that listing publishes.

## Browser support — do not re-add Firefox

The extension repo is explicit (`README.md`): *"Packaging is allowed for Chrome and Edge only…
Firefox artifacts are disabled for this product because Flow requires trusted CDP input."*
`store/` contains only `chrome/`. The site therefore advertises **Chrome and Edge only**, with
Chromium siblings (Brave, Arc, Opera) installing the Chrome build. The hero rail, the store
buttons, the FAQ, the `SoftwareApplication` JSON-LD, `index.md`, and `llms-full.txt` all say
the same thing — keep them in sync if the target list ever changes.

## The family row — what is real

Replymer's engine pills / avatar stack / "Trusted by 1588+ products" line is reproduced as
`.family` in the hero. What sits in it:

- **Pills** link to the live sibling listings: Google Flow (this page, no link), Higgsfield
  (556 users), Magnific (271 users). Per-pill user counts were removed on purpose — printing
  them next to a 1,000+ headline invites the reader to add up three numbers and doubt it.
- **Avatar stack** uses five **placeholder portraits** from randomuser.me, stored locally at
  `assets/avatars/*.webp` (92px source, 46px display, ~2 KB each) so the page stays
  self-contained. They are marked with an HTML comment in `index.html`. **These are not real
  users — replace them with actual customer photos (with permission) or delete the stack
  before treating the page as finished.**
- **The 1,000+ figure is across Deepak Thapa's full extension range** (~20 projects), which is
  why the sentence names the range and not this product. Google Flow Automation on its own had
  2 users on 2026-08-24; Chrome-verified across the three sibling listings was 829.

Grok, Gemini, and Seedance pills were requested but not added: `Extensions/Grok Automation` is
an empty folder, `Extensions/Gemini Automation` holds a downloaded third-party build rather
than a shipped product, and no Seedance project exists. Add a pill when each has a live
listing URL.

## Hero vertical rhythm (measured off replymer.com @ 1920x900)

The hero was overflowing the fold until it was rebuilt against these numbers. Do not add rows.

| Element | Replymer top | Ours | Rule |
| --- | --- | --- | --- |
| nav height | 65 | 69 | — |
| `h1` | 214 | 218 | `max-width: 900px; margin: 26px auto 20px` |
| sub | 383 | 387 | `max-width: 680px; margin-bottom: 30px`, ~3 lines |
| CTA row | 500 | 504 | `margin-bottom: 34px` |
| pill row | 582 | 586 | `margin-bottom: 20px` |
| avatars | 638 | 647 | `margin-bottom: 10px`, 38px circles |
| proof line | 686 | 695 | ends at 720, comfortably above a 900 fold |
| product shot | 742 | 754 | `.mock` `padding-top: 34px` |

Two things that caused the original overflow, both fixed:

1. `h1` was capped at `16ch` (~560px) instead of `900px`, forcing a cramped two-line wrap; the
   sub was `62ch` instead of `680px` and ran to four lines. Both are now pixel values.
2. There was an extra `.hero__meta` chip row between the CTAs and the pills. Replymer has
   exactly one row there. It was removed — its three claims already appear in the tightened
   sub copy, the CTA note, and the footer.

The hero subhead is deliberately short (~190 chars) so it renders in three lines at 680px, the
same density as the reference. Lengthening it re-breaks the fold.
