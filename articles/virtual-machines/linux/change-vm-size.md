---
title: aaaHow tooresize una VM de Linux con hello 2.0 de CLI de Azure | Documentos de Microsoft
description: "¿Cómo tooscale seguridad o reduzca verticalmente una máquina virtual de Linux, cambiando Hola tamaño de máquina virtual."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: e163f878-b919-45c5-9f5a-75a64f3b14a0
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2017
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e8fba485b5bcc7824f546de5cf3df77624a28008
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a>Cambio de tamaño de una máquina virtual Linux que usa CLI 2.0

Después de aprovisionar una máquina virtual (VM), puede escalar Hola VM hacia arriba o hacia abajo cambiando hello [tamaño de máquina virtual][vm-sizes]. En algunos casos, debe desasignar Hola VM en primer lugar. Necesitará toodeallocate Hola VM si Hola deseado tamaño no está disponible en el clúster de hardware de Hola que hospeda Hola VM. Este artículo detalla cómo tooresize una VM de Linux con Hola 2.0 de CLI de Azure. También puede realizar estos pasos con hello [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="resize-a-vm"></a>Cambiar el tamaño de una máquina virtual
tooresize una máquina virtual, deberá hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).

1. Cambia el tamaño de lista de Hola de vista de la máquina virtual disponible en clúster de hardware de Hola donde se hospeda Hola VM con [lista de vm az-vm-resize-options](/cli/azure/vm#list-vm-resize-options). Hello en el ejemplo siguiente se enumera los tamaños de máquina virtual para la máquina virtual denominada hello `myVM` en grupo de recursos de hello `myResourceGroup` región:
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. Si Hola deseado se muestra el tamaño de máquina virtual, cambiar el tamaño de Hola VM con [cambiar el tamaño de vm az](/cli/azure/vm#resize). Hola después cambia de tamaño de ejemplo Hola máquina virtual denominada `myVM` toohello `Standard_DS3_v2` tamaño:
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    Hola VM se reiniciará durante este proceso. Después del reinicio de hello, se reasignan los discos de datos y el sistema operativo existente. Cualquier cosa en disco temporal de Hola se pierde.

3. Si Hola deseado no se muestra el tamaño de máquina virtual, deberá toofirst desasignar Hola VM con [az vm desasignar](/cli/azure/vm#deallocate). Este proceso permite Hola VM toothen tooany cuyo tamaño ha cambiado tamaño disponible que Hola admite la región y, a continuación, se inicia. Hello pasos siguientes desasignar, cambiar el tamaño e inicie Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`:
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > Hola desasignar VM también libera todas las direcciones IP dinámicas asignadas toohello máquina virtual. Hola OS y discos de datos no se ven afectados.

## <a name="next-steps"></a>Pasos siguientes
Para obtener una mayor escalabilidad, ejecute varias instancias de VM y escálelas horizontalmente. Para obtener más información, consulte [Escalado automático de máquinas de Linux en un conjunto de escalado de máquinas virtuales][scale-set]. 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
