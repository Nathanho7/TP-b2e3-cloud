# Part II : Images

## Construisez votre propre Dockerfile

🌞 Construire votre propre image
```sh
gustave@debian:~$ mkdir ~/docker_apache && cd ~/docker_apache
gustave@debian:~/docker_apache$ cat > index.html << 'EOF'
<!DOCTYPE html>
<html>
  <body>
    <h1>That's my  Gustave Apache Server</h1>
    <p>Propulsé par Docker & Debian</p>
  </body>
</html>
EOF
gustave@debian:~/docker_apache$ cat > apache2.conf << 'EOF'
Listen 80

LoadModule mpm_event_module "/usr/lib/apache2/modules/mod_mpm_event.so"
LoadModule dir_module "/usr/lib/apache2/modules/mod_dir.so"
LoadModule authz_core_module "/usr/lib/apache2/modules/mod_authz_core.so"

DirectoryIndex index.html
DocumentRoot "/var/www/html/"

ErrorLog "logs/error.log"
LogLevel warn
EOF
gustave@debian:~/docker_apache$ cat > Dockerfile << 'EOF'
FROM debian

RUN apt update -y

RUN apt install -y apache2

COPY apache2.conf /etc/apache2/apache2.conf

COPY index.html /var/www/html/index.html

CMD [ "apache2", "-DFOREGROUND" ]
EOF
gustave@debian:~/docker_apache$ ls -la
total 20
drwxrwxr-x  2 gustave gustave 4096 20 mars  10:38 .
drwx------ 21 gustave gustave 4096 20 mars  10:37 ..
-rw-rw-r--  1 gustave gustave  315 20 mars  10:37 apache2.conf
-rw-rw-r--  1 gustave gustave  181 20 mars  10:38 Dockerfile
-rw-rw-r--  1 gustave gustave  137 20 mars  10:37 index.html
gustave@debian:~/docker_apache$
```



