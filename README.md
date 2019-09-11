![Icon](http://wakaba.c3.cx/images/unarchiver_icon.png)

`unar` is the BEST solution for archives containing non UTF-8 encoding file names.

Here is unar mirror for maintenance to build on some distros that had no maintained packages.

It was unar1.10.1 from [upstream](https://unarchiver.c3.cx/commandline).


# `unar`, The Unarchiver unarchiving engine

The Unarchiver is an Objective-C application for uncompressing archive files.

* The unarchiving engine is multi-platform, and command-line tools exist for Linux, Windows and other OSes.
* Uses character set autodetection code from Mozilla to auto-detect the encoding of the filenames in the archives.
* Supports split archives for certain formats, like RAR.
* Version 2.0 uses an archive-handling library built largely from scratch in Objective-C, which makes adding support for new formats and algorithms very easy.
* Uses [libxad](https://github.com/ashang/libxad) for older and more obscure formats. This is an old Amiga library for handling unpacking of archives.

## Build on Linux

### third-party libraries that the XADMaster library depends on
- GNUstep
- zlib
- libbzip2
- OpenSSL
- ICU

### Install third-party libraries
- Debian/Ubuntu
```
apt install build-essential libgnustep-base-dev libz-dev libbz2-dev libssl-dev libicu-dev
```

- Arch
```
pacman -S gnustep-base gnustep-make openssl icu zlib
```

- Gentoo

unar had been in official repo, as `app-arch/unar-1.10.1`

```
emerge unar
```

### Build XADMaster
```shell
cd XADMaster
make -f Makefile.linux
```

## Build on macOS

### Build on macOS from src
### Build on macOS via brew
```
$ brew install unar
...
==> Using the sandbox
==> Downloading https://wakaba.c3.cx/releases/TheUnarchiver/unar1.10.1_src.zip
######################################################################## 100.0%
==> xcodebuild -project ./XADMaster/XADMaster.xcodeproj -alltargets -configuration Release clean
Last 15 lines from /path/to/Library/Logs/Homebrew/unar/01.xcodebuild:
2017-05-02 23:19:18 +0800

xcodebuild
-project
./XADMaster/XADMaster.xcodeproj
-alltargets
-configuration
Release
clean

xcode-select: error: tool 'xcodebuild' requires Xcode, but active developer directory '/Library/Developer/CommandLineTools' is a command line tools instance

READ THIS: http://docs.brew.sh/Troubleshooting.html

```



## Supports formats

The table was from the [original google code wiki page](http://code.google.com/p/theunarchiver/wiki/SupportedFormats)

### Supported popular formats

| Format      | Support level   | Notes                                                                                             |
| -------     | :-------------- | :------                                                                                           |
| Zip         | Full            |                                                                                                   |
| RAR         | Full            | Including encryption and multiple volumes. Can also extract .EXE self-extracting files using RAR. |
| 7z          | No encryption   | Most compression methods are supported, but no encryption. Also supports Unix extensions.         |
| Tar         | Full            |                                                                                                   |
| Gzip        | Full            |                                                                                                   |
| Bzip2       | Full            |                                                                                                   |
| LZMA, XZ    | Full            | Both the old "LZMA-alone" format, usually named .lzma, and the new .xz format.                    |
| CAB         | Full            |                                                                                                   |
| MSI         | Full            | You can use The Unarchiver to extract internal data from DOC and PPT files, and others.           |
| NSIS        | Extensive       | Supports many different versions, starting from version 1.1o                                      |
| EXE         | Some            | Many kinds of .exe self-extracting formats are supported.                                         |
| ISO         | Full            | ISO 9660 CDROM filesystem images, and also .bin raw images.                                       |
| Split files | Basic           | Can join files named .001, .002 that do not use any extra wrapper format.                         |


**Zip**
- Full support for the normal zip format, with additional support for AES encryption, Zip64 extensions for large files, Mac OS extensions of many different kinds, and several unusual compression methods (Deflate64, Bzip, LZMA, PPMd). Can also extract .EXE self-extracting files using Zip.

### Supported old formats

| Format        | Support level   | Was popular on      | Notes                                                                                                                  |
| -------       | :-------------- | :---------------    | :------                                                                                                                |
| StuffIt       | No encryption   | Mac OS              | Can unpack all files I've been able to locate.                                                                         |
| StuffIt X     | Partial         | Mac OS              | Can unpack many files, some more obscure features are still unsupported. JPEG compression is also unsupported.         |
| DiskDoubler   | Almost full     | Mac OS              | All compression algorithms are implemented, but a few rare ones are untested.                                          |
| Compact Pro   | No encryption   | Mac OS              |                                                                                                                        |
| PackIt        | Full            | Mac OS              |                                                                                                                        |
| Cpio          | Full            | Unix                |                                                                                                                        |
| Compress (.Z) | Full            | Unix                |                                                                                                                        |
| ARJ           | No multi-part   | DOS                 |                                                                                                                        |
| ARC, PAK      | Full            | DOS                 | Full support for all algorithms, including proprietary ones from PAK. Encryption only works in command-line utilities. |
| Ace           | Only old files  | DOS                 | No support for Ace 2.0 and up (WinAce).                                                                                |
| Zoo           | Full            | DOS                 |                                                                                                                        |
| LZH           | Full            | DOS, Amiga (as LhA) |                                                                                                                        |
| ADF           | FFS             | Amiga (emulated)    | Can extract files from Amiga disk images using the regular FFS file system.                                            |
| DMS           | FFS             | Amiga               | Can extract files from compressed Amiga disk images using the regular FFS file system.                                 |
| LZX           | Full            | Amiga               |                                                                                                                        |
| PowerPacker   | Full            | Amiga               |                                                                                                                        |
| LBR           | Full            | CP/M, DOS           |                                                                                                                        |
| Squeeze       | Full            | CP/M, DOS           |                                                                                                                        |
| Crunch        | Full            | CP/M                |                                                                                                                        |
| ...           |                 |                     | Many other old formats are also supported through libxad                                                               |

### Supported unusual formats

| Format   | Support level   | Notes                                                                                                                                              |
| -------  | :-------------- | :------                                                                                                                                            |
| XAR      | Full            | Suggested replacement for Tar on Unix. Used in some newer .pkg files on Mac OS X.                                                                  |
| RPM      | Full            | Linux package format.                                                                                                                              |
| ALZip    | No encryption   | Archive format which is mainly popular in South Korea. Support for all known compression methods, including Bzip2, Deflate and obfuscated Deflate. |
| NSA, SAR | Partial         | Game data file. Can unpack all files I've found. If you have ones that do not unpack, please post an issue.                                        |
| NDS      | Full            | Nintendo DS ROM image, which can contain a file system.                                                                                            |
| Zipx     | Full            | WinZip extended Zip files                                                                                                                          |

### Unsupported formats, for which support would be good to have

| Format            | Notes                                                                                                                                                      |
| -------           | :------                                                                                                                                                    |
| Deb               | `Deb` package format. Use `ar x` to operate.                                                                                                               |
| Ace 2.0           | Proprietary, requires reverse engineering.                                                                                                                 |
| DMG               | Mac OS X disk images with a HFS+ filesystem.                                                                                                               |
| PAR               | Not an archive format, but recovery records for missing archive parts.                                                                                     |
| SHK               | Apple II archive format.                                                                                                                                   |
| Amiga compressors | The Amiga had a lot of different single-file compressors. Support for more of these would be useful. libxfd supports many of them, but is mostly 68k only. |
