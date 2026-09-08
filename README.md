# kevinpinscoe/apt

Debian APT repository for [kevinpinscoe](https://github.com/kevinpinscoe) tools and apps, served via GitHub Pages.

## Install

```bash
curl -sL https://kevinpinscoe.github.io/apt/gpg.key \
  | sudo gpg --dearmor -o /etc/apt/keyrings/kevinpinscoe.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/kevinpinscoe.gpg] \
  https://kevinpinscoe.github.io/apt stable main" \
  | sudo tee /etc/apt/sources.list.d/kevinpinscoe.list

sudo apt update
```

Then install any available tool:

```bash
sudo apt install aws-linux-memory-tools
sudo apt install check-git-branch
sudo apt install check-git-repos
sudo apt install get-wx
sudo apt install marky-editor
sudo apt install menu-app
sudo apt install metar-tool
sudo apt install pause
sudo apt install skills-tui
```

## Available packages

| Package | Description |
|---|---|
| `aws-linux-memory-tools` | AWS Linux memory diagnostics |
| `check-git-branch` | Scan git repos for non-default branches or leftover local branches |
| `check-git-repos` | Scan git repositories under a root directory for ahead/behind/diverged/uncommitted state |
| `get-wx` | Eastern Tennessee weather forecast fetcher |
| `marky-editor` | Apostrophe-inspired Markdown editor (arm64 / Raspberry Pi only) |
| `menu-app` | Run repository scripts from a simple TUI menu |
| `metar-tool` | METAR aviation weather decoder |
| `pause` | Sleep for N seconds with a live countdown status line on stderr |
| `skills-tui` | Interactive TUI skill chooser |

## GPG key

Packages are signed with the key at `gpg.key` in this repo.

Fingerprint: `8CD9AAACEE8B5AFB7607BC2B300FD9BDDA1BF809`

## How packages land here

Each source repo dispatches a `new-release` event to this repo when a tag is pushed.
The `add-package.yml` workflow downloads the `.deb` files from the GitHub release,
adds them via `reprepro`, and pushes the updated repo back to `main`. Pool binaries
over git's 100MB limit are tracked with Git LFS, and `deploy-pages.yml` republishes
the site as a GitHub Actions artifact (so it serves real bytes, not LFS pointers).

To remove a package (e.g. a bad publish), run the `remove-package.yml` workflow
manually via `gh workflow run remove-package.yml -f package=<name>`.
