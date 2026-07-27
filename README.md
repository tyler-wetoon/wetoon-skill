# WeToon Claude Code Plugins

Internal plugin marketplace for WeToon.

## Install

```bash
claude plugin marketplace add tyler-wetoon/wetoon-skill
claude plugin install wetoon-dev-tools@wetoon-internal
```

Or from inside an interactive Claude Code session:

```
/plugin marketplace add tyler-wetoon/wetoon-skill
/plugin install wetoon-dev-tools@wetoon-internal
/reload-plugins
```

If the repository is ever made private, collaborators will need GitHub access to it, and SSH-only setups should use the full URL instead of the `owner/repo` shorthand:

```bash
claude plugin marketplace add git@github.com:tyler-wetoon/wetoon-skill.git
```

## Auto-enable for the whole team

Commit this to `.claude/settings.json` in each consuming repository (frontend and backend). Anyone who clones the repo is prompted to install the plugin on first trusting the folder — one confirmation instead of remembering the commands above:

```json
{
  "extraKnownMarketplaces": {
    "wetoon-internal": {
      "source": { "source": "github", "repo": "tyler-wetoon/wetoon-skill" }
    }
  },
  "enabledPlugins": {
    "wetoon-dev-tools@wetoon-internal": true
  }
}
```

## Available plugins

| Plugin | Skills | Description |
| --- | --- | --- |
| `wetoon-dev-tools` | `/wetoon-dev-tools:write-ticket` | Turns a plain-language description into a Story, Task, or Bug ticket using the team's templates |

## Repository layout

```
.claude-plugin/
  marketplace.json                 catalog listing every plugin
plugins/
  wetoon-dev-tools/
    .claude-plugin/plugin.json     plugin manifest
    skills/
      write-ticket/SKILL.md
```

Only `plugin.json` belongs inside `.claude-plugin/`. Everything else (`skills/`, `agents/`, `hooks/`) sits at the plugin root.

## Develop

Validate before pushing:

```bash
claude plugin validate .
claude plugin validate ./plugins/wetoon-dev-tools
```

Test without installing:

```bash
claude --plugin-dir ./plugins/wetoon-dev-tools
```

Then run `/wetoon-dev-tools:write-ticket` in that session. After editing a skill, `/reload-plugins` picks up changes without restarting.

## Release a change

1. Edit the skill.
2. Bump `version` in **both** `plugins/<plugin>/.claude-plugin/plugin.json` and the matching entry in `.claude-plugin/marketplace.json` — `claude plugin validate` warns when they drift.
3. Commit and push.

Users pull the update with `/plugin marketplace update wetoon-internal`. Because `version` is set explicitly, they only receive updates when the number changes.

## Add another skill

```bash
mkdir -p plugins/wetoon-dev-tools/skills/<skill-name>
```

Create `SKILL.md` inside it with `description` frontmatter. The folder name becomes the command name, namespaced as `/wetoon-dev-tools:<skill-name>`.
