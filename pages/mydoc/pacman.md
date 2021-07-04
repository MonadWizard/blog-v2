---
title: Package Manager (pacman)
keywords: pacman Bangla Tutorials, bangla pacman, pacman, Blog Bangla, Monad wizard , package manager
last_updated: Aug 04 , 2020
# tags: [getting_started]
summary: 'যারা Arch Linux এ new comer , তারা pacman নিয়ে যদি কোন problem face করেন, তা হইলে এই cheat-sheet টা আপনাদের অনেক উপকারে আসতে পারে।'
sidebar: mydoc_sidebar
permalink: pacman.html
folder: mydoc
---


## Update and Upgrade

#### Update package list

```
    sudo pacman -Syy
```

#### Update and upgrade all

```
    sudo pacman -Syu
```

#### Update and upgrade aur packages

```
    yaourt -Syu --aur
```

#### Update and upgrade yaourt packages

```
    yaourt -Syua
```

### Get distro version

```
    lsb_release -a
```

## Install or find Package

#### Install specific package

```
    sudo pacman -S pkgname
```

#### Find available packages

```
    sudo pacman -Ss keyword
```

#### Find available local packages

```
    sudo pacman -Qs keyword
```

#### Show packages of group xorg

```
    pacman -Sg xorg
```

#### List all files from package

```
    pacman -Ql pkgname
```

### Pacman log file

```
    /var/log/pacman.log
```

## Remove Package

#### Remove only a package

```
    pacman -R package_name
```

#### To remove a package and its dependencies which are not required by any other installed package

```
    sudo pacman -Rs package_name
```

#### List all packages no longer required as dependencies

```
    sudo pacman -Qdt
```

#### Clean package cache

```
    pacman -Sc
```

### Screen recording

```
    gtk-recordmydesktop
```

### Mount iso file

```
    fuseiso -p  testimage.iso testimagemountpoint
```

### To unmount

```
    fusermount -u <mountpoint>
```

### Get IP address

```
    ip addr
```

## Operators

| used like      | Specifications                          |
| -------------- | --------------------------------------- |
| -D, --database | Operate on the package database         |
| -Q, --query    | Query the package database              |
| -R, --remove   | Remove package(s) from the system       |
| -S, --sync     | Synchr­onize packages                   |
| -T, --deptest  | Check depend­encies                     |
| -U, --upgrade  | Upgrade or add package(s) to the system |
| -F, --files    | Query the files database                |
| -V, --version  | Display version and exit                |
| -h, --help     | Display syntax for the given operation  |

## Options

| used like                        | Specifications                                                          |
| -------------------------------- | ----------------------------------------------------------------------- |
| -b, --dbpath                     | Specify an altern­ative database location                               |
| -r, --root                       | Specify an altern­ative instal­lation root                              |
| -v, --verbose                    | Output paths such as as the Root, Conf File, DB Path, Cache Dirs        |
| --arch <ar­ch>                   | Specify an alternate archit­ecture                                      |
| --cachedir <di­r>                | Specify al altern­ative package cache location                          |
| --color <wh­en>                  | Specify when to enable coloring                                         |
| --config <fi­le>                 | Specify an alternate config­uration file                                |
| --debug                          | Display debug messages                                                  |
| --gpgdir <di­r>                  | Specify a directory of files used by GnuPG to verify package signatures |
| --hookdir <di­r>                 | Specify an alternate directory containing hook files                    |
| --logfile <fi­le>                | Specify an alternate log file                                           |
| --noco­nfirm                     | Bypass any and all "Are you sure?" messages                             |
| --confirm                        | Cancels the effects of a previous --noco­nfirm                          |
| --disa­ble­-do­wnl­oad­-ti­meout | Disable defaults for low speed limit and timeout on downloads           |
| --sysroot <di­r>                 | Specify an altern­ative system root                                     |
