---
title: aaaOpen puertos tooa VM de Linux con 1.0 de CLI de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooopen un puerto o cree una VM de Linux tooyour de punto de conexión mediante la implementación del Administrador de recursos de Azure Hola modelar y Hola 1.0 de CLI de Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 337c37d151f527b43d4852291159b2f70a00accc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="opening-ports-and-endpoints-tooa-linux-vm-in-azure-using-hello-azure-cli-10"></a>Abrir puertos y los puntos de conexión tooa VM de Linux en Azure mediante Hola 1.0 de CLI de Azure
Abrir un puerto, o crear un punto de conexión, tooa máquina virtual (VM) de Azure mediante la creación de un filtro de red en una subred o una interfaz de red de máquina virtual. Estos filtros, que controlan el tráfico entrante y saliente, se coloca en un recurso de grupo de seguridad de red conectado toohello que recibe el tráfico de Hola. Vamos a usar un ejemplo común de tráfico web en el puerto 80. Este artículo muestra cómo tooopen un puerto tooa VM con Hola 1.0 de CLI de Azure.


## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello
Puede completar la tarea hello mediante uno de hello después de las versiones CLI:

- [Azure 1.0 de CLI](#quick-commands) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)
- [Azure 2.0 CLI](nsg-quickstart.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola


## <a name="quick-commands"></a>Comandos rápidos
toocreate un grupo de seguridad de red y las reglas que necesita [hello Azure CLI 1.0](../../cli-install-nodejs.md) instalada y utiliza el modo de administrador de recursos:

```azurecli
azure config mode arm
```

En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores. Los nombres de parámetro de ejemplo incluían *myResourceGroup*, *myNetworkSecurityGroup* y *myVnet*.

Cree el grupo de seguridad de red y escriba sus propios nombres y su propia ubicación según sea adecuado. Hello en el ejemplo siguiente se crea un grupo de seguridad de red denominado *myNetworkSecurityGroup* en hello *eastus* ubicación:

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

Agregar un servidor Web tooyour de tráfico de regla tooallow HTTP (o ajustar para su propia situación, como conectividad de acceso o de base de datos SSH). Hello en el ejemplo siguiente se crea una regla denominada *myNetworkSecurityGroupRule* tooallow TCP de tráfico en el puerto 80:

```azurecli
azure network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --destination-port-range 80 \
    --access allow
```

Asociar Hola grupo de seguridad de red con la interfaz de red de la máquina virtual (NIC). Hello en el ejemplo siguiente se asocia un NIC existente denominado *myNic* con grupo de seguridad de red denominado hello *myNetworkSecurityGroup*:

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --name myNic
```

Como alternativa, puede asociar el grupo de seguridad de red con una subred de red virtual en lugar de simplemente toohello interfaz de red en una sola máquina virtual. Hello en el ejemplo siguiente se asocia una subred existente denominada *mySubnet* en hello *myVnet* red virtual con hello grupo de seguridad de red denominado *myNetworkSecurityGroup*:

```azurecli
azure network vnet subnet set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a>Más información sobre los grupos de seguridad de red
Hola de comandos rápido aquí le permite tooget seguridad y en ejecución con tooyour del flujo de tráfico máquina virtual. Grupos de seguridad de red proporcionan muchas características excepcionales y granularidad para controlar acceso a los recursos tooyour. Puede leer más sobre la [creación de un grupo de seguridad de red y las reglas de ACL aquí](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).

Los grupos de seguridad de red y las reglas de ACL también se pueden definir como parte de las plantillas de Azure Resource Manager. Más información sobre la [creación de grupos de seguridad de red con plantillas](../../virtual-network/virtual-networks-create-nsg-arm-template.md).

Si necesita toouse toomap de reenvío de puerto un puerto interno de tooan único puerto externo en la máquina virtual, use un equilibrador de carga y las reglas de traducción de direcciones de red (NAT). Por ejemplo, puede desee tooexpose el puerto TCP 8080 externamente y tener el tráfico dirigido tooTCP puerto 80 en una máquina virtual. Puede aprender sobre la [creación de un equilibrador de carga accesible desde Internet](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).

## <a name="next-steps"></a>Pasos siguientes
En este ejemplo, ha creado el tráfico de tooallow HTTP de una regla sencilla. Puede encontrar información sobre cómo crear entornos más detallados en hello siguientes artículos:

* [Información general sobre Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)
* [¿Qué es un grupo de seguridad de red?](../../virtual-network/virtual-networks-nsg.md)
* [Información general de Azure Resource Manager para equilibradores de carga](../../load-balancer/load-balancer-arm.md)

