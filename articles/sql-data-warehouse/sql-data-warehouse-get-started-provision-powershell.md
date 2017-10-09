---
title: aaaCreate almacenamiento de datos SQL mediante PowerShell | Documentos de Microsoft
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
ms.openlocfilehash: d8af29ec285a11285785ab5474e4dfc8c36bc3ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-sql-data-warehouse-using-powershell"></a><span data-ttu-id="4ae69-103">Creación de Almacenamiento de datos SQL con Powershell</span><span class="sxs-lookup"><span data-stu-id="4ae69-103">Create SQL Data Warehouse using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4ae69-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4ae69-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="4ae69-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="4ae69-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="4ae69-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ae69-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="4ae69-107">Este artículo muestra cómo toocreate un almacenamiento de datos SQL mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ae69-107">This article shows you how toocreate a SQL Data Warehouse using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ae69-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4ae69-108">Prerequisites</span></span>
<span data-ttu-id="4ae69-109">tooget iniciado, debe:</span><span class="sxs-lookup"><span data-stu-id="4ae69-109">tooget started, you need:</span></span>

* <span data-ttu-id="4ae69-110">**Cuenta de Azure**: visite [evaluación gratuita de Azure] [ Azure Free Trial] o [créditos de Azure de MSDN] [ MSDN Azure Credits] toocreate una cuenta.</span><span class="sxs-lookup"><span data-stu-id="4ae69-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="4ae69-111">**Servidor de SQL Azure**: vea [crear una base de datos de SQL Azure en hello Azure Portal] [ Create an Azure SQL database in hello Azure Portal] o [crear una base de datos de SQL Azure con PowerShell] [ Create an Azure SQL database with PowerShell] para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="4ae69-111">**Azure SQL server**:  See [Create an Azure SQL database in hello Azure Portal][Create an Azure SQL database in hello Azure Portal] or [Create an Azure SQL database with PowerShell][Create an Azure SQL database with PowerShell] for more details.</span></span>
* <span data-ttu-id="4ae69-112">**Grupo de recursos**: use Hola mismo recurso de grupo como el servidor de SQL Azure o vea [cómo toocreate un grupo de recursos](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4ae69-112">**Resource group**: Either use hello same resource group as your Azure SQL server or see [how toocreate a resource group](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="4ae69-113">**PowerShell versión 1.0.3 o posterior**: para comprobar la versión, ejecute **Get-Module -ListAvailable -Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="4ae69-113">**PowerShell version 1.0.3 or greater**:  You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span></span>  <span data-ttu-id="4ae69-114">se puede instalar la versión más reciente de Hola desde [instalador de plataforma Web de Microsoft][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="4ae69-114">hello latest version can be installed from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="4ae69-115">Para obtener más información acerca de cómo instalar la versión más reciente de hello, consulte [cómo tooinstall y configurar Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="4ae69-115">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>

> [!NOTE]
> <span data-ttu-id="4ae69-116">La creación de una instancia de Almacenamiento de datos SQL puede dar lugar a un nuevo servicio facturable.</span><span class="sxs-lookup"><span data-stu-id="4ae69-116">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="4ae69-117">Consulte [Precios de SQL Data Warehouse][SQL Data Warehouse pricing] para más información sobre los precios.</span><span class="sxs-lookup"><span data-stu-id="4ae69-117">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="4ae69-118">Creación de Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="4ae69-118">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="4ae69-119">Abra Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ae69-119">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="4ae69-120">Ejecute este tooAzure de toologin de cmdlet Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="4ae69-120">Run this cmdlet toologin tooAzure Resource Manager.</span></span>

    ```Powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="4ae69-121">Seleccione la suscripción de Hola que desee toouse para la sesión actual.</span><span class="sxs-lookup"><span data-stu-id="4ae69-121">Select hello subscription you want toouse for your current session.</span></span>

    ```Powershell
    Get-AzureRmSubscription    -SubscriptionName "MySubscription" | Select-AzureRmSubscription
    ```
4. <span data-ttu-id="4ae69-122">Cree la base de datos.</span><span class="sxs-lookup"><span data-stu-id="4ae69-122">Create database.</span></span> <span data-ttu-id="4ae69-123">Este ejemplo crea una base de datos denominada "mynewsqldw", con un nivel objetivo de servicio "DW400", servidor toohello denominado "sqldwserver1", que se encuentra en el grupo de recursos de hello llamado "mywesteuroperesgp1".</span><span class="sxs-lookup"><span data-stu-id="4ae69-123">This example creates a database named "mynewsqldw", with service objective level "DW400", toohello server named "sqldwserver1", which is in hello resource group named "mywesteuroperesgp1".</span></span>

   ```Powershell
   New-AzureRmSqlDatabase -RequestedServiceObjectiveName "DW400" -DatabaseName "mynewsqldw" -ServerName "sqldwserver1" -ResourceGroupName "mywesteuroperesgp1" -Edition "DataWarehouse" -CollationName "SQL_Latin1_General_CP1_CI_AS" -MaxSizeBytes 10995116277760
   ```

<span data-ttu-id="4ae69-124">Los parámetros obligatorios son:</span><span class="sxs-lookup"><span data-stu-id="4ae69-124">Required Parameters are:</span></span>

* <span data-ttu-id="4ae69-125">**RequestedServiceObjectiveName**: cantidad de Hola de [DWU] [ DWU] que está solicitando.</span><span class="sxs-lookup"><span data-stu-id="4ae69-125">**RequestedServiceObjectiveName**: hello amount of [DWU][DWU] you are requesting.</span></span>  <span data-ttu-id="4ae69-126">Los valores admitidos son: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000 y DW6000.</span><span class="sxs-lookup"><span data-stu-id="4ae69-126">Supported values are: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000, and DW6000.</span></span>
* <span data-ttu-id="4ae69-127">**DatabaseName**: nombre de Hola de hello almacenamiento de datos de SQL que se va a crear.</span><span class="sxs-lookup"><span data-stu-id="4ae69-127">**DatabaseName**: hello name of hello SQL Data Warehouse that you are creating.</span></span>
* <span data-ttu-id="4ae69-128">**ServerName**: nombre de hello del servidor de Hola que está usando para la creación (debe ser V12).</span><span class="sxs-lookup"><span data-stu-id="4ae69-128">**ServerName**: hello name of hello server that you are using for creation (must be V12).</span></span>
* <span data-ttu-id="4ae69-129">**ResourceGroupName**: el grupo de recursos que está usando.</span><span class="sxs-lookup"><span data-stu-id="4ae69-129">**ResourceGroupName**: Resource group you are using.</span></span>  <span data-ttu-id="4ae69-130">toofind grupos de recursos disponibles en su suscripción usan Get-AzureResource.</span><span class="sxs-lookup"><span data-stu-id="4ae69-130">toofind available resource groups in your subscription use Get-AzureResource.</span></span>
* <span data-ttu-id="4ae69-131">**Edición**: debe ser "Almacenamiento" toocreate un almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="4ae69-131">**Edition**: Must be "DataWarehouse" toocreate a SQL Data Warehouse.</span></span>

<span data-ttu-id="4ae69-132">Los parámetros opcionales son:</span><span class="sxs-lookup"><span data-stu-id="4ae69-132">Optional Parameters are:</span></span>

* <span data-ttu-id="4ae69-133">**CollationName**: intercalación de hello predeterminada si no se especifica es SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="4ae69-133">**CollationName**: hello default collation if not specified is SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="4ae69-134">No se puede cambiar la intercalación de una base de datos.</span><span class="sxs-lookup"><span data-stu-id="4ae69-134">Collation cannot be changed on a database.</span></span>
* <span data-ttu-id="4ae69-135">**MaxSizeBytes**: tamaño máximo de saludo predeterminado de una base de datos es de 10 GB.</span><span class="sxs-lookup"><span data-stu-id="4ae69-135">**MaxSizeBytes**: hello default max size of a database is 10 GB.</span></span>

<span data-ttu-id="4ae69-136">Para obtener más detalles sobre las opciones de parámetro hello, consulte [New-AzureRmSqlDatabase] [ New-AzureRmSqlDatabase] y [Create Database (almacenamiento de datos de SQL Azure)][Create Database (Azure SQL Data Warehouse)].</span><span class="sxs-lookup"><span data-stu-id="4ae69-136">For more details on hello parameter options, see [New-AzureRmSqlDatabase][New-AzureRmSqlDatabase] and [Create Database (Azure SQL Data Warehouse)][Create Database (Azure SQL Data Warehouse)].</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ae69-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4ae69-137">Next steps</span></span>
<span data-ttu-id="4ae69-138">Después de que el almacenamiento de datos de SQL ha terminado el aprovisionamiento se puede tootry [cargar datos de ejemplo] [ loading sample data] o desproteger cómo demasiado[desarrollar] [ develop] , [cargar][load], o [migrar][migrate].</span><span class="sxs-lookup"><span data-stu-id="4ae69-138">After your SQL Data Warehouse has finished provisioning you may want tootry [loading sample data][loading sample data] or check out how too[develop][develop], [load][load], or [migrate][migrate].</span></span>

<span data-ttu-id="4ae69-139">Si le interesa obtener más información sobre cómo toomanage almacenamiento de datos SQL mediante programación, consulte el artículo sobre cómo toouse [cmdlets de PowerShell y API de REST][PowerShell cmdlets and REST APIs].</span><span class="sxs-lookup"><span data-stu-id="4ae69-139">If you're interested in more on how toomanage SQL Data Warehouse programmatically, check out our article on how toouse [PowerShell cmdlets and REST APIs][PowerShell cmdlets and REST APIs].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[migrate]: ./sql-data-warehouse-overview-migrate.md
[develop]: ./sql-data-warehouse-overview-develop.md
[load]: ./sql-data-warehouse-load-with-bcp.md
[loading sample data]: ./sql-data-warehouse-load-sample-databases.md
[PowerShell cmdlets and REST APIs]: ./sql-data-warehouse-reference-powershell-cmdlets.md
[firewall rules]: ../sql-database-configure-firewall-settings.md

[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[how toocreate a SQL Data Warehouse from hello Azure Portal]: ./sql-data-warehouse-get-started-provision.md
[Create an Azure SQL database in hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-get-started-powershell.md
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group

<!--MSDN references-->
[MSDN]: https://msdn.microsoft.com/library/azure/dn546722.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Create Database (Azure SQL Data Warehouse)]: https://msdn.microsoft.com/library/mt204021.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
