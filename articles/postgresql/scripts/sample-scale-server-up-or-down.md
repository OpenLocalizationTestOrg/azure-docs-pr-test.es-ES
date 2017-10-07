---
title: aaa "base de datos de Azure de la escala de la secuencia de comandos CLI de Azure para PostgreSQL | Documentos de Microsoft"
description: "Ejemplo de secuencia de comandos para Azure CLI - base de datos de Azure de escala de nivel de rendimiento diferentes de PostgreSQL servidor tooa después de consultar las métricas de Hola."
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: 678b28941dbb4334cb374d4888991a00b44966b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-scale-a-single-postgresql-server-using-azure-cli"></a>Supervisión y escalado de un solo servidor PostgreSQL mediante la CLI de Azure
Esta secuencia de comandos CLI de ejemplo, amplía una sola base de datos de Azure para el nivel de rendimiento diferentes de PostgreSQL servidor tooa después de consultar las métricas de Hola. 

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script de ejemplo
En este script de ejemplo, cambie Hola resaltada las líneas toocustomize Hola administrador username y password. Reemplace el Id. de suscripción de hello utilizado en comandos de monitor de hello az con su propio identificador de suscripción.[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Create and scale Azure Database for PostgreSQL.")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación
Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a>Explicación del script
Este script utiliza Hola siga los comandos. Cada comando de documentación específica de hello tabla vínculos toocommand.

| **Comando** | **Notas** |
|---|---|
| [az group create](/cli/azure/group#create) | Crea un grupo de recursos en el que se almacenan todos los recursos. |
| [az postgres server create](/cli/azure/postgres/server#create) | Crea un servidor de PostgreSQL que hospeda las bases de datos de Hola. |
| [az monitor metrics list](/cli/azure/monitor/metrics#list) | Valor de métrica de Hola de lista de recursos de Hola. |
| [az group delete](/cli/azure/group#delete) | Elimina un grupo de recursos, incluidos todos los recursos anidados. |

## <a name="next-steps"></a>Pasos siguientes
- Obtener información detallada sobre Hola CLI de Azure: [documentación de CLI de Azure](/cli/azure/overview)
- Pruebe otros scripts adicionales: [Ejemplos de la CLI de Azure para Azure Database for PostgreSQL](../sample-scripts-azure-cli.md).
- Para más información sobre el escalado, vea [Niveles de servicio](../concepts-service-tiers.md) y [Unidades de proceso y almacenamiento](../concepts-compute-unit-and-storage.md).
