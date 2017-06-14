---
layout: post
title:  "Configurando o sistema"
date:   2017-06-02 12:00:30 -0400
categories: instalação
---
Configurando o sistema

*''Mudar a raiz:''
```
# arch-chroot /mnt /bin/bash
```
*''Alterar a localização:''
```
# nano /etc/locale.gen
```
$$$
Ctrl + w: pesquisar palavra
Ctrl + o: salvar as modificações
Ctrl + x: sair do editor
$$$
>Pesquise pela string `pt_BR` para ir direto a linha:
>`#pt_BR.UTF-8 UTF-8`
>Depois é só apagar o `#` do início da linha, salvar e sair do editor.
```
# locale-gen
```
```
# echo LANG=pt_BR.UTF-8 > /etc/locale.conf
```
*''Layout do teclado:''
```
# echo KEYMAP=br-abnt2 > /etc/vconsole.conf
```
*''Fuso horário:''
```
# tzselect
```
```
# ln -s /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime
```
>Neste exemplo foi definido o horário de São Paulo
```
# hwclock --systohc --utc
```
*''Gerar ambiente ramdisk inicial: ''`(OPCIONAL)`
```
# nano /etc/mkinitcpio.conf
```
```
# mkinitcpio -p linux
```
>Você pode adicionar o HOOK `resume` após o `udev`, ou acrescentar em MODULES o módulo da sua placa de vídeo `radeon`, `nouveau` ou `intel_agp i915` após instalar o driver da mesma.
*''Nome da máquina:''
```
# echo myhostname > /etc/hostname
```
```
# nano /etc/hosts
```
>Mude o nome `myhostname` com o nome que desejar, depois adicione o mesmo nome às entradas `localhost` no arquivo `/etc/hosts`
$$$
127.0.0.1  localhost.localdomain  localhost  myhostname
::1        localhost.localdomain  localhost  myhostname
$$$
*''Instalando o Netctl:''
```
# pacman -S wpa_actiond ifplugd dialog
```
>Esses pacotes são necessários para você usar o `wifi-menu` no sistema instalado.
*''Próximo: [[Instalando o gerenciador de boot]]''
