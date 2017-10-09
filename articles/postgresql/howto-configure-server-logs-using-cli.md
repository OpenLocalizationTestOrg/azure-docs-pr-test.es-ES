---
title: registros del servidor aaaConfigure y acceso para PostgreSQL con CLI de Azure | Documentos de Microsoft
description: "Este artículo describe cómo los registros del servidor hello tooconfigure y acceso en base de datos de Azure para PostgreSQL mediante la línea de comandos de CLI de Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 924d4e7634cc48405bcb0f813cf61d8b72ad8aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a>Configuración y acceso a los registros del servidor con la CLI de Azure
Puede descargar los registros de errores de servidor hello PostgreSQL mediante Hola interfaz de línea de comandos (CLI de Azure). Sin embargo, no se admite el acceso tootransaction registros. 

## <a name="prerequisites"></a>Requisitos previos
toostep a través de este tooguide cómo, necesita:
- Un [servidor de Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md).
- Instalar [CLI de Azure 2.0](/cli/azure/install-azure-cli) de línea de comandos Hola de utilidad o use el Shell de nube de Azure en Explorador de Hola.

## <a name="configure-logging-for-azure-database-for-postgresql"></a>Configuración del registro para Azure Database for PostgreSQL
Puede configurar registros de consultas de hello server tooaccess y registros de errores. Los registros de error pueden contener información de vaciado automático, conexión y puntos de comprobación.
1. Active el registro.
2. Registro de actualización\_instrucción y registro\_min\_duración\_registro de consultas de instrucción tooenable
3. Actualice el período de retención.

Consulte cómo [personalizar los parámetros de configuración del servidor](howto-configure-server-parameters-using-cli.md) para más información.

## <a name="list-logs-for-azure-database-for-postgresql-server"></a>Enumeración de registros del servidor de Azure Database for PostgreSQL
archivos de registro disponibles toolist hello para el servidor, ejecute hello [lista de registros de servidor postgres az](/cli/azure/postgres/server-logs#list) comando.

Puede enumerar los archivos de registro de hello de servidor **mypgserver 20170401.postgres.database.azure.com** en el grupo de recursos **myresourcegroup**y dirigir tooa texto archivo denominado **registro\_archivos\_list.txt.**
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-hello-server"></a>Descargar los registros localmente desde el servidor de Hola
Hola [descargar registros de servidor postgres az](/cli/azure/postgres/server-logs#download) comando permite toodownload distintos archivos de registro para el servidor. 

En este ejemplo Hola de descargas de archivo de registro específico para el servidor de hello **mypgserver 20170401.postgres.database.azure.com** en el grupo de recursos **myresourcegroup** tooyour de entorno local.
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a>Pasos siguientes
- toolearn más información acerca de los registros del servidor, consulte [registros del servidor de base de datos de PostgreSQL](concepts-server-logs.md)
- Para más información sobre los parámetros del servidor, consulte cómo [personalizar los parámetros de configuración del servidor mediante la CLI de Azure](howto-configure-server-parameters-using-cli.md).
