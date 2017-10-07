---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure crear una máquina virtual con un disco duro virtual | Documentos de Microsoft"
description: "Ejemplo de script de la CLI de Azure: crear una máquina virtual mediante un disco duro virtual."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/09/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: ce39092697a51e4e8a8e59ba8eb919955f616458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a>Crear una máquina virtual con un disco duro virtual

Este ejemplo crea una máquina virtual con un disco duro virtual (VHD).
Crea un grupo de recursos, una cuenta de almacenamiento y un contenedor, a continuación, crea una máquina virtual mediante la carga de contenedor de hello VHD toohello.
Reemplaza Hola ssh público de clave con la clave pública para que tenga acceso toohello máquina virtual.

Necesitará un VHD de arranque.
Puede descargar Hola VHD que hemos usado desde https://azclisamples.blob.core.windows.net/vhds/sample.vhd o usar un VHD propio. busca el script de Hola `~/sample.vhd`.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de ejemplo

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación 

Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a>Explicación del script

Este script utiliza Hola después comandos toocreate un grupo de recursos, máquina virtual, conjunto de disponibilidad, equilibrador de carga y todos los recursos relacionados. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Crea un grupo de recursos en el que se almacenan todos los recursos. |
| [az storage account list](https://docs.microsoft.com/cli/azure/storage/account#list) | Enumera las cuentas de almacenamiento |
| [az storage account check-name](https://docs.microsoft.com/cli/azure/storage/account#check-name) | Comprueba que un nombre de cuenta de almacenamiento es válido y que no existe ya |
| [az storage account keys list](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | Enumera las claves hello las cuentas de almacenamiento |
| [az storage blob exists](https://docs.microsoft.com/cli/azure/storage/blob#exists) | Comprueba si existe el blob de Hola |
| [az storage container create](https://docs.microsoft.com/cli/azure/storage/container#create) | Crea un contenedor en una cuenta de almacenamiento. |
| [az storage blob upload](https://docs.microsoft.com/cli/azure/storage/blob#upload) | Crea un blob en contenedor Hola Hola cargar VHD. |
| [az vm list](https://docs.microsoft.com/cli/azure/vm#list) | Usar con `--query` comprobar si el nombre de la máquina virtual de hello está en uso. | 
| [az vm create](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Crea hello las máquinas virtuales. |
| [az vm access set-linux-user](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | Restablece Hola SSH toogive clave Hola actual usuario acceso toohello máquina virtual. |
| [az vm list-ip-addresses](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | Obtiene la dirección IP de Hola de hello máquina virtual que se creó. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Ejemplos de secuencias de comandos CLI de máquina virtual adicional pueden encontrarse en hello [documentación de Azure VM de Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
