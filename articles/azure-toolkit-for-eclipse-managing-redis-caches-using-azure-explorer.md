---
title: "aaaManaging memorias caché Redis utilizando Hola Explorer de Azure para Eclipse | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomanage su redis de Azure almacena en memoria caché mediante el uso de hello Azure Explorer para Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/14/2017
ms.author: robmcm
ms.openlocfilehash: aa0c38862bda7919a3fc6c53c2fdaf555dd64bff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-redis-caches-using-hello-azure-explorer-for-eclipse"></a><span data-ttu-id="c40ce-103">Administración de cachés de Redis mediante hello Azure Explorer para Eclipse</span><span class="sxs-lookup"><span data-stu-id="c40ce-103">Managing Redis Caches using hello Azure Explorer for Eclipse</span></span>

<span data-ttu-id="c40ce-104">Hola Explorador de Azure, que forma parte de hello Azure Toolkit for Eclipse, proporciona a los desarrolladores de Java con una solución fácil de usar para administrar redis memorias caché en su cuenta de Azure desde dentro de Hola Eclipse IDE.</span><span class="sxs-lookup"><span data-stu-id="c40ce-104">hello Azure Explorer, which is part of hello Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing redis caches in their Azure account from inside hello Eclipse IDE.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-eclipse"></a><span data-ttu-id="c40ce-105">Creación de Redis Cache mediante una Eclipse</span><span class="sxs-lookup"><span data-stu-id="c40ce-105">Create a Redis Cache by using Eclipse</span></span>

<span data-ttu-id="c40ce-106">Hola pasos le guiará por hello pasos toocreate una caché en redis mediante Hola Explorador de Azure.</span><span class="sxs-lookup"><span data-stu-id="c40ce-106">hello following steps walk you through hello steps toocreate a redis cache using hello Azure Explorer.</span></span>

1. <span data-ttu-id="c40ce-107">Inicie sesión en tooyour cuenta de Azure siguiendo los pasos de Hola Hola [inicio de sesión en las instrucciones de hello Azure Toolkit for Eclipse] artículo.</span><span class="sxs-lookup"><span data-stu-id="c40ce-107">Sign in tooyour Azure account using hello steps in hello [Sign In Instructions for hello Azure Toolkit for Eclipse] article.</span></span>

1. <span data-ttu-id="c40ce-108">Hola **explorador Azure** ventana de herramientas, expanda hello **Azure** nodo, haga clic en **memorias caché Redis**y, a continuación, haga clic en **crear caché en Redis**.</span><span class="sxs-lookup"><span data-stu-id="c40ce-108">In hello **Azure Explorer** tool window, expand hello **Azure** node, right-click **Redis Caches**, and then click **Create Redis Cache**.</span></span>

   ![Creación de un menú de Redis Cache][CR01]

1. <span data-ttu-id="c40ce-110">Cuando Hola **nueva caché en Redis** aparece el cuadro de diálogo, especifique Hola siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="c40ce-110">When hello **New Redis Cache** dialog box appears, specify hello following options:</span></span>

   ![Creación del cuadro de diálogo Nueva caché en Redis][CR02]

   <span data-ttu-id="c40ce-112">a.</span><span class="sxs-lookup"><span data-stu-id="c40ce-112">a.</span></span> <span data-ttu-id="c40ce-113">**Nombre DNS**: especifica el subdominio DNS de Hola para caché en redis nueva hello, que se antepone demasiado ". redis.cache.windows .net"; por ejemplo: *wingtiptoys.redis.cache.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="c40ce-113">**DNS Name**: Specifies hello DNS subdomain for hello new redis cache, which is prepended too".redis.cache.windows.net"; for example: *wingtiptoys.redis.cache.windows.net*.</span></span>

   <span data-ttu-id="c40ce-114">b.</span><span class="sxs-lookup"><span data-stu-id="c40ce-114">b.</span></span> <span data-ttu-id="c40ce-115">**Suscripción**: especifica Hola desea toouse para caché en redis Hola nueva suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="c40ce-115">**Subscription**: Specifies hello Azure subscription you want toouse for hello new redis cache.</span></span>

   <span data-ttu-id="c40ce-116">c.</span><span class="sxs-lookup"><span data-stu-id="c40ce-116">c.</span></span> <span data-ttu-id="c40ce-117">**Grupo de recursos**: especifica el grupo de recursos de hello para la caché de redis; debe toochoose de hello siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="c40ce-117">**Resource Group**: Specifies hello resource group for your redis cache; you need toochoose one of hello following options:</span></span>
      * <span data-ttu-id="c40ce-118">**Crear nuevo**: Especifica que desea toocreate un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c40ce-118">**Create New**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="c40ce-119">**Usar existente**: especifica que se va a elegir de una lista de grupos de recursos asociados a la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="c40ce-119">**Use Existing**: Specifies that you will choose from a list of resource groups associated with your Azure account.</span></span>

   <span data-ttu-id="c40ce-120">d.</span><span class="sxs-lookup"><span data-stu-id="c40ce-120">d.</span></span> <span data-ttu-id="c40ce-121">**Ubicación**: especifica la ubicación de Hola donde se crea la memoria caché de redis; por ejemplo, *West US*.</span><span class="sxs-lookup"><span data-stu-id="c40ce-121">**Location**: Specifies hello location where your redis cache is created; for example, *West US*.</span></span>

   <span data-ttu-id="c40ce-122">e.</span><span class="sxs-lookup"><span data-stu-id="c40ce-122">e.</span></span> <span data-ttu-id="c40ce-123">**Nivel de precios**: especifica qué nivel de precios que se usa la memoria caché de redis; esta configuración determina el número de Hola de conexiones de cliente.</span><span class="sxs-lookup"><span data-stu-id="c40ce-123">**Pricing Tier**: Specifies which pricing tier your redis cache uses; this setting determines hello number of client connections.</span></span> <span data-ttu-id="c40ce-124">(Para más información, consulte [Precios de Redis Cache]).</span><span class="sxs-lookup"><span data-stu-id="c40ce-124">(For more information, see [Redis Cache Pricing].)</span></span>

   <span data-ttu-id="c40ce-125">f.</span><span class="sxs-lookup"><span data-stu-id="c40ce-125">f.</span></span> <span data-ttu-id="c40ce-126">**Puerto sin SSL**: especifica si Redis Cache permite las conexiones sin SSL. De forma predeterminada, se permiten solo las conexiones SSL.</span><span class="sxs-lookup"><span data-stu-id="c40ce-126">**Non-SSL port**: Specifies whether your redis cache allows non-SSL connections; by default, only SSL connections are allowed.</span></span>

1. <span data-ttu-id="c40ce-127">Cuando haya especificado toda la configuración de Redis Cache, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c40ce-127">When you have specified all your redis cache settings, click **OK**.</span></span>

<span data-ttu-id="c40ce-128">Una vez creada la memoria caché de redis, se mostrará en hello Explorador de Azure.</span><span class="sxs-lookup"><span data-stu-id="c40ce-128">After your redis cache has been created, it will be displayed in hello Azure Explorer.</span></span>

   ![Redis Cache en Azure Explorer][CR03]

> [!NOTE]
>
> <span data-ttu-id="c40ce-130">Para obtener más información acerca de cómo configurar Azure redis configuración de la caché, vea [cómo tooconfigure Azure Redis Cache].</span><span class="sxs-lookup"><span data-stu-id="c40ce-130">For more information about configuring your Azure redis cache settings, see [How tooconfigure Azure Redis Cache].</span></span>
>

## <a name="display-hello-properties-for-your-redis-cache-in-eclipse"></a><span data-ttu-id="c40ce-131">Mostrar propiedades de hello de la caché en Redis en Eclipse</span><span class="sxs-lookup"><span data-stu-id="c40ce-131">Display hello properties for your Redis Cache in Eclipse</span></span>

1. <span data-ttu-id="c40ce-132">Hola Explorador de Azure, haga clic en la memoria caché de redis y haga clic en **mostrar propiedades**.</span><span class="sxs-lookup"><span data-stu-id="c40ce-132">In hello Azure Explorer, right-click your redis cache and click **Show properties**.</span></span>

   ![Azure explorador menú toodisplay propiedades de contexto de una caché de redis][SP01]

1. <span data-ttu-id="c40ce-134">Hola explorador Azure muestra las propiedades de hello para la caché en redis.</span><span class="sxs-lookup"><span data-stu-id="c40ce-134">hello Azure Explorer displays hello properties for your redis cache.</span></span>

   ![Propiedades de caché en Redis][SP02]

## <a name="delete-your-redis-cache-by-using-eclipse"></a><span data-ttu-id="c40ce-136">Eliminación de Redis Cache con Eclipse</span><span class="sxs-lookup"><span data-stu-id="c40ce-136">Delete your Redis Cache by using Eclipse</span></span>

1. <span data-ttu-id="c40ce-137">Hola Explorador de Azure, haga clic en la memoria caché de redis y haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="c40ce-137">In hello Azure Explorer, right-click your redis cache and click **Delete**.</span></span>

   ![Toodelete de menú contextual de Azure explorador una caché de redis][DE01]

1. <span data-ttu-id="c40ce-139">Haga clic en **Aceptar** cuando se le pida toodelete su caché de redis.</span><span class="sxs-lookup"><span data-stu-id="c40ce-139">Click **OK** when prompted toodelete your redis cache.</span></span>

   ![Eliminar una instancia de Redis Cache][DE02]

## <a name="next-steps"></a><span data-ttu-id="c40ce-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c40ce-141">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="c40ce-142">Para obtener más información acerca de las cachés de redis de Azure, opciones de configuración y precios, vea Hola siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="c40ce-142">For more information about Azure redis caches, configuration settings and pricing, see hello following links:</span></span>

* <span data-ttu-id="c40ce-143">[Azure Redis Cache]</span><span class="sxs-lookup"><span data-stu-id="c40ce-143">[Azure Redis Cache]</span></span>
* <span data-ttu-id="c40ce-144">[Documentación de Redis Cache]</span><span class="sxs-lookup"><span data-stu-id="c40ce-144">[Redis Cache Documentation]</span></span>
* <span data-ttu-id="c40ce-145">[Precios de Redis Cache]</span><span class="sxs-lookup"><span data-stu-id="c40ce-145">[Redis Cache Pricing]</span></span>
* <span data-ttu-id="c40ce-146">[cómo tooconfigure Azure Redis Cache]</span><span class="sxs-lookup"><span data-stu-id="c40ce-146">[How tooconfigure Azure Redis Cache]</span></span>

<!-- URL List -->

[Precios de Redis Cache]: https://azure.microsoft.com/pricing/details/cache/
[Azure Redis Cache]: https://azure.microsoft.com/services/cache/
[Documentación de Redis Cache]: ./redis-cache/index.md
[cómo tooconfigure Azure Redis Cache]: ./redis-cache/cache-configure.md
[inicio de sesión en las instrucciones de hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md

<!-- IMG List -->

[CR01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE02.png
