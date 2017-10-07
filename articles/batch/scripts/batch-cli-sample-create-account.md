---
title: Ejemplo de secuencia de comandos de CLI - aaaAzure crear una cuenta de lote | Documentos de Microsoft
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
ms.openlocfilehash: 62b640eebbafdd1081822a638fd0720121ef067a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-cli"></a>Crear una cuenta de lote con hello CLI de Azure

Este script crea una cuenta de lote de Azure y muestra cómo varias propiedades de cuenta de hello pueden consultar y actualizar.

## <a name="prerequisites"></a>Requisitos previos

Instalación Hola CLI de Azure utilizando instrucciones de hello proporcionadas en hello [Guía de instalación de CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), si aún no lo ha hecho.

## <a name="batch-account-sample-script"></a>Script de ejemplo de la cuenta de Batch

Cuando se crea una cuenta de lote, de forma predeterminada los nodos de proceso se asignan internamente por hello servicio por lotes. Nodos de proceso asignadas será cuota de núcleos independiente de tooa de asunto y cuenta de hello se puede autenticar mediante credenciales de clave compartida o un símbolo (token) de Active directorio de Azure.

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]

## <a name="batch-account-using-user-subscription-sample-script"></a>Cuenta de Batch con un script de ejemplo de suscripción de usuario

También puede optar por lotes toohave crear sus nodos de proceso en su propia suscripción de Azure.
Las cuentas que se asignan a proceso nodos en su suscripción deben ser autenticados mediante un símbolo (token) de Azure Active Directory y los nodos de proceso de hello asignados contará para la cuota de suscripción. toocreate una cuenta en este modo, al crear la cuenta de hello, uno debe especificar una referencia de almacén de claves.

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación

Después de ejecutar cualquiera de Hola por encima de las secuencias de comandos de ejemplo, ejecute hello después comando tooremove el grupo de recursos y todos ellos relacionados con recursos (incluidas las cuentas de lote, las cuentas de almacenamiento de Azure y almacenes de claves de Azure).

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explicación del script

Este script utiliza Hola siguientes comandos toocreate un grupo de recursos, cuenta de lote y todos ellos relacionados con recursos. Cada comando de la tabla de hello vincula documentación específica del toocommand.

| Comando | Notas |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Crea un grupo de recursos en el que se almacenan todos los recursos. |
| [az batch account create](https://docs.microsoft.com/cli/azure/batch/account#create) | Crea la cuenta de lote de Hola.  |
| [az batch account set](https://docs.microsoft.com/cli/azure/batch/account#set) | Actualiza las propiedades del programa Hola a cuenta de lote.  |
| [az batch account show](https://docs.microsoft.com/cli/azure/batch/account#show) | Recupera detalles de hello especifican cuenta de lote.  |
| [az batch account keys list](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | Recupera las teclas de acceso de Hola de hello especifican cuenta de lote.  |
| [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) | Autentica contra Hola especificado cuenta para la interacción de CLI más de lote.  |
| [az storage account create](https://docs.microsoft.com/cli/azure/storage/account#create) | Crea una cuenta de almacenamiento. |
| [az keyvault create](https://docs.microsoft.com/cli/azure/keyvault#create) | Crea un almacén de claves. |
| [az keyvault set-policy](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | Actualizar directiva de seguridad de Hola de almacén de claves especificado Hola. |
| [az group delete](https://docs.microsoft.com/cli/azure/group#delete) | Elimina un grupo de recursos, incluidos todos los recursos anidados. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Encontrará más ejemplos de secuencias de comandos de CLI de lote en hello [documentación de CLI de lote de Azure](../batch-cli-samples.md).
