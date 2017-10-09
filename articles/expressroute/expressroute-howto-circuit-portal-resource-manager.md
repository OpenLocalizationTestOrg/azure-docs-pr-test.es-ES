---
title: "Creación y modificación de un circuito ExpressRoute mediante Azure Portal | Microsoft Docs"
description: "Este artículo describe cómo toocreate, aprovisionar, compruebe, actualizar, eliminar y cancelar el aprovisionamiento de un circuito de ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68d59d59-ed4d-482f-9cbc-534ebb090613
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/07/2017
ms.author: cherylmc;ganesr
ms.openlocfilehash: 200418aed6bdebace43a2f57cf532d1c8d13cb83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit"></a><span data-ttu-id="98625-103">Creación y modificación de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="98625-103">Create and modify an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="98625-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="98625-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="98625-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="98625-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="98625-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="98625-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="98625-107">Vídeo: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="98625-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="98625-108">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="98625-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="98625-109">Este artículo describe cómo toocreate un circuito de ExpressRoute de Azure mediante el uso de hello Azure modelo de implementación de Azure Resource Manager hello y portal.</span><span class="sxs-lookup"><span data-stu-id="98625-109">This article describes how toocreate an Azure ExpressRoute circuit by using hello Azure portal and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="98625-110">Hola siguientes pasos también muestra cómo actualizarlo, estado de hello toocheck del circuito de hello, o eliminar y Cancelar.</span><span class="sxs-lookup"><span data-stu-id="98625-110">hello following steps also show you how toocheck hello status of hello circuit, update it, or delete and deprovision it.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="98625-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="98625-111">Before you begin</span></span>
* <span data-ttu-id="98625-112">Hola de revisión [requisitos previos](expressroute-prerequisites.md) y [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="98625-112">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="98625-113">Asegúrese de que tiene acceso toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="98625-113">Ensure that you have access toohello [Azure portal](https://portal.azure.com).</span></span>
* <span data-ttu-id="98625-114">Asegúrese de que dispone de recursos de red nuevos permisos toocreate.</span><span class="sxs-lookup"><span data-stu-id="98625-114">Ensure that you have permissions toocreate new networking resources.</span></span> <span data-ttu-id="98625-115">Si no tiene los permisos adecuados de hello, póngase en contacto con el Administrador de cuentas.</span><span class="sxs-lookup"><span data-stu-id="98625-115">Contact your account administrator if you do not have hello right permissions.</span></span>
* <span data-ttu-id="98625-116">También puede [ver un vídeo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) antes de comenzar en orden toobetter comprender los pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="98625-116">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) before beginning in order toobetter understand hello steps.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="98625-117">Creación y aprovisionamiento de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="98625-117">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-toohello-azure-portal"></a><span data-ttu-id="98625-118">1. Inicie sesión en toohello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="98625-118">1. Sign in toohello Azure portal</span></span>
<span data-ttu-id="98625-119">Desde un explorador, navegue toohello [portal de Azure](http://portal.azure.com) e inicie sesión con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="98625-119">From a browser, navigate toohello [Azure portal](http://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="2-create-a-new-expressroute-circuit"></a><span data-ttu-id="98625-120">2. Creación de un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="98625-120">2. Create a new ExpressRoute circuit</span></span>
> [!IMPORTANT]
> <span data-ttu-id="98625-121">El circuito de ExpressRoute se cobrará desde el momento de Hola que se emite una clave de servicio.</span><span class="sxs-lookup"><span data-stu-id="98625-121">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="98625-122">Asegúrese de que lleva a cabo esta operación cuando proveedor de conectividad de hello circuito de hello tooprovision listo.</span><span class="sxs-lookup"><span data-stu-id="98625-122">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

1. <span data-ttu-id="98625-123">Puede crear un circuito ExpressRoute seleccionando Hola opción toocreate un nuevo recurso.</span><span class="sxs-lookup"><span data-stu-id="98625-123">You can create an ExpressRoute circuit by selecting hello option toocreate a new resource.</span></span> <span data-ttu-id="98625-124">Haga clic en **New** > **red** > **ExpressRoute**, tal y como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="98625-124">Click **New** > **Networking** > **ExpressRoute**, as shown in hello following image:</span></span>
   
    ![Creación de un circuito ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. <span data-ttu-id="98625-126">Tras hacer clic en **ExpressRoute**, verá hello **circuito de ExpressRoute crear** hoja.</span><span class="sxs-lookup"><span data-stu-id="98625-126">After you click **ExpressRoute**, you'll see hello **Create ExpressRoute circuit** blade.</span></span> <span data-ttu-id="98625-127">Cuando está rellena los valores de hello en esta hoja, asegúrese de que se especifique nivel correcto de la SKU de Hola y medición de datos.</span><span class="sxs-lookup"><span data-stu-id="98625-127">When you're filling in hello values on this blade, make sure that you specify hello correct SKU tier and data metering.</span></span>
   
   * <span data-ttu-id="98625-128">**Nivel** determina si está habilitado un complemento estándar o premium de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="98625-128">**Tier** determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="98625-129">Puede especificar **estándar** tooget Hola SKU estándar o **Premium** para el complemento de hello premium.</span><span class="sxs-lookup"><span data-stu-id="98625-129">You can specify **Standard** tooget hello standard SKU or **Premium** for hello premium add-on.</span></span>
   * <span data-ttu-id="98625-130">**Medición de datos** determina el tipo de facturación de Hola.</span><span class="sxs-lookup"><span data-stu-id="98625-130">**Data metering** determines hello billing type.</span></span> <span data-ttu-id="98625-131">Puede especificar **Metered** (Limitado) para un plan de datos limitado y **Unlimited** (Ilimitado) para un plan de datos ilimitado.</span><span class="sxs-lookup"><span data-stu-id="98625-131">You can specify **Metered** for a metered data plan and **Unlimited** for an unlimited data plan.</span></span> <span data-ttu-id="98625-132">Tenga en cuenta que puede cambiar el tipo de facturación de Hola de **Metered** demasiado**Unlimited**, pero no se puede cambiar tipo hello de **Unlimited** demasiado**Metered**.</span><span class="sxs-lookup"><span data-stu-id="98625-132">Note that you can change hello billing type from **Metered** too**Unlimited**, but you can't change hello type from **Unlimited** too**Metered**.</span></span>
     
     ![Configurar el nivel de la SKU de Hola y medición de datos](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> <span data-ttu-id="98625-134">Ten en cuenta esa ubicación de emparejamiento de hello indica hello [ubicación física](expressroute-locations.md) donde están emparejamiento con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="98625-134">Please be aware that hello Peering Location indicates hello [physical location](expressroute-locations.md) where you are peering with Microsoft.</span></span> <span data-ttu-id="98625-135">Se trata de **no** vinculado demasiado propiedad "Location", que hace referencia geography toohello donde se encuentra Hola proveedor de recursos de red de Azure.</span><span class="sxs-lookup"><span data-stu-id="98625-135">This is **not** linked too"Location" property, which refers toohello geography where hello Azure Network Resource Provider is located.</span></span> <span data-ttu-id="98625-136">Aunque no están relacionadas, es un toochoose recomendable una ubicación de emparejamiento del circuito de Hola de proveedor de recursos de red geográficamente cerrar toohello.</span><span class="sxs-lookup"><span data-stu-id="98625-136">While they are not related, it is a good practice toochoose a Network Resource Provider geographically close toohello Peering Location of hello circuit.</span></span> 
> 
> 

### <a name="3-view-hello-circuits-and-properties"></a><span data-ttu-id="98625-137">3. Vista Hola circuitos y propiedades</span><span class="sxs-lookup"><span data-stu-id="98625-137">3. View hello circuits and properties</span></span>
<span data-ttu-id="98625-138">**Ver todos los circuitos de Hola**</span><span class="sxs-lookup"><span data-stu-id="98625-138">**View all hello circuits**</span></span>

<span data-ttu-id="98625-139">Puede ver todos los circuitos de Hola que creaste seleccionando **todos los recursos** en el menú del lado izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="98625-139">You can view all hello circuits that you created by selecting **All resources** on hello left-side menu.</span></span>

![Visualización de circuitos](./media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

<span data-ttu-id="98625-141">**Ver propiedades de Hola**</span><span class="sxs-lookup"><span data-stu-id="98625-141">**View hello properties**</span></span>

    You can view hello properties of hello circuit by selecting it. On this blade, note hello service key for hello circuit. You must copy hello circuit key for your circuit and pass it down toohello service provider toocomplete hello provisioning process. hello circuit key is specific tooyour circuit.

![Ver propiedades](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="98625-143">4. Enviar el proveedor de conectividad de tooyour clave de servicio de hello para el aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="98625-143">4. Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="98625-144">En esta hoja, **estado del proveedor** proporciona información sobre el estado actual de Hola de aprovisionamiento en el lado del proveedor de servicios de Hola.</span><span class="sxs-lookup"><span data-stu-id="98625-144">On this blade, **Provider status** provides information on hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="98625-145">**Estado de circuito** proporciona el estado de hello en hello side de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="98625-145">**Circuit status** provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="98625-146">Para obtener más información acerca de los Estados de aprovisionamiento del circuito, vea hello [flujos de trabajo](expressroute-workflows.md#expressroute-circuit-provisioning-states) artículo.</span><span class="sxs-lookup"><span data-stu-id="98625-146">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="98625-147">Cuando se crea un nuevo circuito de ExpressRoute, circuito Hola estará en hello siguiente estado:</span><span class="sxs-lookup"><span data-stu-id="98625-147">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

<span data-ttu-id="98625-148">Estado de proveedor: No aprovisionado</span><span class="sxs-lookup"><span data-stu-id="98625-148">Provider status: Not provisioned</span></span><BR>
<span data-ttu-id="98625-149">Estado de circuito: Habilitado</span><span class="sxs-lookup"><span data-stu-id="98625-149">Circuit status: Enabled</span></span>

![Inicio del proceso de aprovisionamiento](./media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

<span data-ttu-id="98625-151">circuito Hola cambiará toohello siguiente estado cuando el proveedor de conectividad de hello está en proceso de Hola de habilitarla para:</span><span class="sxs-lookup"><span data-stu-id="98625-151">hello circuit will change toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

<span data-ttu-id="98625-152">Estado de proveedor: Aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="98625-152">Provider status: Provisioning</span></span><BR>
<span data-ttu-id="98625-153">Estado de circuito: Habilitado</span><span class="sxs-lookup"><span data-stu-id="98625-153">Circuit status: Enabled</span></span>

<span data-ttu-id="98625-154">Para toobe pueda toouse un circuito ExpressRoute, debe estar en hello siguiente estado:</span><span class="sxs-lookup"><span data-stu-id="98625-154">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

<span data-ttu-id="98625-155">Estado de proveedor: Aprovisionado</span><span class="sxs-lookup"><span data-stu-id="98625-155">Provider status: Provisioned</span></span><BR>
<span data-ttu-id="98625-156">Estado de circuito: Habilitado</span><span class="sxs-lookup"><span data-stu-id="98625-156">Circuit status: Enabled</span></span>

### <a name="5-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="98625-157">5. Comprobar periódicamente el estado de Hola y el estado de Hola de clave de circuito de Hola</span><span class="sxs-lookup"><span data-stu-id="98625-157">5. Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="98625-158">Puede ver propiedades de Hola de circuito de Hola que le interesa, selecciónelo.</span><span class="sxs-lookup"><span data-stu-id="98625-158">You can view hello properties of hello circuit that you're interested in by selecting it.</span></span> <span data-ttu-id="98625-159">Comprobar hello **estado del proveedor** y asegúrese de que se ha movido demasiado**aprovisionado** antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="98625-159">Check hello **Provider status** and ensure that it has moved too**Provisioned** before you continue.</span></span>

![Estado del circuito y proveedor](./media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a><span data-ttu-id="98625-161">6. Creación de la configuración de enrutamiento</span><span class="sxs-lookup"><span data-stu-id="98625-161">6. Create your routing configuration</span></span>
<span data-ttu-id="98625-162">Para obtener instrucciones detalladas, consulte toohello [circuito de ExpressRoute de configuración de enrutamiento](expressroute-howto-routing-portal-resource-manager.md) artículo toocreate y modificar los emparejamientos de circuito.</span><span class="sxs-lookup"><span data-stu-id="98625-162">For step-by-step instructions, refer toohello [ExpressRoute circuit routing configuration](expressroute-howto-routing-portal-resource-manager.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="98625-163">Estas instrucciones aplican solo toocircuits que se crean con proveedores de servicios que ofrecen servicios de conectividad de 2 niveles.</span><span class="sxs-lookup"><span data-stu-id="98625-163">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="98625-164">Si usa un proveedor de servicios que ofrece servicios administrados de nivel 3 (normalmente VPN IP, como MPLS), el mismo proveedor de conectividad configurará y administrará el enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="98625-164">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="7-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="98625-165">7. Vincular un circuito de ExpressRoute de tooan de red virtual</span><span class="sxs-lookup"><span data-stu-id="98625-165">7. Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="98625-166">A continuación, vincular un circuito de ExpressRoute de tooyour de red virtual.</span><span class="sxs-lookup"><span data-stu-id="98625-166">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="98625-167">Hola de uso [vinculación virtual redes tooExpressRoute circuitos](expressroute-howto-linkvnet-arm.md) artículo cuando se trabaja con el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="98625-167">Use hello [Linking virtual networks tooExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with hello Resource Manager deployment model.</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="98625-168">Obtener el estado de saludo de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="98625-168">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="98625-169">Puede ver el estado de Hola de un circuito, selecciónelo.</span><span class="sxs-lookup"><span data-stu-id="98625-169">You can view hello status of a circuit by selecting it.</span></span> 

![Estado de un circuito ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="98625-171">Modificación de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="98625-171">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="98625-172">Puede modificar determinadas propiedades de un circuito ExpressRoute sin afectar a la conectividad.</span><span class="sxs-lookup"><span data-stu-id="98625-172">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="98625-173">Puede hacer Hola sigue sin tiempo de inactividad:</span><span class="sxs-lookup"><span data-stu-id="98625-173">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="98625-174">Habilitar o deshabilitar el complemento ExpressRoute Premium en su circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="98625-174">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="98625-175">Ancho de banda de Hola de aumento de su circuito de ExpressRoute proporciona hay capacidad disponible en el puerto de Hola.</span><span class="sxs-lookup"><span data-stu-id="98625-175">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="98625-176">Tenga en cuenta que no se admite la degradación de ancho de banda de Hola de un circuito.</span><span class="sxs-lookup"><span data-stu-id="98625-176">Note that downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="98625-177">Cambiar Hola plan desde tooUnlimited datos limitados de datos de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="98625-177">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="98625-178">Tenga en cuenta ese plan de disponibilidad de hello cambiante de tooMetered datos ilimitados que datos no se admiten.</span><span class="sxs-lookup"><span data-stu-id="98625-178">Note that changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="98625-179">Puede habilitar y deshabilitar *Allow Classic Operations*(Permitir operaciones clásicas).</span><span class="sxs-lookup"><span data-stu-id="98625-179">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="98625-180">Para obtener más información sobre los límites y limitaciones, consulte toohello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="98625-180">For more information on limits and limitations, refer toohello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

<span data-ttu-id="98625-181">toomodify un circuito ExpressRoute, haga clic en hello **configuración** tal y como se muestra en la siguiente ilustración de Hola.</span><span class="sxs-lookup"><span data-stu-id="98625-181">toomodify an ExpressRoute circuit, click on hello **Configuration** as shown in hello figure below.</span></span>

![Modificación del circuito](./media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

<span data-ttu-id="98625-183">Puede modificar el ancho de banda de hello, SKU, modelo de facturación y permiten operaciones clásicas dentro de la hoja de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="98625-183">You can modify hello bandwidth, SKU, billing model and allow classic operations within hello configuration blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="98625-184">Puede tener circuito de ExpressRoute de hello toorecreate si hay capacidad inadecuada en el puerto existente Hola.</span><span class="sxs-lookup"><span data-stu-id="98625-184">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="98625-185">No puede actualizar el circuito de hello si no hay ninguna capacidad adicional disponible en esa ubicación.</span><span class="sxs-lookup"><span data-stu-id="98625-185">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="98625-186">No se puede reducir el ancho de banda de Hola de un circuito de ExpressRoute sin interrupciones.</span><span class="sxs-lookup"><span data-stu-id="98625-186">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="98625-187">Degradar de ancho de banda requiere circuito de ExpressRoute de toodeprovision hello y, a continuación, vuelva a aprovisionar un nuevo circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="98625-187">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> <span data-ttu-id="98625-188">Deshabilitar complemento premium puede producir un error en la operación si usa recursos que son mayores que lo que está permitido para el circuito de hello estándar.</span><span class="sxs-lookup"><span data-stu-id="98625-188">Disable premium add-on operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="98625-189">Desaprovisionamiento y eliminación de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="98625-189">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="98625-190">Puede eliminar el circuito de ExpressRoute seleccionando hello **eliminar** icono.</span><span class="sxs-lookup"><span data-stu-id="98625-190">You can delete your ExpressRoute circuit by selecting hello **delete** icon.</span></span> <span data-ttu-id="98625-191">Tenga en cuenta los siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="98625-191">Note hello following:</span></span>

* <span data-ttu-id="98625-192">Debe desvincular todas las redes virtuales de hello circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="98625-192">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="98625-193">Si se produce un error en esta operación, compruebe si las redes virtuales están vinculadas toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="98625-193">If this operation fails, check whether any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="98625-194">Si es el proveedor de servicios del circuito de ExpressRoute de hello estado de aprovisionamiento **Provisioning** o **aprovisionado** debe trabajar con el circuito de Hola de toodeprovision de proveedor de servicio en uno de su lados.</span><span class="sxs-lookup"><span data-stu-id="98625-194">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="98625-195">Se continuará tooreserve recursos y facturar hasta que el proveedor de servicios de hello finaliza desaprovisionamiento circuito de Hola y notifica a nosotros.</span><span class="sxs-lookup"><span data-stu-id="98625-195">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="98625-196">Si el proveedor de servicios de Hola se canceló el aprovisionamiento de circuito de hello (proveedor de servicios de hello estado de aprovisionamiento se establece demasiado**no aprovisionado**), a continuación, puede eliminar el circuito de Hola.</span><span class="sxs-lookup"><span data-stu-id="98625-196">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="98625-197">Se detendrá la facturación para el circuito de Hola</span><span class="sxs-lookup"><span data-stu-id="98625-197">This will stop billing for hello circuit</span></span>

## <a name="next-steps"></a><span data-ttu-id="98625-198">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="98625-198">Next steps</span></span>
<span data-ttu-id="98625-199">Después de crear el circuito, asegúrese de que Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="98625-199">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="98625-200">Crear y modificar el enrutamiento para el circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="98625-200">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-portal-resource-manager.md)
* [<span data-ttu-id="98625-201">Vincular el circuito de ExpressRoute de tooyour de red virtual</span><span class="sxs-lookup"><span data-stu-id="98625-201">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

