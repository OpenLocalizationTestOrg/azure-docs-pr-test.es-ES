---
title: "¿Cómo tooconfigure enrutamiento por un circuito ExpressRoute de Azure: CLI | Documentos de Microsoft"
description: "En este artículo le ayuda a crear y aprovisionar Hola privado, público y emparejamiento de Microsoft de un circuito de ExpressRoute. Este artículo también muestra cómo toocheck estado de hello, actualizar o eliminar emparejamientos para el circuito."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 33130af050045527cdb316e77821c6d101b6a82a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a><span data-ttu-id="7446a-104">Creación y modificación del enrutamiento de un circuito ExpressRoute mediante la CLI</span><span class="sxs-lookup"><span data-stu-id="7446a-104">Create and modify routing for an ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="7446a-105">En este artículo le ayuda a crear y administrar la configuración de enrutamiento para un circuito ExpressRoute en modelo de implementación del Administrador de recursos Hola con CLI.</span><span class="sxs-lookup"><span data-stu-id="7446a-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using CLI.</span></span> <span data-ttu-id="7446a-106">También puede comprobar el estado de hello, update o delete y desaprovisionar los emparejamientos de un circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7446a-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="7446a-107">Si desea toouse una toowork otro método con el circuito, seleccione un artículo de hello lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="7446a-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7446a-108">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="7446a-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="7446a-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7446a-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="7446a-110">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="7446a-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="7446a-111">Vídeo: pares privados</span><span class="sxs-lookup"><span data-stu-id="7446a-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="7446a-112">Vídeo: pares públicos</span><span class="sxs-lookup"><span data-stu-id="7446a-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="7446a-113">Vídeo: emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="7446a-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="7446a-114">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="7446a-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="7446a-115">Requisitos previos de configuración</span><span class="sxs-lookup"><span data-stu-id="7446a-115">Configuration prerequisites</span></span>

* <span data-ttu-id="7446a-116">Antes de comenzar, instalar la versión más reciente de Hola de comandos de CLI de hello (2.0 o posteriores).</span><span class="sxs-lookup"><span data-stu-id="7446a-116">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="7446a-117">Para obtener información acerca de cómo instalar los comandos de CLI de hello, consulte [instalar Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7446a-117">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="7446a-118">Asegúrese de que ha revisado hello [requisitos previos](expressroute-prerequisites.md), [requisitos de enrutamiento](expressroute-routing.md), y [flujo de trabajo](expressroute-workflows.md) páginas antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="7446a-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflow](expressroute-workflows.md) pages before you begin configuration.</span></span>
* <span data-ttu-id="7446a-119">Tiene que tener un circuito ExpressRoute activo.</span><span class="sxs-lookup"><span data-stu-id="7446a-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="7446a-120">Siga las instrucciones de hello demasiado[crear un circuito ExpressRoute](howto-circuit-cli.md) y tener circuito de hello habilitada por el proveedor de conectividad antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="7446a-120">Follow hello instructions too[Create an ExpressRoute circuit](howto-circuit-cli.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="7446a-121">Hola circuito de ExpressRoute debe estar en un estado habilitado y aprovisionado para que los comandos de toobe toorun capaz de hello en este artículo.</span><span class="sxs-lookup"><span data-stu-id="7446a-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello commands in this article.</span></span>

<span data-ttu-id="7446a-122">Estas instrucciones aplican solo toocircuits creado con proveedores de servicios que ofrece servicios de conectividad de nivel 2.</span><span class="sxs-lookup"><span data-stu-id="7446a-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="7446a-123">Si usa un proveedor de servicios que ofrece servicios administrados de nivel 3 (normalmente VPN IP, como MPLS), el mismo proveedor de conectividad configurará y administrará el enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="7446a-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

<span data-ttu-id="7446a-124">Puede configurar una, dos o las tres configuraciones entre pares (Azure privado, Azure público y Microsoft) para un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7446a-124">You can configure one, two, or all three peerings (Azure private, Azure public, and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="7446a-125">Puede establecer las configuraciones entre pares en cualquier orden.</span><span class="sxs-lookup"><span data-stu-id="7446a-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="7446a-126">Sin embargo, debe asegurarse de completar configuración de Hola de cada uno de ellos emparejamiento a la vez.</span><span class="sxs-lookup"><span data-stu-id="7446a-126">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="7446a-127">Configuración entre pares privados de Azure</span><span class="sxs-lookup"><span data-stu-id="7446a-127">Azure private peering</span></span>

<span data-ttu-id="7446a-128">En esta sección le ayuda a crear, obtener, actualizar y eliminar hello Azure configuración privada de emparejamiento de un circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7446a-128">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="7446a-129">toocreate emparejamiento privado de Azure</span><span class="sxs-lookup"><span data-stu-id="7446a-129">toocreate Azure private peering</span></span>

1. <span data-ttu-id="7446a-130">Instale la versión más reciente de Hola de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="7446a-130">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="7446a-131">Debe usar la versión más reciente de Hola de hello interfaz de línea de comandos (CLI) de Azure. * Hola revisión [requisitos previos](expressroute-prerequisites.md) y [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="7446a-131">You must use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="7446a-132">Seleccionar suscripción Hola desea toocreate circuito de ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="7446a-132">Select hello subscription you want toocreate ExpressRoute circuit</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="7446a-133">Crear un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7446a-133">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="7446a-134">Siga Hola instrucciones toocreate una [circuito de ExpressRoute](howto-circuit-cli.md) y hacer que se aprovisiona proveedor de conectividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="7446a-134">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="7446a-135">Si el proveedor de conectividad ofrece servicios administrados de capa 3, puede solicitar su tooenable de proveedor de conectividad Azure privada emparejamiento para usted.</span><span class="sxs-lookup"><span data-stu-id="7446a-135">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="7446a-136">En ese caso, no necesitará toofollow instrucciones que se indican en las secciones siguientes se Hola.</span><span class="sxs-lookup"><span data-stu-id="7446a-136">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="7446a-137">Sin embargo, si el proveedor de conectividad no administra el enrutamiento para usted, después de crear el circuito, continuar la configuración mediante los pasos siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="7446a-137">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="7446a-138">Compruebe hello toomake de circuito de ExpressRoute seguro de que esté aprovisionado y también habilitado.</span><span class="sxs-lookup"><span data-stu-id="7446a-138">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="7446a-139">Utilice el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="7446a-139">Use hello following example:</span></span>

  ```azurecli
  az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
  ```

  <span data-ttu-id="7446a-140">respuesta de Hello es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7446a-140">hello response is similar toohello following example:</span></span>

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="7446a-141">Configurar Azure intercambio de tráfico privado para el circuito de Hola.</span><span class="sxs-lookup"><span data-stu-id="7446a-141">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="7446a-142">Asegúrese de que dispone de hello siguientes elementos antes de continuar con los pasos siguientes de hello:</span><span class="sxs-lookup"><span data-stu-id="7446a-142">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="7446a-143">/ 30 subred para el vínculo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="7446a-143">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="7446a-144">subred de Hello no debe formar parte de cualquier espacio de direcciones reservada para las redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="7446a-144">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="7446a-145">/ 30 subred para el vínculo secundario Hola.</span><span class="sxs-lookup"><span data-stu-id="7446a-145">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="7446a-146">subred de Hello no debe formar parte de cualquier espacio de direcciones reservada para las redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="7446a-146">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="7446a-147">Un tooestablish de Id. de VLAN válido este emparejamiento correctamente.</span><span class="sxs-lookup"><span data-stu-id="7446a-147">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="7446a-148">No Asegúrese de que ningún otro emparejamiento en el circuito de hello usa Hola mismo identificador de VLAN.</span><span class="sxs-lookup"><span data-stu-id="7446a-148">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="7446a-149">Número de sistema autónomo (AS) para la configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="7446a-149">AS number for peering.</span></span> <span data-ttu-id="7446a-150">Puede usar 2 bytes o 4 bytes como números AS.</span><span class="sxs-lookup"><span data-stu-id="7446a-150">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="7446a-151">Puede usar un número AS privado para esta configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="7446a-151">You can use a private AS number for this peering.</span></span> <span data-ttu-id="7446a-152">Asegúrese de que no usa 65515.</span><span class="sxs-lookup"><span data-stu-id="7446a-152">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="7446a-153">**Opcional:** un hash MD5 si elige toouse uno.</span><span class="sxs-lookup"><span data-stu-id="7446a-153">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="7446a-154">Usar hello después tooconfigure Azure privada de emparejamiento para el circuito de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7446a-154">Use hello following example tooconfigure Azure private peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  <span data-ttu-id="7446a-155">Si elige toouse un hash MD5, use Hola siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7446a-155">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="7446a-156">Asegúrese de especificar su número AS como ASN de configuración entre pares, no como cliente ASN.</span><span class="sxs-lookup"><span data-stu-id="7446a-156">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  > 

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="7446a-157">tooview privada emparejamiento detalles de Azure</span><span class="sxs-lookup"><span data-stu-id="7446a-157">tooview Azure private peering details</span></span>

<span data-ttu-id="7446a-158">Puede obtener detalles de configuración mediante el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="7446a-158">You can get configuration details by using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

<span data-ttu-id="7446a-159">Hola de salida es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7446a-159">hello output is similar toohello following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePrivatePeering",
  "ipv6PeeringConfig": null,
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePrivatePeering",
  "peerAsn": 7671,
  "peeringType": "AzurePrivatePeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="7446a-160">tooupdate configuración de emparejamiento privada de Azure</span><span class="sxs-lookup"><span data-stu-id="7446a-160">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="7446a-161">Puede actualizar cualquier parte de la configuración de hello mediante el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7446a-161">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="7446a-162">En este ejemplo, Id. de VLAN del circuito de Hola Hola se está actualizando desde too500 100.</span><span class="sxs-lookup"><span data-stu-id="7446a-162">In this example, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="7446a-163">toodelete emparejamiento privado de Azure</span><span class="sxs-lookup"><span data-stu-id="7446a-163">toodelete Azure private peering</span></span>

<span data-ttu-id="7446a-164">Puede quitar la configuración de emparejamiento ejecutando el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="7446a-164">You can remove your peering configuration by running hello following example:</span></span>

> [!WARNING]
> <span data-ttu-id="7446a-165">También debe asegurarse de que todas las redes virtuales se desvincula de hello circuito de ExpressRoute antes de ejecutar este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7446a-165">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this example.</span></span> 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a><span data-ttu-id="7446a-166">Configuración entre pares públicos de Azure</span><span class="sxs-lookup"><span data-stu-id="7446a-166">Azure public peering</span></span>

<span data-ttu-id="7446a-167">En esta sección le ayuda a crear, obtener, actualizar y eliminar hello Azure configuración de emparejamiento público de un circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7446a-167">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="7446a-168">toocreate pares públicos de Azure</span><span class="sxs-lookup"><span data-stu-id="7446a-168">toocreate Azure public peering</span></span>

1. <span data-ttu-id="7446a-169">Instale la versión más reciente de Hola de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="7446a-169">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="7446a-170">Debe usar la versión más reciente de Hola de hello interfaz de línea de comandos (CLI) de Azure. * Hola revisión [requisitos previos](expressroute-prerequisites.md) y [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="7446a-170">You must use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="7446a-171">Seleccione la suscripción de hello para el que desea toocreate circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7446a-171">Select hello subscription for which you want toocreate ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="7446a-172">Crear un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7446a-172">Create an ExpressRoute circuit.</span></span>  <span data-ttu-id="7446a-173">Siga Hola instrucciones toocreate una [circuito de ExpressRoute](howto-circuit-cli.md) y hacer que se aprovisiona proveedor de conectividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="7446a-173">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="7446a-174">Si su proveedor de conectividad ofrece servicios administrados de nivel 3, puede solicitarle que habilite la configuración entre pares privados de Azure.</span><span class="sxs-lookup"><span data-stu-id="7446a-174">If your connectivity provider offers managed Layer 3 services, you can request that your connectivity provider enables Azure private peering for you.</span></span> <span data-ttu-id="7446a-175">En ese caso, no necesitará toofollow instrucciones que se indican en las secciones siguientes se Hola.</span><span class="sxs-lookup"><span data-stu-id="7446a-175">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="7446a-176">Sin embargo, si el proveedor de conectividad no administra el enrutamiento para usted, después de crear el circuito, continuar la configuración mediante los pasos siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="7446a-176">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="7446a-177">Compruebe tooensure de circuito de ExpressRoute Hola está aprovisionado y también está habilitado.</span><span class="sxs-lookup"><span data-stu-id="7446a-177">Check hello ExpressRoute circuit tooensure it is provisioned and also enabled.</span></span> <span data-ttu-id="7446a-178">Utilice el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="7446a-178">Use hello following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="7446a-179">respuesta de Hello es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7446a-179">hello response is similar toohello following example:</span></span>

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
    "bandwidthInMbps": 200,
    "peeringLocation": "Silicon Valley",
    "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="7446a-180">Configure pares públicos de Azure para el circuito de Hola.</span><span class="sxs-lookup"><span data-stu-id="7446a-180">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="7446a-181">Asegúrese de que dispone de hello siguiente información antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="7446a-181">Make sure that you have hello following information before you proceed further.</span></span>

  * <span data-ttu-id="7446a-182">/ 30 subred para el vínculo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="7446a-182">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="7446a-183">Tiene que ser un prefijo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="7446a-183">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="7446a-184">/ 30 subred para el vínculo secundario Hola.</span><span class="sxs-lookup"><span data-stu-id="7446a-184">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="7446a-185">Tiene que ser un prefijo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="7446a-185">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="7446a-186">Un tooestablish de Id. de VLAN válido este emparejamiento correctamente.</span><span class="sxs-lookup"><span data-stu-id="7446a-186">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="7446a-187">No Asegúrese de que ningún otro emparejamiento en el circuito de hello usa Hola mismo identificador de VLAN.</span><span class="sxs-lookup"><span data-stu-id="7446a-187">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="7446a-188">Número de sistema autónomo (AS) para la configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="7446a-188">AS number for peering.</span></span> <span data-ttu-id="7446a-189">Puede usar 2 bytes o 4 bytes como números AS.</span><span class="sxs-lookup"><span data-stu-id="7446a-189">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="7446a-190">**Opcional:** un hash MD5 si elige toouse uno.</span><span class="sxs-lookup"><span data-stu-id="7446a-190">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="7446a-191">Ejecute hello después tooconfigure Azure pública de emparejamiento para el circuito de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7446a-191">Run hello following example tooconfigure Azure public peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  <span data-ttu-id="7446a-192">Si elige toouse un hash MD5, use Hola siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7446a-192">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="7446a-193">Asegúrese de especificar su número AS como ASN de configuración entre pares, no como cliente ASN.</span><span class="sxs-lookup"><span data-stu-id="7446a-193">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="7446a-194">tooview Azure pública emparejamiento detalles</span><span class="sxs-lookup"><span data-stu-id="7446a-194">tooview Azure public peering details</span></span>

<span data-ttu-id="7446a-195">Puede obtener detalles de configuración mediante el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="7446a-195">You can get configuration details using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

<span data-ttu-id="7446a-196">Hola de salida es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7446a-196">hello output is similar toohello following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePublicPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePublicPeering",
  "peerAsn": 7671,
  "peeringType": "AzurePublicPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="7446a-197">tooupdate configuración de interconexión pública de Azure</span><span class="sxs-lookup"><span data-stu-id="7446a-197">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="7446a-198">Puede actualizar cualquier parte de la configuración de hello mediante el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7446a-198">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="7446a-199">En este ejemplo, Id. de VLAN del circuito de Hola Hola se está actualizando desde too600 200.</span><span class="sxs-lookup"><span data-stu-id="7446a-199">In this example, hello VLAN ID of hello circuit is being updated from 200 too600.</span></span>

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="7446a-200">toodelete pares públicos de Azure</span><span class="sxs-lookup"><span data-stu-id="7446a-200">toodelete Azure public peering</span></span>

<span data-ttu-id="7446a-201">Puede quitar la configuración de emparejamiento ejecutando el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="7446a-201">You can remove your peering configuration by running hello following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a><span data-ttu-id="7446a-202">Emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="7446a-202">Microsoft peering</span></span>

<span data-ttu-id="7446a-203">En esta sección le ayuda a crear, obtener, actualizar y eliminar la configuración de emparejamiento de Microsoft de Hola por un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7446a-203">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7446a-204">Emparejamiento de Microsoft de circuitos ExpressRoute que estaban configurados anterior tooAugust 1, 2017 tendrá todos los prefijos de servicio implementados a través de emparejamiento de Microsoft hello, incluso si no se definen los filtros de ruta.</span><span class="sxs-lookup"><span data-stu-id="7446a-204">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="7446a-205">Emparejamiento de Microsoft de circuitos ExpressRoute configurados en o después del 1 de agosto de 2017 no tendrá todos los prefijos anunciados hasta que se conecte un filtro de ruta toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="7446a-205">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="7446a-206">Para más información, consulte [Configuración de un filtro de ruta para el emparejamiento de Microsoft](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="7446a-206">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="7446a-207">emparejamiento de Microsoft toocreate</span><span class="sxs-lookup"><span data-stu-id="7446a-207">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="7446a-208">Instale la versión más reciente de Hola de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="7446a-208">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="7446a-209">Usar versión más reciente de Hola de hello interfaz de línea de comandos (CLI) de Azure. * Hola revisión [requisitos previos](expressroute-prerequisites.md) y [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="7446a-209">Use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="7446a-210">Seleccione la suscripción de hello para el que desea toocreate circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7446a-210">Select hello subscription for which you want toocreate ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="7446a-211">Crear un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7446a-211">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="7446a-212">Siga Hola instrucciones toocreate una [circuito de ExpressRoute](howto-circuit-cli.md) y hacer que se aprovisiona proveedor de conectividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="7446a-212">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="7446a-213">Si el proveedor de conectividad ofrece servicios administrados de capa 3, puede solicitar su tooenable de proveedor de conectividad Azure privada emparejamiento para usted.</span><span class="sxs-lookup"><span data-stu-id="7446a-213">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="7446a-214">En ese caso, no necesitará toofollow instrucciones que se indican en las secciones siguientes se Hola.</span><span class="sxs-lookup"><span data-stu-id="7446a-214">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="7446a-215">Sin embargo, si el proveedor de conectividad no administra el enrutamiento para usted, después de crear el circuito, continuar la configuración mediante los pasos siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="7446a-215">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>

3. <span data-ttu-id="7446a-216">Compruebe hello toomake de circuito de ExpressRoute seguro de que esté aprovisionado y también habilitado.</span><span class="sxs-lookup"><span data-stu-id="7446a-216">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="7446a-217">Utilice el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="7446a-217">Use hello following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="7446a-218">respuesta de Hello es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7446a-218">hello response is similar toohello following example:</span></span>

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
    "bandwidthInMbps": 200,
    "peeringLocation": "Silicon Valley",
    "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="7446a-219">Configurar Microsoft emparejamiento para el circuito de Hola.</span><span class="sxs-lookup"><span data-stu-id="7446a-219">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="7446a-220">Asegúrese de que haya Hola siguiente información antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="7446a-220">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="7446a-221">/ 30 subred para el vínculo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="7446a-221">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="7446a-222">Debe ser un prefijo de IPv4 público válido que sea de su propiedad y esté registrado en un Registro regional de Internet (RIR) o un Registro de enrutamiento de Internet (IRR).</span><span class="sxs-lookup"><span data-stu-id="7446a-222">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="7446a-223">/ 30 subred para el vínculo secundario Hola.</span><span class="sxs-lookup"><span data-stu-id="7446a-223">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="7446a-224">Debe ser un prefijo de IPv4 público válido que sea de su propiedad y esté registrado en un Registro regional de Internet (RIR) o un Registro de enrutamiento de Internet (IRR).</span><span class="sxs-lookup"><span data-stu-id="7446a-224">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="7446a-225">Un tooestablish de Id. de VLAN válido este emparejamiento correctamente.</span><span class="sxs-lookup"><span data-stu-id="7446a-225">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="7446a-226">No Asegúrese de que ningún otro emparejamiento en el circuito de hello usa Hola mismo identificador de VLAN.</span><span class="sxs-lookup"><span data-stu-id="7446a-226">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="7446a-227">Número de sistema autónomo (AS) para la configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="7446a-227">AS number for peering.</span></span> <span data-ttu-id="7446a-228">Puede usar 2 bytes o 4 bytes como números AS.</span><span class="sxs-lookup"><span data-stu-id="7446a-228">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="7446a-229">Anuncian prefijos: debe proporcionar una lista de todos los prefijos piensa tooadvertise en las sesiones BGP Hola.</span><span class="sxs-lookup"><span data-stu-id="7446a-229">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="7446a-230">Se aceptan solo prefijos de direcciones IP públicas.</span><span class="sxs-lookup"><span data-stu-id="7446a-230">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="7446a-231">Si tiene previsto toosend un conjunto de prefijos, puede enviar una lista separada por comas.</span><span class="sxs-lookup"><span data-stu-id="7446a-231">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="7446a-232">Estos prefijos deben ser tooyou registrado en un RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="7446a-232">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="7446a-233">**Opcional:** cliente ASN: si es que los prefijos de publicidad que no están registrado toohello emparejamiento como número, puede especificar hello como número toowhich están registrados.</span><span class="sxs-lookup"><span data-stu-id="7446a-233">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="7446a-234">Nombre del enrutamiento del registro: Puede especificar Hola RIR / IRR en qué hello como número y los prefijos registrados.</span><span class="sxs-lookup"><span data-stu-id="7446a-234">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="7446a-235">**Opcional:** un hash MD5 si elige toouse uno.</span><span class="sxs-lookup"><span data-stu-id="7446a-235">**Optional -** An MD5 hash if you choose toouse one.</span></span>

   <span data-ttu-id="7446a-236">Ejecute hello siguiendo la emparejamiento de Microsoft tooconfigure de ejemplo para el circuito:</span><span class="sxs-lookup"><span data-stu-id="7446a-236">Run hello following example tooconfigure Microsoft peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="tooget-microsoft-peering-details"></a><span data-ttu-id="7446a-237">detalles de emparejamiento de Microsoft tooget</span><span class="sxs-lookup"><span data-stu-id="7446a-237">tooget Microsoft peering details</span></span>

<span data-ttu-id="7446a-238">Puede obtener detalles de configuración mediante el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="7446a-238">You can get configuration details by using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

<span data-ttu-id="7446a-239">Hola de salida es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7446a-239">hello output is similar toohello following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzureMicrosoftPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": {
    "advertisedPublicPrefixes": [
        ""
      ],
     "advertisedPublicPrefixesState": "",
     "customerASN": ,
     "routingRegistryName": ""
  }
  "name": "AzureMicrosoftPeering",
  "peerAsn": ,
  "peeringType": "AzureMicrosoftPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="7446a-240">configuración de emparejamiento de Microsoft tooupdate</span><span class="sxs-lookup"><span data-stu-id="7446a-240">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="7446a-241">Puede actualizar cualquier parte de la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="7446a-241">You can update any part of hello configuration.</span></span> <span data-ttu-id="7446a-242">Hola anuncia prefijos del circuito de Hola se están actualizando desde 123.1.0.0/24 too124.1.0.0/24 en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="7446a-242">hello advertised prefixes of hello circuit are being updated from 123.1.0.0/24 too124.1.0.0/24 in hello following example:</span></span>

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="7446a-243">emparejamiento de Microsoft toodelete</span><span class="sxs-lookup"><span data-stu-id="7446a-243">toodelete Microsoft peering</span></span>

<span data-ttu-id="7446a-244">Puede quitar la configuración de emparejamiento ejecutando el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="7446a-244">You can remove your peering configuration by running hello following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a><span data-ttu-id="7446a-245">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7446a-245">Next steps</span></span>

<span data-ttu-id="7446a-246">Siguiente paso, [vincular un circuito de ExpressRoute de red virtual tooan](howto-linkvnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7446a-246">Next step, [Link a VNet tooan ExpressRoute circuit](howto-linkvnet-cli.md).</span></span>

* <span data-ttu-id="7446a-247">Para más información sobre los flujos de trabajo de ExpressRoute, vea [Flujos de trabajo de ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="7446a-247">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="7446a-248">Para más información sobre el emparejamiento de circuitos, vea [Circuitos y dominios de enrutamiento de ExpressRoute](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="7446a-248">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="7446a-249">Para más información sobre redes virtuales, vea [Información general sobre redes virtuales](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7446a-249">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>