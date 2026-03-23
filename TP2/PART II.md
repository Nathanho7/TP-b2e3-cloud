# II. Spawn des VMs

### 1. Depuis la WebUI

🌞 Connectez-vous en SSH à la VM pour preuve
```sh
gusta@NATHANHOAMB:~$ ssh -i ~/.ssh/cloud_tp1 gustave@68.221.16.139
The authenticity of host '68.221.16.139 (68.221.16.139)' can't be established.
ED25519 key fingerprint is SHA256:7kuhE8lkaHmTbvNPSKHifTlJpRojEI+2V5OB9ednndM.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '68.221.16.139' (ED25519) to the list of known hosts.
Enter passphrase for key '/home/gusta/.ssh/cloud_tp1':
Welcome to Ubuntu 24.04.4 LTS (GNU/Linux 6.17.0-1008-azure x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Mon Mar 23 13:14:54 UTC 2026

  System load:  0.08              Processes:             137
  Usage of /:   5.7% of 28.02GB   Users logged in:       0
  Memory usage: 34%               IPv4 address for eth0: 10.0.0.4
  Swap usage:   0%

Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


The list of available updates is more than a week old.
To check for new updates run: sudo apt update


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

gustave@cloud-tp2:~$
```
```sh
az>> az vm create -g cloud-tp2_group -n cloud-tp2-alma --image AlmaLinux:almalinux-x86_64:9-gen2:latest --admin-username gustave --size Standard_B2ts_v2 --location spaincentral --ssh-key-values "ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAICUxGSGcf1uYW5mqRy//1I+dj5RHUEgy4waRTVsqeQhB gusta@NATHANHOAMB"
Consider upgrading security for your workloads using Azure Trusted Launch VMs. To know more about Trusted Launch, please visit https://aka.ms/TrustedLaunch.
{
  "fqdns": "",
  "id": "/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2_group/providers/Microsoft.Compute/virtualMachines/cloud-tp2-alma",
  "location": "spaincentral",
  "macAddress": "70-A8-A5-23-F2-20",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.5",
  "publicIpAddress": "158.158.72.161",
  "resourceGroup": "cloud-tp2_group"
}
az>>
```

🌞 Assurez-vous que vous pouvez vous connecter à la VM en SSH sur son IP publique
```sh
gusta@NATHANHOAMB:~$ ssh -i ~/.ssh/cloud_tp1 gustave@158.158.72.161
The authenticity of host '158.158.72.161 (158.158.72.161)' can't be established.
ED25519 key fingerprint is SHA256:6PikCXRz0qE24XIQyQGXgoJv0tefnaa4roapNgYit88.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '158.158.72.161' (ED25519) to the list of known hosts.
[gustave@cloud-tp2-alma ~]$
```

🌞 Une fois connecté, prouvez la présence...
```sh
[gustave@cloud-tp2-alma ~]$  systemctl status waagent.service
● waagent.service - Azure Linux Agent
     Loaded: loaded (/usr/lib/systemd/system/waagent.service; enabled; preset: disabled)
     Active: active (running) since Mon 2026-03-23 14:40:34 UTC; 7min ago
   Main PID: 1274 (python3)
      Tasks: 6 (limit: 5172)
     Memory: 41.1M (peak: 45.8M)
        CPU: 1.655s
     CGroup: /azure.slice/waagent.service
             ├─1274 /usr/bin/python3 -u /usr/sbin/waagent -daemon
             └─1397 /usr/bin/python3 -u bin/WALinuxAgent-2.15.0.1-py3.12.egg -run-exthandlers

Mar 23 14:40:37 cloud-tp2-alma python3[1397]: 2: eth0    inet6 fe80::72a8:a5ff:fe23:f220/64 sco>
Mar 23 14:40:37 cloud-tp2-alma python3[1397]: 2026-03-23T14:40:37.983551Z WARNING EnvHandler Ex>
Mar 23 14:40:37 cloud-tp2-alma python3[1397]: 2026-03-23T14:40:37.984567Z INFO ExtHandler ExtHa>
Mar 23 14:40:37 cloud-tp2-alma python3[1397]: 2026-03-23T14:40:37.993118Z INFO EnvHandler ExtHa>
Mar 23 14:40:38 cloud-tp2-alma python3[1397]: 2026-03-23T14:40:38.017490Z INFO ExtHandler ExtHa>
Mar 23 14:40:38 cloud-tp2-alma python3[1397]: 2026-03-23T14:40:38.017585Z INFO ExtHandler ExtHa>
Mar 23 14:40:38 cloud-tp2-alma python3[1397]: 2026-03-23T14:40:38.017883Z INFO ExtHandler ExtHa>
Mar 23 14:40:38 cloud-tp2-alma python3[1397]: 2026-03-23T14:40:38.018306Z INFO ExtHandler ExtHa>
Mar 23 14:40:38 cloud-tp2-alma python3[1397]: 2026-03-23T14:40:38.033908Z INFO ExtHandler ExtHa>
Mar 23 14:40:38 cloud-tp2-alma python3[1397]: 2026-03-23T14:40:38.036527Z INFO ExtHandler ExtHa>
lines 1-21/21 (END)
```

- ...du service cloud-init.service
```sh
[gustave@cloud-tp2-alma ~]$  systemctl status cloud-init.service
● cloud-init.service - Cloud-init: Network Stage
     Loaded: loaded (/usr/lib/systemd/system/cloud-init.service; enabled; preset: disabled)
     Active: active (exited) since Mon 2026-03-23 14:40:34 UTC; 8min ago
   Main PID: 957 (code=exited, status=0/SUCCESS)
      Tasks: 0 (limit: 5172)
     Memory: 5.2M (peak: 41.4M)
        CPU: 609ms
     CGroup: /system.slice/cloud-init.service

Mar 23 14:40:34 cloud-tp2-alma cloud-init[978]: |=.+.             |
Mar 23 14:40:34 cloud-tp2-alma cloud-init[978]: |.+. ...          |
Mar 23 14:40:34 cloud-tp2-alma cloud-init[978]: |. +o.+.o         |
Mar 23 14:40:34 cloud-tp2-alma cloud-init[978]: | oo.X +.So .     |
Mar 23 14:40:34 cloud-tp2-alma cloud-init[978]: |+..= B  o +      |
Mar 23 14:40:34 cloud-tp2-alma cloud-init[978]: |+..+. o. o       |
Mar 23 14:40:34 cloud-tp2-alma cloud-init[978]: | ++o.=. .        |
Mar 23 14:40:34 cloud-tp2-alma cloud-init[978]: |+..oEo+.         |
Mar 23 14:40:34 cloud-tp2-alma cloud-init[978]: +----[SHA256]-----+
Mar 23 14:40:34 cloud-tp2-alma systemd[1]: Finished Cloud-init: Network Stage.
[gustave@cloud-tp2-alma ~]$
```

## 3. Terraforming planets infrastructures
🌞 Utilisez Terraform pour créer une VM dans Azure
```sh
-> Voir ficher main.tf
azurerm_resource_group.main: Creating...
azurerm_resource_group.main: Still creating... [00m11s elapsed]
azurerm_resource_group.main: Still creating... [00m21s elapsed]
azurerm_resource_group.main: Still creating... [00m31s elapsed]
azurerm_resource_group.main: Creation complete after 39s [id=/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group]
azurerm_virtual_network.main: Creating...
azurerm_public_ip.main: Creating...
azurerm_virtual_network.main: Still creating... [00m10s elapsed]
azurerm_public_ip.main: Still creating... [00m10s elapsed]
azurerm_public_ip.main: Creation complete after 14s [id=/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Network/publicIPAddresses/vm-ip]
azurerm_virtual_network.main: Creation complete after 17s [id=/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Network/virtualNetworks/vm-vnet]
azurerm_subnet.main: Creating...
azurerm_subnet.main: Still creating... [00m10s elapsed]
azurerm_subnet.main: Creation complete after 17s [id=/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Network/virtualNetworks/vm-vnet/subnets/vm-subnet]
azurerm_network_interface.main: Creating...
azurerm_network_interface.main: Creation complete after 10s [id=/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Network/networkInterfaces/vm-nic]
azurerm_linux_virtual_machine.main: Creating...
azurerm_linux_virtual_machine.main: Still creating... [00m10s elapsed]
azurerm_linux_virtual_machine.main: Still creating... [00m21s elapsed]
azurerm_linux_virtual_machine.main: Still creating... [00m31s elapsed]
azurerm_linux_virtual_machine.main: Still creating... [00m41s elapsed]
azurerm_linux_virtual_machine.main: Still creating... [00m52s elapsed]
azurerm_linux_virtual_machine.main: Still creating... [01m02s elapsed]
azurerm_linux_virtual_machine.main: Creation complete after 1m6s [id=/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Compute/virtualMachines/cloud-tp2-terraform]

Apply complete! Resources: 6 added, 0 changed, 0 destroyed.
```

🌞 Prouvez avec une connexion SSH sur l'IP publique que la VM est up
```sh
gusta@NATHANHOAMB:~$ ssh gustave@158.158.42.28 -i ~/.ssh/cloud_tp1
Enter passphrase for key '/home/gusta/.ssh/cloud_tp1':
Last login: Mon Mar 23 16:30:17 2026 from 176.159.167.242
[gustave@cloud-tp2-terraform ~]$
```





