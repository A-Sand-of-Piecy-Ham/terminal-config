---
name: dotfiles
description: User's dotfiles repo — location, purpose, contents, and how to contribute to it
metadata:
  type: reference
---

Dotfiles repo lives at `~/projects/ConfigMe/` (GitHub remote is still named `terminal-config`). Managed with symlinks via `install.sh` — run after cloning on a new machine. `install.sh` detects the platform (macOS / Linux+WSL / Git Bash) and links only what applies.

**Two checkouts, one source of truth:** the WSL checkout at `~/projects/ConfigMe` is authoritative; a second native clone at `C:\Users\maxwa\ConfigMe` is a read-only mirror installed by `install.ps1`. Edit in WSL, commit, push, then pull and re-run `install.ps1` on Windows. The mirror exists because Windows reads through `\\wsl.localhost` cross the 9p bridge, which costs roughly an order of magnitude per file operation.

**Purpose:** Replicate development environment (editor, terminal, tools, Claude config) across machines without committing machine-specific or proprietary config.

**Current contents:**
- `nvim/` → `~/.config/nvim` — AstroNvim config with clangd, DAP/codelldb, Telescope, Copilot; `lazy-lock.json` tracked for reproducible plugin versions
- `tmux/` → `~/.tmux.conf` — tmux with tpm plugins
- `ghostty/` → `~/Library/Application Support/com.mitchellh.ghostty/config` (macOS) or `~/.config/ghostty/config` (Linux)
- `wezterm/` → `~/.wezterm.lua` on Windows; defaults to WSL+tmux with Git Bash, plain WSL, and PowerShell in the launcher
- `bash/` → per-OS `bashrc.{darwin,linux,windows}` and matching `bash_profile.*`, over a shared `common.sh` linked to `~/.config/dotfiles/common.sh`. Platform-specific config must go in the per-OS file, never `common.sh`.
- `git/` → `~/.gitconfig` + `~/.gitignore_global`
- `ccache/` → `~/Library/Preferences/ccache/ccache.conf` (macOS) or `~/.config/ccache/ccache.conf`
- `github-templates/` → generic PR template and project-standards reference doc, not tied to any specific repo
- `claude/` → `CLAUDE.md` (global instructions), memory, skills

**What is intentionally excluded:** fish config, 1Password, employer/work-project-specific config (proprietary tool names, internal paths, ticket systems), auth tokens and keys, machine-specific paths.

**How to add new config:**
1. Copy the live config file into the appropriate subdir of `~/projects/ConfigMe/`
2. Add a `link` call in `install.sh`, and a `New-DirLink`/`New-Shim` call in `install.ps1` if it applies to Windows
3. Run `install.sh` to replace the original with a symlink

**How to apply:** Suggest adding config to dotfiles when the user sets up a new tool, tweaks a config that isn't tracked yet, or when a setting would clearly be useful on other machines. Keep suggestions lightweight — one line is enough.
