---
layout: post
title:  "Instação do Arch Linux"
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
