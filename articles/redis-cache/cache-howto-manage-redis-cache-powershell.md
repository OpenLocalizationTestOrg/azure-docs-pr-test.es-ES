---
title: "Administración de Azure Redis Cache con Azure PowerShell | Microsoft Docs"
description: "Aprenda a realizar tareas administrativas para Caché en Redis de Azure usando Azure PowerShell."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1136efe5-1e33-4d91-bb49-c8e2a6dca475
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: sdanie
ms.openlocfilehash: 0a5c95eab3fd01f611fc049e80c5c506857e0b81
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="manage-azure-redis-cache-with-azure-powershell"></a><span data-ttu-id="b023f-103">Administración de Caché en Redis de Azure con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b023f-103">Manage Azure Redis Cache with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b023f-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b023f-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="b023f-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="b023f-105">Azure CLI</span></span>](cache-manage-cli.md)
> 
> 

<span data-ttu-id="b023f-106">Este tema muestra cómo realizar tareas comunes, como crear, actualizar y escalar las instancias de caché en Redis de Azure, cómo volver a generar las claves de acceso y cómo ver información acerca de las memorias caché.</span><span class="sxs-lookup"><span data-stu-id="b023f-106">This topic shows you how to perform common tasks such as create, update, and scale your Azure Redis Cache instances, how to regenerate access keys, and how to view information about your caches.</span></span> <span data-ttu-id="b023f-107">Para obtener una lista completa de cmdlets de PowerShell de caché en Redis de Azure, consulte [Azure Redis Cache cmdlets](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span><span class="sxs-lookup"><span data-stu-id="b023f-107">For a complete list of Azure Redis Cache PowerShell cmdlets, see [Azure Redis Cache cmdlets](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="b023f-108">Para más información acerca del modelo de implementación clásico, consulte [Azure Resource Manager vs. classic deployment: Understand deployment models and the state of your resources](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics) (Implementación clásica frente a implementación con Azure Resource Manager: los modelos de implementación y el estado de los recursos).</span><span class="sxs-lookup"><span data-stu-id="b023f-108">For more information about the classic deployment model, see [Azure Resource Manager vs. classic deployment: Understand deployment models and the state of your resources](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b023f-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b023f-109">Prerequisites</span></span>
<span data-ttu-id="b023f-110">Si ya ha instalado Azure PowerShell, debe tener la versión 1.0.0 (o posterior) de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b023f-110">If you have already installed Azure PowerShell, you must have Azure PowerShell version 1.0.0 or later.</span></span> <span data-ttu-id="b023f-111">Puede comprobar la versión de Azure PowerShell que ha instalado con este comando en el símbolo del sistema de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b023f-111">You can check the version of Azure PowerShell that you have installed with this command at the Azure PowerShell command prompt.</span></span>

    Get-Module azure | format-table version


<span data-ttu-id="b023f-112">En primer lugar, debe iniciar sesión en Azure con este comando.</span><span class="sxs-lookup"><span data-stu-id="b023f-112">First, you must log in to Azure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="b023f-113">Especifique la dirección de correo electrónico de la cuenta de Azure y su contraseña en el cuadro de diálogo de inicio de sesión de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b023f-113">Specify the email address of your Azure account and its password in the Microsoft Azure sign-in dialog.</span></span>

<span data-ttu-id="b023f-114">A continuación, si tiene varias suscripciones de Azure, deberá establecer la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="b023f-114">Next, if you have multiple Azure subscriptions, you need to set your Azure subscription.</span></span> <span data-ttu-id="b023f-115">Para ver una lista de las suscripciones actuales, ejecute este comando.</span><span class="sxs-lookup"><span data-stu-id="b023f-115">To see a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="b023f-116">Para especificar la suscripción, ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="b023f-116">To specify the subscription, run the following command.</span></span> <span data-ttu-id="b023f-117">En el ejemplo siguiente, el nombre de la suscripción es `ContosoSubscription`.</span><span class="sxs-lookup"><span data-stu-id="b023f-117">In the following example, the subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

<span data-ttu-id="b023f-118">Para poder usar Windows PowerShell con el Administrador de recursos de Azure, necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b023f-118">Before you can use Windows PowerShell with Azure Resource Manager, you need the following:</span></span>

* <span data-ttu-id="b023f-119">Windows PowerShell, versión 3.0 o 4.0.</span><span class="sxs-lookup"><span data-stu-id="b023f-119">Windows PowerShell, Version 3.0 or 4.0.</span></span> <span data-ttu-id="b023f-120">Para buscar la versión de Windows PowerShell, escriba:`$PSVersionTable` y compruebe que el valor de `PSVersion` es 3.0 o 4.0.</span><span class="sxs-lookup"><span data-stu-id="b023f-120">To find the version of Windows PowerShell, type:`$PSVersionTable` and verify the value of `PSVersion` is 3.0 or 4.0.</span></span> <span data-ttu-id="b023f-121">Para instalar una versión compatible, consulte [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) o [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span><span class="sxs-lookup"><span data-stu-id="b023f-121">To install a compatible version, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

<span data-ttu-id="b023f-122">Para obtener ayuda detallada con cualquier cmdlet que aparezca en este tutorial, use el cmdlet Get-Help.</span><span class="sxs-lookup"><span data-stu-id="b023f-122">To get detailed help for any cmdlet you see in this tutorial, use the Get-Help cmdlet.</span></span>

    Get-Help <cmdlet-name> -Detailed

<span data-ttu-id="b023f-123">Por ejemplo, para obtener ayuda para el cmdlet `New-AzureRmRedisCache` , escriba:</span><span class="sxs-lookup"><span data-stu-id="b023f-123">For example, to get help for the `New-AzureRmRedisCache` cmdlet, type:</span></span>

    Get-Help New-AzureRmRedisCache -Detailed

### <a name="how-to-connect-to-other-clouds"></a><span data-ttu-id="b023f-124">Conexión a otras nubes</span><span class="sxs-lookup"><span data-stu-id="b023f-124">How to connect to other clouds</span></span>
<span data-ttu-id="b023f-125">De forma predeterminada, el entorno de Azure es `AzureCloud`, que representa la instancia de nube de Azure global.</span><span class="sxs-lookup"><span data-stu-id="b023f-125">By default the Azure environment is `AzureCloud`, which represents the global Azure cloud instance.</span></span> <span data-ttu-id="b023f-126">Para conectarse a una instancia diferente, utilice el comando `Add-AzureRmAccount` con el conmutador de línea de comandos `-Environment` o -`EnvironmentName` con el nombre de entorno o el entorno deseado.</span><span class="sxs-lookup"><span data-stu-id="b023f-126">To connect to a different instance, use the `Add-AzureRmAccount` command with the `-Environment` or -`EnvironmentName` command line switch with the desired environment or environment name.</span></span>

<span data-ttu-id="b023f-127">Para ver la lista de entornos disponibles, ejecute el cmdlet `Get-AzureRmEnvironment` .</span><span class="sxs-lookup"><span data-stu-id="b023f-127">To see the list of available environments, run the `Get-AzureRmEnvironment` cmdlet.</span></span>

### <a name="to-connect-to-the-azure-government-cloud"></a><span data-ttu-id="b023f-128">Conexión a la nube de Azure Government</span><span class="sxs-lookup"><span data-stu-id="b023f-128">To connect to the Azure Government Cloud</span></span>
<span data-ttu-id="b023f-129">Para conectarse a la nube de Azure Government, utilice uno de los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="b023f-129">To connect to the Azure Government Cloud, use one of the following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureUSGovernment

<span data-ttu-id="b023f-130">o</span><span class="sxs-lookup"><span data-stu-id="b023f-130">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureUSGovernment)

<span data-ttu-id="b023f-131">Para crear una memoria caché en la nube de Azure Government, utilice una de las siguientes ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="b023f-131">To create a cache in the Azure Government Cloud, use one of the following locations.</span></span>

* <span data-ttu-id="b023f-132">USGov Virginia</span><span class="sxs-lookup"><span data-stu-id="b023f-132">USGov Virginia</span></span>
* <span data-ttu-id="b023f-133">USGov Iowa</span><span class="sxs-lookup"><span data-stu-id="b023f-133">USGov Iowa</span></span>

<span data-ttu-id="b023f-134">Para más información acerca de la nube de Azure Government, consulte [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) y la [Guía para desarrolladores de Microsoft Azure Government](../azure-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="b023f-134">For more information about the Azure Government Cloud, see [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) and [Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>

### <a name="to-connect-to-the-azure-china-cloud"></a><span data-ttu-id="b023f-135">Para conectarse a la nube de China de Azure</span><span class="sxs-lookup"><span data-stu-id="b023f-135">To connect to the Azure China Cloud</span></span>
<span data-ttu-id="b023f-136">Para conectarse a la nube de China de Azure, use uno de los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="b023f-136">To connect to the Azure China Cloud, use one of the following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureChinaCloud

<span data-ttu-id="b023f-137">o</span><span class="sxs-lookup"><span data-stu-id="b023f-137">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureChinaCloud)

<span data-ttu-id="b023f-138">Para crear una caché en la nube de China de Azure, use una de las siguientes ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="b023f-138">To create a cache in the Azure China Cloud, use one of the following locations.</span></span>

* <span data-ttu-id="b023f-139">Este de China</span><span class="sxs-lookup"><span data-stu-id="b023f-139">China East</span></span>
* <span data-ttu-id="b023f-140">Norte de China</span><span class="sxs-lookup"><span data-stu-id="b023f-140">China North</span></span>

<span data-ttu-id="b023f-141">Para obtener más información acerca de la nube de China de Azure, consulte [AzureChinaCloud for Azure operated by 21Vianet in China (Nube de China de Azure operada por 21Vianet en China)](http://www.windowsazure.cn/).</span><span class="sxs-lookup"><span data-stu-id="b023f-141">For more information about the Azure China Cloud, see [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span>

### <a name="to-connect-to-microsoft-azure-germany"></a><span data-ttu-id="b023f-142">Conexión a Microsoft Azure Alemania</span><span class="sxs-lookup"><span data-stu-id="b023f-142">To connect to Microsoft Azure Germany</span></span>
<span data-ttu-id="b023f-143">Para conectarse a Microsoft Azure Alemania, utilice uno de los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="b023f-143">To connect to Microsoft Azure Germany, use one of the following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureGermanCloud


<span data-ttu-id="b023f-144">o</span><span class="sxs-lookup"><span data-stu-id="b023f-144">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureGermanCloud)

<span data-ttu-id="b023f-145">Para crear una memoria caché en Microsoft Azure Alemania, use una de las siguientes ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="b023f-145">To create a cache in Microsoft Azure Germany, use one of the following locations.</span></span>

* <span data-ttu-id="b023f-146">Centro de Alemania</span><span class="sxs-lookup"><span data-stu-id="b023f-146">Germany Central</span></span>
* <span data-ttu-id="b023f-147">Noreste de Alemania</span><span class="sxs-lookup"><span data-stu-id="b023f-147">Germany Northeast</span></span>

<span data-ttu-id="b023f-148">Para obtener más información acerca de Microsoft Azure Alemania, consulte [Microsoft Azure Germany](https://azure.microsoft.com/overview/clouds/germany/).</span><span class="sxs-lookup"><span data-stu-id="b023f-148">For more information about Microsoft Azure Germany, see [Microsoft Azure Germany](https://azure.microsoft.com/overview/clouds/germany/).</span></span>

### <a name="properties-used-for-azure-redis-cache-powershell"></a><span data-ttu-id="b023f-149">Propiedades utilizadas para Caché en Redis de Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="b023f-149">Properties used for Azure Redis Cache PowerShell</span></span>
<span data-ttu-id="b023f-150">La tabla siguiente contiene las propiedades y las descripciones de los parámetros normalmente utilizados al crear y administrar las instancias de Caché en Redis de Azure mediante Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b023f-150">The following table contains properties and descriptions for commonly used parameters when creating and managing your Azure Redis Cache instances using Azure PowerShell.</span></span>

| <span data-ttu-id="b023f-151">Parámetro</span><span class="sxs-lookup"><span data-stu-id="b023f-151">Parameter</span></span> | <span data-ttu-id="b023f-152">Description</span><span class="sxs-lookup"><span data-stu-id="b023f-152">Description</span></span> | <span data-ttu-id="b023f-153">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="b023f-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b023f-154">Nombre</span><span class="sxs-lookup"><span data-stu-id="b023f-154">Name</span></span> |<span data-ttu-id="b023f-155">Nombre de la memoria caché</span><span class="sxs-lookup"><span data-stu-id="b023f-155">Name of the cache</span></span> | |
| <span data-ttu-id="b023f-156">Ubicación</span><span class="sxs-lookup"><span data-stu-id="b023f-156">Location</span></span> |<span data-ttu-id="b023f-157">Ubicación de la memoria caché</span><span class="sxs-lookup"><span data-stu-id="b023f-157">Location of the cache</span></span> | |
| <span data-ttu-id="b023f-158">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="b023f-158">ResourceGroupName</span></span> |<span data-ttu-id="b023f-159">Nombre del grupo de recursos en el que se va a crear la memoria caché</span><span class="sxs-lookup"><span data-stu-id="b023f-159">Resource group name in which to create the cache</span></span> | |
| <span data-ttu-id="b023f-160">Tamaño</span><span class="sxs-lookup"><span data-stu-id="b023f-160">Size</span></span> |<span data-ttu-id="b023f-161">El tamaño de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="b023f-161">The size of the cache.</span></span> <span data-ttu-id="b023f-162">Los valores válidos son: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250 MB, 1 GB, 2,5 GB, 6 GB, 13 GB, 26 GB, 53 GB</span><span class="sxs-lookup"><span data-stu-id="b023f-162">Valid values are: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB</span></span> |<span data-ttu-id="b023f-163">1 GB</span><span class="sxs-lookup"><span data-stu-id="b023f-163">1GB</span></span> |
| <span data-ttu-id="b023f-164">ShardCount</span><span class="sxs-lookup"><span data-stu-id="b023f-164">ShardCount</span></span> |<span data-ttu-id="b023f-165">El número de particiones para crear durante la creación de una memoria caché premium con clúster habilitado.</span><span class="sxs-lookup"><span data-stu-id="b023f-165">The number of shards to create when creating a premium cache with clustering enabled.</span></span> <span data-ttu-id="b023f-166">Los valores válidos son: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span><span class="sxs-lookup"><span data-stu-id="b023f-166">Valid values are: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span></span> | |
| <span data-ttu-id="b023f-167">SKU</span><span class="sxs-lookup"><span data-stu-id="b023f-167">SKU</span></span> |<span data-ttu-id="b023f-168">Especifica la SKU de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="b023f-168">Specifies the SKU of the cache.</span></span> <span data-ttu-id="b023f-169">Los valores válidos son: Básico, Estándar y Premium</span><span class="sxs-lookup"><span data-stu-id="b023f-169">Valid values are: Basic, Standard, Premium</span></span> |<span data-ttu-id="b023f-170">Estándar</span><span class="sxs-lookup"><span data-stu-id="b023f-170">Standard</span></span> |
| <span data-ttu-id="b023f-171">RedisConfiguration</span><span class="sxs-lookup"><span data-stu-id="b023f-171">RedisConfiguration</span></span> |<span data-ttu-id="b023f-172">Especifica la configuración de Redis.</span><span class="sxs-lookup"><span data-stu-id="b023f-172">Specifies Redis configuration settings.</span></span> <span data-ttu-id="b023f-173">Para ver detalles sobre cada opción de configuración, consulte la siguiente tabla [Propiedades de RedisConfiguration](#redisconfiguration-properties) .</span><span class="sxs-lookup"><span data-stu-id="b023f-173">For details on each setting, see the following [RedisConfiguration properties](#redisconfiguration-properties) table.</span></span> | |
| <span data-ttu-id="b023f-174">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="b023f-174">EnableNonSslPort</span></span> |<span data-ttu-id="b023f-175">Indica si el puerto no SSL está habilitado.</span><span class="sxs-lookup"><span data-stu-id="b023f-175">Indicates whether the non-SSL port is enabled.</span></span> |<span data-ttu-id="b023f-176">False</span><span class="sxs-lookup"><span data-stu-id="b023f-176">False</span></span> |
| <span data-ttu-id="b023f-177">MaxMemoryPolicy</span><span class="sxs-lookup"><span data-stu-id="b023f-177">MaxMemoryPolicy</span></span> |<span data-ttu-id="b023f-178">Este parámetro está en desuso; utilice RedisConfiguration en su lugar.</span><span class="sxs-lookup"><span data-stu-id="b023f-178">This parameter has been deprecated - use RedisConfiguration instead.</span></span> | |
| <span data-ttu-id="b023f-179">StaticIP</span><span class="sxs-lookup"><span data-stu-id="b023f-179">StaticIP</span></span> |<span data-ttu-id="b023f-180">Si hospeda la memoria caché en una red virtual, especifica una dirección IP única en la subred de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="b023f-180">When hosting your cache in a VNET, specifies a unique IP address in the subnet for the cache.</span></span> <span data-ttu-id="b023f-181">Si no se ofrece, elija una para usted en la subred.</span><span class="sxs-lookup"><span data-stu-id="b023f-181">If not provided, one is chosen for you from the subnet.</span></span> | |
| <span data-ttu-id="b023f-182">Subred</span><span class="sxs-lookup"><span data-stu-id="b023f-182">Subnet</span></span> |<span data-ttu-id="b023f-183">Si hospeda la memoria caché en una red virtual, especifica el nombre de la subred en la que se va a implementar la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="b023f-183">When hosting your cache in a VNET, specifies the name of the subnet in which to deploy the cache.</span></span> | |
| <span data-ttu-id="b023f-184">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="b023f-184">VirtualNetwork</span></span> |<span data-ttu-id="b023f-185">Si hospeda la memoria caché en una red virtual, especifica el identificador de recurso de la red virtual en la que se va a implementar la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="b023f-185">When hosting your cache in a VNET, specifies the resource ID of the VNET in which to deploy the cache.</span></span> | |
| <span data-ttu-id="b023f-186">KeyType</span><span class="sxs-lookup"><span data-stu-id="b023f-186">KeyType</span></span> |<span data-ttu-id="b023f-187">Especifica la clave de acceso que hay que volver a generar cuando se renueven las claves de acceso.</span><span class="sxs-lookup"><span data-stu-id="b023f-187">Specifies which access key to regenerate when renewing access keys.</span></span> <span data-ttu-id="b023f-188">Los valores válidos son: primario, secundario</span><span class="sxs-lookup"><span data-stu-id="b023f-188">Valid values are: Primary, Secondary</span></span> | |

### <a name="redisconfiguration-properties"></a><span data-ttu-id="b023f-189">Propiedades de RedisConfiguration</span><span class="sxs-lookup"><span data-stu-id="b023f-189">RedisConfiguration properties</span></span>
| <span data-ttu-id="b023f-190">Propiedad</span><span class="sxs-lookup"><span data-stu-id="b023f-190">Property</span></span> | <span data-ttu-id="b023f-191">Description</span><span class="sxs-lookup"><span data-stu-id="b023f-191">Description</span></span> | <span data-ttu-id="b023f-192">Planes de tarifa</span><span class="sxs-lookup"><span data-stu-id="b023f-192">Pricing tiers</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b023f-193">rdb-backup-enabled</span><span class="sxs-lookup"><span data-stu-id="b023f-193">rdb-backup-enabled</span></span> |<span data-ttu-id="b023f-194">Si [Persistencia de los datos en Redis](cache-how-to-premium-persistence.md) está habilitado</span><span class="sxs-lookup"><span data-stu-id="b023f-194">Whether [Redis data persistence](cache-how-to-premium-persistence.md) is enabled</span></span> |<span data-ttu-id="b023f-195">Solo Premium</span><span class="sxs-lookup"><span data-stu-id="b023f-195">Premium only</span></span> |
| <span data-ttu-id="b023f-196">rdb-storage-connection-string</span><span class="sxs-lookup"><span data-stu-id="b023f-196">rdb-storage-connection-string</span></span> |<span data-ttu-id="b023f-197">La cadena de conexión a la cuenta de almacenamiento para [Persistencia de los datos en Redis](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="b023f-197">The connection string to the storage account for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="b023f-198">Solo Premium</span><span class="sxs-lookup"><span data-stu-id="b023f-198">Premium only</span></span> |
| <span data-ttu-id="b023f-199">rdb-backup-frequency</span><span class="sxs-lookup"><span data-stu-id="b023f-199">rdb-backup-frequency</span></span> |<span data-ttu-id="b023f-200">La frecuencia de copia de seguridad de [Persistencia de los datos en Redis](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="b023f-200">The backup frequency for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="b023f-201">Solo Premium</span><span class="sxs-lookup"><span data-stu-id="b023f-201">Premium only</span></span> |
| <span data-ttu-id="b023f-202">maxmemory-reserved</span><span class="sxs-lookup"><span data-stu-id="b023f-202">maxmemory-reserved</span></span> |<span data-ttu-id="b023f-203">Configura la [memoria reservada](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) para procesos que no están en caché</span><span class="sxs-lookup"><span data-stu-id="b023f-203">Configures the [memory reserved](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for non-cache processes</span></span> |<span data-ttu-id="b023f-204">Estándar y Premium</span><span class="sxs-lookup"><span data-stu-id="b023f-204">Standard and Premium</span></span> |
| <span data-ttu-id="b023f-205">maxmemory-policy</span><span class="sxs-lookup"><span data-stu-id="b023f-205">maxmemory-policy</span></span> |<span data-ttu-id="b023f-206">Configura la [directiva de expulsión](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) para la memoria caché</span><span class="sxs-lookup"><span data-stu-id="b023f-206">Configures the [eviction policy](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for the cache</span></span> |<span data-ttu-id="b023f-207">Todos los planes de tarifa</span><span class="sxs-lookup"><span data-stu-id="b023f-207">All pricing tiers</span></span> |
| <span data-ttu-id="b023f-208">notify-keyspace-events</span><span class="sxs-lookup"><span data-stu-id="b023f-208">notify-keyspace-events</span></span> |<span data-ttu-id="b023f-209">Configura las [notificaciones de Keyspace](cache-configure.md#keyspace-notifications-advanced-settings)</span><span class="sxs-lookup"><span data-stu-id="b023f-209">Configures [keyspace notifications](cache-configure.md#keyspace-notifications-advanced-settings)</span></span> |<span data-ttu-id="b023f-210">Estándar y Premium</span><span class="sxs-lookup"><span data-stu-id="b023f-210">Standard and Premium</span></span> |
| <span data-ttu-id="b023f-211">hash-max-ziplist-entries</span><span class="sxs-lookup"><span data-stu-id="b023f-211">hash-max-ziplist-entries</span></span> |<span data-ttu-id="b023f-212">Configura la [optimización de memoria](http://redis.io/topics/memory-optimization) para tipos de datos agregados pequeños</span><span class="sxs-lookup"><span data-stu-id="b023f-212">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="b023f-213">Estándar y Premium</span><span class="sxs-lookup"><span data-stu-id="b023f-213">Standard and Premium</span></span> |
| <span data-ttu-id="b023f-214">hash-max-ziplist-value</span><span class="sxs-lookup"><span data-stu-id="b023f-214">hash-max-ziplist-value</span></span> |<span data-ttu-id="b023f-215">Configura la [optimización de memoria](http://redis.io/topics/memory-optimization) para tipos de datos agregados pequeños</span><span class="sxs-lookup"><span data-stu-id="b023f-215">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="b023f-216">Estándar y Premium</span><span class="sxs-lookup"><span data-stu-id="b023f-216">Standard and Premium</span></span> |
| <span data-ttu-id="b023f-217">set-max-intset-entries</span><span class="sxs-lookup"><span data-stu-id="b023f-217">set-max-intset-entries</span></span> |<span data-ttu-id="b023f-218">Configura la [optimización de memoria](http://redis.io/topics/memory-optimization) para tipos de datos agregados pequeños</span><span class="sxs-lookup"><span data-stu-id="b023f-218">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="b023f-219">Estándar y Premium</span><span class="sxs-lookup"><span data-stu-id="b023f-219">Standard and Premium</span></span> |
| <span data-ttu-id="b023f-220">zset-max-ziplist-entries</span><span class="sxs-lookup"><span data-stu-id="b023f-220">zset-max-ziplist-entries</span></span> |<span data-ttu-id="b023f-221">Configura la [optimización de memoria](http://redis.io/topics/memory-optimization) para tipos de datos agregados pequeños</span><span class="sxs-lookup"><span data-stu-id="b023f-221">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="b023f-222">Estándar y Premium</span><span class="sxs-lookup"><span data-stu-id="b023f-222">Standard and Premium</span></span> |
| <span data-ttu-id="b023f-223">zset-max-ziplist-value</span><span class="sxs-lookup"><span data-stu-id="b023f-223">zset-max-ziplist-value</span></span> |<span data-ttu-id="b023f-224">Configura la [optimización de memoria](http://redis.io/topics/memory-optimization) para tipos de datos agregados pequeños</span><span class="sxs-lookup"><span data-stu-id="b023f-224">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="b023f-225">Estándar y Premium</span><span class="sxs-lookup"><span data-stu-id="b023f-225">Standard and Premium</span></span> |
| <span data-ttu-id="b023f-226">bases de datos</span><span class="sxs-lookup"><span data-stu-id="b023f-226">databases</span></span> |<span data-ttu-id="b023f-227">Configura el número de bases de datos.</span><span class="sxs-lookup"><span data-stu-id="b023f-227">Configures the number of databases.</span></span> <span data-ttu-id="b023f-228">Esta propiedad solo se puede configurar al crear la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="b023f-228">This property can be configured only at cache creation.</span></span> |<span data-ttu-id="b023f-229">Estándar y Premium</span><span class="sxs-lookup"><span data-stu-id="b023f-229">Standard and Premium</span></span> |

## <a name="to-create-a-redis-cache"></a><span data-ttu-id="b023f-230">Creación de una memoria caché en Redis</span><span class="sxs-lookup"><span data-stu-id="b023f-230">To create a Redis Cache</span></span>
<span data-ttu-id="b023f-231">Se crean nuevas instancias de caché en Redis de Azure mediante el cmdlet [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b023f-231">New Azure Redis Cache instances are created using the [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b023f-232">La primera vez que crea una caché en Redis en una suscripción mediante el portal de Azure, el portal registra el espacio de nombres `Microsoft.Cache` para esa suscripción.</span><span class="sxs-lookup"><span data-stu-id="b023f-232">The first time you create a Redis cache in a subscription using the Azure portal, the portal registers the `Microsoft.Cache` namespace for that subscription.</span></span> <span data-ttu-id="b023f-233">Si trata de crear la primera caché en Redis en una suscripción mediante PowerShell, primero debe registrar ese espacio de nombres mediante el comando siguiente; en caso contrario los cmdlets como `New-AzureRmRedisCache` y `Get-AzureRmRedisCache` producirán un error.</span><span class="sxs-lookup"><span data-stu-id="b023f-233">If you attempt to create the first Redis cache in a subscription using PowerShell, you must first register that namespace using the following command; otherwise cmdlets such as `New-AzureRmRedisCache` and `Get-AzureRmRedisCache` fail.</span></span>
> 
> `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Cache"`
> 
> 

<span data-ttu-id="b023f-234">Para ver una lista de parámetros disponibles y sus descripciones para `New-AzureRmRedisCache`, ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="b023f-234">To see a list of available parameters and their descriptions for `New-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help New-AzureRmRedisCache -detailed

    NAME
        New-AzureRmRedisCache

    SYNOPSIS
        Creates a new redis cache.


    SYNTAX
        New-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Location <String> [-RedisVersion <String>]
        [-Size <String>] [-Sku <String>] [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort
        <Boolean>] [-ShardCount <Integer>] [-VirtualNetwork <String>] [-Subnet <String>] [-StaticIP <String>]
        [<CommonParameters>]


    DESCRIPTION
        The New-AzureRmRedisCache cmdlet creates a new redis cache.


    PARAMETERS
        -Name <String>
            Name of the redis cache to create.

        -ResourceGroupName <String>
            Name of resource group in which to create the redis cache.

        -Location <String>
            Location in which to create the redis cache.

        -RedisVersion <String>
            RedisVersion is deprecated and will be removed in future release.

        -Size <String>
            Size of the redis cache. The default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. The default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            The 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting to set
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value, databases.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. If no value is provided, the default value is false and the
            non-SSL port will be disabled. Possible values are true and false.

        -ShardCount <Integer>
            The number of shards to create on a Premium Cluster Cache.

        -VirtualNetwork <String>
            The exact ARM resource ID of the virtual network to deploy the redis cache in. Example format: /subscriptions/{
            subid}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicNetwork/VirtualNetworks/{vnetName}

        -Subnet <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        -StaticIP <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="b023f-235">Para crear una memoria caché con parámetros predeterminados, ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="b023f-235">To create a cache with default parameters, run the following command.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US"

<span data-ttu-id="b023f-236">`ResourceGroupName`, `Name`, y `Location` son parámetros necesarios, pero el resto son opcionales y tienen valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="b023f-236">`ResourceGroupName`, `Name`, and `Location` are required parameters, but the rest are optional and have default values.</span></span> <span data-ttu-id="b023f-237">Ejecutar el comando anterior crea una instancia de caché en Redis de Azure de SKU estándar con el nombre, ubicación y grupo de recursos especificados, que es de 1 GB de tamaño con el puerto no SSL deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="b023f-237">Running the previous command creates a Standard SKU Azure Redis Cache instance with the specified name, location, and resource group, that is 1 GB in size with the non-SSL port disabled.</span></span>

<span data-ttu-id="b023f-238">Para crear una memoria caché premium, especifique un tamaño de P1 (6 GB - 60 GB), P2 (13 GB - 130 GB), P3 (26 GB - 260 GB) o P4 (53 GB - 530 GB).</span><span class="sxs-lookup"><span data-stu-id="b023f-238">To create a premium cache, specify a size of P1 (6 GB - 60 GB), P2 (13 GB - 130 GB), P3 (26 GB - 260 GB), or P4 (53 GB - 530 GB).</span></span> <span data-ttu-id="b023f-239">Para habilitar la agrupación en clústeres, especifique un número de particiones mediante el parámetro `ShardCount` .</span><span class="sxs-lookup"><span data-stu-id="b023f-239">To enable clustering, specify a shard count using the `ShardCount` parameter.</span></span> <span data-ttu-id="b023f-240">En el ejemplo siguiente se crea una memoria caché premium P1 con 3 particiones.</span><span class="sxs-lookup"><span data-stu-id="b023f-240">The following example creates a P1 premium cache with 3 shards.</span></span> <span data-ttu-id="b023f-241">Una memoria caché premium P1 tiene 6 GB de tamaño y, puesto que especificamos tres particiones el tamaño total es de 18 GB (3 x 6 GB).</span><span class="sxs-lookup"><span data-stu-id="b023f-241">A P1 premium cache is 6 GB in size, and since we specified three shards the total size is 18 GB (3 x 6 GB).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P1 -ShardCount 3

<span data-ttu-id="b023f-242">Para especificar valores para el parámetro `RedisConfiguration`, incluya los valores dentro de `{}` como pares de valor o de clave como en `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span><span class="sxs-lookup"><span data-stu-id="b023f-242">To specify values for the `RedisConfiguration` parameter, enclose the values inside `{}` as key/value pairs like `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span></span> <span data-ttu-id="b023f-243">En el ejemplo siguiente se crea una memoria caché estándar de 1 GB con `allkeys-random` maxmemory-policy y notificaciones de keyspace configuradas con `KEA`.</span><span class="sxs-lookup"><span data-stu-id="b023f-243">The following example creates a standard 1 GB cache with `allkeys-random` maxmemory policy and keyspace notifications configured with `KEA`.</span></span> <span data-ttu-id="b023f-244">Para más información, consulte [Notificaciones de Keyspace (configuración avanzada)](cache-configure.md#keyspace-notifications-advanced-settings) y [Directivas de memoria](cache-configure.md#memory-policies).</span><span class="sxs-lookup"><span data-stu-id="b023f-244">For more information, see [Keyspace notifications (advanced settings)](cache-configure.md#keyspace-notifications-advanced-settings) and [Memory policies](cache-configure.md#memory-policies).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}

<a name="databases"></a>

## <a name="to-configure-the-databases-setting-during-cache-creation"></a><span data-ttu-id="b023f-245">Configuración de las bases de datos al crear la memoria caché</span><span class="sxs-lookup"><span data-stu-id="b023f-245">To configure the databases setting during cache creation</span></span>
<span data-ttu-id="b023f-246">El parámetro `databases` se puede configurar al crear la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="b023f-246">The `databases` setting can be configured only during cache creation.</span></span> <span data-ttu-id="b023f-247">En el ejemplo siguiente se crea una memoria caché premium P3 (26 GB) con 48 bases de datos mediante el cmdlet [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b023f-247">The following example creates a premium P3 (26 GB) cache with 48 databases using the [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P3 -RedisConfiguration @{"databases" = "48"}

<span data-ttu-id="b023f-248">Para más información sobre la propiedad `databases` , consulte [Configuración predeterminada del servidor Redis](cache-configure.md#default-redis-server-configuration).</span><span class="sxs-lookup"><span data-stu-id="b023f-248">For more information on the `databases` property, see [Default Azure Redis Cache server configuration](cache-configure.md#default-redis-server-configuration).</span></span> <span data-ttu-id="b023f-249">Para más información sobre la creación de una memoria caché mediante el cmdlet [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx), consulte la sección anterior [Creación de una memoria caché en Redis](#to-create-a-redis-cache).</span><span class="sxs-lookup"><span data-stu-id="b023f-249">For more information on creating a cache using the [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet, see the previous [To create a Redis Cache](#to-create-a-redis-cache) section.</span></span>

## <a name="to-update-a-redis-cache"></a><span data-ttu-id="b023f-250">Actualización de una caché en Redis</span><span class="sxs-lookup"><span data-stu-id="b023f-250">To update a Redis cache</span></span>
<span data-ttu-id="b023f-251">Las instancias de caché en Redis de Azure se actualizan mediante el cmdlet [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b023f-251">Azure Redis Cache instances are updated using the [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet.</span></span>

<span data-ttu-id="b023f-252">Para ver una lista de parámetros disponibles y sus descripciones para `Set-AzureRmRedisCache`, ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="b023f-252">To see a list of available parameters and their descriptions for `Set-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Set-AzureRmRedisCache -detailed

    NAME
        Set-AzureRmRedisCache

    SYNOPSIS
        Set redis cache updatable parameters.

    SYNTAX
        Set-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Size <String>] [-Sku <String>]
        [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort <Boolean>] [-ShardCount
        <Integer>] [<CommonParameters>]

    DESCRIPTION
        The Set-AzureRmRedisCache cmdlet sets redis cache parameters.

    PARAMETERS
        -Name <String>
            Name of the redis cache to update.

        -ResourceGroupName <String>
            Name of the resource group for the cache.

        -Size <String>
            Size of the redis cache. The default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. The default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            The 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting to set
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. The default value is null and no change will be made to the
            currently configured value. Possible values are true and false.

        -ShardCount <Integer>
            The number of shards to create on a Premium Cluster Cache.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="b023f-253">El cmdlet `Set-AzureRmRedisCache` puede utilizarse para actualizar propiedades tales como `Size`, `Sku`, `EnableNonSslPort` y los valores de `RedisConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="b023f-253">The `Set-AzureRmRedisCache` cmdlet can be used to update properties such as `Size`, `Sku`, `EnableNonSslPort`, and the `RedisConfiguration` values.</span></span> 

<span data-ttu-id="b023f-254">El comando siguiente actualiza el parámetro maxmemory-policy para la caché en Redis denominada myCache.</span><span class="sxs-lookup"><span data-stu-id="b023f-254">The following command updates the maxmemory-policy for the Redis Cache named myCache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName "myGroup" -Name "myCache" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random"}

<a name="scale"></a>

## <a name="to-scale-a-redis-cache"></a><span data-ttu-id="b023f-255">Para escalar una caché en Redis</span><span class="sxs-lookup"><span data-stu-id="b023f-255">To scale a Redis cache</span></span>
<span data-ttu-id="b023f-256">Se puede usar `Set-AzureRmRedisCache` para escalar una instancia de caché en Redis de Azure si se modifican las propiedades `Size`, `Sku`, o `ShardCount`.</span><span class="sxs-lookup"><span data-stu-id="b023f-256">`Set-AzureRmRedisCache` can be used to scale an Azure Redis cache instance when the `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> 

> [!NOTE]
> <span data-ttu-id="b023f-257">El escalado de una caché con PowerShell está sujeto a los mismos límites y directrices que el escalado de una caché desde el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b023f-257">Scaling a cache using PowerShell is subject to the same limits and guidelines as scaling a cache from the Azure portal.</span></span> <span data-ttu-id="b023f-258">Puede escalar a un nivel de precios diferente con las siguientes restricciones.</span><span class="sxs-lookup"><span data-stu-id="b023f-258">You can scale to a different pricing tier with the following restrictions.</span></span>
> 
> * <span data-ttu-id="b023f-259">No se puede escalar desde un plan de tarifa superior a un plan de tarifa inferior.</span><span class="sxs-lookup"><span data-stu-id="b023f-259">You can't scale from a higher pricing tier to a lower pricing tier.</span></span>
> * <span data-ttu-id="b023f-260">No puede cambiar de una memoria caché **Premium** a una memoria caché **Estándar** o **Básica**.</span><span class="sxs-lookup"><span data-stu-id="b023f-260">You can't scale from a **Premium** cache down to a **Standard** or a **Basic** cache.</span></span>
> * <span data-ttu-id="b023f-261">No puede cambiar de una memoria caché **Estándar** a una memoria caché **Básica**.</span><span class="sxs-lookup"><span data-stu-id="b023f-261">You can't scale from a **Standard** cache down to a **Basic** cache.</span></span>
> * <span data-ttu-id="b023f-262">Puede cambiar de una memoria caché **Básica** a una memoria caché **Estándar**, pero no puede cambiar el tamaño al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="b023f-262">You can scale from a **Basic** cache to a **Standard** cache but you can't change the size at the same time.</span></span> <span data-ttu-id="b023f-263">Si necesita un tamaño distinto, puede realizar una operación de escalado posterior hasta el tamaño deseado.</span><span class="sxs-lookup"><span data-stu-id="b023f-263">If you need a different size, you can do a subsequent scaling operation to the desired size.</span></span>
> * <span data-ttu-id="b023f-264">No puede escalar de una memoria caché **Básica** directamente a una memoria caché **Premium**.</span><span class="sxs-lookup"><span data-stu-id="b023f-264">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="b023f-265">Debe escalar desde **Básica** a **Estándar** en una operación de escalado y, después, desde **Estándar** a **Premium** en una operación de escalado posterior.</span><span class="sxs-lookup"><span data-stu-id="b023f-265">You must scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
> * <span data-ttu-id="b023f-266">No puede escalar desde un tamaño mayor hasta el tamaño **C0 (250 MB)** .</span><span class="sxs-lookup"><span data-stu-id="b023f-266">You can't scale from a larger size down to the **C0 (250 MB)** size.</span></span>
> 
> <span data-ttu-id="b023f-267">Para más información, vea [Escalado de caché en Redis de Azure](cache-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="b023f-267">For more information, see [How to Scale Azure Redis Cache](cache-how-to-scale.md).</span></span>
> 
> 

<span data-ttu-id="b023f-268">En el ejemplo siguiente se muestra cómo escalar una memoria caché denominada `myCache` a una caché de 2,5 GB.</span><span class="sxs-lookup"><span data-stu-id="b023f-268">The following example shows how to scale a cache named `myCache` to a 2.5 GB cache.</span></span> <span data-ttu-id="b023f-269">Tenga en cuenta que este comando funciona con una memoria caché básica o una estándar.</span><span class="sxs-lookup"><span data-stu-id="b023f-269">Note that this command works for both a Basic or a Standard cache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="b023f-270">Después de emitir este comando, el estado de la memoria caché se devuelve (de forma similar a una llamada a `Get-AzureRmRedisCache`).</span><span class="sxs-lookup"><span data-stu-id="b023f-270">After this command is issued, the status of the cache is returned (similar to calling `Get-AzureRmRedisCache`).</span></span> <span data-ttu-id="b023f-271">Tenga en cuenta que `ProvisioningState` es `Scaling`.</span><span class="sxs-lookup"><span data-stu-id="b023f-271">Note that the `ProvisioningState` is `Scaling`.</span></span>

    PS C:\> Set-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup -Size 2.5GB


    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/mygroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Scaling
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 150], [notify-keyspace-events, KEA],
                         [maxmemory-delta, 150]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : mygroup
    PrimaryKey         : ....
    SecondaryKey       : ....
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

<span data-ttu-id="b023f-272">Cuando se complete la operación de escalado, `ProvisioningState` cambia a `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="b023f-272">When the scaling operation is complete, the `ProvisioningState` changes to `Succeeded`.</span></span> <span data-ttu-id="b023f-273">Si necesita realizar una operación de escalado posterior, como cambiar de básica a estándar y, a continuación, cambiar el tamaño, debe esperar hasta que se complete la operación anterior o recibirá un error similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="b023f-273">If you need to make a subsequent scaling operation, such as changing from Basic to Standard and then changing the size, you must wait until the previous operation is complete or you receive an error similar to the following.</span></span>

    Set-AzureRmRedisCache : Conflict: The resource '...' is not in a stable state, and is currently unable to accept the update request.

## <a name="to-get-information-about-a-redis-cache"></a><span data-ttu-id="b023f-274">Obtención de información acerca de una caché de Redis</span><span class="sxs-lookup"><span data-stu-id="b023f-274">To get information about a Redis cache</span></span>
<span data-ttu-id="b023f-275">Puede recuperar información sobre una caché con el cmdlet [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b023f-275">You can retrieve information about a cache using the [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet.</span></span>

<span data-ttu-id="b023f-276">Para ver una lista de parámetros disponibles y sus descripciones para `Get-AzureRmRedisCache`, ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="b023f-276">To see a list of available parameters and their descriptions for `Get-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCache -detailed

    NAME
        Get-AzureRmRedisCache

    SYNOPSIS
        Gets details about a single cache or all caches in the specified resource group or all caches in the current
        subscription.

    SYNTAX
        Get-AzureRmRedisCache [-Name <String>] [-ResourceGroupName <String>] [<CommonParameters>]

    DESCRIPTION
        The Get-AzureRmRedisCache cmdlet gets the details about a cache or caches depending on input parameters. If both
        ResourceGroupName and Name parameters are provided then Get-AzureRmRedisCache will return details about the
        specific cache name provided.

        If only ResourceGroupName is provided than it will return details about all caches in the specified resource group.

        If no parameters are given than it will return details about all caches the current subscription.

    PARAMETERS
        -Name <String>
            The name of the cache. When this parameter is provided along with ResourceGroupName, Get-AzureRmRedisCache
            returns the details for the cache.

        -ResourceGroupName <String>
            The name of the resource group that contains the cache or caches. If ResourceGroupName is provided with Name
            then Get-AzureRmRedisCache returns the details of the cache specified by Name. If only the ResourceGroup
            parameter is provided, then details for all caches in the resource group are returned.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="b023f-277">Para devolver información sobre todas las cachés de la suscripción actual, ejecute `Get-AzureRmRedisCache` sin ningún parámetro.</span><span class="sxs-lookup"><span data-stu-id="b023f-277">To return information about all caches in the current subscription, run `Get-AzureRmRedisCache` without any parameters.</span></span>

    Get-AzureRmRedisCache

<span data-ttu-id="b023f-278">Para devolver información sobre todas las cachés de un grupo de recursos específico, ejecute `Get-AzureRmRedisCache` con el parámetro `ResourceGroupName`.</span><span class="sxs-lookup"><span data-stu-id="b023f-278">To return information about all caches in a specific resource group, run `Get-AzureRmRedisCache` with the `ResourceGroupName` parameter.</span></span>

    Get-AzureRmRedisCache -ResourceGroupName myGroup

<span data-ttu-id="b023f-279">Para devolver información sobre una caché específica, ejecute `Get-AzureRmRedisCache` con el parámetro `Name` que contiene el nombre de la caché y el parámetro `ResourceGroupName` con el grupo de recursos que contiene esa caché.</span><span class="sxs-lookup"><span data-stu-id="b023f-279">To return information about a specific cache, run `Get-AzureRmRedisCache` with the `Name` parameter containing the name of the cache, and the `ResourceGroupName` parameter with the resource group containing that cache.</span></span>

    PS C:\> Get-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/myGroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Succeeded
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 62], [notify-keyspace-events, KEA],
                         [maxclients, 1000]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : myGroup
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

## <a name="to-retrieve-the-access-keys-for-a-redis-cache"></a><span data-ttu-id="b023f-280">Recuperación de las claves de acceso de una caché en Redis</span><span class="sxs-lookup"><span data-stu-id="b023f-280">To retrieve the access keys for a Redis cache</span></span>
<span data-ttu-id="b023f-281">Para recuperar las claves de acceso de la caché, puede usar el cmdlet [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b023f-281">To retrieve the access keys for your cache, you can use the [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet.</span></span>

<span data-ttu-id="b023f-282">Para ver una lista de parámetros disponibles y sus descripciones para `Get-AzureRmRedisCacheKey`, ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="b023f-282">To see a list of available parameters and their descriptions for `Get-AzureRmRedisCacheKey`, run the following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCacheKey -detailed

    NAME
        Get-AzureRmRedisCacheKey

    SYNOPSIS
        Gets the accesskeys for the specified redis cache.


    SYNTAX
        Get-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> [<CommonParameters>]

    DESCRIPTION
        The Get-AzureRmRedisCacheKey cmdlet gets the access keys for the specified cache.

    PARAMETERS
        -Name <String>
            Name of the redis cache.

        -ResourceGroupName <String>
            Name of the resource group for the cache.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="b023f-283">Para recuperar las claves de la caché, llame al cmdlet `Get-AzureRmRedisCacheKey` y pase el nombre de la memoria caché y el nombre del grupo de recursos que contiene la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="b023f-283">To retrieve the keys for your cache, call the `Get-AzureRmRedisCacheKey` cmdlet and pass in the name of your cache the name of the resource group that contains the cache.</span></span>

    PS C:\> Get-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup

    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : ABhfB757JgjIgt785JgKH9865eifmekfnn649303JKL=

## <a name="to-regenerate-access-keys-for-your-redis-cache"></a><span data-ttu-id="b023f-284">Regeneración de las claves de acceso de la caché en Redis</span><span class="sxs-lookup"><span data-stu-id="b023f-284">To regenerate access keys for your Redis cache</span></span>
<span data-ttu-id="b023f-285">Para regenerar las claves de acceso de la caché, puede usar el cmdlet [New-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b023f-285">To regenerate the access keys for your cache, you can use the [New-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet.</span></span>

<span data-ttu-id="b023f-286">Para ver una lista de parámetros disponibles y sus descripciones para `New-AzureRmRedisCacheKey`, ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="b023f-286">To see a list of available parameters and their descriptions for `New-AzureRmRedisCacheKey`, run the following command.</span></span>

    PS C:\> Get-Help New-AzureRmRedisCacheKey -detailed

    NAME
        New-AzureRmRedisCacheKey

    SYNOPSIS
        Regenerates the access key of a redis cache.

    SYNTAX
        New-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> -KeyType <String> [-Force] [<CommonParameters>]

    DESCRIPTION
        The New-AzureRmRedisCacheKey cmdlet regenerate the access key of a redis cache.

    PARAMETERS
        -Name <String>
            Name of the redis cache.

        -ResourceGroupName <String>
            Name of the resource group for the cache.

        -KeyType <String>
            Specifies whether to regenerate the primary or secondary access key. Possible values are Primary or Secondary.

        -Force
            When the Force parameter is provided, the specified access key is regenerated without any confirmation prompts.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="b023f-287">Para regenerar la clave principal o secundaria de la caché, llame al cmdlet `New-AzureRmRedisCacheKey` y pase el nombre, el grupo de recursos y especifique `Primary` o `Secondary` para el parámetro `KeyType`.</span><span class="sxs-lookup"><span data-stu-id="b023f-287">To regenerate the primary or secondary key for your cache, call the `New-AzureRmRedisCacheKey` cmdlet and pass in the name, resource group, and specify either `Primary` or `Secondary` for the `KeyType` parameter.</span></span> <span data-ttu-id="b023f-288">En el ejemplo siguiente, se regenera la clave de acceso secundaria de una memoria caché.</span><span class="sxs-lookup"><span data-stu-id="b023f-288">In the following example, the secondary access key for a cache is regenerated.</span></span>

    PS C:\> New-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup -KeyType Secondary

    Confirm
    Are you sure you want to regenerate Secondary key for redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : c53hj3kh4jhHjPJk8l0jji785JgKH9865eifmekfnn6=

## <a name="to-delete-a-redis-cache"></a><span data-ttu-id="b023f-289">Eliminación de una caché en Redis</span><span class="sxs-lookup"><span data-stu-id="b023f-289">To delete a Redis cache</span></span>
<span data-ttu-id="b023f-290">Para eliminar una caché en Redis, use el cmdlet [Remove-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b023f-290">To delete a Redis cache, use the [Remove-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet.</span></span>

<span data-ttu-id="b023f-291">Para ver una lista de parámetros disponibles y sus descripciones para `Remove-AzureRmRedisCache`, ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="b023f-291">To see a list of available parameters and their descriptions for `Remove-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Remove-AzureRmRedisCache -detailed

    NAME
        Remove-AzureRmRedisCache

    SYNOPSIS
        Remove redis cache if exists.

    SYNTAX
        Remove-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Force] [-PassThru] [<CommonParameters>

    DESCRIPTION
        The Remove-AzureRmRedisCache cmdlet removes a redis cache if it exists.

    PARAMETERS
        -Name <String>
            Name of the redis cache to remove.

        -ResourceGroupName <String>
            Name of the resource group of the cache to remove.

        -Force
            When the Force parameter is provided, the cache is removed without any confirmation prompts.

        -PassThru
            By default Remove-AzureRmRedisCache removes the cache and does not return any value. If the PassThru par
            is provided then Remove-AzureRmRedisCache returns a boolean value indicating the success of the operatio

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="b023f-292">En el ejemplo siguiente, se quita la memoria caché denominada `myCache` .</span><span class="sxs-lookup"><span data-stu-id="b023f-292">In the following example, the cache named `myCache` is removed.</span></span>

    PS C:\> Remove-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Confirm
    Are you sure you want to remove redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


## <a name="to-import-a-redis-cache"></a><span data-ttu-id="b023f-293">Importación de una caché en Redis</span><span class="sxs-lookup"><span data-stu-id="b023f-293">To import a Redis cache</span></span>
<span data-ttu-id="b023f-294">Puede importar datos a una instancia de Caché en Redis de Azure mediante el cmdlet `Import-AzureRmRedisCache` .</span><span class="sxs-lookup"><span data-stu-id="b023f-294">You can import data into an Azure Redis Cache instance using the `Import-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b023f-295">Importación/Exportación solo está disponible para las memorias caché de [nivel premium](cache-premium-tier-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="b023f-295">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="b023f-296">Para más información e instrucciones sobre Importación/Exportación, consulte [Importación y exportación de datos en la Caché en Redis de Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="b023f-296">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="b023f-297">Para ver una lista de parámetros disponibles y sus descripciones para `Import-AzureRmRedisCache`, ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="b023f-297">To see a list of available parameters and their descriptions for `Import-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Import-AzureRmRedisCache -detailed

    NAME
        Import-AzureRmRedisCache

    SYNOPSIS
        Import data from blobs to Azure Redis Cache.


    SYNTAX
        Import-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Files <String[]> [-Format <String>] [-Force]
        [-PassThru] [<CommonParameters>]


    DESCRIPTION
        The Import-AzureRmRedisCache cmdlet imports data from the specified blobs into Azure Redis Cache.


    PARAMETERS
        -Name <String>
            The name of the cache.

        -ResourceGroupName <String>
            The name of the resource group that contains the cache.

        -Files <String[]>
            SAS urls of blobs whose content should be imported into the cache.

        -Format <String>
            Format for the blob.  Currently "rdb" is the only supported, with other formats expected in the future.

        -Force
            When the Force parameter is provided, import will be performed without any confirmation prompts.

        -PassThru
            By default Import-AzureRmRedisCache imports data in cache and does not return any value. If the PassThru
            parameter is provided then Import-AzureRmRedisCache returns a boolean value indicating the success of the
            operation.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="b023f-298">El siguiente comando importa datos desde el blob especificado por el identificador URI de SAS de Caché en Redis de Azure.</span><span class="sxs-lookup"><span data-stu-id="b023f-298">The following command imports data from the blob specified by the SAS uri into Azure Redis Cache.</span></span>

    PS C:\>Import-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Files @("https://mystorageaccount.blob.core.windows.net/mycontainername/blobname?sv=2015-04-05&sr=b&sig=caIwutG2uDa0NZ8mjdNJdgOY8%2F8mhwRuGNdICU%2B0pI4%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwd") -Force

## <a name="to-export-a-redis-cache"></a><span data-ttu-id="b023f-299">Exportación de una caché en Redis</span><span class="sxs-lookup"><span data-stu-id="b023f-299">To export a Redis cache</span></span>
<span data-ttu-id="b023f-300">Puede exportar datos a una instancia de Caché en Redis de Azure mediante el cmdlet `Export-AzureRmRedisCache` .</span><span class="sxs-lookup"><span data-stu-id="b023f-300">You can export data from an Azure Redis Cache instance using the `Export-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b023f-301">Importación/Exportación solo está disponible para las memorias caché de [nivel premium](cache-premium-tier-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="b023f-301">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="b023f-302">Para más información e instrucciones sobre Importación/Exportación, consulte [Importación y exportación de datos en la Caché en Redis de Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="b023f-302">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="b023f-303">Para ver una lista de parámetros disponibles y sus descripciones para `Export-AzureRmRedisCache`, ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="b023f-303">To see a list of available parameters and their descriptions for `Export-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Export-AzureRmRedisCache -detailed

    NAME
        Export-AzureRmRedisCache

    SYNOPSIS
        Exports data from Azure Redis Cache to a specified container.


    SYNTAX
        Export-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Prefix <String> -Container <String> [-Format
        <String>] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        The Export-AzureRmRedisCache cmdlet exports data from Azure Redis Cache to a specified container.


    PARAMETERS
        -Name <String>
            The name of the cache.

        -ResourceGroupName <String>
            The name of the resource group that contains the cache.

        -Prefix <String>
            Prefix to use for blob names.

        -Container <String>
            SAS url of container where data should be exported.

        -Format <String>
            Format for the blob.  Currently "rdb" is the only supported, with other formats expected in the future.

        -PassThru
            By default Export-AzureRmRedisCache does not return any value. If the PassThru parameter is provided
            then Export-AzureRmRedisCache returns a boolean value indicating the success of the operation.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="b023f-304">El siguiente comando exporta los datos desde una instancia de Caché en Redis de Azure en el contenedor especificado por el identificador URI de SAS.</span><span class="sxs-lookup"><span data-stu-id="b023f-304">The following command exports data from an Azure Redis Cache instance into the container specified by the SAS uri.</span></span>

        PS C:\>Export-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Prefix "blobprefix"
        -Container "https://mystorageaccount.blob.core.windows.net/mycontainer?sv=2015-04-05&sr=c&sig=HezZtBZ3DURmEGDduauE7
        pvETY4kqlPI8JCNa8ATmaw%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwdl"

## <a name="to-reboot-a-redis-cache"></a><span data-ttu-id="b023f-305">Reinicio de una caché en Redis</span><span class="sxs-lookup"><span data-stu-id="b023f-305">To reboot a Redis cache</span></span>
<span data-ttu-id="b023f-306">Puede reiniciar la instancia de Caché en Redis de Azure mediante el cmdlet `Reset-AzureRmRedisCache` .</span><span class="sxs-lookup"><span data-stu-id="b023f-306">You can reboot your Azure Redis Cache instance using the `Reset-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b023f-307">El reinicio solo está disponible para las memorias caché de [nivel premium](cache-premium-tier-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="b023f-307">Reboot is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="b023f-308">Para más información acerca de cómo reiniciar la caché, consulte [Administración de caché: reinicio](cache-administration.md#reboot).</span><span class="sxs-lookup"><span data-stu-id="b023f-308">For more information about rebooting your cache, see [Cache administration - reboot](cache-administration.md#reboot).</span></span>
> 
> 

<span data-ttu-id="b023f-309">Para ver una lista de parámetros disponibles y sus descripciones para `Reset-AzureRmRedisCache`, ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="b023f-309">To see a list of available parameters and their descriptions for `Reset-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Reset-AzureRmRedisCache -detailed

    NAME
        Reset-AzureRmRedisCache

    SYNOPSIS
        Reboot specified node(s) of an Azure Redis Cache instance.


    SYNTAX
        Reset-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -RebootType <String> [-ShardId <Integer>]
        [-Force] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        The Reset-AzureRmRedisCache cmdlet reboots the specified node(s) of an Azure Redis Cache instance.


    PARAMETERS
        -Name <String>
            The name of the cache.

        -ResourceGroupName <String>
            The name of the resource group that contains the cache.

        -RebootType <String>
            Which node to reboot. Possible values are "PrimaryNode", "SecondaryNode", "AllNodes".

        -ShardId <Integer>
            Which shard to reboot when rebooting a premium cache with clustering enabled.

        -Force
            When the Force parameter is provided, reset will be performed without any confirmation prompts.

        -PassThru
            By default Reset-AzureRmRedisCache does not return any value. If the PassThru parameter is provided
            then Reset-AzureRmRedisCache returns a boolean value indicating the success of the operation.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="b023f-310">El siguiente comando reinicia ambos nodos de la memoria caché especificada.</span><span class="sxs-lookup"><span data-stu-id="b023f-310">The following command reboots both nodes of the specified cache.</span></span>

        PS C:\>Reset-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -RebootType "AllNodes"
        -Force


## <a name="next-steps"></a><span data-ttu-id="b023f-311">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b023f-311">Next steps</span></span>
<span data-ttu-id="b023f-312">Para obtener más información acerca de Windows PowerShell con Azure, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="b023f-312">To learn more about using Windows PowerShell with Azure, see the following resources:</span></span>

* [<span data-ttu-id="b023f-313">Documentación de cmdlet de caché en Redis de Azure en MSDN</span><span class="sxs-lookup"><span data-stu-id="b023f-313">Azure Redis Cache cmdlet documentation on MSDN</span></span>](https://msdn.microsoft.com/library/azure/mt634513.aspx)
* <span data-ttu-id="b023f-314">[Cmdlets de Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkID=394765): obtenga información acerca del uso de los cmdlets en el módulo de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b023f-314">[Azure Resource Manager Cmdlets](http://go.microsoft.com/fwlink/?LinkID=394765): Learn to use the cmdlets in the Azure Resource Manager module.</span></span>
* <span data-ttu-id="b023f-315">[Uso de grupos de recursos para administrar los recursos de Azure](../azure-resource-manager/resource-group-template-deploy-portal.md): obtenga información sobre la creación y administración de grupos de recursos en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b023f-315">[Using Resource groups to manage your Azure resources](../azure-resource-manager/resource-group-template-deploy-portal.md): Learn how to create and manage resource groups in the Azure portal.</span></span>
* <span data-ttu-id="b023f-316">[Blog de Azure](http://blogs.msdn.com/windowsazure): obtenga información acerca de las nuevas características de Azure.</span><span class="sxs-lookup"><span data-stu-id="b023f-316">[Azure blog](http://blogs.msdn.com/windowsazure): Learn about new features in Azure.</span></span>
* <span data-ttu-id="b023f-317">[Blog de Windows PowerShell](http://blogs.msdn.com/powershell): obtenga información acerca de las nuevas características de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b023f-317">[Windows PowerShell blog](http://blogs.msdn.com/powershell): Learn about new features in Windows PowerShell.</span></span>
* <span data-ttu-id="b023f-318">[Blog ¡Hola, chicos del scripting!](http://blogs.technet.com/b/heyscriptingguy/): Obtenga sugerencias y trucos del mundo real de la comunidad de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b023f-318">["Hey, Scripting Guy!" Blog](http://blogs.technet.com/b/heyscriptingguy/): Get real-world tips and tricks from the Windows PowerShell community.</span></span>

