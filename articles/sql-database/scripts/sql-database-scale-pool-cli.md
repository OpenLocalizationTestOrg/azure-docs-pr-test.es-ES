---
title: "en el ejemplo aaaCLI se escala una base de datos SQL de Azure de grupo elástico de SQL | Documentos de Microsoft"
description: "Azure CLI ejemplo script tooscale un grupo elástico de SQL en la base de datos de SQL Azure"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 436128b8183213f78b9abc2ec46efe2a3ed3c37c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-tooscale-a-sql-elastic-pool-in-azure-sql-database"></a>Utilice CLI tooscale un grupo elástico de SQL en la base de datos de SQL Azure

Este script de ejemplo de la CLI de Azure crea grupos elásticos de SQL, traslada bases de datos agrupadas y cambia los niveles de rendimiento de los grupos elásticos. 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script de ejemplo

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación

Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explicación del script

Este script utiliza Hola después comandos toocreate un grupo de recursos, servidor lógico, base de datos SQL y las reglas de firewall. Cada comando de documentación específica de hello tabla vínculos toocommand.

| Comando | Notas |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Crea un grupo de recursos en el que se almacenan todos los recursos. |
| [az sql server create](https://docs.microsoft.com/cli/azure/sql/server#create) | Crea un servidor lógico que hospeda Hola base de datos SQL. |
| [az sql elastic-pools create](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | Crea un grupo elástico de base de datos en el servidor lógico Hola. |
| [az sql db create](https://docs.microsoft.com/cli/azure/sql/db#create) | Crea Hola base de datos SQL en el servidor lógico Hola. |
| [az sql elastic-pools update](https://docs.microsoft.com/cli/azure/sql/elastic-pool#update) | Actualiza un grupo elástico de base de datos, en este Hola de cambios en el ejemplo se asignan eDTU. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Elimina un grupo de recursos, incluidos todos los recursos anidados. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Encontrará más ejemplos de secuencias de comandos de CLI de base de datos de SQL en hello [documentación de la base de datos de SQL Azure](../sql-database-cli-samples.md).
