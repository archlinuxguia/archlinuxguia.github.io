---
layout: post
title:  "Particionando os discos"
date:   2017-06-02 12:00:10 -0400
categories: instalação
---
* __MBR ou GPT?__

>Se a sua inicialização é do tipo UEFI você pode usar a tabela de partição GPT, caso contrário use a tabela do tipo MBR.

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

---
Partições:

| # | Caminho | Tipo | Tamanho |
| --- | --- | --- | --- |
| 1 | swap | 82 | 1-4GiB |
| 2 | / | 83 | 16-24GiB |
| 3 | /home | 83 | Restante

---
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

---
Partições:

| # | Caminho | Tamanho | Tipo | Nome |
| --- | --- | --- | --- | --- |
| 1 | /boot | 512MiB | EF00 | Padrão |
| 2 | swap | 1-4GiB | 8200 | swap |
| 3 | / | 16-24GiB | 8300 | Linux |
| 4 | /home | Restante | 8300 | Padrão

---
>Não esqueça de definir os nomes __swap__ e __Linux__ de acordo com a tabela acima, Estes nomes serão usados depois na instalação do __rEFInd__.

* __Próximo:__ [Criando os sistemas de arquivos]({{ site.baseurl }}{% link _drafts/criando-os-sistemas-de-arquivos.md %})
