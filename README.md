# OpenCode Themes

A curated collection of themes for the [OpenCode](https://opencode.ai/) CLI.

> **Unofficial Community Project**
>
> This repository is a community-maintained third-party theme pack and is **not affiliated with, endorsed by, or supported by the upstream OpenCode project or its authors**. For official OpenCode resources, please visit [opencode.ai](https://opencode.ai/).

## Themes Included

### Solarized

Ported from the classic [Solarized](https://ethanschoonover.com/solarized/) color scheme by Ethan Schoonover.

| Theme | Description |
|-------|-------------|
| `solarized` | Canonical Solarized with both dark & light mode support using original base color names |
| `solarized-dark` | Dark variant with traditional 16-color terminal palette |
| `solarized-light` | Light variant with traditional 16-color terminal palette |
| `solarized-dark-higher-contrast` | Higher contrast dark variant for better readability |
| `solarized-dark-patched` | Patched dark variant with adjusted color values |
| `solarized-darcula` | Solarized meets Darcula — a darker, muted take on the palette |
| `solarized-osaka-night` | Osaka Night inspired variant using Solarized hues |

### Winter is Coming

Ported from the VS Code [Winter is Coming](https://github.com/johnpapa/vscode-winteriscoming) theme by John Papa.

| Theme | Description |
|-------|-------------|
| `winter-is-coming-dark-blue` | Deep navy blue background (#011627) with bright blue and teal accents — the signature variant |
| `winter-is-coming-dark-black` | Dark charcoal background (#282822) with the same bright foreground palette |
| `winter-is-coming-light` | Clean light theme with blue foreground on white background |

### Bearded Theme

Ported from the VS Code/Zed [Bearded Theme](https://github.com/BeardedBear/bearded-theme) by BeardedBear.

| Theme | Description |
|-------|-------------|
| `bearded-theme-arc` | Signature dark variant — deep navy background (#1c2433) with vibrant blue, green, and pink accents |

## Installation

### Global Installation

1. Create the themes directory:

```bash
mkdir -p ~/.config/opencode/themes
```

2. Download the desired theme file(s):

```bash
# --- Solarized variants ---

# Canonical solarized (supports both dark & light)
curl -o ~/.config/opencode/themes/solarized.json \
  https://raw.githubusercontent.com/adamancini/opencode-themes/main/.opencode/themes/solarized.json

# Dark only variant
curl -o ~/.config/opencode/themes/solarized-dark.json \
  https://raw.githubusercontent.com/adamancini/opencode-themes/main/.opencode/themes/solarized-dark.json

# Light only variant
curl -o ~/.config/opencode/themes/solarized-light.json \
  https://raw.githubusercontent.com/adamancini/opencode-themes/main/.opencode/themes/solarized-light.json

# Higher contrast dark
curl -o ~/.config/opencode/themes/solarized-dark-higher-contrast.json \
  https://raw.githubusercontent.com/adamancini/opencode-themes/main/.opencode/themes/solarized-dark-higher-contrast.json

# Patched dark
curl -o ~/.config/opencode/themes/solarized-dark-patched.json \
  https://raw.githubusercontent.com/adamancini/opencode-themes/main/.opencode/themes/solarized-dark-patched.json

# Darcula variant
curl -o ~/.config/opencode/themes/solarized-darcula.json \
  https://raw.githubusercontent.com/adamancini/opencode-themes/main/.opencode/themes/solarized-darcula.json

# Osaka Night variant
curl -o ~/.config/opencode/themes/solarized-osaka-night.json \
  https://raw.githubusercontent.com/adamancini/opencode-themes/main/.opencode/themes/solarized-osaka-night.json

# --- Winter is Coming variants ---

# Dark Blue (signature variant)
curl -o ~/.config/opencode/themes/winter-is-coming-dark-blue.json \
  https://raw.githubusercontent.com/adamancini/opencode-themes/main/.opencode/themes/winter-is-coming-dark-blue.json

# Dark Black
curl -o ~/.config/opencode/themes/winter-is-coming-dark-black.json \
  https://raw.githubusercontent.com/adamancini/opencode-themes/main/.opencode/themes/winter-is-coming-dark-black.json

# Light
curl -o ~/.config/opencode/themes/winter-is-coming-light.json \
  https://raw.githubusercontent.com/adamancini/opencode-themes/main/.opencode/themes/winter-is-coming-light.json

# --- Bearded Theme variants ---

# Arc (signature dark variant)
curl -o ~/.config/opencode/themes/bearded-theme-arc.json \
  https://raw.githubusercontent.com/adamancini/opencode-themes/main/.opencode/themes/bearded-theme-arc.json
```

3. Add the theme to your `~/.config/opencode/opencode.json`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "theme": "solarized-dark"
}
```

4. Restart OpenCode to apply the theme.

### Using the `/theme` Command

Inside OpenCode, type `/theme` and select any of the installed variants.

## Color Palettes

### Solarized Canonical Colors

| Color Name | Hex | Usage |
|------------|-----|-------|
| base03 | #002b36 | Dark background |
| base02 | #073642 | Dark panels |
| base01 | #586e75 | Dark muted text / borders |
| base00 | #657b83 | Light muted text |
| base0 | #839496 | Dark primary text |
| base1 | #93a1a1 | Light primary text / borders |
| base2 | #eee8d5 | Light panels |
| base3 | #fdf6e3 | Light background |
| yellow | #b58900 | Warnings, types |
| orange | #cb4b16 | Variables |
| red | #dc322f | Errors |
| magenta | #d33682 | Numbers, accents |
| violet | #6c71c4 | Links, accents |
| blue | #268bd2 | Primary, keywords, headings |
| cyan | #2aa198 | Secondary, functions, links |
| green | #859900 | Success, strings |

### Winter is Coming — Dark Blue & Dark Black Variants

| Role | Hex | Usage |
|------|-----|-------|
| Background | #011627 (blue) / #282822 (black) | Editor background |
| Foreground | #a7dbf7 | Primary text |
| Primary | #219fd5 | Links, active elements, headings |
| Secondary | #5ABEB0 | Secondary highlights |
| Accent | #c792ea | Purple accents |
| Error | #ef5350 | Errors, removed diffs |
| Warning | #ffca28 | Warnings |
| Success | #5ABEB0 | Success, added diffs |
| String | #bcf0c0 | Strings |
| Keyword | #00bff9 | Keywords, operators |
| Function | #87aff4 | Functions |
| Type | #d29ffc | Types, classes |
| Number | #8dec95 | Numbers, booleans |
| Variable | #d6deeb | Variables |
| Comment | #999999 | Comments |

### Winter is Coming — Light Variant

| Role | Hex | Usage |
|------|-----|-------|
| Background | #FFFFFF | Editor background |
| Foreground | #236ebf | Primary text |
| Primary | #219fd5 | Links, active elements |
| Secondary | #2f86d2 | Secondary highlights |
| Accent | #c792ea | Purple accents |
| Error | #ef5350 | Errors |
| Warning | #f7ecb5 | Warnings |
| Success | #189b2c | Success |
| String | #a44185 | Strings |
| Keyword | #0991b6 | Keywords |
| Function | #b1108e | Functions |
| Type | #0444ac | Types |
| Number | #174781 | Numbers |
| Variable | #2f86d2 | Variables |
| Comment | #357b42 | Comments |

### Bearded Theme — Arc Variant

| Role | Hex | Usage |
|------|-----|-------|
| Background | #1c2433 | Editor background |
| Panel Background | #181f2c | Sidebars, panels |
| Element Background | #253043 | Inputs, selections |
| Foreground | #d0d7e4 | Primary text |
| Primary | #8196b5 | Links, active elements, headings |
| Secondary | #69c3ff | Alternate accent, functions |
| Accent | #f38cec | Standout highlights, decorators |
| Error | #e35535 | Errors, removed diffs, constants |
| Warning | #ff955c | Warnings, accessors, numbers |
| Success | #3cec85 | Success, added diffs, strings |
| Info | #69c3ff | Info highlights |
| Keyword | #eacd61 | Keywords, operators |
| Function | #69c3ff | Functions |
| Type | #b78aff | Types, classes |
| Variable | #ff738a | Variables |
| String | #3cec85 | Strings |
| Comment | #4a5e84 | Comments, muted text |
| Cyan | #22ecdb | Storage keywords |

## Terminal Requirements

For best results, ensure your terminal supports **truecolor** (24-bit color):

- Check support: `echo $COLORTERM` (should output `truecolor` or `24bit`)
- Enable if needed: `export COLORTERM=truecolor`

Most modern terminals (iTerm2, Alacritty, Kitty, Windows Terminal, GNOME Terminal) support this by default.

## Theme Development Skill

This repository includes the **OpenCode Themer** skill — a guide for absorbing and distilling color themes from other applications (VS Code, terminal emulators, CSS, etc.) into valid OpenCode `theme.json` files.

To use it, copy the skill into your OpenCode skills directory:

```bash
mkdir -p ~/.claude/skills/opencode-themer
curl -o ~/.claude/skills/opencode-themer/SKILL.md \
  https://raw.githubusercontent.com/adamancini/opencode-themes/main/SKILL.md
```

Restart OpenCode and mention "port a theme" or "absorb a VS Code theme" to activate the skill.

## Contributing

Want to add a new theme? See the [OpenCode Theme Documentation](https://opencode.ai/docs) for the theme schema and color token reference.

## License

MIT License — see [LICENSE](LICENSE) file for details.

## Acknowledgments

- [Solarized](https://ethanschoonover.com/solarized/) by Ethan Schoonover
- [Winter is Coming](https://github.com/johnpapa/vscode-winteriscoming) by [John Papa](https://twitter.com/john_papa)
- Light theme co-authored by [Brian Clark](https://twitter.com/_clarkio)
- [Bearded Theme](https://github.com/BeardedBear/bearded-theme) by [BeardedBear](https://bento.me/bearded)
- Ported for the [OpenCode](https://opencode.ai/) CLI
