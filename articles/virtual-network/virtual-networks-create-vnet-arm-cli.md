---
title: aaaCreate una red virtual - 2.0 de CLI de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una red virtual con Hola 2.0 de CLI de Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 75966bcc-0056-4667-8482-6f08ca38e77a
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e79b7fe780fc81f4866f810d830824e43a5a43b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli-20"></a>Crear una red virtual con hello 2.0 de CLI de Azure

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Azure cuenta con dos modelos de implementación: Azure Resource Manager y el clásico. Microsoft recomienda crear recursos a través del modelo de implementación del Administrador de recursos de Hola. Obtenga más información sobre toolearn Hola diferencias entre Hola dos modelos, leer hello [modelos de implementación de Azure comprender](../azure-resource-manager/resource-manager-deployment-model.md) artículo.

## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello
Puede completar la tarea hello mediante uno de hello después de las versiones CLI:

- [Azure 1.0 de CLI](virtual-networks-create-vnet-cli-nodejs.md) – nuestro CLI para modelos de implementación de administración de recursos y clásico Hola
- [Azure 2.0 CLI](#create-a-virtual-network) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de hello (en este artículo)'
 
    También puede crear una red virtual mediante el Administrador de recursos con otras herramientas o crear una red virtual a través del modelo de implementación clásica de hello seleccionando una opción diferente de hello lista siguiente:

> [!div class="op_single_selector"]
> * [Portal](virtual-networks-create-vnet-arm-pportal.md)
> * [PowerShell](virtual-networks-create-vnet-arm-ps.md)
> * [CLI](virtual-networks-create-vnet-arm-cli.md)
> * [Plantilla](virtual-networks-create-vnet-arm-template-click.md)
> * [Portal (clásico)](virtual-networks-create-vnet-classic-pportal.md)
> * [PowerShell (clásico)](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [CLI (clásico)](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]


## <a name="create-a-virtual-network"></a>Crear una red virtual

toocreate una red virtual con Hola CLI de Azure 2.0, Hola completa pasos:

1. Instalar y configurar hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) e inicie sesión con cuenta de Azure de tooan [inicio de sesión de az](/cli/azure/#login).

2. Crear un grupo de recursos para una red virtual con hello [crear grupo az](/cli/azure/group#create) comando con hello `--name` y `--location` argumentos:

    ```azurecli
    az group create --name TestRG --location centralus
    ```

3. Creación de una red virtual y una subred:

    ```azurecli
    az network vnet create \
    --name TestVNet \
    --resource-group TestRG \
    --location centralus \
    --address-prefix 192.168.0.0/16 \
    --subnet-name FrontEnd \
    --subnet-prefix 192.168.1.0/24
    ```

    Resultado esperado:
    
    ```json
    {
        "newVNet": {
            "addressSpace": {
            "addressPrefixes": [
            "192.168.0.0/16"
            ]
            },
            "dhcpOptions": {
            "dnsServers": []
            },
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>",
            "subnets": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                "name": "FrontEnd",
                "properties": {
                "addressPrefix": "192.168.1.0/24",
                "provisioningState": "Succeeded"
                },
                "resourceGroup": "TestRG"
            }
            ]
            }
    }
    ```

    Parámetros usados:

    - `--name TestVNet`: Nombre de hello toobe de red virtual creado.
    - `--resource-group TestRG`: nombre de grupo de recursos de Hola de # que controla el recurso de Hola. 
    - `--location centralus`: Hola ubicación en que toodeploy.
    - `--address-prefix 192.168.0.0/16`: Hola prefijo de dirección y el bloque.  
    - `--subnet-name FrontEnd`: nombre de Hola de subred de Hola.
    - `--subnet-prefix 192.168.1.0/24`: Hola prefijo de dirección y el bloque.

    toolist toouse de información básica de Hola Hola comando a continuación, puede realizar consultas Hola red virtual con un [filtro de consulta](/cli/azure/query-az-cli2):

    ```azurecli
    az network vnet list --query '[?name==`TestVNet`].{Where:location,Name:name,Group:resourceGroup}' -o table
    ```

    Lo que produce Hola después de salida:

        Where      Name      Group

        centralus  TestVNet  TestRG

4. Creación de una subred:

    ```azurecli
    az network vnet subnet create \
    --address-prefix 192.168.2.0/24 \
    --name BackEnd \
    --resource-group TestRG \
    --vnet-name TestVNet
    ```

    Resultado esperado:

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid> \"",
    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "TestRG",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```

    Parámetros usados:

    - `--address-prefix 192.168.2.0/24`: el bloque CIDR de subred.
    - `--name BackEnd`: Nombre de subred nueva Hola.
    - `--resource-group TestRG`: grupo de recursos de Hola.
    - `--vnet-name TestVNet`: nombre de Hola de hello propietaria de la red virtual.

5. Propiedades de Hola de consulta de Hola nueva red virtual:

    ```azurecli
    az network vnet show \
    -g TestRG \
    -n TestVNet \
    --query '{Name:name,Where:location,Group:resourceGroup,Status:provisioningState,SubnetCount:subnets | length(@)}' \
    -o table
    ```

    Resultado esperado:

        Name      Where      Group    Status       SubnetCount

        TestVNet  centralus  TestRG   Succeeded              2

6. Consultar propiedades de Hola de subredes de hello:

    ```azurecli
    az network vnet subnet list \
    -g TestRG \
    --vnet-name testvnet \
    --query '[].{Name:name,CIDR:addressPrefix,Status:provisioningState}' \
    -o table
    ```

    Resultado esperado:

        Name      CIDR            Status

        FrontEnd  192.168.1.0/24  Succeeded
        BackEnd   192.168.2.0/24  Succeeded

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo tooconnect:

- Una red virtual de máquina virtual (VM) tooa leyendo hello [crear una VM Linux](../virtual-machines/linux/quick-create-cli.md) artículo. En lugar de crear una red virtual y la subred en los pasos de Hola de artículos de hello, puede seleccionar una red virtual existente y la subred tooconnect una máquina virtual a.
- Hola redes virtuales de red virtual tooother leyendo hello [conectar redes virtuales](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) artículo.
- Hola tooan de red virtual local de la red mediante una red privada virtual (VPN) de sitio a sitio o el circuito de ExpressRoute. Obtenga información acerca de cómo leyendo hello [conectar una red de red virtual tooan local mediante una VPN de sitio a sitio](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) y [vincular un circuito de ExpressRoute de red virtual tooan](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).
