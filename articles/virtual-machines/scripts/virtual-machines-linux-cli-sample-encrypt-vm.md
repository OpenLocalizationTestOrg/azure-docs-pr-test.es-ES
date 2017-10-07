---
title: Ejemplo de secuencia de comandos de CLI - aaaAzure cifrar una VM de Linux | Documentos de Microsoft
description: "Ejemplo de script de la CLI de Azure: cifrado de una máquina virtual Linux"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 1e455da4a8ea6d75b6d0d74b338d2e4d84973413
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-linux-virtual-machine-in-azure"></a>Cifrado de una máquina virtual Linux en Azure

Este script crea un almacén Azure Key Vault seguro, claves de cifrado, una entidad de servicio de Azure Active Directory y una máquina virtual (VM) Linux. Hola VM, a continuación, se cifra mediante la clave de cifrado de Hola desde el almacén de claves y credenciales de servicio principal.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de ejemplo

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_vm.sh "Encrypt VM disks")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación 

Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explicación del script

Esta secuencia de comandos usa Hola después comandos toocreate una recurso grupo, almacén de claves de Azure, servicio principal, máquina virtual, y todos los recursos relacionados. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Crea un grupo de recursos en el que se almacenan todos los recursos. |
| [az keyvault create](https://docs.microsoft.com/cli/azure/keyvault#create) | Crea un almacén de claves de Azure toostore proteger los datos, como las claves de cifrado. |
| [az keyvault key create](https://docs.microsoft.com/cli/azure/keyvault/key#create) | Crea una clave de cifrado en el almacén Key Vault. |
| [az ad sp create-for-rbac](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | Crea un servicio de Azure Active Directory principal toosecurely autenticar y acceso tooencryption teclas de control. |
| [az keyvault set-policy](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | Establece permisos en toogrant de almacén de claves de hello claves de tooencryption de acceso principal de servicio de Hola. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Crea la máquina virtual de Hola y lo conecta toohello tarjeta de red, red virtual, subred y NSG. Este comando también especifica toobe de imagen de máquina virtual de hello usa y credenciales administrativas.  |
| [az vm encryption enable](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | Habilita el cifrado en una máquina virtual usando las credenciales de entidad de seguridad de servicio de Hola y clave de cifrado. |
| [az vm encryption show](https://docs.microsoft.com/cli/azure/vm/encryption#show) | Muestra el estado de Hola de hello proceso de cifrado de la máquina virtual. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Elimina un grupo de recursos, incluidos todos los recursos anidados. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Ejemplos de secuencias de comandos CLI de máquina virtual adicional pueden encontrarse en hello [documentación de Azure VM de Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
