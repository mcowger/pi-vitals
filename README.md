# Pi Footer Extension

A customizable powerline-style footer for the pi coding agent. This extension provides a rich, informative status bar at the bottom of the terminal showing model info, git status, token usage, and more.

<img width="1014" height="45" alt="Screenshot 2026-02-15 at 4 44 54 PM" src="https://github.com/user-attachments/assets/278fb369-f3cf-47b9-9a6b-1e49c32ba3c9" />

## Features

- **Customizable segments**: Choose which info to display on the left and right sides
- **Git integration**: Shows current branch and working tree status (staged, unstaged, untracked)
- **Token tracking**: Display input/output/total tokens and cache read/write
- **Context awareness**: Shows context window usage percentage
- **Thinking level**: Visual indicator of model reasoning level
- **Nerd Font support**: Automatic detection with ASCII fallbacks
- **Live updates**: Git status refreshes automatically as you work

## Installation

Install from npm using pi:

```bash
pi install npm:pi-vitals
```

Or copy the extension files to your pi extensions directory manually:

```bash
# Copy to global extensions directory
cp -r . ~/.pi/agent/extensions/pi-footer

# Or use directly for testing
pi -e ./index.ts
```

## Configuration

Create `~/.pi/agent/powerline.json` to customize the footer:

```json
{
  "leftSegments": [
    "pi",
    "separator",
    "model",
    "thinking",
    "separator",
    "path",
    "git",
    "separator",
    "token_total",
    "token_in",
    "token_out",
    "cache_read",
    "cache_write"
  ],
  "rightSegments": [
    "separator",
    "context_pct"
  ],
  "icons": {
    "pi": "π",
    "model": "◈",
    "thinking": "🧠",
    "folder": "📁",
    "git": "⎇",
    "tokens": "⊛",
    "input": "↑",
    "output": "↓",
    "cacheRead": "↙",
    "cacheWrite": "↗",
    "contextPct": "◫",
    "separator": "|"
  },
  "colors": {
    "pi": "accent",
    "model": "#d787af",
    "path": "#00afaf",
    "git": "success",
    "gitDirty": "warning",
    "gitClean": "success",
    "thinking": "muted",
    "context": "dim",
    "contextWarn": "warning",
    "contextError": "error",
    "cost": "text",
    "tokens": "muted",
    "separator": "dim"
  },
  "segmentOptions": {
    "path": {
      "mode": "basename"
    },
    "git": {
      "showBranch": true,
      "showStaged": true,
      "showUnstaged": true,
      "showUntracked": true
    },
    "context_pct": {
      "showAutoIcon": false
    }
  }
}
```

## Available Segments

| Segment | Description |
|---------|-------------|
| `pi` | Pi logo/icon |
| `model` | Current model name |
| `thinking` | Thinking/reasoning level indicator |
| `path` | Current working directory |
| `git` | Git branch and status |
| `token_in` | Input tokens |
| `token_out` | Output tokens |
| `token_total` | Total tokens (input + output + cache) |
| `cache_read` | Cache read tokens |
| `cache_write` | Cache write tokens |
| `cost` | Estimated cost |
| `context_pct` | Context window usage percentage |
| `context_total` | Total context window size |
| `separator` | Visual separator icon |
| `text:...` | Custom text segment (e.g., `text:⚡`) |

## Commands

- `/footer reload` - Reload configuration from disk
- `/footer debug` - Show current configuration

## Path Modes

The `path` segment supports three modes:
- `basename` - Just the directory name (default)
- `abbreviated` - Shortened path with `~` for home
- `full` - Full path

## Git Status Indicators

The `git` segment shows:
- Branch name with icon
- `*N` - Unstaged changes (warning color)
- `+N` - Staged changes (success color)  
- `?N` - Untracked files (muted color)

Colors indicate clean (green) vs dirty (yellow) working tree.

## Icons

The extension automatically detects Nerd Font support (via `TERM_PROGRAM` or `GHOSTTY_RESOURCES_DIR`) and uses appropriate icons. You can force Nerd Fonts with:

```bash
export POWERLINE_NERD_FONTS=1
```

Or disable with:

```bash
export POWERLINE_NERD_FONTS=0
```
