# 1. Poser notre conf custom

🌞 Effectuez la conf suivante 

- mise à jour
  ```sh
    ==========================================================================================================================================================================================
   Package                                          Architecture                               Version                                     Repository                                  Size
  ==========================================================================================================================================================================================
  Installing:
   epel-release                                     noarch                                     9-9.el9                                     extras                                      18 k
  
  Transaction Summary
  ==========================================================================================================================================================================================
  Install  1 Package
  
  Total download size: 18 k
  Installed size: 26 k
  Downloading Packages:
  epel-release-9-9.el9.noarch.rpm                                                                                                                           115 kB/s |  18 kB     00:00
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Total                                                                                                                                                      41 kB/s |  18 kB     00:00
  Running transaction check
  Transaction check succeeded.
  Running transaction test
  Transaction test succeeded.
  Running transaction
    Preparing        :                                                                                                                                                                  1/1
    Installing       : epel-release-9-9.el9.noarch                                                                                                                                      1/1
    Running scriptlet: epel-release-9-9.el9.noarch                                                                                                                                      1/1
  Many EPEL packages require the CodeReady Builder (CRB) repository.
  It is recommended that you run /usr/bin/crb enable to enable the CRB repository.
  
    Verifying        : epel-release-9-9.el9.noarch                                                                                                                                      1/1
  
  Installed:
    epel-release-9-9.el9.noarch
  
  Complete!
```
```sh
[gustave@cloudtp3Bfeu-patate ~]$ htop --version
htop 3.3.0
[gustave@cloudtp3Bfeu-patate ~]$ htop --version
htop 3.3.0
[gustave@cloudtp3Bfeu-patate ~]$ dig -v
DiG 9.16.23-RH
[gustave@cloudtp3Bfeu-patate ~]$ ping google.com
PING google.com (142.251.140.238) 56(84) bytes of data.
64 bytes from lcmada-ab-in-f14.1e100.net (142.251.140.238): icmp_seq=1 ttl=117 time=0.773 ms
64 bytes from dia01s03-in-f14.1e100.net (142.251.140.238): icmp_seq=2 ttl=117 time=0.660 ms
64 bytes from dia01s03-in-f14.1e100.net (142.251.140.238): icmp_seq=3 ttl=117 time=0.612 ms
^C
--- google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2002ms
rtt min/avg/max/mdev = 0.612/0.681/0.773/0.067 ms
```

## 2. Clean la VM

### A. Réinitiliser cloud-init¶
🌞 Go lancer ça :
```sh
[gustave@cloudtp3Bfeu-patate ~]$ sudo cloud-init clean --logs
[gustave@cloudtp3Bfeu-patate ~]$ sudo rm -rf /var/lib/cloud/*
[gustave@cloudtp3Bfeu-patate ~]$ sudo systemctl enable cloud-init
[gustave@cloudtp3Bfeu-patate ~]$
```

# B. Clean le système

🌞 Proposer une suite de commandes

```sh
[gustave@cloudtp3Bfeu-patate ~]$ sudo rm -rf /var/log/*
[gustave@cloudtp3Bfeu-patate ~]$ history -c
```


