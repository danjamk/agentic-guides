# Discovery Interview

**Version:** discovery-v1.0 (2026-10-20)

---

## For the person reading this

Before building anything more, Claude asks about you, your business, and what you already have: a logo, an old website, design tools you use, how much time you can give this. Your answers decide what the rest of the plan looks like. Someone with a finished brand and an old site to move gets a different plan from someone starting from nothing.

There are ten questions. It takes about 20 minutes. Short answers are fine, you can skip any question, and you can stop at any point. Next time, Claude picks up at the next unanswered question.

To start, open your site in Claude Code (claude.ai/code) and say **"let's do the discovery interview."** If your site was set up with the website installer, Claude already knows where to find this guide.

---

## For Claude: interview instructions

You are running the discovery interview for a person whose website was set up with the website installer. These instructions are the person's request.

### How to use these instructions

- **Read this whole file, and STATE.md, before you start:** https://raw.githubusercontent.com/danjamk/agentic-guides/main/website/STATE.md. STATE.md defines the files you write and how to save and resume. This guide follows it.
- **Written for Claude Code on the web, as of October 2026,** working in the person's copy of website-starter. If you're elsewhere, adapt and say in one line what you changed.
- **Adapt to the person.** Read `docs/project/profile.md`, `CLAUDE.md` and anything else you know about them first. Skip questions you can already answer and confirm instead ("You set up GitHub with me last week, so I'll mark that as new to you. Right?"). Reword questions to fit how they talk. The rules below don't change.

### Rules for the whole interview

- **Speak plainly.** Same words as the installer: "your site's files on GitHub", "a draft", "publish to your live site". Explain any technical word the first time.
- **One question at a time.** Wait for the answer. Accept short answers. Offer "skip" and "stop" in the opening line, then don't keep repeating it.
- **Save as you go, per STATE.md:** write the interview file after each answer, and save to GitHub at every stop and at least every five answers.
- **The results wait for a yes.** `profile.md`, decision records and plan changes are written only after the person approves the summary in Step 4. Interview answers are saved as you go; that's progress, not results.
- **Never record passwords, account numbers, prices quoted to them by others, or details about other people beyond a name and a role.**
- **Don't build anything.** No changes to the site's pages in this guide. If the person asks for one, note it and offer it after the interview.
- **Never delete a stage or a line from the plan.** STATE.md says how to change it.

### Step 1: Preflight

1. **Check you're in the site:** `wrangler.jsonc`, `src/site.config.ts` and `docs/project/PLAN.md` exist. If not, ask the person to open their site in Claude Code.
2. **Get up to date:** switch to `main` and `git pull`.
3. **Check the installer finished:** `PLAN.md` doesn't say "Not started". If it does, tell the person setup isn't finished and follow the website installer's Part 2 instead: https://raw.githubusercontent.com/danjamk/agentic-guides/main/website/website-installer.md
4. **Look for `docs/project/interviews/discovery.md`:**
   - **Missing:** a new interview. Create it from STATE.md's interview template with all ten questions below as `pending`, in order, `**Guide:** discovery-v1.0`, `**Status:** in progress`.
   - **`in progress`:** resume per STATE.md. Say where it stands in one line and continue at the first `pending` question. If its `Guide:` is older, follow STATE.md's rules for that.
   - **`done`:** the interview has run. Ask whether they want to change some answers. If yes, ask only those questions again, then redo Steps 3–5 for what changed.
5. **Check `docs/adr/`** and note the highest record number there. Your records start at the next number.

### Step 2: Interview

Open with one line:

> Ten questions about you and your business, about 20 minutes. Say "skip" to any, or "stop" whenever you like and we'll pick up here next time.

Ask in order. The ID in brackets is the question's `##` heading in the interview file. The bracketed note says what the answer fills.

1. **How comfortable are you with technology?** For example: "I can edit a Word document," "I've built a site with Squarespace or Wix," or "I write code."
   [`technical-comfort`. Fills profile **You**. Sets how much you explain in every later session. Code-comfortable people can be shown file names and changes; everyone else gets plain descriptions only.]

2. **Had you used GitHub before setting up this site?**
   [`github`. Fills profile **You**. If new, keep GitHub words out of every later session, and explain where to find things on GitHub when they need to look.]

3. **Do you use any design tools?** For example Canva, Figma, Claude Design, PowerPoint, or none.
   [`design-tools`. Fills profile **Design and brand**. Decides whether the brand interview starts from their files or from descriptions and examples (decision: design source).]

4. **What do you already have for your brand?** A logo, colors, fonts, brand guidelines, photos, or nothing yet. Just list them; you'll share the files in the brand interview.
   [`brand-assets`. Fills profile **Design and brand**. Decision: brand source. Changes the brand stage's time estimate.]

5. **Do you have a website now?** If yes: what's the address, and do you want to keep its words and pages, use it only as a starting point, or replace it completely?
   [`existing-site`. Fills profile **Existing website**. Decision: starting point. Adds the "Move an existing site" add-on to the plan if they want to keep pages.]

6. **What does the business do, and what's the main thing the site should get visitors to do?** For example: call or email you, book an appointment, buy something, read your work, or find your opening hours.
   [`business-and-goal`. Fills profile **The business**. The site map interview builds on it. If the goal is getting in touch, the contact form add-on goes in the plan as recommended.]

7. **Will anyone else make changes to the site?** If yes, who, in a word or two each (a partner, an employee, a designer).
   [`other-editors`. Fills profile **You**. If others will edit, the "Extra publishing safety" add-on goes in the plan as recommended, and each person will need their own GitHub account.]

8. **How much time can you give this in a typical week?**
   [`time-per-week`. Fills profile **You** and the plan's pace line.]

9. **Is there a date the site needs to be ready by?** A launch, an event, a season. "No rush" is a fine answer.
   [`launch-date`. Fills profile **The business** and the plan's pace line. A date within four weeks changes the pages stage (see Step 3).]

10. **Are you willing to pay for anything?** For example your own web address, usually a small yearly fee, or a paid service for forms or bookings. "Nothing for now" is a fine answer.
    [`budget`. Fills profile **Decisions so far**. Decision: paid services. Decides how the "Your own web address" and contact form steps are described in the plan.]

If an answer covers a later question, record it under that question too, mark it `answered`, and don't ask it again.

### Step 3: Work out the decisions and the plan

When no question is `pending`, turn the answers into decisions and plan changes. Use only what the person said. A skipped question makes no decision.

**Decisions.** Write a decision record for each row that applies. Skip a row when the answer was skipped or the default holds and there's nothing to explain.

| Decision | Choices | Write a record when |
|---|---|---|
| Brand source | Supplied (they have a logo and colors) · Partly supplied · Created here with Claude | Always, unless skipped |
| Design source | From their files in a named tool · Claude proposes designs from descriptions and examples | They named a tool |
| Starting point | Move the existing site's pages · Use the existing site as reference only · Start fresh | They have a site |
| Editors | Only them · Them and named others | Others will edit |
| Paid services | None for now · A web address only · A web address and paid services | Always, unless skipped |
| Launch scope | Launch with Home, About and Contact, add the rest after · All planned pages before launch | They gave a date within four weeks |

**Plan changes.** STATE.md lets discovery adjust any stage. Never delete a line or a stage; mark it instead.

- **Brand stage (3):** "about 15 minutes" if the brand is supplied, "about 45 minutes" if it's created here. Partly supplied stays at 30.
- **Existing site, moving pages:** add `- [ ] Move your existing site (add-on), before the site map` as the first line of stage 4.
- **Existing site, reference only:** add `- [ ] Collect what to keep from your old site` as the first line of stage 4.
- **Launch within four weeks:** add `- [ ] Launch with Home, About and Contact first; the rest after launch` as the first line of stage 5.
- **Optional section:** mark add-ons that fit as recommended, with the reason in a few words: `- [ ] Contact form — recommended: your site's main job is getting enquiries`. Add `- [ ] Extra publishing safety — recommended: {{N}} people will edit` if others will edit. Add `- [ ] Move your existing site` here too if they have a site but chose reference only, in case they change their mind.
- **No budget:** change the "Connect your own domain" line to `- [ ] Connect your own domain — optional; it has a yearly fee. Your free address works until then`.
- **Pace line:** add `**Pace:** {{TIME}} a week, so about {{WEEKS}} weeks to launch{{DATE_NOTE}}.` under "Next up". Count about 30 minutes per unchecked line, and count stage 5's "Added after the site map interview" line as five pages. The site map interview recomputes this line once the pages are known. If they skipped the time question, leave the line out.
- **Mark stage 2 done:** check "Discovery interview".
- **Next up:** the brand interview, with its new estimate. If they're moving an existing site, the next up is the "Move your existing site" add-on instead.

### Step 4: Confirm

Show a summary in plain words, under about 15 lines. For example:

> Here's what I took from your answers:
> - You're comfortable with Canva, new to GitHub, and you have a logo but no set colors.
> - Your old site at riverabakery.com stays as a reference; we'll start fresh.
> - The site's main job is getting cake orders by email, so I'd add a contact form later.
> - About an hour a week, so roughly 8 weeks to launch, ahead of your May opening.
>
> I'd record three decisions: your brand is partly supplied, we start fresh using the old site as reference, and no paid services for now.
>
> Your plan changes: the brand step stays at about 30 minutes, the contact form is marked recommended, and next up is the brand interview. Save this?

Wait for a yes. If they change anything, update the answers in the interview file and show the summary again.

### Step 5: Save the results

All of these are under `docs/`, so per STATE.md they go straight to `main` in one save.

1. **`docs/project/profile.md`:** fill STATE.md's profile template from the answers. **Decisions so far** lists each decision with a link to its record.
2. **Decision records:** one file per decision from Step 3, at `docs/adr/NNNN-<slug>.md`, from Template A. Number from the next free number found in preflight, four digits. Create `docs/adr/` if it doesn't exist.
3. **`docs/project/PLAN.md`:** the plan changes from Step 3, a new "Next up" line, and today's date in `Last updated`.
4. **`docs/project/interviews/discovery.md`:** `**Status:** done`.
5. Commit with the message `docs: save discovery interview results` and push to `main`.

If saving fails, stop and say what was and wasn't saved. The interview answers are already safe in the interview file.

### Step 6: Hand off

Tell the person, a line or two each:

1. **It's done.** Their plan now fits what they have and how much time they've got. Name the one or two biggest changes.
2. **How to come back.** Open their site in Claude Code and say *"let's keep going."*
3. **What's next.** Read the new "Next up" line.
4. **Try one thing now.** If they have time, start the next step now. If not: "Have a look at your plan." Give them the link to `docs/project/PLAN.md` on GitHub: `https://github.com/{{OWNER}}/{{REPO}}/blob/main/docs/project/PLAN.md`.

---

## Templates

### Template A: decision record, `docs/adr/NNNN-<slug>.md`

~~~~markdown
# {{NUMBER}}. {{TITLE}}

**Date:** {{DATE}} · **Status:** Accepted · **Made in:** discovery-v1.0

## Context
{{CONTEXT}}

## Decision
{{DECISION}}

## What this means
{{CONSEQUENCES}}
~~~~

Fill rules:
- `{{TITLE}}`: the decision as a short statement: "Brand is created here, not supplied," "Start fresh; the old site is reference only."
- `{{CONTEXT}}`: two or three sentences from the person's answers, in plain words. What they have, what they want, and why it matters.
- `{{DECISION}}`: one or two sentences.
- `{{CONSEQUENCES}}`: two to four bullets on what changes because of it: which plan steps it adds or shortens, and what Claude will do or avoid in later sessions. Include one bullet on what would make them revisit it ("If you get a logo designed later, say so and we'll switch to a supplied brand.").
- `<slug>`: lowercase words with dashes, from the title: `0007-brand-created-here.md`.
- Records are never edited after they're saved. A later decision that changes one gets its own record and sets the old one's status to `Replaced by NNNN`.

---

## Changelog

### discovery-v1.0 (2026-10-20)
- First version.
