---
title: "Suscripción a una oferta | Microsoft Docs"
description: "Aprenda cómo se suscriben los inquilinos a las ofertas."
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
ms.openlocfilehash: 3cd87ebe9827249d32f15b5de0ad8521d0282c47
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="subscribe-to-an-offer"></a><span data-ttu-id="8c54a-103">Suscripción a una oferta</span><span class="sxs-lookup"><span data-stu-id="8c54a-103">Subscribe to an offer</span></span>
<span data-ttu-id="8c54a-104">Ahora que ha [creado una oferta](azure-stack-create-offer.md), compruebe que los inquilinos pueden crear una suscripción.</span><span class="sxs-lookup"><span data-stu-id="8c54a-104">Now that you've [created an offer](azure-stack-create-offer.md), test that your tenants can create a subscription.</span></span>

1. <span data-ttu-id="8c54a-105">[Inicie sesión](azure-stack-connect-azure-stack.md) el portal de inquilinos de Azure Stack (https://portal.local.azurestack.external/) y haga clic en **Obtener una suscripción**.</span><span class="sxs-lookup"><span data-stu-id="8c54a-105">[Sign in](azure-stack-connect-azure-stack.md) to the Azure Stack tenant portal (https://portal.local.azurestack.external) and click **Get a Subscription**.</span></span>

   ![](media/azure-stack-subscribe-plan-provision-vm/image01.png)
2. <span data-ttu-id="8c54a-106">En el campo **Nombre para mostrar**, escriba un nombre para la suscripción, haga clic en **Oferta**, haga clic en una de las ofertas en la hoja **Elija una oferta** y, después, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="8c54a-106">In the **Display Name** field, type a name for your subscription, click **Offer**, click one of the offers in the **Choose an offer** blade, and then click **Create**.</span></span>

   ![](media/azure-stack-subscribe-plan-provision-vm/image02.png)
3. <span data-ttu-id="8c54a-107">Para ver la suscripción que ha creado, haga clic en **Más servicios**, en **Suscripciones** y, luego, en la nueva suscripción.</span><span class="sxs-lookup"><span data-stu-id="8c54a-107">To view the subscription you created, click **More services**, click **Subscriptions**, then click your new subscription.</span></span>  

<span data-ttu-id="8c54a-108">Después de suscribirse a una oferta, actualice el portal para ver los servicios que forman parte de la nueva suscripción.</span><span class="sxs-lookup"><span data-stu-id="8c54a-108">After you subscribe to an offer, refresh the portal to see which services are part of the new subscription.</span></span>

## <a name="subscribe-to-an-add-on-plan"></a><span data-ttu-id="8c54a-109">Suscripción a un plan complementario</span><span class="sxs-lookup"><span data-stu-id="8c54a-109">Subscribe to an add-on plan</span></span>
<span data-ttu-id="8c54a-110">Si la oferta tiene algún plan complementario, los inquilinos pueden agregarlo a su suscripción en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="8c54a-110">If the offer has an add-on plan, tenants can add them to their subscription at any time.</span></span>  

1. <span data-ttu-id="8c54a-111">En el portal de inquilinos, seleccione **más servicios** > **Suscripciones**.</span><span class="sxs-lookup"><span data-stu-id="8c54a-111">In the tenant portal, select **More services** > **Subscriptions**.</span></span>

2. <span data-ttu-id="8c54a-112">Haga clic en la suscripción > botón **Agregar Plan** y seleccione el plan complementario.</span><span class="sxs-lookup"><span data-stu-id="8c54a-112">Click on the subscription > **Add Plan** button, and select the add-on plan.</span></span>



## <a name="next-steps"></a><span data-ttu-id="8c54a-113">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8c54a-113">Next steps</span></span>
[<span data-ttu-id="8c54a-114">Aprovisionamiento de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8c54a-114">Provision a virtual machine</span></span>](azure-stack-provision-vm.md)
