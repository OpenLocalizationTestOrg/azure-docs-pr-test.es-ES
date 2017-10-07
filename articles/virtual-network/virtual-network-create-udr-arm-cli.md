---
title: dispositivos de enrutamiento y virtual aaaControl utilizando Hola 2.0 de CLI de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocontrol dispositivos de enrutamiento y virtual utilizando Hola 2.0 de CLI de Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5452a0b8-21a6-4699-8d6a-e2d8faf32c25
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/12/2017
ms.author: jdial
ms.openlocfilehash: 79b908848932a4365dab1b7497b6a0dbf44bbaf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-20"></a>Crear rutas definidas por el usuario (UDR) mediante Hola 2.0 de CLI de Azure

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [CLI de Azure](virtual-network-create-udr-arm-cli.md)
> * [Plantilla](virtual-network-create-udr-arm-template.md)
> * [PowerShell: implementación clásica](virtual-network-create-udr-classic-ps.md)
> * [CLI: implementación clásica](virtual-network-create-udr-classic-cli.md)

## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello 

Puede completar la tarea hello mediante uno de hello después de las versiones CLI: 

- [Azure 1.0 de CLI](virtual-network-create-udr-arm-cli-nodejs.md) – nuestro CLI para modelos de implementación de administración de recursos y clásico Hola 
- [Azure 2.0 CLI](#Create-the-UDR-for-the-front-end-subnet) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de hello (en este artículo)

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

comandos de CLI de Azure de ejemplo de Hola a continuación esperan un entorno simple ya creado basándose en el escenario de hello anterior. Si desea toorun comandos de hello, que se muestran en este documento, en primer lugar crear entorno de prueba de hello implementando [esta plantilla](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), haga clic en **implementar tooAzure**, reemplace los valores de parámetros predeterminados de Hola Si fuera necesario y siga las instrucciones de hello en Hola portal.


## <a name="create-hello-udr-for-hello-front-end-subnet"></a>Crear hello UDR para la subred de front-end de Hola
tabla de rutas de hello toocreate y ruta necesarios para una subred de front-end de hello basándose en el escenario de hello anterior, siga los pasos de hello siguientes.

1. Crear una tabla de rutas de subred de front-end de hello con hello [crear tabla de rutas de red az](/cli/azure/network/route-table#create) comando:

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --location centralus \
    --name UDR-FrontEnd
    ```

    Salida:

    ```json
    {
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
    "location": "centralus",
    "name": "UDR-FrontEnd",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "routes": [],
    "subnets": null,
    "tags": null,
    "type": "Microsoft.Network/routeTables"
    }
    ```

2. Cree una ruta que envía todo el tráfico destinado toohello subred de back-end (192.168.2.0/24) toohello **FW1** máquina virtual (192.168.0.4) con hello [crear ruta de tabla de rutas de red az](/cli/azure/network/route-table/route#create) comando:

    ```azurecli 
    az network route-table route create \
    --resource-group testrg \
    --name RouteToBackEnd \
    --route-table-name UDR-FrontEnd \
    --address-prefix 192.168.2.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

    Salida:

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd/routes/RouteToBackEnd",
    "name": "RouteToBackEnd",
    "nextHopIpAddress": "192.168.0.4",
    "nextHopType": "VirtualAppliance",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg"
    }
    ```
    Parámetros:

    * **--route-table-name**. Nombre de tabla de rutas de Hola donde se agregará la ruta de Hola. En este escenario, *UDR-FrontEnd*.
    * **--address-prefix**. Prefijo de dirección de subred de Hola donde los paquetes destinados a. En este escenario, *192.168.2.0/24*.
    * **--next-hop-type**. Tipo de objeto al que se enviará el tráfico. Los valores posibles son *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* o *None*.
    * **--next-hop-ip-address**. Dirección IP para el próximo salto. En este escenario, *192.168.0.4*.

3. Ejecute hello [actualización de subred de red virtual de red az](/cli/azure/network/vnet/subnet#update) tabla de enrutamiento de comandos tooassociate Hola creada anteriormente con hello **front-end** subred:

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name FrontEnd \
    --route-table UDR-FrontEnd
    ```

    Salida:

    ```json
    {
    "addressPrefix": "192.168.1.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testvnet/subnets/FrontEnd",
    "ipConfigurations": null,
    "name": "FrontEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": {
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
        "location": null,
        "name": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "routes": null,
        "subnets": null,
        "tags": null,
        "type": null
        }
    }
    ```

    Parámetros:
    
    * **--vnet-name**. Nombre de red virtual donde se encuentra la subred de Hola Hola. En este escenario, *TestVNet*.

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>Crear hello UDR de subred de back-end de Hola

Hola toocreate tabla de rutas y necesarios para la subred de back-end de hello en función de hello escenario anterior, Hola completa siguiendo los pasos de ruta:

1. Ejecute hello después comando toocreate una tabla de rutas de subred de back-end de hello:

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --name UDR-BackEnd \
    --location centralus
    ```

2. Ejecute hello después comando toocreate una ruta en toosend de tabla de ruta de hello todo el tráfico destinado toohello subred front-end (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):

    ```azurecli
    az network route-table route create \
    --resource-group testrg \
    --name RouteToFrontEnd \
    --route-table-name UDR-BackEnd \
    --address-prefix 192.168.1.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

3. Ejecución hello después de la tabla de rutas de comando tooassociate Hola con hello **back-end** subred:

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name BackEnd \
    --route-table UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a>Habilitación del reenvío IP en FW1

reenvío de IP tooenable Hola NIC que se utiliza por **FW1**completa Hola lo siguiente:

1. Ejecute hello [show de nic de red az](/cli/azure/network/nic#show) comando con un hello de toodisplay JMESPATH filtro actual **Habilitar reenvío de ip** valor **reenvío IP habilitar**. Se debe establecer demasiado*false*.

    ```azurecli
    az network nic show \
    --resource-group testrg \
    --nname nicfw1 \
    --query 'enableIpForwarding' -o tsv
    ```

    Salida:

        false

2. Ejecute hello después de reenvío de IP de tooenable de comando:

    ```azurecli
    az network nic update \
    --resource-group testrg \
    --name nicfw1 \
    --ip-forwarding true
    ```

    Puede examinar la consola de toohello transmitido por secuencias de salida de hello, o simplemente volver a probar para saludo específico **enableIpForwarding** valor:

    ```azurecli
    az network nic show -g testrg -n nicfw1 --query 'enableIpForwarding' -o tsv
    ```

    Salida:

        true

    Parámetros:

    **--ip-forwarding**: *true* o *false*.

