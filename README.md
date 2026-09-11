# puush for Linux

A single bash script that uploads screenshots and files to
[puush.me](https://puush.me) and copies the link. Made for GNOME on Wayland
(Ubuntu 26.04); X11 is not supported.

## Install

```sh
git clone https://github.com/lostallmymoney/Puush-Linux-CLI
cd Puush-Linux-CLI
./puush --install
```

This copies puush to `~/.local/bin` (no root needed), then offers to install
the optional `chafa` and `wl-clipboard` if they are missing.

The first run logs you in with your puush.me email and password (or an API key
from <https://puush.me/account/settings>). Only the API key is saved, in
`~/.config/puush/puush.conf`, readable by you alone.

## Usage

```
puush -a            area, window or screen, picked in GNOME's screenshot tool
puush -d            whole desktop at once
puush [-f] FILE...  upload files
puush -z            choose files to upload in a dialog
puush -h [N]        list your last N uploads (default 5, max 10)
puush -x [LINK|N]   delete uploads by link or number (of your last 5), or pick
puush -l            log in again (email + password, or API key)
puush --logout      forget your API key (other settings are kept)
puush -o md5 false  stop sending an MD5 checksum with uploads (on by default)
puush -o thumbs 0   hide thumbnails in -h and -x (same as false)
puush -o thumbs 50  thumbnail size in percent, 6-100 (default 16)
puush -u            uninstall, including settings, API key and cache
```

Links are printed in a terminal, copied to the clipboard and shown in a
notification. Screenshots are deleted once uploaded, and kept if the upload
fails.

Uploads include an MD5 checksum so puush.me can reject a corrupted transfer; a
failed upload is retried once automatically.

`-h` lists your last 5 uploads (up to 10 with `-h 10`) with their name, upload
date, size and MD5, each with its puush.me thumbnail drawn in the terminal by
`chafa` (without it, the list is text only). Thumbnails, sizes and MD5s are
cached in `~/.cache/puush`, up to 10 MiB. `-x` picks uploads to delete from the
same list, and `-x LINK` deletes any upload, however old.

## Keyboard shortcuts

In Settings → Keyboard → View and Customize Shortcuts → Custom Shortcuts, add
`/home/<you>/.local/bin/puush -a` (and `-d`, `-z` if you like) with shortcuts of
your choice, e.g. <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>1</kbd> for `-a`.

## Dependencies

- `curl`: uploads
- `gdbus` + xdg-desktop-portal-gnome: screenshots (preinstalled)
- `zenity`: the file dialog (preinstalled)
- `wl-clipboard`: copying the link (optional)
- `chafa`: thumbnails in `-h` and `-x` (optional)
- `libnotify-bin`: notifications (optional, preinstalled)

## License

LGPL-2.1-or-later. A rewrite of [jacklul/puush-linux](https://github.com/jacklul/puush-linux),
itself a rewrite of [sunmockyang/puush-linux](https://github.com/sunmockyang/puush-linux).
