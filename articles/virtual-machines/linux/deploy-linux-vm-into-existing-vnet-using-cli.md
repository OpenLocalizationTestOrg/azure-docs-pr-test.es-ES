---
title: "aaaDeploy máquinas virtuales de Linux en la red existente con 2.0 de CLI de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toodeploy una máquina virtual de Linux en una red Virtual existente mediante Hola 2.0 de CLI de Azure"
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
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0df44b3437002df050db56f3b3899083fb49d803
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli"></a>¿Cómo toodeploy una máquina virtual de Linux en una red Virtual de Azure existente con hello CLI de Azure

Este artículo muestra cómo toouse Hola toodeploy 2.0 de CLI de Azure a una máquina virtual (VM) en una red virtual existente. Hola requisitos son:

- [una cuenta de Azure](https://azure.microsoft.com/pricing/free-trial/);
- [archivos de clave SSH pública y privada](mac-create-ssh-keys.md).

También puede realizar estos pasos con hello [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).


## <a name="quick-commands"></a>Comandos rápidos
Si necesita tooquickly realizar la tarea hello, Hola pasos de la sección detalles comandos Hola necesarios. Obtener más información y el contexto de cada paso se encuentran rest Hola de documento de hello, [a partir de aquí](#detailed-walkthrough).

toocreate este entorno personalizado, deberá hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).

En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores. Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *myVnet* y *myVM*.

**Requisitos previos:** grupo de recursos de Azure, red virtual y subred, grupo de seguridad de red con SSH entrante y una tarjeta de interfaz de red virtual.

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Implementar Hola VM en la infraestructura de red virtual de Hola

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

## <a name="detailed-walkthrough"></a>Tutorial detallado

Los recursos de Azure, como las redes virtuales y los grupos de seguridad de red, deben ser recursos estáticos y de larga duración que se implementen con poca frecuencia. Una vez que se ha implementado una red virtual, se puede reutilizar con nuevas implementaciones sin ninguna infraestructura de toohello afectará de forma negativa. Piense en una red virtual como un conmutador de red tradicionales de hardware: no tendría tooconfigure hardware completamente nuevo cambiar con cada implementación. Con una red virtual configurada correctamente, puede continuar toodeploy nuevas máquinas virtuales en la red virtual una y otra vez con pocas, si lo hay, cambios necesario durante la vigencia de Hola de red virtual de Hola.

toocreate este entorno personalizado, deberá hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).

En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores. Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *myVnet* y *myVM*.

## <a name="create-hello-resource-group"></a>Crear grupo de recursos de Hola

En primer lugar, cree una tooorganize de grupo de recursos de Azure todo lo que cree en este tutorial. Para más información sobre los grupos de recursos, consulte [Información general de Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md). Crear grupo de recursos de hello con [crear grupo az](/cli/azure/group#create). Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación:

```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

## <a name="create-hello-virtual-network"></a>Crear red virtual de Hola

Permite generar un hello toolaunch de red virtual de Azure VM en. Para obtener más información sobre redes virtuales, vea [crear una red virtual mediante el uso de hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md). Crear red virtual de hello con [crear red virtual de red az](/cli/azure/network/vnet#create). Hello en el ejemplo siguiente se crea una red virtual denominada *myVnet* y subred denominada *mySubnet*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefix 10.10.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.10.1.0/24
```

## <a name="create-hello-network-security-group"></a>Crear grupo de seguridad de red de Hola

Grupos de seguridad de red de Azure son firewall tooa equivalente en la capa de red Hola. Para obtener más información sobre los grupos de seguridad de red, consulte [cómo grupos de seguridad de red de toocreate en hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md). Crear grupo de seguridad de red de hello con [crear az red nsg](/cli/azure/network/nsg#create). Hello en el ejemplo siguiente se crea un grupo de seguridad de red denominado *myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Agregar regla de permiso de SSH entrante

Hola VM necesita acceso de hello internet, por lo que una regla que permita el puerto de entrada 22 tráfico toobe pasa a través de la red de hello tooport 22 en hello VM es necesario. Agregar una regla de entrada para el grupo de seguridad de red de hello con [crear regla de nsg de red az](/cli/azure/network/nsg/rule#create). Hello en el ejemplo siguiente se crea una regla denominada *myNetworkSecurityGroupRuleSSH*:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --priority 1000 \
    --protocol tcp \
    --destination-port-range 22 \
```

## <a name="attach-hello-subnet-toohello-network-security-group"></a>Asociar el grupo de seguridad de red de hello subred toohello

reglas del grupo de seguridad de red de Hello pueden ser aplicada tooa subred o una interfaz de red virtual específica. Permite adjuntar Hola seguridad grupo tooour subred. Asociar el grupo de seguridad de red de subred toohello con [actualización de subred de red virtual de red az](/cli/azure/network/vnet/subnet#update):

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="add-a-virtual-network-interface-card-toohello-subnet"></a>Agregar una subred de toohello de tarjeta de interfaz de red virtual

Tarjetas de interfaz de red virtual (VNics) son importantes tal y como se puede reutilizar conectándolos toodifferent las máquinas virtuales. Volver a utilizar este permite tookeep Hola VNic como un recurso estático mientras hello las máquinas virtuales puede ser temporal. Crear un VNic y asociarla a la subred de hello con [crear nic de red az](/cli/azure/network/nic#create). Hello en el ejemplo siguiente se crea un VNic denominado *myNic*:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Implementar Hola VM en la infraestructura de red virtual de Hola

Ahora tiene una red virtual y subred y una subred de hello red tooprotect de grupo de seguridad bloqueando todo el tráfico entrante excepto el puerto 22 de SSH. Hola VM ahora pueden implementarse dentro de esta infraestructura de red existente.

Creee la máquina virtual con [az vm create](/cli/azure/vm#create). Para obtener más información sobre Hola marcas toouse con hello Azure CLI 2.0 toodeploy una máquina virtual completa, consulte [crear un entorno completo de Linux mediante el uso de hello Azure CLI](create-cli-complete.md).

Hola de ejemplo siguiente crea una máquina virtual mediante discos de Azure administrados. Estos discos se controlan mediante la plataforma Windows Azure hello y no requieren ningún toostore los preparativos o ubicación ellos. Para más información acerca de los discos administrados, consulte [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md) (Introducción a los discos administrados de Azure). Si desea que los discos toouse no administrado, vea la nota adicional de hello siguiente.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

Si usa Azure Managed Disks, omita este paso. Si desea que los discos toouse no administrado, deberá hello tooadd siguientes parámetros adicionales toohello continuar comando toocreate no administrada de discos en la cuenta de almacenamiento de hello denominada `mystorageaccount`: 

```azurecli
    --use-unmanaged-disk \
    --storage-account mystorageaccount
```

Mediante el uso de hello CLI marcas toocall recursos existentes, indicar hello toodeploy Azure VM dentro de la red existente Hola. Una vez que se ha implementado una red virtual y una subred, estas pueden dejarse como recursos estáticos o permanentes dentro de su región de Azure. En este ejemplo, no cree y asignar una toohello de dirección IP pública VNic, por lo que esta máquina virtual no es accesible públicamente sobre Hola Internet. Para obtener más información, consulte [crear una máquina virtual con una dirección IP pública estática con hello Azure CLI](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de las formas toocreate virtual máquinas en Azure, vea Hola recursos siguientes:

* [Usar un toocreate de plantilla una implementación específica de Azure Resource Manager](../windows/cli-deploy-templates.md)
* [Creación de un entorno personalizado para una máquina virtual Linux mediante el uso de comandos de la CLI de Azure directamente](create-cli-complete.md)
* [Implementación y administración de máquinas virtuales con plantillas de Azure Resource Manager y la CLI de Azure](create-ssh-secured-vm-from-template.md)
