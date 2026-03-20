# Part I : Docker basics

## 1. Install

🌞 Installer Docker votre machine Azure
```sh
gustave@debian:~$ sudo apt remove $(dpkg --get-selections docker.io docker-compose docker-doc podman-docker containerd runc | cut -f1)
dpkg: aucun paquet ne correspond à docker.io
dpkg: aucun paquet ne correspond à docker-compose
dpkg: aucun paquet ne correspond à docker-doc
dpkg: aucun paquet ne correspond à podman-docker
dpkg: aucun paquet ne correspond à containerd
dpkg: aucun paquet ne correspond à runc
[sudo] Mot de passe de gustave :
Sommaire :
  Mise à niveau de : 0. Installation de : 0Supprimé : 0. Non mis à jour : 0
gustave@debian:~$
gustave@debian:~$ sudo apt update
Atteint : 1 http://deb.debian.org/debian trixie InRelease
Atteint : 2 http://deb.debian.org/debian trixie-updates InRelease
Atteint : 3 http://security.debian.org/debian-security trixie-security InRelease
Tous les paquets sont à jour.
gustave@debian:~$ sudo apt install ca-certificates curl
ca-certificates est déjà la version la plus récente (20250419).
Installation de :
  curl

Sommaire :
  Mise à niveau de : 0. Installation de : 1Supprimé : 0. Non mis à jour : 0
Taille du téléchargement : 270 kB
  Espace nécessaire : 506 kB / 13,5 GB disponible

Continuer ? [O/n] O
Réception de : 1 http://deb.debian.org/debian trixie/main amd64 curl amd64 8.14.1-2+deb13u2 [270 kB]
270 ko réceptionnés en 0s (1 971 ko/s)
Sélection du paquet curl précédemment désélectionné.
(Lecture de la base de données... 139410 fichiers et répertoires déjà installés.)
Préparation du dépaquetage de .../curl_8.14.1-2+deb13u2_amd64.deb ...
Dépaquetage de curl (8.14.1-2+deb13u2) ...
Paramétrage de curl (8.14.1-2+deb13u2) ...
Traitement des actions différées (« triggers ») pour man-db (2.13.1-1) ...
gustave@debian:~$ sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
gustave@debian:~$ sudo chmod a+r /etc/apt/keyrings/docker.asc
gustave@debian:~$
gustave@debian:~$ sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/debian
Suites: $(. /etc/os-release && echo "$VERSION_CODENAME")
Components: stable
Signed-By: /etc/apt/keyrings/docker.asc
EOF

sudo apt update
Types: deb
URIs: https://download.docker.com/linux/debian
Suites: trixie
Components: stable
Signed-By: /etc/apt/keyrings/docker.asc
Atteint : 1 http://deb.debian.org/debian trixie InRelease
Atteint : 2 http://security.debian.org/debian-security trixie-security InRelease
Atteint : 3 http://deb.debian.org/debian trixie-updates InRelease
Réception de : 4 https://download.docker.com/linux/debian trixie InRelease [32,5 kB]
Réception de : 5 https://download.docker.com/linux/debian trixie/stable amd64 Packages [29,1 kB]
61,6 ko réceptionnés en 0s (178 ko/s)
Tous les paquets sont à jour.
gustave@debian:~$ sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
Installation de :
  containerd.io         docker-ce      docker-compose-plugin
  docker-buildx-plugin  docker-ce-cli

Installation de dépendances :
  docker-ce-rootless-extras  iptables       libip6tc2  pigz
  git                        liberror-perl  libslirp0  slirp4netns
  git-man                    libip4tc2      patch

Paquets suggérés :
  cgroupfs-mount       git-doc    gitk     git-mediawiki  ed
  | cgroup-lite        git-email  gitweb   git-svn        diffutils-doc
  docker-model-plugin  git-gui    git-cvs  firewalld

Sommaire :
  Mise à niveau de : 0. Installation de : 16Supprimé : 0. Non mis à jour : 0
Taille du téléchargement : 109 MB
  Espace nécessaire : 448 MB / 13,5 GB disponible

Continuer ? [O/n] O
Réception de : 1 http://deb.debian.org/debian trixie/main amd64 libip4tc2 amd64 1.8.11-2 [20,0 kB]
Réception de : 2 http://deb.debian.org/debian trixie/main amd64 libip6tc2 amd64 1.8.11-2 [20,3 kB]
Réception de : 3 http://deb.debian.org/debian trixie/main amd64 iptables amd64 1.8.11-2 [361 kB]
Réception de : 4 https://download.docker.com/linux/debian trixie/stable amd64 containerd.io amd64 2.2.2-1~debian.13~trixie [23,6 MB]
Réception de : 5 http://deb.debian.org/debian trixie/main amd64 pigz amd64 2.8-1 [62,7 kB]
Réception de : 6 http://deb.debian.org/debian trixie/main amd64 liberror-perl all 0.17030-1 [26,9 kB]
Réception de : 7 http://deb.debian.org/debian trixie/main amd64 git-man all 1:2.47.3-0+deb13u1 [2 205 kB]
Réception de : 8 http://deb.debian.org/debian trixie/main amd64 git amd64 1:2.47.3-0+deb13u1 [8 862 kB]
Réception de : 9 http://deb.debian.org/debian trixie/main amd64 libslirp0 amd64 4.8.0-1+b1 [66,4 kB]
Réception de : 10 http://deb.debian.org/debian trixie/main amd64 patch amd64 2.8-2 [134 kB]
Réception de : 11 http://deb.debian.org/debian trixie/main amd64 slirp4netns amd64 1.2.1-1.1 [39,3 kB]
Réception de : 12 https://download.docker.com/linux/debian trixie/stable amd64 docker-ce-cli amd64 5:29.3.0-1~debian.13~trixie [16,4 MB]
Réception de : 13 https://download.docker.com/linux/debian trixie/stable amd64 docker-ce amd64 5:29.3.0-1~debian.13~trixie [22,6 MB]
Réception de : 14 https://download.docker.com/linux/debian trixie/stable amd64 docker-buildx-plugin amd64 0.31.1-1~debian.13~trixie [20,3 MB]
Réception de : 15 https://download.docker.com/linux/debian trixie/stable amd64 docker-ce-rootless-extras amd64 5:29.3.0-1~debian.13~trixie [6 387 kB]
Réception de : 16 https://download.docker.com/linux/debian trixie/stable amd64 docker-compose-plugin amd64 5.1.0-1~debian.13~trixie [7 847 kB]
109 Mo réceptionnés en 4s (26,8 Mo/s)
Sélection du paquet containerd.io précédemment désélectionné.
(Lecture de la base de données... 139422 fichiers et répertoires déjà installés.)
Préparation du dépaquetage de .../00-containerd.io_2.2.2-1~debian.13~trixie_amd64.deb ...
Dépaquetage de containerd.io (2.2.2-1~debian.13~trixie) ...
Sélection du paquet docker-ce-cli précédemment désélectionné.
Préparation du dépaquetage de .../01-docker-ce-cli_5%3a29.3.0-1~debian.13~trixie_amd64.deb ...
Dépaquetage de docker-ce-cli (5:29.3.0-1~debian.13~trixie) ...
Sélection du paquet libip4tc2:amd64 précédemment désélectionné.
Préparation du dépaquetage de .../02-libip4tc2_1.8.11-2_amd64.deb ...
Dépaquetage de libip4tc2:amd64 (1.8.11-2) ...
Sélection du paquet libip6tc2:amd64 précédemment désélectionné.
Préparation du dépaquetage de .../03-libip6tc2_1.8.11-2_amd64.deb ...
Dépaquetage de libip6tc2:amd64 (1.8.11-2) ...
Sélection du paquet iptables précédemment désélectionné.
Préparation du dépaquetage de .../04-iptables_1.8.11-2_amd64.deb ...
Dépaquetage de iptables (1.8.11-2) ...
Sélection du paquet docker-ce précédemment désélectionné.
Préparation du dépaquetage de .../05-docker-ce_5%3a29.3.0-1~debian.13~trixie_amd64.deb ...
Dépaquetage de docker-ce (5:29.3.0-1~debian.13~trixie) ...
Sélection du paquet pigz précédemment désélectionné.
Préparation du dépaquetage de .../06-pigz_2.8-1_amd64.deb ...
Dépaquetage de pigz (2.8-1) ...
Sélection du paquet docker-buildx-plugin précédemment désélectionné.
Préparation du dépaquetage de .../07-docker-buildx-plugin_0.31.1-1~debian.13~trixie_amd64.deb ...
Dépaquetage de docker-buildx-plugin (0.31.1-1~debian.13~trixie) ...
Sélection du paquet docker-ce-rootless-extras précédemment désélectionné.
Préparation du dépaquetage de .../08-docker-ce-rootless-extras_5%3a29.3.0-1~debian.13~trixie_amd64.deb ...
Dépaquetage de docker-ce-rootless-extras (5:29.3.0-1~debian.13~trixie) ...
Sélection du paquet docker-compose-plugin précédemment désélectionné.
Préparation du dépaquetage de .../09-docker-compose-plugin_5.1.0-1~debian.13~trixie_amd64.deb ...
Dépaquetage de docker-compose-plugin (5.1.0-1~debian.13~trixie) ...
Sélection du paquet liberror-perl précédemment désélectionné.
Préparation du dépaquetage de .../10-liberror-perl_0.17030-1_all.deb ...
Dépaquetage de liberror-perl (0.17030-1) ...
Sélection du paquet git-man précédemment désélectionné.
Préparation du dépaquetage de .../11-git-man_1%3a2.47.3-0+deb13u1_all.deb ...
Dépaquetage de git-man (1:2.47.3-0+deb13u1) ...
Sélection du paquet git précédemment désélectionné.
Préparation du dépaquetage de .../12-git_1%3a2.47.3-0+deb13u1_amd64.deb ...
Dépaquetage de git (1:2.47.3-0+deb13u1) ...
Sélection du paquet libslirp0:amd64 précédemment désélectionné.
Préparation du dépaquetage de .../13-libslirp0_4.8.0-1+b1_amd64.deb ...
Dépaquetage de libslirp0:amd64 (4.8.0-1+b1) ...
Sélection du paquet patch précédemment désélectionné.
Préparation du dépaquetage de .../14-patch_2.8-2_amd64.deb ...
Dépaquetage de patch (2.8-2) ...
Sélection du paquet slirp4netns précédemment désélectionné.
Préparation du dépaquetage de .../15-slirp4netns_1.2.1-1.1_amd64.deb ...
Dépaquetage de slirp4netns (1.2.1-1.1) ...
Paramétrage de libip4tc2:amd64 (1.8.11-2) ...
Paramétrage de libip6tc2:amd64 (1.8.11-2) ...
Paramétrage de liberror-perl (0.17030-1) ...
Paramétrage de docker-buildx-plugin (0.31.1-1~debian.13~trixie) ...
Paramétrage de containerd.io (2.2.2-1~debian.13~trixie) ...
Created symlink '/etc/systemd/system/multi-user.target.wants/containerd.service' → '/usr/lib/systemd/system/containerd.service'.
Paramétrage de patch (2.8-2) ...
Paramétrage de docker-compose-plugin (5.1.0-1~debian.13~trixie) ...
Paramétrage de docker-ce-cli (5:29.3.0-1~debian.13~trixie) ...
Paramétrage de libslirp0:amd64 (4.8.0-1+b1) ...
Paramétrage de pigz (2.8-1) ...
Paramétrage de git-man (1:2.47.3-0+deb13u1) ...
Paramétrage de docker-ce-rootless-extras (5:29.3.0-1~debian.13~trixie) ...
Paramétrage de slirp4netns (1.2.1-1.1) ...
Paramétrage de iptables (1.8.11-2) ...
update-alternatives: utilisation de « /usr/sbin/iptables-legacy » pour fournir « /usr/sbin/iptables » (iptables) en mode automatique
update-alternatives: utilisation de « /usr/sbin/ip6tables-legacy » pour fournir « /usr/sbin/ip6tables » (ip6tables) en mode automatique
update-alternatives: utilisation de « /usr/sbin/iptables-nft » pour fournir « /usr/sbin/iptables » (iptables) en mode automatique
update-alternatives: utilisation de « /usr/sbin/ip6tables-nft » pour fournir « /usr/sbin/ip6tables » (ip6tables) en mode automatique
update-alternatives: utilisation de « /usr/sbin/arptables-nft » pour fournir « /usr/sbin/arptables » (arptables) en mode automatique
update-alternatives: utilisation de « /usr/sbin/ebtables-nft » pour fournir « /usr/sbin/ebtables » (ebtables) en mode automatique
Paramétrage de docker-ce (5:29.3.0-1~debian.13~trixie) ...
Created symlink '/etc/systemd/system/multi-user.target.wants/docker.service' → '/usr/lib/systemd/system/docker.service'.
Created symlink '/etc/systemd/system/sockets.target.wants/docker.socket' → '/usr/lib/systemd/system/docker.socket'.
Paramétrage de git (1:2.47.3-0+deb13u1) ...
Traitement des actions différées (« triggers ») pour man-db (2.13.1-1) ...
Traitement des actions différées (« triggers ») pour libc-bin (2.41-12+deb13u2) ...
gustave@debian:~$
gustave@debian:~$  sudo systemctl status docker
● docker.service - Docker Application Container Engine
     Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled; preset: e>
     Active: active (running) since Thu 2026-03-19 20:12:24 CET; 31s ago
 Invocation: 9a2fae3d7a3b412893f278ff4aa290ca
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 3287 (dockerd)
      Tasks: 11
     Memory: 30M (peak: 32.1M)
        CPU: 2.037s
     CGroup: /system.slice/docker.service
             └─3287 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/cont>

mars 19 20:12:22 debian dockerd[3287]: time="2026-03-19T20:12:22.924336381+01:0>
mars 19 20:12:23 debian dockerd[3287]: time="2026-03-19T20:12:23.176961183+01:0>
mars 19 20:12:23 debian dockerd[3287]: time="2026-03-19T20:12:23.224691415+01:0>
mars 19 20:12:24 debian dockerd[3287]: time="2026-03-19T20:12:24.752262448+01:0>
mars 19 20:12:24 debian dockerd[3287]: time="2026-03-19T20:12:24.784158889+01:0>
mars 19 20:12:24 debian dockerd[3287]: time="2026-03-19T20:12:24.784572462+01:0>
mars 19 20:12:24 debian dockerd[3287]: time="2026-03-19T20:12:24.861553973+01:0>
mars 19 20:12:24 debian dockerd[3287]: time="2026-03-19T20:12:24.882581690+01:0>
mars 19 20:12:24 debian dockerd[3287]: time="2026-03-19T20:12:24.882999715+01:0>
mars 19 20:12:24 debian systemd[1]: Started docker.service - Docker Application>

gustave@debian:~$ sudo systemctl start docker
gustave@debian:~$ sudo docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
17eec7bbc9d7: Pull complete
ea52d2000f90: Download complete
Digest: sha256:85404b3c53951c3ff5d40de0972b1bb21fafa2e8daa235355baf44f33db9dbdd
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

## 3. Lancement de conteneurs

🌞 Utiliser la commande docker run
```sh
gustave@debian:~$ docker run --name gusweb -d -p 9999:80 nginx
60b0aeab9f94dcd4ce12a235ea7ee0ac8b765ca40ecfdd13ea73e54a1db2d343
```

🌞 Rendre le service dispo sur internet
```sh
gustave@debian:~$ curl http://localhost:9999
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, nginx is successfully installed and working.
Further configuration is required for the web server, reverse proxy,
API gateway, load balancer, content cache, or other features.</p>

<p>For online documentation and support please refer to
<a href="https://nginx.org/">nginx.org</a>.<br/>
To engage with the community please visit
<a href="https://community.nginx.org/">community.nginx.org</a>.<br/>
For enterprise grade support, professional services, additional
security features and capabilities please refer to
<a href="https://f5.com/nginx">f5.com/nginx</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
gustave@debian:~$
```

🌞 Custom un peu le lancement du conteneur
```sh
gustave@debian:~$ mkdir -p ~/docker_lab/conf ~/docker_lab/html
gustave@debian:~$ cat > ~/docker_lab/conf/meow.conf << 'EOF'
server {
  listen 7777;
  root /var/www/tp_docker;
}
EOF
gustave@debian:~$ cat > ~/docker_lab/html/index.html << 'EOF'
<html>
  <body>
    <h1>🐱 Bienvenue sur le serveur meow !</h1>
  </body>
</html>
EOF
gustave@debian:~$ docker run --name meow -d \
  -p 7777:7777 \
  -v ~/docker_lab/conf/meow.conf:/etc/nginx/conf.d/meow.conf \
  -v ~/docker_lab/html:/var/www/tp_docker \
  --memory="512m" \
  nginx
7e40afeec9dd7ebef112868b3d0eaea1daa229c3f555fc8ad272890f67e9a5d5
gustave@debian:~$ curl http://localhost:7777
<html>
  <body>
    <h1>🐱 Bienvenue sur le serveur meow !</h1>
  </body>
</html>
gustave@debian:~$







gustave@debian:~$

