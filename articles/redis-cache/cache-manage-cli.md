---
title: "Caché en Redis de Azure mediante Azure CLI aaaManage | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooinstall Hola CLI de Azure en cualquier plataforma, cómo toouse se tooconnect tooyour cuenta de Azure y cómo toocreate y administrar una caché en Redis de hello CLI de Azure."
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
ms.openlocfilehash: e8ee30090133e6b4edea93dcd13fd171e75989bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-azure-redis-cache-using-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="c16b1-103">¿Cómo toocreate y administrar caché en Redis de Azure con hello Azure interfaz de línea de comandos (CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="c16b1-103">How toocreate and manage Azure Redis Cache using hello Azure Command-Line Interface (Azure CLI)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c16b1-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c16b1-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="c16b1-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="c16b1-105">Azure CLI</span></span>](cache-manage-cli.md)
>
>

<span data-ttu-id="c16b1-106">Hola CLI de Azure es una excelente manera toomanage su infraestructura de Azure desde cualquier plataforma.</span><span class="sxs-lookup"><span data-stu-id="c16b1-106">hello Azure CLI is a great way toomanage your Azure infrastructure from any platform.</span></span> <span data-ttu-id="c16b1-107">Este artículo muestra cómo toocreate y administrar las instancias de caché en Redis de Azure con hello CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="c16b1-107">This article shows you how toocreate and manage your Azure Redis Cache instances using hello Azure CLI.</span></span>

> [!NOTE]
> <span data-ttu-id="c16b1-108">En este artículo se aplica la versión anterior de tooa de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="c16b1-108">This article applies tooa previous version of Azure CLI.</span></span> <span data-ttu-id="c16b1-109">Para los scripts de ejemplo de CLI de Azure 2.0 más recientes hello, consulte [ejemplos de caché Redis de Azure CLI](cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c16b1-109">For hello latest Azure CLI 2.0 sample scripts, see [Azure CLI Redis cache samples](cli-samples.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="c16b1-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c16b1-110">Prerequisites</span></span>
<span data-ttu-id="c16b1-111">toocreate y administrar instancias de caché en Redis de Azure mediante Azure CLI, debe completar pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c16b1-111">toocreate and manage Azure Redis Cache instances using Azure CLI, you must complete hello following steps.</span></span>

* <span data-ttu-id="c16b1-112">Debe tener una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="c16b1-112">You must have an Azure account.</span></span> <span data-ttu-id="c16b1-113">En caso de no tener ninguna, puede crear una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/) en tan solo unos momentos.</span><span class="sxs-lookup"><span data-stu-id="c16b1-113">If you don't have one, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a few moments.</span></span>
* <span data-ttu-id="c16b1-114">[Instalar hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c16b1-114">[Install hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="c16b1-115">Conectarse a la instalación de CLI de Azure con una cuenta personal de Azure, o con un trabajo o escuela cuenta de Azure e inicie sesión de hello CLI de Azure con hello `azure login` comando.</span><span class="sxs-lookup"><span data-stu-id="c16b1-115">Connect your Azure CLI installation with a personal Azure account, or with a work or school Azure account, and log in from hello Azure CLI using hello `azure login` command.</span></span> <span data-ttu-id="c16b1-116">toounderstand Hola diferencias y elegir, consulte [conectarse tooan suscripción de Azure desde hello Azure interfaz de línea de comandos (CLI de Azure)](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="c16b1-116">toounderstand hello differences and choose, see [Connect tooan Azure subscription from hello Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="c16b1-117">Antes de ejecutar cualquiera de hello después de comandos, cambie hello Azure CLI en modo de administrador de recursos mediante la ejecución de hello `azure config mode arm` comando.</span><span class="sxs-lookup"><span data-stu-id="c16b1-117">Before running any of hello following commands, switch hello Azure CLI into Resource Manager mode by running hello `azure config mode arm` command.</span></span> <span data-ttu-id="c16b1-118">Para obtener más información, consulte [usar hello Azure CLI toomanage Azure y grupos de recursos](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="c16b1-118">For more information, see [Use hello Azure CLI toomanage Azure resources and resource groups](../xplat-cli-azure-resource-manager.md).</span></span>

## <a name="redis-cache-properties"></a><span data-ttu-id="c16b1-119">Propiedades de caché en Redis</span><span class="sxs-lookup"><span data-stu-id="c16b1-119">Redis Cache properties</span></span>
<span data-ttu-id="c16b1-120">Hello siguientes propiedades se utilizan al crear y actualizar instancias de caché en Redis.</span><span class="sxs-lookup"><span data-stu-id="c16b1-120">hello following properties are used when creating and updating Redis Cache instances.</span></span>

| <span data-ttu-id="c16b1-121">Propiedad</span><span class="sxs-lookup"><span data-stu-id="c16b1-121">Property</span></span> | <span data-ttu-id="c16b1-122">Switch</span><span class="sxs-lookup"><span data-stu-id="c16b1-122">Switch</span></span> | <span data-ttu-id="c16b1-123">Description</span><span class="sxs-lookup"><span data-stu-id="c16b1-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c16b1-124">name</span><span class="sxs-lookup"><span data-stu-id="c16b1-124">name</span></span> |<span data-ttu-id="c16b1-125">-n,--name</span><span class="sxs-lookup"><span data-stu-id="c16b1-125">-n, --name</span></span> |<span data-ttu-id="c16b1-126">Nombre del programa Hola a caché en Redis.</span><span class="sxs-lookup"><span data-stu-id="c16b1-126">Name of hello Redis Cache.</span></span> |
| <span data-ttu-id="c16b1-127">resource group</span><span class="sxs-lookup"><span data-stu-id="c16b1-127">resource group</span></span> |<span data-ttu-id="c16b1-128">-g, --resource-group</span><span class="sxs-lookup"><span data-stu-id="c16b1-128">-g, --resource-group</span></span> |<span data-ttu-id="c16b1-129">Nombre del grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c16b1-129">Name of hello Resource Group.</span></span> |
| <span data-ttu-id="c16b1-130">location</span><span class="sxs-lookup"><span data-stu-id="c16b1-130">location</span></span> |<span data-ttu-id="c16b1-131">-l, --location</span><span class="sxs-lookup"><span data-stu-id="c16b1-131">-l, --location</span></span> |<span data-ttu-id="c16b1-132">Memoria caché de ubicación toocreate.</span><span class="sxs-lookup"><span data-stu-id="c16b1-132">Location toocreate cache.</span></span> |
| <span data-ttu-id="c16b1-133">size</span><span class="sxs-lookup"><span data-stu-id="c16b1-133">size</span></span> |<span data-ttu-id="c16b1-134">-z, --size</span><span class="sxs-lookup"><span data-stu-id="c16b1-134">-z, --size</span></span> |<span data-ttu-id="c16b1-135">Tamaño de caché en Redis Hola.</span><span class="sxs-lookup"><span data-stu-id="c16b1-135">Size of hello Redis Cache.</span></span> <span data-ttu-id="c16b1-136">Valores válidos: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span><span class="sxs-lookup"><span data-stu-id="c16b1-136">Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span></span> |
| <span data-ttu-id="c16b1-137">sku</span><span class="sxs-lookup"><span data-stu-id="c16b1-137">sku</span></span> |<span data-ttu-id="c16b1-138">-x, --sku</span><span class="sxs-lookup"><span data-stu-id="c16b1-138">-x, --sku</span></span> |<span data-ttu-id="c16b1-139">SKU de Redis.</span><span class="sxs-lookup"><span data-stu-id="c16b1-139">Redis SKU.</span></span> <span data-ttu-id="c16b1-140">Debe ser uno de estos valores: [Basic, Standard, Premium]</span><span class="sxs-lookup"><span data-stu-id="c16b1-140">Should be one of : [Basic, Standard, Premium]</span></span> |
| <span data-ttu-id="c16b1-141">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="c16b1-141">EnableNonSslPort</span></span> |<span data-ttu-id="c16b1-142">-e, --enable-non-ssl-port</span><span class="sxs-lookup"><span data-stu-id="c16b1-142">-e, --enable-non-ssl-port</span></span> |<span data-ttu-id="c16b1-143">Propiedad EnableNonSslPort de hello caché en Redis.</span><span class="sxs-lookup"><span data-stu-id="c16b1-143">EnableNonSslPort property of hello Redis Cache.</span></span> <span data-ttu-id="c16b1-144">Agregar esta marca si desea tooenable hello no SSL puerto de la memoria caché</span><span class="sxs-lookup"><span data-stu-id="c16b1-144">Add this flag if you want tooenable hello Non SSL Port for your cache</span></span> |
| <span data-ttu-id="c16b1-145">Configuración de Redis</span><span class="sxs-lookup"><span data-stu-id="c16b1-145">Redis Configuration</span></span> |<span data-ttu-id="c16b1-146">-c, --redis-configuration</span><span class="sxs-lookup"><span data-stu-id="c16b1-146">-c, --redis-configuration</span></span> |<span data-ttu-id="c16b1-147">Configuración de Redis.</span><span class="sxs-lookup"><span data-stu-id="c16b1-147">Redis Configuration.</span></span> <span data-ttu-id="c16b1-148">Escriba una cadena con formato JSON de valores y claves de configuración aquí.</span><span class="sxs-lookup"><span data-stu-id="c16b1-148">Enter a JSON formatted string of configuration keys and values here.</span></span> <span data-ttu-id="c16b1-149">Formato:"{"":"","":""}"</span><span class="sxs-lookup"><span data-stu-id="c16b1-149">Format:"{"":"","":""}"</span></span> |
| <span data-ttu-id="c16b1-150">Configuración de Redis</span><span class="sxs-lookup"><span data-stu-id="c16b1-150">Redis Configuration</span></span> |<span data-ttu-id="c16b1-151">-f, --redis-configuration-file</span><span class="sxs-lookup"><span data-stu-id="c16b1-151">-f, --redis-configuration-file</span></span> |<span data-ttu-id="c16b1-152">Configuración de Redis.</span><span class="sxs-lookup"><span data-stu-id="c16b1-152">Redis Configuration.</span></span> <span data-ttu-id="c16b1-153">Escriba la ruta de acceso de Hola de un archivo que contiene las claves de configuración y los valores aquí.</span><span class="sxs-lookup"><span data-stu-id="c16b1-153">Enter hello path of a file containing configuration keys and values here.</span></span> <span data-ttu-id="c16b1-154">Formato de entrada del archivo de hello: {"": "","": ""}</span><span class="sxs-lookup"><span data-stu-id="c16b1-154">Format for hello file entry: {"":"","":""}</span></span> |
| <span data-ttu-id="c16b1-155">Número de particiones</span><span class="sxs-lookup"><span data-stu-id="c16b1-155">Shard Count</span></span> |<span data-ttu-id="c16b1-156">-r, --shard-count</span><span class="sxs-lookup"><span data-stu-id="c16b1-156">-r, --shard-count</span></span> |<span data-ttu-id="c16b1-157">Número de particiones toocreate en una caché de clúster Premium con agrupación en clústeres.</span><span class="sxs-lookup"><span data-stu-id="c16b1-157">Number of Shards toocreate on a Premium Cluster Cache with clustering.</span></span> |
| <span data-ttu-id="c16b1-158">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="c16b1-158">Virtual Network</span></span> |<span data-ttu-id="c16b1-159">-v, --virtual-network</span><span class="sxs-lookup"><span data-stu-id="c16b1-159">-v, --virtual-network</span></span> |<span data-ttu-id="c16b1-160">Cuando se hospeda la memoria caché en una red virtual, especifica Hola exacta ARM Id. de recurso de Hola Hola de toodeploy de red virtual redis caché en.</span><span class="sxs-lookup"><span data-stu-id="c16b1-160">When hosting your cache in a VNET, specifies hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in.</span></span> <span data-ttu-id="c16b1-161">Formato de ejemplo: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="c16b1-161">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="c16b1-162">key type</span><span class="sxs-lookup"><span data-stu-id="c16b1-162">key type</span></span> |<span data-ttu-id="c16b1-163">-t, --key-type</span><span class="sxs-lookup"><span data-stu-id="c16b1-163">-t, --key-type</span></span> |<span data-ttu-id="c16b1-164">Tipo de clave toorenew.</span><span class="sxs-lookup"><span data-stu-id="c16b1-164">Type of key toorenew.</span></span> <span data-ttu-id="c16b1-165">Valores válidos: [Primary, Secondary]</span><span class="sxs-lookup"><span data-stu-id="c16b1-165">Valid values: [Primary, Secondary]</span></span> |
| <span data-ttu-id="c16b1-166">StaticIP</span><span class="sxs-lookup"><span data-stu-id="c16b1-166">StaticIP</span></span> |<span data-ttu-id="c16b1-167">-p, --static-ip <static-ip></span><span class="sxs-lookup"><span data-stu-id="c16b1-167">-p, --static-ip <static-ip></span></span> |<span data-ttu-id="c16b1-168">Al hospedar la memoria caché en una red virtual, especifica una dirección IP única en la subred de Hola para caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="c16b1-168">When hosting your cache in a VNET, specifies a unique IP address in hello subnet for hello cache.</span></span> <span data-ttu-id="c16b1-169">Si no se proporciona, se elige una automáticamente de la subred de Hola.</span><span class="sxs-lookup"><span data-stu-id="c16b1-169">If not provided, one is chosen for you from hello subnet.</span></span> |
| <span data-ttu-id="c16b1-170">Subred</span><span class="sxs-lookup"><span data-stu-id="c16b1-170">Subnet</span></span> |<span data-ttu-id="c16b1-171">t, --subnet <subnet></span><span class="sxs-lookup"><span data-stu-id="c16b1-171">t, --subnet <subnet></span></span> |<span data-ttu-id="c16b1-172">Al hospedar la memoria caché en una red virtual, especifica el nombre de Hola de subred de hello en la caché de hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="c16b1-172">When hosting your cache in a VNET, specifies hello name of hello subnet in which toodeploy hello cache.</span></span> |
| <span data-ttu-id="c16b1-173">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="c16b1-173">VirtualNetwork</span></span> |<span data-ttu-id="c16b1-174">-v, --virtual-network <virtual-network></span><span class="sxs-lookup"><span data-stu-id="c16b1-174">-v, --virtual-network <virtual-network></span></span> |<span data-ttu-id="c16b1-175">Cuando se hospeda la memoria caché en una red virtual, especifica Hola exacta ARM Id. de recurso de Hola Hola de toodeploy de red virtual redis caché en.</span><span class="sxs-lookup"><span data-stu-id="c16b1-175">When hosting your cache in a VNET, specifies hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in.</span></span> <span data-ttu-id="c16b1-176">Formato de ejemplo: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="c16b1-176">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="c16b1-177">Subscription</span><span class="sxs-lookup"><span data-stu-id="c16b1-177">Subscription</span></span> |<span data-ttu-id="c16b1-178">-s, --subscription</span><span class="sxs-lookup"><span data-stu-id="c16b1-178">-s, --subscription</span></span> |<span data-ttu-id="c16b1-179">identificador de la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="c16b1-179">hello subscription identifier.</span></span> |

## <a name="see-all-redis-cache-commands"></a><span data-ttu-id="c16b1-180">Consulta de todos los comandos de caché en Redis</span><span class="sxs-lookup"><span data-stu-id="c16b1-180">See all Redis Cache commands</span></span>
<span data-ttu-id="c16b1-181">toosee todos los comandos de caché en Redis y sus parámetros, usar hello `azure rediscache -h` comando.</span><span class="sxs-lookup"><span data-stu-id="c16b1-181">toosee all Redis Cache commands and their parameters, use hello `azure rediscache -h` command.</span></span>

    C:\>azure rediscache -h
    help:    Commands toomanage your Azure Redis Cache(s)
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
    help:    Renew hello authentication key for an existing Redis Cache
    help:      rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:      rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help  output usage information
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="create-a-redis-cache"></a><span data-ttu-id="c16b1-182">Creación de una caché en Redis</span><span class="sxs-lookup"><span data-stu-id="c16b1-182">Create a Redis Cache</span></span>
<span data-ttu-id="c16b1-183">toocreate una caché en Redis, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c16b1-183">toocreate a Redis Cache, use hello following command:</span></span>

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

<span data-ttu-id="c16b1-184">Para obtener más información sobre este comando, ejecute hello `azure rediscache create -h` comando.</span><span class="sxs-lookup"><span data-stu-id="c16b1-184">For more information about this command, run hello `azure rediscache create -h` command.</span></span>

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
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -l, --location <location>                                Location toocreate cache.
    help:      -z, --size <size>                                        Size of hello Redis Cache. Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]
    help:      -x, --sku <sku>                                          Redis SKU. Should be one of : [Basic, Standard, Premium]
    help:      -e, --enable-non-ssl-port                                EnableNonSslPort property of hello Redis Cache. Add this flag if you want tooenable hello Non SSL Port for your cache
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here. Format:"{"<key1>":"<value1>","<key2>":"<value2>"}"
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here. Format for hello file entry: {"<key1>":"<value1>","<key2>":"<value2>"}
    help:      -r, --shard-count <shard-count>                          Number of Shards toocreate on a Premium Cluster Cache
    help:      -v, --virtual-network <virtual-network>                  hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1
    help:      -t, --subnet <subnet>                                    Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -p, --static-ip <static-ip>                              Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -s, --subscription <id>                                  hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="delete-an-existing-redis-cache"></a><span data-ttu-id="c16b1-185">Eliminación de una caché en Redis existente</span><span class="sxs-lookup"><span data-stu-id="c16b1-185">Delete an existing Redis Cache</span></span>
<span data-ttu-id="c16b1-186">toodelete una caché en Redis, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c16b1-186">toodelete a Redis Cache, use hello following command:</span></span>

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

<span data-ttu-id="c16b1-187">Para obtener más información sobre este comando, ejecute hello `azure rediscache delete -h` comando.</span><span class="sxs-lookup"><span data-stu-id="c16b1-187">For more information about this command, run hello `azure rediscache delete -h` command.</span></span>

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
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which hello cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a><span data-ttu-id="c16b1-188">Lista de todas las memorias Redis Cache dentro de su suscripción o del grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="c16b1-188">List all Redis Caches within your Subscription or Resource Group</span></span>
<span data-ttu-id="c16b1-189">toolist todas las cachés de Redis dentro de la suscripción o el grupo de recursos, utilice Hola comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="c16b1-189">toolist all Redis Caches within your Subscription or Resource Group, use hello following command:</span></span>

    azure rediscache list [options]

<span data-ttu-id="c16b1-190">Para obtener más información sobre este comando, ejecute hello `azure rediscache list -h` comando.</span><span class="sxs-lookup"><span data-stu-id="c16b1-190">For more information about this command, run hello `azure rediscache list -h` command.</span></span>

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
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="show-properties-of-an-existing-redis-cache"></a><span data-ttu-id="c16b1-191">Presentación de las propiedades de una caché en Redis existente</span><span class="sxs-lookup"><span data-stu-id="c16b1-191">Show properties of an existing Redis Cache</span></span>
<span data-ttu-id="c16b1-192">propiedades de tooshow de una caché de Redis existente, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c16b1-192">tooshow properties of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache show [--name <name> --resource-group <resource-group>]

<span data-ttu-id="c16b1-193">Para obtener más información sobre este comando, ejecute hello `azure rediscache show -h` comando.</span><span class="sxs-lookup"><span data-stu-id="c16b1-193">For more information about this command, run hello `azure rediscache show -h` command.</span></span>

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
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

<a name="scale"></a>

## <a name="change-settings-of-an-existing-redis-cache"></a><span data-ttu-id="c16b1-194">Cambio de la configuración de una caché en Redis existente</span><span class="sxs-lookup"><span data-stu-id="c16b1-194">Change settings of an existing Redis Cache</span></span>
<span data-ttu-id="c16b1-195">configuración de toochange de una caché de Redis existente, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c16b1-195">toochange settings of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

<span data-ttu-id="c16b1-196">Para obtener más información sobre este comando, ejecute hello `azure rediscache set -h` comando.</span><span class="sxs-lookup"><span data-stu-id="c16b1-196">For more information about this command, run hello `azure rediscache set -h` command.</span></span>

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
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here.
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here.
    help:      -s, --subscription <subscription>                        hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="renew-hello-authentication-key-for-an-existing-redis-cache"></a><span data-ttu-id="c16b1-197">Renovar la clave de autenticación de Hola para una caché en Redis existente</span><span class="sxs-lookup"><span data-stu-id="c16b1-197">Renew hello authentication key for an existing Redis Cache</span></span>
<span data-ttu-id="c16b1-198">clave de autenticación de hello toorenew para una caché existente de Redis, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c16b1-198">toorenew hello authentication key for an existing Redis Cache, use hello following command:</span></span>

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

<span data-ttu-id="c16b1-199">Especifique `Primary` o `Secondary` para `key-type`.</span><span class="sxs-lookup"><span data-stu-id="c16b1-199">Specify `Primary` or `Secondary` for `key-type`.</span></span>

<span data-ttu-id="c16b1-200">Para obtener más información sobre este comando, ejecute hello `azure rediscache renew-key -h` comando.</span><span class="sxs-lookup"><span data-stu-id="c16b1-200">For more information about this command, run hello `azure rediscache renew-key -h` command.</span></span>

    C:\>azure rediscache renew-key -h
    help:    Renew hello authentication key for an existing Redis Cache
    help:
    help:    Usage: rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which cache exists
    help:      -t, --key-type <key-type>              type of key toorenew. Valid values are: 'Primary', 'Secondary'.
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a><span data-ttu-id="c16b1-201">Lista de las claves principal y secundaria de una caché en Redis existente</span><span class="sxs-lookup"><span data-stu-id="c16b1-201">List Primary and Secondary keys of an existing Redis Cache</span></span>
<span data-ttu-id="c16b1-202">claves principales y secundarios de toolist de una caché de Redis existente, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c16b1-202">toolist Primary and Secondary keys of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

<span data-ttu-id="c16b1-203">Para obtener más información sobre este comando, ejecute hello `azure rediscache list-keys -h` comando.</span><span class="sxs-lookup"><span data-stu-id="c16b1-203">For more information about this command, run hello `azure rediscache list-keys -h` command.</span></span>

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
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which Cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)
