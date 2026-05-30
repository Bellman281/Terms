# Smart Word Game — Legal Site

Static HTML legal pages for Smart Word Game. Drop into any GitHub Pages repo and they work — no build step, no dependencies.

## Files

```
index.html        Landing page with links to all four documents.
privacy.html      Privacy Policy — Turkish (primary, KVKK compliant).
privacy-en.html   Privacy Policy — English mirror.
terms.html        Terms of Service — Turkish.
terms-en.html     Terms of Service — English mirror.
```

All four pages share visual style (purple gradient header, white content card, language switcher in the top bar) and are self-contained — CSS is inline, no external assets, no JS frameworks.

## Before publishing — REQUIRED

The documents contain three placeholder tokens, highlighted in yellow in the rendered HTML. Find-and-replace them across all four content pages:

| Token                       | Replace with                                                   |
|-----------------------------|----------------------------------------------------------------|
| `[YOUR_FULL_NAME]` / `[ADINIZ_SOYADINIZ]` | Your full legal name as the data controller / service provider |
| `[YOUR_EMAIL_ADDRESS]` / `[E_POSTA_ADRESİNİZ]` | The privacy / contact email you want listed (can be a Gmail) |
| `[PUBLICATION_DATE]` / `[YAYIN_TARİHİ]` | Publication date in the format `29 May 2026` (or your locale's equivalent) |
| `[ISTANBUL/ANKARA/...]`     | The Turkish city whose courts will have jurisdiction (Terms doc only) |

`index.html` also has a `mailto:[YOUR_EMAIL]` link in the footer to replace.

Quick way to do all of them on macOS:

```bash
cd legal-site
sed -i '' \
  -e 's/\[YOUR_FULL_NAME\]/Omid Lastname/g' \
  -e 's/\[ADINIZ_SOYADINIZ\]/Omid Lastname/g' \
  -e 's/\[YOUR_EMAIL_ADDRESS\]/you@example.com/g' \
  -e 's/\[E_POSTA_ADRESİNİZ\]/you@example.com/g' \
  -e 's/\[YOUR_EMAIL\]/you@example.com/g' \
  -e 's/\[PUBLICATION_DATE\]/29 May 2026/g' \
  -e 's/\[YAYIN_TARİHİ\]/29 Mayıs 2026/g' \
  -e 's|\[ISTANBUL/ANKARA/\.\.\.\]|İstanbul|g' \
  *.html
```

Then open each file in a browser and visually confirm there's no leftover bracket text.

## Publish to GitHub Pages

1. Create a new GitHub repo named e.g. `smart-word-game-legal` (public).
2. Copy these files into the repo root, commit, push.
3. In the repo on GitHub → **Settings** → **Pages** → set **Source** to `main` branch, `/ (root)` folder. Save.
4. After ~1 minute the site is live at `https://<your-username>.github.io/smart-word-game-legal/`.

## App Store Connect / Google Play

When submitting the app, use the following URLs:

- **Privacy Policy URL** (required by both stores):
  `https://<your-username>.github.io/smart-word-game-legal/privacy.html`
- **Terms / EULA URL** (optional but recommended; iOS requires an EULA if you have IAP):
  `https://<your-username>.github.io/smart-word-game-legal/terms.html`
- **Support URL** (required by App Store): point at the landing page (`index.html`) or at a separate support page you set up.

You can also link to the English versions if a reviewer flags the Turkish-default. Both languages live behind the same domain.

## Custom domain (optional)

If you later buy a domain like `smartwordgame.com`:

1. Add a `CNAME` file in the repo root containing just `legal.smartwordgame.com` (or whatever subdomain you want).
2. In your DNS provider, add a `CNAME` record from `legal` → `<your-username>.github.io`.
3. GitHub Pages → **Settings** → **Pages** → **Custom domain** → enter `legal.smartwordgame.com`, check **Enforce HTTPS**.

You then update the URLs you submitted to Apple/Google to use the custom domain.

## ⚠️ Legal disclaimer

These documents are **drafts based on KVKK and standard mobile-app practice**. They are not a substitute for legal advice. Before publishing for a production app — especially one that takes money via in-app purchases — have a Turkish lawyer review them. If you operate as a registered company (LLC, A.Ş., etc.) rather than as an individual, the data-controller section and the IP/EULA framing should be adjusted accordingly.
