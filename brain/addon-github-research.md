# GitHub add-on: research notes

Working notes for `addon-github.md`. Delete this file before merging the branch to `main`.

Research date: 2026-10-01. "Verified" means the source was fetched and says this. "Inferred" means it wasn't.

## Summary

The add-on has three parts:

1. **Local sync.** The brain folder becomes a git repository and syncs with a private GitHub repository through the Obsidian Git plugin.
2. **Remote access.** GitHub's own MCP server is added in Claude as a custom connector, so Claude can read and write the repository from web, phone, desktop, and Cowork.
3. **Rules in CLAUDE.md** for two writers: where remote Claude may write, how to spot a stuck sync, and what never goes in the repository.

Cowork can't run git on the Mac (see "Who runs the setup"), so the setup should run in the desktop app's Code tab.

## Remote access: Claude connector

| Option | Reads | Writes | Every surface | Notes |
|---|---|---|---|---|
| Anthropic's built-in GitHub Integration | Yes | No | No | Read-only, one branch, manual "Sync now." "Add from GitHub isn't supported" in the merged chat/Cowork experience. Verified: [connector doc](https://claude.com/docs/connectors/github.md), [merged experience](https://support.claude.com/en/articles/16761823-claude-cowork-and-chat-are-one-claude). |
| GitHub's MCP server as a custom connector | Yes | Yes | Yes | Recommended. URL `https://api.githubcopilot.com/mcp/x/repos` (repos toolset only). No paid GitHub plan or Copilot needed. Verified: [remote server doc](https://github.com/github/github-mcp-server/blob/main/docs/remote-server.md), [GitHub docs](https://docs.github.com/en/copilot/how-tos/provide-context/use-mcp-in-your-ide/set-up-the-github-mcp-server). |
| Zapier / Composio hosted connectors | Yes | Yes | Yes | A third party holds the GitHub token. Not recommended. Unverified. |

**Adding the connector.** Customize > Connectors > "+ Add" > "Add custom connector." Then enter the name and URL, pick an authentication option, optionally add request headers, and click Add. Auth settings can't be edited later; the connector has to be removed and added again. Verified: [custom connectors](https://support.claude.com/en/articles/11175166-get-started-with-custom-connectors-using-remote-mcp), [add unlisted](https://claude.com/docs/connectors/custom/add-unlisted.md).

**Authentication.** GitHub's OAuth server doesn't support automatic client registration, so Claude's default sign-in can't register with it (verified by probing the endpoint). There are two working paths:

- **(a) Fine-grained personal access token in a request header.** Choose "No sign in" and add the header `authorization: Bearer github_pat_…`. Limit the token to the one brain repository with Contents: Read and write. Request headers are in beta. Anthropic staff said on 2026-08-31 they're available to Pro, Max, and Team ([issue #112](https://github.com/anthropics/claude-ai-mcp/issues/112)), but at least one user didn't have them on 2026-09-19. Recommended when available.
- **(b) The person's own GitHub OAuth App.** Register one under GitHub Settings > Developer settings > OAuth Apps, with callback `https://claude.ai/api/mcp/auth_callback`. In Claude, choose "Use your own OAuth client." The OAuth `repo` scope covers every repository the account can reach, so this can't be limited to one. The flow is inferred, not tested.

**Plans.** Custom connectors are on all plans; Free gets one. On Team and Enterprise, **only owners can add custom connectors**, and a header token would be shared with every member. So the add-on is for Pro and Max accounts. Verified: [connectors](https://support.claude.com/en/articles/11176164-use-connectors-to-extend-claude-s-capabilities).

**Safety settings.**
- Use the `/x/repos` toolset.
- In Claude's tool permissions for the connector, block `delete_repository`, `create_repository`, and `fork_repository`.
- A token limited to one repository can't delete it anyway (inferred).

**Known problems.**
- Write tools commit straight to whatever branch is named.
- `create_or_update_file` needs the current file's SHA and fails on a stale one.
- Parallel writes conflict.
- Files over 1 MB can't be read through the contents API.
- Limits: 80 content-creating requests per minute and 5,000 requests per hour.
- An expiring token fails without warning.
- Users have reported connector sign-in problems on mobile and desktop.

Sources: [contents API](https://docs.github.com/en/rest/repos/contents), [rate limits](https://docs.github.com/en/rest/using-the-rest-api/rate-limits-for-the-rest-api).

## Local sync on the Mac

**Obsidian Git plugin.** Recommended.
- It's active, with v2.41.0 released 2026-10-01.
- It needs the system `git` installed, plus a credential helper for HTTPS.
- Its settings live in the app. They can probably be written to `.obsidian/plugins/obsidian-git/data.json` (inferred).
- Sources: [plugin docs](https://publish.obsidian.md/git-doc/Installation), [authentication](https://publish.obsidian.md/git-doc/Authentication), [features](https://publish.obsidian.md/git-doc/Features).

**Getting git and signing in.**
- **git:** install Xcode Command Line Tools (`xcode-select --install`, or the dialog macOS shows the first time `git` is run).
- **Sign-in:** the Git Credential Manager `.pkg` (double-click install). The first push opens a browser sign-in, and no token is needed for local git.
- Check the result with `git config --global credential.helper`.
- Sources: [GitHub credential caching](https://docs.github.com/en/get-started/git-basics/caching-your-github-credentials-in-git), [git for Mac](https://git-scm.com/install/mac).

**Settings to use.**
- All automatic options are off by default.
- Turn on: pull on startup, auto pull about every 5 minutes, and auto commit-and-sync about 5 minutes after edits stop.
- Pull method: **Merge**, not Rebase. A failed merge leaves plain conflict markers that Claude can fix.
- Merge strategy on conflicts: **None**. "Ours" and "Theirs" silently drop the other side.
- Add `.obsidian/workspace*.json` to `.gitignore`.

**Limits.**
- Obsidian Git syncs **only while Obsidian is open**. Add Obsidian to the Mac's Login Items.
- A merge conflict **stops automatic sync** until it's resolved. The plugin shows a notice and a help window.

**Rejected alternatives.**
- **GitHub Desktop:** no automatic sync, and its sign-in doesn't carry over to command-line git.
- **launchd script, the reference brain's setup:** runs without any app open, but macOS privacy controls can block it for `~/Documents` and `~/Desktop`, it fails silently, and it's hard for a non-technical person to maintain. The reference brain's script also never pulls, so remote writes would make its pushes fail.

## Who runs the setup

Cowork can't be relied on to run git on the Mac:
- Cloud sessions run in Anthropic's sandbox and reach local files only through the desktop app. File access is documented; a shell on the Mac isn't.
- Local Cowork sessions run shell commands in a Linux VM. An open bug ([#55206](https://github.com/anthropics/claude-code/issues/55206)) reports that `git commit` fails on mounted folders. That was reproduced on Windows.
- Sources: [Cowork on web, desktop, and mobile](https://support.claude.com/en/articles/15520349-use-claude-cowork-on-web-desktop-and-mobile), [architecture overview](https://support.claude.com/en/articles/14479288-claude-cowork-architecture-overview).

So the add-on should run in the **desktop app's Code tab** (Claude Code), which has a shell on the Mac and asks before running each command. The Code tab is newer to non-technical users, but it's a window in the same app, not the Terminal.

Related: [issue #98754](https://github.com/anthropics/claude-code/issues/98754) (filed 2026-10-01). The desktop app's bundled git ignores the macOS keychain helper. The workaround is `git config --global credential.helper osxkeychain`.

## Two writers

All inferred practice:

- **Remote Claude creates new files and doesn't edit existing ones.** It saves to something like `from-phone/YYYY-MM-DD-<topic>.md`. New files never conflict. Local Claude files them into the right place at the start of a session. This is the main defense against conflicts.
- **Stuck sync, locally:** local Claude searches notes for `<<<<<<<` and tells the user how to finish the merge in Obsidian.
- **Stuck sync, remotely:** remote Claude checks the latest commit time with `list_commits`. If it's older than about a day, it says sync looks stuck.
- **CLAUDE.md is committed to the repository**, so remote Claude follows the same rules. The reference brain ignores it in git, so its remote Claude can't see the rules.

## Privacy

- **Who can see a private repository:** the owner and anyone they invite. GitHub staff only for security, abuse scanning, support with consent, operations, or legal reasons. Verified: [terms, section E](https://docs.github.com/en/site-policy/github-terms/github-terms-of-service).
- **AI training:** GitHub says it doesn't train AI on private repository content at rest. From 2026-04-24, Copilot interaction data on Free, Pro, and Pro+ is used for training unless the user opts out. Verified: [GitHub changelog](https://github.blog/changelog/2026-03-25-updates-to-our-privacy-statement-and-terms-of-service-how-we-use-your-data/). The opt-out path is unverified.
- **Git history:** git keeps every version. Deleting a note doesn't remove it from history.
- **Separate areas, such as clients:** client agreements may not allow storing their information with a third party. The add-on should ask, and offer to leave separate areas out of the repository.

## Open questions

1. Does the Git Credential Manager `.pkg` set itself up as git's credential helper automatically?
2. Can Obsidian Git settings be written to `data.json` before Obsidian first opens the vault?
3. Does a brain in an iCloud-synced `Documents` folder conflict with git? Common advice says to keep `.git` out of iCloud. The installer currently suggests `Documents/Brain`.
4. How does the OAuth App path (b) actually behave? Not tested.
5. Do request headers show up on Dan's Pro or Max account today?
