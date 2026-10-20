# Website project state files

**Version:** website-state-v1.0 (2026-10-20)

The format every website guide uses to save a person's progress, and to pick it up again in a later session. The installer, the interviews and the template all read and write these files, so they follow this spec and not their own variants.

This file is for the agent running a website guide, and for whoever writes one.

## Why state lives in the person's repository

The person stops whenever they want and comes back days later, often in a new Claude Code session. Claude Code cloud sessions are thrown away when they end. The person's copy of website-starter on GitHub is the only place that survives, so every answer, decision and plan lives there, under `docs/project/`.

Astro only builds `src/` and `public/`, so nothing in `docs/` is published on the site. It is still visible to anyone who can see the repository, which is why the copy is private by default.

## Files

| File | Written by | Holds |
|---|---|---|
| `docs/project/PLAN.md` | The installer creates it; every guide updates it | The person's plan: stages, time estimates, checkboxes, and one "Next up" line |
| `docs/project/profile.md` | The discovery interview; later interviews update it | A short summary of who the person is and what shapes the site's strategy |
| `docs/project/interviews/<name>.md` | Each interview, one file per interview | Every question with its answer, or marked skipped or pending |

`<name>` is the interview's short name: `discovery`, `brand`, `sitemap`, or `page-<page-slug>` for a page interview (`page-about`). Decisions an interview makes as architecture decision records go in `docs/adr/`, defined by the base ADRs (#18, base ADRs), not here.

Every file starts with a format line, so a later guide can tell which version of this spec wrote it:

~~~~markdown
**Format:** website-state-v1.0
~~~~

## PLAN.md

~~~~markdown
# Website plan

**Format:** website-state-v1.0 · **Last updated:** {{DATE}}

**Next up:** {{NEXT_UP}}

## 1. Get a site online — about 15 minutes
- [ ] Accounts: GitHub and Cloudflare
- [ ] Deploy the starter site
- [ ] See your first change on a preview link

## 2. Tell Claude about you — about 20 minutes
- [ ] Discovery interview

## 3. Brand — about 30 minutes
- [ ] Brand interview: colors, fonts, logo, voice

## 4. Site map — about 20 minutes
- [ ] Site map interview: which pages, and what each one is for

## 5. Pages — about 30 minutes each
{{PAGE_LINES}}

## 6. Go live
- [ ] Connect your own domain
- [ ] Let search engines index the site

## Optional
- [ ] Contact form
- [ ] Analytics
~~~~

Fill rules:
- `{{DATE}}`: today, `YYYY-MM-DD`.
- `{{NEXT_UP}}`: one action the person can start next, with its time estimate, in plain words: "Discovery interview, about 20 minutes. Say *let's do the discovery interview*." Rewrite it every time a guide ends or stops.
- `{{PAGE_LINES}}`: one `- [ ] <Page name>` line per page. Until the site map interview has run, write `- [ ] Added after the site map interview`.

Rules:
- A guide checks its own boxes and no others. A box is checked only when that step is done, not when it starts.
- A guide may add lines inside its own stage, for example one per page. It does not remove or reorder stages.
- An interview that stops partway leaves its box unchecked and puts "(in progress)" after the line.
- Time estimates are for the person's time, not Claude's.

## profile.md

~~~~markdown
# About you and your site

**Format:** website-state-v1.0 · **Last updated:** {{DATE}}

Written from the discovery interview. Claude reads this before every session; edit it any time.

## You
{{YOU}}

## Design and brand
{{DESIGN}}

## Existing website
{{EXISTING_SITE}}

## The business
{{BUSINESS}}

## Decisions so far
{{DECISIONS}}
~~~~

Fill rules:
- Each section is two to five short bullets, written as facts about the person: "Comfortable editing text, not code." "Has a logo as a PNG; no brand colors defined."
- `{{DECISIONS}}`: one bullet per decision, linking its ADR when there is one: "Keep the current domain, move it later ([ADR 0003](../adr/0003-domain.md))."
- A section with no answers yet says `Not asked yet.` A section the person skipped says `Skipped.` Never leave a placeholder.

The interview files hold the full answers. `profile.md` is the summary a guide reads first. When a later interview changes something here, it updates the bullet and the date.

## interviews/<name>.md

~~~~markdown
# {{INTERVIEW_TITLE}}

**Format:** website-state-v1.0 · **Guide:** {{GUIDE_VERSION}}
**Status:** {{STATUS}} · **Started:** {{STARTED}} · **Last updated:** {{UPDATED}}

## {{QUESTION_ID}}
**Q:** {{QUESTION_TEXT}}
**Status:** {{ANSWER_STATUS}}
**A:** {{ANSWER}}
~~~~

One `##` section per question, in the guide's order, written when the interview starts so the whole list is visible from the first session.

Fill rules:
- `{{GUIDE_VERSION}}`: the stamp of the guide running the interview, for example `discovery-v1.0`.
- `{{STATUS}}`: `in progress` or `done`. It is `done` only when no question is `pending`.
- `{{QUESTION_ID}}`: the guide's stable ID for the question, such as `github-account`. A guide never reuses an ID for a different question. That is how a newer guide version matches old answers to its questions.
- `{{ANSWER_STATUS}}`: `pending`, `answered` or `skipped`.
- `{{ANSWER}}`: the person's answer in their own words, trimmed, or Claude's summary of a long answer, marked "(summary)". Empty while `pending`. For `skipped`, the reason if they gave one.

Never write passwords, tokens, API keys or payment details into any state file, even if the person types them in an answer. Write "(given, not saved)" instead.

## Saving

State changes go straight to `main`. They only touch `docs/project/` and `docs/adr/`, never the site's pages, so they skip the branch-and-preview step that site changes go through. The person does not confirm each save. Claude says "Saved." and moves on.

1. **Before the first save in a session**, check the repository's visibility with `gh api repos/{owner}/{repo} --jq .private`. Use the REST form: cloud sessions block `gh repo view`, which uses GraphQL. If `gh` is not available, ask the person whether the repository shows "Private" next to its name on GitHub. If it is public, tell the person their answers will be readable by anyone, offer the way to make it private (GitHub → the repository → Settings → General → Danger Zone → Change visibility), and wait for their choice.
2. **After each answer**, write the interview file and update `Last updated`.
3. **Commit and push at every stop, and at least every five answers.** A stop is when the person says to stop or pause, when the interview ends, or before Claude starts a long task. Commit message: `docs: save <name> interview (<answered> of <total>)`.
4. **Before pushing**, run `git pull --ff-only`. If that fails, run `git pull` and resolve any conflict in favor of the newer `Last updated`.
5. **If a commit would touch anything outside `docs/`**, it is a site change. It goes on a branch with a preview, never straight to `main`.

A Claude Code cloud session usually starts on its own branch. For state saves, Claude switches to `main` first and keeps the interview there. Site changes that come out of an interview, such as a page built from a page interview, start on a new branch after the interview's answers are pushed.

Each push to `main` rebuilds the live site. The content is unchanged, so the only visible difference is the build time in the footer. See [Rebuilds on docs-only changes](#rebuilds-on-docs-only-changes).

## Resuming

At the start of any website guide:

1. Switch to `main` and run `git pull`.
2. Read `PLAN.md` and `profile.md`. If either is missing, the installer has not finished: run its resume step instead.
3. Look for interview files with `**Status:** in progress`. If the person asked for something else, mention the unfinished interview in one line and do what they asked.
4. Look for state saved on other branches by mistake: `git log main..origin/<branch> --oneline -- docs/project` for each remote branch. If any commits turn up, tell the person and offer to bring those files into `main`.
5. Before resuming an interview, say where it stands in one line: "You've answered 7 of 12 discovery questions; last time was October 18." Continue at the first `pending` question.

Answers given after the last push in a session that has since ended are gone. The interview file shows the last saved question. Ask from there and do not guess the lost answers.

When the interview file's `Guide:` is older than the running guide:
- Keep every answer whose question ID still exists.
- Add new questions as `pending` in the guide's order.
- Move answers whose question ID no longer exists to a `## Retired questions` section at the end. Don't delete them.
- Update `Guide:` to the running version.

When a file's `Format:` is older than this spec, apply the changelog entries below in order, then update the format line.

## Rebuilds on docs-only changes

**Decided 2026-10-20: accept them.** A push that only changes `docs/` rebuilds and redeploys the live site.

- Why: the only alternative found is Cloudflare's build watch paths, which are set in the dashboard, not in the repository (Settings → Build → Build watch paths). That would add a manual step to the installer for a person who is not technical. A rebuild takes about 45 seconds and serves the same pages.
- Revisit if: build minutes on the free plan become a limit, or interview saves start to crowd out real deploys in Cloudflare's deployment list.
- How to change it: exclude `docs/*` under Build watch paths for the Worker. Pushes with no file changes, 20 or more commits, or 3,000 or more files always build regardless.

## Template contents

website-starter ships:
- `docs/project/PLAN.md` and `docs/project/profile.md`, with the format line and `Not started.` The installer replaces both.
- `docs/project/interviews/` holding a `README.md` that points to this spec.
- A "Project state" section in `CLAUDE.md` that points to these files and to this spec on `main`.

## Changelog

### website-state-v1.0 (2026-10-20)
- First version.
