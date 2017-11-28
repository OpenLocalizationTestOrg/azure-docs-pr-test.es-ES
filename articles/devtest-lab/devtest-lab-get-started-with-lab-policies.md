---
title: "las directivas de laboratorio básico aaaManage en los laboratorios de desarrollo y pruebas de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooset algunos hello básico de directivas de (configuración) para un laboratorio de prácticas de desarrollo y pruebas"
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
ms.openlocfilehash: 792c0d19cfe73964be9c03d3de7751a868fd86e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="d2520-103">Administración de directivas básicas para un laboratorio de Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="d2520-103">Manage basic policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="d2520-104">Laboratorios de desarrollo y pruebas de Azure permite toocontrol costo y minimizar residuos en los laboratorios de mediante la administración de directivas (valores) para cada laboratorio.</span><span class="sxs-lookup"><span data-stu-id="d2520-104">Azure DevTest Labs enables you toocontrol cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="d2520-105">En este artículo, empezar a trabajar con las directivas de aprendizaje cómo tooset dos directivas más importantes de hello - limitar Hola número de máquinas virtuales (VM) que se puede crear o presentadas por un usuario individual y configurar apagado automático.</span><span class="sxs-lookup"><span data-stu-id="d2520-105">In this article, you get started with policies by learning how tooset two of hello most critical policies - limiting hello number of virtual machines (VM) that can be created or claimed by a single user, and configuring auto-shutdown.</span></span> <span data-ttu-id="d2520-106">tooview cómo tooset todas las directivas de laboratorio, consulte el artículo de hello, [definir directivas de laboratorio en los laboratorios de desarrollo y pruebas de Azure](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="d2520-106">tooview how tooset every lab policy, see hello article, [Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span></span>  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a><span data-ttu-id="d2520-107">Acceso a las directivas de laboratorio en Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="d2520-107">Accessing a lab's policies in Azure DevTest Labs</span></span>
<span data-ttu-id="d2520-108">Hello siguientes pasos le guiarán configuración de directivas para un laboratorio de prácticas de desarrollo y pruebas de Azure:</span><span class="sxs-lookup"><span data-stu-id="d2520-108">hello following steps guide you through setting up policies for a lab in Azure DevTest Labs:</span></span>

<span data-ttu-id="d2520-109">directivas de hello tooview (y cambiar) para un laboratorio, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="d2520-109">tooview (and change) hello policies for a lab, follow these steps:</span></span>

1. <span data-ttu-id="d2520-110">Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="d2520-110">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="d2520-111">Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2520-111">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="d2520-112">En lista de Hola de laboratorios, seleccione laboratorio deseado Hola.</span><span class="sxs-lookup"><span data-stu-id="d2520-112">From hello list of labs, select hello desired lab.</span></span>   

1. <span data-ttu-id="d2520-113">Seleccione **Configuration and policies** (Directivas y configuración).</span><span class="sxs-lookup"><span data-stu-id="d2520-113">Select **Configuration and policies**.</span></span>

    ![Hoja de configuración de directiva](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. <span data-ttu-id="d2520-115">Hola **directivas y configuración** hoja contiene un menú de opciones que puede especificar.</span><span class="sxs-lookup"><span data-stu-id="d2520-115">hello **Configuration and policies** blade contains a menu of settings that you can specify.</span></span> <span data-ttu-id="d2520-116">En este artículo se analizan sólo las opciones de Hola para **máquinas virtuales por usuario** y **apagado automático**.</span><span class="sxs-lookup"><span data-stu-id="d2520-116">This article covers only hello settings for **Virtual machines per user** and **Auto-shutdown**.</span></span> <span data-ttu-id="d2520-117">toolearn sobre Hola restantes de la configuración, consulte [administrar todas las directivas para un laboratorio de prácticas de desarrollo y pruebas de Azure](./devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="d2520-117">toolearn about hello remaining settings, see [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span></span> 
   
## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="d2520-118">Establecimiento de máquinas virtuales por usuario</span><span class="sxs-lookup"><span data-stu-id="d2520-118">Set virtual machines per user</span></span>
<span data-ttu-id="d2520-119">Hola directiva para **máquinas virtuales por usuario** permite un número máximo de hello toospecify de máquinas virtuales que se pueden crear un usuario individual.</span><span class="sxs-lookup"><span data-stu-id="d2520-119">hello policy for **Virtual machines per user** allows you toospecify hello maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="d2520-120">Si un usuario intenta toocreate o notificación de una máquina virtual cuando se ha alcanzado el límite de usuarios de hello, un mensaje de error indica que Hola que VM no se puede que crear/presentado.</span><span class="sxs-lookup"><span data-stu-id="d2520-120">If a user attempts toocreate or claim a VM when hello user limit has been met, an error message indicates that hello VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="d2520-121">En el laboratorio de hello **directivas y configuración** menú, seleccione **máquinas virtuales por usuario**.</span><span class="sxs-lookup"><span data-stu-id="d2520-121">On hello lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Máquinas virtuales por usuario](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="d2520-123">Seleccione **Sí** toolimit número de Hola de máquinas virtuales por usuario.</span><span class="sxs-lookup"><span data-stu-id="d2520-123">Select **Yes** toolimit hello number of VMs per user.</span></span> <span data-ttu-id="d2520-124">Si no desea toolimit número de Hola de máquinas virtuales por usuario, seleccione **No**.</span><span class="sxs-lookup"><span data-stu-id="d2520-124">If you do not want toolimit hello number of VMs per user, select **No**.</span></span> <span data-ttu-id="d2520-125">Si selecciona **Sí**, especifique un valor numérico que indica el número máximo de Hola de máquinas virtuales que se puede crear o presentado por un usuario.</span><span class="sxs-lookup"><span data-stu-id="d2520-125">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="d2520-126">Seleccione **Sí** número de hello toolimit de máquinas virtuales que puede usar SSD (disco de estado sólido).</span><span class="sxs-lookup"><span data-stu-id="d2520-126">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="d2520-127">Si no desea toolimit número de Hola de máquinas virtuales que puede usar SSD, seleccione **No**.</span><span class="sxs-lookup"><span data-stu-id="d2520-127">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="d2520-128">Si selecciona **Sí**, escriba un valor que indica el número máximo de Hola de máquinas virtuales que pueden crearse con SSD.</span><span class="sxs-lookup"><span data-stu-id="d2520-128">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="d2520-129">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="d2520-129">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="d2520-130">Establecimiento del apagado automático</span><span class="sxs-lookup"><span data-stu-id="d2520-130">Set auto-shutdown</span></span>
<span data-ttu-id="d2520-131">Directiva de cierre automático de Hello ayuda toominimize laboratorio residuos permitiéndole tiempo de hello toospecify que apagar máquinas virtuales de este laboratorio.</span><span class="sxs-lookup"><span data-stu-id="d2520-131">hello auto-shutdown policy helps toominimize lab waste by allowing you toospecify hello time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="d2520-132">En el laboratorio de hello **directivas y configuración** hoja, seleccione **apagado automático**.</span><span class="sxs-lookup"><span data-stu-id="d2520-132">On hello lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Apagado automático](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="d2520-134">Seleccione **en** tooenable esta directiva, y **desactivar** toodisable lo.</span><span class="sxs-lookup"><span data-stu-id="d2520-134">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="d2520-135">Si habilita esta directiva, especifique hello tooshut hora (y zona horaria) hacia abajo de todas las máquinas virtuales en laboratorio actual Hola.</span><span class="sxs-lookup"><span data-stu-id="d2520-135">If you enable this policy, specify hello time (and time zone) tooshut down all VMs in hello current lab.</span></span>

1. <span data-ttu-id="d2520-136">Especifique **Sí** o **n** para hello opción toosend un toohello antes de 15 minutos de notificación especificado tiempo de cierre automático.</span><span class="sxs-lookup"><span data-stu-id="d2520-136">Specify **Yes** or **No** for hello option toosend a notification 15 minutes prior toohello specified auto-shutdown time.</span></span> <span data-ttu-id="d2520-137">Si especifica **Sí**, escriba una notificación de hello webhook tooreceive de punto de conexión de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="d2520-137">If you specify **Yes**, enter a webhook URL endpoint tooreceive hello notification.</span></span> <span data-ttu-id="d2520-138">Para obtener más información sobre los webhooks, consulte [Creación de un webhook o una función de API de Azure](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="d2520-138">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="d2520-139">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="d2520-139">Select **Save**.</span></span>

    <span data-ttu-id="d2520-140">De forma predeterminada, una vez habilitada, esta directiva aplica a máquinas virtuales de tooall en laboratorio actual Hola.</span><span class="sxs-lookup"><span data-stu-id="d2520-140">By default, once enabled, this policy applies tooall VMs in hello current lab.</span></span> <span data-ttu-id="d2520-141">tooremove esta configuración de una máquina virtual específica, abra la máquina virtual de hello hoja y cambie su **apagado automático** configuración</span><span class="sxs-lookup"><span data-stu-id="d2520-141">tooremove this setting from a specific VM, open hello VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="d2520-142">Establecimiento del inicio automático</span><span class="sxs-lookup"><span data-stu-id="d2520-142">Set auto-start</span></span>
<span data-ttu-id="d2520-143">Directiva de inicio automático de Hello permite toospecify cuando se debe iniciar hello las máquinas virtuales en el laboratorio actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="d2520-143">hello auto-start policy allows you toospecify when hello VMs in hello current lab should be started.</span></span>  

1. <span data-ttu-id="d2520-144">En el laboratorio de hello **directivas y configuración** hoja, seleccione **inicio automático**.</span><span class="sxs-lookup"><span data-stu-id="d2520-144">On hello lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Inicio automático](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="d2520-146">Seleccione **en** tooenable esta directiva, y **desactivar** toodisable lo.</span><span class="sxs-lookup"><span data-stu-id="d2520-146">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

3. <span data-ttu-id="d2520-147">Si habilita esta directiva, especifique la hora de inicio programada de hello, zona horaria y Hola días de la semana de Hola para qué hello tiempo se aplica.</span><span class="sxs-lookup"><span data-stu-id="d2520-147">If you enable this policy, specify hello scheduled start time, time zone, and hello days of hello week for which hello time applies.</span></span> 

4. <span data-ttu-id="d2520-148">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="d2520-148">Select **Save**.</span></span>

    <span data-ttu-id="d2520-149">Una vez habilitada, esta directiva no está tooany aplica automáticamente las máquinas virtuales en laboratorio actual Hola.</span><span class="sxs-lookup"><span data-stu-id="d2520-149">Once enabled, this policy is not automatically applied tooany VMs in hello current lab.</span></span> <span data-ttu-id="d2520-150">tooapply este tooa configuración VM específica, la máquina virtual de hello Abrir hoja y cambie su **inicio automático** configuración</span><span class="sxs-lookup"><span data-stu-id="d2520-150">tooapply this setting tooa specific VM, open hello VM's blade and change its **Auto-start** setting</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d2520-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d2520-151">Next steps</span></span>

- <span data-ttu-id="d2520-152">[Definir directivas de laboratorio en los laboratorios de desarrollo y pruebas de Azure](devtest-lab-set-lab-policy.md) -Obtenga información acerca de cómo toomodify otras directivas de laboratorio</span><span class="sxs-lookup"><span data-stu-id="d2520-152">[Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md) - Learn how toomodify other lab policies</span></span> 
