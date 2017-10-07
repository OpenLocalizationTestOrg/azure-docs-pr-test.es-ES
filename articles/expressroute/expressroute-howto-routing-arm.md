---
title: "¿Cómo tooconfigure enrutamiento (emparejamiento) por un circuito ExpressRoute: el Administrador de recursos: PowerShell: Azure | Documentos de Microsoft"
description: "En este artículo le guiará por los pasos de Hola para crear y aprovisionamiento Hola privado, público y emparejamiento de Microsoft de un circuito de ExpressRoute. Este artículo también muestra cómo toocheck estado de hello, actualizar o eliminar emparejamientos para el circuito."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0a036d51-77ae-4fee-9ddb-35f040fbdcdf
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: eb3ddf5c05a086ac3e22c64417e51381ef465921
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="c8905-104">Creación y modificación del emparejamiento de un circuito ExpressRoute mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8905-104">Create and modify peering for an ExpressRoute circuit using PowerShell</span></span>

<span data-ttu-id="c8905-105">En este artículo le ayuda a crear y administrar la configuración de enrutamiento para un circuito ExpressRoute en modelo de implementación de administrador de recursos de hello mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c8905-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="c8905-106">También puede comprobar el estado de hello, update o delete y desaprovisionar los emparejamientos de un circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c8905-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="c8905-107">Si desea toouse una toowork otro método con el circuito, seleccione un artículo de hello lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="c8905-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c8905-108">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c8905-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="c8905-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8905-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="c8905-110">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="c8905-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="c8905-111">Vídeo: pares privados</span><span class="sxs-lookup"><span data-stu-id="c8905-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="c8905-112">Vídeo: pares públicos</span><span class="sxs-lookup"><span data-stu-id="c8905-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="c8905-113">Vídeo: emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="c8905-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="c8905-114">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="c8905-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="c8905-115">Requisitos previos de configuración</span><span class="sxs-lookup"><span data-stu-id="c8905-115">Configuration prerequisites</span></span>

* <span data-ttu-id="c8905-116">Necesitará la versión más reciente de Hola de hello cmdlets de PowerShell del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="c8905-116">You will need hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="c8905-117">Para obtener más información, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c8905-117">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 
* <span data-ttu-id="c8905-118">Asegúrese de que ha revisado hello [requisitos previos](expressroute-prerequisites.md) página hello [requisitos de enrutamiento](expressroute-routing.md) hello y página [flujos de trabajo](expressroute-workflows.md) página antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="c8905-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="c8905-119">Tiene que tener un circuito ExpressRoute activo.</span><span class="sxs-lookup"><span data-stu-id="c8905-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="c8905-120">Siga las instrucciones de hello demasiado[crear un circuito ExpressRoute](expressroute-howto-circuit-arm.md) y tener circuito de hello habilitada por el proveedor de conectividad antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="c8905-120">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="c8905-121">Hola circuito de ExpressRoute debe estar en un estado habilitado y aprovisionado para usted toobe toorun capaz de hello cmdlets en este artículo.</span><span class="sxs-lookup"><span data-stu-id="c8905-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets in this article.</span></span>

<span data-ttu-id="c8905-122">Estas instrucciones aplican solo toocircuits creado con proveedores de servicios que ofrece servicios de conectividad de nivel 2.</span><span class="sxs-lookup"><span data-stu-id="c8905-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="c8905-123">Si usa un proveedor de servicios que ofrece servicios administrados de nivel 3 (normalmente VPN IP, como MPLS), el mismo proveedor de conectividad configurará y administrará el enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="c8905-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c8905-124">Se actualmente no se publica emparejamientos configurados por los proveedores de servicios a través del portal de administración de servicios de Hola.</span><span class="sxs-lookup"><span data-stu-id="c8905-124">We currently do not advertise peerings configured by service providers through hello service management portal.</span></span> <span data-ttu-id="c8905-125">Se está trabajando para habilitar esta funcionalidad pronto.</span><span class="sxs-lookup"><span data-stu-id="c8905-125">We are working on enabling this capability soon.</span></span> <span data-ttu-id="c8905-126">Antes de configurar los emparejamientos BGP, realice las comprobaciones pertinentes con su proveedor de servicios.</span><span class="sxs-lookup"><span data-stu-id="c8905-126">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="c8905-127">Puede configurar una, dos o las tres configuraciones entre pares (Azure privado, Azure público y Microsoft) para un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c8905-127">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="c8905-128">Puede establecer las configuraciones entre pares en cualquier orden.</span><span class="sxs-lookup"><span data-stu-id="c8905-128">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="c8905-129">Sin embargo, debe asegurarse de completar configuración de Hola de cada uno de ellos emparejamiento a la vez.</span><span class="sxs-lookup"><span data-stu-id="c8905-129">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span> 

## <a name="azure-private-peering"></a><span data-ttu-id="c8905-130">Configuración entre pares privados de Azure</span><span class="sxs-lookup"><span data-stu-id="c8905-130">Azure private peering</span></span>

<span data-ttu-id="c8905-131">En esta sección le ayuda a crear, obtener, actualizar y eliminar hello Azure configuración privada de emparejamiento de un circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c8905-131">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="c8905-132">toocreate emparejamiento privado de Azure</span><span class="sxs-lookup"><span data-stu-id="c8905-132">toocreate Azure private peering</span></span>

1. <span data-ttu-id="c8905-133">Importe el módulo de PowerShell de Hola para ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c8905-133">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="c8905-134">Debe instalar Hola installer más reciente de PowerShell de [Galería de PowerShell](http://www.powershellgallery.com/) e importar módulos de Azure Resource Manager hello en la sesión de PowerShell de hello en toostart orden mediante cmdlets de ExpressRoute Hola.</span><span class="sxs-lookup"><span data-stu-id="c8905-134">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="c8905-135">Necesitará toorun PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="c8905-135">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  <span data-ttu-id="c8905-136">Importar todos los módulos de AzureRM.* hello en hello conocida el intervalo de versiones semántico de.</span><span class="sxs-lookup"><span data-stu-id="c8905-136">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="c8905-137">También puede importar un módulo seleccione dentro de hello conocida el intervalo de versiones semántico.</span><span class="sxs-lookup"><span data-stu-id="c8905-137">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network 
  ```

  <span data-ttu-id="c8905-138">Inicie sesión en la cuenta de tooyour.</span><span class="sxs-lookup"><span data-stu-id="c8905-138">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="c8905-139">Seleccione la suscripción de hello desea toocreate circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c8905-139">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="c8905-140">Crear un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c8905-140">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="c8905-141">Siga Hola instrucciones toocreate una [circuito de ExpressRoute](expressroute-howto-circuit-arm.md) y hacer que se aprovisiona proveedor de conectividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="c8905-141">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="c8905-142">Si el proveedor de conectividad ofrece servicios administrados de capa 3, puede solicitar su tooenable de proveedor de conectividad Azure privada emparejamiento para usted.</span><span class="sxs-lookup"><span data-stu-id="c8905-142">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="c8905-143">En ese caso, no necesitará toofollow instrucciones que se indican en las secciones siguientes se Hola.</span><span class="sxs-lookup"><span data-stu-id="c8905-143">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="c8905-144">Sin embargo, si el proveedor de conectividad no administra el enrutamiento para usted, después de crear el circuito, continuar la configuración mediante los pasos siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="c8905-144">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="c8905-145">Compruebe hello toomake de circuito de ExpressRoute seguro de que esté aprovisionado y también habilitado.</span><span class="sxs-lookup"><span data-stu-id="c8905-145">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="c8905-146">Utilice el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="c8905-146">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="c8905-147">respuesta de Hello es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c8905-147">hello response is similar toohello following example:</span></span>

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. <span data-ttu-id="c8905-148">Configurar Azure intercambio de tráfico privado para el circuito de Hola.</span><span class="sxs-lookup"><span data-stu-id="c8905-148">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="c8905-149">Asegúrese de que dispone de hello siguientes elementos antes de continuar con los pasos siguientes de hello:</span><span class="sxs-lookup"><span data-stu-id="c8905-149">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="c8905-150">/ 30 subred para el vínculo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="c8905-150">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="c8905-151">subred de Hello no debe formar parte de cualquier espacio de direcciones reservada para las redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="c8905-151">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="c8905-152">/ 30 subred para el vínculo secundario Hola.</span><span class="sxs-lookup"><span data-stu-id="c8905-152">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="c8905-153">subred de Hello no debe formar parte de cualquier espacio de direcciones reservada para las redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="c8905-153">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="c8905-154">Un tooestablish de Id. de VLAN válido este emparejamiento correctamente.</span><span class="sxs-lookup"><span data-stu-id="c8905-154">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="c8905-155">No Asegúrese de que ningún otro emparejamiento en el circuito de hello usa Hola mismo identificador de VLAN.</span><span class="sxs-lookup"><span data-stu-id="c8905-155">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="c8905-156">Número de sistema autónomo (AS) para la configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="c8905-156">AS number for peering.</span></span> <span data-ttu-id="c8905-157">Puede usar 2 bytes o 4 bytes como números AS.</span><span class="sxs-lookup"><span data-stu-id="c8905-157">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="c8905-158">Puede usar un número AS privado para esta configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="c8905-158">You can use a private AS number for this peering.</span></span> <span data-ttu-id="c8905-159">Asegúrese de que no usa 65515.</span><span class="sxs-lookup"><span data-stu-id="c8905-159">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="c8905-160">**Opcional:** un hash MD5 si elige toouse uno.</span><span class="sxs-lookup"><span data-stu-id="c8905-160">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="c8905-161">Usar hello después tooconfigure Azure privada de emparejamiento para el circuito de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c8905-161">Use hello following example tooconfigure Azure private peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="c8905-162">Si elige toouse un hash MD5, use Hola siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c8905-162">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="c8905-163">Asegúrese de especificar su número AS como ASN de configuración entre pares, no como cliente ASN.</span><span class="sxs-lookup"><span data-stu-id="c8905-163">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="c8905-164">tooview privada emparejamiento detalles de Azure</span><span class="sxs-lookup"><span data-stu-id="c8905-164">tooview Azure private peering details</span></span>

<span data-ttu-id="c8905-165">Puede obtener detalles de configuración mediante el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="c8905-165">You can get configuration details by using hello following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt
```

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="c8905-166">tooupdate configuración de emparejamiento privada de Azure</span><span class="sxs-lookup"><span data-stu-id="c8905-166">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="c8905-167">Puede actualizar cualquier parte de la configuración de hello mediante el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c8905-167">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="c8905-168">En este ejemplo, Id. de VLAN del circuito de Hola Hola se está actualizando desde too500 100.</span><span class="sxs-lookup"><span data-stu-id="c8905-168">In this example, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="c8905-169">toodelete emparejamiento privado de Azure</span><span class="sxs-lookup"><span data-stu-id="c8905-169">toodelete Azure private peering</span></span>

<span data-ttu-id="c8905-170">Puede quitar la configuración de emparejamiento ejecutando el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="c8905-170">You can remove your peering configuration by running hello following example:</span></span>

> [!WARNING]
> <span data-ttu-id="c8905-171">También debe asegurarse de que todas las redes virtuales se desvincula de hello circuito de ExpressRoute antes de ejecutar este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c8905-171">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this example.</span></span> 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="azure-public-peering"></a><span data-ttu-id="c8905-172">Configuración entre pares públicos de Azure</span><span class="sxs-lookup"><span data-stu-id="c8905-172">Azure public peering</span></span>

<span data-ttu-id="c8905-173">En esta sección le ayuda a crear, obtener, actualizar y eliminar hello Azure configuración de emparejamiento público de un circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c8905-173">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="c8905-174">toocreate pares públicos de Azure</span><span class="sxs-lookup"><span data-stu-id="c8905-174">toocreate Azure public peering</span></span>

1. <span data-ttu-id="c8905-175">Importe el módulo de PowerShell de Hola para ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c8905-175">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="c8905-176">Debe instalar Hola installer más reciente de PowerShell de [Galería de PowerShell](http://www.powershellgallery.com/) e importar módulos de Azure Resource Manager hello en la sesión de PowerShell de hello en toostart orden mediante cmdlets de ExpressRoute Hola.</span><span class="sxs-lookup"><span data-stu-id="c8905-176">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="c8905-177">Necesitará toorun PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="c8905-177">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  <span data-ttu-id="c8905-178">Importar todos los módulos de AzureRM.* hello en hello conocida el intervalo de versiones semántico de.</span><span class="sxs-lookup"><span data-stu-id="c8905-178">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="c8905-179">También puede importar un módulo seleccione dentro de hello conocida el intervalo de versiones semántico.</span><span class="sxs-lookup"><span data-stu-id="c8905-179">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
```

  <span data-ttu-id="c8905-180">Inicie sesión en la cuenta de tooyour.</span><span class="sxs-lookup"><span data-stu-id="c8905-180">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="c8905-181">Seleccione la suscripción de hello desea toocreate circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c8905-181">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="c8905-182">Crear un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c8905-182">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="c8905-183">Siga Hola instrucciones toocreate una [circuito de ExpressRoute](expressroute-howto-circuit-arm.md) y hacer que se aprovisiona proveedor de conectividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="c8905-183">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="c8905-184">Si el proveedor de conectividad ofrece servicios administrados de capa 3, puede solicitar su tooenable de proveedor de conectividad Azure privada emparejamiento para usted.</span><span class="sxs-lookup"><span data-stu-id="c8905-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="c8905-185">En ese caso, no necesitará toofollow instrucciones que se indican en las secciones siguientes se Hola.</span><span class="sxs-lookup"><span data-stu-id="c8905-185">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="c8905-186">Sin embargo, si el proveedor de conectividad no administra el enrutamiento para usted, después de crear el circuito, continuar la configuración mediante los pasos siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="c8905-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="c8905-187">Compruebe tooensure de circuito de ExpressRoute Hola está aprovisionado y también está habilitado.</span><span class="sxs-lookup"><span data-stu-id="c8905-187">Check hello ExpressRoute circuit tooensure it is provisioned and also enabled.</span></span> <span data-ttu-id="c8905-188">Utilice el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="c8905-188">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="c8905-189">respuesta de Hello es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c8905-189">hello response is similar toohello following example:</span></span>

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                      "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. <span data-ttu-id="c8905-190">Configure pares públicos de Azure para el circuito de Hola.</span><span class="sxs-lookup"><span data-stu-id="c8905-190">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="c8905-191">Asegúrese de que dispone de hello siguiente información antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="c8905-191">Make sure that you have hello following information before you proceed further.</span></span>

  * <span data-ttu-id="c8905-192">/ 30 subred para el vínculo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="c8905-192">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="c8905-193">Tiene que ser un prefijo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="c8905-193">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="c8905-194">/ 30 subred para el vínculo secundario Hola.</span><span class="sxs-lookup"><span data-stu-id="c8905-194">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="c8905-195">Tiene que ser un prefijo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="c8905-195">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="c8905-196">Un tooestablish de Id. de VLAN válido este emparejamiento correctamente.</span><span class="sxs-lookup"><span data-stu-id="c8905-196">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="c8905-197">No Asegúrese de que ningún otro emparejamiento en el circuito de hello usa Hola mismo identificador de VLAN.</span><span class="sxs-lookup"><span data-stu-id="c8905-197">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="c8905-198">Número de sistema autónomo (AS) para la configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="c8905-198">AS number for peering.</span></span> <span data-ttu-id="c8905-199">Puede usar 2 bytes o 4 bytes como números AS.</span><span class="sxs-lookup"><span data-stu-id="c8905-199">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="c8905-200">**Opcional:** un hash MD5 si elige toouse uno.</span><span class="sxs-lookup"><span data-stu-id="c8905-200">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="c8905-201">Ejecute hello siguiendo el ejemplo tooconfigure pública de emparejamiento para el circuito de Azure</span><span class="sxs-lookup"><span data-stu-id="c8905-201">Run hello following example tooconfigure Azure public peering for your circuit</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="c8905-202">Si elige toouse un hash MD5, use Hola siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c8905-202">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="c8905-203">Asegúrese de especificar su número AS como ASN de configuración entre pares, no como cliente ASN.</span><span class="sxs-lookup"><span data-stu-id="c8905-203">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="c8905-204">tooview Azure pública emparejamiento detalles</span><span class="sxs-lookup"><span data-stu-id="c8905-204">tooview Azure public peering details</span></span>

<span data-ttu-id="c8905-205">Puede obtener detalles de configuración mediante Hola siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c8905-205">You can get configuration details using hello following cmdlet:</span></span>

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="c8905-206">tooupdate configuración de interconexión pública de Azure</span><span class="sxs-lookup"><span data-stu-id="c8905-206">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="c8905-207">Puede actualizar cualquier parte de la configuración de hello mediante el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c8905-207">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="c8905-208">En este ejemplo, Id. de VLAN del circuito de Hola Hola se está actualizando desde too600 200.</span><span class="sxs-lookup"><span data-stu-id="c8905-208">In this example, hello VLAN ID of hello circuit is being updated from 200 too600.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="c8905-209">toodelete pares públicos de Azure</span><span class="sxs-lookup"><span data-stu-id="c8905-209">toodelete Azure public peering</span></span>

<span data-ttu-id="c8905-210">Puede quitar la configuración de emparejamiento ejecutando el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="c8905-210">You can remove your peering configuration by running hello following example:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="microsoft-peering"></a><span data-ttu-id="c8905-211">Emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="c8905-211">Microsoft peering</span></span>

<span data-ttu-id="c8905-212">En esta sección le ayuda a crear, obtener, actualizar y eliminar la configuración de emparejamiento de Microsoft de Hola por un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c8905-212">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c8905-213">Emparejamiento de Microsoft de circuitos ExpressRoute que estaban configurados anterior tooAugust 1, 2017 tendrá todos los prefijos de servicio implementados a través de emparejamiento de Microsoft hello, incluso si no se definen los filtros de ruta.</span><span class="sxs-lookup"><span data-stu-id="c8905-213">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="c8905-214">Emparejamiento de Microsoft de circuitos ExpressRoute configurados en o después del 1 de agosto de 2017 no tendrá todos los prefijos anunciados hasta que se conecte un filtro de ruta toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="c8905-214">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="c8905-215">Para más información, consulte [Configuración de un filtro de ruta para el emparejamiento de Microsoft](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c8905-215">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="c8905-216">emparejamiento de Microsoft toocreate</span><span class="sxs-lookup"><span data-stu-id="c8905-216">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="c8905-217">Importe el módulo de PowerShell de Hola para ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c8905-217">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="c8905-218">Debe instalar Hola installer más reciente de PowerShell de [Galería de PowerShell](http://www.powershellgallery.com/) e importar módulos de Azure Resource Manager hello en la sesión de PowerShell de hello en toostart orden mediante cmdlets de ExpressRoute Hola.</span><span class="sxs-lookup"><span data-stu-id="c8905-218">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="c8905-219">Necesitará toorun PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="c8905-219">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  <span data-ttu-id="c8905-220">Importar todos los módulos de AzureRM.* hello en hello conocida el intervalo de versiones semántico de.</span><span class="sxs-lookup"><span data-stu-id="c8905-220">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="c8905-221">También puede importar un módulo seleccione dentro de hello conocida el intervalo de versiones semántico.</span><span class="sxs-lookup"><span data-stu-id="c8905-221">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
  ```

  <span data-ttu-id="c8905-222">Inicie sesión en la cuenta de tooyour.</span><span class="sxs-lookup"><span data-stu-id="c8905-222">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="c8905-223">Seleccione la suscripción de hello desea toocreate circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c8905-223">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="c8905-224">Crear un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c8905-224">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="c8905-225">Siga Hola instrucciones toocreate una [circuito de ExpressRoute](expressroute-howto-circuit-arm.md) y hacer que se aprovisiona proveedor de conectividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="c8905-225">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="c8905-226">Si el proveedor de conectividad ofrece servicios administrados de capa 3, puede solicitar su tooenable de proveedor de conectividad Azure privada emparejamiento para usted.</span><span class="sxs-lookup"><span data-stu-id="c8905-226">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="c8905-227">En ese caso, no necesitará toofollow instrucciones que se indican en las secciones siguientes se Hola.</span><span class="sxs-lookup"><span data-stu-id="c8905-227">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="c8905-228">Sin embargo, si el proveedor de conectividad no administra el enrutamiento para usted, después de crear el circuito, continuar la configuración mediante los pasos siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="c8905-228">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="c8905-229">Compruebe hello toomake de circuito de ExpressRoute seguro de que esté aprovisionado y también habilitado.</span><span class="sxs-lookup"><span data-stu-id="c8905-229">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="c8905-230">Utilice el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="c8905-230">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="c8905-231">respuesta de Hello es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c8905-231">hello response is similar toohello following example:</span></span>

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. <span data-ttu-id="c8905-232">Configurar Microsoft emparejamiento para el circuito de Hola.</span><span class="sxs-lookup"><span data-stu-id="c8905-232">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="c8905-233">Asegúrese de que haya Hola siguiente información antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="c8905-233">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="c8905-234">/ 30 subred para el vínculo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="c8905-234">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="c8905-235">Debe ser un prefijo de IPv4 público válido que sea de su propiedad y esté registrado en un Registro regional de Internet (RIR) o un Registro de enrutamiento de Internet (IRR).</span><span class="sxs-lookup"><span data-stu-id="c8905-235">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="c8905-236">/ 30 subred para el vínculo secundario Hola.</span><span class="sxs-lookup"><span data-stu-id="c8905-236">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="c8905-237">Debe ser un prefijo de IPv4 público válido que sea de su propiedad y esté registrado en un Registro regional de Internet (RIR) o un Registro de enrutamiento de Internet (IRR).</span><span class="sxs-lookup"><span data-stu-id="c8905-237">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="c8905-238">Un tooestablish de Id. de VLAN válido este emparejamiento correctamente.</span><span class="sxs-lookup"><span data-stu-id="c8905-238">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="c8905-239">No Asegúrese de que ningún otro emparejamiento en el circuito de hello usa Hola mismo identificador de VLAN.</span><span class="sxs-lookup"><span data-stu-id="c8905-239">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="c8905-240">Número de sistema autónomo (AS) para la configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="c8905-240">AS number for peering.</span></span> <span data-ttu-id="c8905-241">Puede usar 2 bytes o 4 bytes como números AS.</span><span class="sxs-lookup"><span data-stu-id="c8905-241">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="c8905-242">Anuncian prefijos: debe proporcionar una lista de todos los prefijos piensa tooadvertise en las sesiones BGP Hola.</span><span class="sxs-lookup"><span data-stu-id="c8905-242">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="c8905-243">Se aceptan solo prefijos de direcciones IP públicas.</span><span class="sxs-lookup"><span data-stu-id="c8905-243">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="c8905-244">Si tiene previsto toosend un conjunto de prefijos, puede enviar una lista separada por comas.</span><span class="sxs-lookup"><span data-stu-id="c8905-244">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="c8905-245">Estos prefijos deben ser tooyou registrado en un RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="c8905-245">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="c8905-246">**Opcional:** cliente ASN: si es que los prefijos de publicidad que no están registrado toohello emparejamiento como número, puede especificar hello como número toowhich están registrados.</span><span class="sxs-lookup"><span data-stu-id="c8905-246">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="c8905-247">Nombre del enrutamiento del registro: Puede especificar Hola RIR / IRR en qué hello como número y los prefijos registrados.</span><span class="sxs-lookup"><span data-stu-id="c8905-247">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="c8905-248">**Opcional:** un hash MD5 si elige toouse uno.</span><span class="sxs-lookup"><span data-stu-id="c8905-248">**Optional -** An MD5 hash if you choose toouse one.</span></span>

   <span data-ttu-id="c8905-249">Usar hello siguiendo la emparejamiento de Microsoft tooconfigure de ejemplo para el circuito:</span><span class="sxs-lookup"><span data-stu-id="c8905-249">Use hello following example tooconfigure Microsoft peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="tooget-microsoft-peering-details"></a><span data-ttu-id="c8905-250">detalles de emparejamiento de Microsoft tooget</span><span class="sxs-lookup"><span data-stu-id="c8905-250">tooget Microsoft peering details</span></span>

<span data-ttu-id="c8905-251">Puede obtener detalles de configuración mediante el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="c8905-251">You can get configuration details using hello following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="c8905-252">configuración de emparejamiento de Microsoft tooupdate</span><span class="sxs-lookup"><span data-stu-id="c8905-252">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="c8905-253">Puede actualizar cualquier parte de la configuración de hello mediante el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="c8905-253">You can update any part of hello configuration using hello following example:</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="c8905-254">emparejamiento de Microsoft toodelete</span><span class="sxs-lookup"><span data-stu-id="c8905-254">toodelete Microsoft peering</span></span>

<span data-ttu-id="c8905-255">Puede quitar la configuración de intercambio de tráfico mediante la ejecución de hello siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c8905-255">You can remove your peering configuration by running hello following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a><span data-ttu-id="c8905-256">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c8905-256">Next steps</span></span>

<span data-ttu-id="c8905-257">Siguiente paso, [vincular un circuito de ExpressRoute de red virtual tooan](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="c8905-257">Next step, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

* <span data-ttu-id="c8905-258">Para más información sobre los flujos de trabajo de ExpressRoute, vea [Flujos de trabajo de ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="c8905-258">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="c8905-259">Para más información sobre el emparejamiento de circuitos, vea [Circuitos y dominios de enrutamiento de ExpressRoute](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="c8905-259">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="c8905-260">Para más información sobre redes virtuales, vea [Información general sobre redes virtuales](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c8905-260">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
