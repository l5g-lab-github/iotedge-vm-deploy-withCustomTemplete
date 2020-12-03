# iotedge-vm-deploy 
IoT EdgeモジュールがデプロイされたLinux VMを手軽に作成する.

[オリジナルテンプレート](https://github.com/Azure/iotedge-vm-deploy)を使用すると、VMなどの名前がランダム文字列になってしまう問題を解決した。

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
az deployment group create \
  --resource-group <replace-with-rg-name> \
  --template-uri "https://raw.githubusercontent.com/l5g-lab-github/iotedge-vm-deploy-withCustomTemplete/main/edgeDeploy.json" \
  --parameters dnsLabelPrefix='<replace-with-VM-name>' \
  --parameters adminUsername='<replace-with-adminUser-name>' \
  --parameters deviceConnectionString=$(az iot hub device-identity show-connection-string --device-id <replace-with-device-name> --hub-name <replace-with-hub-name> -o tsv) \
  --parameters authenticationType='password' 
```

Example:
```bash
az deployment group create \
--resource-group rg-factory-ai \
--template-uri "https://raw.githubusercontent.com/l5g-lab-github/iotedge-vm-deploy-withCustomTemplete/main/edgeDeploy.json" \
--parameters dnsLabelPrefix='myiotedge' \
--parameters adminUsername='azureUser' \
--parameters deviceConnectionString=$(az iot hub device-identity connection-string show --device-id cam04 --hub-name factory-AI -o tsv) \
--parameters authenticationType='password'
```
troubleshooting：

dnsLabelPrefixはすべて小文字の半角英数字。deviceConnectionStringiotHubに登録してあるデバイスの接続文字列を直接コピペしてもいい。
 # Details
 Detailed documentation is available on 
 
 [Ubuntu 仮想マシン上で Azure IoT Edge を実行する](https://docs.microsoft.com/ja-jp/azure/iot-edge/how-to-install-iot-edge-ubuntuvm?WT.mc_id=github-iotedgevmdeploy-pdecarlo)
 
 [クイック スタート:初めての IoT Edge モジュールを Linux 仮想デバイスにデプロイする](https://docs.microsoft.com/ja-jp/azure/iot-edge/quickstart-linux?view=iotedge-2018-06#code-try-5)
