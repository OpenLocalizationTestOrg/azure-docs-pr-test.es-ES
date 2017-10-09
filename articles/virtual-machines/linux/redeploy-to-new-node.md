---
title: "aaaRedeploy máquinas virtuales de Linux en Azure | Documentos de Microsoft"
description: "Cómo emite máquinas virtuales de Linux tooredeploy en conexión de SSH de toomitigate de Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: e9530dd6-f5b0-4160-b36b-d75151d99eb7
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 9adfd1b11f262d362133366b2bba5e69c70c9b82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-linux-virtual-machine-toonew-azure-node"></a>Volver a implementar la máquina virtual de Linux toonew nodos de Azure
Si se enfrentan dificultades en la solución de problemas de SSH o aplicación tener acceso a la máquina virtual de Linux de tooa (VM) en Azure, volver a implementar Hola VM puede ayudar. Cuando se vuelve a implementar una máquina virtual, se desplaza Hola VM tooa nuevo nodo dentro de hello infraestructura de Azure y, a continuación, enciende. Se conservan todas las opciones de configuración y los recursos asociados. Este artículo muestra cómo tooredeploy una máquina virtual mediante la CLI de Azure o hello portal de Azure.

> [!NOTE]
> Después de volver a implementar una máquina virtual, se perderá disco temporal de Hola y direcciones IP dinámicas asociadas con la interfaz de red virtual se actualizan. 

Puede volver a implementar una máquina virtual mediante una de las siguientes opciones de Hola. Solo necesita toochoose una opción tooredeploy la máquina virtual:

- [CLI de Azure 2.0](#azure-cli-20)
- [CLI de Azure 1.0](#azure-cli-10)
- [Portal de Azure](#using-azure-portal)

## <a name="use-hello-azure-cli-20"></a>Usar hello 2.0 de CLI de Azure
Hola de instalación más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) e inicie sesión con cuenta de Azure de tooan [inicio de sesión de az](/cli/azure/#login).

Vuelva a implementar la máquina virtual con [az vm redeploy](/cli/azure/vm#redeploy). Después de nuevas implementaciones de ejemplo de Hola Hola máquina virtual denominada *myVM* en grupo de recursos de hello llamado *myResourceGroup*:

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM 
```

## <a name="use-hello-azure-cli-10"></a>Usar hello Azure CLI 1.0
Instalar hello [más reciente Azure CLI 1.0](../../cli-install-nodejs.md), inicie sesión en tooan cuenta de Azure y asegúrese de que está en modo de administrador de recursos (`azure config mode arm`).

Después de nuevas implementaciones de ejemplo de Hola Hola máquina virtual denominada *myVM* en grupo de recursos de hello llamado *myResourceGroup*:

```azurecli
azure vm redeploy --resource-group myResourceGroup --vm-name myVM 
```

[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a>Pasos siguientes
Si tiene problemas para conectarse tooyour VM, puede buscar ayuda específica en [solucionar problemas de conexión de SSH](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [detallan los pasos para solucionar problemas de SSH](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). También puede leer sobre la [solución de problemas de aplicaciones](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) si no puede acceder a una aplicación que se ejecuta en la máquina virtual.

