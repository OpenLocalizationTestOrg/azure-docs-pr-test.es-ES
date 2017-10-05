---
title: "Solución de problemas de conexiones y puerta de enlace de Azure Virtual Network: PowerShell | Microsoft Docs"
description: "En esta página se explica cómo usar Azure Network Watcher para solucionar problemas con el cmdlet de PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: 0bdffbac18d1d236b7674feed4dbc784e50e0ea8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="a1a7a-103">Solución de problemas de las conexiones y la puerta de enlace de Virtual Network mediante PowerShell de Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="a1a7a-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a1a7a-104">Portal</span><span class="sxs-lookup"><span data-stu-id="a1a7a-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="a1a7a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a1a7a-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="a1a7a-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a1a7a-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="a1a7a-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a1a7a-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="a1a7a-108">API DE REST</span><span class="sxs-lookup"><span data-stu-id="a1a7a-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="a1a7a-109">Network Watcher proporciona numerosas funcionalidades con relación a los recursos de red de Azure.</span><span class="sxs-lookup"><span data-stu-id="a1a7a-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="a1a7a-110">Una de estas funcionalidades es la solución de problemas de recursos.</span><span class="sxs-lookup"><span data-stu-id="a1a7a-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="a1a7a-111">Se puede llamar a la solución de problemas de recursos mediante el portal, PowerShell, la CLI o la API de REST.</span><span class="sxs-lookup"><span data-stu-id="a1a7a-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="a1a7a-112">Cuando se llama a Network Watcher, este inspecciona el estado de una puerta de enlace de Virtual Network o de una conexión y devuelve sus conclusiones.</span><span class="sxs-lookup"><span data-stu-id="a1a7a-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a1a7a-113">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="a1a7a-113">Before you begin</span></span>

<span data-ttu-id="a1a7a-114">En este escenario, se da por hecho que ya ha seguido los pasos descritos en [Create an Azure Network Watcher instance](network-watcher-create.md) (Creación de una instancia de Azure Network Watcher) para crear una instancia de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="a1a7a-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="a1a7a-115">Para obtener una lista de los tipos de puerta de enlace compatibles, vea el artículo sobre los [tipos de puerta de enlace compatibles](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="a1a7a-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="a1a7a-116">Información general</span><span class="sxs-lookup"><span data-stu-id="a1a7a-116">Overview</span></span>

<span data-ttu-id="a1a7a-117">La solución de problemas de recursos permite solucionar los problemas que surgen con las puertas de enlace y las conexiones de Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="a1a7a-117">Resource troubleshooting provides the ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="a1a7a-118">Cuando se envía una solicitud para solucionar problemas de recursos, se consultan y se inspeccionan los registros.</span><span class="sxs-lookup"><span data-stu-id="a1a7a-118">When a request is made to resource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="a1a7a-119">Una vez finalizada la inspección, se devuelven los resultados.</span><span class="sxs-lookup"><span data-stu-id="a1a7a-119">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="a1a7a-120">Las solicitudes para solucionar problemas de recursos son de larga ejecución, y podrían tardar varios minutos en devolver un resultado.</span><span class="sxs-lookup"><span data-stu-id="a1a7a-120">Resource troubleshooting requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="a1a7a-121">Los registros de solución de problemas se almacenan en un contenedor en una cuenta de almacenamiento especificada.</span><span class="sxs-lookup"><span data-stu-id="a1a7a-121">The logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="a1a7a-122">Recuperación de Network Watcher</span><span class="sxs-lookup"><span data-stu-id="a1a7a-122">Retrieve Network Watcher</span></span>

<span data-ttu-id="a1a7a-123">El primer paso consiste en recuperar la instancia de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="a1a7a-123">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="a1a7a-124">La variable `$networkWatcher` se pasa al cmdlet `Start-AzureRmNetworkWatcherResourceTroubleshooting` en el paso 4.</span><span class="sxs-lookup"><span data-stu-id="a1a7a-124">The `$networkWatcher` variable is passed to the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="a1a7a-125">Recuperación de una conexión de puerta de enlace de Virtual Network</span><span class="sxs-lookup"><span data-stu-id="a1a7a-125">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="a1a7a-126">En este ejemplo, la solución de problemas de recursos se va a ejecutar en una conexión.</span><span class="sxs-lookup"><span data-stu-id="a1a7a-126">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="a1a7a-127">También puede pasarla una puerta de enlace de Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="a1a7a-127">You can also pass it a Virtual Network Gateway.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "2to3" -ResourceGroupName "testrg"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="a1a7a-128">Crear una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="a1a7a-128">Create a storage account</span></span>

<span data-ttu-id="a1a7a-129">La solución de problemas de recursos devuelve datos sobre el estado de mantenimiento del recurso; también guarda registros en una cuenta de almacenamiento para su revisión.</span><span class="sxs-lookup"><span data-stu-id="a1a7a-129">Resource troubleshooting returns data about the health of the resource, it also saves logs to a storage account to be reviewed.</span></span> <span data-ttu-id="a1a7a-130">En este paso, se crea una cuenta de almacenamiento; si ya existe una cuenta de almacenamiento, puede usarla.</span><span class="sxs-lookup"><span data-stu-id="a1a7a-130">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

```powershell
$sa = New-AzureRmStorageAccount -Name "contosoexamplesa" -SKU "Standard_LRS" -ResourceGroupName "testrg" -Location "WestCentralUS"
Set-AzureRmCurrentStorageAccount -ResourceGroupName $sa.ResourceGroupName -Name $sa.StorageAccountName
$sc = New-AzureStorageContainer -Name logs
```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="a1a7a-131">Ejecución de la solución de problemas de recursos Network Watcher</span><span class="sxs-lookup"><span data-stu-id="a1a7a-131">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="a1a7a-132">Los problemas de recursos se solucionan con el cmdlet `Start-AzureRmNetworkWatcherResourceTroubleshooting`.</span><span class="sxs-lookup"><span data-stu-id="a1a7a-132">You troubleshoot resources with the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet.</span></span> <span data-ttu-id="a1a7a-133">Pasamos el cmdlet, el objeto de Network Watcher, el identificador de la conexión o la puerta de enlace de Virtual Network, el identificador de la cuenta de almacenamiento y la ruta de acceso para almacenar los resultados.</span><span class="sxs-lookup"><span data-stu-id="a1a7a-133">We pass the cmdlet the Network Watcher object, the Id of the Connection or Virtual Network Gateway, the storage account id, and the path to store the results.</span></span>

> [!NOTE]
> <span data-ttu-id="a1a7a-134">El cmdlet `Start-AzureRmNetworkWatcherResourceTroubleshooting` es de larga ejecución y puede tardar unos minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="a1a7a-134">The `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet is long running and may take a few minutes to complete.</span></span>

```powershell
Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath "$($sa.PrimaryEndpoints.Blob)$($sc.name)"
```

<span data-ttu-id="a1a7a-135">Después de ejecutar el cmdlet, Network Watcher revisa los recursos para comprobar el estado.</span><span class="sxs-lookup"><span data-stu-id="a1a7a-135">Once you run the cmdlet, Network Watcher reviews the resource to verify the health.</span></span> <span data-ttu-id="a1a7a-136">Devuelve los resultados al shell y almacena los registros de los resultados en la cuenta de almacenamiento especificada.</span><span class="sxs-lookup"><span data-stu-id="a1a7a-136">It returns the results to the shell and stores logs of the results in the storage account specified.</span></span>

## <a name="understanding-the-results"></a><span data-ttu-id="a1a7a-137">Descripción de los resultados</span><span class="sxs-lookup"><span data-stu-id="a1a7a-137">Understanding the results</span></span>

<span data-ttu-id="a1a7a-138">El texto de la acción ofrece instrucciones generales sobre cómo resolver el problema.</span><span class="sxs-lookup"><span data-stu-id="a1a7a-138">The action text provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="a1a7a-139">Si se puede realizar una acción para el problema, se proporciona un vínculo con instrucciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="a1a7a-139">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="a1a7a-140">Si no hay instrucciones adicionales, la respuesta proporciona la dirección URL para abrir un caso de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="a1a7a-140">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="a1a7a-141">Para más información acerca de las propiedades de la respuesta y lo que incluye, consulte la [introducción a la solución de problemas en Network Watcher](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a1a7a-141">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="a1a7a-142">Para más instrucciones acerca de cómo descargar archivos desde cuentas de Azure Storage, consulte [Introducción a Azure Blob Storage mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="a1a7a-142">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="a1a7a-143">Otra herramienta que se puede utilizar es el Explorador de Storage.</span><span class="sxs-lookup"><span data-stu-id="a1a7a-143">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="a1a7a-144">Encontrará más información acerca del Explorador de Storage en el siguiente vínculo: [Explorador de Storage](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="a1a7a-144">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1a7a-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a1a7a-145">Next steps</span></span>

<span data-ttu-id="a1a7a-146">Si se cambió la configuración y la conectividad de VPN se ha detenido, consulte [Administración de grupos de seguridad de red](../virtual-network/virtual-network-manage-nsg-arm-portal.md) para realizar un seguimiento de los grupos de seguridad de red y las reglas de seguridad que pueden estar afectados.</span><span class="sxs-lookup"><span data-stu-id="a1a7a-146">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>
