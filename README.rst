==========
vgm-player
==========

A Linux launcher script for ``vgmplay``, the official and always up-to-date
VGM player (also some manpages and a new Makefile)

This is intended to be used in conjunction with the official source for
``vgmplay``, available at http://vgm.mdscene.net/forum/viewtopic.php?t=112,
with the goal of eventually being made part of that distribution.

Build
=====

1. Ensure ``zlib``'s development headers are available.
2. Acquire and extract the source of ``vgmplay`` - if it already has all the
files listed here, just build and play!
3. Place all files from here into ``vgmplay``'s directory; the only overwrite
should be the Makefile.
4. Build and install::
  $ make
  # make install

By default, ``vgmplay`` and ``vgm-player`` install into /usr/local; to alter
this, install with ``make PREFIX=/your/favorite/path install``.  If you know
your system lacks support for hardware emulation of FM chips or get a build
error to the effect of "sys/io.h missing", invoke ``make`` as
``CFLAGS=-DDISABLE_HW_SUPPORT make``.
5. Play music!

Usage
=====

`vgm-player [options] file`

Supported File Types
--------------------
* .VGM: Video Game Music
* .VGZ: Video Game Music (Compressed)
* .CMF: Creative Music File
* .DRO: DOSBox Raw OPL  

* .M3U: Playlist containing the above
* .ZIP, .7Z: Release packs from mdscene.net, Project2612, etc. containing a
set of supported music files and a playlist referencing them.  

Release pack support requires a method of extracting Zip/7z; this launcher
supports:

* ``bsdtar`` (from ``libarchive`` - both)
* ``p7zip`` (``7z{,a}`` - both, ``7zr`` - .7Z only)
* ``unzip`` (.ZIP only)

Options
-------



