---
title: Flujo de trabajo para configurar un circuito ExpressRoute | Microsoft Docs
description: "Esta página le guiará a través de los flujos de trabajo para configurar el circuito ExpressRoute y las configuraciones entre pares"
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 55e0418c-e0bf-44a7-9aa1-720076df9297
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: cba1b2cfee379e7d2b079bcb3089981ef1044d66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a><span data-ttu-id="25b91-103">Flujos de trabajo de ExpressRoute para aprovisionamiento de circuitos y estados de circuitos de ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="25b91-103">ExpressRoute workflows for circuit provisioning and circuit states</span></span>
<span data-ttu-id="25b91-104">Esta página le guiará a través del aprovisionamiento de servicios y de los flujos de trabajo de configuración del enrutamiento a alto nivel.</span><span class="sxs-lookup"><span data-stu-id="25b91-104">This page walks you through the service provisioning and routing configuration workflows at a high level.</span></span>

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

<span data-ttu-id="25b91-105">Tanto la ilustración como los pasos correspondientes siguientes muestran las tareas que se deben realizar para aprovisionar un circuito ExpressRoute de un extremo a otro.</span><span class="sxs-lookup"><span data-stu-id="25b91-105">The following figure and corresponding steps show the tasks you must follow in order to have an ExpressRoute circuit provisioned end-to-end.</span></span> 

1. <span data-ttu-id="25b91-106">Use PowerShell para configurar un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="25b91-106">Use PowerShell to configure an ExpressRoute circuit.</span></span> <span data-ttu-id="25b91-107">Para obtener más información, siga las instrucciones del artículo [Creación y modificación de circuitos de ExpressRoute](expressroute-howto-circuit-classic.md) .</span><span class="sxs-lookup"><span data-stu-id="25b91-107">Follow the instructions in the [Create ExpressRoute circuits](expressroute-howto-circuit-classic.md) article for more details.</span></span>
2. <span data-ttu-id="25b91-108">Solicite conectividad al proveedor de servicios.</span><span class="sxs-lookup"><span data-stu-id="25b91-108">Order connectivity from the service provider.</span></span> <span data-ttu-id="25b91-109">Este proceso varía.</span><span class="sxs-lookup"><span data-stu-id="25b91-109">This process varies.</span></span> <span data-ttu-id="25b91-110">Para obtener más información sobre cómo solicitar conectividad, póngase en contacto con su proveedor de conectividad.</span><span class="sxs-lookup"><span data-stu-id="25b91-110">Contact your connectivity provider for more details about how to order connectivity.</span></span>
3. <span data-ttu-id="25b91-111">Asegúrese de que el circuito se ha aprovisionado correctamente, para lo que debe comprobar el estado de aprovisionamiento del circuito ExpressRoute a través de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="25b91-111">Ensure that the circuit has been provisioned successfully by verifying the ExpressRoute circuit provisioning state through PowerShell.</span></span> 
4. <span data-ttu-id="25b91-112">Configure los dominios de enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="25b91-112">Configure routing domains.</span></span> <span data-ttu-id="25b91-113">Si el proveedor de conectividad administra el nivel 3, configurará el enrutamiento del circuito.</span><span class="sxs-lookup"><span data-stu-id="25b91-113">If your connectivity provider manages Layer 3 for you, they will configure routing for your circuit.</span></span> <span data-ttu-id="25b91-114">Si el proveedor de conectividad solo ofrece servicios de nivel 2, debe configurar el enrutamiento según las instrucciones que se describen en las páginas de [requisitos de enrutamiento](expressroute-routing.md) y [configuración de enrutamiento](expressroute-howto-routing-classic.md).</span><span class="sxs-lookup"><span data-stu-id="25b91-114">If your connectivity provider only offers Layer 2 services, you must configure routing per guidelines described in the [routing requirements](expressroute-routing.md) and [routing configuration](expressroute-howto-routing-classic.md) pages.</span></span>
   
   * <span data-ttu-id="25b91-115">Habilitar la configuración entre pares privados de Azure: debe habilitar esta configuración entre pares para conectarse a las máquinas virtuales/servicios en la nube implementados en redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="25b91-115">Enable Azure private peering - You must enable this peering to connect to VMs / cloud services deployed within virtual networks.</span></span>
   * <span data-ttu-id="25b91-116">Habilitar la configuración entre pares públicos de Azure: debe habilitar la configuración entre pares públicos de Azure si desea conectarse a los servicios de Azure hospedados en direcciones IP públicas.</span><span class="sxs-lookup"><span data-stu-id="25b91-116">Enable Azure public peering - You must enable Azure public peering if you wish to connect to Azure services hosted on public IP addresses.</span></span> <span data-ttu-id="25b91-117">Se trata de un requisito para acceder a los recursos de Azure si ha elegido habilitar el enrutamiento predeterminado para la configuración entre pares privados de Azure.</span><span class="sxs-lookup"><span data-stu-id="25b91-117">This is a requirement to access Azure resources if you have chosen to enable default routing for Azure private peering.</span></span>
   * <span data-ttu-id="25b91-118">Habilitar el emparejamiento de Microsoft: debe habilitarlo para acceder a Office 365 y Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="25b91-118">Enable Microsoft peering - You must enable this to access Office 365 and Dynamics 365.</span></span> 
     
     > [!IMPORTANT]
     > <span data-ttu-id="25b91-119">Debe asegurarse de que usa un proxy o borde independientes para conectarse a Microsoft distinto del que usa para Internet.</span><span class="sxs-lookup"><span data-stu-id="25b91-119">You must ensure that you use a separate proxy / edge to connect to Microsoft than the one you use for the Internet.</span></span> <span data-ttu-id="25b91-120">Si usa el mismo borde para ExpressRoute e Internet se producirá un enrutamiento asimétrico y causará interrupciones en la conectividad de la red.</span><span class="sxs-lookup"><span data-stu-id="25b91-120">Using the same edge for both ExpressRoute and the Internet will cause asymmetric routing and cause connectivity outages for your network.</span></span>
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. <span data-ttu-id="25b91-121">Vinculación de redes virtuales a circuitos de ExpressRoute: puede vincular redes virtuales a un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="25b91-121">Linking virtual networks to ExpressRoute circuits - You can link virtual networks to your ExpressRoute circuit.</span></span> <span data-ttu-id="25b91-122">Siga las instrucciones [para vincular redes virtuales](expressroute-howto-linkvnet-arm.md) al circuito.</span><span class="sxs-lookup"><span data-stu-id="25b91-122">Follow instructions [to link VNets](expressroute-howto-linkvnet-arm.md) to your circuit.</span></span> <span data-ttu-id="25b91-123">Dichas redes virtuales pueden estar en la misma suscripción de Azure que el circuito ExpressRoute, o bien pueden estar en una suscripción diferente.</span><span class="sxs-lookup"><span data-stu-id="25b91-123">These VNets can either be in the same Azure subscription as the ExpressRoute circuit, or can be in a different subscription.</span></span>

## <a name="expressroute-circuit-provisioning-states"></a><span data-ttu-id="25b91-124">Estados de aprovisionamiento de circuitos de ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="25b91-124">ExpressRoute circuit provisioning states</span></span>
<span data-ttu-id="25b91-125">Cada circuito ExpressRoute tiene dos estados:</span><span class="sxs-lookup"><span data-stu-id="25b91-125">Each ExpressRoute circuit has two states:</span></span>

* <span data-ttu-id="25b91-126">Estado de aprovisionamiento de proveedor de servicio</span><span class="sxs-lookup"><span data-stu-id="25b91-126">Service provider provisioning state</span></span>
* <span data-ttu-id="25b91-127">Estado</span><span class="sxs-lookup"><span data-stu-id="25b91-127">Status</span></span>

<span data-ttu-id="25b91-128">Estado representa el estado de aprovisionamiento de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="25b91-128">Status represents Microsoft's provisioning state.</span></span> <span data-ttu-id="25b91-129">Esta propiedad se establece en Habilitado al crear un circuito Expressroute.</span><span class="sxs-lookup"><span data-stu-id="25b91-129">This property is set to Enabled when you create an Expressroute circuit</span></span>

<span data-ttu-id="25b91-130">El estado de aprovisionamiento del proveedor de conectividad representa el estado del lado del proveedor de conectividad.</span><span class="sxs-lookup"><span data-stu-id="25b91-130">The connectivity provider provisioning state represents the state on the connectivity provider's side.</span></span> <span data-ttu-id="25b91-131">Puede ser *No aprovisionado*, *Aprovisionando* o *Aprovisionado*.</span><span class="sxs-lookup"><span data-stu-id="25b91-131">It can either be *NotProvisioned*, *Provisioning*, or *Provisioned*.</span></span> <span data-ttu-id="25b91-132">El circuito ExpressRoute debe estar en estado Aprovisionado para poder usarlo.</span><span class="sxs-lookup"><span data-stu-id="25b91-132">The ExpressRoute circuit must be in Provisioned state for you to be able to use it.</span></span>

### <a name="possible-states-of-an-expressroute-circuit"></a><span data-ttu-id="25b91-133">Posibles estados de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="25b91-133">Possible states of an ExpressRoute circuit</span></span>
<span data-ttu-id="25b91-134">En esta sección se enumeran los posibles estados de un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="25b91-134">This section lists out the possible states for an ExpressRoute circuit.</span></span>

<span data-ttu-id="25b91-135">**En tiempo de creación**</span><span class="sxs-lookup"><span data-stu-id="25b91-135">**At creation time**</span></span>

<span data-ttu-id="25b91-136">Verá el circuito ExpressRoute en el estado siguiente en cuanto ejecute el cmdlet de PowerShell para crear el circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="25b91-136">You will see the ExpressRoute circuit in the following state as soon as you run the PowerShell cmdlet to create the ExpressRoute circuit.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="25b91-137">**Cuando el proveedor de conectividad está en el proceso de aprovisionamiento del circuito**</span><span class="sxs-lookup"><span data-stu-id="25b91-137">**When connectivity provider is in the process of provisioning the circuit**</span></span>

<span data-ttu-id="25b91-138">Verá el circuito ExpressRoute en el estado siguiente en cuanto pase la clave de servicio al proveedor de conectividad y hayan iniciado el proceso de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="25b91-138">You will see the ExpressRoute circuit in the following state as soon as you pass the service key to the connectivity provider and they have started the provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


<span data-ttu-id="25b91-139">**Cuando el proveedor de conectividad haya completado el proceso de aprovisionamiento**</span><span class="sxs-lookup"><span data-stu-id="25b91-139">**When connectivity provider has completed the provisioning process**</span></span>

<span data-ttu-id="25b91-140">Verá el circuito ExpressRoute en el estado siguiente en cuanto el proveedor de conectividad haya completado el proceso de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="25b91-140">You will see the ExpressRoute circuit in the following state as soon as the connectivity provider has completed the provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

<span data-ttu-id="25b91-141">Aprovisionado y habilitado es el único estado en que puede estar el circuito para poder usarlo.</span><span class="sxs-lookup"><span data-stu-id="25b91-141">Provisioned and Enabled is the only state the circuit can be in for you to be able to use it.</span></span> <span data-ttu-id="25b91-142">Si usa un proveedor de nivel 2, puede configurar el enrutamiento para el circuito solo cuando se encuentre en este estado.</span><span class="sxs-lookup"><span data-stu-id="25b91-142">If you are using a Layer 2 provider, you can configure routing for your circuit only when it is in this state.</span></span>

<span data-ttu-id="25b91-143">**Cuando el proveedor de conectividad está desaprovisionando el circuito**</span><span class="sxs-lookup"><span data-stu-id="25b91-143">**When connectivity provider is deprovisioning the circuit**</span></span>

<span data-ttu-id="25b91-144">Si solicitó al proveedor de servicios que desaprovisione el circuito ExpressRoute, verá el circuito establecido en el estado siguiente una vez que el proveedor de servicios haya completado el proceso de desaprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="25b91-144">If you requested the service provider to deprovision the ExpressRoute circuit, you will see the circuit set to the following state after the service provider has completed the deprovisioning process.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="25b91-145">Si es necesario, puede volver a habilitarlo, o bien ejecutar los cmdlets de PowerShell para eliminar el circuito.</span><span class="sxs-lookup"><span data-stu-id="25b91-145">You can choose to re-enable it if needed, or run PowerShell cmdlets to delete the circuit.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="25b91-146">Si ejecuta el cmdlet de PowerShell para eliminar el circuito cuando el estado de ServiceProviderProvisioningState es Aprovisionamiento o Aprovisionado, se producirá un error en la operación.</span><span class="sxs-lookup"><span data-stu-id="25b91-146">If you run the PowerShell cmdlet to delete the circuit when the ServiceProviderProvisioningState is Provisioning or Provisioned the operation will fail.</span></span> <span data-ttu-id="25b91-147">Colabore con el proveedor de conectividad para desaprovisionar el circuito ExpressRoute primero y, después, eliminar el circuito.</span><span class="sxs-lookup"><span data-stu-id="25b91-147">Please work with your connectivity provider to deprovision the ExpressRoute circuit first and then delete the circuit.</span></span> <span data-ttu-id="25b91-148">Microsoft seguirá facturando el circuito hasta que se ejecute el cmdlet de PowerShell para eliminar el circuito.</span><span class="sxs-lookup"><span data-stu-id="25b91-148">Microsoft will continue to bill the circuit until you run the PowerShell cmdlet to delete the circuit.</span></span>
> 
> 

## <a name="routing-session-configuration-state"></a><span data-ttu-id="25b91-149">Estado de configuración de sesión de enrutamiento</span><span class="sxs-lookup"><span data-stu-id="25b91-149">Routing session configuration state</span></span>
<span data-ttu-id="25b91-150">El estado de aprovisionamiento de BGP permite saber si la sesión BGP se ha habilitado en el borde de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="25b91-150">The BGP provisioning state lets you know if the BGP session has been enabled on the Microsoft edge.</span></span> <span data-ttu-id="25b91-151">El estado debe habilitarse para poder usar la configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="25b91-151">The state must be enabled for you to be able to use the peering.</span></span>

<span data-ttu-id="25b91-152">Es importante comprobar el estado de sesión de BGP, especialmente para la configuración entre pares de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="25b91-152">It is important to check the BGP session state especially for Microsoft peering.</span></span> <span data-ttu-id="25b91-153">Además del estado de aprovisionamiento de BGP, hay otro estado denominado *estado de prefijos públicos anunciados*.</span><span class="sxs-lookup"><span data-stu-id="25b91-153">In addition to the BGP provisioning state, there is another state called *advertised public prefixes state*.</span></span> <span data-ttu-id="25b91-154">El estado de los prefijos públicos anunciados debe estar en estado *configurado* , tanto para que la sesión BGP esté activa como para que el enrutamiento funcione de un extremo a otro.</span><span class="sxs-lookup"><span data-stu-id="25b91-154">The advertised public prefixes state must be in *configured* state, both for the BGP session to be up and for your routing to work end-to-end.</span></span> 

<span data-ttu-id="25b91-155">Si el estado de los prefijos públicos anunciados se establece en el estado de *validación necesaria* , la sesión BGP no se habilita, ya que los prefijos anunciados no coincidían con el número AS en ninguno de los registros de enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="25b91-155">If the advertised public prefix state is set to a *validation needed* state, the BGP session is not enabled, as the advertised prefixes did not match the AS number in any of the routing registries.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="25b91-156">Si el estado de los prefijos públicos anunciados es *validación manual* , debe abrir una incidencia de soporte técnico en el [servicio de soporte técnico de Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) y aportar una evidencia de que posee la dirección IP anunciada, junto con el número del sistema autónomo asociado.</span><span class="sxs-lookup"><span data-stu-id="25b91-156">If the advertised public prefixes state is in *manual validation* state, you must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and provide evidence that you own the IP addresses advertised along with the associated Autonomous System number.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="25b91-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="25b91-157">Next steps</span></span>
* <span data-ttu-id="25b91-158">Configure su conexión ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="25b91-158">Configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="25b91-159">Creación de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="25b91-159">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-arm.md)
  * [<span data-ttu-id="25b91-160">Configuración del enrutamiento</span><span class="sxs-lookup"><span data-stu-id="25b91-160">Configure routing</span></span>](expressroute-howto-routing-arm.md)
  * [<span data-ttu-id="25b91-161">Vinculación de redes virtuales a circuitos ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="25b91-161">Link a VNet to an ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

