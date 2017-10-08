---
title: aaaCreate un servidor de Analysis Services en Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un servidor de Analysis Services de instancia de Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 7f560216-8a9a-4d06-852e-48cf24deab19
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 3668f659039f79f3dd71498d1066e8682bf33228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a><span data-ttu-id="ffab3-103">Creación de un servidor de Azure Analysis Services en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ffab3-103">Create an Azure Analysis Services server in Azure portal</span></span>
<span data-ttu-id="ffab3-104">Este artículo lo guiará por la creación de un recurso de servidor de Analysis Services en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="ffab3-104">This article walks you through creating an Analysis Services server resource in your Azure subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ffab3-105">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="ffab3-105">Before you begin</span></span>
<span data-ttu-id="ffab3-106">toocomplete este tutorial rápido, necesita:</span><span class="sxs-lookup"><span data-stu-id="ffab3-106">toocomplete this quickstart, you need:</span></span>

* <span data-ttu-id="ffab3-107">**Suscripción de Azure**: visite [evaluación gratuita de Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate una cuenta.</span><span class="sxs-lookup"><span data-stu-id="ffab3-107">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate an account.</span></span>
* <span data-ttu-id="ffab3-108">**Azure Active Directory**: la suscripción debe estar asociada a un inquilino de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ffab3-108">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant.</span></span> <span data-ttu-id="ffab3-109">Y necesita toobe iniciado sesión tooAzure con una cuenta en que Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ffab3-109">And, you need toobe signed in tooAzure with an account in that Azure Active Directory.</span></span> <span data-ttu-id="ffab3-110">No se admiten cuentas de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ffab3-110">Microsoft accounts are not supported.</span></span> <span data-ttu-id="ffab3-111">más información, consulte toolearn [permisos de usuario y la autenticación](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="ffab3-111">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>
* <span data-ttu-id="ffab3-112">**Grupo de recursos**: use un grupo de recursos que ya tenga o [cree uno nuevo](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ffab3-112">**Resource group**: Use a resource group you already have or [create a new one](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ffab3-113">La creación de un servidor puede dar lugar a un nuevo servicio facturable.</span><span class="sxs-lookup"><span data-stu-id="ffab3-113">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="ffab3-114">más información, consulte toolearn [precios de Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="ffab3-114">toolearn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
> 
> 

## <a name="toocreate-a-server-in-azure-portal"></a><span data-ttu-id="ffab3-115">toocreate un servidor en el portal de Azure</span><span class="sxs-lookup"><span data-stu-id="ffab3-115">toocreate a server in Azure portal</span></span>
1. <span data-ttu-id="ffab3-116">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ffab3-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="ffab3-117">Haga clic en **+ Nuevo** > **Datos y análisis** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="ffab3-117">Click **+ New** > **Data + analytics** > **Analysis Services**.</span></span>
3. <span data-ttu-id="ffab3-118">Hola **Analysis Services** hoja, rellene los campos de hello necesario y, a continuación, presione **crear**.</span><span class="sxs-lookup"><span data-stu-id="ffab3-118">In hello **Analysis Services** blade, fill in hello required fields, and then press **Create**.</span></span>
   
    ![Crear un servidor](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * <span data-ttu-id="ffab3-120">**Nombre del servidor**: escriba un servidor de nombre único usado tooreference Hola.</span><span class="sxs-lookup"><span data-stu-id="ffab3-120">**Server name**: Type a unique name used tooreference hello server.</span></span>
   * <span data-ttu-id="ffab3-121">**Suscripción**: seleccione suscripción Hola facturas de este servidor a.</span><span class="sxs-lookup"><span data-stu-id="ffab3-121">**Subscription**: Select hello subscription this server bills to.</span></span>
   * <span data-ttu-id="ffab3-122">**Grupo de recursos**: estos contenedores están diseñado toohelp administrar una colección de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="ffab3-122">**Resource group**: These containers are designed toohelp you manage a collection of Azure resources.</span></span> <span data-ttu-id="ffab3-123">más información, consulte toolearn [grupos de recursos](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ffab3-123">toolearn more, see [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="ffab3-124">**Ubicación**: Hola de hosts de ubicación de centro de datos de Azure de este servidor.</span><span class="sxs-lookup"><span data-stu-id="ffab3-124">**Location**: This Azure datacenter location hosts hello server.</span></span> <span data-ttu-id="ffab3-125">Elija una ubicación más cercana a su base de usuarios más grande.</span><span class="sxs-lookup"><span data-stu-id="ffab3-125">Choose a location nearest your largest user base.</span></span>
   * <span data-ttu-id="ffab3-126">**Plan de tarifa**: seleccione un plan de tarifa.</span><span class="sxs-lookup"><span data-stu-id="ffab3-126">**Pricing tier**: Select a pricing tier.</span></span> <span data-ttu-id="ffab3-127">Se admiten los modelos tabulares backup too400 GB.</span><span class="sxs-lookup"><span data-stu-id="ffab3-127">Tabular models up too400 GB are supported.</span></span> <span data-ttu-id="ffab3-128">más información, consulte toolearn [precios de Azure Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="ffab3-128">toolearn more, see [Azure Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
4. <span data-ttu-id="ffab3-129">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ffab3-129">Click **Create**.</span></span>

<span data-ttu-id="ffab3-130">La creación normalmente tarda menos de un minuto, a menudo solo unos pocos segundos.</span><span class="sxs-lookup"><span data-stu-id="ffab3-130">Create usually takes under a minute; often just a few seconds.</span></span> <span data-ttu-id="ffab3-131">Si seleccionó **agregar tooPortal**, vaya a tooyour portal toosee el nuevo servidor.</span><span class="sxs-lookup"><span data-stu-id="ffab3-131">If you selected **Add tooPortal**, navigate tooyour portal toosee your new server.</span></span> <span data-ttu-id="ffab3-132">O bien, navegue demasiado**más servicios** > **Analysis Services** toosee si el servidor está listo.</span><span class="sxs-lookup"><span data-stu-id="ffab3-132">Or, navigate too**More services** > **Analysis Services** toosee if your server is ready.</span></span>

 ![Panel](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a><span data-ttu-id="ffab3-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ffab3-134">Next steps</span></span>
<span data-ttu-id="ffab3-135">Una vez que haya creado el servidor, puede [implementar un modelo](analysis-services-deploy.md) tooit mediante SSDT o con SSMS.</span><span class="sxs-lookup"><span data-stu-id="ffab3-135">Once you've created your server, you can [deploy a model](analysis-services-deploy.md) tooit by using SSDT or with SSMS.</span></span>

<span data-ttu-id="ffab3-136">Si un modelo se implementa tooyour servidor conecta a orígenes de datos locales de tooon, deberá tooinstall un [puerta de enlace de datos local](analysis-services-gateway.md) en un equipo de la red.</span><span class="sxs-lookup"><span data-stu-id="ffab3-136">If a model you deploy tooyour server connects tooon-premises data sources, you need tooinstall an [On-premises data gateway](analysis-services-gateway.md) on a computer in your network.</span></span>

