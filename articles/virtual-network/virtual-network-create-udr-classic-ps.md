---
title: "aaaControl enrutamiento en una red Virtual de Azure - PowerShell - clásico | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocontrol enrutamiento en redes virtuales mediante PowerShell | Clásico"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: d8d07c16-cbe5-4536-acd6-870269346fe3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 36edf263fb434d5fb13310d4324da20e57f016a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-powershell"></a>Control del enrutamiento y uso de aplicaciones virtuales (clásico) mediante PowerShell

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [CLI de Azure](virtual-network-create-udr-arm-cli.md)
> * [Plantilla](virtual-network-create-udr-arm-template.md)
> * [PowerShell (clásico)](virtual-network-create-udr-classic-ps.md)
> * [CLI (clásico)](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> Antes de trabajar con recursos de Azure, es importante toounderstand que Azure tiene dos modelos de implementación: Administrador de recursos de Azure y clásico. Asegúrese de que comprende los [modelos de implementación y las herramientas](../azure-resource-manager/resource-manager-deployment-model.md) antes de trabajar con recursos de Azure. Puede ver la documentación de Hola para distintas herramientas seleccionando una opción de la parte superior de Hola de este artículo. Este artículo trata el modelo de implementación clásica de Hola.
> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

ejemplo Hello Azure PowerShell siguientes comandos de esperan un entorno simple ya creado se basa en el escenario de hello anterior. Si desea toorun comandos de hello, que se muestran en este documento, crear se muestra en el entorno de hello [crear una red virtual (clásica) mediante PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a>Crear hello UDR para la subred de front-end de Hola
tabla de rutas de hello toocreate y ruta necesarios para una subred de front-end de hello basándose en el escenario de hello anterior, siga los pasos de hello siguientes.

1. Ejecute hello después comando toocreate una tabla de rutas de subred de front-end de hello:

    ```powershell
    New-AzureRouteTable -Name UDR-FrontEnd -Location uswest `
    -Label "Route table for front end subnet"
    ```

2. Ejecute hello después comando toocreate una ruta en toosend de tabla de ruta de hello todo el tráfico destinado toohello subred de back-end (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):

    ```powershell
    Get-AzureRouteTable UDR-FrontEnd `
    |Set-AzureRoute -RouteName RouteToBackEnd -AddressPrefix 192.168.2.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. Ejecución hello después de la tabla de rutas de comando tooassociate Hola con hello **front-end** subred:

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName FrontEnd `
    -RouteTableName UDR-FrontEnd
    ```

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>Crear hello UDR de subred de back-end de Hola
tabla de rutas de hello toocreate y ruta sea necesario para la copia de Hola finalizar una subred basándose en el escenario de hello, siga Hola siguiendo los pasos:

1. Ejecute hello después comando toocreate una tabla de rutas de subred de back-end de hello:

    ```powershell
    New-AzureRouteTable -Name UDR-BackEnd `
    -Location uswest `
    -Label "Route table for back end subnet"
    ```

2. Ejecute hello después comando toocreate una ruta en toosend de tabla de ruta de hello todo el tráfico destinado toohello subred front-end (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):

    ```powershell
    Get-AzureRouteTable UDR-BackEnd
    | Set-AzureRoute `
    -RouteName RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. Ejecución hello después de la tabla de rutas de comando tooassociate Hola con hello **back-end** subred:

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName BackEnd `
    -RouteTableName UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-hello-fw1-vm"></a>Habilitar el reenvío IP en hello FW1 VM

reenvío de IP tooenable en hello FW1 VM, Hola completa pasos:

1. Ejecute hello siguiendo el estado del comando toocheck Hola de reenvío IP:

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Get-AzureIPForwarding
    ```

2. Siguiente ejecución Hola comando tooenable el reenvío IP para hello *FW1* VM:

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Set-AzureIPForwarding -Enable
    ```
