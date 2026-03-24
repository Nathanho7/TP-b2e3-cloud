```sh
output "vm_public_ip" {
  value       = azurerm_public_ip.main.ip_address
  description = "IP publique de la VM"
}

output "vm_dns_name" {
  value       = azurerm_public_ip.main.fqdn
  description = "Nom DNS de la VM"
}

output "vm_ssh_command" {
  value       = "ssh -p 2222 ${var.admin_username}@${azurerm_public_ip.main.fqdn}"
  description = "Commande SSH prête à copier"
}

output "secret_value" {
  value       = random_password.main.result
  sensitive   = true
  description = "Valeur du secret généré dans la Key Vault"
}
```
