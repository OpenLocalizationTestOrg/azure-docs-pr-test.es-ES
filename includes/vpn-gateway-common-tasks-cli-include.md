### <a name="tooview-local-network-gateways"></a><span data-ttu-id="89a5f-101">puertas de enlace de red local de tooview</span><span class="sxs-lookup"><span data-stu-id="89a5f-101">tooview local network gateways</span></span>

<span data-ttu-id="89a5f-102">tooview una lista de puertas de enlace de la red local de hello, use hello [lista de puerta de enlace local de red az](https://docs.microsoft.com/cli/azure/network/local-gateway#list) comando.</span><span class="sxs-lookup"><span data-stu-id="89a5f-102">tooview a list of hello local network gateways, use hello [az network local-gateway list](https://docs.microsoft.com/cli/azure/network/local-gateway#list) command.</span></span>

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="tooverify-hello-shared-key-values"></a><span data-ttu-id="89a5f-103">Hola tooverify comparten valores de clave</span><span class="sxs-lookup"><span data-stu-id="89a5f-103">tooverify hello shared key values</span></span>

<span data-ttu-id="89a5f-104">Compruebe que el valor de clave de hello compartido es Hola mismo valor que utilizó para la configuración del dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="89a5f-104">Verify that hello shared key value is hello same value that you used for your VPN device configuration.</span></span> <span data-ttu-id="89a5f-105">Si no es así, ejecute conexión Hola utilizando de nuevo valor de hello de dispositivo de Hola o actualizar dispositivo Hola con el valor de Hola de hello devuelto.</span><span class="sxs-lookup"><span data-stu-id="89a5f-105">If it is not, either run hello connection again using hello value from hello device, or update hello device with hello value from hello return.</span></span> <span data-ttu-id="89a5f-106">Hola valores deben coincidir.</span><span class="sxs-lookup"><span data-stu-id="89a5f-106">hello values must match.</span></span> <span data-ttu-id="89a5f-107">Hola tooview compartido clave, use hello [lista de conexiones vpn de red az](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).</span><span class="sxs-lookup"><span data-stu-id="89a5f-107">tooview hello shared key, use hello [az network vpn-connection-list](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).</span></span>

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="tooview-hello-vpn-gateway-public-ip-address"></a><span data-ttu-id="89a5f-108">puerta de enlace VPN de hello tooview dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="89a5f-108">tooview hello VPN gateway Public IP address</span></span>

<span data-ttu-id="89a5f-109">dirección IP toofind Hola pública de la puerta de enlace de red virtual, use hello [lista de ip pública de red az](https://docs.microsoft.com/cli/azure/network/public-ip#list) comando.</span><span class="sxs-lookup"><span data-stu-id="89a5f-109">toofind hello public IP address of your virtual network gateway, use hello [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="89a5f-110">Para facilitar la lectura, la salida de hello en este ejemplo es la lista de Hola de toodisplay con formato de direcciones IP públicas en formato de tabla.</span><span class="sxs-lookup"><span data-stu-id="89a5f-110">For easy reading, hello output for this example is formatted toodisplay hello list of public IPs in table format.</span></span>

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
