# IV. Monitoring¶

## 2. Une alerte CPU¶
🌞 Compléter votre plan Terraform et mettez en place une alerte CPU
```sh
voir main.tf
monitoring.tf
autre ficher modif variables.tf
terraform.tfvars
```

## 3. Alerte mémoire¶
🌞 Compléter votre plan Terraform et mettez en place une alerte mémoire
```sh
déja fait voire main.tf et montoring.tf
```

# B. Stress pour fire les alertes¶
🌞 Stress de la machine
 ```sh 
gusta@NATHANHOAMB:~/terraform-tp2-azure$ az monitor metrics alert list --resource-group cloud-tp2-terraform_group --output table
AutoMitigate    Description                                     Enabled    EvaluationFrequency    Location    Name                           ResourceGroup              Severity    TargetResourceRegion    TargetResourceType    WindowSize
--------------  ----------------------------------------------  ---------  ---------------------  ----------  -----------------------------  -------------------------  ----------  ----------------------  --------------------  ------------
True            Alert when available memory is less than 512MB  True       PT1M                   global      ram-alert-cloud-tp2-terraform  cloud-tp2-terraform_group  2                                                         PT5M
True            Alert when CPU usage exceeds 70%                True       PT1M                   global      cpu-alert-cloud-tp2-terraform  cloud-tp2-terraform_group  2                                                         PT5M
gusta@NATHANHOAMB:~/terraform-tp2-azure$
```
🌞 Vérifier que des alertes ont été fired
```sh
gusta@NATHANHOAMB:~/terraform-tp2-azure$ az monitor activity-log list --resource-group cloud-tp2-terraform_group --caller "Microsoft.Insights" --output table

gusta@NATHANHOAMB:~/terraform-tp2-azure$ az monitor activity-log list \
  --resource-group cloud-tp2-terraform_group \
  --output table \
  --query "[?contains(operationName.value, 'Microsoft.Insights/metricAlerts')]"
Caller                        CorrelationId                         Description    EventDataId                           EventTimestamp                Level          OperationId                           ResourceGroupName          ResourceId                                                                                                                                                            SubmissionTimestamp    SubscriptionId                        TenantId                              ResourceGroup
----------------------------  ------------------------------------  -------------  ------------------------------------  ----------------------------  -------------  ------------------------------------  -------------------------  --------------------------------------------------------------------------------------------------------------------------------------------------------------------  ---------------------  ------------------------------------  ------------------------------------  -------------------------
ilyass.el-meknassi@efrei.net  5aed8d18-9fd6-7a80-b85e-6729c3e62ebb                 8bafebaa-02d1-4d07-af4f-6c716e679fc2  2026-03-24T08:40:34.6433856Z  Informational  bdfd938d-ada2-4f6c-bc3c-f0462eafb916  cloud-tp2-terraform_group  /subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Insights/metricAlerts/cpu-alert-cloud-tp2-terraform  2026-03-24T08:41:40Z   f2760058-a494-48ea-bb1a-2c7e7e67a572  413600cf-bd4e-4c7c-8a61-69e73cddf731  cloud-tp2-terraform_group
ilyass.el-meknassi@efrei.net  5aed8d18-9fd6-7a80-b85e-6729c3e62ebb                 d38f3fcc-da46-4fa8-a48f-8858732c5d17  2026-03-24T08:40:34.4772048Z  Informational  e0d3ed2d-8cae-40cd-84dc-f2b7b943a485  cloud-tp2-terraform_group  /subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Insights/metricAlerts/ram-alert-cloud-tp2-terraform  2026-03-24T08:42:00Z   f2760058-a494-48ea-bb1a-2c7e7e67a572  413600cf-bd4e-4c7c-8a61-69e73cddf731  cloud-tp2-terraform_group
ilyass.el-meknassi@efrei.net  5aed8d18-9fd6-7a80-b85e-6729c3e62ebb                 e5563d0d-74c3-424a-8a0b-087f61caeb82  2026-03-24T08:40:31.1277442Z  Informational  bdfd938d-ada2-4f6c-bc3c-f0462eafb916  cloud-tp2-terraform_group  /subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Insights/metricAlerts/cpu-alert-cloud-tp2-terraform  2026-03-24T08:41:40Z   f2760058-a494-48ea-bb1a-2c7e7e67a572  413600cf-bd4e-4c7c-8a61-69e73cddf731  cloud-tp2-terraform_group
ilyass.el-meknassi@efrei.net  5aed8d18-9fd6-7a80-b85e-6729c3e62ebb                 b6e967d0-a1c0-49e5-968e-b9ac735b9e02  2026-03-24T08:40:28.9460029Z  Informational  e0d3ed2d-8cae-40cd-84dc-f2b7b943a485  cloud-tp2-terraform_group  /subscriptions/f2760058-a494-48ea-bb1a-2c7e7e67a572/resourceGroups/cloud-tp2-terraform_group/providers/Microsoft.Insights/metricAlerts/ram-alert-cloud-tp2-terraform  2026-03-24T08:42:00Z   f2760058-a494-48ea-bb1a-2c7e7e67a572  413600cf-bd4e-4c7c-8a61-69e73cddf731  cloud-tp2-terraform_group
gusta@NATHANHOAMB:~/terraform-tp2-azure$
```







