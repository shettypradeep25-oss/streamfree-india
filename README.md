# StreamFree India

A legal-only movie discovery site. It never hosts, embeds, or proxies any video —
every "Watch Now" button links straight to the movie's official page on ZEE5,
Amazon miniTV, or another licensed platform. It's a single static file
(`index.html`, no build step, no server, no dependencies) so it deploys anywhere
that serves static HTML.

## 1. Get a domain

`streamfree.com` is already registered (parked for resale). Pick a name that's
actually free and register it with any registrar — Namecheap, Cloudflare
Registrar, GoDaddy, or (for a `.in` domain) a registrar accredited by NIXI such
as GoDaddy or BigRock. Always do the final availability check on the
registrar's own search box right before buying; third-party WHOIS lookup pages
can be unreliable.

## 2. Deploy the site (pick one — all have generous free tiers)

**Vercel** (easiest)
1. Go to vercel.com → New Project → "Deploy without Git" / drag-and-drop this
   folder, or run `npx vercel` from inside this folder and follow the prompts.
2. Once deployed, go to the project's Settings → Domains → add your domain.
   Vercel shows the exact A/CNAME records to add.


**Netlify**
1. Go to app.netlify.com → Sites → drag this folder onto the "Deploy manually"
   drop zone (or `npx netlify-cli deploy --prod`).
2. Site settings → Domain management → Add a domain → follow the DNS
   instructions it gives you.

**Cloudflare Pages**
1. Go to the Cloudflare dashboard → Workers & Pages → Create → Pages → Upload
   assets → upload this folder.
2. Custom domains tab → Add a domain (works especially smoothly if your
   domain's nameservers are already on Cloudflare).

## 3. Point the domain

Whichever host you pick will show you 1–2 DNS records to add at your
registrar (usually one `A`/`ALIAS` record for the bare domain and a `CNAME`
for `www`). Add those in your registrar's DNS panel; it typically takes a few
minutes to a few hours to propagate. All three hosts above issue a free SSL
certificate automatically once the DNS is verified.

## Keeping the movie list fresh

`index.html` has one JS array called `MOVIES` near the top of the `<script>`
block — each entry is `{t: title, l: language, g: [genres], p: platform,
u: official URL}`. Ad-supported "free" catalogs on ZEE5 / Amazon miniTV /
MX Player / Sony LIV / JioHotstar change week to week, so this list will go
stale. To keep it current either:

- Edit the array by hand periodically, or
- Build a small scheduled job (a cron script, a GitHub Action) that checks
  each platform's official free-movies page and rewrites this array — that's
  a natural next step once the site is live and you want to automate it.

## Legal note

Keep every entry pointing at the title's real page on the platform that
actually licenses it. Don't add links to unofficial mirrors, torrent sites, or
"free streaming" aggregators that rehost content without rights — that's what
keeps this project on the right side of copyright law.
