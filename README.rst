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
   files listed here, just build and play.
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


Options
-------

--help        Displays usage information and exits

--version     Displays ``vgmplay`` version, VGM format version, and exits

Output
~~~~~~

``vgmplay`` only supports OSS; ``vgm-player`` will attempt to detect and use
the proper OSS wrapper for your system in the following order and criteria:

1. PULSE_SERVER is set: ``padsp`` wrapper for PulseAudio used and stream sent
   to $PULSE_SERVER.
2. ``/dev/dsp`` exists: Implies ALSA's OSS emulation modules, ``ossp``, or
   OSS running - uses plain OSS output
3. PulseAudio daemon running: ``padsp`` wrapper for PulseAudio used
4. ``aoss`` present: ``aoss`` wrapper for ALSA used
5. None of the above true and --log not specified: returns error

To force a given output type, use one of the following options; these options
are exclusive:

-a, --alsa    ``aoss`` wrapper for ALSA.

-o, --oss     ``oss`` output, for use with actual OSS, ALSA's OSS
              emulation modules, or the ``ossp`` emulation daemon.

-p, --pulse   ``padsp`` wrapper for PulseAudio; respects the PULSE_SERVER
              environment variable if set.  Sets stream role to music.

--pulse-server=server
              ``padsp`` wrapper for PulseAudio; forces output to specified
              PulseAudio server.  Sets stream role to music.

-l, --log     Outputs to .WAV in current directory.

--log-to=path
              Outputs to .WAV in specified path.

Configuration
~~~~~~~~~~~~~

``vgmplay`` expects ``VGMPlay.ini`` in its working directory; ``vgm-player``
will look for a custom ``VGMPlay.ini`` in the following order and use the
first found:
``$XDG_CONFIG_HOME/vgm-player/VGMPlay.ini``,
``$HOME/.config/vgm-player/VGMPlay.ini``,
``$XDG_CONFIG_DIRS/vgm-player/VGMPlay.ini``,
``/etc/xdg/vgm-player/VGMPlay.ini``.

--config=configfile
              Uses specified configuration file; this does not have to be
              named ``VGMPlay.ini``

--binary=binary
              Uses specified ``vgmplay`` binary

--override=options
              Overrides options from the [General] section of ``VGMPlay.ini``.
              The list should be quoted and comma-separated, e.g.
              ``--override="SampleRate = 22050,MaxLoops = 0x03"``

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
