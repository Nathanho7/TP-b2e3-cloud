# 1. Créer le template

🌞 Let's go, balancez :
```sh
gusta@NATHANHOAMB:~$ az vm deallocate --resource-group cloud-tp2_group --name cloudtp3B_feu-patate
gusta@NATHANHOAMB:~$ az vm generalize --resource-group cloud-tp2_group --name cloudtp3B_feu-patate
gusta@NATHANHOAMB:~$ az image create \
  --resource-group cloud-tp2_group \
  --name cloudtp3-template \
  --source cloudtp3B_feu-patate \
  --location spaincentral \
  --hyper-v-generation V2
{
  "hyperVGeneration": "V2",
  "id": "/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2_group/providers/Microsoft.Compute/images/cloudtp3-template",
  "location": "spaincentral",
  "name": "cloudtp3-template",
  "provisioningState": "Succeeded",
  "resourceGroup": "cloud-tp2_group",
  "sourceVirtualMachine": {
    "id": "/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2_group/providers/Microsoft.Compute/virtualMachines/cloudtp3B_feu-patate",
    "resourceGroup": "cloud-tp2_group"
  },
  "storageProfile": {
    "dataDisks": [],
    "osDisk": {
      "caching": "ReadWrite",
      "diskSizeGB": 30,
      "managedDisk": {
        "id": "/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2_group/providers/Microsoft.Compute/disks/cloudtp3B_feu-patate_OsDisk_1_91937b2498be4cfcab7640ab68b42d79",
        "resourceGroup": "cloud-tp2_group"
      },
      "osState": "Generalized",
      "osType": "Linux",
      "storageAccountType": "Premium_LRS"
    }
  },
  "tags": {},
  "type": "Microsoft.Compute/images"
}
```
# 2. Tester le template¶
🌞 Lancer une VM à partir de votre template
```sh


