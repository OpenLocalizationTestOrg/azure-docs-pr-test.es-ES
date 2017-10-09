---
title: "tráfico de aaaVerify con flujo de IP de Monitor de red de Azure Compruebe - REST | Documentos de Microsoft"
description: "Este artículo se describe cómo toocheck si se permite o deniega el tráfico tooor desde una máquina virtual"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3307a79f-03be-46a0-aaaf-b2079cb5f3b2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 956db0d326db597c6c402a9e8d4a5522c47c02d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Comprobar si se permite o se deniega el tráfico con la Comprobación del flujo de IP, un componente de Azure Network Watcher

> [!div class="op_single_selector"]
> - [Portal de Azure](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [API de REST de Azure](network-watcher-check-ip-flow-verify-rest.md)


Flujo IP comprobar es una característica de Monitor de red que le permite tooverify si se permite el tráfico tooor desde una máquina virtual. validación de Hola se puede ejecutar para el tráfico entrante o saliente. Este escenario es útil tooget un estado actual del si una máquina virtual puede comunicarse un recurso externo tooan o back-end. Flujo IP comprobar puede ser usado tooverify si las reglas del grupo de seguridad de red (NSG) se han configurado correctamente y solucionar los problemas flujos que se bloquean las reglas de NSG. Otra razón para usar IP flujo Compruebe es que quiera bloquear el tráfico de tooensure está bloqueando correctamente hello NSG.

## <a name="before-you-begin"></a>Antes de empezar

ARMclient es la API de REST de hello toocall utilizados mediante PowerShell. ARMClient se encuentra en Chocolatey en [ARMClient en Chocolatey](https://chocolatey.org/packages/ARMClient)

Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.

## <a name="scenario"></a>Escenario

Este escenario utiliza IP flujo Compruebe tooverify si una máquina virtual puede comunicarse tooanother máquina a través del puerto 443. Si se deniega el tráfico de hello, devuelve la regla de seguridad de Hola que deniega ese tráfico. toolearn más información acerca del flujo IP Verify, visite [flujo IP comprobar información general](network-watcher-ip-flow-verify-overview.md)

En este escenario, podrá:

* Recuperación de una máquina virtual
* Llamar a la Comprobación del flujo de IP
* Comprobar los resultados

## <a name="log-in-with-armclient"></a>Inicio de sesión con ARMClient

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a>Recuperación de una máquina virtual

Ejecutar Hola después tooreturn de secuencia de comandos en una máquina virtual. Hello siguiente código necesita valores para las variables de hello:

* **Id. de suscripción** -Hola toouse de Id. de suscripción.
* **resourceGroupName** : hello nombre de un grupo de recursos que contiene máquinas virtuales.

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

información que se necesita Hello es Id. de hello en tipo hello `Microsoft.Compute/virtualMachines`. resultados de Hello deberían ser similar toohello siguiendo el ejemplo de código:

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft
.Network/networkInterfaces/contosovm842"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Com
pute/virtualMachines/ContosoVM/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="call-ip-flow-verify"></a>Llamar a la Comprobación del flujo de IP

Hello en el ejemplo siguiente se crea un tráfico de hello tooverify de solicitud para una máquina virtual especificada. respuesta de Hello devuelve si se permite el tráfico de Hola o si se deniega el tráfico de Hola. Si se deniega el tráfico también devuelve los bloques de reglas Hola tráfico.

> [!NOTE]
> Flujo IP comprobar requiere que se asigna el recurso de máquina virtual de Hola.

script de Hola requiere recursos Hola Id. de una máquina virtual y de una tarjeta de interfaz de red en la máquina virtual de Hola. Estos valores se proporcionan con hello anterior de salida.

> [!Important]
> Para el resto de Monitor de red llamadas Hola nombre de grupo de recursos en solicitud de hello que URI es hello uno que contiene la instancia del Monitor de red de hello, no se está realizando acciones de diagnóstico de hello en recursos de Hola.

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$vmName = "<vm name>"
$vmNICName = "<vm NIC name>"
$direction = "<direction of traffic>" # Examples are: Inbound or Outbound
$localIP = "<source IP>"
$localPort = "<source Port>"
$remoteIP = "<destination IP>"
$remotePort = "<destination Port>" # Examples are: 80, or 80-120
$protocol = "<UDP, TCP or *>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.compute/virtualMachine/${vmName}
$targetNic = "<uri of target nic resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkInterfaces/${vmNICName}

$requestBody = @"
{
    'targetResourceId':  '$targetUri',
    'direction':  '$direction',
    'protocol':  '$protocol',
    'localPort':  '$localPort',
    'remotePort':  '$remotePort',
    'localIPAddress':  '$localIP',
    'remoteIPAddress':  '$remoteIP',
    'targetNICResourceId':  '$targetNic'
}
"@
        
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/ipFlowVerify?api-version=2016-12-01" $requestBody -verbose
```

## <a name="understanding-hello-results"></a>Descripción de los resultados de Hola

respuesta de Hello que regresar indica si se permite o deniega el tráfico de Hola. respuesta de Hello es similar a uno de hello en los ejemplos siguientes:

**Se permite**

```json
{
  "access": "Allow",
  "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

**Se deniega**

```json
{
  "access": "Deny",
  "ruleName": "defaultSecurityRules/DefaultInboundDenyAll"
}
```

## <a name="next-steps"></a>Pasos siguientes

Si se está bloqueando el tráfico y no debe ser, consulte [administrar grupos de seguridad de red](../virtual-network/virtual-network-manage-nsg-arm-portal.md) toolearn más acerca de los grupos de seguridad de red.












