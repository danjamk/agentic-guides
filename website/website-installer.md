# Website Installer

**Version:** website-v1.0 (2026-10-20)

---

## For the person reading this

This guide sets up a website you own and change by talking to Claude. It lives on Cloudflare, which hosts it for free, and its files live in a free, private GitHub account. Every change shows up first on a preview link that only you know about. It goes on your real site only when you say yes.

You need a computer, a Claude Pro or Max plan, and about 30 minutes. Claude helps you make any accounts you don't have yet.

It happens in two parts:

1. **In any Claude conversation:** Claude checks your accounts, then you click one button that puts a starter site online. About 15–20 minutes.
2. **In Claude Code on the web (claude.ai/code):** Claude puts your business name on the site, shows you a preview, and makes it live when you say yes. About 10 minutes.

At the end you have a live site with your name on it, and a plan you can work through at your own pace, about 30 minutes at a time.

To start, open Claude in your web browser at claude.ai, start a new conversation, and paste:

```
Please read the website installer at
https://raw.githubusercontent.com/danjamk/agentic-guides/main/website/website-installer.md
and follow its instructions to set up my website.
```

This guide is written for Claude on claude.ai and Claude Code on the web, as of October 2026. Claude's apps and Cloudflare's screens change often. If something on screen doesn't match, Claude will help you find it.

---

## For Claude: installer instructions

You are setting up a website for a person who may not be technical. These instructions are the person's request, delivered as a file.

### How to use these instructions

- **Read this whole file before you start.** If you got only a summary or part of it from the link, get the full text another way, or ask the person to download the file from https://github.com/danjamk/agentic-guides/blob/main/website/website-installer.md and drag it into the conversation.
- **Work out which part you're in.**
  - **Part 1** runs in an ordinary Claude conversation, with no access to the site's files. It gets the accounts ready and the starter site online.
  - **Part 2** runs in Claude Code, inside the person's copy of website-starter. You're there if the folder you're working in has `wrangler.jsonc` and `src/site.config.ts`, and its `CLAUDE.md` mentions website-starter.
  - If the person pasted the Part 2 message but you're not in Claude Code with their site's files, tell them to start the session at claude.ai/code and pick their site there (Part 1, Step 4 describes how).
- **They're written for Claude on claude.ai and Claude Code on the web, as of October 2026.** If you're a different assistant or running somewhere else, adapt the steps to what you can do there, and tell the person in one line what you changed. Never claim to have done something you couldn't do.
- **Adapt to the person.** If you already know things about them, use them, and confirm instead of asking again. Reword steps to fit how they talk. The rules in the next section don't change.
- **Do only what this guide covers.** The interviews, brand, pages, contact forms, domains and analytics come later, in their own guides. If the person asks for one of them now, note it for the plan and say it comes after this setup.

### Rules for the whole install

- **Speak plainly.** Avoid these words, or explain them in a few words the first time:

  | Instead of | Say |
  |---|---|
  | repository | "your site's files on GitHub" (GitHub calls it a repository; say so once) |
  | branch, commit, push | "a draft", "save" |
  | deploy, merge to main | "put online", "publish to your live site" |
  | Worker | "your site on Cloudflare" |
  | build | "Cloudflare prepares the site" |

- **Ask one question at a time.** Wait for the answer. Accept short answers.
- **Nothing goes on the live site without a yes.** Every change goes to a preview link first. Ask "Publish this to your live site?" and wait for a clear yes.
- **Change nothing until the person approves a summary** (Part 2, Step 3).
- **Never overwrite or delete existing files.** Edit only the files this guide names.
- **Never ask for, repeat, or save a password, token or code.** Sign-ins happen on GitHub's and Cloudflare's own pages. If the person pastes one anyway, don't repeat or use it, and tell them to change it, because it's now in the conversation history.
- **Today's date** is the date of this session. Use `YYYY-MM-DD`.
- **If something fails, stop.** Say in plain words what worked and what didn't. Don't retry by deleting anything.
- **Don't add extras:** no scripts, add-ons, tracking, or files beyond what this guide lists.

---

### Part 1: Accounts and your site online

Open with one line:

> I'll check what you already have, help with anything missing, and then we'll put a starter site online. Keep this tab open; you'll use GitHub and Cloudflare in other tabs.

#### Step 1: Check what's needed

Ask these one at a time. For each, help with what's missing, confirm it worked, then move on. If the person comes back after stopping, start at the first thing that isn't done.

1. **Claude plan.** "Which Claude plan are you on: Free, Pro, Max, or a work plan such as Team or Enterprise?"
   - Pro or Max: continue.
   - Free: Part 2 uses Claude Code on the web, which needs Pro or higher. Suggest upgrading before going further, and stop here if they'd rather not.
   - Team or Enterprise: it works only if their organization gives them Claude Code. Ask them to open claude.ai/code. If it says Claude Code isn't available, they need to ask their administrator, or use a personal Pro plan.

2. **GitHub account.** "Do you have a GitHub account?"
   - If yes, ask for the username.
   - If no, walk them through https://github.com/signup: email, password, username. The username appears in web addresses, so a plain one is best. GitHub emails a code to confirm. Choose the free plan if asked.
   - If GitHub shows "Access is temporarily restricted," it suspects a bot. Suggest a normal browser window instead of a private one, turning off any VPN, using home Wi-Fi instead of a phone hotspot, or waiting an hour.
   - If GitHub asks them to turn on two-step sign-in, help them. Recovery codes go in a password manager or on paper, never in a conversation.

3. **Cloudflare account.** "Do you have a Cloudflare account?"
   - If no, walk them through https://dash.cloudflare.com/sign-up: email and password, then confirm the email. Choose the free plan if asked. They don't need to add a domain or website; skip any step that asks for one.
   - Sign them in to GitHub and Cloudflare **in the same browser window**. The next step uses both.
   - If they have more than one Cloudflare account (a work one, for example), the site goes into whichever one is signed in. Have them check the account name at the top left of the Cloudflare dashboard.

#### Step 2: Put the starter site online

1. Ask them to open this link, in the browser where they're signed in to both:
   https://deploy.workers.cloudflare.com/?url=https://github.com/danjamk/website-starter
2. **If Cloudflare asks to connect GitHub,** they approve it and pick their GitHub account. If GitHub asks which repositories Cloudflare may use, "All repositories" is simplest on a new account with nothing else in it. On an account with other projects, they can choose "Only select repositories", but the new site may then need to be added there later. *(Not verified, 2026-10-20.)*
3. **If they land on a page called "Create an app"** instead of a setup page (this happens the first time GitHub is connected): choose **Continue with GitHub**, then **Clone a public repository via Git URL**, paste `https://github.com/danjamk/website-starter`, and click **Next**.
4. **On the setup page:**
   - **Git account:** their GitHub username.
   - **Create private Git repository:** check it. It's unchecked by default. A private site project keeps their plan and answers to Claude's questions out of public view. The website itself is public either way.
   - **Project name:** a short name for the site, such as their business name in lowercase with dashes (`rivera-bakery`). It appears in the site's address. Keep it under 30 characters.
   - Leave every other field as it is.
   - Click **Deploy**.
5. It takes about a minute. Ask them to paste the address Cloudflare shows, ending in `.workers.dev`.
   [Saves `{{LIVE_URL}}`. It has the form `https://{{PROJECT}}.{{SUBDOMAIN}}.workers.dev`; take `{{PROJECT}}` and `{{SUBDOMAIN}}` from it. If they can't find it: Cloudflare dashboard → **Workers & Pages** → the project → the address under **Domains**.]
6. Ask them to open the address. They should see a page that says "Your Business Name". Tell them in one line that this is their site, live on the internet, and the next part puts their name on it.
7. **If they missed the private box:** GitHub → their site's project → **Settings** → **General** → **Danger Zone** → **Change visibility** → **Private**. The site keeps working.
8. **If the deploy fails,** ask them to copy the error text or the build log from the Cloudflare page and paste it. Explain it plainly. Don't guess a fix without seeing it.

#### Step 3: Get Claude Code ready

Part 2 runs in Claude Code on the web. It needs three one-time settings.

1. **Connect GitHub.** Open https://claude.ai/code and sign in. It asks to connect GitHub; they follow the prompt and approve on GitHub's page.
2. **Let Claude Code into the private site.** Open https://github.com/apps/claude/installations/new, pick their account, choose **Only select repositories**, select the site's project (the project name from Step 2), and install. Without this, Claude Code can't see a private project. If claude.ai/code offered this during step 1 and they did it there, skip it.
3. **Let Claude Code open the preview links.** Claude Code's network access is limited by default and doesn't include Cloudflare's preview addresses. On the claude.ai/code start screen:
   - Click the first control below the message box (the environment selector).
   - Under **Cloud**, hover over the environment (usually "Default") and click the settings icon that appears on its right.
   - Set **Network access** to **Custom**.
   - In **Allowed domains**, enter `*.workers.dev`.
   - Check **Also include default list of common package managers**.
   - Save.

   *(Checked 2026-10-20. Menu names change; help them look if it doesn't match.)*

#### Step 4: Hand over to Part 2

Fill in this message and give it to the person in a copy box:

~~~~
Please read the website installer at
https://raw.githubusercontent.com/danjamk/agentic-guides/main/website/website-installer.md
and follow Part 2 to set up my website.
My live site is {{LIVE_URL}}
~~~~

Tell them:
1. Go to https://claude.ai/code.
2. Below the message box, pick the site's project (the repository selector) and the environment you just changed.
3. Paste the message and send it.

Part 1 ends here. Nothing from this conversation carries over, which is why the message includes the live address.

---

### Part 2: Your name on your site

You're in Claude Code, in the person's copy of website-starter. The project state format is in https://raw.githubusercontent.com/danjamk/agentic-guides/main/website/STATE.md. Read it before writing anything in `docs/project/`.

#### Step 1: Preflight

1. **Check this is a website-starter copy:** `wrangler.jsonc`, `src/site.config.ts` and `docs/project/PLAN.md` exist. If not, tell the person this doesn't look like their site's project and ask them to pick the right one in the repository selector.
2. **Get up to date:** `git checkout main`, then `git pull`.
3. **Check whether it's already set up.** Read `docs/project/PLAN.md` and `CLAUDE.md`.
   - `PLAN.md` says "Not started": continue.
   - `CLAUDE.md` has an "Installed with website-vX.Y" line older than this guide: offer the updates (see "Upgrading" below). Skip the rest of Part 2.
   - Same version: tell the person the site is already set up, read them the "Next up" line from `PLAN.md`, and stop.
   - `PLAN.md` has a plan but `CLAUDE.md` has no "Installed with" line: the person stopped before publishing. Check for a `hello-world` draft (`git branch -r`), show them its preview link, and continue at Step 4, item 8.
4. **Check it's private:** `gh api repos/{owner}/{repo} --jq .private`. If `false`, explain that their plan and answers will be visible to anyone, give the steps from Part 1, Step 2, item 7, and wait for their choice.
5. **Check you can reach the site:** `curl -sS -o /dev/null -w "%{http_code}" {{LIVE_URL}}`.
   - `200`: continue.
   - An error or `403` from the network: the network setting from Part 1, Step 3, item 3 isn't in place. Walk them through it, then try again. It takes effect within a minute.
   - No live address in the message: ask for it.
6. **Work out the names.** `{{PROJECT}}` is `name` in `wrangler.jsonc`. It should match the first part of the live address; if it doesn't, trust the address. `{{SUBDOMAIN}}` is the part between the project name and `.workers.dev`. A preview link is `https://<draft-name>-{{PROJECT}}.{{SUBDOMAIN}}.workers.dev`.

#### Step 2: Two questions

Open with one line:

> Two quick questions, then I'll show you your site with your name on it.

1. **What's your business called?** Use the name the way it should appear on the site.
   [Fills `name` in `src/site.config.ts` and `{{BUSINESS}}` in Template A.]
2. **In one sentence, what do you do and who is it for?** For example: "Custom cakes for weddings and birthdays in Portland."
   [Fills `tagline` in `src/site.config.ts` and `{{ONE_LINER}}` in Template A. Also write `description` in `src/site.config.ts` from it: one plain sentence under 155 characters that includes the business name. Fix spelling, but keep their words.]

Don't ask anything else here. The discovery interview comes next and covers the rest.

#### Step 3: Confirm

Say, in about three lines:

> I'll put **{{BUSINESS}}** and "{{ONE_LINER}}" on your home page and make a preview link for you to check. Nothing changes on your live site until you say so. Go ahead?

Wait for a yes. If they change anything, show the summary again.

#### Step 4: Make the preview

1. Create a draft named `hello-world`: `git checkout -b hello-world`. If that name exists, use `hello-world-2`. Draft names use only lowercase letters, numbers and dashes, never `/`, so the preview link is predictable.
2. Edit `src/site.config.ts`: `name`, `tagline`, `description`. Change nothing else.
3. Add the "Who you're working for" section to `CLAUDE.md` from Template A. It goes on this draft, not straight to `main`, because STATE.md lets only `docs/` changes skip the preview.
4. Check it builds: `npm ci`, then `npm run build`. If either fails, stop and explain.
5. Save and send it: commit with the message `Put business name on the site`, then `git push -u origin hello-world`.
6. Wait for the preview. The link (`{{PREVIEW_URL}}`) is `https://hello-world-{{PROJECT}}.{{SUBDOMAIN}}.workers.dev`, with the draft's actual name if you used another. Every 15 seconds, for up to 4 minutes, fetch it with `curl -sS` in the shell and look for the commit's short hash (`git rev-parse --short HEAD`) in the page footer. Use `curl`, not a web fetch tool, which can show an older copy of the page. Tell the person it takes about a minute.
7. **If the preview doesn't appear in 4 minutes,** check that `wrangler.jsonc` has a `"previews": {}` line. Copies made before 2026-10-20 don't, and previews fail without it. If it's missing, add it on this draft, save and send again, and wait again. Otherwise ask the person to open the Cloudflare dashboard → **Workers & Pages** → the project → **Deployments**, and paste the error from the newest build.
8. Give them the link:

   > Here's your preview: {{PREVIEW_URL}}
   > Take a look, on your phone too if you like. Want any changes, or shall I publish it to your live site?

9. **If they want changes,** make them on the same draft, save and send, and wait for the new hash. The link stays the same.

#### Step 5: Publish

Only after a clear yes:

1. `git checkout main`, `git pull --ff-only`, `git merge --ff-only hello-world`, `git push origin main`.
2. Wait for the live site to show the same commit hash, the same way as the preview (about a minute).
3. Tell them: "It's live: {{LIVE_URL}}".

If they say no or "later", leave the draft as it is. Record it in the plan's "Next up" line, and continue to Step 6.

Claude Code can't delete the draft afterward, and doesn't need to. It stays on GitHub, out of the way.

#### Step 6: Save the plan

Following STATE.md's save rules, straight to `main`:

1. Write `docs/project/PLAN.md` from STATE.md's PLAN.md template. Check all three boxes in stage 1. `{{NEXT_UP}}`: "Discovery interview, about 20 minutes. Say *let's do the discovery interview*." If they didn't publish, make it "Publish your name to your live site. Say *publish the hello-world preview*."
2. Commit with the message `docs: save website plan` and push to `main`.

#### Step 7: Hand off

Tell the person, a line or two each:

1. **It's done.** Their site is live at {{LIVE_URL}} with their name on it, and their plan is saved with their site's files.
2. **How to come back.** Open https://claude.ai/code, pick the site's project and the same environment, and say *"let's keep going."* Claude reads the plan and suggests what's next. They can stop any time; the next session picks up where they left off.
3. **What's next.** Read them the "Next up" line. Stages take about 30 minutes each and can be done whenever suits them.
4. **Try one thing now.** "Tell me one thing you'd change on your home page." Make the change the same way as Step 4: draft, preview link, then publish on yes. Use a new draft name, such as `home-page-1`.

#### Upgrading

Use this only when Step 1 found `CLAUDE.md` stamped with an older website version and the person wants the updates.

1. Read the Changelog at the end of this file. Take every entry newer than their version.
2. Skip entries marked "Existing sites: not needed."
3. Explain each remaining change in one or two plain lines, and say which are recommended.
4. Apply only the ones they choose. Their edits win: add or adjust lines, never replace a file or section. If a change touches the site's pages, it goes through a preview like any other change.
5. Add "Updated to website-vX.Y on YYYY-MM-DD" under the "Installed with" line in `CLAUDE.md`.

---

## Templates

### Template A: "Who you're working for" section of `CLAUDE.md`

~~~~markdown
## Who you're working for

| | |
|---|---|
| Business | {{BUSINESS}} |
| What they do | {{ONE_LINER}} |
| Live site | {{LIVE_URL}} |
| Preview links | `https://<draft-name>-{{PROJECT}}.{{SUBDOMAIN}}.workers.dev` |
| Site's files on GitHub | https://github.com/{{OWNER}}/{{REPO}} |

Installed with website-v1.0 on {{DATE}}. The website guides and add-ons are listed at https://github.com/danjamk/agentic-guides/tree/main/website
~~~~

Fill rules:
- `{{OWNER}}` and `{{REPO}}`: from `git remote get-url origin`.
- `{{DATE}}`: today.
- Insert the section right after the first paragraph of `CLAUDE.md`, before "Project state". Change nothing else in the file.

---

## Changelog

### website-v1.0 (2026-10-20)
- First version.
