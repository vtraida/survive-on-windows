> I've used Linux for about 10+ years now. Here's what I setup on windows.

# Setup

## Initial actions

- Source an *up to date* [Windows ISO](https://www.microsoft.com/en-gb/software-download/windows10ISO)
- To prepare a usb based instalation from Linux, you can use [WoeUSB](https://github.com/slacka/WoeUSB) : It'll setup the ISO to USB with UEFI support
- Install windows
- Install [Chocolatey](https://chocolatey.org/), reserve [Scoop](https://github.com/lukesampson/scoop) only for sudo (chocolatey's sudo is behaving weirdly)
- Use [DisableWinTracking](https://github.com/10se1ucgo/DisableWinTracking/releases/) to clean stuff a bit
- Update Windows, of force an update if you have a outdated Windows installation
- Install [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10) (require a system restart)
- Change windows time to UTC if using dual boot with linux :

    ``` powershell
    Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_QWORD /d 1
    ```

- Reboot
- Go to the initial setup of [WSL](#WSL) (setup name, hostname..). Use [shellconfig](https://github.com/replicajune/shellconfig) to spice up your shell

# Tools

## Package managers

Two options exists :

- [Chocolatey](https://chocolatey.org) helps to install packages for windows the way apt or yum would do. Use that by default
- [Scoop](https://scoop.sh/) on the other hand will install program in its own workspace. 

Chocolatey is more suitable for products that require a deep integration with the system or for apps that you'll want to be available for multiple users on your system. Scoop on the other hand uses "portable" versions and install stuff for a given user (the application data/folders will be located into the user directory)

Almost all tools given bellow are available either with Chocolatey, Scoop or both. Use Chocolatey by default if you're not sure about Scoop, as app integration can be hazardous with the later.

### Install

> use powershell as admin for both.

- Chocolatey:

``` powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

- Scoop:

``` powershell
iex (new-object net.webclient).downloadstring('https://get.scoop.sh')
scoop install git 7zip
scoop bucket add extras
scoop update *
```

## Utilities

- [DisableWinTracking](https://github.com/10se1ucgo/DisableWinTracking): Disable tracking, remove onedrive
- [Bulk Crap Uninstaller](https://www.bcuninstaller.com): removing adwares and pre-installed (windows) components
- [7zip](https://www.7-zip.org/): to replace to winrar, winzip..
- [SysinternalsSuite](https://docs.microsoft.com/en-us/sysinternals/downloads/): a couple of utilities, including [Process Explorer](https://docs.microsoft.com/en-us/sysinternals/downloads/process-explorer) and [Autoruns](https://docs.microsoft.com/en-us/sysinternals/downloads/autoruns)
- [Veracrypt](https://www.veracrypt.fr/en/Downloads.html): Setup encrypted drives. Known as a safe alternative to bitlocker, and compatible with Linux
- [Keypirinha](https://keypirinha.com/): A launcher, similar to Alfred, spotlight, Ulauncher..
- [Microsoft-windows-terminal](https://github.com/Microsoft/Terminal): the new terminal from Ms

## Workflows:

- [Github Desktop](https://desktop.github.com/): git client (use https scheme for your local clones, instead of ssh)
- [Atom](https://atom.io/): IDE, compatible with *Github Desktop* ([VScode](https://code.visualstudio.com/) is also a good option)
- [meld](http://meldmerge.org/): graphical tool to manage merge conflicts

## Linux, VM

Some stuff will need a proper Linux installation instead of WSL, you might want to use :

- [Vagrant](https://www.vagrantup.com/) : automatic provision of VMs with Virtualbox (or Hyper-V if you're into that)
- [Virtualbox](https://www.virtualbox.org/) : a backend for Vagrant

# WSL Legacy

[WSL](https://docs.microsoft.com/en-us/windows/wsl/about) ships with flavors of Linux distributions instead of being a dedicated flavor "like" Cygwin is, meaning that you'll use your WSL instance as Ubuntu, Fedora, Suse, etc..

Once you've installed WSL, you'll need a flavor.

## Files import

Be careful when importing files from Windows and WSL environment, as file encoding between *DOS* and *UNIX* are not the same.. To convert a file using vim, do :

``` vim
:set ff=unix
```

A tool called dos2unix to do the same on command line:

```sh
dos2unix file
```

Generally speaking, its quite a bad idea to mix files used by wsl 1 and windows, partially because of that problem. Recents updates made that thing a bit less painful but it still cause issues from time to time.

## Upgrade

You might need to update *WSL* at some point. Two options exists : One using `lxrun`, the other one through *WSL*.

### Using WSL

This is a bit like a `dist-upgrade` :

``` bash
do-release-upgrade
```

> :information_source: one or more reboot might be needed.

### Via *wslconfig*

> :warning: This will **wipe** your *WSL* installation. **BACKUP EVERYTHING** :warning:

- Uninstall *WSL* (replace <distrib> with the distrib name you choosed) :

``` powershell
wslconfig /u Ubuntu
```

- Go back to the [Windows store](https://docs.microsoft.com/en-us/windows/wsl/install-win10#install-your-linux-distribution-of-choice), install *WSL*, and setup everything again/back.

# Other nice stuff to have

I personally like those tools on any windows installation :thumbsup: :

- [Brave](https://laptop-updates.brave.com/latest/winx64) : use chromium, with security by design and have a neat adblocker included.
- [Winamp](https://www.winamp.com/) : it's still alive !
- [Spotify](https://www.spotify.com/fr/download/windows) : needs no introduction.
- [BleachBit](https://www.bleachbit.org/download/windows) : because the other candidate is becoming a bit weird lately..
