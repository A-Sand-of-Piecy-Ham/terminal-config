---
name: dotfiles
description: User's dotfiles repo — location, purpose, contents, and how to contribute to it
metadata:
  type: reference
---

Dotfiles repo lives at `~/projects/dotfiles/`. Managed with symlinks via `install.sh` — run after cloning on a new machine.

**Purpose:** Replicate development environment (editor, terminal, tools, Claude config) across machines without committing machine-specific or proprietary config.

**Current contents:**
- `nvim/` → `~/.config/nvim` — AstroNvim config with clangd, DAP/codelldb, Telescope, Copilot; `lazy-lock.json` tracked for reproducible plugin versions
- `tmux/` → `~/.tmux.conf` — tmux with tpm plugins
- `ghostty/` → `~/Library/Application Support/com.mitchellh.ghostty/config.ghostty`
- `wezterm/` → reference config for a secondary machine, not symlinked by `install.sh`
- `bash/` → `~/.bashrc` + `~/.bash_profile`
- `git/` → `~/.gitconfig` + `~/.gitignore_global`
- `ccache/` → `~/Library/Preferences/ccache/ccache.conf`
- `github-templates/` → generic PR template and project-standards reference doc, not tied to any specific repo
- `claude/` → `CLAUDE.md` (global instructions), memory, skills

**What is intentionally excluded:** fish config, 1Password, employer/work-project-specific config (proprietary tool names, internal paths, ticket systems), auth tokens and keys, machine-specific paths.

**How to add new config:**
1. Copy the live config file into the appropriate subdir of `~/projects/dotfiles/`
2. Add a `link` call in `install.sh`
3. Run `install.sh` to replace the original with a symlink

**How to apply:** Suggest adding config to dotfiles when the user sets up a new tool, tweaks a config that isn't tracked yet, or when a setting would clearly be useful on other machines. Keep suggestions lightweight — one line is enough.
