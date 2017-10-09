---
title: "aaaManage caché en Redis de Azure con PowerShell de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooperform las tareas administrativas para caché en Redis de Azure con Azure PowerShell."
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
ms.openlocfilehash: 1d526ce65c4bc05345cd6c3ff370211ed562cab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-redis-cache-with-azure-powershell"></a><span data-ttu-id="3e2b5-103">Administración de Caché en Redis de Azure con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3e2b5-103">Manage Azure Redis Cache with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3e2b5-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3e2b5-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="3e2b5-105">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="3e2b5-105">Azure CLI</span></span>](cache-manage-cli.md)
> 
> 

<span data-ttu-id="3e2b5-106">Este tema muestra cómo tooperform comunes tareas como crear, actualizar y ampliar las instancias de caché en Redis de Azure, cómo tooregenerate teclas de acceso y cómo tooview información acerca de sus cachés.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-106">This topic shows you how tooperform common tasks such as create, update, and scale your Azure Redis Cache instances, how tooregenerate access keys, and how tooview information about your caches.</span></span> <span data-ttu-id="3e2b5-107">Para obtener una lista completa de cmdlets de PowerShell de caché en Redis de Azure, consulte [Azure Redis Cache cmdlets](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span><span class="sxs-lookup"><span data-stu-id="3e2b5-107">For a complete list of Azure Redis Cache PowerShell cmdlets, see [Azure Redis Cache cmdlets](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="3e2b5-108">Para obtener más información sobre el modelo de implementación clásica de hello, consulte [Azure Resource Manager frente a la implementación clásica: comprender los modelos de implementación y Hola estado de los recursos](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span><span class="sxs-lookup"><span data-stu-id="3e2b5-108">For more information about hello classic deployment model, see [Azure Resource Manager vs. classic deployment: Understand deployment models and hello state of your resources](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e2b5-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3e2b5-109">Prerequisites</span></span>
<span data-ttu-id="3e2b5-110">Si ya ha instalado Azure PowerShell, debe tener la versión 1.0.0 (o posterior) de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-110">If you have already installed Azure PowerShell, you must have Azure PowerShell version 1.0.0 or later.</span></span> <span data-ttu-id="3e2b5-111">Puede comprobar la versión de Hola de PowerShell de Azure que ha instalado con este comando en el símbolo del sistema de PowerShell de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-111">You can check hello version of Azure PowerShell that you have installed with this command at hello Azure PowerShell command prompt.</span></span>

    Get-Module azure | format-table version


<span data-ttu-id="3e2b5-112">En primer lugar, debe iniciar sesión en tooAzure con este comando.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-112">First, you must log in tooAzure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="3e2b5-113">Especifique la dirección de correo electrónico de Hola de su cuenta de Azure y su contraseña en el cuadro de diálogo de hello en el inicio de sesión de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-113">Specify hello email address of your Azure account and its password in hello Microsoft Azure sign-in dialog.</span></span>

<span data-ttu-id="3e2b5-114">A continuación, si tiene varias suscripciones de Azure, deberá tooset su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-114">Next, if you have multiple Azure subscriptions, you need tooset your Azure subscription.</span></span> <span data-ttu-id="3e2b5-115">toosee una lista de las suscripciones actuales, ejecute este comando.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-115">toosee a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="3e2b5-116">suscripción de hello toospecify, ejecute el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-116">toospecify hello subscription, run hello following command.</span></span> <span data-ttu-id="3e2b5-117">En el siguiente ejemplo de Hola, es el nombre de la suscripción de hello `ContosoSubscription`.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-117">In hello following example, hello subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

<span data-ttu-id="3e2b5-118">Para poder usar Windows PowerShell con el Administrador de recursos de Azure, necesita Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="3e2b5-118">Before you can use Windows PowerShell with Azure Resource Manager, you need hello following:</span></span>

* <span data-ttu-id="3e2b5-119">Windows PowerShell, versión 3.0 o 4.0.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-119">Windows PowerShell, Version 3.0 or 4.0.</span></span> <span data-ttu-id="3e2b5-120">versión de hello toofind de Windows PowerShell, escriba:`$PSVersionTable` y comprobar el valor de Hola de `PSVersion` es 3.0 o 4.0.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-120">toofind hello version of Windows PowerShell, type:`$PSVersionTable` and verify hello value of `PSVersion` is 3.0 or 4.0.</span></span> <span data-ttu-id="3e2b5-121">tooinstall una versión compatible, consulte [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) o [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span><span class="sxs-lookup"><span data-stu-id="3e2b5-121">tooinstall a compatible version, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

<span data-ttu-id="3e2b5-122">tooget ayuda detallada de cualquier cmdlet que se ven en este tutorial, use el cmdlet Get-Help de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-122">tooget detailed help for any cmdlet you see in this tutorial, use hello Get-Help cmdlet.</span></span>

    Get-Help <cmdlet-name> -Detailed

<span data-ttu-id="3e2b5-123">Por ejemplo, tooget ayuda para hello `New-AzureRmRedisCache` cmdlet, escriba:</span><span class="sxs-lookup"><span data-stu-id="3e2b5-123">For example, tooget help for hello `New-AzureRmRedisCache` cmdlet, type:</span></span>

    Get-Help New-AzureRmRedisCache -Detailed

### <a name="how-tooconnect-tooother-clouds"></a><span data-ttu-id="3e2b5-124">Cómo tooconnect tooother nubes</span><span class="sxs-lookup"><span data-stu-id="3e2b5-124">How tooconnect tooother clouds</span></span>
<span data-ttu-id="3e2b5-125">Hola predeterminado Azure entorno es `AzureCloud`, que representa Hola instancia global de nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-125">By default hello Azure environment is `AzureCloud`, which represents hello global Azure cloud instance.</span></span> <span data-ttu-id="3e2b5-126">tooconnect tooa otra instancia, utilice hello `Add-AzureRmAccount` comando con hello `-Environment` o -`EnvironmentName` modificador de línea de comandos con el entorno deseado de Hola o nombre del entorno.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-126">tooconnect tooa different instance, use hello `Add-AzureRmAccount` command with hello `-Environment` or -`EnvironmentName` command line switch with hello desired environment or environment name.</span></span>

<span data-ttu-id="3e2b5-127">lista de hello toosee de entornos disponibles, ejecute hello `Get-AzureRmEnvironment` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-127">toosee hello list of available environments, run hello `Get-AzureRmEnvironment` cmdlet.</span></span>

### <a name="tooconnect-toohello-azure-government-cloud"></a><span data-ttu-id="3e2b5-128">tooconnect toohello nube de la administración pública de Azure</span><span class="sxs-lookup"><span data-stu-id="3e2b5-128">tooconnect toohello Azure Government Cloud</span></span>
<span data-ttu-id="3e2b5-129">tooconnect toohello nube de la administración pública de Azure, use uno de hello siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-129">tooconnect toohello Azure Government Cloud, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureUSGovernment

<span data-ttu-id="3e2b5-130">o</span><span class="sxs-lookup"><span data-stu-id="3e2b5-130">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureUSGovernment)

<span data-ttu-id="3e2b5-131">toocreate una memoria caché en hello Azure gobierno en la nube, use uno de hello ubicaciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-131">toocreate a cache in hello Azure Government Cloud, use one of hello following locations.</span></span>

* <span data-ttu-id="3e2b5-132">USGov Virginia</span><span class="sxs-lookup"><span data-stu-id="3e2b5-132">USGov Virginia</span></span>
* <span data-ttu-id="3e2b5-133">USGov Iowa</span><span class="sxs-lookup"><span data-stu-id="3e2b5-133">USGov Iowa</span></span>

<span data-ttu-id="3e2b5-134">Para obtener más información acerca de hello Azure gobierno en la nube, consulte [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) y [guía para desarrolladores de Microsoft Azure Government](../azure-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="3e2b5-134">For more information about hello Azure Government Cloud, see [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) and [Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>

### <a name="tooconnect-toohello-azure-china-cloud"></a><span data-ttu-id="3e2b5-135">tooconnect toohello Azure China en la nube</span><span class="sxs-lookup"><span data-stu-id="3e2b5-135">tooconnect toohello Azure China Cloud</span></span>
<span data-ttu-id="3e2b5-136">tooconnect toohello Azure China en la nube, use uno de hello siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-136">tooconnect toohello Azure China Cloud, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureChinaCloud

<span data-ttu-id="3e2b5-137">o</span><span class="sxs-lookup"><span data-stu-id="3e2b5-137">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureChinaCloud)

<span data-ttu-id="3e2b5-138">toocreate una memoria caché en hello Azure China en la nube, use uno de hello ubicaciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-138">toocreate a cache in hello Azure China Cloud, use one of hello following locations.</span></span>

* <span data-ttu-id="3e2b5-139">Este de China</span><span class="sxs-lookup"><span data-stu-id="3e2b5-139">China East</span></span>
* <span data-ttu-id="3e2b5-140">Norte de China</span><span class="sxs-lookup"><span data-stu-id="3e2b5-140">China North</span></span>

<span data-ttu-id="3e2b5-141">Para obtener más información acerca de la nube de Azure China hello, consulte [AzureChinaCloud de Azure operado por 21Vianet en China](http://www.windowsazure.cn/).</span><span class="sxs-lookup"><span data-stu-id="3e2b5-141">For more information about hello Azure China Cloud, see [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span>

### <a name="tooconnect-toomicrosoft-azure-germany"></a><span data-ttu-id="3e2b5-142">tooconnect tooMicrosoft Alemania de Azure</span><span class="sxs-lookup"><span data-stu-id="3e2b5-142">tooconnect tooMicrosoft Azure Germany</span></span>
<span data-ttu-id="3e2b5-143">tooconnect tooMicrosoft Alemania de Azure, use uno de hello siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-143">tooconnect tooMicrosoft Azure Germany, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureGermanCloud


<span data-ttu-id="3e2b5-144">o</span><span class="sxs-lookup"><span data-stu-id="3e2b5-144">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureGermanCloud)

<span data-ttu-id="3e2b5-145">toocreate una memoria caché en Microsoft Azure en Alemania, utilice uno de hello ubicaciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-145">toocreate a cache in Microsoft Azure Germany, use one of hello following locations.</span></span>

* <span data-ttu-id="3e2b5-146">Centro de Alemania</span><span class="sxs-lookup"><span data-stu-id="3e2b5-146">Germany Central</span></span>
* <span data-ttu-id="3e2b5-147">Noreste de Alemania</span><span class="sxs-lookup"><span data-stu-id="3e2b5-147">Germany Northeast</span></span>

<span data-ttu-id="3e2b5-148">Para obtener más información acerca de Microsoft Azure Alemania, consulte [Microsoft Azure Germany](https://azure.microsoft.com/overview/clouds/germany/).</span><span class="sxs-lookup"><span data-stu-id="3e2b5-148">For more information about Microsoft Azure Germany, see [Microsoft Azure Germany](https://azure.microsoft.com/overview/clouds/germany/).</span></span>

### <a name="properties-used-for-azure-redis-cache-powershell"></a><span data-ttu-id="3e2b5-149">Propiedades utilizadas para Caché en Redis de Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="3e2b5-149">Properties used for Azure Redis Cache PowerShell</span></span>
<span data-ttu-id="3e2b5-150">Hello en la tabla siguiente contiene las propiedades y las descripciones de parámetros utilizados con frecuencia al crear y administrar las instancias de caché en Redis de Azure con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-150">hello following table contains properties and descriptions for commonly used parameters when creating and managing your Azure Redis Cache instances using Azure PowerShell.</span></span>

| <span data-ttu-id="3e2b5-151">Parámetro</span><span class="sxs-lookup"><span data-stu-id="3e2b5-151">Parameter</span></span> | <span data-ttu-id="3e2b5-152">Description</span><span class="sxs-lookup"><span data-stu-id="3e2b5-152">Description</span></span> | <span data-ttu-id="3e2b5-153">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="3e2b5-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e2b5-154">Nombre</span><span class="sxs-lookup"><span data-stu-id="3e2b5-154">Name</span></span> |<span data-ttu-id="3e2b5-155">Nombre de caché de Hola</span><span class="sxs-lookup"><span data-stu-id="3e2b5-155">Name of hello cache</span></span> | |
| <span data-ttu-id="3e2b5-156">Ubicación</span><span class="sxs-lookup"><span data-stu-id="3e2b5-156">Location</span></span> |<span data-ttu-id="3e2b5-157">Ubicación de caché de Hola</span><span class="sxs-lookup"><span data-stu-id="3e2b5-157">Location of hello cache</span></span> | |
| <span data-ttu-id="3e2b5-158">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="3e2b5-158">ResourceGroupName</span></span> |<span data-ttu-id="3e2b5-159">Nombre de grupo de recursos en la caché de hello toocreate</span><span class="sxs-lookup"><span data-stu-id="3e2b5-159">Resource group name in which toocreate hello cache</span></span> | |
| <span data-ttu-id="3e2b5-160">Tamaño</span><span class="sxs-lookup"><span data-stu-id="3e2b5-160">Size</span></span> |<span data-ttu-id="3e2b5-161">tamaño de Hola de caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-161">hello size of hello cache.</span></span> <span data-ttu-id="3e2b5-162">Los valores válidos son: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250 MB, 1 GB, 2,5 GB, 6 GB, 13 GB, 26 GB, 53 GB</span><span class="sxs-lookup"><span data-stu-id="3e2b5-162">Valid values are: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB</span></span> |<span data-ttu-id="3e2b5-163">1 GB</span><span class="sxs-lookup"><span data-stu-id="3e2b5-163">1GB</span></span> |
| <span data-ttu-id="3e2b5-164">ShardCount</span><span class="sxs-lookup"><span data-stu-id="3e2b5-164">ShardCount</span></span> |<span data-ttu-id="3e2b5-165">número de Hola de particiones toocreate al crear una caché premium con clúster habilitado.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-165">hello number of shards toocreate when creating a premium cache with clustering enabled.</span></span> <span data-ttu-id="3e2b5-166">Los valores válidos son: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span><span class="sxs-lookup"><span data-stu-id="3e2b5-166">Valid values are: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span></span> | |
| <span data-ttu-id="3e2b5-167">SKU</span><span class="sxs-lookup"><span data-stu-id="3e2b5-167">SKU</span></span> |<span data-ttu-id="3e2b5-168">Especifica la SKU de la memoria caché de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-168">Specifies hello SKU of hello cache.</span></span> <span data-ttu-id="3e2b5-169">Los valores válidos son: Básico, Estándar y Premium</span><span class="sxs-lookup"><span data-stu-id="3e2b5-169">Valid values are: Basic, Standard, Premium</span></span> |<span data-ttu-id="3e2b5-170">Estándar</span><span class="sxs-lookup"><span data-stu-id="3e2b5-170">Standard</span></span> |
| <span data-ttu-id="3e2b5-171">RedisConfiguration</span><span class="sxs-lookup"><span data-stu-id="3e2b5-171">RedisConfiguration</span></span> |<span data-ttu-id="3e2b5-172">Especifica la configuración de Redis.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-172">Specifies Redis configuration settings.</span></span> <span data-ttu-id="3e2b5-173">Para obtener más información acerca de cada opción, vea el siguiente hello [RedisConfiguration propiedades](#redisconfiguration-properties) tabla.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-173">For details on each setting, see hello following [RedisConfiguration properties](#redisconfiguration-properties) table.</span></span> | |
| <span data-ttu-id="3e2b5-174">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="3e2b5-174">EnableNonSslPort</span></span> |<span data-ttu-id="3e2b5-175">Indica si está habilitado el puerto no SSL de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-175">Indicates whether hello non-SSL port is enabled.</span></span> |<span data-ttu-id="3e2b5-176">False</span><span class="sxs-lookup"><span data-stu-id="3e2b5-176">False</span></span> |
| <span data-ttu-id="3e2b5-177">MaxMemoryPolicy</span><span class="sxs-lookup"><span data-stu-id="3e2b5-177">MaxMemoryPolicy</span></span> |<span data-ttu-id="3e2b5-178">Este parámetro está en desuso; utilice RedisConfiguration en su lugar.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-178">This parameter has been deprecated - use RedisConfiguration instead.</span></span> | |
| <span data-ttu-id="3e2b5-179">StaticIP</span><span class="sxs-lookup"><span data-stu-id="3e2b5-179">StaticIP</span></span> |<span data-ttu-id="3e2b5-180">Al hospedar la memoria caché en una red virtual, especifica una dirección IP única en la subred de Hola para caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-180">When hosting your cache in a VNET, specifies a unique IP address in hello subnet for hello cache.</span></span> <span data-ttu-id="3e2b5-181">Si no se proporciona, se elige una automáticamente de la subred de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-181">If not provided, one is chosen for you from hello subnet.</span></span> | |
| <span data-ttu-id="3e2b5-182">Subred</span><span class="sxs-lookup"><span data-stu-id="3e2b5-182">Subnet</span></span> |<span data-ttu-id="3e2b5-183">Al hospedar la memoria caché en una red virtual, especifica el nombre de Hola de subred de hello en la caché de hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-183">When hosting your cache in a VNET, specifies hello name of hello subnet in which toodeploy hello cache.</span></span> | |
| <span data-ttu-id="3e2b5-184">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="3e2b5-184">VirtualNetwork</span></span> |<span data-ttu-id="3e2b5-185">Cuando se hospeda la memoria caché en una red virtual, especifica el identificador de recurso de Hola de Hola red virtual en la caché de hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-185">When hosting your cache in a VNET, specifies hello resource ID of hello VNET in which toodeploy hello cache.</span></span> | |
| <span data-ttu-id="3e2b5-186">KeyType</span><span class="sxs-lookup"><span data-stu-id="3e2b5-186">KeyType</span></span> |<span data-ttu-id="3e2b5-187">Especifica qué tecla de acceso tooregenerate cuando se renueva las claves de acceso.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-187">Specifies which access key tooregenerate when renewing access keys.</span></span> <span data-ttu-id="3e2b5-188">Los valores válidos son: primario, secundario</span><span class="sxs-lookup"><span data-stu-id="3e2b5-188">Valid values are: Primary, Secondary</span></span> | |

### <a name="redisconfiguration-properties"></a><span data-ttu-id="3e2b5-189">Propiedades de RedisConfiguration</span><span class="sxs-lookup"><span data-stu-id="3e2b5-189">RedisConfiguration properties</span></span>
| <span data-ttu-id="3e2b5-190">Propiedad</span><span class="sxs-lookup"><span data-stu-id="3e2b5-190">Property</span></span> | <span data-ttu-id="3e2b5-191">Description</span><span class="sxs-lookup"><span data-stu-id="3e2b5-191">Description</span></span> | <span data-ttu-id="3e2b5-192">Planes de tarifa</span><span class="sxs-lookup"><span data-stu-id="3e2b5-192">Pricing tiers</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e2b5-193">rdb-backup-enabled</span><span class="sxs-lookup"><span data-stu-id="3e2b5-193">rdb-backup-enabled</span></span> |<span data-ttu-id="3e2b5-194">Si [Persistencia de los datos en Redis](cache-how-to-premium-persistence.md) está habilitado</span><span class="sxs-lookup"><span data-stu-id="3e2b5-194">Whether [Redis data persistence](cache-how-to-premium-persistence.md) is enabled</span></span> |<span data-ttu-id="3e2b5-195">Solo Premium</span><span class="sxs-lookup"><span data-stu-id="3e2b5-195">Premium only</span></span> |
| <span data-ttu-id="3e2b5-196">rdb-storage-connection-string</span><span class="sxs-lookup"><span data-stu-id="3e2b5-196">rdb-storage-connection-string</span></span> |<span data-ttu-id="3e2b5-197">Hola cuenta de almacenamiento de toohello de cadena de conexión para [Redis persistencia de datos](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="3e2b5-197">hello connection string toohello storage account for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="3e2b5-198">Solo Premium</span><span class="sxs-lookup"><span data-stu-id="3e2b5-198">Premium only</span></span> |
| <span data-ttu-id="3e2b5-199">rdb-backup-frequency</span><span class="sxs-lookup"><span data-stu-id="3e2b5-199">rdb-backup-frequency</span></span> |<span data-ttu-id="3e2b5-200">Hola frecuencia de copia de seguridad para [Redis persistencia de datos](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="3e2b5-200">hello backup frequency for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="3e2b5-201">Solo Premium</span><span class="sxs-lookup"><span data-stu-id="3e2b5-201">Premium only</span></span> |
| <span data-ttu-id="3e2b5-202">maxmemory-reserved</span><span class="sxs-lookup"><span data-stu-id="3e2b5-202">maxmemory-reserved</span></span> |<span data-ttu-id="3e2b5-203">Configura hello [memoria reservada](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) para procesos sin caché</span><span class="sxs-lookup"><span data-stu-id="3e2b5-203">Configures hello [memory reserved](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for non-cache processes</span></span> |<span data-ttu-id="3e2b5-204">Estándar y Premium</span><span class="sxs-lookup"><span data-stu-id="3e2b5-204">Standard and Premium</span></span> |
| <span data-ttu-id="3e2b5-205">maxmemory-policy</span><span class="sxs-lookup"><span data-stu-id="3e2b5-205">maxmemory-policy</span></span> |<span data-ttu-id="3e2b5-206">Configura hello [directiva de expulsión](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) para caché de Hola</span><span class="sxs-lookup"><span data-stu-id="3e2b5-206">Configures hello [eviction policy](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for hello cache</span></span> |<span data-ttu-id="3e2b5-207">Todos los planes de tarifa</span><span class="sxs-lookup"><span data-stu-id="3e2b5-207">All pricing tiers</span></span> |
| <span data-ttu-id="3e2b5-208">notify-keyspace-events</span><span class="sxs-lookup"><span data-stu-id="3e2b5-208">notify-keyspace-events</span></span> |<span data-ttu-id="3e2b5-209">Configura las [notificaciones de Keyspace](cache-configure.md#keyspace-notifications-advanced-settings)</span><span class="sxs-lookup"><span data-stu-id="3e2b5-209">Configures [keyspace notifications](cache-configure.md#keyspace-notifications-advanced-settings)</span></span> |<span data-ttu-id="3e2b5-210">Estándar y Premium</span><span class="sxs-lookup"><span data-stu-id="3e2b5-210">Standard and Premium</span></span> |
| <span data-ttu-id="3e2b5-211">hash-max-ziplist-entries</span><span class="sxs-lookup"><span data-stu-id="3e2b5-211">hash-max-ziplist-entries</span></span> |<span data-ttu-id="3e2b5-212">Configura la [optimización de memoria](http://redis.io/topics/memory-optimization) para tipos de datos agregados pequeños</span><span class="sxs-lookup"><span data-stu-id="3e2b5-212">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="3e2b5-213">Estándar y Premium</span><span class="sxs-lookup"><span data-stu-id="3e2b5-213">Standard and Premium</span></span> |
| <span data-ttu-id="3e2b5-214">hash-max-ziplist-value</span><span class="sxs-lookup"><span data-stu-id="3e2b5-214">hash-max-ziplist-value</span></span> |<span data-ttu-id="3e2b5-215">Configura la [optimización de memoria](http://redis.io/topics/memory-optimization) para tipos de datos agregados pequeños</span><span class="sxs-lookup"><span data-stu-id="3e2b5-215">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="3e2b5-216">Estándar y Premium</span><span class="sxs-lookup"><span data-stu-id="3e2b5-216">Standard and Premium</span></span> |
| <span data-ttu-id="3e2b5-217">set-max-intset-entries</span><span class="sxs-lookup"><span data-stu-id="3e2b5-217">set-max-intset-entries</span></span> |<span data-ttu-id="3e2b5-218">Configura la [optimización de memoria](http://redis.io/topics/memory-optimization) para tipos de datos agregados pequeños</span><span class="sxs-lookup"><span data-stu-id="3e2b5-218">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="3e2b5-219">Estándar y Premium</span><span class="sxs-lookup"><span data-stu-id="3e2b5-219">Standard and Premium</span></span> |
| <span data-ttu-id="3e2b5-220">zset-max-ziplist-entries</span><span class="sxs-lookup"><span data-stu-id="3e2b5-220">zset-max-ziplist-entries</span></span> |<span data-ttu-id="3e2b5-221">Configura la [optimización de memoria](http://redis.io/topics/memory-optimization) para tipos de datos agregados pequeños</span><span class="sxs-lookup"><span data-stu-id="3e2b5-221">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="3e2b5-222">Estándar y Premium</span><span class="sxs-lookup"><span data-stu-id="3e2b5-222">Standard and Premium</span></span> |
| <span data-ttu-id="3e2b5-223">zset-max-ziplist-value</span><span class="sxs-lookup"><span data-stu-id="3e2b5-223">zset-max-ziplist-value</span></span> |<span data-ttu-id="3e2b5-224">Configura la [optimización de memoria](http://redis.io/topics/memory-optimization) para tipos de datos agregados pequeños</span><span class="sxs-lookup"><span data-stu-id="3e2b5-224">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="3e2b5-225">Estándar y Premium</span><span class="sxs-lookup"><span data-stu-id="3e2b5-225">Standard and Premium</span></span> |
| <span data-ttu-id="3e2b5-226">bases de datos</span><span class="sxs-lookup"><span data-stu-id="3e2b5-226">databases</span></span> |<span data-ttu-id="3e2b5-227">Configura el número de Hola de bases de datos.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-227">Configures hello number of databases.</span></span> <span data-ttu-id="3e2b5-228">Esta propiedad solo se puede configurar al crear la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-228">This property can be configured only at cache creation.</span></span> |<span data-ttu-id="3e2b5-229">Estándar y Premium</span><span class="sxs-lookup"><span data-stu-id="3e2b5-229">Standard and Premium</span></span> |

## <a name="toocreate-a-redis-cache"></a><span data-ttu-id="3e2b5-230">toocreate una caché en Redis</span><span class="sxs-lookup"><span data-stu-id="3e2b5-230">toocreate a Redis Cache</span></span>
<span data-ttu-id="3e2b5-231">Se crean nuevas instancias de caché en Redis de Azure con hello [AzureRmRedisCache New](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-231">New Azure Redis Cache instances are created using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3e2b5-232">Hello primera vez que cree una caché de Redis en una suscripción mediante el portal de Azure, Hola portal Hola registra hello `Microsoft.Cache` espacio de nombres para esa suscripción.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-232">hello first time you create a Redis cache in a subscription using hello Azure portal, hello portal registers hello `Microsoft.Cache` namespace for that subscription.</span></span> <span data-ttu-id="3e2b5-233">Si intenta toocreate Hola primero la caché en una suscripción mediante PowerShell en Redis, primero debe registrar ese espacio de nombres mediante el siguiente comando; de Hola en caso contrario cmdlets como `New-AzureRmRedisCache` y `Get-AzureRmRedisCache` producirá un error.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-233">If you attempt toocreate hello first Redis cache in a subscription using PowerShell, you must first register that namespace using hello following command; otherwise cmdlets such as `New-AzureRmRedisCache` and `Get-AzureRmRedisCache` fail.</span></span>
> 
> `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Cache"`
> 
> 

<span data-ttu-id="3e2b5-234">toosee una lista de parámetros disponibles y sus descripciones para `New-AzureRmRedisCache`, ejecute hello después del comando.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-234">toosee a list of available parameters and their descriptions for `New-AzureRmRedisCache`, run hello following command.</span></span>

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
        hello New-AzureRmRedisCache cmdlet creates a new redis cache.


    PARAMETERS
        -Name <String>
            Name of hello redis cache toocreate.

        -ResourceGroupName <String>
            Name of resource group in which toocreate hello redis cache.

        -Location <String>
            Location in which toocreate hello redis cache.

        -RedisVersion <String>
            RedisVersion is deprecated and will be removed in future release.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value, databases.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. If no value is provided, hello default value is false and the
            non-SSL port will be disabled. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        -VirtualNetwork <String>
            hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{
            subid}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicNetwork/VirtualNetworks/{vnetName}

        -Subnet <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        -StaticIP <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="3e2b5-235">toocreate una memoria caché con los parámetros predeterminados, ejecute el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-235">toocreate a cache with default parameters, run hello following command.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US"

<span data-ttu-id="3e2b5-236">`ResourceGroupName`, `Name`, y `Location` son parámetros necesarios, pero el resto de hello son opcional y tienen valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-236">`ResourceGroupName`, `Name`, and `Location` are required parameters, but hello rest are optional and have default values.</span></span> <span data-ttu-id="3e2b5-237">Ejecuta el comando anterior Hola crea una instancia de caché de Redis de Azure de SKU estándar con el nombre especificado de hello, la ubicación y el grupo de recursos, que es de 1 GB de tamaño con el puerto no SSL de hello deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-237">Running hello previous command creates a Standard SKU Azure Redis Cache instance with hello specified name, location, and resource group, that is 1 GB in size with hello non-SSL port disabled.</span></span>

<span data-ttu-id="3e2b5-238">toocreate una caché premium, especifique un tamaño de P1 (6 GB - 60 GB), P2 (13 GB a 130 GB), P3 (26 GB - 260 GB), o P4 (53 GB - 530 GB).</span><span class="sxs-lookup"><span data-stu-id="3e2b5-238">toocreate a premium cache, specify a size of P1 (6 GB - 60 GB), P2 (13 GB - 130 GB), P3 (26 GB - 260 GB), or P4 (53 GB - 530 GB).</span></span> <span data-ttu-id="3e2b5-239">tooenable agrupación en clústeres, especifique un número de particiones con hello `ShardCount` parámetro.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-239">tooenable clustering, specify a shard count using hello `ShardCount` parameter.</span></span> <span data-ttu-id="3e2b5-240">Hello en el ejemplo siguiente se crea una memoria caché premium de P1 con 3 particiones.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-240">hello following example creates a P1 premium cache with 3 shards.</span></span> <span data-ttu-id="3e2b5-241">Una memoria caché premium de P1 es 6 GB de tamaño y, puesto que se especifican tres particiones Hola tamaño total es 18 GB (3 x 6 GB).</span><span class="sxs-lookup"><span data-stu-id="3e2b5-241">A P1 premium cache is 6 GB in size, and since we specified three shards hello total size is 18 GB (3 x 6 GB).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P1 -ShardCount 3

<span data-ttu-id="3e2b5-242">valores toospecify para hello `RedisConfiguration` parámetro, incluya valores de hello `{}` como clave y valor como pares `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-242">toospecify values for hello `RedisConfiguration` parameter, enclose hello values inside `{}` as key/value pairs like `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span></span> <span data-ttu-id="3e2b5-243">Hello en el ejemplo siguiente se crea una caché de 1 GB estándar con `allkeys-random` notificaciones de keyspace y directivas de maxmemory configuradas con `KEA`.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-243">hello following example creates a standard 1 GB cache with `allkeys-random` maxmemory policy and keyspace notifications configured with `KEA`.</span></span> <span data-ttu-id="3e2b5-244">Para más información, consulte [Notificaciones de Keyspace (configuración avanzada)](cache-configure.md#keyspace-notifications-advanced-settings) y [Directivas de memoria](cache-configure.md#memory-policies).</span><span class="sxs-lookup"><span data-stu-id="3e2b5-244">For more information, see [Keyspace notifications (advanced settings)](cache-configure.md#keyspace-notifications-advanced-settings) and [Memory policies](cache-configure.md#memory-policies).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}

<a name="databases"></a>

## <a name="tooconfigure-hello-databases-setting-during-cache-creation"></a><span data-ttu-id="3e2b5-245">bases de datos de tooconfigure Hola establecer durante la creación de cachés</span><span class="sxs-lookup"><span data-stu-id="3e2b5-245">tooconfigure hello databases setting during cache creation</span></span>
<span data-ttu-id="3e2b5-246">Hola `databases` se puede configurar solo durante la creación de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-246">hello `databases` setting can be configured only during cache creation.</span></span> <span data-ttu-id="3e2b5-247">Hello en el ejemplo siguiente se crea un P3 premium (26 GB) de memoria caché con 48 bases de datos mediante hello [AzureRmRedisCache New](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-247">hello following example creates a premium P3 (26 GB) cache with 48 databases using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P3 -RedisConfiguration @{"databases" = "48"}

<span data-ttu-id="3e2b5-248">Para obtener más información sobre hello `databases` propiedad, vea [configuración del servidor de caché en Redis de Azure predeterminado](cache-configure.md#default-redis-server-configuration).</span><span class="sxs-lookup"><span data-stu-id="3e2b5-248">For more information on hello `databases` property, see [Default Azure Redis Cache server configuration](cache-configure.md#default-redis-server-configuration).</span></span> <span data-ttu-id="3e2b5-249">Para obtener más información acerca de cómo crear una memoria caché mediante hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet, vea Hola anterior [toocreate una caché en Redis](#to-create-a-redis-cache) sección.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-249">For more information on creating a cache using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet, see hello previous [toocreate a Redis Cache](#to-create-a-redis-cache) section.</span></span>

## <a name="tooupdate-a-redis-cache"></a><span data-ttu-id="3e2b5-250">tooupdate una caché de Redis</span><span class="sxs-lookup"><span data-stu-id="3e2b5-250">tooupdate a Redis cache</span></span>
<span data-ttu-id="3e2b5-251">Instancias de caché en Redis de Azure se actualizan utilizando hello [AzureRmRedisCache conjunto](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-251">Azure Redis Cache instances are updated using hello [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet.</span></span>

<span data-ttu-id="3e2b5-252">toosee una lista de parámetros disponibles y sus descripciones para `Set-AzureRmRedisCache`, ejecute hello después del comando.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-252">toosee a list of available parameters and their descriptions for `Set-AzureRmRedisCache`, run hello following command.</span></span>

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
        hello Set-AzureRmRedisCache cmdlet sets redis cache parameters.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooupdate.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. hello default value is null and no change will be made toothe
            currently configured value. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="3e2b5-253">Hola `Set-AzureRmRedisCache` cmdlet puede ser propiedades tooupdate usado como `Size`, `Sku`, `EnableNonSslPort`, hello y `RedisConfiguration` valores.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-253">hello `Set-AzureRmRedisCache` cmdlet can be used tooupdate properties such as `Size`, `Sku`, `EnableNonSslPort`, and hello `RedisConfiguration` values.</span></span> 

<span data-ttu-id="3e2b5-254">Hello siguiente comando actualizaciones Hola directiva maxmemory para hello caché en Redis denominado myCache.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-254">hello following command updates hello maxmemory-policy for hello Redis Cache named myCache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName "myGroup" -Name "myCache" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random"}

<a name="scale"></a>

## <a name="tooscale-a-redis-cache"></a><span data-ttu-id="3e2b5-255">tooscale una caché de Redis</span><span class="sxs-lookup"><span data-stu-id="3e2b5-255">tooscale a Redis cache</span></span>
<span data-ttu-id="3e2b5-256">`Set-AzureRmRedisCache`puede ser tooscale usa una instancia de caché Redis de Azure cuando hello `Size`, `Sku`, o `ShardCount` propiedades se modifican.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-256">`Set-AzureRmRedisCache` can be used tooscale an Azure Redis cache instance when hello `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> 

> [!NOTE]
> <span data-ttu-id="3e2b5-257">Escalar una memoria caché con PowerShell es asunto toohello mismos límites y directrices como escalar una memoria caché de Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-257">Scaling a cache using PowerShell is subject toohello same limits and guidelines as scaling a cache from hello Azure portal.</span></span> <span data-ttu-id="3e2b5-258">Puede escalar tooa otro nivel de precios con hello siguiendo las restricciones.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-258">You can scale tooa different pricing tier with hello following restrictions.</span></span>
> 
> * <span data-ttu-id="3e2b5-259">No se puede escalar de un plan de tarifa mayor nivel tooa menor nivel de precios.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-259">You can't scale from a higher pricing tier tooa lower pricing tier.</span></span>
> * <span data-ttu-id="3e2b5-260">No se puede escalar de un **Premium** caché hacia abajo tooa **estándar** o un **básica** memoria caché.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-260">You can't scale from a **Premium** cache down tooa **Standard** or a **Basic** cache.</span></span>
> * <span data-ttu-id="3e2b5-261">No se puede escalar de un **estándar** caché hacia abajo tooa **básica** memoria caché.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-261">You can't scale from a **Standard** cache down tooa **Basic** cache.</span></span>
> * <span data-ttu-id="3e2b5-262">Puede escalar de un **básica** almacenar en caché tooa **estándar** caché pero no se puede cambiar el tamaño de hello en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-262">You can scale from a **Basic** cache tooa **Standard** cache but you can't change hello size at hello same time.</span></span> <span data-ttu-id="3e2b5-263">Si tiene un tamaño diferente, puede hacer un tamaño de toohello deseado de operación de escalado posteriores.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-263">If you need a different size, you can do a subsequent scaling operation toohello desired size.</span></span>
> * <span data-ttu-id="3e2b5-264">No se puede escalar de un **básica** almacenar en caché directamente tooa **Premium** memoria caché.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-264">You can't scale from a **Basic** cache directly tooa **Premium** cache.</span></span> <span data-ttu-id="3e2b5-265">Debe escalar **básica** demasiado**estándar** en una sola operación de escala y, a continuación, desde **estándar** demasiado**Premium** en una escala posteriores operación.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-265">You must scale from **Basic** too**Standard** in one scaling operation, and then from **Standard** too**Premium** in a subsequent scaling operation.</span></span>
> * <span data-ttu-id="3e2b5-266">No se puede escalar de un tamaño mayor profundidad toohello **C0 (250 MB)** tamaño.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-266">You can't scale from a larger size down toohello **C0 (250 MB)** size.</span></span>
> 
> <span data-ttu-id="3e2b5-267">Para obtener más información, consulte [cómo tooScale Redis de Azure almacenan en caché](cache-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="3e2b5-267">For more information, see [How tooScale Azure Redis Cache](cache-how-to-scale.md).</span></span>
> 
> 

<span data-ttu-id="3e2b5-268">Hello en el ejemplo siguiente se muestra cómo tooscale una memoria caché denominado `myCache` 2,5 GB de memoria caché de tooa.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-268">hello following example shows how tooscale a cache named `myCache` tooa 2.5 GB cache.</span></span> <span data-ttu-id="3e2b5-269">Tenga en cuenta que este comando funciona con una memoria caché básica o una estándar.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-269">Note that this command works for both a Basic or a Standard cache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="3e2b5-270">Después de emite este comando, se devuelve el estado de Hola de caché de hello (toocalling similar `Get-AzureRmRedisCache`).</span><span class="sxs-lookup"><span data-stu-id="3e2b5-270">After this command is issued, hello status of hello cache is returned (similar toocalling `Get-AzureRmRedisCache`).</span></span> <span data-ttu-id="3e2b5-271">Tenga en cuenta que hello `ProvisioningState` es `Scaling`.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-271">Note that hello `ProvisioningState` is `Scaling`.</span></span>

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

<span data-ttu-id="3e2b5-272">Una vez completada la operación de escalado de hello, Hola `ProvisioningState` cambia demasiado`Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-272">When hello scaling operation is complete, hello `ProvisioningState` changes too`Succeeded`.</span></span> <span data-ttu-id="3e2b5-273">Si necesita toomake una operación de escalado subsiguientes, como cambiar de tooStandard básico y, a continuación, cambiar tamaño de hello, debe esperar a que se ha completado la operación anterior de Hola o recibir un siguiente toohello de error similar.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-273">If you need toomake a subsequent scaling operation, such as changing from Basic tooStandard and then changing hello size, you must wait until hello previous operation is complete or you receive an error similar toohello following.</span></span>

    Set-AzureRmRedisCache : Conflict: hello resource '...' is not in a stable state, and is currently unable tooaccept hello update request.

## <a name="tooget-information-about-a-redis-cache"></a><span data-ttu-id="3e2b5-274">tooget información acerca de una caché de Redis</span><span class="sxs-lookup"><span data-stu-id="3e2b5-274">tooget information about a Redis cache</span></span>
<span data-ttu-id="3e2b5-275">Puede recuperar información sobre una memoria caché mediante hello [AzureRmRedisCache Get](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-275">You can retrieve information about a cache using hello [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet.</span></span>

<span data-ttu-id="3e2b5-276">toosee una lista de parámetros disponibles y sus descripciones para `Get-AzureRmRedisCache`, ejecute hello después del comando.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-276">toosee a list of available parameters and their descriptions for `Get-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCache -detailed

    NAME
        Get-AzureRmRedisCache

    SYNOPSIS
        Gets details about a single cache or all caches in hello specified resource group or all caches in hello current
        subscription.

    SYNTAX
        Get-AzureRmRedisCache [-Name <String>] [-ResourceGroupName <String>] [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCache cmdlet gets hello details about a cache or caches depending on input parameters. If both
        ResourceGroupName and Name parameters are provided then Get-AzureRmRedisCache will return details about the
        specific cache name provided.

        If only ResourceGroupName is provided than it will return details about all caches in hello specified resource group.

        If no parameters are given than it will return details about all caches hello current subscription.

    PARAMETERS
        -Name <String>
            hello name of hello cache. When this parameter is provided along with ResourceGroupName, Get-AzureRmRedisCache
            returns hello details for hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache or caches. If ResourceGroupName is provided with Name
            then Get-AzureRmRedisCache returns hello details of hello cache specified by Name. If only hello ResourceGroup
            parameter is provided, then details for all caches in hello resource group are returned.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="3e2b5-277">ejecutar tooreturn información acerca de todas las memorias caché en la suscripción actual de hello, `Get-AzureRmRedisCache` sin ningún parámetro.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-277">tooreturn information about all caches in hello current subscription, run `Get-AzureRmRedisCache` without any parameters.</span></span>

    Get-AzureRmRedisCache

<span data-ttu-id="3e2b5-278">tooreturn información acerca de todas las memorias caché en un grupo de recursos específico, ejecute `Get-AzureRmRedisCache` con hello `ResourceGroupName` parámetro.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-278">tooreturn information about all caches in a specific resource group, run `Get-AzureRmRedisCache` with hello `ResourceGroupName` parameter.</span></span>

    Get-AzureRmRedisCache -ResourceGroupName myGroup

<span data-ttu-id="3e2b5-279">tooreturn información acerca de una memoria caché específica, ejecute `Get-AzureRmRedisCache` con hello `Name` parámetro que contiene el nombre de Hola de caché de Hola y Hola `ResourceGroupName` parámetro con el grupo de recursos de Hola que contiene esa memoria caché.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-279">tooreturn information about a specific cache, run `Get-AzureRmRedisCache` with hello `Name` parameter containing hello name of hello cache, and hello `ResourceGroupName` parameter with hello resource group containing that cache.</span></span>

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

## <a name="tooretrieve-hello-access-keys-for-a-redis-cache"></a><span data-ttu-id="3e2b5-280">teclas de acceso de hello tooretrieve para una caché de Redis</span><span class="sxs-lookup"><span data-stu-id="3e2b5-280">tooretrieve hello access keys for a Redis cache</span></span>
<span data-ttu-id="3e2b5-281">tooretrieve hello las teclas de acceso de la memoria caché, puede usar hello [AzureRmRedisCacheKey Get](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-281">tooretrieve hello access keys for your cache, you can use hello [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet.</span></span>

<span data-ttu-id="3e2b5-282">toosee una lista de parámetros disponibles y sus descripciones para `Get-AzureRmRedisCacheKey`, ejecute hello después del comando.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-282">toosee a list of available parameters and their descriptions for `Get-AzureRmRedisCacheKey`, run hello following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCacheKey -detailed

    NAME
        Get-AzureRmRedisCacheKey

    SYNOPSIS
        Gets hello accesskeys for hello specified redis cache.


    SYNTAX
        Get-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCacheKey cmdlet gets hello access keys for hello specified cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="3e2b5-283">Hola tooretrieve claves de la memoria caché, llamada hello `Get-AzureRmRedisCacheKey` nombre hello del grupo de recursos que contiene la caché de Hola Hola a cmdlet y pase nombre hello de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-283">tooretrieve hello keys for your cache, call hello `Get-AzureRmRedisCacheKey` cmdlet and pass in hello name of your cache hello name of hello resource group that contains hello cache.</span></span>

    PS C:\> Get-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup

    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : ABhfB757JgjIgt785JgKH9865eifmekfnn649303JKL=

## <a name="tooregenerate-access-keys-for-your-redis-cache"></a><span data-ttu-id="3e2b5-284">teclas de acceso de tooregenerate para su caché de Redis</span><span class="sxs-lookup"><span data-stu-id="3e2b5-284">tooregenerate access keys for your Redis cache</span></span>
<span data-ttu-id="3e2b5-285">tooregenerate hello las teclas de acceso de la memoria caché, puede usar hello [AzureRmRedisCacheKey New](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-285">tooregenerate hello access keys for your cache, you can use hello [New-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet.</span></span>

<span data-ttu-id="3e2b5-286">toosee una lista de parámetros disponibles y sus descripciones para `New-AzureRmRedisCacheKey`, ejecute hello después del comando.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-286">toosee a list of available parameters and their descriptions for `New-AzureRmRedisCacheKey`, run hello following command.</span></span>

    PS C:\> Get-Help New-AzureRmRedisCacheKey -detailed

    NAME
        New-AzureRmRedisCacheKey

    SYNOPSIS
        Regenerates hello access key of a redis cache.

    SYNTAX
        New-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> -KeyType <String> [-Force] [<CommonParameters>]

    DESCRIPTION
        hello New-AzureRmRedisCacheKey cmdlet regenerate hello access key of a redis cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -KeyType <String>
            Specifies whether tooregenerate hello primary or secondary access key. Possible values are Primary or Secondary.

        -Force
            When hello Force parameter is provided, hello specified access key is regenerated without any confirmation prompts.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="3e2b5-287">clave primario o secundario de Hola de tooregenerate para la memoria caché, llamada hello `New-AzureRmRedisCacheKey` cmdlet y pase Hola nombre, grupo de recursos y especifique `Primary` o `Secondary` para hello `KeyType` parámetro.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-287">tooregenerate hello primary or secondary key for your cache, call hello `New-AzureRmRedisCacheKey` cmdlet and pass in hello name, resource group, and specify either `Primary` or `Secondary` for hello `KeyType` parameter.</span></span> <span data-ttu-id="3e2b5-288">En el siguiente ejemplo de Hola, se vuelve a generar clave de acceso secundaria de Hola para una caché.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-288">In hello following example, hello secondary access key for a cache is regenerated.</span></span>

    PS C:\> New-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup -KeyType Secondary

    Confirm
    Are you sure you want tooregenerate Secondary key for redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : c53hj3kh4jhHjPJk8l0jji785JgKH9865eifmekfnn6=

## <a name="toodelete-a-redis-cache"></a><span data-ttu-id="3e2b5-289">toodelete una caché de Redis</span><span class="sxs-lookup"><span data-stu-id="3e2b5-289">toodelete a Redis cache</span></span>
<span data-ttu-id="3e2b5-290">toodelete una caché en Redis, usar hello [Remove-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-290">toodelete a Redis cache, use hello [Remove-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet.</span></span>

<span data-ttu-id="3e2b5-291">toosee una lista de parámetros disponibles y sus descripciones para `Remove-AzureRmRedisCache`, ejecute hello después del comando.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-291">toosee a list of available parameters and their descriptions for `Remove-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Remove-AzureRmRedisCache -detailed

    NAME
        Remove-AzureRmRedisCache

    SYNOPSIS
        Remove redis cache if exists.

    SYNTAX
        Remove-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Force] [-PassThru] [<CommonParameters>

    DESCRIPTION
        hello Remove-AzureRmRedisCache cmdlet removes a redis cache if it exists.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooremove.

        -ResourceGroupName <String>
            Name of hello resource group of hello cache tooremove.

        -Force
            When hello Force parameter is provided, hello cache is removed without any confirmation prompts.

        -PassThru
            By default Remove-AzureRmRedisCache removes hello cache and does not return any value. If hello PassThru par
            is provided then Remove-AzureRmRedisCache returns a boolean value indicating hello success of hello operatio

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="3e2b5-292">En el siguiente ejemplo de Hola Hola caché denominado `myCache` se quita.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-292">In hello following example, hello cache named `myCache` is removed.</span></span>

    PS C:\> Remove-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Confirm
    Are you sure you want tooremove redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


## <a name="tooimport-a-redis-cache"></a><span data-ttu-id="3e2b5-293">tooimport una caché de Redis</span><span class="sxs-lookup"><span data-stu-id="3e2b5-293">tooimport a Redis cache</span></span>
<span data-ttu-id="3e2b5-294">Puede importar datos en una instancia de caché en Redis de Azure mediante hello `Import-AzureRmRedisCache` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-294">You can import data into an Azure Redis Cache instance using hello `Import-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3e2b5-295">Importación/Exportación solo está disponible para las memorias caché de [nivel premium](cache-premium-tier-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="3e2b5-295">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="3e2b5-296">Para más información e instrucciones sobre Importación/Exportación, consulte [Importación y exportación de datos en la Caché en Redis de Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="3e2b5-296">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="3e2b5-297">toosee una lista de parámetros disponibles y sus descripciones para `Import-AzureRmRedisCache`, ejecute hello después del comando.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-297">toosee a list of available parameters and their descriptions for `Import-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Import-AzureRmRedisCache -detailed

    NAME
        Import-AzureRmRedisCache

    SYNOPSIS
        Import data from blobs tooAzure Redis Cache.


    SYNTAX
        Import-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Files <String[]> [-Format <String>] [-Force]
        [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Import-AzureRmRedisCache cmdlet imports data from hello specified blobs into Azure Redis Cache.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Files <String[]>
            SAS urls of blobs whose content should be imported into hello cache.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -Force
            When hello Force parameter is provided, import will be performed without any confirmation prompts.

        -PassThru
            By default Import-AzureRmRedisCache imports data in cache and does not return any value. If hello PassThru
            parameter is provided then Import-AzureRmRedisCache returns a boolean value indicating hello success of the
            operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="3e2b5-298">Hello siguiente comando importa datos de blob de hello especificado por el identificador uri SAS de hello en caché en Redis de Azure.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-298">hello following command imports data from hello blob specified by hello SAS uri into Azure Redis Cache.</span></span>

    PS C:\>Import-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Files @("https://mystorageaccount.blob.core.windows.net/mycontainername/blobname?sv=2015-04-05&sr=b&sig=caIwutG2uDa0NZ8mjdNJdgOY8%2F8mhwRuGNdICU%2B0pI4%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwd") -Force

## <a name="tooexport-a-redis-cache"></a><span data-ttu-id="3e2b5-299">tooexport una caché de Redis</span><span class="sxs-lookup"><span data-stu-id="3e2b5-299">tooexport a Redis cache</span></span>
<span data-ttu-id="3e2b5-300">Puede exportar datos desde una instancia de caché en Redis de Azure mediante hello `Export-AzureRmRedisCache` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-300">You can export data from an Azure Redis Cache instance using hello `Export-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3e2b5-301">Importación/Exportación solo está disponible para las memorias caché de [nivel premium](cache-premium-tier-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="3e2b5-301">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="3e2b5-302">Para más información e instrucciones sobre Importación/Exportación, consulte [Importación y exportación de datos en la Caché en Redis de Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="3e2b5-302">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="3e2b5-303">toosee una lista de parámetros disponibles y sus descripciones para `Export-AzureRmRedisCache`, ejecute hello después del comando.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-303">toosee a list of available parameters and their descriptions for `Export-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Export-AzureRmRedisCache -detailed

    NAME
        Export-AzureRmRedisCache

    SYNOPSIS
        Exports data from Azure Redis Cache tooa specified container.


    SYNTAX
        Export-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Prefix <String> -Container <String> [-Format
        <String>] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Export-AzureRmRedisCache cmdlet exports data from Azure Redis Cache tooa specified container.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Prefix <String>
            Prefix toouse for blob names.

        -Container <String>
            SAS url of container where data should be exported.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -PassThru
            By default Export-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Export-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="3e2b5-304">Hello siguiente comando exporta los datos de una instancia de caché en Redis de Azure en contenedor Hola especificado por el uri de SAS de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-304">hello following command exports data from an Azure Redis Cache instance into hello container specified by hello SAS uri.</span></span>

        PS C:\>Export-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Prefix "blobprefix"
        -Container "https://mystorageaccount.blob.core.windows.net/mycontainer?sv=2015-04-05&sr=c&sig=HezZtBZ3DURmEGDduauE7
        pvETY4kqlPI8JCNa8ATmaw%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwdl"

## <a name="tooreboot-a-redis-cache"></a><span data-ttu-id="3e2b5-305">tooreboot una caché de Redis</span><span class="sxs-lookup"><span data-stu-id="3e2b5-305">tooreboot a Redis cache</span></span>
<span data-ttu-id="3e2b5-306">Puede reiniciar la instancia de caché en Redis de Azure con hello `Reset-AzureRmRedisCache` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-306">You can reboot your Azure Redis Cache instance using hello `Reset-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3e2b5-307">El reinicio solo está disponible para las memorias caché de [nivel premium](cache-premium-tier-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="3e2b5-307">Reboot is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="3e2b5-308">Para más información acerca de cómo reiniciar la caché, consulte [Administración de caché: reinicio](cache-administration.md#reboot).</span><span class="sxs-lookup"><span data-stu-id="3e2b5-308">For more information about rebooting your cache, see [Cache administration - reboot](cache-administration.md#reboot).</span></span>
> 
> 

<span data-ttu-id="3e2b5-309">toosee una lista de parámetros disponibles y sus descripciones para `Reset-AzureRmRedisCache`, ejecute hello después del comando.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-309">toosee a list of available parameters and their descriptions for `Reset-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Reset-AzureRmRedisCache -detailed

    NAME
        Reset-AzureRmRedisCache

    SYNOPSIS
        Reboot specified node(s) of an Azure Redis Cache instance.


    SYNTAX
        Reset-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -RebootType <String> [-ShardId <Integer>]
        [-Force] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Reset-AzureRmRedisCache cmdlet reboots hello specified node(s) of an Azure Redis Cache instance.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -RebootType <String>
            Which node tooreboot. Possible values are "PrimaryNode", "SecondaryNode", "AllNodes".

        -ShardId <Integer>
            Which shard tooreboot when rebooting a premium cache with clustering enabled.

        -Force
            When hello Force parameter is provided, reset will be performed without any confirmation prompts.

        -PassThru
            By default Reset-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Reset-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="3e2b5-310">Hello siguiente comando reinicia ambos nodos de hello especificado caché.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-310">hello following command reboots both nodes of hello specified cache.</span></span>

        PS C:\>Reset-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -RebootType "AllNodes"
        -Force


## <a name="next-steps"></a><span data-ttu-id="3e2b5-311">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3e2b5-311">Next steps</span></span>
<span data-ttu-id="3e2b5-312">toolearn más sobre el uso de Windows PowerShell con Azure, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3e2b5-312">toolearn more about using Windows PowerShell with Azure, see hello following resources:</span></span>

* [<span data-ttu-id="3e2b5-313">Documentación de cmdlet de caché en Redis de Azure en MSDN</span><span class="sxs-lookup"><span data-stu-id="3e2b5-313">Azure Redis Cache cmdlet documentation on MSDN</span></span>](https://msdn.microsoft.com/library/azure/mt634513.aspx)
* <span data-ttu-id="3e2b5-314">[Cmdlets de Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkID=394765): obtener información sobre toouse Hola cmdlets en el módulo de Azure Resource Manager Hola.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-314">[Azure Resource Manager Cmdlets](http://go.microsoft.com/fwlink/?LinkID=394765): Learn toouse hello cmdlets in hello Azure Resource Manager module.</span></span>
* <span data-ttu-id="3e2b5-315">[Uso del recurso agrupa toomanage los recursos de Azure](../azure-resource-manager/resource-group-template-deploy-portal.md): Obtenga información acerca de cómo toocreate y administrar grupos de recursos de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-315">[Using Resource groups toomanage your Azure resources](../azure-resource-manager/resource-group-template-deploy-portal.md): Learn how toocreate and manage resource groups in hello Azure portal.</span></span>
* <span data-ttu-id="3e2b5-316">[Blog de Azure](http://blogs.msdn.com/windowsazure): obtenga información acerca de las nuevas características de Azure.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-316">[Azure blog](http://blogs.msdn.com/windowsazure): Learn about new features in Azure.</span></span>
* <span data-ttu-id="3e2b5-317">[Blog de Windows PowerShell](http://blogs.msdn.com/powershell): obtenga información acerca de las nuevas características de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-317">[Windows PowerShell blog](http://blogs.msdn.com/powershell): Learn about new features in Windows PowerShell.</span></span>
* <span data-ttu-id="3e2b5-318">[Blog Blog](http://blogs.technet.com/b/heyscriptingguy/): obtener reales sugerencias y trucos de hello Comunidad de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3e2b5-318">["Hey, Scripting Guy!" Blog](http://blogs.technet.com/b/heyscriptingguy/): Get real-world tips and tricks from hello Windows PowerShell community.</span></span>

