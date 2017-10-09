## <a name="network-security-group"></a>Grupo de seguridad de red (NSG)
Un recurso NSG permite la creación de hello de límite de seguridad para las cargas de trabajo, mediante la implementación de permitir y denegar las reglas. Estas reglas se pueden aplicar tooa máquina virtual, una NIC o una subred.

| Propiedad | Descripción | Valores de ejemplo |
| --- | --- | --- |
| **subredes** |Lista de identificadores de subred hello NSG se aplica a. |/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd |
| **securityRules** |Lista de reglas de seguridad que componen hello NSG |Consulte la [regla de seguridad](#Security-rule) que tiene a continuación |
| **defaultSecurityRules** |Lista de reglas de seguridad predeterminadas presentes en cada Grupo de seguridad de red |Consulte las [reglas de seguridad predeterminadas](#Default-security-rules) que tiene a continuación |

* **Regla de seguridad** : un grupo de seguridad de red puede contener varias reglas de seguridad definidas. Cada regla puede permitir o denegar distintos tipos de tráfico.

### <a name="security-rule"></a>regla de seguridad
Una regla de seguridad es un recurso secundario de un NSG que contiene propiedades de Hola a continuación.

| Propiedad | Descripción | Valores de ejemplo |
| --- | --- | --- |
| **descripción** |Descripción de regla de Hola |Permite el tráfico entrante para todas las máquinas virtuales en la subred X |
| **protocolo** |Toomatch de protocolo para la regla de Hola |TCP, UDP o *. |
| **sourcePortRange** |Toomatch de intervalo de puerto de origen para la regla de Hola |80, 100-200, * |
| **destinationPortRange** |Toomatch de intervalo de puerto de destino para la regla de Hola |80, 100-200, * |
| **sourceAddressPrefix** |Toomatch de prefijo de dirección de origen para la regla de Hola |10.10.10.1, 10.10.10.0/24, VirtualNetwork |
| **destinationAddressPrefix** |Toomatch de prefijo de dirección de destino para la regla de Hola |10.10.10.1, 10.10.10.0/24, VirtualNetwork |
| **dirección** |Dirección del tráfico toomatch de regla de Hola |entrada o salida |
| **prioridad** |Prioridad de la regla de Hola. Las reglas se comprueban según su orden de prioridad; una vez se aplica una regla, no se prueban más reglas para realizar la coincidencia. |10, 100, 65000 |
| **acceso** |Tipo de acceso tooapply si coincide con la regla de Hola |permitir o denegar |

Grupo de seguridad de red de ejemplo en formato JSON:

    {
        "name": "NSG-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkSecurityGroups",
        "location": "westus",
        "tags": {
            "displayName": "NSG - Front End"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "securityRules": [
                {
                    "name": "rdp-rule",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/rdp-rule",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "description": "Allow RDP",
                        "protocol": "Tcp",
                        "sourcePortRange": "*",
                        "destinationPortRange": "3389",
                        "sourceAddressPrefix": "Internet",
                        "destinationAddressPrefix": "*",
                        "access": "Allow",
                        "priority": 100,
                        "direction": "Inbound"
                    }
                }
            ],
            "defaultSecurityRules": [
                { [...],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                }
            ]
        }
    }

### <a name="default-security-rules"></a>reglas de seguridad predeterminadas

Reglas de seguridad predeterminadas tienen Hola mismas propiedades disponibles en las reglas de seguridad. Existen tooprovide la conectividad básica entre los recursos que tienen los NSG aplicados toothem. Asegúrese de que sabe qué [reglas de seguridad predeterminadas](../articles/virtual-network/virtual-networks-nsg.md#default-rules) existen.

### <a name="additional-resources"></a>Recursos adicionales
* Obtenga más información acerca de los [Grupos de seguridad de red](../articles/virtual-network/virtual-networks-nsg.md).
* Hola de lectura [documentación de referencia de API de REST](https://msdn.microsoft.com/library/azure/mt163615.aspx) para NSG.
* Hola de lectura [documentación de referencia de API de REST](https://msdn.microsoft.com/library/azure/mt163580.aspx) para reglas de seguridad.
