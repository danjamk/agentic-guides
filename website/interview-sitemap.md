# Site Map Interview

**Version:** sitemap-v1.0 (2026-10-20)

---

## For the person reading this

This step decides which pages your site has, what each one is for, and which ones go in the menu. Claude suggests a set of pages that suits your kind of business, and you add, drop or rename them. Then Claude adds each new page to your site with sample text, so you can click through the whole site before any page is written, and your plan gets one step per page.

It takes about 20 minutes. You can stop at any point and pick up later.

To start, open your site in Claude Code (claude.ai/code) and say **"let's plan the pages."**

---

## For Claude: interview instructions

You are running the site map interview for a person whose website was set up with the website installer. These instructions are the person's request.

### How to use these instructions

- **Read this whole file, and STATE.md, before you start:** https://raw.githubusercontent.com/danjamk/agentic-guides/main/website/STATE.md. Follow the site's own `CLAUDE.md` and its skills (**preview**, **publish**).
- **Written for Claude Code on the web, as of October 2026,** in the person's copy of website-starter. If you're elsewhere, adapt and say in one line what you changed.
- **Adapt to the person.** Read `docs/project/profile.md`, `docs/project/brand.md`, `docs/adr/` and anything else you know first.

### Rules for the whole interview

- **Speak plainly.** "Pages," "the menu at the top," "the links at the bottom of every page."
- **One question at a time.** Accept short answers. "Skip" and "stop" work any time.
- **Save as you go, per STATE.md.**
- **Fewer pages is better.** A small business site usually needs four to eight. Suggest a page only when it has a job a visitor needs done. Say so if the person's list grows past about ten: each page is another 30 minutes, and every page has to be kept up to date.
- **Don't write page content here.** New pages get sample text only. The page interview writes each one.
- **Keep the privacy page.** It describes what the site collects. If the person wants to drop it, explain why it stays, in a line.
- **Every change to the site goes through a preview** and is published only on a yes, per `CLAUDE.md`.

### Step 1: Preflight

1. **Check you're in the site:** `src/pages/`, `src/site.config.ts` and `docs/project/PLAN.md` exist.
2. **Get up to date:** switch to `main` and `git pull`.
3. **Read what's known:** `profile.md` (**The business**, **Existing website**), the decision records from discovery (starting point, launch scope), and `PLAN.md` stage 4. If discovery hasn't run, recommend it first. If the person goes ahead, ask what the business does and what the site's main job is before Step 3.
4. **Existing site being moved:** if `PLAN.md` stage 4 has an unchecked "Move your existing site (add-on)" line, that comes first. Recommend running it, because it brings over the old site's page list. If the person wants to plan pages anyway, continue; you'll ask for the old pages in question 4.
5. **Look for `docs/project/interviews/sitemap.md`:**
   - **Missing:** new interview. Create it per STATE.md with `**Guide:** sitemap-v1.0`, `**Status:** in progress`, and questions 1–3 as `pending` (plus question 4 if they have an existing site).
   - **`in progress`:** resume at the first `pending` question.
   - **`done`:** the site map exists. Ask what they'd like to change (add, drop, rename, reorder the menu), make those changes with Steps 4–6, and update `docs/project/sitemap.md`.
6. **List the pages that exist now:** each `.astro` file in `src/pages/` except `404.astro` and `robots.txt.ts`. A page with `data-placeholder` in it still has sample text.

### Step 2: Suggest a starting set

Pick the shape closest to the business from `profile.md`, and adjust it to the site's main job. Combine shapes when the business spans two.

| Kind of business | Suggested pages |
|---|---|
| Local service (trades, cleaning, salon, repair) | Home, Services, About, Reviews, Contact |
| Professional or consultant (accountant, coach, lawyer) | Home, Services, About, Approach or How it works, Contact |
| Food and drink (café, restaurant, bakery) | Home, Menu, About, Visit (hours and location), Contact or Order |
| Shop or maker (selling products) | Home, Products, About, How to order, Contact |
| Creative or portfolio (designer, photographer, writer) | Home, Work, About, Contact |
| Nonprofit or community group | Home, What we do, Get involved, About, Contact |
| Event or venue | Home, The event or The space, Plan your visit, About, Contact |

Then:
- **Main job "get in touch"**: Contact is one click from every page (menu), and the home page will point to it.
- **Main job "book"**: add a Book page, even if booking happens on another service.
- **Main job "buy"**: keep "How to order" or "Products" in the menu.
- **Privacy** is always in the footer links.
- The starter already has **Home**, **About**, **Contact** and **Privacy**, with sample text. Reuse them; don't recreate them.
- **Launch within four weeks** (a discovery record): mark everything beyond Home, About and Contact "after launch."

### Step 3: Interview

Open with one line:

> I'll suggest a set of pages for your site, and you can change it. Three or four questions, about 20 minutes.

1. **The pages.** Show the suggested set as a short list, each page with one line on what it's for:

   > Here's what I'd suggest:
   > - **Home**: what you do and who for, and the next step
   > - **Services**: each service, who it's for, and what it costs or how to get a price
   > - **About**: who you are and why people can trust you
   > - **Contact**: how to reach you
   > - **Privacy**: what the site collects (in the footer)
   >
   > Would you add, drop or rename any?

   [`pages`. Loop until they're happy. Record the final list with each page's name, purpose, and address (`/services`). Addresses: lowercase words with dashes. Keep the page's name in the person's words.]

2. **The menu.** Suggest which pages go in the menu at the top, in order, and which go only in the links at the bottom. Five items at most in the menu, because it wraps onto a second line on phones beyond that. Home doesn't need a menu item when the logo or name links home, but keep it if the person wants it.
   > For the menu at the top, I'd suggest: Services, About, Contact. Privacy goes in the links at the bottom. OK?

   [`menu`. Fills `nav` and `footerLinks` in `src/site.config.ts` and the "In menu" column of `sitemap.md`.]

3. **Order of work.** Suggest an order for writing the pages, and ask if it suits them. Recommend: the page that does the site's main job first (Services, Menu, Products), then About and Contact, then the rest, and **Home last**, because it points to the other pages and is easiest to write once they exist. Pages marked "after launch" go at the end.
   [`order`. Fills the page lines in `PLAN.md` stage 5, in this order.]

4. **Only with an existing site:** "What are the addresses of the pages on your current site? Paste them, or the menu as you see it." If the migration add-on ran, use its list and skip the question.
   [`old-pages`. For each old page, the new page that replaces it, or "dropped." Goes in the "Old address" column of `sitemap.md`, for redirects when the domain moves. Don't fetch the old site; the network may not reach it.]

### Step 4: Confirm

Summarize in under 12 lines: the pages with their addresses, the menu, the footer links, the order of work, and which new pages get sample text. Example ending:

> I'll add Services and Reviews with sample text, update the menu, and show you a preview. Your plan will list one step per page, starting with Services. Go ahead?

Wait for a yes.

### Step 5: Build on a draft

On a draft named `site-map` (the **preview** skill):

1. **New pages:** create `src/pages/<address>.astro` from Template B for each page that doesn't exist yet.
2. **Renamed pages:** rename the file if the address changed (`git mv`), and update the page's title and heading.
3. **Dropped starter pages** (About, for example): delete the file only because the person dropped it in question 1. Remove links to it from other pages.
4. **Menu and footer:** set `nav` and `footerLinks` in `src/site.config.ts`.
5. Build, save, send, and give the preview link. Suggest they click through the menu.

**Publishing:** check whether the site has launched: `curl -sS <live address>/robots.txt`. `Disallow: /` means search engines are still kept out, so it hasn't launched. The plan's "Let search engines index the site" line being checked also means it has.
- **Not launched yet** (the usual case): publish on a yes. Pages with sample text are fine on a site search engines can't see yet.
- **Already launched:** don't publish pages with sample text to the live site. Ask whether to publish only the menu changes that don't involve new pages, or to leave the draft until the new pages are written. Say which you recommend.

### Step 6: Save the results

Straight to `main`, per STATE.md:

1. **`docs/project/sitemap.md`** from Template A.
2. **`docs/project/PLAN.md`:** replace stage 5's "Added after the site map interview" line with one line per page in the agreed order: `- [ ] <Page name> — say *let's work on the <page name> page*`. Pages marked "after launch" get "(after launch)" at the end of the line. Check the site map line in stage 4. Next up: the first page, about 30 minutes.
3. **`docs/project/interviews/sitemap.md`:** `**Status:** done`.
4. Commit with `docs: save site map` and push.

### Step 7: Hand off

1. **It's done.** Name the pages and the menu, with the preview or live link.
2. **How to come back.** Open the site in Claude Code and say *"let's keep going,"* or name a page: *"let's work on the Services page."*
3. **What's next.** The first page in the plan, about 30 minutes.
4. **Try one thing now.** "Click through your site's menu on your phone, and tell me if any page name doesn't feel right."

---

## Templates

### Template A: `docs/project/sitemap.md`

~~~~markdown
# Site map

**Format:** website-state-v1.4 · **Made in:** sitemap-v1.0 · **Last updated:** {{DATE}}

The pages of the site, what each one is for, and where each one stands. The page interview works through this list.

| Page | Address | For | In menu | Status | Old address |
|---|---|---|---|---|---|
{{PAGE_ROWS}}

**Menu order:** {{MENU_ORDER}}
**Footer links:** {{FOOTER_LINKS}}
~~~~

Fill rules:
- `{{PAGE_ROWS}}`: one row per page, in the order of work. "For" is one line on the page's job. "In menu" is `top`, `footer` or `no`. "Old address" is the existing site's address for that page, `dropped` for an old page with no new one (as its own row with Page "—"), or empty.
- **Status** is one of: `planned` (no file yet), `sample text` (file exists with `data-placeholder` content), `drafted` (the page interview has a preview), `published` (written and live). The page interview updates it.
- Leave the "Old address" column out entirely if there's no existing site.

### Template B: a new page with sample text

~~~~astro
---
import Base from '../layouts/Base.astro';
import { site } from '../site.config';
---

<Base title="{{PAGE_NAME}}" description={`{{PAGE_NAME}} at ${site.name}.`}>
  <section class="section">
    <div class="container reading">
      <h1>{{PAGE_NAME}}</h1>
      <p class="lead" data-placeholder>
        {{PURPOSE_SENTENCE}}
      </p>
      <div data-placeholder>
        <p>{{SAMPLE_PARAGRAPH}}</p>
      </div>
    </div>
  </section>
</Base>
~~~~

Fill rules:
- `{{PURPOSE_SENTENCE}}`: the page's purpose from question 1, written as an instruction to the owner: "What you offer, who it's for, and what it costs or how to get a price."
- `{{SAMPLE_PARAGRAPH}}`: one or two sentences saying what will go here and why visitors need it, in the same style as the starter's About page. Not real content.
- Everything marked `data-placeholder` is replaced by the page interview.

---

## Changelog

### sitemap-v1.0 (2026-10-20)
- First version.
