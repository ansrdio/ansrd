# NIST 800-171 / CMMC Readiness Tracker

A free, practical compliance-readiness tool for small and mid-sized regulated healthcare organizations and Defense Industrial Base (DIB) contractors.

**Live:** [https://ansrd.io](https://ansrd.io)

---

## What's included

| Path | Description |
|------|-------------|
| `/` | Marketing landing page |
| `/app/` | In-browser tracker (all 110 controls, dashboard + SPRS score, Microsoft-stack mapping, CMMC L1/L2 toggle, POA&M, roadmap, access review) |
| `/NIST_800-171_CMMC_Tracker.xlsx` | Downloadable spreadsheet template |

## Tracker features (v2)

- **SPRS score** — DoD self-assessment estimate per the [NIST SP 800-171 DoD Assessment Methodology v1.2.1](https://www.acq.osd.mil/asda/dpc/cp/cyber/docs/safeguarding/NIST-SP-800-171-Assessment-Methodology-Version-1.2.1-6.24.2020.pdf), Annex A: start at 110, subtract each unimplemented control's weighted value (1/3/5). Built-in partial credit for 3.5.3 (MFA) and 3.13.11 (FIPS crypto); 3.12.4 (SSP) treated as a prerequisite (NA), consistent with the methodology; floor −203. Labeled as an estimate, not an official submission.
- **Microsoft-stack mapping** — indicative per-control mapping to Defender, Intune, Entra ID, and Purview, informed by the [Microsoft Product Placemat for CMMC 2.0](https://www.microsoft.com/en-us/download/details.aspx?id=102536), the Microsoft Technical Reference Guide for CMMC L2, and [Microsoft Learn CMMC guidance](https://learn.microsoft.com/en-us/entra/standards/configure-for-cmmc-compliance).
- **CMMC Level 1 / Level 2 toggle** — the 17 FAR 52.204-21 controls (asterisked in Annex A) vs. all 110; filters the tracker and dashboard rollups. SPRS remains calculated over all 110.
- **Roadmap** — phased view generated from open POA&M items (Overdue / 30 / 90 / beyond / unscheduled), highest-weight gaps first, with recoverable SPRS points per phase.
- **Export/Import** — .xlsx and JSON round-trip; state schema unchanged from v1, so existing localStorage data and old JSON exports still load. MSPs can keep one exported file per client.

Note: DoD Class Deviation 2024-O0013 keeps CMMC Level 2 on NIST SP 800-171 **Rev 2** — this tool intentionally does not use Rev 3.

## Tech Stack

- **Static HTML + CSS + vanilla JS** — no build step, no framework
- **SheetJS (CDN)** — XLSX export/import in the `/app` page
- **Vercel** — hosting with automatic HTTPS, deployed via Git
- **Cloudflare Web Analytics** — privacy-respecting, no cookies

## Deploy to Vercel (via GitHub)

### 1. Push to GitHub

```bash
cd /path/to/ansrd/
git init
git add .
git commit -m "Initial commit: NIST 800-171 Readiness Tracker"
git branch -M main
git remote add origin git@github.com:YOUR_USERNAME/ansrd.git
git push -u origin main
```

### 2. Import into Vercel

1. Go to [vercel.com/new](https://vercel.com/new)
2. Click **"Import Git Repository"** → select the `ansrd` repo
3. Framework Preset: **Other** (it's a static site, no build needed)
4. Root Directory: `.` (leave default)
5. Click **Deploy**

Vercel will assign you a URL like `ansrd.vercel.app`. Every push to `main` auto-deploys.

### 3. Add Custom Domain (ansrd.io)

In Vercel dashboard:
1. Go to your project → **Settings** → **Domains**
2. Add `ansrd.io`
3. Vercel will show you the DNS records to set

### 4. DNS Records in Squarespace Domains

Go to [domains.squarespace.com](https://domains.squarespace.com) → select `ansrd.io` → **DNS** → **DNS Settings** → **Custom Records**:

| Type | Host | Value | TTL |
|------|------|-------|-----|
| **A** | `@` | `76.76.21.21` | 3600 |
| **CNAME** | `www` | `cname.vercel-dns.com` | 3600 |

> **Note:** Vercel's A record IP is `76.76.21.21`. Add it as an A record with host `@` (root/apex).

**After adding records:**
- DNS propagation takes 1–30 minutes
- Vercel will auto-provision a TLS certificate once records resolve
- Confirm in Vercel dashboard → **Domains** — status should show ✓ Valid Configuration

### 5. HTTPS

Vercel provisions a free certificate automatically once DNS propagates. No manual action required.

### 6. Cloudflare Web Analytics

1. Go to [cloudflare.com](https://dash.cloudflare.com) → **Web Analytics** → **Add a site**
2. Enter `ansrd.io` (you don't need Cloudflare DNS — just the analytics snippet)
3. Copy the token
4. Replace `CLOUDFLARE_ANALYTICS_TOKEN` in both `index.html` and `app/index.html` with your real token

This provides:
- Page views and unique visitors
- No cookies, no PII collected
- GDPR/CCPA compliant by design

---

## Privacy

- **No accounts, no signup, no data collection**
- All tracker state is stored in the user's browser (`localStorage`)
- No cookies set by the application
- Analytics are privacy-respecting (Cloudflare Web Analytics — no user tracking)

## Accessibility

- Semantic HTML landmarks (`<header>`, `<main>`, `<nav>`, `<section>`)
- ARIA labels on interactive elements
- `focus-visible` outlines for keyboard navigation
- Sufficient color contrast (WCAG 2.1 AA)
- Responsive design (mobile → desktop)
- `prefers-reduced-motion` respected

## File Structure

```
ansrd/
├── index.html                       # Landing page
├── app/
│   └── index.html                   # In-browser tracker
├── NIST_800-171_CMMC_Tracker.xlsx   # Downloadable spreadsheet
├── favicon.svg                      # Vector favicon
├── apple-touch-icon.png             # iOS home screen icon
├── og-image.svg                     # Open Graph preview image
├── robots.txt                       # Search engine directives
├── sitemap.xml                      # Sitemap for crawlers
├── vercel.json                      # Vercel routing & headers config
├── .gitignore
└── README.md                        # This file
```

## Honest Scope

This tracker supports compliance work; it does not by itself make an organization compliant. Control text is summarized from the publicly available NIST SP 800-171 Rev.2 — always refer to the official NIST publication for authoritative wording.

---

Created by **Abolaji Filani** · A practical resource for regulated healthcare cybersecurity readiness.
