## <a name="virtual-network"></a>Red virtual
Los recursos de redes virtuales (VNET) y de subredes le ayudarán a definir un límite de seguridad para las cargas de trabajo que se ejecuten en Azure. Una red virtual se caracteriza por una colección de espacios de direcciones, también denominados bloques CIDR. 

> [!NOTE]
> Los administradores de red ya están familiarizados con la notación CIDR. Si no está familiarizado con el formato CIDR, [puede obtener más información](http://whatismyipaddress.com/cidr).
> 
> 

![Redes virtuales con varias subredes](./media/resource-groups-networking/Figure4.png)

Redes virtuales contienen Hola propiedades siguientes.

| Propiedad | Descripción | Valores de ejemplo |
| --- | --- | --- |
| **addressSpace** |Colección de prefijos de direcciones que constituyen Hola red virtual en la notación CIDR |192.168.0.0/16 |
| **subredes** |Colección de subredes que componen Hola red virtual |Consulte la información acerca de las [subredes](#Subnets) que tiene a continuación. |
| **ipAddress** |Dirección IP asignada tooobject. Se trata de una propiedad de solo lectura. |104.42.233.77 |

### <a name="subnets"></a>Subredes
Una subred es un recurso secundario de una red virtual que le ayudará a definir segmentos de espacios de direcciones dentro de un bloque CIDR mediante prefijos de direcciones IP. Pueden agregarse NIC toosubnets y tooVMs conectados, proporcionar conectividad para diversas cargas de trabajo.

Subredes contienen Hola propiedades siguientes. 

| Propiedad | Descripción | Valores de ejemplo |
| --- | --- | --- |
| **addressPrefix** |Prefijo de dirección única que componen la subred de hello en la notación CIDR |192.168.1.0/24 |
| **networkSecurityGroup** |NSG aplica toohello subred |Consulte [Grupos de seguridad de red](#Network-Security-Group) |
| **routeTable** |Tabla de ruta aplicado toohello subred |Consulte [Enrutamiento definido por el usuario](#Route-table) |
| **ipConfigurations** |Colección de objetos de configuración IP utilizada por NIC conectado toohello subred |Consulte [Enrutamiento definido por el usuario](#Route-table) |

Red virtual de ejemplo en formato JSON:

    {
        "name": "TestVNet",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/virtualNetworks",
        "location": "westus",
        "tags": {
            "displayName": "VNet"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "addressSpace": {
                "addressPrefixes": [
                    "192.168.0.0/16"
                ]
            },
            "subnets": [
                {
                    "name": "FrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "networkSecurityGroup": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd"
                        },
                        "routeTable": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd"
                        },
                        "ipConfigurations": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConfigurations/ipconfig1"
                            },
                            ...]
                    }
                },
                ...]
        }
    }

### <a name="additional-resources"></a>Recursos adicionales
* Obtenga más información acerca de las [Redes virtuales](../articles/virtual-network/virtual-networks-overview.md).
* Hola de lectura [documentación de referencia de API de REST](https://msdn.microsoft.com/library/azure/mt163650.aspx) para redes virtuales.
* Hola de lectura [documentación de referencia de API de REST](https://msdn.microsoft.com/library/azure/mt163618.aspx) para subredes.

