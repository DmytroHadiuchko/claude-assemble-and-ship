# qa-kit

A small Claude Code plugin with two helpers for the end of a coding session: one summarises what changed on your branch, the other reviews those changes.

## What's inside

```
.
├── .claude-plugin/
│   └── plugin.json            # manifest: name "qa-kit", version
├── commands/
│   └── summarize-changes.md   # slash command
└── agents/
    └── code-reviewer.md       # subagent
```

### `/qa-kit:summarize-changes` (command)

Summarises the changes on the current branch: every touched file with a one-line description of what changed in it. The output is short enough to paste straight into a pull-request description.

### `code-reviewer` (subagent)

Reviews recently changed code for bugs, missing error handling and unclear names. Returns a short list grouped by severity (high, medium, low), each item naming the file and what to fix in one sentence. It is read-only (`Read`, `Grep`, `Glob`) and runs on Sonnet.

## Usage

Load the plugin from the repo root:

```bash
claude --plugin-dir .
```

Then, inside Claude Code:

- Run `/qa-kit:summarize-changes` to get a summary of your branch.
- Ask Claude to review your recent changes, e.g. *"review my recent changes"*. It should delegate to the `code-reviewer` subagent.
- After editing any plugin file, run `/reload-plugins` to pick up the changes.
