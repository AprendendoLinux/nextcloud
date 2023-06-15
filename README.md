# NextCloud com Docker Composer
Subindo servidor NextCloud com Docker Composer

Criei um composer para subir um NextCloud com tudo que é necessário.

<img src="https://temporario.aprendendolinux.com/pic_docker_hub/nextcloud.png" alt="NextCloud" width="500" title="NextCloud">

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

http://cloud.meudominio.com.br:8080<br>
**Usuário padrão:** admin@example.com<br>
**Senha padrãoo:** changeme

Faça as devidas alterações, adicione o proxy host, adicione o SSL e na guia "Advanced", adicione o seguinte conteúdo:

```
client_body_buffer_size 512k;
proxy_read_timeout 86400s;
client_max_body_size 0;

location /.well-known/carddav {
return 301 $scheme://$host/remote.php/dav;
}

location /.well-known/caldav {
return 301 $scheme://$host/remote.php/dav;
}

location /.well-known/webfinger {
return 301 $scheme://$host/index.php/.well-known/webfinger;
}

location /.well-known/nodeinfo {
return 301 $scheme://$host/index.php/.well-known/nodeinfo;
}
```
Agora, no Linux, rode o seguinte comando:

`docker exec --user www-data -it nextcloud php occ config:system:set default_phone_region --value="BR"`

Tudo pronto! Basta acessar o servidor agora:

https://cloud.meudominio.com.br<br>
**Usuário:** admin<br>
**Senha:** admin

Isso é tudo!
