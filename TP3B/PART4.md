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

