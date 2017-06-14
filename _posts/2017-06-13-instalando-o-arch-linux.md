---
layout: post
title:  "Instalando o Arch Linux"
date:   2017-06-13 21:55:05 -0400
categories: instalação
---
Este documento irá guiá-lo durante o processo de instalação do Arch Linux.

Página do projeto: [https://github.com/archlinuxguia/archlinuxguia.github.io](https://github.com/archlinuxguia/archlinuxguia.github.io)

Após iniciar a mídia de instalação do Arch Linux, processa com os comandos a seguir:

* __Legacy ou UEFI?__

~~~
# ls /sys/firmware/efi/efivars
~~~

> Se o diretório acima contiver arquivos então a inicialização é do tipo UEFI

* __Layout do teclado:__

~~~
# loadkeys br-abnt2
~~~

* __Conexão com a internet:__

Para conectar a uma rede sem fio:

~~~
# wifi-menu
~~~

> Para redes cabeadas a configuração deve ocorrer de forma automática usando DHCP.

* __Sincronizar o horário:__

~~~
# timedatectl set-ntp true
~~~

* __MBR ou GPT?__

Se a sua inicialização é do tipo UEFI você pode usar a tabela de partição GPT, caso contrário use a tabela do tipo MBR.

* __MBR:__

~~~
# fdisk /dev/sda
~~~

Atalhos:

|m:|exibe lista de comandos|
| o: | cria uma tabela MBR vazia |
| n: | cria uma nova partição |
| d: | exclui uma partição |
| t: | altera o tipo da partição |
| p: | mostra a tabela de partição |
| w: | grava a tabela no disco e sai |
| q: | sai sem salvar as alterações

Partições:

| # | Caminho | Tipo | Tamanho |
| --- | --- | --- | --- |
| 1 | swap | 82 | 1-4GiB |
| 2 | / | 83 | 16-24GiB |
| 3 | /home | 83 | Restante

* __GPT:__

~~~
# gdisk /dev/sda
~~~

Atalhos:

| ?: | exibe lista de comandos |
| o: | cria uma tabela GPT vazia |
| n: | cria uma nova partição |
| d: | exclui uma partição |
| t: | altera o tipo da partição |
| c: | muda o nome da partição |
| p: | mostra a tabela de partição |
| w: | grava a tabela no disco e sai |
| q: | sai sem salvar as alterações

Partições:

| # | Caminho | Tamanho | Tipo | Nome |
| --- | --- | --- | --- | --- |
| 1 | /boot | 512MiB | EF00 | Padrão |
| 2 | swap | 1-4GiB | 8200 | swap |
| 3 | / | 16-24GiB | 8300 | Linux |
| 4 | /home | Restante | 8300 | Padrão

>Não esqueça de definir os nomes __swap__ e __Linux__ de acordo com a tabela acima, Estes nomes serão usados depois na instalação do __rEFInd__.

* __ext4 ou Btrfs?__

Btrfs é um sistema de arquivos com recursos avançados como RAID por software, checagem de integridade, backup incremental, instantâneo e compressão.

* __MBR:__

~~~
# mkswap /dev/sda1
~~~

Escolha um:

~~~
# mkfs.ext4 /dev/sda2
# mkfs.btrfs /dev/sda2
~~~

~~~
# mkfs.ext4 /dev/sda3
~~~

* __GPT:__

~~~
# mkfs.vfat -F32 /dev/sda1
~~~

~~~
# mkswap /dev/sda2
~~~

Escolha um:

~~~
# mkfs.ext4 /dev/sda3
# mkfs.btrfs /dev/sda3
~~~

~~~
# mkfs.ext4 /dev/sda4
~~~

* __ext4(MBR):__

~~~
# mount /dev/sda2 /mnt
~~~

~~~
# mkdir -p /mnt/home
~~~

~~~
# mount /dev/sda3 /mnt/home
~~~

~~~
# swapon /dev/sda1
~~~

* __ext4(GPT):__

~~~
# mount /dev/sda3 /mnt
~~~

~~~
# mkdir -p /mnt/boot
~~~

~~~
# mount /dev/sda1 /mnt/boot
~~~

~~~
# mkdir -p /mnt/home
~~~

~~~
# mount /dev/sda4 /mnt/home
~~~

~~~
# swapon /dev/sda2
~~~

* __Btrfs(MBR):__

>Vamos criar um subvolume chamado __@arch__ que montaremos no diretório __raiz__, e outro subvolume __@pkg__ que montaremos no diretório __/var/cache/pacman/pkg__

~~~
# mount -o noatime,compress=lzo /dev/sda2 /mnt
~~~

~~~
# btrfs subvolume create /mnt/@arch
~~~

~~~
# btrfs subvolume create /mnt/@pkg
~~~

~~~
# umount /dev/sda2
~~~

~~~
# mount -o noatime,compress=lzo,subvol=@arch /dev/sda2 /mnt
~~~

~~~
# mkdir -p /mnt/var/cache/pacman/pkg
~~~

~~~
# mount -o noatime,compress=lzo,subvol=@pkg /dev/sda2 /mnt/var/cache/pacman/pkg
~~~

~~~
# mkdir -p /mnt/home
~~~

~~~
# mount /dev/sda3 /mnt/home
~~~

~~~
# swapon /dev/sda1
~~~

* __Btrfs(GPT):__

~~~
# mount -o noatime,compress=lzo /dev/sda3 /mnt
~~~

~~~
# btrfs subvolume create /mnt/@arch
~~~

~~~
# btrfs subvolume create /mnt/@pkg
~~~

~~~
# umount /dev/sda3
~~~

~~~
# mount -o noatime,compress=lzo,subvol=@arch /dev/sda3 /mnt
~~~

~~~
# mkdir -p /mnt/var/cache/pacman/pkg
~~~

~~~
# mount -o noatime,compress=lzo,subvol=@pkg /dev/sda3 /mnt/var/cache/pacman/pkg
~~~

~~~
# mkdir -p /mnt/home
~~~

~~~
# mount /dev/sda4 /mnt/home
~~~

~~~
# mkdir -p /mnt/boot
~~~

~~~
# mount /dev/sda1 /mnt/boot
~~~

~~~
# swapon /dev/sda2
~~~

* __Configurar o espelho:__

~~~
# cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.old
~~~

~~~
# nano /etc/pacman.d/mirrorlist.old
~~~

>Memorize o endereço do espelho (ou parte dele)

~~~
# cat /etc/pacman.d/mirrorlist.old | grep arch.localmsp > /etc/pacman.d/mirrorlist
~~~

>Neste exemplo o espelho escolhido foi:
>__Server = http://arch.localmsp.org/arch/$repo/os/$arch__
>Verifique o repositório escolhido:

~~~
# cat /etc/pacman.d/mirrorlist
~~~

* __Instalar o sistema base:__

~~~
# pacstrap -i /mnt base base-devel
~~~

* __Gerar o fstab:__

~~~
# genfstab -U /mnt > /mnt/etc/fstab
~~~

* __Mudar a raiz:__

~~~
# arch-chroot /mnt /bin/bash
~~~

* __Alterar a localização:__

~~~
# nano /etc/locale.gen
~~~

Atalhos:

| Ctrl + w: | pesquisar palavra |
| Ctrl + o: | salvar as modificações |
| Ctrl + x: | sair do editor |

>Pesquise pela string __pt_BR__ para ir direto a linha: `#pt_BR.UTF-8 UTF-8`. Apague o `#` do início da linha, salve e saia do editor.

~~~
# locale-gen
~~~

~~~
# echo LANG=pt_BR.UTF-8 > /etc/locale.conf
~~~

* __Layout do teclado:__

~~~
# echo KEYMAP=br-abnt2 > /etc/vconsole.conf
~~~

* __Fuso horário:__

~~~
# tzselect
~~~

~~~
# ln -s /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime
~~~

>Neste exemplo foi definido o horário de São Paulo

~~~
# hwclock --systohc --utc
~~~

* __Gerar ambiente ramdisk inicial: (OPCIONAL)__

~~~
# nano /etc/mkinitcpio.conf
~~~

~~~
# mkinitcpio -p linux
~~~

>Você pode adicionar o HOOK __resume__ após o __udev__, ou acrescentar em MODULES o módulo da sua placa de vídeo __radeon__, __nouveau__ ou __intel_agp i915__ após instalar o driver da mesma.

* __Nome da máquina:__

~~~
# echo myhostname > /etc/hostname
~~~

~~~
# nano /etc/hosts
~~~

>Mude o nome __myhostname__ com o nome que desejar, depois adicione o mesmo nome às entradas __localhost__ no arquivo __/etc/hosts__

~~~
127.0.0.1  localhost.localdomain  localhost  myhostname
::1        localhost.localdomain  localhost  myhostname
~~~

* __Instalando o Netctl:__

~~~
# pacman -S wpa_actiond ifplugd dialog
~~~

>Esses pacotes são necessários para você usar o __wifi-menu__ no sistema instalado.

* __Grub (Legacy):__

~~~
# pacman -S grub
~~~

~~~
# grub-install --recheck --target=i386-pc /dev/sda
~~~

~~~
# grub-mkconfig -o /boot/grub/grub.cfg
~~~

* __Grub (UEFI):__

~~~
# pacman -S grub efibootmgr
~~~

~~~
# grub-install --recheck --target=x86_64-efi --efi-directory=/boot --bootloader-id=grub
~~~

~~~
# grub-mkconfig -o /boot/grub/grub.cfg
~~~

* __rEFInd (ext4):__

~~~
# pacman -S refind-efi
~~~

~~~
# refind-install --alldrivers
~~~

* __rEFInd (Btrfs):__

~~~
# pacman -S refind-efi
~~~

~~~
# refind-install --alldrivers
~~~

~~~
# nano /boot/EFI/refind/refind.conf
~~~

>No final do arquivo adicione a seguinte entrada, depois salve as alterações e feche o editor:

~~~
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
~~~

* __Definir a senha do usuário root:__

~~~
# passwd
~~~

* __Mudar a raiz:__

~~~
# exit
~~~

* __Desmontar os sistemas de arquivos:__

~~~
# umount -R /mnt
~~~

* __Reiniciar o sistema:__

~~~
# reboot
~~~

* __Instalação finalizada!__
