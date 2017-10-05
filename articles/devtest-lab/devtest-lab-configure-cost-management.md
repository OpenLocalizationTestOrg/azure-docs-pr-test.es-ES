---
title: "Visualización de las tendencias de costos mensuales estimados de laboratorio en Azure DevTest Labs | Microsoft Docs"
description: "Aprenda sobre el gráfico de tendencias de costos mensuales estimados de Azure DevTest Labs."
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
ms.openlocfilehash: b3ad1ead522908d4b41b7cca98d20ac91664998e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="view-the-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a><span data-ttu-id="b0e11-103">Visualización de las tendencias de costos mensuales estimados de laboratorio en Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="b0e11-103">View the monthly estimated lab cost trend in Azure DevTest Labs</span></span>
<span data-ttu-id="b0e11-104">La característica de administración de costos de Laboratorios de desarrollo y pruebas le ayuda a controlar el costo del laboratorio.</span><span class="sxs-lookup"><span data-stu-id="b0e11-104">The Cost Management feature of DevTest Labs helps you track the cost of your lab.</span></span> <span data-ttu-id="b0e11-105">En este artículo se muestra el uso del gráfico **Monthly Estimated Cost Trend** (Tendencia de costos estimados mensuales) para ver el costo estimado hasta la fecha del mes de calendario actual, así como el costo a fin de mes previsto para el mes de calendario actual.</span><span class="sxs-lookup"><span data-stu-id="b0e11-105">This article illustrates how to use the **Monthly Estimated Cost Trend** chart to view the current calendar month's estimated cost-to-date and the projected end-of-month cost for the current calendar month.</span></span> <span data-ttu-id="b0e11-106">En él aprenderá a ver el gráfico de tendencias de costos mensuales estimados en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b0e11-106">In this article, you learn how to view the monthly estimated cost trend chart in the Azure portal.</span></span>

## <a name="viewing-the-monthly-estimated-cost-trend-chart"></a><span data-ttu-id="b0e11-107">Visualización del gráfico de tendencias de costo estimado mensual</span><span class="sxs-lookup"><span data-stu-id="b0e11-107">Viewing the Monthly Estimated Cost Trend chart</span></span>
<span data-ttu-id="b0e11-108">Para ver el gráfico de tendencias de costos mensuales estimados, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="b0e11-108">To view the Monthly Estimated Cost Trend chart, follow these steps:</span></span> 

1. <span data-ttu-id="b0e11-109">Inicie sesión en el [Portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="b0e11-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="b0e11-110">Seleccione **Más servicios** y, luego, **DevTest Labs** en la lista.</span><span class="sxs-lookup"><span data-stu-id="b0e11-110">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="b0e11-111">En la lista de laboratorios, seleccione el laboratorio que desee.</span><span class="sxs-lookup"><span data-stu-id="b0e11-111">From the list of labs, select the desired lab.</span></span>   
4. <span data-ttu-id="b0e11-112">En la hoja del laboratorio, seleccione **Cost settings**(Configuración de costos).</span><span class="sxs-lookup"><span data-stu-id="b0e11-112">On the lab's blade, select **Cost settings**.</span></span>
5. <span data-ttu-id="b0e11-113">En la hoja **Configuración de costo** del laboratorio, seleccione **Tendencia de costos mensual**.</span><span class="sxs-lookup"><span data-stu-id="b0e11-113">On the lab's **Cost settings** blade, select **Lab cost trend**.</span></span>
6. <span data-ttu-id="b0e11-114">La siguiente captura de pantalla muestra un ejemplo de gráfico de costos.</span><span class="sxs-lookup"><span data-stu-id="b0e11-114">The following screen shot shows an example of a cost chart.</span></span> 
   
    ![Gráfico de costos](./media/devtest-lab-configure-cost-management/graph.png)

<span data-ttu-id="b0e11-116">El valor **Costo estimado** es el costo estimado hasta la fecha del mes de calendario actual.</span><span class="sxs-lookup"><span data-stu-id="b0e11-116">The **Estimated cost** value is the current calendar month's estimated cost-to-date.</span></span> <span data-ttu-id="b0e11-117">El valor de **Projected cost** (Costo previsto) es el costo estimado para el mes de calendario actual completo, calculado con el costo de laboratorio para los cinco días anteriores.</span><span class="sxs-lookup"><span data-stu-id="b0e11-117">The **Projected cost** is the estimated cost for the entire current calendar month, calculated using the lab cost for the previous five days.</span></span>

<span data-ttu-id="b0e11-118">Los importes de los costos se redondean al siguiente número entero.</span><span class="sxs-lookup"><span data-stu-id="b0e11-118">The cost amounts are rounded up to the next whole number.</span></span> <span data-ttu-id="b0e11-119">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b0e11-119">For example:</span></span> 

* <span data-ttu-id="b0e11-120">5,01 se redondea a 6.</span><span class="sxs-lookup"><span data-stu-id="b0e11-120">5.01 rounds up to 6</span></span> 
* <span data-ttu-id="b0e11-121">5,50 se redondea a 6.</span><span class="sxs-lookup"><span data-stu-id="b0e11-121">5.50 rounds up to 6</span></span>
* <span data-ttu-id="b0e11-122">5,99 se redondea a 6.</span><span class="sxs-lookup"><span data-stu-id="b0e11-122">5.99 rounds up to 6</span></span>

<span data-ttu-id="b0e11-123">Como indica anteriormente el gráfico, los costos que se ven en el gráfico son costos *estimados* con tarifas de oferta de [Pago por uso](https://azure.microsoft.com/offers/ms-azr-0003p/) .</span><span class="sxs-lookup"><span data-stu-id="b0e11-123">As it states above the chart, the costs you see in the chart are *estimated* costs using [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) offer rates.</span></span>
<span data-ttu-id="b0e11-124">Además, en el cálculo de costos *no* se incluye lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b0e11-124">Additionally, the following are *not* included in the cost calculation:</span></span>

* <span data-ttu-id="b0e11-125">Actualmente no se admiten suscripciones de DreamSpark y CSP, puesto que Azure DevTest Labs emplea las [API de facturación de Azure](../billing/billing-usage-rate-card-overview.md) para calcular el costo de laboratorio, y estas suscripciones no las admiten.</span><span class="sxs-lookup"><span data-stu-id="b0e11-125">CSP and Dreamspark subscriptions are currently not supported as Azure DevTest Labs uses the [Azure billing APIs](../billing/billing-usage-rate-card-overview.md) to calculate the lab cost, which does not support CSP or Dreamspark subscriptions.</span></span>
* <span data-ttu-id="b0e11-126">Las tarifas de su oferta.</span><span class="sxs-lookup"><span data-stu-id="b0e11-126">Your offer rates.</span></span> <span data-ttu-id="b0e11-127">Actualmente, no es posible usar las tarifas de su oferta (que aparecen en su suscripción) negociadas con Microsoft o con asociados de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b0e11-127">Currently, we are not able to use your offer rates (shown under your subscription) that you have negotiated with Microsoft or Microsoft partners.</span></span> <span data-ttu-id="b0e11-128">Se usan tarifas de pago por uso.</span><span class="sxs-lookup"><span data-stu-id="b0e11-128">We are using Pay-As-You-Go rates.</span></span>
* <span data-ttu-id="b0e11-129">Los impuestos</span><span class="sxs-lookup"><span data-stu-id="b0e11-129">Your taxes</span></span>
* <span data-ttu-id="b0e11-130">Los descuentos</span><span class="sxs-lookup"><span data-stu-id="b0e11-130">Your discounts</span></span>
* <span data-ttu-id="b0e11-131">La divisa de facturación.</span><span class="sxs-lookup"><span data-stu-id="b0e11-131">Your billing currency.</span></span> <span data-ttu-id="b0e11-132">Actualmente, el costo de laboratorio solo se muestra en divisa USD.</span><span class="sxs-lookup"><span data-stu-id="b0e11-132">Currently, the lab cost is displayed only in USD currency.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="b0e11-133">Entradas blogs relacionadas</span><span class="sxs-lookup"><span data-stu-id="b0e11-133">Related blog posts</span></span>
* [<span data-ttu-id="b0e11-134">Two more things to keep your cost on track in DevTest Labs (Dos cosas para mantener el costo por el buen camino en DevTest Labs)</span><span class="sxs-lookup"><span data-stu-id="b0e11-134">Two more things to keep your cost on track in DevTest Labs</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [<span data-ttu-id="b0e11-135">Why Cost Thresholds? (¿Por qué los umbrales de costo?)</span><span class="sxs-lookup"><span data-stu-id="b0e11-135">Why Cost Thresholds?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a><span data-ttu-id="b0e11-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b0e11-136">Next steps</span></span>
<span data-ttu-id="b0e11-137">Vea algunas acciones que puede probar a continuación:</span><span class="sxs-lookup"><span data-stu-id="b0e11-137">Here are some things to try next:</span></span>

* <span data-ttu-id="b0e11-138">[Definición de directivas de laboratorio](devtest-lab-set-lab-policy.md): obtenga información sobre cómo establecer las distintas directivas que se emplean para controlar el uso del laboratorio y sus máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="b0e11-138">[Define lab policies](devtest-lab-set-lab-policy.md) - Learn how to set the various policies used to govern how your lab and its VMs are used.</span></span> 
* <span data-ttu-id="b0e11-139">[Creación de una imagen personalizada](devtest-lab-create-template.md): cuando cree una máquina virtual, tendrá que especificar una base, que puede ser una imagen personalizada o una imagen de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b0e11-139">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="b0e11-140">Este artículo muestra cómo crear una imagen personalizada desde un archivo VHD.</span><span class="sxs-lookup"><span data-stu-id="b0e11-140">This article illustrates how to create a custom image from a VHD file.</span></span>
* <span data-ttu-id="b0e11-141">[Configuración de imágenes de Marketplace](devtest-lab-configure-marketplace-images.md): DevTest Labs admite la creación de máquinas virtuales basadas en imágenes de Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b0e11-141">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="b0e11-142">En este artículo se muestra cómo especificar las imágenes de Azure Marketplace, si corresponde, que se pueden usar en el momento de crear máquinas virtuales en un laboratorio.</span><span class="sxs-lookup"><span data-stu-id="b0e11-142">This article illustrates how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="b0e11-143">[Creación de una máquina virtual en un laboratorio](devtest-lab-add-vm-with-artifacts.md): se muestra cómo crear una máquina virtual desde una imagen base (ya sea personalizada o de Marketplace) y cómo trabajar con artefactos en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b0e11-143">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how to create a VM from a base image (either custom or Marketplace), and how to work with artifacts in your VM.</span></span>

