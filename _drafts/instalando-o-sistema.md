---
layout: post
title:  "Instalando o sistema"
date:   2017-06-02 12:00:25 -0400
categories: instalação
---
Instalando o sistema

*''Configurar o espelho:''
```
# cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.old
```
>Memorize o endereço do espelho (ou parte dele):

```
# nano /etc/pacman.d/mirrorlist.old
```
```
# cat /etc/pacman.d/mirrorlist.old | grep arch.localmsp > /etc/pacman.d/mirrorlist
```
>Neste exemplo o espelho escolhido foi:
>`Server = http://arch.localmsp.org/arch/$repo/os/$arch`
>Verifique o repositório escolhido:

```
# cat /etc/pacman.d/mirrorlist
```
*''Instalar o sistema base:''
```
# pacstrap -i /mnt base base-devel
```
*''Gerar o fstab:''
```
# genfstab -U /mnt > /mnt/etc/fstab
```
*''Próximo: [[Configurando o sistema]]''
