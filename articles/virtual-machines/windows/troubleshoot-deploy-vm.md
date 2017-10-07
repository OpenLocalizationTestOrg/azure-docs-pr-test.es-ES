---
title: "aaaTroubleshoot implementar problemas de la máquina virtual de Windows de Azure | Documentos de Microsoft"
description: "Solución de problemas de implementación de máquinas virtuales Windows en el modelo de implementación de Azure Resource Manager"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: genli
ms.openlocfilehash: 30de25827c050cc266761cfc14548bcc64237dac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-windows-virtual-machine-issues-in-azure"></a><span data-ttu-id="5db3e-103">Solución de problemas de implementación de máquinas virtuales Windows en Azure</span><span class="sxs-lookup"><span data-stu-id="5db3e-103">Troubleshoot deploying Windows virtual machine issues in Azure</span></span>

<span data-ttu-id="5db3e-104">problemas de implementación de máquina virtual (VM) de tootroubleshoot en Azure, revise hello [problemas principales](#top-issues) para las soluciones y los errores comunes.</span><span class="sxs-lookup"><span data-stu-id="5db3e-104">tootroubleshoot virtual machine (VM) deployment issues in Azure, review hello [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="5db3e-105">Si necesita más ayuda en cualquier momento en este artículo, puede ponerse en contacto con hello Azure expertos en [Hola foros de Azure de MSDN y el desbordamiento de la pila](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="5db3e-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="5db3e-106">Como alternativa, puede registrar un incidente de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="5db3e-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="5db3e-107">Vaya toohello [sitio de soporte técnico de Azure](https://azure.microsoft.com/support/options/) y seleccione **obtener admiten**.</span><span class="sxs-lookup"><span data-stu-id="5db3e-107">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="5db3e-108">Principales problemas</span><span class="sxs-lookup"><span data-stu-id="5db3e-108">Top issues</span></span>
[!INCLUDE [virtual-machines-windows-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a><span data-ttu-id="5db3e-109">no admiten clústeres de Hola Hola solicitado tamaño de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="5db3e-109">hello cluster cannot support hello requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="5db3e-110">Vuelva a intentar la solicitud Hola con un tamaño más pequeño de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5db3e-110">Retry hello request using a smaller VM size.</span></span>
- <span data-ttu-id="5db3e-111">Si hello tamaño de hello solicitada que no se puede cambiar la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="5db3e-111">If hello size of hello requested VM cannot be changed:</span></span>
    - <span data-ttu-id="5db3e-112">Detener todas las máquinas virtuales de hello en el conjunto de disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="5db3e-112">Stop all hello VMs in hello availability set.</span></span> <span data-ttu-id="5db3e-113">Haga clic en **Grupos de recursos** > su grupo de recursos > **Recursos** > su conjunto de disponibilidad > **Máquinas virtuales** > su máquina virtual > **Detener**.</span><span class="sxs-lookup"><span data-stu-id="5db3e-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="5db3e-114">Después de que todos Hola detener las máquinas virtuales, crear Hola VM en el tamaño de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="5db3e-114">After all hello VMs stop, create hello VM in hello desired size.</span></span>
    - <span data-ttu-id="5db3e-115">Iniciar Hola nueva máquina virtual en primer lugar y, a continuación, seleccione cada uno de hello detiene las máquinas virtuales y haga clic en Inicio.</span><span class="sxs-lookup"><span data-stu-id="5db3e-115">Start hello new VM first, and then select each of hello stopped VMs and click Start.</span></span>


## <a name="hello-cluster-does-not-have-free-resources"></a><span data-ttu-id="5db3e-116">Hola clúster no tiene recursos libres</span><span class="sxs-lookup"><span data-stu-id="5db3e-116">hello cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="5db3e-117">Reintentar solicitud de hello más tarde.</span><span class="sxs-lookup"><span data-stu-id="5db3e-117">Retry hello request later.</span></span>
- <span data-ttu-id="5db3e-118">Si puede hello nueva máquina virtual se establecer parte de una disponibilidad diferentes</span><span class="sxs-lookup"><span data-stu-id="5db3e-118">If hello new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="5db3e-119">Crear una máquina virtual en un conjunto de disponibilidad diferentes (Hola misma región).</span><span class="sxs-lookup"><span data-stu-id="5db3e-119">Create a VM in a different availability set (in hello same region).</span></span>
    - <span data-ttu-id="5db3e-120">Agregar Hola nueva VM toohello misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="5db3e-120">Add hello new VM toohello same virtual network.</span></span>

## <a name="how-can-i-use-and-deploy-a-windows-client-image-into-azure"></a><span data-ttu-id="5db3e-121">¿Cómo puedo usar e implementar una imagen de cliente de Windows en Azure?</span><span class="sxs-lookup"><span data-stu-id="5db3e-121">How can I use and deploy a windows client image into Azure?</span></span>

<span data-ttu-id="5db3e-122">Puede usar Windows 7, Windows 8 o Windows 10 en Azure para escenarios de desarrollo y pruebas siempre que tenga una suscripción adecuada a Visual Studio (anteriormente MSDN).</span><span class="sxs-lookup"><span data-stu-id="5db3e-122">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios if you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> <span data-ttu-id="5db3e-123">Esto [artículo](client-images.md) contornos Hola requisitos de elegibilidad para ejecutar el cliente de Windows en Azure y usos de hello imágenes de la Galería de Azure.</span><span class="sxs-lookup"><span data-stu-id="5db3e-123">This [article](client-images.md) outlines hello eligibility requirements for running Windows client in Azure and uses of hello Azure Gallery images.</span></span>

## <a name="how-can-i-deploy-a-virtual-machine-using-hello-hybrid-use-benefit-hub"></a><span data-ttu-id="5db3e-124">¿Cómo puedo implementar una máquina virtual mediante Hola híbrida uso beneficio (concentrador)?</span><span class="sxs-lookup"><span data-stu-id="5db3e-124">How can I deploy a virtual machine using hello Hybrid Use Benefit (HUB)?</span></span>

<span data-ttu-id="5db3e-125">Hay un par de maneras diferentes toodeploy Windows máquinas virtuales Hola ventaja de usar híbrida de Azure.</span><span class="sxs-lookup"><span data-stu-id="5db3e-125">There are a couple of different ways toodeploy Windows virtual machines with hello Azure Hybrid Use Benefit.</span></span>

<span data-ttu-id="5db3e-126">Con una suscripción con un contrato Enterprise:</span><span class="sxs-lookup"><span data-stu-id="5db3e-126">For an Enterprise Agreement subscription:</span></span>

<span data-ttu-id="5db3e-127">•  Implementar máquinas virtuales desde imágenes de Marketplace específicas que estén preconfiguradas con la ventaja de uso híbrido de Azure.</span><span class="sxs-lookup"><span data-stu-id="5db3e-127">•   Deploy VMs from specific Marketplace images that are pre-configured with Azure Hybrid Use Benefit.</span></span>

<span data-ttu-id="5db3e-128">Con el contrato Enterprise:</span><span class="sxs-lookup"><span data-stu-id="5db3e-128">For Enterprise agreement:</span></span>

<span data-ttu-id="5db3e-129">•  Cargar una máquina virtual personalizada e implementar mediante una plantilla de Resource Manager o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5db3e-129">•   Upload a custom VM and deploy using a Resource Manager template or Azure PowerShell.</span></span>

<span data-ttu-id="5db3e-130">Para obtener más información, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="5db3e-130">For more information, see hello following resources:</span></span>

 - [<span data-ttu-id="5db3e-131">Información general sobre la ventaja de uso híbrido de Azure</span><span class="sxs-lookup"><span data-stu-id="5db3e-131">Azure Hybrid Use Benefit overview </span></span>](https://azure.microsoft.com/pricing/hybrid-use-benefit/)

 - [<span data-ttu-id="5db3e-132">Preguntas más frecuentes descargables</span><span class="sxs-lookup"><span data-stu-id="5db3e-132">Downloadable FAQ</span></span>](http://download.microsoft.com/download/4/2/1/4211AC94-D607-4A45-B472-4B30EDF437DE/Windows_Server_Azure_Hybrid_Use_FAQ_EN_US.pdf)

 - <span data-ttu-id="5db3e-133">[Ventaja de uso híbrido de Azure para Windows Server y cliente de Windows](hybrid-use-benefit-licensing.md).</span><span class="sxs-lookup"><span data-stu-id="5db3e-133">[Azure Hybrid Use Benefit for Windows Server and Windows Client](hybrid-use-benefit-licensing.md).</span></span>

 - [<span data-ttu-id="5db3e-134">¿Cómo puedo utilizar Hola ventaja de usar híbridas en Azure</span><span class="sxs-lookup"><span data-stu-id="5db3e-134">How can I use hello Hybrid Use Benefit in Azure</span></span>](https://blogs.msdn.microsoft.com/azureedu/2016/04/13/how-can-i-use-the-hybrid-use-benefit-in-azure)

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="5db3e-135">Cómo se activa mi crédito mensual para Visual Studio Enterprise (BizSpark)</span><span class="sxs-lookup"><span data-stu-id="5db3e-135">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="5db3e-136">tooactivate su mensual del crédito, vea este [artículo](https://azure.microsoft.com/offers/ms-azr-0064p/).</span><span class="sxs-lookup"><span data-stu-id="5db3e-136">tooactivate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="how-tooadd-enterprise-devtest-toomy-enterprise-agreement-ea-tooget-access-toowindow-client-images"></a><span data-ttu-id="5db3e-137">¿Cómo tooadd Enterprise para desarrollo/pruebas toomy contrato Enterprise (EA) tooget acceder a imágenes de cliente tooWindow?</span><span class="sxs-lookup"><span data-stu-id="5db3e-137">How tooadd Enterprise Dev/Test toomy Enterprise Agreement (EA) tooget access tooWindow client images?</span></span>

<span data-ttu-id="5db3e-138">suscripciones de toocreate de capacidad de Hello basadas en hello Enterprise para desarrollo/pruebas ofrecen es propietarios tooAccount restringido que se han concedido permiso toodo es así por un administrador de empresa.</span><span class="sxs-lookup"><span data-stu-id="5db3e-138">hello ability toocreate subscriptions based on hello Enterprise Dev/Test offer is restricted tooAccount Owners who have been given permission toodo so by an Enterprise Administrator.</span></span> <span data-ttu-id="5db3e-139">Propietario de la cuenta de Hello crea suscripciones a través de hello Portal de cuentas de Azure y, a continuación, debe agregar los suscriptores activos de Visual Studio como coadministradores.</span><span class="sxs-lookup"><span data-stu-id="5db3e-139">hello Account Owner creates subscriptions via hello Azure Account Portal, and then should add active Visual Studio subscribers as co-administrators.</span></span> <span data-ttu-id="5db3e-140">Por lo que pueden administrar y utilizar recursos de hello necesarios para desarrollo y pruebas.</span><span class="sxs-lookup"><span data-stu-id="5db3e-140">So that they can manage and use hello resources needed for development and testing.</span></span> <span data-ttu-id="5db3e-141">Para más información, consulte [Desarrollo/pruebas - Enterprise](https://azure.microsoft.com/offers/ms-azr-0148p/).</span><span class="sxs-lookup"><span data-stu-id="5db3e-141">For more information, see [Enterprise Dev/Test](https://azure.microsoft.com/offers/ms-azr-0148p/).</span></span>

## <a name="my-drivers-are-missing-for-my-windows-n-series-vm"></a><span data-ttu-id="5db3e-142">Faltan los controladores para mi máquina virtual de la serie N de Windows</span><span class="sxs-lookup"><span data-stu-id="5db3e-142">My drivers are missing for my Windows N-Series VM</span></span>

<span data-ttu-id="5db3e-143">Los controladores para las máquinas virtuales basadas en Windows se encuentran [aquí](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="5db3e-143">Drivers for Windows-based VMs are located [here](n-series-driver-setup.md).</span></span>

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="5db3e-144">No puedo encontrar una instancia de la GPU en mi máquina virtual de la serie N</span><span class="sxs-lookup"><span data-stu-id="5db3e-144">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="5db3e-145">tootake aprovechar las capacidades GPU de Hola de Azure N-series máquinas virtuales que ejecutan Windows Server 2016 o Windows Server 2012 R2, debe instalar a los controladores de gráficos NVIDIA en cada máquina virtual después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="5db3e-145">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="5db3e-146">La información de instalación del controlador está disponible para las [máquinas virtuales Windows](n-series-driver-setup.md) y las [máquinas virtuales Linux](../linux/n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="5db3e-146">Driver setup information is available for [Windows VMs](n-series-driver-setup.md) and [Linux VMs](../linux/n-series-driver-setup.md).</span></span>

## <a name="are-client-images-supported-for-n-series"></a><span data-ttu-id="5db3e-147">¿Se admiten imágenes de cliente para la serie N?</span><span class="sxs-lookup"><span data-stu-id="5db3e-147">Are client images supported for N-Series?</span></span>

<span data-ttu-id="5db3e-148">Actualmente, Azure solo admite la serie N en las máquinas virtuales que ejecutan los sistemas operativos Windows Server o Linux.</span><span class="sxs-lookup"><span data-stu-id="5db3e-148">Currently, Azure only supports N-Series on VMs running Windows Server and Linux operating systems.</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="5db3e-149">¿Hay máquinas virtuales de la serie N en mi región?</span><span class="sxs-lookup"><span data-stu-id="5db3e-149">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="5db3e-150">Puede consultar la disponibilidad de Hola de hello [productos disponibles por tabla region](https://azure.microsoft.com/regions/services)y el precio de [aquí](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span><span class="sxs-lookup"><span data-stu-id="5db3e-150">You can check hello availability from hello [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="what-client-images-can-i-use-and-deploy-in-azure-and-how-tooi-get-them"></a><span data-ttu-id="5db3e-151">¿Qué imágenes de cliente puedo usar e implementar en Azure y cómo tooI obténgalos?</span><span class="sxs-lookup"><span data-stu-id="5db3e-151">What client images can I use and deploy in Azure, and how tooI get them?</span></span>

<span data-ttu-id="5db3e-152">Puede usar Windows 7, Windows 8 o Windows 10 en Azure para escenarios de desarrollo y pruebas siempre que tenga una suscripción adecuada a Visual Studio (anteriormente MSDN).</span><span class="sxs-lookup"><span data-stu-id="5db3e-152">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios provided you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> 

- <span data-ttu-id="5db3e-153">Imágenes de Windows 10 están disponibles desde la Galería de Azure de hello en [ofrece apto para desarrollo y pruebas](client-images.md#eligible-offers).</span><span class="sxs-lookup"><span data-stu-id="5db3e-153">Windows 10 images are available from hello Azure Gallery within [eligible dev/test offers](client-images.md#eligible-offers).</span></span> 
- <span data-ttu-id="5db3e-154">Visual Studio los suscriptores dentro de cualquier tipo de oferta pueden también [adecuadamente preparar y crear](prepare-for-upload-vhd-image.md) una imagen de Windows 7, Windows 8 o Windows 10 de 64 bits y, a continuación, [cargar tooAzure](upload-generalized-managed.md).</span><span class="sxs-lookup"><span data-stu-id="5db3e-154">Visual Studio subscribers within any type of offer can also [adequately prepare and create](prepare-for-upload-vhd-image.md) a 64-bit Windows 7, Windows 8, or Windows 10 image and then [upload tooAzure](upload-generalized-managed.md).</span></span> <span data-ttu-id="5db3e-155">uso de Hello sigue siendo toodev/prueba limitada por los suscriptores activos de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5db3e-155">hello use remains limited toodev/test by active Visual Studio subscribers.</span></span>

<span data-ttu-id="5db3e-156">Esto [artículo](client-images.md) contornos Hola requisitos de elegibilidad para ejecutar el cliente de Windows en Azure y el uso de hello imágenes de la Galería de Azure.</span><span class="sxs-lookup"><span data-stu-id="5db3e-156">This [article](client-images.md) outlines hello eligibility requirements for running Windows client in Azure and use of hello Azure Gallery images.</span></span>

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="5db3e-157">No estoy toosee capaz de familia de tamaño de máquina virtual que desea al cambiar el tamaño de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5db3e-157">I am not able toosee VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="5db3e-158">Cuando una máquina virtual se está ejecutando, es el servidor físico tooa implementado.</span><span class="sxs-lookup"><span data-stu-id="5db3e-158">When a VM is running, it is deployed tooa physical server.</span></span> <span data-ttu-id="5db3e-159">servidores físicos de Hello en regiones de Azure se agrupan en clústeres de hardware físico comunes.</span><span class="sxs-lookup"><span data-stu-id="5db3e-159">hello physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="5db3e-160">Cambiar el tamaño de una máquina virtual que requiere clústeres de hardware de hello VM toobe movido toodifferent es diferente en función de qué modelo de implementación se usa toodeploy Hola VM.</span><span class="sxs-lookup"><span data-stu-id="5db3e-160">Resizing a VM that requires hello VM toobe moved toodifferent hardware clusters is different depending on which deployment model was used toodeploy hello VM.</span></span>

- <span data-ttu-id="5db3e-161">Máquinas virtuales implementadas en el modelo de implementación clásico, implementación del servicio de nube de hello deben quitarse y volver a implementar las máquinas virtuales tooa tamaño de toochange Hola de otra familia de tamaño.</span><span class="sxs-lookup"><span data-stu-id="5db3e-161">VMs deployed in Classic deployment model, hello cloud service deployment must be removed and redeployed toochange hello VMs tooa size in another size family.</span></span>

- <span data-ttu-id="5db3e-162">Máquinas virtuales implementadas en el modelo de implementación de administrador de recursos, debe detener todas las máquinas virtuales en conjunto antes de cambiar el tamaño de Hola de cualquier máquina virtual en el conjunto de disponibilidad de Hola de disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="5db3e-162">VMs deployed in Resource Manager deployment model, you must stop all VMs in hello availability set before changing hello size of any VM in hello availability set.</span></span>

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="5db3e-163">Hello lista tamaño de máquina virtual no se admite mientras se implementa en el conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="5db3e-163">hello listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="5db3e-164">Elija un tamaño que es compatible con clúster del conjunto de disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="5db3e-164">Choose a size that is supported on hello availability set's cluster.</span></span> <span data-ttu-id="5db3e-165">Se recomienda al crear que un conjunto de disponibilidad toochoose Hola mayor tamaño de máquina virtual piensa que necesita y tiene que ser el primer toohello de implementación de conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="5db3e-165">It is recommended when creating an availability set toochoose hello largest VM size you think you need, and have that be your first deployment toohello Availability set.</span></span>

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a><span data-ttu-id="5db3e-166">¿Puedo agregar un conjunto de disponibilidad de tooan clásico VM existente?</span><span class="sxs-lookup"><span data-stu-id="5db3e-166">Can I add an existing Classic VM tooan availability set?</span></span>

<span data-ttu-id="5db3e-167">Sí.</span><span class="sxs-lookup"><span data-stu-id="5db3e-167">Yes.</span></span> <span data-ttu-id="5db3e-168">Puede agregar una existente tooa VM clásico nueva o conjunto de disponibilidad existentes.</span><span class="sxs-lookup"><span data-stu-id="5db3e-168">You can add an existing classic VM tooa new or existing Availability Set.</span></span> <span data-ttu-id="5db3e-169">Para obtener más información, consulte [agrega un conjunto de disponibilidad de tooan de máquina virtual existente](classic/configure-availability.md#addmachine).</span><span class="sxs-lookup"><span data-stu-id="5db3e-169">For more information see [Add an existing virtual machine tooan availability set](classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="5db3e-170">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5db3e-170">Next steps</span></span>
<span data-ttu-id="5db3e-171">Si necesita más ayuda en cualquier momento en este artículo, puede ponerse en contacto con hello Azure expertos en [Hola foros de Azure de MSDN y el desbordamiento de la pila](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="5db3e-171">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="5db3e-172">Como alternativa, puede registrar un incidente de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="5db3e-172">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="5db3e-173">Vaya toohello [sitio de soporte técnico de Azure](https://azure.microsoft.com/support/options/) y seleccione **obtener admiten**.</span><span class="sxs-lookup"><span data-stu-id="5db3e-173">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
