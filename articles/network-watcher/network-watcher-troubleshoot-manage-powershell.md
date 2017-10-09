---
title: aaaTroubleshoot puerta de enlace de red Virtual Azure y conexiones, PowerShell | Documentos de Microsoft
description: "Esta página explica cómo solucionar problemas de cmdlet de PowerShell hello toouse Monitor de red de Azure"
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
ms.openlocfilehash: b7dbe6e44e0fa1ea0481223a84098d7a57c068a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="1109f-103">Solución de problemas de las conexiones y la puerta de enlace de Virtual Network mediante PowerShell de Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="1109f-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="1109f-104">Portal</span><span class="sxs-lookup"><span data-stu-id="1109f-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="1109f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1109f-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="1109f-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1109f-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="1109f-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1109f-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="1109f-108">API DE REST</span><span class="sxs-lookup"><span data-stu-id="1109f-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="1109f-109">Monitor de red proporciona muchas de las capacidades en lo referente a toounderstanding los recursos de red en Azure.</span><span class="sxs-lookup"><span data-stu-id="1109f-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="1109f-110">Una de estas funcionalidades es la solución de problemas de recursos.</span><span class="sxs-lookup"><span data-stu-id="1109f-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="1109f-111">Solución de problemas de recursos se puede llamar a través del portal de hello, PowerShell, CLI o API de REST.</span><span class="sxs-lookup"><span data-stu-id="1109f-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="1109f-112">Cuando se llama, Monitor de red inspecciona el estado de saludo de una puerta de enlace de red Virtual o una conexión y devuelve sus conclusiones.</span><span class="sxs-lookup"><span data-stu-id="1109f-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1109f-113">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="1109f-113">Before you begin</span></span>

<span data-ttu-id="1109f-114">Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.</span><span class="sxs-lookup"><span data-stu-id="1109f-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="1109f-115">Para obtener una lista de los tipos de puerta de enlace compatibles, vea el artículo sobre los [tipos de puerta de enlace compatibles](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="1109f-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="1109f-116">Información general</span><span class="sxs-lookup"><span data-stu-id="1109f-116">Overview</span></span>

<span data-ttu-id="1109f-117">Solución de problemas de recursos de hello permite solucionar los problemas que surgen con puertas de enlace de red Virtual y las conexiones.</span><span class="sxs-lookup"><span data-stu-id="1109f-117">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="1109f-118">Cuando se realiza una solicitud de solución de problemas de tooresource, los registros se va a consultar e inspeccionar.</span><span class="sxs-lookup"><span data-stu-id="1109f-118">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="1109f-119">Una vez finalizada la inspección, se devuelven resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="1109f-119">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="1109f-120">Solicitudes de recursos para solucionar problemas de las solicitudes son de largos ejecución, este proceso puede tardar varios tooreturn minutos un resultado.</span><span class="sxs-lookup"><span data-stu-id="1109f-120">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="1109f-121">registros de Hola de solución de problemas se almacenan en un contenedor en una cuenta de almacenamiento especificado.</span><span class="sxs-lookup"><span data-stu-id="1109f-121">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="1109f-122">Recuperación de Network Watcher</span><span class="sxs-lookup"><span data-stu-id="1109f-122">Retrieve Network Watcher</span></span>

<span data-ttu-id="1109f-123">Hola primer paso es instancia de Monitor de red de tooretrieve Hola.</span><span class="sxs-lookup"><span data-stu-id="1109f-123">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="1109f-124">Hola `$networkWatcher` pasa una variable toohello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet en el paso 4.</span><span class="sxs-lookup"><span data-stu-id="1109f-124">hello `$networkWatcher` variable is passed toohello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="1109f-125">Recuperación de una conexión de puerta de enlace de Virtual Network</span><span class="sxs-lookup"><span data-stu-id="1109f-125">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="1109f-126">En este ejemplo, la solución de problemas de recursos se va a ejecutar en una conexión.</span><span class="sxs-lookup"><span data-stu-id="1109f-126">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="1109f-127">También puede pasarla una puerta de enlace de Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="1109f-127">You can also pass it a Virtual Network Gateway.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "2to3" -ResourceGroupName "testrg"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="1109f-128">Crear una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="1109f-128">Create a storage account</span></span>

<span data-ttu-id="1109f-129">Solución de problemas de recursos devuelve datos sobre el estado de saludo del recurso de hello, también guarda la cuenta de almacenamiento de registros tooa toobe revisado.</span><span class="sxs-lookup"><span data-stu-id="1109f-129">Resource troubleshooting returns data about hello health of hello resource, it also saves logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="1109f-130">En este paso, se crea una cuenta de almacenamiento; si ya existe una cuenta de almacenamiento, puede usarla.</span><span class="sxs-lookup"><span data-stu-id="1109f-130">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

```powershell
$sa = New-AzureRmStorageAccount -Name "contosoexamplesa" -SKU "Standard_LRS" -ResourceGroupName "testrg" -Location "WestCentralUS"
Set-AzureRmCurrentStorageAccount -ResourceGroupName $sa.ResourceGroupName -Name $sa.StorageAccountName
$sc = New-AzureStorageContainer -Name logs
```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="1109f-131">Ejecución de la solución de problemas de recursos Network Watcher</span><span class="sxs-lookup"><span data-stu-id="1109f-131">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="1109f-132">Solucionar problemas de recursos con hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1109f-132">You troubleshoot resources with hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet.</span></span> <span data-ttu-id="1109f-133">Se pasan el objeto de Monitor de red de hello cmdlet hello, Hola Id. de conexión de Hola o puerta de enlace de red Virtual, Id. de cuenta de almacenamiento de Hola y Hola ruta de acceso toostore Hola da.</span><span class="sxs-lookup"><span data-stu-id="1109f-133">We pass hello cmdlet hello Network Watcher object, hello Id of hello Connection or Virtual Network Gateway, hello storage account id, and hello path toostore hello results.</span></span>

> [!NOTE]
> <span data-ttu-id="1109f-134">Hola `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet es de larga ejecución y puede tardar unos toocomplete minutos.</span><span class="sxs-lookup"><span data-stu-id="1109f-134">hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet is long running and may take a few minutes toocomplete.</span></span>

```powershell
Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath "$($sa.PrimaryEndpoints.Blob)$($sc.name)"
```

<span data-ttu-id="1109f-135">Una vez que ejecute el cmdlet de hello, Monitor de red se revisan mantenimiento de hello recursos tooverify Hola.</span><span class="sxs-lookup"><span data-stu-id="1109f-135">Once you run hello cmdlet, Network Watcher reviews hello resource tooverify hello health.</span></span> <span data-ttu-id="1109f-136">Devuelve los resultados de hello toohello shell y almacena los registros de los resultados de hello en hello cuenta de almacenamiento especificada.</span><span class="sxs-lookup"><span data-stu-id="1109f-136">It returns hello results toohello shell and stores logs of hello results in hello storage account specified.</span></span>

## <a name="understanding-hello-results"></a><span data-ttu-id="1109f-137">Descripción de los resultados de Hola</span><span class="sxs-lookup"><span data-stu-id="1109f-137">Understanding hello results</span></span>

<span data-ttu-id="1109f-138">texto de acción de Hello ofrece instrucciones generales sobre cómo tooresolve Hola problema.</span><span class="sxs-lookup"><span data-stu-id="1109f-138">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="1109f-139">Si el problema de Hola se pueda realizar una acción, se proporciona un vínculo con instrucciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="1109f-139">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="1109f-140">En caso de hello donde no haya ninguna orientación adicional, respuesta de hello proporciona Hola url tooopen un caso de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="1109f-140">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="1109f-141">Para obtener más información acerca de las propiedades de Hola de respuesta de Hola y qué se incluye, visite [información general de solución de problemas del Monitor de red](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="1109f-141">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="1109f-142">Para obtener instrucciones acerca de cómo descargar archivos desde cuentas de almacenamiento de azure, consulte demasiado[Introducción al almacenamiento de blobs de Azure mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="1109f-142">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="1109f-143">Otra herramienta que se puede utilizar es el Explorador de Storage.</span><span class="sxs-lookup"><span data-stu-id="1109f-143">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="1109f-144">Para obtener más información acerca del explorador de almacenamiento puede encontrarse aquí en hello siguiente vínculo: [Explorador de almacenamiento](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="1109f-144">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="1109f-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1109f-145">Next steps</span></span>

<span data-ttu-id="1109f-146">Si se cambiaron las configuraciones que detenga la conectividad de VPN, consulte [administrar grupos de seguridad de red](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hacia abajo Hola red seguridad y el grupo de reglas de seguridad que pueden estar en cuestión.</span><span class="sxs-lookup"><span data-stu-id="1109f-146">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
