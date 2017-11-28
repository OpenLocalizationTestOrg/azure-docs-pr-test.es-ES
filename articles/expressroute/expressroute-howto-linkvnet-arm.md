---
title: "Vinculación de una red virtual a un circuito ExpressRoute mediante PowerShell y Azure | Microsoft Docs"
description: "Este documento proporciona información general sobre cómo vincular redes virtuales a circuitos ExpressRoute mediante el modelo de implementación de Resource Manager y PowerShell."
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
ms.openlocfilehash: 8c2f3036f754a98090ab860f95900416690ebf83
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="bfeba-103">Conexión de una red virtual a un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="bfeba-103">Connect a virtual network to an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bfeba-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="bfeba-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="bfeba-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bfeba-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="bfeba-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="bfeba-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="bfeba-107">Vídeo: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="bfeba-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="bfeba-108">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="bfeba-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="bfeba-109">Este artículo lo ayudará a vincular redes virtuales a circuitos ExpressRoute de Azure a través del modelo de implementación de Resource Manager y PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bfeba-109">This article helps you link virtual networks (VNets) to Azure ExpressRoute circuits by using the Resource Manager deployment model and PowerShell.</span></span> <span data-ttu-id="bfeba-110">Las redes virtuales pueden estar en la misma suscripción o formar parte de otra suscripción.</span><span class="sxs-lookup"><span data-stu-id="bfeba-110">Virtual networks can either be in the same subscription or part of another subscription.</span></span> <span data-ttu-id="bfeba-111">En este artículo también se muestra cómo actualizar el vínculo de una red virtual.</span><span class="sxs-lookup"><span data-stu-id="bfeba-111">This article also shows you how to update a virtual network link.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="bfeba-112">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="bfeba-112">Before you begin</span></span>
* <span data-ttu-id="bfeba-113">Instale la versión más reciente de los módulos de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bfeba-113">Install the latest version of the Azure PowerShell modules.</span></span> <span data-ttu-id="bfeba-114">Para más información, vea [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bfeba-114">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="bfeba-115">Revise los [requisitos previos](expressroute-prerequisites.md), los [requisitos de enrutamiento](expressroute-routing.md) y los [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="bfeba-115">Review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="bfeba-116">Tiene que tener un circuito ExpressRoute activo.</span><span class="sxs-lookup"><span data-stu-id="bfeba-116">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="bfeba-117">Siga las instrucciones para [crear un circuito ExpressRoute](expressroute-howto-circuit-arm.md) y habilite el circuito mediante el proveedor de conectividad.</span><span class="sxs-lookup"><span data-stu-id="bfeba-117">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="bfeba-118">Asegúrese de que dispone de un emparejamiento privado de Azure configurado para el circuito.</span><span class="sxs-lookup"><span data-stu-id="bfeba-118">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="bfeba-119">Consulte el artículo de [configuración del enrutamiento](expressroute-howto-routing-arm.md) para obtener instrucciones sobre el enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="bfeba-119">See the [configure routing](expressroute-howto-routing-arm.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="bfeba-120">Asegúrese de que el emparejamiento privado de Azure está configurado y el emparejamiento BGP entre la red y Microsoft está activo para habilitar la conectividad de extremo a extremo.</span><span class="sxs-lookup"><span data-stu-id="bfeba-120">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="bfeba-121">Asegúrese de que ha creado y aprovisionado totalmente una red virtual y una puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="bfeba-121">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="bfeba-122">Siga las instrucciones para [crear una puerta de enlace de red virtual en ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="bfeba-122">Follow the instructions to [create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="bfeba-123">Una puerta de enlace de red virtual para ExpressRoute usa el GatewayType "ExpressRoute", no VPN.</span><span class="sxs-lookup"><span data-stu-id="bfeba-123">A virtual network gateway for ExpressRoute uses the GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="bfeba-124">Es posible vincular hasta 10 redes virtuales a un circuito ExpressRoute estándar.</span><span class="sxs-lookup"><span data-stu-id="bfeba-124">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span></span> <span data-ttu-id="bfeba-125">Todas las redes virtuales deben pertenecer a la misma región geopolítica al utilizar un circuito de ExpressRoute estándar.</span><span class="sxs-lookup"><span data-stu-id="bfeba-125">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="bfeba-126">Puede vincular una red virtual fuera de la región geopolítica del circuito de ExpressRoute, o bien conectar un mayor número de redes virtuales a este si habilitó el complemento premium de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="bfeba-126">You can link a virtual networks outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit if you enabled the ExpressRoute premium add-on.</span></span> <span data-ttu-id="bfeba-127">Consulte las [preguntas más frecuentes](expressroute-faqs.md) para obtener más detalles sobre el complemento premium.</span><span class="sxs-lookup"><span data-stu-id="bfeba-127">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span></span>


## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="bfeba-128">Conexión de una red virtual en la misma suscripción a un circuito</span><span class="sxs-lookup"><span data-stu-id="bfeba-128">Connect a virtual network in the same subscription to a circuit</span></span>
<span data-ttu-id="bfeba-129">Puede conectar una puerta de enlace de red virtual a un circuito ExpressRoute mediante el siguiente cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bfeba-129">You can connect a virtual network gateway to an ExpressRoute circuit by using the following cmdlet.</span></span> <span data-ttu-id="bfeba-130">Asegúrese de que la puerta de enlace de red virtual se crea y está lista para vincular antes de ejecutar el cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bfeba-130">Make sure that the virtual network gateway is created and is ready for linking before you run the cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="bfeba-131">Conexión de una red virtual en una suscripción diferente a un circuito</span><span class="sxs-lookup"><span data-stu-id="bfeba-131">Connect a virtual network in a different subscription to a circuit</span></span>
<span data-ttu-id="bfeba-132">Puede compartir un circuito ExpressRoute entre varias suscripciones.</span><span class="sxs-lookup"><span data-stu-id="bfeba-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="bfeba-133">En la ilustración siguiente se muestra un sencillo esquema de cómo funciona el uso compartido de circuitos ExpressRoute entre varias suscripciones.</span><span class="sxs-lookup"><span data-stu-id="bfeba-133">The following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="bfeba-134">Cada una de las nubes más pequeñas dentro de la nube de gran tamaño se usa para representar las suscripciones que pertenecen a diferentes departamentos dentro de una organización.</span><span class="sxs-lookup"><span data-stu-id="bfeba-134">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span> <span data-ttu-id="bfeba-135">Cada departamento de la organización puede usar su propia suscripción para implementar sus servicios, pero puede compartir un único circuito ExpressRoute para volver a conectarse a la red local.</span><span class="sxs-lookup"><span data-stu-id="bfeba-135">Each of the departments within the organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span> <span data-ttu-id="bfeba-136">Un solo departamento (en este ejemplo: TI) puede ser el propietario del circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="bfeba-136">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="bfeba-137">Otras suscripciones dentro de la organización pueden usar el circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="bfeba-137">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="bfeba-138">Los cargos de conectividad y ancho de banda de un circuito ExpressRoute recaerán en el propietario de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="bfeba-138">Connectivity and bandwidth charges for the ExpressRoute circuit will be applied to the subscription owner.</span></span> <span data-ttu-id="bfeba-139">Todas las redes virtuales comparten el mismo ancho de banda.</span><span class="sxs-lookup"><span data-stu-id="bfeba-139">All virtual networks share the same bandwidth.</span></span>
> 
> 

![Conectividad entre suscripciones](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="bfeba-141">Administración: los propietarios de circuito y los usuarios de circuito</span><span class="sxs-lookup"><span data-stu-id="bfeba-141">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="bfeba-142">El "propietario del circuito" es un usuario avanzado autorizado del recurso de circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="bfeba-142">The 'circuit owner' is an authorized Power User of the ExpressRoute circuit resource.</span></span> <span data-ttu-id="bfeba-143">Puede crear autorizaciones que los "propietarios del circuito", a su vez, pueden canjear.</span><span class="sxs-lookup"><span data-stu-id="bfeba-143">The circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="bfeba-144">Los usuarios del circuito son propietarios de puertas de enlace de red virtual que no se incluyen en la misma suscripción que el circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="bfeba-144">Circuit users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span></span> <span data-ttu-id="bfeba-145">Los usuarios del circuito pueden canjear autorizaciones (una autorización por red virtual).</span><span class="sxs-lookup"><span data-stu-id="bfeba-145">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="bfeba-146">El propietario del circuito tiene la capacidad de modificar y revocar las autorizaciones en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="bfeba-146">The circuit owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="bfeba-147">La revocación de una autorización dará como resultado la eliminación de todas las conexiones de vínculos de la suscripción cuyo acceso se haya revocado.</span><span class="sxs-lookup"><span data-stu-id="bfeba-147">Revoking an authorization results in all link connections being deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="bfeba-148">Operaciones del propietario del circuito</span><span class="sxs-lookup"><span data-stu-id="bfeba-148">Circuit owner operations</span></span>

<span data-ttu-id="bfeba-149">**Creación de una autorización**</span><span class="sxs-lookup"><span data-stu-id="bfeba-149">**To create an authorization**</span></span>

<span data-ttu-id="bfeba-150">El propietario del circuito crea una autorización.</span><span class="sxs-lookup"><span data-stu-id="bfeba-150">The circuit owner creates an authorization.</span></span> <span data-ttu-id="bfeba-151">Esto da lugar a la creación de una clave de autorización que puede usar un usuario del circuito para conectar sus puertas de enlace de red virtual al circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="bfeba-151">This results in the creation of an authorization key that can be used by a circuit user to connect their virtual network gateways to the ExpressRoute circuit.</span></span> <span data-ttu-id="bfeba-152">Una autorización solo es válida para una conexión.</span><span class="sxs-lookup"><span data-stu-id="bfeba-152">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="bfeba-153">El fragmento de código del cmdlet siguiente muestra cómo crear una autorización:</span><span class="sxs-lookup"><span data-stu-id="bfeba-153">The following cmdlet snippet shows how to create an authorization:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


<span data-ttu-id="bfeba-154">La respuesta a esta contendrá la clave y el estado de la autorización:</span><span class="sxs-lookup"><span data-stu-id="bfeba-154">The response to this will contain the authorization key and status:</span></span>

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



<span data-ttu-id="bfeba-155">**Revisión de autorizaciones**</span><span class="sxs-lookup"><span data-stu-id="bfeba-155">**To review authorizations**</span></span>

<span data-ttu-id="bfeba-156">El propietario del circuito puede revisar todas las autorizaciones emitidas en un circuito concreto ejecutando el siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bfeba-156">The circuit owner can review all authorizations that are issued on a particular circuit by running the following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="bfeba-157">**Adición de autorizaciones**</span><span class="sxs-lookup"><span data-stu-id="bfeba-157">**To add authorizations**</span></span>

<span data-ttu-id="bfeba-158">El propietario del circuito puede agregar las autorizaciones mediante el siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bfeba-158">The circuit owner can add authorizations by using the following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="bfeba-159">**Eliminación de autorizaciones**</span><span class="sxs-lookup"><span data-stu-id="bfeba-159">**To delete authorizations**</span></span>

<span data-ttu-id="bfeba-160">El propietario del circuito puede revocar o eliminar las autorizaciones al usuario ejecutando el siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bfeba-160">The circuit owner can revoke/delete authorizations to the user by running the following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a><span data-ttu-id="bfeba-161">Operaciones del usuario del circuito</span><span class="sxs-lookup"><span data-stu-id="bfeba-161">Circuit user operations</span></span>

<span data-ttu-id="bfeba-162">El usuario del circuito necesita el Id. de mismo nivel y una clave de autorización del propietario del circuito.</span><span class="sxs-lookup"><span data-stu-id="bfeba-162">The circuit user needs the peer ID and an authorization key from the circuit owner.</span></span> <span data-ttu-id="bfeba-163">la clave de autorización es un GUID.</span><span class="sxs-lookup"><span data-stu-id="bfeba-163">The authorization key is a GUID.</span></span>

<span data-ttu-id="bfeba-164">El id. de mismo nivel se puede comprobar con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="bfeba-164">Peer ID can be checked from the following command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="bfeba-165">**Canje de una autorización de conexión**</span><span class="sxs-lookup"><span data-stu-id="bfeba-165">**To redeem a connection authorization**</span></span>

<span data-ttu-id="bfeba-166">El usuario del circuito puede ejecutar el siguiente cmdlet para canjear una autorización de vínculo:</span><span class="sxs-lookup"><span data-stu-id="bfeba-166">The circuit user can run the following cmdlet to redeem a link authorization:</span></span>

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="bfeba-167">**Liberación de una autorización de conexión**</span><span class="sxs-lookup"><span data-stu-id="bfeba-167">**To release a connection authorization**</span></span>

<span data-ttu-id="bfeba-168">Puede liberar una autorización eliminando la conexión que vincula el circuito ExpressRoute a la red virtual.</span><span class="sxs-lookup"><span data-stu-id="bfeba-168">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span></span>

## <a name="modify-a-virtual-network-connection"></a><span data-ttu-id="bfeba-169">Modificación de una conexión de red virtual</span><span class="sxs-lookup"><span data-stu-id="bfeba-169">Modify a virtual network connection</span></span>
<span data-ttu-id="bfeba-170">Puede actualizar ciertas propiedades de una conexión de red virtual.</span><span class="sxs-lookup"><span data-stu-id="bfeba-170">You can update certain properties of a virtual network connection.</span></span> 

<span data-ttu-id="bfeba-171">**Actualización del peso de la conexión**</span><span class="sxs-lookup"><span data-stu-id="bfeba-171">**To update the connection weight**</span></span>

<span data-ttu-id="bfeba-172">La red virtual puede estar conectada a varios circuitos ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="bfeba-172">Your virtual network can be connected to multiple ExpressRoute circuits.</span></span> <span data-ttu-id="bfeba-173">Es posible que reciba el mismo prefijo de más de un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="bfeba-173">You may receive the same prefix from more than one ExpressRoute circuit.</span></span> <span data-ttu-id="bfeba-174">Para elegir la conexión por la que enviar el tráfico destinado a este prefijo, puede cambiar el valor de *RoutingWeight* de una conexión.</span><span class="sxs-lookup"><span data-stu-id="bfeba-174">To choose which connection to send traffic destined for this prefix, you can change *RoutingWeight* of a connection.</span></span> <span data-ttu-id="bfeba-175">El tráfico se enviará por la conexión con el valor más alto de *RoutingWeight*.</span><span class="sxs-lookup"><span data-stu-id="bfeba-175">Traffic will be sent on the connection with the highest *RoutingWeight*.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

<span data-ttu-id="bfeba-176">El intervalo de *RoutingWeight* abarca de 0 a 32 000.</span><span class="sxs-lookup"><span data-stu-id="bfeba-176">The range of *RoutingWeight* is 0 to 32000.</span></span> <span data-ttu-id="bfeba-177">El valor predeterminado es 0.</span><span class="sxs-lookup"><span data-stu-id="bfeba-177">The default value is 0.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfeba-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bfeba-178">Next steps</span></span>
<span data-ttu-id="bfeba-179">Para obtener más información acerca de ExpressRoute, consulte [P+F de ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="bfeba-179">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
