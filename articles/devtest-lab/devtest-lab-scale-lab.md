---
title: "aaaScale las cuotas y límites en el laboratorio de prácticas de desarrollo y pruebas de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooscale un laboratorio de prácticas de desarrollo y pruebas de Azure"
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
ms.openlocfilehash: 7fb429c0aabdfbce3a4a5aa6d9259daa2ee270d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a><span data-ttu-id="d2fb6-103">Escalado de cuotas y límites en DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="d2fb6-103">Scale quotas and limits in DevTest Labs</span></span>
<span data-ttu-id="d2fb6-104">Cuando se trabaja en los laboratorios de desarrollo y pruebas, podría Observe que hay determinado toosome de límites de forma predeterminada los recursos de Azure, lo que pueden afectar al servicio de laboratorios de desarrollo y pruebas de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2fb6-104">As you work in DevTest Labs, you might notice that there are certain default limits toosome Azure resources, which can affect hello DevTest Labs service.</span></span> <span data-ttu-id="d2fb6-105">Estos límites son los que se hace referencia tooas **cuotas**.</span><span class="sxs-lookup"><span data-stu-id="d2fb6-105">These limits are referred tooas **quotas**.</span></span>

> [!NOTE]
> <span data-ttu-id="d2fb6-106">Hola servicio laboratorios de desarrollo y pruebas no impone cuotas.</span><span class="sxs-lookup"><span data-stu-id="d2fb6-106">hello DevTest Labs service doesn't impose any quotas.</span></span> <span data-ttu-id="d2fb6-107">Las cuotas que pueden surgir son restricciones default de hello suscripción de Azure en general.</span><span class="sxs-lookup"><span data-stu-id="d2fb6-107">Any quotas you might encounter are default constraints of hello overall Azure subscription.</span></span>

<span data-ttu-id="d2fb6-108">Puede usar cada recurso de Azure hasta que alcance su cuota.</span><span class="sxs-lookup"><span data-stu-id="d2fb6-108">You can use each Azure resource until you reach its quota.</span></span> <span data-ttu-id="d2fb6-109">Cada suscripción tiene cuotas independientes y se realiza el seguimiento del uso para cada suscripción.</span><span class="sxs-lookup"><span data-stu-id="d2fb6-109">Each subscription has separate quotas and usage is tracked per subscription.</span></span>

<span data-ttu-id="d2fb6-110">Por ejemplo, cada suscripción tiene una cuota predeterminada de 20 núcleos.</span><span class="sxs-lookup"><span data-stu-id="d2fb6-110">For example, each subscription has a default quota of 20 cores.</span></span> <span data-ttu-id="d2fb6-111">Por lo tanto, si va a crear en el laboratorio máquinas virtuales con cuatro núcleos, solo puede crear cinco.</span><span class="sxs-lookup"><span data-stu-id="d2fb6-111">So, if you are creating VMs in your lab with four cores each, then you can only create five VMs.</span></span> 

<span data-ttu-id="d2fb6-112">[Suscripción de Azure y límites de servicio](https://docs.microsoft.com/azure/azure-subscription-service-limits) se enumeran algunas de las cuotas más comunes de Hola para recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="d2fb6-112">[Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits) lists some of hello most common quotas for Azure resources.</span></span> <span data-ttu-id="d2fb6-113">Hola suelen usados en un laboratorio de recursos, y para que pueden surgir cuotas, incluir núcleos de la máquina virtual, las direcciones IP públicas, interfaz de red, discos administrados, asignación de roles RBAC y circuitos ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d2fb6-113">hello resources most commonly used in a lab, and for which you might encounter quotas, include VM cores, public IP addresses, network interface, managed disks, RBAC role assignment, and ExpressRoute circuits.</span></span>

## <a name="view-your-usage-and-quotas"></a><span data-ttu-id="d2fb6-114">Visualización del uso y las cuotas</span><span class="sxs-lookup"><span data-stu-id="d2fb6-114">View your usage and quotas</span></span>
<span data-ttu-id="d2fb6-115">Estos pasos muestra cómo tooview Hola cuotas actuales en su suscripción a recursos específicos de Azure y toosee qué porcentaje de cada cuota ha usado.</span><span class="sxs-lookup"><span data-stu-id="d2fb6-115">These steps show you how tooview hello current quotas in your subscription for specific Azure resources, and toosee what percentage of each quota you have used.</span></span>

1. <span data-ttu-id="d2fb6-116">Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="d2fb6-116">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="d2fb6-117">Seleccione **más servicios**y, a continuación, seleccione **facturación** de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2fb6-117">Select **More Services**, and then select **Billing** from hello list.</span></span>
1. <span data-ttu-id="d2fb6-118">En la hoja de facturación de hello, seleccione una suscripción.</span><span class="sxs-lookup"><span data-stu-id="d2fb6-118">In hello Billing blade, select a subscription.</span></span>
4. <span data-ttu-id="d2fb6-119">Seleccione **Uso y cuotas**.</span><span class="sxs-lookup"><span data-stu-id="d2fb6-119">Select **Usage + quotas**.</span></span>

   ![Botón Uso y cuotas](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   <span data-ttu-id="d2fb6-121">Hola uso + cuotas hoja aparecerá una lista de diferentes recursos disponibles en ese porcentaje hello y suscripción de cuota de Hola que se utiliza por recurso.</span><span class="sxs-lookup"><span data-stu-id="d2fb6-121">hello Usage + quotas blade appears, listing different resources available in that subscription and hello percentage of hello quota that is being used per resource.</span></span>

   ![Cuotas y uso](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a><span data-ttu-id="d2fb6-123">Solicitud de más recursos en la suscripción</span><span class="sxs-lookup"><span data-stu-id="d2fb6-123">Requesting more resources in your subscription</span></span>
<span data-ttu-id="d2fb6-124">Si alcanza un límite de cuota, límite predeterminado de Hola de un recurso en una suscripción se puede aumentar la longitud máxima tooa, tal y como se describe en [suscripción a Azure y límites de servicio](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span><span class="sxs-lookup"><span data-stu-id="d2fb6-124">If you reach a quota cap, hello default limit of a resource in a subscription can be increased up tooa maximum limit, as described in [Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span></span>

<span data-ttu-id="d2fb6-125">Estos pasos muestra cómo toorequest una cuota aumentar a través de hello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="d2fb6-125">These steps show you how toorequest a quota increase through hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="d2fb6-126">Seleccione **Más servicios**, **Facturación**, y **Uso y cuotas**.</span><span class="sxs-lookup"><span data-stu-id="d2fb6-126">Select **More Services**, select **Billing**, and then select **Usage + quotas**.</span></span>
1. <span data-ttu-id="d2fb6-127">En Hola uso + hoja de cuotas, seleccione hello **solicitar aumentar** botón.</span><span class="sxs-lookup"><span data-stu-id="d2fb6-127">In hello Usage + quotas blade, select hello **Request Increase** button.</span></span>

   ![Botón Solicitar aumento](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. <span data-ttu-id="d2fb6-129">toocomplete y enviar solicitud de hello, rellene la información de hello necesario en todas las tres pestañas de hello **nueva solicitud de soporte técnico** formulario.</span><span class="sxs-lookup"><span data-stu-id="d2fb6-129">toocomplete and submit hello request, fill out hello required information on all three tabs of hello **New support request** form.</span></span>

   ![Formulario Solicitar aumento](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

<span data-ttu-id="d2fb6-131">[Límites de Azure de descripción y aumenta](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) proporciona más información acerca de cómo ponerse en contacto con soporte técnico de Azure toorequest una cuota de aumento.</span><span class="sxs-lookup"><span data-stu-id="d2fb6-131">[Understanding Azure Limits and Increases](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) provides more information about contacting Azure support toorequest a quota increase.</span></span>



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a><span data-ttu-id="d2fb6-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d2fb6-132">Next steps</span></span>
* <span data-ttu-id="d2fb6-133">Explorar hello [Galería de plantillas de desarrollo y pruebas laboratorios Azure Resource Manager QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="d2fb6-133">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span></span>
