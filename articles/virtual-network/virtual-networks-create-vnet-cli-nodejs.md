---
title: aaaCreate una red virtual con Hola 1.0 de CLI de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una red virtual con Hola 1.0 de CLI de Azure | Administrador de recursos."
services: virtual-network
documentationcenter: 
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.openlocfilehash: f48a8b23a5994164b71c9b51ee8a6810d17f9392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli"></a>Crear una red virtual con hello CLI de Azure

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Azure cuenta con dos modelos de implementación: Azure Resource Manager y el clásico. Microsoft recomienda crear recursos a través del modelo de implementación del Administrador de recursos de Hola. Obtenga más información sobre toolearn Hola diferencias entre Hola dos modelos, leer hello [modelos de implementación de Azure comprender](../azure-resource-manager/resource-manager-deployment-model.md) artículo.

## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello
Puede completar la tarea hello mediante uno de hello después de las versiones CLI:

- [Azure 2.0 CLI](virtual-networks-create-vnet-arm-cli.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola
- [Azure 1.0 de CLI](#create-a-virtual-network) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)

 
[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a>Crear una red virtual

toocreate una red virtual con Hola CLI de Azure, Hola completa pasos:

1. Instalar y configurar Hola CLI de Azure por hello siguiente pasos en hello [instalar y configurar hello Azure CLI](../cli-install-nodejs.md) artículo.

2. Creación de una red virtual y una subred:

    ```azurecli
    azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
    ```

    Resultado esperado:
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK

    Parámetros usados:

   * **--vnet**. Nombre de hello toobe de red virtual creado. En este escenario, *TestVNet*
   * **-e (o --address-space)**. Espacio de direcciones de red virtual. En este escenario, *192.168.0.0*
   * **-i (o -cidr)**. Máscara de red en formato CIDR. En este escenario, *16*.
   * **-n (o --subnet-name**). Nombre de la primera subred de Hola. En este escenario, *FrontEnd*.
   * **-p (or --subnet-start-ip)**. Dirección IP inicial de la subred o el espacio de direcciones de la subred. En este escenario, *192.168.1.0*.
   * **-r (o --subnet-cidr)**. Máscara de red en formato CIDR para subred. En este escenario, *24*.
   * **-l (o --location)**. Región de Azure donde se crea Hola red virtual. En este escenario, *Central US*.

3. Creación de una subred:

    ```azurecli
    azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
    ```
   
    Resultado esperado:

            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK

    Parámetros usados:

   * **-t (o --vnet-name**. Nombre de red virtual donde se creará la subred de Hola Hola. En este escenario, *TestVNet*.
   * **-n (o --name)**. Nombre de subred nueva Hola. En este escenario, *BackEnd*.
   * **-a (or --address-prefix)**. Bloque CIDR de subred. En este escenario, *192.168.2.0/24*.
   
4. propiedades de hello tooview de Hola nueva red virtual:

    ```azurecli
    azure network vnet show
    ```
   
    Resultado esperado:
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo tooconnect:

- Una red virtual de máquina virtual (VM) tooa leyendo hello [crear una VM Linux](../virtual-machines/linux/quick-create-cli.md) artículo. En lugar de crear una red virtual y la subred en los pasos de Hola de artículos de hello, puede seleccionar una red virtual existente y la subred tooconnect una máquina virtual a.
- Hola redes virtuales de red virtual tooother leyendo hello [conectar redes virtuales](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) artículo.
- Hola tooan de red virtual local de la red mediante una red privada virtual (VPN) de sitio a sitio o el circuito de ExpressRoute. Obtenga información acerca de cómo leyendo hello [conectar una red de red virtual tooan local mediante una VPN de sitio a sitio](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) y [vincular un circuito de ExpressRoute de red virtual tooan](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).
