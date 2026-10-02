# Brain Installer

Claude starts every conversation knowing nothing about you. A "brain" fixes that. It's a folder of plain notes on your computer about your work, your life, the people in it, and what you were last doing. Claude reads it at the start of a conversation and adds to it as you go. This installer sets one up for you by asking a few questions.

## What this sets up

The installer creates a folder of ordinary text files. Every brain starts with:

- **A main instruction file** that tells Claude who you are, how you like to work, and how the brain is organized. You can edit it, and Claude suggests changes to it when you correct something.
- **A "where we left off" note**, so the next conversation picks up where the last one ended.
- **An inbox** for quick one-line thoughts to sort out later.
- `daily/`: one note per day, with tasks and notes.
- `people/`: a short note on each person who matters in your work or life.

Then Claude suggests a few folders that fit you, based on your answers. A consultant might get a folder per client, each kept separate from the others. Someone looking for work might get a note per job application. Someone focused on family and health might get private folders for those. You see the plan and can change it before anything is saved.

## How you use it

You talk to Claude normally. A few phrases do specific things:

- **"Plan my day"** starts today's note and brings up unfinished tasks.
- **"Log this"** saves what you've been thinking about to the right place.
- **"Capture for later"** adds a one-liner to the inbox.
- **"Remember this decision"** records what you decided and why.
- **"Wrap up"** saves where you left off.

Next time, Claude reads the notes and already knows the context.

## What you need

- The Claude desktop app, on a paid plan. This guide is written for a Mac, as of October 2026. It should work on Windows too.
- An empty folder, such as `Documents/Brain`.
- Optional: Obsidian, a free app for browsing your notes. You don't need it to use the brain.

## Steps

1. **Make an empty folder**, such as `Documents/Brain`.
2. **Start a new conversation in the Claude desktop app.** If your app has separate Chat and Cowork options, choose Cowork. The website and phone app won't work for setup, because they can't reach folders on your computer.
3. **Give Claude access to the empty folder.** Claude asks for your permission the first time.
4. **Paste this message into the conversation:**

   ```
   Please read the brain installer at
   https://raw.githubusercontent.com/danjamk/agentic-guides/main/brain/brain-installer.md
   and follow its instructions to set up my brain in this folder.
   ```

5. **Answer the questions.** There are seven or eight. Short answers are fine. It takes around 10 minutes.

Claude shows you the plan and waits for your OK before saving anything.

**If Claude says it can't open the link,** download the installer instead. Open [this page](https://github.com/danjamk/agentic-guides/blob/main/brain/brain-installer.md) and click the download button (a downward arrow) near the top right. Drag the downloaded file into the conversation and type: **Run this installer.**

## Using your brain outside the desktop app

- **On your computer:** a folder you connect to one conversation doesn't carry over to the next. Make a project from your brain folder in the Claude desktop app instead, so every conversation in that project has the brain connected. Claude walks you through this at the end of setup.
- **On your phone or the website:** Claude can reach the brain only in a conversation you started on your computer, and only while the desktop app is still open there. A brand-new conversation on your phone can't see it.
- **Everywhere:** at the end of setup, Claude gives you a few lines to paste into Claude's settings, under "Instructions for Claude." Those lines apply to every conversation, so Claude always knows the brain exists and asks you to connect it instead of guessing.

## It changes with you

As you use it, Claude notices when something keeps coming up with no place to go, or when a folder stops being used. It suggests a change and asks before making it. You can also say "Review my folders" at any time.

## Privacy

- Your notes are ordinary files in a folder on your computer. They aren't locked inside an app, and you can open, move, or back them up like any other files.
- When you use the brain in a conversation, Claude reads the parts it needs, the same way it reads anything else you share with Claude.
- Never put passwords, account numbers, or ID numbers in your brain.

## Learn more

This installer is one way to give an AI assistant good context about you. These pieces explain the idea and show other ways to do it.

**Getting started**

- [File over app](https://stephango.com/file-over-app), by Steph Ango, the CEO of Obsidian. Why your notes should be plain files you own instead of living inside one app.
- [The PARA Method](https://fortelabs.com/blog/para/), by Tiago Forte. A popular, simple way to organize notes into projects, areas, resources, and archives.
- [How to Use Claude Code as a Thinking Partner](https://every.to/podcast/how-to-use-claude-code-as-a-thinking-partner), a podcast episode with transcript from Every, where Noah Brier shows how he works with Claude across about 1,500 notes.
- [How I Connected Claude Code to My Obsidian Vault: A Guide for Non-Coders](https://darrenrowse.com/posts/how-i-connected-claude-code-to-my-obsidian-vault-a-guide-for-non-coders), by Darren Rowse. A self-described non-technical person sets up Claude to read two years of his notes.
- [Stop Repeating Yourself: Give Claude Code a Memory](https://www.producttalk.org/give-claude-code-a-memory/), by Teresa Torres. Three layers of notes, so she stops re-explaining herself to Claude. Part of it is for subscribers only.
- [Context Engineering](https://simonwillison.net/2025/Jun/27/context-engineering/), by Simon Willison. A short post on why giving AI the right information matters more than clever wording.

**Going deeper**

- [LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f), by Andrej Karpathy. A pattern where the AI builds and maintains a personal wiki of notes for you. This is the closest idea to the brain.
- [Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents), from Anthropic. How AI agents use structured notes to keep track of work over time.
- [How Claude remembers your project](https://code.claude.com/docs/en/memory), from Anthropic. The official explanation of the instruction file Claude reads at the start of each session.
- [claudesidian](https://github.com/heyitsnoah/claudesidian), by Noah Brier. A ready-made notes setup for Claude and Obsidian, for people comfortable with technical tools. This installer started from ideas in it.
