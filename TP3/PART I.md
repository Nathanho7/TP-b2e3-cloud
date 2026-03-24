# I. Network Security Group¶
## 2. Ajouter un NSG au déploiement

🌞 Ajouter un NSG à votre déploiement Terraform
```sh
voir ficher network.tf
```

## 3. Proofs !¶
🌞 Prouver que ça fonctionne, rendu attendu :

```sh
azurerm_virtual_network.main: Creating...
azurerm_network_security_group.main: Creating...
azurerm_public_ip.main: Creating...
azurerm_network_security_group.main: Still creating... [00m12s elapsed]
azurerm_virtual_network.main: Still creating... [00m12s elapsed]
azurerm_public_ip.main: Still creating... [00m12s elapsed]
azurerm_public_ip.main: Creation complete after 21s [id=/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Network/publicIPAddresses/vm-ip]
azurerm_virtual_network.main: Still creating... [00m22s elapsed]
azurerm_network_security_group.main: Still creating... [00m22s elapsed]
azurerm_network_security_group.main: Creation complete after 28s [id=/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Network/networkSecurityGroups/vm-nsg]
azurerm_virtual_network.main: Still creating... [00m32s elapsed]
azurerm_virtual_network.main: Creation complete after 33s [id=/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Network/virtualNetworks/vm-vnet]
azurerm_subnet.main: Creating...
azurerm_subnet.main: Still creating... [00m10s elapsed]
azurerm_subnet.main: Creation complete after 22s [id=/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Network/virtualNetworks/vm-vnet/subnets/vm-subnet]
azurerm_network_interface.main: Creating...
azurerm_network_interface.main: Still creating... [00m10s elapsed]
azurerm_network_interface.main: Creation complete after 10s [id=/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Network/networkInterfaces/vm-nic]
azurerm_network_interface_security_group_association.main: Creating...
azurerm_linux_virtual_machine.main: Creating...
azurerm_network_interface_security_group_association.main: Still creating... [00m10s elapsed]
azurerm_linux_virtual_machine.main: Still creating... [00m10s elapsed]
azurerm_network_interface_security_group_association.main: Creation complete after 19s [id=/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Network/networkInterfaces/vm-nic|/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Network/networkSecurityGroups/vm-nsg]
azurerm_linux_virtual_machine.main: Still creating... [00m22s elapsed]
azurerm_linux_virtual_machine.main: Still creating... [00m32s elapsed]
azurerm_linux_virtual_machine.main: Still creating... [00m42s elapsed]
azurerm_linux_virtual_machine.main: Still creating... [00m52s elapsed]
azurerm_linux_virtual_machine.main: Still creating... [01m02s elapsed]
azurerm_linux_virtual_machine.main: Still creating... [01m14s elapsed]
azurerm_linux_virtual_machine.main: Creation complete after 1m17s [id=/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Compute/virtualMachines/cloud-tp2-terraform]
```
- Infos de la VM 
  ```sh
  gusta@NATHANHOAMB:~/terraform-tp2-azure$ az vm show --resource-group cloud-tp2-terraform_group --name cloud-tp2-terraform --show-details
  {
    "diagnosticsProfile": {
      "bootDiagnostics": {
        "enabled": false
      }
    },
    "etag": "\"1\"",
    "extensionsTimeBudget": "PT1H30M",
    "fqdns": "",
    "hardwareProfile": {
      "vmSize": "Standard_B2ts_v2"
    },
    "id": "/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Compute/virtualMachines/cloud-tp2-terraform",
    "location": "spaincentral",
    "macAddresses": "7C-ED-8D-16-2D-D3",
    "name": "cloud-tp2-terraform",
    "networkProfile": {
      "networkInterfaces": [
        {
          "id": "/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Network/networkInterfaces/vm-nic",
          "primary": true,
          "resourceGroup": "cloud-tp2-terraform_group"
        }
      ]
    },
    "osProfile": {
      "adminUsername": "gustave",
      "allowExtensionOperations": true,
      "computerName": "cloud-tp2-terraform",
      "linuxConfiguration": {
        "disablePasswordAuthentication": true,
        "patchSettings": {
          "assessmentMode": "ImageDefault",
          "patchMode": "ImageDefault"
        },
        "provisionVMAgent": true,
        "ssh": {
          "publicKeys": [
            {
              "keyData": "ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAICUxGSGcf1uYW5mqRy//1I+dj5RHUEgy4waRTVsqeQhB gusta@NATHANHOAMB\n",
              "path": "/home/gustave/.ssh/authorized_keys"
            }
          ]
        }
      },
      "requireGuestProvisionSignal": true,
      "secrets": []
    },
    "powerState": "VM running",
    "priority": "Regular",
    "privateIps": "10.0.1.4",
    "provisioningState": "Succeeded",
    "publicIps": "68.221.64.221",
    "resourceGroup": "cloud-tp2-terraform_group",
    "storageProfile": {
      "dataDisks": [],
      "diskControllerType": "SCSI",
      "imageReference": {
        "exactVersion": "9.7.2025121501",
        "offer": "almalinux-x86_64",
        "publisher": "almalinux",
        "sku": "9-gen2",
        "version": "9.7.2025121501"
      },
      "osDisk": {
        "caching": "ReadWrite",
        "createOption": "FromImage",
        "deleteOption": "Detach",
        "diskSizeGB": 30,
        "managedDisk": {
          "id": "/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Compute/disks/vm-os-disk",
          "resourceGroup": "cloud-tp2-terraform_group",
          "storageAccountType": "Standard_LRS"
        },
        "name": "vm-os-disk",
        "osType": "Linux",
        "writeAcceleratorEnabled": false
      }
    },
    "tags": {},
    "timeCreated": "2026-03-23T23:48:32.0450228+00:00",
    "type": "Microsoft.Compute/virtualMachines",
    "vmId": "35b61f2e-7d8a-4994-ae9e-e3af314ef5c5"
  }
  ```
  - NSG
  ```sh
  gusta@NATHANHOAMB:~/terraform-tp2-azure$ az network nic show --resource-group cloud-tp2-terraform_group --name vm-nic --query "{Interface:name, NSG:networkSecurityGroup.id}" -o table
  Interface    NSG
  -----------  -----------------------------------------------------------------------------------------------------------------------------------------------------
  vm-nic       /subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Network/networkSecurityGroups/vm-nsg
  gusta@NATHANHOAMB:~/terraform-tp2-azure$
  ```

  c) SSH
  ```sh
  gusta@NATHANHOAMB:~$ ssh -i ~/.ssh/cloud_tp1 gustave@68.221.64.221
  The authenticity of host '68.221.64.221 (68.221.64.221)' can't be established.
  ED25519 key fingerprint is SHA256:IoGel4uLGaNjzsiOosAgAs2SbnTRgnlw5m4dz/LD9qw.
  This key is not known by any other names.
  Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
  Warning: Permanently added '68.221.64.221' (ED25519) to the list of known hosts.
  Enter passphrase for key '/home/gusta/.ssh/cloud_tp1':
  Enter passphrase for key '/home/gusta/.ssh/cloud_tp1':
  [gustave@cloud-tp2-terraform ~]
  ```

```sh
  Port 2222
#AddressFamily any
#ListenAddress 0.0.0.0
#ListenAddress ::

[gustave@cloud-tp2-terraform ~]$  sudo systemctl status sshd
● sshd.service - OpenSSH server daemon
     Loaded: loaded (/usr/lib/systemd/system/sshd.service; enabled; preset: enabled)
     Active: active (running) since Tue 2026-03-24 00:33:16 UTC; 3s ago
       Docs: man:sshd(8)
             man:sshd_config(5)
   Main PID: 10950 (sshd)
      Tasks: 1 (limit: 5145)
     Memory: 1.7M (peak: 2.2M)
        CPU: 9ms
     CGroup: /system.slice/sshd.service
             └─10950 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups"

[gustave@cloud-tp2-terraform ~]$ sudo ss -tulnp | grep sshd
tcp   LISTEN 0      128          0.0.0.0:2222      0.0.0.0:*    users:(("sshd",pid=10950,fd=3))
tcp   LISTEN 0      128             [::]:2222         [::]:*    users:(("sshd",pid=10950,fd=4))
```

-Connection ban NSG
```sh
gusta@NATHANHOAMB:~$ ssh -p 2222 -i ~/.ssh/cloud_tp1 gustave@68.221.64.221
ssh: connect to host 68.221.64.221 port 2222: Connection timed out
```




