---
title: "aaaTroubleshoot implementar problemas de la máquina virtual de Linux de Azure | Documentos de Microsoft"
description: "Solución de problemas de implementación de la máquina virtual Linux en el modelo de implementación de Azure Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
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
ms.openlocfilehash: d1092ca3d9d51af7510b19c8c9a79e6dda588697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a><span data-ttu-id="9dead-103">Solución de problemas de implementación de la máquina virtual Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="9dead-103">Troubleshoot deploying Linux virtual machine issues in Azure</span></span>

<span data-ttu-id="9dead-104">problemas de implementación de máquina virtual (VM) de tootroubleshoot en Azure, revise hello [problemas principales](#top-issues) para las soluciones y los errores comunes.</span><span class="sxs-lookup"><span data-stu-id="9dead-104">tootroubleshoot virtual machine (VM) deployment issues in Azure, review hello [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="9dead-105">Si necesita más ayuda en cualquier momento en este artículo, puede ponerse en contacto con hello Azure expertos en [Hola foros de Azure de MSDN y el desbordamiento de la pila](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="9dead-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="9dead-106">Como alternativa, puede registrar un incidente de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="9dead-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="9dead-107">Vaya toohello [sitio de soporte técnico de Azure](https://azure.microsoft.com/support/options/) y seleccione **obtener admiten**.</span><span class="sxs-lookup"><span data-stu-id="9dead-107">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="9dead-108">Principales problemas</span><span class="sxs-lookup"><span data-stu-id="9dead-108">Top issues</span></span>
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a><span data-ttu-id="9dead-109">no admiten clústeres de Hola Hola solicitado tamaño de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9dead-109">hello cluster cannot support hello requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="9dead-110">Vuelva a intentar la solicitud Hola con un tamaño más pequeño de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9dead-110">Retry hello request using a smaller VM size.</span></span>
- <span data-ttu-id="9dead-111">Si hello tamaño de hello solicitada que no se puede cambiar la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="9dead-111">If hello size of hello requested VM cannot be changed:</span></span>
    - <span data-ttu-id="9dead-112">Detener todas las máquinas virtuales de hello en el conjunto de disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="9dead-112">Stop all hello VMs in hello availability set.</span></span> <span data-ttu-id="9dead-113">Haga clic en **Grupos de recursos** > su grupo de recursos > **Recursos** > su conjunto de disponibilidad > **Máquinas virtuales** > su máquina virtual > **Detener**.</span><span class="sxs-lookup"><span data-stu-id="9dead-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="9dead-114">Después de que todos Hola detener las máquinas virtuales, crear Hola VM en el tamaño de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="9dead-114">After all hello VMs stop, create hello VM in hello desired size.</span></span>
    - <span data-ttu-id="9dead-115">Iniciar Hola nueva máquina virtual en primer lugar y, a continuación, seleccione cada uno de hello detiene las máquinas virtuales y haga clic en Inicio.</span><span class="sxs-lookup"><span data-stu-id="9dead-115">Start hello new VM first, and then select each of hello stopped VMs and click Start.</span></span>


## <a name="hello-cluster-does-not-have-free-resources"></a><span data-ttu-id="9dead-116">Hola clúster no tiene recursos libres</span><span class="sxs-lookup"><span data-stu-id="9dead-116">hello cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="9dead-117">Reintentar solicitud de hello más tarde.</span><span class="sxs-lookup"><span data-stu-id="9dead-117">Retry hello request later.</span></span>
- <span data-ttu-id="9dead-118">Si puede hello nueva máquina virtual se establecer parte de una disponibilidad diferentes</span><span class="sxs-lookup"><span data-stu-id="9dead-118">If hello new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="9dead-119">Crear una máquina virtual en un conjunto de disponibilidad diferentes (Hola misma región).</span><span class="sxs-lookup"><span data-stu-id="9dead-119">Create a VM in a different availability set (in hello same region).</span></span>
    - <span data-ttu-id="9dead-120">Agregar Hola nueva VM toohello misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="9dead-120">Add hello new VM toohello same virtual network.</span></span>

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="9dead-121">Cómo se activa mi crédito mensual para Visual Studio Enterprise (BizSpark)</span><span class="sxs-lookup"><span data-stu-id="9dead-121">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="9dead-122">tooactivate su mensual del crédito, vea este [artículo](https://azure.microsoft.com/offers/ms-azr-0064p/).</span><span class="sxs-lookup"><span data-stu-id="9dead-122">tooactivate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="why-can-i-not-install-hello-gpu-driver-for-an-ubuntu-nv-vm"></a><span data-ttu-id="9dead-123">¿Por qué no puedo instalar controladores GPU de Hola para una máquina virtual NV de Ubuntu?</span><span class="sxs-lookup"><span data-stu-id="9dead-123">Why can I not install hello GPU driver for an Ubuntu NV VM?</span></span>

<span data-ttu-id="9dead-124">Actualmente, la compatibilidad con la GPU de Linux solo está disponible en las máquinas virtuales de Azure NC que ejecutan Ubuntu Server 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="9dead-124">Currently, Linux GPU support is only available on Azure NC VMs running Ubuntu Server 16.04 LTS.</span></span> <span data-ttu-id="9dead-125">Para más información consulte [Configuración de controladores de GPU para máquinas virtuales de la serie N con Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="9dead-125">For more information, see [Set up GPU drivers for N-series VMs running Linux](n-series-driver-setup.md).</span></span>

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a><span data-ttu-id="9dead-126">Faltan los controladores para mi máquina virtual de la serie N de Linux</span><span class="sxs-lookup"><span data-stu-id="9dead-126">My drivers are missing for my Linux N-Series VM</span></span>

<span data-ttu-id="9dead-127">Los controladores para las máquinas virtuales basadas en Linux se encuentran [aquí](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="9dead-127">Drivers for Linux-based VMs are located [here](n-series-driver-setup.md).</span></span> 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="9dead-128">No puedo encontrar una instancia de la GPU en mi máquina virtual de la serie N</span><span class="sxs-lookup"><span data-stu-id="9dead-128">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="9dead-129">tootake aprovechar las capacidades GPU de Hola de Azure N-series máquinas virtuales que ejecutan Windows Server 2016 o Windows Server 2012 R2, debe instalar a los controladores de gráficos NVIDIA en cada máquina virtual después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="9dead-129">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="9dead-130">La información de instalación del controlador está disponible para las [máquinas virtuales Windows](../windows/n-series-driver-setup.md) y las [máquinas virtuales Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="9dead-130">Driver setup information is available for [Windows VMs](../windows/n-series-driver-setup.md) and [Linux VMs](n-series-driver-setup.md).</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="9dead-131">¿Hay máquinas virtuales de la serie N en mi región?</span><span class="sxs-lookup"><span data-stu-id="9dead-131">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="9dead-132">Puede consultar la disponibilidad de Hola de hello [productos disponibles por tabla region](https://azure.microsoft.com/regions/services)y el precio de [aquí](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span><span class="sxs-lookup"><span data-stu-id="9dead-132">You can check hello availability from hello [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="9dead-133">No estoy toosee capaz de familia de tamaño de máquina virtual que desea al cambiar el tamaño de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9dead-133">I am not able toosee VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="9dead-134">Cuando una máquina virtual se está ejecutando, es el servidor físico tooa implementado.</span><span class="sxs-lookup"><span data-stu-id="9dead-134">When a VM is running, it is deployed tooa physical server.</span></span> <span data-ttu-id="9dead-135">servidores físicos de Hello en regiones de Azure se agrupan en clústeres de hardware físico comunes.</span><span class="sxs-lookup"><span data-stu-id="9dead-135">hello physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="9dead-136">Cambiar el tamaño de una máquina virtual que requiere clústeres de hardware de hello VM toobe movido toodifferent es diferente en función de qué modelo de implementación se usa toodeploy Hola VM.</span><span class="sxs-lookup"><span data-stu-id="9dead-136">Resizing a VM that requires hello VM toobe moved toodifferent hardware clusters is different depending on which deployment model was used toodeploy hello VM.</span></span>

- <span data-ttu-id="9dead-137">Máquinas virtuales implementadas en el modelo de implementación clásico, implementación del servicio de nube de hello deben quitarse y volver a implementar las máquinas virtuales tooa tamaño de toochange Hola de otra familia de tamaño.</span><span class="sxs-lookup"><span data-stu-id="9dead-137">VMs deployed in Classic deployment model, hello cloud service deployment must be removed and redeployed toochange hello VMs tooa size in another size family.</span></span>

- <span data-ttu-id="9dead-138">Máquinas virtuales implementadas en el modelo de implementación de administrador de recursos, debe detener todas las máquinas virtuales en conjunto antes de cambiar el tamaño de Hola de cualquier máquina virtual en el conjunto de disponibilidad de Hola de disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="9dead-138">VMs deployed in Resource Manager deployment model, you must stop all VMs in hello availability set before changing hello size of any VM in hello availability set.</span></span>

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="9dead-139">Hello lista tamaño de máquina virtual no se admite mientras se implementa en el conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="9dead-139">hello listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="9dead-140">Elija un tamaño que es compatible con clúster del conjunto de disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="9dead-140">Choose a size that is supported on hello availability set's cluster.</span></span> <span data-ttu-id="9dead-141">Se recomienda al crear que un conjunto de disponibilidad toochoose Hola mayor tamaño de máquina virtual piensa que necesita y tiene que ser el primer toohello de implementación de conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="9dead-141">It is recommended when creating an availability set toochoose hello largest VM size you think you need, and have that be your first deployment toohello Availability set.</span></span>

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a><span data-ttu-id="9dead-142">¿Qué distribuciones o versiones de Linux son compatibles con Azure?</span><span class="sxs-lookup"><span data-stu-id="9dead-142">What Linux distributions/versions are supported on Azure?</span></span>

<span data-ttu-id="9dead-143">Encontrará la lista de hello en Linux en [Azure-Endorsed distribuciones](endorsed-distros.md).</span><span class="sxs-lookup"><span data-stu-id="9dead-143">You can find hello list at Linux on [Azure-Endorsed Distributions](endorsed-distros.md).</span></span>

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a><span data-ttu-id="9dead-144">¿Puedo agregar un conjunto de disponibilidad de tooan clásico VM existente?</span><span class="sxs-lookup"><span data-stu-id="9dead-144">Can I add an existing Classic VM tooan availability set?</span></span>

<span data-ttu-id="9dead-145">Sí.</span><span class="sxs-lookup"><span data-stu-id="9dead-145">Yes.</span></span> <span data-ttu-id="9dead-146">Puede agregar una existente tooa VM clásico nueva o conjunto de disponibilidad existentes.</span><span class="sxs-lookup"><span data-stu-id="9dead-146">You can add an existing classic VM tooa new or existing Availability Set.</span></span> <span data-ttu-id="9dead-147">Para obtener más información, consulte [agrega un conjunto de disponibilidad de tooan de máquina virtual existente](../windows/classic/configure-availability.md#addmachine).</span><span class="sxs-lookup"><span data-stu-id="9dead-147">For more information see [Add an existing virtual machine tooan availability set](../windows/classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="9dead-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9dead-148">Next steps</span></span>
<span data-ttu-id="9dead-149">Si necesita más ayuda en cualquier momento en este artículo, puede ponerse en contacto con hello Azure expertos en [Hola foros de Azure de MSDN y el desbordamiento de la pila](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="9dead-149">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="9dead-150">Como alternativa, puede registrar un incidente de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="9dead-150">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="9dead-151">Vaya toohello [sitio de soporte técnico de Azure](https://azure.microsoft.com/support/options/) y seleccione **obtener admiten**.</span><span class="sxs-lookup"><span data-stu-id="9dead-151">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
