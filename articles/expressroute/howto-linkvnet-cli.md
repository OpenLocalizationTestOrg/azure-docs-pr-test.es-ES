---
title: 'Vincular un circuito de ExpressRoute de tooan de red virtual: CLI: Azure | Documentos de Microsoft'
description: "Este documento proporciona información general sobre cómo toolink virtual redes (redes virtuales) tooExpressRoute circuitos utilizando el modelo de implementación del Administrador de recursos de Hola y la CLI."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlit
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 1251f016d9b94d3fee81de1df164cb085cbe9d78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-cli"></a><span data-ttu-id="b3abe-103">Conectarse a un circuito de ExpressRoute de tooan de red virtual con CLI</span><span class="sxs-lookup"><span data-stu-id="b3abe-103">Connect a virtual network tooan ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="b3abe-104">En este artículo le ayuda a vincular circuitos de ExpressRoute de tooAzure de redes virtuales (Vnet) mediante la CLI.</span><span class="sxs-lookup"><span data-stu-id="b3abe-104">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits using CLI.</span></span> <span data-ttu-id="b3abe-105">toolink mediante CLI de Azure, se deben crear redes virtuales de hello mediante modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3abe-105">toolink using Azure CLI, hello virtual networks must be created using hello Resource Manager deployment model.</span></span> <span data-ttu-id="b3abe-106">O bien pueden estar en hello misma suscripción o parte de otra suscripción.</span><span class="sxs-lookup"><span data-stu-id="b3abe-106">They can either be in hello same subscription, or part of another subscription.</span></span> <span data-ttu-id="b3abe-107">Si desea toouse tooconnect de un método diferente para el circuito de ExpressRoute de tooan de red virtual, puede seleccionar un artículo de hello lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="b3abe-107">If you want toouse a different method tooconnect your VNet tooan ExpressRoute circuit, you can select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b3abe-108">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="b3abe-108">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="b3abe-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3abe-109">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="b3abe-110">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="b3abe-110">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="b3abe-111">Vídeo: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b3abe-111">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="b3abe-112">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="b3abe-112">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="b3abe-113">Requisitos previos de configuración</span><span class="sxs-lookup"><span data-stu-id="b3abe-113">Configuration prerequisites</span></span>

* <span data-ttu-id="b3abe-114">Necesita la versión más reciente de Hola de hello interfaz de línea de comandos (CLI).</span><span class="sxs-lookup"><span data-stu-id="b3abe-114">You need hello latest version of hello command-line interface (CLI).</span></span> <span data-ttu-id="b3abe-115">Para más información, consulte [Instalación de la CLI de Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b3abe-115">For more information, see [Install Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="b3abe-116">Necesita hello tooreview [requisitos previos](expressroute-prerequisites.md), [requisitos de enrutamiento](expressroute-routing.md), y [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="b3abe-116">You need tooreview hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="b3abe-117">Tiene que tener un circuito ExpressRoute activo.</span><span class="sxs-lookup"><span data-stu-id="b3abe-117">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="b3abe-118">Siga las instrucciones de hello demasiado[crear un circuito ExpressRoute](howto-circuit-cli.md) y tener habilitada por el proveedor de conectividad de circuito de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3abe-118">Follow hello instructions too[create an ExpressRoute circuit](howto-circuit-cli.md) and have hello circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="b3abe-119">Asegúrese de que dispone de un emparejamiento privado de Azure configurado para el circuito.</span><span class="sxs-lookup"><span data-stu-id="b3abe-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="b3abe-120">Vea hello [configurar el enrutamiento de](howto-routing-cli.md) artículo para las instrucciones de enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="b3abe-120">See hello [configure routing](howto-routing-cli.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="b3abe-121">Asegúrese de que se haya configurado un emparejamiento privado de Azure.</span><span class="sxs-lookup"><span data-stu-id="b3abe-121">Ensure that Azure private peering is configured.</span></span> <span data-ttu-id="b3abe-122">emparejamiento de BGP de Hello entre la red y Microsoft debe ser una para que se puede habilitar la conectividad de extremo a extremo.</span><span class="sxs-lookup"><span data-stu-id="b3abe-122">hello BGP peering between your network and Microsoft must be up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="b3abe-123">Asegúrese de que ha creado y aprovisionado totalmente una red virtual y una puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="b3abe-123">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="b3abe-124">Siga las instrucciones de hello demasiado[configurar una puerta de enlace de red virtual para ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span><span class="sxs-lookup"><span data-stu-id="b3abe-124">Follow hello instructions too[Configure a virtual network gateway for ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span> <span data-ttu-id="b3abe-125">Ser seguro toouse `--gateway-type ExpressRoute`.</span><span class="sxs-lookup"><span data-stu-id="b3abe-125">Be sure toouse `--gateway-type ExpressRoute`.</span></span>

* <span data-ttu-id="b3abe-126">Puede vincular una circuito de ExpressRoute estándar de too10 redes virtuales tooa.</span><span class="sxs-lookup"><span data-stu-id="b3abe-126">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="b3abe-127">Todas las redes virtuales deben estar en hello misma región geopolíticos cuando se usa un circuito de ExpressRoute estándar.</span><span class="sxs-lookup"><span data-stu-id="b3abe-127">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="b3abe-128">Si habilita el complemento de hello ExpressRoute premium, puede vincular una red virtual fuera de la región geopolítica de Hola de hello circuito de ExpressRoute o conectar un mayor número de redes virtuales tooyour circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b3abe-128">If you enable hello ExpressRoute premium add-on, you can link a virtual network outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="b3abe-129">Para obtener más información sobre el complemento de hello premium, vea hello [preguntas más frecuentes sobre](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="b3abe-129">For more information about hello premium add-on, see hello [FAQ](expressroute-faqs.md).</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="b3abe-130">Conectar una red virtual en hello mismo circuito de tooa de suscripción</span><span class="sxs-lookup"><span data-stu-id="b3abe-130">Connect a virtual network in hello same subscription tooa circuit</span></span>

<span data-ttu-id="b3abe-131">Puede conectar un circuito de ExpressRoute de tooan de puerta de enlace de red virtual mediante el ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3abe-131">You can connect a virtual network gateway tooan ExpressRoute circuit by using hello example.</span></span> <span data-ttu-id="b3abe-132">Asegúrese de que esa puerta de enlace de red virtual de Hola se crea y está listo para crear un vínculo antes de ejecutar el comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3abe-132">Make sure that hello virtual network gateway is created and is ready for linking before you run hello command.</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="b3abe-133">Conectar una red virtual en un circuito de tooa otra suscripción</span><span class="sxs-lookup"><span data-stu-id="b3abe-133">Connect a virtual network in a different subscription tooa circuit</span></span>

<span data-ttu-id="b3abe-134">Puede compartir un circuito ExpressRoute entre varias suscripciones.</span><span class="sxs-lookup"><span data-stu-id="b3abe-134">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="b3abe-135">Hola siguiente ilustración muestra un sencillo esquemática de cómo compartir funciona para los circuitos ExpressRoute en varias suscripciones.</span><span class="sxs-lookup"><span data-stu-id="b3abe-135">hello figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="b3abe-136">Cada una de las nubes más pequeñas de hello en nube de gran tamaño hello es toorepresent usado suscripciones que pertenecen los departamentos de toodifferent dentro de una organización.</span><span class="sxs-lookup"><span data-stu-id="b3abe-136">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="b3abe-137">Cada uno de los departamentos de Hola de organización de hello puede utilizar su propia suscripción para implementar sus servicios, pero se puede compartir una sola red de ExpressRoute circuito tooconnect tooyour atrás local.</span><span class="sxs-lookup"><span data-stu-id="b3abe-137">Each of hello departments within hello organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="b3abe-138">Un departamento único (en este ejemplo: TI) puede poseer el circuito de ExpressRoute Hola.</span><span class="sxs-lookup"><span data-stu-id="b3abe-138">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="b3abe-139">Otras suscripciones dentro de la organización de hello pueden utilizar el circuito de ExpressRoute Hola.</span><span class="sxs-lookup"><span data-stu-id="b3abe-139">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="b3abe-140">Los cargos de conectividad y ancho de banda para el circuito dedicado de hello será aplicado toohello propietario del circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b3abe-140">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute Circuit Owner.</span></span> <span data-ttu-id="b3abe-141">Todas las redes virtuales compartan Hola mismo ancho de banda.</span><span class="sxs-lookup"><span data-stu-id="b3abe-141">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![Conectividad entre suscripciones](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="b3abe-143">Administración: los propietarios del circuito y los usuarios del circuito</span><span class="sxs-lookup"><span data-stu-id="b3abe-143">Administration - Circuit Owners and Circuit Users</span></span>

<span data-ttu-id="b3abe-144">Hola 'Propietario del circuito' es un usuario autorizado de alimentación de hello recursos de circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b3abe-144">hello 'Circuit Owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="b3abe-145">Hola propietario del circuito puede crear autorizaciones que se pueden canjear por 'Usuarios del circuito'.</span><span class="sxs-lookup"><span data-stu-id="b3abe-145">hello Circuit Owner can create authorizations that can be redeemed by 'Circuit Users'.</span></span> <span data-ttu-id="b3abe-146">Los usuarios de circuito son propietarios de red virtual puertas de enlace que no están en Hola misma suscripción como Hola circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b3abe-146">Circuit Users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="b3abe-147">Los usuarios del circuito pueden canjear autorizaciones (una autorización por red virtual).</span><span class="sxs-lookup"><span data-stu-id="b3abe-147">Circuit Users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="b3abe-148">Hola propietario del circuito tiene Hola power toomodify y revocar las autorizaciones en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="b3abe-148">hello Circuit Owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="b3abe-149">Cuando se revoca una autorización, se eliminan todas las conexiones de vínculo de suscripción de hello cuyo acceso se ha revocado.</span><span class="sxs-lookup"><span data-stu-id="b3abe-149">When an authorization is revoked, all link connections are deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="b3abe-150">Operaciones del propietario del circuito</span><span class="sxs-lookup"><span data-stu-id="b3abe-150">Circuit Owner operations</span></span>

<span data-ttu-id="b3abe-151">**toocreate una autorización**</span><span class="sxs-lookup"><span data-stu-id="b3abe-151">**toocreate an authorization**</span></span>

<span data-ttu-id="b3abe-152">Hola propietario del circuito crea una autorización, que crea una clave de autorización que puede ser utilizado por un usuario de circuito tooconnect su toohello de puertas de enlace de red virtual circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b3abe-152">hello Circuit Owner creates an authorization, which creates an authorization key that can be used by a Circuit User tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="b3abe-153">Una autorización solo es válida para una conexión.</span><span class="sxs-lookup"><span data-stu-id="b3abe-153">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="b3abe-154">Hola siguiente ejemplo se muestra cómo toocreate una autorización:</span><span class="sxs-lookup"><span data-stu-id="b3abe-154">hello following example shows how toocreate an authorization:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization
```

<span data-ttu-id="b3abe-155">respuesta de Hello contiene el estado y clave de autorización de hello:</span><span class="sxs-lookup"><span data-stu-id="b3abe-155">hello response contains hello authorization key and status:</span></span>

```azurecli
"authorizationKey": "0a7f3020-541f-4b4b-844a-5fb43472e3d7",
"authorizationUseStatus": "Available",
"etag": "W/\"010353d4-8955-4984-807a-585c21a22ae0\"",
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/authorizations/MyAuthorization1",
"name": "MyAuthorization1",
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup"
```

<span data-ttu-id="b3abe-156">**tooreview autorizaciones**</span><span class="sxs-lookup"><span data-stu-id="b3abe-156">**tooreview authorizations**</span></span>

<span data-ttu-id="b3abe-157">Hola propietario del circuito puede revisar todas las autorizaciones que se emiten en un circuito concreto mediante la ejecución de hello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b3abe-157">hello Circuit Owner can review all authorizations that are issued on a particular circuit by running hello following example:</span></span>

```azurecli
az network express-route auth list --circuit-name MyCircuit -g ExpressRouteResourceGroup
```

<span data-ttu-id="b3abe-158">**tooadd autorizaciones**</span><span class="sxs-lookup"><span data-stu-id="b3abe-158">**tooadd authorizations**</span></span>

<span data-ttu-id="b3abe-159">Hola propietario del circuito puede agregar autorizaciones mediante el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="b3abe-159">hello Circuit Owner can add authorizations by using hello following example:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

<span data-ttu-id="b3abe-160">**toodelete autorizaciones**</span><span class="sxs-lookup"><span data-stu-id="b3abe-160">**toodelete authorizations**</span></span>

<span data-ttu-id="b3abe-161">Hola propietario del circuito puede revocar o eliminar un autorizaciones toohello usuario ejecutando el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="b3abe-161">hello Circuit Owner can revoke/delete authorizations toohello user by running hello following example:</span></span>

```azurecli
az network express-route auth delete --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

### <a name="circuit-user-operations"></a><span data-ttu-id="b3abe-162">Operaciones del usuario del circuito</span><span class="sxs-lookup"><span data-stu-id="b3abe-162">Circuit User operations</span></span>

<span data-ttu-id="b3abe-163">Hola circuito usuario necesita Id. del mismo nivel de hello y una clave de autorización de propietario del circuito de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3abe-163">hello Circuit User needs hello peer ID and an authorization key from hello Circuit Owner.</span></span> <span data-ttu-id="b3abe-164">clave de autorización de Hello es un GUID.</span><span class="sxs-lookup"><span data-stu-id="b3abe-164">hello authorization key is a GUID.</span></span>

```azurecli
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="b3abe-165">**tooredeem una autorización de conexión**</span><span class="sxs-lookup"><span data-stu-id="b3abe-165">**tooredeem a connection authorization**</span></span>

<span data-ttu-id="b3abe-166">Hola usuario del circuito puede ejecutar después de tooredeem de ejemplo de Hola una autorización de vínculo:</span><span class="sxs-lookup"><span data-stu-id="b3abe-166">hello Circuit User can run hello following example tooredeem a link authorization:</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit --authorization-key "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="b3abe-167">**toorelease una autorización de conexión**</span><span class="sxs-lookup"><span data-stu-id="b3abe-167">**toorelease a connection authorization**</span></span>

<span data-ttu-id="b3abe-168">Puede liberar una autorización mediante la eliminación de la conexión de Hola que vincula la red virtual del toohello de circuito ExpressRoute Hola.</span><span class="sxs-lookup"><span data-stu-id="b3abe-168">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3abe-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b3abe-169">Next steps</span></span>

<span data-ttu-id="b3abe-170">Para obtener más información sobre ExpressRoute, consulte hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="b3abe-170">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
