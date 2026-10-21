# Page Interview

**Version:** page-v1.0 (2026-10-20)

---

## For the person reading this

This is how each page of your site gets written. Claude asks a few questions about the page (who it's for, what they should do next, what you already have), writes it in your site's voice, and shows it to you on a preview link. You ask for changes until it's right, and it goes live when you say so.

One page takes about 30 minutes. You can stop partway through, and next time Claude picks up where you left off. Do the pages in the order your plan suggests, or any order you like.

To start, open your site in Claude Code (claude.ai/code) and say **"let's work on the <page name> page,"** for example "let's work on the Services page."

---

## For Claude: interview instructions

You are writing one page of a website with a person whose site was set up with the website installer. These instructions are the person's request. Run them once per page.

### How to use these instructions

- **Read this whole file, and STATE.md, before you start:** https://raw.githubusercontent.com/danjamk/agentic-guides/main/website/STATE.md. Follow the site's own `CLAUDE.md`, its skills (**preview**, **publish**), and its decision records in `docs/adr/`.
- **Written for Claude Code on the web, as of October 2026,** in the person's copy of website-starter. If you're elsewhere, adapt and say in one line what you changed.
- **Adapt to the person and the page.** Read `docs/project/profile.md`, `docs/project/brand.md`, `docs/project/sitemap.md` and the page's current file first. Skip questions you can already answer from them, and confirm instead.

### Rules for the whole interview

- **Speak plainly.** One question at a time. "Skip" and "stop" work any time.
- **"Just make something"** or "enough questions": stop asking, mark the rest `skipped`, and write the draft from what you have. Leave out sections that need facts you don't have, and say what's missing in the preview message.
- **Questions off the page's subject** ("can people pay a deposit online?"): answer in two lines, add an `Idea:` line to the plan per STATE.md, and come back to the page.
- **Save as you go, per STATE.md.**
- **Write in the person's voice,** from the Voice section of `brand.md`: how it sounds, "we" or "I", words to use and avoid. Without a `brand.md`, write plainly and warmly, and ask after the first draft whether it sounds like them.
- **Use only facts the person gave you.** Never invent prices, hours, credentials, client names, reviews, numbers or claims. If a section needs a fact you don't have, ask, or leave the section out. Never publish a guess.
- **Every fact is in the page's HTML** (record 0004): text, prices, hours, addresses. A PDF or an embedded video may add to the page, but never replaces the facts in text.
- **No third-party embeds** (maps, videos, booking widgets, review widgets) without the person's sign-off on that company, per `CLAUDE.md`. When they agree, put a plain-text version of what it shows next to it: the address beside a map, a short description or transcript summary beside a video.
- **Accessibility:** one `h1`, headings in order, link text that says where it goes ("See our prices," not "click here"), alt text on every meaningful image, and an empty `alt=""` on purely decorative ones.
- **Every change goes through a preview** and is published only on a yes, per `CLAUDE.md`.

### Step 1: Preflight

1. **Check you're in the site** and switch to `main`, then `git pull`.
2. **Find the page** in `docs/project/sitemap.md` by name or address.
   - **Not in the site map:** ask whether it's a new page. If yes, add it to `sitemap.md` (status `planned`) and to the plan's stage 5 as a `docs/` save first, then continue.
   - **No `sitemap.md`:** in the `guided` way, recommend the site map interview first. In the `direct` way, or if the person goes ahead, continue with just this page.
3. **Check `brand.md` exists.** If not, write in the voice rule from `CLAUDE.md` and continue. In the `guided` way, say it can be adjusted after the brand interview.
   **Check the contact details.** If `email` in `src/site.config.ts` is still `hello@example.com`, ask how visitors should reach them before writing anything: phone, email or both, and the number or address. Pages and the footer link to them. If they want calls only, set `email` to `''`. Set both in `site.config.ts` on this page's draft. [`contact`. The first question in the interview file when asked.]
4. **Look for `docs/project/interviews/page-<slug>.md`** (`<slug>` is the page's address without the `/`; `home` for the home page):
   - **Missing:** create it per STATE.md with `**Guide:** page-v1.0`, `**Status:** in progress`, and questions 1–4 plus the page-type questions from Step 2, all `pending`.
   - **`in progress`:** resume. If a `page-<slug>` draft exists (`git branch -r`), the page has been drafted: show its preview link and ask what to change. Otherwise continue at the first `pending` question.
   - **`done`:** the page has been written. Ask what they'd like to change and make it with **preview**.
5. **Read the page's current file.** Note what's sample text (`data-placeholder`) and what's already real.
6. **Read the site map's notes:** the **Notes for pages** line in `sitemap.md` may hold requests for this page ("Home: link to Seed Library"). Do them in this draft. If the page's row has an old address, ask in question 3 for the old page's words: "Paste the text from your old <page> page, and I'll reuse what still fits."

### Step 2: Interview

Open with one line:

> {{COUNT}} questions about the {{PAGE_NAME}} page, then I'll write it and show you. About 30 minutes. You can stop any time, or say "just make something" and I'll write it from what I have.

`{{COUNT}}`: the questions you'll actually ask, after leaving out what you already know.

**Questions for every page:**

1. **Who is this page for, and what are they looking for when they land on it?**
   Offer your guess from `sitemap.md` and `profile.md`: "I'd guess this is for people comparing a few local bakeries for a wedding cake. Right?"
   [`audience`. Shapes what goes first and what can be left out.]
2. **What should they do after reading it?** Call, email, book, visit, buy, or read another page.
   [`next-step`. Becomes the page's main button or closing link. One main action per page.]
3. **What do you already have for this page?** Text you've written before, photos, a price list, a menu, reviews, documents, links. Paste text here; upload photos and documents to the `docs/project/uploads` folder on GitHub (Add file → Upload files) and tell me when they're in.
   Give the folder's link: `https://github.com/{{OWNER}}/{{REPO}}/tree/main/docs/project/uploads`.
   [`materials`. After uploads, `git pull` and read them. Pasted text is source material: reuse their words where they work.]
4. **Is there anything this page must say, or must not say?** Prices, guarantees, areas you cover, qualifications, things you don't do.
   [`must-say`. Facts here go on the page as they gave them.]

**Questions by kind of page.** Ask the ones whose answers you don't already have from question 3. One at a time. A page that fits two rows (a Cakes page lists products and explains ordering) takes questions from both.

| Page | Ask about |
|---|---|
| Home | Nothing new: it's built from the other pages. Ask only which one or two things should be most prominent. |
| Services, Products, Menu, Work | Each item: name, a sentence on what it is, who it's for, price or how to get one. Which to put first. |
| About | How the business started; who's behind it (names, roles, a line each); what you care about; anything that builds trust: years running, qualifications, memberships. A photo of the people if they have one. |
| Contact, Visit | Every way to reach you, and which you prefer; when you reply; hours; address and whether visitors can come; parking or directions. Whether they'd like a contact form (that's the contact form add-on, later). |
| Reviews | Two to six reviews they have permission to use, with a first name or initials and what the review was about. Never write or edit a review's words beyond fixing typos. |
| How to order, Book, Get involved | The steps, in order; what it costs; how long it takes; where it happens (on this site, by email, on another service). |
| Privacy | Whether anything has been added that collects information: a form, analytics, embeds, a newsletter. The starter's text is accurate only if nothing has. Suggest checking with an adviser if they handle sensitive information. |

[Each answer: `<slug>-<topic>` as its ID, using the page's slug, for example `services-items`, `volunteer-steps`.]

### Step 3: Plan the page

Choose a layout from the shared building blocks in `src/styles/global.css`: `.section` (and `.section--alt` for alternate backgrounds), `.container`, `.reading` (comfortable line length for text), `.lead`, `.button`, `.cards`/`.card` for a set of short items, `.figure` for a photo with a caption. Look at `src/pages/index.astro` for how they fit together. Use semantic tokens for any new style, per record 0005, and put a style only the page needs in the page's own `<style>` block.

A page usually runs:
1. **Heading and lead:** the page's name (or a clear headline) and one or two sentences that answer what the visitor came for.
2. **The substance:** the services, the story, the details. Most important first.
3. **The next step:** the action from question 2, as a `.button` or a clear link.

Keep it as short as the content allows. A page that does its job in 200 words is better than one that pads to 600.

### Step 4: Write the draft

On a draft named `page-<slug>` (the **preview** skill):

1. **Write the page** in `src/pages/<slug>.astro` (`index.astro` for home), in the person's voice. Replace every `data-placeholder` element with real content, and remove the attribute. Keep the `Base` layout.
2. **Title and description:** pass `title` (the page's name, under about 60 characters) and `description` (one sentence under about 155 characters, saying what the page offers) to `Base`. The home page uses the site's description from `site.config.ts`.
3. **Photos:** copy from `docs/project/uploads/` to `public/images/<slug>/`, with plain lowercase names (`team.jpg`). Use `<img src width height alt loading="lazy">` with the image's real pixel size; inside a `.figure` with a `<figcaption>` when a caption helps. The first image near the top of the page doesn't get `loading="lazy"`. If a photo is over about 1 MB, say so and ask for a smaller version, or use it for now and note it.
4. **Documents:** copy to `public/files/` and link them with the file type and size in the link text ("Download our menu (PDF, 240 KB)"). Put the key facts on the page as text too.
5. **Home page:** link to the main pages, and lead with the site's main job from `profile.md`. Update `site.tagline` in `site.config.ts` too if the person's one-liner has changed.
6. **Contact details** belong in `site.config.ts` when other pages need them (`email`, `phone`). Change them there, not in each page. Add facts the person gave that other pages may need (hours, area served) to **The business** in `profile.md`.
7. **Build, save, send, preview.** Give the link to the page, and one line on what's on it.

> Here's the {{PAGE_NAME}} page: {{PREVIEW_LINK}}
> {{ONE_LINE_SUMMARY}} Have a read, on your phone too. What would you change?

Save the interview file and push at this point, even though the page isn't published, so a stop here resumes at the preview.

### Step 5: Revise and publish

- **Changes:** make them on the same draft, save, send, and say what changed. The link stays the same. Keep going until they're happy.
- **"Publish it":** use **publish**. If the site has already launched (live `robots.txt` doesn't say `Disallow: /`), check there's no sample text left on the page first: `grep data-placeholder src/pages/<slug>.astro` finds nothing.
- **"Not yet":** leave the draft. Next up becomes "Finish the {{PAGE_NAME}} page."

### Step 6: Save the results

Straight to `main`, per STATE.md:

1. **`docs/project/sitemap.md`:** the page's status becomes `published`, or `drafted` if they didn't publish. Remove any note in **Notes for pages** that this page took care of.
2. **`docs/project/PLAN.md`:** check the page's line in stage 5 if it was published. Next up: the next unchecked page, about 30 minutes. When every page is checked, Next up is the first line of stage 6, "Go live."
3. **`docs/project/interviews/page-<slug>.md`:** `**Status:** done` when published. Leave it `in progress` if they didn't publish.
4. Commit with `docs: save <page name> page` and push.

### Step 7: Hand off

1. **It's done.** The page is live at {{LIVE_LINK}} (or waiting on the preview).
2. **How to come back.** Open the site in Claude Code and say *"let's keep going."*
3. **What's next.** The next page and its phrase. If it was the last page, say the site is ready to go live and what that involves.
4. **Try one thing now.** "Read the page out loud. Anything that doesn't sound like you, tell me and I'll change it."

---

## Changelog

### page-v1.0 (2026-10-20)
- First version.
