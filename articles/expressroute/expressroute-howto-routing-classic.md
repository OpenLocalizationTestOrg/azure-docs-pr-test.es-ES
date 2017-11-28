---
title: "¿Cómo tooconfigure enrutamiento (emparejamiento) por un circuito ExpressRoute: Azure: clásico | Documentos de Microsoft"
description: "En este artículo le guiará por los pasos de Hola para crear y aprovisionamiento Hola privado, público y emparejamiento de Microsoft de un circuito de ExpressRoute. Este artículo también muestra cómo toocheck estado de hello, actualizar o eliminar emparejamientos para el circuito."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: a4bd39d2-373a-467a-8b06-36cfcc1027d2
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: dc5bcc4b86c3bc965a88281b6c2a660f3bc58eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a><span data-ttu-id="82dd9-104">Creación y modificación del emparejamiento de un circuito ExpressRoute (clásica)</span><span class="sxs-lookup"><span data-stu-id="82dd9-104">Create and modify peering for an ExpressRoute circuit (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="82dd9-105">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="82dd9-105">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="82dd9-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="82dd9-106">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="82dd9-107">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="82dd9-107">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="82dd9-108">Vídeo: pares privados</span><span class="sxs-lookup"><span data-stu-id="82dd9-108">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="82dd9-109">Vídeo: pares públicos</span><span class="sxs-lookup"><span data-stu-id="82dd9-109">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="82dd9-110">Vídeo: emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="82dd9-110">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="82dd9-111">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="82dd9-111">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

<span data-ttu-id="82dd9-112">Este artículo le guía a través de hello pasos toocreate y administrar la configuración de enrutamiento para un circuito de ExpressRoute con el modelo de implementación clásica de hello y PowerShell.</span><span class="sxs-lookup"><span data-stu-id="82dd9-112">This article walks you through hello steps toocreate and manage routing configuration for an ExpressRoute circuit using PowerShell and hello classic deployment model.</span></span> <span data-ttu-id="82dd9-113">estos pasos Hello también le mostrará cómo actualizar, estado de hello toocheck, o eliminar y desaprovisionar los emparejamientos de un circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="82dd9-113">hello steps below will also show you how toocheck hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="82dd9-114">**Información sobre los modelos de implementación de Azure**</span><span class="sxs-lookup"><span data-stu-id="82dd9-114">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]


## <a name="configuration-prerequisites"></a><span data-ttu-id="82dd9-115">Requisitos previos de configuración</span><span class="sxs-lookup"><span data-stu-id="82dd9-115">Configuration prerequisites</span></span>
* <span data-ttu-id="82dd9-116">Necesitará la versión más reciente de Hola de hello cmdlets de PowerShell de administración de servicio de Azure (SM).</span><span class="sxs-lookup"><span data-stu-id="82dd9-116">You will need hello latest version of hello Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="82dd9-117">Para obtener más información, consulte [Introducción a los cmdlets de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="82dd9-117">For more information, see [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="82dd9-118">Asegúrese de que ha revisado hello [requisitos previos](expressroute-prerequisites.md) página hello [requisitos de enrutamiento](expressroute-routing.md) hello y página [flujos de trabajo](expressroute-workflows.md) página antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="82dd9-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="82dd9-119">Tiene que tener un circuito ExpressRoute activo.</span><span class="sxs-lookup"><span data-stu-id="82dd9-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="82dd9-120">Siga las instrucciones de hello demasiado[crear un circuito ExpressRoute](expressroute-howto-circuit-classic.md) y tener circuito de hello habilitada por el proveedor de conectividad antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="82dd9-120">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="82dd9-121">Hola circuito de ExpressRoute debe estar en un estado habilitado y aprovisionado para usted toobe toorun capaz de hello cmdlets que se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="82dd9-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets described below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="82dd9-122">Estas instrucciones aplican solo toocircuits creado con proveedores de servicios que ofrece servicios de conectividad de nivel 2.</span><span class="sxs-lookup"><span data-stu-id="82dd9-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="82dd9-123">Si usa un proveedor de servicios que ofrece servicios administrados de nivel 3 (normalmente IPVPN, como MPLS), el mismo proveedor de conectividad configurará y administrará el enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="82dd9-123">If you are using a service provider offering managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

<span data-ttu-id="82dd9-124">Puede configurar una, dos o las tres configuraciones entre pares (Azure privado, Azure público y Microsoft) para un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="82dd9-124">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="82dd9-125">Puede establecer las configuraciones entre pares en cualquier orden.</span><span class="sxs-lookup"><span data-stu-id="82dd9-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="82dd9-126">Sin embargo, debe asegurarse de completar configuración de Hola de cada uno de ellos emparejamiento a la vez.</span><span class="sxs-lookup"><span data-stu-id="82dd9-126">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>


### <a name="log-in-tooyour-azure-account-and-select-a-subscription"></a><span data-ttu-id="82dd9-127">Inicie sesión en tooyour cuenta de Azure y seleccione una suscripción</span><span class="sxs-lookup"><span data-stu-id="82dd9-127">Log in tooyour Azure account and select a subscription</span></span>
1. <span data-ttu-id="82dd9-128">Abra la consola de PowerShell con derechos elevados y conectar con tooyour cuenta.</span><span class="sxs-lookup"><span data-stu-id="82dd9-128">Open your PowerShell console with elevated rights and connect tooyour account.</span></span> <span data-ttu-id="82dd9-129">Usar hello después toohelp de ejemplo que se conecta:</span><span class="sxs-lookup"><span data-stu-id="82dd9-129">Use hello following example toohelp you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="82dd9-130">Compruebe las suscripciones de hello para la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="82dd9-130">Check hello subscriptions for hello account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="82dd9-131">Si tiene más de una suscripción, seleccione Hola suscripción que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="82dd9-131">If you have more than one subscription, select hello subscription that you want toouse.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="82dd9-132">A continuación, usar hello siguiente cmdlet tooadd su tooPowerShell de suscripción de Azure para el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="82dd9-132">Next, use hello following cmdlet tooadd your Azure subscription tooPowerShell for hello classic deployment model.</span></span>

        Add-AzureAccount


## <a name="azure-private-peering"></a><span data-ttu-id="82dd9-133">Configuración entre pares privados de Azure</span><span class="sxs-lookup"><span data-stu-id="82dd9-133">Azure private peering</span></span>
<span data-ttu-id="82dd9-134">Esta sección proporciona instrucciones sobre cómo toocreate, obtener, actualizar y eliminar hello Azure configuración privada de emparejamiento de un circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="82dd9-134">This section provides instructions on how toocreate, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="82dd9-135">toocreate emparejamiento privado de Azure</span><span class="sxs-lookup"><span data-stu-id="82dd9-135">toocreate Azure private peering</span></span>
1. <span data-ttu-id="82dd9-136">**Importe el módulo de PowerShell de Hola para ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="82dd9-136">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="82dd9-137">Debe importar los módulos de Azure y ExpressRoute de hello en la sesión de PowerShell de hello en toostart orden mediante cmdlets de ExpressRoute Hola.</span><span class="sxs-lookup"><span data-stu-id="82dd9-137">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="82dd9-138">Siguiente ejecución Hola comandos de módulos de Azure y ExpressRoute hello tooimport en la sesión de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="82dd9-138">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="82dd9-139">**Creación de un circuito ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="82dd9-139">**Create an ExpressRoute circuit.**</span></span>
   
    <span data-ttu-id="82dd9-140">Siga Hola instrucciones toocreate una [circuito de ExpressRoute](expressroute-howto-circuit-classic.md) y hacer que se aprovisiona proveedor de conectividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="82dd9-140">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="82dd9-141">Si el proveedor de conectividad ofrece servicios administrados de capa 3, puede solicitar su tooenable de proveedor de conectividad Azure privada emparejamiento para usted.</span><span class="sxs-lookup"><span data-stu-id="82dd9-141">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="82dd9-142">En ese caso, no necesitará toofollow instrucciones que se indican en las secciones siguientes se Hola.</span><span class="sxs-lookup"><span data-stu-id="82dd9-142">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="82dd9-143">Sin embargo, si el proveedor de conectividad no administra el enrutamiento para usted, después de crear el circuito, siga estas instrucciones Hola.</span><span class="sxs-lookup"><span data-stu-id="82dd9-143">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span> 
3. <span data-ttu-id="82dd9-144">**Compruebe tooensure de circuito de ExpressRoute Hola se aprovisiona.**</span><span class="sxs-lookup"><span data-stu-id="82dd9-144">**Check hello ExpressRoute circuit tooensure it is provisioned.**</span></span>
   
    <span data-ttu-id="82dd9-145">En primer lugar debe comprobar toosee si Hola circuito de ExpressRoute se aprovisionan y también habilitada.</span><span class="sxs-lookup"><span data-stu-id="82dd9-145">You must first check toosee if hello ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="82dd9-146">Vea el ejemplo de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="82dd9-146">See hello example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="82dd9-147">Asegúrese de que el circuito de hello muestra como aprovisionado y habilitado.</span><span class="sxs-lookup"><span data-stu-id="82dd9-147">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="82dd9-148">Si no es así, trabajar con su tooget de proveedor de conectividad el circuito toohello necesario al estado y.</span><span class="sxs-lookup"><span data-stu-id="82dd9-148">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="82dd9-149">**Configurar Azure intercambio de tráfico privado para el circuito de Hola.**</span><span class="sxs-lookup"><span data-stu-id="82dd9-149">**Configure Azure private peering for hello circuit.**</span></span>
   
    <span data-ttu-id="82dd9-150">Asegúrese de que dispone de hello siguientes elementos antes de continuar con los pasos siguientes de hello:</span><span class="sxs-lookup"><span data-stu-id="82dd9-150">Make sure that you have hello following items before you proceed with hello next steps:</span></span>
   
   * <span data-ttu-id="82dd9-151">/ 30 subred para el vínculo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="82dd9-151">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="82dd9-152">No debe ser parte de ningún espacio de direcciones reservado para redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="82dd9-152">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="82dd9-153">/ 30 subred para el vínculo secundario Hola.</span><span class="sxs-lookup"><span data-stu-id="82dd9-153">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="82dd9-154">No debe ser parte de ningún espacio de direcciones reservado para redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="82dd9-154">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="82dd9-155">Un tooestablish de Id. de VLAN válido este emparejamiento correctamente.</span><span class="sxs-lookup"><span data-stu-id="82dd9-155">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="82dd9-156">No Asegúrese de que ningún otro emparejamiento en el circuito de hello usa Hola mismo identificador de VLAN.</span><span class="sxs-lookup"><span data-stu-id="82dd9-156">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="82dd9-157">Número de sistema autónomo (AS) para la configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="82dd9-157">AS number for peering.</span></span> <span data-ttu-id="82dd9-158">Puede usar 2 bytes o 4 bytes como números AS.</span><span class="sxs-lookup"><span data-stu-id="82dd9-158">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="82dd9-159">Puede usar un número AS privado para esta configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="82dd9-159">You can use a private AS number for this peering.</span></span> <span data-ttu-id="82dd9-160">Asegúrese de que no usa 65515.</span><span class="sxs-lookup"><span data-stu-id="82dd9-160">Ensure that you are not using 65515.</span></span>
   * <span data-ttu-id="82dd9-161">Hash MD5 si elige toouse uno.</span><span class="sxs-lookup"><span data-stu-id="82dd9-161">An MD5 hash if you choose toouse one.</span></span> <span data-ttu-id="82dd9-162">**Esto es opcional**.</span><span class="sxs-lookup"><span data-stu-id="82dd9-162">**This is optional**.</span></span>
     
    <span data-ttu-id="82dd9-163">Puede ejecutar Hola después tooconfigure cmdlet Azure intercambio de tráfico privado para el circuito.</span><span class="sxs-lookup"><span data-stu-id="82dd9-163">You can run hello following cmdlet tooconfigure Azure private peering for your circuit.</span></span>
     
        <span data-ttu-id="82dd9-164">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span><span class="sxs-lookup"><span data-stu-id="82dd9-164">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span></span>
     
    <span data-ttu-id="82dd9-165">Puede utilizar la siguiente cmdlet de hello si elige toouse un hash MD5.</span><span class="sxs-lookup"><span data-stu-id="82dd9-165">You can use hello cmdlet below if you choose toouse an MD5 hash.</span></span>
     
        <span data-ttu-id="82dd9-166">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="82dd9-166">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="82dd9-167">Asegúrese de especificar su número AS como ASN de configuración entre pares, no como cliente ASN.</span><span class="sxs-lookup"><span data-stu-id="82dd9-167">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
     > 
     > 

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="82dd9-168">tooview privada emparejamiento detalles de Azure</span><span class="sxs-lookup"><span data-stu-id="82dd9-168">tooview Azure private peering details</span></span>
<span data-ttu-id="82dd9-169">Puede obtener detalles de configuración mediante el siguiente cmdlet de Hola</span><span class="sxs-lookup"><span data-stu-id="82dd9-169">You can get configuration details using hello following cmdlet</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100


### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="82dd9-170">tooupdate configuración de emparejamiento privada de Azure</span><span class="sxs-lookup"><span data-stu-id="82dd9-170">tooupdate Azure private peering configuration</span></span>
<span data-ttu-id="82dd9-171">Puede actualizar cualquier parte de configuración de hello mediante Hola siguiente cmdlet.</span><span class="sxs-lookup"><span data-stu-id="82dd9-171">You can update any part of hello configuration using hello following cmdlet.</span></span> <span data-ttu-id="82dd9-172">En el ejemplo de Hola a continuación, Id. de VLAN del circuito de Hola Hola se está actualizando desde too500 100.</span><span class="sxs-lookup"><span data-stu-id="82dd9-172">In hello example below, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="82dd9-173">toodelete emparejamiento privado de Azure</span><span class="sxs-lookup"><span data-stu-id="82dd9-173">toodelete Azure private peering</span></span>
<span data-ttu-id="82dd9-174">Puede quitar la configuración de intercambio de tráfico mediante la ejecución de hello siguiente cmdlet.</span><span class="sxs-lookup"><span data-stu-id="82dd9-174">You can remove your peering configuration by running hello following cmdlet.</span></span>

> [!WARNING]
> <span data-ttu-id="82dd9-175">También debe asegurarse de que todas las redes virtuales se desvincula de hello circuito de ExpressRoute antes de ejecutar este cmdlet.</span><span class="sxs-lookup"><span data-stu-id="82dd9-175">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this cmdlet.</span></span> 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a><span data-ttu-id="82dd9-176">Configuración entre pares públicos de Azure</span><span class="sxs-lookup"><span data-stu-id="82dd9-176">Azure public peering</span></span>
<span data-ttu-id="82dd9-177">Esta sección proporciona instrucciones sobre cómo toocreate, obtener, actualizar y eliminar hello Azure configuración de emparejamiento público de un circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="82dd9-177">This section provides instructions on how toocreate, get, update and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="82dd9-178">toocreate pares públicos de Azure</span><span class="sxs-lookup"><span data-stu-id="82dd9-178">toocreate Azure public peering</span></span>
1. <span data-ttu-id="82dd9-179">**Importe el módulo de PowerShell de Hola para ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="82dd9-179">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="82dd9-180">Debe importar los módulos de Azure y ExpressRoute de hello en la sesión de PowerShell de hello en toostart orden mediante cmdlets de ExpressRoute Hola.</span><span class="sxs-lookup"><span data-stu-id="82dd9-180">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="82dd9-181">Siguiente ejecución Hola comandos de módulos de Azure y ExpressRoute hello tooimport en la sesión de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="82dd9-181">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span> 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="82dd9-182">**Creación de un circuito ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="82dd9-182">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="82dd9-183">Siga Hola instrucciones toocreate una [circuito de ExpressRoute](expressroute-howto-circuit-classic.md) y hacer que se aprovisiona proveedor de conectividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="82dd9-183">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="82dd9-184">Si el proveedor de conectividad ofrece servicios administrados de capa 3, puede solicitar su tooenable de proveedor de conectividad Azure pública de emparejamiento para usted.</span><span class="sxs-lookup"><span data-stu-id="82dd9-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure public peering for you.</span></span> <span data-ttu-id="82dd9-185">En ese caso, no necesitará toofollow instrucciones que se indican en las secciones siguientes se Hola.</span><span class="sxs-lookup"><span data-stu-id="82dd9-185">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="82dd9-186">Sin embargo, si el proveedor de conectividad no administra el enrutamiento para usted, después de crear el circuito, siga estas instrucciones Hola.</span><span class="sxs-lookup"><span data-stu-id="82dd9-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span>
3. <span data-ttu-id="82dd9-187">**Compruebe tooensure de circuito de ExpressRoute se aprovisiona**</span><span class="sxs-lookup"><span data-stu-id="82dd9-187">**Check ExpressRoute circuit tooensure it is provisioned**</span></span>
   
    <span data-ttu-id="82dd9-188">En primer lugar debe comprobar toosee si Hola circuito de ExpressRoute se aprovisionan y también habilitada.</span><span class="sxs-lookup"><span data-stu-id="82dd9-188">You must first check toosee if hello ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="82dd9-189">Vea el ejemplo de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="82dd9-189">See hello example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="82dd9-190">Asegúrese de que el circuito de hello muestra como aprovisionado y habilitado.</span><span class="sxs-lookup"><span data-stu-id="82dd9-190">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="82dd9-191">Si no es así, trabajar con su tooget de proveedor de conectividad el circuito toohello necesario al estado y.</span><span class="sxs-lookup"><span data-stu-id="82dd9-191">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="82dd9-192">**Configurar Azure el emparejamiento público para el circuito de Hola**</span><span class="sxs-lookup"><span data-stu-id="82dd9-192">**Configure Azure public peering for hello circuit**</span></span>
   
    <span data-ttu-id="82dd9-193">Asegúrese de que tiene Hola siguiente información antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="82dd9-193">Ensure that you have hello following information before you proceed further.</span></span>
   
   * <span data-ttu-id="82dd9-194">/ 30 subred para el vínculo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="82dd9-194">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="82dd9-195">Tiene que ser un prefijo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="82dd9-195">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="82dd9-196">/ 30 subred para el vínculo secundario Hola.</span><span class="sxs-lookup"><span data-stu-id="82dd9-196">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="82dd9-197">Tiene que ser un prefijo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="82dd9-197">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="82dd9-198">Un tooestablish de Id. de VLAN válido este emparejamiento correctamente.</span><span class="sxs-lookup"><span data-stu-id="82dd9-198">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="82dd9-199">No Asegúrese de que ningún otro emparejamiento en el circuito de hello usa Hola mismo identificador de VLAN.</span><span class="sxs-lookup"><span data-stu-id="82dd9-199">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="82dd9-200">Número de sistema autónomo (AS) para la configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="82dd9-200">AS number for peering.</span></span> <span data-ttu-id="82dd9-201">Puede usar 2 bytes o 4 bytes como números AS.</span><span class="sxs-lookup"><span data-stu-id="82dd9-201">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="82dd9-202">Hash MD5 si elige toouse uno.</span><span class="sxs-lookup"><span data-stu-id="82dd9-202">An MD5 hash if you choose toouse one.</span></span> <span data-ttu-id="82dd9-203">**Esto es opcional**.</span><span class="sxs-lookup"><span data-stu-id="82dd9-203">**This is optional**.</span></span>
     
    <span data-ttu-id="82dd9-204">Puede ejecutar Hola después tooconfigure cmdlet pares públicos de Azure para el circuito</span><span class="sxs-lookup"><span data-stu-id="82dd9-204">You can run hello following cmdlet tooconfigure Azure public peering for your circuit</span></span>
     
        <span data-ttu-id="82dd9-205">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span><span class="sxs-lookup"><span data-stu-id="82dd9-205">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span></span>
     
    <span data-ttu-id="82dd9-206">Puede usar el cmdlet de hello si elige toouse un hash MD5</span><span class="sxs-lookup"><span data-stu-id="82dd9-206">You can use hello cmdlet below if you choose toouse an MD5 hash</span></span>
     
        <span data-ttu-id="82dd9-207">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="82dd9-207">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="82dd9-208">Asegúrese de especificar su número AS como ASN de configuración entre pares y no como cliente ASN.</span><span class="sxs-lookup"><span data-stu-id="82dd9-208">Ensure that you specify your AS number as peering ASN and not customer ASN.</span></span>
     > 
     > 

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="82dd9-209">tooview Azure pública emparejamiento detalles</span><span class="sxs-lookup"><span data-stu-id="82dd9-209">tooview Azure public peering details</span></span>
<span data-ttu-id="82dd9-210">Puede obtener detalles de configuración mediante el siguiente cmdlet de Hola</span><span class="sxs-lookup"><span data-stu-id="82dd9-210">You can get configuration details using hello following cmdlet</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 131.107.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 131.107.0.4/30
    State                          : Enabled
    VlanId                         : 200


### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="82dd9-211">tooupdate configuración de interconexión pública de Azure</span><span class="sxs-lookup"><span data-stu-id="82dd9-211">tooupdate Azure public peering configuration</span></span>
<span data-ttu-id="82dd9-212">Puede actualizar cualquier parte de configuración de hello mediante el siguiente cmdlet de Hola</span><span class="sxs-lookup"><span data-stu-id="82dd9-212">You can update any part of hello configuration using hello following cmdlet</span></span>

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

<span data-ttu-id="82dd9-213">Id. de VLAN del circuito de Hola Hola se está actualizando de 200 too600 Hola ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="82dd9-213">hello VLAN ID of hello circuit is being updated from 200 too600 in hello above example.</span></span>

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="82dd9-214">toodelete pares públicos de Azure</span><span class="sxs-lookup"><span data-stu-id="82dd9-214">toodelete Azure public peering</span></span>
<span data-ttu-id="82dd9-215">Puede quitar la configuración de emparejamiento ejecutando el siguiente cmdlet de Hola</span><span class="sxs-lookup"><span data-stu-id="82dd9-215">You can remove your peering configuration by running hello following cmdlet</span></span>

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a><span data-ttu-id="82dd9-216">Emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="82dd9-216">Microsoft peering</span></span>
<span data-ttu-id="82dd9-217">Esta sección proporciona instrucciones sobre cómo toocreate, obtener, actualizar y eliminar la configuración de emparejamiento de Microsoft de Hola por un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="82dd9-217">This section provides instructions on how toocreate, get, update and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="82dd9-218">emparejamiento de Microsoft toocreate</span><span class="sxs-lookup"><span data-stu-id="82dd9-218">toocreate Microsoft peering</span></span>
1. <span data-ttu-id="82dd9-219">**Importe el módulo de PowerShell de Hola para ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="82dd9-219">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="82dd9-220">Debe importar los módulos de Azure y ExpressRoute de hello en la sesión de PowerShell de hello en toostart orden mediante cmdlets de ExpressRoute Hola.</span><span class="sxs-lookup"><span data-stu-id="82dd9-220">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="82dd9-221">Siguiente ejecución Hola comandos de módulos de Azure y ExpressRoute hello tooimport en la sesión de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="82dd9-221">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="82dd9-222">**Creación de un circuito ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="82dd9-222">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="82dd9-223">Siga Hola instrucciones toocreate una [circuito de ExpressRoute](expressroute-howto-circuit-classic.md) y hacer que se aprovisiona proveedor de conectividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="82dd9-223">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="82dd9-224">Si el proveedor de conectividad ofrece servicios administrados de capa 3, puede solicitar su tooenable de proveedor de conectividad Azure privada emparejamiento para usted.</span><span class="sxs-lookup"><span data-stu-id="82dd9-224">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="82dd9-225">En ese caso, no necesitará toofollow instrucciones que se indican en las secciones siguientes se Hola.</span><span class="sxs-lookup"><span data-stu-id="82dd9-225">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="82dd9-226">Sin embargo, si el proveedor de conectividad no administra el enrutamiento para usted, después de crear el circuito, siga estas instrucciones Hola.</span><span class="sxs-lookup"><span data-stu-id="82dd9-226">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span>
3. <span data-ttu-id="82dd9-227">**Compruebe tooensure de circuito de ExpressRoute se aprovisiona**</span><span class="sxs-lookup"><span data-stu-id="82dd9-227">**Check ExpressRoute circuit tooensure it is provisioned**</span></span>
   
    <span data-ttu-id="82dd9-228">En primer lugar debe comprobar toosee si Hola circuito de ExpressRoute se encuentra en estado aprovisionado y habilitado.</span><span class="sxs-lookup"><span data-stu-id="82dd9-228">You must first check toosee if hello ExpressRoute circuit is in Provisioned and Enabled state.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="82dd9-229">Asegúrese de que el circuito de hello muestra como aprovisionado y habilitado.</span><span class="sxs-lookup"><span data-stu-id="82dd9-229">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="82dd9-230">Si no es así, trabajar con su tooget de proveedor de conectividad el circuito toohello necesario al estado y.</span><span class="sxs-lookup"><span data-stu-id="82dd9-230">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="82dd9-231">**Configurar Microsoft emparejamiento para el circuito de Hola**</span><span class="sxs-lookup"><span data-stu-id="82dd9-231">**Configure Microsoft peering for hello circuit**</span></span>
   
    <span data-ttu-id="82dd9-232">Asegúrese de que haya Hola siguiente información antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="82dd9-232">Make sure that you have hello following information before you proceed.</span></span>
   
   * <span data-ttu-id="82dd9-233">/ 30 subred para el vínculo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="82dd9-233">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="82dd9-234">Debe ser un prefijo de IPv4 público válido que sea de su propiedad y esté registrado en un Registro regional de Internet (RIR) o un Registro de enrutamiento de Internet (IRR).</span><span class="sxs-lookup"><span data-stu-id="82dd9-234">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="82dd9-235">/ 30 subred para el vínculo secundario Hola.</span><span class="sxs-lookup"><span data-stu-id="82dd9-235">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="82dd9-236">Debe ser un prefijo de IPv4 público válido que sea de su propiedad y esté registrado en un Registro regional de Internet (RIR) o un Registro de enrutamiento de Internet (IRR).</span><span class="sxs-lookup"><span data-stu-id="82dd9-236">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="82dd9-237">Un tooestablish de Id. de VLAN válido este emparejamiento correctamente.</span><span class="sxs-lookup"><span data-stu-id="82dd9-237">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="82dd9-238">No Asegúrese de que ningún otro emparejamiento en el circuito de hello usa Hola mismo identificador de VLAN.</span><span class="sxs-lookup"><span data-stu-id="82dd9-238">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="82dd9-239">Número de sistema autónomo (AS) para la configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="82dd9-239">AS number for peering.</span></span> <span data-ttu-id="82dd9-240">Puede usar 2 bytes o 4 bytes como números AS.</span><span class="sxs-lookup"><span data-stu-id="82dd9-240">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="82dd9-241">Anuncian prefijos: debe proporcionar una lista de todos los prefijos piensa tooadvertise en las sesiones BGP Hola.</span><span class="sxs-lookup"><span data-stu-id="82dd9-241">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="82dd9-242">Se aceptan solo prefijos de direcciones IP públicas.</span><span class="sxs-lookup"><span data-stu-id="82dd9-242">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="82dd9-243">Puede enviar una lista separada por comas si tiene previsto toosend un conjunto de prefijos.</span><span class="sxs-lookup"><span data-stu-id="82dd9-243">You can send a comma separated list if you plan toosend a set of prefixes.</span></span> <span data-ttu-id="82dd9-244">Estos prefijos deben ser tooyou registrado en un RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="82dd9-244">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
   * <span data-ttu-id="82dd9-245">Cliente ASN: Si se anuncian prefijos que no están registrado toohello emparejamiento como número, puede especificar hello como número toowhich que están registrados.</span><span class="sxs-lookup"><span data-stu-id="82dd9-245">Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span> <span data-ttu-id="82dd9-246">**Esto es opcional**.</span><span class="sxs-lookup"><span data-stu-id="82dd9-246">**This is optional**.</span></span>
   * <span data-ttu-id="82dd9-247">Nombre del enrutamiento del registro: Puede especificar Hola RIR / IRR en qué hello como número y los prefijos registrados.</span><span class="sxs-lookup"><span data-stu-id="82dd9-247">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
   * <span data-ttu-id="82dd9-248">Un hash MD5, si elige toouse uno.</span><span class="sxs-lookup"><span data-stu-id="82dd9-248">An MD5 hash, if you choose toouse one.</span></span> <span data-ttu-id="82dd9-249">**Esto es opcional.**</span><span class="sxs-lookup"><span data-stu-id="82dd9-249">**This is optional.**</span></span>
     
    <span data-ttu-id="82dd9-250">Puede ejecutar Hola después pering de Microsoft tooconfigure de cmdlet para el circuito</span><span class="sxs-lookup"><span data-stu-id="82dd9-250">You can run hello following cmdlet tooconfigure Microsoft pering for your circuit</span></span>
     
        <span data-ttu-id="82dd9-251">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="82dd9-251">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span></span>

### <a name="tooview-microsoft-peering-details"></a><span data-ttu-id="82dd9-252">detalles de emparejamiento de Microsoft tooview</span><span class="sxs-lookup"><span data-stu-id="82dd9-252">tooview Microsoft peering details</span></span>
<span data-ttu-id="82dd9-253">Puede obtener detalles de configuración mediante el siguiente cmdlet de Hola.</span><span class="sxs-lookup"><span data-stu-id="82dd9-253">You can get configuration details using hello following cmdlet.</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 123.0.0.0/30
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 2245
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : ARIN
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 300


### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="82dd9-254">configuración de emparejamiento de Microsoft tooupdate</span><span class="sxs-lookup"><span data-stu-id="82dd9-254">tooupdate Microsoft peering configuration</span></span>
<span data-ttu-id="82dd9-255">Puede actualizar cualquier parte de configuración de hello mediante Hola siguiente cmdlet.</span><span class="sxs-lookup"><span data-stu-id="82dd9-255">You can update any part of hello configuration using hello following cmdlet.</span></span>

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="82dd9-256">emparejamiento de Microsoft toodelete</span><span class="sxs-lookup"><span data-stu-id="82dd9-256">toodelete Microsoft peering</span></span>
<span data-ttu-id="82dd9-257">Puede quitar la configuración de intercambio de tráfico mediante la ejecución de hello siguiente cmdlet.</span><span class="sxs-lookup"><span data-stu-id="82dd9-257">You can remove your peering configuration by running hello following cmdlet.</span></span>

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a><span data-ttu-id="82dd9-258">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="82dd9-258">Next steps</span></span>
<span data-ttu-id="82dd9-259">Después, [vincular un circuito de ExpressRoute de red virtual tooan](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="82dd9-259">Next, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

* <span data-ttu-id="82dd9-260">Para obtener más información sobre los flujos de trabajo, consulte [Flujos de trabajo de ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="82dd9-260">For more information about workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="82dd9-261">Para más información sobre el emparejamiento de circuitos, vea [Circuitos y dominios de enrutamiento de ExpressRoute](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="82dd9-261">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>

