## <a name="nic"></a>NIC
Un recurso de tarjeta (NIC) de interfaz de red proporciona conectividad tooan existente subred en un recurso de red virtual. Aunque puede crear una NIC como un objeto independiente, necesita tooassociate se tooanother objeto tooactually proporcionar conectividad. Una NIC puede ser tooconnect usa una subred VM tooa, una dirección IP pública o un equilibrador de carga.  

| Propiedad | Descripción | Valores de ejemplo |
| --- | --- | --- |
| **virtualMachine** |Hola VM NIC está asociado. |/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1 |
| **macAddress** |Dirección MAC para hello NIC |cualquier valor entre 4 y 30 |
| **networkSecurityGroup** |NSG asociados toohello NIC |/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1 |
| **dnsSettings** |Configuración de DNS para hello NIC |Consulte [PIP](#Public-IP-address) |

Una tarjeta de interfaz de red o NIC, representa una interfaz de red que puede ser la máquina virtual (VM) de tooa asociado. Una máquina virtual puede tener una o varias NIC.

![NIC en una sola máquina virtual](./media/resource-groups-networking/Figure3.png)

### <a name="ip-configurations"></a>Configuraciones IP
NIC tienen un objeto secundario denominado **ipConfigurations** que contiene Hola propiedades siguientes:

| Propiedad | Descripción | Valores de ejemplo |
| --- | --- | --- |
| **subnet** |Hola de subred NIC está conectada a. |/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1 |
| **privateIPAddress** |Dirección IP para hello NIC en la subred de Hola |10.0.0.8 |
| **privateIPAllocationMethod** |Método de asignación de direcciones IP |Dynamic o Static |
| **enableIPForwarding** |Si se puede usar Hola NIC para el enrutamiento |true o false |
| **primary** |Si es Hola NIC Hola NIC principal para hello VM |true o false |
| **publicIPAddress** |PIP asociada Hola NIC |vea [Configuración de DNS](#DNS-settings) |
| **loadBalancerBackendAddressPools** |Hacer copia de Hola de grupos de dirección final que está asociado a la NIC | |
| **loadBalancerInboundNatRules** |Entrada Hola de reglas NAT carga equilibrador A que NIC está asociado | |

Dirección IP pública de ejemplo en formato JSON:

    {
        "name": "lb-nic1-be",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkInterfaces",
        "location": "eastus",
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "ipConfigurations": [
                {
                    "name": "NIC-config",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/NIC-config",
                    "etag": "W/\"0027f1a2-3ac8-49de-b5d5-fd46550500b1\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "privateIPAddress": "10.0.0.4",
                        "privateIPAllocationMethod": "Dynamic",
                        "subnet": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet"
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1"
                            }
                        ]
                    }
                }
            ],
            "dnsSettings": { ... },
            "macAddress": "00-0D-3A-10-F1-29",
            "enableIPForwarding": false,
            "primary": true,
            "virtualMachine": {
                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Compute/virtualMachines/web1"
            }
        }
    }

### <a name="additional-resources"></a>Recursos adicionales
* Hola de lectura [documentación de referencia de API de REST](https://msdn.microsoft.com/library/azure/mt163579.aspx) de NIC.

