---
title: Restablecimiento de la interfaz de red para VM de Microsoft Azure| Microsoft Docs
description: "Muestra cómo restablecer la interfaz de red para VM de Microsoft Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: genli
ms.openlocfilehash: 220e426be20086841854d89831f6c9d67529867f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-network-interface-for-azure-windows-vm"></a><span data-ttu-id="d234d-103">Restablecimiento de la interfaz de red para VM de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d234d-103">How to reset network interface for Azure Windows VM</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="d234d-104">No puede conectarse a la máquina virtual (VM) de Microsoft Azure después de deshabilitar la interfaz de red (NIC) predeterminada o de establecer manualmente un IP estático para la NIC.</span><span class="sxs-lookup"><span data-stu-id="d234d-104">You cannot connect to Microsoft Azure Windows Virtual Machine (VM) after you disable the default Network Interface (NIC) or manually sets a static IP for the NIC.</span></span> <span data-ttu-id="d234d-105">Este artículo muestra cómo restablecer la interfaz de red para la máquina virtual de Microsoft Azure, que resolverá el problema de conexión remota.</span><span class="sxs-lookup"><span data-stu-id="d234d-105">This article shows how to reset the network interface for Azure Windows VM, which will resolve the remote connection issue.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]
## <a name="reset-network-interface"></a><span data-ttu-id="d234d-106">Restablecimiento de la interfaz de red</span><span class="sxs-lookup"><span data-stu-id="d234d-106">Reset network interface</span></span>

### <a name="for-classic-vms"></a><span data-ttu-id="d234d-107">Para máquinas virtuales clásicas</span><span class="sxs-lookup"><span data-stu-id="d234d-107">For Classic VMs</span></span>

<span data-ttu-id="d234d-108">Para restablecer la interfaz de red, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="d234d-108">To reset network interface, follow these steps:</span></span>

1.  <span data-ttu-id="d234d-109">Vaya al [Portal de Azure]( https://ms.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d234d-109">Go to the [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="d234d-110">Seleccione **Máquinas virtuales (clásico)**.</span><span class="sxs-lookup"><span data-stu-id="d234d-110">Select **Virtual Machines (Classic)**.</span></span>
3.  <span data-ttu-id="d234d-111">Seleccione la máquina virtual afectada.</span><span class="sxs-lookup"><span data-stu-id="d234d-111">Select the affected Virtual Machine.</span></span>
4.  <span data-ttu-id="d234d-112">Seleccione **Direcciones IP**.</span><span class="sxs-lookup"><span data-stu-id="d234d-112">Select **IP addresses**.</span></span>
5.  <span data-ttu-id="d234d-113">Si la **Asignación de IP privada** no es  **Estática**, cámbiela a **Estática**.</span><span class="sxs-lookup"><span data-stu-id="d234d-113">If the **Private IP assignment**  is not  **Static**, change it to **Static**.</span></span>
6.  <span data-ttu-id="d234d-114">Cambie la **Dirección IP** a otra dirección IP disponible en la subred.</span><span class="sxs-lookup"><span data-stu-id="d234d-114">Change the **IP address** to another IP address that is available in the Subnet.</span></span>
7.  <span data-ttu-id="d234d-115">Seleccione Guardar.</span><span class="sxs-lookup"><span data-stu-id="d234d-115">Select Save.</span></span>
8.  <span data-ttu-id="d234d-116">La máquina virtual se reiniciará para inicializar la nueva NIC en el sistema.</span><span class="sxs-lookup"><span data-stu-id="d234d-116">The virtual machine will restart to initialize the new NIC to the system.</span></span>
9.  <span data-ttu-id="d234d-117">Intente utilizar RDP en la máquina.</span><span class="sxs-lookup"><span data-stu-id="d234d-117">Try to RDP to your machine.</span></span> <span data-ttu-id="d234d-118">Si la operación se realiza correctamente, puede volver a la dirección IP privada original si lo desea.</span><span class="sxs-lookup"><span data-stu-id="d234d-118">If successful, you can change the Private IP address back to the original if you would like.</span></span> <span data-ttu-id="d234d-119">De lo contrario, manténgala.</span><span class="sxs-lookup"><span data-stu-id="d234d-119">Otherwise, you can keep it.</span></span> 

### <a name="for-vms-deployed-in-resource-group-model"></a><span data-ttu-id="d234d-120">Para máquinas virtuales implementadas en el módulo de grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="d234d-120">For VMs deployed in Resource group model</span></span>

1.  <span data-ttu-id="d234d-121">Vaya al [Portal de Azure]( https://ms.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d234d-121">Go to the [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="d234d-122">Seleccione la máquina virtual afectada.</span><span class="sxs-lookup"><span data-stu-id="d234d-122">Select the affected Virtual Machine.</span></span>
3.  <span data-ttu-id="d234d-123">Seleccione **Interfaces de red**.</span><span class="sxs-lookup"><span data-stu-id="d234d-123">Select **Network Interfaces**.</span></span>
4.  <span data-ttu-id="d234d-124">Seleccione la interfaz de red asociada a la máquina.</span><span class="sxs-lookup"><span data-stu-id="d234d-124">Select the Network Interface associated with your machine</span></span>
5.  <span data-ttu-id="d234d-125">Seleccione **Configuraciones IP**.</span><span class="sxs-lookup"><span data-stu-id="d234d-125">Select **IP configurations**.</span></span>
6.  <span data-ttu-id="d234d-126">Seleccione la IP.</span><span class="sxs-lookup"><span data-stu-id="d234d-126">Select the IP.</span></span> 
7.  <span data-ttu-id="d234d-127">Si la **Asignación de IP privada** no es  **Estática**, cámbiela a **Estática**.</span><span class="sxs-lookup"><span data-stu-id="d234d-127">If the **Private IP assignment**  is not  **Static**, change it to **Static**.</span></span>
8.  <span data-ttu-id="d234d-128">Cambie la **Dirección IP** a otra dirección IP disponible en la subred.</span><span class="sxs-lookup"><span data-stu-id="d234d-128">Change the **IP address** to another IP address that is available in the Subnet.</span></span>
9. <span data-ttu-id="d234d-129">La máquina virtual se reiniciará para inicializar la nueva NIC en el sistema.</span><span class="sxs-lookup"><span data-stu-id="d234d-129">The virtual machine will restart to initialize the new NIC to the system.</span></span>
10. <span data-ttu-id="d234d-130">Intente utilizar RDP en la máquina.</span><span class="sxs-lookup"><span data-stu-id="d234d-130">Try to RDP to your machine.</span></span> <span data-ttu-id="d234d-131">Si la operación se realiza correctamente, puede volver a la dirección IP privada original si lo desea.</span><span class="sxs-lookup"><span data-stu-id="d234d-131">If successful, you can change the Private IP address back to the original if you would like.</span></span> <span data-ttu-id="d234d-132">De lo contrario, manténgala.</span><span class="sxs-lookup"><span data-stu-id="d234d-132">Otherwise, you can keep it.</span></span> 

## <a name="delete-the-unavailable-nics"></a><span data-ttu-id="d234d-133">Eliminación de las NIC no disponibles</span><span class="sxs-lookup"><span data-stu-id="d234d-133">Delete the unavailable NICs</span></span>
<span data-ttu-id="d234d-134">Cuando pueda utilizar el escritorio remoto en la máquina, debe eliminar las NIC antiguas para evitar el posible problema:</span><span class="sxs-lookup"><span data-stu-id="d234d-134">After you can remote desktop to the machine, you must delete the old NICs to avoid the potential problem:</span></span>

1.  <span data-ttu-id="d234d-135">Abra el Administrador de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d234d-135">Open Device Manager.</span></span>
2.  <span data-ttu-id="d234d-136">Seleccione **Vista** > **Mostrar dispositivos ocultos**.</span><span class="sxs-lookup"><span data-stu-id="d234d-136">Select **View** > **Show hidden devices**.</span></span>
3.  <span data-ttu-id="d234d-137">Seleccione **Adaptadores de red**.</span><span class="sxs-lookup"><span data-stu-id="d234d-137">Select **Network Adapters**.</span></span> 
4.  <span data-ttu-id="d234d-138">Compruebe que los adaptadores tengan el nombre de "Adaptador de red Microsoft Hyper-V".</span><span class="sxs-lookup"><span data-stu-id="d234d-138">Check for the adapters named as "Microsoft Hyper-V Network Adapter".</span></span>
5.  <span data-ttu-id="d234d-139">Puede que vea un adaptador no disponible atenuado.</span><span class="sxs-lookup"><span data-stu-id="d234d-139">You might see an unavailable adapter that is grayed out.</span></span> <span data-ttu-id="d234d-140">Haga clic con el botón derecho en el adaptador y, a continuación, seleccione Desinstalar.</span><span class="sxs-lookup"><span data-stu-id="d234d-140">Right-click the adapter and then select Uninstall.</span></span>

    ![la imagen de la NIC](media/reset-network-interface/nicpage.png)

    > [!NOTE]
    > <span data-ttu-id="d234d-142">Solo desinstale los adaptadores no disponibles con el nombre "Adaptador de red de Microsoft Hyper-V".</span><span class="sxs-lookup"><span data-stu-id="d234d-142">Only uninstall the unavailable adapters that have the name "Microsoft Hyper-V Network Adapter".</span></span> <span data-ttu-id="d234d-143">Si desinstala alguno de los adaptadores ocultos, podrían producirse problemas adicionales.</span><span class="sxs-lookup"><span data-stu-id="d234d-143">If you uninstall any of the other hidden adapters, it could cause additional issues.</span></span>
    >
    >

6.  <span data-ttu-id="d234d-144">Ahora deben borrarse todos los adaptadores no disponibles del sistema.</span><span class="sxs-lookup"><span data-stu-id="d234d-144">Now all unavailable adapter should be cleared out from your system.</span></span>