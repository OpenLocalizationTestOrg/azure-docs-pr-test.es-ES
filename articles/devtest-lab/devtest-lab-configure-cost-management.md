---
title: tendencia de costo laboratorio estimado mensual de aaaView de hello en los laboratorios de desarrollo y pruebas de Azure | Documentos de Microsoft
description: "Obtenga información sobre el gráfico de tendencias de coste estimado mensual de hello laboratorios de desarrollo y pruebas de Azure."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1f46fdc5-d917-46e3-a1ea-f6dd41212ba4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 47c7dd4cf91b76de74b502c50f05e79cd501ee35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="view-hello-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a><span data-ttu-id="6be7d-103">Tendencia de costo laboratorio estimado mensual de vista de hello en los laboratorios de desarrollo y pruebas de Azure</span><span class="sxs-lookup"><span data-stu-id="6be7d-103">View hello monthly estimated lab cost trend in Azure DevTest Labs</span></span>
<span data-ttu-id="6be7d-104">característica de administración de costos de Hola de laboratorios de desarrollo y pruebas le ayuda a controlar el costo de hello del laboratorio.</span><span class="sxs-lookup"><span data-stu-id="6be7d-104">hello Cost Management feature of DevTest Labs helps you track hello cost of your lab.</span></span> <span data-ttu-id="6be7d-105">Este artículo se explica cómo hello toouse **tendencia de costo estimado mensual** tooview gráfico estimado costo hasta la fecha del mes natural actual de Hola y Hola costo proyectado de fin de mes de hello mes natural actual.</span><span class="sxs-lookup"><span data-stu-id="6be7d-105">This article illustrates how toouse hello **Monthly Estimated Cost Trend** chart tooview hello current calendar month's estimated cost-to-date and hello projected end-of-month cost for hello current calendar month.</span></span> <span data-ttu-id="6be7d-106">En este artículo, aprenderá cómo tooview Hola gráfico de tendencias de coste estimado mensual en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="6be7d-106">In this article, you learn how tooview hello monthly estimated cost trend chart in hello Azure portal.</span></span>

## <a name="viewing-hello-monthly-estimated-cost-trend-chart"></a><span data-ttu-id="6be7d-107">Ver gráfico de tendencia de costo mensual estimado Hola</span><span class="sxs-lookup"><span data-stu-id="6be7d-107">Viewing hello Monthly Estimated Cost Trend chart</span></span>
<span data-ttu-id="6be7d-108">Hola tooview gráfico de tendencia de costo mensual estimado, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="6be7d-108">tooview hello Monthly Estimated Cost Trend chart, follow these steps:</span></span> 

1. <span data-ttu-id="6be7d-109">Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="6be7d-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="6be7d-110">Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="6be7d-110">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="6be7d-111">En lista de Hola de laboratorios, seleccione laboratorio deseado Hola.</span><span class="sxs-lookup"><span data-stu-id="6be7d-111">From hello list of labs, select hello desired lab.</span></span>   
4. <span data-ttu-id="6be7d-112">En la hoja del laboratorio de hello, seleccione **costo configuración**.</span><span class="sxs-lookup"><span data-stu-id="6be7d-112">On hello lab's blade, select **Cost settings**.</span></span>
5. <span data-ttu-id="6be7d-113">En el laboratorio de hello **costo configuración** hoja, seleccione **tendencia de costo de laboratorio**.</span><span class="sxs-lookup"><span data-stu-id="6be7d-113">On hello lab's **Cost settings** blade, select **Lab cost trend**.</span></span>
6. <span data-ttu-id="6be7d-114">Hello captura de pantalla siguiente muestra un ejemplo de un gráfico de costo.</span><span class="sxs-lookup"><span data-stu-id="6be7d-114">hello following screen shot shows an example of a cost chart.</span></span> 
   
    ![Gráfico de costos](./media/devtest-lab-configure-cost-management/graph.png)

<span data-ttu-id="6be7d-116">Hola **costo estimado** valor es Hola estimado costo hasta la fecha del mes natural actual.</span><span class="sxs-lookup"><span data-stu-id="6be7d-116">hello **Estimated cost** value is hello current calendar month's estimated cost-to-date.</span></span> <span data-ttu-id="6be7d-117">Hola **costo previsto** se hello costo estimado de toda Hola mes actual del calendario, calcula con costo de laboratorio de Hola para hello cinco días anteriores.</span><span class="sxs-lookup"><span data-stu-id="6be7d-117">hello **Projected cost** is hello estimated cost for hello entire current calendar month, calculated using hello lab cost for hello previous five days.</span></span>

<span data-ttu-id="6be7d-118">Hola costo cantidades se redondean hacia arriba toohello siguiente número de entero.</span><span class="sxs-lookup"><span data-stu-id="6be7d-118">hello cost amounts are rounded up toohello next whole number.</span></span> <span data-ttu-id="6be7d-119">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6be7d-119">For example:</span></span> 

* <span data-ttu-id="6be7d-120">5.01 se redondea hacia arriba too6</span><span class="sxs-lookup"><span data-stu-id="6be7d-120">5.01 rounds up too6</span></span> 
* <span data-ttu-id="6be7d-121">5.50 se redondea hacia arriba too6</span><span class="sxs-lookup"><span data-stu-id="6be7d-121">5.50 rounds up too6</span></span>
* <span data-ttu-id="6be7d-122">5.99 se redondea hacia arriba too6</span><span class="sxs-lookup"><span data-stu-id="6be7d-122">5.99 rounds up too6</span></span>

<span data-ttu-id="6be7d-123">Como indica anteriormente gráfico hello, los costos de Hola que se ven en el gráfico de hello son *estimado* cuesta mediante [pago por uso](https://azure.microsoft.com/offers/ms-azr-0003p/) ofrecer tarifas.</span><span class="sxs-lookup"><span data-stu-id="6be7d-123">As it states above hello chart, hello costs you see in hello chart are *estimated* costs using [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) offer rates.</span></span>
<span data-ttu-id="6be7d-124">Además, es siguiente hello *no* incluido en el cálculo del costo de hello:</span><span class="sxs-lookup"><span data-stu-id="6be7d-124">Additionally, hello following are *not* included in hello cost calculation:</span></span>

* <span data-ttu-id="6be7d-125">Las suscripciones de Dreamspark y CSP no se admiten como laboratorios de desarrollo y pruebas de Azure usa hello [API de facturación de Azure](../billing/billing-usage-rate-card-overview.md) laboratorio de hello toocalculate un costo, que no admite las suscripciones de CSP o Dreamspark.</span><span class="sxs-lookup"><span data-stu-id="6be7d-125">CSP and Dreamspark subscriptions are currently not supported as Azure DevTest Labs uses hello [Azure billing APIs](../billing/billing-usage-rate-card-overview.md) toocalculate hello lab cost, which does not support CSP or Dreamspark subscriptions.</span></span>
* <span data-ttu-id="6be7d-126">Las tarifas de su oferta.</span><span class="sxs-lookup"><span data-stu-id="6be7d-126">Your offer rates.</span></span> <span data-ttu-id="6be7d-127">Actualmente, no es capaz de toouse las tarifas de oferta (se muestra en su suscripción) que se han negociado asociados con Microsoft o Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6be7d-127">Currently, we are not able toouse your offer rates (shown under your subscription) that you have negotiated with Microsoft or Microsoft partners.</span></span> <span data-ttu-id="6be7d-128">Se usan tarifas de pago por uso.</span><span class="sxs-lookup"><span data-stu-id="6be7d-128">We are using Pay-As-You-Go rates.</span></span>
* <span data-ttu-id="6be7d-129">Los impuestos</span><span class="sxs-lookup"><span data-stu-id="6be7d-129">Your taxes</span></span>
* <span data-ttu-id="6be7d-130">Los descuentos</span><span class="sxs-lookup"><span data-stu-id="6be7d-130">Your discounts</span></span>
* <span data-ttu-id="6be7d-131">La divisa de facturación.</span><span class="sxs-lookup"><span data-stu-id="6be7d-131">Your billing currency.</span></span> <span data-ttu-id="6be7d-132">Actualmente, el costo de laboratorio de Hola se muestra únicamente en la moneda USD.</span><span class="sxs-lookup"><span data-stu-id="6be7d-132">Currently, hello lab cost is displayed only in USD currency.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="6be7d-133">Entradas blogs relacionadas</span><span class="sxs-lookup"><span data-stu-id="6be7d-133">Related blog posts</span></span>
* [<span data-ttu-id="6be7d-134">Dos tookeep cosas más el costo por el buen camino en los laboratorios de desarrollo y pruebas</span><span class="sxs-lookup"><span data-stu-id="6be7d-134">Two more things tookeep your cost on track in DevTest Labs</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [<span data-ttu-id="6be7d-135">Why Cost Thresholds? (¿Por qué los umbrales de costo?)</span><span class="sxs-lookup"><span data-stu-id="6be7d-135">Why Cost Thresholds?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a><span data-ttu-id="6be7d-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6be7d-136">Next steps</span></span>
<span data-ttu-id="6be7d-137">A continuación le presentamos algunas tootry cosas:</span><span class="sxs-lookup"><span data-stu-id="6be7d-137">Here are some things tootry next:</span></span>

* <span data-ttu-id="6be7d-138">[Definir directivas de laboratorio](devtest-lab-set-lab-policy.md) -Obtenga información acerca de cómo tooset Hola varias directivas se usan toogovern cómo se usan el laboratorio y sus máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="6be7d-138">[Define lab policies](devtest-lab-set-lab-policy.md) - Learn how tooset hello various policies used toogovern how your lab and its VMs are used.</span></span> 
* <span data-ttu-id="6be7d-139">[Creación de una imagen personalizada](devtest-lab-create-template.md): cuando cree una máquina virtual, deberá especificar una base, que puede ser una imagen personalizada o una imagen de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6be7d-139">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="6be7d-140">Este artículo explica cómo toocreate personalizado de la imagen desde un archivo de disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="6be7d-140">This article illustrates how toocreate a custom image from a VHD file.</span></span>
* <span data-ttu-id="6be7d-141">[Configuración de imágenes de Marketplace](devtest-lab-configure-marketplace-images.md): DevTest Labs admite la creación de máquinas virtuales basadas en imágenes de Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6be7d-141">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="6be7d-142">Este artículo se explica cómo toospecify que, si lo hay, imágenes de Azure Marketplace se pueden usar al crear máquinas virtuales en un laboratorio.</span><span class="sxs-lookup"><span data-stu-id="6be7d-142">This article illustrates how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="6be7d-143">[Crear una máquina virtual en un laboratorio](devtest-lab-add-vm-with-artifacts.md) -ilustra cómo toocreate una máquina virtual desde una imagen base (ya sea personalizado o Marketplace) y cómo toowork con los artefactos en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6be7d-143">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how toocreate a VM from a base image (either custom or Marketplace), and how toowork with artifacts in your VM.</span></span>

