---
title: aaaOpen puertos tooa Linux VM con Azure CLI 2.0 | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooopen un puerto o cree una VM de Linux tooyour de punto de conexión mediante la implementación del Administrador de recursos de Azure Hola modelar y Hola 2.0 de CLI de Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: eef9842b-495a-46cf-99a6-74e49807e74e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c79b31206e97558171609cf033bb3cb3370777c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-and-endpoints-tooa-linux-vm-with-hello-azure-cli"></a>Abrir puertos y los puntos de conexión tooa VM de Linux con hello CLI de Azure
Abrir un puerto, o crear un punto de conexión, tooa máquina virtual (VM) de Azure mediante la creación de un filtro de red en una subred o una interfaz de red de máquina virtual. Estos filtros, que controlan el tráfico entrante y saliente, se coloca en un recurso de grupo de seguridad de red conectado toohello que recibe el tráfico de Hola. Vamos a usar un ejemplo común de tráfico web en el puerto 80. Este artículo muestra cómo tooopen una tooa de puerto virtual con hello 2.0 de CLI de Azure. También puede realizar estos pasos con hello [Azure CLI 1.0](nsg-quickstart-nodejs.md).


## <a name="quick-commands"></a>Comandos rápidos
Grupo de seguridad de red de toocreate y reglas que necesita más reciente Hola [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).

En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores. Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *myNetworkSecurityGroup* y *myVnet*.

Crear grupo de seguridad de red de hello con [crear az red nsg](/cli/azure/network/nsg#create). Hello en el ejemplo siguiente se crea un grupo de seguridad de red denominado *myNetworkSecurityGroup* en hello *eastus* ubicación:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

Agregar una regla con [crear regla de nsg de red az](/cli/azure/network/nsg/rule#create) tooallow HTTP tráfico tooyour webserver (o ajustar para su propia situación, como conectividad de acceso o de base de datos SSH). Hello en el ejemplo siguiente se crea una regla denominada *myNetworkSecurityGroupRule* tooallow TCP de tráfico en el puerto 80:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 80
```

Asociar Hola grupo de seguridad de red con la interfaz de red de la máquina virtual (NIC) a [actualizar la nic de red az](/cli/azure/network/nic#update). Hello en el ejemplo siguiente se asocia un NIC existente denominado *myNic* con grupo de seguridad de red denominado hello *myNetworkSecurityGroup*:

```azurecli
az network nic update \
    --resource-group myResourceGroup \
    --name myNic \
    --network-security-group myNetworkSecurityGroup
```

Como alternativa, puede asociar el grupo de seguridad de red con una subred de red virtual con [actualización de subred de red virtual de red az](/cli/azure/network/vnet/subnet#update) en lugar de simplemente toohello interfaz de red en una sola máquina virtual. Hello en el ejemplo siguiente se asocia una subred existente denominada *mySubnet* en hello *myVnet* red virtual con hello grupo de seguridad de red denominado *myNetworkSecurityGroup*:

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="more-information-on-network-security-groups"></a>Más información sobre los grupos de seguridad de red
Hola de comandos rápido aquí le permite tooget seguridad y en ejecución con tooyour del flujo de tráfico máquina virtual. Grupos de seguridad de red proporcionan muchas características excepcionales y granularidad para controlar acceso a los recursos tooyour. Puede leer más sobre la [creación de un grupo de seguridad de red y las reglas de ACL aquí](tutorial-virtual-network.md#secure-network-traffic).

Para las aplicaciones web de alta disponibilidad, debe colocar las máquinas virtuales detrás de una instancia de Azure Load Balancer. equilibrador de carga de Hello distribuye el tráfico tooVMs, con un grupo de seguridad de red que proporciona filtrado de tráfico. Para obtener más información, consulte [cómo equilibrar tooload Linux virtual máquinas en Azure toocreate una aplicación de alta disponibilidad](tutorial-load-balancer.md).

## <a name="next-steps"></a>Pasos siguientes
En este ejemplo, ha creado el tráfico de tooallow HTTP de una regla sencilla. Puede encontrar información sobre cómo crear entornos más detallados en hello siguientes artículos:

* [Información general sobre Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)
* [¿Qué es un grupo de seguridad de red?](../../virtual-network/virtual-networks-nsg.md)
