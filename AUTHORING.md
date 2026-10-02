# Authoring a guide

Conventions for writing a new guide. `brain/brain-installer.md` is the reference example.

## Delivery modes

| Mode | How it works | Use when |
|---|---|---|
| **Pointer prompt** (default) | The human pastes a one-line prompt that has the agent read the guide from a link and follow it. | Most setups. The agent can usually open a public link. |
| **Dropped file** (fallback) | The human downloads the guide and hands it to the agent. | The agent can't open the link, for example because web access is turned off for the account. |

- Write the guide so it works either way. Both modes use the same file.
- In the pointer prompt, link the raw file on `main` (`raw.githubusercontent.com/<owner>/<repo>/main/<path>`), so the agent gets plain text and the link never changes. `main` is the release branch: merge to it only when a version is ready, and tag it. Put the link on its own line in the README's copy box, because GitHub doesn't wrap code blocks.
- Word the prompt as the human's own request ("Please read … and follow its instructions to …"). An agent may treat instructions it finds on a web page as content to summarize, unless the human clearly asked it to follow them.
- Offer the dropped file in the folder README as the fallback, with a link to the file's page on `main`. Don't link the raw file for downloads.

## Structure

Every guide has these parts, in this order.

1. **Human section at the top.** A short section addressed to the person: what the guide does, how to start it, how long it takes. Then a heading that hands over to the agent ("For Claude: ... instructions").
2. **Rules for the whole run.** These apply to every step:
   - Plain language. Name the technical words the agent must avoid or explain.
   - One question at a time. Wait for each answer.
   - No writes until the human approves a summary.
   - Never overwrite or delete existing files.
3. **Preflight.** Check the environment and the folder state before anything else. List each case and what to do: empty folder, folder that already has this guide's output, folder with other files, no folder open.
4. **Interview.** Numbered questions, asked in order. After each question, a bracketed note for the agent naming the exact placeholder, file, or section the answer fills. If a question doesn't map to output, cut it. Say "skip" is allowed.
5. **Confirm before write.** The agent summarizes what it will create in plain language, under about 12 lines, and waits for a yes. Changes loop back to a new summary.
6. **Build.** List every file to create, grouped by "always" and "only if." Each file names its template.
7. **Templates inline.** Put templates in the guide itself, fenced with `~~~~` so they can contain ``` blocks. Use `{{PLACEHOLDERS}}` and give a fill rule for each one that isn't obvious. State what to do when an answer was skipped: delete the line or section, never leave a placeholder behind.
   When the right output depends on the person, don't hardcode modes. Give the agent a fixed core, a small set of named shapes, and design rules, and have it show the layout it designed in the confirm step. If the output should keep changing after setup, write the rules for that change into the output itself (see "How this brain grows" in the brain installer).
8. **Handoff.** Tell the human three things: what was done, how to come back next time (the exact phrase to type), and one thing to try right now.

## Version stamp

- Put the version in the guide's header: `**Version:** <guide>-vX.Y (YYYY-MM-DD)`.
- Write the version into whatever the guide produces, so the output records which version made it.
- Release by tagging the repo `<guide>-vX.Y`. Bump the minor number for wording and template fixes. Bump the major number when the output's structure changes.
- Keep a **Changelog** section at the end of the guide file itself, not in a separate file, because the agent only reads the guide file. Newest first. Write each change for an agent upgrading something an older version produced:

  ```
  ### <guide>-vX.Y (YYYY-MM-DD)
  - **<What changed>.** Affects: <file and section, or "installer only">.
    Existing output: recommended | optional | not needed.
    How to apply: <one or two sentences, as intent, not exact text>.
  ```

  Pair it with an upgrade path in the preflight: when the agent finds output stamped with an older version, it offers the changes since then, applies only what the human approves, merges instead of replacing, and updates the stamp.
- If a guide is based on another project, credit it in the root README's Credits section. Before each release, review that project's changes since your last release and bring over what fits your guide's audience. The guide itself never fetches the other project when it runs, because that would make the same version produce different results on different days.

## Folder layout

Each guide gets its own folder:

```
<guide>/
├── README.md        # for the human who lands here
└── <guide>.md       # the guide itself
```

The folder README is for the end user, who may not be technical. Keep technical words out of it. Link the download to the file's page on `main`, not the raw file, because a raw link opens as a page of text instead of downloading.

**Add-ons** extend what a guide built. Put each one in the guide's folder as `addon-<name>.md`, structured like a guide, with its own version stamp and changelog. Its preflight checks that the base output exists and which version made it, and its handoff tests that the add-on works. List every add-on, including planned ones, in an "Add-ons" table in the folder README. The base output links to that table on `main`, so output made by older versions still finds new add-ons.

## Writing the agent instructions

- Write instructions as direct commands to the agent.
- Name the agent and platform the guide was written for (for example, Claude in Cowork on a Mac). Tell other agents to adapt the steps and say what they changed.
- Separate the fixed rules from everything else. Let the agent adapt the interview and templates to the person, including skipping questions it can already answer from what it knows about them.
- Say what to do when something goes wrong or is missing. Agents fill gaps by guessing.
- Give the agent no room to add extras: no unrequested folders, scripts, or automations.
- Tell the agent never to record sensitive data (passwords, account numbers, ID numbers).
- Add a row to the root README's guide table.
