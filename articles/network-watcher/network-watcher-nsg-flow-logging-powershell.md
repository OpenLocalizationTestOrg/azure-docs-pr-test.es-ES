---
title: "Administración de registros de flujo de grupos de seguridad de red en Azure Network Watcher (PowerShell) | Microsoft Docs"
description: "En esta página se explica cómo administrar registros de flujo de grupos de seguridad de red en Azure Network Watcher con PowerShell."
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
ms.openlocfilehash: 9fa2e2e1c09b119bd2a1e149fd2cc080957af296
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-network-security-group-flow-logs-with-powershell"></a><span data-ttu-id="3f4b8-103">Configuración de registros de flujo de grupos de seguridad de red con PowerShell</span><span class="sxs-lookup"><span data-stu-id="3f4b8-103">Configuring Network Security Group Flow logs with PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="3f4b8-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="3f4b8-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="3f4b8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3f4b8-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="3f4b8-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="3f4b8-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="3f4b8-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3f4b8-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="3f4b8-108">API DE REST</span><span class="sxs-lookup"><span data-stu-id="3f4b8-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="3f4b8-109">Los registros de flujo de grupos de seguridad de red son una característica de Network Watcher que permite ver información acerca del tráfico IP de entrada y de salida en un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="3f4b8-109">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="3f4b8-110">Estos registros de flujo se escriben en formato JSON y muestran los flujos de entrada y salida en función de cada regla, la NIC a la que se aplica el flujo, información de 5-tupla sobre el flujo (IP de origen/destino, puerto de origen/destino, protocolo), y si se permitió o denegó el tráfico.</span><span class="sxs-lookup"><span data-stu-id="3f4b8-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="3f4b8-111">Registro del proveedor de Insights</span><span class="sxs-lookup"><span data-stu-id="3f4b8-111">Register Insights provider</span></span>

<span data-ttu-id="3f4b8-112">Para que el registro del flujo de trabajo funcione correctamente, es necesario registrar el proveedor **Microsoft.Insights**.</span><span class="sxs-lookup"><span data-stu-id="3f4b8-112">In order for flow logging to work successfully, the **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="3f4b8-113">Si no está seguro de si el proveedor **Microsoft.Insights**está registrado, ejecute el siguiente script.</span><span class="sxs-lookup"><span data-stu-id="3f4b8-113">If you are not sure if the **Microsoft.Insights** provider is registered, run the following script.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Insights
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="3f4b8-114">Habilitación de los registros de flujo de grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="3f4b8-114">Enable Network Security Group Flow logs</span></span>

<span data-ttu-id="3f4b8-115">El ejemplo siguiente muestra el comando para habilitar los registros de flujo:</span><span class="sxs-lookup"><span data-stu-id="3f4b8-115">The command to enable flow logs is shown in the following example:</span></span>

```powershell
$NW = Get-AzurermNetworkWatcher -ResourceGroupName NetworkWatcherRg -Name NetworkWatcher_westcentralus
$nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName nsgRG-Name nsgName
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName StorageRG -Name contosostorage123
Get-AzureRmNetworkWatcherFlowLogStatus -NetworkWatcher $NW -TargetResourceId $nsg.Id
Set-AzureRmNetworkWatcherConfigFlowLog -NetworkWatcher $NW -TargetResourceId $nsg.Id -StorageAccountId $storageAccount.Id -EnableFlowLog $true
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="3f4b8-116">Deshabilitación de los registros de flujo de grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="3f4b8-116">Disable Network Security Group Flow logs</span></span>

<span data-ttu-id="3f4b8-117">Use el ejemplo siguiente para deshabilitar los registros de flujo:</span><span class="sxs-lookup"><span data-stu-id="3f4b8-117">Use the following example to disable flow logs:</span></span>

```powershell
Set-AzureRmNetworkWatcherConfigFlowLog -NetworkWatcher $NW -TargetResourceId $nsg.Id -StorageAccountId $storageAccount.Id -EnableFlowLog $false
```

## <a name="download-a-flow-log"></a><span data-ttu-id="3f4b8-118">Descarga de un registro de flujo</span><span class="sxs-lookup"><span data-stu-id="3f4b8-118">Download a Flow log</span></span>

<span data-ttu-id="3f4b8-119">La ubicación de almacenamiento de un registro de flujo se define en el momento de la creación.</span><span class="sxs-lookup"><span data-stu-id="3f4b8-119">The storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="3f4b8-120">Una herramienta práctica para acceder a estos registros de flujo guardados en una cuenta de almacenamiento es el Explorador de Microsoft Azure Storage, que puede descargarse aquí: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="3f4b8-120">A convenient tool to access these flow logs saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="3f4b8-121">Si se especifica una cuenta de almacenamiento, los archivos de captura de paquetes se guardan en una cuenta de almacenamiento en la siguiente ubicación:</span><span class="sxs-lookup"><span data-stu-id="3f4b8-121">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="3f4b8-122">Para más información sobre la estructura del registro, vea la [introducción a los registros de flujo de grupos de seguridad de red](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3f4b8-122">For information about the structure of the log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f4b8-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3f4b8-123">Next Steps</span></span>

<span data-ttu-id="3f4b8-124">Obtenga información sobre cómo [visualizar los registros de flujo de NSG con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="3f4b8-124">Learn how to [Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="3f4b8-125">Aprenda a [visualizar los registros de flujo de NSG con herramientas de código abierto](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="3f4b8-125">Learn how to [Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>