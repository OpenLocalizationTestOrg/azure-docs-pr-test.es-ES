---
title: 'Flujo de grupo de seguridad de red registra aaaManage con Monitor de red de Azure: PowerShell | Documentos de Microsoft'
description: "Esta página explica cómo toomanage flujo de grupo de seguridad de red se registra en el Monitor de red de Azure con PowerShell"
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
ms.openlocfilehash: 987e8728fb6459fd6ff8eb5cd3d36ff855f2ccfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-with-powershell"></a><span data-ttu-id="d2433-103">Configuración de registros de flujo de grupos de seguridad de red con PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2433-103">Configuring Network Security Group Flow logs with PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="d2433-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="d2433-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="d2433-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2433-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="d2433-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d2433-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="d2433-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d2433-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="d2433-108">API DE REST</span><span class="sxs-lookup"><span data-stu-id="d2433-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="d2433-109">Registros de flujo de grupo de seguridad de red son una característica del Monitor de red que permite tooview información sobre el tráfico IP de entrada y de salida a través de un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="d2433-109">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="d2433-110">Estos registros de flujo se escriben en formato json y mostrar salidos y flujos de entrada en cada regla, Hola flujo Hola NIC que se aplica, tupla de 5 información acerca del flujo de hello (protocolo IP de origen/destino, puerto de origen/destino,) y si hello se permita el tráfico o denegado.</span><span class="sxs-lookup"><span data-stu-id="d2433-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="d2433-111">Registro del proveedor de Insights</span><span class="sxs-lookup"><span data-stu-id="d2433-111">Register Insights provider</span></span>

<span data-ttu-id="d2433-112">En orden para el flujo de registro toowork correctamente, Hola **Microsoft.Insights** proveedor debe estar registrado.</span><span class="sxs-lookup"><span data-stu-id="d2433-112">In order for flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="d2433-113">Si no está seguro de si hello **Microsoft.Insights** proveedor está registrado, hello ejecución siguiente secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="d2433-113">If you are not sure if hello **Microsoft.Insights** provider is registered, run hello following script.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Insights
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="d2433-114">Habilitación de los registros de flujo de grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="d2433-114">Enable Network Security Group Flow logs</span></span>

<span data-ttu-id="d2433-115">Hola comando tooenable flujo registros se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="d2433-115">hello command tooenable flow logs is shown in hello following example:</span></span>

```powershell
$NW = Get-AzurermNetworkWatcher -ResourceGroupName NetworkWatcherRg -Name NetworkWatcher_westcentralus
$nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName nsgRG-Name nsgName
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName StorageRG -Name contosostorage123
Get-AzureRmNetworkWatcherFlowLogStatus -NetworkWatcher $NW -TargetResourceId $nsg.Id
Set-AzureRmNetworkWatcherConfigFlowLog -NetworkWatcher $NW -TargetResourceId $nsg.Id -StorageAccountId $storageAccount.Id -EnableFlowLog $true
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="d2433-116">Deshabilitación de los registros de flujo de grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="d2433-116">Disable Network Security Group Flow logs</span></span>

<span data-ttu-id="d2433-117">Hola de uso después de registros de flujo de toodisable de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d2433-117">Use hello following example toodisable flow logs:</span></span>

```powershell
Set-AzureRmNetworkWatcherConfigFlowLog -NetworkWatcher $NW -TargetResourceId $nsg.Id -StorageAccountId $storageAccount.Id -EnableFlowLog $false
```

## <a name="download-a-flow-log"></a><span data-ttu-id="d2433-118">Descarga de un registro de flujo</span><span class="sxs-lookup"><span data-stu-id="d2433-118">Download a Flow log</span></span>

<span data-ttu-id="d2433-119">ubicación de almacenamiento de Hola de un registro de flujo se define en la creación.</span><span class="sxs-lookup"><span data-stu-id="d2433-119">hello storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="d2433-120">Un tooaccess herramienta adecuada estas cuentas de almacenamiento de tooa de guardar registros de flujo es Microsoft Azure Storage Explorer, que puede descargarse aquí: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="d2433-120">A convenient tool tooaccess these flow logs saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="d2433-121">Si se especifica una cuenta de almacenamiento, archivos de captura de paquetes se guardan tooa cuenta de almacenamiento en hello ubicación siguiente:</span><span class="sxs-lookup"><span data-stu-id="d2433-121">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="d2433-122">Para obtener información acerca de la estructura de Hola de registro de hello visite [información general de registro de flujo de grupo de seguridad de red](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d2433-122">For information about hello structure of hello log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2433-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d2433-123">Next Steps</span></span>

<span data-ttu-id="d2433-124">Obtenga información acerca de cómo demasiado[visualizar los registros de flujo NSG con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="d2433-124">Learn how too[Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="d2433-125">Obtenga información acerca de cómo demasiado[visualizar los registros de flujo NSG con herramientas de código abierto](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="d2433-125">Learn how too[Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
