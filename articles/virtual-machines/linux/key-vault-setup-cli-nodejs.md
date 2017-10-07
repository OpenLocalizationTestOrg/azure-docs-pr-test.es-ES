---
title: "aaaSet el almacén de claves para las máquinas virtuales de Linux con hello 1.0 de CLI de Azure | Documentos de Microsoft"
description: "Cómo tooset el almacén de claves para su uso con una máquina virtual de Azure Resource Manager con Hola 1.0 de CLI de Azure."
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: 275022e4e7e26d7363784c289dd7512047c07bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager-with-hello-azure-cli-10"></a>Configurar el almacén de claves para las máquinas virtuales en el Administrador de recursos de Azure con hello Azure CLI 1.0
En la pila del Administrador de recursos de Azure hello, secretos/certificados se modelan como recursos proporcionados por el proveedor de recursos de Hola de almacén de claves. toolearn más información acerca del almacén de claves de Azure, consulte [¿qué es el almacén de claves de Azure?](../../key-vault/key-vault-whatis.md) En orden para toobe de almacén de claves que se utiliza con máquinas virtuales del Administrador de recursos de Azure, Hola *EnabledForDeployment* propiedad en el almacén de claves se debe establecer tootrue. Puede hacer esto en varios clientes. Este artículo muestra cómo tooset el almacén de claves para su uso con máquinas virtuales de Azure.

## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello
Puede completar la tarea hello mediante uno de los siguientes versiones CLI de Hola

- [Azure 1.0 de CLI](#quick-commands) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)
- [Azure 2.0 CLI](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola

## <a name="use-cli-10-tooset-up-key-vault"></a>Utilice CLI 1.0 tooset el almacén de claves
toocreate un almacén de claves mediante Hola interfaz de línea de comandos (CLI), consulte [administrar el almacén de claves con CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).

Para CLI 1.0, es necesario el almacén de claves de hello toocreate antes de asignar la directiva de implementación de Hola. A continuación, puede asignar directivas de hello mediante Hola siguiente comando:

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a>Usar plantillas tooset el almacén de claves
Cuando se usa una plantilla, deberá hello tooset `enabledForDeployment` propiedad demasiado`true` para hello recursos de almacén de claves.

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

Para otras opciones que puede configurar al crear un almacén de claves mediante plantillas, consulte [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/)(Creación de un almacén de claves).
