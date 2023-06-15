# NextCloud com Docker Composer
Subindo servidor NextCloud com Docker Composer

Criei um composer para subir um NextCloud com tudo que é necessário.

<img src="https://temporario.aprendendolinux.com/pic_docker_hub/nextcloud.png" alt="NextCloud" width="600" title="NextCloud">

**Instale o docker com os comandos abaixo:**

```
apt update && apt -y install \
apt-transport-https \
ca-certificates curl gnupg2 \
software-properties-common

curl -fsSL https://download.docker.com/linux/debian/gpg | gpg \
--dearmor -o /etc/apt/trusted.gpg.d/docker-archive-keyring.gpg

add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"

apt update && apt install docker-ce docker-ce-cli \
containerd.io docker-compose-plugin -y
systemctl enable --now docker

curl -fsSL \
github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m) \
-o /usr/local/bin/docker-compose

chmod +x /usr/local/bin/docker-compose
apt autoremove -y && apt clean && apt clean all
```
**Agora baixe o arquivo:**

`wget https://raw.githubusercontent.com/AprendendoLinux/nextcloud/main/docker-compose.yml`

Depois de ter editado o [docker-compose.yml](https://github.com/AprendendoLinux/nextcloud/blob/main/docker-compose.yml) conforme o seu domínio, rode o comando abaixo:

`docker-compose -f /root/docker-compose.yml up -d`

**Agora acesse o endereço, conforme as explicações no arquivo:**

[](http://cloud.meudominio.com.br:8080)
**Usuario padrao:** admin@example.com
**Senha padrao:** changeme

Isso é tudo!
