---
title: aaaCreate y administrar la base de datos PostgreSQL las reglas de firewall mediante la CLI de Azure | Documentos de Microsoft
description: "Este artículo se describe cómo toocreate y administrar la base de datos PostgreSQL las reglas de firewall mediante la línea de comandos de CLI de Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 06e34c9e3996c2ec3df63191d794bc34d0ca0cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a>Creación y administración de reglas de firewall de Azure Database for PostgreSQL mediante la CLI de Azure
Las reglas de firewall de nivel de servidor habilitar administradores toomanage acceso tooan base de datos de Azure para PostgreSQL Server desde una dirección IP específica o intervalo de direcciones IP. Usar comandos de CLI de Azure adecuadas, puede crear, actualizar, eliminar, enumerar y mostrar toomanage de reglas de firewall en el servidor. Para obtener información general sobre los firewalls de Azure Database for PostgreSQL, consulte [Reglas de firewall de un servidor de Azure Database for PostgreSQL](concepts-firewall-rules.md)

## <a name="prerequisites"></a>Requisitos previos
toostep a través de este tooguide cómo, necesita:
- Un [servidor y una base de datos de Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md).
- Instalar [CLI de Azure 2.0](/cli/azure/install-azure-cli) línea de comandos utilidad o use Hola Shell en la nube de Azure en el Explorador de Hola.

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a>Configuración de reglas de firewall para Azure Database for PostgreSQL
Hola [az postgres servidor regla de firewall](/cli/azure/postgres/server/firewall-rule) comandos son tooconfigure usa reglas de firewall.

## <a name="list-firewall-rules"></a>Enumerar reglas de firewall 
toolist Hola existente de reglas de firewall de servidor en el servidor de hello, ejecute hello [lista de regla de firewall del servidor de az postgres](/cli/azure/postgres/server/firewall-rule#list) comando.
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
salida de Hello enumera las reglas de hello si los hay, de forma predeterminada en JSON de formato. Puede usar el modificador de hello `--output table` para un formato más legible de la tabla como resultado de hello.
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a>Crear reglas de firewall
una nueva regla de firewall en servidor de hello, ejecute hello toocreate [crear az postgres servidor regla de firewall](/cli/azure/postgres/server/firewall-rule#create) comando. 

Este ejemplo permite una serie de todos los servidores de Hola de tooaccess de direcciones IP **mypgserver 20170401.postgres.database.azure.com**
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
tooallow una tooaccess de dirección IP singular, proporcionar Hola la misma dirección como Hola IP inicial y final de IP, como en este ejemplo.
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
Cuando se realiza correctamente, el resultado del comando de hello muestra detalles de Hola Hola de regla de firewall que ha creado, de forma predeterminada en formato JSON. Si se produce un error, Hola había salida showserror texto del mensaje en su lugar.

## <a name="update-firewall-rule"></a>Actualizar reglas de firewall 
Actualizar una regla de firewall existente sobre el uso de servidor de hello [actualización de regla de firewall de servidor de az postgres](/cli/azure/postgres/server/firewall-rule#update) comando. Proporcione el nombre de Hola de regla de firewall existente hello como entrada y Hola inicio IP y final IP atributos tooupdate.
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
Cuando se realiza correctamente, el resultado del comando de hello muestra detalles de Hola Hola de regla de firewall que ha actualizado, de forma predeterminada en formato JSON. Si se produce un error, Hola había salida showserror texto del mensaje en su lugar.
> [!NOTE]
> Si la regla de firewall de hello no existe, se crea mediante el comando de actualización de Hola.

## <a name="show-firewall-rule-details"></a>Mostrar los detalles de la regla de firewall
También puede mostrar detalles de la regla para un servidor de firewall existente Hola ejecutando [demostración de regla de firewall de servidor de az postgres](/cli/azure/postgres/server/firewall-rule#show) comando.
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
Cuando se realiza correctamente, el resultado del comando de hello muestra detalles de Hola Hola de regla de firewall que ha especificado, de forma predeterminada en formato JSON. Si se produce un error, Hola había salida showserror texto del mensaje en su lugar.

## <a name="delete-firewall-rule"></a>Eliminar reglas de firewall
acceso de toorevoke para un intervalo IP del servidor de hello, eliminar una regla de firewall existente mediante la ejecución de hello [eliminar az postgres servidor regla de firewall](/cli/azure/postgres/server/firewall-rule#delete) comando. Proporcione el nombre de Hola Hola existente de regla de firewall.
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
Cuando se realiza correctamente, no hay ninguna salida. En caso de error, se devuelve el texto del mensaje de error de Hola.

## <a name="next-steps"></a>Pasos siguientes
- De forma similar, puede utilizar un explorador web demasiado[crear y administrar la base de datos PostgreSQL las reglas de firewall mediante Hola portal de Azure](howto-manage-firewall-using-portal.md)
- Para más información, consulte [Reglas de firewall de servidor de Azure Database for PostgreSQL](concepts-firewall-rules.md).
- Para obtener ayuda sobre conexión tooan base de datos de Azure para PostgreSQL server, vea [bibliotecas de conexiones de base de datos de PostgreSQL](concepts-connection-libraries.md)
