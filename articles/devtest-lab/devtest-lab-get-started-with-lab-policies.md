---
title: "Administración de directivas de laboratorio básicas en Azure DevTest Labs | Microsoft Docs"
description: "Obtenga información sobre cómo establecer algunas de las directivas básicas (configuración) para un laboratorio de DevTest Labs."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: tarcher
ms.openlocfilehash: ed35d081b191ec41ed9e5970515057a4715c0d59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="4dffb-103">Administración de directivas básicas para un laboratorio de Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4dffb-103">Manage basic policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="4dffb-104">Azure DevTest Labs permite controlar los costos y desperdiciar lo mínimo posible en sus laboratorios gracias a la posibilidad de administrar políticas (configuración) en cada uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="4dffb-104">Azure DevTest Labs enables you to control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="4dffb-105">En este artículo, empezará a trabajar con las directivas. Aprenderá a establecer dos de las directivas más importantes: limitar el número de máquinas virtuales que puede crear o reclamar un solo usuario, y configurar el apagado automático.</span><span class="sxs-lookup"><span data-stu-id="4dffb-105">In this article, you get started with policies by learning how to set two of the most critical policies - limiting the number of virtual machines (VM) that can be created or claimed by a single user, and configuring auto-shutdown.</span></span> <span data-ttu-id="4dffb-106">Para ver cómo establecer todas las directivas de laboratorio, consulte el artículo [Definición de directivas de laboratorio en Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="4dffb-106">To view how to set every lab policy, see the article, [Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span></span>  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a><span data-ttu-id="4dffb-107">Acceso a las directivas de laboratorio en Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4dffb-107">Accessing a lab's policies in Azure DevTest Labs</span></span>
<span data-ttu-id="4dffb-108">Los siguientes pasos le guiarán a través de la configuración de directivas para un laboratorio en Azure DevTest Labs:</span><span class="sxs-lookup"><span data-stu-id="4dffb-108">The following steps guide you through setting up policies for a lab in Azure DevTest Labs:</span></span>

<span data-ttu-id="4dffb-109">Para ver (y cambiar) las directivas de un laboratorio, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4dffb-109">To view (and change) the policies for a lab, follow these steps:</span></span>

1. <span data-ttu-id="4dffb-110">Inicie sesión en el [Portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="4dffb-110">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="4dffb-111">Seleccione **Más servicios** y, luego, **DevTest Labs** en la lista.</span><span class="sxs-lookup"><span data-stu-id="4dffb-111">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="4dffb-112">En la lista de laboratorios, seleccione el laboratorio que desee.</span><span class="sxs-lookup"><span data-stu-id="4dffb-112">From the list of labs, select the desired lab.</span></span>   

1. <span data-ttu-id="4dffb-113">Seleccione **Configuration and policies** (Directivas y configuración).</span><span class="sxs-lookup"><span data-stu-id="4dffb-113">Select **Configuration and policies**.</span></span>

    ![Hoja de configuración de directiva](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. <span data-ttu-id="4dffb-115">La hoja **Configuration and policies** (Directivas y configuración) contiene un menú de configuración donde puede especificar parámetros.</span><span class="sxs-lookup"><span data-stu-id="4dffb-115">The **Configuration and policies** blade contains a menu of settings that you can specify.</span></span> <span data-ttu-id="4dffb-116">Este artículo trata solo la configuración de **máquinas virtuales por usuario** y el **apagado automático**.</span><span class="sxs-lookup"><span data-stu-id="4dffb-116">This article covers only the settings for **Virtual machines per user** and **Auto-shutdown**.</span></span> <span data-ttu-id="4dffb-117">Para obtener información sobre las opciones restantes, vea [Definición de directivas de laboratorio en Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="4dffb-117">To learn about the remaining settings, see [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span></span> 
   
## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="4dffb-118">Establecimiento de máquinas virtuales por usuario</span><span class="sxs-lookup"><span data-stu-id="4dffb-118">Set virtual machines per user</span></span>
<span data-ttu-id="4dffb-119">La directiva de **Máquinas virtuales por usuario** le permite especificar el número máximo de máquinas virtuales que puede crear un usuario individual.</span><span class="sxs-lookup"><span data-stu-id="4dffb-119">The policy for **Virtual machines per user** allows you to specify the maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="4dffb-120">Si un usuario trata de crear o reclamar una máquina virtual una vez alcanzado el límite, aparece un mensaje de error que indica que la máquina virtual no se puede crear ni exigir.</span><span class="sxs-lookup"><span data-stu-id="4dffb-120">If a user attempts to create or claim a VM when the user limit has been met, an error message indicates that the VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="4dffb-121">En el menú **Configuration and policies** (Directivas y configuración) del laboratorio, seleccione **Máquinas virtuales por usuario**.</span><span class="sxs-lookup"><span data-stu-id="4dffb-121">On the lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Máquinas virtuales por usuario](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="4dffb-123">Seleccione **Sí** para limitar el número de máquinas virtuales por usuario.</span><span class="sxs-lookup"><span data-stu-id="4dffb-123">Select **Yes** to limit the number of VMs per user.</span></span> <span data-ttu-id="4dffb-124">Si no quiere limitar el número de máquinas virtuales por usuario, seleccione **No**.</span><span class="sxs-lookup"><span data-stu-id="4dffb-124">If you do not want to limit the number of VMs per user, select **No**.</span></span> <span data-ttu-id="4dffb-125">Si elige **Sí**, escriba un valor numérico que indique el número máximo de máquinas virtuales que un usuario puede crear o reclamar.</span><span class="sxs-lookup"><span data-stu-id="4dffb-125">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="4dffb-126">Seleccione **Sí** para limitar el número de máquinas virtuales que puede usar SSD (discos de estado sólido).</span><span class="sxs-lookup"><span data-stu-id="4dffb-126">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="4dffb-127">Si no quiere limitar el número de máquinas virtuales que puede usar SSD, seleccione **No**.</span><span class="sxs-lookup"><span data-stu-id="4dffb-127">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="4dffb-128">Si elige **Sí**, escriba un valor que indique el número máximo de máquinas virtuales que se pueden crear con SSD.</span><span class="sxs-lookup"><span data-stu-id="4dffb-128">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="4dffb-129">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4dffb-129">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="4dffb-130">Establecimiento del apagado automático</span><span class="sxs-lookup"><span data-stu-id="4dffb-130">Set auto-shutdown</span></span>
<span data-ttu-id="4dffb-131">La directiva de apagado automático ayuda a minimizar la pérdida del laboratorio, ya que permite especificar la hora de apagado de la máquina virtual de este laboratorio.</span><span class="sxs-lookup"><span data-stu-id="4dffb-131">The auto-shutdown policy helps to minimize lab waste by allowing you to specify the time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="4dffb-132">En la hoja **Configuration and Policies** (Directivas y configuración) del laboratorio, seleccione **Apagado automático**.</span><span class="sxs-lookup"><span data-stu-id="4dffb-132">On the lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Apagado automático](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="4dffb-134">Seleccione **Activado** para habilitar esta directiva, y **Desactivado** para deshabilitarla.</span><span class="sxs-lookup"><span data-stu-id="4dffb-134">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="4dffb-135">Si habilita esta directiva, especifique la hora local (y la zona horaria) para apagar todas las máquinas virtuales del laboratorio actual.</span><span class="sxs-lookup"><span data-stu-id="4dffb-135">If you enable this policy, specify the time (and time zone) to shut down all VMs in the current lab.</span></span>

1. <span data-ttu-id="4dffb-136">Especifique **Sí** o **No** en la opción de enviar una notificación 15 minutos antes de la hora especificada para el apagado automático.</span><span class="sxs-lookup"><span data-stu-id="4dffb-136">Specify **Yes** or **No** for the option to send a notification 15 minutes prior to the specified auto-shutdown time.</span></span> <span data-ttu-id="4dffb-137">Si selecciona **Sí**, escriba un punto de conexión de URL de webhooks para recibir la notificación.</span><span class="sxs-lookup"><span data-stu-id="4dffb-137">If you specify **Yes**, enter a webhook URL endpoint to receive the notification.</span></span> <span data-ttu-id="4dffb-138">Para obtener más información sobre los webhooks, consulte [Creación de un webhook o una función de API de Azure](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="4dffb-138">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="4dffb-139">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4dffb-139">Select **Save**.</span></span>

    <span data-ttu-id="4dffb-140">De manera predeterminada, una vez que se habilite, esta directiva se aplica a todas las máquinas virtuales del laboratorio actual.</span><span class="sxs-lookup"><span data-stu-id="4dffb-140">By default, once enabled, this policy applies to all VMs in the current lab.</span></span> <span data-ttu-id="4dffb-141">Para quitar esta configuración de una máquina virtual específica, abra la hoja de la máquina virtual y cambie la configuración de **Apagado automático** .</span><span class="sxs-lookup"><span data-stu-id="4dffb-141">To remove this setting from a specific VM, open the VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="4dffb-142">Establecimiento del inicio automático</span><span class="sxs-lookup"><span data-stu-id="4dffb-142">Set auto-start</span></span>
<span data-ttu-id="4dffb-143">La directiva de inicio automático le permite especificar cuándo se deben iniciar las máquinas virtuales del laboratorio actual.</span><span class="sxs-lookup"><span data-stu-id="4dffb-143">The auto-start policy allows you to specify when the VMs in the current lab should be started.</span></span>  

1. <span data-ttu-id="4dffb-144">En la hoja **Configuration and Policies** (Directivas y configuración) del laboratorio, seleccione **Inicio automático**.</span><span class="sxs-lookup"><span data-stu-id="4dffb-144">On the lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Inicio automático](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="4dffb-146">Seleccione **Activado** para habilitar esta directiva, y **Desactivado** para deshabilitarla.</span><span class="sxs-lookup"><span data-stu-id="4dffb-146">Select **On** to enable this policy, and **Off** to disable it.</span></span>

3. <span data-ttu-id="4dffb-147">Si habilita esta directiva, especifique a la hora local de inicio programado, la zona horaria los días de la semana en los que se aplica esta hora.</span><span class="sxs-lookup"><span data-stu-id="4dffb-147">If you enable this policy, specify the scheduled start time, time zone, and the days of the week for which the time applies.</span></span> 

4. <span data-ttu-id="4dffb-148">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4dffb-148">Select **Save**.</span></span>

    <span data-ttu-id="4dffb-149">Una vez que se habilite, esta directiva no se aplica automáticamente a ninguna máquina virtual del laboratorio actual.</span><span class="sxs-lookup"><span data-stu-id="4dffb-149">Once enabled, this policy is not automatically applied to any VMs in the current lab.</span></span> <span data-ttu-id="4dffb-150">Para aplicar esta configuración a una máquina virtual específica, abra la hoja de la máquina virtual y cambie su configuración de **Inicio automático** .</span><span class="sxs-lookup"><span data-stu-id="4dffb-150">To apply this setting to a specific VM, open the VM's blade and change its **Auto-start** setting</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4dffb-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4dffb-151">Next steps</span></span>

- <span data-ttu-id="4dffb-152">[Definición de directivas de laboratorio en Azure DevTest Labs](devtest-lab-set-lab-policy.md) (información sobre cómo modificar otras directivas de laboratorio)</span><span class="sxs-lookup"><span data-stu-id="4dffb-152">[Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md) - Learn how to modify other lab policies</span></span> 
