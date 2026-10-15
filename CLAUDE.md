# agentic-guides

Agentic guides: markdown files an AI agent follows to set something up for a person, starting with the brain installer.

## Stack

Markdown only. No code, no build, no CI. The guides are instructions for an agent (Claude first), so they are the product. Treat a wording change in a guide the way you'd treat a code change.

## Layout

| Path | What it is |
|---|---|
| `AUTHORING.md` | Conventions for writing guides. Read it before editing any guide. |
| `brain/brain-installer.md` | The brain installer. The agent reads this file. |
| `brain/README.md` | For the end user, who may not be technical. No technical words except in the Add-ons table. |
| `brain/addon-*.md` | Add-on guides that extend a brain |

## Conventions

- **Public repo.** Before every commit, check changed files for client names, private brain content, and local paths (anything under `/Users/` or `~/`).
- **Links in READMEs and prompts point at `main`.** People paste a link to the raw file on `main`, so anything merged to `main` reaches them right away.
- **Unverified claims about Claude's apps are marked as unverified**, in the guide or in the PR. Claude's apps change often; date any statement about menus or features.
- Follow `AUTHORING.md` for guide structure, delivery modes, version stamps, changelogs, and add-ons.

## Branch topology

`main` is the latest released version of every guide. Work happens on branches and arrives by PR.

**Protected branches:** `main`

## Versioning

**Each guide is versioned on its own; the repo has no version.** This is a deliberate exception to repo-wide semver.

- A guide's version is in its header: `**Version:** <guide>-vX.Y (YYYY-MM-DD)`. The guide also writes its version into what it produces.
- Each guide ends with a Changelog section written for an agent upgrading something an older version made. The version bump and the changelog entry land in the PR that changes the guide.
- Minor bump for wording and template fixes. Major bump when the output's structure changes.
- Tags named `<guide>-vX.Y` mark releases for history and for anyone who wants a fixed version. Links don't depend on them.
- The `/release` skill doesn't apply.
