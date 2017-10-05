---
title: Crear SQL Data Warehouse mediante el uso de Powershell | Microsoft Docs
description: "Creación de Almacenamiento de datos SQL con Powershell"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 97434863-7938-4129-8949-5a119f5949e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: a763f1c600c1a3f37cb565a8eb7db3c3f27dcf75
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-sql-data-warehouse-using-powershell"></a><span data-ttu-id="dab37-103">Creación de Almacenamiento de datos SQL con Powershell</span><span class="sxs-lookup"><span data-stu-id="dab37-103">Create SQL Data Warehouse using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dab37-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="dab37-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="dab37-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="dab37-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="dab37-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dab37-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="dab37-107">En este artículo se explica cómo crear un Almacenamiento de datos SQL mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dab37-107">This article shows you how to create a SQL Data Warehouse using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dab37-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="dab37-108">Prerequisites</span></span>
<span data-ttu-id="dab37-109">Para empezar, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="dab37-109">To get started, you need:</span></span>

* <span data-ttu-id="dab37-110">**Cuenta de Azure**: visite las secciones sobre [evaluación gratuita de Azure][Azure Free Trial] o [Crédito mensual de MSDN de Azure][MSDN Azure Credits] para crear una cuenta.</span><span class="sxs-lookup"><span data-stu-id="dab37-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] to create an account.</span></span>
* <span data-ttu-id="dab37-111">**Azure SQL Server**: consulte [Creación de una base de datos de Azure SQL en Azure Portal][Create an Azure SQL database in the Azure Portal] o [Creación de una base de datos de Azure SQL con PowerShell][Create an Azure SQL database with PowerShell] para más información.</span><span class="sxs-lookup"><span data-stu-id="dab37-111">**Azure SQL server**:  See [Create an Azure SQL database in the Azure Portal][Create an Azure SQL database in the Azure Portal] or [Create an Azure SQL database with PowerShell][Create an Azure SQL database with PowerShell] for more details.</span></span>
* <span data-ttu-id="dab37-112">**Nombre del grupo de recursos**: use el mismo grupo de recursos que el servidor SQL Server de Azure o consulte [Creación de un grupo de recursos](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="dab37-112">**Resource group**: Either use the same resource group as your Azure SQL server or see [how to create a resource group](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="dab37-113">**PowerShell versión 1.0.3 o posterior**: para comprobar la versión, ejecute **Get-Module -ListAvailable -Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="dab37-113">**PowerShell version 1.0.3 or greater**:  You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span></span>  <span data-ttu-id="dab37-114">Se puede instalar la versión más reciente desde el [Instalador de plataforma web de Microsoft][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="dab37-114">The latest version can be installed from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="dab37-115">Para más información sobre cómo instalar la versión más reciente, consulte [Cómo instalar y configurar Azure PowerShell][How to install and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="dab37-115">For more information on installing the latest version, see [How to install and configure Azure PowerShell][How to install and configure Azure PowerShell].</span></span>

> [!NOTE]
> <span data-ttu-id="dab37-116">La creación de una instancia de Almacenamiento de datos SQL puede dar lugar a un nuevo servicio facturable.</span><span class="sxs-lookup"><span data-stu-id="dab37-116">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="dab37-117">Consulte [Precios de SQL Data Warehouse][SQL Data Warehouse pricing] para más información sobre los precios.</span><span class="sxs-lookup"><span data-stu-id="dab37-117">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="dab37-118">Creación de Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="dab37-118">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="dab37-119">Abra Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dab37-119">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="dab37-120">Ejecute este cmdlet para iniciar sesión en el Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="dab37-120">Run this cmdlet to login to Azure Resource Manager.</span></span>

    ```Powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="dab37-121">Seleccione la suscripción que desea utilizar para la sesión actual.</span><span class="sxs-lookup"><span data-stu-id="dab37-121">Select the subscription you want to use for your current session.</span></span>

    ```Powershell
    Get-AzureRmSubscription    -SubscriptionName "MySubscription" | Select-AzureRmSubscription
    ```
4. <span data-ttu-id="dab37-122">Cree la base de datos.</span><span class="sxs-lookup"><span data-stu-id="dab37-122">Create database.</span></span> <span data-ttu-id="dab37-123">En este ejemplo se crea una base de datos denominada "mynewsqldw", con el nivel de objetivo de servicio "DW400", en el servidor llamado "sqldwserver1" que se encuentra en el grupo de recursos denominado "mywesteuroperesgp1".</span><span class="sxs-lookup"><span data-stu-id="dab37-123">This example creates a database named "mynewsqldw", with service objective level "DW400", to the server named "sqldwserver1", which is in the resource group named "mywesteuroperesgp1".</span></span>

   ```Powershell
   New-AzureRmSqlDatabase -RequestedServiceObjectiveName "DW400" -DatabaseName "mynewsqldw" -ServerName "sqldwserver1" -ResourceGroupName "mywesteuroperesgp1" -Edition "DataWarehouse" -CollationName "SQL_Latin1_General_CP1_CI_AS" -MaxSizeBytes 10995116277760
   ```

<span data-ttu-id="dab37-124">Los parámetros obligatorios son:</span><span class="sxs-lookup"><span data-stu-id="dab37-124">Required Parameters are:</span></span>

* <span data-ttu-id="dab37-125">**RequestedServiceObjectiveName**: la cantidad de [DWU][DWU] solicitada.</span><span class="sxs-lookup"><span data-stu-id="dab37-125">**RequestedServiceObjectiveName**: The amount of [DWU][DWU] you are requesting.</span></span>  <span data-ttu-id="dab37-126">Los valores admitidos son: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000 y DW6000.</span><span class="sxs-lookup"><span data-stu-id="dab37-126">Supported values are: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000, and DW6000.</span></span>
* <span data-ttu-id="dab37-127">**DatabaseName**: el nombre del Almacenamiento de datos SQL que está creando.</span><span class="sxs-lookup"><span data-stu-id="dab37-127">**DatabaseName**: The name of the SQL Data Warehouse that you are creating.</span></span>
* <span data-ttu-id="dab37-128">**ServerName**: el nombre del servidor que se usa para la creación (tiene que ser V12).</span><span class="sxs-lookup"><span data-stu-id="dab37-128">**ServerName**: The name of the server that you are using for creation (must be V12).</span></span>
* <span data-ttu-id="dab37-129">**ResourceGroupName**: el grupo de recursos que está usando.</span><span class="sxs-lookup"><span data-stu-id="dab37-129">**ResourceGroupName**: Resource group you are using.</span></span>  <span data-ttu-id="dab37-130">Para buscar grupos de recursos que estén disponibles en su suscripción, use Get-AzureResource.</span><span class="sxs-lookup"><span data-stu-id="dab37-130">To find available resource groups in your subscription use Get-AzureResource.</span></span>
* <span data-ttu-id="dab37-131">**Edition**: la edición debe ser "DataWarehouse" para crear un Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="dab37-131">**Edition**: Must be "DataWarehouse" to create a SQL Data Warehouse.</span></span>

<span data-ttu-id="dab37-132">Los parámetros opcionales son:</span><span class="sxs-lookup"><span data-stu-id="dab37-132">Optional Parameters are:</span></span>

* <span data-ttu-id="dab37-133">**CollationName**: la intercalación predeterminada cuando no se especifica otra es SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="dab37-133">**CollationName**: The default collation if not specified is SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="dab37-134">No se puede cambiar la intercalación de una base de datos.</span><span class="sxs-lookup"><span data-stu-id="dab37-134">Collation cannot be changed on a database.</span></span>
* <span data-ttu-id="dab37-135">**MaxSizeBytes**: el tamaño máximo predeterminado de una base de datos es 10 GB.</span><span class="sxs-lookup"><span data-stu-id="dab37-135">**MaxSizeBytes**: The default max size of a database is 10 GB.</span></span>

<span data-ttu-id="dab37-136">Para más información sobre las opciones de parámetros, consulte [New-AzureRmSqlDatabase][New-AzureRmSqlDatabase] y [Create Database (Azure SQL Data Warehouse)][Create Database (Azure SQL Data Warehouse)] (Creación de base de datos [Azure SQL Data Warehouse]).</span><span class="sxs-lookup"><span data-stu-id="dab37-136">For more details on the parameter options, see [New-AzureRmSqlDatabase][New-AzureRmSqlDatabase] and [Create Database (Azure SQL Data Warehouse)][Create Database (Azure SQL Data Warehouse)].</span></span>

## <a name="next-steps"></a><span data-ttu-id="dab37-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dab37-137">Next steps</span></span>
<span data-ttu-id="dab37-138">Después de que Azure SQL Data Warehouse finalice el aprovisionamiento, puede intentar [cargar datos de ejemplo][loading sample data] o averiguar cómo [desarrollar][develop], [cargar][load] o [migrar][migrate].</span><span class="sxs-lookup"><span data-stu-id="dab37-138">After your SQL Data Warehouse has finished provisioning you may want to try [loading sample data][loading sample data] or check out how to [develop][develop], [load][load], or [migrate][migrate].</span></span>

<span data-ttu-id="dab37-139">Si está interesado en más información sobre cómo administrar SQL Data Warehouse mediante programación, consulte nuestro artículo sobre cómo usar [las API de REST y los cmdlets de PowerShell][PowerShell cmdlets and REST APIs].</span><span class="sxs-lookup"><span data-stu-id="dab37-139">If you're interested in more on how to manage SQL Data Warehouse programmatically, check out our article on how to use [PowerShell cmdlets and REST APIs][PowerShell cmdlets and REST APIs].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[migrate]: ./sql-data-warehouse-overview-migrate.md
[develop]: ./sql-data-warehouse-overview-develop.md
[load]: ./sql-data-warehouse-load-with-bcp.md
[loading sample data]: ./sql-data-warehouse-load-sample-databases.md
[PowerShell cmdlets and REST APIs]: ./sql-data-warehouse-reference-powershell-cmdlets.md
[firewall rules]: ../sql-database-configure-firewall-settings.md

[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[how to create a SQL Data Warehouse from the Azure Portal]: ./sql-data-warehouse-get-started-provision.md
[Create an Azure SQL database in the Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-get-started-powershell.md
[how to create a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group

<!--MSDN references-->
[MSDN]: https://msdn.microsoft.com/library/azure/dn546722.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Create Database (Azure SQL Data Warehouse)]: https://msdn.microsoft.com/library/mt204021.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
