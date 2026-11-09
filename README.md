# NKT Sidebar

A lightweight, static sidebar for **Nashediyon Ki Toli**. Built with vanilla HTML, CSS and JavaScript modules; no build step or backend required.

## Project structure

```text
nkt-sidebar/
├── index.html
├── README.md
├── css/
│   └── styles.css
├── js/
│   ├── app.js
│   ├── chess-api.js
│   ├── config.js
│   ├── music-player.js
│   └── ui.js
└── assets/
    ├── images/
    └── music/
        ├── 01-the-first-move.mp3
        ├── 02-midnight-gambit.mp3
        ├── 03-quiet-calculations.mp3
        ├── 04-the-kings-march.mp3
        └── 05-after-the-checkmate.mp3
```

## Automated data

The sidebar uses the Chess.com Published-Data API (PubAPI):

- `GET /pub/club/{url-ID}` — club name/description, creation timestamp, member count and average daily rating where the endpoint provides them.
- `GET /pub/club/{url-ID}/members` — member usernames and joined timestamps, grouped into `weekly`, `monthly` and `all_time` activity buckets. The sidebar merges those buckets, de-duplicates usernames and sorts by `joined` to show the three newest join dates.
- `GET /pub/player/{username}` — profile avatar/title for those three displayed members.

Important limitations:
- The members endpoint groups users by club-page activity, not by join recency. The `joined` timestamp is used to sort the merged response, but Chess.com documents that the endpoint cache refreshes at most every 12 hours. Therefore “Recently Joined” means newest join dates among records currently returned by PubAPI, not guaranteed real-time membership.
- PubAPI is read-only. It cannot create tournaments, join members, or access private club information.
- The club API may return 404 if the supplied URL ID is incorrect, unavailable or not yet published. In that case the UI shows an error rather than invented numbers.
- The project caches successful responses in local storage for 12 hours. It does not repeatedly poll the API. Profile requests for the three visible members are made sequentially to reduce the chance of HTTP 429 responses.
- Some browser/Chess.com embedding contexts may restrict cross-origin API requests or module loading. Test the hosted page in the actual club sidebar. If Chess.com blocks external scripts or API fetches in its embed, GitHub Pages alone cannot bypass that restriction; a small proxy backend would be a separate later decision.

## Music: add your files

Put your five own audio files in `assets/music/` using the exact filenames shown in the tree. You can replace the files while keeping the same names; no JavaScript edits are needed. To change track names or file paths, edit only `music` in `js/config.js`.

The player is ready for local MP3 files but will show “NO FILE” until you add them. No external/copyrighted tracks are bundled. Browsers require a user click before audio can start.

## Configure and host

1. Confirm the club's public URL is `https://www.chess.com/club/nashediyon-ki-toli-nkt`.
2. If the URL ID differs, change `clubSlug` and `clubPage` in `js/config.js`, plus the four quick links in `index.html`.
3. Add the five audio files (optional).
4. Test locally with a static server. For example, in VS Code use the Live Server extension, or run `python -m http.server 5500` from this folder and open `http://localhost:5500`.
5. Create a GitHub repository, upload the project contents (not the parent folder), then enable **Settings → Pages → Deploy from a branch → main / root**.
6. Open the GitHub Pages URL over HTTPS and verify data and audio.
7. Add the hosted URL to the appropriate Chess.com club sidebar/embed configuration. The exact insertion field and allowed iframe dimensions depend on the current Chess.com club editor; this project does not automate Chess.com page editing.

## Included / intentionally excluded

Included: club profile facts when returned, member count, average daily rating, club creation year, newest joined records (with the 12-hour PubAPI freshness limitation), member profile links/avatars, static Chess.com shortcuts, five-track local audio player.

Excluded: leaderboards, featured members, tournament countdowns, event feeds, manual announcements, challenges, pulse counters, fabricated statistics, and any content requiring routine source edits.

## Independent project notice

This community-made sidebar uses public Chess.com data. It is not affiliated with, endorsed by, or sponsored by Chess.com.
