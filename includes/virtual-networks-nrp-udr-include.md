## <a name="route-tables"></a>Tablas de ruta
Recursos de la tabla de enrutamiento contiene toodefine rutas utiliza cómo fluye el tráfico dentro de su infraestructura de Azure. Puede usar toosend de rutas (UDR) definidos por el usuario de todo el tráfico de subred determinada tooa dispositivo virtual, como un sistema de detección de intrusión o de firewall (ID). Puede asociar un toosubnets de la tabla de ruta. 

Tablas de rutas contienen Hola propiedades siguientes.

| Propiedad | Descripción | Valores de ejemplo |
| --- | --- | --- |
| **rutas** |Colección de usuario definido por las rutas en la tabla de rutas de Hola |Consulte las [rutas definidas por el usuario](#User-defined-routes) |
| **subredes** |Se aplica demasiado la colección de tabla de rutas de Hola de subredes|consulte [subredes](#Subnets) |

### <a name="user-defined-routes"></a>rutas definidas por el usuario
Puede crear toospecify UDRs dónde se debería enviar tráfico, en función de su dirección de destino. Una ruta se puede considerar como definición de puerta de enlace predeterminada de hello en función de la dirección de destino de Hola de un paquete de red.

UDRs contienen Hola propiedades siguientes. 

| Propiedad | Descripción | Valores de ejemplo |
| --- | --- | --- |
| **addressPrefix** |Prefijo de dirección o dirección IP completa destino Hola |192.168.1.0/24, 192.168.1.101 |
| **nextHopType** |Tipo de dispositivo Hola tráfico se enviará demasiado|VirtualAppliance, puerta de enlace VPN, Internet |
| **nextHopIpAddress** |Dirección IP de próximo salto de Hola |192.168.1.4 |

Tabla de ruta de ejemplo en formato JSON:

    {
        "name": "UDR-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/routeTables",
        "location": "westus",
        "properties": {
            "provisioningState": "Succeeded",
            "routes": [
                {
                    "name": "RouteToFrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd/routes/RouteToFrontEnd",
                    "etag": "W/\"v\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "nextHopType": "VirtualAppliance",
                        "nextHopIpAddress": "192.168.0.4"
                    }
                }
            ],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd"
                }
            ]
        }
    }

### <a name="additional-resources"></a>Recursos adicionales
* Obtenga más información acerca de las [Rutas definidas por el usuario](../articles/virtual-network/virtual-networks-udr-overview.md).
* Hola de lectura [documentación de referencia de API de REST](https://msdn.microsoft.com/library/azure/mt502549.aspx) para tablas de rutas.
* Hola de lectura [documentación de referencia de API de REST](https://msdn.microsoft.com/library/azure/mt502539.aspx) para el usuario definido rutas (UDRs).

