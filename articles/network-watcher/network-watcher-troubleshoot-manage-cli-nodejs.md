---
title: aaaTroubleshoot conexiones - 1.0 de CLI de Azure y Azure puerta de enlace de red Virtual | Documentos de Microsoft
description: "Esta página explica cómo solucionar problemas de hello toouse Monitor de red de Azure 1.0 de CLI de Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2838bc61-b182-4da8-8533-27db8fdbd177
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: a0511689d773f9c7216b0fe5470e27f754eb600b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-10"></a><span data-ttu-id="81b38-103">Solución de problemas de puerta de enlace y conexiones de Virtual Network mediante la CLI de Azure 1.0 de Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="81b38-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="81b38-104">Portal</span><span class="sxs-lookup"><span data-stu-id="81b38-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="81b38-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="81b38-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="81b38-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="81b38-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="81b38-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="81b38-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="81b38-108">API DE REST</span><span class="sxs-lookup"><span data-stu-id="81b38-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="81b38-109">Monitor de red proporciona muchas de las capacidades en lo referente a toounderstanding los recursos de red en Azure.</span><span class="sxs-lookup"><span data-stu-id="81b38-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="81b38-110">Una de estas funcionalidades es la solución de problemas de recursos.</span><span class="sxs-lookup"><span data-stu-id="81b38-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="81b38-111">Solución de problemas de recursos se puede llamar a través del portal de hello, PowerShell, CLI o API de REST.</span><span class="sxs-lookup"><span data-stu-id="81b38-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="81b38-112">Cuando se llama, Monitor de red inspecciona el estado de saludo de una puerta de enlace de red Virtual o una conexión y devuelve sus conclusiones.</span><span class="sxs-lookup"><span data-stu-id="81b38-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="81b38-113">En este artículo, se utiliza la multiplataforma Azure CLI 1.0, que está disponible para Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="81b38-113">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="81b38-114">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="81b38-114">Before you begin</span></span>

<span data-ttu-id="81b38-115">Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.</span><span class="sxs-lookup"><span data-stu-id="81b38-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="81b38-116">Para obtener una lista de los tipos de puerta de enlace compatibles, vea el artículo sobre los [tipos de puerta de enlace compatibles](/network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="81b38-116">For a list of supported gateway types visit, [Supported Gateway types](/network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="81b38-117">Información general</span><span class="sxs-lookup"><span data-stu-id="81b38-117">Overview</span></span>

<span data-ttu-id="81b38-118">Solución de problemas de recursos de hello permite solucionar los problemas que surgen con puertas de enlace de red Virtual y las conexiones.</span><span class="sxs-lookup"><span data-stu-id="81b38-118">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="81b38-119">Cuando se realiza una solicitud de solución de problemas de tooresource, los registros se va a consultar e inspeccionar.</span><span class="sxs-lookup"><span data-stu-id="81b38-119">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="81b38-120">Una vez finalizada la inspección, se devuelven resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="81b38-120">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="81b38-121">Solicitudes de recursos para solucionar problemas de las solicitudes son de largos ejecución, este proceso puede tardar varios tooreturn minutos un resultado.</span><span class="sxs-lookup"><span data-stu-id="81b38-121">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="81b38-122">registros de Hola de solución de problemas se almacenan en un contenedor en una cuenta de almacenamiento especificado.</span><span class="sxs-lookup"><span data-stu-id="81b38-122">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="81b38-123">Recuperación de una conexión de puerta de enlace de Virtual Network</span><span class="sxs-lookup"><span data-stu-id="81b38-123">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="81b38-124">En este ejemplo, la solución de problemas de recursos se va a ejecutar en una conexión.</span><span class="sxs-lookup"><span data-stu-id="81b38-124">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="81b38-125">También puede pasarla una puerta de enlace de Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="81b38-125">You can also pass it a Virtual Network Gateway.</span></span> <span data-ttu-id="81b38-126">Hello siguiente cmdlet enumera Hola conexiones vpn en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="81b38-126">hello following cmdlet lists hello vpn-connections in a resource group.</span></span>

```azurecli
azure network vpn-connection list -g resourceGroupName
```

<span data-ttu-id="81b38-127">También puede ejecutar Hola comando toosee conexiones hello en una suscripción.</span><span class="sxs-lookup"><span data-stu-id="81b38-127">You can also run hello command toosee hello connections in a subscription.</span></span>

```azurecli
azure network vpn-connection list -s subscription
```

<span data-ttu-id="81b38-128">Una vez que tenga el nombre de Hola de conexión de hello, puede ejecutar este comando tooget su Id. de recurso:</span><span class="sxs-lookup"><span data-stu-id="81b38-128">Once you have hello name of hello connection, you can run this command tooget its resource Id:</span></span>

```azurecli
azure network vpn-connection show -g resourceGroupName -n connectionName
```

## <a name="create-a-storage-account"></a><span data-ttu-id="81b38-129">Crear una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="81b38-129">Create a storage account</span></span>

<span data-ttu-id="81b38-130">Solución de problemas de recursos devuelve datos sobre el estado de saludo del recurso de hello, también guarda la cuenta de almacenamiento de registros tooa toobe revisado.</span><span class="sxs-lookup"><span data-stu-id="81b38-130">Resource troubleshooting returns data about hello health of hello resource, it also saves logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="81b38-131">En este paso, se crea una cuenta de almacenamiento; si ya existe una cuenta de almacenamiento, puede usarla.</span><span class="sxs-lookup"><span data-stu-id="81b38-131">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

1. <span data-ttu-id="81b38-132">Crear cuenta de almacenamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="81b38-132">Create hello storage account</span></span>

    ```azurecli
    azure storage account create -n storageAccountName -l location -g resourceGroupName
    ```

1. <span data-ttu-id="81b38-133">Obtener claves de cuenta de almacenamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="81b38-133">Get hello storage account keys</span></span>

    ```azurecli
    azure storage account keys list storageAccountName -g resourcegroupName
    ```

1. <span data-ttu-id="81b38-134">Crear contenedor de Hola</span><span class="sxs-lookup"><span data-stu-id="81b38-134">Create hello container</span></span>

    ```azurecli
    azure storage container create --account-name storageAccountName -g resourcegroupName --account-key {storageAccountKey} --container logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="81b38-135">Ejecución de la solución de problemas de recursos Network Watcher</span><span class="sxs-lookup"><span data-stu-id="81b38-135">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="81b38-136">Solucionar problemas de recursos con hello `network watcher troubleshoot` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="81b38-136">You troubleshoot resources with hello `network watcher troubleshoot` cmdlet.</span></span> <span data-ttu-id="81b38-137">Pasamos el grupo de recursos de hello cmdlet hello, nombre de Monitor de red, Hola Id. de conexión de hello, hello Hola Hola Id. de cuenta de almacenamiento de Hola y Hola ruta de acceso toohello blob toostore Hola solucionar da como resultado.</span><span class="sxs-lookup"><span data-stu-id="81b38-137">We pass hello cmdlet hello resource group, hello name of hello Network Watcher, hello Id of hello connection, hello Id of hello storage account, and hello path toohello blob toostore hello troubleshoot results in.</span></span>

```azurecli
azure network watcher troubleshoot -g resourceGroupName -n networkWatcherName -t connectionId -i storageId -p storagePath
```

<span data-ttu-id="81b38-138">Una vez que ejecute el cmdlet de hello, Monitor de red se revisan mantenimiento de hello recursos tooverify Hola.</span><span class="sxs-lookup"><span data-stu-id="81b38-138">Once you run hello cmdlet, Network Watcher reviews hello resource tooverify hello health.</span></span> <span data-ttu-id="81b38-139">Devuelve los resultados de hello toohello shell y almacena los registros de los resultados de hello en hello cuenta de almacenamiento especificada.</span><span class="sxs-lookup"><span data-stu-id="81b38-139">It returns hello results toohello shell and stores logs of hello results in hello storage account specified.</span></span>

## <a name="understanding-hello-results"></a><span data-ttu-id="81b38-140">Descripción de los resultados de Hola</span><span class="sxs-lookup"><span data-stu-id="81b38-140">Understanding hello results</span></span>

<span data-ttu-id="81b38-141">texto de acción de Hello ofrece instrucciones generales sobre cómo tooresolve Hola problema.</span><span class="sxs-lookup"><span data-stu-id="81b38-141">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="81b38-142">Si el problema de Hola se pueda realizar una acción, se proporciona un vínculo con instrucciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="81b38-142">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="81b38-143">En caso de hello donde no haya ninguna orientación adicional, respuesta de hello proporciona Hola url tooopen un caso de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="81b38-143">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="81b38-144">Para obtener más información acerca de las propiedades de Hola de respuesta de Hola y qué se incluye, visite [información general de solución de problemas del Monitor de red](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="81b38-144">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="81b38-145">Para obtener instrucciones acerca de cómo descargar archivos desde cuentas de almacenamiento de azure, consulte demasiado[Introducción al almacenamiento de blobs de Azure mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="81b38-145">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="81b38-146">Otra herramienta que se puede utilizar es el Explorador de Storage.</span><span class="sxs-lookup"><span data-stu-id="81b38-146">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="81b38-147">Para obtener más información acerca del explorador de almacenamiento puede encontrarse aquí en hello siguiente vínculo: [Explorador de almacenamiento](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="81b38-147">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="81b38-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="81b38-148">Next steps</span></span>

<span data-ttu-id="81b38-149">Si se cambiaron las configuraciones que detenga la conectividad de VPN, consulte [administrar grupos de seguridad de red](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hacia abajo Hola red seguridad y el grupo de reglas de seguridad que pueden estar en cuestión.</span><span class="sxs-lookup"><span data-stu-id="81b38-149">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
