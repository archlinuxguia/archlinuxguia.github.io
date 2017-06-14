Pós-instalação do Arch Linux

''Após a instalação do Arch Linux, você precisará adicionar funcionalidades adicionais. Separamos algumas delas neste documento, organizadas por categoria:''

*''Sistema:''
**[[Adicionar usuário]]
**[[Configurar o Netctl]]
**[[Instalar o Xorg]]
**[[Xinitrc]]
*''Ambiente gráfico:''
**[[Gnome]]
**[[MATE]]

Adicionar usuário

''Para adicionar um novo usuário com privilégios administrativos proceda com os seguintes comandos:''

```
# useradd -m -G wheel -s /bin/bash archie
```
>Onde `archie` é o seu nome de usuário
```
# EDITOR=nano visudo
```
>Descomente a seguinte linha, depois salve o arquivo e feche o editor:
$$$
%wheel      ALL=(ALL) ALL
$$$
>Defina um senha para o seu usuário:

```
# passwd archie
```

Configurar o Netctl

''Para configurar o Netctl proceda com os seguintes comandos:''

```
# ip link
```
>Tome nota dos nomes das interfaces de redes, enpXsY para rede cabeada e wlpXsY para redes sem fio
```
# cp /etc/netctl/examples/ethernet-dhcp /etc/netctl/ethernet-dhcp
```
```
# nano /etc/netctl/ethernet-dhcp
```
>Modifique a seguinte linha, substituindo `eth0` pelo nome da sua interface:
$$$
Interface=enpXsY
$$$
>Habilite os serviços do Netctl:

```
# sudo systemctl enable netctl-ifplugd@enpXsY.service
```
```
# sudo systemctl enable netctl-auto@wlpXsY.service
```

Instalar o Xorg

''Para instalar o Xorg proceda com os seguintes comandos:''

```
# pacman -S xorg-server xorg-server-utils
```
>Driver de vídeo:
|!Marca|!Tipo|!Driver|
|!AMD|Open source|xf86-video-amdgpu|
|~|~|xf86-video-ati|
|~|Proprietário|catalyst^^AUR^^|
|!Intel|Open source|xf86-video-intel|
|!Nvidia|Open source|xf86-video-nouveau|
|~|Proprietário|nvidia|
|~|~|nvidia-340xx|
|~|~|nvidia-304xx|
```
# pacman -S nome_do_driver
```
>Se você optou por instalar o xf86-input-evdev, instale um driver para o touchpad:
```
# pacman -S xf86-input-synaptics
# pacman -S xf86-input-libinput

Xinitrc

''Se você não gosta de gerenciadores de login e prefere usar o comando `startx` para iniciar o ambiente gráfico, proceda com os seguintes comandos:''

```
# pacman -S xorg-xinit
```
>Copie e edite o arquivo de configuração padrão:
```
$ cp /etc/X11/xinit/xinitrc ~/.xinitrc
```
```
$ nano ~/.xinitrc
```
>Apage ou comente as seguintes linhas e adicione o comando correspondente ao seu ambiente gráfico:
```
#twm &
#xclock -geometry 50x50-1+1 &
#xterm -geometry 80x50+494+51 &
#xterm -geometry 80x20+494-0 &
#exec xterm -geometry 80x66+0+0 -name login

exec mate-session

Gnome

''Para instalar o Gnome proceda com os seguintes comandos:''


```
# pacman -S gnome gnome-extra
```
```
# systemctl enable gdm
```
```
# systemctl enable NetworkManager
```

MATE

''Para instalar o ambiente gráfico MATE proceda com os seguintes comandos:''

```
# pacman -S mate mate-extra
```
>Para um instalação mínima:
```
$ pacman -S marco mate-panel mate-session-manager
```
```
$ nano ~/.xinitrc
```
>Apage ou comente as seguintes linhas e adicione o comando correspondente ao seu ambiente gráfico:
```
#twm &
#xclock -geometry 50x50-1+1 &
#xterm -geometry 80x50+494+51 &
#xterm -geometry 80x20+494-0 &
#exec xterm -geometry 80x66+0+0 -name login

exec mate-session
