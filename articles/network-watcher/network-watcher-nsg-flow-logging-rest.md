---
title: "Administración de registros de flujo de grupos de seguridad de red en Azure Network Watcher: API de REST| Microsoft Docs"
description: "Esta página explica cómo administrar registros de flujo de grupos de seguridad de red en Azure Network Watcher con la API de REST"
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
ms.openlocfilehash: c89a2ab4c39978771c940a819493b4e2283d5f9f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-network-security-group-flow-logs-using-rest-api"></a><span data-ttu-id="34a84-103">Configuración de registros de flujo de grupos de seguridad de red mediante la API de REST</span><span class="sxs-lookup"><span data-stu-id="34a84-103">Configuring Network Security Group flow logs using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="34a84-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="34a84-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="34a84-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="34a84-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="34a84-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="34a84-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="34a84-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="34a84-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="34a84-108">API DE REST</span><span class="sxs-lookup"><span data-stu-id="34a84-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="34a84-109">Los registros de flujo de grupos de seguridad de red son una característica de Network Watcher que permite ver información acerca del tráfico IP de entrada y de salida en un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="34a84-109">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="34a84-110">Estos registros de flujo se escriben en formato JSON y muestran los flujos de entrada y salida en función de cada regla, la NIC a la que se aplica el flujo, información de 5-tupla sobre el flujo (IP de origen/destino, puerto de origen/destino, protocolo), y si se permitió o denegó el tráfico.</span><span class="sxs-lookup"><span data-stu-id="34a84-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="34a84-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="34a84-111">Before you begin</span></span>

<span data-ttu-id="34a84-112">ARMclient se usa para llamar a la API de REST con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="34a84-112">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="34a84-113">ARMClient se encuentra en Chocolatey en [ARMClient en Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="34a84-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="34a84-114">En este escenario, se da por hecho que ya ha seguido los pasos descritos en [Create an Azure Network Watcher instance](network-watcher-create.md) (Creación de una instancia de Azure Network Watcher) para crear una instancia de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="34a84-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

> [!Important]
> <span data-ttu-id="34a84-115">En las llamadas a la API de REST de Network Watcher, el nombre del grupo de recursos en el identificador URI de la solicitud es el grupo de recursos que contiene Network Watcher, y no los recursos sobre los que realiza las acciones de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="34a84-115">For Network Watcher REST API calls the resource group name in the request URI is the resource group that contains the Network Watcher, not the resources you are performing the diagnostic actions on.</span></span>

## <a name="scenario"></a><span data-ttu-id="34a84-116">Escenario</span><span class="sxs-lookup"><span data-stu-id="34a84-116">Scenario</span></span>

<span data-ttu-id="34a84-117">El escenario descrito en este artículo muestra cómo habilitar, deshabilitar y realizar consultas de los registros de flujo con la API de REST.</span><span class="sxs-lookup"><span data-stu-id="34a84-117">The scenario covered in this article shows you how to enable, disable, and query flow logs using the REST API.</span></span> <span data-ttu-id="34a84-118">Para más información sobre registros de flujos de grupo de seguridad de red, consulte la [introducción al registro de flujos de grupo de seguridad de red](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="34a84-118">To learn more about Network Security Group flow loggings, visit [Network Security Group flow logging - Overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="34a84-119">En este escenario va a:</span><span class="sxs-lookup"><span data-stu-id="34a84-119">In this scenario, you will:</span></span>

* <span data-ttu-id="34a84-120">Habilitar los registros de flujo</span><span class="sxs-lookup"><span data-stu-id="34a84-120">Enable flow logs</span></span>
* <span data-ttu-id="34a84-121">Deshabilitar los registros de flujo</span><span class="sxs-lookup"><span data-stu-id="34a84-121">Disable flow logs</span></span>
* <span data-ttu-id="34a84-122">Consultar el estado de los registros de flujo</span><span class="sxs-lookup"><span data-stu-id="34a84-122">Query flow logs status</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="34a84-123">Inicio de sesión con ARMClient</span><span class="sxs-lookup"><span data-stu-id="34a84-123">Log in with ARMClient</span></span>

<span data-ttu-id="34a84-124">Inicie sesión en armclient con las credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="34a84-124">Log in to armclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="register-insights-provider"></a><span data-ttu-id="34a84-125">Registro del proveedor de Insights</span><span class="sxs-lookup"><span data-stu-id="34a84-125">Register Insights provider</span></span>

<span data-ttu-id="34a84-126">Para que el registro del flujo de trabajo funcione correctamente, es necesario registrar el proveedor **Microsoft.Insights**.</span><span class="sxs-lookup"><span data-stu-id="34a84-126">In order for flow logging to work successfully, the **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="34a84-127">Si no está seguro de si el proveedor **Microsoft.Insights**está registrado, ejecute el siguiente script.</span><span class="sxs-lookup"><span data-stu-id="34a84-127">If you are not sure if the **Microsoft.Insights** provider is registered, run the following script.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
armclient post "https://management.azure.com//subscriptions/${subscriptionId}/providers/Microsoft.Insights/register?api-version=2016-09-01"
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="34a84-128">Habilitación de los registros de flujo de grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="34a84-128">Enable Network Security Group flow logs</span></span>

<span data-ttu-id="34a84-129">El ejemplo siguiente muestra el comando para habilitar los registros de flujo:</span><span class="sxs-lookup"><span data-stu-id="34a84-129">The command to enable flow logs is shown in the following example:</span></span>

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

<span data-ttu-id="34a84-130">La respuesta devuelta por el ejemplo anterior es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="34a84-130">The response returned from the preceding example is as follows:</span></span>

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

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="34a84-131">Deshabilitación de los registros de flujo de grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="34a84-131">Disable Network Security Group flow logs</span></span>

<span data-ttu-id="34a84-132">Use el ejemplo siguiente para deshabilitar los registros de flujo.</span><span class="sxs-lookup"><span data-stu-id="34a84-132">Use the following example to disable flow logs.</span></span> <span data-ttu-id="34a84-133">La llamada es la misma que para habilitar los registros de flujo, excepto que la propiedad activada está establecida en **false**.</span><span class="sxs-lookup"><span data-stu-id="34a84-133">The call is the same as enabling flow logs, except **false** is set for the enabled property.</span></span>

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

<span data-ttu-id="34a84-134">La respuesta devuelta por el ejemplo anterior es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="34a84-134">The response returned from the preceding example is as follows:</span></span>

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

## <a name="query-flow-logs"></a><span data-ttu-id="34a84-135">Consulta del estado de los registros de flujo</span><span class="sxs-lookup"><span data-stu-id="34a84-135">Query flow logs</span></span>

<span data-ttu-id="34a84-136">La siguiente llamada de REST consulta el estado del flujo de registros en un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="34a84-136">The following REST call queries the status of flow logs on a Network Security Group.</span></span>

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

<span data-ttu-id="34a84-137">El siguiente es un ejemplo de la respuesta devuelta:</span><span class="sxs-lookup"><span data-stu-id="34a84-137">The following is an example of the response returned:</span></span>

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

## <a name="download-a-flow-log"></a><span data-ttu-id="34a84-138">Descarga de un registro de flujo</span><span class="sxs-lookup"><span data-stu-id="34a84-138">Download a flow log</span></span>

<span data-ttu-id="34a84-139">La ubicación de almacenamiento de un registro de flujo se define en el momento de la creación.</span><span class="sxs-lookup"><span data-stu-id="34a84-139">The storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="34a84-140">Una herramienta práctica para acceder a estos registros de flujo guardados en una cuenta de almacenamiento es el Explorador de Microsoft Azure Storage, que puede descargarse aquí: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="34a84-140">A convenient tool to access these flow logs saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="34a84-141">Si se especifica una cuenta de almacenamiento, los archivos de captura de paquetes se guardan en una cuenta de almacenamiento en la siguiente ubicación:</span><span class="sxs-lookup"><span data-stu-id="34a84-141">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

## <a name="next-steps"></a><span data-ttu-id="34a84-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="34a84-142">Next steps</span></span>

<span data-ttu-id="34a84-143">Aprenda a [visualizar los registros de flujo de NSG con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="34a84-143">Learn how to [Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="34a84-144">Aprenda a [visualizar los registros de flujo de NSG con herramientas de código abierto](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="34a84-144">Learn how to [Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
