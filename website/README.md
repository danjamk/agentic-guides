# Website Installer

A website for your business that you own and change by talking to Claude. It's hosted for free on Cloudflare, and every change shows up on a private preview link before it goes on your real site.

> **In development.** The website guides are being built and tested. This page and the guides it links will change before the first release.

## What you get

- **A live website** at a free web address, with your business name on it, in about 30 minutes.
- **A plan** in small steps of about 30 minutes each: telling Claude about your business, your look and feel, which pages you need, and each page in turn. Do them whenever suits you.
- **Previews before anything goes live.** Claude shows you each change on its own link. Nothing changes on your real site until you say yes.
- **No monthly bill for hosting.** GitHub and Cloudflare are free at this size. You pay for a Claude plan, and for your own web address (a domain) if you want one later.

## What you need

- A computer, for setup.
- A Claude **Pro** or **Max** plan. Setup uses Claude Code on the web, which isn't available on the free plan.
- About 30 minutes. You don't need a GitHub or Cloudflare account yet; Claude helps you make them. GitHub is a website for storing files with a history of every change. Cloudflare runs your site.

## Steps

1. **On a computer, open Claude in your web browser** at claude.ai and start a new conversation.
2. **Paste this message:**

   ```
   Please read the website installer at
   https://raw.githubusercontent.com/danjamk/agentic-guides/main/website/website-installer.md
   and follow its instructions to set up my website.
   ```

3. **Follow Claude's steps.** Claude checks which accounts you have, helps with any you don't, and then you click one button that puts a starter site online.
4. **Switch to Claude Code** when Claude says so. Claude gives you a message to paste there. In Claude Code, it asks two questions (your business name and what you do), shows you a preview, and puts it live when you say yes.

**If Claude says it can't open the link,** download the installer instead. Open [this page](https://github.com/danjamk/agentic-guides/blob/main/website/website-installer.md) and click the download button (a downward arrow) near the top right. Drag the file into the conversation and type: **Run this installer.**

## Coming back

Open claude.ai/code, pick your site, and say **"let's keep going."** Claude reads your plan and suggests the next step. You can stop at any point, mid-question included, and pick up later.

## The steps

Your plan lists these in order. Each is a separate guide Claude follows inside your site; you just say the phrase.

| Step | What happens | Time | Say | Guide | Status |
|---|---|---|---|---|---|
| Setup | Accounts, a live starter site, your name on it | About 30 minutes | (see Steps above) | [website-installer.md](website-installer.md) | Ready to test |
| Discovery | Questions about you, your business and what you already have; your plan is adjusted to fit | About 20 minutes | "let's do the discovery interview" | [interview-discovery.md](interview-discovery.md) | Ready to test |
| Brand | Colors, fonts, logo and the way your site sounds | 15–45 minutes | "let's do the brand interview" | [interview-brand.md](interview-brand.md) | Ready to test |
| Site map | Which pages you need and what each one is for | About 20 minutes | "let's plan the pages" | [interview-sitemap.md](interview-sitemap.md) | Ready to test |
| Pages | One page at a time, each on a preview link first | About 30 minutes a page | "let's work on the <page> page" | [interview-page.md](interview-page.md) | Ready to test |

## Add-ons

Add-ons do things not every site needs. Each is a separate guide Claude follows. You don't need to remember this list: when you ask for something your site can't do yet, Claude checks here and suggests what fits.

| Add-on | What it adds | Effort | Say | Status |
|---|---|---|---|---|
| Contact form | A form visitors fill in to reach you. Claude helps you pick where messages go: your email, a customer-management tool you already use, or a form service | About 30 minutes | | Planned |
| Move an existing site | Brings the pages and words from a site you already have, and keeps old links working | Depends on the size of the site | | Planned |
| [Your own web address](addon-custom-domain.md) | Puts the site on a domain you own, such as `yourbusiness.com`, and lets search engines find it | About 20 minutes, plus waiting for the address to switch over | "connect my domain" | Ready to test |
| [Visitor statistics](addon-analytics.md) | Counts of visits, which pages are read, and where visitors came from | About 10 minutes, after your own web address | "add visitor statistics" | Ready to test |
| Extra publishing safety | A separate check before changes reach the live site, for sites where several people make changes | More technical | | Planned |

## Privacy

- **Your site's files are private** on GitHub, along with your plan and your answers to Claude's questions. Only the website itself is public.
- **Visitors aren't tracked.** The starter site sets no cookies and loads nothing from other companies. Cloudflare processes visits to serve the site.
- Never put passwords or account numbers in your answers to Claude.

## For maintainers

- [STATE.md](STATE.md): the format the website guides save progress in.
- [verification.md](verification.md): dated test results for the Cloudflare and GitHub steps.
- The starter site is [website-starter](https://github.com/danjamk/website-starter).
