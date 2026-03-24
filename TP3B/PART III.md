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
gusta@NATHANHOAMB:~$ az vm create -g cloud-tp2_group -n haaland-cloudtp3   --image cloudtp3-template   --admin-username gustave   --ssh-key-values "ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAICUxGSGcf1uYW5mqRy//1I+dj5RHUEgy4waRTVsqeQhB gusta@NATHANHOAMB"  --size Standard_B2ts_v2  --location spaincentral
The default value of '--size' will be changed to 'Standard_D2s_v5' from 'Standard_DS1_v2' in a future release.
{
  "fqdns": "",
  "id": "/subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2_group/providers/Microsoft.Compute/virtualMachines/haaland-cloudtp3",
  "location": "spaincentral",
  "macAddress": "7C-ED-8D-64-9B-B1",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.5",
  "publicIpAddress": "158.158.43.255",
  "resourceGroup": "cloud-tp2_group"
}
```
🌞 Vérification !
```sh
[gustave@haaland-cloudtp3 ~]$ cloud-init status
status: done
[gustave@haaland-cloudtp3 ~]$ sudo tail -20 /var/log/cloud-init.log
2026-03-24 11:16:54,225 - handlers.py[DEBUG]: start: modules-final/config-final_message: running config-final_message with frequency always
2026-03-24 11:16:54,225 - helpers.py[DEBUG]: Running config-final_message using lock (<cloudinit.helpers.DummyLock object at 0x7f3d41e1d3d0>)
2026-03-24 11:16:54,226 - util.py[DEBUG]: Reading from /proc/uptime (quiet=False)
2026-03-24 11:16:54,226 - util.py[DEBUG]: Reading 12 bytes from /proc/uptime
2026-03-24 11:16:54,237 - performance.py[DEBUG]: Rendering jinja2 template took 0.012 seconds
2026-03-24 11:16:54,238 - log_util.py[DEBUG]: Cloud-init v. 24.4-7.el9_7.1.alma.1 finished at Tue, 24 Mar 2026 11:16:54 +0000. Datasource DataSourceAzure [seed=/dev/sr0].  Up 21.42 seconds
2026-03-24 11:16:54,238 - util.py[DEBUG]: Writing to /var/lib/cloud/instance/boot-finished - wb: [644] 67 bytes
2026-03-24 11:16:54,251 - util.py[DEBUG]: Restoring selinux mode for /var/lib/cloud/instances/9df861a1-eb8d-4819-9346-40fbb596c845/boot-finished (recursive=False)
2026-03-24 11:16:54,252 - util.py[DEBUG]: Restoring selinux mode for /var/lib/cloud/instances/9df861a1-eb8d-4819-9346-40fbb596c845/boot-finished (recursive=False)
2026-03-24 11:16:54,252 - performance.py[DEBUG]: Writing file took 0.015 seconds
2026-03-24 11:16:54,252 - handlers.py[DEBUG]: finish: modules-final/config-final_message: SUCCESS: config-final_message ran successfully and took 0.027 seconds
2026-03-24 11:16:54,253 - main.py[DEBUG]: Ran 10 modules with 0 failures
2026-03-24 11:16:54,253 - util.py[DEBUG]: Reading from /proc/uptime (quiet=False)
2026-03-24 11:16:54,253 - util.py[DEBUG]: Reading 12 bytes from /proc/uptime
2026-03-24 11:16:54,253 - atomic_helper.py[DEBUG]: Atomically writing to file /var/lib/cloud/data/status.json (via temporary file /var/lib/cloud/data/tmp7nk_eq1u) - w: [644] 520 bytes/chars
2026-03-24 11:16:54,253 - atomic_helper.py[DEBUG]: Atomically writing to file /var/lib/cloud/data/result.json (via temporary file /var/lib/cloud/data/tmpekjw40gt) - w: [644] 82 bytes/chars
2026-03-24 11:16:54,254 - util.py[DEBUG]: Creating symbolic link from '/run/cloud-init/result.json' => '../../var/lib/cloud/data/result.json'
2026-03-24 11:16:54,254 - performance.py[DEBUG]: cloud-init stage: 'modules-final' took 0.303 seconds
2026-03-24 11:16:54,254 - handlers.py[DEBUG]: finish: modules-final: SUCCESS: running modules for final
2026-03-24 11:16:54,254 - handlers.py[DEBUG]: HyperVReportingHandler flushing remaining events
[gustave@haaland-cloudtp3 ~]$ sudo systemctl status waagent
● waagent.service - Azure Linux Agent
     Loaded: loaded (/usr/lib/systemd/system/waagent.service; enabled; preset: disabled)
     Active: active (running) since Tue 2026-03-24 11:16:53 UTC; 4min 26s ago
   Main PID: 1269 (python3)
      Tasks: 6 (limit: 3906)
     Memory: 42.7M (peak: 47.2M)
        CPU: 1.787s
     CGroup: /azure.slice/waagent.service
             ├─1269 /usr/bin/python3 -u /usr/sbin/waagent -daemon
             └─2877 /usr/bin/python3 -u bin/WALinuxAgent-2.15.0.1-py3.12.egg -run-exthandlers

Mar 24 11:16:58 haaland-cloudtp3 python3[2877]: 1: lo    inet6 ::1/128 scope host \       valid_lf>
Mar 24 11:16:58 haaland-cloudtp3 python3[2877]: 2: eth0    inet6 fe80::7eed:8dff:fe64:9bb1/64 scop>
Mar 24 11:16:58 haaland-cloudtp3 python3[2877]: 2026-03-24T11:16:58.343791Z WARNING EnvHandler Ext>
Mar 24 11:16:58 haaland-cloudtp3 python3[2877]: 2026-03-24T11:16:58.347238Z INFO EnvHandler ExtHan>
Mar 24 11:16:58 haaland-cloudtp3 python3[2877]: 2026-03-24T11:16:58.398200Z INFO ExtHandler ExtHan>
Mar 24 11:16:58 haaland-cloudtp3 python3[2877]: 2026-03-24T11:16:58.398867Z INFO ExtHandler ExtHan>
Mar 24 11:16:58 haaland-cloudtp3 python3[2877]: 2026-03-24T11:16:58.403870Z INFO ExtHandler ExtHan>
Mar 24 11:16:58 haaland-cloudtp3 python3[2877]: 2026-03-24T11:16:58.424464Z INFO ExtHandler ExtHan>
Mar 24 11:16:58 haaland-cloudtp3 python3[2877]: 2026-03-24T11:16:58.464393Z INFO ExtHandler ExtHan>
Mar 24 11:16:58 haaland-cloudtp3 python3[2877]: 2026-03-24T11:16:58.484282Z INFO ExtHandler ExtHan>
```



