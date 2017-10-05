---
title: "Prueba de la oferta de plantilla de solución en Marketplace | Microsoft Docs"
description: "Conozca cómo probar la oferta de plantilla de solución en Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: ef8f9b5e-b98c-49f3-913f-cdf772c14c12
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/04/2015
ms.author: hascipio; v-divte
ms.openlocfilehash: da1fc4713fd1d832c7ba91226f72cbef63b241bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="test-your-solution-template-offer-in-staging"></a><span data-ttu-id="49c0c-103">Prueba de la oferta de plantilla de solución en ensayo</span><span class="sxs-lookup"><span data-stu-id="49c0c-103">Test your solution template offer in staging</span></span>
<span data-ttu-id="49c0c-104">En la etapa de ensayo se implementa la oferta en un “espacio aislado” privado, donde puede probar y comprobar su funcionalidad antes pasarla a producción.</span><span class="sxs-lookup"><span data-stu-id="49c0c-104">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it to production.</span></span> <span data-ttu-id="49c0c-105">La oferta aparece en un entorno de ensayo tal y como lo haría para un cliente que la ha implementado.</span><span class="sxs-lookup"><span data-stu-id="49c0c-105">The offer appears in staging just as it would to a customer who has deployed it.</span></span> <span data-ttu-id="49c0c-106">La oferta debe estar certificada para pasar a un entorno de ensayo.</span><span class="sxs-lookup"><span data-stu-id="49c0c-106">Your offer must be certified to be pushed to staging.</span></span>

<span data-ttu-id="49c0c-107">Después de preconfigurar la oferta, puede verla y probarla en el [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="49c0c-107">After the offer is staged, you can view and test the offer in the [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="49c0c-108">Siga los pasos indicados a continuación para insertar la oferta en el entorno de ensayo y probarla en el [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="49c0c-108">Follow the steps below to push your offer to staging and test it in the [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="49c0c-109">Vaya al [Portal de publicación](https://publish.windowsazure.com) >  pestaña **Plantillas de solución** > su oferta > **Publicar** > **Push to Staging** (Pasar a ensayo).</span><span class="sxs-lookup"><span data-stu-id="49c0c-109">Go to the [Publishing Portal](https://publish.windowsazure.com) > **Solution Templates** tab > your offer > **Publish** > **Push to Staging**.</span></span>
2. <span data-ttu-id="49c0c-110">Proporcione la lista de suscripciones de Azure que va a usar para obtener la vista previa de la oferta y probarla.</span><span class="sxs-lookup"><span data-stu-id="49c0c-110">Provide the list of Azure subscriptions that you will use to preview and test your offer.</span></span>
3. <span data-ttu-id="49c0c-111">Inicie sesión en el Portal de vista previa de Azure mediante el identificador de suscripción que usó en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="49c0c-111">Sign in to the Azure preview portal by using the subscription ID that you used in the previous step.</span></span>
4. <span data-ttu-id="49c0c-112">Realice al menos una ronda de pruebas en el Portal de vista previa de Azure sobre los puntos que se mencionan a continuación:</span><span class="sxs-lookup"><span data-stu-id="49c0c-112">Carry out at least one round of testing in the Azure preview portal on the points mentioned below:</span></span>
   * <span data-ttu-id="49c0c-113">Asegúrese de que el contenido de marketing se muestra correctamente en el Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="49c0c-113">Make sure that marketing content shows up correctly in the Azure Marketplace.</span></span>
   * <span data-ttu-id="49c0c-114">Compruebe la implementación completa de la topología.</span><span class="sxs-lookup"><span data-stu-id="49c0c-114">End-to-end deployment of the topology.</span></span>
   * <span data-ttu-id="49c0c-115">Realice pruebas de rendimiento y pruebas de esfuerzo.</span><span class="sxs-lookup"><span data-stu-id="49c0c-115">Perform performance testing and stress testing.</span></span>
   * <span data-ttu-id="49c0c-116">Asegúrese de que la topología se ajusta a las prácticas recomendadas.</span><span class="sxs-lookup"><span data-stu-id="49c0c-116">Ensure that your topology adheres to the best practices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49c0c-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="49c0c-117">Next steps</span></span>
<span data-ttu-id="49c0c-118">Si está satisfecho con los resultados, puede continuar en la fase de publicación de la oferta final, **paso 4**: [Implementación de la oferta en Marketplace](marketplace-publishing-push-to-production.md).</span><span class="sxs-lookup"><span data-stu-id="49c0c-118">If you are satisfied with the results, then you can proceed to the final offer publishing phase, **Step 4**:  [Deploying your offer to the Marketplace](marketplace-publishing-push-to-production.md).</span></span> <span data-ttu-id="49c0c-119">Si no, realice cambios en la oferta y vuelva a solicitar la certificación.</span><span class="sxs-lookup"><span data-stu-id="49c0c-119">Otherwise, make changes in your offer and request certification again.</span></span>

> [!NOTE]
> <span data-ttu-id="49c0c-120">Para los cambios de contenido de marketing, no se requiere certificación.</span><span class="sxs-lookup"><span data-stu-id="49c0c-120">For marketing content changes, certification is not required.</span></span>
> 
> 

<span data-ttu-id="49c0c-121">Vea [Introducción: Publicación de una oferta en Azure Marketplace](marketplace-publishing-getting-started.md) para obtener una guía de todas las tareas del publicador.</span><span class="sxs-lookup"><span data-stu-id="49c0c-121">See [Getting started: How to publish an offer to the Azure Marketplace](marketplace-publishing-getting-started.md) for a guide to all publisher tasks.</span></span>

