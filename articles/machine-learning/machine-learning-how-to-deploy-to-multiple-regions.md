---
title: aaaHow toodeploy un servicio Web regiones toomultiple | Documentos de Microsoft
description: Pasos toodeploy (copiar) un regiones de tooother nuevo servicio Web.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: cgronlun
ms.assetid: 36c60411-f2db-4ee2-9b66-b1f1d77a8f44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 21fcdb96f118c60ed98b60b1b2df833766c7c8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-web-service-toomultiple-regions"></a><span data-ttu-id="9ba1b-103">¿Cómo toodeploy un servicio Web toomultiple regiones</span><span class="sxs-lookup"><span data-stu-id="9ba1b-103">How toodeploy a Web Service toomultiple regions</span></span>
<span data-ttu-id="9ba1b-104">Hola nuevos servicios de Web de Azure le permiten tooeasily implementar un regiones de toomultiple del servicio web sin necesidad de varias suscripciones o áreas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="9ba1b-104">hello New Azure Web Services allow you tooeasily deploy a web service toomultiple regions without needing multiple subscriptions or workspaces.</span></span> 

<span data-ttu-id="9ba1b-105">El precio es específica, por tanto, debe definir un plan de facturación para cada región en el que va a implementar el servicio web de hello de la región.</span><span class="sxs-lookup"><span data-stu-id="9ba1b-105">Pricing is region specific, therefore you must define a billing plan for each region in which you will deploy hello web service.</span></span>

## <a name="toocreate-a-plan-in-another-region"></a><span data-ttu-id="9ba1b-106">toocreate un plan en otra región</span><span class="sxs-lookup"><span data-stu-id="9ba1b-106">toocreate a plan in another region</span></span>
1. <span data-ttu-id="9ba1b-107">Inicie sesión en el [portal de servicios web de Aprendizaje automático de Microsoft Azure](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="9ba1b-107">Sign into [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/).</span></span>
2. <span data-ttu-id="9ba1b-108">Haga clic en hello **planes** opción de menú.</span><span class="sxs-lookup"><span data-stu-id="9ba1b-108">Click hello **Plans** menu option.</span></span>
3. <span data-ttu-id="9ba1b-109">En los planes de Hola a través de la página de vista, haga clic en **nuevo**.</span><span class="sxs-lookup"><span data-stu-id="9ba1b-109">On hello Plans over view page, click **New**.</span></span>
4. <span data-ttu-id="9ba1b-110">De hello **suscripción** lista desplegable, suscripción Hola seleccione en qué Hola va a residir nuevo plan.</span><span class="sxs-lookup"><span data-stu-id="9ba1b-110">From hello **Subscription** dropdown, select hello subscription in which hello new plan will reside.</span></span>
5. <span data-ttu-id="9ba1b-111">De hello **región** lista desplegable, seleccione una región para el nuevo plan de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ba1b-111">From hello **Region** dropdown, select a region for hello new plan.</span></span> <span data-ttu-id="9ba1b-112">Hola opciones del Plan para la región seleccionada Hola se mostrará en hello **opciones del Plan de** sección de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ba1b-112">hello Plan Options for hello selected region will display in hello **Plan Options** section of hello page.</span></span>
6. <span data-ttu-id="9ba1b-113">De hello **grupo de recursos** lista desplegable, seleccione un recurso de grupo para el plan de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ba1b-113">From hello **Resource Group** dropdown, select a resource group for hello plan.</span></span> <span data-ttu-id="9ba1b-114">Para más información sobre los grupos de recursos, consulte [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9ba1b-114">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
7. <span data-ttu-id="9ba1b-115">En **el nombre del Plan** nombre de plan de Hola Hola de tipo.</span><span class="sxs-lookup"><span data-stu-id="9ba1b-115">In **Plan Name** type hello name of hello plan.</span></span>
8. <span data-ttu-id="9ba1b-116">En **opciones del Plan de**, haga clic en el nivel de facturación de Hola de nuevo plan de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ba1b-116">Under **Plan Options**, click hello billing level for hello new plan.</span></span>
9. <span data-ttu-id="9ba1b-117">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9ba1b-117">Click **Create**.</span></span>

## <a name="deploying-hello-web-service-tooanother-region"></a><span data-ttu-id="9ba1b-118">Implementar hello web servicio tooanother área</span><span class="sxs-lookup"><span data-stu-id="9ba1b-118">Deploying hello web service tooanother region</span></span>
1. <span data-ttu-id="9ba1b-119">Haga clic en hello **servicios Web** opción de menú.</span><span class="sxs-lookup"><span data-stu-id="9ba1b-119">Click hello **Web Services** menu option.</span></span>
2. <span data-ttu-id="9ba1b-120">Seleccione Hola servicio Web que se va a implementar tooa nueva región.</span><span class="sxs-lookup"><span data-stu-id="9ba1b-120">Select hello Web Service you are deploying tooa new region.</span></span>
3. <span data-ttu-id="9ba1b-121">Haga clic en **Copiar**.</span><span class="sxs-lookup"><span data-stu-id="9ba1b-121">Click **Copy**.</span></span>
4. <span data-ttu-id="9ba1b-122">En **nombre del servicio Web**, escriba un nombre nuevo para el servicio web de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ba1b-122">In **Web Service Name**, type a new name for hello web service.</span></span>
5. <span data-ttu-id="9ba1b-123">En **descripción de servicio Web**, escriba una descripción para el servicio web de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ba1b-123">In **Web service description**, type a description for hello web service.</span></span>
6. <span data-ttu-id="9ba1b-124">De hello **suscripción** lista desplegable, suscripción Hola seleccione en qué Hola va a residir nuevo servicio web.</span><span class="sxs-lookup"><span data-stu-id="9ba1b-124">From hello **Subscription** dropdown, select hello subscription in which hello new web service will reside.</span></span>
7. <span data-ttu-id="9ba1b-125">De hello **grupo de recursos** lista desplegable, seleccione un recurso de grupo para el servicio web de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ba1b-125">From hello **Resource Group** dropdown, select a resource group for hello web service.</span></span> <span data-ttu-id="9ba1b-126">Para más información sobre los grupos de recursos, consulte [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9ba1b-126">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="9ba1b-127">De hello **región** lista desplegable región seleccione hello en el servicio web que toodeploy Hola.</span><span class="sxs-lookup"><span data-stu-id="9ba1b-127">From hello **Region** dropdown, select hello region in which toodeploy hello web service.</span></span>
9. <span data-ttu-id="9ba1b-128">De hello **cuenta de almacenamiento** lista desplegable, seleccione una cuenta de almacenamiento en qué hello toostore servicio web.</span><span class="sxs-lookup"><span data-stu-id="9ba1b-128">From hello **Storage account** dropdown, select a storage account in which toostore hello web service.</span></span>
10. <span data-ttu-id="9ba1b-129">De hello **Plan de precios** lista desplegable, seleccione un plan en la región de Hola que seleccionó en el paso 8.</span><span class="sxs-lookup"><span data-stu-id="9ba1b-129">From hello **Price Plan** dropdown, select a plan in hello region you selected in step 8.</span></span>
11. <span data-ttu-id="9ba1b-130">Haga clic en **Copiar**.</span><span class="sxs-lookup"><span data-stu-id="9ba1b-130">Click **Copy**.</span></span>

