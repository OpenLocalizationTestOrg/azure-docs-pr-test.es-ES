---
title: "aaaSet la clave de almacén para máquinas virtuales de Windows en el Administrador de recursos de Azure | Documentos de Microsoft"
description: "Cómo tooset el almacén de claves para su uso con una máquina virtual de Azure Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 33a483e2-cfbc-4c62-a588-5d9fd52491e2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: kasing
ms.openlocfilehash: 53bbe90708202ecfdcf754822d04bf2469631f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a>Configuración de un Almacén de claves para máquinas virtuales en Azure Resource Manager

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

En la pila del Administrador de recursos de Azure, los secretos/certificados se modelan como recursos proporcionados por el proveedor de recursos de Hola de almacén de claves. toolearn más información sobre el almacén de claves, consulte [¿qué es el almacén de claves de Azure?](../../key-vault/key-vault-whatis.md)

> [!NOTE]
> 1. En orden para toobe de almacén de claves que se utiliza con máquinas virtuales del Administrador de recursos de Azure, Hola **EnabledForDeployment** propiedad en el almacén de claves se debe establecer tootrue. Puede hacer esto en varios clientes.
> 2. necesidades del almacén de claves de Hello toobe creado en Hola misma suscripción y ubicación como Hola Máquina Virtual.
>
>

## <a name="use-powershell-tooset-up-key-vault"></a>Usar PowerShell tooset el almacén de claves
toocreate un almacén de claves mediante PowerShell, consulte [empezar a trabajar con el almacén de claves de Azure](../../key-vault/key-vault-get-started.md#vault).

Para almacenes de claves nuevos, puede usar este cmdlet de PowerShell:

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

Para almacenes de claves existentes, puede usar este cmdlet de PowerShell:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-tooset-up-key-vault"></a>Nos CLI tooset el almacén de claves
toocreate un almacén de claves mediante Hola interfaz de línea de comandos (CLI), consulte [administrar el almacén de claves con CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).

Para CLI, es necesario el almacén de claves de hello toocreate antes de asignar la directiva de implementación de Hola. Puede hacerlo mediante el uso de hello siguiente comando:

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a>Usar plantillas tooset el almacén de claves
Mientras usa una plantilla, deberá hello tooset `enabledForDeployment` propiedad demasiado`true` para hello recursos de almacén de claves.

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
