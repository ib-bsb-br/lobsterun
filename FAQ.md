### Q: What platforms does gvrun support?

[](https://github.com/ssokolow/gvrun/wiki/Potentially-Asked-Questions#q-what-platforms-does-gvrun-support)

**A:** Currently, it's only tested on the current version of Lubuntu Linux, but it should theoretically work on any Linux or MacOS X machine which can provide GTK+ 3.x, libgee, and Vala.

Windows is not explicitly _un_ supported, but there are still TODOs that need to be cleared out regarding Win32 compatibility.

### Q: How do I change which program gvrun uses to open a file?

[](https://github.com/ssokolow/gvrun/wiki/Potentially-Asked-Questions#q-how-do-i-change-which-program-gvrun-uses-to-open-a-file)

**A:** The first thing you need to do is figure out which backend gvrun is using to open your file. It will use the following backends, preferring the first one that is available and applies:

1.   Is it an executable command or path? Use `$SHELL -c <your input>`
2.   Is it a URL or an existing path? Use the first available choice from: 1. `xdg-open` 1. `mimeopen` 1. `start` (Windows) 1. `open` (MacOS X)
3.   Fall back to feeding it to `$SHELL` in case it's a shell built-in or script snippet.

* * *

*   `xdg-open`, `start`, and `open` use your desktop's file associations system.
*   `mimeopen` can be reconfigured with `mimeopen -d <filename to re-associate>`.

### Q: I'm not running a desktop environment like KDE or GNOME. Where is `xdg-open` getting its info?

[](https://github.com/ssokolow/gvrun/wiki/Potentially-Asked-Questions#q-im-not-running-a-desktop-environment-like-kde-or-gnome-where-is-xdg-open-getting-its-info)

When not using a desktop-specific mechanism to look up applications, `xdg-open` falls back to this set of resolvers:

1.   Identify the mimetype

*   If it's a URL, use `x-scheme-handler/SCHEME` where `SCHEME` is "http", "ftp", etc..
*   If it's a path, ask `xdg-mime query filetype <path>`

1.   Use `xdg-mime query default <mimetype>` to look up the application

*   Edit `~/.local/share/applications/mimeapps.list` to control this. (See [mime-actions-spec](http://www.freedesktop.org/wiki/Specifications/mime-actions-spec) for details.)
*   Use xdg-utils to [register new mimetypes](http://stackoverflow.com/questions/30931/register-file-extensions-mime-types-in-linux).
*   [Write a .desktop file](http://library.gnome.org/admin/system-admin-guide/stable/menustructure-desktopentry.html.en) to register a new application.

1.   If `xdg-mime` returns no result...

*   If the value is a path, fall back to `mimeopen`.
*   If the value is a URL, check `$BROWSER` and fall back to an internal list.
