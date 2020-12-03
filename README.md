# iotedge-vm-deploy

[オリジナルテンプレート](https://raw.githubusercontent.com/Azure/iotedge-vm-deploy/master/edgeDeploy.json)を使用すると、VMなどの名前がランダム文字列になってしまう問題を解決した。

Detailed documentation is available on [Microsoft Docs](https://docs.microsoft.com/en-us/azure/iot-edge/how-to-install-iot-edge-ubuntuvm?WT.mc_id=github-iotedgevmdeploy-pdecarlo)

## ARM Template to deploy IoT Edge enabled VM

ARM template to deploy a VM with IoT Edge pre-installed (via cloud-init)

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fl5g-lab-github%2Fiotedge-vm-deploy-withCustomTemplete%2Fmain%2FedgeDeploy.json" target="_blank">
    <img src="https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.png" />
</a>

The ARM template visualized for exploration

## Azure CLI command to deploy IoT Edge enabled VM

```bash
az group deployment create \
  --name edgeVm \
  --resource-group replace-with-rg-name \
  --template-uri "https://raw.githubusercontent.com/l5g-lab-github/iotedge-vm-deploy-withCustomTemplete/main/edgeDeploy.json" \
  --parameters dnsLabelPrefix='my-edge-vm1' \
  --parameters adminUsername='azureuser' \
  --parameters deviceConnectionString=$(az iot hub device-identity show-connection-string --device-id replace-with-device-name --hub-name replace-with-hub-name -o tsv) \
  --parameters authenticationType='sshPublicKey' \
  --parameters adminPasswordOrKey="$(< ~/.ssh/id_rsa.pub)"
```
