
 # network.tf
 
 ```sh         
resource "azurerm_network_security_group" "main" {
  name                = "vm-nsg"
  location            = azurerm_resource_group.main.location
  resource_group_name = azurerm_resource_group.main.name

  security_rule {
    name                       = "allow-ssh-from-home"
    priority                   = 100
    direction                  = "Inbound"
    access                     = "Allow"
    protocol                   = "Tcp"
    source_port_range          = "*"
    destination_port_range     = "22"
    source_address_prefix      = var.my_public_ip
    destination_address_prefix = "*"
  }
}

resource "azurerm_network_interface_security_group_associatio>
  network_interface_id      = azurerm_network_interface.main.>
  network_security_group_id = azurerm_network_security_group.>
}
```
