# 2. Feu patate
```sh
gusta@NATHANHOAMB:~$ az vm create -g cloud-tp2_group -n cloudtp3B_feu-patate --image AlmaLinux:almalinux-x86_64:9-gen2:latest --admin-username gustave --size Standard_B2ts_v2 --location spaincentral  --ssh-key-values "ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAICUxGSGcf1uYW5mqRy//1I+dj5RHUEgy4waRTVsqeQhB gusta@NATHANHOAMB"
The default value of '--size' will be changed to 'Standard_D2s_v5' from 'Standard_DS1_v2' in a future release.
Consider upgrading security for your workloads using Azure Trusted Launch VMs. To know more about Trusted Launch, please visit https://aka.ms/TrustedLaunch.
{
  "fqdns": "",
  "id": "/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2_group/providers/Microsoft.Compute/virtualMachines/cloudtp3B_feu-patate",
  "location": "spaincentral",
  "macAddress": "7C-ED-8D-16-A8-E2",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "158.158.97.24",
  "resourceGroup": "cloud-tp2_group"
}
```

🌞 Connexion SSH
```sh
gusta@NATHANHOAMB:~$ ssh -i ~/.ssh/cloud_tp1 gustave@158.158.97.24
The authenticity of host '158.158.97.24 (158.158.97.24)' can't be established.
ED25519 key fingerprint is SHA256:rbkwLbbTUT7EhvKppNFkVyRPUk3G10Eo00E8QKwosuQ.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '158.158.97.24' (ED25519) to the list of known hosts.
[gustave@cloudtp3Bfeu-patate ~]$
```



