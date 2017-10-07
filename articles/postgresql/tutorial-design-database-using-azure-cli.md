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
# <a name="design-your-first-azure-database-for-postgresql-using-azure-cli"></a><span data-ttu-id="2f364-103">Diseño de la primera base de datos de Azure Database for PostgreSQL con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="2f364-103">Design your first Azure Database for PostgreSQL using Azure CLI</span></span> 
<span data-ttu-id="2f364-104">En este tutorial, usará Azure CLI (interfaz de línea de comandos) y otra utilidades toolearn cómo para:</span><span class="sxs-lookup"><span data-stu-id="2f364-104">In this tutorial, you use Azure CLI (command-line interface) and other utilities toolearn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="2f364-105">Creación de una instancia de Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="2f364-105">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="2f364-106">Configurar firewall de servidor hello</span><span class="sxs-lookup"><span data-stu-id="2f364-106">Configure hello server firewall</span></span>
> * <span data-ttu-id="2f364-107">Use [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) utilidad toocreate una base de datos</span><span class="sxs-lookup"><span data-stu-id="2f364-107">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility toocreate a database</span></span>
> * <span data-ttu-id="2f364-108">Carga de datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2f364-108">Load sample data</span></span>
> * <span data-ttu-id="2f364-109">Datos de consulta</span><span class="sxs-lookup"><span data-stu-id="2f364-109">Query data</span></span>
> * <span data-ttu-id="2f364-110">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="2f364-110">Update data</span></span>
> * <span data-ttu-id="2f364-111">Restauración de datos</span><span class="sxs-lookup"><span data-stu-id="2f364-111">Restore data</span></span>

<span data-ttu-id="2f364-112">Puede usar hello Shell en la nube de Azure en el Explorador de hello, o [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli) en sus propios bloques de código de equipo toorun hello en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="2f364-112">You may use hello Azure Cloud Shell in hello browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer toorun hello code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2f364-113">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="2f364-113">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="2f364-114">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f364-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="2f364-115">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2f364-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="2f364-116">Si tiene varias suscripciones, elija Hola de suscripción adecuado en el que recurso de hello existe o se factura para.</span><span class="sxs-lookup"><span data-stu-id="2f364-116">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="2f364-117">Seleccione un identificador de suscripción específico en su cuenta mediante el comando [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="2f364-117">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="2f364-118">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="2f364-118">Create a resource group</span></span>
<span data-ttu-id="2f364-119">Crear un [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md) con hello [crear grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="2f364-119">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="2f364-120">Un grupo de recursos es un contenedor lógico en el que se implementan y se administran recursos de Azure como un grupo.</span><span class="sxs-lookup"><span data-stu-id="2f364-120">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="2f364-121">Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myresourcegroup` en hello `westus` ubicación.</span><span class="sxs-lookup"><span data-stu-id="2f364-121">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="2f364-122">Creación de un servidor de Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="2f364-122">Create an Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="2f364-123">Crear un [base de datos de Azure para PostgreSQL server](overview.md) con hello [az postgres servidor crear](/cli/azure/postgres/server#create) comando.</span><span class="sxs-lookup"><span data-stu-id="2f364-123">Create an [Azure Database for PostgreSQL server](overview.md) using hello [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="2f364-124">Un servidor contiene un conjunto de bases de datos administradas como un grupo.</span><span class="sxs-lookup"><span data-stu-id="2f364-124">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="2f364-125">Hello en el ejemplo siguiente se crea un servidor denominado `mypgserver-20170401` en el grupo de recursos `myresourcegroup` con inicio de sesión de administrador de servidor `mylogin`.</span><span class="sxs-lookup"><span data-stu-id="2f364-125">hello following example creates a server called `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="2f364-126">Nombre de un servidor asigna nombre tooDNS y, por tanto, es necesario toobe globalmente único en Azure.</span><span class="sxs-lookup"><span data-stu-id="2f364-126">Name of a server maps tooDNS name and is thus required toobe globally unique in Azure.</span></span> <span data-ttu-id="2f364-127">Hola sustituto `<server_admin_password>` con su propio valor.</span><span class="sxs-lookup"><span data-stu-id="2f364-127">Substitute hello `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401 --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="2f364-128">inicio de sesión de administrador de servidor de Hola y la contraseña que especifique aquí son necesario toolog en toohello server y sus bases de datos más adelante en esta guía de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="2f364-128">hello server admin login and password that you specify here are required toolog in toohello server and its databases later in this quick start.</span></span> <span data-ttu-id="2f364-129">Recuerde o grabe esta información para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="2f364-129">Remember or record this information for later use.</span></span>

<span data-ttu-id="2f364-130">De forma predeterminada, la base de datos de **postgres** se crea en el servidor.</span><span class="sxs-lookup"><span data-stu-id="2f364-130">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="2f364-131">Hola [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) base de datos es una base de datos predeterminada destinado a los usuarios, utilidades y aplicaciones de otros fabricantes.</span><span class="sxs-lookup"><span data-stu-id="2f364-131">hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="2f364-132">Configuración de una regla de firewall de nivel de servidor</span><span class="sxs-lookup"><span data-stu-id="2f364-132">Configure a server-level firewall rule</span></span>

<span data-ttu-id="2f364-133">Crear una regla de firewall de nivel de servidor de Azure PostgreSQL con hello [crear az postgres servidor regla de firewall](/cli/azure/postgres/server/firewall-rule#create) comando.</span><span class="sxs-lookup"><span data-stu-id="2f364-133">Create an Azure PostgreSQL server-level firewall rule with hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="2f364-134">Una regla de firewall de nivel de servidor permite que una aplicación externa, como [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) o [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server a través de firewall de servicio de hello Azure PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="2f364-134">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server through hello Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="2f364-135">Puede establecer una regla de firewall que abarca un intervalo IP toobe tooconnect capaz de la red.</span><span class="sxs-lookup"><span data-stu-id="2f364-135">You can set a firewall rule that covers an IP range toobe able tooconnect from your network.</span></span> <span data-ttu-id="2f364-136">Hello siguiente ejemplo se utiliza [crear az postgres servidor regla de firewall](/cli/azure/postgres/server/firewall-rule#create) toocreate una regla de firewall `AllowAllIps` para una dirección IP, intervalo.</span><span class="sxs-lookup"><span data-stu-id="2f364-136">hello following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) toocreate a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="2f364-137">tooopen todas las direcciones IP, utilice 0.0.0.0 como Hola a partir de dirección IP y 255.255.255.255 como Hola dirección final.</span><span class="sxs-lookup"><span data-stu-id="2f364-137">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="2f364-138">El servidor Azure PostgreSQL se comunica a través de puerto 5432.</span><span class="sxs-lookup"><span data-stu-id="2f364-138">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="2f364-139">Al conectarse desde una red corporativa, es posible que el firewall de la red no permita el tráfico saliente a través del puerto 5432.</span><span class="sxs-lookup"><span data-stu-id="2f364-139">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="2f364-140">Tiene el departamento de TI abrir puerto 5432 tooconnect tooyour base de datos de Azure SQL server.</span><span class="sxs-lookup"><span data-stu-id="2f364-140">Have your IT department open port 5432 tooconnect tooyour Azure SQL Database server.</span></span>
>

## <a name="get-hello-connection-information"></a><span data-ttu-id="2f364-141">Obtener información de conexión de Hola</span><span class="sxs-lookup"><span data-stu-id="2f364-141">Get hello connection information</span></span>

<span data-ttu-id="2f364-142">tooconnect tooyour server, necesita credenciales de acceso y la información de host de tooprovide.</span><span class="sxs-lookup"><span data-stu-id="2f364-142">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="2f364-143">resultado de Hello es en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="2f364-143">hello result is in JSON format.</span></span> <span data-ttu-id="2f364-144">Tome nota de hello **Iniciodesesióndeadministrador** y **fullyQualifiedDomainName**.</span><span class="sxs-lookup"><span data-stu-id="2f364-144">Make a note of hello **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
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

## <a name="connect-tooazure-database-for-postgresql-database-using-psql"></a><span data-ttu-id="2f364-145">Conectar tooAzure base de datos para la base de datos de PostgreSQL mediante psql</span><span class="sxs-lookup"><span data-stu-id="2f364-145">Connect tooAzure Database for PostgreSQL database using psql</span></span>
<span data-ttu-id="2f364-146">Si el equipo cliente tenga PostgreSQL instalado, puede usar una instancia local de [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), o el servidor de hello consola en la nube de Azure tooconnect tooan PostgreSQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="2f364-146">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), or hello Azure Cloud Console tooconnect tooan Azure PostgreSQL server.</span></span> <span data-ttu-id="2f364-147">Vamos a usar ahora hello psql utilidad de línea de comandos tooconnect toohello base de datos de Azure para servidor de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="2f364-147">Let's now use hello psql command-line utility tooconnect toohello Azure Database for PostgreSQL server.</span></span>

1. <span data-ttu-id="2f364-148">Ejecute hello después psql comandos tooconnect tooan base de datos de Azure para servidor de PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="2f364-148">Run hello following psql command tooconnect tooan Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="2f364-149">Por ejemplo, hello siguiente comando conecta a base de datos de toohello predeterminada denominada **postgres** en el servidor de PostgreSQL **mypgserver 20170401.postgres.database.azure.com** utilizando las credenciales de acceso.</span><span class="sxs-lookup"><span data-stu-id="2f364-149">For example, hello following command connects toohello default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="2f364-150">Escriba hello `<server_admin_password>` elegido cuando se le solicite una contraseña.</span><span class="sxs-lookup"><span data-stu-id="2f364-150">Enter hello `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 ---dbname=postgres
```

2.  <span data-ttu-id="2f364-151">Una vez que esté conectado toohello server, cree una base de datos en blanco en el símbolo del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f364-151">Once you are connected toohello server, create a blank database at hello prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="2f364-152">En el símbolo del sistema de hello, ejecute hello después de la base de datos de comando tooswitch conexión toohello recién creado **mypgsqldb**:</span><span class="sxs-lookup"><span data-stu-id="2f364-152">At hello prompt, execute hello following command tooswitch connection toohello newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="2f364-153">Crear tablas de base de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="2f364-153">Create tables in hello database</span></span>
<span data-ttu-id="2f364-154">Ahora que sabe cómo tooconnect toohello base de datos de Azure para PostgreSQL, podemos ver cómo toocomplete algunas tareas básicas.</span><span class="sxs-lookup"><span data-stu-id="2f364-154">Now that you know how tooconnect toohello Azure Database for PostgreSQL, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="2f364-155">En primer lugar, podemos crear una tabla y cargarla con algunos datos.</span><span class="sxs-lookup"><span data-stu-id="2f364-155">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="2f364-156">Vamos a crear una tabla que hace el seguimiento de información del inventario.</span><span class="sxs-lookup"><span data-stu-id="2f364-156">Let's create a table that tracks inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

<span data-ttu-id="2f364-157">Puede ver Hola recién creado tabla en la lista de Hola de tablas ahora escribiendo:</span><span class="sxs-lookup"><span data-stu-id="2f364-157">You can see hello newly created table in hello list of tables now by typing:</span></span>
```sql
\dt
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="2f364-158">Cargar datos en tablas de Hola</span><span class="sxs-lookup"><span data-stu-id="2f364-158">Load data into hello tables</span></span>
<span data-ttu-id="2f364-159">Ahora que tenemos una tabla, podemos insertar algunos datos en ella.</span><span class="sxs-lookup"><span data-stu-id="2f364-159">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="2f364-160">En la ventana de símbolo del sistema abierto hello, ejecute hello después consulta tooinsert algunas filas de datos</span><span class="sxs-lookup"><span data-stu-id="2f364-160">At hello open command prompt window, run hello following query tooinsert some rows of data</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="2f364-161">Tiene ahora dos filas de datos de ejemplo en la tabla de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2f364-161">You have now two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="2f364-162">Consultar y actualizar los datos de hello en tablas de Hola</span><span class="sxs-lookup"><span data-stu-id="2f364-162">Query and update hello data in hello tables</span></span>
<span data-ttu-id="2f364-163">Ejecute hello siguientes tooretrieve información de consulta de tabla de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f364-163">Execute hello following query tooretrieve information from hello database table.</span></span> 
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="2f364-164">También puede actualizar los datos de hello en tablas de Hola</span><span class="sxs-lookup"><span data-stu-id="2f364-164">You can also update hello data in hello tables</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="2f364-165">fila de Hola se actualiza en consecuencia cuando se recuperan datos.</span><span class="sxs-lookup"><span data-stu-id="2f364-165">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="2f364-166">Restaurar un punto anterior de tooa de base de datos en el tiempo</span><span class="sxs-lookup"><span data-stu-id="2f364-166">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="2f364-167">Imagine que ha eliminado accidentalmente una tabla.</span><span class="sxs-lookup"><span data-stu-id="2f364-167">Imagine you have accidentally deleted a table.</span></span> <span data-ttu-id="2f364-168">No se puede recuperar con facilidad.</span><span class="sxs-lookup"><span data-stu-id="2f364-168">This is something you cannot easily recover from.</span></span> <span data-ttu-id="2f364-169">Base de datos de Azure para PostgreSQL permite toogo tooany atrás en un momento (en Hola última too7 días (Basic) y 35 días (estándar)) y restaurar este punto-in-time tooa nuevo servidor.</span><span class="sxs-lookup"><span data-stu-id="2f364-169">Azure Database for PostgreSQL allows you toogo back tooany point-in-time (in hello last up too7 days (Basic) and 35 days (Standard)) and restore this point-in-time tooa new server.</span></span> <span data-ttu-id="2f364-170">Puede usar esta nueva toorecover server los datos eliminados.</span><span class="sxs-lookup"><span data-stu-id="2f364-170">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="2f364-171">Hola siguiendo los pasos restauración Hola ejemplo servidor tooa punto antes de que se ha agregado Hola tabla.</span><span class="sxs-lookup"><span data-stu-id="2f364-171">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="2f364-172">Hola `az postgres server restore` comando necesita Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="2f364-172">hello `az postgres server restore` command needs hello following parameters:</span></span>
| <span data-ttu-id="2f364-173">Configuración</span><span class="sxs-lookup"><span data-stu-id="2f364-173">Setting</span></span> | <span data-ttu-id="2f364-174">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="2f364-174">Suggested value</span></span> | <span data-ttu-id="2f364-175">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f364-175">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="2f364-176">--resource-group</span><span class="sxs-lookup"><span data-stu-id="2f364-176">--resource-group</span></span> |  <span data-ttu-id="2f364-177">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2f364-177">myResourceGroup</span></span> |  <span data-ttu-id="2f364-178">El grupo de recursos en qué Hola existe el servidor de origen.</span><span class="sxs-lookup"><span data-stu-id="2f364-178">The resource group in which hello source server exists.</span></span>  |
| <span data-ttu-id="2f364-179">--name</span><span class="sxs-lookup"><span data-stu-id="2f364-179">--name</span></span> | <span data-ttu-id="2f364-180">mypgserver-restored</span><span class="sxs-lookup"><span data-stu-id="2f364-180">mypgserver-restored</span></span> | <span data-ttu-id="2f364-181">nombre de Hola de hello nuevo servidor que se crea mediante el comando de restauración de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f364-181">hello name of hello new server that is created by hello restore command.</span></span> |
| <span data-ttu-id="2f364-182">restore-point-in-time</span><span class="sxs-lookup"><span data-stu-id="2f364-182">restore-point-in-time</span></span> | <span data-ttu-id="2f364-183">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="2f364-183">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="2f364-184">Seleccione un toorestore en un momento a.</span><span class="sxs-lookup"><span data-stu-id="2f364-184">Select a point-in-time toorestore to.</span></span> <span data-ttu-id="2f364-185">Esta fecha y hora deben ser dentro del período de retención de copia de seguridad del servidor de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f364-185">This date and time must be within hello source server's backup retention period.</span></span> <span data-ttu-id="2f364-186">Use el formato de fecha y hora ISO8601.</span><span class="sxs-lookup"><span data-stu-id="2f364-186">Use ISO8601 date and time format.</span></span> <span data-ttu-id="2f364-187">Por ejemplo, puede usar su propia zona horaria local, como `2017-04-13T05:59:00-08:00`, o usar el formato de hora Zulú UTC `2017-04-13T13:59:00Z`.</span><span class="sxs-lookup"><span data-stu-id="2f364-187">For example, you may use your own local timezone, such as `2017-04-13T05:59:00-08:00`, or use UTC Zulu format `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="2f364-188">--source-server</span><span class="sxs-lookup"><span data-stu-id="2f364-188">--source-server</span></span> | <span data-ttu-id="2f364-189">mypgserver-20170401</span><span class="sxs-lookup"><span data-stu-id="2f364-189">mypgserver-20170401</span></span> | <span data-ttu-id="2f364-190">nombre de Hola o Id. de hello toorestore de servidor de origen de.</span><span class="sxs-lookup"><span data-stu-id="2f364-190">hello name or ID of hello source server toorestore from.</span></span> |

<span data-ttu-id="2f364-191">Restaurar un servidor tooa en un momento, crea un nuevo servidor, copiar como servidor original, Hola desde el punto de hello en el tiempo que especifique.</span><span class="sxs-lookup"><span data-stu-id="2f364-191">Restoring a server tooa point-in-time creates a new server, copying as hello original server as of hello point in time you specify.</span></span> <span data-ttu-id="2f364-192">ubicación de Hola y precios valores de nivel de servidor hello restaurado se Hola igual que el servidor de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f364-192">hello location and pricing tier values for hello restored server are hello same as hello source server.</span></span>

<span data-ttu-id="2f364-193">comando Hello es sincrónico y se devolverá una vez se haya restaurado el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f364-193">hello command is synchronous, and will return after hello server is restored.</span></span> <span data-ttu-id="2f364-194">Una vez finalizada la restauración de hello, busque servidor nuevo de Hola que se creó.</span><span class="sxs-lookup"><span data-stu-id="2f364-194">Once hello restore finishes, locate hello new server that was created.</span></span> <span data-ttu-id="2f364-195">Compruebe Hola se restauran datos según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="2f364-195">Verify hello data was restored as expected.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2f364-196">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2f364-196">Next steps</span></span>
<span data-ttu-id="2f364-197">En este tutorial, se habrá aprendido cómo toouse Azure CLI (interfaz de línea de comandos) y otras utilidades para:</span><span class="sxs-lookup"><span data-stu-id="2f364-197">In this tutorial, you learned how toouse Azure CLI (command-line interface) and other utilities to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="2f364-198">Creación de una instancia de Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="2f364-198">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="2f364-199">Configurar firewall de servidor hello</span><span class="sxs-lookup"><span data-stu-id="2f364-199">Configure hello server firewall</span></span>
> * <span data-ttu-id="2f364-200">Use [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) utilidad toocreate una base de datos</span><span class="sxs-lookup"><span data-stu-id="2f364-200">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility toocreate a database</span></span>
> * <span data-ttu-id="2f364-201">Carga de datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2f364-201">Load sample data</span></span>
> * <span data-ttu-id="2f364-202">Datos de consulta</span><span class="sxs-lookup"><span data-stu-id="2f364-202">Query data</span></span>
> * <span data-ttu-id="2f364-203">Actualización de datos</span><span class="sxs-lookup"><span data-stu-id="2f364-203">Update data</span></span>
> * <span data-ttu-id="2f364-204">Restauración de datos</span><span class="sxs-lookup"><span data-stu-id="2f364-204">Restore data</span></span>

<span data-ttu-id="2f364-205">A continuación, obtenga información acerca de cómo toouse Hola tareas similares de Azure toodo portal, revise este tutorial: [diseñar la primera base de datos de Azure para usar PostgreSQL Hola portal de Azure](tutorial-design-database-using-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="2f364-205">Next, learn how toouse hello Azure portal toodo similar tasks, review this tutorial: [Design your first Azure Database for PostgreSQL using hello Azure portal](tutorial-design-database-using-azure-portal.md)</span></span>
