---
layout: post
title:  "Iniciando o Arch Linux"
date:   2017-06-02 12:00:05 -0400
categories: instalação
---
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

* __Próximo:__ [Particionando os discos]({{ site.baseurl }}{% link _drafts/particionando-os-discos.md %})
