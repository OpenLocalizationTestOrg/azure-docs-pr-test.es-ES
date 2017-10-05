---
title: "Creación de un servidor de Analysis Services en Azure | Microsoft Docs"
description: Aprenda a crear una instancia de servidor de Analysis Services en Azure.
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
ms.openlocfilehash: 95b367e7cd74405088190c1fe19cf92990759d90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a><span data-ttu-id="f054d-103">Creación de un servidor de Azure Analysis Services en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f054d-103">Create an Azure Analysis Services server in Azure portal</span></span>
<span data-ttu-id="f054d-104">Este artículo lo guiará por la creación de un recurso de servidor de Analysis Services en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="f054d-104">This article walks you through creating an Analysis Services server resource in your Azure subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f054d-105">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="f054d-105">Before you begin</span></span>
<span data-ttu-id="f054d-106">Para completar este inicio rápido necesita instalar:</span><span class="sxs-lookup"><span data-stu-id="f054d-106">To complete this quickstart, you need:</span></span>

* <span data-ttu-id="f054d-107">**Suscripción de Azure**: visite [Evaluación gratuita de Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) para crear una cuenta.</span><span class="sxs-lookup"><span data-stu-id="f054d-107">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) to create an account.</span></span>
* <span data-ttu-id="f054d-108">**Azure Active Directory**: la suscripción debe estar asociada a un inquilino de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f054d-108">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant.</span></span> <span data-ttu-id="f054d-109">Además, debe estar conectado en Azure con una cuenta en ese Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f054d-109">And, you need to be signed in to Azure with an account in that Azure Active Directory.</span></span> <span data-ttu-id="f054d-110">No se admiten cuentas de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f054d-110">Microsoft accounts are not supported.</span></span> <span data-ttu-id="f054d-111">Para más información, consulte [Permisos de usuario y autenticación](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="f054d-111">To learn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>
* <span data-ttu-id="f054d-112">**Grupo de recursos**: use un grupo de recursos que ya tenga o [cree uno nuevo](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f054d-112">**Resource group**: Use a resource group you already have or [create a new one](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f054d-113">La creación de un servidor puede dar lugar a un nuevo servicio facturable.</span><span class="sxs-lookup"><span data-stu-id="f054d-113">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="f054d-114">Para obtener más información, consulte los [precios de Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="f054d-114">To learn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
> 
> 

## <a name="to-create-a-server-in-azure-portal"></a><span data-ttu-id="f054d-115">Creación de un servidor de Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f054d-115">To create a server in Azure portal</span></span>
1. <span data-ttu-id="f054d-116">Inicie sesión en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f054d-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="f054d-117">Haga clic en **+ Nuevo** > **Datos y análisis** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="f054d-117">Click **+ New** > **Data + analytics** > **Analysis Services**.</span></span>
3. <span data-ttu-id="f054d-118">En la hoja de **Analysis Services**, rellene los campos obligatorios y, a continuación, presione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="f054d-118">In the **Analysis Services** blade, fill in the required fields, and then press **Create**.</span></span>
   
    ![Crear un servidor](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * <span data-ttu-id="f054d-120">**Nombre del servidor**: escriba un nombre único que se pueda utilizar para hacer referencia al servidor.</span><span class="sxs-lookup"><span data-stu-id="f054d-120">**Server name**: Type a unique name used to reference the server.</span></span>
   * <span data-ttu-id="f054d-121">**Suscripción**: seleccione la suscripción al que este servidor se puede facturar.</span><span class="sxs-lookup"><span data-stu-id="f054d-121">**Subscription**: Select the subscription this server bills to.</span></span>
   * <span data-ttu-id="f054d-122">**Grupos de recursos**: son contenedores diseñados para ayudarlo a administrar una colección de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f054d-122">**Resource group**: These containers are designed to help you manage a collection of Azure resources.</span></span> <span data-ttu-id="f054d-123">Para más información, consulte [grupos de recursos](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f054d-123">To learn more, see [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="f054d-124">**Ubicación**: esta ubicación del centro de datos de Azure hospeda el servidor.</span><span class="sxs-lookup"><span data-stu-id="f054d-124">**Location**: This Azure datacenter location hosts the server.</span></span> <span data-ttu-id="f054d-125">Elija una ubicación más cercana a su base de usuarios más grande.</span><span class="sxs-lookup"><span data-stu-id="f054d-125">Choose a location nearest your largest user base.</span></span>
   * <span data-ttu-id="f054d-126">**Plan de tarifa**: seleccione un plan de tarifa.</span><span class="sxs-lookup"><span data-stu-id="f054d-126">**Pricing tier**: Select a pricing tier.</span></span> <span data-ttu-id="f054d-127">Se admiten modelos tabulares de hasta 400 GB.</span><span class="sxs-lookup"><span data-stu-id="f054d-127">Tabular models up to 400 GB are supported.</span></span> <span data-ttu-id="f054d-128">Para obtener más información, consulte los [precios de Azure Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="f054d-128">To learn more, see [Azure Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
4. <span data-ttu-id="f054d-129">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="f054d-129">Click **Create**.</span></span>

<span data-ttu-id="f054d-130">La creación normalmente tarda menos de un minuto, a menudo solo unos pocos segundos.</span><span class="sxs-lookup"><span data-stu-id="f054d-130">Create usually takes under a minute; often just a few seconds.</span></span> <span data-ttu-id="f054d-131">Si seleccionó **Add to Portal** (Agregar al portal), desplácese hasta el portal para ver el nuevo servidor.</span><span class="sxs-lookup"><span data-stu-id="f054d-131">If you selected **Add to Portal**, navigate to your portal to see your new server.</span></span> <span data-ttu-id="f054d-132">O bien, vaya a **Más servicios** > **Analysis Services** para ver si el servidor está listo.</span><span class="sxs-lookup"><span data-stu-id="f054d-132">Or, navigate to **More services** > **Analysis Services** to see if your server is ready.</span></span>

 ![Panel](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a><span data-ttu-id="f054d-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f054d-134">Next steps</span></span>
<span data-ttu-id="f054d-135">Una vez creado el servidor, puede [implementar un modelo](analysis-services-deploy.md) en él mediante SSDT o con SSMS.</span><span class="sxs-lookup"><span data-stu-id="f054d-135">Once you've created your server, you can [deploy a model](analysis-services-deploy.md) to it by using SSDT or with SSMS.</span></span>

<span data-ttu-id="f054d-136">Si un modelo que se implemente en el servidor se conecta a orígenes de datos locales, deberá instalar una [puerta de enlace de datos local](analysis-services-gateway.md) en un equipo de la red.</span><span class="sxs-lookup"><span data-stu-id="f054d-136">If a model you deploy to your server connects to on-premises data sources, you need to install an [On-premises data gateway](analysis-services-gateway.md) on a computer in your network.</span></span>

