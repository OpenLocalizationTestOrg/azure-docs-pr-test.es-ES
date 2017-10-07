---
title: "CLI de Azure: creación de una base de datos SQL | Microsoft Docs"
description: "Obtenga información acerca de cómo toocreate un servidor lógico de la base de datos SQL, regla de firewall de nivel de servidor y bases de datos mediante Hola CLI de Azure."
keywords: "tutorial de sql database, creación de una base de datos sql"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: 9b1ffb17eabeb70a000ff0c997128832b07aa4fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-hello-azure-cli"></a>Crear una base de datos de SQL Azure solo mediante Hola CLI de Azure

Hola CLI de Azure es toocreate usado y administrar recursos de Azure desde la línea de comandos de Hola o en scripts. Esta guía de detalles mediante hello Azure CLI toodeploy una base de datos de SQL Azure en un [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md) en un [servidor lógico de base de datos de SQL Azure](sql-database-features.md).

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="define-variables"></a>Definición de variables

Definir variables para su uso en scripts de hello en esta guía de inicio rápido.

```azurecli-interactive
# hello data center and resource name for your resources
export resourcegroupname = myResourceGroup
export location = westeurope
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
export servername = server-$RANDOM
# Set an admin login and password for your database
export adminlogin = ServerAdmin
export password = ChangeYourAdminPassword1
# hello ip address range that you want tooallow tooaccess your DB
export startip = "0.0.0.0"
export endip = "0.0.0.0"
# hello database name
export databasename = mySampleDatabase
```

## <a name="create-a-resource-group"></a>Crear un grupo de recursos

Crear un [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md) con hello [crear grupo az](/cli/azure/group#create) comando. Un grupo de recursos es un contenedor lógico en el que se implementan y se administran recursos de Azure como un grupo. Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en hello `westeurope` ubicación.

```azurecli-interactive
az group create --name $resourcegroupname --location $location
```
## <a name="create-a-logical-server"></a>un servidor lógico

Crear un [servidor lógico de base de datos de SQL Azure](sql-database-features.md) con hello [az sql server crear](/cli/azure/sql/server#create) comando. Un servidor lógico contiene un conjunto de bases de datos administradas como un grupo. Hello en el ejemplo siguiente se crea un servidor de forma aleatoria con nombre en el grupo de recursos con un inicio de sesión de administración denominado `ServerAdmin` y una contraseña de `ChangeYourAdminPassword1`. Cambie estos valores predefinidos por los que prefiera.

```azurecli-interactive
az sql server create --name $servername --resource-group $resourcegroupname --location $location \
    --admin-user $adminlogin --admin-password $password
```

## <a name="configure-a-server-firewall-rule"></a>Configuración de una regla de firewall del servidor

Crear un [regla de firewall de nivel de servidor de base de datos de SQL Azure](sql-database-firewall-configure.md) con hello [az sql server crea](/cli/azure/sql/server/firewall-rule#create) comando. Una regla de firewall de nivel de servidor permite que una aplicación externa, como SQL Server Management Studio o hello SQLCMD utilidad tooconnect tooa base de datos SQL a través de firewall de servicio de base de datos SQL de Hola. En el siguiente ejemplo de Hola, solo se abrirá el firewall de Hola para otros recursos de Azure. tooenable conectividad externa, cambio Hola IP dirección tooan dirección adecuada para su entorno. tooopen todas las direcciones IP, utilice 0.0.0.0 como Hola a partir de dirección IP y 255.255.255.255 como Hola dirección final.  

```azurecli-interactive
az sql server firewall-rule create --resource-group $resourcegroupname --server $servername \
    -n AllowYourIp --start-ip-address $startip --end-ip-address $endip
```

> [!NOTE]
> SQL Database se comunica a través del puerto 1433. Si está tratando de tooconnect desde dentro de una red corporativa, es posible que firewall de su red no permite el tráfico saliente en el puerto 1433. Si es así, no será capaz de tooconnect tooyour base de datos de SQL Azure servidor a menos que el departamento de TI abre el puerto 1433.
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a>Crear una base de datos en el servidor de hello con datos de ejemplo

Crear una base de datos con un [nivel de rendimiento S0](sql-database-service-tiers.md) en servidor de hello mediante Hola [crear base de datos de sql az](/cli/azure/sql/db#create) comando. Hello en el ejemplo siguiente se crea una base de datos denominada `mySampleDatabase` y carga Hola datos de ejemplo AdventureWorksLT en esta base de datos. Reemplazar predefinidos de estos valores según sea necesario (otras guías rápidas en esta colección se basan en valores de hello en esta guía de inicio rápido).

```azurecli-interactive
az sql db create --resource-group $resourcegroupname --server $servername \
    --name $databasename --sample-name AdventureWorksLT --service-objective S0
```

## <a name="clean-up-resources"></a>Limpieza de recursos

Otras guías de inicio rápido de esta colección se basan en los valores de esta. 

> [!TIP]
> Si tiene previsto toocontinue toowork con guías rápidas posteriores, no limpiar los recursos de hello creados en esta rápida se inician. Si no tiene previsto toocontinue, use Hola seguido toodelete pasos creado todos los recursos de esta guía de inicio rápido en hello portal de Azure.
>

```azurecli-interactive
az group delete --name $resourcegroupname
```

## <a name="next-steps"></a>Pasos siguientes

Ahora que tiene una base de datos, puede conectarse y realizar consultas con las herramientas que desee. Para más información, seleccione una de las herramientas siguientes:

- [SQL Server Management Studio](sql-database-connect-query-ssms.md)
- [código de Visual Studio](sql-database-connect-query-vscode.md)
- [.NET](sql-database-connect-query-dotnet.md)
- [PHP](sql-database-connect-query-php.md)
- [Node.js](sql-database-connect-query-nodejs.md)
- [Java](sql-database-connect-query-java.md)
- [Python](sql-database-connect-query-python.md)
- [Ruby](sql-database-connect-query-ruby.md)

