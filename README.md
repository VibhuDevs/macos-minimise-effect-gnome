# macOS Genie Minimize Effect for GNOME Shell 46

Brings the macOS magic lamp (genie) minimize animation to Ubuntu/GNOME — tuned to match the real Mac behavior as closely as possible.

![GNOME Shell](https://img.shields.io/badge/GNOME%20Shell-46-blue) ![Ubuntu](https://img.shields.io/badge/Ubuntu-22.04-orange) ![License](https://img.shields.io/badge/License-GPL--3.0-green)

## What's different from the original

The original [compiz-alike-magic-lamp-effect](https://github.com/hermes83/compiz-alike-magic-lamp-effect) is great but doesn't quite nail the Mac look. This fork tweaks:

- **No lateral wobble** — sides stay clean, just like macOS
- **Stronger funnel pinch** (`pow 1.8`) — tighter collapse toward the dock icon
- **Cubic ease-out** on minimize, ease-out on restore — matches Mac's feel
- **Snappier phase split** (`0.15`) — window collapses faster at the end
- **Fixed 250ms duration** — no more variable timing based on window size
- **6×35 tile mesh** — low horizontal, high vertical for a silky smooth curve

## Requirements

- Ubuntu 22.04 (or any distro running GNOME Shell 46 / mutter 46.x)
- X11 session (not Wayland)

## Installation

### 1. Clone the repo

```bash
git clone https://github.com/VibhuDevs/macos-minimise-effect-gnome.git
cd macos-minimise-effect-gnome
```

### 2. Compile the schema

```bash
cd schemas/
glib-compile-schemas .
cd ..
```

### 3. Install the schema system-wide

```bash
sudo cp schemas/org.gnome.shell.extensions.com.github.hermes83.compiz-alike-magic-lamp-effect.gschema.xml /usr/share/glib-2.0/schemas/
sudo glib-compile-schemas /usr/share/glib-2.0/schemas/
```

### 4. Symlink into GNOME extensions folder

```bash
mkdir -p ~/.local/share/gnome-shell/extensions/
ln -s $(pwd) ~/.local/share/gnome-shell/extensions/compiz-alike-magic-lamp-effect@hermes83.github.com
```

### 5. Apply the settings

```bash
gsettings set org.gnome.shell.extensions.com.github.hermes83.compiz-alike-magic-lamp-effect duration 250
gsettings set org.gnome.shell.extensions.com.github.hermes83.compiz-alike-magic-lamp-effect x-tiles 6
gsettings set org.gnome.shell.extensions.com.github.hermes83.compiz-alike-magic-lamp-effect y-tiles 35
gsettings set org.gnome.shell.extensions.com.github.hermes83.compiz-alike-magic-lamp-effect effect default
```

### 6. Reload GNOME Shell

```bash
busctl --user call org.gnome.Shell /org/gnome/Shell org.gnome.Shell Eval s 'Meta.restart("Restarting…")'
```

### 7. Enable the extension

```bash
gnome-extensions enable compiz-alike-magic-lamp-effect@hermes83.github.com
```

Minimize any window — you should see the genie effect.

## Uninstall

```bash
gnome-extensions disable compiz-alike-magic-lamp-effect@hermes83.github.com
rm ~/.local/share/gnome-shell/extensions/compiz-alike-magic-lamp-effect@hermes83.github.com
sudo rm /usr/share/glib-2.0/schemas/org.gnome.shell.extensions.com.github.hermes83.compiz-alike-magic-lamp-effect.gschema.xml
sudo glib-compile-schemas /usr/share/glib-2.0/schemas/
```

## Credits

Based on the original work by [hermes83](https://github.com/hermes83/compiz-alike-magic-lamp-effect). This fork tunes the animation parameters to match macOS behavior.
