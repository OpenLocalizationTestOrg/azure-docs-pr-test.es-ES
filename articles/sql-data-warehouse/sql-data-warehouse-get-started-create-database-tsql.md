---
title: aaaCreate un almacenamiento de datos de SQL con TSQL | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un Azure SQL del almacenamiento de datos con TSQL"
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
ms.openlocfilehash: 81ef59a66c61452ff8a2aca29837f155e87d017d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-sql-data-warehouse-database-by-using-transact-sql-tsql"></a><span data-ttu-id="7c31d-103">Creación de una base de datos de Almacenamiento de datos SQL mediante Transact-SQL (TSQL)</span><span class="sxs-lookup"><span data-stu-id="7c31d-103">Create a SQL Data Warehouse database by using Transact-SQL (TSQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7c31d-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7c31d-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="7c31d-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="7c31d-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="7c31d-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c31d-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="7c31d-107">Este artículo muestra cómo toocreate un almacenamiento de datos SQL mediante T-SQL.</span><span class="sxs-lookup"><span data-stu-id="7c31d-107">This article shows you how toocreate a SQL Data Warehouse using T-SQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c31d-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7c31d-108">Prerequisites</span></span>
<span data-ttu-id="7c31d-109">tooget iniciado, debe:</span><span class="sxs-lookup"><span data-stu-id="7c31d-109">tooget started, you need:</span></span>

* <span data-ttu-id="7c31d-110">**Cuenta de Azure**: visite [evaluación gratuita de Azure] [ Azure Free Trial] o [créditos de Azure de MSDN] [ MSDN Azure Credits] toocreate una cuenta.</span><span class="sxs-lookup"><span data-stu-id="7c31d-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="7c31d-111">**Servidor de SQL Azure**: consulte [crear un servidor lógico de la base de datos de SQL Azure con hello Portal de Azure] [crear un servidor lógico de la base de datos de SQL Azure con hello Portal de Azure] o [crear un servidor lógico de la base de datos de SQL Azure con PowerShell] [crear un SQL Azure Servidor lógico de base de datos con PowerShell] para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="7c31d-111">**Azure SQL server**:  See [Create an Azure SQL Database logical server with hello Azure Portal][Create an Azure SQL Database logical server with hello Azure Portal] or [Create an Azure SQL Database logical server with PowerShell][Create an Azure SQL Database logical server with PowerShell] for more details.</span></span>
* <span data-ttu-id="7c31d-112">**Grupo de recursos**: use Hola mismo recurso de grupo como el servidor de SQL Azure o vea [cómo un grupo de recursos de toocreate][how toocreate a resource group].</span><span class="sxs-lookup"><span data-stu-id="7c31d-112">**Resource group**: Either use hello same resource group as your Azure SQL server or see [how toocreate a resource group][how toocreate a resource group].</span></span>
* <span data-ttu-id="7c31d-113">**Entorno tooexecute T-SQL**: puede usar [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], o [SSMS] [ SSMS] tooexecute T-SQL.</span><span class="sxs-lookup"><span data-stu-id="7c31d-113">**Environment tooexecute T-SQL**: You can use [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], or [SSMS][SSMS] tooexecute T-SQL.</span></span>

> [!NOTE]
> <span data-ttu-id="7c31d-114">La creación de una instancia de Almacenamiento de datos SQL puede dar lugar a un nuevo servicio facturable.</span><span class="sxs-lookup"><span data-stu-id="7c31d-114">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="7c31d-115">Consulte [Precios de SQL Data Warehouse][SQL Data Warehouse pricing] para más información sobre los precios.</span><span class="sxs-lookup"><span data-stu-id="7c31d-115">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-database-with-visual-studio"></a><span data-ttu-id="7c31d-116">Creación de una base de datos con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7c31d-116">Create a database with Visual Studio</span></span>
<span data-ttu-id="7c31d-117">Si es nuevo tooVisual Studio, consulte el artículo de hello [almacenamiento de datos de SQL de Azure de consulta (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].</span><span class="sxs-lookup"><span data-stu-id="7c31d-117">If you are new tooVisual Studio, see hello article [Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].</span></span>  <span data-ttu-id="7c31d-118">toostart, abra el Explorador de objetos de SQL Server en Visual Studio y conecte toohello servidor que hospedará la base de datos de almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="7c31d-118">toostart, open SQL Server Object Explorer in Visual Studio and connect toohello server that will host your SQL Data Warehouse database.</span></span>  <span data-ttu-id="7c31d-119">Una vez conectado, puede crear un almacén de datos de SQL ejecutando el siguiente comando SQL contra Hola de hello **maestro** base de datos.</span><span class="sxs-lookup"><span data-stu-id="7c31d-119">Once connected, you can create a SQL Data Warehouse by running hello following SQL command against hello **master** database.</span></span>  <span data-ttu-id="7c31d-120">Este comando crea la base de datos de hello MySqlDwDb con un objetivo de DW400 de servicio y permitir Hola base de datos toogrow tooa tamaño máximo de 10 TB.</span><span class="sxs-lookup"><span data-stu-id="7c31d-120">This command creates hello database MySqlDwDb with a Service Objective of DW400 and allow hello database toogrow tooa maximum size of 10 TB.</span></span>

```sql
CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB);
```

## <a name="create-a-database-with-sqlcmd"></a><span data-ttu-id="7c31d-121">Creación de una base de datos con sqlcmd</span><span class="sxs-lookup"><span data-stu-id="7c31d-121">Create a database with sqlcmd</span></span>
<span data-ttu-id="7c31d-122">Como alternativa, puede ejecutar Hola mismo comando con sqlcmd ejecutando Hola siguientes en un símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="7c31d-122">Alternatively, you can run hello same command with sqlcmd by running hello following at a command prompt.</span></span>

```sql
sqlcmd -S <Server Name>.database.windows.net -I -U <User> -P <Password> -Q "CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB)"
```

<span data-ttu-id="7c31d-123">intercalación predeterminada de Hello cuando no se especifica es COLLATE SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="7c31d-123">hello default collation when not specified is COLLATE SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="7c31d-124">Hola `MAXSIZE` puede estar comprendido entre 250 GB y TB 240.</span><span class="sxs-lookup"><span data-stu-id="7c31d-124">hello `MAXSIZE` can be between 250 GB and 240 TB.</span></span>  <span data-ttu-id="7c31d-125">Hola `SERVICE_OBJECTIVE` puede estar comprendido entre DW100 y DW2000 [DWU][DWU].</span><span class="sxs-lookup"><span data-stu-id="7c31d-125">hello `SERVICE_OBJECTIVE` can be between DW100 and DW2000 [DWU][DWU].</span></span>  <span data-ttu-id="7c31d-126">Para obtener una lista de todos los valores válidos, vea la documentación de MSDN de Hola para [CREATE DATABASE][CREATE DATABASE].</span><span class="sxs-lookup"><span data-stu-id="7c31d-126">For a list of all valid values, see hello MSDN documentation for [CREATE DATABASE][CREATE DATABASE].</span></span>  <span data-ttu-id="7c31d-127">Hola MAXSIZE y puede SERVICE_OBJECTIVE cambiar con una [ALTER DATABASE] [ ALTER DATABASE] comando T-SQL.</span><span class="sxs-lookup"><span data-stu-id="7c31d-127">Both hello MAXSIZE and SERVICE_OBJECTIVE can be changed with an [ALTER DATABASE][ALTER DATABASE] T-SQL command.</span></span>  <span data-ttu-id="7c31d-128">no se puede cambiar la intercalación de Hola de una base de datos después de su creación.</span><span class="sxs-lookup"><span data-stu-id="7c31d-128">hello collation of a database cannot be changed after creation.</span></span>   <span data-ttu-id="7c31d-129">Debe tener precaución cuando variación hello SERVICE_OBJECTIVE como cambiar de DWU da lugar a un reinicio de servicios, lo que cancela todas las consultas en tránsito.</span><span class="sxs-lookup"><span data-stu-id="7c31d-129">Caution should be used when changing hello SERVICE_OBJECTIVE as changing DWU causes a restart of services, which cancels all queries in flight.</span></span>  <span data-ttu-id="7c31d-130">Con el cambio de MAXSIZE no se reinician servicios, ya que es solo una operación de metadatos sencilla.</span><span class="sxs-lookup"><span data-stu-id="7c31d-130">Changing MAXSIZE does not restart services as it is just a simple metadata operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c31d-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7c31d-131">Next steps</span></span>
<span data-ttu-id="7c31d-132">Después de que el almacenamiento de datos de SQL ha terminado el aprovisionamiento puede [cargar datos de ejemplo] [ load sample data] o desproteger cómo demasiado[desarrollar][develop], [cargar][load], o [migrar][migrate].</span><span class="sxs-lookup"><span data-stu-id="7c31d-132">After your SQL Data Warehouse has finished provisioning you can [load sample data][load sample data] or check out how too[develop][develop], [load][load], or [migrate][migrate].</span></span>

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[how toocreate a SQL Data Warehouse from hello Azure portal]: sql-data-warehouse-get-started-provision.md
[Query Azure SQL Data Warehouse (Visual Studio)]: sql-data-warehouse-query-visual-studio.md
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data]: sql-data-warehouse-load-sample-databases.md
[Create an Azure SQL database with hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group
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
