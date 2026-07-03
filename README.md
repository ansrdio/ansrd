# NIST 800-171 / CMMC Readiness Tracker

A free, no-signup, browser-based tool to track your progress against all **110 NIST SP 800-171 Rev 2 controls** — for small/mid-sized healthcare organizations and Defense Industrial Base (DIB) contractors working toward CMMC.

**Live:** [ansrd.io](https://ansrd.io) · **App:** [ansrd.io/app](https://ansrd.io/app/)

## Your data never leaves your browser — and you can verify it

There's no backend. This is static HTML/CSS/JS. Your assessment (statuses, notes, owners, evidence, POA&M) is saved to `localStorage` and **never sent anywhere** — open DevTools → Network and watch: nothing posts your data. Export/Import (`.xlsx` + JSON) is how you back it up or move it between machines. No account, no cookies, no PII.

The only network call is a first-party, cookieless [Vercel Web Analytics](https://vercel.com/docs/analytics) beacon that counts anonymous page views — no user tracking.

## Features

- **110 controls** across all 14 families, each Met / Partial / Gap / Not Started, with owner, notes, evidence, and review date.
- **Readiness %** dashboard with a per-family breakdown.
- **SPRS score** — DoD self-assessment estimate per the [NIST SP 800-171 DoD Assessment Methodology v1.2.1](https://www.acq.osd.mil/asda/dpc/cp/cyber/docs/safeguarding/NIST-SP-800-171-Assessment-Methodology-Version-1.2.1-6.24.2020.pdf), Annex A: start at 110, subtract each unimplemented control's weight (1/3/5). Partial credit for 3.5.3 (MFA) and 3.13.11 (FIPS crypto); 3.12.4 (SSP) treated as a prerequisite; floor −203. *An estimate, not an official submission.*
- **Microsoft-stack mapping** — indicative per-control mapping to Defender, Intune, Entra ID, and Purview, informed by the [Microsoft Product Placemat for CMMC 2.0](https://www.microsoft.com/en-us/download/details.aspx?id=102536) and [Microsoft Learn CMMC guidance](https://learn.microsoft.com/en-us/entra/standards/configure-for-cmmc-compliance).
- **CMMC Level 1 / Level 2 toggle** — the 17 FAR 52.204-21 controls vs. all 110.
- **POA&M + Roadmap** — log gaps, then get a phased remediation view (Overdue / 30 / 90 / beyond), highest-weight gaps first.
- **Access-review cycle** checklist.
- **Export / Import** — `.xlsx` and JSON round-trip. MSPs can keep one file per client.
- **Reset** with a confirmation guard (offers a backup export first).

> DoD Class Deviation 2024-O0013 keeps CMMC Level 2 on NIST SP 800-171 **Rev 2** — this tool intentionally does not use Rev 3.

## Run it locally

No build step. Clone and serve the folder:

```bash
git clone https://github.com/ansrdio/ansrd.git
cd ansrd
python3 -m http.server 8000   # then open http://localhost:8000/app/
```

## Tech

Static HTML + CSS + vanilla JS · [SheetJS](https://sheetjs.com) (CDN) for XLSX · hosted on Vercel · Vercel Web Analytics (cookieless).

## Honest scope

Control text is summarized from the public NIST SP 800-171 Rev 2 — always refer to the [official publication](https://csrc.nist.gov/pubs/sp/800/171/r2/upd1/final) for authoritative wording. This tracker supports compliance work; it does not by itself make an organization compliant, and the SPRS figure is a self-assessment estimate, not an official SPRS submission. It does not grant CMMC certification.

---

Created by **Abolaji Filani**. Issues and suggestions welcome.
