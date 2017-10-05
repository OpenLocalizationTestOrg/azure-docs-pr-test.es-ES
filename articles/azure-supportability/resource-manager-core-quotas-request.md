---
title: "Solicitudes de aumento de cuota de núcleos de Azure Resource Manager | Microsoft Docs"
description: "Solicitudes de aumento de cuota de núcleos de Azure Resource Manager"
author: ganganarayanan
ms.author: gangan
ms.date: 1/18/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: ce37c848-ddd9-46ab-978e-6a1445728a3b
ms.openlocfilehash: cb6c5b3e86f126d4110d1cd29d8c9891e356e414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="resource-manager-core-quota-increase-requests"></a><span data-ttu-id="a033e-103">Solicitudes de aumento de cuota de núcleos de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a033e-103">Resource Manager core quota increase requests</span></span>

<span data-ttu-id="a033e-104">Se imponen cuotas de núcleos de Resource Manager en el nivel de región y de familia de SKU.</span><span class="sxs-lookup"><span data-stu-id="a033e-104">Resource Manager core quotas are enforced at the region level and SKU family level.</span></span>
<span data-ttu-id="a033e-105">Aprenda más sobre cómo se imponen cuotas en la página [Límites de servicios y suscripciones de Azure](http://aka.ms/quotalimits).</span><span class="sxs-lookup"><span data-stu-id="a033e-105">Learn more about how quotas are enforced on the [Azure subscription and service limits](http://aka.ms/quotalimits) page.</span></span>
<span data-ttu-id="a033e-106">Para más información sobre las familias de SKU, puede comparar coste y el rendimiento de la [precios de máquinas virtuales](http://aka.ms/pricingcompute) página.</span><span class="sxs-lookup"><span data-stu-id="a033e-106">To learn more about SKU Families, you may compare cost and performance on the [Virtual Machines Pricing](http://aka.ms/pricingcompute) page.</span></span>

<span data-ttu-id="a033e-107">Para solicitar un aumento, cree un caso de soporte técnico de cuotas en el portal de Azure, [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a033e-107">To request an increase, create a Quota support case for Cores in the Azure portal, [https://portal.azure.com](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="a033e-108">Aprenda a [crear una solicitud de soporte técnico](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) en el portal de Azure</span><span class="sxs-lookup"><span data-stu-id="a033e-108">Learn how to [create a support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) in the Azure portal</span></span>

1. <span data-ttu-id="a033e-109">En la nueva página de solicitud de soporte técnico, seleccione el tipo de problema de "Cuota" y el tipo de cuota de "Núcleos".</span><span class="sxs-lookup"><span data-stu-id="a033e-109">On the new support request page, select Issue type as "Quota" and Quota type as "Cores".</span></span>

    ![Hoja de aspectos básicos de Cuota](./media/resource-manager-core-quotas-request/Basics-blade.png)

2. <span data-ttu-id="a033e-111">Seleccione el modelo de implementación "Resource Manager" y seleccione una ubicación.</span><span class="sxs-lookup"><span data-stu-id="a033e-111">Select Deployment model as "Resource Manager" and select a location.</span></span>

    ![Hoja de problema de Cuota](./media/resource-manager-core-quotas-request/Problem-step.png)

3. <span data-ttu-id="a033e-113">Seleccione las familias de SKU que requieren un aumento.</span><span class="sxs-lookup"><span data-stu-id="a033e-113">Select the SKU Families that require an increase.</span></span>

    ![Series de SKU seleccionadas](./media/resource-manager-core-quotas-request/SKU-selected.png)

4. <span data-ttu-id="a033e-115">Escriba los nuevos límites que quiere en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="a033e-115">Enter the new limits you would like on the subscription.</span></span>

    ![Nueva solicitud de cuota de SKU](./media/resource-manager-core-quotas-request/SKU-new-quota.png)

- <span data-ttu-id="a033e-117">Para quitar una línea, desactive la SKU de la lista desplegable de familias de SKU o haga clic en el icono de descartar "x".</span><span class="sxs-lookup"><span data-stu-id="a033e-117">To remove a line, uncheck the SKU from the SKU family dropdown or click the discard "x" icon.</span></span>
<span data-ttu-id="a033e-118">Después de escribir la cuota deseada para cada familia de SKU, haga clic en "Siguiente" en la página de pasos del problema para continuar con la creación de la solicitud de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="a033e-118">After entering the desired quota for each SKU family, click "Next" on the Problem step page to continue with the support request creation.</span></span>
