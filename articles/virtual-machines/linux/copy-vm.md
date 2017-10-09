---
title: una VM de Linux mediante Azure CLI 2.0 aaaCopy | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una copia de la máquina virtual Linux de Azure mediante Azure CLI 2.0 y discos administrados."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 03/10/2017
ms.author: cynthn
ms.openlocfilehash: ee34a4259dd0c1e7bf49312fe3fe3ba809bf69e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-vm-by-using-azure-cli-20-and-managed-disks"></a>Creación de una copia de una máquina virtual Linux mediante la CLI de Azure 2.0 y los discos administrados


Este artículo muestra cómo toocreate una copia de la máquina virtual (VM de) Azure ejecutando Linux mediante Hola CLI de Azure 2.0 y el modelo de implementación de hello Azure Resource Manager. También puede realizar estos pasos con hello [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

También puede [cargar y crear una máquina virtual a partir de un VHD](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="prerequisites"></a>Requisitos previos


-   Instalar la [CLI de Azure 2.0](/cli/azure/install-az-cli2)

-   Inicie sesión en tooan Azure cuenta con [inicio de sesión de az](/cli/azure/#login).

-   Tener un toouse de máquina virtual de Azure como origen de hello para la copia.

## <a name="step-1-stop-hello-source-vm"></a>Paso 1: Detener Hola una VM de origen


Desasignar una VM de origen Hola utilizando [cancelar la asignación de máquina virtual az](/cli/azure/vm#deallocate).
Hello en el ejemplo siguiente se desasigna Hola máquina virtual denominada **myVM** en grupo de recursos de hello **myResourceGroup**:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

## <a name="step-2-copy-hello-source-vm"></a>Paso 2: Copiar una VM de origen Hola


toocopy una máquina virtual, cree una copia del disco de duro virtual subyacente Hola. Este proceso crea un disco duro virtual especializado como un disco administrado que contiene Hola misma configuración y la configuración como Hola VM de origen.

Para más información sobre Azure Managed Disks, consulte [Azure Managed Disks overview](../windows/managed-disks-overview.md) (Introducción a Azure Managed Disks). 

1.  Lista de cada máquina virtual y Hola el nombre de su disco de sistema operativo con [lista de vm az](/cli/azure/vm#list). Hello en el ejemplo siguiente se enumera todas las máquinas virtuales en el grupo de recursos denominado **myResourceGroup**:
    
    ```azurecli
    az vm list -g myTestRG --query '[].{Name:name,DiskName:storageProfile.osDisk.name}' --output table
    ```

    Hola de salida es similar toohello siguiente ejemplo:

    ```azurecli
    Name    DiskName
    ------  --------
    myVM    myDisk
    ```

1.  Administrar de disco de Hola de copia mediante la creación de un nuevo disco mediante [crear disco az](/cli/azure/disk#create). Hello en el ejemplo siguiente se crea un disco llamado **myCopiedDisk** desde Hola administrado disco llamado **myDisk**:

    ```azurecli
    az disk create --resource-group myResourceGroup --name myCopiedDisk --source myDisk
    ``` 

1.  Comprobar los discos de hello administrado ahora en el grupo de recursos mediante el uso de [lista de discos az](/cli/azure/disk#list). Hello en el ejemplo siguiente se enumera los Hola administrado discos Hola grupo de recursos denominado **myResourceGroup**:

    ```azurecli
    az disk list --resource-group myResourceGroup --output table
    ```

1.  Omitir demasiado["paso 3: configurar una red virtual"](#step-3-set-up-a-virtual-network).


## <a name="step-3-set-up-a-virtual-network"></a>Paso 3: Configuración de una red virtual


Hello pasos opcionales siguientes crea una nueva red virtual, la subred, la dirección IP pública y la tarjeta de interfaz de red virtual (NIC).

Si va a copiar una máquina virtual para solucionar problemas con fines o implementaciones adicionales, no conviene toouse una máquina virtual en una red virtual existente.

Si desea toocreate una infraestructura de red virtual para las máquinas virtuales copiadas, siga a continuación Hola pocos pasos. Si no desea toocreate una red virtual, omitir demasiado[paso 4: crear una máquina virtual](#step-4-create-a-vm).

1.  Crear red virtual de hello mediante [crear red virtual de red az](/cli/azure/network/vnet#create). Hello en el ejemplo siguiente se crea una red virtual denominada **myVnet** y una subred denominada **mySubnet**:

    ```azurecli
    az network vnet create --resource-group myResourceGroup --location westus --name myVnet \
        --address-prefix 192.168.0.0/16 --subnet-name mySubnet --subnet-prefix 192.168.1.0/24
    ```

1.  Cree una IP pública mediante [az network public-ip create](/cli/azure/network/public-ip#create). Hello en el ejemplo siguiente se crea una IP pública denominada **myPublicIP** con el nombre DNS de Hola de **mypublicdns**. (nombre DNS de hello debe ser único, por lo que proporcione un nombre único.)

    ```azurecli
    az network public-ip create --resource-group myResourceGroup --location westus \
        --name myPublicIP --dns-name mypublicdns --allocation-method static --idle-timeout 4
    ```

1.  Crear Hola NIC utilizando [crear nic de red az](/cli/azure/network/nic#create).
    Hello en el ejemplo siguiente se crea una NIC denominada **myNic** toothe adjunto que **mySubnet** subred:

    ```azurecli
    az network nic create --resource-group myResourceGroup --location westus --name myNic \
        --vnet-name myVnet --subnet mySubnet --public-ip-address myPublicIP
    ```

## <a name="step-4-create-a-vm"></a>Paso 4: Creación de una máquina virtual

Ahora puede crear la máquina virtual mediante [az vm create](/cli/azure/vm#create).

Especificar Hola copia disco administrado toouse como disco de SO hello (--adjuntar-os-disk), como sigue:

```azurecli
az vm create --resource-group myResourceGroup --name myCopiedVM \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics myNic --size Standard_DS1_v2 --os-type Linux \
    --attach-os-disk myCopiedDisk
```

## <a name="next-steps"></a>Pasos siguientes

toolearn cómo toouse CLI de Azure toomanage la nueva máquina virtual, consulte [comandos de CLI de Azure para hello Azure Resource Manager](../azure-cli-arm-commands.md).
