---
name: opencode-themer
description: >-
  This skill should be used when the user wants to port, absorb, distill, or
  convert a color theme from another application (VS Code, terminal emulator,
  IDE, web palette, CSS variables, etc.) into an OpenCode-compatible
  theme.json file.  Provides the complete schema mapping, extraction
  heuristics, and a repeatable workflow for generating validated OpenCode
  themes.
version: 0.1.0
---

# OpenCode Themer

Converts third-party color themes into OpenCode `theme.json` files.

## When to Use This Skill

- A user asks to "port my VS Code theme to OpenCode"
- A user pastes a color palette and wants an OpenCode theme generated
- A user wants to convert a terminal/iTerm/Alacritty theme to OpenCode
- A user wants to extract colors from a website/CSS and build an OpenCode theme
- A user wants to create a new OpenCode theme based on an existing palette

## Core Workflow

### Step 1 — Ingest the Source Palette

Gather the source colors by any available means:

| Source | How to ingest |
|--------|---------------|
| **VS Code** | Ask for the `.json` theme file, or look up `colors` and `tokenColors` arrays |
| **Terminal / iTerm** | Ask for the `.itermcolors` plist, or a screenshot with a color picker |
| **CSS / Web** | Ask for the stylesheet or a list of CSS custom properties |
| **Image / Screenshot** | Use the image directly; OpenCode can extract dominant colors |
| **Plain text** | Accept a list of hex values with semantic labels |

**Key fields to extract from VS Code themes:**
- `colors.editor.background` → background
- `colors.editor.foreground` → text
- `colors.editor.selectionBackground` → accent / secondary
- `colors.terminal.ansi*` → error, warning, success, primary, secondary
- `colors.activityBarBadge.background` → accent
- `tokenColors` with `scope` → syntax tokens (keyword, string, function, etc.)

### Step 2 — Build the `defs` Block

The `defs` object holds reusable color names.  All values must be **6-digit hex** (`#RRGGBB`) or **ANSI codes** (`0-255`).

Use semantic names so the `theme` block reads like prose:

```json
"defs": {
  "bg": "#1e1e2e",
  "bgPanel": "#181825",
  "bgElement": "#313244",
  "fg": "#cdd6f4",
  "muted": "#6c7086",
  "primary": "#89b4fa",
  "secondary": "#a6e3a1",
  "accent": "#f5c2e7",
  "error": "#f38ba8",
  "warning": "#fab387",
  "success": "#a6e3a1",
  "info": "#89b4fa",
  "cyan": "#89dceb",
  "blue": "#89b4fa",
  "purple": "#cba6f7",
  "green": "#a6e3a1",
  "red": "#f38ba8",
  "yellow": "#f9e2af",
  "orange": "#fab387",
  "white": "#cdd6f4",
  "comment": "#6c7086"
}
```

**Guidelines:**
- Keep `defs` to **12–20 entries**.  Too many names become unmaintainable.
- Prefer abstract semantic names (`bg`, `fg`, `primary`) over literal color names (`darkBlue`, `lightGreen`).
- If the source theme has both dark and light variants, use the same key names in both variants so the `theme` block can reference them consistently.

### Step 3 — Map to the `theme` Block

Every key in `theme` resolves to a color via:
- A `defs` name (e.g. `"dark": "bg"`)
- A raw hex string (e.g. `"dark": "#1e1e2e"`)
- An ANSI code (e.g. `"dark": 235`)
- `"none"` for terminal default

**Required tokens:** `primary`, `secondary`, `accent`, `text`, `textMuted`, `background`

**Complete token map:**

| Token | Typical mapping from source |
|-------|----------------------------|
| `primary` | Brand / link / heading color |
| `secondary` | Alternate accent / highlight |
| `accent` | Badge / selection / standout |
| `error` | Red / `ansiRed` |
| `warning` | Orange / yellow / `ansiYellow` |
| `success` | Green / `ansiGreen` |
| `info` | Blue / `ansiCyan` |
| `text` | `editor.foreground` |
| `textMuted` | `editorLineNumber.foreground` / comment color |
| `background` | `editor.background` |
| `backgroundPanel` | `sideBar.background` / slightly lighter/darker than background |
| `backgroundElement` | `input.background` / `list.activeSelectionBackground` |
| `border` | `panel.border` / `editorGroup.border` |
| `borderActive` | `focusBorder` / `tab.activeBorder` |
| `borderSubtle` | `tree.indentGuidesStroke` |
| `diffAdded` | `diffEditor.insertedTextBackground` foreground color |
| `diffRemoved` | `diffEditor.removedTextBackground` foreground color |
| `diffContext` | `textMuted` |
| `diffHunkHeader` | `textMuted` |
| `diffHighlightAdded` | `diffAdded` |
| `diffHighlightRemoved` | `diffRemoved` |
| `diffAddedBg` | `backgroundPanel` |
| `diffRemovedBg` | `backgroundPanel` |
| `diffContextBg` | `backgroundPanel` |
| `diffLineNumber` | `textMuted` |
| `diffAddedLineNumberBg` | `backgroundPanel` |
| `diffRemovedLineNumberBg` | `backgroundPanel` |
| `markdownText` | `text` |
| `markdownHeading` | `primary` |
| `markdownLink` | `secondary` |
| `markdownLinkText` | `accent` |
| `markdownCode` | `success` / `green` |
| `markdownBlockQuote` | `textMuted` |
| `markdownEmph` | `accent` |
| `markdownStrong` | `primary` |
| `markdownHorizontalRule` | `border` |
| `markdownListItem` | `secondary` |
| `markdownListEnumeration` | `primary` |
| `markdownImage` | `secondary` |
| `markdownImageText` | `accent` |
| `markdownCodeBlock` | `text` |
| `syntaxComment` | `comment` |
| `syntaxKeyword` | `primary` / `cyan` |
| `syntaxFunction` | `blue` / `secondary` |
| `syntaxVariable` | `text` / `white` |
| `syntaxString` | `green` |
| `syntaxNumber` | `yellow` / `mint` |
| `syntaxType` | `purple` / `yellow` |
| `syntaxOperator` | `cyan` / `secondary` |
| `syntaxPunctuation` | `text` / `white` |

**Dark/Light split:**

If the source has **only one mode**, use identical values for `dark` and `light`:

```json
"text": { "dark": "fg", "light": "fg" }
```

If the source has **separate dark and light palettes**, reference different `defs`:

```json
"text": { "dark": "fgDark", "light": "fgLight" }
```

### Step 4 — Assemble and Validate

**Minimal valid theme.json:**

```json
{
  "$schema": "https://opencode.ai/theme.json",
  "defs": {
    "bg": "#1e1e2e",
    "fg": "#cdd6f4",
    "primary": "#89b4fa",
    "secondary": "#a6e3a1",
    "accent": "#f5c2e7",
    "error": "#f38ba8",
    "warning": "#fab387",
    "success": "#a6e3a1",
    "info": "#89b4fa",
    "muted": "#6c7086"
  },
  "theme": {
    "primary":   { "dark": "primary",   "light": "primary" },
    "secondary": { "dark": "secondary", "light": "secondary" },
    "accent":    { "dark": "accent",    "light": "accent" },
    "error":     { "dark": "error",     "light": "error" },
    "warning":   { "dark": "warning",   "light": "warning" },
    "success":   { "dark": "success",   "light": "success" },
    "info":      { "dark": "info",      "light": "info" },
    "text":      { "dark": "fg",        "light": "fg" },
    "textMuted": { "dark": "muted",     "light": "muted" },
    "background":         { "dark": "bg", "light": "bg" },
    "backgroundPanel":    { "dark": "bg", "light": "bg" },
    "backgroundElement":  { "dark": "bg", "light": "bg" },
    "border":             { "dark": "muted", "light": "muted" },
    "borderActive":       { "dark": "primary", "light": "primary" },
    "borderSubtle":       { "dark": "bg", "light": "bg" }
  }
}
```

**Validation checklist:**
- [ ] `"$schema"` is present
- [ ] All `defs` values are valid hex (`#RRGGBB`) or integers `0-255`
- [ ] Every `theme` value resolves to a known `defs` key, a hex string, an ANSI code, or `"none"`
- [ ] Every `theme` token uses either `{ "dark": ..., "light": ... }` or a flat value
- [ ] Required tokens exist: `primary`, `secondary`, `accent`, `text`, `textMuted`, `background`
- [ ] No extra properties outside `defs` and `theme`

### Step 5 — Test in OpenCode

1. Write the file to `~/.config/opencode/themes/<name>.json`
2. Set `"theme": "<name>"` in `~/.config/opencode/opencode.json`
3. Restart OpenCode and run `/theme` to verify rendering

## Extraction Cheat-Sheets

### VS Code Theme → OpenCode

```bash
# Extract the palette with jq (install jq if needed)
jq '{ background: .colors["editor.background"],
      foreground: .colors["editor.foreground"],
      ansiRed: .colors["terminal.ansiRed"],
      ansiGreen: .colors["terminal.ansiGreen"],
      ansiYellow: .colors["terminal.ansiYellow"],
      ansiBlue: .colors["terminal.ansiBlue"],
      ansiMagenta: .colors["terminal.ansiMagenta"],
      ansiCyan: .colors["terminal.ansiCyan"],
      ansiWhite: .colors["terminal.ansiWhite"] }' theme.json
```

Map the extracted hex values directly into `defs` and wire up `theme` tokens.

### Terminal Emulator (iTerm2) → OpenCode

iTerm2 colors are stored as plists.  Convert to JSON with `plutil`:

```bash
plutil -convert json -o theme.json theme.itermcolors
```

Then extract the `Ansi 0`–`Ansi 15` and `Background` / `Foreground` entries.

### CSS Custom Properties → OpenCode

Given CSS like:

```css
:root {
  --color-bg: #0d1117;
  --color-fg: #c9d1d9;
  --color-accent: #58a6ff;
}
```

Strip `--color-` prefixes and use the hex values as `defs` entries.

## Tips for Good Contrast

- **Background vs Text**: Ensure a contrast ratio of at least 4.5:1 (WCAG AA).
- **Muted text**: Should still be readable; do not push it below ~3:1.
- **Accents on backgrounds**: Test `primary`, `secondary`, and `accent` on both `background` and `backgroundPanel`.
- **Diff colors**: `diffAdded` and `diffRemoved` must be distinguishable from each other and from `background`.

## Common Pitfalls

- **Using `#RRGGBBAA` or `rgb(...)`**: OpenCode only accepts 6-digit hex or ANSI codes.
- **Inconsistent defs references**: A `theme` token points to a `defs` key that does not exist.
- **Missing required tokens**: Forgetting `textMuted` or `background` causes fallback to the built-in default theme.
- **Too many defs entries**: Keep the palette tight; 15–20 colors is usually enough.
- **Dark/light asymmetry**: If you support both modes, make sure both `dark` and `light` keys are present in every split token.

## Additional Resources

- Official OpenCode theme schema: `https://opencode.ai/theme.json`
- Example themes: `https://github.com/adamancini/opencode-themes/tree/main/.opencode/themes`
