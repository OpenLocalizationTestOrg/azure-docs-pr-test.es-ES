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
# <a name="create-an-azure-database-for-postgresql-using-hello-azure-cli"></a><span data-ttu-id="18e9c-103">Crear una base de datos de Azure para PostgreSQL mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="18e9c-103">Create an Azure Database for PostgreSQL using hello Azure CLI</span></span>
<span data-ttu-id="18e9c-104">Base de datos de Azure para PostgreSQL es un servicio administrado que le permite toorun, administrar y escalar las bases de datos de PostgreSQL altamente disponibles en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="18e9c-104">Azure Database for PostgreSQL is a managed service that enables you toorun, manage, and scale highly available PostgreSQL databases in hello cloud.</span></span> <span data-ttu-id="18e9c-105">Hola CLI de Azure es toocreate usado y administrar recursos de Azure desde la línea de comandos de Hola o en scripts.</span><span class="sxs-lookup"><span data-stu-id="18e9c-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="18e9c-106">Este tutorial rápido muestra cómo toocreate una Azure base de datos para el servidor de PostgreSQL en un [grupo de recursos de Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) utilizando Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="18e9c-106">This quickstart shows you how toocreate an Azure Database for PostgreSQL server in an [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) using hello Azure CLI.</span></span>

<span data-ttu-id="18e9c-107">Si no tiene una suscripción a Azure, cree una cuenta [gratuita](https://azure.microsoft.com/free/) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="18e9c-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="18e9c-108">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuten hello Azure CLI versión 2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="18e9c-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="18e9c-109">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="18e9c-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="18e9c-110">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="18e9c-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="18e9c-111">Si tiene varias suscripciones, elija suscripción adecuado de hello en el que se cobrará recursos Hola.</span><span class="sxs-lookup"><span data-stu-id="18e9c-111">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource will be billed.</span></span> <span data-ttu-id="18e9c-112">Seleccione un identificador de suscripción específico en su cuenta mediante el comando [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="18e9c-112">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="18e9c-113">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="18e9c-113">Create a resource group</span></span>

<span data-ttu-id="18e9c-114">Crear un [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md) con hello [crear grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="18e9c-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="18e9c-115">Un grupo de recursos es un contenedor lógico en el que se implementan y se administran recursos de Azure como un grupo.</span><span class="sxs-lookup"><span data-stu-id="18e9c-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="18e9c-116">Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myresourcegroup` en hello `westus` ubicación.</span><span class="sxs-lookup"><span data-stu-id="18e9c-116">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="18e9c-117">Creación de un servidor de Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="18e9c-117">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="18e9c-118">Crear un [base de datos de Azure para PostgreSQL server](overview.md) con hello [az postgres servidor crear](/cli/azure/postgres/server#create) comando.</span><span class="sxs-lookup"><span data-stu-id="18e9c-118">Create an [Azure Database for PostgreSQL server](overview.md) using hello [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="18e9c-119">Un servidor contiene un conjunto de bases de datos administradas como un grupo.</span><span class="sxs-lookup"><span data-stu-id="18e9c-119">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="18e9c-120">Hello en el ejemplo siguiente se crea un servidor denominado `mypgserver-20170401` en el grupo de recursos `myresourcegroup` con inicio de sesión de administrador de servidor `mylogin`.</span><span class="sxs-lookup"><span data-stu-id="18e9c-120">hello following example creates a server named `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="18e9c-121">nombre de Hola de un servidor asigna nombre tooDNS y, por tanto, es necesario toobe globalmente único en Azure.</span><span class="sxs-lookup"><span data-stu-id="18e9c-121">hello name of a server maps tooDNS name and is thus required toobe globally unique in Azure.</span></span> <span data-ttu-id="18e9c-122">Hola sustituto `<server_admin_password>` con su propio valor.</span><span class="sxs-lookup"><span data-stu-id="18e9c-122">Substitute hello `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401  --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="18e9c-123">inicio de sesión de administrador de servidor de Hola y la contraseña que especifique aquí son necesario toolog en toohello server y sus bases de datos más adelante en esta guía de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="18e9c-123">hello server admin login and password that you specify here are required toolog in toohello server and its databases later in this quick start.</span></span> <span data-ttu-id="18e9c-124">Recuerde o grabe esta información para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="18e9c-124">Remember or record this information for later use.</span></span>

<span data-ttu-id="18e9c-125">De forma predeterminada, la base de datos de **postgres** se crea en el servidor.</span><span class="sxs-lookup"><span data-stu-id="18e9c-125">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="18e9c-126">Hola [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) base de datos es una base de datos predeterminada destinado a los usuarios, utilidades y aplicaciones de otros fabricantes.</span><span class="sxs-lookup"><span data-stu-id="18e9c-126">hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="18e9c-127">Configuración de una regla de firewall de nivel de servidor</span><span class="sxs-lookup"><span data-stu-id="18e9c-127">Configure a server-level firewall rule</span></span>

<span data-ttu-id="18e9c-128">Crear una regla de firewall de nivel de servidor de Azure PostgreSQL con hello [crear az postgres servidor regla de firewall](/cli/azure/postgres/server/firewall-rule#create) comando.</span><span class="sxs-lookup"><span data-stu-id="18e9c-128">Create an Azure PostgreSQL server-level firewall rule with hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="18e9c-129">Una regla de firewall de nivel de servidor permite que una aplicación externa, como [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) o [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server a través de firewall de servicio de hello Azure PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="18e9c-129">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server through hello Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="18e9c-130">Puede establecer una regla de firewall que abarca un intervalo IP toobe tooconnect capaz de la red.</span><span class="sxs-lookup"><span data-stu-id="18e9c-130">You can set a firewall rule that covers an IP range toobe able tooconnect from your network.</span></span> <span data-ttu-id="18e9c-131">Hello siguiente ejemplo se utiliza [crear az postgres servidor regla de firewall](/cli/azure/postgres/server/firewall-rule#create) toocreate una regla de firewall `AllowAllIps` para una dirección IP, intervalo.</span><span class="sxs-lookup"><span data-stu-id="18e9c-131">hello following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) toocreate a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="18e9c-132">tooopen todas las direcciones IP, utilice 0.0.0.0 como Hola a partir de dirección IP y 255.255.255.255 como Hola dirección final.</span><span class="sxs-lookup"><span data-stu-id="18e9c-132">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="18e9c-133">El servidor Azure PostgreSQL se comunica a través de puerto 5432.</span><span class="sxs-lookup"><span data-stu-id="18e9c-133">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="18e9c-134">Al conectarse desde una red corporativa, es posible que el firewall de la red no permita el tráfico saliente a través del puerto 5432.</span><span class="sxs-lookup"><span data-stu-id="18e9c-134">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="18e9c-135">Tiene el departamento de TI abrir puerto 5432 tooconnect tooyour base de datos de Azure SQL server.</span><span class="sxs-lookup"><span data-stu-id="18e9c-135">Have your IT department open port 5432 tooconnect tooyour Azure SQL Database server.</span></span>

## <a name="get-hello-connection-information"></a><span data-ttu-id="18e9c-136">Obtener información de conexión de Hola</span><span class="sxs-lookup"><span data-stu-id="18e9c-136">Get hello connection information</span></span>

<span data-ttu-id="18e9c-137">tooconnect tooyour server, necesita credenciales de acceso y la información de host de tooprovide.</span><span class="sxs-lookup"><span data-stu-id="18e9c-137">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="18e9c-138">resultado de Hello es en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="18e9c-138">hello result is in JSON format.</span></span> <span data-ttu-id="18e9c-139">Tome nota de hello **Iniciodesesióndeadministrador** y **fullyQualifiedDomainName**.</span><span class="sxs-lookup"><span data-stu-id="18e9c-139">Make a note of hello **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
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

## <a name="connect-toopostgresql-database-using-psql"></a><span data-ttu-id="18e9c-140">Conectar la base de datos de tooPostgreSQL con psql</span><span class="sxs-lookup"><span data-stu-id="18e9c-140">Connect tooPostgreSQL database using psql</span></span>

<span data-ttu-id="18e9c-141">Si el equipo cliente tenga PostgreSQL instalado, puede usar una instancia local de [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooconnect tooan Azure PostgreSQL server.</span><span class="sxs-lookup"><span data-stu-id="18e9c-141">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooconnect tooan Azure PostgreSQL server.</span></span> <span data-ttu-id="18e9c-142">Vamos a usar ahora servidor de hello psql utilidad de línea de comandos tooconnect toohello PostgreSQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="18e9c-142">Let's now use hello psql command-line utility tooconnect toohello Azure PostgreSQL server.</span></span>

1. <span data-ttu-id="18e9c-143">Ejecute hello después psql comandos tooconnect tooan base de datos de Azure para servidor de PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="18e9c-143">Run hello following psql command tooconnect tooan Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="18e9c-144">Por ejemplo, hello siguiente comando conecta a base de datos de toohello predeterminada denominada **postgres** en el servidor de PostgreSQL **mypgserver 20170401.postgres.database.azure.com** utilizando las credenciales de acceso.</span><span class="sxs-lookup"><span data-stu-id="18e9c-144">For example, hello following command connects toohello default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="18e9c-145">Escriba hello `<server_admin_password>` elegido cuando se le solicite una contraseña.</span><span class="sxs-lookup"><span data-stu-id="18e9c-145">Enter hello `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
```

2.  <span data-ttu-id="18e9c-146">Una vez que esté conectado toohello server, cree una base de datos en blanco en el símbolo del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="18e9c-146">Once you are connected toohello server, create a blank database at hello prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="18e9c-147">En el símbolo del sistema de hello, ejecute hello después de la base de datos de comando tooswitch conexión toohello recién creado **mypgsqldb**:</span><span class="sxs-lookup"><span data-stu-id="18e9c-147">At hello prompt, execute hello following command tooswitch connection toohello newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="connect-toopostgresql-database-using-pgadmin"></a><span data-ttu-id="18e9c-148">Conectar la base de datos de tooPostgreSQL mediante pgAdmin</span><span class="sxs-lookup"><span data-stu-id="18e9c-148">Connect tooPostgreSQL database using pgAdmin</span></span>

<span data-ttu-id="18e9c-149">tooconnect tooAzure PostgreSQL server mediante la herramienta de interfaz gráfica de usuario de hello _pgAdmin_</span><span class="sxs-lookup"><span data-stu-id="18e9c-149">tooconnect tooAzure PostgreSQL server using hello GUI tool _pgAdmin_</span></span>
1.  <span data-ttu-id="18e9c-150">Iniciar hello _pgAdmin_ aplicación en el equipo cliente.</span><span class="sxs-lookup"><span data-stu-id="18e9c-150">Launch hello _pgAdmin_ application on your client computer.</span></span> <span data-ttu-id="18e9c-151">Puede instalar _pgAdmin_ desde http://www.pgadmin.org/.</span><span class="sxs-lookup"><span data-stu-id="18e9c-151">You can install _pgAdmin_ from http://www.pgadmin.org/.</span></span>
2.  <span data-ttu-id="18e9c-152">Elija **Agregar nuevo servidor** de hello **vínculos rápidos** menú.</span><span class="sxs-lookup"><span data-stu-id="18e9c-152">Choose **Add New Server** from hello **Quick Links** menu.</span></span>
3.  <span data-ttu-id="18e9c-153">Hola **crear - Server** cuadro de diálogo **General** ficha, escriba un nombre descriptivo único para el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="18e9c-153">In hello **Create - Server** dialog box **General** tab, enter a unique friendly Name for hello server.</span></span> <span data-ttu-id="18e9c-154">como **Azure PostgreSQL Server**.</span><span class="sxs-lookup"><span data-stu-id="18e9c-154">Say **Azure PostgreSQL Server**.</span></span>
 <span data-ttu-id="18e9c-155">![Herramienta pgAdmin: crear servidor](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span><span class="sxs-lookup"><span data-stu-id="18e9c-155">![pgAdmin tool - create - server](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span></span>
4.  <span data-ttu-id="18e9c-156">Hola **crear - Server** cuadro de diálogo, **conexión** ficha:</span><span class="sxs-lookup"><span data-stu-id="18e9c-156">In hello **Create - Server** dialog box, **Connection** tab:</span></span>
    - <span data-ttu-id="18e9c-157">Escriba el nombre del servidor de acceso completa de hello (por ejemplo, **mypgserver 20170401.postgres.database.azure.com**) en hello **nombre de Host / dirección** cuadro.</span><span class="sxs-lookup"><span data-stu-id="18e9c-157">Enter hello fully qualified server name (for example, **mypgserver-20170401.postgres.database.azure.com**) in hello **Host Name/ Address** box.</span></span> 
    - <span data-ttu-id="18e9c-158">Escriba el puerto 5432 en hello **puerto** cuadro.</span><span class="sxs-lookup"><span data-stu-id="18e9c-158">Enter port 5432 into hello **Port** box.</span></span> 
    - <span data-ttu-id="18e9c-159">Escriba hello **inicio de sesión de administrador de servidor (user@mypgserver)** obtenido anteriormente en este inicio rápido y la contraseña que especificó cuando creó el servidor hello en hello **nombre de usuario** y **contraseña** cuadros, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="18e9c-159">Enter hello **Server admin login (user@mypgserver)** obtained earlier in this quickstart and password you entered when you created hello server into hello **Username** and **Password** boxes, respectively.</span></span>
    - <span data-ttu-id="18e9c-160">Seleccione el **Modo SSL** como **Requerir**.</span><span class="sxs-lookup"><span data-stu-id="18e9c-160">Select **SSL Mode** as **Require**.</span></span> <span data-ttu-id="18e9c-161">De forma predeterminada, todos los servidores de Azure PostgreSQL se crean para que se EXIJA SSL.</span><span class="sxs-lookup"><span data-stu-id="18e9c-161">By default, all Azure PostgreSQL servers are created with SSL enforcing turned ON.</span></span> <span data-ttu-id="18e9c-162">tooturn desactivar exigir SSL, consulte los detalles en [exigir SSL](./concepts-ssl-connection-security.md).</span><span class="sxs-lookup"><span data-stu-id="18e9c-162">tooturn OFF SSL enforcing, see details in [Enforcing SSL](./concepts-ssl-connection-security.md).</span></span>

    ![pgAdmin: Crear servidor](./media/quickstart-create-server-database-azure-cli/2-pgadmin-create-server.png)
5.  <span data-ttu-id="18e9c-164">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="18e9c-164">Click **Save**.</span></span>
6.  <span data-ttu-id="18e9c-165">En el panel izquierdo del explorador de hello, expanda hello **grupos de servidores**.</span><span class="sxs-lookup"><span data-stu-id="18e9c-165">In hello Browser left pane, expand hello **Server Groups**.</span></span> <span data-ttu-id="18e9c-166">Seleccione su **servidor Azure PostgreSQL**.</span><span class="sxs-lookup"><span data-stu-id="18e9c-166">Choose your server **Azure PostgreSQL Server**.</span></span>
7.  <span data-ttu-id="18e9c-167">Elija hello **Server** conectado a y, a continuación, elija **bases de datos** en él.</span><span class="sxs-lookup"><span data-stu-id="18e9c-167">Choose hello **Server** you connected to, and then choose **Databases** under it.</span></span> 
8.  <span data-ttu-id="18e9c-168">Haga doble clic en **bases de datos** tooCreate una base de datos.</span><span class="sxs-lookup"><span data-stu-id="18e9c-168">Right-click on **Databases** tooCreate a Database.</span></span>
9.  <span data-ttu-id="18e9c-169">Elija un nombre de base de datos **mypgsqldb** y propietario de Hola para él como inicio de sesión de administrador de servidor **mylogin**.</span><span class="sxs-lookup"><span data-stu-id="18e9c-169">Choose a database name **mypgsqldb** and hello owner for it as server admin login **mylogin**.</span></span>
10. <span data-ttu-id="18e9c-170">Haga clic en **guardar** toocreate una base de datos en blanco.</span><span class="sxs-lookup"><span data-stu-id="18e9c-170">Click **Save** toocreate a blank database.</span></span>
11. <span data-ttu-id="18e9c-171">Hola **explorador**, expanda hello **servidores** grupo.</span><span class="sxs-lookup"><span data-stu-id="18e9c-171">In hello **Browser**, expand hello **Servers** group.</span></span> <span data-ttu-id="18e9c-172">Expanda servidor hello que ha creado y vea base de datos de hello **mypgsqldb** en él.</span><span class="sxs-lookup"><span data-stu-id="18e9c-172">Expand hello server you created, and see hello database **mypgsqldb** under it.</span></span>
 <span data-ttu-id="18e9c-173">![pgAdmin: Crear base de datos](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span><span class="sxs-lookup"><span data-stu-id="18e9c-173">![pgAdmin - Create - Database](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span></span>


## <a name="clean-up-resources"></a><span data-ttu-id="18e9c-174">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="18e9c-174">Clean up resources</span></span>

<span data-ttu-id="18e9c-175">Limpiar todos los recursos creados en Inicio rápido de hello eliminando hello [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="18e9c-175">Clean up all resources you created in hello quickstart by deleting hello [Azure resource group](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!TIP]
> <span data-ttu-id="18e9c-176">Otras guías de inicio rápido de esta colección se basan en los valores de esta.</span><span class="sxs-lookup"><span data-stu-id="18e9c-176">Other quickstarts in this collection build upon this quick start.</span></span> <span data-ttu-id="18e9c-177">Si tiene previsto toocontinue toowork con los siguientes tutoriales rápidos, realice la limpieza no Hola recursos creados en este tutorial rápido.</span><span class="sxs-lookup"><span data-stu-id="18e9c-177">If you plan toocontinue on toowork with subsequent quickstarts, do not clean up hello resources created in this quickstart.</span></span> <span data-ttu-id="18e9c-178">Si no tiene previsto toocontinue, use Hola siguiendo los pasos toodelete todos los recursos creados por este inicio rápido en hello CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="18e9c-178">If you do not plan toocontinue, use hello following steps toodelete all resources created by this quickstart in hello Azure CLI.</span></span>

```azurecli-interactive
az group delete --name myresourcegroup
```

<span data-ttu-id="18e9c-179">Si solo desea que servidor de toodelete Hola uno recién creado, puede ejecutar [eliminación del servidor postgres az](/cli/azure/postgres/server#delete) comando.</span><span class="sxs-lookup"><span data-stu-id="18e9c-179">If you just would like toodelete hello one newly created server, you can run [az postgres server delete](/cli/azure/postgres/server#delete) command.</span></span>
```azurecli-interactive
az postgres server delete --resource-group myresourcegroup --name mypgserver-20170401
```

## <a name="next-steps"></a><span data-ttu-id="18e9c-180">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="18e9c-180">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="18e9c-181">Migración de una base de datos mediante exportación e importación</span><span class="sxs-lookup"><span data-stu-id="18e9c-181">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
