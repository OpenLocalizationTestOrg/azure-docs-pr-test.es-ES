---
title: aaaDesign Azure primero la base de datos para la base de datos de MySQL - CLI de Azure | Documentos de Microsoft
description: "Este tutorial le explica cómo toocreate y administrar la base de datos de MySQL server y base de datos mediante Azure CLI 2.0 de línea de comandos de Hola."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 6339913c2af58e0e4c4eabb69097a5c9c245781c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a>Diseño de la primera base de datos de Azure Database for MySQL

Base de datos de Azure para MySQL es un servicio de base de datos relacional en la nube de Microsoft que se basa en el motor de base de datos de MySQL Community Edition Hola. En este tutorial, usará Azure CLI (interfaz de línea de comandos) y otra utilidades toolearn cómo para:

> [!div class="checklist"]
> * Creación de una instancia de Azure Database for MySQL
> * Configurar firewall de servidor hello
> * Use [herramienta de línea de comandos de mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate una base de datos
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
Cree un [grupo de recursos](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) con el comando [az group create](https://docs.microsoft.com/cli/azure/group#create). Un grupo de recursos es un contenedor lógico en el que se implementan y se administran recursos de Azure como un grupo.

Hello en el ejemplo siguiente se crea un grupo de recursos denominado `mycliresource` en hello `westus` ubicación.

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a>Creación de un servidor de Azure Database for MySQL
Cree una base de datos de MySQL server con servidor de mysql de hello az crear comando. Un servidor puede administrar varias bases de datos. Normalmente se usa una base de datos independiente para cada proyecto o para cada usuario.

Hello en el ejemplo siguiente se crea una base de datos de Azure para MySQL server que se encuentra en `westus` en grupo de recursos de hello `mycliresource` con nombre `mycliserver`. servidor de Hello tiene un inicio de sesión de administrador en denominado `myadmin` y la contraseña `Password01!`. Hola servidor se crea con **básica** nivel de rendimiento y **50** unidades que se comparten entre todas las bases de datos de hello en el servidor de Hola de proceso. Puede escalar almacenamiento y el proceso hacia arriba o hacia abajo según las necesidades de aplicación Hola.

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a>Configurar de la regla de firewall
Crear una base de datos de Azure para comando de creación de la regla de firewall de nivel de servidor de MySQL con hello az mysql server-regla de firewall. Una regla de firewall de nivel de servidor permite que una aplicación externa, como **mysql** herramienta de línea de comandos o servidor de MySQL Workbench tooconnect tooyour a través de firewall de servicio de MySQL de Azure de Hola. 

Hello en el ejemplo siguiente se crea una regla de firewall para un intervalo de direcciones predefinidas. Este ejemplo muestra hello todo posible intervalo de direcciones IP.

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-hello-connection-information"></a>Obtener información de conexión de Hola

tooconnect tooyour server, necesita credenciales de acceso y la información de host de tooprovide.
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

resultado de Hello es en formato JSON. Tome nota de hello **fullyQualifiedDomainName** y **Iniciodesesióndeadministrador**.
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mycliserver.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/mycliresource/providers/Microsoft.DBforMySQL/servers/mycliserver",
  "location": "westus",
  "name": "mycliserver",
  "resourceGroup": "mycliresource",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "MYSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforMySQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

## <a name="connect-toohello-server-using-mysql"></a>Conectar con mysql de servidor de toohello
Use [herramienta de línea de comandos de mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish una tooyour de conexión base de datos de MySQL server. En este ejemplo, el comando de hello es:
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a>Crear una base de datos en blanco
Una vez que esté conectado toohello server, cree una base de datos en blanco.
```sql
mysql> CREATE DATABASE mysampledb;
```

En el símbolo del sistema de hello, ejecute hello después de la base de datos de comando tooswitch Hola conexión toothis recién creado:
```sql
mysql> USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a>Crear tablas de base de datos de Hola
Ahora que sabe cómo tooconnect toohello base de datos de Azure para la base de datos MySQL, podemos ver cómo toocomplete algunas tareas básicas.

En primer lugar, podemos crear una tabla y cargarla con algunos datos. Vamos a crear una tabla que almacena la información del inventario.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a>Cargar datos en tablas de Hola
Ahora que tenemos una tabla, podemos insertar algunos datos en ella. En la ventana de símbolo del sistema abierto hello, ejecute hello después consulta tooinsert algunas filas de datos.
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

Ahora tiene dos filas de datos de ejemplo en la tabla de Hola que creó anteriormente.

## <a name="query-and-update-hello-data-in-hello-tables"></a>Consultar y actualizar los datos de hello en tablas de Hola
Ejecute hello siguientes tooretrieve información de consulta de tabla de base de datos de Hola.
```sql
SELECT * FROM inventory;
```

También puede actualizar los datos de hello en tablas de Hola.
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

fila de Hola se actualiza en consecuencia cuando se recuperan datos.
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Restaurar un punto anterior de tooa de base de datos en el tiempo
Imagine que eliminó accidentalmente esta tabla. No se puede recuperar con facilidad. Azure base de datos de MySQL permite toogo tooany atrás punto en el tiempo en hello última los días de too35 y restaurar este punto en el nuevo servidor de tiempo tooa. Puede usar esta nueva toorecover server los datos eliminados. Hola siguiendo los pasos restauración Hola ejemplo servidor tooa punto antes de que se ha agregado Hola tabla.

Para hello restauración necesita Hola siguiente información:

- Punto de restauración: seleccione un punto-in-time que se produce antes de hello servidor se ha modificado. Debe ser mayor que o igual a value de copia de seguridad más antigua toohello origen la base de datos.
- Servidor de destino: especifique un nuevo nombre de servidor que desee toorestore a
- Servidor de origen: proporcionar nombre Hola Hola del servidor de que desea toorestore desde
- Ubicación: No se puede seleccionar una región hello, de forma predeterminada es igual que el servidor de origen de Hola

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

servidor de hello toorestore y [tooa en el momento de restaurar](./howto-restore-server-portal.md) antes de que se eliminó la tabla de Hola. Restauración tooa otro punto de servidor en el tiempo crea un duplicado en el servidor nuevo como servidor original Hola de punto de hello en el tiempo especificado, siempre que esté dentro del período de retención de Hola para su [nivel de servicio](./concepts-service-tiers.md).

## <a name="next-steps"></a>Pasos siguientes
En este tutorial aprendió lo siguiente:
> [!div class="checklist"]
> * Creación de una instancia de Azure Database for MySQL
> * Configurar firewall de servidor hello
> * Use [herramienta de línea de comandos de mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate una base de datos
> * Carga de datos de ejemplo
> * Datos de consulta
> * Actualización de datos
> * Restauración de datos

> [!div class="nextstepaction"]
> [Ejemplos de la CLI de Azure para Azure Database for MySQL](./sample-scripts-azure-cli.md)
