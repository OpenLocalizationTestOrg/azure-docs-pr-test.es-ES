---
title: 'aaa "CLI de Azure Script: crear una base de datos de Azure para PostgreSQL | Documentos de Microsoft"'
description: 'Ejemplo de script de la CLI de Azure: crea un servidor de Azure Database for PostgreSQL (Base de datos de Azure para PostgreSQL) y configura una regla de firewall de nivel de servidor.'
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: bbe31f77283aa4a3bb36d1fd9171c280594a8267
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-server-and-configure-a-firewall-rule-using-hello-azure-cli"></a>Crear una base de datos de Azure para servidor de PostgreSQL y configurar una regla de firewall mediante Hola CLI de Azure
Este script de la CLI de ejemplo crea un servidor de Azure Database for PostgreSQL (Base de datos de Azure para PostgreSQL) y configura una regla de firewall de nivel de servidor. Una vez que se ha ejecutado correctamente el script de Hola, servidor de PostgreSQL Hola puede tener acceso desde todos los servicios de Azure y Hola configurado direcciones IP.

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script de ejemplo
En este script de ejemplo, editar Hola resaltada las líneas toocustomize Hola administrador username y password.
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for PostgreSQL, and server-level firewall rule.")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación
Después de ejecutar el ejemplo de script de Hola, Hola siguiente comando puede ser usado tooremove grupo de recursos de Hola y todos los recursos asociados con él.
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a>Explicación del script
Este script utiliza Hola siga los comandos. Cada comando de documentación específica de hello tabla vínculos toocommand.

| **Comando** | **Notas** |
|---|---|
| [az group create](/cli/azure/group#create) | Crea un grupo de recursos en el que se almacenan todos los recursos. |
| [az postgres server create](/cli/azure/postgres/server#create) | Crea un servidor de PostgreSQL que hospeda las bases de datos de Hola. |
| [az postgres server firewall create](/cli/azure/postgres/server/firewall-rule#create) | Crea un servidor de toohello de acceso de firewall regla tooallow y bases de datos en él desde el intervalo de direcciones IP de hello especificado. |
| [az group delete](/cli/azure/group#delete) | Elimina un grupo de recursos, incluidos todos los recursos anidados. |

## <a name="next-steps"></a>Pasos siguientes
- Obtener información detallada sobre Hola CLI de Azure: [documentación de CLI de Azure](/cli/azure/overview)
- Pruebe otros scripts adicionales: [Ejemplos de la CLI de Azure para Azure Database for PostgreSQL](../sample-scripts-azure-cli.md).
