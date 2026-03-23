# I. Prérequis

## 2. Une paire de clés SSH

### A. Choix de l'algorithme de chiffrement

🌞 Déterminer quel algorithme de chiffrement utiliser pour vos clés

```sh
Algorithme choisi : Ed25519

[N0 TO RSA] (https://blog.vitalvas.com/post/2025/03/01/comparing-ssh-keys-rsa-ecdsa-ed25519/)

[YES TO Ed25519] (https://dev.to/ccoveille/how-to-generate-a-secure-and-robust-ssh-key-in-2024-3f4f)
```

## B. Génération de votre paire de clés¶
🌞 Générer une paire de clés pour ce TP

```sh
gusta@NATHANHOAMB:~$ ssh-keygen -t ed25519 -f ~/.ssh/cloud_tp1 -C "cloud_tp1_key"
Generating public/private ed25519 key pair.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/gusta/.ssh/cloud_tp1
Your public key has been saved in /home/gusta/.ssh/cloud_tp1.pub
The key fingerprint is:
SHA256:8doKCMwyfTYclStchhinVgSs9/Zrk54066Lcx4xumSY cloud_tp1_key
The key's randomart image is:
+--[ED25519 256]--+
| .o=+...         |
|  o+..+          |
| .o..o ..        |
|.=..o..  o       |
|o.=.=.  S .      |
| o +oo   o       |
|   ..B+.. .      |
| .E.B.O= .       |
|  o*o**o.        |
+----[SHA256]-----+
gusta@NATHANHOAMB:~$ ls -la ~/.ssh/
total 36
drwx------ 2 gusta gusta 4096 Mar 23 11:53 .
drwxr-x--- 8 gusta gusta 4096 Mar 23 11:36 ..
-rw------- 1 gusta gusta  444 Mar 23 11:53 cloud_tp1
-rw-r--r-- 1 gusta gusta   95 Mar 23 11:53 cloud_tp1.pub
-rw-r--r-- 1 gusta gusta  115 Nov  4 08:21 config
-rw------- 1 gusta gusta 6846 Nov  4 09:41 known_hosts
-rw------- 1 gusta gusta 6010 Nov  4 09:40 known_hosts.old
gusta@NATHANHOAMB:~$
```

## C. Agent SSH
🌞 Configurer un agent SSH sur votre poste
```sh
# SSH Agent

if ! pgrep -u "$USER" ssh-agent > /dev/null; then
    ssh-agent -t 1h > "$HOME/.ssh/agent-environment"
fi
if [ ! -f "$SSH_AUTH_SOCK" ]; then
    source "$HOME/.ssh/agent-environment" > /dev/null
fi
```
```sh
Explication : 
pgrep -u "$USER" ssh-agent	Vérifie l'agent SSH tourne déjà pour mon user
ssh-agent -t 1h	vas demarrer l'agent avec un timeout de 1h (en gros clé oubliée après 1h)
> "$HOME/.ssh/agent-environment"	Sauvegarde les variables d'env (SSH_AUTH_SOCK, SSH_AGENT_PID) dans un fichier
source "$HOME/.ssh/agent-environment"	Charge ces variables dans le shell si l'agent tourne déjà
```








