---
title: aaaConfigure una red virtual en los laboratorios de desarrollo y pruebas de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconfigure una red virtual existente y la subred y usarlos en una máquina virtual con los laboratorios de desarrollo y pruebas de Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 6cda99c2-b87e-4047-90a0-5df10d8e9e14
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: a11ce8315e3c540e44aeacc9c5ee3dde014d4621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a><span data-ttu-id="4f441-103">Configuración de una red virtual en Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4f441-103">Configure a virtual network in Azure DevTest Labs</span></span>
<span data-ttu-id="4f441-104">Como se explica en el artículo de hello, [agregar una máquina virtual con el laboratorio de artefactos tooa](devtest-lab-add-vm-with-artifacts.md), cuando se crea una máquina virtual en un laboratorio, puede especificar una red virtual configurada.</span><span class="sxs-lookup"><span data-stu-id="4f441-104">As explained in hello article, [Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md), when you create a VM in a lab, you can specify a configured virtual network.</span></span> <span data-ttu-id="4f441-105">Un escenario para hacer esto es si necesita tooaccess los recursos de la red corporativa desde las máquinas virtuales mediante Hola red virtual que se configuró con VPN de sitio a sitio o ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="4f441-105">One scenario for doing this is if you need tooaccess your corpnet resources from your VMs using hello virtual network that was configured with ExpressRoute or site-to-site VPN.</span></span> <span data-ttu-id="4f441-106">Hello próximas secciones se muestran cómo tooadd la red virtual existente a la configuración de red Virtual de un laboratorio para que esté disponible toochoose al crear máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="4f441-106">hello following sections illustrate how tooadd your existing virtual network into a lab's Virtual Network settings so that it is available toochoose when creating VMs.</span></span>

## <a name="configure-a-virtual-network-for-a-lab-using-hello-azure-portal"></a><span data-ttu-id="4f441-107">Configurar una red virtual para un laboratorio mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="4f441-107">Configure a virtual network for a lab using hello Azure portal</span></span>
<span data-ttu-id="4f441-108">Hello pasos siguientes le guían a través de agregar una existente virtual red (subred) tooa laboratorio y, por lo que se puede utilizar al crear una máquina virtual en hello mismo laboratorio.</span><span class="sxs-lookup"><span data-stu-id="4f441-108">hello following steps walk you through adding an existing virtual network (and subnet) tooa lab so that it can be used when creating a VM in hello same lab.</span></span> 

1. <span data-ttu-id="4f441-109">Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="4f441-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="4f441-110">Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f441-110">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="4f441-111">En lista de Hola de laboratorios, seleccione laboratorio deseado Hola.</span><span class="sxs-lookup"><span data-stu-id="4f441-111">From hello list of labs, select hello desired lab.</span></span> 
4. <span data-ttu-id="4f441-112">En la hoja del laboratorio de hello, seleccione **configuración**.</span><span class="sxs-lookup"><span data-stu-id="4f441-112">On hello lab's blade, select **Configuration**.</span></span>
5. <span data-ttu-id="4f441-113">En el laboratorio de hello **configuración** hoja, seleccione **redes virtuales**.</span><span class="sxs-lookup"><span data-stu-id="4f441-113">On hello lab's **Configuration** blade, select **Virtual networks**.</span></span>
6. <span data-ttu-id="4f441-114">En hello **redes virtuales** hoja, verá una lista de redes virtuales configuradas para el laboratorio de hello actual, así como la red virtual de hello predeterminada que se crea para el laboratorio.</span><span class="sxs-lookup"><span data-stu-id="4f441-114">On hello **Virtual networks** blade, you see a list of virtual networks configured for hello current lab as well as hello default virtual network that is created for your lab.</span></span> 
7. <span data-ttu-id="4f441-115">Seleccione **+Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4f441-115">Select **+ Add**.</span></span>
   
    ![Agregar un laboratorio de tooyour de red virtual existente](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. <span data-ttu-id="4f441-117">En hello **red Virtual** hoja, seleccione **[red virtual seleccione]**.</span><span class="sxs-lookup"><span data-stu-id="4f441-117">On hello **Virtual network** blade, select **[Select virtual network]**.</span></span>
   
    ![Selección de una red virtual existente](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. <span data-ttu-id="4f441-119">En hello **red virtual de elegir** hoja, red virtual de hello seleccione deseado.</span><span class="sxs-lookup"><span data-stu-id="4f441-119">On hello **Choose virtual network** blade, select hello desired virtual network.</span></span> <span data-ttu-id="4f441-120">hoja Hello muestra todas las redes virtuales Hola que están bajo Hola misma región en la suscripción Hola laboratorio Hola.</span><span class="sxs-lookup"><span data-stu-id="4f441-120">hello blade shows all hello virtual networks that are under hello same region in hello subscription as hello lab.</span></span>  
10. <span data-ttu-id="4f441-121">Después de seleccionar una red virtual, se devuelven toohello **red Virtual** haga clic en la subred de hello en lista de hello en parte inferior de Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f441-121">After selecting a virtual network, you are returned toohello **Virtual network** Click hello subnet in hello list at hello bottom of hello blade.</span></span>

    ![Lista de subredes](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    <span data-ttu-id="4f441-123">se muestra la hoja de la subred del laboratorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="4f441-123">hello Lab Subnet blade is displayed.</span></span>

    ![Hoja de la subred de laboratorio](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. <span data-ttu-id="4f441-125">Especifique un **nombre de subred de laboratorio**.</span><span class="sxs-lookup"><span data-stu-id="4f441-125">Specify a **Lab subnet name**.</span></span>
12. <span data-ttu-id="4f441-126">tooallow un toobe de subred utilizado en laboratorio creación de VM, seleccione **uso en la creación de máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="4f441-126">tooallow a subnet toobe used in lab VM creation, select **Use in virtual machine creation**.</span></span>
13. <span data-ttu-id="4f441-127">tooenable una [comparten la dirección IP pública](devtest-lab-shared-ip.md), seleccione **habilitar la IP pública compartida**.</span><span class="sxs-lookup"><span data-stu-id="4f441-127">tooenable a [shared public IP address](devtest-lab-shared-ip.md), select **Enable shared public IP**.</span></span>
14. <span data-ttu-id="4f441-128">Seleccione tooallow de direcciones IP públicas en una subred, **permiten la creación de IP pública**.</span><span class="sxs-lookup"><span data-stu-id="4f441-128">tooallow public IP addresses in a subnet, select **Allow public IP creation**.</span></span>
15. <span data-ttu-id="4f441-129">Hola **máquinas virtuales de máximo por usuario** , especifique Hola máximas máquinas virtuales por usuario para cada subred.</span><span class="sxs-lookup"><span data-stu-id="4f441-129">In hello **Maximum virtual machines per user** field, specify hello maximum VMs per user for each subnet.</span></span> <span data-ttu-id="4f441-130">Si quiere un número ilimitado de máquinas virtuales, deje este campo en blanco.</span><span class="sxs-lookup"><span data-stu-id="4f441-130">If you want an unrestricted number of VMs, leave this field blank.</span></span>
16. <span data-ttu-id="4f441-131">Seleccione **Aceptar** hoja de subred del laboratorio de tooclose Hola.</span><span class="sxs-lookup"><span data-stu-id="4f441-131">Select **OK** tooclose hello Lab Subnet blade.</span></span>
17. <span data-ttu-id="4f441-132">Seleccione **guardar** hoja de red Virtual de tooclose Hola.</span><span class="sxs-lookup"><span data-stu-id="4f441-132">Select **Save** tooclose hello Virtual network blade.</span></span>
18. <span data-ttu-id="4f441-133">Ahora que hello red virtual está configurada, se puede seleccionar al crear una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4f441-133">Now that hello virtual network is configured, it can be selected when creating a VM.</span></span> 
    <span data-ttu-id="4f441-134">toosee cómo toocreate una máquina virtual y especifique una red virtual, consulte el artículo toohello, [agregar una máquina virtual con el laboratorio de artefactos tooa](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="4f441-134">toosee how toocreate a VM and specify a virtual network, refer toohello article, [Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md).</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="4f441-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4f441-135">Next steps</span></span>
<span data-ttu-id="4f441-136">Cuando haya agregado Hola deseado laboratorio tooyour de red virtual, paso siguiente hello es demasiado[agregar un laboratorio VM tooyour](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="4f441-136">Once you have added hello desired virtual network tooyour lab, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

