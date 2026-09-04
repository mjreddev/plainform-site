# plainform.app

Static site for **Plainform** — the trading name of MJRed Dev LLC.

Two pages, no build step, no dependencies:

- `index.html` — landing page (the organization website Google Play asks for)
- `privacy.html` — privacy policy (Play requires one per app; this covers all)

---

## Deploy to GitHub Pages

### 1. Push to GitHub

Repo must be **public** — private-repo Pages needs a paid plan.

```bash
cd mjred-site
git init && git add -A
git commit -m "Plainform site"
git branch -M main
git remote add origin https://github.com/mjreddev/plainform-site.git
git push -u origin main
```

### 2. Enable Pages

Settings → Pages → Source: **Deploy from a branch** → branch `main`, folder `/ (root)`.

### 3. DNS at Namecheap

Domain List → Manage → **Advanced DNS**. Delete the default parking records
(Namecheap adds a CNAME `www` → `parkingpage.namecheap.com` and a URL redirect —
both must go), then add:

| Type          | Host | Value                   | TTL       |
|---------------|------|-------------------------|-----------|
| A Record      | @    | 185.199.108.153         | Automatic |
| A Record      | @    | 185.199.109.153         | Automatic |
| A Record      | @    | 185.199.110.153         | Automatic |
| A Record      | @    | 185.199.111.153         | Automatic |
| CNAME Record  | www  | `mjreddev.github.io.` | Automatic |

Namecheap's nameservers must be set to **Namecheap BasicDNS** for the Advanced
DNS tab to apply.

### 4. Custom domain + HTTPS

Settings → Pages → Custom domain: `plainform.app` → Save. GitHub re-checks DNS,
then issues a free Let's Encrypt certificate (usually minutes, occasionally up
to 24h). When **Enforce HTTPS** becomes tickable, tick it.

> **`.app` is HSTS-preloaded.** Browsers refuse to load `.app` over plain HTTP,
> so the site will show errors until the certificate is issued. That is expected
> during setup, not a misconfiguration — wait for the cert, then enforce HTTPS.

### 5. Give the URL to Play

Enter `https://plainform.app` as the organization website in Play Console.

---

## Notes

- `CNAME` and `.nojekyll` are required by Pages — leave them in place.
- Certificates renew automatically; nothing to maintain.
- When SiteProof ships, remove its "In development" tag in `index.html` and add
  the Play listing link.
- The footer and privacy section 1 both state that Plainform is a trading name
  of MJRed Dev LLC, so Play verification can reconcile the developer name with
  the registered entity. Check whether your state requires a DBA filing to
  trade under a name other than the LLC's.
