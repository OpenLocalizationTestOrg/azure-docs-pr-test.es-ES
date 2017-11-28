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
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="f482c-103">Diseño de la primera base de datos de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="f482c-103">Design your first Azure Database for MySQL database</span></span>

<span data-ttu-id="f482c-104">Base de datos de Azure para MySQL es un servicio de base de datos relacional en la nube de Microsoft que se basa en el motor de base de datos de MySQL Community Edition Hola.</span><span class="sxs-lookup"><span data-stu-id="f482c-104">Azure Database for MySQL is a relational database service in hello Microsoft cloud based on MySQL Community Edition database engine.</span></span> <span data-ttu-id="f482c-105">En este tutorial, usará Azure CLI (interfaz de línea de comandos) y otra utilidades toolearn cómo para:</span><span class="sxs-lookup"><span data-stu-id="f482c-105">In this tutorial, you use Azure CLI (command-line interface) and other utilities toolearn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f482c-106">Creación de una instancia de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="f482c-106">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="f482c-107">Configurar firewall de servidor hello</span><span class="sxs-lookup"><span data-stu-id="f482c-107">Configure hello server firewall</span></span>
> * <span data-ttu-id="f482c-108">Use [herramienta de línea de comandos de mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate una base de datos</span><span class="sxs-lookup"><span data-stu-id="f482c-108">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate a database</span></span>
> * <span data-ttu-id="f482c-109">Carga de datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f482c-109">Load sample data</span></span>
> * <span data-ttu-id="f482c-110">Datos de consulta</span><span class="sxs-lookup"><span data-stu-id="f482c-110">Query data</span></span>
> * <span data-ttu-id="f482c-111">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="f482c-111">Update data</span></span>
> * <span data-ttu-id="f482c-112">Restauración de datos</span><span class="sxs-lookup"><span data-stu-id="f482c-112">Restore data</span></span>

<span data-ttu-id="f482c-113">Puede usar hello Shell en la nube de Azure en el Explorador de hello, o [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli) en sus propios bloques de código de equipo toorun hello en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="f482c-113">You may use hello Azure Cloud Shell in hello browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer toorun hello code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f482c-114">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="f482c-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f482c-115">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="f482c-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="f482c-116">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f482c-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="f482c-117">Si tiene varias suscripciones, elija Hola de suscripción adecuado en el que recurso de hello existe o se factura para.</span><span class="sxs-lookup"><span data-stu-id="f482c-117">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="f482c-118">Seleccione un identificador de suscripción específico en su cuenta mediante el comando [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="f482c-118">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="f482c-119">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="f482c-119">Create a resource group</span></span>
<span data-ttu-id="f482c-120">Cree un [grupo de recursos](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) con el comando [az group create](https://docs.microsoft.com/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f482c-120">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) with [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="f482c-121">Un grupo de recursos es un contenedor lógico en el que se implementan y se administran recursos de Azure como un grupo.</span><span class="sxs-lookup"><span data-stu-id="f482c-121">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="f482c-122">Hello en el ejemplo siguiente se crea un grupo de recursos denominado `mycliresource` en hello `westus` ubicación.</span><span class="sxs-lookup"><span data-stu-id="f482c-122">hello following example creates a resource group named `mycliresource` in hello `westus` location.</span></span>

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="f482c-123">Creación de un servidor de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="f482c-123">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="f482c-124">Cree una base de datos de MySQL server con servidor de mysql de hello az crear comando.</span><span class="sxs-lookup"><span data-stu-id="f482c-124">Create an Azure Database for MySQL server with hello az mysql server create command.</span></span> <span data-ttu-id="f482c-125">Un servidor puede administrar varias bases de datos.</span><span class="sxs-lookup"><span data-stu-id="f482c-125">A server can manage multiple databases.</span></span> <span data-ttu-id="f482c-126">Normalmente se usa una base de datos independiente para cada proyecto o para cada usuario.</span><span class="sxs-lookup"><span data-stu-id="f482c-126">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="f482c-127">Hello en el ejemplo siguiente se crea una base de datos de Azure para MySQL server que se encuentra en `westus` en grupo de recursos de hello `mycliresource` con nombre `mycliserver`.</span><span class="sxs-lookup"><span data-stu-id="f482c-127">hello following example creates an Azure Database for MySQL server located in `westus` in hello resource group `mycliresource` with name `mycliserver`.</span></span> <span data-ttu-id="f482c-128">servidor de Hello tiene un inicio de sesión de administrador en denominado `myadmin` y la contraseña `Password01!`.</span><span class="sxs-lookup"><span data-stu-id="f482c-128">hello server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="f482c-129">Hola servidor se crea con **básica** nivel de rendimiento y **50** unidades que se comparten entre todas las bases de datos de hello en el servidor de Hola de proceso.</span><span class="sxs-lookup"><span data-stu-id="f482c-129">hello server is created with **Basic** performance tier and **50** compute units shared between all hello databases in hello server.</span></span> <span data-ttu-id="f482c-130">Puede escalar almacenamiento y el proceso hacia arriba o hacia abajo según las necesidades de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="f482c-130">You can scale compute and storage up or down depending on hello application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="f482c-131">Configurar de la regla de firewall</span><span class="sxs-lookup"><span data-stu-id="f482c-131">Configure firewall rule</span></span>
<span data-ttu-id="f482c-132">Crear una base de datos de Azure para comando de creación de la regla de firewall de nivel de servidor de MySQL con hello az mysql server-regla de firewall.</span><span class="sxs-lookup"><span data-stu-id="f482c-132">Create an Azure Database for MySQL server-level firewall rule with hello az mysql server firewall-rule create command.</span></span> <span data-ttu-id="f482c-133">Una regla de firewall de nivel de servidor permite que una aplicación externa, como **mysql** herramienta de línea de comandos o servidor de MySQL Workbench tooconnect tooyour a través de firewall de servicio de MySQL de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="f482c-133">A server-level firewall rule allows an external application, such as **mysql** command-line tool or MySQL Workbench tooconnect tooyour server through hello Azure MySQL service firewall.</span></span> 

<span data-ttu-id="f482c-134">Hello en el ejemplo siguiente se crea una regla de firewall para un intervalo de direcciones predefinidas.</span><span class="sxs-lookup"><span data-stu-id="f482c-134">hello following example creates a firewall rule for a predefined address range.</span></span> <span data-ttu-id="f482c-135">Este ejemplo muestra hello todo posible intervalo de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="f482c-135">This example shows hello entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-hello-connection-information"></a><span data-ttu-id="f482c-136">Obtener información de conexión de Hola</span><span class="sxs-lookup"><span data-stu-id="f482c-136">Get hello connection information</span></span>

<span data-ttu-id="f482c-137">tooconnect tooyour server, necesita credenciales de acceso y la información de host de tooprovide.</span><span class="sxs-lookup"><span data-stu-id="f482c-137">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

<span data-ttu-id="f482c-138">resultado de Hello es en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="f482c-138">hello result is in JSON format.</span></span> <span data-ttu-id="f482c-139">Tome nota de hello **fullyQualifiedDomainName** y **Iniciodesesióndeadministrador**.</span><span class="sxs-lookup"><span data-stu-id="f482c-139">Make a note of hello **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
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

## <a name="connect-toohello-server-using-mysql"></a><span data-ttu-id="f482c-140">Conectar con mysql de servidor de toohello</span><span class="sxs-lookup"><span data-stu-id="f482c-140">Connect toohello server using mysql</span></span>
<span data-ttu-id="f482c-141">Use [herramienta de línea de comandos de mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish una tooyour de conexión base de datos de MySQL server.</span><span class="sxs-lookup"><span data-stu-id="f482c-141">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish a connection tooyour Azure Database for MySQL server.</span></span> <span data-ttu-id="f482c-142">En este ejemplo, el comando de hello es:</span><span class="sxs-lookup"><span data-stu-id="f482c-142">In this example, hello command is:</span></span>
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="f482c-143">Crear una base de datos en blanco</span><span class="sxs-lookup"><span data-stu-id="f482c-143">Create a blank database</span></span>
<span data-ttu-id="f482c-144">Una vez que esté conectado toohello server, cree una base de datos en blanco.</span><span class="sxs-lookup"><span data-stu-id="f482c-144">Once you’re connected toohello server, create a blank database.</span></span>
```sql
mysql> CREATE DATABASE mysampledb;
```

<span data-ttu-id="f482c-145">En el símbolo del sistema de hello, ejecute hello después de la base de datos de comando tooswitch Hola conexión toothis recién creado:</span><span class="sxs-lookup"><span data-stu-id="f482c-145">At hello prompt, run hello following command tooswitch hello connection toothis newly created database:</span></span>
```sql
mysql> USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="f482c-146">Crear tablas de base de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="f482c-146">Create tables in hello database</span></span>
<span data-ttu-id="f482c-147">Ahora que sabe cómo tooconnect toohello base de datos de Azure para la base de datos MySQL, podemos ver cómo toocomplete algunas tareas básicas.</span><span class="sxs-lookup"><span data-stu-id="f482c-147">Now that you know how tooconnect toohello Azure Database for MySQL database, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="f482c-148">En primer lugar, podemos crear una tabla y cargarla con algunos datos.</span><span class="sxs-lookup"><span data-stu-id="f482c-148">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="f482c-149">Vamos a crear una tabla que almacena la información del inventario.</span><span class="sxs-lookup"><span data-stu-id="f482c-149">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="f482c-150">Cargar datos en tablas de Hola</span><span class="sxs-lookup"><span data-stu-id="f482c-150">Load data into hello tables</span></span>
<span data-ttu-id="f482c-151">Ahora que tenemos una tabla, podemos insertar algunos datos en ella.</span><span class="sxs-lookup"><span data-stu-id="f482c-151">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="f482c-152">En la ventana de símbolo del sistema abierto hello, ejecute hello después consulta tooinsert algunas filas de datos.</span><span class="sxs-lookup"><span data-stu-id="f482c-152">At hello open command prompt window, run hello following query tooinsert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="f482c-153">Ahora tiene dos filas de datos de ejemplo en la tabla de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f482c-153">Now you have two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="f482c-154">Consultar y actualizar los datos de hello en tablas de Hola</span><span class="sxs-lookup"><span data-stu-id="f482c-154">Query and update hello data in hello tables</span></span>
<span data-ttu-id="f482c-155">Ejecute hello siguientes tooretrieve información de consulta de tabla de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f482c-155">Execute hello following query tooretrieve information from hello database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="f482c-156">También puede actualizar los datos de hello en tablas de Hola.</span><span class="sxs-lookup"><span data-stu-id="f482c-156">You can also update hello data in hello tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="f482c-157">fila de Hola se actualiza en consecuencia cuando se recuperan datos.</span><span class="sxs-lookup"><span data-stu-id="f482c-157">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="f482c-158">Restaurar un punto anterior de tooa de base de datos en el tiempo</span><span class="sxs-lookup"><span data-stu-id="f482c-158">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="f482c-159">Imagine que eliminó accidentalmente esta tabla.</span><span class="sxs-lookup"><span data-stu-id="f482c-159">Imagine you have accidentally deleted this table.</span></span> <span data-ttu-id="f482c-160">No se puede recuperar con facilidad.</span><span class="sxs-lookup"><span data-stu-id="f482c-160">This is something you cannot easily recover from.</span></span> <span data-ttu-id="f482c-161">Azure base de datos de MySQL permite toogo tooany atrás punto en el tiempo en hello última los días de too35 y restaurar este punto en el nuevo servidor de tiempo tooa.</span><span class="sxs-lookup"><span data-stu-id="f482c-161">Azure Database for MySQL allows you toogo back tooany point in time in hello last up too35 days and restore this point in time tooa new server.</span></span> <span data-ttu-id="f482c-162">Puede usar esta nueva toorecover server los datos eliminados.</span><span class="sxs-lookup"><span data-stu-id="f482c-162">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="f482c-163">Hola siguiendo los pasos restauración Hola ejemplo servidor tooa punto antes de que se ha agregado Hola tabla.</span><span class="sxs-lookup"><span data-stu-id="f482c-163">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

<span data-ttu-id="f482c-164">Para hello restauración necesita Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="f482c-164">For hello Restore you need hello following information:</span></span>

- <span data-ttu-id="f482c-165">Punto de restauración: seleccione un punto-in-time que se produce antes de hello servidor se ha modificado.</span><span class="sxs-lookup"><span data-stu-id="f482c-165">Restore point: Select a point-in-time that occurs before hello server was changed.</span></span> <span data-ttu-id="f482c-166">Debe ser mayor que o igual a value de copia de seguridad más antigua toohello origen la base de datos.</span><span class="sxs-lookup"><span data-stu-id="f482c-166">Must be greater than or equal toohello source database's Oldest backup value.</span></span>
- <span data-ttu-id="f482c-167">Servidor de destino: especifique un nuevo nombre de servidor que desee toorestore a</span><span class="sxs-lookup"><span data-stu-id="f482c-167">Target server: Provide a new server name you want toorestore to</span></span>
- <span data-ttu-id="f482c-168">Servidor de origen: proporcionar nombre Hola Hola del servidor de que desea toorestore desde</span><span class="sxs-lookup"><span data-stu-id="f482c-168">Source server: Provide hello name of hello server you want toorestore from</span></span>
- <span data-ttu-id="f482c-169">Ubicación: No se puede seleccionar una región hello, de forma predeterminada es igual que el servidor de origen de Hola</span><span class="sxs-lookup"><span data-stu-id="f482c-169">Location: You cannot select hello region, by default it is same as hello source server</span></span>

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

<span data-ttu-id="f482c-170">servidor de hello toorestore y [tooa en el momento de restaurar](./howto-restore-server-portal.md) antes de que se eliminó la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="f482c-170">toorestore hello server and [restore tooa point-in-time](./howto-restore-server-portal.md) before hello table was deleted.</span></span> <span data-ttu-id="f482c-171">Restauración tooa otro punto de servidor en el tiempo crea un duplicado en el servidor nuevo como servidor original Hola de punto de hello en el tiempo especificado, siempre que esté dentro del período de retención de Hola para su [nivel de servicio](./concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="f482c-171">Restoring a server tooa different point in time creates a duplicate new server as hello original server as of hello point in time you specify, provided that it is within hello retention period for your [service tier](./concepts-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f482c-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f482c-172">Next Steps</span></span>
<span data-ttu-id="f482c-173">En este tutorial aprendió lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f482c-173">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="f482c-174">Creación de una instancia de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="f482c-174">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="f482c-175">Configurar firewall de servidor hello</span><span class="sxs-lookup"><span data-stu-id="f482c-175">Configure hello server firewall</span></span>
> * <span data-ttu-id="f482c-176">Use [herramienta de línea de comandos de mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate una base de datos</span><span class="sxs-lookup"><span data-stu-id="f482c-176">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate a database</span></span>
> * <span data-ttu-id="f482c-177">Carga de datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f482c-177">Load sample data</span></span>
> * <span data-ttu-id="f482c-178">Datos de consulta</span><span class="sxs-lookup"><span data-stu-id="f482c-178">Query data</span></span>
> * <span data-ttu-id="f482c-179">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="f482c-179">Update data</span></span>
> * <span data-ttu-id="f482c-180">Restauración de datos</span><span class="sxs-lookup"><span data-stu-id="f482c-180">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f482c-181">Ejemplos de la CLI de Azure para Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="f482c-181">Azure Database for MySQL - Azure CLI samples</span></span>](./sample-scripts-azure-cli.md)
