vgm-player
==========

Linux launcher script to `vgmplay`, the official and always up-to-date player for VGM files. (also some mnapages and a new Makefile)

This is intended to be used in conjunction with the official source for `vgmplay`, available at [mdscene.net](http://vgm.mdscene.net/forum/viewtopic.php?t=112), with the goal of eventually being made part of that distribution.

Build
-----

1. Acquire and extract the source of `vgmplay` - if it already has all the files listed here, just build and play!
2. Place all files from here into `vgmplay`'s directory; the only overwrite should be the Makefile.
3. Build and install!
    $ make
    # make install

By default, `vgmplay` and `vgm-player` install into /usr/local; to alter this, install with `make PREFIX=/your/favorite/path install`.  If you know your system lacks support for hardware emulation of FM chips or get a build error to the effect of "sys/io.h missing", invoke `make` as `CFLAGS=-DDISABLE_HW_SUPPORT make`.
4. Play music!

Usage
-----

`vgm-player [options] file`
