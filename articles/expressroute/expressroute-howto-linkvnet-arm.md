---
title: 'Vincular un circuito de ExpressRoute de tooan de red virtual: PowerShell: Azure | Documentos de Microsoft'
description: "Este documento proporciona información general sobre cómo toolink virtual redes (redes virtuales) tooExpressRoute circuitos utilizando el modelo de implementación del Administrador de recursos de Hola y PowerShell."
services: expressroute
documentationcenter: na
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: daacb6e5-705a-456f-9a03-c4fc3f8c1f7e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: ganesr
ms.openlocfilehash: e75a9f6b42fa8e1a579e4f19882ec99b277b545f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="b6276-103">Conectarse a un circuito de ExpressRoute de tooan de red virtual</span><span class="sxs-lookup"><span data-stu-id="b6276-103">Connect a virtual network tooan ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b6276-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="b6276-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="b6276-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b6276-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="b6276-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="b6276-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="b6276-107">Vídeo: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b6276-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="b6276-108">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="b6276-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="b6276-109">En este artículo le ayuda a vincular circuitos ExpressRoute de tooAzure de redes virtuales (Vnet) mediante el modelo de implementación del Administrador de recursos de Hola y PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b6276-109">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello Resource Manager deployment model and PowerShell.</span></span> <span data-ttu-id="b6276-110">Redes virtuales pueden ser Hola misma suscripción o parte de otra suscripción.</span><span class="sxs-lookup"><span data-stu-id="b6276-110">Virtual networks can either be in hello same subscription or part of another subscription.</span></span> <span data-ttu-id="b6276-111">Este artículo también muestra cómo vincular tooupdate una red virtual.</span><span class="sxs-lookup"><span data-stu-id="b6276-111">This article also shows you how tooupdate a virtual network link.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="b6276-112">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="b6276-112">Before you begin</span></span>
* <span data-ttu-id="b6276-113">Instalar versión más reciente de Hola de módulos de PowerShell de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6276-113">Install hello latest version of hello Azure PowerShell modules.</span></span> <span data-ttu-id="b6276-114">Para obtener más información, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b6276-114">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="b6276-115">Hola de revisión [requisitos previos](expressroute-prerequisites.md), [requisitos de enrutamiento](expressroute-routing.md), y [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="b6276-115">Review hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="b6276-116">Tiene que tener un circuito ExpressRoute activo.</span><span class="sxs-lookup"><span data-stu-id="b6276-116">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="b6276-117">Siga las instrucciones de hello demasiado[crear un circuito ExpressRoute](expressroute-howto-circuit-arm.md) y tener habilitada por el proveedor de conectividad de circuito de Hola.</span><span class="sxs-lookup"><span data-stu-id="b6276-117">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="b6276-118">Asegúrese de que dispone de un emparejamiento privado de Azure configurado para el circuito.</span><span class="sxs-lookup"><span data-stu-id="b6276-118">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="b6276-119">Vea hello [configurar el enrutamiento de](expressroute-howto-routing-arm.md) artículo para las instrucciones de enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="b6276-119">See hello [configure routing](expressroute-howto-routing-arm.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="b6276-120">Asegúrese de que el emparejamiento privado Azure está configurado y Hola emparejamiento de BGP entre la red y Microsoft está activo para que se puede habilitar la conectividad de extremo a extremo.</span><span class="sxs-lookup"><span data-stu-id="b6276-120">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="b6276-121">Asegúrese de que ha creado y aprovisionado totalmente una red virtual y una puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="b6276-121">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="b6276-122">Siga las instrucciones de hello demasiado[crear una puerta de enlace de red virtual para ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b6276-122">Follow hello instructions too[create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="b6276-123">Una puerta de enlace de red virtual para ExpressRoute usa Hola el GatewayType 'ExpressRoute', no VPN.</span><span class="sxs-lookup"><span data-stu-id="b6276-123">A virtual network gateway for ExpressRoute uses hello GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="b6276-124">Puede vincular una circuito de ExpressRoute estándar de too10 redes virtuales tooa.</span><span class="sxs-lookup"><span data-stu-id="b6276-124">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="b6276-125">Todas las redes virtuales deben estar en hello misma región geopolíticos cuando se usa un circuito de ExpressRoute estándar.</span><span class="sxs-lookup"><span data-stu-id="b6276-125">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="b6276-126">Puede vincular una red virtual fuera de la región geopolítica de Hola de hello circuito de ExpressRoute o conectar un mayor número de redes virtuales tooyour circuito ExpressRoute si ha habilitado el complemento de hello ExpressRoute premium.</span><span class="sxs-lookup"><span data-stu-id="b6276-126">You can link a virtual networks outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="b6276-127">Comprobar hello [preguntas más frecuentes sobre](expressroute-faqs.md) para obtener más detalles sobre el complemento de hello premium.</span><span class="sxs-lookup"><span data-stu-id="b6276-127">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>


## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="b6276-128">Conectar una red virtual en hello mismo circuito de tooa de suscripción</span><span class="sxs-lookup"><span data-stu-id="b6276-128">Connect a virtual network in hello same subscription tooa circuit</span></span>
<span data-ttu-id="b6276-129">Puede conectarse un tooan de puerta de enlace de red virtual circuito ExpressRoute mediante Hola siguiente cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b6276-129">You can connect a virtual network gateway tooan ExpressRoute circuit by using hello following cmdlet.</span></span> <span data-ttu-id="b6276-130">Asegúrese de que esa puerta de enlace de red virtual de Hola se crea y está listo para crear un vínculo antes de ejecutar el cmdlet de hello:</span><span class="sxs-lookup"><span data-stu-id="b6276-130">Make sure that hello virtual network gateway is created and is ready for linking before you run hello cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="b6276-131">Conectar una red virtual en un circuito de tooa otra suscripción</span><span class="sxs-lookup"><span data-stu-id="b6276-131">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="b6276-132">Puede compartir un circuito ExpressRoute entre varias suscripciones.</span><span class="sxs-lookup"><span data-stu-id="b6276-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="b6276-133">Hola figura siguiente muestra un sencillo esquema de cómo compartir funciona para los circuitos ExpressRoute en varias suscripciones.</span><span class="sxs-lookup"><span data-stu-id="b6276-133">hello following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="b6276-134">Cada una de las nubes más pequeñas de hello en nube de gran tamaño hello es toorepresent usado suscripciones que pertenecen los departamentos de toodifferent dentro de una organización.</span><span class="sxs-lookup"><span data-stu-id="b6276-134">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="b6276-135">Cada uno de los departamentos de Hola de organización de hello puede utilizar su propia suscripción para implementar sus servicios, pero se puede compartir una sola red de ExpressRoute circuito tooconnect tooyour atrás local.</span><span class="sxs-lookup"><span data-stu-id="b6276-135">Each of hello departments within hello organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="b6276-136">Un departamento único (en este ejemplo: TI) puede poseer el circuito de ExpressRoute Hola.</span><span class="sxs-lookup"><span data-stu-id="b6276-136">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="b6276-137">Otras suscripciones dentro de la organización de hello pueden utilizar el circuito de ExpressRoute Hola.</span><span class="sxs-lookup"><span data-stu-id="b6276-137">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="b6276-138">Cargos de conectividad y ancho de banda de circuito de ExpressRoute de Hola será propietario de la suscripción de toohello aplicado.</span><span class="sxs-lookup"><span data-stu-id="b6276-138">Connectivity and bandwidth charges for hello ExpressRoute circuit will be applied toohello subscription owner.</span></span> <span data-ttu-id="b6276-139">Todas las redes virtuales compartan Hola mismo ancho de banda.</span><span class="sxs-lookup"><span data-stu-id="b6276-139">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![Conectividad entre suscripciones](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="b6276-141">Administración: los propietarios de circuito y los usuarios de circuito</span><span class="sxs-lookup"><span data-stu-id="b6276-141">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="b6276-142">Hola 'propietario del circuito' es un usuario autorizado de alimentación de hello recursos de circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b6276-142">hello 'circuit owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="b6276-143">propietario del circuito Hola puede crear autorizaciones que se pueden canjear por 'usuarios del circuito'.</span><span class="sxs-lookup"><span data-stu-id="b6276-143">hello circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="b6276-144">Los usuarios de circuito son propietarios de red virtual puertas de enlace que no están en Hola misma suscripción como Hola circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b6276-144">Circuit users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="b6276-145">Los usuarios del circuito pueden canjear autorizaciones (una autorización por red virtual).</span><span class="sxs-lookup"><span data-stu-id="b6276-145">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="b6276-146">propietario del circuito Hello tiene Hola power toomodify y revocar las autorizaciones en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="b6276-146">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="b6276-147">Revocar el resultado de una autorización en todas las conexiones de vínculo que se va a eliminar de suscripción de hello cuyo acceso se ha revocado.</span><span class="sxs-lookup"><span data-stu-id="b6276-147">Revoking an authorization results in all link connections being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="b6276-148">Operaciones del propietario del circuito</span><span class="sxs-lookup"><span data-stu-id="b6276-148">Circuit owner operations</span></span>

<span data-ttu-id="b6276-149">**toocreate una autorización**</span><span class="sxs-lookup"><span data-stu-id="b6276-149">**toocreate an authorization**</span></span>

<span data-ttu-id="b6276-150">propietario del circuito Hola crea una autorización.</span><span class="sxs-lookup"><span data-stu-id="b6276-150">hello circuit owner creates an authorization.</span></span> <span data-ttu-id="b6276-151">Esto resulta en hello creación de una clave de autorización que puede ser utilizados por un tooconnect de usuario de circuito su toohello de puertas de enlace de red virtual circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b6276-151">This results in hello creation of an authorization key that can be used by a circuit user tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="b6276-152">Una autorización solo es válida para una conexión.</span><span class="sxs-lookup"><span data-stu-id="b6276-152">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="b6276-153">Hola cmdlet fragmento siguiente muestra cómo toocreate una autorización:</span><span class="sxs-lookup"><span data-stu-id="b6276-153">hello following cmdlet snippet shows how toocreate an authorization:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


<span data-ttu-id="b6276-154">Hola toothis de respuesta contendrá el estado y la clave de autorización de hello:</span><span class="sxs-lookup"><span data-stu-id="b6276-154">hello response toothis will contain hello authorization key and status:</span></span>

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



<span data-ttu-id="b6276-155">**tooreview autorizaciones**</span><span class="sxs-lookup"><span data-stu-id="b6276-155">**tooreview authorizations**</span></span>

<span data-ttu-id="b6276-156">propietario del circuito Hola puede revisar todas las autorizaciones que se ejecutan en un circuito concreto mediante la ejecución de hello siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b6276-156">hello circuit owner can review all authorizations that are issued on a particular circuit by running hello following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="b6276-157">**tooadd autorizaciones**</span><span class="sxs-lookup"><span data-stu-id="b6276-157">**tooadd authorizations**</span></span>

<span data-ttu-id="b6276-158">propietario del circuito Hola puede agregar autorizaciones mediante Hola siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b6276-158">hello circuit owner can add authorizations by using hello following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="b6276-159">**toodelete autorizaciones**</span><span class="sxs-lookup"><span data-stu-id="b6276-159">**toodelete authorizations**</span></span>

<span data-ttu-id="b6276-160">propietario del circuito Hola puede revocar o eliminar un autorizaciones toohello usuario ejecutando Hola siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b6276-160">hello circuit owner can revoke/delete authorizations toohello user by running hello following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a><span data-ttu-id="b6276-161">Operaciones del usuario del circuito</span><span class="sxs-lookup"><span data-stu-id="b6276-161">Circuit user operations</span></span>

<span data-ttu-id="b6276-162">usuario de circuito de Hello necesita Id. del mismo nivel de hello y una clave de autorización de propietario del circuito Hola.</span><span class="sxs-lookup"><span data-stu-id="b6276-162">hello circuit user needs hello peer ID and an authorization key from hello circuit owner.</span></span> <span data-ttu-id="b6276-163">clave de autorización de Hello es un GUID.</span><span class="sxs-lookup"><span data-stu-id="b6276-163">hello authorization key is a GUID.</span></span>

<span data-ttu-id="b6276-164">Identificador del mismo nivel se puede comprobar de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b6276-164">Peer ID can be checked from hello following command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="b6276-165">**tooredeem una autorización de conexión**</span><span class="sxs-lookup"><span data-stu-id="b6276-165">**tooredeem a connection authorization**</span></span>

<span data-ttu-id="b6276-166">usuario de circuito de Hello puede ejecutar Hola siguiente cmdlet tooredeem una autorización de vínculo:</span><span class="sxs-lookup"><span data-stu-id="b6276-166">hello circuit user can run hello following cmdlet tooredeem a link authorization:</span></span>

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="b6276-167">**toorelease una autorización de conexión**</span><span class="sxs-lookup"><span data-stu-id="b6276-167">**toorelease a connection authorization**</span></span>

<span data-ttu-id="b6276-168">Puede liberar una autorización mediante la eliminación de la conexión de Hola que vincula la red virtual del toohello de circuito ExpressRoute Hola.</span><span class="sxs-lookup"><span data-stu-id="b6276-168">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="modify-a-virtual-network-connection"></a><span data-ttu-id="b6276-169">Modificación de una conexión de red virtual</span><span class="sxs-lookup"><span data-stu-id="b6276-169">Modify a virtual network connection</span></span>
<span data-ttu-id="b6276-170">Puede actualizar ciertas propiedades de una conexión de red virtual.</span><span class="sxs-lookup"><span data-stu-id="b6276-170">You can update certain properties of a virtual network connection.</span></span> 

<span data-ttu-id="b6276-171">**peso de conexión de hello tooupdate**</span><span class="sxs-lookup"><span data-stu-id="b6276-171">**tooupdate hello connection weight**</span></span>

<span data-ttu-id="b6276-172">La red virtual puede ser circuitos ExpressRoute de toomultiple conectado.</span><span class="sxs-lookup"><span data-stu-id="b6276-172">Your virtual network can be connected toomultiple ExpressRoute circuits.</span></span> <span data-ttu-id="b6276-173">Puede recibir Hola mismo prefijo de más de un circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b6276-173">You may receive hello same prefix from more than one ExpressRoute circuit.</span></span> <span data-ttu-id="b6276-174">toochoose qué tráfico de toosend conexión destinados a este prefijo, puede cambiar *RoutingWeight* de una conexión.</span><span class="sxs-lookup"><span data-stu-id="b6276-174">toochoose which connection toosend traffic destined for this prefix, you can change *RoutingWeight* of a connection.</span></span> <span data-ttu-id="b6276-175">El tráfico se enviará en conexión Hola con hello mayor *RoutingWeight*.</span><span class="sxs-lookup"><span data-stu-id="b6276-175">Traffic will be sent on hello connection with hello highest *RoutingWeight*.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

<span data-ttu-id="b6276-176">Hola intervalo de *RoutingWeight* es too32000 0.</span><span class="sxs-lookup"><span data-stu-id="b6276-176">hello range of *RoutingWeight* is 0 too32000.</span></span> <span data-ttu-id="b6276-177">valor predeterminado de Hello es 0.</span><span class="sxs-lookup"><span data-stu-id="b6276-177">hello default value is 0.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6276-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b6276-178">Next steps</span></span>
<span data-ttu-id="b6276-179">Para obtener más información sobre ExpressRoute, consulte hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="b6276-179">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
