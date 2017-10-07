---
title: "Azure PowerShell: Creación de una instancia de SQL Database | Microsoft Docs"
description: "Obtenga información acerca de cómo toocreate un servidor lógico de la base de datos SQL, regla de firewall de nivel de servidor y bases de datos de Hola portal de Azure."
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
ms.devlang: PowerShell
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: e89f68b44083a3b64e61f95117dbbedfa6647ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-powershell"></a><span data-ttu-id="dc49d-104">Creación de una sola instancia de Azure SQL Database con PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc49d-104">Create a single Azure SQL database using PowerShell</span></span>

<span data-ttu-id="dc49d-105">PowerShell es toocreate usado y administrar recursos de Azure desde la línea de comandos de Hola o en scripts.</span><span class="sxs-lookup"><span data-stu-id="dc49d-105">PowerShell is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="dc49d-106">Esta guía de detalles mediante PowerShell toodeploy una base de datos de SQL Azure en un [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md) en un [servidor lógico de base de datos de SQL Azure](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="dc49d-106">This guide details using PowerShell toodeploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="dc49d-107">Si no tiene una suscripción a Azure, cree una cuenta [gratuita](https://azure.microsoft.com/free/) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="dc49d-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

<span data-ttu-id="dc49d-108">Este tutorial requiere hello Azure PowerShell versión 4.0 o posterior del módulo.</span><span class="sxs-lookup"><span data-stu-id="dc49d-108">This tutorial requires hello Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="dc49d-109">Ejecutar ` Get-Module -ListAvailable AzureRM` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc49d-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="dc49d-110">Si necesita tooinstall o una actualización, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="dc49d-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

## <a name="log-in-tooazure"></a><span data-ttu-id="dc49d-111">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="dc49d-111">Log in tooAzure</span></span>

<span data-ttu-id="dc49d-112">Inicie sesión en tooyour suscripción de Azure con hello [AzureRmAccount agregar](/powershell/module/azurerm.profile/add-azurermaccount) comando y siga hello en pantalla instrucciones.</span><span class="sxs-lookup"><span data-stu-id="dc49d-112">Log in tooyour Azure subscription using hello [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command and follow hello on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-variables"></a><span data-ttu-id="dc49d-113">Creación de variables</span><span class="sxs-lookup"><span data-stu-id="dc49d-113">Create variables</span></span>

<span data-ttu-id="dc49d-114">Definir variables para su uso en scripts de hello en esta guía de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="dc49d-114">Define variables for use in hello scripts in this quick start.</span></span>

```powershell
# hello data center and resource name for your resources
$resourcegroupname = "myResourceGroup"
$location = "WestEurope"
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
$servername = "server-$(Get-Random)"
# Set an admin login and password for your database
# hello login information for hello server
$adminlogin = "ServerAdmin"
$password = "ChangeYourAdminPassword1"
# hello ip address range that you want tooallow tooaccess your server - change as appropriate
$startip = "0.0.0.0"
$endip = "0.0.0.0"
# hello database name
$databasename = "mySampleDatabase"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="dc49d-115">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="dc49d-115">Create a resource group</span></span>

<span data-ttu-id="dc49d-116">Crear un [grupo de recursos de Azure](../azure-resource-manager/resource-group-overview.md) con hello [AzureRmResourceGroup New](/powershell/module/azurerm.resources/new-azurermresourcegroup) comando.</span><span class="sxs-lookup"><span data-stu-id="dc49d-116">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="dc49d-117">Un grupo de recursos es un contenedor lógico en el que se implementan y se administran recursos de Azure como un grupo.</span><span class="sxs-lookup"><span data-stu-id="dc49d-117">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="dc49d-118">Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en hello `westeurope` ubicación.</span><span class="sxs-lookup"><span data-stu-id="dc49d-118">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location.</span></span>

```powershell
New-AzureRmResourceGroup -Name $resourcegroupname -Location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="dc49d-119">un servidor lógico</span><span class="sxs-lookup"><span data-stu-id="dc49d-119">Create a logical server</span></span>

<span data-ttu-id="dc49d-120">Crear un [servidor lógico de base de datos de SQL Azure](sql-database-features.md) con hello [AzureRmSqlServer New](/powershell/module/azurerm.sql/new-azurermsqlserver) comando.</span><span class="sxs-lookup"><span data-stu-id="dc49d-120">Create an [Azure SQL Database logical server](sql-database-features.md) using hello [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) command.</span></span> <span data-ttu-id="dc49d-121">Un servidor lógico contiene un conjunto de bases de datos administradas como un grupo.</span><span class="sxs-lookup"><span data-stu-id="dc49d-121">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="dc49d-122">Hello en el ejemplo siguiente se crea un servidor de forma aleatoria con nombre en el grupo de recursos con un inicio de sesión de administración denominado `ServerAdmin` y una contraseña de `ChangeYourAdminPassword1`.</span><span class="sxs-lookup"><span data-stu-id="dc49d-122">hello following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="dc49d-123">Cambie estos valores predefinidos por los que prefiera.</span><span class="sxs-lookup"><span data-stu-id="dc49d-123">Replace these pre-defined values as desired.</span></span>

```powershell
New-AzureRmSqlServer -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -Location $location `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="dc49d-124">Configuración de una regla de firewall del servidor</span><span class="sxs-lookup"><span data-stu-id="dc49d-124">Configure a server firewall rule</span></span>

<span data-ttu-id="dc49d-125">Crear un [regla de firewall de nivel de servidor de base de datos de SQL Azure](sql-database-firewall-configure.md) con hello [AzureRmSqlServerFirewallRule New](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) comando.</span><span class="sxs-lookup"><span data-stu-id="dc49d-125">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using hello [New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) command.</span></span> <span data-ttu-id="dc49d-126">Una regla de firewall de nivel de servidor permite que una aplicación externa, como SQL Server Management Studio o hello SQLCMD utilidad tooconnect tooa base de datos SQL a través de firewall de servicio de base de datos SQL de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc49d-126">A server-level firewall rule allows an external application, such as SQL Server Management Studio or hello SQLCMD utility tooconnect tooa SQL database through hello SQL Database service firewall.</span></span> <span data-ttu-id="dc49d-127">En el siguiente ejemplo de Hola, solo se abrirá el firewall de Hola para otros recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc49d-127">In hello following example, hello firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="dc49d-128">tooenable conectividad externa, cambio Hola IP dirección tooan dirección adecuada para su entorno.</span><span class="sxs-lookup"><span data-stu-id="dc49d-128">tooenable external connectivity, change hello IP address tooan appropriate address for your environment.</span></span> <span data-ttu-id="dc49d-129">tooopen todas las direcciones IP, utilice 0.0.0.0 como Hola a partir de dirección IP y 255.255.255.255 como Hola dirección final.</span><span class="sxs-lookup"><span data-stu-id="dc49d-129">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress $startip -EndIpAddress $endip
```

> [!NOTE]
> <span data-ttu-id="dc49d-130">SQL Database se comunica a través del puerto 1433.</span><span class="sxs-lookup"><span data-stu-id="dc49d-130">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="dc49d-131">Si está tratando de tooconnect desde dentro de una red corporativa, es posible que firewall de su red no permite el tráfico saliente en el puerto 1433.</span><span class="sxs-lookup"><span data-stu-id="dc49d-131">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="dc49d-132">Si es así, no será capaz de tooconnect tooyour base de datos de SQL Azure servidor a menos que el departamento de TI abre el puerto 1433.</span><span class="sxs-lookup"><span data-stu-id="dc49d-132">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a><span data-ttu-id="dc49d-133">Crear una base de datos en el servidor de hello con datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="dc49d-133">Create a database in hello server with sample data</span></span>

<span data-ttu-id="dc49d-134">Crear una base de datos con un [nivel de rendimiento S0](sql-database-service-tiers.md) en servidor de hello mediante Hola [AzureRmSqlDatabase New](/powershell/module/azurerm.sql/new-azurermsqldatabase) comando.</span><span class="sxs-lookup"><span data-stu-id="dc49d-134">Create a database with an [S0 performance level](sql-database-service-tiers.md) in hello server using hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) command.</span></span> <span data-ttu-id="dc49d-135">Hello en el ejemplo siguiente se crea una base de datos denominada `mySampleDatabase` y carga Hola datos de ejemplo AdventureWorksLT en esta base de datos.</span><span class="sxs-lookup"><span data-stu-id="dc49d-135">hello following example creates a database called `mySampleDatabase` and loads hello AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="dc49d-136">Reemplazar predefinidos de estos valores según sea necesario (otras guías rápidas en esta colección se basan en valores de hello en esta guía de inicio rápido).</span><span class="sxs-lookup"><span data-stu-id="dc49d-136">Replace these predefined values as desired (other quick starts in this collection build upon hello values in this quick start).</span></span>

```powershell
New-AzureRmSqlDatabase  -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -DatabaseName $databasename `
    -SampleName "AdventureWorksLT" `
    -RequestedServiceObjectiveName "S0"
```

## <a name="clean-up-resources"></a><span data-ttu-id="dc49d-137">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="dc49d-137">Clean up resources</span></span>

<span data-ttu-id="dc49d-138">Otras guías de inicio rápido de esta colección se basan en los valores de esta.</span><span class="sxs-lookup"><span data-stu-id="dc49d-138">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="dc49d-139">Si tiene previsto toocontinue toowork con guías rápidas posteriores, no limpiar los recursos de hello creados en esta rápida se inician.</span><span class="sxs-lookup"><span data-stu-id="dc49d-139">If you plan toocontinue on toowork with subsequent quick starts, do not clean up hello resources created in this quick start.</span></span> <span data-ttu-id="dc49d-140">Si no tiene previsto toocontinue, use Hola seguido toodelete pasos creado todos los recursos de esta guía de inicio rápido en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="dc49d-140">If you do not plan toocontinue, use hello following steps toodelete all resources created by this quick start in hello Azure portal.</span></span>
>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="dc49d-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dc49d-141">Next steps</span></span>

<span data-ttu-id="dc49d-142">Ahora que tiene una base de datos, puede conectarse y realizar consultas con las herramientas que desee.</span><span class="sxs-lookup"><span data-stu-id="dc49d-142">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="dc49d-143">Para más información, seleccione una de las herramientas siguientes:</span><span class="sxs-lookup"><span data-stu-id="dc49d-143">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="dc49d-144">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="dc49d-144">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="dc49d-145">código de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dc49d-145">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="dc49d-146">.NET</span><span class="sxs-lookup"><span data-stu-id="dc49d-146">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="dc49d-147">PHP</span><span class="sxs-lookup"><span data-stu-id="dc49d-147">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="dc49d-148">Node.js</span><span class="sxs-lookup"><span data-stu-id="dc49d-148">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="dc49d-149">Java</span><span class="sxs-lookup"><span data-stu-id="dc49d-149">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="dc49d-150">Python</span><span class="sxs-lookup"><span data-stu-id="dc49d-150">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="dc49d-151">Ruby</span><span class="sxs-lookup"><span data-stu-id="dc49d-151">Ruby</span></span>](sql-database-connect-query-ruby.md)

