# Shir Shimon Makeup — Landing Page Design Spec
Date: 2026-06-22

## Context
Shir Shimon Kliff (@shirshimon_makeup) is a professional makeup artist offering bridal makeup, event makeup, and seasonal Purim makeup. She needs a digital business card landing page whose primary goal is to drive visitors to contact her via WhatsApp or Instagram. There is no e-commerce, booking system, or gallery requirement at this stage.

## Goals
- Serve as a digital business card that establishes trust and professionalism
- Lead visitors clearly to WhatsApp or Instagram to book/inquire
- Display the 3 services she offers (bridal, events, Purim)
- Work beautifully on mobile (primary audience)

## Tech Stack
- Single HTML file (`index.html`)
- Pure CSS (no frameworks)
- Google Fonts via CDN (Heebo — Hebrew-friendly, elegant)
- Minimal vanilla JS for smooth scroll only
- No build tools, no dependencies

## Visual Identity
- **Palette:**
  - Background light: `#FFF8F0` (cream)
  - Background accent: `#F2D7D5` (dusty pink)
  - Accent / CTA: `#C9956C` (rose gold)
  - Text primary: `#7A5C61` (deep mauve)
  - Text secondary: `#A08080`
- **Typography:** Heebo (Google Fonts), RTL Hebrew
- **Aesthetic:** Romantic, delicate, feminine — suitable for brides and events
- **Direction:** RTL (`dir="rtl"`)

## Page Structure

### Section 1 — Hero (full viewport height)
- Background: soft gradient cream → dusty pink (placeholder until real photo provided)
- Large name: **שיר שמעון כליף**
- Subtitle: מאפרת מקצועית | כלות ואירועים
- Tagline: *"כי כל אישה ראויה להרגיש יפה ביום המיוחד שלה"*
- CTA button: "בואי נדבר" → smooth scroll to contact section
- Subtle floating animation on hero element

### Section 2 — Services (3 cards)
Three equal cards in a responsive grid (3 cols desktop, 1 col mobile):

1. **איפור כלות** — 💍 — "ליום הכי חשוב בחייך"
2. **איפור אירועים** — ✨ — "לבת מצווה, חתונה, מסיבה וכל אירוע מיוחד"
3. **איפור פורים** — 🎭 — "פעם בשנה — נשגע ביחד"

Cards: white background, soft shadow, rose gold top border, hover lift effect.

### Section 3 — About
- Short 2–3 sentence bio placeholder (to be filled by client)
- Circular photo placeholder (to be replaced by real photo)
- Warm personal tone

### Section 4 — Contact (CTA)
- Section heading: "בואי נדבר 💬"
- Two large buttons, stacked on mobile:
  - WhatsApp: green-tinted, "שלחי הודעה בוואטסאפ" → `https://wa.me/972XXXXXXXXX`
  - Instagram: rose gold, "@shirshimon_makeup" → `https://instagram.com/shirshimon_makeup`
- WhatsApp number: **placeholder — client must provide**

### Footer
- Copyright line: © 2026 שיר שמעון כליף
- Minimal, same cream background

## Responsive Design
- Mobile-first CSS
- Hero text scales down on small screens
- Cards stack to single column on mobile
- Buttons full-width on mobile

## Placeholders / To Fill Later
- Hero background image (replace gradient)
- About section photo
- About section bio text
- WhatsApp phone number

## Verification
1. Open `index.html` directly in browser (no server needed)
2. Check on mobile viewport (Chrome DevTools → iPhone)
3. Verify all 4 sections visible on scroll
4. Click WhatsApp button → confirm it opens WhatsApp
5. Click Instagram button → confirm it opens Instagram profile
6. Verify RTL text renders correctly in Hebrew
