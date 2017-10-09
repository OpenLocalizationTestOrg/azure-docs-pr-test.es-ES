---
title: "aaaControl enrutamiento en una red Virtual de Azure - CLI - clásico | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocontrol enrutamiento en redes virtuales mediante Hola CLI de Azure en el modelo de implementación clásica de Hola"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: ca2b4638-8777-4d30-b972-eb790a7c804f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 07dde573f1a605bf280156c261d51e213ede0cdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-hello-azure-cli"></a>Enrutamiento de control y el uso de dispositivos virtuales (clásicos) de uso Hola CLI de Azure

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [CLI de Azure](virtual-network-create-udr-arm-cli.md)
> * [Plantilla](virtual-network-create-udr-arm-template.md)
> * [PowerShell (clásico)](virtual-network-create-udr-classic-ps.md)
> * [CLI (clásico)](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artículo trata el modelo de implementación clásica de Hola. También puede [controlar el enrutamiento y usar dispositivos virtuales en el modelo de implementación del Administrador de recursos de hello](virtual-network-create-udr-arm-cli.md).

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

comandos de CLI de Azure de ejemplo de Hola a continuación esperan un entorno simple ya creado basándose en el escenario de hello anterior. Si desea toorun comandos de hello, que se muestran en este documento, crear se muestra en el entorno de hello [crear una red virtual (clásica) con hello Azure CLI](virtual-networks-create-vnet-classic-cli.md).

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a>Crear hello UDR para la subred de front-end de Hola
tabla de rutas de hello toocreate y ruta necesarios para una subred de front-end de hello basándose en el escenario de hello anterior, siga los pasos de hello siguientes.

1. Siguiente ejecución Hola comando tooswitch tooclassic modo:

    ```azurecli
    azure config mode asm
    ```

    Salida:

        info:    New mode is asm

2. Ejecute hello después comando toocreate una tabla de rutas de subred de front-end de hello:

    ```azurecli
    azure network route-table create -n UDR-FrontEnd -l uswest
    ```
   
    Salida:
   
        info:    Executing command network route-table create
        info:    Creating route table "UDR-FrontEnd"
        info:    Getting route table "UDR-FrontEnd"
        data:    Name                            : UDR-FrontEnd
        data:    Location                        : West US
        info:    network route-table create command OK
   
    Parámetros:
   
   * **-l (o --location)**. Región de Azure donde hello nuevo NSG se creará. En este escenario, *TestRG*.
   * **-n (o --name)**. Nombre de hello nuevo NSG. En este escenario, *NSG-FrontEnd*.
3. Ejecute hello después comando toocreate una ruta en toosend de tabla de ruta de hello todo el tráfico destinado toohello subred de back-end (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):

    ```azurecli
    azure network route-table route set -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

    Salida:
   
        info:    Executing command network route-table route set
        info:    Getting route table "UDR-FrontEnd"
        info:    Setting route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    network route-table route set command OK
   
    Parámetros:
   
   * **-r (o --route-table-name)**. Nombre de tabla de rutas de Hola donde se agregará la ruta de Hola. En este escenario, *UDR-FrontEnd*.
   * **-a (o --address-prefix)**. Prefijo de dirección de subred de Hola donde los paquetes destinados a. En este escenario, *192.168.2.0/24*.
   * **-t (o --next-hop-type)**. Tipo de objeto al que se enviará el tráfico. Los valores posibles son *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* o *None*.
   * **-p (o --next-hop-ip-address**). Dirección IP para el próximo salto. En este escenario, *192.168.0.4*.
4. Siguiente ejecución Hola comando tabla de rutas de hello tooassociate creado con hello **front-end** subred:

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    Salida:
   
        info:    Executing command network vnet subnet route-table add
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        info:    Associating route table "UDR-FrontEnd" and subnet "FrontEnd"
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        data:    Route table name                : UDR-FrontEnd
        data:      Location                      : West US
        data:      Routes:
        info:    network vnet subnet route-table add command OK    
   
    Parámetros:
   
   * **-t (o --vnet-name)**. Nombre de red virtual donde se encuentra la subred de Hola Hola. En este escenario, *TestVNet*.
   * **-n (o --subnet-name**. Nombre de tabla de rutas de Hola Hola subred se agregará a. En este escenario, *FrontEnd*.

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>Crear hello UDR de subred de back-end de Hola
tabla de rutas de hello toocreate y necesarios para la subred de back-end de hello en función de escenario de hello, Hola completa siguiendo los pasos de ruta:

1. Ejecute hello después comando toocreate una tabla de rutas de subred de back-end de hello:

    ```azurecli
    azure network route-table create -n UDR-BackEnd -l uswest
    ```

2. Ejecute hello después comando toocreate una ruta en toosend de tabla de ruta de hello todo el tráfico destinado toohello subred front-end (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):

    ```azurecli
    azure network route-table route set -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

3. Ejecución hello después de la tabla de rutas de comando tooassociate Hola con hello **back-end** subred:

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n BackEnd -r UDR-BackEnd
    ```

