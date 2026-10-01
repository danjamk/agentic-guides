# Agentic Guides

Files written for an AI agent to follow. You hand one to Claude; it does the work and asks you what it needs.

Each guide names the platform it was written for. Other agents and platforms can usually follow a guide, adapting the steps where they differ. Guides also tell the agent to adapt to the person, using what it already knows about them.

## How to use a guide

1. Download the guide's `.md` file from its folder.
2. Give it to Claude (drag it into the chat) and say "Run this."
3. Answer Claude's questions.

Each guide's folder has a README with the exact steps for that guide.

## Guides

| Guide | What it sets up | Who it's for | Runs in | Folder |
|---|---|---|---|---|
| Brain installer | A personal "brain": a folder of plain notes Claude reads each session to remember your projects, people, and where you left off | Non-technical people, for work, personal life, or both | Claude desktop app (Mac), with a folder connected | [`brain/`](brain/) |

## Before you run a guide

- **Read it first.** A guide is instructions your agent will follow on your computer. Skim it before you hand it over.
- **Use a tagged version, not `main`.** `main` can change at any time. A tag is a fixed snapshot. Pick one from the [tags page](https://github.com/danjamk/agentic-guides/tags).

## Versioning

- Each guide carries a version stamp in its header, such as `brain-v1.0 (2026-10-01)`.
- A guide also writes its version into whatever it produces, so you can tell later which version made it.
- Releases are git tags named `<guide>-vX.Y`. The first is `brain-v1.0`.
- Each guide ends with a changelog written for the agent. If you run a newer version of a guide on something an older version made, the agent reads the changes since then, explains them, and applies only the ones you approve.

## Credits

The brain installer started from ideas in [claudesidian](https://github.com/heyitsnoah/claudesidian), an MIT-licensed starter kit for using Claude Code with Obsidian. The installer is a separate, simpler setup for non-technical people using Cowork. It doesn't copy claudesidian's files or folder layout.

For background on giving AI assistants good personal context, see the reading list in [`brain/README.md`](brain/README.md#learn-more).

## Writing a guide

See [AUTHORING.md](AUTHORING.md) for the conventions.

## License

MIT. See [LICENSE](LICENSE).
