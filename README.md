# archlinuxguia.github.io
Arch Linux - Guia do Iniciante

Este projeto visa disponibilizar guias para o usuário iniciante na distribuição Arch Linux.

## Como contribuir:

### Caso tenha o Ruby instalado:

1. Crie um fork deste repositório

2. Clone o repositório

```
$ git clone https://github.com/nome-de-usuario/archlinuxguia.github.io archlinuxguia
```

3. Rode o Jekyll

```
$ cd archlinuxguia
```

```
$ bundle exec jekyll serve --drafts
```

### Se não possuir o Ruby instalado, ou preferir usar o mesmo ambiente que o nosso (Vagrant ou Docker/Docker Compose):

#### Vagrant:

1. Instale o [VirtualBox com Pacote de Extensões](https://www.virtualbox.org/wiki/Downloads)

2. Instale o [Vagrant](https://www.vagrantup.com/downloads.html)

3. Crie um fork deste repositório

4. Clone o repositório

```
$ git clone https://github.com/nome-de-usuario/archlinuxguia.github.io archlinuxguia
```

5. Inicie o ambiente de desenvolvimento

```
$ cd archlinuxguia
```

```
$ vagrant up
```

6. Conecte-se ao ambiente

```
$ vagrant ssh
```

7. Instale o Bundler

```
$ gem install bundler
```

> Talvez seja necessário sair do ambiente (`$ exit`) e voltar (`$ vagrant ssh`)

8. Rode o Jekyll

```
$ cd /vagrant
```

```
$ bundle exec jekyll serve --host 0.0.0.0 --drafts --force_polling
```

#### Docker:

1. Instale o [VirtualBox com Pacote de Extensões](https://www.virtualbox.org/wiki/Downloads)

2. Instale o [Docker](https://docs.docker.com/engine/installation/)

3. Instale o [Docker Compose](https://docs.docker.com/compose/install/) (Opcional)

4. Crie um fork deste repositório

5. Clone o repositório

```
$ git clone https://github.com/nome-de-usuario/archlinuxguia.github.io archlinuxguia
```

6. Inicie o container do Jekyll

```
$ cd archlinuxguia
```

```
$ docker-composer up
```

ou

```
$ docker run --rm --label=jekyll --volume=%CD%:/srv/jekyll -it -p 4000:4000 jekyll/jekyll:pages serve --drafts --force_polling
```
