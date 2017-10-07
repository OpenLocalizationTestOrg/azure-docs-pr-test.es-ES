---
title: "aaaOpen puertos tooa máquina virtual mediante PowerShell de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooopen un puerto o cree una máquina virtual de Windows de punto de conexión tooyour con modo de implementación de administrador de recursos de Azure de Hola y PowerShell de Azure"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf45f7d8-451a-48ab-8419-730366d54f1e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c1817a0c447ae4ce7a1ce2a1fc6927bedf2dacb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-and-endpoints-tooa-vm-in-azure-using-powershell"></a>¿Cómo tooopen puertos y los puntos de conexión tooa VM en Azure con PowerShell
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a>Comandos rápidos
Grupo de seguridad de red de toocreate y reglas de ACL tiene [versión más reciente de Hola de PowerShell de Azure instalado](/powershell/azureps-cmdlets-docs). También puede [realizar estos pasos con el portal de Azure hello](nsg-quickstart-portal.md).

Inicie sesión en tooyour cuenta de Azure:

```powershell
Login-AzureRmAccount
```

En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores. Los nombres de parámetro de ejemplo incluían *myResourceGroup*, *myNetworkSecurityGroup* y *myVnet*.

Creación de una regla con [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig). Hello en el ejemplo siguiente se crea una regla denominada *myNetworkSecurityGroupRule* tooallow *tcp* tráfico en el puerto *80*:

```powershell
$httprule = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRule" `
    -Description "Allow HTTP" `
    -Access "Allow" `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority "100" `
    -SourceAddressPrefix "Internet" `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80
```

A continuación, cree el grupo de seguridad de red con [AzureRmNetworkSecurityGroup New](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) y asignar Hola HTTP regla que acaba de crear como sigue. Hello en el ejemplo siguiente se crea un grupo de seguridad de red denominado *myNetworkSecurityGroup*:

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName "myResourceGroup" `
    -Location "EastUS" `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $httprule
```

Ahora vamos a asignar la subred de tooa del grupo de seguridad de red. Hello en el ejemplo siguiente se asigna una red virtual existente denominada *myVnet* toohello variable *$vnet* con [AzureRmVirtualNetwork Get](/powershell/module/azurerm.network/get-azurermvirtualnetwork):

```powershell
$vnet = Get-AzureRmVirtualNetwork `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVnet"
```

Asocie el grupo de seguridad de red con la subred con [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig). Hello en el ejemplo siguiente se asocia con el nombre de subred de hello *mySubnet* con su grupo de seguridad de red:

```powershell
$subnetPrefix = $vnet.Subnets|?{$_.Name -eq 'mySubnet'}

Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name "mySubnet" `
    -AddressPrefix $subnetPrefix.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

Por último, actualizar la red virtual con [AzureRmVirtualNetwork conjunto](/powershell/module/azurerm.network/set-azurermvirtualnetwork) en orden para el efecto de tootake de cambios:

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```


## <a name="more-information-on-network-security-groups"></a>Más información sobre los grupos de seguridad de red
Hola de comandos rápido aquí le permite tooget seguridad y en ejecución con tooyour del flujo de tráfico máquina virtual. Grupos de seguridad de red proporcionan muchas características excepcionales y granularidad para controlar acceso a los recursos tooyour. Puede leer más sobre la [creación de un grupo de seguridad de red y las reglas de ACL aquí](tutorial-virtual-network.md#manage-internal-traffic).

Para las aplicaciones web de alta disponibilidad, debe colocar las máquinas virtuales detrás de una instancia de Azure Load Balancer. equilibrador de carga de Hello distribuye el tráfico tooVMs, con un grupo de seguridad de red que proporciona filtrado de tráfico. Para obtener más información, consulte [cómo equilibrar tooload Linux virtual máquinas en Azure toocreate una aplicación de alta disponibilidad](tutorial-load-balancer.md).

## <a name="next-steps"></a>Pasos siguientes
En este ejemplo, ha creado el tráfico de tooallow HTTP de una regla sencilla. Puede encontrar información sobre cómo crear entornos más detallados en hello siguientes artículos:

* [Información general sobre Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)
* [¿Qué es un grupo de seguridad de red?](../../virtual-network/virtual-networks-nsg.md)
* [Información general de Azure Resource Manager para equilibradores de carga](../../load-balancer/load-balancer-arm.md)

