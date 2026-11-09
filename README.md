# NKT Sidebar — GitHub Pages

A responsive, animated black / antique-gold / emerald sidebar concept for Nashediyon Ki Toli.

## Files
- `index.html` — the sidebar page
- `assets/chess-texture.jpg` — cropped chess background texture from the concept art

## Publish with GitHub Pages
1. Create a public GitHub repository (e.g. `nkt-sidebar`).
2. Upload `index.html` and the `assets` folder, preserving the folder structure.
3. Open **Settings → Pages**.
4. Under Build and deployment, choose **Deploy from a branch**.
5. Select `main` and `/ (root)`, then Save.
6. Wait for GitHub Pages to publish and open the provided URL.

## Customize
Open `index.html` and edit the `NKT_CONFIG` object near the bottom:
- `eventUrl`
- `links.rules`, `links.forums`, `links.events`, `links.challenges`
- `eventDate` (ISO date with timezone)
- `eventName`

The displayed member/stat figures are demo placeholders. Replace them with confirmed values before publishing. The “LIVE*” label is explicitly marked as demo until a data workflow is connected.

## Important
This is a static front-end. It does **not** automatically fetch Chess.com club data. For reliable automation, add a scheduled GitHub Actions workflow that fetches supported public data and publishes a sanitized `data.json`, then update the page to read it. Do not put API keys or private credentials in client-side JavaScript.

## Iframe
First publish and test the GitHub Pages URL in the Chess.com sidebar. If Chess.com blocks iframe embedding, use a compact native HTML/CSS sidebar or link to the hosted full experience instead.
