# AI Config

Shared AI configuration for use across machines.

## Install

- [RTK](https://github.com/rtk-ai/rtk#installation)
- [Caveman](https://github.com/JuliusBrussee/caveman/blob/main/INSTALL.md)
- [Ponytail](https://github.com/DietrichGebert/ponytail#codex)

## Share preferences between Codex and Claude

`configs/FORBIDDEN_PATTERNS.md` and `configs/OPINIONS.md` are canonical files.
Link each AI tool's copy to them so one edit applies everywhere.

### Linux

1. Clone this repository somewhere permanent, such as `~/ai-config`.
2. Run these commands from repository root.

```bash
mkdir -p ~/.codex ~/.claude
ln -sfn "$PWD/configs/FORBIDDEN_PATTERNS.md" ~/.codex/FORBIDDEN_PATTERNS.md
ln -sfn "$PWD/configs/OPINIONS.md" ~/.codex/OPINIONS.md
ln -sfn "$PWD/configs/FORBIDDEN_PATTERNS.md" ~/.claude/FORBIDDEN_PATTERNS.md
ln -sfn "$PWD/configs/OPINIONS.md" ~/.claude/OPINIONS.md
```

`ln -sfn` safely refreshes existing symlinks, but will not overwrite a regular file.
Move or back up a regular destination file before running it.

### Windows

1. Clone this repository somewhere permanent, such as `%USERPROFILE%\ai-config`.
2. Open PowerShell.
3. Enable Windows Developer Mode or open PowerShell as Administrator so Windows permits symlinks.
4. Set `$repo` to this repository's full path, then run these commands.

```powershell
$repo = "$HOME\ai-config"
$source = Join-Path $repo "configs"
New-Item -ItemType Directory -Force -Path "$HOME\.codex", "$HOME\.claude"
New-Item -ItemType SymbolicLink -Path "$HOME\.codex\FORBIDDEN_PATTERNS.md" -Target "$source\FORBIDDEN_PATTERNS.md"
New-Item -ItemType SymbolicLink -Path "$HOME\.codex\OPINIONS.md" -Target "$source\OPINIONS.md"
New-Item -ItemType SymbolicLink -Path "$HOME\.claude\FORBIDDEN_PATTERNS.md" -Target "$source\FORBIDDEN_PATTERNS.md"
New-Item -ItemType SymbolicLink -Path "$HOME\.claude\OPINIONS.md" -Target "$source\OPINIONS.md"
```

If a destination file already exists, move or back it up before creating its symlink.

### Edit and verify

Edit only these repository files:

- `configs/FORBIDDEN_PATTERNS.md`
- `configs/OPINIONS.md`

Restart any agent session already open after editing.
New sessions read updated files through their symlinks.
