Puede comprobar que la conexión se realizó correctamente mediante el uso de hello [show de conexión vpn de red az](/cli/azure/network/vpn-connection#show) comando. En el ejemplo de Hola, ', nombre ' hace referencia toohello nombre de conexión de Hola que desea tootest. Una vez Hola conexión en proceso de Hola de que se va a establecer, su estado de conexión muestra 'Conectar'. Una vez establecida la conexión de hello, estado de hello cambia too'Connected'.

```azurecli
az network vpn-connection show --name VNet1toSite2 --resource-group TestRG1
```

