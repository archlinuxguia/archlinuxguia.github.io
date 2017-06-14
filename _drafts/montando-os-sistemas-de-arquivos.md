---
layout: post
title:  "Montando os sistemas de arquivos"
date:   2017-06-02 12:00:20 -0400
categories: instalação
---
Montando os sistemas de arquivos

*''ext4:''
`MBR:`

```
# mount /dev/sda2 /mnt
```
```
# mkdir -p /mnt/home
```
```
# mount /dev/sda3 /mnt/home
```
```
# swapon /dev/sda1
```
`GPT:`

```
# mount /dev/sda3 /mnt
```
```
# mkdir -p /mnt/boot
```
```
# mount /dev/sda1 /mnt/boot
```
```
# mkdir -p /mnt/home
```
```
# mount /dev/sda4 /mnt/home
```
```
# swapon /dev/sda2
```
*''Btrfs:''
>Vamos criar um subvolume chamado `@arch` que montaremos no diretório `raiz`, e outro subvolume `@pkg` que montaremos no diretório `/var/cache/pacman/pkg`
`MBR:`

```
# mount -o noatime,compress=lzo /dev/sda2 /mnt
```
```
# btrfs subvolume create /mnt/@arch
```
```
# btrfs subvolume create /mnt/@pkg
```
```
# umount /dev/sda2
```
```
# mount -o noatime,compress=lzo,subvol=@arch /dev/sda2 /mnt
```
```
# mkdir -p /mnt/var/cache/pacman/pkg
```
```
# mount -o noatime,compress=lzo,subvol=@pkg /dev/sda2 /mnt/var/cache/pacman/pkg
```
```
# mkdir -p /mnt/home
```
```
# mount /dev/sda3 /mnt/home
```
```
# swapon /dev/sda1
```
`GPT:`

```
# mount -o noatime,compress=lzo /dev/sda3 /mnt
```
```
# btrfs subvolume create /mnt/@arch
```
```
# btrfs subvolume create /mnt/@pkg
```
```
# umount /dev/sda3
```
```
# mount -o noatime,compress=lzo,subvol=@arch /dev/sda3 /mnt
```
```
# mkdir -p /mnt/var/cache/pacman/pkg
```
```
# mount -o noatime,compress=lzo,subvol=@pkg /dev/sda3 /mnt/var/cache/pacman/pkg
```
```
# mkdir -p /mnt/home
```
```
# mount /dev/sda4 /mnt/home
```
```
# mkdir -p /mnt/boot
```
```
# mount /dev/sda1 /mnt/boot
```
```
# swapon /dev/sda2
```
*''Próximo: [[Instalando o sistema]]''
