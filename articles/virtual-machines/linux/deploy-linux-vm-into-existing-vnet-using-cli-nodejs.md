---
title: "aaaDeploy máquinas virtuales de Linux en la red existente con 1.0 de CLI de Azure | Documentos de Microsoft"
description: "¿Cómo toodeploy una VM de Linux en una red Virtual existente mediante Hola 1.0 de CLI de Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e660f1563d386efc7788bd236f8b067145ea09bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli-10"></a>¿Cómo toodeploy una máquina virtual de Linux en una red Virtual de Azure existente con hello Azure CLI 1.0

Este artículo muestra cómo toodeploy toouse 1.0 de CLI de Azure una máquina virtual (VM) en una red Virtual (VNet). Hola requisitos son:

- [una cuenta de Azure](https://azure.microsoft.com/pricing/free-trial/);
- [archivos de clave SSH pública y privada](mac-create-ssh-keys.md).


## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello
Puede completar la tarea hello mediante uno de hello después de las versiones CLI:

- [Azure 1.0 de CLI](#quick-commands) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)
- [Azure 2.0 CLI](deploy-linux-vm-into-existing-vnet-using-cli.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola


## <a name="quick-commands"></a>Comandos rápidos

Si necesita tooquickly realizar la tarea hello, Hola pasos de la sección detalles comandos Hola necesarios. Obtener más información y el contexto de cada paso se encuentran rest Hola de documento de hello, [a partir de aquí](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).

Requisitos previos: grupo de recursos, red virtual, NSG con SSH entrante, subred. Reemplace los ejemplos por su propia configuración.

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Implementar Hola VM en la infraestructura de red virtual de Hola

```azurecli
azure vm create myVM \
    -g myResourceGroup \
    -l eastus \
    -y linux \
    -Q Debian \
    -o mystorageaccount \
    -u myAdminUser \
    -M ~/.ssh/id_rsa.pub \
    -n myVM \
    -F myVNet \
    -j mySubnet \
    -N myVNic
```

## <a name="detailed-walkthrough"></a>Tutorial detallado

Activos de Azure como Hola redes virtuales y grupos de seguridad de red deben ser estáticos y larga duración recursos que rara vez se implementan. Una vez que se ha implementado una red virtual, se puede reutilizar con nuevas implementaciones sin ninguna infraestructura de toohello afectará de forma negativa. Imagine que una red virtual es un conmutador de red de hardware tradicional. No tendrá tooconfigure hardware completamente nuevo cambiar con cada implementación. Con una red virtual configurada correctamente, puede seguir el toodeploy nuevos servidores en esa red virtual una y otra vez con pocos, si lo hay, cambios necesarios durante la vigencia de Hola de hello red virtual.

## <a name="create-hello-resource-group"></a>Crear grupo de recursos de Hola

En primer lugar, cree una tooorganize de grupo de recursos todo lo que cree en este tutorial. Para más información sobre los grupos de recursos, consulte [Información general de Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-hello-vnet"></a>Crear red virtual de hello

Hola primer paso es toobuild Hola a las máquinas virtuales en un toolaunch de red virtual. Hola red virtual contiene una subred para este tutorial. Para obtener más información sobre redes virtuales de Azure, consulte [crear una red virtual mediante el uso de hello CLI de Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-hello-network-security-group"></a>Crear grupo de seguridad de red de Hola

subred de Hola se compila detrás de un grupo de seguridad de red existente por lo que crear grupo de seguridad de red de hello antes de subred Hola. Grupos de seguridad de red de Azure son firewall tooa equivalente en la capa de red Hola. Para obtener más información sobre los grupos de seguridad de red de Azure, vea [cómo grupos de seguridad de red de toocreate Hola CLI de Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Agregar regla de permiso de SSH entrante

Hola VM necesita acceso de hello internet para que una regla que permita el puerto de entrada 22 tráfico toobe pasa a través de la red de hello tooport 22 en hello VM es necesario.

```azurecli
azure network nsg rule create inboundSSH \
    --resource-group myResourceGroup \
    --nsg-name myNSG \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range 22 \
    --destination-address-prefix 10.10.0.0/24 \
    --destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a>Agregar una red virtual de toohello de subred

Las máquinas virtuales de hello red virtual deben estar ubicadas en una subred. Cada red virtual puede tener varias subredes. Crear una subred de Hola y asocie al grupo de seguridad de red de Hola.

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

Hola subred ahora se agregaron dentro de la red virtual de Hola y asociado a la regla y el grupo de seguridad de red de Hola.


## <a name="add-a-vnic-toohello-subnet"></a>Agregar una subred de toohello VNic

Tarjetas de red virtual (VNics) son importantes tal y como se puede reutilizar conectándolos toodifferent las máquinas virtuales. Este enfoque conserva Hola VNic como un recurso estático mientras hello las máquinas virtuales puede ser temporal. Cree un VNic y asociarla a la subred de hello creado en el paso anterior de Hola.

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>Implementar Hola VM en la red virtual de Hola y NSG

Ahora tiene una red virtual y subred dentro de esa red virtual y un grupo de seguridad de red actúan de subred de hello tooprotect bloqueando todo el tráfico entrante excepto el puerto 22 de SSH. Hola VM ahora pueden implementarse dentro de esta infraestructura de red existente.

Mediante Hola CLI de Azure y Hola `azure vm create` comando hello Linux VM está implementado toohello grupo de recursos de Azure, red virtual, subred y VNic existentes. Para obtener más información sobre el uso de hello CLI toodeploy una máquina virtual completa, consulte [crear un entorno completo de Linux mediante Hola CLI de Azure](create-cli-complete.md)

```azurecli
azure vm create myVM \
    --resource-group myResourceGroup \
    --location eastus \
    --os-type linux \
    --image-urn Debian \
    --storage-account-name mystorageaccount \
    --admin-username myAdminUser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --vnet-name myVNet \
    --vnet-subnet-name mySubnet \
    --nic-name myVNic
```

Mediante el uso de hello CLI marcas toocall recursos existentes, indicar hello toodeploy Azure VM dentro de la red existente Hola. Una vez que se ha implementado una red virtual y una subred, estas pueden dejarse como recursos estáticos o permanentes dentro de su región de Azure.  

## <a name="next-steps"></a>Pasos siguientes

* [Usar un toocreate de plantilla una implementación específica de Azure Resource Manager](../windows/cli-deploy-templates.md)
* [Creación de un entorno personalizado para una máquina virtual Linux mediante el uso de comandos de la CLI de Azure directamente](create-cli-complete.md)
* [Implementación y administración de máquinas virtuales con plantillas de Azure Resource Manager y la CLI de Azure](create-ssh-secured-vm-from-template.md)
