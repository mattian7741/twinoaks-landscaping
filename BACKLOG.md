# Twin Oaks Landscaping — BACKLOG

Goal: provider‑agnostic static site, fast conversions, easy migration to home server.

## Now (1–2 hrs)
- [ ] **Contact form (static, no backend)**
  - Option A: Formspree / Basin / Getform (POST webhook). Keep HTML minimal and JS-free fallback.
  - Acceptance: submits OK, spam-protected (honeypot), success/fail states, no cookies.
- [ ] **Add logo asset**
  - Place at `assets/logo.png`; update `<img>` src in header.
- [ ] **.vcf contact card**
  - Generate `assets/twin-oaks.vcf` with: name, phone `+1-267-397-7850`, email `info@twinoaksods.com`, URL, “Lower & Central Bucks County”.
  - Link in header/footer: “Save Contact”.
- [ ] **QR code (SVG)**
  - `assets/qr-site.svg` pointing to `https://twinoaksods.com/` and optional `tel:+12673977850`.
  - Add small “Scan to contact” section.

## Next (this week)
- [ ] **Analytics (privacy-first)**: Plausible (no cookies) via `<script defer data-domain="twinoaksods.com" src="https://plausible.io/js/script.js"></script>`.
- [ ] **Open Graph & social preview**: create `assets/og.jpg` (1200×630); add `og:*` + `twitter:*` meta tags.
- [ ] **404 page**: `404.html` with link back to home; server rule via `.htaccess` `ErrorDocument 404 /404.html`.
- [ ] **Performance polish**: preconnect to `images.unsplash.com`, compress logo (≤30KB), set `loading="lazy"` on gallery.
- [ ] **Accessibility sweep**: alt text, focus states, color contrast (green/brown palette).
- [ ] **Schema enrich**: add `hasOfferCatalog` with top services; `areaServed` as `GeoCircle` or list of towns.

## Later (1–2 weeks)
- [ ] **Gallery**: small grid of 6–9 compressed images; file names like `mowing-yardley-01.jpg`.
- [ ] **Service subpages (SEO)**: `/lawn-mowing-bucks/`, `/tree-trimming-bucks/`, `/snow-removal-bucks/` (static pages).
- [ ] **Google Business Profile**: claim/verify; add NAP, hours, photos, link to site; turn on messaging.
- [ ] **Review engine**: “Review us” link + simple post‑job SMS/email template.
- [ ] **Referral program**: page section; track via unique code in form.
- [ ] **Call tracking (optional)**: swap `tel:` with tracking number provider; keep original as fallback.
- [ ] **Deployment matrix**: extend GH Actions to deploy to home server (`HOME_*` secrets) alongside Hostinger.
- [ ] **Uptime pings**: add free monitor (e.g., UptimeRobot); alert to email.
- [ ] **Security/Headers**: add `.htaccess` with basic `Content-Security-Policy`, `X-Frame-Options`, `Referrer-Policy`.

---

## Implementation Notes

### Contact form (no vendor lock)
HTML (embed on page):
```html
<form action="https://formspree.io/f/REPLACE_ME" method="POST" novalidate>
  <input type="text" name="name" placeholder="Name" required>
  <input type="tel"  name="phone" placeholder="Phone" required>
  <input type="email" name="email" placeholder="Email">
  <textarea name="message" placeholder="What do you need done?" required></textarea>
  <!-- Honeypot -->
  <input type="text" name="_hp" tabindex="-1" autocomplete="off" style="position:absolute;left:-9999px">
  <button type="submit">Request Free Estimate</button>
  <p class="form-status" aria-live="polite"></p>
</form>