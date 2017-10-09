---
title: "una función de Azure que se conecta la base de datos de Azure Cosmos tooan aaaCreate | Documentos de Microsoft"
description: "Script de CLI de Azure de ejemplo: crear una función de Azure que se conecta la base de datos de Azure Cosmos tooan"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: 0fbc1ebec2dfd480e0cf3ca64f9febcec8af9a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-that-connects-tooan-azure-cosmos-db"></a>Crea una función de Azure que se conecta la base de datos de Azure Cosmos tooan

Este script de ejemplo crea una aplicación de la función de Azure y conecta la base de datos de base de datos de Azure Cosmos tooan.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script de ejemplo

Este ejemplo crea una aplicación de la función de Azure y agrega una configuración de clave tooapp de punto de conexión y acceso de Cosmos DB.

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Create an Azure Function that connects tooan Azure Cosmos DB")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación

Después de ejecutar el ejemplo de script de Hola, Hola seguimiento comando puede escribirse como grupo de recursos de hello tooremove usados y todos los recursos relacionados.

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Explicación del script

Este script utiliza Hola siga los comandos. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [az login](https://docs.microsoft.com/cli/azure/#login) | TooAzure de inicio de sesión. |
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Crea un grupo de recursos con una ubicación. |
| [az storage account create](https://docs.microsoft.com/cli/azure/storage/account) | Crear una cuenta de almacenamiento |
| [az functionapp create](https://docs.microsoft.com/cli/azure/functionapp#create) | Crea una nueva instancia de Function App. |
| [az documentdb create](https://docs.microsoft.com/cli/azure/documentdb#create) | Crea una base de datos de DocumentDB. |
| [az group delete](https://docs.microsoft.com/cli/azure/group#delete) | Limpieza |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Encontrará más ejemplos de secuencias de comandos de CLI de funciones de Azure en hello [documentación sobre las funciones de Azure](../functions-cli-samples.md).




