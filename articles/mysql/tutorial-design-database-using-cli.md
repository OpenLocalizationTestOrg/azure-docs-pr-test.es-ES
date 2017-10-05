---
title: "Diseño de la primera base de datos de Azure Database for MySQL: CLI de Azure | Microsoft Docs"
description: "En este tutorial se explica cómo crear y administrar la base de datos y el servidor de Azure Database for MySQL con la CLI de Azure 2.0 desde la línea de comandos."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 590cba6cb58d0c0eaedb9f122ac048c33988004d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="a9215-103">Diseño de la primera base de datos de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="a9215-103">Design your first Azure Database for MySQL database</span></span>

<span data-ttu-id="a9215-104">Azure Database for MySQL es un servicio de base de datos relacional de Microsoft Cloud basado en el motor de base de datos de MySQL Community Edition.</span><span class="sxs-lookup"><span data-stu-id="a9215-104">Azure Database for MySQL is a relational database service in the Microsoft cloud based on MySQL Community Edition database engine.</span></span> <span data-ttu-id="a9215-105">En este tutorial, usa la CLI (interfaz de la línea de comandos) de Azure y otras utilidades para aprender a hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a9215-105">In this tutorial, you use Azure CLI (command-line interface) and other utilities to learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a9215-106">Creación de una instancia de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="a9215-106">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="a9215-107">Configuración del firewall del servidor</span><span class="sxs-lookup"><span data-stu-id="a9215-107">Configure the server firewall</span></span>
> * <span data-ttu-id="a9215-108">Uso de la [herramienta de línea de comandos de mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) para crear una base de datos</span><span class="sxs-lookup"><span data-stu-id="a9215-108">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to create a database</span></span>
> * <span data-ttu-id="a9215-109">Carga de datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a9215-109">Load sample data</span></span>
> * <span data-ttu-id="a9215-110">Datos de consulta</span><span class="sxs-lookup"><span data-stu-id="a9215-110">Query data</span></span>
> * <span data-ttu-id="a9215-111">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="a9215-111">Update data</span></span>
> * <span data-ttu-id="a9215-112">Restauración de datos</span><span class="sxs-lookup"><span data-stu-id="a9215-112">Restore data</span></span>

<span data-ttu-id="a9215-113">Puede usar Azure Cloud Shell en el explorador, o bien [instalar la CLI de Azure 2.0]( /cli/azure/install-azure-cli) en su propio equipo para ejecutar los bloques de código de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="a9215-113">You may use the Azure Cloud Shell in the browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer to run the code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a9215-114">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="a9215-114">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a9215-115">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="a9215-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="a9215-116">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a9215-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="a9215-117">Si tiene varias suscripciones, elija la adecuada donde se encuentre el recurso o para la cual se facture.</span><span class="sxs-lookup"><span data-stu-id="a9215-117">If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span></span> <span data-ttu-id="a9215-118">Seleccione un identificador de suscripción específico en su cuenta mediante el comando [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="a9215-118">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="a9215-119">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="a9215-119">Create a resource group</span></span>
<span data-ttu-id="a9215-120">Cree un [grupo de recursos](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) con el comando [az group create](https://docs.microsoft.com/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="a9215-120">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) with [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="a9215-121">Un grupo de recursos es un contenedor lógico en el que se implementan y se administran recursos de Azure como un grupo.</span><span class="sxs-lookup"><span data-stu-id="a9215-121">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="a9215-122">En el ejemplo siguiente, se crea un grupo de recursos denominado `mycliresource` en la ubicación `westus`.</span><span class="sxs-lookup"><span data-stu-id="a9215-122">The following example creates a resource group named `mycliresource` in the `westus` location.</span></span>

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="a9215-123">Creación de un servidor de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="a9215-123">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="a9215-124">Cree un servidor de Azure Database for MySQL con el comando az mysql server create.</span><span class="sxs-lookup"><span data-stu-id="a9215-124">Create an Azure Database for MySQL server with the az mysql server create command.</span></span> <span data-ttu-id="a9215-125">Un servidor puede administrar varias bases de datos.</span><span class="sxs-lookup"><span data-stu-id="a9215-125">A server can manage multiple databases.</span></span> <span data-ttu-id="a9215-126">Normalmente se usa una base de datos independiente para cada proyecto o para cada usuario.</span><span class="sxs-lookup"><span data-stu-id="a9215-126">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="a9215-127">En el ejemplo siguiente se crea una Base de datos de Azure para el servidor MySQL situado en `westus` en el grupo de recursos `mycliresource` con el nombre `mycliserver`.</span><span class="sxs-lookup"><span data-stu-id="a9215-127">The following example creates an Azure Database for MySQL server located in `westus` in the resource group `mycliresource` with name `mycliserver`.</span></span> <span data-ttu-id="a9215-128">El servidor tiene un inicio de sesión de administrador con el nombre `myadmin` y la contraseña `Password01!`.</span><span class="sxs-lookup"><span data-stu-id="a9215-128">The server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="a9215-129">El servidor se crea con un nivel de rendimiento **Básico** y **50** unidades de proceso compartidas entre todas las bases de datos en el servidor.</span><span class="sxs-lookup"><span data-stu-id="a9215-129">The server is created with **Basic** performance tier and **50** compute units shared between all the databases in the server.</span></span> <span data-ttu-id="a9215-130">Puede escalar o reducir verticalmente el proceso y el almacenamiento según las necesidades de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a9215-130">You can scale compute and storage up or down depending on the application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="a9215-131">Configurar de la regla de firewall</span><span class="sxs-lookup"><span data-stu-id="a9215-131">Configure firewall rule</span></span>
<span data-ttu-id="a9215-132">Cree una regla de firewall de nivel de servidor de Azure Database for MySQL con el comando az mysql server firewall-rule create.</span><span class="sxs-lookup"><span data-stu-id="a9215-132">Create an Azure Database for MySQL server-level firewall rule with the az mysql server firewall-rule create command.</span></span> <span data-ttu-id="a9215-133">Una regla de firewall de nivel de servidor permite que una aplicación externa, como una herramienta de línea de comandos de **mysql** o MySQL Workbench para conectarse al servidor a través del firewall del servicio Azure MySQL.</span><span class="sxs-lookup"><span data-stu-id="a9215-133">A server-level firewall rule allows an external application, such as **mysql** command-line tool or MySQL Workbench to connect to your server through the Azure MySQL service firewall.</span></span> 

<span data-ttu-id="a9215-134">En el ejemplo siguiente se crea una regla de firewall para un intervalo predefinido de direcciones.</span><span class="sxs-lookup"><span data-stu-id="a9215-134">The following example creates a firewall rule for a predefined address range.</span></span> <span data-ttu-id="a9215-135">En este ejemplo se muestra todo el posible intervalo de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="a9215-135">This example shows the entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-the-connection-information"></a><span data-ttu-id="a9215-136">Obtención de la información de conexión</span><span class="sxs-lookup"><span data-stu-id="a9215-136">Get the connection information</span></span>

<span data-ttu-id="a9215-137">Para conectarse al servidor, debe proporcionar las credenciales de acceso y la información del host.</span><span class="sxs-lookup"><span data-stu-id="a9215-137">To connect to your server, you need to provide host information and access credentials.</span></span>
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

<span data-ttu-id="a9215-138">El resultado está en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="a9215-138">The result is in JSON format.</span></span> <span data-ttu-id="a9215-139">Tome nota de los valores de **fullyQualifiedDomainName** y **administratorLogin**.</span><span class="sxs-lookup"><span data-stu-id="a9215-139">Make a note of the **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
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

## <a name="connect-to-the-server-using-mysql"></a><span data-ttu-id="a9215-140">Conexión al servidor con MySQL</span><span class="sxs-lookup"><span data-stu-id="a9215-140">Connect to the server using mysql</span></span>
<span data-ttu-id="a9215-141">Use la [herramienta de línea de comandos mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) para establecer una conexión con el servidor de Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="a9215-141">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to establish a connection to your Azure Database for MySQL server.</span></span> <span data-ttu-id="a9215-142">En este ejemplo, el comando es:</span><span class="sxs-lookup"><span data-stu-id="a9215-142">In this example, the command is:</span></span>
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="a9215-143">Crear una base de datos en blanco</span><span class="sxs-lookup"><span data-stu-id="a9215-143">Create a blank database</span></span>
<span data-ttu-id="a9215-144">Una vez conectado al servidor, cree una base de datos vacía.</span><span class="sxs-lookup"><span data-stu-id="a9215-144">Once you’re connected to the server, create a blank database.</span></span>
```sql
mysql> CREATE DATABASE mysampledb;
```

<span data-ttu-id="a9215-145">En el símbolo del sistema, ejecute el comando siguiente para cambiar la conexión a esta base de datos recién creada:</span><span class="sxs-lookup"><span data-stu-id="a9215-145">At the prompt, run the following command to switch the connection to this newly created database:</span></span>
```sql
mysql> USE mysampledb;
```

## <a name="create-tables-in-the-database"></a><span data-ttu-id="a9215-146">Creación de tablas en la base de datos</span><span class="sxs-lookup"><span data-stu-id="a9215-146">Create tables in the database</span></span>
<span data-ttu-id="a9215-147">Ahora que sabe cómo conectarse a la base de datos de Azure Database for MySQL, podemos ver cómo completar algunas tareas básicas.</span><span class="sxs-lookup"><span data-stu-id="a9215-147">Now that you know how to connect to the Azure Database for MySQL database, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="a9215-148">En primer lugar, podemos crear una tabla y cargarla con algunos datos.</span><span class="sxs-lookup"><span data-stu-id="a9215-148">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="a9215-149">Vamos a crear una tabla que almacena la información del inventario.</span><span class="sxs-lookup"><span data-stu-id="a9215-149">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="a9215-150">Carga de datos en las tablas</span><span class="sxs-lookup"><span data-stu-id="a9215-150">Load data into the tables</span></span>
<span data-ttu-id="a9215-151">Ahora que tenemos una tabla, podemos insertar algunos datos en ella.</span><span class="sxs-lookup"><span data-stu-id="a9215-151">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="a9215-152">En la ventana de símbolo del sistema abierta, ejecute la consulta siguiente para insertar algunas filas de datos.</span><span class="sxs-lookup"><span data-stu-id="a9215-152">At the open command prompt window, run the following query to insert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="a9215-153">Ahora tiene dos filas de datos de ejemplo en la tabla que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a9215-153">Now you have two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="a9215-154">Consulta y actualización de los datos en las tablas</span><span class="sxs-lookup"><span data-stu-id="a9215-154">Query and update the data in the tables</span></span>
<span data-ttu-id="a9215-155">Ejecute la consulta siguiente para recuperar información de la tabla de base de datos.</span><span class="sxs-lookup"><span data-stu-id="a9215-155">Execute the following query to retrieve information from the database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="a9215-156">También puede actualizar los datos en las tablas.</span><span class="sxs-lookup"><span data-stu-id="a9215-156">You can also update the data in the tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="a9215-157">La fila se actualiza en consecuencia cuando se recuperan los datos.</span><span class="sxs-lookup"><span data-stu-id="a9215-157">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="a9215-158">Restauración de una base de datos a un momento anterior en el tiempo</span><span class="sxs-lookup"><span data-stu-id="a9215-158">Restore a database to a previous point in time</span></span>
<span data-ttu-id="a9215-159">Imagine que eliminó accidentalmente esta tabla.</span><span class="sxs-lookup"><span data-stu-id="a9215-159">Imagine you have accidentally deleted this table.</span></span> <span data-ttu-id="a9215-160">No se puede recuperar con facilidad.</span><span class="sxs-lookup"><span data-stu-id="a9215-160">This is something you cannot easily recover from.</span></span> <span data-ttu-id="a9215-161">Azure Database for MySQL permite volver a cualquier momento dado en el período de los últimos 35 días y restaurar este momento en un servidor nuevo.</span><span class="sxs-lookup"><span data-stu-id="a9215-161">Azure Database for MySQL allows you to go back to any point in time in the last up to 35 days and restore this point in time to a new server.</span></span> <span data-ttu-id="a9215-162">Puede usar este servidor nuevo para recuperar los datos eliminados.</span><span class="sxs-lookup"><span data-stu-id="a9215-162">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="a9215-163">Los pasos siguientes restauran el servidor de ejemplo a un punto antes de que se agregara la tabla.</span><span class="sxs-lookup"><span data-stu-id="a9215-163">The following steps restore the sample server to a point before the table was added.</span></span>

<span data-ttu-id="a9215-164">Para realizar la restauración, necesita la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="a9215-164">For the Restore you need the following information:</span></span>

- <span data-ttu-id="a9215-165">Punto de restauración: seleccione el momento antes de que se modificara la base de datos.</span><span class="sxs-lookup"><span data-stu-id="a9215-165">Restore point: Select a point-in-time that occurs before the server was changed.</span></span> <span data-ttu-id="a9215-166">Debe ser mayor o igual que el valor de la copia de seguridad más antigua de la base de datos de origen.</span><span class="sxs-lookup"><span data-stu-id="a9215-166">Must be greater than or equal to the source database's Oldest backup value.</span></span>
- <span data-ttu-id="a9215-167">Servidor de destino: especifique el nombre del nuevo servidor donde desea restaurar</span><span class="sxs-lookup"><span data-stu-id="a9215-167">Target server: Provide a new server name you want to restore to</span></span>
- <span data-ttu-id="a9215-168">Servidor de origen: especifique el nombre del servidor desde donde desea restaurar</span><span class="sxs-lookup"><span data-stu-id="a9215-168">Source server: Provide the name of the server you want to restore from</span></span>
- <span data-ttu-id="a9215-169">Ubicación: no se puede seleccionar la región; de forma predeterminada, es la misma que la del servidor de origen</span><span class="sxs-lookup"><span data-stu-id="a9215-169">Location: You cannot select the region, by default it is same as the source server</span></span>

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

<span data-ttu-id="a9215-170">Para restaurar el servidor y [restaurar a un momento dado](./howto-restore-server-portal.md) antes de que se eliminara la tabla.</span><span class="sxs-lookup"><span data-stu-id="a9215-170">To restore the server and [restore to a point-in-time](./howto-restore-server-portal.md) before the table was deleted.</span></span> <span data-ttu-id="a9215-171">Restaurar un servidor a un momento dado distinto crea un servidor nuevo duplicado como el servidor original a partir del momento dado que especifique, siempre que se encuentren dentro del período de retención para el [nivel de servicio](./concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="a9215-171">Restoring a server to a different point in time creates a duplicate new server as the original server as of the point in time you specify, provided that it is within the retention period for your [service tier](./concepts-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9215-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a9215-172">Next Steps</span></span>
<span data-ttu-id="a9215-173">En este tutorial aprendió lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a9215-173">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="a9215-174">Creación de una instancia de Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="a9215-174">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="a9215-175">Configuración del firewall del servidor</span><span class="sxs-lookup"><span data-stu-id="a9215-175">Configure the server firewall</span></span>
> * <span data-ttu-id="a9215-176">Uso de la [herramienta de línea de comandos de mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) para crear una base de datos</span><span class="sxs-lookup"><span data-stu-id="a9215-176">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to create a database</span></span>
> * <span data-ttu-id="a9215-177">Carga de datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a9215-177">Load sample data</span></span>
> * <span data-ttu-id="a9215-178">Datos de consulta</span><span class="sxs-lookup"><span data-stu-id="a9215-178">Query data</span></span>
> * <span data-ttu-id="a9215-179">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="a9215-179">Update data</span></span>
> * <span data-ttu-id="a9215-180">Restauración de datos</span><span class="sxs-lookup"><span data-stu-id="a9215-180">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a9215-181">Ejemplos de la CLI de Azure para Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="a9215-181">Azure Database for MySQL - Azure CLI samples</span></span>](./sample-scripts-azure-cli.md)
