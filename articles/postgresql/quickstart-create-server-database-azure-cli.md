---
title: Crear una base de datos de Azure para PostgreSQL con la CLI de Azure | Microsoft Docs
description: "Guía de inicio rápido para crear y administrar la base de datos de Azure para el servidor PostgreSQL mediante la CLI (interfaz de la línea de comandos) de Azure."
services: postgresql
author: sanagama
ms.author: sanagama
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: quickstart
ms.date: 06/13/2017
ms.openlocfilehash: d78243abc140c7b3f0b99bdf56821b7920568550
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-azure-database-for-postgresql-using-the-azure-cli"></a><span data-ttu-id="d8f79-103">Crear una base de datos de Azure para PostgreSQL con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="d8f79-103">Create an Azure Database for PostgreSQL using the Azure CLI</span></span>
<span data-ttu-id="d8f79-104">La base de datos de Azure para PostgreSQL es un servicio administrado que le permite ejecutar, administrar y escalar bases de datos de PostgreSQL de alta disponibilidad en la nube.</span><span class="sxs-lookup"><span data-stu-id="d8f79-104">Azure Database for PostgreSQL is a managed service that enables you to run, manage, and scale highly available PostgreSQL databases in the cloud.</span></span> <span data-ttu-id="d8f79-105">La CLI de Azure se usa para crear y administrar recursos de Azure desde la línea de comandos o en scripts.</span><span class="sxs-lookup"><span data-stu-id="d8f79-105">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="d8f79-106">En esta guía de inicio rápido se muestra cómo crear una base de datos de Azure para el servidor PostgreSQL en un [grupo de recursos de Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="d8f79-106">This quickstart shows you how to create an Azure Database for PostgreSQL server in an [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) using the Azure CLI.</span></span>

<span data-ttu-id="d8f79-107">Si no tiene una suscripción a Azure, cree una cuenta [gratuita](https://azure.microsoft.com/free/) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="d8f79-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d8f79-108">Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="d8f79-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d8f79-109">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="d8f79-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="d8f79-110">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d8f79-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="d8f79-111">Si tiene varias suscripciones, elija la suscripción en la que se vaya a facturar el recurso.</span><span class="sxs-lookup"><span data-stu-id="d8f79-111">If you have multiple subscriptions, choose the appropriate subscription in which the resource will be billed.</span></span> <span data-ttu-id="d8f79-112">Seleccione un identificador de suscripción específico en su cuenta mediante el comando [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="d8f79-112">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="d8f79-113">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="d8f79-113">Create a resource group</span></span>

<span data-ttu-id="d8f79-114">Cree un [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md) con el comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="d8f79-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="d8f79-115">Un grupo de recursos es un contenedor lógico en el que se implementan y se administran recursos de Azure como un grupo.</span><span class="sxs-lookup"><span data-stu-id="d8f79-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="d8f79-116">En el ejemplo siguiente, se crea un grupo de recursos denominado `myresourcegroup` en la ubicación `westus`.</span><span class="sxs-lookup"><span data-stu-id="d8f79-116">The following example creates a resource group named `myresourcegroup` in the `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="d8f79-117">Creación de un servidor de Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="d8f79-117">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="d8f79-118">Cree un [servidor de Azure Database for PostgreSQL](overview.md) con el comando [az postgres server create](/cli/azure/postgres/server#create).</span><span class="sxs-lookup"><span data-stu-id="d8f79-118">Create an [Azure Database for PostgreSQL server](overview.md) using the [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="d8f79-119">Un servidor contiene un conjunto de bases de datos administradas como un grupo.</span><span class="sxs-lookup"><span data-stu-id="d8f79-119">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="d8f79-120">En el ejemplo siguiente se crea un servidor denominado `mypgserver-20170401` en el grupo de recursos `myresourcegroup` con el inicio de sesión de administrador de servidor `mylogin`.</span><span class="sxs-lookup"><span data-stu-id="d8f79-120">The following example creates a server named `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="d8f79-121">El nombre de un servidor se asigna al nombre DNS y, por tanto, debe ser único a nivel global en Azure.</span><span class="sxs-lookup"><span data-stu-id="d8f79-121">The name of a server maps to DNS name and is thus required to be globally unique in Azure.</span></span> <span data-ttu-id="d8f79-122">Sustituya `<server_admin_password>` por su propio valor.</span><span class="sxs-lookup"><span data-stu-id="d8f79-122">Substitute the `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401  --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="d8f79-123">Se requiere el inicio de sesión y la contraseña de administrador de servidor que especifique aquí para iniciar sesión en el servidor y a sus bases de datos más adelante en esta guía de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="d8f79-123">The server admin login and password that you specify here are required to log in to the server and its databases later in this quick start.</span></span> <span data-ttu-id="d8f79-124">Recuerde o grabe esta información para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="d8f79-124">Remember or record this information for later use.</span></span>

<span data-ttu-id="d8f79-125">De forma predeterminada, la base de datos de **postgres** se crea en el servidor.</span><span class="sxs-lookup"><span data-stu-id="d8f79-125">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="d8f79-126">La base de datos [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) es una base de datos predeterminada pensada para que la usen los usuarios, las utilidades y aplicaciones de otros fabricantes.</span><span class="sxs-lookup"><span data-stu-id="d8f79-126">The [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="d8f79-127">Configuración de una regla de firewall de nivel de servidor</span><span class="sxs-lookup"><span data-stu-id="d8f79-127">Configure a server-level firewall rule</span></span>

<span data-ttu-id="d8f79-128">Cree una regla de firewall de nivel de servidor de Azure PostgreSQL con el comando [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create).</span><span class="sxs-lookup"><span data-stu-id="d8f79-128">Create an Azure PostgreSQL server-level firewall rule with the [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="d8f79-129">Una regla de firewall de nivel de servidor permite que una aplicación externa, como [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) o [PgAdmin](https://www.pgadmin.org/), se conecte al servidor a través del firewall del servicio Azure PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="d8f79-129">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) to connect to your server through the Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="d8f79-130">Puede establecer una regla de firewall que abarque un intervalo de IP para poder conectarse desde la red.</span><span class="sxs-lookup"><span data-stu-id="d8f79-130">You can set a firewall rule that covers an IP range to be able to connect from your network.</span></span> <span data-ttu-id="d8f79-131">En el ejemplo siguiente se usa [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) para crear una regla de firewall `AllowAllIps` para un intervalo de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="d8f79-131">The following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) to create a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="d8f79-132">Para abrir todas las direcciones IP, utilice 0.0.0.0 como la dirección IP inicial y 255.255.255.255 como la dirección final.</span><span class="sxs-lookup"><span data-stu-id="d8f79-132">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="d8f79-133">El servidor Azure PostgreSQL se comunica a través de puerto 5432.</span><span class="sxs-lookup"><span data-stu-id="d8f79-133">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="d8f79-134">Al conectarse desde una red corporativa, es posible que el firewall de la red no permita el tráfico saliente a través del puerto 5432.</span><span class="sxs-lookup"><span data-stu-id="d8f79-134">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="d8f79-135">Haga que el departamento de TI abra el puerto 5432 para conectarse al servidor de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="d8f79-135">Have your IT department open port 5432 to connect to your Azure SQL Database server.</span></span>

## <a name="get-the-connection-information"></a><span data-ttu-id="d8f79-136">Obtención de la información de conexión</span><span class="sxs-lookup"><span data-stu-id="d8f79-136">Get the connection information</span></span>

<span data-ttu-id="d8f79-137">Para conectarse al servidor, debe proporcionar las credenciales de acceso y la información del host.</span><span class="sxs-lookup"><span data-stu-id="d8f79-137">To connect to your server, you need to provide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="d8f79-138">El resultado está en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="d8f79-138">The result is in JSON format.</span></span> <span data-ttu-id="d8f79-139">Tome nota de los valores de **administratorLogin** y **fullyQualifiedDomainName**.</span><span class="sxs-lookup"><span data-stu-id="d8f79-139">Make a note of the **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
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

## <a name="connect-to-postgresql-database-using-psql"></a><span data-ttu-id="d8f79-140">Conectarse a la base de datos de PostgreSQL mediante psql</span><span class="sxs-lookup"><span data-stu-id="d8f79-140">Connect to PostgreSQL database using psql</span></span>

<span data-ttu-id="d8f79-141">Si el equipo cliente tiene PostgreSQL instalado, puede usar una instancia local de [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) para conectarse a un servidor Azure PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="d8f79-141">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) to connect to an Azure PostgreSQL server.</span></span> <span data-ttu-id="d8f79-142">Ahora vamos a usar la utilidad de línea de comandos psql para conectarnos al servidor Azure PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="d8f79-142">Let's now use the psql command-line utility to connect to the Azure PostgreSQL server.</span></span>

1. <span data-ttu-id="d8f79-143">Ejecute el comando psql siguiente para conectarse a un servidor de Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="d8f79-143">Run the following psql command to connect to an Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="d8f79-144">Por ejemplo, el siguiente comando se conecta a la base de datos predeterminada denominada **postgres** en el servidor PostgreSQL **mypgserver-20170401.postgres.database.azure.com** con las credenciales de acceso.</span><span class="sxs-lookup"><span data-stu-id="d8f79-144">For example, the following command connects to the default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="d8f79-145">Escriba el valor de `<server_admin_password>` que eligió cuando se le solicitó una contraseña.</span><span class="sxs-lookup"><span data-stu-id="d8f79-145">Enter the `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
```

2.  <span data-ttu-id="d8f79-146">Una vez conectado al servidor, cree una base de datos vacía en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="d8f79-146">Once you are connected to the server, create a blank database at the prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="d8f79-147">En el símbolo del sistema, ejecute el siguiente comando para cambiar la conexión a la base de datos **mypgsqldb** recién creada:</span><span class="sxs-lookup"><span data-stu-id="d8f79-147">At the prompt, execute the following command to switch connection to the newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="connect-to-postgresql-database-using-pgadmin"></a><span data-ttu-id="d8f79-148">Conectarse a la base de datos de PostgreSQL mediante pgAdmin</span><span class="sxs-lookup"><span data-stu-id="d8f79-148">Connect to PostgreSQL database using pgAdmin</span></span>

<span data-ttu-id="d8f79-149">Para conectarse al servidor Azure PostgreSQL mediante la herramienta _pgAdmin_ de la GUI:</span><span class="sxs-lookup"><span data-stu-id="d8f79-149">To connect to Azure PostgreSQL server using the GUI tool _pgAdmin_</span></span>
1.  <span data-ttu-id="d8f79-150">Inicie la aplicación _pgAdmin_ en el equipo cliente.</span><span class="sxs-lookup"><span data-stu-id="d8f79-150">Launch the _pgAdmin_ application on your client computer.</span></span> <span data-ttu-id="d8f79-151">Puede instalar _pgAdmin_ desde http://www.pgadmin.org/.</span><span class="sxs-lookup"><span data-stu-id="d8f79-151">You can install _pgAdmin_ from http://www.pgadmin.org/.</span></span>
2.  <span data-ttu-id="d8f79-152">Seleccione **Agregar nuevo servidor** en el menú **Vínculos rápidos**.</span><span class="sxs-lookup"><span data-stu-id="d8f79-152">Choose **Add New Server** from the **Quick Links** menu.</span></span>
3.  <span data-ttu-id="d8f79-153">En la pestaña **General** del cuadro de diálogo **Crear servidor**, escriba un nombre descriptivo único para el servidor,</span><span class="sxs-lookup"><span data-stu-id="d8f79-153">In the **Create - Server** dialog box **General** tab, enter a unique friendly Name for the server.</span></span> <span data-ttu-id="d8f79-154">como **Azure PostgreSQL Server**.</span><span class="sxs-lookup"><span data-stu-id="d8f79-154">Say **Azure PostgreSQL Server**.</span></span>
 <span data-ttu-id="d8f79-155">![Herramienta pgAdmin: Crear servidor](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span><span class="sxs-lookup"><span data-stu-id="d8f79-155">![pgAdmin tool - create - server](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span></span>
4.  <span data-ttu-id="d8f79-156">En el cuadro de diálogo **Crear servidor**, en la pestaña **Conexión**:</span><span class="sxs-lookup"><span data-stu-id="d8f79-156">In the **Create - Server** dialog box, **Connection** tab:</span></span>
    - <span data-ttu-id="d8f79-157">Escriba el nombre completo del servidor (por ejemplo, **mypgserver-20170401.postgres.database.azure.com**) en el cuadro **Host Name/Address** (Nombre o dirección de host).</span><span class="sxs-lookup"><span data-stu-id="d8f79-157">Enter the fully qualified server name (for example, **mypgserver-20170401.postgres.database.azure.com**) in the **Host Name/ Address** box.</span></span> 
    - <span data-ttu-id="d8f79-158">Escriba el puerto 5432 en el cuadro **Puerto**.</span><span class="sxs-lookup"><span data-stu-id="d8f79-158">Enter port 5432 into the **Port** box.</span></span> 
    - <span data-ttu-id="d8f79-159">Escriba el **Inicio de sesión del administrador del servidor (user@mypgserver)** obtenido anteriormente en esta guía de inicio rápido y la contraseña que especificó al crear el servidor en los cuadros **Nombre de usuario** y **Contraseña**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="d8f79-159">Enter the **Server admin login (user@mypgserver)** obtained earlier in this quickstart and password you entered when you created the server into the **Username** and **Password** boxes, respectively.</span></span>
    - <span data-ttu-id="d8f79-160">Seleccione el **Modo SSL** como **Requerir**.</span><span class="sxs-lookup"><span data-stu-id="d8f79-160">Select **SSL Mode** as **Require**.</span></span> <span data-ttu-id="d8f79-161">De forma predeterminada, todos los servidores Azure PostgreSQL se crean de modo que se exija SSL.</span><span class="sxs-lookup"><span data-stu-id="d8f79-161">By default, all Azure PostgreSQL servers are created with SSL enforcing turned ON.</span></span> <span data-ttu-id="d8f79-162">Para desactivar la obligación de SSL, vea los detalles en la sección sobre la [obligación de SSL](./concepts-ssl-connection-security.md).</span><span class="sxs-lookup"><span data-stu-id="d8f79-162">To turn OFF SSL enforcing, see details in [Enforcing SSL](./concepts-ssl-connection-security.md).</span></span>

    ![pgAdmin: Crear servidor](./media/quickstart-create-server-database-azure-cli/2-pgadmin-create-server.png)
5.  <span data-ttu-id="d8f79-164">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="d8f79-164">Click **Save**.</span></span>
6.  <span data-ttu-id="d8f79-165">En el panel izquierdo del explorador, expanda **Grupos de servidores**.</span><span class="sxs-lookup"><span data-stu-id="d8f79-165">In the Browser left pane, expand the **Server Groups**.</span></span> <span data-ttu-id="d8f79-166">Seleccione su **servidor Azure PostgreSQL**.</span><span class="sxs-lookup"><span data-stu-id="d8f79-166">Choose your server **Azure PostgreSQL Server**.</span></span>
7.  <span data-ttu-id="d8f79-167">Elija el **Server** (Servidor) al que se ha conectado y sus **Databases** (Bases de datos).</span><span class="sxs-lookup"><span data-stu-id="d8f79-167">Choose the **Server** you connected to, and then choose **Databases** under it.</span></span> 
8.  <span data-ttu-id="d8f79-168">Haga clic con el botón derecho en **Bases de datos** para crear una base de datos.</span><span class="sxs-lookup"><span data-stu-id="d8f79-168">Right-click on **Databases** to Create a Database.</span></span>
9.  <span data-ttu-id="d8f79-169">Elija el nombre de base de datos **mypgsqldb** y su propietario como valor **mylogin** para el inicio de sesión de administrador de servidor.</span><span class="sxs-lookup"><span data-stu-id="d8f79-169">Choose a database name **mypgsqldb** and the owner for it as server admin login **mylogin**.</span></span>
10. <span data-ttu-id="d8f79-170">Haga clic en **Guardar** para crear una base de datos vacía.</span><span class="sxs-lookup"><span data-stu-id="d8f79-170">Click **Save** to create a blank database.</span></span>
11. <span data-ttu-id="d8f79-171">En **Explorador**, expanda el grupo **Servidores**.</span><span class="sxs-lookup"><span data-stu-id="d8f79-171">In the **Browser**, expand the **Servers** group.</span></span> <span data-ttu-id="d8f79-172">Expanda el servidor que ha creado y verá su base de datos **mypgsqldb**.</span><span class="sxs-lookup"><span data-stu-id="d8f79-172">Expand the server you created, and see the database **mypgsqldb** under it.</span></span>
 <span data-ttu-id="d8f79-173">![pgAdmin: Crear base de datos](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span><span class="sxs-lookup"><span data-stu-id="d8f79-173">![pgAdmin - Create - Database](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span></span>


## <a name="clean-up-resources"></a><span data-ttu-id="d8f79-174">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="d8f79-174">Clean up resources</span></span>

<span data-ttu-id="d8f79-175">Elimine el [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md) para eliminar todos los recursos que ha creado en la guía de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="d8f79-175">Clean up all resources you created in the quickstart by deleting the [Azure resource group](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!TIP]
> <span data-ttu-id="d8f79-176">Otras guías de inicio rápido de esta colección se basan en los valores de esta.</span><span class="sxs-lookup"><span data-stu-id="d8f79-176">Other quickstarts in this collection build upon this quick start.</span></span> <span data-ttu-id="d8f79-177">Si tiene previsto seguir trabajando con las siguientes guías de inicio rápido, no elimine los recursos creados en esta.</span><span class="sxs-lookup"><span data-stu-id="d8f79-177">If you plan to continue on to work with subsequent quickstarts, do not clean up the resources created in this quickstart.</span></span> <span data-ttu-id="d8f79-178">Si no tiene previsto continuar, siga estos pasos para eliminar todos los recursos creados en esta guía de inicio rápido en la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="d8f79-178">If you do not plan to continue, use the following steps to delete all resources created by this quickstart in the Azure CLI.</span></span>

```azurecli-interactive
az group delete --name myresourcegroup
```

<span data-ttu-id="d8f79-179">Si solo desea eliminar el servidor recién creado uno, puede ejecutar el comando [az postgres server delete](/cli/azure/postgres/server#delete).</span><span class="sxs-lookup"><span data-stu-id="d8f79-179">If you just would like to delete the one newly created server, you can run [az postgres server delete](/cli/azure/postgres/server#delete) command.</span></span>
```azurecli-interactive
az postgres server delete --resource-group myresourcegroup --name mypgserver-20170401
```

## <a name="next-steps"></a><span data-ttu-id="d8f79-180">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d8f79-180">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="d8f79-181">Migración de una base de datos mediante exportación e importación</span><span class="sxs-lookup"><span data-stu-id="d8f79-181">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
