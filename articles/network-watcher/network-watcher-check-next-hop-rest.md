---
title: "aaaFind próximo salto con Azure red Monitor de próximo salto - REST | Documentos de Microsoft"
description: "En este artículo se describe cómo puede ver qué Hola siguiente tipo de salto es y dirección ip mediante el uso de salto siguiente Hola API de REST de Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2216c059-45ba-4214-8304-e56769b779a6
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a2b61b355aae8ae513ebd44837184fbc6cfd668c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a>Averiguar qué tipo de hello próximo salto es con capacidad de próximo salto de hello en Monitor de red de Azure mediante la API de REST de Azure

> [!div class="op_single_selector"]
> - [Portal de Azure](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [API de REST de Azure](network-watcher-check-next-hop-rest.md)

Próximo salto es una característica del Monitor de red que proporciona la capacidad de hello obtener tipo hello de próximo salto y la dirección IP basándose en una máquina virtual especificada. Esta capacidad es útil para determinar si el tráfico que sale de una máquina virtual recorre una puerta de enlace, internet o redes virtuales tooget tooits destino.

## <a name="before-you-begin"></a>Antes de empezar

ARMclient es la API de REST de hello toocall utilizados mediante PowerShell. ARMClient se encuentra en Chocolatey en [ARMClient en Chocolatey](https://chocolatey.org/packages/ARMClient)

Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.

## <a name="scenario"></a>Escenario

escenario de Hello descrito en este artículo usa próximo salto, una característica de Monitor de red que se determina el tipo de próximo salto hello y dirección IP para un recurso. toolearn más información acerca de próximo salto, visite [información general sobre salto siguiente](network-watcher-next-hop-overview.md).

En este escenario va a:

* Recuperar próximo salto Hola para una máquina virtual.

## <a name="log-in-with-armclient"></a>Inicio de sesión con ARMClient

Inicie sesión en tooarmclient con sus credenciales de Azure.

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a>Recuperación de una máquina virtual

Ejecutar Hola después tooreturn de secuencia de comandos en una máquina virtual. Esta información es necesaria para ejecutar el próximo salto.

Hola después el código necesita valores para hello siguientes variables:

- **Id. de suscripción** -Hola toouse de Id. de suscripción.
- **resourceGroupName** : hello nombre de un grupo de recursos que contiene máquinas virtuales.

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

Desde la siguiente Hola resultado, Id. de Hola de máquina virtual de Hola se usa en el siguiente ejemplo de Hola:

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="get-next-hop"></a>Obtención del próximo salto

Una vez creado el encabezado de autorización de hello, se puede recuperar el próximo salto de Hola desde una máquina virtual. Hello valores siguientes se deben reemplazar para toowork de ejemplo de código de hello.

> [!Important]
> Para la API de REST de Monitor de red llamadas Hola nombre de grupo de recursos en solicitud de hello que URI es el grupo de recursos de Hola que contiene Hola Monitor de red, no se está realizando acciones de diagnóstico de hello en recursos de Hola.

```powershell
$sourceIP = "10.0.0.4"
$destinationIP = "8.8.8.8"
$resourceGroupName = <resource group name>
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'sourceIpAddress': '${sourceIP}',
    'destinationIpAddress': '${destinationIP}',
    'targetNicResourceId' : '${targetNic}'
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/nextHop?api-version=2016-12-01" $requestBody
```

> [!NOTE]
> Salto siguiente requiere que el recurso de máquina virtual de Hola se asigna toorun.

## <a name="results"></a>Results

Hello fragmento de código siguiente es un ejemplo de salida de hello recibido. resultados de Hello contienen Hola siguientes valores:

* **nextHopType** -este valor es uno de hello siguientes valores: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway o ninguno.
* **nextHopIpAddress** -Hola dirección IP del próximo salto de Hola.
* **routeTableId** : valor de hello es un identificador uri para la tabla de ruta de hello asociado a la ruta de hello, o si no definido por el usuario ruta es valor Hola definido de *ruta del sistema* se devuelve.

siguiente Hola se muestran resultados de hello en formato json.

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a>Pasos siguientes

Una vez que han sido capaz de toofind out próximo salto Hola para una máquina virtual, puede ver seguridad Hola de los recursos de red visitando [información general de la vista de la seguridad](network-watcher-security-group-view-overview.md)














