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
# <a name="create-a-single-azure-sql-database-using-hello-azure-cli"></a><span data-ttu-id="489d2-104">Crear una base de datos de SQL Azure solo mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="489d2-104">Create a single Azure SQL database using hello Azure CLI</span></span>

<span data-ttu-id="489d2-105">Hola CLI de Azure es toocreate usado y administrar recursos de Azure desde la línea de comandos de Hola o en scripts.</span><span class="sxs-lookup"><span data-stu-id="489d2-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="489d2-106">Esta guía de detalles mediante hello Azure CLI toodeploy una base de datos de SQL Azure en un [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md) en un [servidor lógico de base de datos de SQL Azure](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="489d2-106">This guide details using hello Azure CLI toodeploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="489d2-107">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="489d2-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="489d2-108">Si elige tooinstall y usar hello CLI localmente, en este tema requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="489d2-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="489d2-109">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="489d2-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="489d2-110">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="489d2-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="define-variables"></a><span data-ttu-id="489d2-111">Definición de variables</span><span class="sxs-lookup"><span data-stu-id="489d2-111">Define variables</span></span>

<span data-ttu-id="489d2-112">Definir variables para su uso en scripts de hello en esta guía de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="489d2-112">Define variables for use in hello scripts in this quick start.</span></span>

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

## <a name="create-a-resource-group"></a><span data-ttu-id="489d2-113">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="489d2-113">Create a resource group</span></span>

<span data-ttu-id="489d2-114">Crear un [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md) con hello [crear grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="489d2-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="489d2-115">Un grupo de recursos es un contenedor lógico en el que se implementan y se administran recursos de Azure como un grupo.</span><span class="sxs-lookup"><span data-stu-id="489d2-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="489d2-116">Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en hello `westeurope` ubicación.</span><span class="sxs-lookup"><span data-stu-id="489d2-116">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location.</span></span>

```azurecli-interactive
az group create --name $resourcegroupname --location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="489d2-117">un servidor lógico</span><span class="sxs-lookup"><span data-stu-id="489d2-117">Create a logical server</span></span>

<span data-ttu-id="489d2-118">Crear un [servidor lógico de base de datos de SQL Azure](sql-database-features.md) con hello [az sql server crear](/cli/azure/sql/server#create) comando.</span><span class="sxs-lookup"><span data-stu-id="489d2-118">Create an [Azure SQL Database logical server](sql-database-features.md) using hello [az sql server create](/cli/azure/sql/server#create) command.</span></span> <span data-ttu-id="489d2-119">Un servidor lógico contiene un conjunto de bases de datos administradas como un grupo.</span><span class="sxs-lookup"><span data-stu-id="489d2-119">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="489d2-120">Hello en el ejemplo siguiente se crea un servidor de forma aleatoria con nombre en el grupo de recursos con un inicio de sesión de administración denominado `ServerAdmin` y una contraseña de `ChangeYourAdminPassword1`.</span><span class="sxs-lookup"><span data-stu-id="489d2-120">hello following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="489d2-121">Cambie estos valores predefinidos por los que prefiera.</span><span class="sxs-lookup"><span data-stu-id="489d2-121">Replace these pre-defined values as desired.</span></span>

```azurecli-interactive
az sql server create --name $servername --resource-group $resourcegroupname --location $location \
    --admin-user $adminlogin --admin-password $password
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="489d2-122">Configuración de una regla de firewall del servidor</span><span class="sxs-lookup"><span data-stu-id="489d2-122">Configure a server firewall rule</span></span>

<span data-ttu-id="489d2-123">Crear un [regla de firewall de nivel de servidor de base de datos de SQL Azure](sql-database-firewall-configure.md) con hello [az sql server crea](/cli/azure/sql/server/firewall-rule#create) comando.</span><span class="sxs-lookup"><span data-stu-id="489d2-123">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using hello [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create) command.</span></span> <span data-ttu-id="489d2-124">Una regla de firewall de nivel de servidor permite que una aplicación externa, como SQL Server Management Studio o hello SQLCMD utilidad tooconnect tooa base de datos SQL a través de firewall de servicio de base de datos SQL de Hola.</span><span class="sxs-lookup"><span data-stu-id="489d2-124">A server-level firewall rule allows an external application, such as SQL Server Management Studio or hello SQLCMD utility tooconnect tooa SQL database through hello SQL Database service firewall.</span></span> <span data-ttu-id="489d2-125">En el siguiente ejemplo de Hola, solo se abrirá el firewall de Hola para otros recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="489d2-125">In hello following example, hello firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="489d2-126">tooenable conectividad externa, cambio Hola IP dirección tooan dirección adecuada para su entorno.</span><span class="sxs-lookup"><span data-stu-id="489d2-126">tooenable external connectivity, change hello IP address tooan appropriate address for your environment.</span></span> <span data-ttu-id="489d2-127">tooopen todas las direcciones IP, utilice 0.0.0.0 como Hola a partir de dirección IP y 255.255.255.255 como Hola dirección final.</span><span class="sxs-lookup"><span data-stu-id="489d2-127">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>  

```azurecli-interactive
az sql server firewall-rule create --resource-group $resourcegroupname --server $servername \
    -n AllowYourIp --start-ip-address $startip --end-ip-address $endip
```

> [!NOTE]
> <span data-ttu-id="489d2-128">SQL Database se comunica a través del puerto 1433.</span><span class="sxs-lookup"><span data-stu-id="489d2-128">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="489d2-129">Si está tratando de tooconnect desde dentro de una red corporativa, es posible que firewall de su red no permite el tráfico saliente en el puerto 1433.</span><span class="sxs-lookup"><span data-stu-id="489d2-129">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="489d2-130">Si es así, no será capaz de tooconnect tooyour base de datos de SQL Azure servidor a menos que el departamento de TI abre el puerto 1433.</span><span class="sxs-lookup"><span data-stu-id="489d2-130">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a><span data-ttu-id="489d2-131">Crear una base de datos en el servidor de hello con datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="489d2-131">Create a database in hello server with sample data</span></span>

<span data-ttu-id="489d2-132">Crear una base de datos con un [nivel de rendimiento S0](sql-database-service-tiers.md) en servidor de hello mediante Hola [crear base de datos de sql az](/cli/azure/sql/db#create) comando.</span><span class="sxs-lookup"><span data-stu-id="489d2-132">Create a database with an [S0 performance level](sql-database-service-tiers.md) in hello server using hello [az sql db create](/cli/azure/sql/db#create) command.</span></span> <span data-ttu-id="489d2-133">Hello en el ejemplo siguiente se crea una base de datos denominada `mySampleDatabase` y carga Hola datos de ejemplo AdventureWorksLT en esta base de datos.</span><span class="sxs-lookup"><span data-stu-id="489d2-133">hello following example creates a database called `mySampleDatabase` and loads hello AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="489d2-134">Reemplazar predefinidos de estos valores según sea necesario (otras guías rápidas en esta colección se basan en valores de hello en esta guía de inicio rápido).</span><span class="sxs-lookup"><span data-stu-id="489d2-134">Replace these predefined values as desired (other quick starts in this collection build upon hello values in this quick start).</span></span>

```azurecli-interactive
az sql db create --resource-group $resourcegroupname --server $servername \
    --name $databasename --sample-name AdventureWorksLT --service-objective S0
```

## <a name="clean-up-resources"></a><span data-ttu-id="489d2-135">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="489d2-135">Clean up resources</span></span>

<span data-ttu-id="489d2-136">Otras guías de inicio rápido de esta colección se basan en los valores de esta.</span><span class="sxs-lookup"><span data-stu-id="489d2-136">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="489d2-137">Si tiene previsto toocontinue toowork con guías rápidas posteriores, no limpiar los recursos de hello creados en esta rápida se inician.</span><span class="sxs-lookup"><span data-stu-id="489d2-137">If you plan toocontinue on toowork with subsequent quick starts, do not clean up hello resources created in this quick start.</span></span> <span data-ttu-id="489d2-138">Si no tiene previsto toocontinue, use Hola seguido toodelete pasos creado todos los recursos de esta guía de inicio rápido en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="489d2-138">If you do not plan toocontinue, use hello following steps toodelete all resources created by this quick start in hello Azure portal.</span></span>
>

```azurecli-interactive
az group delete --name $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="489d2-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="489d2-139">Next steps</span></span>

<span data-ttu-id="489d2-140">Ahora que tiene una base de datos, puede conectarse y realizar consultas con las herramientas que desee.</span><span class="sxs-lookup"><span data-stu-id="489d2-140">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="489d2-141">Para más información, seleccione una de las herramientas siguientes:</span><span class="sxs-lookup"><span data-stu-id="489d2-141">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="489d2-142">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="489d2-142">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="489d2-143">código de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="489d2-143">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="489d2-144">.NET</span><span class="sxs-lookup"><span data-stu-id="489d2-144">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="489d2-145">PHP</span><span class="sxs-lookup"><span data-stu-id="489d2-145">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="489d2-146">Node.js</span><span class="sxs-lookup"><span data-stu-id="489d2-146">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="489d2-147">Java</span><span class="sxs-lookup"><span data-stu-id="489d2-147">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="489d2-148">Python</span><span class="sxs-lookup"><span data-stu-id="489d2-148">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="489d2-149">Ruby</span><span class="sxs-lookup"><span data-stu-id="489d2-149">Ruby</span></span>](sql-database-connect-query-ruby.md)

