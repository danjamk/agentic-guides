# Brain Installer

**Version:** brain-v1.0 (2026-10-01)

---

## For the person reading this

This file sets up a personal "brain" for you. The brain is a folder of plain notes that Claude reads at the start of every session, so it remembers your projects, your people, and what you were last working on. Claude asks about your life and work, suggests a set of folders that fits, and builds it once you agree. The folders change over time as your life does.

How to use it:

1. Make an empty folder somewhere easy to find, such as `Documents/Brain`.
2. Open the Claude desktop app and start a new conversation. If your app has separate **Chat** and **Cowork** options, choose **Cowork**.
3. Give Claude access to the empty folder. Claude asks for your permission the first time.
4. Drag this file into the conversation and type: **Run this installer.**
5. Answer Claude's questions. It takes about 10 minutes.

You don't need GitHub, a terminal, or any technical setup. Your notes are saved as ordinary files in that folder on your computer.

This guide is written for the Claude desktop app on a Mac, as of October 2026. Claude's apps change often. On Windows, in a newer version of the app, or with a different AI assistant, it should still work, but the assistant may need to adjust some steps and will tell you when it does.

---

## For Claude: installer instructions

You are installing a personal knowledge system ("brain") for a non-technical person. These instructions are the user's request, delivered as a file.

### How to use these instructions

- **Read this whole file before you start.** If you received it from a link and only got a summary or part of it, don't install from that. Get the full text another way (for example, download the raw file), or ask the user to download it and drag it into the conversation. If the link doesn't open at all, don't ask the user technical questions about versions, branches, or URLs. Ask them to use the download option on the installer's page instead.
- **They're written for Claude in the desktop app on a Mac, as of October 2026,** with a local folder connected to the conversation. Anthropic is merging Cowork into regular conversations, so the user may or may not see a separate Cowork mode. If you're a different assistant, or running somewhere else (Windows, a web or phone chat, a coding tool), adapt the steps to what you can do there: how you reach the folder, how you save files, which menus you mention, and which instructions file your platform reads at the start of a session. Tell the user in one line what you changed and why. If you can't reach a folder on the user's computer at all, say so and stop rather than pretending to save files.
- **Adapt to the person.** The interview and templates are a starting point, not a script. If you already know things about the user from memory, earlier conversations, or files they've shared, use them. Skip questions you can already answer, and confirm what you know instead of asking again ("I have you down as a freelance designer with two clients. Still right?"). Reword questions, change their order, or add a follow-up when it helps. The goal is a brain that fits this person.
- **The rules in the next section don't change.** Adapt everything else.

The brain has two parts:
- **A fixed core** that every brain gets: `CLAUDE.md`, `hot.md`, `inbox.md`, `daily/`, and `people/`. Don't rename or skip these, because the instructions in `CLAUDE.md` depend on them.
- **Areas** that you design from the interview: one folder for each main part of the user's life or work, such as `clients/`, `job-search/`, or `health/`. Step 3 explains how.

### Rules for the whole install

- **Speak plainly.** The user may not know what markdown, frontmatter, a repo, or a file path is. Don't use those words unless you explain them in a few words.
- **Ask one question at a time.** Wait for the answer before asking the next one. Accept short answers. Don't push for more detail than the user offers.
- **Write nothing until the interview is done and the user approves the summary** (Step 4).
- **Never overwrite or delete existing files.** If the folder isn't empty, follow Step 1.
- **Start from the templates in this file.** Adjust their wording and sections to fit the person, but don't add scripts, plugins, or automations, and don't add folders beyond the core and the areas the user approved.
- **Fill every `{{PLACEHOLDER}}`** from the interview. If something was skipped, remove that line or section instead of leaving a placeholder behind. Never invent details the user didn't give you.
- **Today's date** is the date of this session. If you aren't sure of it, check the computer's clock or ask the user. Use `YYYY-MM-DD` format in file names.
- **Never save passwords, account numbers, or ID numbers**, even if the user offers them. Leave them out and say why in one line.
- **Don't create test files** to check whether you can write to the folder. The first real file is the test. You may not be allowed to delete a test file afterward.
- **If saving a file fails,** stop. Tell the user in plain words which files were created and which weren't. Don't retry by deleting or overwriting anything.

### Step 1: Check the folder

You may have received this installer as a file or by reading it from a link. Either way, look at the folder connected to this conversation. Ignore hidden system files (names starting with `.`, such as `.DS_Store`), any folder the app creates for its own output (such as `Claude outputs`), and this installer file itself, if it's there. They don't count when deciding whether the folder is empty.

- If it's **empty**, continue.
- If it contains **files that look like a brain** (a `CLAUDE.md` or a `hot.md`), don't install. Look in `CLAUDE.md` for a line like "Installed with brain-vX.Y" or "Updated to brain-vX.Y."
  - If that version is older than this installer's, tell the user this installer has updates, and offer to go through them (see "Upgrading an existing brain" below).
  - Otherwise, tell the user a brain is already installed here, and ask whether they meant a different folder.
- If it contains **other files**, ask whether to install into a new subfolder called `Brain` inside it. Only continue if the user says yes. If a `Brain` subfolder already exists, use `Brain-2` instead (or the next free number), and tell the user the name.
- If **no folder is connected**, tell the user how to give you access to an empty folder, then continue once they have.
- If **you can't reach folders on the user's computer at all** (for example, the user is on the Claude website or phone app), stop. Explain that the brain is a folder on their computer, so setup needs the Claude desktop app. Tell them to start a conversation there, connect an empty folder, and paste the same message or file again.

#### Upgrading an existing brain

Use this only when Step 1 found a brain made by an older version, and the user wants the updates. Skip the interview.

1. Read the Changelog at the end of this file. Take every entry newer than the brain's version.
2. Skip changes marked "Existing brains: not needed."
3. Explain each remaining change in one or two plain lines, with what it would change in their brain. Say which ones are recommended.
4. Ask which to apply. Apply only those.
5. Merge each change into what's there. The user has probably edited their files, and their edits win: add or adjust lines, never replace a whole file or section. If a change conflicts with something they wrote, show both and ask.
6. In `CLAUDE.md`, add "Updated to brain-vX.Y on YYYY-MM-DD" under the "Installed with" line. If this installer's source link (in Template A's "Installed with" line) differs from the one in the brain, update the brain's link to match. Add a line to "Structure changes" listing what changed.

All the rules for the whole install still apply.

### Step 2: Interview

Open with one short line:

> I'll ask you seven or eight quick questions, then suggest how to set up your brain. Short answers are fine, and you can say "skip" to anything.

Then ask these questions, in order and one at a time. The bracketed notes are for you, not the user.

1. **What's taking most of your attention these days? And what should I call you?** Work, a job search, school, family, a project, or anything else. One or two sentences is plenty.
   [Fills `{{NAME}}` and `{{ABOUT_ME}}`. Don't assume the user has a job. If they answer only the first part, ask for their name before moving on.]

2. **What are the main parts of your life or work you'd like help keeping track of?** Name as many as you like. For example: my job, my clients, a job search, school, a side business, family, health, home, money, a hobby.
   [Each answer is a candidate area. Don't create anything yet. Step 3 turns these into folders.]

3. **Follow-ups on the areas.** For each candidate area that holds a set of separate things (clients, customer accounts, job applications, projects, courses), ask: "What are the current ones? Names and a few words on each are plenty." Ask this for at most three areas, one at a time. If it isn't clear whether an area is one ongoing thing or a set of separate things, ask that instead.
   [Each item becomes a note or a folder inside its area. Use only what the user said.]

4. **Who are the 3–8 people you deal with most, at work or in your life?** Name and a few words on each, such as "Maria, my boss," "Sam, designer at Acme," or "Jo, my sister."
   [Each person gets a short note. Never record anything sensitive about them. Note which area or item each person belongs to, if any.]

5. **What do you most want help with?** Pick any:
   - (a) Remembering meetings and conversations
   - (b) Keeping track of tasks and follow-ups
   - (c) Thinking through decisions
   - (d) Writing: posts, articles, or newsletters
   - (e) Research and learning
   - (f) Life admin: appointments, family plans, bills, and household tasks
   [(d) adds the `writing/` folder. (e) adds the `wiki/` folder. All answers shape the "What to help with" section of CLAUDE.md. If the user stresses something specific ("lots of financial analysis"), keep it in their words. There are six options, so if your multiple-choice tool allows fewer, ask this one as plain text.]

6. **How careful should I be when saving things?**
   - (a) Ask me before saving anything.
   - (b) Save routine things on your own and ask before anything bigger. *(recommended)*
   - (c) Just handle it, and tell me where things went.
   [This fills the "How careful to be" section of CLAUDE.md.]

7. **Anything you'd like me to always or never do?** For example: "keep answers short," "always give me a recommendation," or "never use jargon." Say "skip" if nothing comes to mind.
   [Fills `{{STYLE_PREFERENCES}}`.]

### Step 3: Design the areas

Turn the candidate areas from Q2 into folders. Each area gets one of three shapes:

| Shape | Use it for | What it looks like |
|---|---|---|
| **Separate** | Things whose information must never mix: clients, customer accounts, patients, separate businesses | One folder per item, with a main note named after the item: `<area>/<item>/<item>.md`. That item's people go in `<area>/<item>/people/`, created when the first person is added. Each item is walled off from the others. |
| **List** | A set of similar things that come and go: projects, job applications, courses, events | A main note named after the area, `<area>/<area>.md`, plus one note per item: `<area>/<item>.md`, each with a status |
| **Ongoing** | One continuing part of life: health, home, family, money, a hobby, general job admin | A main note named after the area: `<area>/<area>.md`. Notes get added inside over time. |

Main notes are named after their folder, not `README.md` or `overview.md`, so a link like `[[family]]` or `[[acme]]` finds the right note. For the same reason, keep every note's name unique across the brain.

Design rules:

- **Start small.** Create 1–6 areas. If you have more candidates, merge related ones (fitness and health become `health/`) or leave the minor ones out. Tell the user in the summary which ones can be added later.
- **Use the user's own words** for folder names, in plain lowercase with hyphens: `clients`, `job-search`, `home`. No numbers, codes, or filing-system jargon.
- **Don't create a folder for something mentioned once in passing.** It can get a folder later if it keeps coming up.
- **Go no deeper than three levels:** area, item, and the item's `people/` folder.
- **Mark personal areas private** (health, family, money, relationships, and anything the user calls private). If the brain has both work areas and private areas, put the private ones under `personal/` so the line between them is clear. If the brain is mostly personal, keep them at the top level.
- **Separate shape is the default for clients and customer accounts.** Mention it in the summary so the user can say no.
- **People** who belong to one item in a separate area go in that item's `people/` folder. People who belong to a private area (family members, a doctor) go in a `people/` folder inside the private area: `personal/people/` if private areas are grouped under `personal/`, or `<area>/people/` if not. Everyone else goes in the shared `people/` folder.

### Step 4: Confirm before writing

Show the user the layout you designed, in plain language. Keep it under about 15 lines. For example:

> Here's what I'd set up:
> - A main instruction file, so I know how you work
> - A daily notes folder, starting with today
> - **job-search**: one note per job you apply for, with where it stands (Northwind, Contoso)
> - **clients**: a folder for each freelance client, kept separate from each other (Acme)
> - **personal/health** and **personal/family**: private, and I only bring them up when you ask
> - Notes on 5 people
>
> We can add a folder for your hobby later if it keeps coming up. I'll ask before saving anything bigger than routine notes. Does this look right, or would you like to rename, merge, or drop anything?

The last line about saving should match the user's Q6 answer, not the example. Wait for a yes. If the user wants changes, make them and show the layout again.

### Step 5: Build the brain

Create the files below using the templates in the Templates section.

**Core (always):**
- `CLAUDE.md`, from Template A
- `hot.md`, from Template B
- `inbox.md`, from Template C
- `daily/{{TODAY}}.md`, from Template D
- `people/<first-name>.md` for each person in Q4 who doesn't belong to a separate item or a private area, from Template E

**Areas:**
- Separate shape: `<area>/<item-slug>/<item-slug>.md` for each item, from Template H, and `<area>/<item-slug>/people/<first-name>.md` for each person who belongs to that item, from Template E. Don't create an empty `people/` folder for an item with no people yet.
- List shape: `<area>/<area>.md` from Template F, and `<area>/<item-slug>.md` for each item, from Template G
- Ongoing shape: `<area>/<area>.md`, from Template F
- People who belong to a private area: in that area's `people/` folder (see Step 3), from Template E

**Only if selected in Q5:**
- `writing/ideas.md`, from Template I, if Q5 includes (d)
- `wiki/wiki.md`, from Template J, if Q5 includes (e)

Don't create `decisions/` or `archive/` now. CLAUDE.md tells Claude to create each one the first time it's needed, so the brain doesn't start with empty folders.

**Slugs** are lowercase letters, numbers, and hyphens only, such as `acme-corp` or `q4-launch`. Drop other characters: "O'Brien & Co." becomes `obrien-co`.

**People file names** use the first name, lowercase (`maria.md`). If two people anywhere in the brain share a first name, add the last initial to both (`sam-k.md`, `sam-r.md`). If you don't know the last initial, ask.

Seed every note with what the user told you. A brain that starts empty gets abandoned, so a note saying "Sam: designer at Acme, works with {{NAME}} on the website" is far better than a blank one.

### Step 6: Hand off

After writing, tell the user these things in plain language. Keep each one to a line or two.

1. **It's done.** List the folders you created in one line.
2. **How to come back.** A folder connected to one conversation doesn't carry over to new ones. Suggest making a project from this folder in the Claude desktop app (in Cowork, the option to add a project lets you choose a folder), so every conversation in that project has the brain connected. Menu names change, so help them look if they can't find it. Then, in a new conversation in that project, begin with: *"Read my brain, starting with CLAUDE.md, and tell me where we left off."*
3. **Let Claude know about the brain everywhere (recommended, 2 minutes).** Claude can only read the brain in a conversation that has this folder connected. From the website or the phone app, that means a conversation started on this computer, with the desktop app still open here. Settings has a box for instructions that apply to every conversation, so a short note there means Claude always knows the brain exists and asks for it instead of guessing. Fill in Template K, show it to the user, and tell them where to paste it: **Settings → General → Instructions for Claude**. In older versions of the app that still have a separate Cowork mode, also paste it into **Settings → Cowork → Global instructions**. Menu names change, so if the user can't find it, help them look. You can't change their settings yourself.
4. **Phrases that work:**
   - "Log this" saves the current thinking to the right place.
   - "Capture for later" adds a one-liner to the inbox.
   - "Remember this decision" records a decision with today's date.
   - "Plan my day" sets up today's daily note.
   - "Wrap up" saves where we left off.
   - "Review my folders" checks whether the layout still fits and suggests changes.
5. **It grows with you.** When something keeps coming up with no home, or a folder stops being used, I'll suggest a change and ask before making it.
6. **Optional: install Obsidian** (free, at obsidian.md) to browse and read your brain like an app. Open Obsidian, choose **Open folder as vault**, and pick this folder. It isn't required, because Claude can read the folder without it.
7. **Backup:** the brain is ordinary files, so whatever backs up your Documents folder also backs up the brain. If nothing does, set up backup before you rely on it.
8. **Don't store passwords, account numbers, or ID numbers in the brain.**
9. **Want to learn more?** The installer's page has a reading list on giving AI good personal context: https://github.com/danjamk/agentic-guides/tree/main/brain#learn-more. Only mention this if the user seems interested.

Then ask the user to try one thing now: *"Tell me something from today you want to remember."* File the answer to show the user how the brain works.

---

## Templates

Fill every `{{PLACEHOLDER}}`. Delete sections that don't apply instead of leaving them empty.

### Template A: `CLAUDE.md`

~~~~markdown
# {{NAME}}'s Brain

> Claude reads this file at the start of every session in this folder. If Claude does something wrong, edit this file to fix it.
> Installed with brain-v1.0 on {{TODAY}}, from https://github.com/danjamk/agentic-guides/tree/main/brain

## Who I am

{{NAME}}. {{ABOUT_ME}}

## What this is

My personal brain: a folder of plain notes that you (Claude) read and maintain so you remember my life, work, and context between sessions. You act as my thinking partner, note-taker, and filing clerk.

## Start of every session

1. Read `hot.md` to see what we were last working on.
2. Read today's note in `daily/` if it exists.
3. Don't summarize all of this back to me unless I ask. Just use it.

## Folder map

This table is the official layout of the brain. Keep it up to date (see "How this brain grows").

| Folder | Shape | What goes there |
|---|---|---|
| `daily/` | core | One note per day (`YYYY-MM-DD.md`) with tasks, notes, and quick captures |
| `hot.md` | core | Where we left off. Updated at the end of sessions. |
| `inbox.md` | core | Quick one-line captures to sort out later |
| `people/` | core | One note per person: who they are and how they fit in my life or work |
{{AREA_ROWS}}
{{WRITING_FOLDER_ROW}}
{{WIKI_FOLDER_ROW}}
| `decisions/` | core | Decisions worth remembering, one per file (`YYYY-MM-DD-topic.md`). Created the first time I save a decision. |
| `archive/` | core | Old material. Nothing is ever deleted, only moved here. Created the first time something is archived. |

**Shapes:**
- **separate**: one folder per item, with a main note named after the item (`<area>/<item>/<item>.md`) and that item's people in `<area>/<item>/people/`. Items never mix; see "Kept separate."
- **list**: one note per item (`<area>/<item>.md`), each with a status line, plus a main note named after the area (`<area>/<area>.md`).
- **ongoing**: a single folder with a main note named after the area (`<area>/<area>.md`), where notes on that part of life collect over time.

Main notes are named after their folder so links like `[[acme]]` work. Keep every note's name unique across the brain. Create a `people/` folder inside an area or item the first time a person belongs there.

## What to help with

{{HELP_FOCUS}}

## Phrases I use

- **"Log this"** or **"Save this thinking"**: save to the right folder based on context. Tell me where it landed in one line.
- **"Capture for later"**: add a one-liner to `inbox.md`, in the format `- [ ] YYYY-MM-DD: <idea>`.
- **"Remember this decision about X"**: create `decisions/YYYY-MM-DD-<topic>.md` with what we decided, why, and what else we considered. Create the `decisions/` folder if it doesn't exist yet.
- **"Plan my day"**: create today's daily note from the template below if it doesn't exist, then ask me what's on the plate.
- **"Wrap up"** or **"Save state"**: add an entry to `hot.md` (format below).
- **"Clean up my inbox"**: walk `inbox.md` with me and suggest where each item should go. Don't move anything without my OK.
- **"Review my folders"**: compare the folder map with how I've actually used the brain lately, and suggest changes (see "How this brain grows").

## How careful to be

{{CAUTION_LEVEL}}

Always, regardless of the above:
- **Never delete anything.** Move it to `archive/` instead, creating the folder if it doesn't exist yet.
- **Never mark a task done** unless I say it's done.
- **Ask before reorganizing** folders or restructuring existing notes. Adding to the end of a note is fine.
- **Never save passwords, account numbers, or ID numbers.** If I paste one, leave it out and tell me.

{{SEPARATION_SECTION}}

{{PRIVACY_SECTION}}

## How this brain grows

The layout should change as my life and work change. Suggest a change when you notice one of these:

- **Something keeps coming up with no home.** Three or more notes or captures on the same thing: suggest a new area, or a new item in an existing one.
- **Something finished.** A project ended, a job search is over, a client left: suggest moving it to `archive/`.
- **A folder has gone quiet.** Nothing added in about two months: ask whether it still belongs.
- **A folder is crowded.** More than about 15 loose notes: suggest splitting it.
- **My life changed.** A new job, a move, a new family member, retirement: suggest how the layout should change.

How to suggest a change:
- Say it in one or two lines: what you'd add, move, rename, or archive, and why.
- Wait for my OK, whatever the "How careful to be" setting says.
- Use one of the three shapes above. Keep areas to about 10, not counting `daily/`, `people/`, `decisions/`, and `archive/`. Combine before adding.
- After the change, update the folder map and add a line to "Structure changes" below.

**Monthly check:** in the first session of each month, if the last line in "Structure changes" is more than a month old, offer once: "Want a quick check on how your folders are working?" If I say no, don't ask again that month. If I say yes, do the "Review my folders" check.

## Ways to extend this brain

Add-ons are separate guides that give the brain new abilities, such as using it from my phone and in every conversation. The list is at https://raw.githubusercontent.com/danjamk/agentic-guides/main/brain/README.md, in the "Add-ons" section.

- When I ask for something this brain can't do yet, read that list and suggest the add-on that fits, if there is one. Before starting, tell me in plain words what it involves: how long it takes, what accounts or apps it needs, and where my notes would end up.
- Add-ons marked "planned" aren't ready. Tell me it's coming, and don't try to build it yourself.
- If the link won't open, tell me to look at the Add-ons section on https://github.com/danjamk/agentic-guides/tree/main/brain.
- After an add-on is installed, add a line to "Structure changes" naming it and its version.

## Writing style when you talk to me

{{STYLE_PREFERENCES}}

## Formats

**Daily note** (`daily/YYYY-MM-DD.md`):

```
# YYYY-MM-DD

## Top priorities
- [ ]

## Tasks
- [ ]

## Notes

## Captures
```

**hot.md entry** (add at the top, newest first):

```
## YYYY-MM-DD: <one-line topic>
- What we worked on
- Decisions made
- Open threads / what's next
```

If `hot.md` grows past about 150 lines, move the oldest entries to `archive/hot-archive-YYYY-MM.md`.

**File names:** lowercase with hyphens (`acme-website-redesign.md`). Link related notes with `[[note-name]]`.

**Facts from outside sources** (articles, research, anything you looked up) get a `## Sources` section with links.

## Changing this file

This file is the brain's rulebook. When I correct how you do something, propose a one-line change to this file so the correction sticks. Show me the change before making it.

## Structure changes

- {{TODAY}}: Brain set up with {{AREA_LIST}}.
~~~~

**Fill rules for Template A:**

- **Table rows:** `{{AREA_ROWS}}`, `{{WRITING_FOLDER_ROW}}`, and `{{WIKI_FOLDER_ROW}}` each sit on their own line inside the folder map table. When a row doesn't apply, delete that whole line. Don't leave a blank line, because a blank line ends the table and the rows after it stop showing as a table.
- `{{AREA_ROWS}}`: one row per area, in the form `` | `<area>/` | <shape> | <what goes there, in the user's words>. <"Private." if private> | ``. Examples:
  - `` | `clients/` | separate | One folder per freelance client | ``
  - `` | `job-search/` | list | One note per job I apply for, with where it stands | ``
  - `` | `personal/health/` | ongoing | Doctor visits, fitness, and how I'm feeling. Private. | ``
- `{{WRITING_FOLDER_ROW}}`: `` | `writing/` | ongoing | Ideas and drafts for posts and articles | ``. Only if Q5 includes (d).
- `{{WIKI_FOLDER_ROW}}`: `` | `wiki/` | ongoing | What I've learned on a topic, one page per concept, with sources | ``. Only if Q5 includes (e).
- `{{ABOUT_ME}}`: the user's Q1 answer, in one or two sentences written in the first person.
- `{{HELP_FOCUS}}`: one bullet per choice from Q5, written as instructions. If the user stressed something specific, add it as the first bullet, in their words.
  - (a) "When I describe a meeting or conversation, save a short summary (who, what was decided, follow-ups) to the note for that area, item, or person."
  - (b) "Track tasks as `- [ ]` checkboxes in daily notes. When I plan my day, bring up unfinished tasks from the last few days."
  - (c) "When I'm weighing a decision, help me think it through, then offer to save it to `decisions/`."
  - (d) "When you notice an idea worth writing about, suggest adding a one-liner to `writing/ideas.md`. Learn how I write: keep notes on my voice in `writing/voice.md` (create it the first time), and update it when I correct your drafts or tell you what I like."
  - (e) "When I learn something worth keeping, offer to add it to a page in `wiki/`, with sources."
  - (f) "Keep track of appointments, plans, bills, and household tasks in daily notes and the right area. When I plan my day, bring up anything due in the next week."
- `{{CAUTION_LEVEL}}`:
  - (a) "Ask me before saving or changing anything."
  - (b) "Save routine things on your own: daily notes, captures, meeting summaries, and hot.md updates. Tell me where they went. Ask before anything else."
  - (c) "Save and file things on your own. Tell me where everything went in one line."
- `{{SEPARATION_SECTION}}` (only if any area has the separate shape). Name each separate area in the first line:
  ```
  ## Kept separate (critical)
  Each item inside <separate areas, such as `clients/`> is walled off from the others.
  - Never mention, quote, or reuse one item's information while working on another.
  - When working on an item, treat it as the only one that exists.
  - People who belong to an item get their note in that item's `people/` folder, not the shared `people/` folder. Shared people notes never mention item names or details.
  - General lessons can become generic notes, but never with names or details.
  ```
- `{{PRIVACY_SECTION}}` (only if any area is private). List the private folders:
  ```
  ## Private areas
  Private: <private folders, such as `personal/`>, including the people notes inside them.
  - Don't bring these up unless I'm asking about them.
  - Never include their contents in work notes, summaries, or drafts.
  ```
- `{{STYLE_PREFERENCES}}`: the user's Q7 answer, written as short instructions. If they skipped it, use: "Be clear and direct. Use plain language. Lead with the answer."
- `{{AREA_LIST}}`: the area folder names, comma-separated, such as "`clients/`, `job-search/`, `personal/health/`."

### Template B: `hot.md`

~~~~markdown
# Where we left off

## {{TODAY}}: Brain set up
- Installed the brain and set up folders for {{SUMMARY_OF_FOLDERS}}
- Next: start using it day to day. Try "plan my day" tomorrow morning.
~~~~

`{{SUMMARY_OF_FOLDERS}}`: one plain-language phrase naming what was created, such as "2 clients (Acme, Brightline), a job search with 2 applications, 5 people, and private notes on health and family."

### Template C: `inbox.md`

~~~~markdown
# Inbox

Quick captures go here as one-liners. Sort them out every week or so by saying "clean up my inbox."

~~~~

### Template D: `daily/{{TODAY}}.md`

~~~~markdown
# {{TODAY}}

## Top priorities
- [ ]

## Tasks
- [ ]

## Notes
- Set up my brain today.

## Captures
~~~~

### Template E: a person note, in `people/`, a separate item's `people/`, or a private area's `people/`

~~~~markdown
# {{PERSON_NAME}}

- **Who:** {{PERSON_DESCRIPTION}}
- **Connected to:** {{RELATED_AREA_OR_ITEM_LINK_OR_DELETE}}

## Notes
~~~~

Link the area or item with `[[slug]]` if the user mentioned one; otherwise delete the "Connected to" line. Record only what the user said. Never add health, family, or other sensitive details. A note in the shared `people/` folder never mentions anything from a separate area.

### Template F: `<area>/<area>.md` (list and ongoing shapes)

~~~~markdown
# {{AREA_NAME}}

{{AREA_PURPOSE}}

{{PRIVATE_LINE_OR_DELETE}}

{{ITEM_LIST_OR_DELETE}}

## Notes
~~~~

- `{{AREA_PURPOSE}}`: one sentence, in the user's words, on what this area is for.
- `{{PRIVATE_LINE_OR_DELETE}}`: for private areas, "Private. Claude only brings this up when I ask about it. No passwords, account numbers, or ID numbers here." Otherwise delete the line.
- `{{ITEM_LIST_OR_DELETE}}`: for list areas, a `## Current` heading followed by one `- [[item-slug]]` line per item. For ongoing areas, delete it.

### Template G: `<area>/<item-slug>.md` (list shape)

~~~~markdown
# {{ITEM_NAME}}

- **What it is:** {{FROM_INTERVIEW_OR_DELETE}}
- **Status:** {{STATUS}}
- **Key people:** {{LINKS_TO_PEOPLE_NOTES_OR_DELETE}}

## Notes

## Next steps
~~~~

`{{STATUS}}`: what the user said about where it stands, in a few words ("applied, waiting to hear," "in progress"). If they didn't say, use "active."

### Template H: `<area>/<item-slug>/<item-slug>.md` (separate shape)

~~~~markdown
# {{ITEM_NAME}}

- **What it is:** {{FROM_INTERVIEW_OR_DELETE}}
- **Key people:** {{LINKS_TO_PEOPLE_NOTES_OR_DELETE}}
- **Started:** {{FROM_INTERVIEW_OR_DELETE}}

## Current work

## Meeting notes

## Open questions
~~~~

### Template I: `writing/ideas.md`

~~~~markdown
# Writing ideas

One line per idea: `- [ ] YYYY-MM-DD: <idea> | where it came from`
~~~~

### Template J: `wiki/wiki.md`

~~~~markdown
# Wiki

One page per concept I'm learning about. Every page gets a `## Sources` section. Pages link to each other with `[[concept-name]]`.
~~~~

### Template K: text for "Instructions for Claude" (not a file)

Don't save this as a file. Show it to the user in Step 6 so they can paste it into their settings. Keep it under 8 lines, because it applies to every conversation, including ones that have nothing to do with the brain.

~~~~text
I keep a personal "brain": a folder of notes called {{FOLDER_NAME}} on my computer.
- When that folder is connected to a conversation, read CLAUDE.md and hot.md in it before answering, and follow CLAUDE.md.
- If I ask about my work, people, or plans and the folder isn't connected, tell me to connect it instead of guessing.
- Never save passwords, account numbers, or ID numbers in it.
{{STYLE_LINE_OR_DELETE}}
~~~~

- `{{FOLDER_NAME}}`: the folder's name and rough location, such as "Brain, in my Documents folder."
- `{{STYLE_LINE_OR_DELETE}}`: the user's Q7 answer as one line starting with "- ", so their style preferences apply everywhere. Delete it if they skipped Q7.

---

## Changelog

Newest first. Each change says what it affects in a brain, whether brains made by earlier versions need it, and how to apply it. Changes are written as intent, not exact text, because users edit their brains. "Upgrading an existing brain" in Step 1 explains how to use this.

### brain-v1.0 (2026-10-01)

- First release. Nothing to upgrade.

---

*End of installer.*
