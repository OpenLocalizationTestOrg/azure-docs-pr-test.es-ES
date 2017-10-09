---
title: "Inicio rápido: Creación de una Base de datos de Azure para el servidor MySQL: CLI de Azure | Microsoft Docs"
description: "Este tutorial describe cómo toouse Hola toocreate de CLI de Azure a una base de datos de Azure para servidor de MySQL en un grupo de recursos de Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: hero-article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 708d0cce12e812cb464adcf7e83e6f85c196bafe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a>Creación de una Base de datos de Azure para el servidor MySQL con la CLI de Azure
Este tutorial describe cómo toouse Hola CLI de Azure toocreate una base de datos de Azure para servidor de MySQL en un grupo de recursos de Azure en aproximadamente cinco minutos. Hola CLI de Azure es toocreate usado y administrar recursos de Azure desde la línea de comandos de Hola o en scripts.

Si no tiene una suscripción a Azure, cree una cuenta [gratuita](https://azure.microsoft.com/free/) antes de empezar.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

Si tiene varias suscripciones, elija Hola de suscripción adecuado en el que recurso de hello existe o se factura para. Seleccione un identificador de suscripción específico en su cuenta mediante el comando [az account set](/cli/azure/account#set).
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a>Crear un grupo de recursos
Crear un [grupo de recursos de Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) con hello [crear grupo az](https://docs.microsoft.com/cli/azure/group#create) comando. Un grupo de recursos es un contenedor lógico en el que se implementan y se administran recursos de Azure como un grupo.

Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myresourcegroup` en hello `westus` ubicación.

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a>Creación de un servidor de Azure Database for MySQL
Crear una base de datos de Azure para servidor de MySQL con hello **crear servidor de mysql az** comando. Un servidor puede administrar varias bases de datos. Normalmente se usa una base de datos independiente para cada proyecto o para cada usuario.

Hello en el ejemplo siguiente se crea una base de datos de Azure para MySQL server que se encuentra en `westus` en grupo de recursos de hello `myresourcegroup` con nombre `myserver4demo`. servidor de Hello tiene un inicio de sesión de administrador en denominado `myadmin` y la contraseña `Password01!`. Hola servidor se crea con **básica** nivel de rendimiento y **50** unidades que se comparten entre todas las bases de datos de hello en el servidor de Hola de proceso. Puede escalar almacenamiento y el proceso hacia arriba o hacia abajo según las necesidades de aplicación Hola.

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a>Configurar de la regla de firewall
Crear una base de datos de Azure para la regla de firewall de nivel de servidor de MySQL mediante hello **crear az mysql server regla de firewall** comando. Una regla de firewall de nivel de servidor permite que una aplicación externa, por ejemplo, hello **mysql.exe** herramienta de línea de comandos o servidor de MySQL Workbench tooconnect tooyour a través de firewall de servicio de MySQL de Azure de Hola. 

Hello en el ejemplo siguiente se crea una regla de firewall para un intervalo de direcciones predefinidos, que en este ejemplo es Hola todo posible intervalo de direcciones IP.

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a>Configuración de SSL
De manera predeterminada, se exigen conexiones SSL entre su servidor y las aplicaciones cliente.  Esto garantiza la seguridad de "en movimiento" Hola a datos mediante el cifrado de flujo de datos de hello en internet.  toomake más fácil de inicio de este rápido, se deshabilita las conexiones SSL para el servidor.  Esto no se recomienda en servidores de producción.  Para obtener más información, consulte [tooAzure base de datos de conexión de conectividad de configurar SSL en su aplicación toosecurely para MySQL](./howto-configure-ssl.md).

Hello en el ejemplo siguiente se deshabilita la implantación SSL en el servidor MySQL.
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo -g -n --ssl-enforcement Disabled
 ```

## <a name="get-hello-connection-information"></a>Obtener información de conexión de Hola

tooconnect tooyour server, necesita credenciales de acceso y la información de host de tooprovide.

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

resultado de Hello es en formato JSON. Tome nota de hello **fullyQualifiedDomainName** y **Iniciodesesióndeadministrador**.
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "myserver4demo.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforMySQL/servers/myserver4demo",
  "location": "westus",
  "name": "myserver4demo",
  "resourceGroup": "myresourcegroup",
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

## <a name="connect-toohello-server-using-hello-mysqlexe-command-line-tool"></a>Conectar servidor toohello mediante la herramienta de línea de comandos de hello mysql.exe
Conectar servidor tooyour con hello **mysql.exe** herramienta de línea de comandos. Puede descargarlo desde [aquí](https://dev.mysql.com/downloads/) e instalarlo en su equipo. En su lugar, también puede hacer clic en hello **inténtelo** situado en ejemplos de código u Hola `>_` botón de hello superior derecho barra de herramientas de hello portal de Azure y lanzamiento hello **Shell en la nube de Azure**.

Escriba Hola siguientes comandos: 

1. Conectar con servidor de toohello **mysql** herramienta de línea de comandos:
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. Ver el estado del servidor:
```sql
 mysql> status
```
Si todo va bien, herramienta de línea de comandos de hello debe devolver Hola siguiente texto:

```dos
C:\Users\>mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
Enter password: ***********
Welcome toohello MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 65512
Server version: 5.6.26.0 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' tooclear hello current input statement.

mysql> status
--------------
mysql  Ver 14.14 Distrib 5.6.35, for Win64 (x86_64)

Connection id:          65512
Current database:
Current user:           myadmin@116.230.243.143
SSL:                    Not in use
Using delimiter:        ;
Server version:         5.6.26.0 MySQL Community Server (GPL)
Protocol version:       10
Connection:             myserver4demo.mysql.database.azure.com via TCP/IP
Server characterset:    latin1
Db     characterset:    latin1
Client characterset:    gbk
Conn.  characterset:    gbk
TCP port:               3306
Uptime:                 2 days 9 hours 47 min 20 sec

Threads: 4  Questions: 34833  Slow queries: 2  Opens: 84  Flush tables: 4  Open tables: 1  Queries per second avg: 0.167
--------------

mysql>
```

> [!TIP]
> Para otros comandos, consulte el [capítulo 4.5.1 del Manual de referencia de MySQL 5.7](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a>Conectar servidor toohello mediante la herramienta de interfaz gráfica de usuario de MySQL Workbench Hola
1.  Inicie Hola aplicación MySQL Workbench en el equipo cliente. Puede descargar e instalar MySQL Workbench desde [aquí](https://dev.mysql.com/downloads/workbench/).

2.  Hola **el programa de instalación nueva conexión** diálogo cuadro, escriba Hola siguiente información **parámetros** ficha:

   ![Configuración de una conexión nueva](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| **Configuración** | **Valor sugerido** | **Descripción** |
|---|---|---|
|   Nombre de la conexión | Mi conexión | Especifique una etiqueta para esta conexión (puede ser cualquier cosa) |
| Método de conexión | elija Estándar (TCP/IP) | Usar TCP/IP protocolo tooconnect tooAzure base de datos de MySQL > |
| Nombre de host. | myserver4demo.mysql.database.azure.com | Nombre del servidor que anotó anteriormente. |
| Port | 3306 | se utiliza el puerto predeterminado de Hola para MySQL. |
| Nombre de usuario | myadmin@myserver4demo | Hola servidor administrador inicio de sesión que anotó anteriormente. |
| Password | **** | Utilice la contraseña de la cuenta de administrador Hola que configuró anteriormente. |

Haga clic en **Probar conexión** tootest si todos los parámetros están configurados correctamente.
Ahora, puede hacer clic en conexión de hello toosuccessfully conectar toohello server.

## <a name="clean-up-resources"></a>Limpieza de recursos
Si no necesita estos recursos para otro/tutorial de inicio rápido, puede eliminarlas haciendo Hola siguiente comando: 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Diseño de una base de datos MySQL con la CLI de Azure](./tutorial-design-database-using-cli.md)
