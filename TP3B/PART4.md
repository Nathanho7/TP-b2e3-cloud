# Intro

Setup ur env¶
🌞 Créez une VM qui servira à créer le template

```sh
gusta@NATHANHOAMB:~$ az vm create -g cloud-tp2_group -n cloudtp3-harder --image AlmaLinux:almalinux-x86_64:9-gen2:latest --admin-username gustave --size Standard_B2ts_v2 --location spaincentral --ssh-key-values "ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAICUxGSGcf1uYW5mqRy//1I+dj5RHUEgy4waRTVsqeQhB gusta@NATHANHOAMB"
The default value of '--size' will be changed to 'Standard_D2s_v5' from 'Standard_DS1_v2' in a future release.
Consider upgrading security for your workloads using Azure Trusted Launch VMs. To know more about Trusted Launch, please visit https://aka.ms/TrustedLaunch.
{
  "fqdns": "",
  "id": "/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2_group/providers/Microsoft.Compute/virtualMachines/cloudtp3-harder",
  "location": "spaincentral",
  "macAddress": "7C-ED-8D-16-86-8F",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.6",
  "publicIpAddress": "158.158.96.202",
  "resourceGroup": "cloud-tp2_group"
}
```
```sh
gusta@NATHANHOAMB:~$ ssh -i ~/.ssh/cloud_tp1 gustave@158.158.96.202
The authenticity of host '158.158.96.202 (158.158.96.202)' can't be established.
ED25519 key fingerprint is SHA256:qBYycvAYKfmyix2itEvwHEH5tbIYA/RXOgBiweZlD00.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
gusta@NATHANHOAMB:~$ ssh -i ~/.ssh/cloud_tp1 gustave@158.158.96.202
[gustave@cloudtp3-harder ~]$
```

## Part4 - A. Firewalling baby

🌞 Firewall conf
```sh
[gustave@cloudtp3-harder ~]$ sudo systemctl status firewalld
● firewalld.service - firewalld - dynamic firewall daemon
     Loaded: loaded (/usr/lib/systemd/system/firewalld.service; enabled; preset: enabled)
     Active: active (running) since Tue 2026-03-24 14:42:42 UTC; 13min ago
       Docs: man:firewalld(1)
   Main PID: 10451 (firewalld)
      Tasks: 4 (limit: 5172)
     Memory: 29.7M (peak: 36.9M)
        CPU: 2.864s
     CGroup: /system.slice/firewalld.service
             └─10451 /usr/bin/python3 -s /usr/sbin/firewalld --nofork --nopid

Mar 24 14:42:42 cloudtp3-harder systemd[1]: Starting firewalld - dynamic firewall daemon...
Mar 24 14:42:42 cloudtp3-harder systemd[1]: Started firewalld - dynamic firewall daemon.
Mar 24 14:44:46 cloudtp3-harder firewalld[10451]: WARNING: ZONE_ALREADY_SET: public
Mar 24 14:47:01 cloudtp3-harder firewalld[10451]: WARNING: ZONE_ALREADY_SET: public
Mar 24 14:47:02 cloudtp3-harder firewalld[10451]: WARNING: ALREADY_ENABLED: 22:tcp
Mar 24 14:48:53 cloudtp3-harder firewalld[10451]: WARNING: ALREADY_ENABLED: 22:tcp
Mar 24 14:53:00 cloudtp3-harder systemd[1]: Started firewalld - dynamic firewall daemon.
Mar 24 14:53:09 cloudtp3-harder firewalld[10451]: WARNING: NOT_ENABLED: ssh
Mar 24 14:53:09 cloudtp3-harder firewalld[10451]: WARNING: NOT_ENABLED: dhcpv6-client
Mar 24 14:55:35 cloudtp3-harder systemd[1]: Started firewalld - dynamic firewall daemon.
[gustave@cloudtp3-harder ~]$
```

- conf
  ```sh
  [gustave@cloudtp3-harder ~]$ sudo firewall-cmd --permanent --add-port=22/tcp
  success
  [gustave@cloudtp3-harder ~]$ sudo firewall-cmd --reload
  success
  [gustave@cloudtp3-harder ~]$ sudo firewall-cmd --list-all
  public (active)
    target: default
    icmp-block-inversion: no
    interfaces: eth0
    sources:
    services:
    ports: 22/tcp
    protocols:
    forward: yes
    masquerade: no
    forward-ports:
    source-ports:
    icmp-blocks:
    rich rules:
  [gustave@cloudtp3-harder ~]$
  ```

# Part4 - B. Stronk SSH

🌞 Proposez une conf OpenSSH forte
```sh
[gustave@cloudtp3-harder ~]$ sudo vi /etc/ssh/sshd_config
Port 22
Protocol 2
LogLevel VERBOSE
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
PermitEmptyPasswords no
AllowUsers gustave
MaxAuthTries 3
LoginGraceTime 30
ClientAliveInterval 0
ClientAliveCountMax 2
UseDNS no
X11Forwarding no
Subsystem sftp internal-sftp
```

# Part4 - C. fail2ban

🌞 Installer et configurer fail2ban
```sh
[gustave@cloudtp3-harder ~]$ sudo vi /etc/fail2ban/jail.d/sshd.conf
[sshd]
enabled = true
port    = 22
filter  = sshd
backend = systemd
maxretry = 2
findtime = 3600
bantime  = -1
```
```sh
[gustave@cloudtp3-harder ~]$ sudo systemctl enable --now fail2ban
Created symlink /etc/systemd/system/multi-user.target.wants/fail2ban.service → /usr/lib/systemd/system/fail2ban.service.
[gustave@cloudtp3-harder ~]$ sudo systemctl status fail2ban
● fail2ban.service - Fail2Ban Service
     Loaded: loaded (/usr/lib/systemd/system/fail2ban.service; enabled; preset: disabled)
     Active: active (running) since Tue 2026-03-24 15:30:10 UTC; 6s ago
       Docs: man:fail2ban(1)
    Process: 49471 ExecStartPre=/bin/mkdir -p /run/fail2ban (code=exited, status=0/SUCCESS)
   Main PID: 49472 (fail2ban-server)
      Tasks: 5 (limit: 5172)
     Memory: 17.2M (peak: 38.8M)
        CPU: 263ms
     CGroup: /system.slice/fail2ban.service
             └─49472 /usr/bin/python3 -s /usr/bin/fail2ban-server -xf start

Mar 24 15:30:10 cloudtp3-harder systemd[1]: Starting Fail2Ban Service...
Mar 24 15:30:10 cloudtp3-harder systemd[1]: Started Fail2Ban Service.
Mar 24 15:30:10 cloudtp3-harder fail2ban-server[49472]: Server ready
[gustave@cloudtp3-harder ~]$
```
🌞 Prouvez que fail2ban fonctionne

-Me suis fait ban 
```sh
gusta@NATHANHOAMB:~$ ssh -i ~/.ssh/cloud_tp1 gustave@158.158.96.202
ssh: connect to host 158.158.96.202 port 22: Connection timed out
```

# Part4 - D. Harden kernel parameters

## 2. Setup¶
🌞 Proposer une conf sysctl
```sh





