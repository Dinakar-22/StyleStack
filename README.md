# StyleStack

A blue glass theme for Discord with an animated Re:Zero Rem background.
Semi-transparent blurred panels, glowing blue borders, smooth spring animations, a rotating ring on the active server and a soft glow on whoever is speaking in voice.

Works with **Vencord**, **BetterDiscord** and any client that loads `.theme.css` files.

> Still under development. Expect small changes between versions. Current version: **1.3**

![StyleStack Overview](https://raw.githubusercontent.com/Dinakar-22/StyleStack/main/assets/screenshots/StyleStack-overview.png)

## Install

**Vencord (online, auto-updates)**

1. Open Discord, then Settings, Vencord, Themes.
2. Paste this into **Online Themes** and save:

```
https://raw.githubusercontent.com/Dinakar-22/StyleStack/refs/heads/main/stylestack.theme.css
```

The theme header also carries an `@updateUrl` pointing at the same file, so clients that support it can check for new versions. Bump `@version` in the header when you publish a change. If you edit a local copy and your changes disappear, remove the `@updateUrl` line.

**Vencord / BetterDiscord (local file)**

1. Download `stylestack.theme.css`. The file name must end in `.theme.css`, or the client will not list it.
2. Open Settings, Vencord (or BetterDiscord), Themes, then **Open Themes Folder**.
3. Drop the file in, then enable it in the Themes list.

The wallpaper files live in the `assets/` folder of this repo. Keep `rem-wallpaper.webp`, `rem-wallpaper-static.jpg` and `Rem.svg` there, because the theme loads them from GitHub.

---

## Options

All options are near the top of `:root` in `stylestack.theme.css`.

### Style preset

```css
--style-preset: glass;   /* glass | solid | minimal */
```

| Preset | Look |
| --- | --- |
| `glass` | Default. Wallpaper, frosted blur, glowing borders, top-edge shine |
| `solid` | No wallpaper, no blur, plain opaque panels. Lightest on the GPU |
| `minimal` | Keeps the wallpaper but uses flat panels: no blur, glow or shine |

### Usability switches

Each one is set to `on` or `off`:

```css
--collapsible-members: on;
--compact-mode:        on;
--readability-mode:    off;
```

| Switch | What it does |
| --- | --- |
| `--collapsible-members` | The member list shrinks to avatars and expands when you hover it. Widths are set with `--member-collapsed-width` (72px) and `--member-expanded-width` (240px). The chat area resizes as the list expands |
| `--compact-mode` | Smaller gaps, corners and message spacing |
| `--readability-mode` | Brighter text, darker panels, a darker wallpaper overlay and a soft shadow behind message text. Use it if the wallpaper makes text hard to read |

---

## Change the wallpaper

The wallpaper is one variable near the top of `:root` in `stylestack.theme.css`:

```css
--wallpaper: url('https://raw.githubusercontent.com/Dinakar-22/StyleStack/refs/heads/main/assets/rem-wallpaper.webp');
```

**Use your own image**

1. Put your image in the `assets/` folder of your repo and commit it.
2. Copy its raw link: `https://raw.githubusercontent.com/<user>/<repo>/main/assets/<file>`
3. Paste it inside `url('...')` in `--wallpaper`.

**Tips**

| Want | Do this |
| --- | --- |
| Smooth performance | Use the static `.jpg` line instead of the animated `.webp` (swap the commented line in `:root`) |
| Animated wallpaper | `.webp` or `.gif` both work. WebP is about 4x smaller, so prefer it |
| No wallpaper, just dark panels | Set `--style-preset: solid;` |
| Darker or brighter wallpaper | Change `--dim-top` and `--dim-bottom` (0 = no dim, 1 = black) |
| More or less glass blur | Change `--blur-amount` (default `8px`, `0px` looks flat) |

Image advice: around 1920x1080, JPG or WebP, ideally under 5 MB. Dark or medium images look best. Links to your own PC (`file://`) usually do not load in Discord, and Discord CDN links expire, so host the image on GitHub.

**Shrink a GIF to animated WebP** (needs ffmpeg):

```bash
ffmpeg -i input.gif -vf "fps=12" -c:v libwebp_anim -quality 60 -loop 0 output.webp
```

---

## Change the colors

### The quick way: four numbers

At the top of `:root` there are color knobs. Change the numbers and the whole theme follows (borders, glows, scrollbars, selection, badges, mentions, buttons).

```css
--hue:     198;   /* main accent color, 0-360 */
--hue-hi:  192;   /* lighter highlight on hover, keep near --hue */
--hue-2:   207;   /* second shade for gradients, keep near --hue */
--hue-bg:  255;   /* tint of the dark panels */
```

The file also has ready-made palettes in a comment inside `:root`. Copy one block over the four lines above:

| Palette | `--hue` | `--hue-hi` | `--hue-2` | `--hue-bg` |
| --- | --- | --- | --- | --- |
| Rem (blue, default) | 198 | 192 | 207 | 255 |
| Ram (pink and red) | 345 | 352 | 335 | 340 |
| Emilia (ice purple) | 262 | 252 | 272 | 260 |

Other examples: green `150`, orange `20`, red `0` for `--hue`. For `--hue-bg`: `255` is indigo, `220` is navy, `0` is neutral.

Only the Rem wallpaper ships with the theme. For Ram or Emilia, paste the URL of an image you like into `--wallpaper`. The Home button icon (`--dms-icon-svg-url`) can be swapped the same way.

### Fine control

All of these are in `:root`:

| What | Variables |
| --- | --- |
| Panel color and see-through amount | `--bg-1` to `--bg-4` (the last number is opacity, lower is more see-through) |
| Text colors | `--text-1` (brightest) to `--text-5` (dimmest) |
| Accent shades | `--blue-1` to `--blue-5`, `--accent-1` to `--accent-5` |
| Panel borders | `--border-light`, `--border`, `--border-hover` |
| Mention highlight | `--mention`, `--mention-hover` |
| Reply highlight | `--reply`, `--reply-hover` |
| Glow colors | `--glow-blue`, `--glow-hi` |
| Shape and spacing | `--gap`, `--radius-sm`, `--radius-md`, `--radius-lg`, `--border-thickness` |
| Server list home icon | `--dms-icon-svg-url` (must be an SVG link) |
| Active server ring speed | `--ring-speed` (seconds per turn, default `7s`) |
| Speaking glow speed | `--speak-speed` (seconds per pulse, default `1.4s`) |
| Handwritten header font | `--font-rem` (default Caveat) |
| Cursor | `--cursor-default` and `--cursor-pointer` (see below) |

### Cursor

The theme ships a crystal-style cursor drawn as an inline SVG, so no image files are needed. It uses one arrow for normal areas and one with a small sparkle over links and buttons. Text fields keep the normal I-beam.

To use your own cursor, replace the value of `--cursor-default-base` and `--cursor-pointer-base` with a `url(...)` to a 32x32 image. The two numbers after the `url()` are the click point (`4 3` is the tip of the arrow).

### Tags, badges and mentions

Server tags (PRX, GODA and so on) have no box, fill or glow. Bot tags (APP) are left as Discord draws them. The rule that flattens server tags is under **NO BOX ON SERVER TAGS** near the end of the file.

The rules under **MENTIONS & COUNTERS** control the rest:

- Inline @mentions get a blue box.
- Unread and mention counters get a blue fill and keep their pill shape.

Edit those rules to change the fill, border or glow, or delete the `.mention` rule to get plain mentions.

### Font

The theme uses Figtree from Google Fonts. To change it, replace the font name in the first `@import` line at the top, then replace `'Figtree'` in the body font rule and in `--font-primary` and `--font-display`.

Caveat (from Google Fonts) is used for the server name and channel headers. To use another font there, change `--font-rem` and the second `@import` line.

### Window buttons

The window controls are red, yellow and green dots inside a small pill at the top right, next to the inbox button. Their colors are fixed on purpose, so they stay recognizable whatever hue you pick.

---

## Performance

- The wallpaper is an animated WebP (about 6 MB, down from a 24 MB GIF).
- For weak GPUs, the easy way is `--style-preset: solid;`. It turns off the wallpaper and all blur.
- The manual way: find **LITE MODE** at the end of the animations section and remove the comment markers around it. It turns off all blur. Also switch `--wallpaper` to the static `.jpg`.
- Animations switch off automatically if your OS has "reduce motion" enabled.

---

## Troubleshooting

**A panel lost its glass style after a Discord update.**
Discord renames some internal classes in updates. Specific names are matched safely, but generic ones (container, wrapper, scroller, header) still carry a hash. Every class from one Discord module shares one hash:

1. Press `Ctrl+Shift+I` and click the broken element.
2. Read its new hash from the class name, for example `container_abc123`.
3. Find and Replace the old hash with the new one in `stylestack.theme.css`.

A list of the hashes in use is in the **MAINTENANCE** comment at the top of the file.

**The active server ring or the profile card does not show.**
These use class names that Discord changes now and then. Inspect the element with `Ctrl+Shift+I`, then update the matching selector in the **VISUAL POLISH** section.

**The speaking glow does not show.**
It only appears while someone is talking in a voice channel.

**The channel list touches or hides behind the bottom panel.**
The channel list leaves room for the user, voice and music panels using a value Discord provides (`--custom-app-panels-height`), plus `--gap`. Increase `--gap` for more space between them.

**The member list jumps when I hover it.**
That is `--collapsible-members`. Set it to `off` to keep the list at full width.

**The wallpaper does not show.**
Check that the image link opens in a browser, that the file is committed in the repo, and that `--style-preset` is not set to `solid`.

**A tag or badge looks different from the others.**
Inspect it with `Ctrl+Shift+I` and add its class name to the tag rule at the end of the file.

**My edits keep disappearing.**
Your client may be auto-updating the theme from `@updateUrl`. Remove that line from your local copy.

---

## Community

Questions, bug reports or screenshots of your setup are welcome in the Team SNC Discord: https://discord.gg/RjXukhYxcK

---

## Credits

- Created by **gvt22**, **Team SNC**.
- The idea came from **refact0r**'s themes, especially [Midnight](https://github.com/refact0r/midnight-discord). Special thanks for the inspiration. Midnight is MIT licensed, so please keep its notice if you reuse any of its code.
- Fonts: Figtree and Caveat, both loaded from Google Fonts and open source.
- Wallpaper: an animated Rem (Re:Zero) live wallpaper. The original artist is unknown. If you made it or know who did, please open an issue so they can be credited, or so it can be removed.

## License

MIT, copyright (c) 2026 gvt22 (Team SNC). See [LICENSE](LICENSE).
