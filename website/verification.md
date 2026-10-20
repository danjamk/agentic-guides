# Website recipe: verification log

Dated results from testing the parts of the website recipe that depend on Cloudflare and GitHub behavior. Cloudflare's dashboard changes often, so each result carries the date it was checked. Re-check anything older than a few months before relying on it.

The template is [website-starter](https://github.com/danjamk/website-starter).

## Deploy to Cloudflare path

Checked 2026-10-20 (#20, Deploy button verification). Test setup:
- An existing Cloudflare account. It already had a `workers.dev` subdomain, so the subdomain-picking screen was not seen.
- A GitHub organization with no apps installed, standing in for a new GitHub account. The personal GitHub account had authorized Cloudflare before, so the "Authorize Cloudflare" screen was not seen.

Both unseen screens are left for the dry run (#30, dry run and release).

| Question | Result |
|---|---|
| Does the button work for a static Astro site with no Worker script? | Yes. `assets` only, no `main`. Build 27 s, under a minute from clicking Deploy to a live site. |
| What does the setup page fill in? | Git account, "Create private Git repository", project name, build command `npm run build`, deploy command `npx wrangler deploy`, preview command `npx wrangler preview`, "Enable Preview builds" (on). |
| Does the button carry the template address through? | Yes when GitHub is already connected: it goes straight to the setup page. On the first run, connecting GitHub mid-flow landed on Cloudflare's general "Create an app" page instead, and the address had to be pasted under "Clone a public repository via Git URL". |
| Can the person's copy be private? | Yes. "Create private Git repository" is a checkbox on the setup page. It was **unchecked by default** on the button path and checked on the "Create an app" path. |
| Does a copy switched to private afterward keep building? | Yes. A repo made public, then switched to private on GitHub, built and deployed its next push. |
| Can the copy go into a GitHub organization? | Yes, through the "Git account" dropdown. |
| What does the copy look like? | One commit, "source repo import", by `cloudflare[bot]`. No shared history with the template. Cloudflare rewrites `name` in `wrangler.jsonc` and `package.json` to the project name. |
| Do branches get previews, or only pull requests? | Every pushed branch, with or without a pull request. Requires a `previews` block in `wrangler.jsonc`; without it every preview build fails. Added to the template in website-starter 0.1.1. `wrangler preview` was an open beta command. |
| Preview address | `<branch>-<project>.<subdomain>.workers.dev`. Later pushes to the branch update the same address. |
| Are preview addresses posted on the pull request? | No comment appeared, and Cloudflare's build settings had no option for one. The pull request shows a "Workers Builds" check that links to the build in the Cloudflare dashboard. Claude has to give the person the preview address itself. |
| Are previews hidden from search engines? | Yes. `noindex`, `Disallow: /`, no sitemap, because `SITE_URL` is unset and the branch is not `main`. |
| Commit shown in the footer | The first build set `WORKERS_CI_COMMIT_SHA` to `main` instead of a hash. Fixed in website-starter 0.1.1 by falling back to git. |

## Claude Code cloud session

Checked 2026-10-20 (#20, Deploy button verification), Claude Code on the web, Pro account.

| Question | Result |
|---|---|
| Where is the network setting? | The environment selector, the first control under the message box on the new-session screen. Hover over the environment under **Cloud** and click its settings icon. In a running session: the caret after the session title, then **Edit cloud environment**. Set **Network access** to **Custom**, add `*.workers.dev` under **Allowed domains**, and check **Also include default list of common package managers**. |
| Is `workers.dev` allowed by default? | No. It is not in the default "Trusted" list, per Claude Code's docs. Fetching with the default setting was not tried. |
| Can Claude read a preview with `curl` after allowing it? | Yes. It returned the current title and the commit in the footer. |
| Can Claude use its web fetch tool instead? | No. The tool returned a page, but an old version: it reported the title from before the latest push. Web fetch runs outside the session's machine and caches pages for 15 minutes. |

## Effect on the recipe

- The installer (#21, accounts and hello world) tells the person to check "Create private Git repository". If it was missed, switch the repository to private on GitHub right after.
- The installer gives the fallback for landing on "Create an app": Continue with GitHub, then Clone a public repository via Git URL, and paste `https://github.com/danjamk/website-starter`.
- Claude works out the preview address from the branch and project name and gives it to the person. No pull request comment carries it.
- Claude checks a preview with `curl` in Bash and confirms the commit in the footer before telling the person it is ready. Its web fetch tool can return a stale page (#17, Claude layer).
- People using Claude Code on the web need `*.workers.dev` allowed in their cloud environment (#21, installer).
- Template updates can't arrive by `git merge`, because the copy shares no history with the template (#17, Claude layer).
