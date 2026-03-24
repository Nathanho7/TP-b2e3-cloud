# V. Azure Vault¶

## 2. Do it !¶
🌞 Compléter votre plan Terraform et mettez en place une Azure Key Vault
```sh
voire keyvault.tf
+ variables.tf modif
outputs.tf modif
terraform.tfvars modif
```

## 3. Proof proof proof¶
🌞 Avec une commande az, afficher le secret
```sh
gusta@NATHANHOAMB:~/terraform-tp2-azure$ az keyvault secret show --name "gustave-secret" --vault-name "kv-gustave-kapi"
{
  "attributes": {
    "created": "2026-03-24T09:13:55+00:00",
    "enabled": true,
    "expires": null,
    "notBefore": null,
    "recoverableDays": 7,
    "recoveryLevel": "CustomizedRecoverable+Purgeable",
    "updated": "2026-03-24T09:13:55+00:00"
  },
  "contentType": "",
  "id": "https://kv-gustave-kapi.vault.azure.net/secrets/gustave-secret/ee95d8a473bc4a329a6206fad8f0974b",
  "kid": null,
  "managed": null,
  "name": "gustave-secret",
  "tags": {},
  "value": "qbSfH*470*SV)7aJ"
}
gusta@NATHANHOAMB:~/terraform-tp2-azure$
```

🌞 Depuis la VM, afficher le secret
```sh
gusta@NATHANHOAMB:~$ nano get_secret.sh
#!/bin/bash

# 1. On demande un token à Azure
TOKEN=$(curl -s -H "Metadata:true" \
  "http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://vault.azure.net" \
  | python3 -c "import sys,json; print(json.load(sys.stdin)['access_token'])")

echo "Token récupéré !"

# 2. On utilise le token pour lire le secret
SECRET=$(curl -s -H "Authorization: Bearer $TOKEN" \
  "https://kv-gustave-kapi.vault.azure.net/secrets/gustave-secret?api-version=7.0" \
  | python3 -c "import sys,json; print(json.load(sys.stdin)['value'])")

echo "The  : $SECRET"

