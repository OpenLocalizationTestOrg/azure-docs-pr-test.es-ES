---
title: "Registro de un vale de soporte técnico a través de StorSimple Device Manager | Microsoft Docs"
description: "Describe la funcionalidad de diagnóstico de StorSimple Device Manager y explica cómo usarla para solucionar problemas de StorSimple Virtual Array."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: a0c394df-957b-49b3-a283-38824f8847fd
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 658afbc178814389fefd7941e2ca030741bd08e8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-log-a-support-request-for-the-storsimple-virtual-array"></a><span data-ttu-id="d4fa4-103">Uso del servicio StorSimple Device Manager para registrar una solicitud de soporte técnico para StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="d4fa4-103">Use the StorSimple Device Manager service to log a Support request for the StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="d4fa4-104">Información general</span><span class="sxs-lookup"><span data-stu-id="d4fa4-104">Overview</span></span>

<span data-ttu-id="d4fa4-105">StorSimple Device Manager proporciona la posibilidad de **registrar una nueva solicitud de soporte técnico** en la hoja de resumen del servicio.</span><span class="sxs-lookup"><span data-stu-id="d4fa4-105">The StorSimple Device Manager provides the capability to **log a new support request** within the service summary blade.</span></span> <span data-ttu-id="d4fa4-106">Este artículo explica cómo puede registrar una nueva solicitud de soporte técnico y administrar su ciclo de vida en el portal.</span><span class="sxs-lookup"><span data-stu-id="d4fa4-106">This article explains how you can log a new support request and manage its lifecycle from within the portal.</span></span>

## <a name="new-support-request"></a><span data-ttu-id="d4fa4-107">Nueva solicitud de soporte</span><span class="sxs-lookup"><span data-stu-id="d4fa4-107">New support request</span></span>

<span data-ttu-id="d4fa4-108">En función de su [plan de soporte técnico](https://azure.microsoft.com/support/plans/), puede crear vales de soporte para un problema en su instancia de StorSimple Virtual Array directamente desde la hoja de resumen del servicio StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="d4fa4-108">Depending upon your [support plan](https://azure.microsoft.com/support/plans/), you can create support tickets for an issue on your StorSimple Virtual array directly from the StorSimple Device Manager service summary blade.</span></span>

#### <a name="to-log-a-new-request"></a><span data-ttu-id="d4fa4-109">Para registrar una nueva solicitud</span><span class="sxs-lookup"><span data-stu-id="d4fa4-109">To log a new request</span></span>

1. <span data-ttu-id="d4fa4-110">Vaya al servicio StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="d4fa4-110">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="d4fa4-111">En la configuración de la hoja de resumen del servicio, vaya a la sección **Soporte técnico y solución de problemas** y haga clic en **Nueva solicitud de soporte técnico**.</span><span class="sxs-lookup"><span data-stu-id="d4fa4-111">In the service summary blade settings, go to **SUPPORT + TROUBLESHOOTING** section and then click **New support request**.</span></span>
   
    ![Nueva solicitud de soporte](./media/storsimple-virtual-array-log-support-ticket/log-support-ticket1.png)

2. <span data-ttu-id="d4fa4-113">En la hoja **Aspectos básicos**, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d4fa4-113">In the **Basics** blade, do the following:</span></span>

    1. <span data-ttu-id="d4fa4-114">En la lista desplegable **Tipo de problema**, seleccione **Técnico**.</span><span class="sxs-lookup"><span data-stu-id="d4fa4-114">From the **Issue type** dropdown list, select **Technical**.</span></span> 
    
    2. <span data-ttu-id="d4fa4-115">Se eligen automáticamente la **Suscripción** actual, el tipo de **Servicio** y el **Recurso** (servicio StorSimple Device Manager).</span><span class="sxs-lookup"><span data-stu-id="d4fa4-115">The current **Subscription**, **Service** type, and the **Resource** (StorSimple Device Manager service) are automatically chosen.</span></span> 

    3. <span data-ttu-id="d4fa4-116">Especifique uno o varios dispositivos registrados en el servicio que están experimentando problemas.</span><span class="sxs-lookup"><span data-stu-id="d4fa4-116">Specify one or more devices registered to your service that are experiencing issues.</span></span>

    4. <span data-ttu-id="d4fa4-117">Elija un **plan de soporte técnico** adecuado si tiene varios planes asociados a la suscripción.</span><span class="sxs-lookup"><span data-stu-id="d4fa4-117">Choose an appropriate **support plan** if you have multiple plans associated with your subscription.</span></span> <span data-ttu-id="d4fa4-118">Para habilitar el soporte técnico, debe contar con un plan de soporte técnico de pago.</span><span class="sxs-lookup"><span data-stu-id="d4fa4-118">You need a paid support plan to enable Technical Support.</span></span>

3. <span data-ttu-id="d4fa4-119">En el **paso 2**, elija la **Gravedad** y especifique si el problema está relacionado con la matriz o con el servicio StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="d4fa4-119">In **Step 2**, choose the **Severity** and specify if the issue is related to the array or the StorSimple Device Manager service.</span></span> <span data-ttu-id="d4fa4-120">Además, elija una **Categoría** para este problema y proporcione más **Detalles** sobre el problema.</span><span class="sxs-lookup"><span data-stu-id="d4fa4-120">Also, choose a **Category** for this issue and provide more **Details** about the issue.</span></span>
   
    ![Nueva solicitud de soporte](./media/storsimple-virtual-array-log-support-ticket/log-support-ticket2.png)

4. <span data-ttu-id="d4fa4-122">En el **paso 3**, proporcione la información de contacto.</span><span class="sxs-lookup"><span data-stu-id="d4fa4-122">In **Step 3**, provide your contact information.</span></span> <span data-ttu-id="d4fa4-123">El Soporte técnico de Microsoft usará esta información para ponerse en contacto con usted para solicitar más información y comunicar el diagnóstico y la resolución.</span><span class="sxs-lookup"><span data-stu-id="d4fa4-123">Microsoft Support will use this information to reach out to you for further information, diagnosis, and resolution.</span></span>
   
    ![Nueva solicitud de soporte](./media/storsimple-virtual-array-log-support-ticket/log-support-ticket3.png)

## <a name="manage-a-support-request"></a><span data-ttu-id="d4fa4-125">Administración de una solicitud de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="d4fa4-125">Manage a support request</span></span>

<span data-ttu-id="d4fa4-126">Después de crear una incidencia de soporte técnico, puede administrar el ciclo de vida de la incidencia desde el portal.</span><span class="sxs-lookup"><span data-stu-id="d4fa4-126">After creating a support ticket, you can manage the lifecycle of the ticket from within the portal.</span></span>

#### <a name="to-manage-your-support-requests"></a><span data-ttu-id="d4fa4-127">Para administrar las solicitudes de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="d4fa4-127">To manage your support requests</span></span>

<span data-ttu-id="d4fa4-128">Para tener acceso a la página de ayuda y soporte técnico, vaya a **Examinar > Ayuda y soporte técnico**.</span><span class="sxs-lookup"><span data-stu-id="d4fa4-128">To get to the help and support page, navigate to **Browse > Help + support**.</span></span>

![Administrar solicitudes de soporte técnico](./media/storsimple-virtual-array-log-support-ticket/manage-support-tickets.png)

## <a name="next-steps"></a><span data-ttu-id="d4fa4-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d4fa4-130">Next steps</span></span>

<span data-ttu-id="d4fa4-131">Aprenda cómo [diagnosticar y solucionar problemas relacionados con StorSimple Virtual Array](storsimple-virtual-array-diagnose-problems.md).</span><span class="sxs-lookup"><span data-stu-id="d4fa4-131">Learn how to [diagnose and solve problems related to your StorSimple Virtual array](storsimple-virtual-array-diagnose-problems.md)</span></span>

