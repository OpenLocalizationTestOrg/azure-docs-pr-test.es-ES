---
title: "Configuración del enrutamiento de un circuito de Azure ExpressRoute: CLI | Microsoft Docs"
description: "Este artículo le ayudará a crear y aprovisionar las configuraciones entre pares privados, públicos y de Microsoft de un circuito ExpressRoute. Este artículo también muestra cómo comprobar el estado, actualizar, o eliminar configuraciones entre pares en el circuito."
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
ms.openlocfilehash: fbf0bd9a139c22bbd63755f6df445f6596aaccc5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a><span data-ttu-id="fe603-104">Creación y modificación del enrutamiento de un circuito ExpressRoute mediante la CLI</span><span class="sxs-lookup"><span data-stu-id="fe603-104">Create and modify routing for an ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="fe603-105">Este artículo le ayuda a crear y administrar la configuración de enrutamiento de un circuito ExpressRoute en el modelo de implementación de Resource Manager mediante la CLI.</span><span class="sxs-lookup"><span data-stu-id="fe603-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in the Resource Manager deployment model using CLI.</span></span> <span data-ttu-id="fe603-106">También puede comprobar el estado de los emparejamientos de un circuito ExpressRoute, así como el modo de actualizarlos o eliminarlos y desaprovisionarlos.</span><span class="sxs-lookup"><span data-stu-id="fe603-106">You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="fe603-107">Si quiere usar un método diferente para trabajar con el circuito, seleccione un artículo de la lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="fe603-107">If you want to use a different method to work with your circuit, select an article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fe603-108">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="fe603-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="fe603-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fe603-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="fe603-110">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="fe603-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="fe603-111">Vídeo: pares privados</span><span class="sxs-lookup"><span data-stu-id="fe603-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="fe603-112">Vídeo: pares públicos</span><span class="sxs-lookup"><span data-stu-id="fe603-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="fe603-113">Vídeo: emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="fe603-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="fe603-114">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="fe603-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="fe603-115">Requisitos previos de configuración</span><span class="sxs-lookup"><span data-stu-id="fe603-115">Configuration prerequisites</span></span>

* <span data-ttu-id="fe603-116">Antes de empezar, instale la versión más reciente de los comandos de la CLI (2.0 o posteriores).</span><span class="sxs-lookup"><span data-stu-id="fe603-116">Before beginning, install the latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="fe603-117">Para más información sobre la instalación de los comandos de la CLI, consulte [Instalación de la CLI de Azure 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fe603-117">For information about installing the CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="fe603-118">Asegúrese de haber revisado los [requisitos previos](expressroute-prerequisites.md), los [requisitos de enrutamiento](expressroute-routing.md) y las páginas del [flujo de trabajo](expressroute-workflows.md) antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="fe603-118">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflow](expressroute-workflows.md) pages before you begin configuration.</span></span>
* <span data-ttu-id="fe603-119">Tiene que tener un circuito ExpressRoute activo.</span><span class="sxs-lookup"><span data-stu-id="fe603-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="fe603-120">Antes de continuar, siga las instrucciones para [crear un circuito ExpressRoute](howto-circuit-cli.md) y para que el proveedor de conectividad habilite el circuito.</span><span class="sxs-lookup"><span data-stu-id="fe603-120">Follow the instructions to [Create an ExpressRoute circuit](howto-circuit-cli.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="fe603-121">El circuito ExpressRoute debe estar en un estado habilitado y aprovisionado para poder ejecutar los comandos que se describen en este artículo.</span><span class="sxs-lookup"><span data-stu-id="fe603-121">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the commands in this article.</span></span>

<span data-ttu-id="fe603-122">Estas instrucciones se aplican solo a los circuitos creados con proveedores de servicios que ofrecen servicios de conectividad de capa 2.</span><span class="sxs-lookup"><span data-stu-id="fe603-122">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="fe603-123">Si usa un proveedor de servicios que ofrece servicios administrados de nivel 3 (normalmente VPN IP, como MPLS), el mismo proveedor de conectividad configurará y administrará el enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="fe603-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

<span data-ttu-id="fe603-124">Puede configurar una, dos o las tres configuraciones entre pares (Azure privado, Azure público y Microsoft) para un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fe603-124">You can configure one, two, or all three peerings (Azure private, Azure public, and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="fe603-125">Puede establecer las configuraciones entre pares en cualquier orden.</span><span class="sxs-lookup"><span data-stu-id="fe603-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="fe603-126">Pero tiene que asegurarse de que completa cada configuración entre pares de una en una.</span><span class="sxs-lookup"><span data-stu-id="fe603-126">However, you must make sure that you complete the configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="fe603-127">Configuración entre pares privados de Azure</span><span class="sxs-lookup"><span data-stu-id="fe603-127">Azure private peering</span></span>

<span data-ttu-id="fe603-128">Esta sección le ayuda a crear, obtener, actualizar y eliminar la configuración de emparejamiento privado de Azure para un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fe603-128">This section helps you create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="fe603-129">Creación de un emparejamiento privado de Azure</span><span class="sxs-lookup"><span data-stu-id="fe603-129">To create Azure private peering</span></span>

1. <span data-ttu-id="fe603-130">Instale la versión más reciente de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="fe603-130">Install the latest version of Azure CLI.</span></span> <span data-ttu-id="fe603-131">Debe usar la versión más reciente de la Interfaz de la línea de comandos de Azure (CLI)*. Revise los [requisitos previos](expressroute-prerequisites.md) y los [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="fe603-131">You must use the latest version of the Azure Command-line Interface (CLI).* Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="fe603-132">Seleccione la suscripción en la que desea crear un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fe603-132">Select the subscription you want to create ExpressRoute circuit</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="fe603-133">Crear un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fe603-133">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="fe603-134">Siga las instrucciones para crear un [circuito ExpressRoute](howto-circuit-cli.md) y habilite su aprovisionamiento a través del proveedor de conectividad.</span><span class="sxs-lookup"><span data-stu-id="fe603-134">Follow the instructions to create an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="fe603-135">Si su proveedor de conectividad ofrece servicios administrados de nivel 3, puede solicitarle que habilite la configuración entre pares privados de Azure.</span><span class="sxs-lookup"><span data-stu-id="fe603-135">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="fe603-136">En ese caso, no necesita seguir las instrucciones que aparecen en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="fe603-136">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="fe603-137">Sin embargo, si el proveedor de conectividad no administra el enrutamiento por usted, después de crear el circuito, continúe con la configuración mediante los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="fe603-137">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="fe603-138">Compruebe el circuito ExpressRoute para asegurarse de que está aprovisionado y también habilitado.</span><span class="sxs-lookup"><span data-stu-id="fe603-138">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="fe603-139">Utilice el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fe603-139">Use the following example:</span></span>

  ```azurecli
  az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
  ```

  <span data-ttu-id="fe603-140">La respuesta es similar al siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fe603-140">The response is similar to the following example:</span></span>

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

4. <span data-ttu-id="fe603-141">Establecimiento de la configuración entre pares privados de Azure para el circuito.</span><span class="sxs-lookup"><span data-stu-id="fe603-141">Configure Azure private peering for the circuit.</span></span> <span data-ttu-id="fe603-142">Asegúrese de que tiene los elementos siguientes antes de continuar con los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="fe603-142">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="fe603-143">Una subred /30 para el vínculo principal.</span><span class="sxs-lookup"><span data-stu-id="fe603-143">A /30 subnet for the primary link.</span></span> <span data-ttu-id="fe603-144">La subred no debe ser parte de ningún espacio de direcciones reservado para redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="fe603-144">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="fe603-145">Una subred /30 para el vínculo secundario.</span><span class="sxs-lookup"><span data-stu-id="fe603-145">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="fe603-146">La subred no debe ser parte de ningún espacio de direcciones reservado para redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="fe603-146">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="fe603-147">Un identificador VLAN válido para establecer esta configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="fe603-147">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="fe603-148">Asegúrese de que ninguna otra configuración entre pares en el circuito usa el mismo identificador de VLAN.</span><span class="sxs-lookup"><span data-stu-id="fe603-148">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="fe603-149">Número de sistema autónomo (AS) para la configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="fe603-149">AS number for peering.</span></span> <span data-ttu-id="fe603-150">Puede usar 2 bytes o 4 bytes como números AS.</span><span class="sxs-lookup"><span data-stu-id="fe603-150">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="fe603-151">Puede usar un número AS privado para esta configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="fe603-151">You can use a private AS number for this peering.</span></span> <span data-ttu-id="fe603-152">Asegúrese de que no usa 65515.</span><span class="sxs-lookup"><span data-stu-id="fe603-152">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="fe603-153">**Opcional:** un hash MD5 si elige usar uno.</span><span class="sxs-lookup"><span data-stu-id="fe603-153">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="fe603-154">Use el ejemplo siguiente para configurar el emparejamiento privado de Azure para su circuito:</span><span class="sxs-lookup"><span data-stu-id="fe603-154">Use the following example to configure Azure private peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  <span data-ttu-id="fe603-155">Si decide usar un hash MD5, use el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fe603-155">If you choose to use an MD5 hash, use the following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="fe603-156">Asegúrese de especificar su número AS como ASN de configuración entre pares, no como cliente ASN.</span><span class="sxs-lookup"><span data-stu-id="fe603-156">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  > 

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="fe603-157">Visualización de los detalles del emparejamiento privado</span><span class="sxs-lookup"><span data-stu-id="fe603-157">To view Azure private peering details</span></span>

<span data-ttu-id="fe603-158">Puede obtener detalles sobre la configuración mediante el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fe603-158">You can get configuration details by using the following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

<span data-ttu-id="fe603-159">La salida es similar a la del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fe603-159">The output is similar to the following example:</span></span>

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

### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="fe603-160">Actualización del establecimiento de configuración del emparejamiento privado de Azure</span><span class="sxs-lookup"><span data-stu-id="fe603-160">To update Azure private peering configuration</span></span>

<span data-ttu-id="fe603-161">Puede actualizar cualquier parte de la configuración mediante el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="fe603-161">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="fe603-162">En este ejemplo, se va a actualizar el identificador de VLAN del circuito de 100 a 500.</span><span class="sxs-lookup"><span data-stu-id="fe603-162">In this example, the VLAN ID of the circuit is being updated from 100 to 500.</span></span>

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="fe603-163">Eliminación del emparejamiento privado de Azure</span><span class="sxs-lookup"><span data-stu-id="fe603-163">To delete Azure private peering</span></span>

<span data-ttu-id="fe603-164">Puede quitar la configuración de emparejamiento mediante la ejecución del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fe603-164">You can remove your peering configuration by running the following example:</span></span>

> [!WARNING]
> <span data-ttu-id="fe603-165">Debe asegurarse de que todas las redes virtuales estén desvinculadas del circuito ExpressRoute antes de ejecutar este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="fe603-165">You must ensure that all virtual networks are unlinked from the ExpressRoute circuit before running this example.</span></span> 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a><span data-ttu-id="fe603-166">Configuración entre pares públicos de Azure</span><span class="sxs-lookup"><span data-stu-id="fe603-166">Azure public peering</span></span>

<span data-ttu-id="fe603-167">Esta sección le ayuda a crear, obtener, actualizar y eliminar la configuración de emparejamiento público de Azure para un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fe603-167">This section helps you create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="fe603-168">Creación de un emparejamiento público de Azure</span><span class="sxs-lookup"><span data-stu-id="fe603-168">To create Azure public peering</span></span>

1. <span data-ttu-id="fe603-169">Instale la versión más reciente de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="fe603-169">Install the latest version of Azure CLI.</span></span> <span data-ttu-id="fe603-170">Debe usar la versión más reciente de la Interfaz de la línea de comandos de Azure (CLI)*. Revise los [requisitos previos](expressroute-prerequisites.md) y los [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="fe603-170">You must use the latest version of the Azure Command-line Interface (CLI).* Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="fe603-171">Seleccione la suscripción para la que desea crear un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fe603-171">Select the subscription for which you want to create ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="fe603-172">Crear un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fe603-172">Create an ExpressRoute circuit.</span></span>  <span data-ttu-id="fe603-173">Siga las instrucciones para crear un [circuito ExpressRoute](howto-circuit-cli.md) y habilite su aprovisionamiento a través del proveedor de conectividad.</span><span class="sxs-lookup"><span data-stu-id="fe603-173">Follow the instructions to create an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="fe603-174">Si su proveedor de conectividad ofrece servicios administrados de nivel 3, puede solicitarle que habilite la configuración entre pares privados de Azure.</span><span class="sxs-lookup"><span data-stu-id="fe603-174">If your connectivity provider offers managed Layer 3 services, you can request that your connectivity provider enables Azure private peering for you.</span></span> <span data-ttu-id="fe603-175">En ese caso, no necesita seguir las instrucciones que aparecen en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="fe603-175">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="fe603-176">Sin embargo, si el proveedor de conectividad no administra el enrutamiento por usted, después de crear el circuito, continúe con la configuración mediante los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="fe603-176">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="fe603-177">Compruebe el circuito ExpressRoute para asegurarse de que está aprovisionado y también habilitado.</span><span class="sxs-lookup"><span data-stu-id="fe603-177">Check the ExpressRoute circuit to ensure it is provisioned and also enabled.</span></span> <span data-ttu-id="fe603-178">Utilice el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fe603-178">Use the following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="fe603-179">La respuesta es similar al siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fe603-179">The response is similar to the following example:</span></span>

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

4. <span data-ttu-id="fe603-180">Establezca la configuración del emparejamiento publico de Azure para el circuito.</span><span class="sxs-lookup"><span data-stu-id="fe603-180">Configure Azure public peering for the circuit.</span></span> <span data-ttu-id="fe603-181">Asegúrese de que tiene la siguiente información antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="fe603-181">Make sure that you have the following information before you proceed further.</span></span>

  * <span data-ttu-id="fe603-182">Una subred /30 para el vínculo principal.</span><span class="sxs-lookup"><span data-stu-id="fe603-182">A /30 subnet for the primary link.</span></span> <span data-ttu-id="fe603-183">Tiene que ser un prefijo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="fe603-183">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="fe603-184">Una subred /30 para el vínculo secundario.</span><span class="sxs-lookup"><span data-stu-id="fe603-184">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="fe603-185">Tiene que ser un prefijo IPv4 público válido.</span><span class="sxs-lookup"><span data-stu-id="fe603-185">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="fe603-186">Un identificador VLAN válido para establecer esta configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="fe603-186">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="fe603-187">Asegúrese de que ninguna otra configuración entre pares en el circuito usa el mismo identificador de VLAN.</span><span class="sxs-lookup"><span data-stu-id="fe603-187">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="fe603-188">Número de sistema autónomo (AS) para la configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="fe603-188">AS number for peering.</span></span> <span data-ttu-id="fe603-189">Puede usar 2 bytes o 4 bytes como números AS.</span><span class="sxs-lookup"><span data-stu-id="fe603-189">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="fe603-190">**Opcional:** un hash MD5 si elige usar uno.</span><span class="sxs-lookup"><span data-stu-id="fe603-190">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="fe603-191">Ejecute el siguiente ejemplo para configurar el emparejamiento público de Azure para su circuito:</span><span class="sxs-lookup"><span data-stu-id="fe603-191">Run the following example to configure Azure public peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  <span data-ttu-id="fe603-192">Si decide usar un hash MD5, use el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fe603-192">If you choose to use an MD5 hash, use the following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="fe603-193">Asegúrese de especificar su número AS como ASN de configuración entre pares, no como cliente ASN.</span><span class="sxs-lookup"><span data-stu-id="fe603-193">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="fe603-194">Visualización de detalles de un emparejamiento público de Azure</span><span class="sxs-lookup"><span data-stu-id="fe603-194">To view Azure public peering details</span></span>

<span data-ttu-id="fe603-195">Puede obtener detalles sobre la configuración mediante el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fe603-195">You can get configuration details using the following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

<span data-ttu-id="fe603-196">La salida es similar a la del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fe603-196">The output is similar to the following example:</span></span>

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

### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="fe603-197">Actualización del establecimiento de configuración del emparejamiento público de Azure</span><span class="sxs-lookup"><span data-stu-id="fe603-197">To update Azure public peering configuration</span></span>

<span data-ttu-id="fe603-198">Puede actualizar cualquier parte de la configuración mediante el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="fe603-198">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="fe603-199">En este ejemplo, se va a actualizar el identificador de VLAN del circuito de 200 a 600.</span><span class="sxs-lookup"><span data-stu-id="fe603-199">In this example, the VLAN ID of the circuit is being updated from 200 to 600.</span></span>

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="fe603-200">Eliminación del emparejamiento público de Azure</span><span class="sxs-lookup"><span data-stu-id="fe603-200">To delete Azure public peering</span></span>

<span data-ttu-id="fe603-201">Puede quitar la configuración de emparejamiento mediante la ejecución del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fe603-201">You can remove your peering configuration by running the following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a><span data-ttu-id="fe603-202">Emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="fe603-202">Microsoft peering</span></span>

<span data-ttu-id="fe603-203">Esta sección le ayuda a crear, obtener, actualizar y eliminar la configuración de emparejamiento de Microsoft para un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fe603-203">This section helps you create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fe603-204">Se anunciarán todos los prefijos de servicio para el emparejamiento de Microsoft de los circuitos ExpressRoute que se configuraron antes del 1 de agosto de 2017, incluso si no se definen filtros de ruta.</span><span class="sxs-lookup"><span data-stu-id="fe603-204">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through the Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="fe603-205">No se anunciará ningún prefijo para el emparejamiento de Microsoft de los circuitos ExpressRoute que se configuraron el 1 de agosto de 2017 o con posterioridad, hasta que se asocie un filtro de ruta al circuito.</span><span class="sxs-lookup"><span data-stu-id="fe603-205">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span> <span data-ttu-id="fe603-206">Para más información, consulte [Configuración de un filtro de ruta para el emparejamiento de Microsoft](how-to-routefilter-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fe603-206">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="fe603-207">Creación del emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="fe603-207">To create Microsoft peering</span></span>

1. <span data-ttu-id="fe603-208">Instale la versión más reciente de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="fe603-208">Install the latest version of Azure CLI.</span></span> <span data-ttu-id="fe603-209">Use la versión más reciente de la Interfaz de la línea de comandos de Azure (CLI)*. Revise los [requisitos previos](expressroute-prerequisites.md) y los [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="fe603-209">Use the latest version of the Azure Command-line Interface (CLI).* Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="fe603-210">Seleccione la suscripción para la que desea crear un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fe603-210">Select the subscription for which you want to create ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="fe603-211">Crear un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="fe603-211">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="fe603-212">Siga las instrucciones para crear un [circuito ExpressRoute](howto-circuit-cli.md) y habilite su aprovisionamiento a través del proveedor de conectividad.</span><span class="sxs-lookup"><span data-stu-id="fe603-212">Follow the instructions to create an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="fe603-213">Si su proveedor de conectividad ofrece servicios administrados de nivel 3, puede solicitarle que habilite la configuración entre pares privados de Azure.</span><span class="sxs-lookup"><span data-stu-id="fe603-213">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="fe603-214">En ese caso, no necesita seguir las instrucciones que aparecen en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="fe603-214">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="fe603-215">Sin embargo, si el proveedor de conectividad no administra el enrutamiento por usted, después de crear el circuito, continúe con la configuración mediante los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="fe603-215">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>

3. <span data-ttu-id="fe603-216">Compruebe el circuito ExpressRoute para asegurarse de que está aprovisionado y también habilitado.</span><span class="sxs-lookup"><span data-stu-id="fe603-216">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="fe603-217">Utilice el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fe603-217">Use the following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="fe603-218">La respuesta es similar al siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fe603-218">The response is similar to the following example:</span></span>

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

4. <span data-ttu-id="fe603-219">Establezca la configuración del emparejamiento de Microsoft para el circuito.</span><span class="sxs-lookup"><span data-stu-id="fe603-219">Configure Microsoft peering for the circuit.</span></span> <span data-ttu-id="fe603-220">Asegúrese de que tiene la siguiente información antes de empezar:</span><span class="sxs-lookup"><span data-stu-id="fe603-220">Make sure that you have the following information before you proceed.</span></span>

  * <span data-ttu-id="fe603-221">Una subred /30 para el vínculo principal.</span><span class="sxs-lookup"><span data-stu-id="fe603-221">A /30 subnet for the primary link.</span></span> <span data-ttu-id="fe603-222">Debe ser un prefijo de IPv4 público válido que sea de su propiedad y esté registrado en un Registro regional de Internet (RIR) o un Registro de enrutamiento de Internet (IRR).</span><span class="sxs-lookup"><span data-stu-id="fe603-222">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="fe603-223">Una subred /30 para el vínculo secundario.</span><span class="sxs-lookup"><span data-stu-id="fe603-223">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="fe603-224">Debe ser un prefijo de IPv4 público válido que sea de su propiedad y esté registrado en un Registro regional de Internet (RIR) o un Registro de enrutamiento de Internet (IRR).</span><span class="sxs-lookup"><span data-stu-id="fe603-224">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="fe603-225">Un identificador VLAN válido para establecer esta configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="fe603-225">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="fe603-226">Asegúrese de que ninguna otra configuración entre pares en el circuito usa el mismo identificador de VLAN.</span><span class="sxs-lookup"><span data-stu-id="fe603-226">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="fe603-227">Número de sistema autónomo (AS) para la configuración entre pares.</span><span class="sxs-lookup"><span data-stu-id="fe603-227">AS number for peering.</span></span> <span data-ttu-id="fe603-228">Puede usar 2 bytes o 4 bytes como números AS.</span><span class="sxs-lookup"><span data-stu-id="fe603-228">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="fe603-229">Prefijos anunciados: tiene que proporcionar una lista de todos los prefijos que planea anunciar en la sesión BGP.</span><span class="sxs-lookup"><span data-stu-id="fe603-229">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="fe603-230">Se aceptan solo prefijos de direcciones IP públicas.</span><span class="sxs-lookup"><span data-stu-id="fe603-230">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="fe603-231">Si tiene pensado enviar un conjunto de prefijos, puede enviar una lista separada por comas.</span><span class="sxs-lookup"><span data-stu-id="fe603-231">If you plan to send a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="fe603-232">Estos prefijos tienen que estar registrados a su nombre en un Registro regional de Internet (RIR) o un Registro de enrutamiento de Internet (IRR).</span><span class="sxs-lookup"><span data-stu-id="fe603-232">These prefixes must be registered to you in an RIR / IRR.</span></span>
  * <span data-ttu-id="fe603-233">**Opcional:** Cliente ASN: si los prefijos anunciados no están registrados en el número AS de emparejamiento, puede especificar el número de AS en el que están registrados.</span><span class="sxs-lookup"><span data-stu-id="fe603-233">**Optional -** Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span>
  * <span data-ttu-id="fe603-234">Nombre del enrutamiento del Registro: puede especificar el RIR o TIR en el que están registrados el número AS y los prefijos.</span><span class="sxs-lookup"><span data-stu-id="fe603-234">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="fe603-235">**Opcional:** un hash MD5 si elige usar uno.</span><span class="sxs-lookup"><span data-stu-id="fe603-235">**Optional -** An MD5 hash if you choose to use one.</span></span>

   <span data-ttu-id="fe603-236">Ejecute el ejemplo siguiente para configurar el emparejamiento de Microsoft para el circuito:</span><span class="sxs-lookup"><span data-stu-id="fe603-236">Run the following example to configure Microsoft peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="to-get-microsoft-peering-details"></a><span data-ttu-id="fe603-237">Obtención de detalles del emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="fe603-237">To get Microsoft peering details</span></span>

<span data-ttu-id="fe603-238">Puede obtener detalles sobre la configuración mediante el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fe603-238">You can get configuration details by using the following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

<span data-ttu-id="fe603-239">La salida es similar a la del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fe603-239">The output is similar to the following example:</span></span>

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

### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="fe603-240">Actualización de la configuración de emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="fe603-240">To update Microsoft peering configuration</span></span>

<span data-ttu-id="fe603-241">Puede actualizar cualquier parte de la configuración.</span><span class="sxs-lookup"><span data-stu-id="fe603-241">You can update any part of the configuration.</span></span> <span data-ttu-id="fe603-242">En el siguiente ejemplo, los prefijos anunciados del circuito se están actualizando de 123.1.0.0/24 a 124.1.0.0/24:</span><span class="sxs-lookup"><span data-stu-id="fe603-242">The advertised prefixes of the circuit are being updated from 123.1.0.0/24 to 124.1.0.0/24 in the following example:</span></span>

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="fe603-243">Eliminación del emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="fe603-243">To delete Microsoft peering</span></span>

<span data-ttu-id="fe603-244">Puede quitar la configuración de emparejamiento mediante la ejecución del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fe603-244">You can remove your peering configuration by running the following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a><span data-ttu-id="fe603-245">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fe603-245">Next steps</span></span>

<span data-ttu-id="fe603-246">Siguiente paso, [Vinculación de redes virtuales a circuitos ExpressRoute](howto-linkvnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="fe603-246">Next step, [Link a VNet to an ExpressRoute circuit](howto-linkvnet-cli.md).</span></span>

* <span data-ttu-id="fe603-247">Para más información sobre los flujos de trabajo de ExpressRoute, vea [Flujos de trabajo de ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="fe603-247">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="fe603-248">Para más información sobre el emparejamiento de circuitos, vea [Circuitos y dominios de enrutamiento de ExpressRoute](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="fe603-248">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="fe603-249">Para más información sobre redes virtuales, vea [Información general sobre redes virtuales](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fe603-249">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>