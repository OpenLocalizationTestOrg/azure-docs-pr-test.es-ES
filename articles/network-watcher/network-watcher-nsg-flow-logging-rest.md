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
# <a name="configuring-network-security-group-flow-logs-using-rest-api"></a><span data-ttu-id="4ffa3-103">Configuración de registros de flujo de grupos de seguridad de red mediante la API de REST</span><span class="sxs-lookup"><span data-stu-id="4ffa3-103">Configuring Network Security Group flow logs using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="4ffa3-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="4ffa3-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="4ffa3-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ffa3-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="4ffa3-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="4ffa3-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="4ffa3-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4ffa3-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="4ffa3-108">API DE REST</span><span class="sxs-lookup"><span data-stu-id="4ffa3-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="4ffa3-109">Registros de flujo de grupo de seguridad de red son una característica del Monitor de red que permite tooview información sobre el tráfico IP de entrada y de salida a través de un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="4ffa3-109">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="4ffa3-110">Estos registros de flujo se escriben en formato json y mostrar salidos y flujos de entrada en cada regla, Hola flujo Hola NIC que se aplica, tupla de 5 información acerca del flujo de hello (protocolo IP de origen/destino, puerto de origen/destino,) y si hello se permita el tráfico o denegado.</span><span class="sxs-lookup"><span data-stu-id="4ffa3-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4ffa3-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="4ffa3-111">Before you begin</span></span>

<span data-ttu-id="4ffa3-112">ARMclient es la API de REST de hello toocall utilizados mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ffa3-112">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="4ffa3-113">ARMClient se encuentra en Chocolatey en [ARMClient en Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="4ffa3-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="4ffa3-114">Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.</span><span class="sxs-lookup"><span data-stu-id="4ffa3-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

> [!Important]
> <span data-ttu-id="4ffa3-115">Para la API de REST de Monitor de red llamadas Hola nombre de grupo de recursos en solicitud de hello que URI es el grupo de recursos de Hola que contiene Hola Monitor de red, no se está realizando acciones de diagnóstico de hello en recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4ffa3-115">For Network Watcher REST API calls hello resource group name in hello request URI is hello resource group that contains hello Network Watcher, not hello resources you are performing hello diagnostic actions on.</span></span>

## <a name="scenario"></a><span data-ttu-id="4ffa3-116">Escenario</span><span class="sxs-lookup"><span data-stu-id="4ffa3-116">Scenario</span></span>

<span data-ttu-id="4ffa3-117">escenario de Hello descrito en este artículo muestra cómo tooenable, deshabilitar y consulta fluyen registros con hello API de REST.</span><span class="sxs-lookup"><span data-stu-id="4ffa3-117">hello scenario covered in this article shows you how tooenable, disable, and query flow logs using hello REST API.</span></span> <span data-ttu-id="4ffa3-118">toolearn más información acerca de loggings de flujo de grupo de seguridad de red, visite [registro de flujo del grupo de seguridad de red: información general sobre](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4ffa3-118">toolearn more about Network Security Group flow loggings, visit [Network Security Group flow logging - Overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="4ffa3-119">En este escenario va a:</span><span class="sxs-lookup"><span data-stu-id="4ffa3-119">In this scenario, you will:</span></span>

* <span data-ttu-id="4ffa3-120">Habilitar los registros de flujo</span><span class="sxs-lookup"><span data-stu-id="4ffa3-120">Enable flow logs</span></span>
* <span data-ttu-id="4ffa3-121">Deshabilitar los registros de flujo</span><span class="sxs-lookup"><span data-stu-id="4ffa3-121">Disable flow logs</span></span>
* <span data-ttu-id="4ffa3-122">Consultar el estado de los registros de flujo</span><span class="sxs-lookup"><span data-stu-id="4ffa3-122">Query flow logs status</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="4ffa3-123">Inicio de sesión con ARMClient</span><span class="sxs-lookup"><span data-stu-id="4ffa3-123">Log in with ARMClient</span></span>

<span data-ttu-id="4ffa3-124">Inicie sesión en tooarmclient con sus credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="4ffa3-124">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="register-insights-provider"></a><span data-ttu-id="4ffa3-125">Registro del proveedor de Insights</span><span class="sxs-lookup"><span data-stu-id="4ffa3-125">Register Insights provider</span></span>

<span data-ttu-id="4ffa3-126">En orden para el flujo de registro toowork correctamente, Hola **Microsoft.Insights** proveedor debe estar registrado.</span><span class="sxs-lookup"><span data-stu-id="4ffa3-126">In order for flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="4ffa3-127">Si no está seguro de si hello **Microsoft.Insights** proveedor está registrado, hello ejecución siguiente secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="4ffa3-127">If you are not sure if hello **Microsoft.Insights** provider is registered, run hello following script.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
armclient post "https://management.azure.com//subscriptions/${subscriptionId}/providers/Microsoft.Insights/register?api-version=2016-09-01"
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="4ffa3-128">Habilitación de los registros de flujo de grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="4ffa3-128">Enable Network Security Group flow logs</span></span>

<span data-ttu-id="4ffa3-129">Hola comando tooenable flujo registros se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="4ffa3-129">hello command tooenable flow logs is shown in hello following example:</span></span>

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

<span data-ttu-id="4ffa3-130">Hola devolvió una respuesta Hola anterior es el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4ffa3-130">hello response returned from hello preceding example is as follows:</span></span>

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

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="4ffa3-131">Deshabilitación de los registros de flujo de grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="4ffa3-131">Disable Network Security Group flow logs</span></span>

<span data-ttu-id="4ffa3-132">Hola de uso después de registros de flujo de toodisable de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="4ffa3-132">Use hello following example toodisable flow logs.</span></span> <span data-ttu-id="4ffa3-133">Hola llamada es Hola igual que habilitar los registros de flujo, excepto **false** está establecido para la propiedad de hello habilitado.</span><span class="sxs-lookup"><span data-stu-id="4ffa3-133">hello call is hello same as enabling flow logs, except **false** is set for hello enabled property.</span></span>

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

<span data-ttu-id="4ffa3-134">Hola devolvió una respuesta Hola anterior es el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4ffa3-134">hello response returned from hello preceding example is as follows:</span></span>

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

## <a name="query-flow-logs"></a><span data-ttu-id="4ffa3-135">Consulta del estado de los registros de flujo</span><span class="sxs-lookup"><span data-stu-id="4ffa3-135">Query flow logs</span></span>

<span data-ttu-id="4ffa3-136">Hola sigue a llamada REST consultas Hola estado del flujo de registros en un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="4ffa3-136">hello following REST call queries hello status of flow logs on a Network Security Group.</span></span>

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

<span data-ttu-id="4ffa3-137">Hola te mostramos un ejemplo de respuesta de hello devuelta:</span><span class="sxs-lookup"><span data-stu-id="4ffa3-137">hello following is an example of hello response returned:</span></span>

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

## <a name="download-a-flow-log"></a><span data-ttu-id="4ffa3-138">Descarga de un registro de flujo</span><span class="sxs-lookup"><span data-stu-id="4ffa3-138">Download a flow log</span></span>

<span data-ttu-id="4ffa3-139">ubicación de almacenamiento de Hola de un registro de flujo se define en la creación.</span><span class="sxs-lookup"><span data-stu-id="4ffa3-139">hello storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="4ffa3-140">Un tooaccess herramienta adecuada estas cuentas de almacenamiento de tooa de guardar registros de flujo es Microsoft Azure Storage Explorer, que puede descargarse aquí: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="4ffa3-140">A convenient tool tooaccess these flow logs saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="4ffa3-141">Si se especifica una cuenta de almacenamiento, archivos de captura de paquetes se guardan tooa cuenta de almacenamiento en hello ubicación siguiente:</span><span class="sxs-lookup"><span data-stu-id="4ffa3-141">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

## <a name="next-steps"></a><span data-ttu-id="4ffa3-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4ffa3-142">Next steps</span></span>

<span data-ttu-id="4ffa3-143">Obtenga información acerca de cómo demasiado[visualizar los registros de flujo NSG con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="4ffa3-143">Learn how too[Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="4ffa3-144">Obtenga información acerca de cómo demasiado[visualizar los registros de flujo NSG con herramientas de código abierto](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="4ffa3-144">Learn how too[Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
