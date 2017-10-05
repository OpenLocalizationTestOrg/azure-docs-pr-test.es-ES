---
title: "Administración de directivas de laboratorio en Azure DevTest Labs | Microsoft Docs"
description: "Obtenga información acerca de cómo definir directivas de laboratorio como tamaños de máquina virtual, máximo de máquinas virtuales por usuario y automatización de apagado."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 7756aa64-49ca-45a0-9f90-0fd101c7be85
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 328a4d893637d7150807855e118b485a2c3bbfc5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="01d68-103">Administración de todas las directivas para un laboratorio de Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="01d68-103">Manage all policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="01d68-104">Azure DevTest Labs le permite controlar los costos y desperdiciar lo mínimo posible en sus laboratorios gracias a la posibilidad de administrar políticas (configuración) en cada uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="01d68-104">Azure DevTest Labs lets you control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="01d68-105">Este artículo explica en detalle paso a paso cómo configurar cada directiva.</span><span class="sxs-lookup"><span data-stu-id="01d68-105">This article explains in step-by-step detail how to set each policy.</span></span>  

## <a name="set-allowed-virtual-machine-sizes"></a><span data-ttu-id="01d68-106">Establecimiento de tamaños de máquina virtual permitidos</span><span class="sxs-lookup"><span data-stu-id="01d68-106">Set allowed virtual machine sizes</span></span>
<span data-ttu-id="01d68-107">La directiva para establecer los tamaños permitidos de la máquina virtual ayuda a minimizar la pérdida del laboratorio al permitirle especificar los tamaños de máquina virtual que se permiten en este.</span><span class="sxs-lookup"><span data-stu-id="01d68-107">The policy for setting the allowed VM sizes helps to minimize lab waste by enabling you to specify which VM sizes are allowed in the lab.</span></span> <span data-ttu-id="01d68-108">Si se activa esta directiva, los tamaños de máquina virtual de esta lista son los únicos que pueden utilizarse en la creación de tales máquinas.</span><span class="sxs-lookup"><span data-stu-id="01d68-108">If this policy is activated, only VM sizes from this list can be used to create VMs.</span></span>

1. <span data-ttu-id="01d68-109">En el menú **Configuration and policies** (Directivas y configuración) del laboratorio, seleccione **Allowed virtual machines sizes** (Tamaños de máquinas virtuales permitidas).</span><span class="sxs-lookup"><span data-stu-id="01d68-109">On the lab's **Configuration and policies** blade, select **Allowed virtual machines sizes**.</span></span>
   
    ![Allowed virtual machines sizes](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. <span data-ttu-id="01d68-111">Seleccione **Activado** para habilitar esta directiva, y **Desactivado** para deshabilitarla.</span><span class="sxs-lookup"><span data-stu-id="01d68-111">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="01d68-112">Si habilita esta directiva, seleccione uno o varios tamaños de máquina virtual que se pueden crear en el laboratorio.</span><span class="sxs-lookup"><span data-stu-id="01d68-112">If you enable this policy, select one or more VM sizes that can be created in your lab.</span></span>

1. <span data-ttu-id="01d68-113">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="01d68-113">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="01d68-114">Establecimiento de máquinas virtuales por usuario</span><span class="sxs-lookup"><span data-stu-id="01d68-114">Set virtual machines per user</span></span>
<span data-ttu-id="01d68-115">La directiva de **Máquinas virtuales por usuario** le permite especificar el número máximo de máquinas virtuales que puede crear un usuario individual.</span><span class="sxs-lookup"><span data-stu-id="01d68-115">The policy for **Virtual machines per user** allows you to specify the maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="01d68-116">Si un usuario trata de crear o reclamar una máquina virtual una vez alcanzado el límite, aparece un mensaje de error que indica que la máquina virtual no se puede crear ni exigir.</span><span class="sxs-lookup"><span data-stu-id="01d68-116">If a user attempts to create or claim a VM when the user limit has been met, an error message indicates that the VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="01d68-117">En el menú **Configuration and policies** (Directivas y configuración) del laboratorio, seleccione **Máquinas virtuales por usuario**.</span><span class="sxs-lookup"><span data-stu-id="01d68-117">On the lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Máquinas virtuales por usuario](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="01d68-119">Seleccione **Sí** para limitar el número de máquinas virtuales por usuario.</span><span class="sxs-lookup"><span data-stu-id="01d68-119">Select **Yes** to limit the number of VMs per user.</span></span> <span data-ttu-id="01d68-120">Si no quiere limitar el número de máquinas virtuales por usuario, seleccione **No**.</span><span class="sxs-lookup"><span data-stu-id="01d68-120">If you do not want to limit the number of VMs per user, select **No**.</span></span> <span data-ttu-id="01d68-121">Si elige **Sí**, escriba un valor numérico que indique el número máximo de máquinas virtuales que un usuario puede crear o reclamar.</span><span class="sxs-lookup"><span data-stu-id="01d68-121">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="01d68-122">Seleccione **Sí** para limitar el número de máquinas virtuales que puede usar SSD (discos de estado sólido).</span><span class="sxs-lookup"><span data-stu-id="01d68-122">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="01d68-123">Si no quiere limitar el número de máquinas virtuales que puede usar SSD, seleccione **No**.</span><span class="sxs-lookup"><span data-stu-id="01d68-123">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="01d68-124">Si elige **Sí**, escriba un valor que indique el número máximo de máquinas virtuales que se pueden crear con SSD.</span><span class="sxs-lookup"><span data-stu-id="01d68-124">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="01d68-125">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="01d68-125">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-lab"></a><span data-ttu-id="01d68-126">Establecimiento de máquinas virtuales por laboratorio</span><span class="sxs-lookup"><span data-stu-id="01d68-126">Set virtual machines per lab</span></span>
<span data-ttu-id="01d68-127">La directiva de **Máquinas virtuales por laboratorio** le permite especificar el número máximo de máquinas virtuales que se pueden crear para el laboratorio actual.</span><span class="sxs-lookup"><span data-stu-id="01d68-127">The policy for **Virtual machines per lab** allows you to specify the maximum number of VMs that can be created for the current lab.</span></span> <span data-ttu-id="01d68-128">Si un usuario intenta crear una máquina virtual una vez alcanzado el límite, aparece un mensaje de error que indica que la máquina virtual no se puede crear.</span><span class="sxs-lookup"><span data-stu-id="01d68-128">If a user attempts to create a VM when the lab limit has been met, an error message indicates that the VM cannot be created.</span></span> 

1. <span data-ttu-id="01d68-129">En el menú **Configuration and policies** (Directivas y configuración) del laboratorio, seleccione **Máquinas virtuales por laboratorio**.</span><span class="sxs-lookup"><span data-stu-id="01d68-129">On the lab's **Configuration and policies** menu, select **Virtual machines per lab**.</span></span>
   
    ![Máquinas virtuales por laboratorio](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. <span data-ttu-id="01d68-131">Seleccione **Sí** para limitar el número de máquinas virtuales por laboratorio.</span><span class="sxs-lookup"><span data-stu-id="01d68-131">Select **Yes** to limit the number of VMs per lab.</span></span> <span data-ttu-id="01d68-132">Si no quiere limitar el número de máquinas virtuales por laboratorio, seleccione **No**.</span><span class="sxs-lookup"><span data-stu-id="01d68-132">If you do not want to limit the number of VMs per lab, select **No**.</span></span> <span data-ttu-id="01d68-133">Si elige **Sí**, escriba un valor numérico que indique el número máximo de máquinas virtuales que un usuario puede crear o reclamar.</span><span class="sxs-lookup"><span data-stu-id="01d68-133">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="01d68-134">Seleccione **Sí** para limitar el número de máquinas virtuales que puede usar SSD (discos de estado sólido).</span><span class="sxs-lookup"><span data-stu-id="01d68-134">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="01d68-135">Si no quiere limitar el número de máquinas virtuales que puede usar SSD, seleccione **No**.</span><span class="sxs-lookup"><span data-stu-id="01d68-135">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="01d68-136">Si elige **Sí**, escriba un valor que indique el número máximo de máquinas virtuales que se pueden crear con SSD.</span><span class="sxs-lookup"><span data-stu-id="01d68-136">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="01d68-137">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="01d68-137">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="01d68-138">Establecimiento del apagado automático</span><span class="sxs-lookup"><span data-stu-id="01d68-138">Set auto-shutdown</span></span>
<span data-ttu-id="01d68-139">La directiva de apagado automático ayuda a minimizar la pérdida del laboratorio, ya que permite especificar la hora de apagado de la máquina virtual de este laboratorio.</span><span class="sxs-lookup"><span data-stu-id="01d68-139">The auto-shutdown policy helps to minimize lab waste by allowing you to specify the time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="01d68-140">En la hoja **Configuration and Policies** (Directivas y configuración) del laboratorio, seleccione **Apagado automático**.</span><span class="sxs-lookup"><span data-stu-id="01d68-140">On the lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Apagado automático](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="01d68-142">Seleccione **Activado** para habilitar esta directiva, y **Desactivado** para deshabilitarla.</span><span class="sxs-lookup"><span data-stu-id="01d68-142">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="01d68-143">Si habilita esta directiva, especifique la hora local (y la zona horaria) para apagar todas las máquinas virtuales del laboratorio actual.</span><span class="sxs-lookup"><span data-stu-id="01d68-143">If you enable this policy, specify the time (and time zone) to shut down all VMs in the current lab.</span></span>

1. <span data-ttu-id="01d68-144">Especifique **Sí** o **No** en la opción de enviar una notificación 15 minutos antes de la hora especificada para el apagado automático.</span><span class="sxs-lookup"><span data-stu-id="01d68-144">Specify **Yes** or **No** for the option to send a notification 15 minutes prior to the specified auto-shutdown time.</span></span> <span data-ttu-id="01d68-145">Si selecciona **Sí**, escriba un punto de conexión de URL de webhooks para recibir la notificación.</span><span class="sxs-lookup"><span data-stu-id="01d68-145">If you specify **Yes**, enter a webhook URL endpoint to receive the notification.</span></span> <span data-ttu-id="01d68-146">Para obtener más información sobre los webhooks, consulte [Creación de un webhook o una función de API de Azure](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="01d68-146">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="01d68-147">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="01d68-147">Select **Save**.</span></span>

    <span data-ttu-id="01d68-148">De manera predeterminada, una vez que se habilite, esta directiva se aplica a todas las máquinas virtuales del laboratorio actual.</span><span class="sxs-lookup"><span data-stu-id="01d68-148">By default, once enabled, this policy applies to all VMs in the current lab.</span></span> <span data-ttu-id="01d68-149">Para quitar esta configuración de una máquina virtual específica, abra la hoja de la máquina virtual y cambie la configuración de **Apagado automático** .</span><span class="sxs-lookup"><span data-stu-id="01d68-149">To remove this setting from a specific VM, open the VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="01d68-150">Establecimiento del inicio automático</span><span class="sxs-lookup"><span data-stu-id="01d68-150">Set auto-start</span></span>
<span data-ttu-id="01d68-151">La directiva de inicio automático le permite especificar cuándo se deben iniciar las máquinas virtuales del laboratorio actual.</span><span class="sxs-lookup"><span data-stu-id="01d68-151">The auto-start policy allows you to specify when the VMs in the current lab should be started.</span></span>  

1. <span data-ttu-id="01d68-152">En la hoja **Configuration and Policies** (Directivas y configuración) del laboratorio, seleccione **Inicio automático**.</span><span class="sxs-lookup"><span data-stu-id="01d68-152">On the lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Inicio automático](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="01d68-154">Seleccione **Activado** para habilitar esta directiva, y **Desactivado** para deshabilitarla.</span><span class="sxs-lookup"><span data-stu-id="01d68-154">Select **On** to enable this policy, and **Off** to disable it.</span></span>

3. <span data-ttu-id="01d68-155">Si habilita esta directiva, especifique a la hora local de inicio programado, la zona horaria los días de la semana en los que se aplica esta hora.</span><span class="sxs-lookup"><span data-stu-id="01d68-155">If you enable this policy, specify the scheduled start time, time zone, and the days of the week for which the time applies.</span></span> 

4. <span data-ttu-id="01d68-156">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="01d68-156">Select **Save**.</span></span>

    <span data-ttu-id="01d68-157">Una vez que se habilite, esta directiva no se aplica automáticamente a ninguna máquina virtual del laboratorio actual.</span><span class="sxs-lookup"><span data-stu-id="01d68-157">Once enabled, this policy is not automatically applied to any VMs in the current lab.</span></span> <span data-ttu-id="01d68-158">Para aplicar esta configuración a una máquina virtual específica, abra la hoja de la máquina virtual y cambie su configuración de **Inicio automático** .</span><span class="sxs-lookup"><span data-stu-id="01d68-158">To apply this setting to a specific VM, open the VM's blade and change its **Auto-start** setting</span></span> 

## <a name="set-expiration-date"></a><span data-ttu-id="01d68-159">Establecimiento de la fecha de expiración</span><span class="sxs-lookup"><span data-stu-id="01d68-159">Set expiration date</span></span>
<span data-ttu-id="01d68-160">Puede establecer una fecha de expiración cuando [cree la VM](devtest-lab-add-vm.md).</span><span class="sxs-lookup"><span data-stu-id="01d68-160">You can set an expiration date when you [create the VM](devtest-lab-add-vm.md).</span></span> <span data-ttu-id="01d68-161">En **Configuración avanzada**, elija el icono del calendario para especificar una fecha en la que la VM se eliminará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="01d68-161">In **Advanced settings**, choose the calendar icon to specify a date on which the VM will be automatically deleted.</span></span>  <span data-ttu-id="01d68-162">De forma predeterminada, la VM nunca expirará.</span><span class="sxs-lookup"><span data-stu-id="01d68-162">By default, the VM will never expire.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="01d68-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="01d68-163">Next steps</span></span>
<span data-ttu-id="01d68-164">Una vez que defina y aplique las distintas configuraciones de las directivas de máquina virtual correspondientes al laboratorio, puede intentar algunos de los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="01d68-164">Once you've defined and applied the various VM policy settings for your lab, here are some things to try next:</span></span>

* <span data-ttu-id="01d68-165">[Direcciones IP compartidas](devtest-lab-shared-ip.md); explica cómo las direcciones IP compartidas se usan en DevTest Labs para minimizar el número de direcciones IP públicas necesarias para conectarse a las máquinas virtuales del laboratorio.</span><span class="sxs-lookup"><span data-stu-id="01d68-165">[Understand shared IP addresses](devtest-lab-shared-ip.md) - Explains how shared IP addresses are used in DevTest Labs to minimize the number of public IP addresses required to connect to your lab VMs.</span></span>
* <span data-ttu-id="01d68-166">[Configuración de la administración de costos](devtest-lab-configure-cost-management.md): muestra cómo utilizar el gráfico **Tendencia de costo estimado mensual**</span><span class="sxs-lookup"><span data-stu-id="01d68-166">[Configure cost management](devtest-lab-configure-cost-management.md) - Illustrates how to use the **Monthly Estimated Cost Trend** chart</span></span>  
  <span data-ttu-id="01d68-167">para ver el costo estimado hasta la fecha del mes de calendario actual, así como el costo previsto para fin de mes.</span><span class="sxs-lookup"><span data-stu-id="01d68-167">to view the current month's estimated cost-to-date and the projected end-of-month cost.</span></span>
* <span data-ttu-id="01d68-168">[Creación de una imagen personalizada](devtest-lab-create-template.md): cuando cree una máquina virtual, deberá especificar una base, que puede ser una imagen personalizada o una imagen de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="01d68-168">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="01d68-169">Este artículo muestra cómo crear una imagen personalizada desde un archivo VHD.</span><span class="sxs-lookup"><span data-stu-id="01d68-169">This article illustrates how to create a custom image from a VHD file.</span></span>
* <span data-ttu-id="01d68-170">[Configuración de imágenes de Marketplace](devtest-lab-configure-marketplace-images.md): Azure DevTest Labs admite la creación de máquinas virtuales basadas en imágenes de Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="01d68-170">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="01d68-171">En este artículo se muestra cómo especificar las imágenes de Azure Marketplace, si corresponde, que se pueden usar en el momento de crear máquinas virtuales en un laboratorio.</span><span class="sxs-lookup"><span data-stu-id="01d68-171">This article illustrates how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="01d68-172">[Creación de una máquina virtual en un laboratorio](devtest-lab-add-vm-with-artifacts.md): se muestra cómo crear una máquina virtual desde una imagen base (ya sea personalizada o de Marketplace) y cómo trabajar con artefactos en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="01d68-172">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how to create a VM from a base image (either custom or Marketplace), and how to work with artifacts in your VM.</span></span>

