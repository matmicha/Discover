# Discover
Yet another Discord overlay for Linux written in Python using GTK3.

Discover-Overlay is a GTK3 overlay written in Python3. It can be configured to show who is currently talking on discord or it can be set to display text and images from a preconfigured channel. It is fully customisable and can be configured to display anywhere on the screen. We fully support X11 and wlroots based environments. We felt the need to make this project due to the shortcomings in support on Linux by the official discord client.

Considerably lighter on system resources and less hack-and-slash included than discord-overlay.

![Screenshot](https://trigg.github.io/Discover/overlay_on_deck.jpg)

For instructions on using Discord see our [User website](https://trigg.github.io/Discover/)

Got a question about development or a feature request? [Join our Discord!](https://discord.gg/jRKWMuDy5V) or open an [issue on GitHub](https://github.com/trigg/Discover/issues)

## Installing

### Flatpak via Flathub

Visit our [Flathub page](https://flathub.org/apps/details/io.github.trigg.discover_overlay) or install via commandline

```bash
flatpak install io.github.trigg.discover_overlay
```



### Stable
```bash
python3 -m pip install discover-overlay
```

### Latest Testing
```bash
git clone https://github.com/trigg/Discover.git
cd Discover
python3 -m pip install .
```

### Externally Packaged 

Note that while we list links to other locations to download, the version provided is unknown and often untested by us. Report bugs in these implementations to their respective project, not here.

##### Arch AUR

[Stable](https://aur.archlinux.org/packages/discover-overlay/)
[Latest](https://aur.archlinux.org/packages/discover-overlay-git/)

##### [Fedora](https://copr.fedorainfracloud.org/coprs/mavit/discover-overlay/)

```bash
sudo yum copr enable mavit/discover-overlay
sudo yum install discover-overlay
```

##### [Gentoo](https://gpo.zugaina.org/net-voip/discover-overlay)

```bash
sudo eselect repository enable guru
sudo emaint -r guru sync
sudo emerge net-voip/discover-overlay
```

## Dependencies

Most requirements should be handled by pip.

A compositor is strongly advised but there is a non-compositor mode optionally

It is advised to install python-gobject from your system's own package manager.

#### Debian/Ubuntu

`apt install python3-gi python3-gi-cairo`

with Wayland support

`apt install gtk-layer-shell`

#### Arch

`pacman -S python-gobject libappindicator-gtk3`

with Wayland support

`pacman -S gtk-layer-shell`


## Usage

Run `discover-overlay` if this fails it is most likely in `~/.local/bin/discover-overlay`

Comes with sane-enough default but has a configuration screen to tweak to your own use. Configuration can be reached by running `discover-overlay --configure`

Desktop shortcuts for both of these are added at install time.

### Debugging
If you are trying to debug on VS Code you are likely to get the following message:
```
/usr/bin/python3: No module named discover_overlay.__main__; 'discover_overlay' is a package and cannot be directly executed
```

To get around this, copy the main file created by discover-overlay with ``cp $(which discover-overlay) /path/to/Discover/discover_overlay/__main__.py``

### Translations

in all cases `XX` should be replaced with the language code, in case of English `en`, Spanish `es` so on as per [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)

#### Adding a new translation

First, find out what language code is required
Copy `discover_overlay/locales/base.pot` to `discover_overlay/locales/XX/LC_MESSAGES/default.po`

Change all lines starting with `msgstr` to contain the translated message in provided quotes, the line above should be a `msgid` which has the original word, sentence or fragment.

```
msgid "Please visit our discord"
msgstr "Ewch i'n Discord"
```

#### Compiling updates

This is NOT required if you are submitting a pull request for a new language to be added or to change a few translations. It should be done in a different commit afterwards.

`gettext` requires the `.po` files to be compiled into `.mo` before it can be used. Once a `.po` file is changed it can be compiled with 

`msgfmt -o discover_overlay/locales/XX/LC_MESSAGES/default.mo discover_overlay/locales/XX/LC_MESSAGES/default.po`

#### Incorrect translations and missing translations

We welcome pull requests and bug reports about missing or wrong translations, but don't have the resources to get it all right. Please be patient with us and alert us if any translations are wildly inaccurate.

#### Adding new phrases to the overlay app

Once you've used `_('something')` in code somewhere the original `base.pot` and all translations need updating to include the new phrase.

```
xgettext -d base --no-location -o discover_overlay/locales/base.pot discover_overlay/*.py
sed -i 's/charset=CHARSET/charset=UTF-8/g' discover_overlay/locales/base.pot
```

At this point the new msgid should be copied to each separate translation `.po` file and if possible a suitable translation be added.

## Why do you keep making Discord Overlays?

I feel like I shouldn't have to at all! Until we get an official one I might just create a new one every few months. Look forward to Rust/Vulkan version coming in a few months. /s

### Are you serious?

Generally, no.

