---
title: "Solución de problemas de puerta de enlace y conexiones de Azure Virtual Network con la CLI de Azure 1.0 | Microsoft Docs"
description: "En esta página se explica cómo usar Azure Network Watcher para solucionar problemas con la CLI de Azure 1.0."
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
ms.openlocfilehash: 9de4b2a0bdda7ffbd269883877a708d67312092f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-10"></a><span data-ttu-id="5063a-103">Solución de problemas de puerta de enlace y conexiones de Virtual Network mediante la CLI de Azure 1.0 de Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="5063a-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="5063a-104">Portal</span><span class="sxs-lookup"><span data-stu-id="5063a-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="5063a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5063a-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="5063a-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5063a-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="5063a-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5063a-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="5063a-108">API DE REST</span><span class="sxs-lookup"><span data-stu-id="5063a-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="5063a-109">Network Watcher proporciona numerosas funcionalidades con relación a los recursos de red de Azure.</span><span class="sxs-lookup"><span data-stu-id="5063a-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="5063a-110">Una de estas funcionalidades es la solución de problemas de recursos.</span><span class="sxs-lookup"><span data-stu-id="5063a-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="5063a-111">Se puede llamar a la solución de problemas de recursos mediante el portal, PowerShell, la CLI o la API de REST.</span><span class="sxs-lookup"><span data-stu-id="5063a-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="5063a-112">Cuando se llama a Network Watcher, este inspecciona el estado de una puerta de enlace de Virtual Network o de una conexión y devuelve sus conclusiones.</span><span class="sxs-lookup"><span data-stu-id="5063a-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="5063a-113">En este artículo, se utiliza la multiplataforma Azure CLI 1.0, que está disponible para Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="5063a-113">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="5063a-114">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="5063a-114">Before you begin</span></span>

<span data-ttu-id="5063a-115">En este escenario, se da por hecho que ya ha seguido los pasos descritos en [Create an Azure Network Watcher instance](network-watcher-create.md) (Creación de una instancia de Azure Network Watcher) para crear una instancia de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="5063a-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="5063a-116">Para obtener una lista de los tipos de puerta de enlace compatibles, vea el artículo sobre los [tipos de puerta de enlace compatibles](/network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="5063a-116">For a list of supported gateway types visit, [Supported Gateway types](/network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="5063a-117">Información general</span><span class="sxs-lookup"><span data-stu-id="5063a-117">Overview</span></span>

<span data-ttu-id="5063a-118">La solución de problemas de recursos permite solucionar los problemas que surgen con las puertas de enlace y las conexiones de Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="5063a-118">Resource troubleshooting provides the ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="5063a-119">Cuando se envía una solicitud para solucionar problemas de recursos, se consultan y se inspeccionan los registros.</span><span class="sxs-lookup"><span data-stu-id="5063a-119">When a request is made to resource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="5063a-120">Una vez finalizada la inspección, se devuelven los resultados.</span><span class="sxs-lookup"><span data-stu-id="5063a-120">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="5063a-121">Las solicitudes para solucionar problemas de recursos son de larga ejecución, y podrían tardar varios minutos en devolver un resultado.</span><span class="sxs-lookup"><span data-stu-id="5063a-121">Resource troubleshooting requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="5063a-122">Los registros de solución de problemas se almacenan en un contenedor en una cuenta de almacenamiento especificada.</span><span class="sxs-lookup"><span data-stu-id="5063a-122">The logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="5063a-123">Recuperación de una conexión de puerta de enlace de Virtual Network</span><span class="sxs-lookup"><span data-stu-id="5063a-123">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="5063a-124">En este ejemplo, la solución de problemas de recursos se va a ejecutar en una conexión.</span><span class="sxs-lookup"><span data-stu-id="5063a-124">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="5063a-125">También puede pasarla una puerta de enlace de Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="5063a-125">You can also pass it a Virtual Network Gateway.</span></span> <span data-ttu-id="5063a-126">El cmdlet siguiente enumera las conexiones de VPN en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5063a-126">The following cmdlet lists the vpn-connections in a resource group.</span></span>

```azurecli
azure network vpn-connection list -g resourceGroupName
```

<span data-ttu-id="5063a-127">También puede ejecutar el comando para ver las conexiones de una suscripción.</span><span class="sxs-lookup"><span data-stu-id="5063a-127">You can also run the command to see the connections in a subscription.</span></span>

```azurecli
azure network vpn-connection list -s subscription
```

<span data-ttu-id="5063a-128">Cuando tenga el nombre de la conexión, puede ejecutar este comando para obtener su identificador de recurso:</span><span class="sxs-lookup"><span data-stu-id="5063a-128">Once you have the name of the connection, you can run this command to get its resource Id:</span></span>

```azurecli
azure network vpn-connection show -g resourceGroupName -n connectionName
```

## <a name="create-a-storage-account"></a><span data-ttu-id="5063a-129">Crear una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="5063a-129">Create a storage account</span></span>

<span data-ttu-id="5063a-130">La solución de problemas de recursos devuelve datos sobre el estado de mantenimiento del recurso; también guarda registros en una cuenta de almacenamiento para su revisión.</span><span class="sxs-lookup"><span data-stu-id="5063a-130">Resource troubleshooting returns data about the health of the resource, it also saves logs to a storage account to be reviewed.</span></span> <span data-ttu-id="5063a-131">En este paso, se crea una cuenta de almacenamiento; si ya existe una cuenta de almacenamiento, puede usarla.</span><span class="sxs-lookup"><span data-stu-id="5063a-131">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

1. <span data-ttu-id="5063a-132">Creación de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="5063a-132">Create the storage account</span></span>

    ```azurecli
    azure storage account create -n storageAccountName -l location -g resourceGroupName
    ```

1. <span data-ttu-id="5063a-133">Obtenga las claves de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="5063a-133">Get the storage account keys</span></span>

    ```azurecli
    azure storage account keys list storageAccountName -g resourcegroupName
    ```

1. <span data-ttu-id="5063a-134">Cree el contenedor.</span><span class="sxs-lookup"><span data-stu-id="5063a-134">Create the container</span></span>

    ```azurecli
    azure storage container create --account-name storageAccountName -g resourcegroupName --account-key {storageAccountKey} --container logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="5063a-135">Ejecución de la solución de problemas de recursos Network Watcher</span><span class="sxs-lookup"><span data-stu-id="5063a-135">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="5063a-136">Los problemas de recursos se solucionan con el cmdlet `network watcher troubleshoot`.</span><span class="sxs-lookup"><span data-stu-id="5063a-136">You troubleshoot resources with the `network watcher troubleshoot` cmdlet.</span></span> <span data-ttu-id="5063a-137">Pasamos al cmdlet el grupo de recursos, el nombre de la instancia de Network Watcher, el identificador de la conexión, el identificador de la cuenta de almacenamiento, y la ruta de acceso al blob donde se van a almacenar los resultados de la solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="5063a-137">We pass the cmdlet the resource group, the name of the Network Watcher, the Id of the connection, the Id of the storage account, and the path to the blob to store the troubleshoot results in.</span></span>

```azurecli
azure network watcher troubleshoot -g resourceGroupName -n networkWatcherName -t connectionId -i storageId -p storagePath
```

<span data-ttu-id="5063a-138">Después de ejecutar el cmdlet, Network Watcher revisa los recursos para comprobar el estado.</span><span class="sxs-lookup"><span data-stu-id="5063a-138">Once you run the cmdlet, Network Watcher reviews the resource to verify the health.</span></span> <span data-ttu-id="5063a-139">Devuelve los resultados al shell y almacena los registros de los resultados en la cuenta de almacenamiento especificada.</span><span class="sxs-lookup"><span data-stu-id="5063a-139">It returns the results to the shell and stores logs of the results in the storage account specified.</span></span>

## <a name="understanding-the-results"></a><span data-ttu-id="5063a-140">Descripción de los resultados</span><span class="sxs-lookup"><span data-stu-id="5063a-140">Understanding the results</span></span>

<span data-ttu-id="5063a-141">El texto de la acción ofrece instrucciones generales sobre cómo resolver el problema.</span><span class="sxs-lookup"><span data-stu-id="5063a-141">The action text provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="5063a-142">Si se puede realizar una acción para el problema, se proporciona un vínculo con instrucciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="5063a-142">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="5063a-143">Si no hay instrucciones adicionales, la respuesta proporciona la dirección URL para abrir un caso de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="5063a-143">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="5063a-144">Para más información acerca de las propiedades de la respuesta y lo que incluye, consulte la [introducción a la solución de problemas en Network Watcher](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="5063a-144">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="5063a-145">Para más instrucciones acerca de cómo descargar archivos desde cuentas de Azure Storage, consulte [Introducción a Azure Blob Storage mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="5063a-145">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="5063a-146">Otra herramienta que se puede utilizar es el Explorador de Storage.</span><span class="sxs-lookup"><span data-stu-id="5063a-146">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="5063a-147">Encontrará más información acerca del Explorador de Storage en el siguiente vínculo: [Explorador de Storage](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="5063a-147">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="5063a-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5063a-148">Next steps</span></span>

<span data-ttu-id="5063a-149">Si se cambió la configuración y la conectividad de VPN se ha detenido, consulte [Administración de grupos de seguridad de red](../virtual-network/virtual-network-manage-nsg-arm-portal.md) para realizar un seguimiento de los grupos de seguridad de red y las reglas de seguridad que pueden estar afectados.</span><span class="sxs-lookup"><span data-stu-id="5063a-149">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>
