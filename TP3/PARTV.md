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
    "created": "2026-03-24T09:48:16+00:00",
    "enabled": true,
    "expires": null,
    "notBefore": null,
    "recoverableDays": 7,
    "recoveryLevel": "CustomizedRecoverable+Purgeable",
    "updated": "2026-03-24T09:48:16+00:00"
  },
  "contentType": null,
  "id": "https://kv-gustave-kapi.vault.azure.net/secrets/gustave-secret/3381d3f7c2f94a908c11a4c9a1389bf5",
  "kid": null,
  "managed": null,
  "name": "gustave-secret",
  "tags": {
    "file-encoding": "utf-8"
  },
  "value": "spiderman Brand New Day yeah"
}
```

🌞 Depuis la VM, afficher le secret
```sh
[gustave@cloud-tp2-terraform ~]$ vi gustave_secret.sh
#!/bin/bash

TOKEN=$(curl -s -H "Metadata:true" \
  "http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://vault.azure.net" \
  | python3 -c "import sys,json; print(json.load(sys.stdin)['access_token'])")

SECRET=$(curl -s -H "Authorization: Bearer $TOKEN" \
  "https://kv-gustave-kapi.vault.azure.net/secrets/gustave-secret?api-version=7.0" \
  | python3 -c "import sys,json; print(json.load(sys.stdin)['value'])")

echo "The Beuatiful Secret is : $SECRET"
```

```sh
[gustave@cloud-tp2-terraform ~]$ ./gustave_secret.sh
The Beuatiful Secret is : spiderman Brand New Day yeah
```



