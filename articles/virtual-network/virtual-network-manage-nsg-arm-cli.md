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
# <a name="manage-network-security-groups-using-hello-azure-cli-20"></a>Administrar grupos de seguridad de red mediante Hola 2.0 de CLI de Azure

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello 

Puede completar la tarea hello mediante uno de hello después de las versiones CLI: 

- [Azure 1.0 de CLI](virtual-network-manage-nsg-cli-nodejs.md) – nuestro CLI para modelos de implementación de administración de recursos y clásico Hola 
- [Azure 2.0 CLI](#View-existing-NSGs) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de hello (en este artículo)


[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md). Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar del modelo de implementación clásica de Hola.
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="prerequisite"></a>Requisito previo
Si aún no lo ha aún, instalar y configurar hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) e inicie sesión con cuenta de Azure de tooan [inicio de sesión de az](/cli/azure/#login). 


## <a name="view-existing-nsgs"></a>Consultar los NSG existentes
lista de hello tooview de NSG en un grupo de recursos específico, ejecute hello [lista de nsg de red az](/cli/azure/network/nsg#list) comando con un `-o table` formato de salida:

```azurecli
az network nsg list -g RG-NSG -o table
```

Resultado esperado:

    Location    Name          ProvisioningState    ResourceGroup    ResourceGuid
    ----------  ------------  -------------------  ---------------  ------------------------------------
    centralus   NSG-BackEnd   Succeeded            RG-NSG           <guid>
    centralus   NSG-FrontEnd  Succeeded            RG-NSG           <guid>

## <a name="list-all-rules-for-an-nsg"></a>Mostrar todas las reglas de un NSG
reglas de hello tooview de un NSG denominado **front-end de NSG**, hello ejecute [presentación con az red nsg](/cli/azure/network/nsg#show) comando mediante un [filtro de consulta JMESPATH](/cli/azure/query-az-cli2) hello y `-o table` formato de salida:

```azurecli
    az network nsg show \
    --resource-group RG-NSG \
    --name NSG-FrontEnd \
    --query '[defaultSecurityRules[],securityRules[]][].{Name:name,Desc:description,Access:access,Direction:direction,DestPortRange:destinationPortRange,DestAddrPrefix:destinationAddressPrefix,SrcPortRange:sourcePortRange,SrcAddrPrefix:sourceAddressPrefix}' \
    -o table
```

Resultado esperado:

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
> También puede usar [lista de reglas de nsg de red az](/cli/azure/network/nsg/rule#list) solo reglas personalizadas de hello toolist de un NSG.
>

## <a name="view-nsg-associations"></a>Consultar las asociaciones de NSG

tooview qué Hola recursos **front-end de NSG** NSG está asociado con la, ejecute hello `az network nsg show` comando tal y como se muestra a continuación. 

```azurecli
az network nsg show -g RG-NSG -n nsg-frontend --query '[subnets,networkInterfaces]'
```

Busque hello **networkInterfaces** y **subredes** propiedades tal y como se muestra a continuación:

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

En el ejemplo de Hola anterior, hello NSG no está asociado tooany interfaces de red (NIC) y es subred tooa asociado con el nombre **front-end**.

## <a name="add-a-rule"></a>Agregar una regla
tooadd una regla que permite **entrada** tráfico tooport **443** desde cualquier máquina toohello **front-end de NSG** NSG, escriba el siguiente comando de hello:

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

Resultado esperado:

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

## <a name="change-a-rule"></a>Cambiar una regla
regla de hello toochange creada anteriormente tooallow el tráfico entrante desde hello **Internet** solo, ejecute hello [actualización de reglas de nsg de red az](/cli/azure/network/nsg/rule#update) comando:

```azurecli
az network nsg rule update \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https \
--source-address-prefix Internet
```

Resultado esperado:

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

## <a name="delete-a-rule"></a>Eliminar una regla
regla de hello toodelete creada anteriormente, ejecute el siguiente comando de hello:

```azurecli
az network nsg rule delete \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https
```


## <a name="associate-an-nsg-tooa-nic"></a>Asociar una NIC de NSG tooa
Hola tooassociate **front-end de NSG** NSG toohello **TestNICWeb1** NIC, use hello [actualizar la nic de red az](/cli/azure/network/nic#update) comando:

```azurecli
az network nic update \
--resource-group RG-NSG \
--name TestNICWeb1 \
--network-security-group NSG-FrontEnd    
```

Resultado esperado:

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

## <a name="dissociate-an-nsg-from-a-nic"></a>Desasociar un NSG de una NIC

Hola toodissociate **front-end de NSG** NSG de hello **TestNICWeb1** NIC, ejecute hello [actualización de reglas de nsg de red az](/cli/azure/network/nsg/rule#update) comando nuevo pero reemplace hello `--network-security-group` argumento con una cadena vacía (`""`).

```azurecli
az network nic update --resource-group RG-NSG --name TestNICWeb3 --network-security-group ""
```

En la salida de hello, Hola `networkSecurityGroup` clave se establece toonull.

## <a name="dissociate-an-nsg-from-a-subnet"></a>Desasociar un NSG de una subred
Hola toodissociate **front-end de NSG** NSG de hello **front-end** subred, vuelva a ejecutar hello [actualización de reglas de nsg de red az](/cli/azure/network/nsg/rule#update) comando nuevo pero reemplace hello `--network-security-group` argumento con una cadena vacía (`""`).

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group ""
```

En la salida de hello, Hola `networkSecurityGroup` clave se establece toonull.

## <a name="associate-an-nsg-tooa-subnet"></a>Asociar una subred de tooa NSG
Hola tooassociate **front-end de NSG** NSG toohello **front-end** subred nuevo, ejecute hello siguiente comando:

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group NSG-FrontEnd
```

En la salida de hello, Hola `networkSecurityGroup` clave tiene algo similar para el valor de hello:

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

## <a name="delete-an-nsg"></a>Eliminación de un grupo de seguridad de red
Sólo se puede eliminar un NSG si no tiene asociados recursos tooany. toodelete un NSG, siga estos pasos Hola.

1. los recursos de hello toocheck asociados tooan NSG, ejecute hello `azure network nsg show` tal y como se muestra en [NSG vista asociaciones](#View-NSGs-associations).
2. Si hello NSG está asociado tooany NIC, ejecute hello `azure network nic set` tal y como se muestra en [desasociar un NSG de una NIC](#Dissociate-an-NSG-from-a-NIC) para cada NIC. 
3. Si hello NSG está asociado tooany subred, ejecute hello `azure network vnet subnet set` tal y como se muestra en [desasociar un NSG de subred](#Dissociate-an-NSG-from-a-subnet) para cada subred.
4. Hola toodelete NSG, ejecute el siguiente comando de hello:

    ```azurecli
    az network nsg delete --resource-group RG-NSG --name NSG-FrontEnd
    ```
## <a name="next-steps"></a>Pasos siguientes
* [Habilite el registro](virtual-network-nsg-manage-log.md) para los NSG.

