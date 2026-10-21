# Add-on: Visitor Statistics

**Version:** analytics-v1.0 (2026-10-20)

---

## For the person reading this

This add-on shows you how many people visit your site, which pages they read, and roughly where they came from. By default it uses Cloudflare's own statistics, which are free and don't track individual visitors. If you need Google Analytics, for example because you run Google ads, Claude explains what that involves first.

It takes about 10 minutes. Your site needs to be on its own web address first (the "Your own web address" add-on).

To start, open your site in Claude Code (claude.ai/code) and say **"add visitor statistics."**

---

## For Claude: add-on instructions

You are adding visitor statistics to a website set up with the website installer. These instructions are the person's request.

### How to use these instructions

- **Read this whole file, and STATE.md:** https://raw.githubusercontent.com/danjamk/agentic-guides/main/website/STATE.md. Follow the site's `CLAUDE.md` and its skills.
- **Written for Claude Code on the web, as of October 2026.** **Cloudflare and Google menu names in this guide were not checked step by step (2026-10-20).** Help the person find things if they don't match.

### Rules for the whole add-on

- **Statistics are switched on by build variables in Cloudflare,** read by `src/analytics.mjs`. Never paste an analytics snippet into a page or layout.
- **One tool at a time** unless the person asks for both; two tools double the scripts and the privacy text.
- **The privacy page must match what the site does.** Update it in the same draft.
- **Don't give legal advice.** Say plainly what each tool collects, and when a cookie notice may be required. Suggest checking with an adviser where it matters.

### Step 1: Preflight

1. **Check you're in the site,** switch to `main`, `git pull`.
2. **Check the template supports it:** `src/analytics.mjs` exists, and `src/layouts/Base.astro` includes `<Analytics />`. If not, the site is on a template older than 0.7.0: run **template-update** first (it's one of the listed updates).
3. **Check the site is on its own address:** `curl -sS <live address>/robots.txt` doesn't say `Disallow: /`. Statistics load only on builds search engines can see, so on a `workers.dev`-only site nothing would load. If it isn't, recommend the custom domain add-on first, and stop.
4. **Check for statistics already running:** `curl -sS <live address>/ | grep -o -e cloudflareinsights -e googletagmanager`. If either appears, say which is already on and ask what they'd like to change.
5. Create or resume `docs/project/interviews/analytics.md` per STATE.md, `**Guide:** analytics-v1.0`.

### Step 2: One question

**"What would you like to know about your visitors?"** Offer examples: how many visit, which pages they read, where they came from (Google, social media, another site), what devices they use. Ask also: "Do you run Google ads, or already have a Google Analytics account you need to keep using?"
[`needs`. Everything except ad tracking and an existing Google Analytics account points to Cloudflare Web Analytics.]

Recommend:
- **Cloudflare Web Analytics** (the default): visits, pages, where visitors came from, countries, devices. Free. Cloudflare says it doesn't use cookies or follow individual visitors (Cloudflare's own description; not verified here). Data stays with Cloudflare, which already serves the site.
- **Google Analytics**, only if they need it. It sets cookies and sends visit data to Google. If any of their visitors are in the EU or the UK, they'll likely need a cookie consent banner, which this site doesn't have. In that case, recommend not adding Google Analytics without technical help (`docs/RUNBOOK.md`).

Get a clear choice before going on.

### Step 3a: Cloudflare Web Analytics

1. Cloudflare dashboard → **Web Analytics** → **Add a site** → choose their domain.
2. Cloudflare may switch on its **automatic setup** for that domain, which adds the script by itself. Use the build variable instead, so the setting is visible and previews aren't counted: open **Manage site** and choose the option to **enable with a JS snippet** (manual installation).
3. In the snippet Cloudflare shows, find `"token": "…"` and copy the value between the quotes. It isn't secret; it appears in every page.
4. Cloudflare → **Workers & Pages** → the project → **Settings** → **Build** → build variables. Add `CF_WEB_ANALYTICS_TOKEN` with that value. Save.

### Step 3b: Google Analytics

Only after the person has heard the cookie point in Step 2 and still wants it.

1. https://analytics.google.com → create an account and a **property** for the site, then a **web data stream** for `https://<their domain>`. Google shows a **Measurement ID** starting with `G-`.
2. Cloudflare → **Workers & Pages** → the project → **Settings** → **Build** → build variables. Add `GA_MEASUREMENT_ID` with that ID. Save.

### Step 4: Update the privacy page

On a draft named `analytics`:

1. Edit `src/pages/privacy.astro`. Replace the sentence saying the site runs no tracking with an accurate one for the chosen tool:
   - **Cloudflare Web Analytics:** the site uses it to count visits and see which pages are read; it collects information such as the page visited, the referring site, browser and country, and, by Cloudflare's description, uses no cookies; link to Cloudflare's privacy policy.
   - **Google Analytics:** the site uses it and it sets cookies; what it collects; that Google processes the data; link to Google's privacy policy and how to opt out (https://tools.google.com/dlpage/gaoptout).
   Keep the rest of the page. Write in the voice from `brand.md`, plainly.
2. Build, save, send, preview. Show the privacy page link and say what changed.
3. Publish on a yes. Publishing also rebuilds the live site with the new build variable.

### Step 5: Check it works

1. `curl -sS <live address>/ | grep -o -e 'static.cloudflareinsights.com/beacon.min.js' -e 'googletagmanager.com/gtag/js'` shows the chosen script.
2. A preview link does **not** include it.
3. Ask the person to open their live site in a browser, then look at the statistics dashboard (Cloudflare → Web Analytics, or Google Analytics → Reports → Realtime). Visits can take a few minutes to appear.
4. **If Cloudflare's automatic setup is still on** as well (the page has the beacon twice: `grep -c cloudflareinsights`), ask them to switch it off in Web Analytics → **Manage site**.

### Step 6: Save the results

Straight to `main`, per STATE.md:
1. **A decision record** in `docs/adr/`: "Visitor statistics with <tool>." Context: what they wanted to know. Decision: the tool, switched on by a build variable. What this means: what's collected; the privacy page says so; for Google Analytics, the open question of a consent banner.
2. **`PLAN.md`:** check the Analytics line in Optional. Next up unchanged unless this was it.
3. **`profile.md`:** add it to **Decisions so far**.
4. **`docs/project/interviews/analytics.md`:** `**Status:** done`.
5. Commit with `docs: save visitor statistics` and push.

### Step 7: Hand off

1. **It's on.** Where to see the numbers, with the link.
2. **What it counts,** in a line, and that the privacy page now says so.
3. **To turn it off:** say "turn off visitor statistics." That's removing the build variable, rebuilding, and changing the privacy page back.
4. **Try one thing now:** "Open your site on your phone, then look at the dashboard in a few minutes and find your own visit."

---

## Changelog

### analytics-v1.0 (2026-10-20)
- First version.
