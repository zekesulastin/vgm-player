==========
vgm-player
==========

A Linux launcher script for ``vgmplay``, the official and always up-to-date
VGM player

This is intended to be used alongside the official source for
``vgmplay``, available at http://vgm.mdscene.net/forum/viewtopic.php?t=112.

Installation
============

Just put this script somewhere convenient and run - as long as the ``vgmplay``
binary is in your $PATH or $(pwd), it should automatically detect and use it;
you can also specify a specific binary in command-line options.

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
2. ``/dev/dsp`` exists: Implies ALSA's OSS emulation modules, OSSProxy, or
   OSS running - uses plain OSS output
3. PulseAudio daemon running: ``padsp`` wrapper for PulseAudio used
4. ``aoss`` present: ``aoss`` wrapper for ALSA used
5. None of the above true and --log not specified: returns error

To force a given output type, use one of the following options; these options
are exclusive:

-a, --alsa    ``aoss`` wrapper for ALSA.

-o, --oss     ``oss`` output, for use with actual OSS, ALSA's OSS
              emulation modules, or the OSSProxy.

-p, --pulse   ``padsp`` wrapper for PulseAudio; respects the PULSE_SERVER
              environment variable if set.

-s server, --pulse-server=server
              ``padsp`` wrapper for PulseAudio; forces output to specified
              PulseAudio server.

-l, --log     Outputs to .WAV in current directory.

--log-path=path
              Outputs to .WAV in specified path.

Configuration
~~~~~~~~~~~~~

``vgmplay`` expects ``vgmplay.ini`` in its working directory; ``vgm-player``
will look for a custom ``vgmplay.ini`` in the following order and use the
first found:
``$(pwd)/vgmplay.ini``
``$XDG_CONFIG_HOME/vgmplay/vgmplay.ini``,
``$HOME/.config/vgmplay/vgmplay.ini``,
``$XDG_CONFIG_DIRS/vgmplay/vgmplay.ini``,
``/etc/xdg/vgmplay/vgmplay.ini``,
``/usr/share/vgmplay/vgmplay.ini``.

--config=configfile
              Uses specified configuration file; this does not have to be
              named ``vgmplay.ini``

--binary=binary
              Uses specified ``vgmplay`` binary

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
