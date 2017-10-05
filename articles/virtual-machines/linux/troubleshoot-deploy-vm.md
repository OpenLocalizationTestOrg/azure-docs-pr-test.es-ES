---
title: "Solución de problemas de implementación de la máquina virtual Linux en Azure | Microsoft Docs"
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
ms.openlocfilehash: 8bc9de90a49caf9155073caaa160585c6cc3728b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a><span data-ttu-id="cae20-103">Solución de problemas de implementación de la máquina virtual Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="cae20-103">Troubleshoot deploying Linux virtual machine issues in Azure</span></span>

<span data-ttu-id="cae20-104">Para solucionar problemas de implementación de la máquina virtual (VM) de Azure, revise la sección [Principales problemas](#top-issues) para conocer errores comunes y sus soluciones.</span><span class="sxs-lookup"><span data-stu-id="cae20-104">To troubleshoot virtual machine (VM) deployment issues in Azure, review the [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="cae20-105">Si necesita más ayuda con cualquier aspecto de este artículo, puede ponerse en contacto con los expertos de Azure en [los foros de MSDN Azure o Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="cae20-105">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="cae20-106">Como alternativa, puede registrar un incidente de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="cae20-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="cae20-107">Vaya al [sitio de soporte técnico de Azure](https://azure.microsoft.com/support/options/) y seleccione **Obtener soporte**.</span><span class="sxs-lookup"><span data-stu-id="cae20-107">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="cae20-108">Principales problemas</span><span class="sxs-lookup"><span data-stu-id="cae20-108">Top issues</span></span>
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

## <a name="the-cluster-cannot-support-the-requested-vm-size"></a><span data-ttu-id="cae20-109">El clúster no admite el tamaño de máquina virtual solicitado</span><span class="sxs-lookup"><span data-stu-id="cae20-109">The cluster cannot support the requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="cae20-110">Vuelva a intentar la solicitud con un tamaño de máquina virtual menor.</span><span class="sxs-lookup"><span data-stu-id="cae20-110">Retry the request using a smaller VM size.</span></span>
- <span data-ttu-id="cae20-111">Si no se puede cambiar el tamaño de la máquina virtual solicitada:</span><span class="sxs-lookup"><span data-stu-id="cae20-111">If the size of the requested VM cannot be changed:</span></span>
    - <span data-ttu-id="cae20-112">Detenga todas las máquinas virtuales en el conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="cae20-112">Stop all the VMs in the availability set.</span></span> <span data-ttu-id="cae20-113">Haga clic en **Grupos de recursos** > su grupo de recursos > **Recursos** > su conjunto de disponibilidad > **Máquinas virtuales** > su máquina virtual > **Detener**.</span><span class="sxs-lookup"><span data-stu-id="cae20-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="cae20-114">Después de detener todas las máquinas virtuales, cree la máquina virtual con el tamaño deseado.</span><span class="sxs-lookup"><span data-stu-id="cae20-114">After all the VMs stop, create the VM in the desired size.</span></span>
    - <span data-ttu-id="cae20-115">Inicie la nueva máquina virtual en primer lugar y luego seleccione cada una de las máquinas virtuales detenidas y haga clic en Iniciar.</span><span class="sxs-lookup"><span data-stu-id="cae20-115">Start the new VM first, and then select each of the stopped VMs and click Start.</span></span>


## <a name="the-cluster-does-not-have-free-resources"></a><span data-ttu-id="cae20-116">El clúster no tiene recursos disponibles</span><span class="sxs-lookup"><span data-stu-id="cae20-116">The cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="cae20-117">Vuelva a intentar realizar la solicitud más tarde.</span><span class="sxs-lookup"><span data-stu-id="cae20-117">Retry the request later.</span></span>
- <span data-ttu-id="cae20-118">Si la nueva máquina virtual puede formar parte de un conjunto de disponibilidad diferente</span><span class="sxs-lookup"><span data-stu-id="cae20-118">If the new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="cae20-119">Cree una máquina virtual en un conjunto de disponibilidad diferente (en la misma región).</span><span class="sxs-lookup"><span data-stu-id="cae20-119">Create a VM in a different availability set (in the same region).</span></span>
    - <span data-ttu-id="cae20-120">Agregue la nueva máquina virtual a la misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="cae20-120">Add the new VM to the same virtual network.</span></span>

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="cae20-121">Cómo se activa mi crédito mensual para Visual Studio Enterprise (BizSpark)</span><span class="sxs-lookup"><span data-stu-id="cae20-121">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="cae20-122">Para activar el crédito mensual, consulte este [artículo](https://azure.microsoft.com/offers/ms-azr-0064p/).</span><span class="sxs-lookup"><span data-stu-id="cae20-122">To activate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="why-can-i-not-install-the-gpu-driver-for-an-ubuntu-nv-vm"></a><span data-ttu-id="cae20-123">¿Por qué no puedo instalar el controlador de GPU para una máquina virtual NV de Ubuntu?</span><span class="sxs-lookup"><span data-stu-id="cae20-123">Why can I not install the GPU driver for an Ubuntu NV VM?</span></span>

<span data-ttu-id="cae20-124">Actualmente, la compatibilidad con la GPU de Linux solo está disponible en las máquinas virtuales de Azure NC que ejecutan Ubuntu Server 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="cae20-124">Currently, Linux GPU support is only available on Azure NC VMs running Ubuntu Server 16.04 LTS.</span></span> <span data-ttu-id="cae20-125">Para más información consulte [Configuración de controladores de GPU para máquinas virtuales de la serie N con Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="cae20-125">For more information, see [Set up GPU drivers for N-series VMs running Linux](n-series-driver-setup.md).</span></span>

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a><span data-ttu-id="cae20-126">Faltan los controladores para mi máquina virtual de la serie N de Linux</span><span class="sxs-lookup"><span data-stu-id="cae20-126">My drivers are missing for my Linux N-Series VM</span></span>

<span data-ttu-id="cae20-127">Los controladores para las máquinas virtuales basadas en Linux se encuentran [aquí](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="cae20-127">Drivers for Linux-based VMs are located [here](n-series-driver-setup.md).</span></span> 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="cae20-128">No puedo encontrar una instancia de la GPU en mi máquina virtual de la serie N</span><span class="sxs-lookup"><span data-stu-id="cae20-128">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="cae20-129">Para aprovechar las funcionalidades de GPU de las máquinas virtuales de la serie N de Azure que ejecutan Windows Server 2016 o Windows Server 2012 R2, debe instalar los controladores de gráficos de NVIDIA en cada máquina virtual después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="cae20-129">To take advantage of the GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="cae20-130">La información de instalación del controlador está disponible para las [máquinas virtuales Windows](../windows/n-series-driver-setup.md) y las [máquinas virtuales Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="cae20-130">Driver setup information is available for [Windows VMs](../windows/n-series-driver-setup.md) and [Linux VMs](n-series-driver-setup.md).</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="cae20-131">¿Hay máquinas virtuales de la serie N en mi región?</span><span class="sxs-lookup"><span data-stu-id="cae20-131">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="cae20-132">Puede comprobar la disponibilidad en la [tabla de productos disponibles por región](https://azure.microsoft.com/regions/services) y el precio [aquí](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span><span class="sxs-lookup"><span data-stu-id="cae20-132">You can check the availability from the [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="i-am-not-able-to-see-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="cae20-133">Al cambiar el tamaño de la máquina virtual, no puedo ver la familia de tamaño de máquina virtual que deseo.</span><span class="sxs-lookup"><span data-stu-id="cae20-133">I am not able to see VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="cae20-134">Cuando una máquina virtual se está ejecutando, se implementa en un servidor físico.</span><span class="sxs-lookup"><span data-stu-id="cae20-134">When a VM is running, it is deployed to a physical server.</span></span> <span data-ttu-id="cae20-135">Los servidores físicos en regiones de Azure se agrupan en clústeres de hardware físico común.</span><span class="sxs-lookup"><span data-stu-id="cae20-135">The physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="cae20-136">El modo de cambiar el tamaño de una máquina virtual que requiere que esta se mueva a clústeres de hardware diferentes difiere en función del modelo de implementación que se usara para implementarla.</span><span class="sxs-lookup"><span data-stu-id="cae20-136">Resizing a VM that requires the VM to be moved to different hardware clusters is different depending on which deployment model was used to deploy the VM.</span></span>

- <span data-ttu-id="cae20-137">En el caso de las máquinas virtuales implementadas en el modelo de implementación clásico, la implementación del servicio de nube debe quitarse y volver a implementarse para cambiar su tamaño por uno de otra familia de tamaño.</span><span class="sxs-lookup"><span data-stu-id="cae20-137">VMs deployed in Classic deployment model, the cloud service deployment must be removed and redeployed to change the VMs to a size in another size family.</span></span>

- <span data-ttu-id="cae20-138">En el caso de las máquinas virtuales implementadas en el modelo de implementación Resource Manager, debe detener todas las máquinas virtuales dentro del conjunto de disponibilidad antes de cambiar el tamaño de cualquiera de estas.</span><span class="sxs-lookup"><span data-stu-id="cae20-138">VMs deployed in Resource Manager deployment model, you must stop all VMs in the availability set before changing the size of any VM in the availability set.</span></span>

## <a name="the-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="cae20-139">El tamaño de máquina virtual enumerado no se admite mientras se implementa en el conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="cae20-139">The listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="cae20-140">Elija un tamaño que se admita en el clúster del conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="cae20-140">Choose a size that is supported on the availability set's cluster.</span></span> <span data-ttu-id="cae20-141">Al crear un conjunto de disponibilidad, se recomienda elegir el mayor tamaño de máquina virtual que piense que va a necesitar y tiene que ser la primera implementación para el conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="cae20-141">It is recommended when creating an availability set to choose the largest VM size you think you need, and have that be your first deployment to the Availability set.</span></span>

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a><span data-ttu-id="cae20-142">¿Qué distribuciones o versiones de Linux son compatibles con Azure?</span><span class="sxs-lookup"><span data-stu-id="cae20-142">What Linux distributions/versions are supported on Azure?</span></span>

<span data-ttu-id="cae20-143">Puede encontrar la lista de Linux en [Linux en distribuciones aprobadas por Azure](endorsed-distros.md).</span><span class="sxs-lookup"><span data-stu-id="cae20-143">You can find the list at Linux on [Azure-Endorsed Distributions](endorsed-distros.md).</span></span>

## <a name="can-i-add-an-existing-classic-vm-to-an-availability-set"></a><span data-ttu-id="cae20-144">¿Puedo agregar una máquina virtual clásica a un conjunto de disponibilidad?</span><span class="sxs-lookup"><span data-stu-id="cae20-144">Can I add an existing Classic VM to an availability set?</span></span>

<span data-ttu-id="cae20-145">Sí.</span><span class="sxs-lookup"><span data-stu-id="cae20-145">Yes.</span></span> <span data-ttu-id="cae20-146">Puede agregar una máquina virtual clásica existente a un conjunto de disponibilidad nuevo o existente.</span><span class="sxs-lookup"><span data-stu-id="cae20-146">You can add an existing classic VM to a new or existing Availability Set.</span></span> <span data-ttu-id="cae20-147">Para más información, consulte [Incorporación de una máquina virtual existente a un conjunto de disponibilidad](../windows/classic/configure-availability.md#addmachine).</span><span class="sxs-lookup"><span data-stu-id="cae20-147">For more information see [Add an existing virtual machine to an availability set](../windows/classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="cae20-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cae20-148">Next steps</span></span>
<span data-ttu-id="cae20-149">Si necesita más ayuda con cualquier aspecto de este artículo, puede ponerse en contacto con los expertos de Azure en [los foros de MSDN Azure o Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="cae20-149">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="cae20-150">Como alternativa, puede registrar un incidente de soporte técnico de Azure.</span><span class="sxs-lookup"><span data-stu-id="cae20-150">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="cae20-151">Vaya al [sitio de soporte técnico de Azure](https://azure.microsoft.com/support/options/) y seleccione **Obtener soporte**.</span><span class="sxs-lookup"><span data-stu-id="cae20-151">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
