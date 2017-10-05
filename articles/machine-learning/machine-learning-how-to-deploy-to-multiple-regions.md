---
title: Procedimiento para implementar un servicio web en varias regiones | Microsoft Docs
description: Pasos para implementar (copiar) un servicio web nuevo en otras regiones
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
ms.openlocfilehash: 3895537bbca72e687838ff5013c291dfee3be707
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-web-service-to-multiple-regions"></a><span data-ttu-id="1e2ee-103">Procedimiento para implementar un servicio web en varias regiones</span><span class="sxs-lookup"><span data-stu-id="1e2ee-103">How to deploy a Web Service to multiple regions</span></span>
<span data-ttu-id="1e2ee-104">Gracias a los servicios web nuevos de Azure, se puede implementar fácilmente un servicio web en varias regiones sin necesidad de disponer de varias suscripciones o áreas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="1e2ee-104">The New Azure Web Services allow you to easily deploy a web service to multiple regions without needing multiple subscriptions or workspaces.</span></span> 

<span data-ttu-id="1e2ee-105">Los precios dependen de la región, por lo tanto, debe definir un plan de facturación para cada región en la que implementará el servicio web.</span><span class="sxs-lookup"><span data-stu-id="1e2ee-105">Pricing is region specific, therefore you must define a billing plan for each region in which you will deploy the web service.</span></span>

## <a name="to-create-a-plan-in-another-region"></a><span data-ttu-id="1e2ee-106">Pasos para crear un plan en otra región</span><span class="sxs-lookup"><span data-stu-id="1e2ee-106">To create a plan in another region</span></span>
1. <span data-ttu-id="1e2ee-107">Inicie sesión en el [portal de servicios web de Aprendizaje automático de Microsoft Azure](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="1e2ee-107">Sign into [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/).</span></span>
2. <span data-ttu-id="1e2ee-108">Haga clic en la opción de menú **Planes** .</span><span class="sxs-lookup"><span data-stu-id="1e2ee-108">Click the **Plans** menu option.</span></span>
3. <span data-ttu-id="1e2ee-109">En la página de información general de Planes, haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="1e2ee-109">On the Plans over view page, click **New**.</span></span>
4. <span data-ttu-id="1e2ee-110">En el menú desplegable **Suscripción** , seleccione la suscripción en que residirá el nuevo plan.</span><span class="sxs-lookup"><span data-stu-id="1e2ee-110">From the **Subscription** dropdown, select the subscription in which the new plan will reside.</span></span>
5. <span data-ttu-id="1e2ee-111">En el menú desplegable **Región** , seleccione una región para el nuevo plan.</span><span class="sxs-lookup"><span data-stu-id="1e2ee-111">From the **Region** dropdown, select a region for the new plan.</span></span> <span data-ttu-id="1e2ee-112">Las opciones de planes de la región seleccionada se mostrarán en la sección de la página **Plan Options** (Opciones de planes).</span><span class="sxs-lookup"><span data-stu-id="1e2ee-112">The Plan Options for the selected region will display in the **Plan Options** section of the page.</span></span>
6. <span data-ttu-id="1e2ee-113">En el menú desplegable **Grupo de recursos** , seleccione un grupo de recursos para el plan.</span><span class="sxs-lookup"><span data-stu-id="1e2ee-113">From the **Resource Group** dropdown, select a resource group for the plan.</span></span> <span data-ttu-id="1e2ee-114">Para más información sobre los grupos de recursos, consulte [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1e2ee-114">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
7. <span data-ttu-id="1e2ee-115">En **Nombre del plan** , escriba el nombre del plan.</span><span class="sxs-lookup"><span data-stu-id="1e2ee-115">In **Plan Name** type the name of the plan.</span></span>
8. <span data-ttu-id="1e2ee-116">En **Plan Options**(Opciones de planes), haga clic en el nivel de facturación del nuevo plan.</span><span class="sxs-lookup"><span data-stu-id="1e2ee-116">Under **Plan Options**, click the billing level for the new plan.</span></span>
9. <span data-ttu-id="1e2ee-117">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="1e2ee-117">Click **Create**.</span></span>

## <a name="deploying-the-web-service-to-another-region"></a><span data-ttu-id="1e2ee-118">Implementación del servicio web en otra región</span><span class="sxs-lookup"><span data-stu-id="1e2ee-118">Deploying the web service to another region</span></span>
1. <span data-ttu-id="1e2ee-119">Haga clic en la pestaña **Servicios web** .</span><span class="sxs-lookup"><span data-stu-id="1e2ee-119">Click the **Web Services** menu option.</span></span>
2. <span data-ttu-id="1e2ee-120">Seleccione el servicio web que se va a implementar en una nueva región.</span><span class="sxs-lookup"><span data-stu-id="1e2ee-120">Select the Web Service you are deploying to a new region.</span></span>
3. <span data-ttu-id="1e2ee-121">Haga clic en **Copiar**.</span><span class="sxs-lookup"><span data-stu-id="1e2ee-121">Click **Copy**.</span></span>
4. <span data-ttu-id="1e2ee-122">En **Nombre de servicio web**, escriba un nombre nuevo del servicio web.</span><span class="sxs-lookup"><span data-stu-id="1e2ee-122">In **Web Service Name**, type a new name for the web service.</span></span>
5. <span data-ttu-id="1e2ee-123">En **Descripción del servicio web**, escriba una descripción del servicio web.</span><span class="sxs-lookup"><span data-stu-id="1e2ee-123">In **Web service description**, type a description for the web service.</span></span>
6. <span data-ttu-id="1e2ee-124">En el menú desplegable **Suscripción** , seleccione la suscripción en que residirá el servicio web nuevo.</span><span class="sxs-lookup"><span data-stu-id="1e2ee-124">From the **Subscription** dropdown, select the subscription in which the new web service will reside.</span></span>
7. <span data-ttu-id="1e2ee-125">En el menú desplegable **Grupo de recursos** , seleccione un grupo de recursos para el servicio web.</span><span class="sxs-lookup"><span data-stu-id="1e2ee-125">From the **Resource Group** dropdown, select a resource group for the web service.</span></span> <span data-ttu-id="1e2ee-126">Para más información sobre los grupos de recursos, consulte [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1e2ee-126">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="1e2ee-127">En el menú desplegable **Región** , seleccione la región en la que se va a implementar el servicio web.</span><span class="sxs-lookup"><span data-stu-id="1e2ee-127">From the **Region** dropdown, select the region in which to deploy the web service.</span></span>
9. <span data-ttu-id="1e2ee-128">En el menú desplegable **Cuenta de almacenamiento** , seleccione la cuenta de almacenamiento en la que se va a almacenar el servicio web.</span><span class="sxs-lookup"><span data-stu-id="1e2ee-128">From the **Storage account** dropdown, select a storage account in which to store the web service.</span></span>
10. <span data-ttu-id="1e2ee-129">En el menú desplegable **Price Plan** (Plan de precios), seleccione un plan en la región que seleccionó en el paso 8.</span><span class="sxs-lookup"><span data-stu-id="1e2ee-129">From the **Price Plan** dropdown, select a plan in the region you selected in step 8.</span></span>
11. <span data-ttu-id="1e2ee-130">Haga clic en **Copiar**.</span><span class="sxs-lookup"><span data-stu-id="1e2ee-130">Click **Copy**.</span></span>

