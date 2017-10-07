---
title: "Diseño de la primera base de datos de Azure Database for PostgreSQL con la CLI de Azure | Microsoft Docs"
description: "Este tutorial muestra cómo tooDesign Azure primera base de datos de PostgreSQL con CLI de Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: tutorial
ms.date: 06/13/2017
ms.openlocfilehash: 7914925c090e0b6f3e7c8a999eedb0b2baf83d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-azure-cli"></a>Diseño de la primera base de datos de Azure Database for PostgreSQL con la CLI de Azure 
En este tutorial, usará Azure CLI (interfaz de línea de comandos) y otra utilidades toolearn cómo para:
> [!div class="checklist"]
> * Creación de una instancia de Azure Database for PostgreSQL
> * Configurar firewall de servidor hello
> * Use [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) utilidad toocreate una base de datos
> * Carga de datos de ejemplo
> * Datos de consulta
> * Actualización de datos
> * Restauración de datos

Puede usar hello Shell en la nube de Azure en el Explorador de hello, o [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli) en sus propios bloques de código de equipo toorun hello en este tutorial.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

Si tiene varias suscripciones, elija Hola de suscripción adecuado en el que recurso de hello existe o se factura para. Seleccione un identificador de suscripción específico en su cuenta mediante el comando [az account set](/cli/azure/account#set).
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a>Crear un grupo de recursos
Crear un [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md) con hello [crear grupo az](/cli/azure/group#create) comando. Un grupo de recursos es un contenedor lógico en el que se implementan y se administran recursos de Azure como un grupo. Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myresourcegroup` en hello `westus` ubicación.
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a>Creación de un servidor de Azure Database for PostgreSQL
Crear un [base de datos de Azure para PostgreSQL server](overview.md) con hello [az postgres servidor crear](/cli/azure/postgres/server#create) comando. Un servidor contiene un conjunto de bases de datos administradas como un grupo. 

Hello en el ejemplo siguiente se crea un servidor denominado `mypgserver-20170401` en el grupo de recursos `myresourcegroup` con inicio de sesión de administrador de servidor `mylogin`. Nombre de un servidor asigna nombre tooDNS y, por tanto, es necesario toobe globalmente único en Azure. Hola sustituto `<server_admin_password>` con su propio valor.
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401 --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> inicio de sesión de administrador de servidor de Hola y la contraseña que especifique aquí son necesario toolog en toohello server y sus bases de datos más adelante en esta guía de inicio rápido. Recuerde o grabe esta información para su uso posterior.

De forma predeterminada, la base de datos de **postgres** se crea en el servidor. Hola [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) base de datos es una base de datos predeterminada destinado a los usuarios, utilidades y aplicaciones de otros fabricantes. 


## <a name="configure-a-server-level-firewall-rule"></a>Configuración de una regla de firewall de nivel de servidor

Crear una regla de firewall de nivel de servidor de Azure PostgreSQL con hello [crear az postgres servidor regla de firewall](/cli/azure/postgres/server/firewall-rule#create) comando. Una regla de firewall de nivel de servidor permite que una aplicación externa, como [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) o [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server a través de firewall de servicio de hello Azure PostgreSQL. 

Puede establecer una regla de firewall que abarca un intervalo IP toobe tooconnect capaz de la red. Hello siguiente ejemplo se utiliza [crear az postgres servidor regla de firewall](/cli/azure/postgres/server/firewall-rule#create) toocreate una regla de firewall `AllowAllIps` para una dirección IP, intervalo. tooopen todas las direcciones IP, utilice 0.0.0.0 como Hola a partir de dirección IP y 255.255.255.255 como Hola dirección final.
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> El servidor Azure PostgreSQL se comunica a través de puerto 5432. Al conectarse desde una red corporativa, es posible que el firewall de la red no permita el tráfico saliente a través del puerto 5432. Tiene el departamento de TI abrir puerto 5432 tooconnect tooyour base de datos de Azure SQL server.
>

## <a name="get-hello-connection-information"></a>Obtener información de conexión de Hola

tooconnect tooyour server, necesita credenciales de acceso y la información de host de tooprovide.
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

resultado de Hello es en formato JSON. Tome nota de hello **Iniciodesesióndeadministrador** y **fullyQualifiedDomainName**.
```json
{
  "administratorLogin": "mylogin",
  "fullyQualifiedDomainName": "mypgserver-20170401.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforPostgreSQL/servers/mypgserver-20170401",
  "location": "westus",
  "name": "mypgserver-20170401",
  "resourceGroup": "myresourcegroup",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "PGSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 51200,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": "9.6"
}
```

## <a name="connect-tooazure-database-for-postgresql-database-using-psql"></a>Conectar tooAzure base de datos para la base de datos de PostgreSQL mediante psql
Si el equipo cliente tenga PostgreSQL instalado, puede usar una instancia local de [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), o el servidor de hello consola en la nube de Azure tooconnect tooan PostgreSQL de Azure. Vamos a usar ahora hello psql utilidad de línea de comandos tooconnect toohello base de datos de Azure para servidor de PostgreSQL.

1. Ejecute hello después psql comandos tooconnect tooan base de datos de Azure para servidor de PostgreSQL
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  Por ejemplo, hello siguiente comando conecta a base de datos de toohello predeterminada denominada **postgres** en el servidor de PostgreSQL **mypgserver 20170401.postgres.database.azure.com** utilizando las credenciales de acceso. Escriba hello `<server_admin_password>` elegido cuando se le solicite una contraseña.
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 ---dbname=postgres
```

2.  Una vez que esté conectado toohello server, cree una base de datos en blanco en el símbolo del sistema de Hola.
```sql
CREATE DATABASE mypgsqldb;
```

3.  En el símbolo del sistema de hello, ejecute hello después de la base de datos de comando tooswitch conexión toohello recién creado **mypgsqldb**:
```sql
\c mypgsqldb
```

## <a name="create-tables-in-hello-database"></a>Crear tablas de base de datos de Hola
Ahora que sabe cómo tooconnect toohello base de datos de Azure para PostgreSQL, podemos ver cómo toocomplete algunas tareas básicas.

En primer lugar, podemos crear una tabla y cargarla con algunos datos. Vamos a crear una tabla que hace el seguimiento de información del inventario.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

Puede ver Hola recién creado tabla en la lista de Hola de tablas ahora escribiendo:
```sql
\dt
```

## <a name="load-data-into-hello-tables"></a>Cargar datos en tablas de Hola
Ahora que tenemos una tabla, podemos insertar algunos datos en ella. En la ventana de símbolo del sistema abierto hello, ejecute hello después consulta tooinsert algunas filas de datos
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

Tiene ahora dos filas de datos de ejemplo en la tabla de Hola que creó anteriormente.

## <a name="query-and-update-hello-data-in-hello-tables"></a>Consultar y actualizar los datos de hello en tablas de Hola
Ejecute hello siguientes tooretrieve información de consulta de tabla de base de datos de Hola. 
```sql
SELECT * FROM inventory;
```

También puede actualizar los datos de hello en tablas de Hola
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

fila de Hola se actualiza en consecuencia cuando se recuperan datos.
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Restaurar un punto anterior de tooa de base de datos en el tiempo
Imagine que ha eliminado accidentalmente una tabla. No se puede recuperar con facilidad. Base de datos de Azure para PostgreSQL permite toogo tooany atrás en un momento (en Hola última too7 días (Basic) y 35 días (estándar)) y restaurar este punto-in-time tooa nuevo servidor. Puede usar esta nueva toorecover server los datos eliminados. Hola siguiendo los pasos restauración Hola ejemplo servidor tooa punto antes de que se ha agregado Hola tabla.

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

Hola `az postgres server restore` comando necesita Hola parámetros siguientes:
| Configuración | Valor sugerido | Descripción  |
| --- | --- | --- |
| --resource-group |  myResourceGroup |  El grupo de recursos en qué Hola existe el servidor de origen.  |
| --name | mypgserver-restored | nombre de Hola de hello nuevo servidor que se crea mediante el comando de restauración de Hola. |
| restore-point-in-time | 2017-04-13T13:59:00Z | Seleccione un toorestore en un momento a. Esta fecha y hora deben ser dentro del período de retención de copia de seguridad del servidor de origen de Hola. Use el formato de fecha y hora ISO8601. Por ejemplo, puede usar su propia zona horaria local, como `2017-04-13T05:59:00-08:00`, o usar el formato de hora Zulú UTC `2017-04-13T13:59:00Z`. |
| --source-server | mypgserver-20170401 | nombre de Hola o Id. de hello toorestore de servidor de origen de. |

Restaurar un servidor tooa en un momento, crea un nuevo servidor, copiar como servidor original, Hola desde el punto de hello en el tiempo que especifique. ubicación de Hola y precios valores de nivel de servidor hello restaurado se Hola igual que el servidor de origen de Hola.

comando Hello es sincrónico y se devolverá una vez se haya restaurado el servidor de Hola. Una vez finalizada la restauración de hello, busque servidor nuevo de Hola que se creó. Compruebe Hola se restauran datos según lo previsto.


## <a name="next-steps"></a>Pasos siguientes
En este tutorial, se habrá aprendido cómo toouse Azure CLI (interfaz de línea de comandos) y otras utilidades para:
> [!div class="checklist"]
> * Creación de una instancia de Azure Database for PostgreSQL
> * Configurar firewall de servidor hello
> * Use [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) utilidad toocreate una base de datos
> * Carga de datos de ejemplo
> * Datos de consulta
> * Actualización de datos
> * Restauración de datos

A continuación, obtenga información acerca de cómo toouse Hola tareas similares de Azure toodo portal, revise este tutorial: [diseñar la primera base de datos de Azure para usar PostgreSQL Hola portal de Azure](tutorial-design-database-using-azure-portal.md)
