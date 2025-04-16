# Docker: Utilização prática no cenário de Microsserviços

## Instalação do Docker no Ubuntu
- Ref.: [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)
- Passos para a instalação:
1) Desinstalar todos os pacotes que causam conflito.
```Shell
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```
2) Instalar usando o repositório `apt`
```Shell
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```
3) Instalar a versão mais recente do pacote docker
```Shell
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
4) Verificar se a instalação foi concluida corretamente
```Shell
sudo docker run hello-world
```

## Script para criar os containers do banco de dados e da aplciação
```Shell

docker run --name mysql-container -e MYSQL_ROOT_PASSWORD=senha123 -e MYSQL_DATABASE=meubanco -e MYSQL_USER=tiago -e MYSQL_PASSWORD=senha123 -d mysql:latest


docker run --name web-server -dt -p 80:80 --mount type=volume,src=app,dst=/app/ webdevops/php-apache:alpine-php7
```
