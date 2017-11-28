### <a name="to-view-local-network-gateways"></a><span data-ttu-id="20a4b-101">Para ver las puertas de enlace de la red local</span><span class="sxs-lookup"><span data-stu-id="20a4b-101">To view local network gateways</span></span>

<span data-ttu-id="20a4b-102">Para ver una lista de las puertas de enlace de red local, use el comando [az network local-gateway list](https://docs.microsoft.com/cli/azure/network/local-gateway#list).</span><span class="sxs-lookup"><span data-stu-id="20a4b-102">To view a list of the local network gateways, use the [az network local-gateway list](https://docs.microsoft.com/cli/azure/network/local-gateway#list) command.</span></span>

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="to-verify-the-shared-key-values"></a><span data-ttu-id="20a4b-103">Para comprobar los valores de la clave compartida</span><span class="sxs-lookup"><span data-stu-id="20a4b-103">To verify the shared key values</span></span>

<span data-ttu-id="20a4b-104">Compruebe que el valor de la clave compartida es el mismo valor que utilizó para la configuración del dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="20a4b-104">Verify that the shared key value is the same value that you used for your VPN device configuration.</span></span> <span data-ttu-id="20a4b-105">Si no es así, ejecute de nuevo la conexión con el valor del dispositivo, o actualice el dispositivo con el valor devuelto.</span><span class="sxs-lookup"><span data-stu-id="20a4b-105">If it is not, either run the connection again using the value from the device, or update the device with the value from the return.</span></span> <span data-ttu-id="20a4b-106">Los valores deben coincidir.</span><span class="sxs-lookup"><span data-stu-id="20a4b-106">The values must match.</span></span> <span data-ttu-id="20a4b-107">Para ver la clave compartida, use [az network vpn-connection-list](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).</span><span class="sxs-lookup"><span data-stu-id="20a4b-107">To view the shared key, use the [az network vpn-connection-list](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).</span></span>

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="to-view-the-vpn-gateway-public-ip-address"></a><span data-ttu-id="20a4b-108">Para ver la dirección IP pública de la puerta de enlace de VPN</span><span class="sxs-lookup"><span data-stu-id="20a4b-108">To view the VPN gateway Public IP address</span></span>

<span data-ttu-id="20a4b-109">Para buscar la dirección IP pública de la puerta de enlace de red virtual, use el comando [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#list).</span><span class="sxs-lookup"><span data-stu-id="20a4b-109">To find the public IP address of your virtual network gateway, use the [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="20a4b-110">Para facilitar la lectura, la salida de este ejemplo tiene el formato preciso para mostrar la lista de direcciones IP públicas en formato de tabla.</span><span class="sxs-lookup"><span data-stu-id="20a4b-110">For easy reading, the output for this example is formatted to display the list of public IPs in table format.</span></span>

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
