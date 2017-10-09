---
title: "aaaTest oferta de la máquina virtual para hello Marketplace | Documentos de Microsoft"
description: "Comprender cómo tootest imagen de la máquina virtual para hello Azure Marketplace."
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
ms.openlocfilehash: ab166d2c3c536810a3a8f48330f0482b9b4e58d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="test-your-vm-offer-for-hello-azure-marketplace-in-staging"></a><span data-ttu-id="069df-103">Probar su oferta VM para hello Azure Marketplace en almacenamiento provisional</span><span class="sxs-lookup"><span data-stu-id="069df-103">Test your VM offer for hello Azure Marketplace in staging</span></span>
<span data-ttu-id="069df-104">Significa que implementar el SKU en privado "espacio aislado" donde pueda probar y validar su funcionalidad antes de implementarla toohello Marketplace de almacenamiento provisional.</span><span class="sxs-lookup"><span data-stu-id="069df-104">Staging means deploying your SKU in a private “sandbox” where you can test and validate its functionality before deploying it toohello Marketplace.</span></span> <span data-ttu-id="069df-105">Hola SKU aparece en ensayo tal como lo haría a tooa cliente que ha implementado.</span><span class="sxs-lookup"><span data-stu-id="069df-105">hello SKU appears in staging just as it would tooa customer who has deployed it.</span></span> <span data-ttu-id="069df-106">La imagen de máquina virtual debe ser toostaging toobe certificadas insertado.</span><span class="sxs-lookup"><span data-stu-id="069df-106">Your VM image must be certified toobe pushed toostaging.</span></span>

## <a name="step-1-push-your-offer-toostaging"></a><span data-ttu-id="069df-107">Paso 1: Insertar su toostaging de oferta</span><span class="sxs-lookup"><span data-stu-id="069df-107">Step 1: Push your offer toostaging</span></span>
1. <span data-ttu-id="069df-108">En hello **publicar** , haga clic en **Push tooStaging**.</span><span class="sxs-lookup"><span data-stu-id="069df-108">On hello **Publish** tab, click **Push tooStaging**.</span></span>
   
    ![dibujo](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. <span data-ttu-id="069df-110">Si el Portal de publicación de hello le informa de los errores, corríjalos.</span><span class="sxs-lookup"><span data-stu-id="069df-110">If hello Publishing Portal notifies you of any errors, correct them.</span></span>
3. <span data-ttu-id="069df-111">Hola **quién puede acceder a su oferta preconfigurada?** diálogo cuadro, escriba Hola lista de suscripciones de Azure que va a usar toopreview su oferta en hello [portal de vista previa](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="069df-111">In hello **Who can access your staged offer?** dialog box, enter hello list of Azure subscriptions that you will use toopreview your offer in hello [Azure preview portal](https://portal.azure.com).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="069df-112">En el caso de las plantillas de soluciones y máquinas virtuales, **no** agregue a la lista blanca suscripciones de tipo CSP, DreamSpark o Azure bajo licencia Open.</span><span class="sxs-lookup"><span data-stu-id="069df-112">In case of Virtual Machines and Solution templates, please **do not** whitelist subscriptions of type CSP, DreamSpark or Azure in Open.</span></span>
   > 
   > 

    > <span data-ttu-id="069df-113">En el caso de máquinas virtuales, al hacer clic en el botón de hello **tooSTAGING de INSERCIÓN**, Hola siguiendo los pasos que se llevan a cabo detrás de escena Hola.</span><span class="sxs-lookup"><span data-stu-id="069df-113">In case of Virtual Machines, when you click on hello button **PUSH tooSTAGING**, hello following steps are performed behind hello scene.</span></span> <span data-ttu-id="069df-114">Será capaz de tooview progreso de Hola de cada paso en la ficha de la publicación de Hola Hola portal de publicación.</span><span class="sxs-lookup"><span data-stu-id="069df-114">You will be able tooview hello progress of each step under hello PUBLISH tab in hello Publishing portal.</span></span> <span data-ttu-id="069df-115">Debe comprobar esta página en intervalos regulares (hasta que el estado de hello muestra almacenado PROVISIONALMENTE) para cualquier información de error que necesita corrección desde el final.</span><span class="sxs-lookup"><span data-stu-id="069df-115">You must check this page at regular interval (until hello status shows STAGED) for any failure information which need correction from your end.</span></span>

    > - <span data-ttu-id="069df-116">En primer lugar la solicitud de almacenamiento provisional va toohello equipo de certificación que validar Hola vhd.</span><span class="sxs-lookup"><span data-stu-id="069df-116">At first your staging request goes toohello certification team who validate hello vhd.</span></span> <span data-ttu-id="069df-117">Sin embargo, si la solicitud tiene solo cambio de marketing, Hola certificación paso se omitirá.</span><span class="sxs-lookup"><span data-stu-id="069df-117">However, if your request has got only marketing change, then hello certification step is skipped.</span></span>
    > - <span data-ttu-id="069df-118">Una vez completada la certificación de hello, replicación de inicio de la oferta de hello en todas las Hola centros de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="069df-118">Once hello certification is complete, replication of hello offer start across all hello Azure datacenters.</span></span> <span data-ttu-id="069df-119">Por lo general toma 24-48hours para toocomplete de replicación de Hola pero puede tardar una semana tooa según tamaño Hola de hello disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="069df-119">It generally takes 24-48hours for hello replication toocomplete but may take up tooa week depending on hello size of hello vhd.</span></span> <span data-ttu-id="069df-120">Sin embargo, si la solicitud tiene solo cambio de marketing, replicación de hello es más rápida.</span><span class="sxs-lookup"><span data-stu-id="069df-120">However, if your request has got only marketing change, then hello replication is faster.</span></span>
    > - <span data-ttu-id="069df-121">Una vez completada la replicación hello, a continuación, oferta Hola estarán disponible en hello [portal de Azure](http:/portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="069df-121">When hello replication is complete, then hello offer will be available in hello [Azure portal](http:/portal.azure.com).</span></span> <span data-ttu-id="069df-122">En ese Hola de tiempo se convierten en ensayo estado Hola portal de publicación.</span><span class="sxs-lookup"><span data-stu-id="069df-122">At that time hello status become STAGED in hello Publishing portal.</span></span> <span data-ttu-id="069df-123">Una oferta de ensayada está visible en hello [portal de Azure](http:/portal.azure.com) únicamente con los identificadores de correo electrónico de hello asociados con qué hello intermedia oferta de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="069df-123">A staged offer is visible in hello [Azure portal](http:/portal.azure.com) only using hello email id(s) associated with hello subscription with which hello offer is staged.</span></span>

1. <span data-ttu-id="069df-124">Inicie sesión en toohello [portal de vista previa](https://portal.azure.com) mediante uno de hello las suscripciones de Azure aparecen en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="069df-124">Sign in toohello [Azure preview portal](https://portal.azure.com) by using one of hello Azure subscriptions listed in hello previous step.</span></span>
2. <span data-ttu-id="069df-125">Busque su oferta y valide los puntos de su imagen de VM:</span><span class="sxs-lookup"><span data-stu-id="069df-125">Find your offer and validate your VM image points:</span></span>
   
   * <span data-ttu-id="069df-126">Asegúrese de que contenido de marketing aparece correctamente en hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="069df-126">Make sure that marketing content shows up correctly in hello Marketplace.</span></span>
   * <span data-ttu-id="069df-127">Implementación to-end de la imagen de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="069df-127">End-to-end deployment of hello VM image.</span></span>
     
      ![img-map-portal](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> <span data-ttu-id="069df-129">Su oferta permanecerá en almacenamiento provisional hasta que notificar a Microsoft a través del Portal de publicación de hello [**publicar** ficha > haga clic en el botón de hello **"Solicitar aprobación tooPush tooProduction"**] que está listo toopush tooproduction.</span><span class="sxs-lookup"><span data-stu-id="069df-129">Your offer will remain in staging until you notify Microsoft via hello Publishing Portal [**Publish** tab > click on hello button **"Request Approval tooPush tooProduction"**] that you are ready toopush tooproduction.</span></span> <span data-ttu-id="069df-130">Se trata de un toohave tiempo ideal que comprobación todos los miembros del equipo a través de todo el contenido de preparación para la oferta va enumeradas.</span><span class="sxs-lookup"><span data-stu-id="069df-130">This is an ideal time toohave all members of your team check over everything in preparation for your offer going listed.</span></span>
> 
> <span data-ttu-id="069df-131">Hola plataforma de almacenamiento provisional está diseñada para pruebas oferta de hello en un modo de vista previa por publicador Hola.</span><span class="sxs-lookup"><span data-stu-id="069df-131">hello staging platform is designed for testing hello offer in a preview mode by hello publisher.</span></span> <span data-ttu-id="069df-132">Se desaconseja encarecidamente usar esta plataforma con fines comerciales.</span><span class="sxs-lookup"><span data-stu-id="069df-132">We strongly discourage using this platofrm for commerical purposes.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="069df-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="069df-133">Next steps</span></span>
<span data-ttu-id="069df-134">Ahora que su oferta "intermedia" y haya probado la funcionalidad y el contenido de marketing, puede continuar la publicación final toohello fase, **paso 4**: [implementar el Marketplace de oferta toohello](marketplace-publishing-push-to-production.md).</span><span class="sxs-lookup"><span data-stu-id="069df-134">Now that your offer is "staged" and you have tested its functionality and marketing content, you can proceed toohello final publishing phase, **Step 4**: [Deploying your offer toohello Marketplace](marketplace-publishing-push-to-production.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="069df-135">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="069df-135">See also</span></span>
* [<span data-ttu-id="069df-136">Introducción: cómo toopublish una toohello de oferta de Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="069df-136">Getting started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

