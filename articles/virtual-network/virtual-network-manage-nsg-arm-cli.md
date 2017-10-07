---
title: aaaManage de red de grupos de seguridad - 2.0 de CLI de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomanage grupos de seguridad de red mediante hello Azure interfaz de línea de comandos (CLI) 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed17d314-07e6-4c7f-bcf1-a8a2535d7c14
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a3036b465e1e4049cba00e5e13ce1b479a2301d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-cli-20"></a><span data-ttu-id="e962c-103">Administrar grupos de seguridad de red mediante Hola 2.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="e962c-103">Manage network security groups using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="e962c-104">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="e962c-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="e962c-105">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="e962c-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="e962c-106">[Azure 1.0 de CLI](virtual-network-manage-nsg-cli-nodejs.md) – nuestro CLI para modelos de implementación de administración de recursos y clásico Hola</span><span class="sxs-lookup"><span data-stu-id="e962c-106">[Azure CLI 1.0](virtual-network-manage-nsg-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="e962c-107">[Azure 2.0 CLI](#View-existing-NSGs) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de hello (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="e962c-107">[Azure CLI 2.0](#View-existing-NSGs) - our next generation CLI for hello resource management deployment model (this article)</span></span>


[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="e962c-108">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e962c-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e962c-109">Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar del modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="e962c-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="prerequisite"></a><span data-ttu-id="e962c-110">Requisito previo</span><span class="sxs-lookup"><span data-stu-id="e962c-110">Prerequisite</span></span>
<span data-ttu-id="e962c-111">Si aún no lo ha aún, instalar y configurar hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) e inicie sesión con cuenta de Azure de tooan [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="e962c-111">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 


## <a name="view-existing-nsgs"></a><span data-ttu-id="e962c-112">Consultar los NSG existentes</span><span class="sxs-lookup"><span data-stu-id="e962c-112">View existing NSGs</span></span>
<span data-ttu-id="e962c-113">lista de hello tooview de NSG en un grupo de recursos específico, ejecute hello [lista de nsg de red az](/cli/azure/network/nsg#list) comando con un `-o table` formato de salida:</span><span class="sxs-lookup"><span data-stu-id="e962c-113">tooview hello list of NSGs in a specific resource group, run hello [az network nsg list](/cli/azure/network/nsg#list) command with a `-o table` output format:</span></span>

```azurecli
az network nsg list -g RG-NSG -o table
```

<span data-ttu-id="e962c-114">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="e962c-114">Expected output:</span></span>

    Location    Name          ProvisioningState    ResourceGroup    ResourceGuid
    ----------  ------------  -------------------  ---------------  ------------------------------------
    centralus   NSG-BackEnd   Succeeded            RG-NSG           <guid>
    centralus   NSG-FrontEnd  Succeeded            RG-NSG           <guid>

## <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="e962c-115">Mostrar todas las reglas de un NSG</span><span class="sxs-lookup"><span data-stu-id="e962c-115">List all rules for an NSG</span></span>
<span data-ttu-id="e962c-116">reglas de hello tooview de un NSG denominado **front-end de NSG**, hello ejecute [presentación con az red nsg](/cli/azure/network/nsg#show) comando mediante un [filtro de consulta JMESPATH](/cli/azure/query-az-cli2) hello y `-o table` formato de salida:</span><span class="sxs-lookup"><span data-stu-id="e962c-116">tooview hello rules of an NSG named **NSG-FrontEnd**, run hello [az network nsg show](/cli/azure/network/nsg#show) command using a [JMESPATH query filter](/cli/azure/query-az-cli2) and hello `-o table` output format:</span></span>

```azurecli
    az network nsg show \
    --resource-group RG-NSG \
    --name NSG-FrontEnd \
    --query '[defaultSecurityRules[],securityRules[]][].{Name:name,Desc:description,Access:access,Direction:direction,DestPortRange:destinationPortRange,DestAddrPrefix:destinationAddressPrefix,SrcPortRange:sourcePortRange,SrcAddrPrefix:sourceAddressPrefix}' \
    -o table
```

<span data-ttu-id="e962c-117">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="e962c-117">Expected output:</span></span>

    Name                           Desc                                                    Access    Direction    DestPortRange    DestAddrPrefix    SrcPortRange    SrcAddrPrefix
    -----------------------------  ------------------------------------------------------  --------  -----------  ---------------  ----------------  --------------  -----------------
    AllowVnetInBound               Allow inbound traffic from all VMs in VNET              Allow     Inbound      *                VirtualNetwork    *               VirtualNetwork
    AllowAzureLoadBalancerInBound  Allow inbound traffic from azure load balancer          Allow     Inbound      *                *                 *               AzureLoadBalancer
    DenyAllInBound                 Deny all inbound traffic                                Deny      Inbound      *                *                 *               *
    AllowVnetOutBound              Allow outbound traffic from all VMs tooall VMs in VNET  Allow     Outbound     *                VirtualNetwork    *               VirtualNetwork
    AllowInternetOutBound          Allow outbound traffic from all VMs tooInternet         Allow     Outbound     *                Internet          *               *
    DenyAllOutBound                Deny all outbound traffic                               Deny      Outbound     *                *                 *               *
    rdp-rule                                                                               Allow     Inbound      3389             *                 *               Internet
    web-rule                                                                               Allow     Inbound      80               *                 *               Internet
> [!NOTE]
> <span data-ttu-id="e962c-118">También puede usar [lista de reglas de nsg de red az](/cli/azure/network/nsg/rule#list) solo reglas personalizadas de hello toolist de un NSG.</span><span class="sxs-lookup"><span data-stu-id="e962c-118">You can also use [az network nsg rule list](/cli/azure/network/nsg/rule#list) toolist only hello custom rules from an NSG .</span></span>
>

## <a name="view-nsg-associations"></a><span data-ttu-id="e962c-119">Consultar las asociaciones de NSG</span><span class="sxs-lookup"><span data-stu-id="e962c-119">View NSG associations</span></span>

<span data-ttu-id="e962c-120">tooview qué Hola recursos **front-end de NSG** NSG está asociado con la, ejecute hello `az network nsg show` comando tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="e962c-120">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello `az network nsg show` command as shown below.</span></span> 

```azurecli
az network nsg show -g RG-NSG -n nsg-frontend --query '[subnets,networkInterfaces]'
```

<span data-ttu-id="e962c-121">Busque hello **networkInterfaces** y **subredes** propiedades tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="e962c-121">Look for hello **networkInterfaces** and **subnets** properties as shown below:</span></span>

```json
[
  [
    {
      "addressPrefix": null,
      "etag": null,
      "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/FrontEnd",
      "ipConfigurations": null,
      "name": null,
      "networkSecurityGroup": null,
      "provisioningState": null,
      "resourceGroup": "RG-NSG",
      "resourceNavigationLinks": null,
      "routeTable": null
    }
  ],
  null
]
```

<span data-ttu-id="e962c-122">En el ejemplo de Hola anterior, hello NSG no está asociado tooany interfaces de red (NIC) y es subred tooa asociado con el nombre **front-end**.</span><span class="sxs-lookup"><span data-stu-id="e962c-122">In hello example above, hello NSG is not associated tooany network interfaces (NICs), and it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="add-a-rule"></a><span data-ttu-id="e962c-123">Agregar una regla</span><span class="sxs-lookup"><span data-stu-id="e962c-123">Add a rule</span></span>
<span data-ttu-id="e962c-124">tooadd una regla que permite **entrada** tráfico tooport **443** desde cualquier máquina toohello **front-end de NSG** NSG, escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="e962c-124">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, enter hello following command:</span></span>

```azurecli
az network nsg rule create  \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd  \
--name allow-https \
--description "Allow access tooport 443 for HTTPS" \
--access Allow \
--protocol Tcp  \
--direction Inbound \
--priority 102 \
--source-address-prefix "*"  \
--source-port-range "*"  \
--destination-address-prefix "*" \
--destination-port-range "443"
```

<span data-ttu-id="e962c-125">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="e962c-125">Expected output:</span></span>

```json
{
  "access": "Allow",
  "description": "Allow access tooport 443 for HTTPS",
  "destinationAddressPrefix": "*",
  "destinationPortRange": "443",
  "direction": "Inbound",
  "etag": "W/\"<guid>\"",
  "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https",
  "name": "allow-https",
  "priority": 102,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "RG-NSG",
  "sourceAddressPrefix": "*",
  "sourcePortRange": "*"
}
```

## <a name="change-a-rule"></a><span data-ttu-id="e962c-126">Cambiar una regla</span><span class="sxs-lookup"><span data-stu-id="e962c-126">Change a rule</span></span>
<span data-ttu-id="e962c-127">regla de hello toochange creada anteriormente tooallow el tráfico entrante desde hello **Internet** solo, ejecute hello [actualización de reglas de nsg de red az](/cli/azure/network/nsg/rule#update) comando:</span><span class="sxs-lookup"><span data-stu-id="e962c-127">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command:</span></span>

```azurecli
az network nsg rule update \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https \
--source-address-prefix Internet
```

<span data-ttu-id="e962c-128">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="e962c-128">Expected output:</span></span>

```json
{
"access": "Allow",
"description": "Allow access tooport 443 for HTTPS",
"destinationAddressPrefix": "*",
"destinationPortRange": "443",
"direction": "Inbound",
"etag": "W/\"<guid>\"",
"id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https",
"name": "allow-https",
"priority": 102,
"protocol": "Tcp",
"provisioningState": "Succeeded",
"resourceGroup": "RG-NSG",
"sourceAddressPrefix": "Internet",
"sourcePortRange": "*"
}
```

## <a name="delete-a-rule"></a><span data-ttu-id="e962c-129">Eliminar una regla</span><span class="sxs-lookup"><span data-stu-id="e962c-129">Delete a rule</span></span>
<span data-ttu-id="e962c-130">regla de hello toodelete creada anteriormente, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="e962c-130">toodelete hello rule created above, run hello following command:</span></span>

```azurecli
az network nsg rule delete \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https
```


## <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="e962c-131">Asociar una NIC de NSG tooa</span><span class="sxs-lookup"><span data-stu-id="e962c-131">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="e962c-132">Hola tooassociate **front-end de NSG** NSG toohello **TestNICWeb1** NIC, use hello [actualizar la nic de red az](/cli/azure/network/nic#update) comando:</span><span class="sxs-lookup"><span data-stu-id="e962c-132">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, use hello [az network nic update](/cli/azure/network/nic#update) command:</span></span>

```azurecli
az network nic update \
--resource-group RG-NSG \
--name TestNICWeb1 \
--network-security-group NSG-FrontEnd    
```

<span data-ttu-id="e962c-133">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="e962c-133">Expected output:</span></span>

```json
{
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": [],
    "internalDnsNameLabel": null,
    "internalDomainNameSuffix": "k0wkaguidnqrh0ud.gx.internal.cloudapp.net",
    "internalFqdn": null
  },
  "enableAcceleratedNetworking": false,
  "enableIpForwarding": false,
  "etag": "W/\"<guid>\"",
  "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1",
  "ipConfigurations": [
    {
      "applicationGatewayBackendAddressPools": null,
      "etag": "W/\"<guid>\"",
      "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1",
      "loadBalancerBackendAddressPools": null,
      "loadBalancerInboundNatRules": null,
      "name": "ipconfig1",
      "primary": true,
      "privateIpAddress": "192.168.1.6",
      "privateIpAddressVersion": "IPv4",
      "privateIpAllocationMethod": "Static",
      "provisioningState": "Succeeded",
      "publicIpAddress": null,
      "resourceGroup": "RG-NSG",
      "subnet": {
        "addressPrefix": null,
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
        "ipConfigurations": null,
        "name": null,
        "networkSecurityGroup": null,
        "provisioningState": null,
        "resourceGroup": "RG-NSG",
        "resourceNavigationLinks": null,
        "routeTable": null
      }
    }
  ],
  "location": "centralus",
  "macAddress": "00-0D-3A-91-A9-60",
  "name": "TestNICWeb1",
  "networkSecurityGroup": {
    "defaultSecurityRules": null,
    "etag": null,
    "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
    "location": null,
    "name": null,
    "networkInterfaces": null,
    "provisioningState": null,
    "resourceGroup": "RG-NSG",
    "resourceGuid": null,
    "securityRules": null,
    "subnets": null,
    "tags": null,
    "type": null
  },
  "primary": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "RG-NSG",
  "resourceGuid": "<guid>",
  "tags": {},
  "type": "Microsoft.Network/networkInterfaces",
  "virtualMachine": null
}
```

## <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="e962c-134">Desasociar un NSG de una NIC</span><span class="sxs-lookup"><span data-stu-id="e962c-134">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="e962c-135">Hola toodissociate **front-end de NSG** NSG de hello **TestNICWeb1** NIC, ejecute hello [actualización de reglas de nsg de red az](/cli/azure/network/nsg/rule#update) comando nuevo pero reemplace hello `--network-security-group` argumento con una cadena vacía (`""`).</span><span class="sxs-lookup"><span data-stu-id="e962c-135">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command again but replace hello `--network-security-group` argument with an empty string (`""`).</span></span>

```azurecli
az network nic update --resource-group RG-NSG --name TestNICWeb3 --network-security-group ""
```

<span data-ttu-id="e962c-136">En la salida de hello, Hola `networkSecurityGroup` clave se establece toonull.</span><span class="sxs-lookup"><span data-stu-id="e962c-136">In hello output, hello `networkSecurityGroup` key is set toonull.</span></span>

## <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="e962c-137">Desasociar un NSG de una subred</span><span class="sxs-lookup"><span data-stu-id="e962c-137">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="e962c-138">Hola toodissociate **front-end de NSG** NSG de hello **front-end** subred, vuelva a ejecutar hello [actualización de reglas de nsg de red az](/cli/azure/network/nsg/rule#update) comando nuevo pero reemplace hello `--network-security-group` argumento con una cadena vacía (`""`).</span><span class="sxs-lookup"><span data-stu-id="e962c-138">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, again run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command again but replace hello `--network-security-group` argument with an empty string (`""`).</span></span>

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group ""
```

<span data-ttu-id="e962c-139">En la salida de hello, Hola `networkSecurityGroup` clave se establece toonull.</span><span class="sxs-lookup"><span data-stu-id="e962c-139">In hello output, hello `networkSecurityGroup` key is set toonull.</span></span>

## <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="e962c-140">Asociar una subred de tooa NSG</span><span class="sxs-lookup"><span data-stu-id="e962c-140">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="e962c-141">Hola tooassociate **front-end de NSG** NSG toohello **front-end** subred nuevo, ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e962c-141">tooassociate hello **NSG-FrontEnd** NSG toohello **FrontEnd** subnet again, run hello following command:</span></span>

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group NSG-FrontEnd
```

<span data-ttu-id="e962c-142">En la salida de hello, Hola `networkSecurityGroup` clave tiene algo similar para el valor de hello:</span><span class="sxs-lookup"><span data-stu-id="e962c-142">In hello output, hello `networkSecurityGroup` key has something similar for hello value:</span></span>

```json
"networkSecurityGroup": {
    "defaultSecurityRules": null,
    "etag": null,
    "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
    "location": null,
    "name": null,
    "networkInterfaces": null,
    "provisioningState": null,
    "resourceGroup": "RG-NSG",
    "resourceGuid": null,
    "securityRules": null,
    "subnets": null,
    "tags": null,
    "type": null
  }
  ```

## <a name="delete-an-nsg"></a><span data-ttu-id="e962c-143">Eliminación de un grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="e962c-143">Delete an NSG</span></span>
<span data-ttu-id="e962c-144">Sólo se puede eliminar un NSG si no tiene asociados recursos tooany.</span><span class="sxs-lookup"><span data-stu-id="e962c-144">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="e962c-145">toodelete un NSG, siga estos pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="e962c-145">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="e962c-146">los recursos de hello toocheck asociados tooan NSG, ejecute hello `azure network nsg show` tal y como se muestra en [NSG vista asociaciones](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="e962c-146">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="e962c-147">Si hello NSG está asociado tooany NIC, ejecute hello `azure network nic set` tal y como se muestra en [desasociar un NSG de una NIC](#Dissociate-an-NSG-from-a-NIC) para cada NIC.</span><span class="sxs-lookup"><span data-stu-id="e962c-147">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="e962c-148">Si hello NSG está asociado tooany subred, ejecute hello `azure network vnet subnet set` tal y como se muestra en [desasociar un NSG de subred](#Dissociate-an-NSG-from-a-subnet) para cada subred.</span><span class="sxs-lookup"><span data-stu-id="e962c-148">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="e962c-149">Hola toodelete NSG, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="e962c-149">toodelete hello NSG, run hello following command:</span></span>

    ```azurecli
    az network nsg delete --resource-group RG-NSG --name NSG-FrontEnd
    ```
## <a name="next-steps"></a><span data-ttu-id="e962c-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e962c-150">Next steps</span></span>
* <span data-ttu-id="e962c-151">[Habilite el registro](virtual-network-nsg-manage-log.md) para los NSG.</span><span class="sxs-lookup"><span data-stu-id="e962c-151">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

