# schnellvermieter-com-site

Static country-selector hub for `schnellvermieter.com` — the `x-default` SEO
entry point for the Schnellvermieter brand. It carries no product logic, no
forms, no checkout, and no analytics. It routes visitors to
`schnellvermieter.de` (Deutschland) or `schnellvermieter.at` (Österreich).

Owner: ML Upskill Agents UG (Vilseck, Bayern). No Impressum is served on this
domain in V1 — each country site owns its own legal pages. (If the owner
later wants an Impressum link here, it should link to
`https://schnellvermieter.de/impressum`, never a copy.)

## Stack

None, deliberately. Hand-written `index.html` with inline CSS, served
directly by GitHub Pages from the repo root — no framework, no build step, no
npm. The page has zero interactivity, so a build pipeline would be
maintenance surface with no payoff.

## Files

- `index.html` — the entire product
- `icon.svg` — favicon
- `robots.txt`
- `sitemap.xml`
- `CNAME` — `schnellvermieter.com`

## Rules for future edits

1. **Manual choice always wins.** This is a pure static two-button page. Do
   not add geo-IP redirects, `Accept-Language` auto-redirects, or a
   remembered/cookie-based choice. A later client-side *hint* is acceptable
   only if it ships with an always-visible manual override — that is out of
   scope for this repo as it stands today.
2. **No price anywhere.** Each country site owns its own checkout and
   pricing.
3. **No data capture, no third-party requests.** The page must load exactly
   two requests: `/` and `/icon.svg`. No web fonts, no analytics, no external
   images, no third-party scripts.
4. **Weightless language.** Never "rechtssicher" / "rechtskonform" / any
   legal guarantee, here or in future copy changes.
5. **Tone register**, if copy ever changes: plain, formal, efficient everyday
   *Sie*-German; short sentences; calm; never ornate.

## Deploy

GitHub Pages, deployed from branch `main`, root `/`. Enforce HTTPS once DNS
resolves.

## DNS runbook (Blacknight.ie registrar panel — owner action)

1. Apex `schnellvermieter.com` **A** records → `185.199.108.153`,
   `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   (+ **AAAA** `2606:50c0:8000::153` … `:8003::153` if the panel supports it).
2. `www` **CNAME** → `<github-username>.github.io.` (GitHub then 301s `www`
   → apex once the custom domain is set).
3. Repo → Settings → Pages → Custom domain `schnellvermieter.com`; wait for
   the DNS check; enable **Enforce HTTPS**.
4. DNS hygiene for this apex: null **MX** (`0 .` per RFC 7505), **TXT** SPF
   `v=spf1 -all`, DMARC record, **CAA** `0 issue "letsencrypt.org"` (GitHub
   Pages certificates are Let's Encrypt), DNSSEC on.

## Acceptance checklist

- [x] Page loads with exactly 2 requests (`/` + `/icon.svg`); zero JS; zero
      external origins.
- [x] Copy, metadata, and hreflang cluster match the country sites'
      reciprocal `de-DE` / `de-AT` / `x-default` links.
- [x] Both buttons navigate correctly; both are reachable and visibly
      focusable by keyboard; flag emojis are `aria-hidden`.
- [x] WCAG AA contrast on both buttons (Deutschland button uses `#15803D`,
      darkened from the nominal `#16A34A` grass token — see comment in
      `index.html`).
- [x] Renders sanely at 360px, 768px, and 1280px widths.
- [x] `robots.txt` + `sitemap.xml` reachable; sitemap validates.
