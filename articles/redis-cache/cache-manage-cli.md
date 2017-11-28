---
title: "Administración de Azure Redis Cache mediante la CLI de Azure | Microsoft Docs"
description: "En este tema se describe cómo instalar la CLI de Azure en cualquier plataforma, cómo usarla para conectarse a la cuenta de Azure y cómo crear y administra una caché en Redis desde la CLI de Azure."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 964ff245-859d-4bc1-bccf-62e4b3c1169f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: ba078a870a3998568170cc197bd6698b97b7fadb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-manage-azure-redis-cache-using-the-azure-command-line-interface-azure-cli"></a><span data-ttu-id="14f3b-103">Creación y administración de Caché en Redis de Azure mediante la interfaz de línea de comandos de Azure (CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="14f3b-103">How to create and manage Azure Redis Cache using the Azure Command-Line Interface (Azure CLI)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="14f3b-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="14f3b-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="14f3b-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="14f3b-105">Azure CLI</span></span>](cache-manage-cli.md)
>
>

<span data-ttu-id="14f3b-106">La CLI de Azure es una excelente manera de administrar la infraestructura de Azure desde cualquier plataforma.</span><span class="sxs-lookup"><span data-stu-id="14f3b-106">The Azure CLI is a great way to manage your Azure infrastructure from any platform.</span></span> <span data-ttu-id="14f3b-107">En este artículo se muestra cómo crear y administrar las instancias de Caché en Redis de Azure usando la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="14f3b-107">This article shows you how to create and manage your Azure Redis Cache instances using the Azure CLI.</span></span>

> [!NOTE]
> <span data-ttu-id="14f3b-108">Este artículo se aplica a una versión anterior de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="14f3b-108">This article applies to a previous version of Azure CLI.</span></span> <span data-ttu-id="14f3b-109">Para conocer los scripts de ejemplo más recientes de la CLI 2.0 de Azure, consulte [Ejemplos de caché de Redis para la CLI de Azure](cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="14f3b-109">For the latest Azure CLI 2.0 sample scripts, see [Azure CLI Redis cache samples](cli-samples.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="14f3b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="14f3b-110">Prerequisites</span></span>
<span data-ttu-id="14f3b-111">Para crear y administrar instancias de Caché en Redis de Azure mediante la CLI de Azure, debe realizar los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="14f3b-111">To create and manage Azure Redis Cache instances using Azure CLI, you must complete the following steps.</span></span>

* <span data-ttu-id="14f3b-112">Debe tener una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="14f3b-112">You must have an Azure account.</span></span> <span data-ttu-id="14f3b-113">En caso de no tener ninguna, puede crear una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/) en tan solo unos momentos.</span><span class="sxs-lookup"><span data-stu-id="14f3b-113">If you don't have one, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a few moments.</span></span>
* <span data-ttu-id="14f3b-114">[Instalación de la CLI de Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="14f3b-114">[Install the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="14f3b-115">Conecte su instalación de CLI de Azure con una cuenta personal de Azure o con una cuenta de Azure profesional o educativa, e inicie sesión desde la CLI de Azure mediante el comando `azure login` .</span><span class="sxs-lookup"><span data-stu-id="14f3b-115">Connect your Azure CLI installation with a personal Azure account, or with a work or school Azure account, and log in from the Azure CLI using the `azure login` command.</span></span> <span data-ttu-id="14f3b-116">Para comprender las diferencias y elegir, consulte [Conexión a una suscripción de Azure desde la interfaz de la línea de comandos de Azure (CLI de Azure)](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="14f3b-116">To understand the differences and choose, see [Connect to an Azure subscription from the Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="14f3b-117">Antes de ejecutar cualquiera de los comandos siguientes, cambie la CLI de Azure al modo de Administrador de recursos mediante la ejecución del comando `azure config mode arm` .</span><span class="sxs-lookup"><span data-stu-id="14f3b-117">Before running any of the following commands, switch the Azure CLI into Resource Manager mode by running the `azure config mode arm` command.</span></span> <span data-ttu-id="14f3b-118">Para más información, vea [Use the Azure CLI to manage Azure resources and resource groups (Uso de la CLI de Azure para administrar los recursos y grupos de recursos de Azure)](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="14f3b-118">For more information, see [Use the Azure CLI to manage Azure resources and resource groups](../xplat-cli-azure-resource-manager.md).</span></span>

## <a name="redis-cache-properties"></a><span data-ttu-id="14f3b-119">Propiedades de caché en Redis</span><span class="sxs-lookup"><span data-stu-id="14f3b-119">Redis Cache properties</span></span>
<span data-ttu-id="14f3b-120">Las siguientes propiedades se utilizan al crear y actualizar instancias de caché en Redis.</span><span class="sxs-lookup"><span data-stu-id="14f3b-120">The following properties are used when creating and updating Redis Cache instances.</span></span>

| <span data-ttu-id="14f3b-121">Propiedad</span><span class="sxs-lookup"><span data-stu-id="14f3b-121">Property</span></span> | <span data-ttu-id="14f3b-122">Switch</span><span class="sxs-lookup"><span data-stu-id="14f3b-122">Switch</span></span> | <span data-ttu-id="14f3b-123">Description</span><span class="sxs-lookup"><span data-stu-id="14f3b-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="14f3b-124">name</span><span class="sxs-lookup"><span data-stu-id="14f3b-124">name</span></span> |<span data-ttu-id="14f3b-125">-n,--name</span><span class="sxs-lookup"><span data-stu-id="14f3b-125">-n, --name</span></span> |<span data-ttu-id="14f3b-126">Nombre de la caché en Redis.</span><span class="sxs-lookup"><span data-stu-id="14f3b-126">Name of the Redis Cache.</span></span> |
| <span data-ttu-id="14f3b-127">resource group</span><span class="sxs-lookup"><span data-stu-id="14f3b-127">resource group</span></span> |<span data-ttu-id="14f3b-128">-g, --resource-group</span><span class="sxs-lookup"><span data-stu-id="14f3b-128">-g, --resource-group</span></span> |<span data-ttu-id="14f3b-129">Nombre del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="14f3b-129">Name of the Resource Group.</span></span> |
| <span data-ttu-id="14f3b-130">location</span><span class="sxs-lookup"><span data-stu-id="14f3b-130">location</span></span> |<span data-ttu-id="14f3b-131">-l, --location</span><span class="sxs-lookup"><span data-stu-id="14f3b-131">-l, --location</span></span> |<span data-ttu-id="14f3b-132">Ubicación donde crear la caché.</span><span class="sxs-lookup"><span data-stu-id="14f3b-132">Location to create cache.</span></span> |
| <span data-ttu-id="14f3b-133">size</span><span class="sxs-lookup"><span data-stu-id="14f3b-133">size</span></span> |<span data-ttu-id="14f3b-134">-z, --size</span><span class="sxs-lookup"><span data-stu-id="14f3b-134">-z, --size</span></span> |<span data-ttu-id="14f3b-135">Tamaño de la caché en Redis.</span><span class="sxs-lookup"><span data-stu-id="14f3b-135">Size of the Redis Cache.</span></span> <span data-ttu-id="14f3b-136">Valores válidos: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span><span class="sxs-lookup"><span data-stu-id="14f3b-136">Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span></span> |
| <span data-ttu-id="14f3b-137">sku</span><span class="sxs-lookup"><span data-stu-id="14f3b-137">sku</span></span> |<span data-ttu-id="14f3b-138">-x, --sku</span><span class="sxs-lookup"><span data-stu-id="14f3b-138">-x, --sku</span></span> |<span data-ttu-id="14f3b-139">SKU de Redis.</span><span class="sxs-lookup"><span data-stu-id="14f3b-139">Redis SKU.</span></span> <span data-ttu-id="14f3b-140">Debe ser uno de estos valores: [Basic, Standard, Premium]</span><span class="sxs-lookup"><span data-stu-id="14f3b-140">Should be one of : [Basic, Standard, Premium]</span></span> |
| <span data-ttu-id="14f3b-141">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="14f3b-141">EnableNonSslPort</span></span> |<span data-ttu-id="14f3b-142">-e, --enable-non-ssl-port</span><span class="sxs-lookup"><span data-stu-id="14f3b-142">-e, --enable-non-ssl-port</span></span> |<span data-ttu-id="14f3b-143">Propiedad EnableNonSslPort de la caché en Redis.</span><span class="sxs-lookup"><span data-stu-id="14f3b-143">EnableNonSslPort property of the Redis Cache.</span></span> <span data-ttu-id="14f3b-144">Agregue esta marca si desea habilitar el puerto que no es SSL de la caché</span><span class="sxs-lookup"><span data-stu-id="14f3b-144">Add this flag if you want to enable the Non SSL Port for your cache</span></span> |
| <span data-ttu-id="14f3b-145">Configuración de Redis</span><span class="sxs-lookup"><span data-stu-id="14f3b-145">Redis Configuration</span></span> |<span data-ttu-id="14f3b-146">-c, --redis-configuration</span><span class="sxs-lookup"><span data-stu-id="14f3b-146">-c, --redis-configuration</span></span> |<span data-ttu-id="14f3b-147">Configuración de Redis.</span><span class="sxs-lookup"><span data-stu-id="14f3b-147">Redis Configuration.</span></span> <span data-ttu-id="14f3b-148">Escriba una cadena con formato JSON de valores y claves de configuración aquí.</span><span class="sxs-lookup"><span data-stu-id="14f3b-148">Enter a JSON formatted string of configuration keys and values here.</span></span> <span data-ttu-id="14f3b-149">Formato:"{"":"","":""}"</span><span class="sxs-lookup"><span data-stu-id="14f3b-149">Format:"{"":"","":""}"</span></span> |
| <span data-ttu-id="14f3b-150">Configuración de Redis</span><span class="sxs-lookup"><span data-stu-id="14f3b-150">Redis Configuration</span></span> |<span data-ttu-id="14f3b-151">-f, --redis-configuration-file</span><span class="sxs-lookup"><span data-stu-id="14f3b-151">-f, --redis-configuration-file</span></span> |<span data-ttu-id="14f3b-152">Configuración de Redis.</span><span class="sxs-lookup"><span data-stu-id="14f3b-152">Redis Configuration.</span></span> <span data-ttu-id="14f3b-153">Escriba la ruta de acceso de un archivo que contiene valores y claves de configuración aquí.</span><span class="sxs-lookup"><span data-stu-id="14f3b-153">Enter the path of a file containing configuration keys and values here.</span></span> <span data-ttu-id="14f3b-154">Formato de la entrada del archivo: {"":"","":""}</span><span class="sxs-lookup"><span data-stu-id="14f3b-154">Format for the file entry: {"":"","":""}</span></span> |
| <span data-ttu-id="14f3b-155">Número de particiones</span><span class="sxs-lookup"><span data-stu-id="14f3b-155">Shard Count</span></span> |<span data-ttu-id="14f3b-156">-r, --shard-count</span><span class="sxs-lookup"><span data-stu-id="14f3b-156">-r, --shard-count</span></span> |<span data-ttu-id="14f3b-157">Número de particiones que se creará en una caché de clúster premium con la agrupación de clústeres.</span><span class="sxs-lookup"><span data-stu-id="14f3b-157">Number of Shards to create on a Premium Cluster Cache with clustering.</span></span> |
| <span data-ttu-id="14f3b-158">Red virtual</span><span class="sxs-lookup"><span data-stu-id="14f3b-158">Virtual Network</span></span> |<span data-ttu-id="14f3b-159">-v, --virtual-network</span><span class="sxs-lookup"><span data-stu-id="14f3b-159">-v, --virtual-network</span></span> |<span data-ttu-id="14f3b-160">Si hospeda la memoria caché en una red virtual, especifica el id. de recurso de ARM exacto de la red virtual en la que se va a implementar la Caché en Redis.</span><span class="sxs-lookup"><span data-stu-id="14f3b-160">When hosting your cache in a VNET, specifies the exact ARM resource ID of the virtual network to deploy the redis cache in.</span></span> <span data-ttu-id="14f3b-161">Formato de ejemplo: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="14f3b-161">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="14f3b-162">key type</span><span class="sxs-lookup"><span data-stu-id="14f3b-162">key type</span></span> |<span data-ttu-id="14f3b-163">-t, --key-type</span><span class="sxs-lookup"><span data-stu-id="14f3b-163">-t, --key-type</span></span> |<span data-ttu-id="14f3b-164">Tipo de la clave que renovar.</span><span class="sxs-lookup"><span data-stu-id="14f3b-164">Type of key to renew.</span></span> <span data-ttu-id="14f3b-165">Valores válidos: [Primary, Secondary]</span><span class="sxs-lookup"><span data-stu-id="14f3b-165">Valid values: [Primary, Secondary]</span></span> |
| <span data-ttu-id="14f3b-166">StaticIP</span><span class="sxs-lookup"><span data-stu-id="14f3b-166">StaticIP</span></span> |<span data-ttu-id="14f3b-167">-p, --static-ip <static-ip></span><span class="sxs-lookup"><span data-stu-id="14f3b-167">-p, --static-ip <static-ip></span></span> |<span data-ttu-id="14f3b-168">Si hospeda la memoria caché en una red virtual, especifica una dirección IP única en la subred de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="14f3b-168">When hosting your cache in a VNET, specifies a unique IP address in the subnet for the cache.</span></span> <span data-ttu-id="14f3b-169">Si no se ofrece, elija una para usted en la subred.</span><span class="sxs-lookup"><span data-stu-id="14f3b-169">If not provided, one is chosen for you from the subnet.</span></span> |
| <span data-ttu-id="14f3b-170">Subred</span><span class="sxs-lookup"><span data-stu-id="14f3b-170">Subnet</span></span> |<span data-ttu-id="14f3b-171">t, --subnet <subnet></span><span class="sxs-lookup"><span data-stu-id="14f3b-171">t, --subnet <subnet></span></span> |<span data-ttu-id="14f3b-172">Si hospeda la memoria caché en una red virtual, especifica el nombre de la subred en la que se va a implementar la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="14f3b-172">When hosting your cache in a VNET, specifies the name of the subnet in which to deploy the cache.</span></span> |
| <span data-ttu-id="14f3b-173">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="14f3b-173">VirtualNetwork</span></span> |<span data-ttu-id="14f3b-174">-v, --virtual-network <virtual-network></span><span class="sxs-lookup"><span data-stu-id="14f3b-174">-v, --virtual-network <virtual-network></span></span> |<span data-ttu-id="14f3b-175">Si hospeda la memoria caché en una red virtual, especifica el id. de recurso de ARM exacto de la red virtual en la que se va a implementar la Caché en Redis.</span><span class="sxs-lookup"><span data-stu-id="14f3b-175">When hosting your cache in a VNET, specifies the exact ARM resource ID of the virtual network to deploy the redis cache in.</span></span> <span data-ttu-id="14f3b-176">Formato de ejemplo: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="14f3b-176">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="14f3b-177">Subscription</span><span class="sxs-lookup"><span data-stu-id="14f3b-177">Subscription</span></span> |<span data-ttu-id="14f3b-178">-s, --subscription</span><span class="sxs-lookup"><span data-stu-id="14f3b-178">-s, --subscription</span></span> |<span data-ttu-id="14f3b-179">Identificador de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="14f3b-179">The subscription identifier.</span></span> |

## <a name="see-all-redis-cache-commands"></a><span data-ttu-id="14f3b-180">Consulta de todos los comandos de caché en Redis</span><span class="sxs-lookup"><span data-stu-id="14f3b-180">See all Redis Cache commands</span></span>
<span data-ttu-id="14f3b-181">Para ver todos los comandos de Caché en Redis y sus parámetros, use el comando `azure rediscache -h` .</span><span class="sxs-lookup"><span data-stu-id="14f3b-181">To see all Redis Cache commands and their parameters, use the `azure rediscache -h` command.</span></span>

    C:\>azure rediscache -h
    help:    Commands to manage your Azure Redis Cache(s)
    help:
    help:    Create a Redis Cache
    help:      rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Delete an existing Redis Cache
    help:      rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    List all Redis Caches within your Subscription or Resource Group
    help:      rediscache list [options]
    help:
    help:    Show properties of an existing Redis Cache
    help:      rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Change settings of an existing Redis Cache
    help:      rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Renew the authentication key for an existing Redis Cache
    help:      rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:      rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help  output usage information
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="create-a-redis-cache"></a><span data-ttu-id="14f3b-182">Creación de una caché en Redis</span><span class="sxs-lookup"><span data-stu-id="14f3b-182">Create a Redis Cache</span></span>
<span data-ttu-id="14f3b-183">Para crear una caché en Redis, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="14f3b-183">To create a Redis Cache, use the following command:</span></span>

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

<span data-ttu-id="14f3b-184">Para más información sobre este comando, ejecute el comando `azure rediscache create -h` .</span><span class="sxs-lookup"><span data-stu-id="14f3b-184">For more information about this command, run the `azure rediscache create -h` command.</span></span>

    C:\>azure rediscache create -h
    help:    Create a Redis Cache
    help:
    help:    Usage: rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of the Resource Group
    help:      -l, --location <location>                                Location to create cache.
    help:      -z, --size <size>                                        Size of the Redis Cache. Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]
    help:      -x, --sku <sku>                                          Redis SKU. Should be one of : [Basic, Standard, Premium]
    help:      -e, --enable-non-ssl-port                                EnableNonSslPort property of the Redis Cache. Add this flag if you want to enable the Non SSL Port for your cache
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here. Format:"{"<key1>":"<value1>","<key2>":"<value2>"}"
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter the path of a file containing configuration keys and values here. Format for the file entry: {"<key1>":"<value1>","<key2>":"<value2>"}
    help:      -r, --shard-count <shard-count>                          Number of Shards to create on a Premium Cluster Cache
    help:      -v, --virtual-network <virtual-network>                  The exact ARM resource ID of the virtual network to deploy the redis cache in. Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1
    help:      -t, --subnet <subnet>                                    Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -p, --static-ip <static-ip>                              Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -s, --subscription <id>                                  the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="delete-an-existing-redis-cache"></a><span data-ttu-id="14f3b-185">Eliminación de una caché en Redis existente</span><span class="sxs-lookup"><span data-stu-id="14f3b-185">Delete an existing Redis Cache</span></span>
<span data-ttu-id="14f3b-186">Para eliminar una caché en Redis, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="14f3b-186">To delete a Redis Cache, use the following command:</span></span>

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

<span data-ttu-id="14f3b-187">Para más información sobre este comando, ejecute el comando `azure rediscache delete -h` .</span><span class="sxs-lookup"><span data-stu-id="14f3b-187">For more information about this command, run the `azure rediscache delete -h` command.</span></span>

    C:\>azure rediscache delete -h
    help:    Delete an existing Redis Cache
    help:
    help:    Usage: rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group under which the cache exists
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a><span data-ttu-id="14f3b-188">Lista de todas las memorias Redis Cache dentro de su suscripción o del grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="14f3b-188">List all Redis Caches within your Subscription or Resource Group</span></span>
<span data-ttu-id="14f3b-189">Para enumerar todas las memorias Redis Cache incluidas en su suscripción o en el grupo de recursos, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="14f3b-189">To list all Redis Caches within your Subscription or Resource Group, use the following command:</span></span>

    azure rediscache list [options]

<span data-ttu-id="14f3b-190">Para más información sobre este comando, ejecute el comando `azure rediscache list -h` .</span><span class="sxs-lookup"><span data-stu-id="14f3b-190">For more information about this command, run the `azure rediscache list -h` command.</span></span>

    C:\>azure rediscache list -h
    help:    List all Redis Caches within your Subscription or Resource Group
    help:
    help:    Usage: rediscache list [options]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -g, --resource-group <resource-group>  Name of the Resource Group
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="show-properties-of-an-existing-redis-cache"></a><span data-ttu-id="14f3b-191">Presentación de las propiedades de una caché en Redis existente</span><span class="sxs-lookup"><span data-stu-id="14f3b-191">Show properties of an existing Redis Cache</span></span>
<span data-ttu-id="14f3b-192">Para mostrar las propiedades de una caché en Redis existente, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="14f3b-192">To show properties of an existing Redis Cache, use the following command:</span></span>

    azure rediscache show [--name <name> --resource-group <resource-group>]

<span data-ttu-id="14f3b-193">Para más información sobre este comando, ejecute el comando `azure rediscache show -h` .</span><span class="sxs-lookup"><span data-stu-id="14f3b-193">For more information about this command, run the `azure rediscache show -h` command.</span></span>

    C:\>azure rediscache show -h
    help:    Show properties of an existing Redis Cache
    help:
    help:    Usage: rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

<a name="scale"></a>

## <a name="change-settings-of-an-existing-redis-cache"></a><span data-ttu-id="14f3b-194">Cambio de la configuración de una caché en Redis existente</span><span class="sxs-lookup"><span data-stu-id="14f3b-194">Change settings of an existing Redis Cache</span></span>
<span data-ttu-id="14f3b-195">Para cambiar la configuración de una caché en Redis existente, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="14f3b-195">To change settings of an existing Redis Cache, use the following command:</span></span>

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

<span data-ttu-id="14f3b-196">Para más información sobre este comando, ejecute el comando `azure rediscache set -h` .</span><span class="sxs-lookup"><span data-stu-id="14f3b-196">For more information about this command, run the `azure rediscache set -h` command.</span></span>

    C:\>azure rediscache set -h
    help:    Change settings of an existing Redis Cache
    help:
    help:    Usage: rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of the Resource Group
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here.
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter the path of a file containing configuration keys and values here.
    help:      -s, --subscription <subscription>                        the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="renew-the-authentication-key-for-an-existing-redis-cache"></a><span data-ttu-id="14f3b-197">Renovación de la clave de autenticación para una caché en Redis existente</span><span class="sxs-lookup"><span data-stu-id="14f3b-197">Renew the authentication key for an existing Redis Cache</span></span>
<span data-ttu-id="14f3b-198">Para renovar la clave de autenticación para una caché en Redis existente, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="14f3b-198">To renew the authentication key for an existing Redis Cache, use the following command:</span></span>

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

<span data-ttu-id="14f3b-199">Especifique `Primary` o `Secondary` para `key-type`.</span><span class="sxs-lookup"><span data-stu-id="14f3b-199">Specify `Primary` or `Secondary` for `key-type`.</span></span>

<span data-ttu-id="14f3b-200">Para más información sobre este comando, ejecute el comando `azure rediscache renew-key -h`.</span><span class="sxs-lookup"><span data-stu-id="14f3b-200">For more information about this command, run the `azure rediscache renew-key -h` command.</span></span>

    C:\>azure rediscache renew-key -h
    help:    Renew the authentication key for an existing Redis Cache
    help:
    help:    Usage: rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group under which cache exists
    help:      -t, --key-type <key-type>              type of key to renew. Valid values are: 'Primary', 'Secondary'.
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a><span data-ttu-id="14f3b-201">Lista de las claves principal y secundaria de una caché en Redis existente</span><span class="sxs-lookup"><span data-stu-id="14f3b-201">List Primary and Secondary keys of an existing Redis Cache</span></span>
<span data-ttu-id="14f3b-202">Para enumerar las claves Principal y Secundaria de una caché en Redis existente, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="14f3b-202">To list Primary and Secondary keys of an existing Redis Cache, use the following command:</span></span>

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

<span data-ttu-id="14f3b-203">Para más información sobre este comando, ejecute el comando `azure rediscache list-keys -h` .</span><span class="sxs-lookup"><span data-stu-id="14f3b-203">For more information about this command, run the `azure rediscache list-keys -h` command.</span></span>

    C:\>azure rediscache list-keys -h
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:
    help:    Usage: rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of the Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of the Resource Group under which Cache exists
    help:      -s, --subscription <subscription>      the subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)
