---
title: "Creación de una instancia de SQL Data Warehouse con TSQL | Microsoft Docs"
description: Aprenda a crear una base de datos de Almacenamiento de datos SQL de Azure con TSQL
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: a4e2e68e-aa9c-4dd3-abb0-f7df997d237a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 10d8aa2b3ab8d7d8a9b91e95ffccf03faa89d237
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-sql-data-warehouse-database-by-using-transact-sql-tsql"></a><span data-ttu-id="6426d-103">Creación de una base de datos de Almacenamiento de datos SQL mediante Transact-SQL (TSQL)</span><span class="sxs-lookup"><span data-stu-id="6426d-103">Create a SQL Data Warehouse database by using Transact-SQL (TSQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6426d-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6426d-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="6426d-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="6426d-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="6426d-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6426d-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="6426d-107">En este artículo se explica cómo crear un Almacenamiento de datos SQL mediante T-SQL.</span><span class="sxs-lookup"><span data-stu-id="6426d-107">This article shows you how to create a SQL Data Warehouse using T-SQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6426d-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6426d-108">Prerequisites</span></span>
<span data-ttu-id="6426d-109">Para empezar, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6426d-109">To get started, you need:</span></span>

* <span data-ttu-id="6426d-110">**Cuenta de Azure**: visite las secciones sobre [evaluación gratuita de Azure][Azure Free Trial] o [Crédito mensual de MSDN de Azure][MSDN Azure Credits] para crear una cuenta.</span><span class="sxs-lookup"><span data-stu-id="6426d-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] to create an account.</span></span>
* <span data-ttu-id="6426d-111">**Servidor de SQL Azure**: consulte [crear un servidor lógico de la base de datos de SQL Azure con el Portal de Azure] [crear un servidor lógico de la base de datos de SQL Azure con el Portal de Azure] o [crear un servidor lógico de la base de datos de SQL Azure con PowerShell] [crear un SQL Azure Servidor lógico de base de datos con PowerShell] para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="6426d-111">**Azure SQL server**:  See [Create an Azure SQL Database logical server with the Azure Portal][Create an Azure SQL Database logical server with the Azure Portal] or [Create an Azure SQL Database logical server with PowerShell][Create an Azure SQL Database logical server with PowerShell] for more details.</span></span>
* <span data-ttu-id="6426d-112">**Nombre del grupo de recursos**: use el mismo grupo de recursos que el servidor SQL Server de Azure o consulte [Creación de un grupo de recursos][how to create a resource group].</span><span class="sxs-lookup"><span data-stu-id="6426d-112">**Resource group**: Either use the same resource group as your Azure SQL server or see [how to create a resource group][how to create a resource group].</span></span>
* <span data-ttu-id="6426d-113">**Entorno para ejecutar T-SQL**: puede usar [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd] o [SSMS][SSMS] para ejecutar T-SQL.</span><span class="sxs-lookup"><span data-stu-id="6426d-113">**Environment to execute T-SQL**: You can use [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], or [SSMS][SSMS] to execute T-SQL.</span></span>

> [!NOTE]
> <span data-ttu-id="6426d-114">La creación de una instancia de Almacenamiento de datos SQL puede dar lugar a un nuevo servicio facturable.</span><span class="sxs-lookup"><span data-stu-id="6426d-114">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="6426d-115">Consulte [Precios de SQL Data Warehouse][SQL Data Warehouse pricing] para más información sobre los precios.</span><span class="sxs-lookup"><span data-stu-id="6426d-115">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-database-with-visual-studio"></a><span data-ttu-id="6426d-116">Creación de una base de datos con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6426d-116">Create a database with Visual Studio</span></span>
<span data-ttu-id="6426d-117">Si no está familiarizado con Visual Studio, consulte el artículo [Consultas en Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].</span><span class="sxs-lookup"><span data-stu-id="6426d-117">If you are new to Visual Studio, see the article [Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].</span></span>  <span data-ttu-id="6426d-118">Para comenzar, abra el Explorador de objetos de SQL Server en Visual Studio y conéctese al servidor que hospedará la base de datos de Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="6426d-118">To start, open SQL Server Object Explorer in Visual Studio and connect to the server that will host your SQL Data Warehouse database.</span></span>  <span data-ttu-id="6426d-119">Una vez conectado, puede crear una instancia de Almacenamiento de datos SQL mediante la ejecución del siguiente comando SQL en la base de datos **maestra** .</span><span class="sxs-lookup"><span data-stu-id="6426d-119">Once connected, you can create a SQL Data Warehouse by running the following SQL command against the **master** database.</span></span>  <span data-ttu-id="6426d-120">Este comando crea la base de datos MySqlDwDb con un objetivo de servicio de DW400 y permite que crezca hasta un tamaño máximo de 10 TB.</span><span class="sxs-lookup"><span data-stu-id="6426d-120">This command creates the database MySqlDwDb with a Service Objective of DW400 and allow the database to grow to a maximum size of 10 TB.</span></span>

```sql
CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB);
```

## <a name="create-a-database-with-sqlcmd"></a><span data-ttu-id="6426d-121">Creación de una base de datos con sqlcmd</span><span class="sxs-lookup"><span data-stu-id="6426d-121">Create a database with sqlcmd</span></span>
<span data-ttu-id="6426d-122">Como alternativa, puede ejecutar el mismo comando con sqlcmd mediante la ejecución del siguiente código en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="6426d-122">Alternatively, you can run the same command with sqlcmd by running the following at a command prompt.</span></span>

```sql
sqlcmd -S <Server Name>.database.windows.net -I -U <User> -P <Password> -Q "CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB)"
```

<span data-ttu-id="6426d-123">La intercalación predeterminada cuando no se especifica otra es COLLATE SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="6426d-123">The default collation when not specified is COLLATE SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="6426d-124">El valor de `MAXSIZE` puede estar entre 250 GB y 240 TB.</span><span class="sxs-lookup"><span data-stu-id="6426d-124">The `MAXSIZE` can be between 250 GB and 240 TB.</span></span>  <span data-ttu-id="6426d-125">El valor de `SERVICE_OBJECTIVE` puede estar entre DW100 y DW2000 [DWU][DWU].</span><span class="sxs-lookup"><span data-stu-id="6426d-125">The `SERVICE_OBJECTIVE` can be between DW100 and DW2000 [DWU][DWU].</span></span>  <span data-ttu-id="6426d-126">Para obtener una lista de todos los valores válidos, consulte la documentación de MSDN para [CREATE DATABASE][CREATE DATABASE].</span><span class="sxs-lookup"><span data-stu-id="6426d-126">For a list of all valid values, see the MSDN documentation for [CREATE DATABASE][CREATE DATABASE].</span></span>  <span data-ttu-id="6426d-127">Se pueden cambiar los valores de MAXSIZE y SERVICE_OBJECTIVE con un comando [ALTER DATABASE][ALTER DATABASE] de T-SQL.</span><span class="sxs-lookup"><span data-stu-id="6426d-127">Both the MAXSIZE and SERVICE_OBJECTIVE can be changed with an [ALTER DATABASE][ALTER DATABASE] T-SQL command.</span></span>  <span data-ttu-id="6426d-128">No se puede cambiar la intercalación de una base de datos después de su creación.</span><span class="sxs-lookup"><span data-stu-id="6426d-128">The collation of a database cannot be changed after creation.</span></span>   <span data-ttu-id="6426d-129">Debe tener precaución al cambiar el valor de SERVICE_OBJECTIVE ya que cambiar la DWU provocará un reinicio de los servicios que cancelará todas las consultas en marcha.</span><span class="sxs-lookup"><span data-stu-id="6426d-129">Caution should be used when changing the SERVICE_OBJECTIVE as changing DWU causes a restart of services, which cancels all queries in flight.</span></span>  <span data-ttu-id="6426d-130">Con el cambio de MAXSIZE no se reinician servicios, ya que es solo una operación de metadatos sencilla.</span><span class="sxs-lookup"><span data-stu-id="6426d-130">Changing MAXSIZE does not restart services as it is just a simple metadata operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6426d-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6426d-131">Next steps</span></span>
<span data-ttu-id="6426d-132">Después de que SQL Data Warehouse termine el aprovisionamiento, [puede cargar datos de ejemplo][load sample data] o averiguar cómo [desarrollar][develop], [cargar][load] o [migrar][migrate].</span><span class="sxs-lookup"><span data-stu-id="6426d-132">After your SQL Data Warehouse has finished provisioning you can [load sample data][load sample data] or check out how to [develop][develop], [load][load], or [migrate][migrate].</span></span>

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[how to create a SQL Data Warehouse from the Azure portal]: sql-data-warehouse-get-started-provision.md
[Query Azure SQL Data Warehouse (Visual Studio)]: sql-data-warehouse-query-visual-studio.md
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data]: sql-data-warehouse-load-sample-databases.md
[Create an Azure SQL database with the Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[how to create a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--MSDN references-->
[CREATE DATABASE]: https://msdn.microsoft.com/library/mt204021.aspx
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx
[SSMS]: https://msdn.microsoft.com/library/mt238290.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
