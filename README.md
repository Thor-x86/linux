# The Scissors Kernel ✂️

A cutting-edge, full-featured custom kernel for [WSL2][about-wsl2]. It uses
[linux-rolling-stable][branch-rolling-stable] branch, equivalent as Arch Linux
kernel. Designed to enable research & development on WSL2 which requires USB
devices. More than that, scissors kernel allows us to use officially
non-supported filesystem at Linux side including ExFAT, NTFS, and F2FS!

## Why bother use custom kernel for WSL2?

Besides of latest (but stable) kernel version, there are things that
didn't included in the official kernel:

+ NTFS-3G
+ ExFAT
+ F2FS
+ Android container support (Still in test with Waydroid)
+ USB Printer
+ USB Camera Support (including Microsoft Kinect, PlayStation Eye, and UVC-compliant)
+ USB Audio & MIDI
+ USB SDCard Adapter (including Realtek)
+ USB Ethernet Support (including RTL815x-based adapter, Android and iPhone USB Tether)
+ USB Modem (CDC MBIM, EEC, and NCM compliant support)
+ Ethernet Teaming (round-robin, load-balance, active backup)
+ ALSA OSS Emulation support
+ USB GPS Support (Bare UART, Garmin, and Navman only)
+ USB4 Support (x86_64 only)
+ Apple iSight support (Read http://bersace03.free.fr/ift first)

## How to use custom kernel?

First, download ready-to-use kernel binary

- [WSL2 Scissors for x86_64](https://raw.githubusercontent.com/Thor-x86/linux/linux-wsl2-scissors/vmlinuz-wsl2-scissors-x86_64)
- [WSL2 Scissors for ARM64](https://raw.githubusercontent.com/Thor-x86/linux/linux-wsl2-scissors/vmlinuz-wsl2-scissors-arm64)

Then put this into Explorer address bar

```
%USERPROFILE%\.wslconfig
```

You'll be prompted open with what, choose Notepad. Once opened, add below
to the end of the file via notepad.

```
[wsl2]
kernel=C:\\<path to vmlinuz file>
```

Don't forget to change ```<path to vmlinuz file>```, notice we're using double
backslash (\\\\) instead of single backlash (\\).

## Issue Report

For now, we can use [issue tab](issues) for a while. I planned to make mailing
list in case of being too popular for some reasons. So please be familiar with
mailing list just like other Linux kernel repo.

Please be aware that you should not post security issue publicly because you'll
threaten other user's security. If you found one, please mail foss@athaariq.my.id
or report it to [Microsoft's security bug page][security-bug].

## Contribution

The [pull request tab](pulls) is available for everyone. However, if the pull
request is not about WSL2, please [submit to the upstream][submit-patch] instead.

## Build Requirements

### With APT

- build-essential
- flex
- bison
- dwarves
- libssl-dev
- libelf-dev

### With RPM

- bsdutils
- coreutils
- diffutils
- findutils
- grep
- gzip
- mount
- ncurses-base
- perl-base
- python-minimal
- sed
- tar
- util-linux
- flex
- bison
- dwarves
- openssl
- libelf

### With Pacman

- base-devel
- flex
- bison
- dwarfs (AUR)
- openssl
- libelf

## Build Instruction

1. Clone this repo with branch `linux-wsl2-scissors`
   ```bash
   git clone https://github.com/Thor-x86/linux -b linux-wsl2-scissors wsl2-scissors
   ```
2. Get into the directory
   ```bash
   cd wsl2-scissors
   ```
3. Then simply compile
   ```bash
   make KCONFIG_CONFIG=Microsoft/config-wsl
   ```
   or if you're running on ARM processor, run this instead
   ```bash
   make KCONFIG_CONFIG=Microsoft/config-wsl-arm64
   ```

Then you'll get the output file called "vmlinux"


[wsl2-kernel]:  https://github.com/microsoft/WSL2-Linux-Kernel
[about-wsl2]:   https://docs.microsoft.com/en-us/windows/wsl/about#what-is-wsl-2
[wsl-issue]:    https://github.com/microsoft/WSL/issues/new/choose
[normal-bug]:   https://www.kernel.org/doc/html/latest/admin-guide/bug-hunting.html#reporting-the-bug
[security-bug]: https://www.kernel.org/doc/html/latest/admin-guide/security-bugs.html
[submit-patch]: https://www.kernel.org/doc/html/latest/process/submitting-patches.html
[install-inst]: https://docs.microsoft.com/en-us/windows/wsl/wsl-config#configure-global-options-with-wslconfig
[branch-rolling-stable]: https://github.com/gregkh/linux/tree/linux-rolling-stable
