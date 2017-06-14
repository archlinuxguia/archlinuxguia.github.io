---
layout: post
title:  "Criando os sistemas de arquivos"
date:   2017-06-02 12:00:15 -0400
categories: instalação
---
Criando os sistemas de arquivos

*''ext4 ou Btrfs?''
<<<
Btrfs é um sistema de arquivos com recursos avançados como RAID por software, checagem de integridade, backup incremental, instantâneo e compressão.
<<<
*''MBR:''
```
# mkswap /dev/sda1
```
`Escolha um:`

```
# mkfs.ext4 /dev/sda2
# mkfs.btrfs /dev/sda2
```
```
# mkfs.ext4 /dev/sda3
```
*''GPT:''
```
# mkfs.vfat -F32 /dev/sda1
```
```
# mkswap /dev/sda2
```
`Escolha um:`

```
# mkfs.ext4 /dev/sda3
# mkfs.btrfs /dev/sda3
```
```
# mkfs.ext4 /dev/sda4
```
*''Próximo: [[Montando os sistemas de arquivos]]''
