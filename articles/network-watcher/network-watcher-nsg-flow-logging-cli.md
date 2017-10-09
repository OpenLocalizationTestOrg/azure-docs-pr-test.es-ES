---
title: 'Flujo de grupo de seguridad de red registra aaaManage con Monitor de red de Azure: CLI de Azure | Documentos de Microsoft'
description: "Esta página explica cómo toomanage flujo de grupo de seguridad de red se registra en el Monitor de red de Azure con CLI de Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2dfc3112-8294-4357-b2f8-f81840da67d3
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2d0b02e7d0a5a9ab20beb491d49a5747f976a079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli"></a>Configuración de registros de flujo de grupos de seguridad de red con la CLI de Azure

> [!div class="op_single_selector"]
> - [Portal de Azure](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [CLI 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [CLI 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [API DE REST](network-watcher-nsg-flow-logging-rest.md)

Registros de flujo de grupo de seguridad de red son una característica del Monitor de red que permite tooview información sobre el tráfico IP de entrada y de salida a través de un grupo de seguridad de red. Estos registros de flujo se escriben en formato json y mostrar salidos y flujos de entrada en cada regla, Hola flujo Hola NIC que se aplica, tupla de 5 información acerca del flujo de hello (protocolo IP de origen/destino, puerto de origen/destino,) y si hello se permita el tráfico o denegado.

En este artículo usa la CLI de próxima generación para el modelo de implementación de administración de recursos hello, CLI de Azure 2.0, que está disponible para Windows, Mac y Linux.

Hola tooperform los pasos de este artículo, deberá demasiado[instalar Hola interfaz de línea de comandos de Azure para Mac, Linux y Windows (CLI de Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="register-insights-provider"></a>Registro del proveedor de Insights

En orden para el flujo de registro toowork correctamente, Hola **Microsoft.Insights** proveedor debe estar registrado. Si no está seguro de si hello **Microsoft.Insights** proveedor está registrado, hello ejecución siguiente secuencia de comandos.

```azurecli
az provider register --namespace Microsoft.Insights
```

## <a name="enable-network-security-group-flow-logs"></a>Habilitación de los registros de flujo de grupos de seguridad de red

Hola comando tooenable flujo registros se muestra en el siguiente ejemplo de Hola:

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled true --nsg nsgName --storage-account storageAccountName
```

## <a name="disable-network-security-group-flow-logs"></a>Deshabilitación de los registros de flujo de grupos de seguridad de red

Hola de uso después de registros de flujo de toodisable de ejemplo:

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled false --nsg nsgName
```

## <a name="download-a-flow-log"></a>Descarga de un registro de flujo

ubicación de almacenamiento de Hola de un registro de flujo se define en la creación. Un tooaccess herramienta adecuada estas cuentas de almacenamiento de tooa de guardar registros de flujo es Microsoft Azure Storage Explorer, que puede descargarse aquí: http://storageexplorer.com/

Si se especifica una cuenta de almacenamiento, archivos de captura de paquetes se guardan tooa cuenta de almacenamiento en hello ubicación siguiente:

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

Para obtener información acerca de la estructura de Hola de registro de hello visite [información general de registro de flujo de grupo de seguridad de red](network-watcher-nsg-flow-logging-overview.md)

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo demasiado[visualizar los registros de flujo NSG con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)

Obtenga información acerca de cómo demasiado[visualizar los registros de flujo NSG con herramientas de código abierto](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)
