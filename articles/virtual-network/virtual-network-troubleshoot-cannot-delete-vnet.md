---
title: aaaCannot eliminar una red virtual de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tootroubleshoot Hola problema en el que no se puede eliminar una red virtual en Azure."
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: genli
ms.openlocfilehash: a9050ab238ccb0380fd46130430222efb8f42388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-failed-toodelete-a-virtual-network-in-azure"></a><span data-ttu-id="1d143-103">Solución de problemas: No se pudo toodelete una red virtual en Azure</span><span class="sxs-lookup"><span data-stu-id="1d143-103">Troubleshooting: Failed toodelete a virtual network in Azure</span></span>

<span data-ttu-id="1d143-104">Puede recibir errores cuando intente toodelete una red virtual en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1d143-104">You might receive errors when you try toodelete a virtual network in Microsoft Azure.</span></span> <span data-ttu-id="1d143-105">Este artículo proporciona toohelp de pasos de solución de problemas para resolver este problema.</span><span class="sxs-lookup"><span data-stu-id="1d143-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a><span data-ttu-id="1d143-106">Guía de solución de problemas</span><span class="sxs-lookup"><span data-stu-id="1d143-106">Troubleshooting guidance</span></span> 

1. <span data-ttu-id="1d143-107">[Compruebe si una puerta de enlace de red virtual se ejecuta en la red virtual de hello](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="1d143-107">[Check whether a virtual network gateway is running in hello virtual network](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span></span>
2. <span data-ttu-id="1d143-108">[Compruebe si una puerta de enlace de la aplicación se ejecuta en la red virtual de hello](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="1d143-108">[Check whether an application gateway is running in hello virtual network](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span></span>
3. <span data-ttu-id="1d143-109">[Comprobar si el servicio del dominio de Active Directory de Azure está habilitada en la red virtual de hello](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="1d143-109">[Check whether Azure Active Directory Domain Service is enabled in hello virtual network](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span></span>
4. <span data-ttu-id="1d143-110">[Comprobar si la red virtual de Hola se tooother conectado recursos](#check-whether-the-virtual-network-is-connected-to-other-resource).</span><span class="sxs-lookup"><span data-stu-id="1d143-110">[Check whether hello virtual network is connected tooother resource](#check-whether-the-virtual-network-is-connected-to-other-resource).</span></span>
5. <span data-ttu-id="1d143-111">[Comprobar si una máquina virtual todavía se está ejecutando en la red virtual de hello](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="1d143-111">[Check whether a virtual machine is still running in hello virtual network](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span></span>
6. <span data-ttu-id="1d143-112">[Compruebe si la red virtual de hello está atascada en migración](#check-whether-the-virtual-network-is-stuck-in-migration).</span><span class="sxs-lookup"><span data-stu-id="1d143-112">[Check whether hello virtual network is stuck in migration](#check-whether-the-virtual-network-is-stuck-in-migration).</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="1d143-113">Pasos para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="1d143-113">Troubleshooting steps</span></span>

### <a name="check-whether-a-virtual-network-gateway-is-running-in-hello-virtual-network"></a><span data-ttu-id="1d143-114">Compruebe si una puerta de enlace de red virtual se ejecuta en la red virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="1d143-114">Check whether a virtual network gateway is running in hello virtual network</span></span>

<span data-ttu-id="1d143-115">red virtual de tooremove hello, primero debe quitar la puerta de enlace de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d143-115">tooremove hello virtual network, you must first remove hello virtual network gateway.</span></span>

<span data-ttu-id="1d143-116">Para las redes virtuales clásicas, visite toohello **Introducción** página de red virtual clásica de Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="1d143-116">For classic virtual networks, go toohello **Overview** page of hello classic virtual network in hello Azure portal.</span></span> <span data-ttu-id="1d143-117">Hola **conexiones VPN** sección, si se ejecuta la puerta de enlace de hello en red virtual de hello, verá Hola IP dirección de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d143-117">In hello **VPN connections** section, if hello gateway is running in hello virtual network, you will see hello IP address of hello gateway.</span></span> 

![Compruebe si la puerta de enlace se está ejecutando](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

<span data-ttu-id="1d143-119">Para las redes virtuales, consulte toohello **Introducción** página de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d143-119">For virtual networks, go toohello **Overview** page of hello virtual network.</span></span> <span data-ttu-id="1d143-120">Comprobar **dispositivos conectados** para puerta de enlace de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d143-120">Check **Connected devices** for hello virtual network gateway.</span></span>

![Compruebe el dispositivo conectado Hola](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

<span data-ttu-id="1d143-122">Antes de poder quitar la puerta de enlace de hello, quite primero cualquier **conexión** objetos de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d143-122">Before you can remove hello gateway, first remove any **Connection** objects in hello gateway.</span></span> 

### <a name="check-whether-an-application-gateway-is-running-in-hello-virtual-network"></a><span data-ttu-id="1d143-123">Compruebe si una puerta de enlace de la aplicación se ejecuta en la red virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="1d143-123">Check whether an application gateway is running in hello virtual network</span></span>

<span data-ttu-id="1d143-124">Vaya toohello **Introducción** página de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d143-124">Go toohello **Overview** page of hello virtual network.</span></span> <span data-ttu-id="1d143-125">Comprobar hello **dispositivos conectados** para puerta de enlace de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="1d143-125">Check hello **Connected devices** for hello application gateway.</span></span>

![Compruebe el dispositivo conectado Hola](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

<span data-ttu-id="1d143-127">Si hay una puerta de enlace de la aplicación, debe quitarlo antes de poder eliminar la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d143-127">If there is an application gateway, you must remove it before you can delete hello virtual network.</span></span>

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-hello-virtual-network"></a><span data-ttu-id="1d143-128">Comprobar si el servicio del dominio de Active Directory de Azure está habilitada en la red virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="1d143-128">Check whether Azure Active Directory Domain Service is enabled in hello virtual network</span></span>

<span data-ttu-id="1d143-129">Si Hola servicios de dominio de Active Directory está habilitado y conectado toohello red virtual, no se puede eliminar esta red virtual.</span><span class="sxs-lookup"><span data-stu-id="1d143-129">If hello Active Directory Domain Service is enabled and connected toohello virtual network, you cannot delete this virtual network.</span></span> 

![Compruebe el dispositivo conectado Hola](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

<span data-ttu-id="1d143-131">toodisable Hola servicio, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="1d143-131">toodisable hello service, follow these steps:</span></span>

1. <span data-ttu-id="1d143-132">Vaya toohello [portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="1d143-132">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="1d143-133">En el panel izquierdo de hello, seleccione **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d143-133">In hello left pane, select  **Active Directory**.</span></span>
3. <span data-ttu-id="1d143-134">Seleccione el directorio de Azure Active Directory (Azure AD) de Hola que tiene el servicio de dominio de Active Directory habilitado.</span><span class="sxs-lookup"><span data-stu-id="1d143-134">Select hello Azure Active Directory (Azure AD) directory that has Active Directory Domain Service enabled.</span></span>
4. <span data-ttu-id="1d143-135">Seleccione hello **configurar** ficha.</span><span class="sxs-lookup"><span data-stu-id="1d143-135">Select hello **Configure** tab.</span></span>
5. <span data-ttu-id="1d143-136">En **los servicios de dominio**, cambiar hello **habilitar los servicios de dominio para este directorio** opción demasiado**No**.</span><span class="sxs-lookup"><span data-stu-id="1d143-136">Under **domain services**, change hello **Enable domain services for this directory** option too**No**.</span></span>  

### <a name="check-whether-hello-virtual-network-is-connected-tooother-resource"></a><span data-ttu-id="1d143-137">Comprobar si la red virtual de Hola se recursos tooother conectado</span><span class="sxs-lookup"><span data-stu-id="1d143-137">Check whether hello virtual network is connected tooother resource</span></span>

<span data-ttu-id="1d143-138">Busque vínculos de circuito, conexiones y emparejamientos de red virtual.</span><span class="sxs-lookup"><span data-stu-id="1d143-138">Check for Circuit Links, connections, and virtual network peerings.</span></span> <span data-ttu-id="1d143-139">Cualquiera de ellos puede producir un toofail de eliminación de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="1d143-139">Any of these can cause a virtual network deletion toofail.</span></span> 

<span data-ttu-id="1d143-140">Hello orden de eliminación recomendada es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="1d143-140">hello recommended deletion order is as follows:</span></span>

1. <span data-ttu-id="1d143-141">Conexiones de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="1d143-141">Gateway connections</span></span>
2. <span data-ttu-id="1d143-142">Puertas de enlace</span><span class="sxs-lookup"><span data-stu-id="1d143-142">Gateways</span></span>
3. <span data-ttu-id="1d143-143">Direcciones IP</span><span class="sxs-lookup"><span data-stu-id="1d143-143">IPs</span></span>
4. <span data-ttu-id="1d143-144">Emparejamientos de red virtual</span><span class="sxs-lookup"><span data-stu-id="1d143-144">Virtual network peerings</span></span>
5. <span data-ttu-id="1d143-145">App Service Environment (ASE)</span><span class="sxs-lookup"><span data-stu-id="1d143-145">App Service Environment (ASE)</span></span>

### <a name="check-whether-a-virtual-machine-is-still-running-in-hello-virtual-network"></a><span data-ttu-id="1d143-146">Comprobar si una máquina virtual todavía se está ejecutando en la red virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="1d143-146">Check whether a virtual machine is still running in hello virtual network</span></span>

<span data-ttu-id="1d143-147">Asegúrese de que ninguna máquina virtual está en red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d143-147">Make sure that no virtual machine is in hello virtual network.</span></span>

### <a name="check-whether-hello-virtual-network-is-stuck-in-migration"></a><span data-ttu-id="1d143-148">Compruebe si la red virtual de hello está atascada en migración</span><span class="sxs-lookup"><span data-stu-id="1d143-148">Check whether hello virtual network is stuck in migration</span></span>

<span data-ttu-id="1d143-149">Si la red virtual de Hola se quede en un estado de migración, no se puede eliminar.</span><span class="sxs-lookup"><span data-stu-id="1d143-149">If hello virtual network is stuck in a migration state, it cannot be deleted.</span></span> <span data-ttu-id="1d143-150">Ejecute hello después de la migración de hello tooabort de comando y, a continuación, eliminar la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d143-150">Run hello following command tooabort hello migration, and then delete hello virtual network.</span></span>

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a><span data-ttu-id="1d143-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1d143-151">Next steps</span></span>

- [<span data-ttu-id="1d143-152">Red virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="1d143-152">Azure Virtual Network</span></span>](virtual-networks-overview.md)
- [<span data-ttu-id="1d143-153">Preguntas más frecuentes (P+F) acerca de Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="1d143-153">Azure Virtual Network frequently asked questions (FAQ)</span></span>](virtual-networks-faq.md)