---
title: "interfaz de red aaaHow tooreset para máquina virtual de Windows Azure | Documentos de Microsoft"
description: "Muestra cómo tooreset interfaz de red de VM en Windows Azure"
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
ms.openlocfilehash: 1b653820927ef4c3bb8f384a7e752846a8be3da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-network-interface-for-azure-windows-vm"></a><span data-ttu-id="3cdaf-103">¿Cómo tooreset interfaz de red de VM en Windows Azure</span><span class="sxs-lookup"><span data-stu-id="3cdaf-103">How tooreset network interface for Azure Windows VM</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="3cdaf-104">No se puede conectar la máquina Virtual de Windows Azure (VM) de tooMicrosoft después de deshabilitar de forma predeterminada Hola de interfaz de red (NIC) o se establece manualmente una dirección IP estática para la NIC de Hola.</span><span class="sxs-lookup"><span data-stu-id="3cdaf-104">You cannot connect tooMicrosoft Azure Windows Virtual Machine (VM) after you disable hello default Network Interface (NIC) or manually sets a static IP for hello NIC.</span></span> <span data-ttu-id="3cdaf-105">Este artículo muestra cómo tooreset Hola interfaz de red de máquina virtual de Windows Azure, que se resolverá el problema de conexión remota de Hola.</span><span class="sxs-lookup"><span data-stu-id="3cdaf-105">This article shows how tooreset hello network interface for Azure Windows VM, which will resolve hello remote connection issue.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]
## <a name="reset-network-interface"></a><span data-ttu-id="3cdaf-106">Restablecimiento de la interfaz de red</span><span class="sxs-lookup"><span data-stu-id="3cdaf-106">Reset network interface</span></span>

### <a name="for-classic-vms"></a><span data-ttu-id="3cdaf-107">Para máquinas virtuales clásicas</span><span class="sxs-lookup"><span data-stu-id="3cdaf-107">For Classic VMs</span></span>

<span data-ttu-id="3cdaf-108">red de tooreset de la interfaz, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="3cdaf-108">tooreset network interface, follow these steps:</span></span>

1.  <span data-ttu-id="3cdaf-109">Vaya toohello [portal de Azure]( https://ms.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3cdaf-109">Go toohello [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="3cdaf-110">Seleccione **Máquinas virtuales (clásico)**.</span><span class="sxs-lookup"><span data-stu-id="3cdaf-110">Select **Virtual Machines (Classic)**.</span></span>
3.  <span data-ttu-id="3cdaf-111">Seleccione Hola había afectado Máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="3cdaf-111">Select hello affected Virtual Machine.</span></span>
4.  <span data-ttu-id="3cdaf-112">Seleccione **Direcciones IP**.</span><span class="sxs-lookup"><span data-stu-id="3cdaf-112">Select **IP addresses**.</span></span>
5.  <span data-ttu-id="3cdaf-113">Si hello **asignación de IP privada** no **estático**, también cambian**estático**.</span><span class="sxs-lookup"><span data-stu-id="3cdaf-113">If hello **Private IP assignment**  is not  **Static**, change it too**Static**.</span></span>
6.  <span data-ttu-id="3cdaf-114">Hola de cambio **dirección IP** dirección IP de tooanother que está disponible en hello subred.</span><span class="sxs-lookup"><span data-stu-id="3cdaf-114">Change hello **IP address** tooanother IP address that is available in hello Subnet.</span></span>
7.  <span data-ttu-id="3cdaf-115">Seleccione Guardar.</span><span class="sxs-lookup"><span data-stu-id="3cdaf-115">Select Save.</span></span>
8.  <span data-ttu-id="3cdaf-116">máquina virtual de Hello reiniciará tooinitialize Hola nuevo NIC toohello sistema.</span><span class="sxs-lookup"><span data-stu-id="3cdaf-116">hello virtual machine will restart tooinitialize hello new NIC toohello system.</span></span>
9.  <span data-ttu-id="3cdaf-117">Intente tooRDP tooyour máquina.</span><span class="sxs-lookup"><span data-stu-id="3cdaf-117">Try tooRDP tooyour machine.</span></span> <span data-ttu-id="3cdaf-118">Si se realiza correctamente, puede cambiar Hola original de toohello inversa de dirección de IP privada si lo desea.</span><span class="sxs-lookup"><span data-stu-id="3cdaf-118">If successful, you can change hello Private IP address back toohello original if you would like.</span></span> <span data-ttu-id="3cdaf-119">De lo contrario, manténgala.</span><span class="sxs-lookup"><span data-stu-id="3cdaf-119">Otherwise, you can keep it.</span></span> 

### <a name="for-vms-deployed-in-resource-group-model"></a><span data-ttu-id="3cdaf-120">Para máquinas virtuales implementadas en el módulo de grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="3cdaf-120">For VMs deployed in Resource group model</span></span>

1.  <span data-ttu-id="3cdaf-121">Vaya toohello [portal de Azure]( https://ms.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3cdaf-121">Go toohello [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="3cdaf-122">Seleccione Hola había afectado Máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="3cdaf-122">Select hello affected Virtual Machine.</span></span>
3.  <span data-ttu-id="3cdaf-123">Seleccione **Interfaces de red**.</span><span class="sxs-lookup"><span data-stu-id="3cdaf-123">Select **Network Interfaces**.</span></span>
4.  <span data-ttu-id="3cdaf-124">Seleccione Hola que asociado la interfaz de red con el equipo</span><span class="sxs-lookup"><span data-stu-id="3cdaf-124">Select hello Network Interface associated with your machine</span></span>
5.  <span data-ttu-id="3cdaf-125">Seleccione **Configuraciones IP**.</span><span class="sxs-lookup"><span data-stu-id="3cdaf-125">Select **IP configurations**.</span></span>
6.  <span data-ttu-id="3cdaf-126">Seleccione IP Hola.</span><span class="sxs-lookup"><span data-stu-id="3cdaf-126">Select hello IP.</span></span> 
7.  <span data-ttu-id="3cdaf-127">Si hello **asignación de IP privada** no **estático**, también cambian**estático**.</span><span class="sxs-lookup"><span data-stu-id="3cdaf-127">If hello **Private IP assignment**  is not  **Static**, change it too**Static**.</span></span>
8.  <span data-ttu-id="3cdaf-128">Hola de cambio **dirección IP** dirección IP de tooanother que está disponible en hello subred.</span><span class="sxs-lookup"><span data-stu-id="3cdaf-128">Change hello **IP address** tooanother IP address that is available in hello Subnet.</span></span>
9. <span data-ttu-id="3cdaf-129">máquina virtual de Hello reiniciará tooinitialize Hola nuevo NIC toohello sistema.</span><span class="sxs-lookup"><span data-stu-id="3cdaf-129">hello virtual machine will restart tooinitialize hello new NIC toohello system.</span></span>
10. <span data-ttu-id="3cdaf-130">Intente tooRDP tooyour máquina.</span><span class="sxs-lookup"><span data-stu-id="3cdaf-130">Try tooRDP tooyour machine.</span></span> <span data-ttu-id="3cdaf-131">Si se realiza correctamente, puede cambiar Hola original de toohello inversa de dirección de IP privada si lo desea.</span><span class="sxs-lookup"><span data-stu-id="3cdaf-131">If successful, you can change hello Private IP address back toohello original if you would like.</span></span> <span data-ttu-id="3cdaf-132">De lo contrario, manténgala.</span><span class="sxs-lookup"><span data-stu-id="3cdaf-132">Otherwise, you can keep it.</span></span> 

## <a name="delete-hello-unavailable-nics"></a><span data-ttu-id="3cdaf-133">Eliminar Hola NIC no está disponible</span><span class="sxs-lookup"><span data-stu-id="3cdaf-133">Delete hello unavailable NICs</span></span>
<span data-ttu-id="3cdaf-134">Después puede máquina toohello de escritorio remoto, debe eliminar Hola antigua NIC tooavoid Hola posible problema:</span><span class="sxs-lookup"><span data-stu-id="3cdaf-134">After you can remote desktop toohello machine, you must delete hello old NICs tooavoid hello potential problem:</span></span>

1.  <span data-ttu-id="3cdaf-135">Abra el Administrador de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="3cdaf-135">Open Device Manager.</span></span>
2.  <span data-ttu-id="3cdaf-136">Seleccione **Vista** > **Mostrar dispositivos ocultos**.</span><span class="sxs-lookup"><span data-stu-id="3cdaf-136">Select **View** > **Show hidden devices**.</span></span>
3.  <span data-ttu-id="3cdaf-137">Seleccione **Adaptadores de red**.</span><span class="sxs-lookup"><span data-stu-id="3cdaf-137">Select **Network Adapters**.</span></span> 
4.  <span data-ttu-id="3cdaf-138">Compruebe si los adaptadores de hello denominados como "Adaptador de red de Hyper-V de Microsoft".</span><span class="sxs-lookup"><span data-stu-id="3cdaf-138">Check for hello adapters named as "Microsoft Hyper-V Network Adapter".</span></span>
5.  <span data-ttu-id="3cdaf-139">Puede que vea un adaptador no disponible atenuado. Haga clic en el adaptador de hello y, a continuación, seleccione Desinstalar.</span><span class="sxs-lookup"><span data-stu-id="3cdaf-139">You might see an unavailable adapter that is grayed out. Right-click hello adapter and then select Uninstall.</span></span>

    ![imagen de Hola de hello NIC](media/reset-network-interface/nicpage.png)

    > [!NOTE]
    > <span data-ttu-id="3cdaf-141">Solo la desinstalación de adaptadores disponibles Hola que tienen el nombre de Hola "Adaptador de red de Hyper-V de Microsoft".</span><span class="sxs-lookup"><span data-stu-id="3cdaf-141">Only uninstall hello unavailable adapters that have hello name "Microsoft Hyper-V Network Adapter".</span></span> <span data-ttu-id="3cdaf-142">Si desinstala cualquiera de hello otros adaptadores ocultos, podrían producirse problemas adicionales.</span><span class="sxs-lookup"><span data-stu-id="3cdaf-142">If you uninstall any of hello other hidden adapters, it could cause additional issues.</span></span>
    >
    >

6.  <span data-ttu-id="3cdaf-143">Ahora deben borrarse todos los adaptadores no disponibles del sistema.</span><span class="sxs-lookup"><span data-stu-id="3cdaf-143">Now all unavailable adapter should be cleared out from your system.</span></span>