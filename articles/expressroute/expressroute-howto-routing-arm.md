---
title: "Configuración del enrutamiento (emparejamiento) de un circuito ExpressRoute: Resource Manager (Azure PowerShell) | Microsoft Docs"
description: "Este artículo le guiará por los pasos necesarios para crear y aprovisionar las configuraciones entre pares privados, públicos y de Microsoft de un circuito ExpressRoute. Este artículo también muestra cómo comprobar el estado, actualizar, o eliminar configuraciones entre pares en el circuito."
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
ms.openlocfilehash: af68955b78239832e413e1b59e033d7d3da8d599
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="12717-104">Creación y modificación del emparejamiento de un circuito ExpressRoute mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="12717-104">Create and modify peering for an ExpressRoute circuit using PowerShell</span></span>

<span data-ttu-id="12717-105">Este artículo le ayuda a crear y administrar la configuración de enrutamiento de un circuito ExpressRoute en el modelo de implementación de Resource Manager mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="12717-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in the Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="12717-106">También puede ver cómo comprobar el estado de los emparejamientos de un circuito ExpressRoute, así como el modo de actualizarlos o eliminarlos y desaprovisionarlos.</span><span class="sxs-lookup"><span data-stu-id="12717-106">You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="12717-107">Si quiere usar un método diferente para trabajar con el circuito, seleccione un artículo de la lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="12717-107">If you want to use a different method to work with your circuit, select an article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="12717-108">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="12717-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="12717-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="12717-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="12717-110">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="12717-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="12717-111">Vídeo: pares privados</span><span class="sxs-lookup"><span data-stu-id="12717-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="12717-112">Vídeo: pares públicos</span><span class="sxs-lookup"><span data-stu-id="12717-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="12717-113">Vídeo: emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="12717-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="12717-114">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="12717-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="12717-115">Requisitos previos de configuración</span><span class="sxs-lookup"><span data-stu-id="12717-115">Configuration prerequisites</span></span>

* <span data-ttu-id="12717-116">Necesitará la versión más reciente de los cmdlets de PowerShell de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="12717-116">You will need the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="12717-117">Para más información, vea [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="12717-117">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> 
* <span data-ttu-id="12717-118">Antes de comenzar la configuración, asegúrese de que ha revisado la página de [requisitos previos](expressroute-prerequisites.md), la página de [requisitos de enrutamiento](expressroute-routing.md) y la página de [flujos de trabajo](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="12717-118">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="12717-119">Tiene que tener un circuito ExpressRoute activo.</span><span class="sxs-lookup"><span data-stu-id="12717-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="12717-120">Antes de continuar, siga las instrucciones para [crear un circuito ExpressRoute](expressroute-howto-circuit-arm.md) y para que el proveedor de conectividad habilite el circuito.</span><span class="sxs-lookup"><span data-stu-id="12717-120">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="12717-121">El circuito ExpressRoute debe estar en un estado habilitado y aprovisionado para poder ejecutar los cmdlets que se describen en este artículo.</span><span class="sxs-lookup"><span data-stu-id="12717-121">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets in this article.</span></span>

<span data-ttu-id="12717-122">Estas instrucciones se aplican solo a los circuitos creados con proveedores de servicios que ofrecen servicios de conectividad de capa 2.</span><span class="sxs-lookup"><span data-stu-id="12717-122">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="12717-123">Si usa un proveedor de servicios que ofrece servicios administrados de nivel 3 (normalmente VPN IP, como MPLS), el mismo proveedor de conectividad configurará y administrará el enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="12717-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="12717-124">Actualmente no anunciamos los emparejamientos configurados por proveedores de servicios a través del Portal de administración de servicios.</span><span class="sxs-lookup"><span data-stu-id="12717-124">We currently do not advertise peerings configured by service providers through the service management portal.</span></span> <span data-ttu-id="12717-125">Se está trabajando para habilitar esta funcionalidad pronto.</span><span class="sxs-lookup"><span data-stu-id="12717-125">We are working on enabling this capability soon.</span></span> <span data-ttu-id="12717-126">Antes de configurar los emparejamientos BGP, realice las comprobaciones pertinentes con su proveedor de servicios.</span><span class="sxs-lookup"><span data-stu-id="12717-126">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="12717-127">Puede configurar una, dos o las tres configuraciones entre pares (Azure privado, Azure público y Microsoft) para un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="12717-127">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="12717-128">Puede establecer las configuraciones entre pares en cualquier orden.</span><span class="sxs-lookup"><span data-stu-id="12717-128">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="12717-129">Pero tiene que asegurarse de que completa cada configuración entre pares de una en una.</span><span class="sxs-lookup"><span data-stu-id="12717-129">However, you must make sure that you complete the configuration of each peering one at a time.</span></span> 

## <a name="azure-private-peering"></a><span data-ttu-id="12717-130">Configuración entre pares privados de Azure</span><span class="sxs-lookup"><span data-stu-id="12717-130">Azure private peering</span></span>

<span data-ttu-id="12717-131">Esta sección le ayuda a crear, obtener, actualizar y eliminar la configuración de emparejamiento privado de Azure para un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="12717-131">This section helps you create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="12717-132">Creación de un emparejamiento privado de Azure</span><span class="sxs-lookup"><span data-stu-id="12717-132">To create Azure private peering</span></span>

1. <span data-ttu-id="12717-133">Importe el módulo de PowerShell para ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="12717-133">Import the PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="12717-134">Para comenzar a usar los cmdlets de ExpressRoute, debe instalar el programa de instalación de PowerShell más reciente desde la [Galería de PowerShell](http://www.powershellgallery.com/) e importar los módulos de Azure Resource Manager en la sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="12717-134">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="12717-135">Deberá ejecutar PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="12717-135">You will need to run PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  <span data-ttu-id="12717-136">Importe todos los módulos de AzureRM.* dentro del intervalo de versiones semánticas conocidas.</span><span class="sxs-lookup"><span data-stu-id="12717-136">Import all of the AzureRM.* modules within the known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="12717-137">También puede importar un módulo determinado en dicho intervalo.</span><span class="sxs-lookup"><span data-stu-id="12717-137">You can also just import a select module within the known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network 
  ```

  <span data-ttu-id="12717-138">Inicie sesión en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="12717-138">Sign in to your account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="12717-139">Seleccione la suscripción en la que desea crear un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="12717-139">Select the subscription you want to create ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="12717-140">Crear un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="12717-140">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="12717-141">Siga las instrucciones para crear un [circuito ExpressRoute](expressroute-howto-circuit-arm.md) y habilite su aprovisionamiento a través del proveedor de conectividad.</span><span class="sxs-lookup"><span data-stu-id="12717-141">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="12717-142">Si su proveedor de conectividad ofrece servicios administrados de nivel 3, puede solicitarle que habilite la configuración entre pares privados de Azure.</span><span class="sxs-lookup"><span data-stu-id="12717-142">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="12717-143">En ese caso, no necesita seguir las instrucciones que aparecen en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="12717-143">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="12717-144">Sin embargo, si el proveedor de conectividad no administra el enrutamiento por usted, después de crear el circuito, continúe con la configuración mediante los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="12717-144">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="12717-145">Compruebe el circuito ExpressRoute para asegurarse de que está aprovisionado y también habilitado.</span><span class="sxs-lookup"><span data-stu-id="12717-145">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="12717-146">Utilice el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="12717-146">Use the following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="12717-147">La respuesta es similar al siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="12717-147">The response is similar to the following example:</span></span>

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
4. <span data-ttu-id="12717-148">Establecimiento de la configuración entre pares privados de Azure para el circuito.</span><span class="sxs-lookup"><span data-stu-id="12717-148">Configure Azure private peering for the circuit.</span></span> <span data-ttu-id="12717-149">Asegúrese de que tiene los elementos siguientes antes de continuar con los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="12717-149">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="12717-150">Una subred /30 para el vínculo principal.</span><span class="sxs-lookup"><span data-stu-id="12717-150">A /30 subnet for the primary link.</span></span> <span data-ttu-id="12717-151">La subred no debe ser parte de ningún espacio de direcciones reservado para redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="12717-151">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="12717-152">Una subred /30 para el vínculo secundario.</span><span class="sxs-lookup"><span data-stu-id="12717-152">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="12717-153">La subred no debe ser parte de ningún espacio de direcciones reservado para redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="12717-153">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="12717-154">Un identificador VLAN válido para establecer esta configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="12717-154">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="12717-155">Asegúrese de que ninguna otra configuración entre pares en el circuito usa el mismo identificador de VLAN.</span><span class="sxs-lookup"><span data-stu-id="12717-155">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="12717-156">Número de sistema autónomo (AS) para la configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="12717-156">AS number for peering.</span></span> <span data-ttu-id="12717-157">Puede usar 2 bytes o 4 bytes como números AS.</span><span class="sxs-lookup"><span data-stu-id="12717-157">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="12717-158">Puede usar un número AS privado para esta configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="12717-158">You can use a private AS number for this peering.</span></span> <span data-ttu-id="12717-159">Asegúrese de que no usa 65515.</span><span class="sxs-lookup"><span data-stu-id="12717-159">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="12717-160">**Opcional:** un hash MD5 si elige usar uno.</span><span class="sxs-lookup"><span data-stu-id="12717-160">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="12717-161">Use el ejemplo siguiente para configurar el emparejamiento privado de Azure para su circuito:</span><span class="sxs-lookup"><span data-stu-id="12717-161">Use the following example to configure Azure private peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="12717-162">Si decide usar un hash MD5, use el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="12717-162">If you choose to use an MD5 hash, use the following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="12717-163">Asegúrese de especificar su número AS como ASN de configuración entre pares, no como cliente ASN.</span><span class="sxs-lookup"><span data-stu-id="12717-163">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="12717-164">Visualización de los detalles del emparejamiento privado</span><span class="sxs-lookup"><span data-stu-id="12717-164">To view Azure private peering details</span></span>

<span data-ttu-id="12717-165">Puede obtener detalles sobre la configuración mediante el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="12717-165">You can get configuration details by using the following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt
```

### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="12717-166">Actualización del establecimiento de configuración del emparejamiento privado de Azure</span><span class="sxs-lookup"><span data-stu-id="12717-166">To update Azure private peering configuration</span></span>

<span data-ttu-id="12717-167">Puede actualizar cualquier parte de la configuración mediante el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="12717-167">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="12717-168">En este ejemplo, se va a actualizar el identificador de VLAN del circuito de 100 a 500.</span><span class="sxs-lookup"><span data-stu-id="12717-168">In this example, the VLAN ID of the circuit is being updated from 100 to 500.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="12717-169">Eliminación del emparejamiento privado de Azure</span><span class="sxs-lookup"><span data-stu-id="12717-169">To delete Azure private peering</span></span>

<span data-ttu-id="12717-170">Puede quitar la configuración de emparejamiento mediante la ejecución del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="12717-170">You can remove your peering configuration by running the following example:</span></span>

> [!WARNING]
> <span data-ttu-id="12717-171">Debe asegurarse de que todas las redes virtuales estén desvinculadas del circuito ExpressRoute antes de ejecutar este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="12717-171">You must ensure that all virtual networks are unlinked from the ExpressRoute circuit before running this example.</span></span> 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="azure-public-peering"></a><span data-ttu-id="12717-172">Configuración entre pares públicos de Azure</span><span class="sxs-lookup"><span data-stu-id="12717-172">Azure public peering</span></span>

<span data-ttu-id="12717-173">Esta sección le ayuda a crear, obtener, actualizar y eliminar la configuración de emparejamiento público de Azure para un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="12717-173">This section helps you create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="12717-174">Creación de un emparejamiento público de Azure</span><span class="sxs-lookup"><span data-stu-id="12717-174">To create Azure public peering</span></span>

1. <span data-ttu-id="12717-175">Importe el módulo de PowerShell para ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="12717-175">Import the PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="12717-176">Para comenzar a usar los cmdlets de ExpressRoute, debe instalar el programa de instalación de PowerShell más reciente desde la [Galería de PowerShell](http://www.powershellgallery.com/) e importar los módulos de Azure Resource Manager en la sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="12717-176">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="12717-177">Deberá ejecutar PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="12717-177">You will need to run PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  <span data-ttu-id="12717-178">Importe todos los módulos de AzureRM.* dentro del intervalo de versiones semánticas conocidas.</span><span class="sxs-lookup"><span data-stu-id="12717-178">Import all of the AzureRM.* modules within the known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="12717-179">También puede importar un módulo determinado en dicho intervalo.</span><span class="sxs-lookup"><span data-stu-id="12717-179">You can also just import a select module within the known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
```

  <span data-ttu-id="12717-180">Inicie sesión en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="12717-180">Sign in to your account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="12717-181">Seleccione la suscripción en la que desea crear un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="12717-181">Select the subscription you want to create ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="12717-182">Crear un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="12717-182">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="12717-183">Siga las instrucciones para crear un [circuito ExpressRoute](expressroute-howto-circuit-arm.md) y habilite su aprovisionamiento a través del proveedor de conectividad.</span><span class="sxs-lookup"><span data-stu-id="12717-183">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="12717-184">Si su proveedor de conectividad ofrece servicios administrados de nivel 3, puede solicitarle que habilite la configuración entre pares privados de Azure.</span><span class="sxs-lookup"><span data-stu-id="12717-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="12717-185">En ese caso, no necesita seguir las instrucciones que aparecen en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="12717-185">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="12717-186">Sin embargo, si el proveedor de conectividad no administra el enrutamiento por usted, después de crear el circuito, continúe con la configuración mediante los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="12717-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="12717-187">Compruebe el circuito ExpressRoute para asegurarse de que está aprovisionado y también habilitado.</span><span class="sxs-lookup"><span data-stu-id="12717-187">Check the ExpressRoute circuit to ensure it is provisioned and also enabled.</span></span> <span data-ttu-id="12717-188">Utilice el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="12717-188">Use the following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="12717-189">La respuesta es similar al siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="12717-189">The response is similar to the following example:</span></span>

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
4. <span data-ttu-id="12717-190">Establezca la configuración del emparejamiento publico de Azure para el circuito.</span><span class="sxs-lookup"><span data-stu-id="12717-190">Configure Azure public peering for the circuit.</span></span> <span data-ttu-id="12717-191">Asegúrese de que tiene la siguiente información antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="12717-191">Make sure that you have the following information before you proceed further.</span></span>

  * <span data-ttu-id="12717-192">Una subred /30 para el vínculo principal.</span><span class="sxs-lookup"><span data-stu-id="12717-192">A /30 subnet for the primary link.</span></span> <span data-ttu-id="12717-193">Tiene que ser un prefijo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="12717-193">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="12717-194">Una subred /30 para el vínculo secundario.</span><span class="sxs-lookup"><span data-stu-id="12717-194">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="12717-195">Tiene que ser un prefijo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="12717-195">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="12717-196">Un identificador VLAN válido para establecer esta configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="12717-196">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="12717-197">Asegúrese de que ninguna otra configuración entre pares en el circuito usa el mismo identificador de VLAN.</span><span class="sxs-lookup"><span data-stu-id="12717-197">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="12717-198">Número de sistema autónomo (AS) para la configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="12717-198">AS number for peering.</span></span> <span data-ttu-id="12717-199">Puede usar 2 bytes o 4 bytes como números AS.</span><span class="sxs-lookup"><span data-stu-id="12717-199">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="12717-200">**Opcional:** un hash MD5 si elige usar uno.</span><span class="sxs-lookup"><span data-stu-id="12717-200">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="12717-201">Ejecute el siguiente ejemplo para configurar el emparejamiento público de Azure para su circuito:</span><span class="sxs-lookup"><span data-stu-id="12717-201">Run the following example to configure Azure public peering for your circuit</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="12717-202">Si decide usar un hash MD5, use el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="12717-202">If you choose to use an MD5 hash, use the following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="12717-203">Asegúrese de especificar su número AS como ASN de configuración entre pares, no como cliente ASN.</span><span class="sxs-lookup"><span data-stu-id="12717-203">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="12717-204">Visualización de detalles de un emparejamiento público de Azure</span><span class="sxs-lookup"><span data-stu-id="12717-204">To view Azure public peering details</span></span>

<span data-ttu-id="12717-205">Puede obtener detalles sobre la configuración mediante el siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="12717-205">You can get configuration details using the following cmdlet:</span></span>

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="12717-206">Actualización del establecimiento de configuración del emparejamiento público de Azure</span><span class="sxs-lookup"><span data-stu-id="12717-206">To update Azure public peering configuration</span></span>

<span data-ttu-id="12717-207">Puede actualizar cualquier parte de la configuración mediante el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="12717-207">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="12717-208">En este ejemplo, se va a actualizar el identificador de VLAN del circuito de 200 a 600.</span><span class="sxs-lookup"><span data-stu-id="12717-208">In this example, the VLAN ID of the circuit is being updated from 200 to 600.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="12717-209">Eliminación del emparejamiento público de Azure</span><span class="sxs-lookup"><span data-stu-id="12717-209">To delete Azure public peering</span></span>

<span data-ttu-id="12717-210">Puede quitar la configuración de emparejamiento mediante la ejecución del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="12717-210">You can remove your peering configuration by running the following example:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="microsoft-peering"></a><span data-ttu-id="12717-211">Emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="12717-211">Microsoft peering</span></span>

<span data-ttu-id="12717-212">Esta sección le ayuda a crear, obtener, actualizar y eliminar la configuración de emparejamiento de Microsoft para un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="12717-212">This section helps you create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="12717-213">Se anunciarán todos los prefijos de servicio para el emparejamiento de Microsoft de los circuitos ExpressRoute que se configuraron antes del 1 de agosto de 2017, incluso si no se definen filtros de ruta.</span><span class="sxs-lookup"><span data-stu-id="12717-213">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through the Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="12717-214">No se anunciará ningún prefijo para el emparejamiento de Microsoft de los circuitos ExpressRoute que se configuraron el 1 de agosto de 2017 o con posterioridad, hasta que se asocie un filtro de ruta al circuito.</span><span class="sxs-lookup"><span data-stu-id="12717-214">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span> <span data-ttu-id="12717-215">Para más información, consulte [Configuración de un filtro de ruta para el emparejamiento de Microsoft](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="12717-215">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="12717-216">Creación del emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="12717-216">To create Microsoft peering</span></span>

1. <span data-ttu-id="12717-217">Importe el módulo de PowerShell para ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="12717-217">Import the PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="12717-218">Para comenzar a usar los cmdlets de ExpressRoute, debe instalar el programa de instalación de PowerShell más reciente desde la [Galería de PowerShell](http://www.powershellgallery.com/) e importar los módulos de Azure Resource Manager en la sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="12717-218">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="12717-219">Deberá ejecutar PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="12717-219">You will need to run PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  <span data-ttu-id="12717-220">Importe todos los módulos de AzureRM.* dentro del intervalo de versiones semánticas conocidas.</span><span class="sxs-lookup"><span data-stu-id="12717-220">Import all of the AzureRM.* modules within the known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="12717-221">También puede importar un módulo determinado en dicho intervalo.</span><span class="sxs-lookup"><span data-stu-id="12717-221">You can also just import a select module within the known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
  ```

  <span data-ttu-id="12717-222">Inicie sesión en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="12717-222">Sign in to your account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="12717-223">Seleccione la suscripción en la que desea crear un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="12717-223">Select the subscription you want to create ExpressRoute circuit.</span></span>

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="12717-224">Crear un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="12717-224">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="12717-225">Siga las instrucciones para crear un [circuito ExpressRoute](expressroute-howto-circuit-arm.md) y habilite su aprovisionamiento a través del proveedor de conectividad.</span><span class="sxs-lookup"><span data-stu-id="12717-225">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="12717-226">Si su proveedor de conectividad ofrece servicios administrados de nivel 3, puede solicitarle que habilite la configuración entre pares privados de Azure.</span><span class="sxs-lookup"><span data-stu-id="12717-226">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="12717-227">En ese caso, no necesita seguir las instrucciones que aparecen en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="12717-227">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="12717-228">Sin embargo, si el proveedor de conectividad no administra el enrutamiento por usted, después de crear el circuito, continúe con la configuración mediante los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="12717-228">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="12717-229">Compruebe el circuito ExpressRoute para asegurarse de que está aprovisionado y también habilitado.</span><span class="sxs-lookup"><span data-stu-id="12717-229">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="12717-230">Utilice el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="12717-230">Use the following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="12717-231">La respuesta es similar al siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="12717-231">The response is similar to the following example:</span></span>

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
4. <span data-ttu-id="12717-232">Establezca la configuración del emparejamiento de Microsoft para el circuito.</span><span class="sxs-lookup"><span data-stu-id="12717-232">Configure Microsoft peering for the circuit.</span></span> <span data-ttu-id="12717-233">Asegúrese de que tiene la siguiente información antes de empezar:</span><span class="sxs-lookup"><span data-stu-id="12717-233">Make sure that you have the following information before you proceed.</span></span>

  * <span data-ttu-id="12717-234">Una subred /30 para el vínculo principal.</span><span class="sxs-lookup"><span data-stu-id="12717-234">A /30 subnet for the primary link.</span></span> <span data-ttu-id="12717-235">Debe ser un prefijo de IPv4 público válido que sea de su propiedad y esté registrado en un Registro regional de Internet (RIR) o un Registro de enrutamiento de Internet (IRR).</span><span class="sxs-lookup"><span data-stu-id="12717-235">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="12717-236">Una subred /30 para el vínculo secundario.</span><span class="sxs-lookup"><span data-stu-id="12717-236">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="12717-237">Debe ser un prefijo de IPv4 público válido que sea de su propiedad y esté registrado en un Registro regional de Internet (RIR) o un Registro de enrutamiento de Internet (IRR).</span><span class="sxs-lookup"><span data-stu-id="12717-237">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="12717-238">Un identificador VLAN válido para establecer esta configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="12717-238">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="12717-239">Asegúrese de que ninguna otra configuración entre pares en el circuito usa el mismo identificador de VLAN.</span><span class="sxs-lookup"><span data-stu-id="12717-239">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="12717-240">Número de sistema autónomo (AS) para la configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="12717-240">AS number for peering.</span></span> <span data-ttu-id="12717-241">Puede usar 2 bytes o 4 bytes como números AS.</span><span class="sxs-lookup"><span data-stu-id="12717-241">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="12717-242">Prefijos anunciados: tiene que proporcionar una lista de todos los prefijos que planea anunciar en la sesión BGP.</span><span class="sxs-lookup"><span data-stu-id="12717-242">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="12717-243">Se aceptan solo prefijos de direcciones IP públicas.</span><span class="sxs-lookup"><span data-stu-id="12717-243">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="12717-244">Si tiene pensado enviar un conjunto de prefijos, puede enviar una lista separada por comas.</span><span class="sxs-lookup"><span data-stu-id="12717-244">If you plan to send a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="12717-245">Estos prefijos tienen que estar registrados a su nombre en un Registro regional de Internet (RIR) o un Registro de enrutamiento de Internet (IRR).</span><span class="sxs-lookup"><span data-stu-id="12717-245">These prefixes must be registered to you in an RIR / IRR.</span></span>
  * <span data-ttu-id="12717-246">**Opcional:** Cliente ASN: si los prefijos anunciados no están registrados en el número AS de emparejamiento, puede especificar el número de AS en el que están registrados.</span><span class="sxs-lookup"><span data-stu-id="12717-246">**Optional -** Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span>
  * <span data-ttu-id="12717-247">Nombre del enrutamiento del Registro: puede especificar el RIR o TIR en el que están registrados el número AS y los prefijos.</span><span class="sxs-lookup"><span data-stu-id="12717-247">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="12717-248">**Opcional:** un hash MD5 si elige usar uno.</span><span class="sxs-lookup"><span data-stu-id="12717-248">**Optional -** An MD5 hash if you choose to use one.</span></span>

   <span data-ttu-id="12717-249">Use el ejemplo siguiente para configurar el emparejamiento de Microsoft para el circuito:</span><span class="sxs-lookup"><span data-stu-id="12717-249">Use the following example to configure Microsoft peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="to-get-microsoft-peering-details"></a><span data-ttu-id="12717-250">Obtención de detalles del emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="12717-250">To get Microsoft peering details</span></span>

<span data-ttu-id="12717-251">Puede obtener detalles sobre la configuración mediante el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="12717-251">You can get configuration details using the following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="12717-252">Actualización de la configuración de emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="12717-252">To update Microsoft peering configuration</span></span>

<span data-ttu-id="12717-253">Puede actualizar cualquier parte de la configuración mediante el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="12717-253">You can update any part of the configuration using the following example:</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="12717-254">Eliminación del emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="12717-254">To delete Microsoft peering</span></span>

<span data-ttu-id="12717-255">Puede quitar la configuración de emparejamiento ejecutando el siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="12717-255">You can remove your peering configuration by running the following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a><span data-ttu-id="12717-256">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="12717-256">Next steps</span></span>

<span data-ttu-id="12717-257">Siguiente paso, [Vinculación de redes virtuales a circuitos ExpressRoute](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="12717-257">Next step, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

* <span data-ttu-id="12717-258">Para más información sobre los flujos de trabajo de ExpressRoute, vea [Flujos de trabajo de ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="12717-258">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="12717-259">Para más información sobre el emparejamiento de circuitos, vea [Circuitos y dominios de enrutamiento de ExpressRoute](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="12717-259">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="12717-260">Para más información sobre redes virtuales, vea [Información general sobre redes virtuales](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="12717-260">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
