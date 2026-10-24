# dotfiles · hyprland, gruvbox, a little retro

My Hyprland setup on Fedora 44. Gruvbox colours with a cream accent, square windows,
a thin text-only bar, and a few small tools of my own: a full-screen "paper" wallpaper
screen, an album-art card, clipboard history and on/off keys for most things.

Light on purpose: no heavy shell or widget framework. It's Waybar, rofi, mako and kitty,
plus short bash and Python scripts.

## What's in it

| Part | Tool | Notes |
|---|---|---|
| Compositor | Hyprland 0.56 (Lua config) | Tiling by default, 5 / 10 px gaps, cream border on the focused window, short animations, blur |
| Bar | Waybar | Thin and text only: `W: ( 1 2 3 4 5 )` · window title · clock · `♪ song` · cpu · mem · vol · net · bat |
| Launcher and menus | rofi | Omarchy-style box with a `>` prompt, also used for the power, clipboard and keybind menus |
| Terminal | kitty | Gruvbox, 85% opaque over the blur |
| Notifications | mako | Borderless dark box with centred text, plus a volume pop-up up to 150% |
| Wallpaper | swaybg + `wallpaper-ui` | Full-screen paper screen with thumbnails, mount / brightness / wash / blur |
| Lock and idle | hyprlock, hypridle | Dim at 5 min, lock at 10, sleep at 30 |
| Clipboard | cliphist | Full history in rofi, newest first |
| Equalizer | EasyEffects | Themed with the KDE colour scheme below |
| GTK / Qt apps | own Gruvbox CSS + KDE colour scheme | Applied only in Hyprland; GNOME keeps its own theme |
| Terminal toys | fastfetch, cava, btop | Pixel-art fastfetch logo drawn 1:1, cream gradient in cava, `gruvbox-cream` btop theme |

## Keys

`Super+K` shows every keybind, searchable. The ones you'll use most:

| Keys | Does |
|---|---|
| `Super+Enter` · `Super+Space` | terminal · app launcher |
| `Super+W` / `Super+Q` | close window |
| `Super+T` · `Super+Alt+T` | float this window · float the whole workspace (floating windows have no border) |
| `Super+F` · `Super+L` | full screen · switch dwindle ↔ master |
| `Super+1…0` · `Super+Shift+1…0` | go to workspace · move window there |
| `Super+Arrows` · `Super+Shift+Arrows` | focus · swap |
| `Super+Ctrl+Space` | wallpaper screen |
| `Super+Ctrl+V` | clipboard history |
| `Super+Ctrl+M` · `Super+Ctrl+Alt+D` · `Super+Ctrl+Alt+T` | album-art card · calendar · clock |
| `Super+Ctrl+E` | equalizer |
| `Super+Escape` · `Super+Ctrl+L` | power menu · lock |
| `Print` · `Shift+Print` · `Super+Print` | region screenshot · screen screenshot · colour picker |

**On/off keys**

| Keys | Toggles |
|---|---|
| `Super+Shift+Space` | bar |
| `Super+Ctrl+Alt+Space` (or right-click the clock) | bar background |
| `Super+Shift+Backspace` | gaps |
| `Super+Ctrl+Alt+A` | animations |
| `Super+Ctrl+I` | lock on idle |
| `Super+Ctrl+,` | do not disturb |

## Scripts (`~/.local/bin`)

| Script | What it does |
|---|---|
| `wallpaper-ui` | Full-screen wallpaper screen in kitty (Python, stdlib only). `--selftest` checks it |
| `wallpaper` | Applies the chosen wallpaper and its settings (`--restore` runs at login) |
| `float-workspace` | Switches the current workspace between tiling and floating |
| `nowplaying` | Album-art card for whatever `playerctl` sees |
| `clipboard` | cliphist history in rofi |
| `volume` | Volume up to 150% with a mako pop-up |
| `powermenu` · `keybinds` | Power menu · searchable keybind list |
| `waybar-bg` | Bar background on/off |
| `gtk-theme-switch` | Gruvbox GTK theme and icons in Hyprland, the normal theme back in GNOME |

## Install

Fedora 44. Hyprland comes from the [lionheartp/Hyprland](https://copr.fedorainfracloud.org/coprs/lionheartp/Hyprland) COPR, which the Hyprland wiki recommends for Fedora.

```bash
sudo dnf copr enable lionheartp/Hyprland
sudo dnf install hyprland hyprlock hypridle hyprpolkitagent cliphist \
  waybar rofi kitty mako swaybg ImageMagick \
  grim slurp wl-clipboard brightnessctl pamixer playerctl \
  easyeffects lsp-plugins-lv2 cava btop fastfetch \
  jetbrains-mono-fonts-all papirus-icon-theme
```

Tan folder icons: get [papirus-folders](https://github.com/PapirusDevelopmentTeam/papirus-folders) and run
`papirus-folders -C paleorange --theme Papirus-Dark`.

The dotfiles are a bare git repo whose work tree is `$HOME`. Files stay where they belong, with no symlinks:

```bash
git clone --bare https://github.com/mint2222222/dotfiles ~/.dotfiles
alias dot='git --git-dir=$HOME/.dotfiles --work-tree=$HOME'
dot config status.showUntrackedFiles no
dot checkout            # move any existing configs out of the way first if it refuses
```

Wallpapers are read from `~/Pictures/gruvbox`. They aren't in the repo, so bring your own.

## Notes

- The fastfetch logo (`.config/fastfetch/logo.png`) is pixel art sized to exactly 36×16 kitty cells at
  `font_size 11`, so it draws 1:1. Change the font size and it gets rescaled.
- Monitors are set up for my laptop (eDP-1, 60 Hz) plus a Samsung on HDMI at 120 Hz. Edit
  the `hl.monitor` blocks at the top of `.config/hypr/hyprland.lua` for yours.
- Keybind layout is adapted from [Omarchy](https://github.com/basecamp/omarchy). The retro bits are inspired by
  Dylan Araps' rices.
