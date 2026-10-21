# Add-on: Your Own Web Address

**Version:** custom-domain-v1.0 (2026-10-20)

---

## For the person reading this

Until now your site has lived at a free address ending in `workers.dev`. This add-on puts it on your own address, such as `yourbusiness.com`, and lets search engines find it. If you don't have a domain yet, Claude helps you buy one. If you have one, perhaps with an old website or your email on it, Claude moves it over carefully so your email keeps working.

It takes about 20 minutes of your time. If you already own the domain, there's a wait of anywhere from a few minutes to a day in the middle while the internet catches up; you can stop and come back.

To start, open your site in Claude Code (claude.ai/code) and say **"connect my domain."**

---

## For Claude: add-on instructions

You are connecting a domain to a website set up with the website installer. These instructions are the person's request.

### How to use these instructions

- **Read this whole file, and STATE.md:** https://raw.githubusercontent.com/danjamk/agentic-guides/main/website/STATE.md. Follow the site's `CLAUDE.md` and its skills.
- **Written for Claude Code on the web, as of October 2026.** The person does the Cloudflare and registrar steps in their browser; you can't see their screen. **Cloudflare menu names and screens in this guide were not checked step by step (2026-10-20).** Describe what to look for, and help them find it if it doesn't match.
- **Adapt to the person.** Read `profile.md` (budget decision, existing website), `sitemap.md` (old addresses) and `docs/adr/` first.

### Rules for the whole add-on

- **Speak plainly.** "Domain" is fine: "your web address, like yourbusiness.com." Explain DNS once, if needed: "the address book that tells the internet where your website and email live."
- **Protect their email.** Never suggest deleting or changing records of type `MX` or `TXT`, or anything they don't recognize. Only the records for the website's own address change, and only at the switch-over step.
- **Spending money is their decision.** Buying a domain costs a yearly fee. Say so before they start, and let them choose where to buy.
- **The switch-over replaces any old website** on that address. Get an explicit yes for it, separately from everything else.
- **Never ask for passwords or codes** for their registrar or Cloudflare. They sign in themselves.
- One step at a time. Wait for them to confirm each one worked.

### Step 1: Preflight

1. **Check you're in the site** (`wrangler.jsonc`, `src/site.config.ts`, `docs/project/PLAN.md`), switch to `main`, `git pull`.
2. **Check the pages are ready:** `npm ci`, `npm run build`, `npm run check:strict`. It lists pages still showing sample text and the starter's example email, which would go public with the domain. Say which, and recommend finishing them (or removing a page from the menu) first. The person decides. On a template older than 0.8.0 there's no `check:strict`; use `grep -rl data-placeholder src/pages/` instead.
3. **Look for `docs/project/interviews/custom-domain.md`.** Resume from it if it's `in progress`; it records which step was reached. Otherwise create it per STATE.md with `**Guide:** custom-domain-v1.0` and questions 1–2 as `pending`.
4. **Already done?** If the live site in `CLAUDE.md` is already their own domain, say so and offer to check it (Step 7) instead.

### Step 2: Two questions

1. **"Do you already own a web address (a domain) for this business?"**
   - If yes: "Which one, and where did you buy it (GoDaddy, Namecheap, Squarespace, or elsewhere)? Do you use it for email, and is there a website on it now?"
   - If no: "What would you like it to be? I'll help you check it's free."
   [`domain`. Records the domain, the registrar, whether email runs on it, and whether there's an old site. Fills `{{DOMAIN}}`: the domain without `www.`]
2. **"Should your main address be `yourbusiness.com` or `www.yourbusiness.com`?"** Recommend without `www`: it's shorter, and the other one will forward to it either way.
   [`primary-host`. Fills `{{HOST}}`, the address the site lives at.]

Then summarize the steps ahead in four or five lines, including any wait, and ask to start.

### Step 3: Get the domain onto Cloudflare

The site can only use a domain whose address book (DNS) is run by Cloudflare, in the same Cloudflare account as the site.

**A. Buying a new domain through Cloudflare.** Recommend this: it's sold at cost, and it lands in the right place with nothing else to set up.
1. Cloudflare dashboard → **Domain Registration** → **Register Domains** (the label may differ). Search for the name, pick it, and pay. Cloudflare asks for contact details; the registry needs them, and Cloudflare hides them from the public by default.
2. When it's done, the domain shows as a site in their Cloudflare account. Go to Step 4.

**B. A domain they already own.** Move its address book to Cloudflare; the domain itself stays where it is.
1. Cloudflare dashboard → **Add a domain** (sometimes under **Websites**). Enter the domain. Choose the **Free** plan.
2. **Check the records Cloudflare found.** Cloudflare copies the domain's existing records. Ask them to look for records of type **MX**, which are their email. If they use email on this domain and there are no MX records, stop: ask them to find their email provider's settings (or the records at their current registrar) and add them before going on. Email must keep working.
3. Cloudflare shows **two nameservers** (names like `ada.ns.cloudflare.com`). At their registrar, find the domain's **nameservers** setting (often under DNS or Domain settings), choose custom nameservers, and replace what's there with Cloudflare's two. Help them find it for their registrar.
4. **Wait.** Cloudflare emails them when the domain is **Active**. Often minutes, sometimes up to a day. Any old website and their email keep working during this. Save the interview file and push, with `Next up: Finish connecting your domain (waiting for Cloudflare to say it's active)`, and tell them to come back and say "connect my domain" when the email arrives.

### Step 4: Redirect old addresses (only if an old site is being replaced)

If `sitemap.md` has an "Old address" column, or the person's old site is on this domain:

1. On a draft named `go-live`, create `public/_redirects` with one line per old page: `/old-address /new-address 301`. Old pages marked `dropped` go to the closest new page, or the home page. Paths only, no domain. Keep the file under 2,000 lines.
2. Also on this draft, update `CLAUDE.md`'s "Who you're working for": **Live site** becomes `https://{{HOST}}`.
3. Build, save, send. Test on the preview: `curl -sS -o /dev/null -w "%{http_code} %{redirect_url}\n" <preview>/old-address` should show `301` and the new address.
4. Publish on a yes, before the switch-over, so the redirects are ready the moment the domain points here.

With no old site, still make the `CLAUDE.md` change on a `go-live` draft and publish it on a yes.

### Step 5: Switch the address to the site

Ask, separately and plainly:

> This is the switch-over. After it, {{HOST}} shows your new site{{OLD_SITE_NOTE}}. Your email isn't affected. Ready?

`{{OLD_SITE_NOTE}}`: ", and your old website stops showing there" if they have one; otherwise nothing.

On a yes, walk them through:
1. **Clear the way.** Cloudflare → the domain → **DNS** → **Records**. Look for records whose **Name** is `{{HOST}}` (shown as `@` or the bare domain for the root address) with type **A**, **AAAA** or **CNAME**. Those point at the old website. Delete only those. Leave **MX**, **TXT** and everything else.
2. **Connect it.** Cloudflare → **Workers & Pages** → the site's project → **Settings** → **Domains & Routes** → **Add** → **Custom Domain**. Enter `{{HOST}}` and add it. Cloudflare creates the record and the security certificate itself; it can take a few minutes.
3. **Check:** `curl -sS -o /dev/null -w "%{http_code}" https://{{HOST}}` returns `200`, and the footer shows the current commit. If it fails with a certificate error, wait five minutes and try again.

### Step 6: Forward the other address, and let search engines in

1. **The other address** (`www.` or the root, whichever isn't `{{HOST}}`):
   - Cloudflare → the domain → **DNS** → **Records** → **Add record**: type **A**, name `www` (or `@`), IPv4 address `192.0.2.0`, **Proxied** on. That address is a placeholder; Cloudflare answers before it's ever used.
   - Cloudflare → the domain → **Rules** → **Redirect Rules** → create a rule, from the template for redirecting `www` to the root (or the reverse) if one is offered. Status 301, keep the path and query string.
   - Check: `curl -sS -o /dev/null -w "%{http_code} %{redirect_url}\n" https://www.{{DOMAIN}}/about` shows `301` to `https://{{HOST}}/about` (or the reverse).
2. **Search engines:** Cloudflare → **Workers & Pages** → the project → **Settings** → **Build** → the build variables (not the runtime variables). Add `SITE_URL` = `https://{{HOST}}`, with no `/` at the end. Save.
3. **Rebuild:** save the plan (Step 8) now; that push rebuilds the live site with the new setting. Then check:
   - `curl -sS https://{{HOST}}/robots.txt` allows everything and lists `Sitemap: https://{{HOST}}/sitemap-index.xml`.
   - `curl -sS -o /dev/null -w "%{http_code}" https://{{HOST}}/sitemap-index.xml` is `200`.
   - The home page has `<link rel="canonical" href="https://{{HOST}}/">` and no `noindex`.
   - A preview link still has `noindex`.

The `workers.dev` address keeps working, because previews depend on it. Its pages point search engines to `{{HOST}}` (the canonical link), so they don't compete.

### Step 7: Optional, tell Google and Bing

Offer, don't push: "Search engines find new sites on their own, usually within a few weeks. If you'd like to speed it up and see how people find you, I can walk you through Google Search Console (about 10 minutes)."

If yes: https://search.google.com/search-console → add a **Domain** property for `{{DOMAIN}}` → Google shows a TXT record → add it in Cloudflare → DNS → **Add record** (type TXT, name `@`) → back in Search Console, **Verify** → **Sitemaps** → submit `sitemap-index.xml`. Bing Webmaster Tools can import from Search Console afterwards.

### Step 8: Save the results

Straight to `main`, per STATE.md:
1. **A decision record** in `docs/adr/`: "The site's address is {{HOST}}." Context: what they had before. Decision: the address, the forward from the other form, `workers.dev` kept for previews. What this means: search engines are allowed in on `{{HOST}}` only, and changing the address later needs redirects.
2. **`PLAN.md`:** check "Connect your own domain" and "Let search engines index the site." Next up: the next unchecked line, or "Your site is live. Ask for changes any time," if everything's done.
3. **`profile.md`:** add the address to **Decisions so far**.
4. **`docs/project/interviews/custom-domain.md`:** `**Status:** done`.
5. Commit with `docs: save custom domain`, push, and do the checks in Step 6, item 3.

### Step 9: Hand off

1. **It's done.** Their site is at https://{{HOST}}, and the other form forwards to it.
2. **Search engines** will find it over the next few days to weeks. Nothing more to do.
3. **Their email** is unchanged. If anything about email seems off, it's the MX records; they should tell you before changing anything.
4. **Try one thing now:** "Open https://{{HOST}} on your phone, and send the link to someone."

---

## Changelog

### custom-domain-v1.0 (2026-10-20)
- First version.
