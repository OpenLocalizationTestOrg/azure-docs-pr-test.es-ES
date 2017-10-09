---
title: 'Agregar varios tooa de conexiones de sitio a sitio de la puerta de enlace VPN red virtual: Portal de Azure: Administrador de recursos | Documentos de Microsoft'
description: "Agregar varios sitio S2S conexiones tooa puerta de enlace VPN que tiene una conexión existente"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3e8b165-f20a-42ab-afbb-bf60974bb4b1
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: cherylmc
ms.openlocfilehash: b8c9ff454967f509dcef725f8bcec8564fad9b00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection"></a><span data-ttu-id="734a9-103">Agregar una tooa de conexión de sitio a sitio red virtual con una conexión de puerta de enlace VPN existente</span><span class="sxs-lookup"><span data-stu-id="734a9-103">Add a Site-to-Site connection tooa VNet with an existing VPN gateway connection</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="734a9-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="734a9-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="734a9-105">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="734a9-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
> 

<span data-ttu-id="734a9-106">Este artículo le guiará a través de hello tooadd portal Azure sitio a sitio (S2S) conexiones tooa puerta de enlace VPN que tiene una conexión existente.</span><span class="sxs-lookup"><span data-stu-id="734a9-106">This article walks you through using hello Azure portal tooadd Site-to-Site (S2S) connections tooa VPN gateway that has an existing connection.</span></span> <span data-ttu-id="734a9-107">Este tipo de conexión es a menudo tooas que se hace referencia una configuración de "varios sitio".</span><span class="sxs-lookup"><span data-stu-id="734a9-107">This type of connection is often referred tooas a "multi-site" configuration.</span></span> <span data-ttu-id="734a9-108">Puede agregar una tooa de conexión de S2S red virtual que ya tiene una conexión de S2S, la conexión de punto a sitio o la conexión de red virtual a red virtual.</span><span class="sxs-lookup"><span data-stu-id="734a9-108">You can add a S2S connection tooa VNet that already has a S2S connection, Point-to-Site connection, or VNet-to-VNet connection.</span></span> <span data-ttu-id="734a9-109">Existen algunas limitaciones al agregar conexiones.</span><span class="sxs-lookup"><span data-stu-id="734a9-109">There are some limitations when adding connections.</span></span> <span data-ttu-id="734a9-110">Comprobar hello [antes de comenzar](#before) sección en este artículo de tooverify antes de iniciar la configuración.</span><span class="sxs-lookup"><span data-stu-id="734a9-110">Check hello [Before you begin](#before) section in this article tooverify before you start your configuration.</span></span> 

<span data-ttu-id="734a9-111">En este artículo se aplica tooVNets creados mediante el modelo de implementación del Administrador de recursos de Hola que tienen una puerta de enlace de VPN RouteBased.</span><span class="sxs-lookup"><span data-stu-id="734a9-111">This article applies tooVNets created using hello Resource Manager deployment model that have a RouteBased VPN gateway.</span></span> <span data-ttu-id="734a9-112">Estos pasos no aplican las configuraciones de conexión coexistentes tooExpressRoute/sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="734a9-112">These steps do not apply tooExpressRoute/Site-to-Site coexisting connection configurations.</span></span> <span data-ttu-id="734a9-113">Consulte [conexiones coexistentes de ExpressRoute/S2S](../expressroute/expressroute-howto-coexist-resource-manager.md) para obtener información sobre las conexiones coexistentes.</span><span class="sxs-lookup"><span data-stu-id="734a9-113">See [ExpressRoute/S2S coexisting connections](../expressroute/expressroute-howto-coexist-resource-manager.md) for information about coexisting connections.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="734a9-114">Modelos de implementación y métodos</span><span class="sxs-lookup"><span data-stu-id="734a9-114">Deployment models and methods</span></span>
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="734a9-115">Esta tabla se actualiza cada vez que hay nuevos artículos y nuevas herramientas disponibles para esta configuración.</span><span class="sxs-lookup"><span data-stu-id="734a9-115">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="734a9-116">Cuando un artículo está disponible, vinculamos directamente tooit de esta tabla.</span><span class="sxs-lookup"><span data-stu-id="734a9-116">When an article is available, we link directly tooit from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <span data-ttu-id="734a9-117"><a name="before"></a>Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="734a9-117"><a name="before"></a>Before you begin</span></span>
<span data-ttu-id="734a9-118">Comprobar Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="734a9-118">Verify hello following items:</span></span>

* <span data-ttu-id="734a9-119">No está creando una conexión coexistente ExpressRoute/S2S.</span><span class="sxs-lookup"><span data-stu-id="734a9-119">You are not creating an ExpressRoute/S2S coexisting connection.</span></span>
* <span data-ttu-id="734a9-120">Tener una red virtual que se creó mediante el modelo de implementación del Administrador de recursos de hello con una conexión existente.</span><span class="sxs-lookup"><span data-stu-id="734a9-120">You have a virtual network that was created using hello Resource Manager deployment model with an existing connection.</span></span>
* <span data-ttu-id="734a9-121">puerta de enlace de red virtual de Hello para la red virtual es RouteBased.</span><span class="sxs-lookup"><span data-stu-id="734a9-121">hello virtual network gateway for your VNet is RouteBased.</span></span> <span data-ttu-id="734a9-122">Si tiene una puerta de enlace PolicyBased VPN, debe eliminar la puerta de enlace de red virtual de Hola y crear una nueva puerta de enlace VPN como del tipo routebased..</span><span class="sxs-lookup"><span data-stu-id="734a9-122">If you have a PolicyBased VPN gateway, you must delete hello virtual network gateway and create a new VPN gateway as RouteBased.</span></span>
* <span data-ttu-id="734a9-123">Ninguno de los intervalos de direcciones de Hola se superponen para cualquiera de hello redes virtuales que se está conectando a esta red virtual.</span><span class="sxs-lookup"><span data-stu-id="734a9-123">None of hello address ranges overlap for any of hello VNets that this VNet is connecting to.</span></span>
* <span data-ttu-id="734a9-124">Dispondrá de dispositivo VPN compatible y alguna persona tooconfigure capaz de él.</span><span class="sxs-lookup"><span data-stu-id="734a9-124">You have compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="734a9-125">Consulte [Acerca de los dispositivos VPN para conexiones de red virtual de sitio a sitio](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="734a9-125">See [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span> <span data-ttu-id="734a9-126">Si no está familiarizado con la configuración de dispositivo VPN, o si está familiarizado con los intervalos de direcciones IP de hello ubicados en la configuración de red local, deberá toocoordinate con alguien que pueda proporcionarle estos detalles para usted.</span><span class="sxs-lookup"><span data-stu-id="734a9-126">If you aren't familiar with configuring your VPN device, or are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span>
* <span data-ttu-id="734a9-127">Tiene una dirección IP pública externa para el dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="734a9-127">You have an externally facing public IP address for your VPN device.</span></span> <span data-ttu-id="734a9-128">Esta dirección IP no puede estar detrás de un NAT.</span><span class="sxs-lookup"><span data-stu-id="734a9-128">This IP address cannot be located behind a NAT.</span></span>

## <span data-ttu-id="734a9-129"><a name="part1"></a>Parte 1: Configuración de una conexión</span><span class="sxs-lookup"><span data-stu-id="734a9-129"><a name="part1"></a>Part 1 - Configure a connection</span></span>
1. <span data-ttu-id="734a9-130">Desde un explorador, navegue toohello [portal de Azure](http://portal.azure.com) y, si es necesario, inicie sesión con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="734a9-130">From a browser, navigate toohello [Azure portal](http://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="734a9-131">Haga clic en **todos los recursos** y busque el **puerta de enlace de red virtual** de lista de Hola de recursos y haga clic en él.</span><span class="sxs-lookup"><span data-stu-id="734a9-131">Click **All resources** and locate your **virtual network gateway** from hello list of resources and click it.</span></span>
3. <span data-ttu-id="734a9-132">En hello **puerta de enlace de red Virtual** hoja, haga clic en **conexiones**.</span><span class="sxs-lookup"><span data-stu-id="734a9-132">On hello **Virtual network gateway** blade, click **Connections**.</span></span>
   
    <span data-ttu-id="734a9-133">![Hoja de conexiones](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Hoja de conexiones")</span><span class="sxs-lookup"><span data-stu-id="734a9-133">![Connections blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Connections blade")</span></span><br>
4. <span data-ttu-id="734a9-134">En hello **conexiones** hoja, haga clic en **+ agregar**.</span><span class="sxs-lookup"><span data-stu-id="734a9-134">On hello **Connections** blade, click **+Add**.</span></span>
   
    <span data-ttu-id="734a9-135">![Botón de agregar conexión](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "botón de agregar conexión")</span><span class="sxs-lookup"><span data-stu-id="734a9-135">![Add connection button](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "Add connection button")</span></span><br>
5. <span data-ttu-id="734a9-136">En hello **Agregar conexión** hoja, rellene Hola siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="734a9-136">On hello **Add connection** blade, fill out hello following fields:</span></span>
   
   * <span data-ttu-id="734a9-137">**Nombre:** nombre hello desea toogive toohello sitio va a crear la conexión de Hola a.</span><span class="sxs-lookup"><span data-stu-id="734a9-137">**Name:** hello name you want toogive toohello site you are creating hello connection to.</span></span>
   * <span data-ttu-id="734a9-138">**Tipo de conexión:** seleccione **Sitio a sitio (IPsec)**.</span><span class="sxs-lookup"><span data-stu-id="734a9-138">**Connection type:** Select **Site-to-site (IPsec)**.</span></span>
     
     <span data-ttu-id="734a9-139">![Agregar hoja de conexión](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "hoja de agregar conexión")</span><span class="sxs-lookup"><span data-stu-id="734a9-139">![Add connection blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Add connection blade")</span></span><br>

## <span data-ttu-id="734a9-140"><a name="part2"></a>Parte 2: Agregar una puerta de enlace de red local</span><span class="sxs-lookup"><span data-stu-id="734a9-140"><a name="part2"></a>Part 2 - Add a local network gateway</span></span>
1. <span data-ttu-id="734a9-141">Haga clic en **Puerta de enlace de red local** ***Elegir una puerta de enlace de red local***.</span><span class="sxs-lookup"><span data-stu-id="734a9-141">Click **Local network gateway** ***Choose a local network gateway***.</span></span> <span data-ttu-id="734a9-142">Se abrirá hello **puerta de enlace de red local elija** hoja.</span><span class="sxs-lookup"><span data-stu-id="734a9-142">This will open hello **Choose local network gateway** blade.</span></span>
   
    <span data-ttu-id="734a9-143">![Puerta de enlace de red local elija](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "elegir puerta de enlace de red local")</span><span class="sxs-lookup"><span data-stu-id="734a9-143">![Choose local network gateway](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "Choose local network gateway")</span></span><br>
2. <span data-ttu-id="734a9-144">Haga clic en **crear nuevo** tooopen hello **crear puerta de enlace de red local** hoja.</span><span class="sxs-lookup"><span data-stu-id="734a9-144">Click **Create new** tooopen hello **Create local network gateway** blade.</span></span>
   
    <span data-ttu-id="734a9-145">![Hoja de puerta de enlace de red local crear](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "crear puerta de enlace de red local")</span><span class="sxs-lookup"><span data-stu-id="734a9-145">![Create local network gateway blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "Create local network gateway")</span></span><br>
3. <span data-ttu-id="734a9-146">En hello **crear puerta de enlace de red local** hoja, rellene Hola siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="734a9-146">On hello **Create local network gateway** blade, fill out hello following fields:</span></span>
   
   * <span data-ttu-id="734a9-147">**Nombre:** nombre hello desea recurso de puerta de enlace de red local de toogive toohello.</span><span class="sxs-lookup"><span data-stu-id="734a9-147">**Name:** hello name you want toogive toohello local network gateway resource.</span></span>
   * <span data-ttu-id="734a9-148">**Dirección IP:** Hola dirección IP pública del dispositivo VPN de hello en el sitio de Hola que desee tooconnect a.</span><span class="sxs-lookup"><span data-stu-id="734a9-148">**IP address:** hello public IP address of hello VPN device on hello site that you want tooconnect to.</span></span>
   * <span data-ttu-id="734a9-149">**Espacio de direcciones:** espacio de direcciones de Hola que desea toobe enruta toohello nuevo sitio de red local.</span><span class="sxs-lookup"><span data-stu-id="734a9-149">**Address space:** hello address space that you want toobe routed toohello new local network site.</span></span>
4. <span data-ttu-id="734a9-150">Haga clic en **Aceptar** en hello **crear puerta de enlace de red local** cambios de hoja toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="734a9-150">Click **OK** on hello **Create local network gateway** blade toosave hello changes.</span></span>

## <span data-ttu-id="734a9-151"><a name="part3"></a>Parte 3: Agregar clave compartida de Hola y crear la conexión de Hola</span><span class="sxs-lookup"><span data-stu-id="734a9-151"><a name="part3"></a>Part 3 - Add hello shared key and create hello connection</span></span>
1. <span data-ttu-id="734a9-152">En hello **Agregar conexión** hoja, Agregar clave compartida de Hola que desea toouse toocreate la conexión.</span><span class="sxs-lookup"><span data-stu-id="734a9-152">On hello **Add connection** blade, add hello shared key that you want toouse toocreate your connection.</span></span> <span data-ttu-id="734a9-153">Puede obtener una clave compartida Hola desde su dispositivo VPN, o crear uno aquí y, a continuación, configurar su Hola de toouse del dispositivo VPN misma clave compartida.</span><span class="sxs-lookup"><span data-stu-id="734a9-153">You can either get hello shared key from your VPN device, or make one up here and then configure your VPN device toouse hello same shared key.</span></span> <span data-ttu-id="734a9-154">Hola importante que es que las claves de hello son exactamente Hola igual.</span><span class="sxs-lookup"><span data-stu-id="734a9-154">hello important thing is that hello keys are exactly hello same.</span></span>
   
    <span data-ttu-id="734a9-155">![Clave compartida](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Clave compartida")</span><span class="sxs-lookup"><span data-stu-id="734a9-155">![Shared key](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Shared key")</span></span><br>
2. <span data-ttu-id="734a9-156">En la parte inferior de Hola de hoja de hello, haga clic en **Aceptar** conexión de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="734a9-156">At hello bottom of hello blade, click **OK** toocreate hello connection.</span></span>

## <span data-ttu-id="734a9-157"><a name="part4"></a>Parte 4: comprobar la conexión de VPN de Hola</span><span class="sxs-lookup"><span data-stu-id="734a9-157"><a name="part4"></a>Part 4 - Verify hello VPN connection</span></span>


[!INCLUDE [vpn-gateway-verify-connection-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="734a9-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="734a9-158">Next steps</span></span>

<span data-ttu-id="734a9-159">Una vez completada la conexión, puede agregar redes virtuales de máquinas virtuales tooyour.</span><span class="sxs-lookup"><span data-stu-id="734a9-159">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="734a9-160">Ver máquinas virtuales de hello [ruta de acceso de aprendizaje](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="734a9-160">See hello virtual machines [learning path](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) for more information.</span></span>
