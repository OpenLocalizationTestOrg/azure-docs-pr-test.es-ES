---
title: "Creación y modificación de un circuito ExpressRoute mediante Azure Portal | Microsoft Docs"
description: "Este artículo describe cómo crear, aprovisionar, comprobar, actualizar, eliminar y desaprovisionar un circuito ExpressRoute."
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
ms.openlocfilehash: e3721cd3c031622788f553e71a6555b844f3f7dc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-an-expressroute-circuit"></a><span data-ttu-id="23fc7-103">Creación y modificación de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="23fc7-103">Create and modify an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="23fc7-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="23fc7-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="23fc7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="23fc7-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="23fc7-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="23fc7-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="23fc7-107">Vídeo: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="23fc7-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="23fc7-108">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="23fc7-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="23fc7-109">En este artículo se describe cómo crear un circuito Azure ExpressRoute con el Portal de Azure y el modelo de implementación de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="23fc7-109">This article describes how to create an Azure ExpressRoute circuit by using the Azure portal and the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="23fc7-110">Los siguientes pasos también le mostrarán cómo comprobar el estado del circuito, actualizarlo, o eliminarlo y desaprovisionarlo.</span><span class="sxs-lookup"><span data-stu-id="23fc7-110">The following steps also show you how to check the status of the circuit, update it, or delete and deprovision it.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="23fc7-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="23fc7-111">Before you begin</span></span>
* <span data-ttu-id="23fc7-112">Revise los [Requisitos previos y lista de comprobación de ExpressRoute](expressroute-prerequisites.md) y los [Flujos de trabajo de ExpressRoute para aprovisionamiento de circuitos y estados de circuitos de ExpressRoute](expressroute-workflows.md) antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="23fc7-112">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="23fc7-113">Compruebe que tiene acceso al [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="23fc7-113">Ensure that you have access to the [Azure portal](https://portal.azure.com).</span></span>
* <span data-ttu-id="23fc7-114">Asegúrese de que tiene permisos para crear recursos de red.</span><span class="sxs-lookup"><span data-stu-id="23fc7-114">Ensure that you have permissions to create new networking resources.</span></span> <span data-ttu-id="23fc7-115">Si no tiene los permisos adecuados, póngase en contacto con el administrador de cuenta.</span><span class="sxs-lookup"><span data-stu-id="23fc7-115">Contact your account administrator if you do not have the right permissions.</span></span>
* <span data-ttu-id="23fc7-116">Puede [ver un vídeo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) antes de comenzar para entender mejor los pasos.</span><span class="sxs-lookup"><span data-stu-id="23fc7-116">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) before beginning in order to better understand the steps.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="23fc7-117">Creación y aprovisionamiento de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="23fc7-117">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-to-the-azure-portal"></a><span data-ttu-id="23fc7-118">1. Inicie sesión en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="23fc7-118">1. Sign in to the Azure portal</span></span>
<span data-ttu-id="23fc7-119">Desde un explorador, navegue al [Portal de Azure](http://portal.azure.com) e inicie sesión con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="23fc7-119">From a browser, navigate to the [Azure portal](http://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="2-create-a-new-expressroute-circuit"></a><span data-ttu-id="23fc7-120">2. Creación de un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="23fc7-120">2. Create a new ExpressRoute circuit</span></span>
> [!IMPORTANT]
> <span data-ttu-id="23fc7-121">El circuito ExpressRoute se facturará a partir del momento en que se emita una clave de servicio.</span><span class="sxs-lookup"><span data-stu-id="23fc7-121">Your ExpressRoute circuit will be billed from the moment a service key is issued.</span></span> <span data-ttu-id="23fc7-122">Asegúrese de realizar esta operación cuando el proveedor de conectividad esté listo para aprovisionar el circuito.</span><span class="sxs-lookup"><span data-stu-id="23fc7-122">Ensure that you perform this operation when the connectivity provider is ready to provision the circuit.</span></span>
> 
> 

1. <span data-ttu-id="23fc7-123">Puede crear un circuito ExpressRoute seleccionando la opción de creación de un recurso.</span><span class="sxs-lookup"><span data-stu-id="23fc7-123">You can create an ExpressRoute circuit by selecting the option to create a new resource.</span></span> <span data-ttu-id="23fc7-124">Haga clic en **Nuevo** > **Redes** > **ExpressRoute**, tal y como se muestra en la imagen siguiente:</span><span class="sxs-lookup"><span data-stu-id="23fc7-124">Click **New** > **Networking** > **ExpressRoute**, as shown in the following image:</span></span>
   
    ![Creación de un circuito ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. <span data-ttu-id="23fc7-126">Tras hacer clic en **ExpressRoute**, verá la hoja **Create ExpressRoute circuit** (Crear circuito ExpressRoute).</span><span class="sxs-lookup"><span data-stu-id="23fc7-126">After you click **ExpressRoute**, you'll see the **Create ExpressRoute circuit** blade.</span></span> <span data-ttu-id="23fc7-127">Al rellenar los valores en esta hoja, asegúrese de especificar el nivel correcto de SKU y medición de datos.</span><span class="sxs-lookup"><span data-stu-id="23fc7-127">When you're filling in the values on this blade, make sure that you specify the correct SKU tier and data metering.</span></span>
   
   * <span data-ttu-id="23fc7-128">**Nivel** determina si está habilitado un complemento estándar o premium de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="23fc7-128">**Tier** determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="23fc7-129">Puede especificar **Estándar** para obtener la SKU estándar o **Premium** si quiere el complemento Premium.</span><span class="sxs-lookup"><span data-stu-id="23fc7-129">You can specify **Standard** to get the standard SKU or **Premium** for the premium add-on.</span></span>
   * <span data-ttu-id="23fc7-130">**Medición de datos** determina el tipo de facturación.</span><span class="sxs-lookup"><span data-stu-id="23fc7-130">**Data metering** determines the billing type.</span></span> <span data-ttu-id="23fc7-131">Puede especificar **Metered** (Limitado) para un plan de datos limitado y **Unlimited** (Ilimitado) para un plan de datos ilimitado.</span><span class="sxs-lookup"><span data-stu-id="23fc7-131">You can specify **Metered** for a metered data plan and **Unlimited** for an unlimited data plan.</span></span> <span data-ttu-id="23fc7-132">Tenga en cuenta que puede cambiar el tipo de facturación de **Metered** (Limitado) a **Unlimited** (Ilimitado), pero no de **Unlimited** (Ilimitado) a **Metered** (Limitado).</span><span class="sxs-lookup"><span data-stu-id="23fc7-132">Note that you can change the billing type from **Metered** to **Unlimited**, but you can't change the type from **Unlimited** to **Metered**.</span></span>
     
     ![Configuración del nivel SKU y medición de datos](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> <span data-ttu-id="23fc7-134">Tenga en cuenta que la ubicación de emparejamiento indica la [ubicación física](expressroute-locations.md) de emparejamiento con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="23fc7-134">Please be aware that the Peering Location indicates the [physical location](expressroute-locations.md) where you are peering with Microsoft.</span></span> <span data-ttu-id="23fc7-135">**No** está vinculada a la propiedad Location, que hace referencia a la ubicación geográfica donde se encuentra el proveedor de recursos de red de Azure.</span><span class="sxs-lookup"><span data-stu-id="23fc7-135">This is **not** linked to "Location" property, which refers to the geography where the Azure Network Resource Provider is located.</span></span> <span data-ttu-id="23fc7-136">Aunque no están relacionadas, se recomienda elegir un proveedor de recursos de red geográficamente cerca de la ubicación de emparejamiento del circuito.</span><span class="sxs-lookup"><span data-stu-id="23fc7-136">While they are not related, it is a good practice to choose a Network Resource Provider geographically close to the Peering Location of the circuit.</span></span> 
> 
> 

### <a name="3-view-the-circuits-and-properties"></a><span data-ttu-id="23fc7-137">3. Visualización de circuitos y propiedades</span><span class="sxs-lookup"><span data-stu-id="23fc7-137">3. View the circuits and properties</span></span>
<span data-ttu-id="23fc7-138">**Visualización de todos los circuitos**</span><span class="sxs-lookup"><span data-stu-id="23fc7-138">**View all the circuits**</span></span>

<span data-ttu-id="23fc7-139">Puede ver todos los circuitos creados seleccionando **Todos los recursos** en el menú de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="23fc7-139">You can view all the circuits that you created by selecting **All resources** on the left-side menu.</span></span>

![Visualización de circuitos](./media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

<span data-ttu-id="23fc7-141">**Visualización de las propiedades**</span><span class="sxs-lookup"><span data-stu-id="23fc7-141">**View the properties**</span></span>

    You can view the properties of the circuit by selecting it. On this blade, note the service key for the circuit. You must copy the circuit key for your circuit and pass it down to the service provider to complete the provisioning process. The circuit key is specific to your circuit.

![Ver propiedades](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-the-service-key-to-your-connectivity-provider-for-provisioning"></a><span data-ttu-id="23fc7-143">4. Envío de la clave de servicio al proveedor de conectividad para el aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="23fc7-143">4. Send the service key to your connectivity provider for provisioning</span></span>
<span data-ttu-id="23fc7-144">En esta hoja, **Estado de proveedor** da información sobre el estado actual del aprovisionamiento en el lado del proveedor de servicios.</span><span class="sxs-lookup"><span data-stu-id="23fc7-144">On this blade, **Provider status** provides information on the current state of provisioning on the service-provider side.</span></span> <span data-ttu-id="23fc7-145">**Estado de circuito** proporciona el estado relativo al lado de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="23fc7-145">**Circuit status** provides the state on the Microsoft side.</span></span> <span data-ttu-id="23fc7-146">Para más información sobre los estados de aprovisionamiento del circuito, consulte el artículo [Flujos de trabajo de ExpressRoute para aprovisionamiento de circuitos y estados de circuitos de ExpressRoute](expressroute-workflows.md#expressroute-circuit-provisioning-states) .</span><span class="sxs-lookup"><span data-stu-id="23fc7-146">For more information about circuit provisioning states, see the [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="23fc7-147">Cuando se crea un nuevo circuito ExpressRoute, dicho circuito estará en el siguiente estado:</span><span class="sxs-lookup"><span data-stu-id="23fc7-147">When you create a new ExpressRoute circuit, the circuit will be in the following state:</span></span>

<span data-ttu-id="23fc7-148">Estado de proveedor: No aprovisionado</span><span class="sxs-lookup"><span data-stu-id="23fc7-148">Provider status: Not provisioned</span></span><BR>
<span data-ttu-id="23fc7-149">Estado de circuito: Habilitado</span><span class="sxs-lookup"><span data-stu-id="23fc7-149">Circuit status: Enabled</span></span>

![Inicio del proceso de aprovisionamiento](./media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

<span data-ttu-id="23fc7-151">El circuito cambiará al estado siguiente cuando el proveedor de conectividad se encuentre en el proceso de habilitarlo:</span><span class="sxs-lookup"><span data-stu-id="23fc7-151">The circuit will change to the following state when the connectivity provider is in the process of enabling it for you:</span></span>

<span data-ttu-id="23fc7-152">Estado de proveedor: Aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="23fc7-152">Provider status: Provisioning</span></span><BR>
<span data-ttu-id="23fc7-153">Estado de circuito: Habilitado</span><span class="sxs-lookup"><span data-stu-id="23fc7-153">Circuit status: Enabled</span></span>

<span data-ttu-id="23fc7-154">Para poder usar un circuito ExpressRoute, dicho circuito tiene que estar en el siguiente estado.</span><span class="sxs-lookup"><span data-stu-id="23fc7-154">For you to be able to use an ExpressRoute circuit, it must be in the following state:</span></span>

<span data-ttu-id="23fc7-155">Estado de proveedor: Aprovisionado</span><span class="sxs-lookup"><span data-stu-id="23fc7-155">Provider status: Provisioned</span></span><BR>
<span data-ttu-id="23fc7-156">Estado de circuito: Habilitado</span><span class="sxs-lookup"><span data-stu-id="23fc7-156">Circuit status: Enabled</span></span>

### <a name="5-periodically-check-the-status-and-the-state-of-the-circuit-key"></a><span data-ttu-id="23fc7-157">5. Comprobación periódica del estado y la condición de la clave del circuito</span><span class="sxs-lookup"><span data-stu-id="23fc7-157">5. Periodically check the status and the state of the circuit key</span></span>
<span data-ttu-id="23fc7-158">Puede ver las propiedades del circuito que le interese seleccionándolo.</span><span class="sxs-lookup"><span data-stu-id="23fc7-158">You can view the properties of the circuit that you're interested in by selecting it.</span></span> <span data-ttu-id="23fc7-159">Compruebe el **Estado de proveedor** y asegúrese de que se ha pasado a **Aprovisionado** antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="23fc7-159">Check the **Provider status** and ensure that it has moved to **Provisioned** before you continue.</span></span>

![Estado del circuito y proveedor](./media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a><span data-ttu-id="23fc7-161">6. Creación de la configuración de enrutamiento</span><span class="sxs-lookup"><span data-stu-id="23fc7-161">6. Create your routing configuration</span></span>
<span data-ttu-id="23fc7-162">Consulte el artículo [Creación y modificación del enrutamiento de un circuito ExpressRoute mediante PowerShell](expressroute-howto-routing-portal-resource-manager.md) para ver las instrucciones paso a paso.</span><span class="sxs-lookup"><span data-stu-id="23fc7-162">For step-by-step instructions, refer to the [ExpressRoute circuit routing configuration](expressroute-howto-routing-portal-resource-manager.md) article to create and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="23fc7-163">Estas instrucciones se aplican solo a los circuitos creados con proveedores de servicios que ofrecen servicios de conectividad de nivel 2.</span><span class="sxs-lookup"><span data-stu-id="23fc7-163">These instructions only apply to circuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="23fc7-164">Si usa un proveedor de servicios que ofrece servicios administrados de nivel 3 (normalmente VPN IP, como MPLS), el mismo proveedor de conectividad configurará y administrará el enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="23fc7-164">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="7-link-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="23fc7-165">7. Vinculación de una red virtual a un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="23fc7-165">7. Link a virtual network to an ExpressRoute circuit</span></span>
<span data-ttu-id="23fc7-166">A continuación, vincule una red virtual a su circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="23fc7-166">Next, link a virtual network to your ExpressRoute circuit.</span></span> <span data-ttu-id="23fc7-167">Consulte el artículo [Vinculación de redes virtuales a circuitos ExpressRoute](expressroute-howto-linkvnet-arm.md) al trabajar con el modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="23fc7-167">Use the [Linking virtual networks to ExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with the Resource Manager deployment model.</span></span>

## <a name="getting-the-status-of-an-expressroute-circuit"></a><span data-ttu-id="23fc7-168">Obtención del estado de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="23fc7-168">Getting the status of an ExpressRoute circuit</span></span>
<span data-ttu-id="23fc7-169">Puede ver el estado de un circuito seleccionándolo.</span><span class="sxs-lookup"><span data-stu-id="23fc7-169">You can view the status of a circuit by selecting it.</span></span> 

![Estado de un circuito ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="23fc7-171">Modificación de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="23fc7-171">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="23fc7-172">Puede modificar determinadas propiedades de un circuito ExpressRoute sin afectar a la conectividad.</span><span class="sxs-lookup"><span data-stu-id="23fc7-172">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="23fc7-173">Puede hacer lo siguiente sin experimentar tiempo de inactividad:</span><span class="sxs-lookup"><span data-stu-id="23fc7-173">You can do the following with no downtime:</span></span>

* <span data-ttu-id="23fc7-174">Habilitar o deshabilitar el complemento ExpressRoute Premium en su circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="23fc7-174">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="23fc7-175">Aumente el ancho de banda del circuito ExpressRoute, siempre que haya capacidad disponible en el puerto.</span><span class="sxs-lookup"><span data-stu-id="23fc7-175">Increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span></span> <span data-ttu-id="23fc7-176">Tenga en cuenta que no se admite la degradación del ancho de banda de un circuito.</span><span class="sxs-lookup"><span data-stu-id="23fc7-176">Note that downgrading the bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="23fc7-177">Cambio del plan de medición de datos limitados a datos ilimitados.</span><span class="sxs-lookup"><span data-stu-id="23fc7-177">Change the metering plan from Metered Data to Unlimited Data.</span></span> <span data-ttu-id="23fc7-178">Tenga en cuenta que no es posible cambiar el plan de medición de datos ilimitados a datos limitados.</span><span class="sxs-lookup"><span data-stu-id="23fc7-178">Note that changing the metering plan from Unlimited Data to Metered Data is not supported.</span></span>
* <span data-ttu-id="23fc7-179">Puede habilitar y deshabilitar *Allow Classic Operations*(Permitir operaciones clásicas).</span><span class="sxs-lookup"><span data-stu-id="23fc7-179">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="23fc7-180">Consulte la página [P+F de ExpressRoute](expressroute-faqs.md)para más información sobre los límites y las limitaciones.</span><span class="sxs-lookup"><span data-stu-id="23fc7-180">For more information on limits and limitations, refer to the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

<span data-ttu-id="23fc7-181">Para modificar un circuito de ExpressRoute, haga clic en el **Configuración** tal como se muestra en la ilustración siguiente.</span><span class="sxs-lookup"><span data-stu-id="23fc7-181">To modify an ExpressRoute circuit, click on the **Configuration** as shown in the figure below.</span></span>

![Modificación del circuito](./media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

<span data-ttu-id="23fc7-183">Puede modificar el ancho de banda,la SKU, el modelo de facturación y permitir operaciones clásicas en la hoja de configuración.</span><span class="sxs-lookup"><span data-stu-id="23fc7-183">You can modify the bandwidth, SKU, billing model and allow classic operations within the configuration blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="23fc7-184">Si el puerto existente no tiene la capacidad adecuada, tendrá que volver a crear el circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="23fc7-184">You may have to recreate the ExpressRoute circuit if there is inadequate capacity on the existing port.</span></span> <span data-ttu-id="23fc7-185">El circuito no se puede actualizar si no hay más capacidad disponible en la ubicación.</span><span class="sxs-lookup"><span data-stu-id="23fc7-185">You cannot upgrade the circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="23fc7-186">No podrá reducir el ancho de banda de un circuito ExpressRoute sin interrupciones.</span><span class="sxs-lookup"><span data-stu-id="23fc7-186">You cannot reduce the bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="23fc7-187">Para degradar un ancho de banda, es necesario desaprovisionar el circuito ExpressRoute y luego volver a aprovisionar un nuevo circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="23fc7-187">Downgrading bandwidth requires you to deprovision the ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> <span data-ttu-id="23fc7-188">La operación de deshabilitación del complemento premium puede producir un error si usa recursos que son más grandes de lo que está permitido para el circuito estándar.</span><span class="sxs-lookup"><span data-stu-id="23fc7-188">Disable premium add-on operation can fail if you're using resources that are greater than what is permitted for the standard circuit.</span></span>
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="23fc7-189">Desaprovisionamiento y eliminación de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="23fc7-189">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="23fc7-190">Puede eliminar el circuito ExpressRoute seleccionando el icono **Eliminar** .</span><span class="sxs-lookup"><span data-stu-id="23fc7-190">You can delete your ExpressRoute circuit by selecting the **delete** icon.</span></span> <span data-ttu-id="23fc7-191">Tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="23fc7-191">Note the following:</span></span>

* <span data-ttu-id="23fc7-192">Tiene que desvincular todas las redes virtuales del circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="23fc7-192">You must unlink all virtual networks from the ExpressRoute circuit.</span></span> <span data-ttu-id="23fc7-193">Si se produce un error en esta operación, compruebe si hay alguna red virtual vinculada al circuito.</span><span class="sxs-lookup"><span data-stu-id="23fc7-193">If this operation fails, check whether any virtual networks are linked to the circuit.</span></span>
* <span data-ttu-id="23fc7-194">Si el estado de aprovisionamiento del proveedor de servicios del circuito ExpressRoute es **Aprovisionando** o **Aprovisionado**, debe colaborar con su proveedor de servicios para que desaprovisionen el circuito.</span><span class="sxs-lookup"><span data-stu-id="23fc7-194">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider to deprovision the circuit on their side.</span></span> <span data-ttu-id="23fc7-195">Se le continuará reservando recursos y facturándole por ello hasta que el proveedor de servicios complete el desaprovisionamiento del circuito y nos lo notifique.</span><span class="sxs-lookup"><span data-stu-id="23fc7-195">We will continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span></span>
* <span data-ttu-id="23fc7-196">Si el proveedor de servicios ha desaprovisionado el circuito (el estado de aprovisionamiento del proveedor de servicios está establecido en **No aprovisionado**), puede eliminar el circuito.</span><span class="sxs-lookup"><span data-stu-id="23fc7-196">If the service provider has deprovisioned the circuit (the service provider provisioning state is set to **Not provisioned**) you can then delete the circuit.</span></span> <span data-ttu-id="23fc7-197">Esto detendrá la facturación del circuito.</span><span class="sxs-lookup"><span data-stu-id="23fc7-197">This will stop billing for the circuit</span></span>

## <a name="next-steps"></a><span data-ttu-id="23fc7-198">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="23fc7-198">Next steps</span></span>
<span data-ttu-id="23fc7-199">Después de crear el circuito, asegúrese de hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="23fc7-199">After you create your circuit, make sure that you do the following:</span></span>

* [<span data-ttu-id="23fc7-200">Crear y modificar el enrutamiento para el circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="23fc7-200">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-portal-resource-manager.md)
* [<span data-ttu-id="23fc7-201">Vincular la red virtual a su circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="23fc7-201">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

