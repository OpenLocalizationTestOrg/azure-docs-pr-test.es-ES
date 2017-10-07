---
title: ejemplos de aaaAzure CLI tooscale una base de datos de MySQL server | Documentos de Microsoft
description: "Esta secuencia de comandos CLI de ejemplo escala base de datos de Azure para el nivel de rendimiento de MySQL server tooa después de consultar las métricas de Hola."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: sample
ms.custom: mvc
ms.date: 05/31/2017
ms.openlocfilehash: 721ef9db35a5f3be7a38438c1abb724187b18b75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-scale-an-azure-database-for-mysql-server-using-azure-cli"></a>Supervisión y escalado de un servidor de Azure Database for MySQL (Base de datos de Azure para MySQL) mediante la CLI de Azure
Esta secuencia de comandos CLI de ejemplo, amplía una sola base de datos de Azure para el nivel de rendimiento de MySQL server tooa después de consultar las métricas de Hola.

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script de ejemplo
En este script de ejemplo, cambie Hola resaltada las líneas toocustomize Hola administrador username y password. Reemplace el Id. de suscripción de hello utilizado en comandos de monitor de hello az con su propio identificador de suscripción.[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación
Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Delete hello resource group.")]

## <a name="script-explanation"></a>Explicación del script
Este script utiliza Hola siga los comandos. Cada comando de documentación específica de hello tabla vínculos toocommand.

| **Comando** | **Notas** |
|---|---|
| [az group create](/cli/azure/group#create) | Crea un grupo de recursos en el que se almacenan todos los recursos. |
| [az mysql server create](/cli/azure/mysql/server#create) | Crea un servidor de MySQL que hospeda las bases de datos de Hola. |
| [az monitor metrics list](/cli/azure/monitor/metrics#list) | Valor de métrica de Hola de lista de recursos de Hola. |
| [az group delete](/cli/azure/group#delete) | Elimina un grupo de recursos, incluidos todos los recursos anidados. |

## <a name="next-steps"></a>Pasos siguientes
- Obtener información detallada sobre Hola CLI de Azure: [documentación de Azure CLI](/cli/azure/overview).
- Pruebe scripts adicionales en: [Ejemplos de la CLI de Azure para Azure Database for MySQL](../sample-scripts-azure-cli.md).
- Para obtener más información sobre el escalado, consulte [Service Tiers](../concepts-service-tiers.md) (Niveles de servicio) y [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md) (Unidades de proceso y almacenamiento).
