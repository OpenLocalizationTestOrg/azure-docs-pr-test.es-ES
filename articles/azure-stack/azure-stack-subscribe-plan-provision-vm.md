---
title: "Suscripción a una oferta | Microsoft Docs"
description: "Aprenda cómo los usuarios se suscriben a una oferta."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 7f3f8683-ef09-4838-92ed-41f2fddbbbed
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/03/2017
ms.author: erikje
ms.openlocfilehash: f70815b5e89753a4b0083ffbe10d9920062d1ff0
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2017
---
# <a name="subscribe-to-an-offer"></a><span data-ttu-id="bbd96-103">Suscripción a una oferta</span><span class="sxs-lookup"><span data-stu-id="bbd96-103">Subscribe to an offer</span></span>

<span data-ttu-id="bbd96-104">*Se aplica a: Sistemas integrados de Azure Stack y Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="bbd96-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="bbd96-105">Ahora que ha [creado una oferta](azure-stack-create-offer.md), compruebe que los usuarios pueden crear una suscripción.</span><span class="sxs-lookup"><span data-stu-id="bbd96-105">Now that you've [created an offer](azure-stack-create-offer.md), test that your users can create a subscription.</span></span>

1. <span data-ttu-id="bbd96-106">[Inicie sesión](azure-stack-connect-azure-stack.md) el portal de usuarios de Azure Stack (https://portal.local.azurestack.external/) y haga clic en **Obtener una suscripción**.</span><span class="sxs-lookup"><span data-stu-id="bbd96-106">[Sign in](azure-stack-connect-azure-stack.md) to the Azure Stack user portal (https://portal.local.azurestack.external) and click **Get a Subscription**.</span></span>

   ![](media/azure-stack-subscribe-plan-provision-vm/image01.png)
2. <span data-ttu-id="bbd96-107">En el campo **Nombre para mostrar**, escriba un nombre para la suscripción, haga clic en **Oferta**, haga clic en una de las ofertas en la hoja **Elija una oferta** y, después, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="bbd96-107">In the **Display Name** field, type a name for your subscription, click **Offer**, click one of the offers in the **Choose an offer** blade, and then click **Create**.</span></span>

   ![](media/azure-stack-subscribe-plan-provision-vm/image02.png)
3. <span data-ttu-id="bbd96-108">Para ver la suscripción que ha creado, haga clic en **Más servicios**, en **Suscripciones** y, luego, en la nueva suscripción.</span><span class="sxs-lookup"><span data-stu-id="bbd96-108">To view the subscription you created, click **More services**, click **Subscriptions**, then click your new subscription.</span></span>  

<span data-ttu-id="bbd96-109">Después de suscribirse a una oferta, actualice el portal para ver los servicios que forman parte de la nueva suscripción.</span><span class="sxs-lookup"><span data-stu-id="bbd96-109">After you subscribe to an offer, refresh the portal to see which services are part of the new subscription.</span></span>

## <a name="subscribe-to-an-add-on-plan"></a><span data-ttu-id="bbd96-110">Suscripción a un plan complementario</span><span class="sxs-lookup"><span data-stu-id="bbd96-110">Subscribe to an add-on plan</span></span>
<span data-ttu-id="bbd96-111">Si la oferta tiene algún plan complementario, los usuarios pueden agregarlo a su suscripción en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="bbd96-111">If the offer has an add-on plan, users can add them to their subscription at any time.</span></span>  

1. <span data-ttu-id="bbd96-112">En el portal de usuarios, seleccione **Más servicios** > **Suscripciones**.</span><span class="sxs-lookup"><span data-stu-id="bbd96-112">In the user portal, select **More services** > **Subscriptions**.</span></span>

2. <span data-ttu-id="bbd96-113">Haga clic en la suscripción > botón **Agregar Plan** y seleccione el plan complementario.</span><span class="sxs-lookup"><span data-stu-id="bbd96-113">Click on the subscription > **Add Plan** button, and select the add-on plan.</span></span>



## <a name="next-steps"></a><span data-ttu-id="bbd96-114">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bbd96-114">Next steps</span></span>
[<span data-ttu-id="bbd96-115">Aprovisionamiento de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="bbd96-115">Provision a virtual machine</span></span>](azure-stack-provision-vm.md)
