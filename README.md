# iotedge-vm-deploy 
IoT EdgeモジュールがデプロイされたLinux VMを手軽に作成する.

[オリジナルテンプレート](https://raw.githubusercontent.com/Azure/iotedge-vm-deploy/master/edgeDeploy.json)を使用すると、VMなどの名前がランダム文字列になってしまう問題を解決した。

## Resource Groupを作る
```bash
az group create --name <replace-with-rg-name> --location JapanEast
```

## ARM Template to deploy IoT Edge enabled VM

ARM template to deploy a VM with IoT Edge pre-installed (via cloud-init)

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fl5g-lab-github%2Fiotedge-vm-deploy-withCustomTemplete%2Fmain%2FedgeDeploy.json" target="_blank">
    <img src="https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.png" />
</a>

The ARM template visualized for exploration

## Azure CLI command to deploy IoT Edge enabled VM

```bash
az group deployment create \
  --name <replace-with-edge-name> \
  --resource-group <replace-with-rg-name> \
  --template-uri "https://raw.githubusercontent.com/l5g-lab-github/iotedge-vm-deploy-withCustomTemplete/main/edgeDeploy.json" \
  --parameters dnsLabelPrefix='<replace-with-VM-name>' \
  --parameters adminUsername='<replace-with-adminUser-name>' \
  --parameters deviceConnectionString=$(az iot hub device-identity show-connection-string --device-id <replace-with-device-name> --hub-name <replace-with-hub-name> -o tsv) \
  --parameters authenticationType='sshPublicKey' \
  --parameters adminPasswordOrKey="$(< ~/.ssh/id_rsa.pub)"
```

Example:
```bash
az group deployment create \
  --name edgeVm \
  --resource-group IoTEdgeResources \
  --template-uri "https://raw.githubusercontent.com/l5g-lab-github/iotedge-vm-deploy-withCustomTemplete/main/edgeDeploy.json" \
  --parameters dnsLabelPrefix='my-edge-vm1' \
  --parameters adminUsername='azureuser' \
  --parameters deviceConnectionString=$(az iot hub device-identity show-connection-string --device-id cam01 --hub-name myFirstIoTHub -o tsv) \
  --parameters authenticationType='sshPublicKey' \
  --parameters adminPasswordOrKey="$(< ~/.ssh/id_rsa.pub)"
  
  
 # Details
 Detailed documentation is available on 
 
 [Microsoft Docs](https://docs.microsoft.com/ja-jp/azure/iot-edge/how-to-install-iot-edge-ubuntuvm?WT.mc_id=github-iotedgevmdeploy-pdecarlo)
 
 [Microsoft Docs](https://docs.microsoft.com/ja-jp/azure/iot-edge/quickstart-linux?view=iotedge-2018-06#code-try-5)
 
