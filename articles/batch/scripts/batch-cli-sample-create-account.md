---
title: "Ejemplo de script de la CLI de Azure: creación de una cuenta de Batch | Microsoft Docs"
description: "Ejemplo de script de la CLI de Azure: creación de una cuenta de Batch"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: 698978fd717091c49a1375e222f46f4325431223
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-batch-account-with-the-azure-cli"></a>Creación de una cuenta de Batch con la CLI de Azure

Este script crea una cuenta de Azure Batch y muestra cómo se pueden consultar y actualizar las distintas propiedades de la cuenta.

## <a name="prerequisites"></a>Requisitos previos

Instale la CLI de Azure con las instrucciones que se encuentran en la [guía de instalación de la CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli) si aún no lo ha hecho.

## <a name="batch-account-sample-script"></a>Script de ejemplo de la cuenta de Batch

Cuando crea una cuenta de Batch, la configuración predeterminada indica que el servicio de Batch asigna de forma interna sus nodos de ejecución. Los nodos de ejecución asignados estarán sujetos a una cuota de núcleos independiente y la cuenta se puede autenticar ya sea a través de credenciales clave compartidas o un token de Azure Active Directory.

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Creación de cuenta")]

## <a name="batch-account-using-user-subscription-sample-script"></a>Cuenta de Batch con un script de ejemplo de suscripción de usuario

También puede optar porque Batch cree los nodos de ejecución en su propia suscripción de Azure.
Las cuentas que asignan nodos de ejecución en la suscripción se deben autenticar a través de un token de Azure Active Directory y los nodos de ejecución asignados se contabilizarán en la cuota de suscripciones. Para crear una cuenta de este modo, debe especificar una referencia de Key Vault cuando cree la cuenta.

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Creación de una cuenta con suscripción de usuario")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación

Después de ejecutar cualquiera de los scripts de ejemplo anteriores, ejecute el comando siguiente para quitar el grupo de recursos y todos los recursos relacionados (incluidas cuentas Batch, cuentas de Azure Storage y Azure Key Vault).

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explicación del script

Este script usa los siguientes comandos para crear un grupo de recursos, una cuenta de Batch y todos los recursos relacionados. Cada comando de la tabla crea un vínculo a documentación específica del comando.

| Comando | Notas |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Crea un grupo de recursos en el que se almacenan todos los recursos. |
| [az batch account create](https://docs.microsoft.com/cli/azure/batch/account#create) | Crea la cuenta de Batch.  |
| [az batch account set](https://docs.microsoft.com/cli/azure/batch/account#set) | Actualiza las propiedades de la cuenta de Batch.  |
| [az batch account show](https://docs.microsoft.com/cli/azure/batch/account#show) | Recupera los detalles de la cuenta de Batch especificada.  |
| [az batch account keys list](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | Recupera las claves de acceso de la cuenta de Batch especificada.  |
| [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) | Realiza la autenticación respecto de la cuenta de Batch especificada para una mayor interacción de la CLI.  |
| [az storage account create](https://docs.microsoft.com/cli/azure/storage/account#create) | Crea una cuenta de almacenamiento. |
| [az keyvault create](https://docs.microsoft.com/cli/azure/keyvault#create) | Crea un almacén de claves. |
| [az keyvault set-policy](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | Actualiza la directiva de seguridad del almacén de Key Vault especificado. |
| [az group delete](https://docs.microsoft.com/cli/azure/group#delete) | Elimina un grupo de recursos, incluidos todos los recursos anidados. |

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).

Puede encontrar ejemplos de script adicionales de la CLI de Batch en la [documentación de la CLI de Azure Batch](../batch-cli-samples.md).
