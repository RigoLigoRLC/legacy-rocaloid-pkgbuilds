# The Legacy Rocaloid Project PKGBUILD Center

## What is this?

[Rocaloid](https://github.com/Rocaloid), is a discontinued free (libre) and open source singing voice synthesis system, contains a third-gen-iteration Cyber Voice Engine synthesis engine and various toolchains built around it. The technologies behind the project has evolved into a patented technology, Low Level Speech Model (now [libllsm2](https://github.com/Sleepwalking/libllsm2)), used in popular UTAU resampler "Moresampler" (4th-gen-iteration) and eventually made it into a successful commercial product, [Synthesizer V](https://dreamtonics.com).

## Why would you do this?

Rocaloid has been discontinued after [Kanru Hua's quit](https://twitter.com/khuasw/status/645628170826289152) and some [patent issues (Chinese page)](https://www.zhihu.com/question/24747703/answer/59832952) around the technologies behind the HNM used in Rocaloid. I consider this as a broken open source dream, a specimen sealed in the past. However, as long as the Rocaloid source code is still available, then we can still tackle around it and make use of it if possible. This repository is for simplifying the steps required to build Rocaloid, for anyone coming later.

These packages are not submitted to Arch Linux User Repository for obvious reasons: they are no longer maintained.

## Requirements

- Arch Linux
- package `base-devel cmake gcc`

## Build Steps

After cloning this repository, you'll have 6 directories in it, each containing a PKGBUILD and associated files. You'll need to build and install them in a specific order:

- `rocaloid-rutil2`
- `rocaloid-rfnl`
- `rocaloid-cvedsp2`
- `rocaloid-cvesvp`
- `rocaloid-ruce`
- `rocaloid-voicetools`

`rocaloid-voicetools` is an optional package, as it is a voicebank toolchain. If you're going to build a RUCE voicebank like [Cyan](https://github.com/Rocaloid/Cyan-RUCE-Source) on your own then you'll need this package (and `sox`, which is available directly in Arch Linux repository).

All of the packages will install corresponding libraries, executables, headers and manpages (Yes Kanru Did write a manpage for voicetools, oh god) into your `/usr/bin`, `/usr/lib`, `/usr/include` and `/usr/share/man`.

Some code have been patched so that dependencies installed into your computer will be linked against, instead of the versions included in various libraries. This is due to a time saving consideration and also a library consistency consideration. `rocaloid-voicetools` ships with a `fixes.patch` that fixes some issues in the code preventing the compilation.

After building RUCE it will produce `RUCE_CLI`, `libRUCE_s.a` and `libRUCE.so`, corresponding to CLI version, static library and dynamic library versions of RUCE. In a typical UTAU setup, what you may need is only `RUCE_CLI`. You can copy it out manually in `rocaloid-ruce/src/RUCE/build` or from `/usr/bin`.

At last, happy tinkering with this old legacy Rocaloid project! The previous days' community will be very happy if someone decides to create another libre voice synthesis sytem. Thank you!
