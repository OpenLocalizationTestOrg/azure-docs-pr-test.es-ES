---
title: "Vinculación de una red virtual a un circuito ExpressRoute mediante PowerShell y Azure clásico | Microsoft Docs"
description: "Este documento proporciona información general sobre cómo vincular redes virtuales a circuitos ExpressRoute mediante el modelo de implementación clásica y PowerShell."
services: expressroute
documentationcenter: na
author: ganesr
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 9b53fd72-9b6b-4844-80b9-4e1d54fd0c17
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/28/2017
ms.author: ganesr
ms.openlocfilehash: 8df8a4c6ff0897c821e13248e0494b17e1a4992d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="a0b93-103">Conexión de una red virtual a un circuito ExpressRoute mediante PowerShell (clásica)</span><span class="sxs-lookup"><span data-stu-id="a0b93-103">Connect a virtual network to an ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a0b93-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="a0b93-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="a0b93-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0b93-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="a0b93-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="a0b93-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="a0b93-107">Vídeo: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a0b93-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="a0b93-108">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="a0b93-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="a0b93-109">Este artículo le ayudará a vincular redes virtuales a circuitos ExpressRoute de Azure a través del modelo de implementación clásica y PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a0b93-109">This article will help you link virtual networks (VNets) to Azure ExpressRoute circuits by using the classic deployment model and PowerShell.</span></span> <span data-ttu-id="a0b93-110">Las redes virtuales pueden estar en la misma suscripción o formar parte de otra suscripción.</span><span class="sxs-lookup"><span data-stu-id="a0b93-110">Virtual networks can either be in the same subscription or can be part of another subscription.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="a0b93-111">**Información sobre los modelos de implementación de Azure**</span><span class="sxs-lookup"><span data-stu-id="a0b93-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a><span data-ttu-id="a0b93-112">Requisitos previos de configuración</span><span class="sxs-lookup"><span data-stu-id="a0b93-112">Configuration prerequisites</span></span>
1. <span data-ttu-id="a0b93-113">Necesitará la versión más reciente de los módulos de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a0b93-113">You need the latest version of the Azure PowerShell modules.</span></span> <span data-ttu-id="a0b93-114">Puede descargar los módulos de PowerShell más recientes desde la sección de PowerShell en la [página de descargas de Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a0b93-114">You can download the latest PowerShell modules from the PowerShell section of the [Azure Downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="a0b93-115">Para obtener instrucciones detalladas sobre cómo configurar el equipo para usar los módulos de Azure PowerShell, siga las instrucciones de la página [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="a0b93-115">Follow the instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) for step-by-step guidance on how to configure your computer to use the Azure PowerShell modules.</span></span>
2. <span data-ttu-id="a0b93-116">Debe revisar los [requisitos previos](expressroute-prerequisites.md), los [requisitos de enrutamiento](expressroute-routing.md) y los [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="a0b93-116">You need to review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
3. <span data-ttu-id="a0b93-117">Tiene que tener un circuito ExpressRoute activo.</span><span class="sxs-lookup"><span data-stu-id="a0b93-117">You must have an active ExpressRoute circuit.</span></span>
   * <span data-ttu-id="a0b93-118">Siga las instrucciones para [crear un circuito ExpressRoute](expressroute-howto-circuit-classic.md) y haga que el proveedor de conectividad habilite el circuito.</span><span class="sxs-lookup"><span data-stu-id="a0b93-118">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have your connectivity provider enable the circuit.</span></span>
   * <span data-ttu-id="a0b93-119">Asegúrese de que dispone de un emparejamiento privado de Azure configurado para el circuito.</span><span class="sxs-lookup"><span data-stu-id="a0b93-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="a0b93-120">Consulte el artículo de [configuración del enrutamiento](expressroute-howto-routing-classic.md) para obtener instrucciones sobre el enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="a0b93-120">See the [Configure routing](expressroute-howto-routing-classic.md) article for routing instructions.</span></span>
   * <span data-ttu-id="a0b93-121">Asegúrese de que el emparejamiento privado de Azure está configurado y el emparejamiento BGP entre la red y Microsoft está activo para habilitar la conectividad de extremo a extremo.</span><span class="sxs-lookup"><span data-stu-id="a0b93-121">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
   * <span data-ttu-id="a0b93-122">Debe crear y aprovisionar totalmente una red virtual y una puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="a0b93-122">You must have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="a0b93-123">Siga las instrucciones para [configurar una red virtual en ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="a0b93-123">Follow the instructions to [configure a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

<span data-ttu-id="a0b93-124">Es posible vincular hasta 10 redes virtuales a un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a0b93-124">You can link up to 10 virtual networks to an ExpressRoute circuit.</span></span> <span data-ttu-id="a0b93-125">Todas las redes virtuales deben estar en la misma región geopolítica.</span><span class="sxs-lookup"><span data-stu-id="a0b93-125">All virtual networks must be in the same geopolitical region.</span></span> <span data-ttu-id="a0b93-126">Puede vincular un mayor número de redes virtuales en el circuito ExpressRoute, o redes virtuales que se encuentren en otras regiones geopolíticas, si habilitó el complemento premium de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a0b93-126">You can link a larger number of virtual networks to your ExpressRoute circuit, or link virtual networks that are in other geopolitical regions if you enabled the ExpressRoute premium add-on.</span></span> <span data-ttu-id="a0b93-127">Consulte las [preguntas más frecuentes](expressroute-faqs.md) para obtener más detalles sobre el complemento premium.</span><span class="sxs-lookup"><span data-stu-id="a0b93-127">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span></span>

## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="a0b93-128">Conexión de una red virtual en la misma suscripción a un circuito</span><span class="sxs-lookup"><span data-stu-id="a0b93-128">Connect a virtual network in the same subscription to a circuit</span></span>
<span data-ttu-id="a0b93-129">Puede vincular una red virtual a un circuito ExpressRoute mediante el siguiente cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a0b93-129">You can link a virtual network to an ExpressRoute circuit by using the following cmdlet.</span></span> <span data-ttu-id="a0b93-130">Asegúrese de que la puerta de enlace de red virtual se crea y está lista para vincular antes de ejecutar el cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a0b93-130">Make sure that the virtual network gateway is created and is ready for linking before you run the cmdlet.</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="a0b93-131">Conexión de una red virtual en una suscripción diferente a un circuito</span><span class="sxs-lookup"><span data-stu-id="a0b93-131">Connect a virtual network in a different subscription to a circuit</span></span>
<span data-ttu-id="a0b93-132">Puede compartir un circuito ExpressRoute entre varias suscripciones.</span><span class="sxs-lookup"><span data-stu-id="a0b93-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="a0b93-133">En la ilustración siguiente se muestra un sencillo esquema de cómo funciona el uso compartido de circuitos ExpressRoute entre varias suscripciones.</span><span class="sxs-lookup"><span data-stu-id="a0b93-133">The following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="a0b93-134">Cada una de las nubes más pequeñas dentro de la nube de gran tamaño se usa para representar las suscripciones que pertenecen a diferentes departamentos dentro de una organización.</span><span class="sxs-lookup"><span data-stu-id="a0b93-134">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span> <span data-ttu-id="a0b93-135">Cada departamento de la organización puede usar su propia suscripción para implementar sus servicios, pero los departamentos pueden compartir un único circuito ExpressRoute para volver a conectarse a la red local.</span><span class="sxs-lookup"><span data-stu-id="a0b93-135">Each of the departments within the organization can use their own subscription for deploying their services--but the departments can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span> <span data-ttu-id="a0b93-136">Un solo departamento (en este ejemplo: TI) puede ser el propietario del circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a0b93-136">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="a0b93-137">Otras suscripciones dentro de la organización pueden usar el circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a0b93-137">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="a0b93-138">Los cargos de conectividad y ancho de banda de un circuito dedicado recaerán en el propietario del circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a0b93-138">Connectivity and bandwidth charges for the dedicated circuit will be applied to the ExpressRoute circuit owner.</span></span> <span data-ttu-id="a0b93-139">Todas las redes virtuales comparten el mismo ancho de banda.</span><span class="sxs-lookup"><span data-stu-id="a0b93-139">All virtual networks share the same bandwidth.</span></span>
> 
> 

![Conectividad entre suscripciones](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a><span data-ttu-id="a0b93-141">Administración</span><span class="sxs-lookup"><span data-stu-id="a0b93-141">Administration</span></span>
<span data-ttu-id="a0b93-142">El *propietario del circuito* es el administrador o coadministrador de la suscripción en la que se crea el circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a0b93-142">The *circuit owner* is the administrator/coadministrator of the subscription in which the ExpressRoute circuit is created.</span></span> <span data-ttu-id="a0b93-143">El propietario del circuito puede autorizar a los administradores o coadministradores de otras suscripciones (denominados *usuarios del circuito*) para que usen el circuito dedicado de su propiedad.</span><span class="sxs-lookup"><span data-stu-id="a0b93-143">The circuit owner can authorize administrators/coadministrators of other subscriptions, referred to as *circuit users*, to use the dedicated circuit that they own.</span></span> <span data-ttu-id="a0b93-144">Los usuarios del circuito autorizados para usar el circuito ExpressRoute de la organización pueden vincular la red virtual de su suscripción al circuito ExpressRoute una vez que estén autorizados.</span><span class="sxs-lookup"><span data-stu-id="a0b93-144">Circuit users who are authorized to use the organization's ExpressRoute circuit can link the virtual network in their subscription to the ExpressRoute circuit after they are authorized.</span></span>

<span data-ttu-id="a0b93-145">El propietario del circuito tiene la capacidad de modificar y revocar las autorizaciones en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="a0b93-145">The circuit owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="a0b93-146">La revocación de una autorización dará como resultado la eliminación de todos los vínculos de la suscripción cuyo acceso se haya revocado.</span><span class="sxs-lookup"><span data-stu-id="a0b93-146">Revoking an authorization will result in all links being deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="a0b93-147">Operaciones del propietario del circuito</span><span class="sxs-lookup"><span data-stu-id="a0b93-147">Circuit owner operations</span></span>

<span data-ttu-id="a0b93-148">**Creación de una autorización**</span><span class="sxs-lookup"><span data-stu-id="a0b93-148">**Creating an authorization**</span></span>

<span data-ttu-id="a0b93-149">El propietario del circuito autoriza a los administradores de otras suscripciones para que usen el circuito especificado.</span><span class="sxs-lookup"><span data-stu-id="a0b93-149">The circuit owner authorizes the administrators of other subscriptions to use the specified circuit.</span></span> <span data-ttu-id="a0b93-150">En el ejemplo siguiente, el administrador del circuito (TI de Contoso) permite que el administrador de otra suscripción (Dev-Test), cree un vínculo de hasta 2 redes virtuales al circuito.</span><span class="sxs-lookup"><span data-stu-id="a0b93-150">In the following example, the administrator of the circuit (Contoso IT) enables the administrator of another subscription (Dev-Test) to link up to two virtual networks to the circuit.</span></span> <span data-ttu-id="a0b93-151">El administrador de TI de Contoso lo permite especificando el identificador de Microsoft de Dev-Test.</span><span class="sxs-lookup"><span data-stu-id="a0b93-151">The Contoso IT administrator enables this by specifying the Dev-Test Microsoft ID.</span></span> <span data-ttu-id="a0b93-152">El cmdlet no envía correo electrónico al identificador de Microsoft especificado.</span><span class="sxs-lookup"><span data-stu-id="a0b93-152">The cmdlet doesn't send email to the specified Microsoft ID.</span></span> <span data-ttu-id="a0b93-153">El propietario del circuito debe notificar de forma explícita al propietario de la otra suscripción que la autorización se ha completado.</span><span class="sxs-lookup"><span data-stu-id="a0b93-153">The circuit owner needs to explicitly notify the other subscription owner that the authorization is complete.</span></span>

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

<span data-ttu-id="a0b93-154">**Revisión de las autorizaciones**</span><span class="sxs-lookup"><span data-stu-id="a0b93-154">**Reviewing authorizations**</span></span>

<span data-ttu-id="a0b93-155">El propietario del circuito puede revisar todas las autorizaciones emitidas en un circuito concreto ejecutando el siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a0b93-155">The circuit owner can review all authorizations that are issued on a particular circuit by running the following cmdlet:</span></span>

    Get-AzureDedicatedCircuitLinkAuthorization -ServiceKey: "**************************"

    Description         : EngineeringTeam
    Limit               : 3
    LinkAuthorizationId : ####################################
    MicrosoftIds        : engadmin@contoso.com
    Used                : 1

    Description         : MarketingTeam
    Limit               : 1
    LinkAuthorizationId : @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    MicrosoftIds        : marketingadmin@contoso.com
    Used                : 0

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : salesadmin@contoso.com
    Used                : 2


<span data-ttu-id="a0b93-156">**Actualización de autorizaciones**</span><span class="sxs-lookup"><span data-stu-id="a0b93-156">**Updating authorizations**</span></span>

<span data-ttu-id="a0b93-157">El propietario del circuito puede modificar las autorizaciones mediante el siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a0b93-157">The circuit owner can modify authorizations by using the following cmdlet:</span></span>

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


<span data-ttu-id="a0b93-158">**Eliminación de autorizaciones**</span><span class="sxs-lookup"><span data-stu-id="a0b93-158">**Deleting authorizations**</span></span>

<span data-ttu-id="a0b93-159">El propietario del circuito puede revocar o eliminar las autorizaciones al usuario ejecutando el siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a0b93-159">The circuit owner can revoke/delete authorizations to the user by running the following cmdlet:</span></span>

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a><span data-ttu-id="a0b93-160">Operaciones del usuario del circuito</span><span class="sxs-lookup"><span data-stu-id="a0b93-160">Circuit user operations</span></span>

<span data-ttu-id="a0b93-161">**Revisión de las autorizaciones**</span><span class="sxs-lookup"><span data-stu-id="a0b93-161">**Reviewing authorizations**</span></span>

<span data-ttu-id="a0b93-162">El usuario del circuito puede revisar las autorizaciones mediante el siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a0b93-162">The circuit user can review authorizations by using the following cmdlet:</span></span>

    Get-AzureAuthorizedDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : ContosoIT
    Location                         : Washington DC
    MaximumAllowedLinks              : 2
    ServiceKey                       : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled
    UsedLinks                        : 0

<span data-ttu-id="a0b93-163">**Canjear autorizaciones de vínculo**</span><span class="sxs-lookup"><span data-stu-id="a0b93-163">**Redeeming link authorizations**</span></span>

<span data-ttu-id="a0b93-164">El usuario del circuito puede ejecutar el siguiente cmdlet para canjear una autorización de vínculo:</span><span class="sxs-lookup"><span data-stu-id="a0b93-164">The circuit user can run the following cmdlet to redeem a link authorization:</span></span>

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

<span data-ttu-id="a0b93-165">Ejecute este comando en la suscripción recién vinculada para la red virtual:</span><span class="sxs-lookup"><span data-stu-id="a0b93-165">Run this command in the newly linked subscription for the virtual network:</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"

## <a name="next-steps"></a><span data-ttu-id="a0b93-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a0b93-166">Next steps</span></span>
<span data-ttu-id="a0b93-167">Para obtener más información acerca de ExpressRoute, consulte [P+F de ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="a0b93-167">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

