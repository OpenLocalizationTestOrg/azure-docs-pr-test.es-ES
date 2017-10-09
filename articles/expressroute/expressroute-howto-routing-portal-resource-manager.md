---
title: "¿Cómo tooconfigure enrutamiento (emparejamiento) por un circuito ExpressRoute: el Administrador de recursos: Azure | Documentos de Microsoft"
description: "En este artículo le guiará por los pasos de Hola para crear y aprovisionamiento Hola privado, público y emparejamiento de Microsoft de un circuito de ExpressRoute. Este artículo también muestra cómo toocheck estado de hello, actualizar o eliminar emparejamientos para el circuito."
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
ms.openlocfilehash: a8ca25f488dde728cb3b06cd2c91873f3069feaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a><span data-ttu-id="53777-104">Creación y modificación del emparejamiento de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="53777-104">Create and modify peering for an ExpressRoute circuit</span></span>

<span data-ttu-id="53777-105">En este artículo le ayuda a crear y administrar la configuración de enrutamiento para un circuito ExpressRoute en modelo de implementación de administrador de recursos de hello mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="53777-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using hello Azure portal.</span></span> <span data-ttu-id="53777-106">También puede comprobar el estado de hello, update o delete y desaprovisionar los emparejamientos de un circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="53777-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="53777-107">Si desea toouse una toowork otro método con el circuito, seleccione un artículo de hello lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="53777-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>


## <a name="configuration-prerequisites"></a><span data-ttu-id="53777-108">Requisitos previos de configuración</span><span class="sxs-lookup"><span data-stu-id="53777-108">Configuration prerequisites</span></span>

* <span data-ttu-id="53777-109">Asegúrese de que ha revisado hello [requisitos previos](expressroute-prerequisites.md) página hello [requisitos de enrutamiento](expressroute-routing.md) hello y página [flujos de trabajo](expressroute-workflows.md) página antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="53777-109">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="53777-110">Tiene que tener un circuito ExpressRoute activo.</span><span class="sxs-lookup"><span data-stu-id="53777-110">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="53777-111">Siga las instrucciones de hello demasiado[crear un circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) y tener circuito de hello habilitada por el proveedor de conectividad antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="53777-111">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="53777-112">Hola circuito de ExpressRoute debe estar en un estado habilitado y aprovisionado para usted toobe toorun capaz de hello cmdlets en las secciones siguientes se Hola.</span><span class="sxs-lookup"><span data-stu-id="53777-112">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets in hello next sections.</span></span>
* <span data-ttu-id="53777-113">Si tiene previsto toouse un hash MD5/clave compartido, ser seguro toouse esto en ambos lados del Hola túnel y límite Hola el número máximo de caracteres tooa de 25.</span><span class="sxs-lookup"><span data-stu-id="53777-113">If you plan toouse a shared key/MD5 hash, be sure toouse this on both sides of hello tunnel and limit hello number of characters tooa maximum of 25.</span></span>

<span data-ttu-id="53777-114">Estas instrucciones aplican solo toocircuits creado con proveedores de servicios que ofrece servicios de conectividad de nivel 2.</span><span class="sxs-lookup"><span data-stu-id="53777-114">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="53777-115">Si usa un proveedor de servicios que ofrece servicios administrados de nivel 3 (normalmente VPN IP, como MPLS), el mismo proveedor de conectividad configura y administra el enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="53777-115">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="53777-116">Se actualmente no se publica emparejamientos configurados por los proveedores de servicios a través del portal de administración de servicios de Hola.</span><span class="sxs-lookup"><span data-stu-id="53777-116">We currently do not advertise peerings configured by service providers through hello service management portal.</span></span> <span data-ttu-id="53777-117">Se está trabajando para habilitar esta funcionalidad pronto.</span><span class="sxs-lookup"><span data-stu-id="53777-117">We are working on enabling this capability soon.</span></span> <span data-ttu-id="53777-118">Antes de configurar los emparejamientos BGP, realice las comprobaciones pertinentes con su proveedor de servicios.</span><span class="sxs-lookup"><span data-stu-id="53777-118">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="53777-119">Puede configurar una, dos o las tres configuraciones entre pares (Azure privado, Azure público y Microsoft) para un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="53777-119">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="53777-120">Puede establecer las configuraciones entre pares en cualquier orden.</span><span class="sxs-lookup"><span data-stu-id="53777-120">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="53777-121">Sin embargo, debe asegurarse de completar configuración de Hola de cada uno de ellos emparejamiento a la vez.</span><span class="sxs-lookup"><span data-stu-id="53777-121">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="53777-122">Configuración entre pares privados de Azure</span><span class="sxs-lookup"><span data-stu-id="53777-122">Azure private peering</span></span>

<span data-ttu-id="53777-123">En esta sección le ayuda a crear, obtener, actualizar y eliminar hello Azure configuración privada de emparejamiento de un circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="53777-123">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="53777-124">toocreate emparejamiento privado de Azure</span><span class="sxs-lookup"><span data-stu-id="53777-124">toocreate Azure private peering</span></span>

1. <span data-ttu-id="53777-125">Configurar circuito de ExpressRoute Hola.</span><span class="sxs-lookup"><span data-stu-id="53777-125">Configure hello ExpressRoute circuit.</span></span> <span data-ttu-id="53777-126">Asegúrese de que el circuito de hello está aprovisionado por completo por el proveedor de conectividad de hello antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="53777-126">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing.</span></span>

  ![list](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="53777-128">Configurar Azure intercambio de tráfico privado para el circuito de Hola.</span><span class="sxs-lookup"><span data-stu-id="53777-128">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="53777-129">Asegúrese de que dispone de hello siguientes elementos antes de continuar con los pasos siguientes de hello:</span><span class="sxs-lookup"><span data-stu-id="53777-129">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="53777-130">/ 30 subred para el vínculo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="53777-130">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="53777-131">subred de Hello no debe formar parte de cualquier espacio de direcciones reservada para las redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="53777-131">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="53777-132">/ 30 subred para el vínculo secundario Hola.</span><span class="sxs-lookup"><span data-stu-id="53777-132">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="53777-133">subred de Hello no debe formar parte de cualquier espacio de direcciones reservada para las redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="53777-133">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="53777-134">Un tooestablish de Id. de VLAN válido este emparejamiento correctamente.</span><span class="sxs-lookup"><span data-stu-id="53777-134">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="53777-135">No Asegúrese de que ningún otro emparejamiento en el circuito de hello usa Hola mismo identificador de VLAN.</span><span class="sxs-lookup"><span data-stu-id="53777-135">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="53777-136">Número de sistema autónomo (AS) para la configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="53777-136">AS number for peering.</span></span> <span data-ttu-id="53777-137">Puede usar 2 bytes o 4 bytes como números AS.</span><span class="sxs-lookup"><span data-stu-id="53777-137">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="53777-138">Puede usar un número AS privado para esta configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="53777-138">You can use a private AS number for this peering.</span></span> <span data-ttu-id="53777-139">Asegúrese de que no usa 65515.</span><span class="sxs-lookup"><span data-stu-id="53777-139">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="53777-140">**Opcional:** un hash MD5 si elige toouse uno.</span><span class="sxs-lookup"><span data-stu-id="53777-140">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="53777-141">Seleccione la fila de emparejamiento privada de Azure de hello, como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="53777-141">Select hello Azure Private peering row, as shown in hello following example:</span></span>

  ![privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. <span data-ttu-id="53777-143">Configure el emparejamiento privado.</span><span class="sxs-lookup"><span data-stu-id="53777-143">Configure private peering.</span></span> <span data-ttu-id="53777-144">Hola siguiente imagen muestra un ejemplo de configuración:</span><span class="sxs-lookup"><span data-stu-id="53777-144">hello following image shows a configuration example:</span></span>

  ![configurar el emparejamiento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. <span data-ttu-id="53777-146">Guardar configuración de hello una vez que haya especificado todos los parámetros.</span><span class="sxs-lookup"><span data-stu-id="53777-146">Save hello configuration once you have specified all parameters.</span></span> <span data-ttu-id="53777-147">Una vez que ha aceptado correctamente la configuración de hello, verá algo similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="53777-147">After hello configuration has been accepted successfully, you see something similar toohello following example:</span></span>

  ![guardar emparejamiento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="53777-149">tooview privada emparejamiento detalles de Azure</span><span class="sxs-lookup"><span data-stu-id="53777-149">tooview Azure private peering details</span></span>

<span data-ttu-id="53777-150">Puede ver propiedades de Hola de emparejamiento privado Azure seleccionando Hola emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="53777-150">You can view hello properties of Azure private peering by selecting hello peering.</span></span>

![ver emparejamiento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="53777-152">tooupdate configuración de emparejamiento privada de Azure</span><span class="sxs-lookup"><span data-stu-id="53777-152">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="53777-153">Puede seleccionar la fila de hello para el emparejamiento y modificar las propiedades de emparejamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="53777-153">You can select hello row for peering and modify hello peering properties.</span></span>

![actualizar emparejamiento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="53777-155">toodelete emparejamiento privado de Azure</span><span class="sxs-lookup"><span data-stu-id="53777-155">toodelete Azure private peering</span></span>

<span data-ttu-id="53777-156">Puede quitar la configuración de emparejamiento seleccionando el icono de eliminación de hello, como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="53777-156">You can remove your peering configuration by selecting hello delete icon, as shown in hello following image:</span></span>

![eliminar emparejamiento privado](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a><span data-ttu-id="53777-158">Configuración entre pares públicos de Azure</span><span class="sxs-lookup"><span data-stu-id="53777-158">Azure public peering</span></span>

<span data-ttu-id="53777-159">En esta sección le ayuda a crear, obtener, actualizar y eliminar hello Azure configuración de emparejamiento público de un circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="53777-159">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="53777-160">toocreate pares públicos de Azure</span><span class="sxs-lookup"><span data-stu-id="53777-160">toocreate Azure public peering</span></span>

1. <span data-ttu-id="53777-161">Configure un circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="53777-161">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="53777-162">Asegúrese de que el circuito de hello está aprovisionado por completo por el proveedor de conectividad de hello antes de continuar más.</span><span class="sxs-lookup"><span data-stu-id="53777-162">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing further.</span></span>

  ![mostrar emparejamiento público](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="53777-164">Configure pares públicos de Azure para el circuito de Hola.</span><span class="sxs-lookup"><span data-stu-id="53777-164">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="53777-165">Asegúrese de que dispone de hello siguientes elementos antes de continuar con los pasos siguientes de hello:</span><span class="sxs-lookup"><span data-stu-id="53777-165">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="53777-166">/ 30 subred para el vínculo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="53777-166">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="53777-167">Tiene que ser un prefijo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="53777-167">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="53777-168">/ 30 subred para el vínculo secundario Hola.</span><span class="sxs-lookup"><span data-stu-id="53777-168">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="53777-169">Tiene que ser un prefijo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="53777-169">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="53777-170">Un tooestablish de Id. de VLAN válido este emparejamiento correctamente.</span><span class="sxs-lookup"><span data-stu-id="53777-170">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="53777-171">No Asegúrese de que ningún otro emparejamiento en el circuito de hello usa Hola mismo identificador de VLAN.</span><span class="sxs-lookup"><span data-stu-id="53777-171">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="53777-172">Número de sistema autónomo (AS) para la configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="53777-172">AS number for peering.</span></span> <span data-ttu-id="53777-173">Puede usar 2 bytes o 4 bytes como números AS.</span><span class="sxs-lookup"><span data-stu-id="53777-173">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="53777-174">**Opcional:** un hash MD5 si elige toouse uno.</span><span class="sxs-lookup"><span data-stu-id="53777-174">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="53777-175">Seleccione hello Azure fila emparejamiento público, tal como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="53777-175">Select hello Azure public peering row, as shown in hello following image:</span></span>

  ![seleccionar fila de emparejamiento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. <span data-ttu-id="53777-177">Configure el emparejamiento público.</span><span class="sxs-lookup"><span data-stu-id="53777-177">Configure public peering.</span></span> <span data-ttu-id="53777-178">Hola siguiente imagen muestra un ejemplo de configuración:</span><span class="sxs-lookup"><span data-stu-id="53777-178">hello following image shows a configuration example:</span></span>

  ![Configuración del emparejamiento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. <span data-ttu-id="53777-180">Guardar configuración de hello una vez que haya especificado todos los parámetros.</span><span class="sxs-lookup"><span data-stu-id="53777-180">Save hello configuration once you have specified all parameters.</span></span> <span data-ttu-id="53777-181">Una vez que ha aceptado correctamente la configuración de hello, verá algo similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="53777-181">After hello configuration has been accepted successfully, you see something similar toohello following example:</span></span>

  ![Guardado de configuración de emparejamiento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="53777-183">tooview Azure pública emparejamiento detalles</span><span class="sxs-lookup"><span data-stu-id="53777-183">tooview Azure public peering details</span></span>

<span data-ttu-id="53777-184">Puede ver propiedades de Hola de emparejamiento público Azure seleccionando Hola emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="53777-184">You can view hello properties of Azure public peering by selecting hello peering.</span></span>

![ver propiedades de emparejamiento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="53777-186">tooupdate configuración de interconexión pública de Azure</span><span class="sxs-lookup"><span data-stu-id="53777-186">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="53777-187">Puede seleccionar la fila de hello para el emparejamiento y modificar las propiedades de emparejamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="53777-187">You can select hello row for peering and modify hello peering properties.</span></span>

![seleccionar fila de emparejamiento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="53777-189">toodelete pares públicos de Azure</span><span class="sxs-lookup"><span data-stu-id="53777-189">toodelete Azure public peering</span></span>

<span data-ttu-id="53777-190">Puede quitar la configuración de emparejamiento seleccionando el icono de eliminación de hello, como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="53777-190">You can remove your peering configuration by selecting hello delete icon, as shown in hello following example:</span></span>

![eliminar emparejamiento público](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a><span data-ttu-id="53777-192">Emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="53777-192">Microsoft peering</span></span>

<span data-ttu-id="53777-193">En esta sección le ayuda a crear, obtener, actualizar y eliminar la configuración de emparejamiento de Microsoft de Hola por un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="53777-193">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="53777-194">Emparejamiento de Microsoft de circuitos ExpressRoute que estaban configurados anterior tooAugust 1, 2017 tendrá todos los prefijos de servicio implementados a través de emparejamiento de Microsoft hello, incluso si no se definen los filtros de ruta.</span><span class="sxs-lookup"><span data-stu-id="53777-194">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="53777-195">Emparejamiento de Microsoft de circuitos ExpressRoute configurados en o después del 1 de agosto de 2017 no tendrá todos los prefijos anunciados hasta que se conecte un filtro de ruta toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="53777-195">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="53777-196">Para más información, consulte [Configuración de un filtro de ruta para el emparejamiento de Microsoft](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="53777-196">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="53777-197">emparejamiento de Microsoft toocreate</span><span class="sxs-lookup"><span data-stu-id="53777-197">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="53777-198">Configure un circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="53777-198">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="53777-199">Asegúrese de que el circuito de hello está aprovisionado por completo por el proveedor de conectividad de hello antes de continuar más.</span><span class="sxs-lookup"><span data-stu-id="53777-199">Ensure that hello circuit is fully provisioned by hello connectivity provider before continuing further.</span></span>

  ![mostrar emparejamiento de Microsoft](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="53777-201">Configurar Microsoft emparejamiento para el circuito de Hola.</span><span class="sxs-lookup"><span data-stu-id="53777-201">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="53777-202">Asegúrese de que haya Hola siguiente información antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="53777-202">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="53777-203">/ 30 subred para el vínculo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="53777-203">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="53777-204">Debe ser un prefijo de IPv4 público válido que sea de su propiedad y esté registrado en un Registro regional de Internet (RIR) o un Registro de enrutamiento de Internet (IRR).</span><span class="sxs-lookup"><span data-stu-id="53777-204">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="53777-205">/ 30 subred para el vínculo secundario Hola.</span><span class="sxs-lookup"><span data-stu-id="53777-205">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="53777-206">Debe ser un prefijo de IPv4 público válido que sea de su propiedad y esté registrado en un Registro regional de Internet (RIR) o un Registro de enrutamiento de Internet (IRR).</span><span class="sxs-lookup"><span data-stu-id="53777-206">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="53777-207">Un tooestablish de Id. de VLAN válido este emparejamiento correctamente.</span><span class="sxs-lookup"><span data-stu-id="53777-207">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="53777-208">No Asegúrese de que ningún otro emparejamiento en el circuito de hello usa Hola mismo identificador de VLAN.</span><span class="sxs-lookup"><span data-stu-id="53777-208">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="53777-209">Número de sistema autónomo (AS) para la configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="53777-209">AS number for peering.</span></span> <span data-ttu-id="53777-210">Puede usar 2 bytes o 4 bytes como números AS.</span><span class="sxs-lookup"><span data-stu-id="53777-210">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="53777-211">Anuncian prefijos: debe proporcionar una lista de todos los prefijos piensa tooadvertise en las sesiones BGP Hola.</span><span class="sxs-lookup"><span data-stu-id="53777-211">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="53777-212">Se aceptan solo prefijos de direcciones IP públicas.</span><span class="sxs-lookup"><span data-stu-id="53777-212">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="53777-213">Si tiene previsto toosend un conjunto de prefijos, puede enviar una lista separada por comas.</span><span class="sxs-lookup"><span data-stu-id="53777-213">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="53777-214">Estos prefijos deben ser tooyou registrado en un RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="53777-214">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="53777-215">**Opcional:** cliente ASN: si es que los prefijos de publicidad que no están registrado toohello emparejamiento como número, puede especificar hello como número toowhich están registrados.</span><span class="sxs-lookup"><span data-stu-id="53777-215">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="53777-216">Nombre del enrutamiento del registro: Puede especificar Hola RIR / IRR en qué hello como número y los prefijos registrados.</span><span class="sxs-lookup"><span data-stu-id="53777-216">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="53777-217">**Opcional:** un hash MD5 si elige toouse uno.</span><span class="sxs-lookup"><span data-stu-id="53777-217">**Optional -** An MD5 hash if you choose toouse one.</span></span>
3. <span data-ttu-id="53777-218">Puede seleccionar Hola emparejamiento desea tooconfigure, como se muestra en hello después de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="53777-218">You can select hello peering you wish tooconfigure, as shown in hello following example.</span></span> <span data-ttu-id="53777-219">Seleccione la fila de emparejamiento de Microsoft de Hola.</span><span class="sxs-lookup"><span data-stu-id="53777-219">Select hello Microsoft peering row.</span></span>

  ![seleccionar fila de emparejamiento de Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. <span data-ttu-id="53777-221">Configure el emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="53777-221">Configure Microsoft peering.</span></span> <span data-ttu-id="53777-222">Hola siguiente imagen muestra un ejemplo de configuración:</span><span class="sxs-lookup"><span data-stu-id="53777-222">hello following image shows a configuration example:</span></span>

  ![configurar emparejamiento de Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. <span data-ttu-id="53777-224">Guardar configuración de hello una vez que haya especificado todos los parámetros.</span><span class="sxs-lookup"><span data-stu-id="53777-224">Save hello configuration once you have specified all parameters.</span></span>

  <span data-ttu-id="53777-225">Si el circuito obtiene tooa 'Validación necesaria' estado (como se muestra en la imagen de hello), debe abrir una tooshow de vale de soporte técnico de prueba de posesión del equipo de soporte técnico de hello prefijos tooour.</span><span class="sxs-lookup"><span data-stu-id="53777-225">If your circuit gets tooa 'Validation needed' state (as shown in hello image), you must open a support ticket tooshow proof of ownership of hello prefixes tooour support team.</span></span>

  ![Guardado de la configuración de emparejamiento de Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  <span data-ttu-id="53777-227">Puede abrir una incidencia de soporte técnico directamente desde el portal de hello, como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="53777-227">You can open a support ticket directly from hello portal, as shown in hello following example:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. <span data-ttu-id="53777-228">Una vez que ha aceptado correctamente la configuración de hello, verá algo similar toohello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="53777-228">After hello configuration has been accepted successfully, you see something similar toohello following image:</span></span>

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="tooview-microsoft-peering-details"></a><span data-ttu-id="53777-229">detalles de emparejamiento de Microsoft tooview</span><span class="sxs-lookup"><span data-stu-id="53777-229">tooview Microsoft peering details</span></span>

<span data-ttu-id="53777-230">Puede ver propiedades de Hola de emparejamiento público Azure seleccionando Hola emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="53777-230">You can view hello properties of Azure public peering by selecting hello peering.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="53777-231">configuración de emparejamiento de Microsoft tooupdate</span><span class="sxs-lookup"><span data-stu-id="53777-231">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="53777-232">Puede seleccionar la fila de hello para el emparejamiento y modificar las propiedades de emparejamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="53777-232">You can select hello row for peering and modify hello peering properties.</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="53777-233">emparejamiento de Microsoft toodelete</span><span class="sxs-lookup"><span data-stu-id="53777-233">toodelete Microsoft peering</span></span>

<span data-ttu-id="53777-234">Puede quitar la configuración de emparejamiento seleccionando el icono de eliminación de hello, como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="53777-234">You can remove your peering configuration by selecting hello delete icon, as shown in hello following image:</span></span>

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a><span data-ttu-id="53777-235">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="53777-235">Next steps</span></span>

<span data-ttu-id="53777-236">Siguiente paso, [vincular un circuito de ExpressRoute de tooan de red virtual](expressroute-howto-linkvnet-portal-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="53777-236">Next step, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-portal-resource-manager.md)</span></span>
* <span data-ttu-id="53777-237">Para más información sobre los flujos de trabajo de ExpressRoute, vea [Flujos de trabajo de ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="53777-237">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="53777-238">Para más información sobre el emparejamiento de circuitos, vea [Circuitos y dominios de enrutamiento de ExpressRoute](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="53777-238">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="53777-239">Para más información sobre redes virtuales, vea [Información general sobre redes virtuales](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="53777-239">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
