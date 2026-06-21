# Shir Shimon Makeup — Landing Page Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a single `index.html` landing page for makeup artist Shir Shimon Kliff that drives visitors to contact her via WhatsApp or Instagram.

**Architecture:** One self-contained HTML file with embedded CSS and minimal inline JS. Four sections scroll vertically: Hero → Services → About → Contact. Mobile-first, RTL Hebrew.

**Tech Stack:** HTML5, CSS3 (custom properties, grid, flexbox), Google Fonts (Heebo), vanilla JS (smooth scroll only).

## Global Constraints

- Single file: `index.html` at project root — no build tools, no external CSS/JS files
- Language: Hebrew, `dir="rtl"`, `lang="he"`
- Fonts: Heebo via Google Fonts CDN (`wght@300;400;500;700`)
- Color palette — exact hex values:
  - `--cream: #FFF8F0`
  - `--dusty-pink: #F2D7D5`
  - `--rose-gold: #C9956C`
  - `--mauve: #7A5C61`
  - `--mauve-light: #A08080`
- WhatsApp number placeholder: `972XXXXXXXXXX` (client must replace)
- Instagram: `https://www.instagram.com/shirshimon_makeup/`
- Verify each task by opening `index.html` directly in Chrome (no server needed)

---

### Task 1: HTML Skeleton + Global CSS

**Files:**
- Create: `index.html`

**Interfaces:**
- Produces: base HTML shell that all subsequent tasks insert sections into

- [ ] **Step 1: Create `index.html` with skeleton and global CSS**

```html
<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>שיר שמעון כליף | מאפרת מקצועית</title>
  <link
    href="https://fonts.googleapis.com/css2?family=Heebo:wght@300;400;500;700&display=swap"
    rel="stylesheet"
  />
  <style>
    /* ── Variables ── */
    :root {
      --cream: #FFF8F0;
      --dusty-pink: #F2D7D5;
      --rose-gold: #C9956C;
      --mauve: #7A5C61;
      --mauve-light: #A08080;
      --white: #FFFFFF;
      --shadow: 0 4px 20px rgba(122, 92, 97, 0.12);
      --radius: 16px;
    }

    /* ── Reset ── */
    *, *::before, *::after {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    html {
      scroll-behavior: smooth;
    }

    body {
      font-family: 'Heebo', sans-serif;
      background-color: var(--cream);
      color: var(--mauve);
      direction: rtl;
      line-height: 1.7;
    }

    img {
      max-width: 100%;
      display: block;
    }

    /* ── Utility ── */
    .container {
      max-width: 1100px;
      margin: 0 auto;
      padding: 0 1.5rem;
    }

    .section-title {
      font-size: clamp(1.6rem, 4vw, 2.2rem);
      font-weight: 700;
      color: var(--mauve);
      text-align: center;
      margin-bottom: 0.5rem;
    }

    .section-subtitle {
      font-size: 1rem;
      color: var(--mauve-light);
      text-align: center;
      margin-bottom: 3rem;
    }
  </style>
</head>
<body>

  <!-- HERO -->
  <!-- SERVICES -->
  <!-- ABOUT -->
  <!-- CONTACT -->
  <!-- FOOTER -->

  <script>
    // Smooth scroll for anchor links (fallback for older browsers)
    document.querySelectorAll('a[href^="#"]').forEach(anchor => {
      anchor.addEventListener('click', function (e) {
        e.preventDefault();
        document.querySelector(this.getAttribute('href')).scrollIntoView({ behavior: 'smooth' });
      });
    });
  </script>
</body>
</html>
```

- [ ] **Step 2: Verify in browser**

Open `index.html` in Chrome. Expected: blank cream-colored page, no console errors, Heebo font loads (check Network tab → Fonts).

- [ ] **Step 3: Commit**

```bash
git init
git add index.html
git commit -m "feat: add HTML skeleton with global CSS variables and reset"
```

---

### Task 2: Hero Section

**Files:**
- Modify: `index.html` — replace `<!-- HERO -->` comment and add CSS inside `<style>`

**Interfaces:**
- Consumes: `.container` utility class from Task 1
- Produces: `#contact` anchor target (used by CTA button in this section)

- [ ] **Step 1: Add hero HTML** — replace `<!-- HERO -->` with:

```html
  <!-- HERO -->
  <section class="hero">
    <div class="hero__content container">
      <p class="hero__eyebrow">✨ מאפרת מקצועית</p>
      <h1 class="hero__name">שיר שמעון כליף</h1>
      <p class="hero__tagline">כי כל אישה ראויה להרגיש יפה<br />ביום המיוחד שלה</p>
      <a href="#contact" class="btn btn--primary">בואי נדבר 💬</a>
    </div>
  </section>
```

- [ ] **Step 2: Add hero CSS** — append inside `<style>` before closing `</style>`:

```css
    /* ── Hero ── */
    .hero {
      min-height: 100vh;
      background: linear-gradient(145deg, var(--dusty-pink) 0%, var(--cream) 60%);
      display: flex;
      align-items: center;
      justify-content: center;
      text-align: center;
      padding: 4rem 1.5rem;
      position: relative;
      overflow: hidden;
    }

    .hero::before {
      content: '';
      position: absolute;
      width: 500px;
      height: 500px;
      border-radius: 50%;
      background: radial-gradient(circle, rgba(201, 149, 108, 0.15) 0%, transparent 70%);
      top: -100px;
      left: -100px;
      pointer-events: none;
    }

    .hero__content {
      position: relative;
      z-index: 1;
      animation: fadeUp 0.9s ease both;
    }

    .hero__eyebrow {
      font-size: 0.95rem;
      font-weight: 500;
      letter-spacing: 0.08em;
      color: var(--rose-gold);
      margin-bottom: 1rem;
      text-transform: uppercase;
    }

    .hero__name {
      font-size: clamp(2.4rem, 7vw, 4.5rem);
      font-weight: 700;
      color: var(--mauve);
      line-height: 1.15;
      margin-bottom: 1.25rem;
    }

    .hero__tagline {
      font-size: clamp(1rem, 2.5vw, 1.25rem);
      font-weight: 300;
      color: var(--mauve-light);
      max-width: 480px;
      margin: 0 auto 2.5rem;
    }

    /* ── Buttons ── */
    .btn {
      display: inline-block;
      padding: 0.85rem 2.4rem;
      border-radius: 50px;
      font-family: 'Heebo', sans-serif;
      font-size: 1rem;
      font-weight: 600;
      text-decoration: none;
      cursor: pointer;
      transition: transform 0.2s ease, box-shadow 0.2s ease;
    }

    .btn:hover {
      transform: translateY(-2px);
      box-shadow: 0 8px 24px rgba(201, 149, 108, 0.35);
    }

    .btn--primary {
      background: var(--rose-gold);
      color: var(--white);
    }

    /* ── Animation ── */
    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(28px); }
      to   { opacity: 1; transform: translateY(0); }
    }
```

- [ ] **Step 3: Verify in browser**

Refresh `index.html`. Expected: full-screen gradient hero, large name, tagline, rose-gold button. Clicking "בואי נדבר" should do nothing yet (anchor doesn't exist). No console errors.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add hero section with gradient background and CTA button"
```

---

### Task 3: Services Section

**Files:**
- Modify: `index.html` — replace `<!-- SERVICES -->` comment and add CSS

**Interfaces:**
- Consumes: `.container`, `.section-title`, `.section-subtitle` from Task 1
- Produces: visible services grid (no anchor needed)

- [ ] **Step 1: Add services HTML** — replace `<!-- SERVICES -->` with:

```html
  <!-- SERVICES -->
  <section class="services">
    <div class="container">
      <h2 class="section-title">מה אני מציעה</h2>
      <p class="section-subtitle">כל שירות מותאם אישית בדיוק בשבילך</p>
      <div class="services__grid">

        <div class="service-card">
          <div class="service-card__icon">💍</div>
          <h3 class="service-card__title">איפור כלות</h3>
          <p class="service-card__desc">ליום הכי חשוב בחייך — איפור עמיד, מחמיא ומרגש שיגרום לך להרגיש כמו גרסה הטובה ביותר של עצמך.</p>
        </div>

        <div class="service-card">
          <div class="service-card__icon">✨</div>
          <h3 class="service-card__title">איפור אירועים</h3>
          <p class="service-card__desc">לבת מצווה, חתונה, מסיבה וכל אירוע מיוחד — נבנה יחד את הלוק שתמיד חלמת עליו.</p>
        </div>

        <div class="service-card">
          <div class="service-card__icon">🎭</div>
          <h3 class="service-card__title">איפור פורים</h3>
          <p class="service-card__desc">פעם בשנה — נשגע ביחד! איפור קריאייטיב, דרמטי ומהנה לפורים שיגרום לך להתבלט.</p>
        </div>

      </div>
    </div>
  </section>
```

- [ ] **Step 2: Add services CSS** — append inside `<style>`:

```css
    /* ── Services ── */
    .services {
      padding: 6rem 0;
      background: var(--white);
    }

    .services__grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 1.75rem;
    }

    @media (max-width: 768px) {
      .services__grid {
        grid-template-columns: 1fr;
      }
    }

    .service-card {
      background: var(--cream);
      border-radius: var(--radius);
      padding: 2rem 1.75rem;
      border-top: 4px solid var(--rose-gold);
      box-shadow: var(--shadow);
      transition: transform 0.25s ease, box-shadow 0.25s ease;
      text-align: center;
    }

    .service-card:hover {
      transform: translateY(-6px);
      box-shadow: 0 12px 32px rgba(122, 92, 97, 0.18);
    }

    .service-card__icon {
      font-size: 2.5rem;
      margin-bottom: 1rem;
    }

    .service-card__title {
      font-size: 1.2rem;
      font-weight: 700;
      color: var(--mauve);
      margin-bottom: 0.75rem;
    }

    .service-card__desc {
      font-size: 0.95rem;
      color: var(--mauve-light);
      line-height: 1.65;
    }
```

- [ ] **Step 3: Verify in browser**

Scroll down past hero. Expected: white section, 3 cards side-by-side on desktop. On mobile viewport (DevTools → iPhone 14) cards should stack vertically. Hover effect lifts card.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add services section with 3 responsive cards"
```

---

### Task 4: About Section

**Files:**
- Modify: `index.html` — replace `<!-- ABOUT -->` comment and add CSS

**Interfaces:**
- Consumes: `.container`, `.section-title` from Task 1
- Produces: circular photo placeholder (`.about__photo`) that client will replace with real image

- [ ] **Step 1: Add about HTML** — replace `<!-- ABOUT -->` with:

```html
  <!-- ABOUT -->
  <section class="about">
    <div class="container">
      <div class="about__inner">
        <div class="about__photo-wrap">
          <div class="about__photo">
            <span class="about__photo-placeholder">📸</span>
          </div>
        </div>
        <div class="about__text">
          <h2 class="section-title" style="text-align: right;">קצת עליי</h2>
          <p class="about__bio">
            היי, אני שיר 👋<br /><br />
            מאפרת מקצועית עם אהבה אמיתית לאמנות האיפור ולגרום לכל אישה להרגיש יפה, בטוחה ומוארת.<br /><br />
            בין אם זה יום החתונה שלך, אירוע מיוחד או פורים — אני כאן כדי שתרגישי בדיוק כמו שרצית.
          </p>
          <a href="#contact" class="btn btn--primary" style="margin-top: 1.5rem;">בואי נדבר 💬</a>
        </div>
      </div>
    </div>
  </section>
```

- [ ] **Step 2: Add about CSS** — append inside `<style>`:

```css
    /* ── About ── */
    .about {
      padding: 6rem 0;
      background: var(--dusty-pink);
    }

    .about__inner {
      display: flex;
      align-items: center;
      gap: 4rem;
    }

    @media (max-width: 768px) {
      .about__inner {
        flex-direction: column;
        gap: 2rem;
        text-align: center;
      }

      .about__text .section-title {
        text-align: center !important;
      }

      .about__text .btn {
        display: block;
        text-align: center;
      }
    }

    .about__photo-wrap {
      flex-shrink: 0;
    }

    .about__photo {
      width: 240px;
      height: 240px;
      border-radius: 50%;
      background: var(--cream);
      border: 5px solid var(--rose-gold);
      display: flex;
      align-items: center;
      justify-content: center;
      box-shadow: var(--shadow);
      overflow: hidden;
    }

    .about__photo img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      border-radius: 50%;
    }

    .about__photo-placeholder {
      font-size: 4rem;
      opacity: 0.5;
    }

    .about__bio {
      font-size: 1rem;
      color: var(--mauve);
      line-height: 1.75;
      max-width: 520px;
    }
```

- [ ] **Step 3: Verify in browser**

Scroll to about section. Expected: dusty-pink background, circular placeholder with 📸 emoji on the right (RTL), text on the left. On mobile: image stacks above text, both centered.

To swap in a real photo later, replace `<div class="about__photo">` content with:
```html
<img src="photo.jpg" alt="שיר שמעון כליף" />
```

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add about section with circular photo placeholder"
```

---

### Task 5: Contact Section + Footer

**Files:**
- Modify: `index.html` — replace `<!-- CONTACT -->` and `<!-- FOOTER -->` comments, add CSS

**Interfaces:**
- Consumes: `#contact` anchor (linked from hero and about CTA buttons)
- Produces: working WhatsApp link + Instagram link

**⚠️ Before this task:** Get the actual WhatsApp number from Shir and replace `972XXXXXXXXXX` with it (e.g. `972501234567` for 050-123-4567).

- [ ] **Step 1: Add contact + footer HTML** — replace `<!-- CONTACT -->` and `<!-- FOOTER -->` with:

```html
  <!-- CONTACT -->
  <section class="contact" id="contact">
    <div class="container">
      <h2 class="section-title">בואי נדבר 💬</h2>
      <p class="section-subtitle">אשמח לענות על כל שאלה ולתאם את הלוק המושלם עבורך</p>
      <div class="contact__buttons">
        <a
          href="https://wa.me/972XXXXXXXXXX"
          target="_blank"
          rel="noopener noreferrer"
          class="btn contact__btn contact__btn--whatsapp"
        >
          <span class="contact__btn-icon">📱</span>
          שלחי הודעה בוואטסאפ
        </a>
        <a
          href="https://www.instagram.com/shirshimon_makeup/"
          target="_blank"
          rel="noopener noreferrer"
          class="btn contact__btn contact__btn--instagram"
        >
          <span class="contact__btn-icon">📸</span>
          @shirshimon_makeup
        </a>
      </div>
    </div>
  </section>

  <!-- FOOTER -->
  <footer class="footer">
    <div class="container">
      <p>© 2026 שיר שמעון כליף | מאפרת מקצועית</p>
    </div>
  </footer>
```

- [ ] **Step 2: Add contact + footer CSS** — append inside `<style>`:

```css
    /* ── Contact ── */
    .contact {
      padding: 6rem 0;
      background: var(--cream);
      text-align: center;
    }

    .contact__buttons {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 1.25rem;
    }

    @media (min-width: 480px) {
      .contact__buttons {
        flex-direction: row;
        justify-content: center;
      }
    }

    .contact__btn {
      display: flex;
      align-items: center;
      gap: 0.6rem;
      padding: 1rem 2.5rem;
      font-size: 1.05rem;
      font-weight: 600;
      min-width: 260px;
      justify-content: center;
    }

    @media (max-width: 479px) {
      .contact__btn {
        width: 100%;
        max-width: 340px;
      }
    }

    .contact__btn--whatsapp {
      background: #25D366;
      color: var(--white);
    }

    .contact__btn--whatsapp:hover {
      box-shadow: 0 8px 24px rgba(37, 211, 102, 0.4);
    }

    .contact__btn--instagram {
      background: var(--rose-gold);
      color: var(--white);
    }

    .contact__btn--instagram:hover {
      box-shadow: 0 8px 24px rgba(201, 149, 108, 0.4);
    }

    .contact__btn-icon {
      font-size: 1.2rem;
    }

    /* ── Footer ── */
    .footer {
      background: var(--mauve);
      color: rgba(255, 248, 240, 0.7);
      text-align: center;
      padding: 1.5rem 0;
      font-size: 0.85rem;
    }
```

- [ ] **Step 3: Verify in browser**

Scroll to bottom. Expected:
- Cream section with two large buttons stacked (mobile) or side-by-side (desktop ≥480px)
- WhatsApp button is green, Instagram button is rose gold
- Clicking "בואי נדבר" from hero/about scrolls smoothly to this section
- Dark mauve footer with copyright text below

Click each button: WhatsApp should open `wa.me` (will say number not set until replaced). Instagram button should open `instagram.com/shirshimon_makeup`.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add contact section with WhatsApp and Instagram CTAs, add footer"
```

---

### Task 6: Scroll Animations + Final Polish

**Files:**
- Modify: `index.html` — add Intersection Observer JS, final responsive tweaks to CSS

**Interfaces:**
- Consumes: all `.service-card` and `.about__inner` elements from Tasks 3–4
- Produces: elements fade in as they enter the viewport

- [ ] **Step 1: Add scroll animation JS** — replace the existing `<script>` block with:

```html
  <script>
    // Smooth scroll for anchor links
    document.querySelectorAll('a[href^="#"]').forEach(anchor => {
      anchor.addEventListener('click', function (e) {
        e.preventDefault();
        document.querySelector(this.getAttribute('href')).scrollIntoView({ behavior: 'smooth' });
      });
    });

    // Fade-in on scroll
    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            entry.target.classList.add('visible');
            observer.unobserve(entry.target);
          }
        });
      },
      { threshold: 0.15 }
    );

    document.querySelectorAll('.service-card, .about__inner, .contact__buttons').forEach(el => {
      observer.observe(el);
    });
  </script>
```

- [ ] **Step 2: Add animation CSS** — append inside `<style>`:

```css
    /* ── Scroll Animations ── */
    .service-card,
    .about__inner,
    .contact__buttons {
      opacity: 0;
      transform: translateY(24px);
      transition: opacity 0.6s ease, transform 0.6s ease;
    }

    .service-card:nth-child(2) { transition-delay: 0.1s; }
    .service-card:nth-child(3) { transition-delay: 0.2s; }

    .service-card.visible,
    .about__inner.visible,
    .contact__buttons.visible {
      opacity: 1;
      transform: translateY(0);
    }
```

- [ ] **Step 3: Final mobile polish** — append inside `<style>`:

```css
    /* ── Mobile Fine-tuning ── */
    @media (max-width: 480px) {
      .hero {
        padding: 5rem 1.25rem;
      }

      .about__photo {
        width: 180px;
        height: 180px;
      }

      .services,
      .about,
      .contact {
        padding: 4rem 0;
      }
    }
```

- [ ] **Step 4: Verify full page**

Open `index.html` in Chrome. Check all of the following:

| Check | Expected |
|---|---|
| Scroll down slowly | Cards and sections fade in as they enter viewport |
| Desktop (1200px) | 3 service cards in a row |
| Tablet (768px) | Cards stack to 1 column |
| Mobile (390px — iPhone) | Everything stacked, buttons full width |
| Click "בואי נדבר" in hero | Smooth scroll to contact section |
| WhatsApp button color | Green `#25D366` |
| Instagram button color | Rose gold `#C9956C` |
| Hebrew text | Reads right-to-left correctly |
| No console errors | Zero errors in DevTools Console |

- [ ] **Step 5: Final commit**

```bash
git add index.html
git commit -m "feat: add scroll animations and mobile polish — landing page complete"
```

---

## Remaining Client Actions

After implementation, share the following checklist with Shir:

1. **WhatsApp number** — replace `972XXXXXXXXXX` in `index.html` (Task 5) with her actual number (e.g. `972501234567` for 050-123-4567)
2. **Hero photo** — add a `<img>` tag in the hero section (or set a CSS `background-image`) to replace the gradient
3. **About photo** — replace `.about__photo-placeholder` span with `<img src="your-photo.jpg" alt="שיר שמעון כליף" />`
4. **About bio** — review and personalize the bio text in the About section
5. **Deployment** — upload `index.html` to any static host (Netlify drag-and-drop, GitHub Pages, or simply share the file)
