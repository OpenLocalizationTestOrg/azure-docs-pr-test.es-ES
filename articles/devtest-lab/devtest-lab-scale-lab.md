---
title: "Escalado de cuotas y límites en su laboratorio en Azure DevTest Labs | Microsoft Docs"
description: Aprenda a escalar un laboratorio en Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: ae624155-9181-45fa-bd2b-1983339b7e0e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: tarcher
ms.openlocfilehash: f11ed42b474e4f208eac92689bfa33fb188d15a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a><span data-ttu-id="fda4c-103">Escalado de cuotas y límites en DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="fda4c-103">Scale quotas and limits in DevTest Labs</span></span>
<span data-ttu-id="fda4c-104">Mientras trabaja en DevTest Labs, puede que observe que hay ciertos límites predeterminados para algunos recursos de Azure, lo que puede afectar al servicio DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="fda4c-104">As you work in DevTest Labs, you might notice that there are certain default limits to some Azure resources, which can affect the DevTest Labs service.</span></span> <span data-ttu-id="fda4c-105">Estos límites se conocen como **cuotas**.</span><span class="sxs-lookup"><span data-stu-id="fda4c-105">These limits are referred to as **quotas**.</span></span>

> [!NOTE]
> <span data-ttu-id="fda4c-106">El servicio DevTest Labs no impone cuotas.</span><span class="sxs-lookup"><span data-stu-id="fda4c-106">The DevTest Labs service doesn't impose any quotas.</span></span> <span data-ttu-id="fda4c-107">Las cuotas que podría encontrar son restricciones predeterminadas de la suscripción de Azure en general.</span><span class="sxs-lookup"><span data-stu-id="fda4c-107">Any quotas you might encounter are default constraints of the overall Azure subscription.</span></span>

<span data-ttu-id="fda4c-108">Puede usar cada recurso de Azure hasta que alcance su cuota.</span><span class="sxs-lookup"><span data-stu-id="fda4c-108">You can use each Azure resource until you reach its quota.</span></span> <span data-ttu-id="fda4c-109">Cada suscripción tiene cuotas independientes y se realiza el seguimiento del uso para cada suscripción.</span><span class="sxs-lookup"><span data-stu-id="fda4c-109">Each subscription has separate quotas and usage is tracked per subscription.</span></span>

<span data-ttu-id="fda4c-110">Por ejemplo, cada suscripción tiene una cuota predeterminada de 20 núcleos.</span><span class="sxs-lookup"><span data-stu-id="fda4c-110">For example, each subscription has a default quota of 20 cores.</span></span> <span data-ttu-id="fda4c-111">Por lo tanto, si va a crear en el laboratorio máquinas virtuales con cuatro núcleos, solo puede crear cinco.</span><span class="sxs-lookup"><span data-stu-id="fda4c-111">So, if you are creating VMs in your lab with four cores each, then you can only create five VMs.</span></span> 

<span data-ttu-id="fda4c-112">En [Límites de suscripción y de servicios de Azure](https://docs.microsoft.com/azure/azure-subscription-service-limits), se enumeran algunas de las cuotas más frecuentes para recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="fda4c-112">[Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits) lists some of the most common quotas for Azure resources.</span></span> <span data-ttu-id="fda4c-113">Entre los recursos que más se usan en un laboratorio y para los que puede encontrar cuotas, están los núcleos de máquina virtual, las direcciones IP públicas, la interfaz de red, los discos administrados, la asignación de roles RBAC y los circuitos ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fda4c-113">The resources most commonly used in a lab, and for which you might encounter quotas, include VM cores, public IP addresses, network interface, managed disks, RBAC role assignment, and ExpressRoute circuits.</span></span>

## <a name="view-your-usage-and-quotas"></a><span data-ttu-id="fda4c-114">Visualización del uso y las cuotas</span><span class="sxs-lookup"><span data-stu-id="fda4c-114">View your usage and quotas</span></span>
<span data-ttu-id="fda4c-115">Estos pasos muestran cómo ver las cuotas actuales en su suscripción para recursos específicos de Azure y comprobar qué porcentaje de cada cuota ha usado.</span><span class="sxs-lookup"><span data-stu-id="fda4c-115">These steps show you how to view the current quotas in your subscription for specific Azure resources, and to see what percentage of each quota you have used.</span></span>

1. <span data-ttu-id="fda4c-116">Inicie sesión en el [Portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="fda4c-116">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="fda4c-117">Seleccione **Más servicios** y **Facturación** en la lista.</span><span class="sxs-lookup"><span data-stu-id="fda4c-117">Select **More Services**, and then select **Billing** from the list.</span></span>
1. <span data-ttu-id="fda4c-118">En la hoja Facturación, seleccione una suscripción.</span><span class="sxs-lookup"><span data-stu-id="fda4c-118">In the Billing blade, select a subscription.</span></span>
4. <span data-ttu-id="fda4c-119">Seleccione **Uso y cuotas**.</span><span class="sxs-lookup"><span data-stu-id="fda4c-119">Select **Usage + quotas**.</span></span>

   ![Botón Uso y cuotas](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   <span data-ttu-id="fda4c-121">Aparece la hoja Uso y cuotas, donde se muestran los distintos recursos disponibles en esa suscripción y el porcentaje de la cuota que está usando para cada uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="fda4c-121">The Usage + quotas blade appears, listing different resources available in that subscription and the percentage of the quota that is being used per resource.</span></span>

   ![Cuotas y uso](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a><span data-ttu-id="fda4c-123">Solicitud de más recursos en la suscripción</span><span class="sxs-lookup"><span data-stu-id="fda4c-123">Requesting more resources in your subscription</span></span>
<span data-ttu-id="fda4c-124">Si alcanza un límite de cuota, se puede aumentar el límite predeterminado de un recurso en una suscripción hasta un máximo, como se describe en [Límites de suscripción y de servicios de Azure](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span><span class="sxs-lookup"><span data-stu-id="fda4c-124">If you reach a quota cap, the default limit of a resource in a subscription can be increased up to a maximum limit, as described in [Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span></span>

<span data-ttu-id="fda4c-125">Estos pasos le muestran cómo solicitar un aumento de la cuota a través de [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="fda4c-125">These steps show you how to request a quota increase through the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="fda4c-126">Seleccione **Más servicios**, **Facturación**, y **Uso y cuotas**.</span><span class="sxs-lookup"><span data-stu-id="fda4c-126">Select **More Services**, select **Billing**, and then select **Usage + quotas**.</span></span>
1. <span data-ttu-id="fda4c-127">En la hoja Uso y cuotas, seleccione el botón **Solicitar aumento**.</span><span class="sxs-lookup"><span data-stu-id="fda4c-127">In the Usage + quotas blade, select the **Request Increase** button.</span></span>

   ![Botón Solicitar aumento](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. <span data-ttu-id="fda4c-129">Para completar y enviar la solicitud, rellene la información necesaria en las tres pestañas del formulario **Nueva solicitud de soporte técnico**.</span><span class="sxs-lookup"><span data-stu-id="fda4c-129">To complete and submit the request, fill out the required information on all three tabs of the **New support request** form.</span></span>

   ![Formulario Solicitar aumento](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

<span data-ttu-id="fda4c-131">[Understanding Azure Limits and Increases](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) (Información sobre los límites y los aumentos de Azure) proporciona más información sobre cómo ponerse en contacto con el soporte técnico de Azure para solicitar un aumento de la cuota.</span><span class="sxs-lookup"><span data-stu-id="fda4c-131">[Understanding Azure Limits and Increases](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) provides more information about contacting Azure support to request a quota increase.</span></span>



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a><span data-ttu-id="fda4c-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fda4c-132">Next steps</span></span>
* <span data-ttu-id="fda4c-133">Explore la [galería de plantillas de inicio rápido de Azure Resource Manager de DevTest Labs](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="fda4c-133">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span></span>
