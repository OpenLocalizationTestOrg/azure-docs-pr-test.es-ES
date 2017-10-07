---
title: "parámetros de servicio de hello aaaConfigure en la base de datos de Azure para PostgreSQL | Documentos de Microsoft"
description: "Este artículo describe cómo tooconfigure parámetros de servicio de hello en la base de datos de Azure para usar PostgreSQL Hola línea de comandos de CLI de Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 84a11de24ba87fc0eb6744aaa4b53f65a183903d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a>Personalización de los parámetros de configuración del servidor con la CLI de Azure
Puede enumerar, mostrar y actualizar los parámetros de configuración para un servidor de Azure PostgreSQL utilizando Hola interfaz de línea de comandos (CLI de Azure). Sin embargo, en el nivel del servidor, solo se expone y se puede modificar un subconjunto de las opciones de configuración del motor. 

## <a name="prerequisites"></a>Requisitos previos
toostep a través de este tooguide cómo, necesita:
- Un servidor y una base de datos [Creación de una instancia de Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md)
- Instalar [CLI de Azure 2.0](/cli/azure/install-azure-cli) línea de comandos utilidad o use Hola Shell en la nube de Azure en el Explorador de Hola.

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a>Lista de los parámetros de configuración del servidor de Azure Database for PostgreSQL
toolist todos los parámetros modificables en un servidor y sus valores, ejecute hello [lista de configuración de servidores de az postgres](/cli/azure/postgres/server/configuration#list) comando.

Puede enumerar los parámetros de configuración de servidor de Hola para servidor hello **mypgserver 20170401.postgres.database.azure.com** en el grupo de recursos **myresourcegroup**.
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a>Presentación de los detalles de los parámetros de configuración del servidor
detalles de tooshow sobre un parámetro de configuración específica para un servidor, ejecute hello [mostrar de configuración de servidor de az postgres](/cli/azure/postgres/server/configuration#show) comando.

Este ejemplo muestra detalles de hello **registro\_min\_mensajes** parámetro de configuración de servidor para el servidor **mypgserver 20170401.postgres.database.azure.com** en grupo de recursos **myresourcegroup.**
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a>Modificación del valor de los parámetros de configuración del servidor
También puede modificar el valor de Hola de ciertos parámetros de configuración de servidor y se actualizará el valor de configuración subyacente Hola Hola PostgreSQL motor de server. Hola de uso de configuración de hello tooupdate [conjunto de configuración de servidor de az postgres](/cli/azure/postgres/server/configuration#set) comando. 

Hola tooupdate **registro\_min\_mensajes** parámetro de configuración de servidor del servidor de **mypgserver 20170401.postgres.database.azure.com** bajo el grupo de recursos **myresourcegroup.**
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
Si desea que el valor de hello tooreset de un parámetro de configuración, simplemente elija tooleave out Hola opcional `--value` parámetro y el servicio de Hola aplicarán el valor predeterminado de Hola. En el ejemplo anterior, sería:
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
Se restablecerá hello **registro\_min\_mensajes** valor predeterminado de configuración toohello **advertencia**. Para más información sobre la configuración del servidor y los valores permitidos, consulte la documentación de PostgreSQL en [Server Configuration](https://www.postgresql.org/docs/9.6/static/runtime-config.html) (Configuración del servidor).

## <a name="next-steps"></a>Pasos siguientes
- registros del servidor de acceso y tooconfigure, consulte [registros del servidor de base de datos de PostgreSQL](concepts-server-logs.md)
