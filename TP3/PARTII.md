# II. Un ptit nom DNS

## 1. Adapter le plan Terraform¶
🌞 Donner un nom DNS à votre VM

```sh
azurerm_public_ip.main: Modifying... [id=/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Network/publicIPAddresses/vm-ip]
azurerm_public_ip.main: Modifications complete after 9s [id=/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Network/publicIPAddresses/vm-ip]
```

## 2. Ajouter un output custom à terraform apply¶
🌞 Un ptit output nan ?

```sh
gusta@NATHANHOAMB:~/terraform-tp2-azure$ nano outputs.tf
output "vm_public_ip" {
  value       = azurerm_public_ip.main.ip_address
  description = "IP publique de la VM"
}

output "vm_dns_name" {
  value       = azurerm_public_ip.main.fqdn
  description = "Nom DNS de la VM"
}

output "vm_ssh_command" {
  value       = "ssh ${var.admin_username}@${azurerm_public_ip.main.fqdn}"
  description = "Commande SSH prête à copier"
}
```

## 3. Proooofs !¶
🌞 Proofs ! Donnez moi :
- terraform apply
```sh
gusta@NATHANHOAMB:~/terraform-tp2-azure$ terraform apply
azurerm_resource_group.main: Refreshing state... [id=/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group]
azurerm_public_ip.main: Refreshing state... [id=/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Network/publicIPAddresses/vm-ip]
azurerm_virtual_network.main: Refreshing state... [id=/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Network/virtualNetworks/vm-vnet]
azurerm_network_security_group.main: Refreshing state... [id=/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Network/networkSecurityGroups/vm-nsg]
azurerm_subnet.main: Refreshing state... [id=/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Network/virtualNetworks/vm-vnet/subnets/vm-subnet]
azurerm_network_interface.main: Refreshing state... [id=/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Network/networkInterfaces/vm-nic]
azurerm_network_interface_security_group_association.main: Refreshing state... [id=/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Network/networkInterfaces/vm-nic|/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Network/networkSecurityGroups/vm-nsg]
azurerm_linux_virtual_machine.main: Refreshing state... [id=/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Compute/virtualMachines/cloud-tp2-terraform]

Changes to Outputs:
  + vm_dns_name    = "cloud-tp2-gustave.spaincentral.cloudapp.azure.com"
  + vm_public_ip   = "68.221.64.221"
  + vm_ssh_command = "ssh gustave@cloud-tp2-gustave.spaincentral.cloudapp.azure.com"

You can apply this plan to save these new output values to the Terraform state, without changing
any real infrastructure.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes


Apply complete! Resources: 0 added, 0 changed, 0 destroyed.

Outputs:

vm_dns_name = "cloud-tp2-gustave.spaincentral.cloudapp.azure.com"
vm_public_ip = "68.221.64.221"
vm_ssh_command = "ssh gustave@cloud-tp2-gustave.spaincentral.cloudapp.azure.com"
```

- Commande ssh
   ```sh
   gusta@NATHANHOAMB:~$ ssh -p 2222 gustave@cloud-tp2-gustave.spaincentral.cloudapp.azure.com
  The authenticity of host '[cloud-tp2-gustave.spaincentral.cloudapp.azure.com]:2222 ([68.221.64.221]:2222)' can't be established.
  ED25519 key fingerprint is SHA256:IoGel4uLGaNjzsiOosAgAs2SbnTRgnlw5m4dz/LD9qw.
  This host key is known by the following other names/addresses:
      ~/.ssh/known_hosts:34: [hashed name]
  Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
  Warning: Permanently added '[cloud-tp2-gustave.spaincentral.cloudapp.azure.com]:2222' (ED25519) to the list of known hosts.
  Last login: Tue Mar 24 00:19:29 2026 from 176.159.167.242
  [gustave@cloud-tp2-terraform ~]$
```
  




