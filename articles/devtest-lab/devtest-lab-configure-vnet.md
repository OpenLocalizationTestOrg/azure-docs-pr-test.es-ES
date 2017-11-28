---
title: "Configuración de una red virtual en Azure DevTest Labs | Microsoft Docs"
description: "Aprenda a configurar una red virtual existente y la subred y a usarlas en una máquina virtual con Azure DevTest Labs."
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
ms.openlocfilehash: 848752085729df7d98a3a4b7be36d894c12cd033
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a><span data-ttu-id="55925-103">Configuración de una red virtual en Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="55925-103">Configure a virtual network in Azure DevTest Labs</span></span>
<span data-ttu-id="55925-104">Como se explica en el artículo [Incorporación de una máquina virtual con artefactos a un laboratorio](devtest-lab-add-vm-with-artifacts.md), al crear una máquina virtual en un laboratorio, puede especificar una red virtual configurada.</span><span class="sxs-lookup"><span data-stu-id="55925-104">As explained in the article, [Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md), when you create a VM in a lab, you can specify a configured virtual network.</span></span> <span data-ttu-id="55925-105">Una situación en la que se podría aplicar esto es si necesita acceder a los recursos de la red corporativa desde las máquinas virtuales mediante la red virtual que se ha configurado con ExpressRoute o VPN de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="55925-105">One scenario for doing this is if you need to access your corpnet resources from your VMs using the virtual network that was configured with ExpressRoute or site-to-site VPN.</span></span> <span data-ttu-id="55925-106">En las siguientes secciones se muestra cómo agregar la red virtual existente a la configuración de red virtual del laboratorio de modo que esté disponible para seleccionarse al crear las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="55925-106">The following sections illustrate how to add your existing virtual network into a lab's Virtual Network settings so that it is available to choose when creating VMs.</span></span>

## <a name="configure-a-virtual-network-for-a-lab-using-the-azure-portal"></a><span data-ttu-id="55925-107">Configuración de una red virtual para un laboratorio mediante el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="55925-107">Configure a virtual network for a lab using the Azure portal</span></span>
<span data-ttu-id="55925-108">Los pasos siguientes le guiarán en el proceso de agregar una red virtual existente (y la subred) a un laboratorio para que esta se pueda utilizar al crear una máquina virtual en el mismo laboratorio.</span><span class="sxs-lookup"><span data-stu-id="55925-108">The following steps walk you through adding an existing virtual network (and subnet) to a lab so that it can be used when creating a VM in the same lab.</span></span> 

1. <span data-ttu-id="55925-109">Inicie sesión en el [Portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="55925-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="55925-110">Seleccione **Más servicios** y, luego, **DevTest Labs** en la lista.</span><span class="sxs-lookup"><span data-stu-id="55925-110">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="55925-111">En la lista de laboratorios, seleccione el laboratorio que desee.</span><span class="sxs-lookup"><span data-stu-id="55925-111">From the list of labs, select the desired lab.</span></span> 
4. <span data-ttu-id="55925-112">En la hoja del laboratorio, seleccione **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="55925-112">On the lab's blade, select **Configuration**.</span></span>
5. <span data-ttu-id="55925-113">En la hoja **Configuración** del laboratorio, selecciones **Redes virtuales**.</span><span class="sxs-lookup"><span data-stu-id="55925-113">On the lab's **Configuration** blade, select **Virtual networks**.</span></span>
6. <span data-ttu-id="55925-114">En la hoja **Redes virtuales** , verá una lista de redes virtuales que se han configurado para el laboratorio actual, así como la red virtual predeterminada que se crea para el laboratorio.</span><span class="sxs-lookup"><span data-stu-id="55925-114">On the **Virtual networks** blade, you see a list of virtual networks configured for the current lab as well as the default virtual network that is created for your lab.</span></span> 
7. <span data-ttu-id="55925-115">Seleccione **+Agregar**.</span><span class="sxs-lookup"><span data-stu-id="55925-115">Select **+ Add**.</span></span>
   
    ![Incorporación de una red virtual existente al laboratorio](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. <span data-ttu-id="55925-117">En la hoja **Red virtual**, elija **[Seleccionar red virtual]**.</span><span class="sxs-lookup"><span data-stu-id="55925-117">On the **Virtual network** blade, select **[Select virtual network]**.</span></span>
   
    ![Selección de una red virtual existente](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. <span data-ttu-id="55925-119">En la hoja **Elegir red virtual** , seleccione la red virtual deseada.</span><span class="sxs-lookup"><span data-stu-id="55925-119">On the **Choose virtual network** blade, select the desired virtual network.</span></span> <span data-ttu-id="55925-120">La hoja muestra todas las redes virtuales que están en la misma región de la suscripción que el laboratorio.</span><span class="sxs-lookup"><span data-stu-id="55925-120">The blade shows all the virtual networks that are under the same region in the subscription as the lab.</span></span>  
10. <span data-ttu-id="55925-121">Después de seleccionar una red virtual, se le redirigirá a la **red virtual**. Haga clic en la subred de la lista en la parte inferior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="55925-121">After selecting a virtual network, you are returned to the **Virtual network** Click the subnet in the list at the bottom of the blade.</span></span>

    ![Lista de subredes](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    <span data-ttu-id="55925-123">Se muestra la hoja de la subred de laboratorio.</span><span class="sxs-lookup"><span data-stu-id="55925-123">The Lab Subnet blade is displayed.</span></span>

    ![Hoja de la subred de laboratorio](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. <span data-ttu-id="55925-125">Especifique un **nombre de subred de laboratorio**.</span><span class="sxs-lookup"><span data-stu-id="55925-125">Specify a **Lab subnet name**.</span></span>
12. <span data-ttu-id="55925-126">Para permitir que una subred se utilice en la creación de máquinas virtuales de laboratorio, seleccione **Use in virtual machine creation** (Usar en la creación de máquinas virtuales).</span><span class="sxs-lookup"><span data-stu-id="55925-126">To allow a subnet to be used in lab VM creation, select **Use in virtual machine creation**.</span></span>
13. <span data-ttu-id="55925-127">Para habilitar una [dirección IP pública compartida](devtest-lab-shared-ip.md), seleccione **Habilitar IP pública compartida**.</span><span class="sxs-lookup"><span data-stu-id="55925-127">To enable a [shared public IP address](devtest-lab-shared-ip.md), select **Enable shared public IP**.</span></span>
14. <span data-ttu-id="55925-128">Para permitir direcciones IP públicas en una subred, seleccione **Allow public IP creation** (Permitir IP pública).</span><span class="sxs-lookup"><span data-stu-id="55925-128">To allow public IP addresses in a subnet, select **Allow public IP creation**.</span></span>
15. <span data-ttu-id="55925-129">En el campo **Maximum virtual machines per user** (Número máximo de máquinas virtuales por usuario), especifique el número máximo de máquinas virtuales por usuario para cada subred.</span><span class="sxs-lookup"><span data-stu-id="55925-129">In the **Maximum virtual machines per user** field, specify the maximum VMs per user for each subnet.</span></span> <span data-ttu-id="55925-130">Si quiere un número ilimitado de máquinas virtuales, deje este campo en blanco.</span><span class="sxs-lookup"><span data-stu-id="55925-130">If you want an unrestricted number of VMs, leave this field blank.</span></span>
16. <span data-ttu-id="55925-131">Seleccione **Aceptar** para cerrar la hoja de subred de laboratorio.</span><span class="sxs-lookup"><span data-stu-id="55925-131">Select **OK** to close the Lab Subnet blade.</span></span>
17. <span data-ttu-id="55925-132">Seleccione **Guardar** para cerrar la hoja de red virtual.</span><span class="sxs-lookup"><span data-stu-id="55925-132">Select **Save** to close the Virtual network blade.</span></span>
18. <span data-ttu-id="55925-133">Ahora que está configurada la red virtual, se puede seleccionar al crear una nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="55925-133">Now that the virtual network is configured, it can be selected when creating a VM.</span></span> 
    <span data-ttu-id="55925-134">Para ver cómo crear una máquina virtual y especificar una red virtual, consulte el artículo [Incorporación de una máquina virtual con artefactos a un laboratorio](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="55925-134">To see how to create a VM and specify a virtual network, refer to the article, [Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md).</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="55925-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="55925-135">Next steps</span></span>
<span data-ttu-id="55925-136">Después de agregar las redes virtuales deseadas al laboratorio, el paso siguiente consiste en [agregar una máquina virtual al laboratorio](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="55925-136">Once you have added the desired virtual network to your lab, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

