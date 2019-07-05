
Debian
====================
This directory contains files used to package tragocoind/tragocoin-qt
for Debian-based Linux systems. If you compile tragocoind/tragocoin-qt yourself, there are some useful files here.

## tragocoin: URI support ##


tragocoin-qt.desktop  (Gnome / Open Desktop)
To install:

	sudo desktop-file-install tragocoin-qt.desktop
	sudo update-desktop-database

If you build yourself, you will either need to modify the paths in
the .desktop file or copy or symlink your tragocoin-qt binary to `/usr/bin`
and the `../../share/pixmaps/tragocoin128.png` to `/usr/share/pixmaps`

tragocoin-qt.protocol (KDE)

