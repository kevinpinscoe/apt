# kevinpinscoe/apt

Debian APT repository for [kevinpinscoe](https://github.com/kevinpinscoe) Go tools, served via GitHub Pages.

## Install

```bash
curl -sL https://kevinpinscoe.github.io/apt/gpg.key \
  | sudo gpg --dearmor -o /etc/apt/keyrings/kevinpinscoe.gpg

echo "deb [signed-by=/etc/apt/keyrings/kevinpinscoe.gpg] \
  https://kevinpinscoe.github.io/apt stable main" \
  | sudo tee /etc/apt/sources.list.d/kevinpinscoe.list

sudo apt update
```

Then install any available tool:

```bash
sudo apt install get-wx
sudo apt install metar-tool
sudo apt install skills-tui
sudo apt install aws-linux-memory-tools
```

## Available packages

| Package | Description |
|---|---|
| `get-wx` | Eastern Tennessee weather forecast fetcher |
| `metar-tool` | METAR aviation weather decoder |
| `skills-tui` | Interactive TUI skill chooser |
| `aws-linux-memory-tools` | AWS Linux memory diagnostics |

## GPG key

Packages are signed with the key at `gpg.key` in this repo.

Fingerprint: `8CD9AAACEE8B5AFB7607BC2B300FD9BDDA1BF809`

## How packages land here

Each Go tool repo dispatches a `new-release` event to this repo when a tag is pushed.
The `add-package.yml` workflow downloads the `.deb` files from the GitHub release,
adds them via `reprepro`, and pushes the updated repo back to `main`.
