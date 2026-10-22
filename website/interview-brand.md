# Brand Interview

**Version:** brand-v1.0 (2026-10-20)

---

## For the person reading this

This step gives your site your look and your voice: colors, fonts, logo, and the way your words sound. If you already have a brand, Claude uses it. If you don't, Claude asks a few questions and shows you two or three designs to choose from. Either way, you see your whole site in its new look on a preview link before it goes live.

It takes 15 to 45 minutes, depending on how much you already have. You can stop at any point and pick up later.

To start, open your site in Claude Code (claude.ai/code) and say **"let's do the brand interview."**

---

## For Claude: interview instructions

You are running the brand interview for a person whose website was set up with the website installer. These instructions are the person's request.

### How to use these instructions

- **Read this whole file, and STATE.md, before you start:** https://raw.githubusercontent.com/danjamk/agentic-guides/main/website/STATE.md. Also follow the site's own `CLAUDE.md` and its skills (**preview**, **publish**). This guide uses them.
- **Written for Claude Code on the web, as of October 2026,** in the person's copy of website-starter. If you're elsewhere, adapt and say in one line what you changed.
- **Adapt to the person.** Read `docs/project/profile.md`, `docs/adr/` and anything else you know first. Skip what you can already answer, and confirm instead.

### Rules for the whole interview

- **Speak plainly.** "Colors," "fonts," "the logo at the top of every page." Say "hex code" only if they use it first, and then explain it ("the six-character code for a color, like #2B59C3").
- **One question at a time.** Accept short answers. "Skip" and "stop" work any time.
- **"I don't know" gets a suggestion, not another question.** For feel, colors, examples and voice, propose an answer from `profile.md` and the kind of business ("For a plumber I'd go with dependable, quick, local. OK?"), and take a yes. Record it per STATE.md. Many people can't describe taste but can pick from options, so get to the options quickly.
- **"Enough questions"** or "just make something": mark the remaining taste questions `skipped`, propose answers yourself, and go straight to building.
- **Waiting on someone else** ("I need to ask the board about colors"): mark that question `waiting` per STATE.md, carry on with questions that don't depend on it (voice doesn't depend on colors), and set Next up to say what's awaited.
- **Save as you go, per STATE.md:** the interview file after each answer; save to GitHub at every stop and at least every five answers. Answers are saved on `main`. Switch to the `brand` draft only to change the site, and back to `main` to save answers.
- **Fonts are part of this interview.** Installing free font packages is expected here. Say once, "I'll add two free fonts, stored with your site; nothing to pay," and their yes covers the package rule in `CLAUDE.md`. Skip this when every font you'll use is already installed (the starter's Inter).
- **Never change a color the person supplied.** If a supplied color can't be read clearly on the site (see Step 4), change *where* it's used, or add a darker or lighter shade alongside it, and tell them.
- **Fonts are served from the site itself.** Use font packages from npm (Fontsource) or font files the person owns a web license for. Never link fonts from Google Fonts or any other company's servers; record 0002 and the hard rules in `CLAUDE.md` explain why.
- **Use only files the person gave you** for the logo and brand. Don't take images from other websites, and don't generate a logo. A logo designed elsewhere can replace the text logo later.
- **Colors live in `src/styles/tokens.css` only,** per record 0005: brand colors in the brand layer, and the semantic layer pointing at them.
- **Every change to the site goes through a preview** and is published only on a yes, per `CLAUDE.md`.

### Step 1: Preflight

1. **Check you're in the site:** `wrangler.jsonc`, `src/site.config.ts`, `src/styles/tokens.css` and `docs/project/PLAN.md` exist. If `docs/project/brand-files/` is missing, this site is on a template older than 0.5.0: offer **template-update** first, or create that folder with a one-line `README.md` as a `docs/` save. If `src/styles/tokens.css` has no `.brand-scope`, the site is older than 0.9.0 and an options page won't show each option's colors: apply that update first (its CHANGELOG entry says how).
2. **Get up to date:** switch to `main` and `git pull`.
3. **Check discovery ran:** `docs/project/interviews/discovery.md` has `**Status:** done`. If not, and `PLAN.md`'s way of working is `guided`, recommend doing discovery first (about 20 minutes). In the `direct` way, don't recommend it. Either way, if the person goes ahead, ask question 0 below.
4. **Look for `docs/project/interviews/brand.md`:**
   - **Missing:** a new interview. Create it from STATE.md's interview template, with `**Guide:** brand-v1.0`, `**Status:** in progress`, and the questions for the path you choose in Step 2, all `pending`.
   - **`in progress`:** resume at the first `pending` question. Check for a `brand` draft (`git branch -r`); if one exists, you were past Step 3.
   - **`done`:** the brand is set. Ask what they'd like to change, make that change with **preview**, and update `docs/project/brand.md`.

### Step 2: Choose the path

Read the "Brand source" and "Design source" decision records in `docs/adr/` (from discovery) and the **Design and brand** section of `profile.md`. If the design source names a tool such as Canva, ask for exports from it in Step 3a: the logo as SVG or PNG, and any page that shows their colors and fonts.

| Brand source | Path |
|---|---|
| Supplied: they have a logo and colors | **Bring**: Step 3a |
| Partly supplied: some pieces, such as a logo but no colors | **Bring** for what exists (Step 3a), then options only for what's missing. Usually the colors come from the logo, and the options are two or three font pairings in those colors. Skip Step 3b's questions that the supplied pieces already answer. |
| Created here | **Create**: Step 3b |

**Question 0, only if there's no decision record:** "Do you already have a logo, brand colors or fonts you want to use?" [`brand-source`. Decides the path. No record is written for it here.]

Then voice (Step 3c) on every path.

Open with one line, for example:

> We'll start with your logo and colors, then a few questions about how your site should sound: {{COUNT}} questions, about {{MINUTES}} minutes. Say "skip" or "stop" any time, and "I don't know" is a fine answer; I'll suggest something.

On the create path, open with "We'll start with how you want your business to come across, and I'll show you two or three looks to pick from" instead of the first clause.

`{{COUNT}}`: the number of questions on the chosen path, voice included. `{{MINUTES}}`: the brand stage's estimate in `PLAN.md`.

### Step 3a: Bring path

1. **Upload your files.** "Please upload your logo, and any brand guidelines or color and font details you have, into your site's `docs/project/brand-files` folder on GitHub: open the folder, click **Add file** → **Upload files**, drag them in, then click **Commit changes**. Tell me when they're in."
   Give the folder's link: `https://github.com/{{OWNER}}/{{REPO}}/tree/main/docs/project/brand-files`.
   [`files`. Then `git pull` and list what arrived: `git log -3 --stat --format='%s' -- docs/project`. People often upload to the wrong folder, so accept files in `docs/project/uploads/` too, and move them to `brand-files/` as a `docs/` save. Read PDFs and images. If the file isn't a logo (a phone photo, say), describe what you see and ask again. If a logo is missing, say what would help (an SVG, or a PNG at least 512 pixels wide with a transparent background) and carry on without it.]
2. **Colors.** "Do you have exact codes for your colors? They're often in brand guidelines, or your designer or printer will have them. If not, I can take them from your logo."
   [`colors`. From guidelines, the person, or the logo file: an SVG's `fill` and `stroke` values; for a PNG, describe the colors you see and ask the person to confirm or find the codes. Name each color by its role: main, second, and any accents.]
3. **Fonts.** "Do you know which fonts your brand uses?"
   [`fonts`. For each, check it's available as a free package: `npm view @fontsource-variable/<slug> version`, then `npm view @fontsource/<slug> version` (slug: lowercase, spaces as dashes). If neither exists, ask whether they own font files with a web license. If not, propose the closest free font and say why it's close. If they don't know, propose one heading and body pairing that suits the logo's style, in words ("a rounded, friendly heading font with a plain body font"), and take a yes. Show it on the brand preview in Step 4; no options page is needed for one pairing.]
4. **Logo.** "Does your logo include your business name written out, or is it a symbol on its own?"
   [`logo-type`. Name included: the header shows only the logo. Symbol only: the header shows the logo and the name as text. Also ask whether there's a square or icon version, for the browser tab.]

### Step 3b: Create path

1. **Feel.** "Give me three words for how you want your business to come across." For example: warm, expert, playful, calm, bold, traditional.
   [`feel`. Drives color and font choices for the options.]
2. **Colors.** "Any colors you love, or want to avoid? Think of your shopfront, packaging, uniforms or van, if you have them."
   [`colors-like`. Use existing physical-brand colors where they fit, so the site matches what customers already see.]
3. **Examples.** "Name one to three websites or brands whose look you like, and what you like about them."
   [`examples`. Don't fetch the sites; your network access may not reach them, and their words are enough. Take the qualities, never their assets.]
4. **Options.** Build two or three options (below) and show them. "Which do you like best? You can also mix them: 'A's colors with B's fonts'."
   [`option-choice`. Record the choice and any mix.]

**Building the options:**

- Start a draft named `brand` (see the **preview** skill).
- Each option: a main color, a neutral set (text, secondary text, borders, light background), and a font pairing (heading and body, or one font for both). If the person named a second color, or accepted one you suggested, give each option an accent (`--brand-accent`) used for highlighted backgrounds (`--color-bg-highlight`), so it isn't lost. Make the options differ in feel, not only in hue. Every option must pass the contrast check in Step 4 before you show it.
- Fonts: install each option's font packages on the draft (`npm install @fontsource-variable/<slug>` where it exists, otherwise `@fontsource/<slug>`). At most three font families across all options.
- Add `src/pages/brand-options.astro`, using the `Base` layout with `noindex`. For each option, a `<section class="section brand-scope">` that sets the option's `--brand-*` values (colors and `--brand-font-heading`/`--brand-font-body`) in its `style` attribute. The `brand-scope` class is what makes the page's text, links, buttons and headings use them. `npm run check` skips this page's colors from template 0.10.0; on an older template it reports "sets colors directly" for this page only, which is expected here. Add `section--alt` to every other option so they're easy to tell apart. Each shows: the option's letter and a one-line description; the business name as a heading; the tagline; a short paragraph; a link; a button; a card; and color swatches with their codes. Import the option fonts in this page only.
- Build, save and send, wait for the preview, and give the person `https://brand-{{PROJECT}}.{{SUBDOMAIN}}.workers.dev/brand-options`.
- When they've chosen: remove the options page (`git rm src/pages/brand-options.astro`), uninstall font packages no longer used, and continue on the same draft with Step 4.

**No logo yet:** the header shows the business name in the heading font, which works as a simple text logo. Tell them a designed logo can replace it any time: upload it and say "add my logo."

### Step 3c: Voice, every path

1. **"Give me three words for how your site should sound."** For example: friendly, straightforward, expert, warm, no-nonsense.
   [`voice-words`. Goes in `brand.md` under Voice.]
2. **"Should the site say 'we', 'I', or use the business name? And is it more casual or more formal?"**
   [`voice-person`.]
3. **"Any words or phrases you always use, or ones you'd never use?"** For example, "we say 'clients', never 'customers'," or "no jargon."
   [`words-use-avoid`.]
4. **"Is there a piece of writing that sounds like you want to sound? Yours, or anyone's. Paste a few sentences, or skip."**
   [`voice-example`. Keep up to about 100 words in `brand.md`; summarize anything longer.]

### Step 4: Apply the brand on the draft

On the draft `brand` (create it now if the bring path didn't need one).

1. **Brand tokens** in `src/styles/tokens.css`, brand layer:
   - `--brand-primary`: the main color.
   - `--brand-primary-dark`: about 15% darker, for hover. `--brand-primary-tint`: a very light version, for highlighted backgrounds. Derive these unless the person supplied them.
   - `--brand-ink`, `--brand-slate`, `--brand-line`, `--brand-mist`: neutrals. Use supplied ones, or derive near-neutrals with a slight tint of the main color.
   - Extra supplied colors get their own brand tokens (`--brand-accent`, `--brand-second`), each with a comment saying what it is.
   - Keep the comments saying what each token is for.
2. **Semantic tokens:** change only where needed, for example to use an accent for highlights, or for contrast (next item).
3. **Contrast check.** Every text color must meet WCAG AA against every background it's used on: **4.5:1** for normal text, **3:1** for large text (about 24px, or 19px bold) and for borders of controls and the focus outline. Check at least these pairs, using the resolved colors:

   | Text or element | On |
   |---|---|
   | `--color-text`, `--color-text-muted` | `--color-bg`, `--color-bg-alt`, `--color-bg-highlight` |
   | `--color-link` | `--color-bg`, `--color-bg-alt` |
   | `--color-action-text` | `--color-action-bg`, `--color-action-bg-hover` |
   | `--color-focus` (3:1) | `--color-bg` |

   From template 0.10.0, `npm run check` checks these pairs from `tokens.css`. For the options page, and on older templates, compute contrast with a one-off `node -e` command using the WCAG relative-luminance formula. Don't save it as a script. If a pair fails, change the semantic token to a shade that passes: point `--color-action-bg` at `--brand-primary-dark`, or add a darker `--brand-primary-deep` and use it for links and buttons. Never change a supplied brand color. Note each adjustment for `brand.md`.
4. **Fonts:** install the chosen packages if they aren't already. In `src/layouts/Base.astro`, replace the `@fontsource-variable/inter` import with the new ones, importing only the weights the site uses (400, 500, 700) for non-variable packages. Set `--brand-font-body` and `--brand-font-heading` to the family names the packages define, followed by the fallback list already there. `npm uninstall @fontsource-variable/inter` if it's no longer used. For licensed font files: copy the `.woff2` files to `public/fonts/`, add `@font-face` rules at the top of `src/styles/global.css`, and note the license in `brand.md`.
5. **Logo:** copy the logo from `docs/project/brand-files/` to `public/logo.svg` (or `.png`). Set `logo` in `src/site.config.ts`: `{ src: '/logo.svg', height: 40, showName: <from logo-type> }`. Use a height between 32 and 56 that suits the logo's shape. If a PNG is over about 300 KB, say so and suggest a smaller export.
6. **Favicon** (the browser tab icon): if they gave a square or icon version as SVG, copy it to `public/favicon.svg`. Otherwise write a new `public/favicon.svg`: a rounded square in the main color with the first letter of the business name in white, using a generic font family. Don't use the full logo unless it's square.
7. **Build, save, send, preview** (the **preview** skill). Give the home page link, and suggest they look at the About and Contact pages and on their phone.

### Step 5: Confirm and publish

> Here's your site in its new look: {{PREVIEW_URL}}
> Colors: {{SUMMARY}}. Fonts: {{FONTS}}. {{ADJUSTMENTS}}
> Want any changes, or shall I publish it to your live site?

`{{ADJUSTMENTS}}`: one line on any contrast change ("I used a slightly darker green for buttons so the white text is easy to read"). Leave it out if there were none.

Changes go on the same draft; show the link again. On a yes, use **publish**. On "not yet," leave the draft.

### Step 6: Save the results

Straight to `main`, per STATE.md, whether or not they published:

1. **`docs/project/brand.md`** from Template A.
2. **`docs/project/profile.md`:** update the **Design and brand** bullets.
3. **`docs/project/interviews/brand.md`:** `**Status:** done`.
4. **`docs/project/PLAN.md`:** check the brand line, removing any "— skipped" note. Next up: "Site map interview, about 20 minutes. Say *let's plan the pages*," or in the `direct` way, "Tell Claude what you'd like to change." If they didn't publish, Next up is "Publish your new look. Say *publish the brand preview*."
5. Commit with `docs: save brand interview results` and push.

### Step 7: Hand off

1. **It's done.** Their site has their look, live at {{LIVE_URL}} (or waiting on the preview).
2. **How to come back.** Open the site in Claude Code and say *"let's keep going."*
3. **Their voice is saved.** Every page Claude writes from now on follows it. They can change it any time: "make the site sound more casual."
4. **Try one thing now.** "Ask me to change one color or font, to see how easy it is."

---

## Templates

### Template A: `docs/project/brand.md`

~~~~markdown
# Brand

**Format:** website-state-v1.5 · **Made in:** brand-v1.0 · **Last updated:** {{DATE}}

Claude follows this file whenever it writes words or changes the look of the site.

## Colors

| Color | Code | Used for |
|---|---|---|
{{COLOR_ROWS}}

{{CONTRAST_NOTE}}

## Fonts

- **Headings:** {{HEADING_FONT}}
- **Body text:** {{BODY_FONT}}
- {{FONT_SOURCE}}

## Logo

- {{LOGO_LINE}}
- Browser tab icon: {{FAVICON_LINE}}

## Voice

- **Sounds:** {{VOICE_WORDS}}
- **Writes as:** {{VOICE_PERSON}}
- **Use:** {{WORDS_USE}}
- **Avoid:** {{WORDS_AVOID}}

{{VOICE_EXAMPLE}}

## Where it came from

{{ORIGIN}}
~~~~

Fill rules:
- `{{COLOR_ROWS}}`: one row per brand token: a plain name ("Main green"), the code, and what it's used for on the site. Mark derived colors "(derived)".
- `{{CONTRAST_NOTE}}`: "All text meets WCAG AA contrast (checked {{DATE}})." plus one line per adjustment made in Step 4.
- `{{FONT_SOURCE}}`: "Free fonts, served from the site itself (Fontsource)," or "Licensed font files in `public/fonts/`; license: <what the person said>."
- `{{LOGO_LINE}}`: the file in `public/`, and whether the name shows next to it. "No logo yet; the name shows in the heading font" if none.
- `{{VOICE_EXAMPLE}}`: "**Sounds like:**" and the example as a quote. Remove the line if skipped.
- `{{ORIGIN}}`: one line: "Supplied by the owner (brand guidelines, logo)," or "Created in the brand interview; option B chosen, with option A's fonts."
- Skipped answers: remove the line. Never leave a placeholder.

---

## Changelog

### brand-v1.0 (2026-10-20)
- First version.
