---
layout: post
title:  "Instalando o gerenciador de boot"
date:   2017-06-02 12:00:35 -0400
categories: instalação
---
Instalando o gerenciador de boot

*''Grub:''
`Legacy:`

```
# pacman -S grub
```
```
# grub-install --recheck --target=i386-pc /dev/sda
```
```
# grub-mkconfig -o /boot/grub/grub.cfg
```
`EFI:`

```
# pacman -S grub efibootmgr
```
```
# grub-install --recheck --target=x86_64-efi --efi-directory=/boot --bootloader-id=grub
```
```
# grub-mkconfig -o /boot/grub/grub.cfg
```
*''rEFInd: ''`(APENAS EFI)`

`ext4:`

```
# pacman -S refind-efi
```
```
# refind-install --alldrivers
```
`Btrfs:`

```
# pacman -S refind-efi
```
```
# refind-install --alldrivers
```
```
# nano /boot/EFI/refind/refind.conf
```
>No final do arquivo adicione a seguinte entrada, depois salve as alterações e feche o editor:
$$$
menuentry "Arch Linux" {
        icon /EFI/refind/icons/os_arch.png
        volume Linux
        loader /@arch/boot/vmlinuz-linux
        initrd /@arch/boot/initramfs-linux.img
        options "root=PARTLABEL=Linux rw rootflags=subvol=@arch resume=PARTLABEL=swap"
        submenuentry "Boot using fallback initramfs" {
                initrd /@arch/boot/initramfs-linux-fallback.img
        }
}
$$$
*''Próximo: [[Finalizando a instalação]]''
