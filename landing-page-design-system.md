# 🎯 TV Production — מדריך עיצוב ומבנה לעמודי נחיתה

> **רפרנס מלא לבניית עמודי נחיתה חדשים באותה שפה עיצובית ושיווקית**
> קובץ מקור: `C:\Users\VAIS_TAL\.gemini\antigravity\scratch\hook-lashivuk\`
> GitHub: `https://github.com/tv-prod/hook-lashivuk`

---

## 🎨 Design Tokens — CSS Variables

כל הצבעים מוגדרים ב-`:root` בתוך `style.css`:

```css
:root {
  --black:         #08080f;   /* רקע כהה ביותר */
  --black-soft:    #0f0f18;   /* רקע סקשנים משניים */
  --black-card:    #14141f;   /* כרטיסים */
  --black-border:  #1c1c2e;   /* גבולות, dividers */
  --white:         #ffffff;
  --white-dim:     #a8a8c0;   /* טקסט משני */
  --cyan:          #00d4ff;   /* אקצנט ראשי — כפתורים, הדגשות */
  --cyan-dk:       #0099cc;
  --cyan-glow:     rgba(0,212,255,.22);
  --cyan-xs:       rgba(0,212,255,.06);
  --green-neon:    #00ff88;   /* urgency bar, coupon */
  --green-glow:    rgba(0,255,136,.18);
  --font: 'Heebo', sans-serif;
  --r-sm: 8px; --r-md: 16px; --r-lg: 24px; --r-xl: 36px;
  --ease: cubic-bezier(.4,0,.2,1);
}
```

### גרדיאנטים נפוצים

```css
/* כפתור ראשי */
background: linear-gradient(135deg, var(--cyan-dk), var(--cyan));

/* buy card */
background: linear-gradient(160deg, #0d1117, #0d1a2e);

/* urgency bar */
background: linear-gradient(180deg, #001a10, #002516);

/* FOMO countdown */
background: linear-gradient(135deg, #0f0808, #1a0a0a);
```

---

## 🔤 טיפוגרפיה

```css
font-family: 'Heebo', sans-serif; /* הכל — עברית */
/* נטען מ: fonts.googleapis.com/css2?family=Heebo:wght@300;400;500;600;700;800;900 */

/* גדלים */
H1 Hero:     clamp(26px, 7vw, 46px) — weight 900
H2 Section:  clamp(24px, 6vw, 38px) — weight 900
H3 Sub:      clamp(18px, 5vw, 22px) — weight 700
Body:        15–16px — weight 400–500
Label/Tag:   12–13px — weight 600–700, letter-spacing .3–.5px
Price big:   clamp(52px, 12vw, 72px) — weight 900
```

---

## 📐 מבנה הדף — Flow שיווקי מלא

```
index.html
│
├─ QUIZ PHASE          (id="quiz-phase")
│   ├── Quiz Header    — לוגו + progress bar + step label
│   └── 5 שאלות       — בחירה בודדת, מעבר אוטומטי
│
├─ LOADING SCREEN      (id="loading-screen")
│   └── Spinner + progress bar אנימציה + "מנתחים את התשובות שלך..."
│
└─ VSL PHASE           (id="vsl-phase")
    ├── 1. NAV BAR          — לוגו בלבד (sticky)
    ├── 2. URGENCY BAR      — countdown + קוד קופון HOOK20
    ├── 3. STICKY CTA       — מופיע בגלילה, מחיר 290₪ + כפתור
    ├── 4. HERO             — H1 + VSL video (Vimeo autoplay) + CTA + stats
    ├── 5. VIDEO TESTIMONIALS — קרוסל וידאו המלצות (Vimeo embeds)
    ├── 6. CLIENT LOGOS     — גריד לוגואים (11 לקוחות, PNG לבן)
    ├── 7. PAIN LOOP        — "reading loop" נקודות כאב ממוקדות
    ├── 8. SOLUTION         — מה מקבלים + feature list ממוספרת
    ├── 9. AWAITS           — benefit cards (גריד)
    ├── 10. TESTIMONIALS    — WhatsApp bubbles + card testimonials
    ├── 11. ABOUT           — cinema cards (גל + טל) + about text
    ├── 12. PHOTO GALLERY   — קרוסל תמונות (gallery-track, swipe)
    ├── 13. PRESS           — ישראל היום — "אמא אני בעיתון!"
    ├── 14. FAQ             — accordion (toggleFaq)
    ├── 15. BUY SECTION     — FOMO pricing + value stack + CTA
    └── 16. FOOTER          — לוגו בלבד
```

---

## 🧩 קומפוננטים — תבניות HTML + CSS

### 1. כפתור ראשי (CTA)

```html
<a href="#buy-section" class="cta-btn cta-btn--hero cta-pulse">
    🔥 סיקרנת אותי!
</a>
```

```css
.cta-btn {
  background: linear-gradient(135deg, var(--cyan-dk), var(--cyan));
  color: var(--black); font-weight: 800; font-size: 18px;
  padding: 16px 28px; border-radius: var(--r-lg);
  box-shadow: 0 4px 24px var(--cyan-glow);
  transition: all .22s var(--ease);
}
.cta-btn--hero  { font-size: clamp(17px,4vw,21px); padding: 20px 36px; width:100%; max-width:420px; }
.cta-btn--buy   { font-size: clamp(18px,4.5vw,22px); padding: 22px 40px; width:100%; display:block; }
.cta-btn--sm    { font-size: 13px; padding: 10px 18px; }
.cta-pulse      { animation: pulse 2.5s ease-in-out infinite; }
```

---

### 2. Section Tag / Badge

```html
<div class="sec-tag">🎯 כותרת קטנה לסקשן</div>
```

```css
.sec-tag {
  display: inline-flex; align-items: center; gap: 6px;
  background: var(--cyan-xs);
  border: 1px solid rgba(0,212,255,.2);
  color: var(--cyan); font-size: 13px; font-weight: 600;
  padding: 6px 14px; border-radius: 99px;
  margin-bottom: 14px;
}
```

---

### 3. Urgency Bar (סטיקי בראש)

```html
<div class="urgency-bar" id="urgencyBar">
  <div class="urgency-inner">
    <div class="urgency-timer-row">
      <span class="urgency-fire">🔥</span>
      <span class="urgency-text">מחיר השקה – מסתיים בעוד:</span>
      <div class="countdown" id="countdown">
        <div class="cd-block"><span class="cd-num" id="cdH">23</span><span class="cd-label">שע'</span></div>
        <div class="cd-sep">:</div>
        <div class="cd-block"><span class="cd-num" id="cdM">59</span><span class="cd-label">דק'</span></div>
        <div class="cd-sep">:</div>
        <div class="cd-block"><span class="cd-num" id="cdS">00</span><span class="cd-label">שנ'</span></div>
      </div>
    </div>
    <div class="coupon-pill">
      <span class="coupon-label">קוד להנחה 20%:</span>
      <span class="coupon-code" onclick="copyCoupon()">HOOK20</span>
    </div>
  </div>
</div>
```

> **JS:** הtimer מנוהל ב-`app.js` → `startCountdown()` — שומר deadline ב-`sessionStorage`

---

### 4. Scroll Reveal Animation

```html
<div data-scroll-reveal="fade-up" data-delay="120">...</div>
<div data-scroll-reveal="fade-left" data-delay="200">...</div>
<div data-scroll-reveal="fade-right">...</div>
<div data-scroll-reveal="scale-up">...</div>
```

```css
[data-scroll-reveal] {
  opacity: 0;
  transition: opacity .65s cubic-bezier(.4,0,.2,1), transform .65s cubic-bezier(.4,0,.2,1);
}
[data-scroll-reveal="fade-up"]    { transform: translateY(36px); }
[data-scroll-reveal="fade-left"]  { transform: translateX(-40px); }
[data-scroll-reveal="fade-right"] { transform: translateX(40px); }
[data-scroll-reveal="scale-up"]   { transform: scale(.92); }
[data-scroll-reveal].revealed     { opacity: 1 !important; transform: none !important; }
```

> **JS:** `initScrollReveal()` ב-`app.js` — IntersectionObserver עם `data-delay`

---

### 5. Video Testimonials Carousel

```html
<section class="video-testi-section">
  <div class="video-carousel-wrap">
    <button class="video-carousel-btn video-carousel-btn--prev" id="vcPrev">›</button>
    <button class="video-carousel-btn video-carousel-btn--next" id="vcNext">‹</button>
    <div class="video-carousel-track" id="vcTrack">
      <div class="video-slide">
        <div class="video-iframe-wrap">
          <iframe src="https://player.vimeo.com/video/VIDEO_ID?..."></iframe>
        </div>
        <div class="video-slide-meta">
          <div class="video-avatar">א</div>
          <div><div class="video-slide-name">שם לקוח</div>
               <div class="video-slide-role">תפקיד / עסק</div></div>
          <div class="video-stars">★★★★★</div>
        </div>
      </div>
    </div>
  </div>
  <div class="video-dots">
    <span class="video-dot active" data-idx="0"></span>
    <span class="video-dot" data-idx="1"></span>
  </div>
</section>
```

> **Vimeo embed:** `https://player.vimeo.com/video/VIDEO_ID?autoplay=0&badge=0&player_id=...`
> גודל: `max-width: 420px`, `aspect-ratio: 9/16` (portrait vertical)

---

### 6. Client Logos Grid

```html
<div class="logos-grid">
  <div class="logo-item">
    <img src="logo-client-01.png" alt="שם לקוח" />
  </div>
  <!-- עד 11 לוגואים -->
</div>
```

```css
.logo-item img {
  height: 38px; max-width: 130px;
  filter: brightness(0) invert(1); /* הופך לבן */
  opacity: 0.45;
}
.logo-item:hover img { opacity: 0.85; }
```

> **חשוב:** לוגואים חייבים PNG עם **רקע שקוף**. הCSS הופך הכל ללבן אוטומטית.

---

### 7. Pain Loop (reading loop)

```html
<section class="pain-section--loop">
  <div class="pain-statements-wrap">
    <div class="pain-stmt pain-stmt--opener">שאלה פותחת...</div>
    <div class="pain-stmt">נקודת כאב 1<br />
      <span class="pain-dim">פרט נוסף</span>
    </div>
    <div class="pain-divider"></div>
    <div class="pain-stmt--verdict">או</div>
    <div class="pain-stmt">הפתרון...</div>
  </div>
</section>
```

---

### 8. Buy Section — FOMO Pricing (מבנה נוכחי)

```html
<section class="buy-section" id="buy-section">
  <div class="section-inner">

    <!-- Pre-close pain statements -->
    <div class="pain-statements-wrap preclose-loop">...</div>

    <div class="buy-card">

      <!-- Live buyers bar -->
      <div class="fomo-social-bar">
        <span class="fomo-dot"></span>
        <span class="fomo-buyers"><span id="buyersCount">17</span> איש רכשו היום</span>
        <span class="fomo-sep">·</span>
        <span class="fomo-live">🔴 חי</span>
      </div>

      <div class="buy-badge">🔥 מחיר השקה בלעדי – לזמן מוגבל!</div>
      <h2 class="buy-title">כותרת ה-offer</h2>
      <p class="buy-sub">תת-כותרת</p>

      <!-- Countdown timer (אדום, בתוך ה-buy card) -->
      <div class="fomo-timer-wrap">
        <div class="fomo-timer-label">⏳ ההנחה פגה בעוד:</div>
        <div class="fomo-countdown">
          <div class="fomo-cd-block">
            <span class="fomo-cd-num" id="fomo-h">01</span>
            <span class="fomo-cd-lbl">שעות</span>
          </div>
          <span class="fomo-cd-sep">:</span>
          <div class="fomo-cd-block">
            <span class="fomo-cd-num" id="fomo-m">47</span>
            <span class="fomo-cd-lbl">דקות</span>
          </div>
          <span class="fomo-cd-sep">:</span>
          <div class="fomo-cd-block">
            <span class="fomo-cd-num" id="fomo-s">33</span>
            <span class="fomo-cd-lbl">שניות</span>
          </div>
        </div>
      </div>

      <!-- Value Stack -->
      <div class="value-stack">
        <div class="vs-item">
          <div class="vs-left"><span class="vs-icon">🎬</span>
            <div>
              <div class="vs-name">שם המוצר/הדרכה</div>
              <div class="vs-desc">פרט תיאור קצר</div>
            </div>
          </div>
        </div>
        <!-- item נוסף לכל bonus -->
      </div>

      <!-- Price — מחיר מחוק + מחיר נוכחי -->
      <div class="buy-price-wrap fomo-price-wrap">
        <div class="fomo-price-tag">המחיר המלא</div>
        <div class="buy-price-row">
          <div class="buy-price-original fomo-original">360 ₪</div>
          <div class="fomo-arrow">→</div>
          <div class="buy-price-main">290 ₪</div>
        </div>
        <div class="buy-price-note">כולל מע"מ | גישה מיידית במייל</div>
      </div>

      <!-- CTA -->
      <a href="PAYMENT_LINK" target="_blank" class="cta-btn cta-btn--buy cta-pulse" id="main-buy-btn">
        🚀 לרכישה מיידית – 290 ₪
      </a>

    </div>
  </div>
</section>
```

---

### 9. FAQ Accordion

```html
<div class="faq-item">
  <button class="faq-q" onclick="toggleFaq(this)">
    <span>שאלה?</span>
    <span class="faq-icon">+</span>
  </button>
  <div class="faq-a">
    <p>תשובה מפורטת...</p>
  </div>
</div>
```

> **JS:** `toggleFaq(btn)` ב-`app.js`

---

### 10. Photo Gallery (קרוסל תמונות)

```html
<div class="photo-gallery" id="photoGallery">
  <button class="gallery-btn gallery-btn--prev" id="galleryPrev">›</button>
  <button class="gallery-btn gallery-btn--next" id="galleryNext">‹</button>
  <div class="gallery-track" id="galleryTrack">
    <div class="gallery-slide">
      <div class="gallery-slide-frame"><img src="action1.jpg" alt="תיאור" /></div>
    </div>
    <!-- slides נוספות -->
  </div>
</div>
```

> תומך ב-touch/swipe ו-resize — JS ב-inline script בתחתית `index.html`

---

## ⚡ JavaScript — פונקציות מרכזיות

### app.js

| פונקציה | תפקיד |
|---|---|
| `selectOption(btn, questionNum)` | קוויז — בחירת תשובה + מעבר שאלה |
| `showLoadingScreen()` | מסך טעינה + progress bar אנימציה |
| `showVslPage()` | חושף VSL, מזריק Vimeo src ל-iframe |
| `startCountdown()` | countdown 24h ב-urgency bar (sessionStorage) |
| `copyCoupon()` | מעתיק קוד HOOK20 ל-clipboard |
| `initStickyCta()` | sticky bar מופיע לאחר 400px גלילה |
| `initScrollReveal()` | IntersectionObserver עם data-delay |
| `initCounters()` | אנימציה קאונטר מספרים (hstat-num.counter) |
| `toggleFaq(btn)` | פותח/סוגר FAQ item |

### inline scripts (תחתית index.html)

| סקריפט | תפקיד |
|---|---|
| Photo Gallery Navigator | prev/next + touch swipe + resize |
| Video Testimonials Carousel | prev/next + dots + touch swipe |
| FOMO Countdown Timer | 1:47h יורד, שמור ב-`sessionStorage('fomo_end')` |
| FOMO Social Proof Counter | מעלה מספר קונים כל 25–80 שניות |

---

## 🗂️ קבצי הפרויקט

```
hook-lashivuk/
├── index.html          ← כל הדף (HTML + inline styles לvideos + inline JS)
├── style.css           ← כל ה-CSS הראשי (1,700+ שורות)
├── app.js              ← לוגיקת קוויז, countdown, scroll reveal, counters
├── logo.png            ← לוגו TV Production (לבן על שקוף)
├── gal.jpg             ← תמונת גל (מייסד) — portrait
├── tal.jpg             ← תמונת טל (מייסד) — portrait
├── press1.jpg          ← תמונת כתבה ישראל היום
├── press2.jpg          ← תמונת כתבה ישראל היום
├── action1–4.jpg       ← תמונות גלריה בשטח
├── logo-client-01.png  ← לוגואי לקוחות (PNG לבן על שקוף)
└── logo-client-02 ... logo-client-11.png
```

---

## 📱 Responsive

```css
/* Mobile first — הכל מבוסס clamp() */
/* אין breakpoints מוגדרים — הכל fluid עם clamp */

/* דוגמאות clamp: */
font-size: clamp(26px, 7vw, 46px);   /* H1 */
font-size: clamp(52px, 12vw, 72px);  /* מחיר */
padding: 0 20px;                      /* section-inner: max-width 740px */
```

---

## ✍️ שפה שיווקית — עקרונות

| עיקרון | הסבר |
|---|---|
| **Pain First** | מתחילים בכאב — הקוויז + pain loop |
| **Direct Response** | כל שורה מיועדת לפעולה, לא תדמית |
| **Specificity** | "150+ עסקים" ולא "אלפי עסקים" |
| **One CTA** | קישור אחד לאורך כל הדף |
| **FOMO Double Layer** | urgency bar countdown + FOMO countdown בתוך buy card |
| **Social Proof** | וידאו + לוגואים + WhatsApp + עיתון |
| **VSL First** | הסרטון הראשי מוזרק רק אחרי הקוויז (autoplay) |

---

## 🔌 אינטגרציות

| שירות | שימוש |
|---|---|
| **Vimeo** | VSL ראשי + וידאו המלצות (iframe autoplay) |
| **Google Fonts** | Heebo (כל המשקלים 300–900) |
| **SessionStorage** | שמירת deadline לשני הcountdowns |
| **mrng.to** | קישור רכישה מקוצר (Poket/כרטיסים) |

---

## 🚀 Quick-Start — עמוד נחיתה חדש

### שלב 1 — תשתית
1. צור תיקייה חדשה: `my-new-product/`
2. העתק: `style.css` + `app.js` + `logo.png`
3. צור `index.html` חדש עם אותו skeleton

### שלב 2 — התאמת תוכן
```
✏️ שנה את אלה בלבד:
├── <title> + <meta description>
├── שאלות הקוויז (5 שאלות)
├── H1 + hero sub
├── Vimeo video ID (iframe data-src)
├── Pain loop statements
├── Solution checklist
├── Testimonials (וידאו + WhatsApp + כרטיסים)
├── Buy card: כותרת, value stack, מחיר, קישור רכישה
└── FAQ שאלות ותשובות
```

### שלב 3 — נכסים
```
📁 החלף תמונות:
├── logo.png         ← לוגו המותג (לבן על שקוף)
├── tal.jpg / gal.jpg ← תמונות מייסדים (portrait 3:4)
├── press1.jpg       ← כתבה (אם רלוונטי)
├── action1–4.jpg    ← תמונות בשטח לגלריה
└── logo-client-XX.png ← לוגואים לקוחות (לבן על שקוף)
```

### שלב 4 — FOMO
```javascript
// ב-app.js — שנה DURATION ל-countdown הרצוי:
var DURATION = 24 * 60 * 60; // 24 שעות

// בbuy section — שנה את ה-FOMO duration:
var DURATION = 107 * 60; // 1:47 שעות (fomo_end)
```

### שלב 5 — פרסום
```bash
git add .
git commit -m "feat: new landing page — [שם מוצר]"
git push origin main
```

---

> 💡 **טיפ מהיר:** כל ה-CSS נמצא ב-`style.css`. סגנונות ספציפיים לרכיבים (photo gallery, video carousel, press section) נמצאים ב-`<style>` inline ב-`index.html` ישירות מעל `</head>`.
