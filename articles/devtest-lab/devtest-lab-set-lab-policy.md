---
title: las directivas de laboratorio aaaManage en los laboratorios de desarrollo y pruebas de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tamaños de directivas de laboratorio toodefine como máquina virtual, máquinas virtuales máximas por usuario y la automatización de cierre."
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
ms.openlocfilehash: 351b3645a1fd729455884e5d177877c2986bd853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="a5b6d-103">Administración de todas las directivas para un laboratorio de Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="a5b6d-103">Manage all policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="a5b6d-104">Azure DevTest Labs le permite controlar los costos y desperdiciar lo mínimo posible en sus laboratorios gracias a la posibilidad de administrar políticas (configuración) en cada uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-104">Azure DevTest Labs lets you control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="a5b6d-105">Este artículo se explica detalladamente paso a paso cómo tooset cada directiva.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-105">This article explains in step-by-step detail how tooset each policy.</span></span>  

## <a name="set-allowed-virtual-machine-sizes"></a><span data-ttu-id="a5b6d-106">Establecimiento de tamaños de máquina virtual permitidos</span><span class="sxs-lookup"><span data-stu-id="a5b6d-106">Set allowed virtual machine sizes</span></span>
<span data-ttu-id="a5b6d-107">Hello directiva para Hola de configuración permite tamaños de máquina virtual ayuda toominimize laboratorio residuos habilitando toospecify qué tamaños de máquina virtual se permiten en el laboratorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-107">hello policy for setting hello allowed VM sizes helps toominimize lab waste by enabling you toospecify which VM sizes are allowed in hello lab.</span></span> <span data-ttu-id="a5b6d-108">Si se activa esta directiva, solo los tamaños de máquinas virtuales de esta lista pueden ser usado toocreate las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-108">If this policy is activated, only VM sizes from this list can be used toocreate VMs.</span></span>

1. <span data-ttu-id="a5b6d-109">En el laboratorio de hello **directivas y configuración** hoja, seleccione **permite tamaños de máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-109">On hello lab's **Configuration and policies** blade, select **Allowed virtual machines sizes**.</span></span>
   
    ![Allowed virtual machines sizes](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. <span data-ttu-id="a5b6d-111">Seleccione **en** tooenable esta directiva, y **desactivar** toodisable lo.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-111">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="a5b6d-112">Si habilita esta directiva, seleccione uno o varios tamaños de máquina virtual que se pueden crear en el laboratorio.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-112">If you enable this policy, select one or more VM sizes that can be created in your lab.</span></span>

1. <span data-ttu-id="a5b6d-113">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-113">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="a5b6d-114">Establecimiento de máquinas virtuales por usuario</span><span class="sxs-lookup"><span data-stu-id="a5b6d-114">Set virtual machines per user</span></span>
<span data-ttu-id="a5b6d-115">Hola directiva para **máquinas virtuales por usuario** permite un número máximo de hello toospecify de máquinas virtuales que se pueden crear un usuario individual.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-115">hello policy for **Virtual machines per user** allows you toospecify hello maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="a5b6d-116">Si un usuario intenta toocreate o notificación de una máquina virtual cuando se ha alcanzado el límite de usuarios de hello, un mensaje de error indica que Hola que VM no se puede que crear/presentado.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-116">If a user attempts toocreate or claim a VM when hello user limit has been met, an error message indicates that hello VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="a5b6d-117">En el laboratorio de hello **directivas y configuración** menú, seleccione **máquinas virtuales por usuario**.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-117">On hello lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Máquinas virtuales por usuario](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="a5b6d-119">Seleccione **Sí** toolimit número de Hola de máquinas virtuales por usuario.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-119">Select **Yes** toolimit hello number of VMs per user.</span></span> <span data-ttu-id="a5b6d-120">Si no desea toolimit número de Hola de máquinas virtuales por usuario, seleccione **No**.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-120">If you do not want toolimit hello number of VMs per user, select **No**.</span></span> <span data-ttu-id="a5b6d-121">Si selecciona **Sí**, especifique un valor numérico que indica el número máximo de Hola de máquinas virtuales que se puede crear o presentado por un usuario.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-121">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="a5b6d-122">Seleccione **Sí** número de hello toolimit de máquinas virtuales que puede usar SSD (disco de estado sólido).</span><span class="sxs-lookup"><span data-stu-id="a5b6d-122">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="a5b6d-123">Si no desea toolimit número de Hola de máquinas virtuales que puede usar SSD, seleccione **No**.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-123">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="a5b6d-124">Si selecciona **Sí**, escriba un valor que indica el número máximo de Hola de máquinas virtuales que pueden crearse con SSD.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-124">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="a5b6d-125">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-125">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-lab"></a><span data-ttu-id="a5b6d-126">Establecimiento de máquinas virtuales por laboratorio</span><span class="sxs-lookup"><span data-stu-id="a5b6d-126">Set virtual machines per lab</span></span>
<span data-ttu-id="a5b6d-127">Hola directiva para **máquinas virtuales por laboratorio** permite un número máximo de hello toospecify de máquinas virtuales que se pueden crear para laboratorio actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-127">hello policy for **Virtual machines per lab** allows you toospecify hello maximum number of VMs that can be created for hello current lab.</span></span> <span data-ttu-id="a5b6d-128">Si un usuario intenta toocreate una máquina virtual cuando se ha alcanzado el límite de laboratorio de hello, un mensaje de error indica que no se puede crear la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-128">If a user attempts toocreate a VM when hello lab limit has been met, an error message indicates that hello VM cannot be created.</span></span> 

1. <span data-ttu-id="a5b6d-129">En el laboratorio de hello **directivas y configuración** menú, seleccione **máquinas virtuales por laboratorio**.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-129">On hello lab's **Configuration and policies** menu, select **Virtual machines per lab**.</span></span>
   
    ![Máquinas virtuales por laboratorio](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. <span data-ttu-id="a5b6d-131">Seleccione **Sí** toolimit número de Hola de máquinas virtuales por laboratorio.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-131">Select **Yes** toolimit hello number of VMs per lab.</span></span> <span data-ttu-id="a5b6d-132">Si no desea toolimit número de Hola de máquinas virtuales por laboratorio, seleccione **No**.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-132">If you do not want toolimit hello number of VMs per lab, select **No**.</span></span> <span data-ttu-id="a5b6d-133">Si selecciona **Sí**, especifique un valor numérico que indica el número máximo de Hola de máquinas virtuales que se puede crear o presentado por un usuario.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-133">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="a5b6d-134">Seleccione **Sí** número de hello toolimit de máquinas virtuales que puede usar SSD (disco de estado sólido).</span><span class="sxs-lookup"><span data-stu-id="a5b6d-134">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="a5b6d-135">Si no desea toolimit número de Hola de máquinas virtuales que puede usar SSD, seleccione **No**.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-135">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="a5b6d-136">Si selecciona **Sí**, escriba un valor que indica el número máximo de Hola de máquinas virtuales que pueden crearse con SSD.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-136">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="a5b6d-137">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-137">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="a5b6d-138">Establecimiento del apagado automático</span><span class="sxs-lookup"><span data-stu-id="a5b6d-138">Set auto-shutdown</span></span>
<span data-ttu-id="a5b6d-139">Directiva de cierre automático de Hello ayuda toominimize laboratorio residuos permitiéndole tiempo de hello toospecify que apagar máquinas virtuales de este laboratorio.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-139">hello auto-shutdown policy helps toominimize lab waste by allowing you toospecify hello time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="a5b6d-140">En el laboratorio de hello **directivas y configuración** hoja, seleccione **apagado automático**.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-140">On hello lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Apagado automático](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="a5b6d-142">Seleccione **en** tooenable esta directiva, y **desactivar** toodisable lo.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-142">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="a5b6d-143">Si habilita esta directiva, especifique hello tooshut hora (y zona horaria) hacia abajo de todas las máquinas virtuales en laboratorio actual Hola.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-143">If you enable this policy, specify hello time (and time zone) tooshut down all VMs in hello current lab.</span></span>

1. <span data-ttu-id="a5b6d-144">Especifique **Sí** o **n** para hello opción toosend un toohello antes de 15 minutos de notificación especificado tiempo de cierre automático.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-144">Specify **Yes** or **No** for hello option toosend a notification 15 minutes prior toohello specified auto-shutdown time.</span></span> <span data-ttu-id="a5b6d-145">Si especifica **Sí**, escriba una notificación de hello webhook tooreceive de punto de conexión de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-145">If you specify **Yes**, enter a webhook URL endpoint tooreceive hello notification.</span></span> <span data-ttu-id="a5b6d-146">Para obtener más información sobre los webhooks, consulte [Creación de un webhook o una función de API de Azure](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="a5b6d-146">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="a5b6d-147">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-147">Select **Save**.</span></span>

    <span data-ttu-id="a5b6d-148">De forma predeterminada, una vez habilitada, esta directiva aplica a máquinas virtuales de tooall en laboratorio actual Hola.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-148">By default, once enabled, this policy applies tooall VMs in hello current lab.</span></span> <span data-ttu-id="a5b6d-149">tooremove esta configuración de una máquina virtual específica, abra la máquina virtual de hello hoja y cambie su **apagado automático** configuración</span><span class="sxs-lookup"><span data-stu-id="a5b6d-149">tooremove this setting from a specific VM, open hello VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="a5b6d-150">Establecimiento del inicio automático</span><span class="sxs-lookup"><span data-stu-id="a5b6d-150">Set auto-start</span></span>
<span data-ttu-id="a5b6d-151">Directiva de inicio automático de Hello permite toospecify cuando se debe iniciar hello las máquinas virtuales en el laboratorio actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-151">hello auto-start policy allows you toospecify when hello VMs in hello current lab should be started.</span></span>  

1. <span data-ttu-id="a5b6d-152">En el laboratorio de hello **directivas y configuración** hoja, seleccione **inicio automático**.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-152">On hello lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Inicio automático](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="a5b6d-154">Seleccione **en** tooenable esta directiva, y **desactivar** toodisable lo.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-154">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

3. <span data-ttu-id="a5b6d-155">Si habilita esta directiva, especifique la hora de inicio programada de hello, zona horaria y Hola días de la semana de Hola para qué hello tiempo se aplica.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-155">If you enable this policy, specify hello scheduled start time, time zone, and hello days of hello week for which hello time applies.</span></span> 

4. <span data-ttu-id="a5b6d-156">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-156">Select **Save**.</span></span>

    <span data-ttu-id="a5b6d-157">Una vez habilitada, esta directiva no está tooany aplica automáticamente las máquinas virtuales en laboratorio actual Hola.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-157">Once enabled, this policy is not automatically applied tooany VMs in hello current lab.</span></span> <span data-ttu-id="a5b6d-158">tooapply este tooa configuración VM específica, la máquina virtual de hello Abrir hoja y cambie su **inicio automático** configuración</span><span class="sxs-lookup"><span data-stu-id="a5b6d-158">tooapply this setting tooa specific VM, open hello VM's blade and change its **Auto-start** setting</span></span> 

## <a name="set-expiration-date"></a><span data-ttu-id="a5b6d-159">Establecimiento de la fecha de expiración</span><span class="sxs-lookup"><span data-stu-id="a5b6d-159">Set expiration date</span></span>
<span data-ttu-id="a5b6d-160">Puede establecer una expiración de fecha cuando se [crear hello VM](devtest-lab-add-vm.md).</span><span class="sxs-lookup"><span data-stu-id="a5b6d-160">You can set an expiration date when you [create hello VM](devtest-lab-add-vm.md).</span></span> <span data-ttu-id="a5b6d-161">En **configuración avanzada**, elija toospecify de icono de calendario Hola una fecha en la que Hola VM se eliminarán automáticamente.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-161">In **Advanced settings**, choose hello calendar icon toospecify a date on which hello VM will be automatically deleted.</span></span>  <span data-ttu-id="a5b6d-162">De forma predeterminada, el Hola VM nunca expirará.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-162">By default, hello VM will never expire.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="a5b6d-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a5b6d-163">Next steps</span></span>
<span data-ttu-id="a5b6d-164">Una vez que haya definido y aplicado Hola distintas configuraciones de directiva de máquina virtual para el laboratorio, a continuación le presentamos algunas tootry cosas:</span><span class="sxs-lookup"><span data-stu-id="a5b6d-164">Once you've defined and applied hello various VM policy settings for your lab, here are some things tootry next:</span></span>

* <span data-ttu-id="a5b6d-165">[Comprender las direcciones IP compartidas](devtest-lab-shared-ip.md) -explica cómo compartido IP direcciones se utilizan en el número de laboratorios de desarrollo y pruebas toominimize Hola pública tooconnect requiere tooyour laboratorio máquinas virtuales de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-165">[Understand shared IP addresses](devtest-lab-shared-ip.md) - Explains how shared IP addresses are used in DevTest Labs toominimize hello number of public IP addresses required tooconnect tooyour lab VMs.</span></span>
* <span data-ttu-id="a5b6d-166">[Configurar la administración de costos](devtest-lab-configure-cost-management.md) -ilustra cómo hello toouse **tendencia de costo mensual estimado** gráfico</span><span class="sxs-lookup"><span data-stu-id="a5b6d-166">[Configure cost management](devtest-lab-configure-cost-management.md) - Illustrates how toouse hello **Monthly Estimated Cost Trend** chart</span></span>  
  <span data-ttu-id="a5b6d-167">tooview Hola estimado costo hasta la fecha del mes actual y el costo de fin de mes de hello proyectado.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-167">tooview hello current month's estimated cost-to-date and hello projected end-of-month cost.</span></span>
* <span data-ttu-id="a5b6d-168">[Creación de una imagen personalizada](devtest-lab-create-template.md): cuando cree una máquina virtual, deberá especificar una base, que puede ser una imagen personalizada o una imagen de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-168">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="a5b6d-169">Este artículo explica cómo toocreate personalizado de la imagen desde un archivo de disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-169">This article illustrates how toocreate a custom image from a VHD file.</span></span>
* <span data-ttu-id="a5b6d-170">[Configuración de imágenes de Marketplace](devtest-lab-configure-marketplace-images.md): Azure DevTest Labs admite la creación de máquinas virtuales basadas en imágenes de Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-170">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="a5b6d-171">Este artículo se explica cómo toospecify que, si lo hay, imágenes de Azure Marketplace se pueden usar al crear máquinas virtuales en un laboratorio.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-171">This article illustrates how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="a5b6d-172">[Crear una máquina virtual en un laboratorio](devtest-lab-add-vm-with-artifacts.md) -ilustra cómo toocreate una máquina virtual desde una imagen base (ya sea personalizado o Marketplace) y cómo toowork con los artefactos en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a5b6d-172">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how toocreate a VM from a base image (either custom or Marketplace), and how toowork with artifacts in your VM.</span></span>

