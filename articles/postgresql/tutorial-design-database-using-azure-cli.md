---
title: "Diseño de la primera base de datos de Azure Database for PostgreSQL con la CLI de Azure | Microsoft Docs"
description: "En este tutorial se muestra cómo diseñar la primera base de datos de Azure Database for PostgreSQL con la CLI de Azure."
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
ms.openlocfilehash: cf536fce8925f9173b541b845af25a8d8c38eabd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-azure-cli"></a><span data-ttu-id="eca71-103">Diseño de la primera base de datos de Azure Database for PostgreSQL con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="eca71-103">Design your first Azure Database for PostgreSQL using Azure CLI</span></span> 
<span data-ttu-id="eca71-104">En este tutorial, usa la CLI (interfaz de la línea de comandos) de Azure y otras utilidades para aprender a hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="eca71-104">In this tutorial, you use Azure CLI (command-line interface) and other utilities to learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="eca71-105">Creación de una base de datos de Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="eca71-105">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="eca71-106">Configuración del firewall del servidor</span><span class="sxs-lookup"><span data-stu-id="eca71-106">Configure the server firewall</span></span>
> * <span data-ttu-id="eca71-107">Uso de la utilidad [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) para crear una base de datos</span><span class="sxs-lookup"><span data-stu-id="eca71-107">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility to create a database</span></span>
> * <span data-ttu-id="eca71-108">Carga de datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="eca71-108">Load sample data</span></span>
> * <span data-ttu-id="eca71-109">Datos de consulta</span><span class="sxs-lookup"><span data-stu-id="eca71-109">Query data</span></span>
> * <span data-ttu-id="eca71-110">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="eca71-110">Update data</span></span>
> * <span data-ttu-id="eca71-111">Restauración de datos</span><span class="sxs-lookup"><span data-stu-id="eca71-111">Restore data</span></span>

<span data-ttu-id="eca71-112">Puede usar Azure Cloud Shell en el explorador, o bien [instalar la CLI de Azure 2.0]( /cli/azure/install-azure-cli) en su propio equipo para ejecutar los bloques de código de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="eca71-112">You may use the Azure Cloud Shell in the browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer to run the code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="eca71-113">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="eca71-113">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="eca71-114">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="eca71-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="eca71-115">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="eca71-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="eca71-116">Si tiene varias suscripciones, elija la adecuada donde se encuentre el recurso o para la cual se facture.</span><span class="sxs-lookup"><span data-stu-id="eca71-116">If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span></span> <span data-ttu-id="eca71-117">Seleccione un identificador de suscripción específico en su cuenta mediante el comando [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="eca71-117">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="eca71-118">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="eca71-118">Create a resource group</span></span>
<span data-ttu-id="eca71-119">Cree un [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md) con el comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="eca71-119">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="eca71-120">Un grupo de recursos es un contenedor lógico en el que se implementan y se administran recursos de Azure como un grupo.</span><span class="sxs-lookup"><span data-stu-id="eca71-120">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="eca71-121">En el ejemplo siguiente, se crea un grupo de recursos denominado `myresourcegroup` en la ubicación `westus`.</span><span class="sxs-lookup"><span data-stu-id="eca71-121">The following example creates a resource group named `myresourcegroup` in the `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="eca71-122">Creación de un servidor de Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="eca71-122">Create an Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="eca71-123">Cree un [servidor de Azure Database for PostgreSQL](overview.md) con el comando [az postgres server create](/cli/azure/postgres/server#create).</span><span class="sxs-lookup"><span data-stu-id="eca71-123">Create an [Azure Database for PostgreSQL server](overview.md) using the [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="eca71-124">Un servidor contiene un conjunto de bases de datos administradas como un grupo.</span><span class="sxs-lookup"><span data-stu-id="eca71-124">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="eca71-125">En el ejemplo siguiente se crea un servidor denominado `mypgserver-20170401` en el grupo de recursos `myresourcegroup` con el inicio de sesión de administrador de servidor `mylogin`.</span><span class="sxs-lookup"><span data-stu-id="eca71-125">The following example creates a server called `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="eca71-126">El nombre de un servidor se asigna al nombre DNS y, por tanto, debe ser único a nivel global en Azure.</span><span class="sxs-lookup"><span data-stu-id="eca71-126">Name of a server maps to DNS name and is thus required to be globally unique in Azure.</span></span> <span data-ttu-id="eca71-127">Sustituya `<server_admin_password>` por su propio valor.</span><span class="sxs-lookup"><span data-stu-id="eca71-127">Substitute the `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401 --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="eca71-128">Se requiere el inicio de sesión y la contraseña de administrador de servidor que especifique aquí para iniciar sesión en el servidor y a sus bases de datos más adelante en esta guía de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="eca71-128">The server admin login and password that you specify here are required to log in to the server and its databases later in this quick start.</span></span> <span data-ttu-id="eca71-129">Recuerde o grabe esta información para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="eca71-129">Remember or record this information for later use.</span></span>

<span data-ttu-id="eca71-130">De forma predeterminada, la base de datos de **postgres** se crea en el servidor.</span><span class="sxs-lookup"><span data-stu-id="eca71-130">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="eca71-131">La base de datos [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) es una base de datos predeterminada pensada para que la usen los usuarios, las utilidades y aplicaciones de otros fabricantes.</span><span class="sxs-lookup"><span data-stu-id="eca71-131">The [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="eca71-132">Configuración de una regla de firewall de nivel de servidor</span><span class="sxs-lookup"><span data-stu-id="eca71-132">Configure a server-level firewall rule</span></span>

<span data-ttu-id="eca71-133">Cree una regla de firewall de nivel de servidor de Azure PostgreSQL con el comando [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create).</span><span class="sxs-lookup"><span data-stu-id="eca71-133">Create an Azure PostgreSQL server-level firewall rule with the [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="eca71-134">Una regla de firewall de nivel de servidor permite que una aplicación externa, como [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) o [PgAdmin](https://www.pgadmin.org/), se conecte al servidor a través del firewall del servicio Azure PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="eca71-134">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) to connect to your server through the Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="eca71-135">Puede establecer una regla de firewall que abarque un intervalo de IP para poder conectarse desde la red.</span><span class="sxs-lookup"><span data-stu-id="eca71-135">You can set a firewall rule that covers an IP range to be able to connect from your network.</span></span> <span data-ttu-id="eca71-136">En el ejemplo siguiente se usa [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) para crear una regla de firewall `AllowAllIps` para un intervalo de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="eca71-136">The following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) to create a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="eca71-137">Para abrir todas las direcciones IP, utilice 0.0.0.0 como la dirección IP inicial y 255.255.255.255 como la dirección final.</span><span class="sxs-lookup"><span data-stu-id="eca71-137">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="eca71-138">El servidor Azure PostgreSQL se comunica a través de puerto 5432.</span><span class="sxs-lookup"><span data-stu-id="eca71-138">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="eca71-139">Al conectarse desde una red corporativa, es posible que el firewall de la red no permita el tráfico saliente a través del puerto 5432.</span><span class="sxs-lookup"><span data-stu-id="eca71-139">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="eca71-140">Haga que el departamento de TI abra el puerto 5432 para conectarse al servidor de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="eca71-140">Have your IT department open port 5432 to connect to your Azure SQL Database server.</span></span>
>

## <a name="get-the-connection-information"></a><span data-ttu-id="eca71-141">Obtención de la información de conexión</span><span class="sxs-lookup"><span data-stu-id="eca71-141">Get the connection information</span></span>

<span data-ttu-id="eca71-142">Para conectarse al servidor, debe proporcionar las credenciales de acceso y la información del host.</span><span class="sxs-lookup"><span data-stu-id="eca71-142">To connect to your server, you need to provide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="eca71-143">El resultado está en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="eca71-143">The result is in JSON format.</span></span> <span data-ttu-id="eca71-144">Tome nota de los valores de **administratorLogin** y **fullyQualifiedDomainName**.</span><span class="sxs-lookup"><span data-stu-id="eca71-144">Make a note of the **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
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

## <a name="connect-to-azure-database-for-postgresql-database-using-psql"></a><span data-ttu-id="eca71-145">Conexión a la base de datos de Azure Database for PostgreSQL mediante psql</span><span class="sxs-lookup"><span data-stu-id="eca71-145">Connect to Azure Database for PostgreSQL database using psql</span></span>
<span data-ttu-id="eca71-146">Si el equipo cliente tiene PostgreSQL instalado, puede usar una instancia local de [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) o usar la consola de Azure Cloud para conectarse a un servidor Azure PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="eca71-146">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), or the Azure Cloud Console to connect to an Azure PostgreSQL server.</span></span> <span data-ttu-id="eca71-147">Ahora vamos a usar la utilidad de línea de comandos psql para conectarnos al servidor de Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="eca71-147">Let's now use the psql command-line utility to connect to the Azure Database for PostgreSQL server.</span></span>

1. <span data-ttu-id="eca71-148">Ejecute el comando psql siguiente para conectarse a un servidor de Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="eca71-148">Run the following psql command to connect to an Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="eca71-149">Por ejemplo, el siguiente comando se conecta a la base de datos predeterminada denominada **postgres** en el servidor PostgreSQL **mypgserver-20170401.postgres.database.azure.com** con las credenciales de acceso.</span><span class="sxs-lookup"><span data-stu-id="eca71-149">For example, the following command connects to the default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="eca71-150">Escriba el valor de `<server_admin_password>` que eligió cuando se le solicitó una contraseña.</span><span class="sxs-lookup"><span data-stu-id="eca71-150">Enter the `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 ---dbname=postgres
```

2.  <span data-ttu-id="eca71-151">Una vez conectado al servidor, cree una base de datos vacía en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="eca71-151">Once you are connected to the server, create a blank database at the prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="eca71-152">En el símbolo del sistema, ejecute el siguiente comando para cambiar la conexión a la base de datos **mypgsqldb** recién creada:</span><span class="sxs-lookup"><span data-stu-id="eca71-152">At the prompt, execute the following command to switch connection to the newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="create-tables-in-the-database"></a><span data-ttu-id="eca71-153">Creación de tablas en la base de datos</span><span class="sxs-lookup"><span data-stu-id="eca71-153">Create tables in the database</span></span>
<span data-ttu-id="eca71-154">Ahora que sabe cómo conectarse a Azure Database for PostgreSQL, podemos ver cómo completar algunas tareas básicas.</span><span class="sxs-lookup"><span data-stu-id="eca71-154">Now that you know how to connect to the Azure Database for PostgreSQL, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="eca71-155">En primer lugar, podemos crear una tabla y cargarla con algunos datos.</span><span class="sxs-lookup"><span data-stu-id="eca71-155">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="eca71-156">Vamos a crear una tabla que hace el seguimiento de información del inventario.</span><span class="sxs-lookup"><span data-stu-id="eca71-156">Let's create a table that tracks inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

<span data-ttu-id="eca71-157">Puede ver la tabla recién creada ahora en la lista de tablas si escribe lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="eca71-157">You can see the newly created table in the list of tables now by typing:</span></span>
```sql
\dt
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="eca71-158">Carga de datos en las tablas</span><span class="sxs-lookup"><span data-stu-id="eca71-158">Load data into the tables</span></span>
<span data-ttu-id="eca71-159">Ahora que tenemos una tabla, podemos insertar algunos datos en ella.</span><span class="sxs-lookup"><span data-stu-id="eca71-159">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="eca71-160">En la ventana de símbolo del sistema abierta, ejecute la consulta siguiente para insertar algunas filas de datos</span><span class="sxs-lookup"><span data-stu-id="eca71-160">At the open command prompt window, run the following query to insert some rows of data</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="eca71-161">Ahora tiene dos filas de datos de ejemplo en la tabla que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="eca71-161">You have now two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="eca71-162">Consulta y actualización de los datos en las tablas</span><span class="sxs-lookup"><span data-stu-id="eca71-162">Query and update the data in the tables</span></span>
<span data-ttu-id="eca71-163">Ejecute la consulta siguiente para recuperar información de la tabla de base de datos.</span><span class="sxs-lookup"><span data-stu-id="eca71-163">Execute the following query to retrieve information from the database table.</span></span> 
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="eca71-164">También puede actualizar los datos en las tablas</span><span class="sxs-lookup"><span data-stu-id="eca71-164">You can also update the data in the tables</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="eca71-165">La fila se actualiza en consecuencia cuando se recuperan los datos.</span><span class="sxs-lookup"><span data-stu-id="eca71-165">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="eca71-166">Restauración de una base de datos a un momento anterior en el tiempo</span><span class="sxs-lookup"><span data-stu-id="eca71-166">Restore a database to a previous point in time</span></span>
<span data-ttu-id="eca71-167">Imagine que ha eliminado accidentalmente una tabla.</span><span class="sxs-lookup"><span data-stu-id="eca71-167">Imagine you have accidentally deleted a table.</span></span> <span data-ttu-id="eca71-168">No se puede recuperar con facilidad.</span><span class="sxs-lookup"><span data-stu-id="eca71-168">This is something you cannot easily recover from.</span></span> <span data-ttu-id="eca71-169">Azure Database for PostgreSQL permite volver a cualquier momento dado en el período de los últimos 7 días (Básico) y los últimos 35 días (Estándar) y restaurar este momento dado en un servidor nuevo.</span><span class="sxs-lookup"><span data-stu-id="eca71-169">Azure Database for PostgreSQL allows you to go back to any point-in-time (in the last up to 7 days (Basic) and 35 days (Standard)) and restore this point-in-time to a new server.</span></span> <span data-ttu-id="eca71-170">Puede usar este servidor nuevo para recuperar los datos eliminados.</span><span class="sxs-lookup"><span data-stu-id="eca71-170">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="eca71-171">Los pasos siguientes restauran el servidor de ejemplo a un punto antes de que se agregara la tabla.</span><span class="sxs-lookup"><span data-stu-id="eca71-171">The following steps restore the sample server to a point before the table was added.</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="eca71-172">El comando `az postgres server restore` necesita los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="eca71-172">The `az postgres server restore` command needs the following parameters:</span></span>
| <span data-ttu-id="eca71-173">Configuración</span><span class="sxs-lookup"><span data-stu-id="eca71-173">Setting</span></span> | <span data-ttu-id="eca71-174">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="eca71-174">Suggested value</span></span> | <span data-ttu-id="eca71-175">Descripción</span><span class="sxs-lookup"><span data-stu-id="eca71-175">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="eca71-176">--resource-group</span><span class="sxs-lookup"><span data-stu-id="eca71-176">--resource-group</span></span> |  <span data-ttu-id="eca71-177">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="eca71-177">myResourceGroup</span></span> |  <span data-ttu-id="eca71-178">Grupo de recursos en el que existe el servidor de origen.</span><span class="sxs-lookup"><span data-stu-id="eca71-178">The resource group in which the source server exists.</span></span>  |
| <span data-ttu-id="eca71-179">--name</span><span class="sxs-lookup"><span data-stu-id="eca71-179">--name</span></span> | <span data-ttu-id="eca71-180">mypgserver-restored</span><span class="sxs-lookup"><span data-stu-id="eca71-180">mypgserver-restored</span></span> | <span data-ttu-id="eca71-181">Nombre del nuevo servidor que se crea mediante el comando de restauración.</span><span class="sxs-lookup"><span data-stu-id="eca71-181">The name of the new server that is created by the restore command.</span></span> |
| <span data-ttu-id="eca71-182">restore-point-in-time</span><span class="sxs-lookup"><span data-stu-id="eca71-182">restore-point-in-time</span></span> | <span data-ttu-id="eca71-183">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="eca71-183">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="eca71-184">Seleccione un momento dado en el que quiere restaurar.</span><span class="sxs-lookup"><span data-stu-id="eca71-184">Select a point-in-time to restore to.</span></span> <span data-ttu-id="eca71-185">Esta fecha y hora debe estar dentro del período de retención de copia de seguridad del servidor de origen.</span><span class="sxs-lookup"><span data-stu-id="eca71-185">This date and time must be within the source server's backup retention period.</span></span> <span data-ttu-id="eca71-186">Use el formato de fecha y hora ISO8601.</span><span class="sxs-lookup"><span data-stu-id="eca71-186">Use ISO8601 date and time format.</span></span> <span data-ttu-id="eca71-187">Por ejemplo, puede usar su propia zona horaria local, como `2017-04-13T05:59:00-08:00`, o usar el formato de hora Zulú UTC `2017-04-13T13:59:00Z`.</span><span class="sxs-lookup"><span data-stu-id="eca71-187">For example, you may use your own local timezone, such as `2017-04-13T05:59:00-08:00`, or use UTC Zulu format `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="eca71-188">--source-server</span><span class="sxs-lookup"><span data-stu-id="eca71-188">--source-server</span></span> | <span data-ttu-id="eca71-189">mypgserver-20170401</span><span class="sxs-lookup"><span data-stu-id="eca71-189">mypgserver-20170401</span></span> | <span data-ttu-id="eca71-190">Nombre o identificador del servidor de origen desde el que se va a restaurar.</span><span class="sxs-lookup"><span data-stu-id="eca71-190">The name or ID of the source server to restore from.</span></span> |

<span data-ttu-id="eca71-191">Al restaurar un servidor a un momento dado, se crea un servidor y se copia el servidor original a un momento dado que especifique.</span><span class="sxs-lookup"><span data-stu-id="eca71-191">Restoring a server to a point-in-time creates a new server, copying as the original server as of the point in time you specify.</span></span> <span data-ttu-id="eca71-192">Los valores de ubicación y plan de tarifa del servidor restaurado son los mismos que los del servidor de origen.</span><span class="sxs-lookup"><span data-stu-id="eca71-192">The location and pricing tier values for the restored server are the same as the source server.</span></span>

<span data-ttu-id="eca71-193">El comando es sincrónico y se devolverá después de que se haya restaurado el servidor.</span><span class="sxs-lookup"><span data-stu-id="eca71-193">The command is synchronous, and will return after the server is restored.</span></span> <span data-ttu-id="eca71-194">Una vez finalizada la restauración, busque el servidor que ha creado.</span><span class="sxs-lookup"><span data-stu-id="eca71-194">Once the restore finishes, locate the new server that was created.</span></span> <span data-ttu-id="eca71-195">Compruebe que los datos se han restaurado del modo esperado.</span><span class="sxs-lookup"><span data-stu-id="eca71-195">Verify the data was restored as expected.</span></span>


## <a name="next-steps"></a><span data-ttu-id="eca71-196">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="eca71-196">Next steps</span></span>
<span data-ttu-id="eca71-197">En este tutorial, aprendió a usar la CLI (interfaz de la línea de comandos) de Azure y otras utilidades para hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="eca71-197">In this tutorial, you learned how to use Azure CLI (command-line interface) and other utilities to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="eca71-198">Creación de una base de datos de Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="eca71-198">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="eca71-199">Configuración del firewall del servidor</span><span class="sxs-lookup"><span data-stu-id="eca71-199">Configure the server firewall</span></span>
> * <span data-ttu-id="eca71-200">Uso de la utilidad [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) para crear una base de datos</span><span class="sxs-lookup"><span data-stu-id="eca71-200">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility to create a database</span></span>
> * <span data-ttu-id="eca71-201">Carga de datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="eca71-201">Load sample data</span></span>
> * <span data-ttu-id="eca71-202">Datos de consulta</span><span class="sxs-lookup"><span data-stu-id="eca71-202">Query data</span></span>
> * <span data-ttu-id="eca71-203">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="eca71-203">Update data</span></span>
> * <span data-ttu-id="eca71-204">Restauración de datos</span><span class="sxs-lookup"><span data-stu-id="eca71-204">Restore data</span></span>

<span data-ttu-id="eca71-205">A continuación, obtenga información sobre cómo usar Azure Portal para hacer tareas simulares en el tutorial [Diseño de la primera base de datos de Azure Database for PostgreSQL con Azure Portal](tutorial-design-database-using-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="eca71-205">Next, learn how to use the Azure portal to do similar tasks, review this tutorial: [Design your first Azure Database for PostgreSQL using the Azure portal](tutorial-design-database-using-azure-portal.md)</span></span>
