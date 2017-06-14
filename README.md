# archlinuxguia.github.io
Arch Linux - Guia do Iniciante

Este projeto visa disponibilizar guias para o usuário iniciante na distribuição Arch Linux.

## Como contribuir:

### Caso tenha o Ruby instalado:

1. Crie um fork deste repositório

2. Clone o repositório

```
$ git clone https://github.com/nome-de-usuario/archlinuxguia.github.io
```

3. Rode o Jekyll

```
$ cd archlinuxguia.github.io
```

```
$ bundle exec jekyll serve --drafts
```

### Se não possuir o Ruby instalado, ou preferir usar o mesmo ambiente que o nosso:

1. Instale o VirtualBox

2. Instale o Vagrant

3. Inicie o ambiente de desenvolvimento

```
$ vagrant up
```

4. Conecte-se ao ambiente

```
$ vagrant ssh
```

5. Instale o Bundler

```
$ gem install bundler
```

> Talvez seja necessário sair do ambiente (`$ exit`) e voltar (`$ vagrant ssh`)

6. Rode o Jekyll

```
$ cd /vagrant
```

```
$ bundle exec jekyll serve --host 0.0.0.0 --drafts --force_polling
```
