# Discord Ultimate Lookup

A single-page, client-side lookup tool for Discord users, servers, invites and applications. Paste an ID or invite and get the public profile data, creation date, snowflake breakdown and CDN asset links. No backend, no build step, one HTML file.

<!-- Add a screenshot: ![Screenshot](screenshot.png) -->

## Features

**Four lookup modes**

| Tab | Input | What you get |
| --- | --- | --- |
| User | User ID (or a `<@123…>` mention) | Display name, username, avatar, banner, avatar decoration, badges, raw and parsed public flags, premium type, accent and banner colour, account creation date |
| Server | Guild ID | Name, icon, online count and channel count when the public widget is on, instant invite link, creation date |
| Invite | Invite code or a `discord.gg/…` / `discord.com/invite/…` link | Server name, icon, banner, guild ID, channel, expiry, approximate member and online counts, description |
| App / Bot | Application ID | Name, icon, description, public/private bot flag, code-grant requirement, linked guild, creation date |

**Extras**

- Snowflake breakdown for every ID: timestamp, worker, process, increment, Unix ms and age in days
- Avatar size picker (128 to 4096 px) with download and open-in-CDN buttons, plus banner download and full banner preview
- Optional live presence (status, platform, activities, Spotify) through Lanyard
- Copy buttons for IDs and an **Export JSON** button that shows and copies the raw API response
- Last 10 lookups saved as clickable chips
- Shareable links: `?id=<ID>&type=user|server|invite|app` loads a lookup automatically
- Responsive layout, press **Enter** to search

## Usage

1. Pick a tab (User, Server, Invite or App / Bot).
2. Enter an ID, invite code or invite link.
3. Press **Look Up** or **Enter**.

Example share links:

```
https://<your-username>.github.io/<repo>/?id=80351110224678912&type=user
https://<your-username>.github.io/<repo>/?id=discord-developers&type=invite
```

## Run locally

It is a static page. Open `index.html` in a browser, or serve the folder:

```bash
python -m http.server 8000
# then visit http://localhost:8000
```

## Deploy to GitHub Pages

1. Name the file `index.html` and commit it to the repo root.
2. In the repo, go to **Settings > Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, select `main` and `/ (root)`, then save.
4. After a minute the site is live at `https://<your-username>.github.io/<repo>/`.

## Where the data comes from

| Source | Used for |
| --- | --- |
| [japi.rest](https://japi.rest) | User profiles, application info, and a fallback for server info |
| Discord API (`discord.com/api`) | Public server widget and invite details |
| [Lanyard](https://github.com/Phineas/lanyard) | Optional live presence |
| Discord CDN (`cdn.discordapp.com`) | Avatars, banners, icons, decorations |
| Google Fonts | Inter and JetBrains Mono |

Everything runs in your browser. The page has no server of its own and sets no cookies. The only thing it stores is your last 10 lookups, in `localStorage` under `dlookup_hist` (use **Clear** to remove it).

## Limitations

- **Public data only.** Nothing private is available, and many fields can be empty for a given user.
- **Servers:** details only appear when the server's public widget is enabled, or the third-party API knows the server. Private servers show just the creation date derived from the ID.
- **Live presence** only works for people Lanyard tracks, which requires them to have joined the Lanyard Discord server. Otherwise that section stays hidden.
- **Third-party APIs** (especially japi.rest) can rate-limit, change or go offline. If a lookup fails, try again later.
- Browsers may block some cross-origin requests; the page shows an error message when that happens.

## Tech

Plain HTML, CSS and JavaScript with no dependencies or build tooling. Snowflake maths uses `BigInt`, so a current browser is required.

## Disclaimer

Not affiliated with or endorsed by Discord Inc. Use the tool responsibly and respect people's privacy and the [Discord Terms of Service](https://discord.com/terms).

## License

MIT. See [LICENSE](LICENSE).
