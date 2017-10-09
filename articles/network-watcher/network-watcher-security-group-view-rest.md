---
title: 'seguridad de red de aaaAnalyze con vista grupo Monitor de seguridad de Azure red: API de REST | Documentos de Microsoft'
description: "En este artículo se describe cómo toouse PowerShell tooanalyze un virtual máquinas seguridad con vista de grupo de seguridad."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a2f418fe-f5d2-43ed-8dc3-df0ed2a4d4ac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 0858a64a9454816e05f06dadb9536ad0c755e90e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-rest-api"></a>Análisis de la seguridad de una máquina virtual con la vista de grupos de seguridad mediante la API de REST

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-security-group-view-powershell.md)
> - [CLI 1.0](network-watcher-security-group-view-cli-nodejs.md)
> - [CLI 2.0](network-watcher-security-group-view-cli.md)
> - [API DE REST](network-watcher-security-group-view-rest.md)

Vista de grupo de seguridad devuelve reglas de seguridad de red configurada y eficaz que están aplicados tooa virtual machine. Esta capacidad es útil tooaudit y diagnosticar los grupos de seguridad de red y las reglas que se configuran en el tráfico de tooensure de una máquina virtual se está correctamente permitirá o denegará. En este artículo, le mostraremos cómo tooretrieve Hola efectivo y aplica la seguridad las reglas de máquina virtual de tooa mediante API de REST

## <a name="before-you-begin"></a>Antes de empezar

En este escenario, llame a vista de grupo de seguridad de Hola Hola API de Rest de Monitor de red tooget para una máquina virtual. ARMclient es la API de REST de hello toocall utilizados mediante PowerShell. ARMClient se encuentra en Chocolatey en [ARMClient en Chocolatey](https://chocolatey.org/packages/ARMClient)

Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red. escenario de Hello también supone que un grupo de recursos con una máquina virtual válida existe toobe usa.

## <a name="scenario"></a>Escenario

escenario de Hello descrito en este artículo recupera reglas de seguridad eficaz y aplicada de Hola para una máquina virtual dada.

## <a name="log-in-with-armclient"></a>Inicio de sesión con ARMClient

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a>Recuperación de una máquina virtual

Ejecute hello después de la secuencia de comandos tooreturn un machineThe virtual después de código debe variables:

- **Id. de suscripción** -también se puede recuperar el Id. de suscripción de hello con hello **AzureRMSubscription Get** cmdlet.
- **resourceGroupName** : hello nombre de un grupo de recursos que contiene máquinas virtuales.

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

información que se necesita Hello es hello **identificador** bajo tipo hello `Microsoft.Compute/virtualMachines` en respuesta, tal como se muestra en el siguiente ejemplo de Hola:

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft
.Network/networkInterfaces/{nicName}"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Com
pute/virtualMachines/{vmName}/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute
/virtualMachines/{vmName}",
      "name": "{vmName}"
    }
  ]
}
```

## <a name="get-security-group-view-for-virtual-machine"></a>Obtención de la vista de grupos de seguridad para una máquina virtual

Hola ejemplo siguiente solicita la vista de grupo de seguridad de Hola de una máquina virtual de destino. resultados de Hola de este ejemplo pueden ser utilizados toocompare toohello reglas y definido por toolook de creación de hello para el desfase de la configuración de seguridad.

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.compute/virtualMachine/$vmName

$requestBody = @"
{
    'targetResourceId': '${targetUri}'

}
"@
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/securityGroupView?api-version=2016-12-01" $requestBody -verbose
```

## <a name="view-hello-response"></a>Respuesta de hello de vista

Hola según muestra es la respuesta de hello procedente de hello anterior comando. Hello resultados muestran todas las reglas de seguridad eficaz y aplicado hello en la máquina virtual de hello desglosado en grupos de **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, y  **EffectiveSecurityRules**.

```json

{
  "networkInterfaces": [
    {
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "securityRules": [
            {
              "name": "default-allow-rdp",
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "etag": "W/\"d4c411d4-0d62-49dc-8092-3d4b57825740\"",
              "properties": {
                "provisioningState": "Succeeded",
                "protocol": "TCP",
                "sourcePortRange": "*",
                "destinationPortRange": "3389",
                "sourceAddressPrefix": "*",
                "destinationAddressPrefix": "*",
                "access": "Allow",
                "priority": 1000,
                "direction": "Inbound"
              }
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "name": "AllowVnetInBound",
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/",
            "properties": {
              "provisioningState": "Succeeded",
              "description": "Allow inbound traffic from all VMs in VNET",
              "protocol": "*",
              "sourcePortRange": "*",
              "destinationPortRange": "*",
              "sourceAddressPrefix": "VirtualNetwork",
              "destinationAddressPrefix": "VirtualNetwork",
              "access": "Allow",
              "priority": 65000,
              "direction": "Inbound"
            }
          },
          ...
        ],
        "effectiveSecurityRules": [
          {
            "name": "DefaultOutboundDenyAll",
            "protocol": "All",
            "sourcePortRange": "0-65535",
            "destinationPortRange": "0-65535",
            "sourceAddressPrefix": "*",
            "destinationAddressPrefix": "*",
            "access": "Deny",
            "priority": 65500,
            "direction": "Outbound"
          },
          ...
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a>Pasos siguientes

Visite [auditoría red seguridad grupos (NSG) con el Monitor de red](network-watcher-security-group-view-powershell.md) toolearn cómo tooautomate validación de grupos de seguridad de red.


