---
title: "una solución de base de datos de SQL Azure distribuidos geográficamente aaaImplement | Documentos de Microsoft"
description: "Obtenga información acerca de tooconfigure la base de datos de SQL Azure y la aplicación para tooa de conmutación por error replica la base de datos y probar la conmutación por error."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/26/2017
ms.author: carlrab
ms.openlocfilehash: 9295d33c669405108a1a64ef1e7cb77f582773a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="implement-a-geo-distributed-database"></a><span data-ttu-id="9a9d2-103">Implementar una base de datos distribuida geográficamente</span><span class="sxs-lookup"><span data-stu-id="9a9d2-103">Implement a geo-distributed database</span></span>

<span data-ttu-id="9a9d2-104">En este tutorial, configurar una base de datos SQL de Azure y la aplicación para la región de conmutación por error tooa remoto y, a continuación, pruebe el plan de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-104">In this tutorial, you configure an Azure SQL database and application for failover tooa remote region, and then test your failover plan.</span></span> <span data-ttu-id="9a9d2-105">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="9a9d2-105">You learn how to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="9a9d2-106">Crear usuarios de base de datos y concederles permisos</span><span class="sxs-lookup"><span data-stu-id="9a9d2-106">Create database users and grant them permissions</span></span>
> * <span data-ttu-id="9a9d2-107">Configurar una regla de firewall de nivel de base de datos</span><span class="sxs-lookup"><span data-stu-id="9a9d2-107">Set up a database-level firewall rule</span></span>
> * <span data-ttu-id="9a9d2-108">Crear un [grupo de conmutación por error de replicación geográfica](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="9a9d2-108">Create a [geo-replication failover group](sql-database-geo-replication-overview.md)</span></span>
> * <span data-ttu-id="9a9d2-109">Crear y compilar un tooquery de aplicación de Java una base de datos de SQL Azure</span><span class="sxs-lookup"><span data-stu-id="9a9d2-109">Create and compile a Java application tooquery an Azure SQL database</span></span>
> * <span data-ttu-id="9a9d2-110">Obtener detalles de recuperación ante desastres</span><span class="sxs-lookup"><span data-stu-id="9a9d2-110">Perform a disaster recovery drill</span></span>

<span data-ttu-id="9a9d2-111">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-111">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="9a9d2-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9a9d2-112">Prerequisites</span></span>

<span data-ttu-id="9a9d2-113">toocomplete se ha completado este tutorial, asegúrese de hello seguro después de requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="9a9d2-113">toocomplete this tutorial, make sure hello following prerequisites are completed:</span></span>

- <span data-ttu-id="9a9d2-114">Hola instalada más reciente [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="9a9d2-114">Installed hello latest [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs).</span></span> 
- <span data-ttu-id="9a9d2-115">Instancia de Azure SQL Database instalada.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-115">Installed an Azure SQL database.</span></span> <span data-ttu-id="9a9d2-116">Este tutorial usa con un nombre de base de datos de ejemplo de Hola AdventureWorksLT **mySampleDatabase** de una de estas guías de inicio rápidos:</span><span class="sxs-lookup"><span data-stu-id="9a9d2-116">This tutorial uses hello AdventureWorksLT sample database with a name of **mySampleDatabase** from one of these quick starts:</span></span>

   - [<span data-ttu-id="9a9d2-117">Creación de la base de datos: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9a9d2-117">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="9a9d2-118">Creación de la base de datos: CLI</span><span class="sxs-lookup"><span data-stu-id="9a9d2-118">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="9a9d2-119">Creación de la base de datos: PowerShell</span><span class="sxs-lookup"><span data-stu-id="9a9d2-119">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="9a9d2-120">Ha identificado una tooexecute método SQL secuencias de comandos en la base de datos, puede usar uno de hello siguientes herramientas de consulta:</span><span class="sxs-lookup"><span data-stu-id="9a9d2-120">Have identified a method tooexecute SQL scripts against your database, you can use one of hello following query tools:</span></span>
   - <span data-ttu-id="9a9d2-121">editor de consultas de Hola Hola [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9a9d2-121">hello query editor in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9a9d2-122">Para obtener más información sobre cómo utilizar el editor de consultas de hello en hello portal de Azure, consulte [conectar y consulta mediante el Editor de consultas](sql-database-get-started-portal.md#query-the-sql-database).</span><span class="sxs-lookup"><span data-stu-id="9a9d2-122">For more information on using hello query editor in hello Azure portal, see [Connect and query using Query Editor](sql-database-get-started-portal.md#query-the-sql-database).</span></span>
   - <span data-ttu-id="9a9d2-123">versión más reciente de Hola de [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), que es un entorno integrado para administrar cualquier infraestructura SQL, desde SQL Server tooSQL base de datos de Microsoft Windows.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-123">hello newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), which is an integrated environment for managing any SQL infrastructure, from SQL Server tooSQL Database for Microsoft Windows.</span></span>
   - <span data-ttu-id="9a9d2-124">versión más reciente de Hola de [código de Visual Studio](https://code.visualstudio.com/docs), que es un editor de código gráfica para Linux, Mac OS, y Windows que admita extensiones, incluidas Hola [mssql extensión](https://aka.ms/mssql-marketplace) para realizar consultas en Microsoft SQL Server , Base de datos SQL azure y almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-124">hello newest version of [Visual Studio Code](https://code.visualstudio.com/docs), which is a graphical code editor for Linux, macOS, and Windows that supports extensions, including hello [mssql extension](https://aka.ms/mssql-marketplace) for querying Microsoft SQL Server, Azure SQL Database, and SQL Data Warehouse.</span></span> <span data-ttu-id="9a9d2-125">Para más información sobre el empleo de esta herramienta con Azure SQL Database, vea [Connect and query with VS Code](sql-database-connect-query-vscode.md) (Conectar y consultar con VS Code).</span><span class="sxs-lookup"><span data-stu-id="9a9d2-125">For more information on using this tool with Azure SQL Database, see [Connect and query with VS Code](sql-database-connect-query-vscode.md).</span></span> 

## <a name="create-database-users-and-grant-permissions"></a><span data-ttu-id="9a9d2-126">Crear usuarios de base de datos y concederles permisos</span><span class="sxs-lookup"><span data-stu-id="9a9d2-126">Create database users and grant permissions</span></span>

<span data-ttu-id="9a9d2-127">Conectar tooyour base de datos y crear cuentas de usuario mediante uno de hello siguientes herramientas de consulta:</span><span class="sxs-lookup"><span data-stu-id="9a9d2-127">Connect tooyour database and create user accounts using one of hello following query tools:</span></span>

- <span data-ttu-id="9a9d2-128">editor de consultas de Hola Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9a9d2-128">hello Query editor in hello Azure portal</span></span>
- <span data-ttu-id="9a9d2-129">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="9a9d2-129">SQL Server Management Studio</span></span>
- <span data-ttu-id="9a9d2-130">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="9a9d2-130">Visual Studio Code</span></span>

<span data-ttu-id="9a9d2-131">Estas cuentas de usuario automáticamente replican servidor secundario tooyour (y mantenerse sincronizado).</span><span class="sxs-lookup"><span data-stu-id="9a9d2-131">These user accounts replicate automatically tooyour secondary server (and be kept in sync).</span></span> <span data-ttu-id="9a9d2-132">toouse SQL Server Management Studio o código de Visual Studio, deberá tooconfigure una regla de firewall que se conecta desde un cliente en una dirección IP para el que todavía no se ha configurado un servidor de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-132">toouse SQL Server Management Studio or Visual Studio Code, you may need tooconfigure a firewall rule if you are connecting from a client at an IP address for which you have not yet configured a firewall.</span></span> <span data-ttu-id="9a9d2-133">Para consultar los pasos detallados, vea [Create a server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) (Crear una regla de firewall de nivel de servidor).</span><span class="sxs-lookup"><span data-stu-id="9a9d2-133">For detailed steps, see [Create a server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span>

- <span data-ttu-id="9a9d2-134">En una ventana de consulta, ejecute hello después consulta toocreate dos cuentas de usuario en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-134">In a query window, execute hello following query toocreate two user accounts in your database.</span></span> <span data-ttu-id="9a9d2-135">Esta secuencia de comandos concede **db_owner** permisos toohello **app_admin** cuenta y concede **seleccione** y **actualización** toohello de permisos **app_user** cuenta.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-135">This script grants **db_owner** permissions toohello **app_admin** account and grants **SELECT** and **UPDATE** permissions toohello **app_user** account.</span></span> 

   ```sql
   CREATE USER app_admin WITH PASSWORD = 'ChangeYourPassword1';
   --Add SQL user toodb_owner role
   ALTER ROLE db_owner ADD MEMBER app_admin; 
   --Create additional SQL user
   CREATE USER app_user WITH PASSWORD = 'ChangeYourPassword1';
   --grant permission tooSalesLT schema
   GRANT SELECT, INSERT, DELETE, UPDATE ON SalesLT.Product tooapp_user;
   ```

## <a name="create-database-level-firewall"></a><span data-ttu-id="9a9d2-136">Creación de firewall de nivel de base de datos</span><span class="sxs-lookup"><span data-stu-id="9a9d2-136">Create database-level firewall</span></span>

<span data-ttu-id="9a9d2-137">Cree una [regla de firewall de nivel de base de datos](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) para la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-137">Create a [database-level firewall rule](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) for your SQL database.</span></span> <span data-ttu-id="9a9d2-138">Esta regla de firewall de nivel de base de datos replica automáticamente toohello servidor secundario que creará en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-138">This database-level firewall rule replicates automatically toohello secondary server that you create in this tutorial.</span></span> <span data-ttu-id="9a9d2-139">Para simplificar el trabajo (en este tutorial), utilice Hola de dirección IP pública del equipo de hello en el que se va a realizar pasos de hello en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-139">For simplicity (in this tutorial), use hello public IP address of hello computer on which you are performing hello steps in this tutorial.</span></span> <span data-ttu-id="9a9d2-140">dirección IP de hello toodetermine utilizada para la regla de firewall de nivel de servidor de hello para el equipo actual, vea [crear un firewall de nivel de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="9a9d2-140">toodetermine hello IP address used for hello server-level firewall rule for your current computer, see [Create a server-level firewall](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span>  

- <span data-ttu-id="9a9d2-141">En la ventana de consulta abierta, reemplace consulta anterior Hola con hello después de consulta, reemplazando las direcciones IP Hola con las direcciones IP de hello adecuadas para su entorno.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-141">In your open query window, replace hello previous query with hello following query, replacing hello IP addresses with hello appropriate IP addresses for your environment.</span></span>  

   ```sql
   -- Create database-level firewall setting for your public IP address
   EXECUTE sp_set_database_firewall_rule @name = N'myGeoReplicationFirewallRule',@start_ip_address = '0.0.0.0', @end_ip_address = '0.0.0.0';
   ```

## <a name="create-an-active-geo-replication-auto-failover-group"></a><span data-ttu-id="9a9d2-142">Crear un grupo de conmutación por error automático de replicación geográfica activa</span><span class="sxs-lookup"><span data-stu-id="9a9d2-142">Create an active geo-replication auto failover group</span></span> 

<span data-ttu-id="9a9d2-143">Uso de PowerShell de Azure, cree un [grupo de conmutación por error de replicación geográfica activa automáticamente](sql-database-geo-replication-overview.md) entre el servidor de SQL Azure y la nueva Hola existente vacío de servidor de SQL Azure en una región de Azure y, a continuación, agregue el grupo de conmutación por error de toohello de base de datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-143">Using Azure PowerShell, create an [active geo-replication auto failover group](sql-database-geo-replication-overview.md) between your existing Azure SQL server and hello new empty Azure SQL server in an Azure region, and then add your sample database toohello failover group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9a9d2-144">Estos cmdlets necesitan Azure PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-144">These cmdlets require Azure PowerShell 4.0.</span></span> [!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install-no-ssh.md)]
>

1. <span data-ttu-id="9a9d2-145">Rellenar las variables para los scripts de PowerShell con valores de hello para el servidor existente y la base de datos de ejemplo y proporcionar un valor único global para el nombre del grupo de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-145">Populate variables for your PowerShell scripts using hello values for your existing server and sample database, and provide a globally unique value for failover group name.</span></span>

   ```powershell
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   $myresourcegroupname = "<your resource group name>"
   $mylocation = "<your resource group location>"
   $myservername = "<your existing server name>"
   $mydatabasename = "mySampleDatabase"
   $mydrlocation = "<your disaster recovery location>"
   $mydrservername = "<your disaster recovery server name>"
   $myfailovergroupname = "<your unique failover group name>"
   ```

2. <span data-ttu-id="9a9d2-146">Cree un servidor de copia de seguridad vacío en la región de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-146">Create an empty backup server in your failover region.</span></span>

   ```powershell
   $mydrserver = New-AzureRmSqlServer -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername `
      -Location $mydrlocation `
      -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   $mydrserver   
   ```

3. <span data-ttu-id="9a9d2-147">Crear un grupo de conmutación por error entre dos servidores de Hola.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-147">Create a failover group between hello two servers.</span></span>

   ```powershell
   $myfailovergroup = New-AzureRMSqlDatabaseFailoverGroup `
      –ResourceGroupName $myresourcegroupname `
      -ServerName $myservername `
      -PartnerServerName $mydrservername  `
      –FailoverGroupName $myfailovergroupname `
      –FailoverPolicy Automatic `
      -GracePeriodWithDataLossHours 2
   $myfailovergroup   
   ```

4. <span data-ttu-id="9a9d2-148">Agregue el grupo de conmutación por error de toohello de base de datos.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-148">Add your database toohello failover group.</span></span>

   ```powershell
   $myfailovergroup = Get-AzureRmSqlDatabase `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $myservername `
      -DatabaseName $mydatabasename | `
    Add-AzureRmSqlDatabaseToFailoverGroup `
      -ResourceGroupName $myresourcegroupname ` `
      -ServerName $myservername `
      -FailoverGroupName $myfailovergroupname
   $myfailovergroup   
   ```

## <a name="install-java-software"></a><span data-ttu-id="9a9d2-149">Instalación del software de Java</span><span class="sxs-lookup"><span data-stu-id="9a9d2-149">Install Java software</span></span>

<span data-ttu-id="9a9d2-150">Hola pasos de esta sección se supone que está familiarizado con el desarrollo de Java de uso y están tooworking nueva con la base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-150">hello steps in this section assume that you are familiar with developing using Java and are new tooworking with Azure SQL Database.</span></span> 

### <a name="mac-os"></a><span data-ttu-id="9a9d2-151">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="9a9d2-151">**Mac OS**</span></span>
<span data-ttu-id="9a9d2-152">Abra su terminal y desplácese directorio tooa donde tiene previsto crear el proyecto de Java.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-152">Open your terminal and navigate tooa directory where you plan on creating your Java project.</span></span> <span data-ttu-id="9a9d2-153">Instalar **brew** y **Maven** escribiendo Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="9a9d2-153">Install **brew** and **Maven** by entering hello following commands:</span></span> 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install maven
```

<span data-ttu-id="9a9d2-154">Para obtener instrucciones detalladas sobre cómo instalar y configurar el entorno de Java y Maven, vaya hello [compilar una aplicación mediante SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), seleccione **Java**, seleccione **MacOS**y, a continuación, siga Hola instrucciones detalladas para configurar Java y Maven en el paso 1.2 y 1.3.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-154">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select **MacOS**, and then follow hello detailed instructions for configuring Java and Maven in step 1.2 and 1.3.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="9a9d2-155">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="9a9d2-155">**Linux (Ubuntu)**</span></span>
<span data-ttu-id="9a9d2-156">Abra su terminal y desplácese directorio tooa donde tiene previsto crear el proyecto de Java.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-156">Open your terminal and navigate tooa directory where you plan on creating your Java project.</span></span> <span data-ttu-id="9a9d2-157">Instalar **Maven** escribiendo Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="9a9d2-157">Install **Maven** by entering hello following commands:</span></span>

```bash
sudo apt-get install maven
```

<span data-ttu-id="9a9d2-158">Para obtener instrucciones detalladas sobre cómo instalar y configurar el entorno de Java y Maven, vaya hello [compilar una aplicación mediante SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), seleccione **Java**, seleccione **Ubuntu**y, a continuación, siga Hola instrucciones detalladas para configurar Java y Maven en el paso 1.2, 1.3 y 1.4.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-158">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select **Ubuntu**, and then follow hello detailed instructions for configuring Java and Maven in step 1.2, 1.3, and 1.4.</span></span>

### <a name="windows"></a><span data-ttu-id="9a9d2-159">**Windows**</span><span class="sxs-lookup"><span data-stu-id="9a9d2-159">**Windows**</span></span>
<span data-ttu-id="9a9d2-160">Instalar [Maven](https://maven.apache.org/download.cgi) con instalador oficial de Hola.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-160">Install [Maven](https://maven.apache.org/download.cgi) using hello official installer.</span></span> <span data-ttu-id="9a9d2-161">Utilice a Maven toohelp administrar dependencias, compilar, probar y ejecutar el proyecto de Java.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-161">Use Maven toohelp manage dependencies, build, test, and run your Java project.</span></span> <span data-ttu-id="9a9d2-162">Para obtener instrucciones detalladas sobre cómo instalar y configurar el entorno de Java y Maven, vaya hello [compilar una aplicación mediante SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), seleccione **Java**, seleccione Windows y, a continuación, siga Hola instrucciones detalladas para configuración de Java y Maven en el paso 1.2 y 1.3.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-162">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select Windows, and then follow hello detailed instructions for configuring Java and Maven in step 1.2 and 1.3.</span></span>

## <a name="create-sqldbsample-project"></a><span data-ttu-id="9a9d2-163">Crear proyecto SqlDbSample</span><span class="sxs-lookup"><span data-stu-id="9a9d2-163">Create SqlDbSample project</span></span>

1. <span data-ttu-id="9a9d2-164">En la consola de comandos de hello (por ejemplo, intensiva de errores), cree un proyecto de Maven.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-164">In hello command console (such as Bash), create a Maven project.</span></span> 
   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=SqlDbSample" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```
2. <span data-ttu-id="9a9d2-165">Escriba **Y** y haga clic en **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-165">Type **Y** and click **Enter**.</span></span>
3. <span data-ttu-id="9a9d2-166">Cambie el directorio al proyecto recién creado.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-166">Change directories into your newly created project.</span></span>

   ```bash
   cd SqlDbSamples
   ```

4. <span data-ttu-id="9a9d2-167">Con su editor favorito, abra el archivo pom.xml de hello en la carpeta del proyecto.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-167">Using your favorite editor, open hello pom.xml file in your project folder.</span></span> 

5. <span data-ttu-id="9a9d2-168">Agregar hello controlador JDBC de Microsoft para proyectos de Maven de tooyour de dependencia de SQL Server, abra el editor de texto y copiar y pegar Hola siguiendo las líneas en el archivo pom.xml.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-168">Add hello Microsoft JDBC Driver for SQL Server dependency tooyour Maven project by opening your favorite text editor and copying and pasting hello following lines into your pom.xml file.</span></span> <span data-ttu-id="9a9d2-169">No sobrescribir los valores existentes de hello rellenados en el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-169">Do not overwrite hello existing values prepopulated in hello file.</span></span> <span data-ttu-id="9a9d2-170">Hola dependencia JDBC se debe pegar dentro de hello sección "dependencias" más grande ().</span><span class="sxs-lookup"><span data-stu-id="9a9d2-170">hello JDBC dependency must be pasted within hello larger “dependencies” section ( ).</span></span>   

   ```xml
   <dependency>
     <groupId>com.microsoft.sqlserver</groupId>
     <artifactId>mssql-jdbc</artifactId>
    <version>6.1.0.jre8</version>
   </dependency>
   ```

6. <span data-ttu-id="9a9d2-171">Especificar versión de Hola del proyecto de Java toocompile hello en agregando Hola después de sección "propiedades" en el archivo de hello pom.xml después de la sección "dependencias" de Hola.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-171">Specify hello version of Java toocompile hello project against by adding hello following “properties” section into hello pom.xml file after hello "dependencies" section.</span></span> 

   ```xml
   <properties>
     <maven.compiler.source>1.8</maven.compiler.source>
     <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```
7. <span data-ttu-id="9a9d2-172">Agregar siguiente Hola "crear" sección en el archivo de hello pom.xml después de hello "propiedades" sección toosupport archivos de manifiesto en archivos JAR.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-172">Add hello following "build" section into hello pom.xml file after hello "properties" section toosupport manifest files in jars.</span></span>       

   ```xml
   <build>
     <plugins>
       <plugin>
         <groupId>org.apache.maven.plugins</groupId>
         <artifactId>maven-jar-plugin</artifactId>
         <version>3.0.0</version>
         <configuration>
           <archive>
             <manifest>
               <mainClass>com.sqldbsamples.App</mainClass>
             </manifest>
           </archive>
        </configuration>
       </plugin>
     </plugins>
   </build>
   ```
8. <span data-ttu-id="9a9d2-173">Guarde y cierre el archivo de hello pom.xml.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-173">Save and close hello pom.xml file.</span></span>
9. <span data-ttu-id="9a9d2-174">Abra el archivo de hello App.java (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) y reemplace el contenido de hello con hello después de contenido.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-174">Open hello App.java file (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) and replace hello contents with hello following contents.</span></span> <span data-ttu-id="9a9d2-175">Sustituir el nombre de grupo de conmutación por error de Hola por hello para el grupo de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-175">Replace hello failover group name with hello name for your failover group.</span></span> <span data-ttu-id="9a9d2-176">Si han cambiado los valores de hello para el nombre de la base de datos de hello, usuario o contraseña, cambie también esos valores.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-176">If you have changed hello values for hello database name, user, or password, change those values as well.</span></span>

   ```java
   package com.sqldbsamples;

   import java.sql.Connection;
   import java.sql.Statement;
   import java.sql.PreparedStatement;
   import java.sql.ResultSet;
   import java.sql.Timestamp;
   import java.sql.DriverManager;
   import java.util.Date;
   import java.util.concurrent.TimeUnit;

   public class App {

      private static final String FAILOVER_GROUP_NAME = "myfailovergroupname";
  
      private static final String DB_NAME = "mySampleDatabase";
      private static final String USER = "app_user";
      private static final String PASSWORD = "ChangeYourPassword1";

      private static final String READ_WRITE_URL = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", FAILOVER_GROUP_NAME, DB_NAME, USER, PASSWORD);
      private static final String READ_ONLY_URL = String.format("jdbc:sqlserver://%s.secondary.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", FAILOVER_GROUP_NAME, DB_NAME, USER, PASSWORD);

      public static void main(String[] args) {
         System.out.println("#######################################");
         System.out.println("## GEO DISTRIBUTED DATABASE TUTORIAL ##");
         System.out.println("#######################################");
         System.out.println(""); 

         int highWaterMark = getHighWaterMarkId();

         try {
            for(int i = 1; i < 1000; i++) {
                //  loop will run for about 1 hour
                System.out.print(i + ": insert on primary " + (insertData((highWaterMark + i))?"successful":"failed"));
                TimeUnit.SECONDS.sleep(1);
                System.out.print(", read from secondary " + (selectData((highWaterMark + i))?"successful":"failed") + "\n");
                TimeUnit.SECONDS.sleep(3);
            }
         } catch(Exception e) {
            e.printStackTrace();
      }
   }

   private static boolean insertData(int id) {
      // Insert data into hello product table with a unique product name that we can use toofind hello product again later
      String sql = "INSERT INTO SalesLT.Product (Name, ProductNumber, Color, StandardCost, ListPrice, SellStartDate) VALUES (?,?,?,?,?,?);";

      try (Connection connection = DriverManager.getConnection(READ_WRITE_URL); 
              PreparedStatement pstmt = connection.prepareStatement(sql)) {
         pstmt.setString(1, "BrandNewProduct" + id);
         pstmt.setInt(2, 200989 + id + 10000);
         pstmt.setString(3, "Blue");
         pstmt.setDouble(4, 75.00);
         pstmt.setDouble(5, 89.99);
         pstmt.setTimestamp(6, new Timestamp(new Date().getTime()));
         return (1 == pstmt.executeUpdate());
      } catch (Exception e) {
         return false;
      }
   }

   private static boolean selectData(int id) {
      // Query hello data that was previously inserted into hello primary database from hello geo replicated database
      String sql = "SELECT Name, Color, ListPrice FROM SalesLT.Product WHERE Name = ?";

      try (Connection connection = DriverManager.getConnection(READ_ONLY_URL); 
              PreparedStatement pstmt = connection.prepareStatement(sql)) {
         pstmt.setString(1, "BrandNewProduct" + id);
         try (ResultSet resultSet = pstmt.executeQuery()) {
            return resultSet.next();
         }
      } catch (Exception e) {
         return false;
      }
   }

   private static int getHighWaterMarkId() {
      // Query hello high water mark id that is stored in hello table toobe able toomake unique inserts 
      String sql = "SELECT MAX(ProductId) FROM SalesLT.Product";
      int result = 1;
        
      try (Connection connection = DriverManager.getConnection(READ_WRITE_URL); 
              Statement stmt = connection.createStatement();
              ResultSet resultSet = stmt.executeQuery(sql)) {
         if (resultSet.next()) {
             result =  resultSet.getInt(1);
            }
         } catch (Exception e) {
          e.printStackTrace();
         }
         return result;
      }
   }
   ```
6. <span data-ttu-id="9a9d2-177">Guarde y cierre el archivo de hello App.java.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-177">Save and close hello App.java file.</span></span>

## <a name="compile-and-run-hello-sqldbsample-project"></a><span data-ttu-id="9a9d2-178">Compilar y ejecutar el proyecto de hello SqlDbSample</span><span class="sxs-lookup"><span data-stu-id="9a9d2-178">Compile and run hello SqlDbSample project</span></span>

1. <span data-ttu-id="9a9d2-179">En la consola de comandos de hello, ejecute el comando de toofollowing.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-179">In hello command console, execute toofollowing command.</span></span>

   ```bash
   mvn package
   ```
2. <span data-ttu-id="9a9d2-180">Cuando termine, ejecute hello tras la aplicación de hello toorun comando (se ejecuta durante aproximadamente 1 hora a menos que detenga manualmente):</span><span class="sxs-lookup"><span data-stu-id="9a9d2-180">When finished, execute hello following command toorun hello application (it runs for about 1 hour unless you stop it manually):</span></span>

   ```bash
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   
   #######################################
   ## GEO DISTRIBUTED DATABASE TUTORIAL ##
   #######################################

   1. insert on primary successful, read from secondary successful
   2. insert on primary successful, read from secondary successful
   3. insert on primary successful, read from secondary successful
   ```

## <a name="perform-disaster-recovery-drill"></a><span data-ttu-id="9a9d2-181">Obtener detalles de recuperación ante desastres</span><span class="sxs-lookup"><span data-stu-id="9a9d2-181">Perform disaster recovery drill</span></span>

1. <span data-ttu-id="9a9d2-182">Llame a la conmutación por error manual del grupo de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-182">Call manual failover of failover group.</span></span> 

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $mydrservername `
   -FailoverGroupName $myfailovergroupname
   ```

2. <span data-ttu-id="9a9d2-183">Observar Hola resultados de la aplicación durante la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-183">Observe hello application results during failover.</span></span> <span data-ttu-id="9a9d2-184">Se producirá un error en algunos inserciones mientras actualiza Hola memoria caché de DNS.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-184">Some inserts fail while hello DNS cache refreshes.</span></span>     

3. <span data-ttu-id="9a9d2-185">Averigüe qué rol realiza el servidor de recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-185">Find out which role your disaster recovery server is performing.</span></span>

   ```powershell
   $mydrserver.ReplicationRole
   ```

4. <span data-ttu-id="9a9d2-186">Conmutación por recuperación.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-186">Failback.</span></span>

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $myservername `
   -FailoverGroupName $myfailovergroupname
   ```

5. <span data-ttu-id="9a9d2-187">Observar Hola resultados de la aplicación durante la conmutación por recuperación.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-187">Observe hello application results during failback.</span></span> <span data-ttu-id="9a9d2-188">Se producirá un error en algunos inserciones mientras actualiza Hola memoria caché de DNS.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-188">Some inserts fail while hello DNS cache refreshes.</span></span>     

6. <span data-ttu-id="9a9d2-189">Averigüe qué rol realiza el servidor de recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="9a9d2-189">Find out which role your disaster recovery server is performing.</span></span>

   ```powershell
   $fileovergroup = Get-AzureRMSqlDatabaseFailoverGroup `
      -FailoverGroupName $myfailovergroupname `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername
   $fileovergroup.ReplicationRole
   ```
## <a name="next-steps"></a><span data-ttu-id="9a9d2-190">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9a9d2-190">Next steps</span></span> 

<span data-ttu-id="9a9d2-191">Para más información, vea [Grupos de conmutación por error y replicación geográfica activa](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9a9d2-191">For more information, see [Active geo-replication and failover groups](sql-database-geo-replication-overview.md).</span></span>
