
Debian
====================
This directory contains files used to package draupnird/draupnir-qt
for Debian-based Linux systems. If you compile draupnird/draupnir-qt yourself, there are some useful files here.

## draupnir: URI support ##


draupnir-qt.desktop  (Gnome / Open Desktop)
To install:

	sudo desktop-file-install draupnir-qt.desktop
	sudo update-desktop-database

If you build yourself, you will either need to modify the paths in
the .desktop file or copy or symlink your draupnir-qt binary to `/usr/bin`
and the `../../share/pixmaps/bitcoin128.png` to `/usr/share/pixmaps`

draupnir-qt.protocol (KDE)

