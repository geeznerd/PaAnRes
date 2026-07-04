# Handoff: Passion Animal Rescue — Nonprofit Website

## Overview
A single-page marketing/donation website for **Passion Animal Rescue**, a 501(c)(3) volunteer-run animal rescue in Long Beach, CA (EIN 84-1880200). Primary goal: **drive donations** (via Zeffy); secondary goals: showcase adoptable pets, recruit fosters/volunteers. Tone: warm, heartfelt, playful "poster/sticker" aesthetic.

## About the Design Files
The files in `design/` are **design references created in HTML** — a prototype showing intended look and behavior, NOT production code to copy directly. Your task is to **recreate this design in the target codebase's environment** (React, Next.js, plain HTML/CSS, etc.) using its established patterns. If no codebase exists yet, a simple static site (plain HTML/CSS or Astro/Next.js static export) is appropriate — this is a small nonprofit site with almost no dynamic data.

`design/Passion Animal Rescue — Site.dc.html` contains the full page as an HTML template (markup between `<x-dc>` tags, all inline styles) plus a small logic class at the bottom (pet data array, donate-widget state). `image-slot.js` is a prototype-only drag-and-drop placeholder component — in production, replace each `<x-import component-from-global-scope="image-slot" …>` with a plain `<img>`.

## Fidelity
**High-fidelity.** Colors, typography, spacing, copy, and interactions are final design intent. Recreate pixel-perfectly. (Pet names/photos are placeholders the client will replace.)

## Design Tokens
- **Brand pink**: `#E9898D` (page background, accents, sticker shadows)
- **Charcoal**: `#393130` (text, borders, dark sections, buttons)
- **Cream**: `#FBF7F2` (light section backgrounds)
- **Dusty rose (accent text)**: `#B0655F`
- **White**: `#fff` (cards)
- **Font**: `'Bricolage Grotesque'` (Google Fonts), weights 400/600/700/800, everywhere. Headlines use weight 800 with `letter-spacing:-.02em`–`-.03em`.
- **Borders**: `2px solid #393130` on cards/buttons; radius 10–20px (cards 16px, big donate card 20px, buttons 10–12px, pills 999px).
- **Signature "sticker" shadows**: hard offset shadows, no blur — `box-shadow: 6px 6px 0 #E9898D` (light cards), `8px 8px 0 #393130` (donate card), `4–5px 4–5px 0 rgba(57,49,47,.35)` (dark buttons). Hero headline: white text with `text-shadow: 4px 4px 0 rgba(57,49,47,.9)`.
- Horizontal page padding: `5vw`; section vertical padding ~60px; page `min-width: 980px` in prototype (add proper responsive/mobile treatment in production — not designed yet).

## Page Structure (top → bottom)
1. **Sticky nav** — pink `#E9898D`, `border-bottom:2px solid #393130`. Left: logo mark (40px) + "PASSION ANIMAL RESCUE" (800, 17px). Right: anchor links (Adopt, Foster & Volunteer, Our Story, Contact, 14px/600) + "DONATE ♥" button (charcoal bg, white text, radius 10, sticker shadow).
2. **Hero** (pink) — logo mark large (~400px) at top-right, ~90% opacity. Headline "STRAY TODAY. FAMILY TOMORROW." — white, `clamp(56px,6.5vw,84px)`, line-height .98, charcoal hard text-shadow. Subcopy 17px/600, max 44ch. Two buttons: "GIVE $25 →" (charcoal, sticker shadow) and "MEET THE PETS" (white, 2px charcoal border). Both anchor-link within page.
3. **Marquee band** — charcoal bg, white 800 15px text, letter-spacing .12em: "ADOPT ♥ FOSTER ♥ DONATE ♥ SPAY & NEUTER ♥ VOLUNTEER ♥ …" duplicated twice, animated `translateX(0 → -50%)` linear 22s infinite loop.
4. **THE ADOPTABLES** (cream) — heading 800/38px + "updated weekly" note in `#B0655F`. 3-column grid, gap 26px, 6 cards: white bg, 2px charcoal border, radius 16, `6px 6px 0 #E9898D` shadow. Each card: photo (240px tall, cover), then row with name (800/22px) + one-line description (13px, 60% opacity) and an "ADOPT ME" pill (pink bg, white text, 2px charcoal border). Footnote line: "Every adoptable pet is spayed/neutered, vaccinated, and microchipped before going home."
5. **How to help** (cream) — 3 cards: ADOPT (pink card, charcoal sticker shadow, white heading with small text-shadow, charcoal CTA "START AN APPLICATION"), FOSTER and VOLUNTEER (white cards, pink sticker shadows, outlined CTAs). Copy is final — see design file.
6. **Our Story** (charcoal) — 2 columns: heading "A LITTLE RESCUE WITH A BIG HEART" (white 800/34px) + two paragraphs (15.5px, rgba(255,255,255,.85)); right: photo (320px, radius 16, faint white border).
7. **Donate** (cream) — the key section. One big white card (2px charcoal border, radius 20, `8px 8px 0 #393130` shadow, padding ~48px, 2 columns):
   - Left: heading "EVERY DOLLAR = DINNER, MEDS & BELLY RUBS" (800/36px); paragraph explaining Zeffy (0% fees); impact lines ($25 vaccinates…, $50 covers one spay/neuter…, $100 feeds a foster pet…); fine print "Tax-deductible · 501(c)(3) · EIN 84-1880200 · Prefer Venmo or PayPal? We accept those too."
   - Right (interactive widget): ONE-TIME / MONTHLY ♥ segmented toggle (selected = charcoal bg + white text); 4 amount chips $10/$25/$50/$100 (selected = pink bg + white text; default $25); big CTA button "DONATE $25 VIA ZEFFY →" (label reflects selection, e.g. "DONATE $50/MO VIA ZEFFY →"), charcoal bg, pink sticker shadow; microcopy "Secure checkout · Apple Pay, Google Pay & cards accepted".
8. **Footer/Contact** (charcoal) — 3 columns: logo (white-inverted) + org name + "501(c)(3) Nonprofit Organization / EIN 84-1880200"; VISIT US: 1200 E Anaheim St., Long Beach, CA 90813; SAY HELLO: 562-326-6194, passionanimalrescue@gmail.com, Facebook: Passion Animal Rescue. Column labels in pink, 12px, letter-spacing .14em. Bottom row: "© 2026 Passion Animal Rescue. Made with love in Long Beach." / "ADOPT ♥ FOSTER ♥ DONATE".

## Interactions & Behavior
- Nav and hero buttons are same-page anchor links; smooth scrolling (`scroll-behavior:smooth`), sections have `scroll-margin-top:80px` for the sticky nav.
- Marquee: continuous CSS keyframe loop (respect `prefers-reduced-motion` in production).
- Donate widget state: `{ amount: 10|25|50|100 (default 25), monthly: boolean (default false) }`. Selecting updates chip/toggle styles and the CTA label.
- **Donate CTA destination**: currently a placeholder link to zeffy.com. The client will create a free Zeffy organization account (zeffy.com) and get a hosted donation-form URL — point the button there (Zeffy also offers an embeddable form/modal if preferred). Amount/monthly selection can simply deep-link or just open the Zeffy form.
- Hover states are not specified — add subtle ones consistent with the sticker aesthetic (e.g. shadow shift + 1–2px translate on buttons).
- No forms, no backend. "START AN APPLICATION" etc. currently anchor to Contact; client may later want a Google Form link.

## Assets
- `assets/logo-mark.png` — transparent-background dog+cat logo mark (extracted from client's business card). Use on any background; invert to white (`filter:brightness(0) invert(1)`) on charcoal.
- `assets/logo-on-pink.png` — original mark on brand-pink background.
- `assets/brand-reference/business-card-front.png`, `business-card-back.png` — client's original branding for reference.
- `assets/photos/` — the placeholder pet photos currently in the design (from Unsplash, free license): mochi-cat, biscuit-dog, clover-bunny, pepper-kitten, duke-dog, willow-cat, about-team. **These are placeholders** — the client will supply real rescue photos; keep image slots easy to swap.

## Files
- `design/Passion Animal Rescue — Site.dc.html` — full page design (markup + inline styles + widget logic/pet data at bottom).
- `design/image-slot.js` — prototype-only image placeholder component; replace with `<img>` in production.
