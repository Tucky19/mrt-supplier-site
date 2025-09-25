# MRT Supplier — GitHub Pages Deploy Helper

This repo is configured to **auto-build and deploy** your Next.js site (with `output: 'export'`) to **GitHub Pages**.

## How to use

1. Ensure your Next.js config is set for static export:

`next.config.js`:
```js
/** @type {import('next').NextConfig} */
const nextConfig = {
  output: 'export',
  images: { unoptimized: true },
};
module.exports = nextConfig;
```

2. Commit your whole project to a new GitHub repo (the one that will host the site).
   - Branch: `main`
   - Include your `package.json`, `next.config.js`, pages, components, etc.

3. Add this folder to your repo (keep path exactly):
```
.github/workflows/deploy.yml
```

4. Push to GitHub:
```bash
git add .
git commit -m "Setup GitHub Pages deploy"
git push origin main
```

5. Wait for Actions to finish (1–3 minutes).
   It will:
   - install dependencies (`npm ci`)
   - `npm run build` → creates `out/`
   - upload `out/` as artifact
   - deploy to GitHub Pages automatically

6. In your repo: Settings → Pages
   - Source: GitHub Actions (should already be selected after the first deploy)
   - Optional: set Custom domain to `www.mrtsupplier.com` (if using your domain).

### Notes
- If you want to deploy from `docs/` instead of GitHub Actions, move your exported files into a `docs/` folder and set Pages Source to `/docs`. The provided workflow uses Actions which is more robust.
- To use a custom domain, add a `CNAME` file at the repo root with the domain name (e.g., `www.mrtsupplier.com`).

Happy shipping! 🚀
