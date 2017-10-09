---
title: "Vincular un circuito de ExpressRoute de tooan de red virtual: PowerShell: clásico: Azure | Documentos de Microsoft"
description: "Este documento proporciona información general sobre cómo toolink virtual redes (redes virtuales) tooExpressRoute circuitos utilizando el modelo de implementación clásica de Hola y PowerShell."
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
ms.openlocfilehash: 6b8a01dcd4bbb9618ec3dd438cf0107538fb2a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="db126-103">Conectarse a un circuito de ExpressRoute de tooan de red virtual con PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="db126-103">Connect a virtual network tooan ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="db126-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="db126-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="db126-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="db126-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="db126-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="db126-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="db126-107">Vídeo: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="db126-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="db126-108">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="db126-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="db126-109">Este artículo le ayudará a vincular circuitos ExpressRoute de tooAzure de redes virtuales (Vnet) mediante el modelo de implementación clásica de Hola y PowerShell.</span><span class="sxs-lookup"><span data-stu-id="db126-109">This article will help you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello classic deployment model and PowerShell.</span></span> <span data-ttu-id="db126-110">Redes virtuales pueden ser en Hola misma suscripción o puede formar parte de otra suscripción.</span><span class="sxs-lookup"><span data-stu-id="db126-110">Virtual networks can either be in hello same subscription or can be part of another subscription.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="db126-111">**Información sobre los modelos de implementación de Azure**</span><span class="sxs-lookup"><span data-stu-id="db126-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a><span data-ttu-id="db126-112">Requisitos previos de configuración</span><span class="sxs-lookup"><span data-stu-id="db126-112">Configuration prerequisites</span></span>
1. <span data-ttu-id="db126-113">Necesita la versión más reciente de Hola de módulos de PowerShell de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="db126-113">You need hello latest version of hello Azure PowerShell modules.</span></span> <span data-ttu-id="db126-114">Puede descargar módulos de PowerShell más recientes de Hola de hello sección PowerShell de hello [página de descargas de Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="db126-114">You can download hello latest PowerShell modules from hello PowerShell section of hello [Azure Downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="db126-115">Siga las instrucciones de hello en [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para obtener instrucciones paso a paso acerca de cómo tooconfigure los módulos de PowerShell de Azure de equipo toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="db126-115">Follow hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for step-by-step guidance on how tooconfigure your computer toouse hello Azure PowerShell modules.</span></span>
2. <span data-ttu-id="db126-116">Necesita hello tooreview [requisitos previos](expressroute-prerequisites.md), [requisitos de enrutamiento](expressroute-routing.md), y [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="db126-116">You need tooreview hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
3. <span data-ttu-id="db126-117">Tiene que tener un circuito ExpressRoute activo.</span><span class="sxs-lookup"><span data-stu-id="db126-117">You must have an active ExpressRoute circuit.</span></span>
   * <span data-ttu-id="db126-118">Siga las instrucciones de hello demasiado[crear un circuito ExpressRoute](expressroute-howto-circuit-classic.md) y tener el proveedor de conectividad habilitar circuito Hola.</span><span class="sxs-lookup"><span data-stu-id="db126-118">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have your connectivity provider enable hello circuit.</span></span>
   * <span data-ttu-id="db126-119">Asegúrese de que dispone de un emparejamiento privado de Azure configurado para el circuito.</span><span class="sxs-lookup"><span data-stu-id="db126-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="db126-120">Vea hello [configurar enrutamiento](expressroute-howto-routing-classic.md) artículo para las instrucciones de enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="db126-120">See hello [Configure routing](expressroute-howto-routing-classic.md) article for routing instructions.</span></span>
   * <span data-ttu-id="db126-121">Asegúrese de que el emparejamiento privado Azure está configurado y Hola emparejamiento de BGP entre la red y Microsoft está activo para que se puede habilitar la conectividad de extremo a extremo.</span><span class="sxs-lookup"><span data-stu-id="db126-121">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
   * <span data-ttu-id="db126-122">Debe crear y aprovisionar totalmente una red virtual y una puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="db126-122">You must have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="db126-123">Siga las instrucciones de hello demasiado[configurar una red virtual para ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="db126-123">Follow hello instructions too[configure a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

<span data-ttu-id="db126-124">Puede vincular una too10 redes virtuales tooan circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="db126-124">You can link up too10 virtual networks tooan ExpressRoute circuit.</span></span> <span data-ttu-id="db126-125">Todas las redes virtuales deben estar en hello misma región geopolíticos.</span><span class="sxs-lookup"><span data-stu-id="db126-125">All virtual networks must be in hello same geopolitical region.</span></span> <span data-ttu-id="db126-126">Puede vincular un mayor número de redes virtuales tooyour circuito de ExpressRoute o vincular redes virtuales que se encuentran en otras regiones geopolíticas si ha habilitado el complemento de hello ExpressRoute premium.</span><span class="sxs-lookup"><span data-stu-id="db126-126">You can link a larger number of virtual networks tooyour ExpressRoute circuit, or link virtual networks that are in other geopolitical regions if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="db126-127">Comprobar hello [preguntas más frecuentes sobre](expressroute-faqs.md) para obtener más detalles sobre el complemento de hello premium.</span><span class="sxs-lookup"><span data-stu-id="db126-127">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="db126-128">Conectar una red virtual en hello mismo circuito de tooa de suscripción</span><span class="sxs-lookup"><span data-stu-id="db126-128">Connect a virtual network in hello same subscription tooa circuit</span></span>
<span data-ttu-id="db126-129">Puede vincular un circuito de ExpressRoute de tooan de red virtual mediante el siguiente cmdlet de Hola.</span><span class="sxs-lookup"><span data-stu-id="db126-129">You can link a virtual network tooan ExpressRoute circuit by using hello following cmdlet.</span></span> <span data-ttu-id="db126-130">Asegúrese de que esa puerta de enlace de red virtual de Hola se crea y está listo para crear un vínculo antes de ejecutar el cmdlet de Hola.</span><span class="sxs-lookup"><span data-stu-id="db126-130">Make sure that hello virtual network gateway is created and is ready for linking before you run hello cmdlet.</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="db126-131">Conectar una red virtual en un circuito de tooa otra suscripción</span><span class="sxs-lookup"><span data-stu-id="db126-131">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="db126-132">Puede compartir un circuito ExpressRoute entre varias suscripciones.</span><span class="sxs-lookup"><span data-stu-id="db126-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="db126-133">Hola figura siguiente muestra un sencillo esquema de cómo compartir funciona para los circuitos ExpressRoute en varias suscripciones.</span><span class="sxs-lookup"><span data-stu-id="db126-133">hello following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="db126-134">Cada una de las nubes más pequeñas de hello en nube de gran tamaño hello es toorepresent usado suscripciones que pertenecen los departamentos de toodifferent dentro de una organización.</span><span class="sxs-lookup"><span data-stu-id="db126-134">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="db126-135">Cada uno de los departamentos de Hola de organización de hello puede utilizar su propia suscripción para implementar sus servicios--pero departamentos Hola puede compartir una sola red de ExpressRoute circuito tooconnect tooyour atrás local.</span><span class="sxs-lookup"><span data-stu-id="db126-135">Each of hello departments within hello organization can use their own subscription for deploying their services--but hello departments can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="db126-136">Un departamento único (en este ejemplo: TI) puede poseer el circuito de ExpressRoute Hola.</span><span class="sxs-lookup"><span data-stu-id="db126-136">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="db126-137">Otras suscripciones dentro de la organización de hello pueden utilizar el circuito de ExpressRoute Hola.</span><span class="sxs-lookup"><span data-stu-id="db126-137">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="db126-138">Los cargos de conectividad y ancho de banda para el circuito dedicado de hello será propietario del circuito de ExpressRoute toohello aplicada.</span><span class="sxs-lookup"><span data-stu-id="db126-138">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute circuit owner.</span></span> <span data-ttu-id="db126-139">Todas las redes virtuales compartan Hola mismo ancho de banda.</span><span class="sxs-lookup"><span data-stu-id="db126-139">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![Conectividad entre suscripciones](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a><span data-ttu-id="db126-141">Administración</span><span class="sxs-lookup"><span data-stu-id="db126-141">Administration</span></span>
<span data-ttu-id="db126-142">Hola *propietario del circuito* es Hola administrador o coadministrator de suscripción de hello en qué hello ExpressRoute se crea el circuito.</span><span class="sxs-lookup"><span data-stu-id="db126-142">hello *circuit owner* is hello administrator/coadministrator of hello subscription in which hello ExpressRoute circuit is created.</span></span> <span data-ttu-id="db126-143">Hello propietario del circuito puede autorizar a los administradores/coadministrators de otras suscripciones, que se hace referencia tooas *a los usuarios de circuito*, toouse Hola dedicado circuito que les pertenecen.</span><span class="sxs-lookup"><span data-stu-id="db126-143">hello circuit owner can authorize administrators/coadministrators of other subscriptions, referred tooas *circuit users*, toouse hello dedicated circuit that they own.</span></span> <span data-ttu-id="db126-144">Los usuarios de circuito que son can de circuito de ExpressRoute de la organización de toouse autorizados Hola vinculan la red virtual de hello en su toohello suscripción circuito ExpressRoute después de que están autorizados.</span><span class="sxs-lookup"><span data-stu-id="db126-144">Circuit users who are authorized toouse hello organization's ExpressRoute circuit can link hello virtual network in their subscription toohello ExpressRoute circuit after they are authorized.</span></span>

<span data-ttu-id="db126-145">propietario del circuito Hello tiene Hola power toomodify y revocar las autorizaciones en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="db126-145">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="db126-146">Revocación de una autorización provocará que todos los vínculos que se va a eliminar de suscripción de hello cuyo acceso se ha revocado.</span><span class="sxs-lookup"><span data-stu-id="db126-146">Revoking an authorization will result in all links being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="db126-147">Operaciones del propietario del circuito</span><span class="sxs-lookup"><span data-stu-id="db126-147">Circuit owner operations</span></span>

<span data-ttu-id="db126-148">**Creación de una autorización**</span><span class="sxs-lookup"><span data-stu-id="db126-148">**Creating an authorization**</span></span>

<span data-ttu-id="db126-149">Hello propietario del circuito autoriza a los administradores de Hola de otras suscripciones toouse Hola especificado circuito.</span><span class="sxs-lookup"><span data-stu-id="db126-149">hello circuit owner authorizes hello administrators of other subscriptions toouse hello specified circuit.</span></span> <span data-ttu-id="db126-150">En el siguiente ejemplo de Hola, Administrador de hello del circuito de hello (TI de Contoso) habilita a administrador Hola de otro toolink de suscripción (desarrollo de prueba) de circuito de toohello de tootwo redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="db126-150">In hello following example, hello administrator of hello circuit (Contoso IT) enables hello administrator of another subscription (Dev-Test) toolink up tootwo virtual networks toohello circuit.</span></span> <span data-ttu-id="db126-151">Administrador de TI de Contoso de Hello hace posible mediante la especificación de hello Id. de desarrollo y pruebas de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="db126-151">hello Contoso IT administrator enables this by specifying hello Dev-Test Microsoft ID.</span></span> <span data-ttu-id="db126-152">Hola cmdlet no envía correo electrónico toohello especificado identificador de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="db126-152">hello cmdlet doesn't send email toohello specified Microsoft ID.</span></span> <span data-ttu-id="db126-153">propietario del circuito Hola necesita tooexplicitly notificar Hola otro propietario de la suscripción que Hola autorización ha finalizado.</span><span class="sxs-lookup"><span data-stu-id="db126-153">hello circuit owner needs tooexplicitly notify hello other subscription owner that hello authorization is complete.</span></span>

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

<span data-ttu-id="db126-154">**Revisión de las autorizaciones**</span><span class="sxs-lookup"><span data-stu-id="db126-154">**Reviewing authorizations**</span></span>

<span data-ttu-id="db126-155">propietario del circuito Hola puede revisar todas las autorizaciones que se ejecutan en un circuito concreto mediante la ejecución de hello siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="db126-155">hello circuit owner can review all authorizations that are issued on a particular circuit by running hello following cmdlet:</span></span>

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


<span data-ttu-id="db126-156">**Actualización de autorizaciones**</span><span class="sxs-lookup"><span data-stu-id="db126-156">**Updating authorizations**</span></span>

<span data-ttu-id="db126-157">propietario del circuito Hola puede modificar las autorizaciones mediante Hola siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="db126-157">hello circuit owner can modify authorizations by using hello following cmdlet:</span></span>

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


<span data-ttu-id="db126-158">**Eliminación de autorizaciones**</span><span class="sxs-lookup"><span data-stu-id="db126-158">**Deleting authorizations**</span></span>

<span data-ttu-id="db126-159">propietario del circuito Hola puede revocar o eliminar un autorizaciones toohello usuario ejecutando Hola siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="db126-159">hello circuit owner can revoke/delete authorizations toohello user by running hello following cmdlet:</span></span>

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a><span data-ttu-id="db126-160">Operaciones del usuario del circuito</span><span class="sxs-lookup"><span data-stu-id="db126-160">Circuit user operations</span></span>

<span data-ttu-id="db126-161">**Revisión de las autorizaciones**</span><span class="sxs-lookup"><span data-stu-id="db126-161">**Reviewing authorizations**</span></span>

<span data-ttu-id="db126-162">usuario de circuito de Hello puede revisar las autorizaciones mediante Hola siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="db126-162">hello circuit user can review authorizations by using hello following cmdlet:</span></span>

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

<span data-ttu-id="db126-163">**Canjear autorizaciones de vínculo**</span><span class="sxs-lookup"><span data-stu-id="db126-163">**Redeeming link authorizations**</span></span>

<span data-ttu-id="db126-164">usuario de circuito de Hello puede ejecutar Hola siguiente cmdlet tooredeem una autorización de vínculo:</span><span class="sxs-lookup"><span data-stu-id="db126-164">hello circuit user can run hello following cmdlet tooredeem a link authorization:</span></span>

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

<span data-ttu-id="db126-165">Ejecute este comando en la suscripción de hello recién vinculado para la red virtual de hello:</span><span class="sxs-lookup"><span data-stu-id="db126-165">Run this command in hello newly linked subscription for hello virtual network:</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"

## <a name="next-steps"></a><span data-ttu-id="db126-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="db126-166">Next steps</span></span>
<span data-ttu-id="db126-167">Para obtener más información sobre ExpressRoute, consulte hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="db126-167">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

