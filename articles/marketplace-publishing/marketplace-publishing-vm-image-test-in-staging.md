---
title: Probar su oferta de VM para Marketplace | Microsoft Docs
description: "Entienda cómo probar su imagen de VM para Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 7a41c3c6-625c-4478-b804-e124dee89040
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: hascipio
ms.openlocfilehash: 26f856059b381be91b9cdd1f98a11dc90813c0c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="test-your-vm-offer-for-the-azure-marketplace-in-staging"></a><span data-ttu-id="22a8d-103">Probar su oferta de VM para Azure Marketplace en un entorno de ensayo</span><span class="sxs-lookup"><span data-stu-id="22a8d-103">Test your VM offer for the Azure Marketplace in staging</span></span>
<span data-ttu-id="22a8d-104">En la etapa de ensayo, se implementa la SKU en un “espacio aislado” privado, donde puede probar y validar su funcionalidad antes de implementarla en Marketplace.</span><span class="sxs-lookup"><span data-stu-id="22a8d-104">Staging means deploying your SKU in a private “sandbox” where you can test and validate its functionality before deploying it to the Marketplace.</span></span> <span data-ttu-id="22a8d-105">La SKU aparece en un entorno de ensayo tal y como lo haría para un cliente que la ha implementado.</span><span class="sxs-lookup"><span data-stu-id="22a8d-105">The SKU appears in staging just as it would to a customer who has deployed it.</span></span> <span data-ttu-id="22a8d-106">Su imagen de VM debe estar certificada para trasladarse a un entorno de ensayo.</span><span class="sxs-lookup"><span data-stu-id="22a8d-106">Your VM image must be certified to be pushed to staging.</span></span>

## <a name="step-1-push-your-offer-to-staging"></a><span data-ttu-id="22a8d-107">Paso 1: trasladar su oferta a un entorno de ensayo</span><span class="sxs-lookup"><span data-stu-id="22a8d-107">Step 1: Push your offer to staging</span></span>
1. <span data-ttu-id="22a8d-108">En la pestaña **Publicar**, haga clic en **Push to Staging** (Pasar a ensayo).</span><span class="sxs-lookup"><span data-stu-id="22a8d-108">On the **Publish** tab, click **Push to Staging**.</span></span>
   
    ![dibujo](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. <span data-ttu-id="22a8d-110">Si el Portal de publicación le informa errores, corríjalos.</span><span class="sxs-lookup"><span data-stu-id="22a8d-110">If the Publishing Portal notifies you of any errors, correct them.</span></span>
3. <span data-ttu-id="22a8d-111">En el cuadro de diálogo **¿Quién puede obtener acceso a su oferta de ensayo?** , escriba la lista de suscripciones de Azure que usará para obtener una vista previa de su oferta en el [portal de vista previa de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="22a8d-111">In the **Who can access your staged offer?** dialog box, enter the list of Azure subscriptions that you will use to preview your offer in the [Azure preview portal](https://portal.azure.com).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="22a8d-112">En el caso de las plantillas de soluciones y máquinas virtuales, **no** agregue a la lista blanca suscripciones de tipo CSP, DreamSpark o Azure bajo licencia Open.</span><span class="sxs-lookup"><span data-stu-id="22a8d-112">In case of Virtual Machines and Solution templates, please **do not** whitelist subscriptions of type CSP, DreamSpark or Azure in Open.</span></span>
   > 
   > 

    > <span data-ttu-id="22a8d-113">En el caso de las máquinas virtuales, al hacer clic en el botón **PUSH TO STAGING**(INSERTAR EN ENTORNO DE ENSAYO) para enviar la oferta a producción, los siguientes pasos se realizan automáticamente.</span><span class="sxs-lookup"><span data-stu-id="22a8d-113">In case of Virtual Machines, when you click on the button **PUSH TO STAGING**, the following steps are performed behind the scene.</span></span> <span data-ttu-id="22a8d-114">Podrá ver el progreso de cada paso en la pestaña Publicar en el Portal de publicación.</span><span class="sxs-lookup"><span data-stu-id="22a8d-114">You will be able to view the progress of each step under the PUBLISH tab in the Publishing portal.</span></span> <span data-ttu-id="22a8d-115">Debe comprobar esta página de forma periódica (hasta que el estado muestre que está en el entorno provisional) para consultar cualquier información de error que tenga que solucionar.</span><span class="sxs-lookup"><span data-stu-id="22a8d-115">You must check this page at regular interval (until the status shows STAGED) for any failure information which need correction from your end.</span></span>

    > - <span data-ttu-id="22a8d-116">En primer lugar, la solicitud de ensayo pasa al equipo de certificación que valida el VHD.</span><span class="sxs-lookup"><span data-stu-id="22a8d-116">At first your staging request goes to the certification team who validate the vhd.</span></span> <span data-ttu-id="22a8d-117">Sin embargo, si la solicitud tiene solo incluye un cambio de marketing, se omite el paso de certificación.</span><span class="sxs-lookup"><span data-stu-id="22a8d-117">However, if your request has got only marketing change, then the certification step is skipped.</span></span>
    > - <span data-ttu-id="22a8d-118">Cuando se complete la certificación, se inicia la replicación de la oferta en todos los centros de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="22a8d-118">Once the certification is complete, replication of the offer start across all the Azure datacenters.</span></span> <span data-ttu-id="22a8d-119">Normalmente, el proceso de replicación de la oferta tarda en completarse entre 24 y 48 horas, aunque puede extenderse hasta una semana en función del tamaño del VHD.</span><span class="sxs-lookup"><span data-stu-id="22a8d-119">It generally takes 24-48hours for the replication to complete but may take up to a week depending on the size of the vhd.</span></span> <span data-ttu-id="22a8d-120">Sin embargo, si la solicitud tiene solo incluye un cambio de marketing, la replicación se realiza más rápidamente.</span><span class="sxs-lookup"><span data-stu-id="22a8d-120">However, if your request has got only marketing change, then the replication is faster.</span></span>
    > - <span data-ttu-id="22a8d-121">Cuando se complete la replicación, la oferta se mostrará en el [Portal de Azure](http:/portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="22a8d-121">When the replication is complete, then the offer will be available in the [Azure portal](http:/portal.azure.com).</span></span> <span data-ttu-id="22a8d-122">En este momento, el estado muestra que la oferta está en el entorno de ensayo en el Portal de publicación.</span><span class="sxs-lookup"><span data-stu-id="22a8d-122">At that time the status become STAGED in the Publishing portal.</span></span> <span data-ttu-id="22a8d-123">Una oferta de ensayo está visible en el [Portal de Azure](http:/portal.azure.com) solo con los identificadores de correo electrónico asociados con la suscripción con la que se envío la oferta al entorno de ensayo.</span><span class="sxs-lookup"><span data-stu-id="22a8d-123">A staged offer is visible in the [Azure portal](http:/portal.azure.com) only using the email id(s) associated with the subscription with which the offer is staged.</span></span>

1. <span data-ttu-id="22a8d-124">Inicie sesión en el [Portal de vista previa de Azure](https://portal.azure.com) mediante una de las suscripciones de Azure anteriores que se enumeran en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="22a8d-124">Sign in to the [Azure preview portal](https://portal.azure.com) by using one of the Azure subscriptions listed in the previous step.</span></span>
2. <span data-ttu-id="22a8d-125">Busque su oferta y valide los puntos de su imagen de VM:</span><span class="sxs-lookup"><span data-stu-id="22a8d-125">Find your offer and validate your VM image points:</span></span>
   
   * <span data-ttu-id="22a8d-126">Asegúrese de que el contenido de marketing se muestra correctamente en el Marketplace.</span><span class="sxs-lookup"><span data-stu-id="22a8d-126">Make sure that marketing content shows up correctly in the Marketplace.</span></span>
   * <span data-ttu-id="22a8d-127">Implementación completa de la imagen de VM.</span><span class="sxs-lookup"><span data-stu-id="22a8d-127">End-to-end deployment of the VM image.</span></span>
     
      ![img-map-portal](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> <span data-ttu-id="22a8d-129">Su oferta permanecerá en un entorno de ensayo hasta que notifique a Microsoft a través del Portal de publicación [pestaña **Publicar** > **"Solicitar aprobación para enviar a producción"**] que está listo para enviar a producción.</span><span class="sxs-lookup"><span data-stu-id="22a8d-129">Your offer will remain in staging until you notify Microsoft via the Publishing Portal [**Publish** tab > click on the button **"Request Approval to Push to Production"**] that you are ready to push to production.</span></span> <span data-ttu-id="22a8d-130">Este es un momento ideal para que todos los miembros de su equipo revisen todo antes de hacer efectiva la oferta.</span><span class="sxs-lookup"><span data-stu-id="22a8d-130">This is an ideal time to have all members of your team check over everything in preparation for your offer going listed.</span></span>
> 
> <span data-ttu-id="22a8d-131">La plataforma de almacenamiento provisional está diseñada para probar la oferta en un modo de versión preliminar del publicador.</span><span class="sxs-lookup"><span data-stu-id="22a8d-131">The staging platform is designed for testing the offer in a preview mode by the publisher.</span></span> <span data-ttu-id="22a8d-132">Se desaconseja encarecidamente usar esta plataforma con fines comerciales.</span><span class="sxs-lookup"><span data-stu-id="22a8d-132">We strongly discourage using this platofrm for commerical purposes.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="22a8d-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="22a8d-133">Next steps</span></span>
<span data-ttu-id="22a8d-134">Ahora que el estado de su oferta es "de ensayo" y que ha probado su funcionalidad y contenido de marketing, puede continuar con la fase de publicación final, el **Paso 4**: [Implementación de su oferta en Marketplace](marketplace-publishing-push-to-production.md).</span><span class="sxs-lookup"><span data-stu-id="22a8d-134">Now that your offer is "staged" and you have tested its functionality and marketing content, you can proceed to the final publishing phase, **Step 4**: [Deploying your offer to the Marketplace](marketplace-publishing-push-to-production.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="22a8d-135">Consulte también</span><span class="sxs-lookup"><span data-stu-id="22a8d-135">See also</span></span>
* [<span data-ttu-id="22a8d-136">Introducción: Publicación de una oferta en Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="22a8d-136">Getting started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

