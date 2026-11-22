# coachhec.com

Static one-page site for Coach Hec's pickleball lessons. No build step: `index.html` + `style.css`.

## Fill in before launch
Search for `TODO`, `FACEBOOK-PAGE`, and `$XX`.

## Preview locally
    python3 -m http.server 8000   # then open http://localhost:8000

## Deploy (Cloudflare Pages)
1. Push this folder to a GitHub repo.
2. Cloudflare dashboard -> Workers & Pages -> Create -> Pages -> connect the repo.
3. Build command: none. Output directory: `/`.
4. Add custom domain `coachhec.com` under the project's Custom domains tab.

## Calendly setup
- Event types: Private Lesson (1:1), Doubles Match Play (group, capacity 3), Coached Open Play (group, capacity 12).
- Connect his Google Calendar and enable conflict checking so Jimmy Moore and Dill Dinkers sessions block time.
