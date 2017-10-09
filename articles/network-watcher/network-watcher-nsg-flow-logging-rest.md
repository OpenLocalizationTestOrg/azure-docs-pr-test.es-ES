---
title: 'registros de aaaManage flujo de grupo de seguridad de red con Monitor de red de Azure: API de REST | Documentos de Microsoft'
description: "Esta página explica cómo toomanage flujo de grupo de seguridad de red se registra en el Monitor de red de Azure con API de REST"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2ab25379-0fd3-4bfe-9d82-425dfc7ad6bb
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: be81e35f4d01c67efef99773e9b4e2ae4b8e209e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-using-rest-api"></a>Configuración de registros de flujo de grupos de seguridad de red mediante la API de REST

> [!div class="op_single_selector"]
> - [Portal de Azure](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [CLI 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [CLI 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [API DE REST](network-watcher-nsg-flow-logging-rest.md)

Registros de flujo de grupo de seguridad de red son una característica del Monitor de red que permite tooview información sobre el tráfico IP de entrada y de salida a través de un grupo de seguridad de red. Estos registros de flujo se escriben en formato json y mostrar salidos y flujos de entrada en cada regla, Hola flujo Hola NIC que se aplica, tupla de 5 información acerca del flujo de hello (protocolo IP de origen/destino, puerto de origen/destino,) y si hello se permita el tráfico o denegado.

## <a name="before-you-begin"></a>Antes de empezar

ARMclient es la API de REST de hello toocall utilizados mediante PowerShell. ARMClient se encuentra en Chocolatey en [ARMClient en Chocolatey](https://chocolatey.org/packages/ARMClient)

Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.

> [!Important]
> Para la API de REST de Monitor de red llamadas Hola nombre de grupo de recursos en solicitud de hello que URI es el grupo de recursos de Hola que contiene Hola Monitor de red, no se está realizando acciones de diagnóstico de hello en recursos de Hola.

## <a name="scenario"></a>Escenario

escenario de Hello descrito en este artículo muestra cómo tooenable, deshabilitar y consulta fluyen registros con hello API de REST. toolearn más información acerca de loggings de flujo de grupo de seguridad de red, visite [registro de flujo del grupo de seguridad de red: información general sobre](network-watcher-nsg-flow-logging-overview.md).

En este escenario va a:

* Habilitar los registros de flujo
* Deshabilitar los registros de flujo
* Consultar el estado de los registros de flujo

## <a name="log-in-with-armclient"></a>Inicio de sesión con ARMClient

Inicie sesión en tooarmclient con sus credenciales de Azure.

```PowerShell
armclient login
```

## <a name="register-insights-provider"></a>Registro del proveedor de Insights

En orden para el flujo de registro toowork correctamente, Hola **Microsoft.Insights** proveedor debe estar registrado. Si no está seguro de si hello **Microsoft.Insights** proveedor está registrado, hello ejecución siguiente secuencia de comandos.

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
armclient post "https://management.azure.com//subscriptions/${subscriptionId}/providers/Microsoft.Insights/register?api-version=2016-09-01"
```

## <a name="enable-network-security-group-flow-logs"></a>Habilitación de los registros de flujo de grupos de seguridad de red

Hola comando tooenable flujo registros se muestra en el siguiente ejemplo de Hola:

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$storageId = "/subscriptions/00000000-0000-0000-0000-000000000000/{resourceGroupName/providers/Microsoft.Storage/storageAccounts/{saName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'properties': {
    'storageId': '${storageId}',
    'enabled': 'true',
    'retentionPolicy' : {
            days: 5,
            enabled: true
        }
    }
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/configureFlowLog?api-version=2016-12-01" $requestBody
```

Hola devolvió una respuesta Hola anterior es el ejemplo siguiente:

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": true,
    "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="disable-network-security-group-flow-logs"></a>Deshabilitación de los registros de flujo de grupos de seguridad de red

Hola de uso después de registros de flujo de toodisable de ejemplo. Hola llamada es Hola igual que habilitar los registros de flujo, excepto **false** está establecido para la propiedad de hello habilitado.

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$storageId = "/subscriptions/00000000-0000-0000-0000-000000000000/{resourceGroupName/providers/Microsoft.Storage/storageAccounts/{saName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'properties': {
    'storageId': '${storageId}',
    'enabled': 'false',
    'retentionPolicy' : {
            days: 5,
            enabled: true
        }
    }
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/configureFlowLog?api-version=2016-12-01" $requestBody
```

Hola devolvió una respuesta Hola anterior es el ejemplo siguiente:

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": false,
    "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="query-flow-logs"></a>Consulta del estado de los registros de flujo

Hola sigue a llamada REST consultas Hola estado del flujo de registros en un grupo de seguridad de red.

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/queryFlowLogStatus?api-version=2016-12-01" $requestBody
```

Hola te mostramos un ejemplo de respuesta de hello devuelta:

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": true,
   "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="download-a-flow-log"></a>Descarga de un registro de flujo

ubicación de almacenamiento de Hola de un registro de flujo se define en la creación. Un tooaccess herramienta adecuada estas cuentas de almacenamiento de tooa de guardar registros de flujo es Microsoft Azure Storage Explorer, que puede descargarse aquí: http://storageexplorer.com/

Si se especifica una cuenta de almacenamiento, archivos de captura de paquetes se guardan tooa cuenta de almacenamiento en hello ubicación siguiente:

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo demasiado[visualizar los registros de flujo NSG con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)

Obtenga información acerca de cómo demasiado[visualizar los registros de flujo NSG con herramientas de código abierto](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)
