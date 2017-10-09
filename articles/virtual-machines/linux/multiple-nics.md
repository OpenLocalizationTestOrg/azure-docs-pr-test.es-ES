---
title: una VM de Linux en Azure con varias NIC aaaCreate | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una VM de Linux con varias NIC había conectado tooit mediante plantillas de hello Azure CLI 2.0 o administrador de recursos."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 5d2d04d0-fc62-45fa-88b1-61808a2bc691
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2723405914777a5dce4354d4f5d8413e357f58e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a>¿Cómo toocreate una máquina virtual de Linux en Azure con red varias tarjetas de interfaz
Puede crear una máquina virtual (VM) de Azure que tiene varios tooit de interfaces (NIC) que están conectados de red virtual. Un escenario común es toohave subredes diferentes para la conectividad de front-end y back-end o una red dedicada tooa supervisión o una solución de copia de seguridad. Este artículo se detalla cómo toocreate una máquina virtual con varias NIC conectado tooit y cómo NIC tooadd o quitar de una máquina virtual existente. Para obtener información detallada, incluyendo cómo toocreate varios NIC dentro de su propio Bash secuencias de comandos, obtenga más información sobre [implementar máquinas virtuales de varias NIC](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md). Diferentes [tamaños de máquina virtual](sizes.md) admiten un número distinto de NIC, así que ajuste el tamaño de su máquina virtual teniendo esto en cuenta.

Este artículo detalla cómo toocreate una VM con varias NIC con Hola 2.0 de CLI de Azure. También puede realizar estos pasos con hello [Azure CLI 1.0](multiple-nics-nodejs.md).


## <a name="create-supporting-resources"></a>Creación de recursos de apoyo
Hola de instalación más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) e inicie sesión con cuenta de Azure de tooan [inicio de sesión de az](/cli/azure/#login).

En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores. Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *mystorageaccount* y *myVM*.

En primer lugar, cree un grupo de recursos con [az group create](/cli/azure/group#create). Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación:

```azurecli
az group create --name myResourceGroup --location eastus
```

Crear red virtual de hello con [crear red virtual de red az](/cli/azure/network/vnet#create). Hello en el ejemplo siguiente se crea una red virtual denominada *myVnet* y subred denominada *mySubnetFrontEnd*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

Crear una subred para el tráfico de back-end de hello con [crear subredes de red virtual de red az](/cli/azure/network/vnet/subnet#create). Hello en el ejemplo siguiente se crea una subred denominada *mySubnetBackEnd*:

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

Cree un grupo de seguridad de red con [az network nsg create](/cli/azure/network/nsg#create). Hello en el ejemplo siguiente se crea un grupo de seguridad de red denominado *myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a>Creación y configuración de varias NIC
Creación de dos NIC con [az network nic create](/cli/azure/network/nic#create). Hello en el ejemplo siguiente se crea dos NIC, denominadas *myNic1* y *myNic2*conectados grupo de seguridad de red de hello, con una NIC conectan tooeach subred:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic1 \
    --vnet-name myVnet \
    --subnet mySubnetFrontEnd \
    --network-security-group myNetworkSecurityGroup
az network nic create \
    --resource-group myResourceGroup \
    --name myNic2 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a>Crear una máquina virtual y adjuntar Hola NIC
Cuando creas Hola de máquina virtual, especifique Hola NIC creadas con `--nics`. También debe tootake cuidado al seleccionar Hola tamaño de máquina virtual. No hay límite para el número total de Hola de NIC que se puede agregar tooa VM. Más información sobre los [tamaños de máquina virtual Linux](sizes.md). 

Cree la máquina virtual con [az vm create](/cli/azure/vm#create). Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVM*:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --size Standard_DS3_v2 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic1 myNic2
```

## <a name="add-a-nic-tooa-vm"></a>Agregar un tooa NIC virtual
los pasos anteriores de Hello crean una máquina virtual con varias NIC. También puede agregar tooan NIC existente VM con hello 2.0 de CLI de Azure. 

Cree otra NIC con [az network nic create](/cli/azure/network/nic#create). Hello en el ejemplo siguiente se crea una NIC denominada *myNic3* conectado toohello subred de back-end y el grupo de seguridad de red creado en los pasos anteriores de hello:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

tooadd una NIC tooan VM existente, primero desasignar Hola VM con [az vm desasignar](/cli/azure/vm#deallocate). Hello en el ejemplo siguiente se desasigna Hola máquina virtual denominada *myVM*:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

Agregar Hola NIC con [agregar nic de vm az](/cli/azure/vm/nic#add). Agrega Hello en el ejemplo siguiente se *myNic3* demasiado*myVM*:

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

Iniciar Hola VM con [inicio de vm az](/cli/azure/vm#start):

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a>Eliminación de una NIC de una máquina virtual
tooremove una NIC de una máquina virtual existente, en primer lugar desasignar Hola VM con [cancelar la asignación de máquina virtual az](/cli/azure/vm#deallocate). Hello en el ejemplo siguiente se desasigna Hola máquina virtual denominada *myVM*:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

Quitar Hola NIC con [az vm nic quitar](/cli/azure/vm/nic#remove). Quita de Hello en el ejemplo siguiente se *myNic3* de *myVM*:

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

Iniciar Hola VM con [inicio de vm az](/cli/azure/vm#start):

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```


## <a name="create-multiple-nics-using-resource-manager-templates"></a>Creación de varias NIC con plantillas de Resource Manager
Plantillas de administrador de recursos de Azure utilizan declarativa toodefine de archivos JSON en su entorno. Puede leer la [introducción a Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md). Plantillas del Administrador de recursos proporcionan una manera toocreate varias instancias de un recurso durante la implementación, como la creación de varias NIC. Usa *copia* número de hello toospecify de toocreate de instancias:

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

Más información sobre la [creación de varias instancias mediante *copia*](../../resource-group-create-multiple.md). 

También puede usar un `copyIndex()` toothen anexar un nombre de recurso tooa número, que le permite toocreate `myNic1`, `myNic2`, etc. Hola continuación muestra un ejemplo de anexar el valor de índice de hello:

```json
"name": "[concat('myNic', copyIndex())]", 
```

Puede leer un ejemplo completo de [cómo crear varias NIC con plantillas de Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).

## <a name="next-steps"></a>Pasos siguientes
Revisión [tamaños de VM de Linux](sizes.md) al tratar de toocreating una máquina virtual con varias NIC. Pagar el número máximo de toohello de atención de NIC es compatible con el tamaño de cada máquina virtual. 
