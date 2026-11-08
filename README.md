# Adharsh Katari - Clay Portfolio

Two ways to run it:

1. **Static (no backend):** open `public/index.html` (multi-page) or `public/single.html` (single page). Admin edits are saved only in that browser (localStorage).
2. **Full-stack (backend + database):** `npm install` then `npm start` and open http://localhost:3000 . Admin edits are saved in `data/db.json` on the server and show for every visitor. Contact-form messages are stored there too.

## Deploy (Render / Railway / Fly.io / any VPS)
- Build command: `npm install`  |  Start command: `npm start`
- Environment variables: `ADMIN_PASSWORD` (your admin password, required), `SECRET` (any long random string), `DATA_FILE` (optional path, e.g. `/var/data/db.json`).
- IMPORTANT: attach a persistent disk/volume and point `DATA_FILE` at it, otherwise the database resets on each deploy (free tiers with ephemeral disks lose data).
- Pages: `/` multi-page site, `/single.html` single-page site.

## Deploy to Netlify
The included `netlify.toml` publishes the static site from `public/`, so `/` serves `public/index.html`. This static deployment does not run the Express API: admin edits and contact messages are saved only in each visitor's browser. Use a Node host listed above for shared edits and server-stored messages.

## Admin portal (hidden from visitors)
There is no admin link on the site. Open it with any of:
- tap/click the footer copyright line 5 times quickly (works on phone and laptop),
- press Ctrl+Shift+A on a laptop,
- add `#katari-owner` to the site address (change this in Admin > Data > Secret admin address).
Then log in with your password. In full-stack mode the login is checked by the server and uploads/edits are saved to the database.

## Files
- `public/` site (index.html, single.html, style.css, app.js, images, resume.pdf)
- `server.js` Express API + JSON-file database
- API: GET /api/data, PUT /api/data (admin), POST /api/login, POST /api/message, GET/DELETE /api/messages (admin), POST /api/password (admin)

To use a hosted database (MongoDB, Postgres, Supabase) replace the load/save functions in `server.js`; the front end only talks to the /api routes.
