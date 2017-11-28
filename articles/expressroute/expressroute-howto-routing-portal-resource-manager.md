---
title: "Configuración del enrutamiento (emparejamiento) de un circuito ExpressRoute: Resource Manager (Azure) | Microsoft Docs"
description: "Este artículo le guiará por los pasos necesarios para crear y aprovisionar las configuraciones entre pares privados, públicos y de Microsoft de un circuito ExpressRoute. Este artículo también muestra cómo comprobar el estado, actualizar, o eliminar configuraciones entre pares en el circuito."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c2a7ed2-ae5c-4e49-81f6-77cf9f2b2ac9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: 55ccadfea55b8098ee58dcaef942f6ba54093665
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a><span data-ttu-id="d4124-104">Creación y modificación del emparejamiento de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="d4124-104">Create and modify peering for an ExpressRoute circuit</span></span>

<span data-ttu-id="d4124-105">Este artículo le ayuda a crear y administrar la configuración de enrutamiento de un circuito ExpressRoute en el modelo de implementación de Resource Manager mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d4124-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in the Resource Manager deployment model using the Azure portal.</span></span> <span data-ttu-id="d4124-106">También puede ver cómo comprobar el estado de los emparejamientos de un circuito ExpressRoute, así como el modo de actualizarlos o eliminarlos y desaprovisionarlos.</span><span class="sxs-lookup"><span data-stu-id="d4124-106">You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="d4124-107">Si quiere usar un método diferente para trabajar con el circuito, seleccione un artículo de la lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="d4124-107">If you want to use a different method to work with your circuit, select an article from the following list:</span></span>


## <a name="configuration-prerequisites"></a><span data-ttu-id="d4124-108">Requisitos previos de configuración</span><span class="sxs-lookup"><span data-stu-id="d4124-108">Configuration prerequisites</span></span>

* <span data-ttu-id="d4124-109">Antes de comenzar la configuración, asegúrese de que ha revisado la página de [requisitos previos](expressroute-prerequisites.md), la página de [requisitos de enrutamiento](expressroute-routing.md) y la página de [flujos de trabajo](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="d4124-109">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="d4124-110">Tiene que tener un circuito ExpressRoute activo.</span><span class="sxs-lookup"><span data-stu-id="d4124-110">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="d4124-111">Antes de continuar, siga las instrucciones para [crear un circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) y para que el proveedor de conectividad habilite el circuito.</span><span class="sxs-lookup"><span data-stu-id="d4124-111">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="d4124-112">El circuito ExpressRoute debe estar en un estado habilitado y aprovisionado para poder ejecutar los cmdlets de las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="d4124-112">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets in the next sections.</span></span>
* <span data-ttu-id="d4124-113">Si tiene pensado usar una clave compartida o un hash MD5, asegúrese de utilizarlos en ambos lados del túnel y limite el número de caracteres a 25 como máximo.</span><span class="sxs-lookup"><span data-stu-id="d4124-113">If you plan to use a shared key/MD5 hash, be sure to use this on both sides of the tunnel and limit the number of characters to a maximum of 25.</span></span>

<span data-ttu-id="d4124-114">Estas instrucciones se aplican solo a los circuitos creados con proveedores de servicios que ofrecen servicios de conectividad de capa 2.</span><span class="sxs-lookup"><span data-stu-id="d4124-114">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="d4124-115">Si usa un proveedor de servicios que ofrece servicios administrados de nivel 3 (normalmente VPN IP, como MPLS), el mismo proveedor de conectividad configura y administra el enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="d4124-115">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d4124-116">Actualmente no anunciamos los emparejamientos configurados por proveedores de servicios a través del Portal de administración de servicios.</span><span class="sxs-lookup"><span data-stu-id="d4124-116">We currently do not advertise peerings configured by service providers through the service management portal.</span></span> <span data-ttu-id="d4124-117">Se está trabajando para habilitar esta funcionalidad pronto.</span><span class="sxs-lookup"><span data-stu-id="d4124-117">We are working on enabling this capability soon.</span></span> <span data-ttu-id="d4124-118">Antes de configurar los emparejamientos BGP, realice las comprobaciones pertinentes con su proveedor de servicios.</span><span class="sxs-lookup"><span data-stu-id="d4124-118">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="d4124-119">Puede configurar una, dos o las tres configuraciones entre pares (Azure privado, Azure público y Microsoft) para un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d4124-119">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="d4124-120">Puede establecer las configuraciones entre pares en cualquier orden.</span><span class="sxs-lookup"><span data-stu-id="d4124-120">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="d4124-121">Pero tiene que asegurarse de que completa cada configuración entre pares de una en una.</span><span class="sxs-lookup"><span data-stu-id="d4124-121">However, you must make sure that you complete the configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="d4124-122">Configuración entre pares privados de Azure</span><span class="sxs-lookup"><span data-stu-id="d4124-122">Azure private peering</span></span>

<span data-ttu-id="d4124-123">Esta sección le ayuda a crear, obtener, actualizar y eliminar la configuración de emparejamiento privado de Azure para un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d4124-123">This section helps you create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="d4124-124">Creación de un emparejamiento privado de Azure</span><span class="sxs-lookup"><span data-stu-id="d4124-124">To create Azure private peering</span></span>

1. <span data-ttu-id="d4124-125">Configure el circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d4124-125">Configure the ExpressRoute circuit.</span></span> <span data-ttu-id="d4124-126">Antes de continuar, asegúrese de que el proveedor de conectividad ha aprovisionado el circuito por completo.</span><span class="sxs-lookup"><span data-stu-id="d4124-126">Ensure that the circuit is fully provisioned by the connectivity provider before continuing.</span></span>

  ![list](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="d4124-128">Establecimiento de la configuración entre pares privados de Azure para el circuito.</span><span class="sxs-lookup"><span data-stu-id="d4124-128">Configure Azure private peering for the circuit.</span></span> <span data-ttu-id="d4124-129">Asegúrese de que tiene los elementos siguientes antes de continuar con los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="d4124-129">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="d4124-130">Una subred /30 para el vínculo principal.</span><span class="sxs-lookup"><span data-stu-id="d4124-130">A /30 subnet for the primary link.</span></span> <span data-ttu-id="d4124-131">La subred no debe ser parte de ningún espacio de direcciones reservado para redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="d4124-131">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="d4124-132">Una subred /30 para el vínculo secundario.</span><span class="sxs-lookup"><span data-stu-id="d4124-132">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="d4124-133">La subred no debe ser parte de ningún espacio de direcciones reservado para redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="d4124-133">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="d4124-134">Un identificador VLAN válido para establecer esta configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="d4124-134">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="d4124-135">Asegúrese de que ninguna otra configuración entre pares en el circuito usa el mismo identificador de VLAN.</span><span class="sxs-lookup"><span data-stu-id="d4124-135">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="d4124-136">Número de sistema autónomo (AS) para la configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="d4124-136">AS number for peering.</span></span> <span data-ttu-id="d4124-137">Puede usar 2 bytes o 4 bytes como números AS.</span><span class="sxs-lookup"><span data-stu-id="d4124-137">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="d4124-138">Puede usar un número AS privado para esta configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="d4124-138">You can use a private AS number for this peering.</span></span> <span data-ttu-id="d4124-139">Asegúrese de que no usa 65515.</span><span class="sxs-lookup"><span data-stu-id="d4124-139">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="d4124-140">**Opcional:** un hash MD5 si elige usar uno.</span><span class="sxs-lookup"><span data-stu-id="d4124-140">**Optional -** An MD5 hash if you choose to use one.</span></span>
3. <span data-ttu-id="d4124-141">Seleccione la fila de emparejamiento privado de Azure, como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d4124-141">Select the Azure Private peering row, as shown in the following example:</span></span>

  ![privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. <span data-ttu-id="d4124-143">Configure el emparejamiento privado.</span><span class="sxs-lookup"><span data-stu-id="d4124-143">Configure private peering.</span></span> <span data-ttu-id="d4124-144">La siguiente imagen muestra un ejemplo de configuración:</span><span class="sxs-lookup"><span data-stu-id="d4124-144">The following image shows a configuration example:</span></span>

  ![configurar el emparejamiento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. <span data-ttu-id="d4124-146">Guarde la configuración una vez que haya especificado todos los parámetros.</span><span class="sxs-lookup"><span data-stu-id="d4124-146">Save the configuration once you have specified all parameters.</span></span> <span data-ttu-id="d4124-147">Una vez que la configuración se haya aceptado correctamente, verá algo similar al siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d4124-147">After the configuration has been accepted successfully, you see something similar to the following example:</span></span>

  ![guardar emparejamiento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="d4124-149">Visualización de los detalles del emparejamiento privado</span><span class="sxs-lookup"><span data-stu-id="d4124-149">To view Azure private peering details</span></span>

<span data-ttu-id="d4124-150">Para ver las propiedades del emparejamiento privado de Azure seleccione el emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="d4124-150">You can view the properties of Azure private peering by selecting the peering.</span></span>

![ver emparejamiento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="d4124-152">Actualización del establecimiento de configuración del emparejamiento privado de Azure</span><span class="sxs-lookup"><span data-stu-id="d4124-152">To update Azure private peering configuration</span></span>

<span data-ttu-id="d4124-153">Puede seleccionar la fila del emparejamiento y modificar las propiedades del mismo.</span><span class="sxs-lookup"><span data-stu-id="d4124-153">You can select the row for peering and modify the peering properties.</span></span>

![actualizar emparejamiento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="d4124-155">Eliminación del emparejamiento privado de Azure</span><span class="sxs-lookup"><span data-stu-id="d4124-155">To delete Azure private peering</span></span>

<span data-ttu-id="d4124-156">Para quitar la configuración de emparejamiento, seleccione el icono de eliminación, como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="d4124-156">You can remove your peering configuration by selecting the delete icon, as shown in the following image:</span></span>

![eliminar emparejamiento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a><span data-ttu-id="d4124-158">Configuración entre pares públicos de Azure</span><span class="sxs-lookup"><span data-stu-id="d4124-158">Azure public peering</span></span>

<span data-ttu-id="d4124-159">Esta sección le ayuda a crear, obtener, actualizar y eliminar la configuración de emparejamiento público de Azure para un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d4124-159">This section helps you create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="d4124-160">Creación de un emparejamiento público de Azure</span><span class="sxs-lookup"><span data-stu-id="d4124-160">To create Azure public peering</span></span>

1. <span data-ttu-id="d4124-161">Configure un circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d4124-161">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="d4124-162">Antes de continuar, asegúrese de que el proveedor de que el proveedor de conectividad ha aprovisionado el circuito por completo.</span><span class="sxs-lookup"><span data-stu-id="d4124-162">Ensure that the circuit is fully provisioned by the connectivity provider before continuing further.</span></span>

  ![mostrar emparejamiento público](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="d4124-164">Establezca la configuración del emparejamiento publico de Azure para el circuito.</span><span class="sxs-lookup"><span data-stu-id="d4124-164">Configure Azure public peering for the circuit.</span></span> <span data-ttu-id="d4124-165">Asegúrese de que tiene los elementos siguientes antes de continuar con los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="d4124-165">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="d4124-166">Una subred /30 para el vínculo principal.</span><span class="sxs-lookup"><span data-stu-id="d4124-166">A /30 subnet for the primary link.</span></span> <span data-ttu-id="d4124-167">Tiene que ser un prefijo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="d4124-167">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="d4124-168">Una subred /30 para el vínculo secundario.</span><span class="sxs-lookup"><span data-stu-id="d4124-168">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="d4124-169">Tiene que ser un prefijo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="d4124-169">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="d4124-170">Un identificador VLAN válido para establecer esta configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="d4124-170">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="d4124-171">Asegúrese de que ninguna otra configuración entre pares en el circuito usa el mismo identificador de VLAN.</span><span class="sxs-lookup"><span data-stu-id="d4124-171">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="d4124-172">Número de sistema autónomo (AS) para la configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="d4124-172">AS number for peering.</span></span> <span data-ttu-id="d4124-173">Puede usar 2 bytes o 4 bytes como números AS.</span><span class="sxs-lookup"><span data-stu-id="d4124-173">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="d4124-174">**Opcional:** un hash MD5 si elige usar uno.</span><span class="sxs-lookup"><span data-stu-id="d4124-174">**Optional -** An MD5 hash if you choose to use one.</span></span>
3. <span data-ttu-id="d4124-175">Seleccione la fila de emparejamiento público de Azure, como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="d4124-175">Select the Azure public peering row, as shown in the following image:</span></span>

  ![seleccionar fila de emparejamiento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. <span data-ttu-id="d4124-177">Configure el emparejamiento público.</span><span class="sxs-lookup"><span data-stu-id="d4124-177">Configure public peering.</span></span> <span data-ttu-id="d4124-178">La siguiente imagen muestra un ejemplo de configuración:</span><span class="sxs-lookup"><span data-stu-id="d4124-178">The following image shows a configuration example:</span></span>

  ![Configuración del emparejamiento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. <span data-ttu-id="d4124-180">Guarde la configuración una vez que haya especificado todos los parámetros.</span><span class="sxs-lookup"><span data-stu-id="d4124-180">Save the configuration once you have specified all parameters.</span></span> <span data-ttu-id="d4124-181">Una vez que la configuración se haya aceptado correctamente, verá algo similar al siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d4124-181">After the configuration has been accepted successfully, you see something similar to the following example:</span></span>

  ![Guardado de configuración de emparejamiento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="d4124-183">Visualización de detalles de un emparejamiento público de Azure</span><span class="sxs-lookup"><span data-stu-id="d4124-183">To view Azure public peering details</span></span>

<span data-ttu-id="d4124-184">Para ver las propiedades de un emparejamiento público de Azure, seleccione el emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="d4124-184">You can view the properties of Azure public peering by selecting the peering.</span></span>

![ver propiedades de emparejamiento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="d4124-186">Actualización del establecimiento de configuración del emparejamiento público de Azure</span><span class="sxs-lookup"><span data-stu-id="d4124-186">To update Azure public peering configuration</span></span>

<span data-ttu-id="d4124-187">Puede seleccionar la fila del emparejamiento y modificar las propiedades del mismo.</span><span class="sxs-lookup"><span data-stu-id="d4124-187">You can select the row for peering and modify the peering properties.</span></span>

![seleccionar fila de emparejamiento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="d4124-189">Eliminación del emparejamiento público de Azure</span><span class="sxs-lookup"><span data-stu-id="d4124-189">To delete Azure public peering</span></span>

<span data-ttu-id="d4124-190">Para quitar la configuración de emparejamiento, seleccione el icono de eliminación, como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d4124-190">You can remove your peering configuration by selecting the delete icon, as shown in the following example:</span></span>

![eliminar emparejamiento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a><span data-ttu-id="d4124-192">Emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="d4124-192">Microsoft peering</span></span>

<span data-ttu-id="d4124-193">Esta sección le ayuda a crear, obtener, actualizar y eliminar la configuración de emparejamiento de Microsoft para un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d4124-193">This section helps you create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4124-194">Se anunciarán todos los prefijos de servicio para el emparejamiento de Microsoft de los circuitos ExpressRoute que se configuraron antes del 1 de agosto de 2017, incluso si no se definen filtros de ruta.</span><span class="sxs-lookup"><span data-stu-id="d4124-194">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through the Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="d4124-195">No se anunciará ningún prefijo para el emparejamiento de Microsoft de los circuitos ExpressRoute que se configuraron el 1 de agosto de 2017 o con posterioridad, hasta que se asocie un filtro de ruta al circuito.</span><span class="sxs-lookup"><span data-stu-id="d4124-195">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span> <span data-ttu-id="d4124-196">Para más información, consulte [Configuración de un filtro de ruta para el emparejamiento de Microsoft](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d4124-196">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="d4124-197">Creación del emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="d4124-197">To create Microsoft peering</span></span>

1. <span data-ttu-id="d4124-198">Configure un circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d4124-198">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="d4124-199">Antes de continuar, asegúrese de que el proveedor de que el proveedor de conectividad ha aprovisionado el circuito por completo.</span><span class="sxs-lookup"><span data-stu-id="d4124-199">Ensure that the circuit is fully provisioned by the connectivity provider before continuing further.</span></span>

  ![mostrar emparejamiento de Microsoft](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="d4124-201">Establezca la configuración del emparejamiento de Microsoft para el circuito.</span><span class="sxs-lookup"><span data-stu-id="d4124-201">Configure Microsoft peering for the circuit.</span></span> <span data-ttu-id="d4124-202">Asegúrese de que tiene la siguiente información antes de empezar:</span><span class="sxs-lookup"><span data-stu-id="d4124-202">Make sure that you have the following information before you proceed.</span></span>

  * <span data-ttu-id="d4124-203">Una subred /30 para el vínculo principal.</span><span class="sxs-lookup"><span data-stu-id="d4124-203">A /30 subnet for the primary link.</span></span> <span data-ttu-id="d4124-204">Debe ser un prefijo de IPv4 público válido que sea de su propiedad y esté registrado en un Registro regional de Internet (RIR) o un Registro de enrutamiento de Internet (IRR).</span><span class="sxs-lookup"><span data-stu-id="d4124-204">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="d4124-205">Una subred /30 para el vínculo secundario.</span><span class="sxs-lookup"><span data-stu-id="d4124-205">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="d4124-206">Debe ser un prefijo de IPv4 público válido que sea de su propiedad y esté registrado en un Registro regional de Internet (RIR) o un Registro de enrutamiento de Internet (IRR).</span><span class="sxs-lookup"><span data-stu-id="d4124-206">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="d4124-207">Un identificador VLAN válido para establecer esta configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="d4124-207">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="d4124-208">Asegúrese de que ninguna otra configuración entre pares en el circuito usa el mismo identificador de VLAN.</span><span class="sxs-lookup"><span data-stu-id="d4124-208">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="d4124-209">Número de sistema autónomo (AS) para la configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="d4124-209">AS number for peering.</span></span> <span data-ttu-id="d4124-210">Puede usar 2 bytes o 4 bytes como números AS.</span><span class="sxs-lookup"><span data-stu-id="d4124-210">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="d4124-211">Prefijos anunciados: tiene que proporcionar una lista de todos los prefijos que planea anunciar en la sesión BGP.</span><span class="sxs-lookup"><span data-stu-id="d4124-211">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="d4124-212">Se aceptan solo prefijos de direcciones IP públicas.</span><span class="sxs-lookup"><span data-stu-id="d4124-212">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="d4124-213">Si tiene pensado enviar un conjunto de prefijos, puede enviar una lista separada por comas.</span><span class="sxs-lookup"><span data-stu-id="d4124-213">If you plan to send a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="d4124-214">Estos prefijos tienen que estar registrados a su nombre en un Registro regional de Internet (RIR) o un Registro de enrutamiento de Internet (IRR).</span><span class="sxs-lookup"><span data-stu-id="d4124-214">These prefixes must be registered to you in an RIR / IRR.</span></span>
  * <span data-ttu-id="d4124-215">**Opcional:** Cliente ASN: si los prefijos anunciados no están registrados en el número AS de emparejamiento, puede especificar el número de AS en el que están registrados.</span><span class="sxs-lookup"><span data-stu-id="d4124-215">**Optional -** Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span>
  * <span data-ttu-id="d4124-216">Nombre del enrutamiento del Registro: puede especificar el RIR o TIR en el que están registrados el número AS y los prefijos.</span><span class="sxs-lookup"><span data-stu-id="d4124-216">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="d4124-217">**Opcional:** un hash MD5 si elige usar uno.</span><span class="sxs-lookup"><span data-stu-id="d4124-217">**Optional -** An MD5 hash if you choose to use one.</span></span>
3. <span data-ttu-id="d4124-218">Puede seleccionar el emparejamiento que desea configurar, como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="d4124-218">You can select the peering you wish to configure, as shown in the following example.</span></span> <span data-ttu-id="d4124-219">Seleccione la fila del emparejamiento de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d4124-219">Select the Microsoft peering row.</span></span>

  ![seleccionar fila de emparejamiento de Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. <span data-ttu-id="d4124-221">Configure el emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="d4124-221">Configure Microsoft peering.</span></span> <span data-ttu-id="d4124-222">La siguiente imagen muestra un ejemplo de configuración:</span><span class="sxs-lookup"><span data-stu-id="d4124-222">The following image shows a configuration example:</span></span>

  ![configurar emparejamiento de Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. <span data-ttu-id="d4124-224">Guarde la configuración una vez que haya especificado todos los parámetros.</span><span class="sxs-lookup"><span data-stu-id="d4124-224">Save the configuration once you have specified all parameters.</span></span>

  <span data-ttu-id="d4124-225">Si el circuito llega a un estado de validación necesaria (como se muestra en la imagen), debe abrir una incidencia de soporte técnico para mostrar la prueba de propiedad de los prefijos a nuestro equipo de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="d4124-225">If your circuit gets to a 'Validation needed' state (as shown in the image), you must open a support ticket to show proof of ownership of the prefixes to our support team.</span></span>

  ![Guardado de la configuración de emparejamiento de Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  <span data-ttu-id="d4124-227">Puede abrir un vale de soporte técnico directamente desde el portal, tal como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d4124-227">You can open a support ticket directly from the portal, as shown in the following example:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. <span data-ttu-id="d4124-228">Después de que la configuración se haya aceptado correctamente, verá algo similar a la imagen siguiente:</span><span class="sxs-lookup"><span data-stu-id="d4124-228">After the configuration has been accepted successfully, you see something similar to the following image:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="to-view-microsoft-peering-details"></a><span data-ttu-id="d4124-229">Visualización de detalles del emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="d4124-229">To view Microsoft peering details</span></span>

<span data-ttu-id="d4124-230">Para ver las propiedades de un emparejamiento público de Azure, seleccione el emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="d4124-230">You can view the properties of Azure public peering by selecting the peering.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="d4124-231">Actualización de la configuración de emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="d4124-231">To update Microsoft peering configuration</span></span>

<span data-ttu-id="d4124-232">Puede seleccionar la fila del emparejamiento y modificar las propiedades del mismo.</span><span class="sxs-lookup"><span data-stu-id="d4124-232">You can select the row for peering and modify the peering properties.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="d4124-233">Eliminación del emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="d4124-233">To delete Microsoft peering</span></span>

<span data-ttu-id="d4124-234">Para quitar la configuración de emparejamiento, seleccione el icono de eliminación, como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="d4124-234">You can remove your peering configuration by selecting the delete icon, as shown in the following image:</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a><span data-ttu-id="d4124-235">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d4124-235">Next steps</span></span>

<span data-ttu-id="d4124-236">Siguiente paso, [Conexión de una red virtual a un circuito ExpressRoute](expressroute-howto-linkvnet-portal-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="d4124-236">Next step, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-portal-resource-manager.md)</span></span>
* <span data-ttu-id="d4124-237">Para más información sobre los flujos de trabajo de ExpressRoute, vea [Flujos de trabajo de ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="d4124-237">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="d4124-238">Para más información sobre el emparejamiento de circuitos, vea [Circuitos y dominios de enrutamiento de ExpressRoute](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="d4124-238">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="d4124-239">Para más información sobre redes virtuales, vea [Información general sobre redes virtuales](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d4124-239">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
