---
title: aaaHow tooresize una VM de Linux con hello 1.0 de CLI de Azure | Documentos de Microsoft
description: "¿Cómo tooscale seguridad o reduzca verticalmente una máquina virtual de Linux, cambiando Hola tamaño de máquina virtual."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2016
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 43dd955dc2f2dd9d1b2da07ecbfbf2459bcaa4d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-vm-with-azure-cli-10"></a>Cambio de tamaño de una máquina virtual Linux con la CLI de Azure 1.0

## <a name="overview"></a>Información general

Después de aprovisionar una máquina virtual (VM), puede escalar Hola VM hacia arriba o hacia abajo cambiando hello [tamaño de máquina virtual][vm-sizes]. En algunos casos, debe desasignar Hola VM en primer lugar. Esto puede ocurrir si no está disponible en clúster de hardware de Hola que hospeda Hola VM nuevo tamaño de Hola.

Este artículo se muestra cómo tooresize una VM de Linux con hello [CLI de Azure][azure-cli].

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello
Puede completar la tarea hello mediante uno de hello después de las versiones CLI:

- [Azure 1.0 de CLI](#resize-a-linux-vm) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)
- [Azure 2.0 CLI](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola


## <a name="resize-a-linux-vm"></a>Cambio de tamaño de una VM de Linux
tooresize una máquina virtual, realice Hola pasos.

1. Ejecute el siguiente comando CLI de Hola. Este comando muestra los tamaños de máquinas virtuales de Hola que están disponibles en el clúster de hardware de Hola donde hello VM se hospeda.
   
    ```azurecli
    azure vm sizes -g myResourceGroup --vm-name myVM
    ```
2. Si Hola deseado se muestra el tamaño, ejecute hello después comando tooresize hello VM.
   
    ```azurecli
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM  \
        --enable-boot-diagnostics
        --boot-diagnostics-storage-uri https://mystorageaccount.blob.core.windows.net/ 
    ```
   
    Hola VM se reiniciará durante este proceso. Después del reinicio de hello, el sistema operativo existente y los discos de datos se volverán a asignar. Cualquier cosa en disco temporal de Hola se perderá.
   
    Hola de uso `--enable-boot-diagnostics` opción habilita [diagnósticos de arranque][boot-diagnostics], toolog cualquier toostartup relacionados con errores.
3. En caso contrario, si Hola deseado no se especifica tamaño, ejecute hello siga los comandos toodeallocate Hola VM, cambiar su tamaño y, a continuación, reiniciar Hola VM.
   
    ```azurecli
    azure vm deallocate -g myResourceGroup myVM
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM \
        --enable-boot-diagnostics --boot-diagnostics-storage-uri \
        https://mystorageaccount.blob.core.windows.net/ 
    azure vm start -g myResourceGroup myVM
    ```
   
   > [!WARNING]
   > Hola desasignar VM también libera todas las direcciones IP dinámicas asignadas toohello máquina virtual. Hola OS y discos de datos no se ven afectados.
   > 
   > 

## <a name="next-steps"></a>Pasos siguientes
Para obtener una mayor escalabilidad, ejecute varias instancias de VM y escálelas horizontalmente. Para obtener más información, consulte [Escalado automático de máquinas de Linux en un conjunto de escalado de máquinas virtuales][scale-set]. 

<!-- links -->

[azure-cli]:../../cli-install-nodejs.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
