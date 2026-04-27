# Deploy do Zabbix com Docker no Ubuntu

Este guia mostra como subir a **última versão do Zabbix** em um servidor **Ubuntu** utilizando **Docker e Docker Compose**.  
A configuração garante persistência de dados no disco do host e permite que os contêineres utilizem toda a memória disponível no sistema.

---

## Pré-requisitos

Antes de começar, instale o **Docker** e o **Docker Compose** no Ubuntu.

### Atualizar sistema
```bash
1. sudo apt update && sudo apt upgrade -y

2. Instalar Docker
sudo apt install docker.io -y
sudo systemctl enable --now docker

3. Instalar Docker Compose
sudo apt install docker-compose -y

4. Adicionar usuário ao grupo Docker
sudo usermod -aG docker $USER

########

Passo a Passo
1. Criar diretório do projeto

mkdir zabbix-docker
cd zabbix-docker

# Utilizar arquivo docker-compose.yml

docker-compose up -d

Recursos Utilizados

Persistência de dados (Disco):
O diretório ./zabbix_data/postgres_data será mapeado para armazenar os dados do banco.
O limite de tamanho dependerá apenas do espaço livre no disco do host.

#

Subindo os contêineres
docker-compose up -d

Verificando status
docker-compose ps


Saída esperada:

      Name                     Command               State           Ports
-----------------------------------------------------------------------------------
postgres-zabbix     docker-entrypoint.sh postgres    Up      5432/tcp
zabbix-server       /usr/sbin/zabbix_server -c ...   Up      0.0.0.0:10051->10051/tcp
zabbix-web          /usr/sbin/nginx                  Up      0.0.0.0:8080->8080/tcp

 Acessando o Zabbix

No navegador:
http://<IP>:8080


Credenciais padrão:
Usuário: Admin
Senha: zabbix

# zbx-docker-deploy
