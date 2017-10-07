---
title: "aaaNetworking para conjuntos de escalas de máquina virtual de Azure | Documentos de Microsoft"
description: "Propiedades de configuración de red para el conjunto de escalado de máquinas virtuales de Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: guybo
ms.openlocfilehash: ef3f0cfe648d2195c051a73987e654f0e15d13bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="networking-for-azure-virtual-machine-scale-sets"></a>Redes para conjuntos de escalado de máquinas virtuales de Azure

Cuando se implementación un conjunto a través del portal de Hola de escalas de máquina virtual de Azure, algunas propiedades de red se establecen de forma predeterminadas, por ejemplo un equilibrador de carga de Azure con las reglas NAT de entrada. Este artículo describe cómo se establece toouse algunos hello más funciones avanzadas de red que se pueden configurar con una escala.

Puede configurar todas las características de hello tratadas en este artículo usando plantillas del Administrador de recursos de Azure. También se incluyen ejemplos de la CLI de Azure y PowerShell para las características seleccionadas. Use CLI 2.10 y PowerShell 4.2.0 o una versión posterior.

## <a name="accelerated-networking"></a>Redes aceleradas
Azure [Accelerated redes](../virtual-network/virtual-network-create-vm-accelerated-networking.md) mejora el rendimiento de la red habilitando la máquina virtual de E/S de raíz única (SR-IOV) de virtualización tooa. toouse accelerated redes con conjuntos de escalas, establezca enableAcceleratedNetworking demasiado**true** en la configuración de networkInterfaceConfigurations de su conjunto de escala. Por ejemplo:
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
      "name": "niconfig1",
      "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
          ...
        ]
      }
    }
   ]
}
```

## <a name="create-a-scale-set-that-references-an-existing-azure-load-balancer"></a>Creación de un conjunto de escalado que hace referencia a una instancia de Azure Load Balancer existente
Cuando se crea un conjunto de escala con hello portal de Azure, se crea un nuevo equilibrador de carga para la mayoría de opciones de configuración. Si crea un conjunto de escala, que debe tooreference un equilibrador de carga existente, puede hacerlo mediante la CLI. Hola siguiente secuencia de comandos de ejemplo crea un equilibrador de carga y, a continuación, crea un conjunto de escala, que hace referencia a él:
```bash
az network lb create -g lbtest -n mylb --vnet-name myvnet --subnet mysubnet --public-ip-address-allocation Static --backend-pool-name mybackendpool

az vmss create -g lbtest -n myvmss --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username negat --ssh-key-value /home/myuser/.ssh/id_rsa.pub --upgrade-policy-mode Automatic --instance-count 3 --vnet-name myvnet --subnet mysubnet --lb mylb --backend-pool-name mybackendpool

```

## <a name="configurable-dns-settings"></a>Valores de DNS configurables
Conjuntos de escalas de adopta de forma predeterminada, en configuración de DNS específico de Hola de hello red virtual y subred que se crearon. Obstante, puede configurar el DNS de Hola para una escala establecer directamente.
~
### <a name="creating-a-scale-set-with-configurable-dns-servers"></a>Creación de un conjunto de escalado con servidores DNS configurables
toocreate una escala configurada con una configuración de DNS personalizada mediante 2.0 de CLI, agregue hello **servidores dns--** argumento toohello **vmss crear** separados de comando, seguido por el espacio de direcciones ip del servidor. Por ejemplo:
```bash
--dns-servers 10.0.0.6 10.0.0.5
```
tooconfigure los servidores DNS personalizados en una plantilla de Azure, agregue una escala de toohello de propiedad de clase dnsSettings la sección networkInterfaceConfigurations del conjunto. Por ejemplo:
```json
"dnsSettings":{
    "dnsServers":["10.0.0.6", "10.0.0.5"]
}
```

### <a name="creating-a-scale-set-with-configurable-virtual-machine-domain-names"></a>Creación de un conjunto de escalado con nombres de dominio de máquinas virtuales configurables
toocreate establece una escala con un nombre DNS personalizado para máquinas virtuales mediante la CLI 2.0, agregar hello **--vm nombre de dominio** argumento toohello **vmss crear** comando, seguido de una cadena que representa el nombre de dominio de Hola.

nombre de dominio de hello tooset en una plantilla de Azure, agregue un **dnsSettings** conjunto de escalas de propiedad toohello **networkInterfaceConfigurations** sección. Por ejemplo:

```json
"networkProfile": {
  "networkInterfaceConfigurations": [
    {
    "name": "nic1",
    "properties": {
      "primary": "true",
      "ipConfigurations": [
      {
        "name": "ip1",
        "properties": {
          "subnet": {
            "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
          },
          "publicIPAddressconfiguration": {
            "name": "publicip",
            "properties": {
            "idleTimeoutInMinutes": 10,
              "dnsSettings": {
                "domainNameLabel": "[parameters('vmssDnsName')]"
              }
            }
          }
        }
      }
    ]
    }
}
```

salida de Hello, para un nombre de dns de la máquina virtual individual sería Hola siguiente forma: 
```
<vm><vmindex>.<specifiedVmssDomainNameLabel>
```

## <a name="public-ipv4-per-virtual-machine"></a>Dirección IPv4 pública por máquina virtual
En general, las máquinas virtuales del conjunto de escalado de Azure no requieren direcciones IP públicas propias. Para la mayoría de los casos, resulta más económico y segura tooassociate un pública IP dirección tooa carga equilibrador o tooan máquina virtual individual (también conocido como un jumpbox), que, a continuación, enruta entrantes conexiones tooscale conjunto de las máquinas virtuales según sea necesario (por ejemplo, mediante reglas NAT de entrada).

Sin embargo, algunos escenarios requieren conjunto de escalado de máquinas virtuales toohave su propia dirección IP pública direcciones. Un ejemplo es juegos, donde una consola necesita toomake una conexión directa tooa nube máquina virtual en que está realizando el procesamiento de juego física. Otro ejemplo es donde máquinas virtuales deben toomake conexiones externas tooone otro a lo largo de las regiones en una base de datos distribuida.

### <a name="creating-a-scale-set-with-public-ip-per-virtual-machine"></a>Creación de un conjunto de escalado con una dirección IP pública por máquina virtual
toocreate un conjunto de escala que asigna una máquina de virtual pública de tooeach dirección IP 2.0 de CLI, agregue hello **--public-ip por vm** parámetro toohello **vmss crear** comando. 

toocreate una escala que se establecen a través de una plantilla de Azure, asegúrese de versión de Hola API de hello Microsoft.Compute/virtualMachineScaleSets recurso es al menos **2017-03-30**y agregue un **publicIpAddressConfiguration**IpConfigurations sección del conjunto de escala de toohello de propiedad JSON. Por ejemplo:

```json
"publicIpAddressConfiguration": {
    "name": "pub1",
    "properties": {
      "idleTimeoutInMinutes": 15
    }
}
```
Ejemplo de plantilla: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)

### <a name="querying-hello-public-ip-addresses-of-hello-virtual-machines-in-a-scale-set"></a>Al consultar la dirección IP pública de Hola el conjunto de direcciones de máquinas virtuales de hello en una escala
asignar las direcciones IP públicas de toolist hello tooscale conjunto de máquinas virtuales con CLI 2.0, use hello **vmss az-instancia de lista-IP pública** comando.

conjunto de escalado de toolist de direcciones IP públicas con PowerShell, use hello _Get AzureRmPublicIpAddress_ comando. Por ejemplo:
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -VirtualMachineScaleSetName myvmss
```

También puede direcciones IP públicas de consulta Hola haciendo referencia directamente a los Id. de recurso de Hola de configuración de dirección IP pública Hola. Por ejemplo:
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -Name myvmsspip
```

asignar las direcciones IP públicas de tooquery hello tooscale conjunto de máquinas virtuales con hello [Explorador de recursos de Azure](https://resources.azure.com), u Hola API de REST de Azure con la versión **2017-03-30** o superior.

tooview de direcciones IP públicas para una escala que se establecen a través de hello Explorador de recursos, mire hello **las publicipaddresses a las** sección en su conjunto de escala. Por ejemplo: https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses

```
GET https://management.azure.com/subscriptions/{your sub ID}/resourceGroups/{RG name}/providers/Microsoft.Compute/virtualMachineScaleSets/{scale set name}/publicipaddresses?api-version=2017-03-30
```

Salida de ejemplo:
```json
{
  "value": [
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/pipvmss/virtualMachines/0/networkInterfaces/pipvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"a64060d5-4dea-4379-a11d-b23cd49a3c8d\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "ee8cb20f-af8e-4cd6-892f-441ae2bf701f",
        "ipAddress": "13.84.190.11",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/0/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    },
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"5f6ff30c-a24c-4818-883c-61ebd5f9eee8\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "036ce266-403f-41bd-8578-d446d7397c2f",
        "ipAddress": "13.84.159.176",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    }
```

## <a name="multiple-ip-addresses-per-nic"></a>Varias direcciones IP por NIC
Cada NIC conectada tooa que máquina virtual en un conjunto de escala puede tener una o varias configuraciones de IP asociadas con él. Se asigna a cada configuración una dirección IP privada. Cada configuración también puede tener un recurso de dirección IP pública asociado con ella. toounderstand cuántas direcciones IP pueden asignarse tooa NIC, y cuántas direcciones IP públicas que puede usar en una suscripción de Azure, consulte demasiado[el límite de Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).

## <a name="multiple-nics-per-virtual-machine"></a>Varias NIC por máquina virtual
Puede tener hasta too8 NIC por máquina virtual, según el tamaño de la máquina. número máximo de Hola de NIC por máquina está disponible en hello [artículo de tamaño de máquina virtual](../virtual-machines/windows/sizes.md). Hello en el ejemplo siguiente se es que una escala de conjunto de perfil de red que muestra varias entradas NIC y varias direcciones IP públicas por máquina virtual:
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
        "name": "nic1",
        "properties": {
            "primary": "true",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        },
        {
        "name": "nic2",
        "properties": {
            "primary": "false",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        }
    ]
}
```

## <a name="nsg-per-scale-set"></a>NSG por conjunto de escalado
Grupos de seguridad de red se pueden aplicar directamente tooa escala, mediante la adición de una sección de configuración de interfaz de referencia toohello red de escala de hello establece propiedades de la máquina virtual.

Por ejemplo: 
```
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre redes virtuales de Azure, consulte demasiado[esta documentación](../virtual-network/virtual-networks-overview.md).
