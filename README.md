# git-dateswap

_Change Git commit dates easily and interactively — one or many at a time._

Easily edit commit dates in a Git repository using text editor. Built on top of [`git-filter-repo`](https://github.com/newren/git-filter-repo), this tool helps you modify dates safely and quickly.

## Features

- Change commit dates via your preferred text editor
- Supports recent N commits or the entire history
- Automatically rewrites the author and committer dates
- Simple and portable (Bash + Python + gum)

## Usage

```bash
git-dateswap [OPTIONS]
```

### Example

Edit the last 3 commits in TUI mode:
```bash
git-dateswap -c 3 --tui
```

Edit all commits and show debug info:
```bash
git-dateswap --all --debug
```

Run without restoring the Git remote:
```bash
git-dateswap --no-restore-remote
```

## Options

| Option                | Description                                                            |
| --------------------- | ---------------------------------------------------------------------- |
| `-c`, `--commits N`   | Number of recent commits to edit                                       |
| `-a`, `--all`         | Edit all commits in the repository                                     |
| `-d`, `--debug`       | Print debug info                                                       |
| `-t`, `--tui`         | Use the interactive TUI (via gum)                                      |
| `--no-restore-remote` | Do **not** restore the `origin` remote after running `git-filter-repo` |

---

## ⚠️ Remote Removal by git-filter-repo

`git-filter-repo` intentionally removes the `origin` remote after rewriting history to prevent accidental `git push --force`. This is expected behavior.

**However, `git-dateswap` will automatically re-add the `origin` remote** (with the same URL) after the process, unless you pass the `--no-restore-remote` flag.

This makes it safer for local or personal use, while still allowing advanced users to disable it when necessary.

---

## 🛠 Dependencies

- [git-filter-repo](https://github.com/newren/git-filter-repo)
- [gum](https://github.com/charmbracelet/gum) (optional, for TUI mode)

The script will check for these tools and guide you through installation if needed.

---

## Installation

```bash
# Clone the repo
git clone https://github.com/paulocsb/git-dateswap.git
cd git-dateswap

# Make it executable
chmod +x git-dateswap

# (Optional) Add it to your $PATH
echo 'export PATH="$PATH:$(pwd)"' >> ~/.bashrc  # or ~/.zshrc
source ~/.bashrc  # or ~/.zshrc
```
> 📌 **Note:** You can place it anywhere in your PATH

---

## Example Workflow

```bash
# Edit last 5 commits in a text editor
git dateswap -c 5

# Edit all commits using the TUI
git dateswap --all --tui

# Push changes
git push --force
```

## Notes
- Commit messages and hashes remain unchanged (except for the date).
- You’ll be prompted once to choose your editor. The preference is saved in `~/.dateswap-settings`.

## Uninstall

Just delete the script:

```bash
rm /<YOUR-PATH>/git-dateswap
rm ~/.dateswap-settings
```
