## libao

A cross-platform audio library.

libao is free software; you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation; either version 2, or (at your option) any later version.

libao is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details.

### Overview

Libao is a cross-platform audio library that allows programs to output audio using a simple API on a wide variety of platforms. It currently supports:

   * Null output
   * WAV files
   * OSS (Open Sound System)
   * ESD (ESounD or Enlightened Sound Daemon)
   * ALSA (Advanced Linux Sound Architecture)
   * PulseAudio (next generation GNOME sound server)
   * AIX
   * Solaris (untested)
   * IRIX (untested)

### History

Libao began life as cross-platform audio library inside of `ac3dec`, an AC3 decoder by Aaron Holtzman that is part of the LiViD project. When ogg123 (part of the command line vorbis tools) needed a way to play audio on multiple operating systems, someone on the vorbis-dev mailing list suggested the libao library as a possible way to add cross-platform 
support to ogg123. Stan Seibert downloaded the libao library, severely hacked it up in order to make the build process simpler and support multiple live-playback devices. (The original code allowed one live playback driver, the wav driver, and a null driver to be compiled into the library.) Jack Moffitt got it supporting dynamically loaded plugins 
so that binary versions of libao could be provided. The API was revised for version 0.8.0.

### Workarounds

The OSS emulation in ALSA deviates from the OSS spec by not returning immediately from an open() call if the OSS device is already in use. Instead, it makes the application wait until the device is available. This is not desirable during the autodetection phase of libao, so a workaround has been included in the source. Since the workaround itself violates the OSS spec and causes other problems on some platforms, it is only enabled when ALSA is detected. The workaround can be turned on or off by passing the `--enable-broken-oss` or
`--disable-broken-oss` flag to the configure script.

### Todo

I think these are the next steps:

- make the plugins dynamically loadable (done)
- make a ao-config liek gtk-config instead of ao_libs.inc (done)
- extend the configuration files to allow default options for
  each driver
- Sample rate conversion on the fly to support sound cards that have few
  sample rate options (like the i810 audio device, which only does 48000)
- Actually test the IRIX plugin.  :)
- Test the macosx plugin