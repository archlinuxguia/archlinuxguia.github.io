Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"

  # Desabilita a checagem automática de atualizações do box.
  # config.vm.box_check_update = false

  # Cria o mapeamento de portas redirecionadas
  config.vm.network "forwarded_port", guest: 4000, host: 4000

  # Compartilha uma pasta adicional para VM.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Configurações específicas para o Provedor:
  config.vm.provider "virtualbox" do |vb|
    # Personaliza a quantidade de memória da VM:
    vb.memory = "1024"
  end

  # Ativa o provisionamento com um script shell
  config.vm.provision "shell", privileged: false, inline: <<-SHELL
    echo 'Atualizando o sistema...'
    sudo apt-get update && sudo apt-get upgrade -y
    echo 'Instalando pacotes essenciais...'
    sudo apt-get install -y build-essential libssl-dev libreadline-dev
    echo 'Instalando rbenv...'
    git clone https://github.com/rbenv/rbenv.git ~/.rbenv
    cd ~/.rbenv && src/configure && make -C src
    export PATH="$HOME/.rbenv/bin:$PATH"
    echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
    rbenv init
    echo 'eval "$(rbenv init -)"' >> ~/.bashrc
    git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
    echo 'Instalando Ruby...'
    rbenv install 2.4.1
    rbenv global 2.4.1
    #echo 'Instalando Bundler...'
    #gem install bundler
    #echo 'Instalando as gems do projeto...'
    #cd /vagrant && bundle update
    #echo 'Iniciando o Jekyll...'
    #jekyll serve --host 0.0.0.0 --drafts --detach
    echo 'Tudo pronto!'
  SHELL
end
