---
title: Crear una base de datos de Azure para PostgreSQL mediante Hola CLI de Azure | Documentos de Microsoft
description: "Rápido toocreate de guía de inicio y administrar la base de datos de Azure para el servidor de PostgreSQL usando Azure CLI (interfaz de línea de comandos)."
services: postgresql
author: sanagama
ms.author: sanagama
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: quickstart
ms.date: 06/13/2017
ms.openlocfilehash: 946aa3cbf5ff9f5ac4e51248412d3da5d718141e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-using-hello-azure-cli"></a>Crear una base de datos de Azure para PostgreSQL mediante Hola CLI de Azure
Base de datos de Azure para PostgreSQL es un servicio administrado que le permite toorun, administrar y escalar las bases de datos de PostgreSQL altamente disponibles en la nube de Hola. Hola CLI de Azure es toocreate usado y administrar recursos de Azure desde la línea de comandos de Hola o en scripts. Este tutorial rápido muestra cómo toocreate una Azure base de datos para el servidor de PostgreSQL en un [grupo de recursos de Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) utilizando Hola CLI de Azure.

Si no tiene una suscripción a Azure, cree una cuenta [gratuita](https://azure.microsoft.com/free/) antes de empezar.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

Si tiene varias suscripciones, elija suscripción adecuado de hello en el que se cobrará recursos Hola. Seleccione un identificador de suscripción específico en su cuenta mediante el comando [az account set](/cli/azure/account#set).
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

Hello en el ejemplo siguiente se crea un servidor denominado `mypgserver-20170401` en el grupo de recursos `myresourcegroup` con inicio de sesión de administrador de servidor `mylogin`. nombre de Hola de un servidor asigna nombre tooDNS y, por tanto, es necesario toobe globalmente único en Azure. Hola sustituto `<server_admin_password>` con su propio valor.
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401  --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
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

## <a name="connect-toopostgresql-database-using-psql"></a>Conectar la base de datos de tooPostgreSQL con psql

Si el equipo cliente tenga PostgreSQL instalado, puede usar una instancia local de [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooconnect tooan Azure PostgreSQL server. Vamos a usar ahora servidor de hello psql utilidad de línea de comandos tooconnect toohello PostgreSQL de Azure.

1. Ejecute hello después psql comandos tooconnect tooan base de datos de Azure para servidor de PostgreSQL
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  Por ejemplo, hello siguiente comando conecta a base de datos de toohello predeterminada denominada **postgres** en el servidor de PostgreSQL **mypgserver 20170401.postgres.database.azure.com** utilizando las credenciales de acceso. Escriba hello `<server_admin_password>` elegido cuando se le solicite una contraseña.
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
```

2.  Una vez que esté conectado toohello server, cree una base de datos en blanco en el símbolo del sistema de Hola.
```sql
CREATE DATABASE mypgsqldb;
```

3.  En el símbolo del sistema de hello, ejecute hello después de la base de datos de comando tooswitch conexión toohello recién creado **mypgsqldb**:
```sql
\c mypgsqldb
```

## <a name="connect-toopostgresql-database-using-pgadmin"></a>Conectar la base de datos de tooPostgreSQL mediante pgAdmin

tooconnect tooAzure PostgreSQL server mediante la herramienta de interfaz gráfica de usuario de hello _pgAdmin_
1.  Iniciar hello _pgAdmin_ aplicación en el equipo cliente. Puede instalar _pgAdmin_ desde http://www.pgadmin.org/.
2.  Elija **Agregar nuevo servidor** de hello **vínculos rápidos** menú.
3.  Hola **crear - Server** cuadro de diálogo **General** ficha, escriba un nombre descriptivo único para el servidor de Hola. como **Azure PostgreSQL Server**.
 ![Herramienta pgAdmin: crear servidor](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)
4.  Hola **crear - Server** cuadro de diálogo, **conexión** ficha:
    - Escriba el nombre del servidor de acceso completa de hello (por ejemplo, **mypgserver 20170401.postgres.database.azure.com**) en hello **nombre de Host / dirección** cuadro. 
    - Escriba el puerto 5432 en hello **puerto** cuadro. 
    - Escriba hello **inicio de sesión de administrador de servidor (user@mypgserver)** obtenido anteriormente en este inicio rápido y la contraseña que especificó cuando creó el servidor hello en hello **nombre de usuario** y **contraseña** cuadros, respectivamente.
    - Seleccione el **Modo SSL** como **Requerir**. De forma predeterminada, todos los servidores de Azure PostgreSQL se crean para que se EXIJA SSL. tooturn desactivar exigir SSL, consulte los detalles en [exigir SSL](./concepts-ssl-connection-security.md).

    ![pgAdmin: Crear servidor](./media/quickstart-create-server-database-azure-cli/2-pgadmin-create-server.png)
5.  Haga clic en **Guardar**.
6.  En el panel izquierdo del explorador de hello, expanda hello **grupos de servidores**. Seleccione su **servidor Azure PostgreSQL**.
7.  Elija hello **Server** conectado a y, a continuación, elija **bases de datos** en él. 
8.  Haga doble clic en **bases de datos** tooCreate una base de datos.
9.  Elija un nombre de base de datos **mypgsqldb** y propietario de Hola para él como inicio de sesión de administrador de servidor **mylogin**.
10. Haga clic en **guardar** toocreate una base de datos en blanco.
11. Hola **explorador**, expanda hello **servidores** grupo. Expanda servidor hello que ha creado y vea base de datos de hello **mypgsqldb** en él.
 ![pgAdmin: Crear base de datos](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)


## <a name="clean-up-resources"></a>Limpieza de recursos

Limpiar todos los recursos creados en Inicio rápido de hello eliminando hello [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md).

> [!TIP]
> Otras guías de inicio rápido de esta colección se basan en los valores de esta. Si tiene previsto toocontinue toowork con los siguientes tutoriales rápidos, realice la limpieza no Hola recursos creados en este tutorial rápido. Si no tiene previsto toocontinue, use Hola siguiendo los pasos toodelete todos los recursos creados por este inicio rápido en hello CLI de Azure.

```azurecli-interactive
az group delete --name myresourcegroup
```

Si solo desea que servidor de toodelete Hola uno recién creado, puede ejecutar [eliminación del servidor postgres az](/cli/azure/postgres/server#delete) comando.
```azurecli-interactive
az postgres server delete --resource-group myresourcegroup --name mypgserver-20170401
```

## <a name="next-steps"></a>Pasos siguientes
> [!div class="nextstepaction"]
> [Migración de una base de datos mediante exportación e importación](./howto-migrate-using-export-and-import.md)
