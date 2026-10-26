# About this fork

This is a personal fork of [WayfireWM/wf-shell](https://github.com/WayfireWM/wf-shell). It only changes `wf-dock`; everything else is upstream as it is. The fork is not meant for upstream, so please don't send these changes there.

The `dock-launchers` branch is the default branch and holds all changes, rebased onto upstream release tags (currently v0.11.0). `master` tracks upstream unchanged.

## What is different

- **Pinned launchers** left of the running apps. List them in the `[dock]` section of `~/.config/wf-shell.ini`: `launchers = firefox org.gnome.Nautilus foot notes`. Entries are desktop file ids, absolute paths to `.desktop` files, or custom launchers defined with `launcher_cmd_<name>`, `launcher_icon_<name>` and `launcher_label_<name>`.
- **Launch bounce:** a launcher's icon hops once when it starts an app. The animation is `launch-bounce` in `data/css/default.css` and can be overridden from your own CSS.
- **Places button** left of the launchers. It pops up a list of folders (`places`, `places_file_manager`, `places_icon`, `places_icon_size`, `places_label`), and a middle click opens the first one.
- **Icons:** running apps prefer the `.desktop` icon, more window icons are resolved, and `~` is expanded in icon paths.
- **Config hot-reload** keeps working after a reload.
- `examples/dock-indicator.css` draws an active-app line under the icons.

All options are declared in `metadata/dock.xml`, so WCM keeps them when it saves `wf-shell.ini`. See `wf-shell.ini.example` for the `[dock]` section.

## Building

`pkg/PKGBUILD` builds an Arch package, `wf-shell-mk`, from the working tree it lives in. It replaces the `wf-shell` package.

```
cd pkg
makepkg -f
sudo pacman -U wf-shell-mk-*.pkg.tar.*
```

It needs `glib2-devel`, `meson` and `wayland-protocols`. If `makepkg` fails with an unknown meson option, delete `pkg/src/build` and run it again.

pacman never updates `wf-shell-mk`, so a new upstream release means a manual rebase and rebuild.

## Keeping up with upstream

```
git fetch upstream --tags
git checkout dock-launchers
git rebase v0.12.0          # the new tag
git push --force-with-lease origin dock-launchers
```
