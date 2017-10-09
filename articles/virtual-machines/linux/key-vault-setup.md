---
title: "aaaSet el almacén de claves de Azure para máquinas virtuales Linux | Documentos de Microsoft"
description: "Cómo tooset el almacén de claves para su uso con una máquina virtual de Azure Resource Manager con Hola CLI 2.0."
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: a5dc1fbe59a71b4456ba5b9bbacdb90440064757
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-key-vault-for-virtual-machines-with-hello-azure-cli-20"></a>Cómo tooset el almacén de claves para máquinas virtuales con Hola 2.0 de CLI de Azure

En la pila del Administrador de recursos de Azure hello, secretos/certificados se modelan como recursos proporcionados por el almacén de claves. toolearn más información acerca del almacén de claves de Azure, consulte [¿qué es el almacén de claves de Azure?](../../key-vault/key-vault-whatis.md) En orden para toobe de almacén de claves que se utiliza con máquinas virtuales del Administrador de recursos de Azure, Hola *EnabledForDeployment* propiedad en el almacén de claves se debe establecer tootrue. Este artículo muestra cómo tooset el almacén de claves para su uso con Azure máquinas virtuales (VM) mediante Hola 2.0 de CLI de Azure. También puede realizar estos pasos con hello [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

tooperform estos pasos, necesita hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).

## <a name="create-a-key-vault"></a>Creación de un Almacén de claves
Crear un almacén de claves y asignar la directiva de implementación de hello con [crear az keyvault](/cli/azure/keyvault#create). Hello en el ejemplo siguiente se crea un almacén de claves denominado `myKeyVault` en hello `myResourceGroup` grupo de recursos:

```azurecli
az keyvault create -l westus -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## <a name="update-a-key-vault-for-use-with-vms"></a>Actualización de un almacén de claves para su uso con VM
Establecer directiva de implementación de hello en un almacén de claves existente con [actualización de keyvault az](/cli/azure/keyvault#update). las actualizaciones siguientes Hola Hola almacén de claves denominado `myKeyVault` en hello `myResourceGroup` grupo de recursos:

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## <a name="use-templates-tooset-up-key-vault"></a>Usar plantillas tooset el almacén de claves
Cuando se usa una plantilla, deberá hello tooset `enabledForDeployment` propiedad demasiado`true` para el recurso de almacén de claves de hello como sigue:

```json
{
    "type": "Microsoft.KeyVault/vaults",
    "name": "ContosoKeyVault",
    "apiVersion": "2015-06-01",
    "location": "<location-of-key-vault>",
    "properties": {
    "enabledForDeployment": "true",
    ....
    ....
    }
}
```

## <a name="next-steps"></a>Pasos siguientes
Para otras opciones que puede configurar al crear un almacén de claves mediante plantillas, consulte [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/)(Creación de un almacén de claves).
