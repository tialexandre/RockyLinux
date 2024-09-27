#!/bin/bash

# Verificar se o script está sendo executado como root
if [ "$EUID" -ne 0 ]; then
  echo "Por favor, execute como root."
  exit
fi

# Atualizar o sistema
echo "Atualizando pacotes do sistema..."
dnf update -y

# Remover versões antigas do Docker, se houver
echo "Removendo versões antigas do Docker, se houver..."
dnf remove -y docker docker-client docker-client-latest docker-common docker-latest docker-latest-logrotate docker-logrotate docker-engine

# Instalar pacotes necessários para o Docker
echo "Instalando pacotes de dependências..."
dnf install -y dnf-plugins-core

# Adicionar o repositório oficial do Docker
echo "Adicionando o repositório oficial do Docker..."
dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

# Instalar Docker
echo "Instalando o Docker..."
dnf install -y docker-ce docker-ce-cli containerd.io

# Habilitar e iniciar o serviço Docker
echo "Habilitando e iniciando o serviço Docker..."
systemctl enable docker
systemctl start docker

# Verificar o status do serviço Docker
echo "Verificando o status do serviço Docker..."
systemctl status docker

# Adicionar o usuário atual ao grupo Docker
echo "Adicionando o usuário ao grupo docker..."
usermod -aG docker $USER

# Testar a instalação com um container hello-world
echo "Testando a instalação com o container hello-world..."
docker run hello-world

echo "Instalação do Docker concluída!"
echo "Lembre-se de reiniciar a sessão para que as permissões do grupo docker tenham efeito."
