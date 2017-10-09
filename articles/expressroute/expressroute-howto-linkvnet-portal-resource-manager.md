---
title: 'Vincular un circuito de ExpressRoute de tooan de red virtual: portal de Azure | Documentos de Microsoft'
description: "Este documento proporciona información general sobre cómo toolink virtual redes circuitos de tooExpressRoute (Vnet)."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f5cb5441-2fba-46d9-99a5-d1d586e7bda4
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8bedcb11df7e30281fd439afdfb76cc67626a8f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="e72da-103">Conectarse a un circuito de ExpressRoute de tooan de red virtual</span><span class="sxs-lookup"><span data-stu-id="e72da-103">Connect a virtual network tooan ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e72da-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="e72da-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="e72da-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e72da-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="e72da-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="e72da-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="e72da-107">Vídeo: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e72da-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="e72da-108">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="e72da-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

<span data-ttu-id="e72da-109">En este artículo le ayuda a vincular circuitos ExpressRoute de tooAzure de redes virtuales (Vnet) mediante el modelo de implementación del Administrador de recursos de Hola y Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e72da-109">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello Resource Manager deployment model and hello Azure portal.</span></span> <span data-ttu-id="e72da-110">Redes virtuales pueden ser Hola misma suscripción, o bien pueden formar parte de otra suscripción.</span><span class="sxs-lookup"><span data-stu-id="e72da-110">Virtual networks can either be in hello same subscription, or they can be part of another subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e72da-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="e72da-111">Before you begin</span></span>
* <span data-ttu-id="e72da-112">Hola de revisión [requisitos previos](expressroute-prerequisites.md), [requisitos de enrutamiento](expressroute-routing.md), y [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="e72da-112">Review hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="e72da-113">Tiene que tener un circuito ExpressRoute activo.</span><span class="sxs-lookup"><span data-stu-id="e72da-113">You must have an active ExpressRoute circuit.</span></span>
  
  * <span data-ttu-id="e72da-114">Siga las instrucciones de hello demasiado[crear un circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) y tener habilitada por el proveedor de conectividad de circuito de Hola.</span><span class="sxs-lookup"><span data-stu-id="e72da-114">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider.</span></span>
  * <span data-ttu-id="e72da-115">Asegúrese de que dispone de un emparejamiento privado de Azure configurado para el circuito.</span><span class="sxs-lookup"><span data-stu-id="e72da-115">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="e72da-116">Vea hello [configurar enrutamiento](expressroute-howto-routing-portal-resource-manager.md) artículo para las instrucciones de enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="e72da-116">See hello [Configure routing](expressroute-howto-routing-portal-resource-manager.md) article for routing instructions.</span></span>
  * <span data-ttu-id="e72da-117">Asegúrese de que el emparejamiento privado Azure está configurado y Hola emparejamiento de BGP entre la red y Microsoft está activo para que se puede habilitar la conectividad de extremo a extremo.</span><span class="sxs-lookup"><span data-stu-id="e72da-117">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="e72da-118">Asegúrese de que ha creado y aprovisionado totalmente una red virtual y una puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="e72da-118">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="e72da-119">Siga las instrucciones de hello demasiado[crear una puerta de enlace de red virtual para ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e72da-119">Follow hello instructions too[create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="e72da-120">Una puerta de enlace de red virtual para ExpressRoute usa Hola el GatewayType 'ExpressRoute', no VPN.</span><span class="sxs-lookup"><span data-stu-id="e72da-120">A virtual network gateway for ExpressRoute uses hello GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="e72da-121">Puede vincular una circuito de ExpressRoute estándar de too10 redes virtuales tooa.</span><span class="sxs-lookup"><span data-stu-id="e72da-121">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="e72da-122">Todas las redes virtuales deben estar en hello misma región geopolíticos cuando se usa un circuito de ExpressRoute estándar.</span><span class="sxs-lookup"><span data-stu-id="e72da-122">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 
* <span data-ttu-id="e72da-123">Puede vincular una red virtual fuera de la región geopolítica de Hola de hello circuito de ExpressRoute o conectar un mayor número de redes virtuales tooyour circuito ExpressRoute si ha habilitado el complemento de hello ExpressRoute premium.</span><span class="sxs-lookup"><span data-stu-id="e72da-123">You can link a virtual network outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="e72da-124">Comprobar hello [preguntas más frecuentes sobre](expressroute-faqs.md) para obtener más detalles sobre el complemento de hello premium.</span><span class="sxs-lookup"><span data-stu-id="e72da-124">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>
* <span data-ttu-id="e72da-125">También puede [ver un vídeo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) antes de principio toobetter saber cuáles son los pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e72da-125">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) before beginning toobetter understand hello steps.</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="e72da-126">Conectar una red virtual en hello mismo circuito de tooa de suscripción</span><span class="sxs-lookup"><span data-stu-id="e72da-126">Connect a virtual network in hello same subscription tooa circuit</span></span>

### <a name="toocreate-a-connection"></a><span data-ttu-id="e72da-127">toocreate una conexión</span><span class="sxs-lookup"><span data-stu-id="e72da-127">toocreate a connection</span></span>

> [!NOTE]
> <span data-ttu-id="e72da-128">Información de configuración de BGP no aparecerá si el proveedor de capa 3 de hello configurado los emparejamientos.</span><span class="sxs-lookup"><span data-stu-id="e72da-128">BGP configuration information will not show up if hello layer 3 provider configured your peerings.</span></span> <span data-ttu-id="e72da-129">Si el circuito está en un estado de aprovisionamiento, debe ser capaz de toocreate conexiones.</span><span class="sxs-lookup"><span data-stu-id="e72da-129">If your circuit is in a provisioned state, you should be able toocreate connections.</span></span>
>

1. <span data-ttu-id="e72da-130">Asegúrese de que el circuito ExpressRoute y el emparejamiento privado de Azure estén correctamente configurados.</span><span class="sxs-lookup"><span data-stu-id="e72da-130">Ensure that your ExpressRoute circuit and Azure private peering have been configured successfully.</span></span> <span data-ttu-id="e72da-131">Siga las instrucciones de hello en [crear un circuito ExpressRoute](expressroute-howto-circuit-arm.md) y [configurar enrutamiento](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="e72da-131">Follow hello instructions in [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [Configure routing](expressroute-howto-routing-arm.md).</span></span> <span data-ttu-id="e72da-132">El circuito de ExpressRoute debe ser similar Hola después de imagen:</span><span class="sxs-lookup"><span data-stu-id="e72da-132">Your ExpressRoute circuit should look like hello following image:</span></span>

    ![Captura de pantalla de un circuito ExpressRoute](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. <span data-ttu-id="e72da-134">Ahora puede iniciar aprovisionamiento de una conexión toolink su tooyour de puerta de enlace de red virtual circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e72da-134">You can now start provisioning a connection toolink your virtual network gateway tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="e72da-135">Haga clic en **conexión** > **agregar** tooopen hello **Agregar conexión** hoja y, a continuación, configure los valores de hello.</span><span class="sxs-lookup"><span data-stu-id="e72da-135">Click **Connection** > **Add** tooopen hello **Add connection** blade, and then configure hello values.</span></span>

    ![Adición de captura de pantalla de conexión](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. <span data-ttu-id="e72da-137">Después de que la conexión se ha configurado correctamente, el objeto de conexión mostrará información de Hola para conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="e72da-137">After your connection has been successfully configured, your connection object will show hello information for hello connection.</span></span>

     ![Captura de pantalla de objeto de conexión](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="toodelete-a-connection"></a><span data-ttu-id="e72da-139">toodelete una conexión</span><span class="sxs-lookup"><span data-stu-id="e72da-139">toodelete a connection</span></span>
<span data-ttu-id="e72da-140">Puede eliminar una conexión seleccionando hello **eliminar** icono en la hoja de hello para la conexión.</span><span class="sxs-lookup"><span data-stu-id="e72da-140">You can delete a connection by selecting hello **Delete** icon on hello blade for your connection.</span></span>

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="e72da-141">Conectar una red virtual en un circuito de tooa otra suscripción</span><span class="sxs-lookup"><span data-stu-id="e72da-141">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="e72da-142">Puede compartir un circuito ExpressRoute entre varias suscripciones.</span><span class="sxs-lookup"><span data-stu-id="e72da-142">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="e72da-143">Hola siguiente ilustración muestra un sencillo esquemática de cómo compartir funciona para los circuitos ExpressRoute en varias suscripciones.</span><span class="sxs-lookup"><span data-stu-id="e72da-143">hello figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

![Conectividad entre suscripciones](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- <span data-ttu-id="e72da-145">Cada una de las nubes más pequeñas de hello en nube de gran tamaño hello es toorepresent usado suscripciones que pertenecen los departamentos de toodifferent dentro de una organización.</span><span class="sxs-lookup"><span data-stu-id="e72da-145">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span>
- <span data-ttu-id="e72da-146">Cada uno de los departamentos de Hola de organización de hello puede utilizar su propia suscripción para implementar sus servicios, pero pueden compartir una sola red de ExpressRoute circuito tooconnect tooyour atrás local.</span><span class="sxs-lookup"><span data-stu-id="e72da-146">Each of hello departments within hello organization can use their own subscription for deploying their services, but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span>
- <span data-ttu-id="e72da-147">Un departamento único (en este ejemplo: TI) puede poseer el circuito de ExpressRoute Hola.</span><span class="sxs-lookup"><span data-stu-id="e72da-147">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="e72da-148">Otras suscripciones dentro de la organización de hello pueden utilizar el circuito de ExpressRoute Hola.</span><span class="sxs-lookup"><span data-stu-id="e72da-148">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e72da-149">Los cargos de conectividad y ancho de banda para el circuito dedicado de hello será propietario del circuito de ExpressRoute toohello aplicada.</span><span class="sxs-lookup"><span data-stu-id="e72da-149">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute circuit owner.</span></span> <span data-ttu-id="e72da-150">Todas las redes virtuales compartan Hola mismo ancho de banda.</span><span class="sxs-lookup"><span data-stu-id="e72da-150">All virtual networks share hello same bandwidth.</span></span>
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="e72da-151">Administración: los propietarios de circuito y los usuarios de circuito</span><span class="sxs-lookup"><span data-stu-id="e72da-151">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="e72da-152">Hola 'propietario del circuito' es un usuario autorizado de alimentación de hello recursos de circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e72da-152">hello 'circuit owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="e72da-153">propietario del circuito Hola puede crear autorizaciones que se pueden canjear por 'usuarios del circuito'.</span><span class="sxs-lookup"><span data-stu-id="e72da-153">hello circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="e72da-154">Los usuarios de circuito son propietarios de red virtual puertas de enlace que no están en Hola misma suscripción como Hola circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e72da-154">Circuit users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="e72da-155">Los usuarios del circuito pueden canjear autorizaciones (una autorización por red virtual).</span><span class="sxs-lookup"><span data-stu-id="e72da-155">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="e72da-156">propietario del circuito Hello tiene Hola power toomodify y revocar las autorizaciones en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="e72da-156">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="e72da-157">Revocar el resultado de una autorización en todas las conexiones de vínculo que se va a eliminar de suscripción de hello cuyo acceso se ha revocado.</span><span class="sxs-lookup"><span data-stu-id="e72da-157">Revoking an authorization results in all link connections being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="e72da-158">Operaciones del propietario del circuito</span><span class="sxs-lookup"><span data-stu-id="e72da-158">Circuit owner operations</span></span>

<span data-ttu-id="e72da-159">**toocreate una autorización de conexión**</span><span class="sxs-lookup"><span data-stu-id="e72da-159">**toocreate a connection authorization**</span></span>

<span data-ttu-id="e72da-160">propietario del circuito Hola crea una autorización.</span><span class="sxs-lookup"><span data-stu-id="e72da-160">hello circuit owner creates an authorization.</span></span> <span data-ttu-id="e72da-161">Esto resulta en hello creación de una clave de autorización que puede ser utilizados por un tooconnect de usuario de circuito su toohello de puertas de enlace de red virtual circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e72da-161">This results in hello creation of an authorization key that can be used by a circuit user tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="e72da-162">Una autorización solo es válida para una conexión.</span><span class="sxs-lookup"><span data-stu-id="e72da-162">An authorization is valid for only one connection.</span></span>

1. <span data-ttu-id="e72da-163">En la hoja de ExpressRoute de hello, haga clic en **autorizaciones** y, a continuación, escriba un **nombre** para la autorización de Hola y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="e72da-163">In hello ExpressRoute blade, Click **Authorizations** and then type a **name** for hello authorization and click **Save**.</span></span>

    ![Autorizaciones](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. <span data-ttu-id="e72da-165">Una vez que se guarda la configuración de hello, copie hello **Id. de recurso** hello y **clave de autorización**.</span><span class="sxs-lookup"><span data-stu-id="e72da-165">Once hello configuration is saved, copy hello **Resource ID** and hello **Authorization Key**.</span></span>

    ![Clave de autorización](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

<span data-ttu-id="e72da-167">**toodelete una autorización de conexión**</span><span class="sxs-lookup"><span data-stu-id="e72da-167">**toodelete a connection authorization**</span></span>

<span data-ttu-id="e72da-168">Puede eliminar una conexión seleccionando hello **eliminar** icono en la hoja de hello para la conexión.</span><span class="sxs-lookup"><span data-stu-id="e72da-168">You can delete a connection by selecting hello **Delete** icon on hello blade for your connection.</span></span>

### <a name="circuit-user-operations"></a><span data-ttu-id="e72da-169">Operaciones del usuario del circuito</span><span class="sxs-lookup"><span data-stu-id="e72da-169">Circuit user operations</span></span>

<span data-ttu-id="e72da-170">usuario de circuito de Hello necesita Id. de recurso de hello y una clave de autorización de propietario del circuito Hola.</span><span class="sxs-lookup"><span data-stu-id="e72da-170">hello circuit user needs hello resource ID and an authorization key from hello circuit owner.</span></span> 

<span data-ttu-id="e72da-171">**tooredeem una autorización de conexión**</span><span class="sxs-lookup"><span data-stu-id="e72da-171">**tooredeem a connection authorization**</span></span>

1.  <span data-ttu-id="e72da-172">Haga clic en hello **+ nuevo** botón.</span><span class="sxs-lookup"><span data-stu-id="e72da-172">Click hello **+New** button.</span></span>

    ![Haga clic en Nuevo](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  <span data-ttu-id="e72da-174">Busque **"Conexión"** Hola Marketplace, selecciónelo y haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="e72da-174">Search for **"Connection"** in hello Marketplace, select it, and click **Create**.</span></span>

    ![Búsqueda de conexión](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  <span data-ttu-id="e72da-176">Asegúrese de hello seguro **tipo de conexión** se establece demasiado "ExpressRoute".</span><span class="sxs-lookup"><span data-stu-id="e72da-176">Make sure hello **Connection type** is set too"ExpressRoute".</span></span>


4.  <span data-ttu-id="e72da-177">Rellene los detalles de hello, a continuación, haga clic en **Aceptar** en la hoja de conceptos básicos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e72da-177">Fill in hello details, then click **OK** in hello Basics blade.</span></span>

    ![Hoja Básico](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  <span data-ttu-id="e72da-179">Hola **configuración** hoja, seleccione hello **puerta de enlace de red Virtual** y comprobar hello **canjear autorización** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="e72da-179">In hello **Settings** blade, Select hello **Virtual network gateway** and check hello **Redeem authorization** check box.</span></span>

6.  <span data-ttu-id="e72da-180">Escriba hello **clave de autorización** hello y **del mismo nivel circuito URI** y asigne un nombre de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="e72da-180">Enter hello **Authorization key** and hello **Peer circuit URI** and give hello connection a name.</span></span> <span data-ttu-id="e72da-181">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e72da-181">Click **OK**.</span></span>

    ![Hoja Configuración](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. <span data-ttu-id="e72da-183">Revise la información de Hola Hola **resumen** hoja y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e72da-183">Review hello information in hello **Summary** blade and click **OK**.</span></span>


<span data-ttu-id="e72da-184">**toorelease una autorización de conexión**</span><span class="sxs-lookup"><span data-stu-id="e72da-184">**toorelease a connection authorization**</span></span>

<span data-ttu-id="e72da-185">Puede liberar una autorización mediante la eliminación de la conexión de Hola que vincula la red virtual del toohello de circuito ExpressRoute Hola.</span><span class="sxs-lookup"><span data-stu-id="e72da-185">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e72da-186">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e72da-186">Next steps</span></span>
<span data-ttu-id="e72da-187">Para obtener más información sobre ExpressRoute, consulte hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="e72da-187">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
