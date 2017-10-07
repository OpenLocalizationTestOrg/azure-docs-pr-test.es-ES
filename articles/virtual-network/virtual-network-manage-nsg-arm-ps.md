---
title: aaaManage de red de grupos de seguridad - PowerShell de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomanage red grupos de seguridad mediante PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3706ce6c-d9ae-46cb-a048-f0a4e84dc5cc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 930fe5e0827896ad67b24d84e41a5d3f898ba838
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-powershell"></a>Administración de grupos de seguridad de red mediante PowerShell

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md). Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar del modelo de implementación clásica de Hola.
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="retrieve-information"></a>Recuperar información
Puede consultar los NSG existentes, recuperar las reglas de un NSG existente y averiguar cuáles son los recursos a los que está asociado un NSG.

### <a name="view-existing-nsgs"></a>Consultar los NSG existentes
tooview todos los NSG existentes en una suscripción, ejecute hello `Get-AzureRmNetworkSecurityGroup` cmdlet.

Resultado esperado:

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : WEB1
    ResourceGroupName    : RG101
    Location             : eastus2
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG101/providers/M
                           icrosoft.Network/networkSecurityGroups/WEB1
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]


lista de hello tooview de NSG en un grupo de recursos específico, ejecute hello `Get-AzureRmNetworkSecurityGroup` cmdlet.

Resultado esperado:

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

### <a name="list-all-rules-for-an-nsg"></a>Mostrar todas las reglas de un NSG
reglas de hello tooview de un NSG denominado **front-end de NSG**, escriba el siguiente comando de hello:

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd | Select SecurityRules -ExpandProperty SecurityRules
```

Resultado esperado:

    Name                     : rdp-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow RDP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 100
    Direction                : Inbound

    Name                     : web-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow HTTP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 80
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 101
    Direction                : Inbound

> [!NOTE]
> También puede usar `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` las reglas predeterminadas de toolist Hola de hello **front-end de NSG** NSG.
> 

### <a name="view-nsgs-associations"></a>Consultar las asociaciones de NSG
tooview qué Hola recursos **front-end de NSG** NSG está asociado con la, hello ejecución del siguiente comando:

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
```

Busque hello **NetworkInterfaces** y **subredes** propiedades tal y como se muestra a continuación:

    NetworkInterfaces    : []
    Subnets              : [
                             {
                               "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                               "IpConfigurations": []
                             }
                           ]

En el ejemplo anterior de hello, hello NSG no está asociado tooany interfaces de red (NIC); es subred tooa asociado con el nombre **front-end**.

## <a name="manage-rules"></a>Administrar las reglas
Puede agregar tooan de reglas existente NSG, editar las reglas existentes y quitar las reglas.

### <a name="add-a-rule"></a>Agregar una regla
tooadd una regla que permite **entrante** tráfico tooport **443** desde cualquier máquina toohello **front-end de NSG** NSG, Hola completa pasos:

1. Comando hello tooretrieve existente NSG siguiente de ejecución hello y almacenarlo en una variable:

    ```powershell   
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Ejecute hello después comando tooadd un NSG de toohello de regla:

    ```powershell
    Add-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. realizado los cambios de hello toosave toohello NSG, ejecute el siguiente comando de hello:

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
    Resultado esperado que muestra hello solo las reglas de seguridad:
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "*",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="change-a-rule"></a>Cambiar una regla
regla de hello toochange creada anteriormente tooallow el tráfico entrante desde hello **Internet** solo, siga estos pasos Hola.

1. Comando hello tooretrieve existente NSG siguiente de ejecución hello y almacenarlo en una variable:

    ```powershell 
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Ejecute hello siguiente comando con la nueva configuración de la regla de hello:

    ```powershell
    Set-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix Internet `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. realizado los cambios de hello toosave toohello NSG, ejecute el siguiente comando de hello:

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    Resultado esperado que muestra hello solo las reglas de seguridad:
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="delete-a-rule"></a>Eliminar una regla
1. Comando hello tooretrieve existente NSG siguiente de ejecución hello y almacenarlo en una variable:

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Ejecute hello siguiendo la regla de comando tooremove Hola de hello NSG:

    ```powershell
    Remove-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name https-rule
    ```

3. Guarde los cambios realizados de hello toohello NSG, ejecutando el siguiente comando de hello:

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    Resultado esperado que muestra solo hello las reglas de seguridad, observe hello **regla https** ya no aparece:
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 }
                               ]

## <a name="manage-associations"></a>Administrar las asociaciones
Puede asociar un NSG toosubnets y NIC. También puede desasociar un NSG de cualquier recurso al que está asociado.

### <a name="associate-an-nsg-tooa-nic"></a>Asociar una NIC de NSG tooa
Hola tooassociate **front-end de NSG** NSG toohello **TestNICWeb1** NIC, Hola completa pasos:

1. Comando hello tooretrieve existente NSG siguiente de ejecución hello y almacenarlo en una variable:

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Comando hello tooretrieve existente NIC siguiente de ejecución hello y almacenarlo en una variable:

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

3. Conjunto hello **grupos** propiedad de hello **NIC** valor toohello variable del programa Hola a **NSG** variable, escribiendo el siguiente comando de hello:

    ```powershell
    $nic.NetworkSecurityGroup = $nsg
    ```

4. realizado los cambios de hello toosave toohello NIC, ejecute el siguiente comando de hello:

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    Hola de resultado esperado que se muestra solo **grupos** propiedad:
   
        NetworkSecurityGroup : {
                                 "SecurityRules": [],
                                 "DefaultSecurityRules": [],
                                 "NetworkInterfaces": [],
                                 "Subnets": [],
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                               }

### <a name="dissociate-an-nsg-from-a-nic"></a>Desasociar un NSG de una NIC
Hola toodissociate **front-end de NSG** NSG de hello **TestNICWeb1** NIC, Hola completa pasos:

1. Comando hello tooretrieve existente NIC siguiente de ejecución hello y almacenarlo en una variable:

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

2. Conjunto hello **grupos** propiedad de hello **NIC** variable demasiado**$null** ejecutando el siguiente comando de hello:

    ```powershell
    $nic.NetworkSecurityGroup = $null
    ```

3. realizado los cambios de hello toosave toohello NIC, ejecute el siguiente comando de hello:

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    Hola de resultado esperado que se muestra solo **grupos** propiedad:
   
        NetworkSecurityGroup : null

### <a name="dissociate-an-nsg-from-a-subnet"></a>Desasociar un NSG de una subred
Hola toodissociate **front-end de NSG** NSG de hello **front-end** subred, Hola completa pasos:

1. Ejecute hello después comando tooretrieve hello existente de la red virtual y almacenarla en una variable:

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. Ejecución hello siguientes comando tooretrieve hello **front-end** subred y almacenarlo en una variable:

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. Conjunto hello **grupos** propiedad de hello **subred** variable demasiado**$null** escribiendo el siguiente comando de hello:

    ```powershell
    $subnet.NetworkSecurityGroup = $null
    ```

4. realizan cambios de hello toosave toohello subred, ejecute el siguiente comando de hello:

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    Resultado esperado que muestran solo Hola propiedades de hello **front-end** subred. Observe que no hay una propiedad para **NetworkSecurityGroup**:
   
            ...
            Subnets           : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                      },
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                      }
                                    ],
                                    "ProvisioningState": "Succeeded"
                                  },
                                    ...
                                ]

### <a name="associate-an-nsg-tooa-subnet"></a>Asociar una subred de tooa NSG
Hola tooassociate **front-end de NSG** NSG toohello **FronEnd** subred nuevo, completa Hola pasos:

1. Ejecute hello después comando tooretrieve hello existente de la red virtual y almacenarla en una variable:

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. Ejecución hello siguientes comando tooretrieve hello **front-end** subred y almacenarlo en una variable:

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. Comando hello tooretrieve existente NSG siguiente de ejecución hello y almacenarlo en una variable:

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

4. Conjunto hello **grupos** propiedad de hello **subred** variable demasiado**$null** ejecutando el siguiente comando de hello:

    ```powershell
    $subnet.NetworkSecurityGroup = $nsg
    ```

5. realizan cambios de hello toosave toohello subred, ejecute el siguiente comando de hello:

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    Hola de resultado esperado que se muestra solo **grupos** propiedad de hello **front-end** subred:
   
        ...
        "NetworkSecurityGroup": {
                                  "SecurityRules": [],
                                  "DefaultSecurityRules": [],
                                  "NetworkInterfaces": [],
                                  "Subnets": [],
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                }
        ...

## <a name="delete-an-nsg"></a>Eliminación de un grupo de seguridad de red
Sólo se puede eliminar un NSG si no tiene asociados recursos tooany. toodelete un NSG, siga estos pasos Hola.

1. los recursos de hello toocheck asociados tooan NSG, ejecute hello `azure network nsg show` tal y como se muestra en [NSG vista asociaciones](#View-NSGs-associations).
2. Si hello NSG está asociado tooany NIC, ejecute hello `azure network nic set` tal y como se muestra en [desasociar un NSG de una NIC](#Dissociate-an-NSG-from-a-NIC) para cada NIC. 
3. Si hello NSG está asociado tooany subred, ejecute hello `azure network vnet subnet set` tal y como se muestra en [desasociar un NSG de subred](#Dissociate-an-NSG-from-a-subnet) para cada subred.
4. Hola toodelete NSG, ejecute el siguiente comando de hello:

    ```powershell
    Remove-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd -Force
    ```
   
   > [!NOTE]
   > Hola `-Force` parámetro garantiza la eliminación de hello tooconfirm no es necesario.
   > 

## <a name="next-steps"></a>Pasos siguientes
* [Habilite el registro](virtual-network-nsg-manage-log.md) para los NSG.

