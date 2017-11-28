---
title: "Creación de una instancia de SQL Data Warehouse en Azure Portal | Microsoft Docs"
description: Aprenda a crear una instancia de Almacenamiento de datos SQL de Azure en el Portal de Azure
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: 552e496e-d560-419c-9996-6bbc80c521cb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 24ed2d8bad3090e378acf2a42fb909dee0a8517b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-sql-data-warehouse"></a><span data-ttu-id="72834-103">Creación de una instancia de Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="72834-103">Create an Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="72834-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="72834-104">Azure portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="72834-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="72834-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="72834-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="72834-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="72834-107">En este tutorial se usa el Portal de Azure para crear una instancia de Almacenamiento de datos SQL que contiene la base de datos de ejemplo AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="72834-107">This tutorial uses the Azure portal to create a SQL Data Warehouse that contains an AdventureWorksDW sample database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72834-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="72834-108">Prerequisites</span></span>
<span data-ttu-id="72834-109">Para empezar, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="72834-109">To get started, you need:</span></span>

* <span data-ttu-id="72834-110">**Cuenta de Azure**: visite las secciones sobre [evaluación gratuita de Azure][Azure Free Trial] o [Crédito mensual de MSDN de Azure][MSDN Azure Credits] para crear una cuenta.</span><span class="sxs-lookup"><span data-stu-id="72834-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] to create an account.</span></span>
* <span data-ttu-id="72834-111">**Azure SQL Server**: consulte [Creación de una base de datos de Azure SQL con Azure Portal][Create an Azure SQL database in the Azure portal] para más información.</span><span class="sxs-lookup"><span data-stu-id="72834-111">**Azure SQL server**:  See [Create an Azure SQL database with the Azure portal][Create an Azure SQL database in the Azure portal] for more details.</span></span>

> [!NOTE]
> <span data-ttu-id="72834-112">La creación de una instancia de Almacenamiento de datos SQL puede dar lugar a un nuevo servicio facturable.</span><span class="sxs-lookup"><span data-stu-id="72834-112">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="72834-113">Consulte [Precios de SQL Data Warehouse][SQL Data Warehouse pricing] para más información.</span><span class="sxs-lookup"><span data-stu-id="72834-113">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="72834-114">Creación de Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="72834-114">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="72834-115">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="72834-115">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="72834-116">Haga clic en **+ Nuevo** > **Bases de datos** > **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="72834-116">Click **+ New** > **Databases** > **SQL Data Warehouse**.</span></span>

    ![Crear](./media/sql-data-warehouse-get-started-provision/create-sample.gif)
3. <span data-ttu-id="72834-118">En la hoja **Almacenamiento de datos SQL** , rellene la información necesaria y presione 'Crear' para crearlo.</span><span class="sxs-lookup"><span data-stu-id="72834-118">In the **SQL Data Warehouse** blade, fill in the information needed, then press 'Create' to create.</span></span>

    ![Crear base de datos](./media/sql-data-warehouse-get-started-provision/create-database.png)

   * <span data-ttu-id="72834-120">**Servidor**: se recomienda que seleccione primero su servidor.</span><span class="sxs-lookup"><span data-stu-id="72834-120">**Server**: We recommend you select your server first.</span></span>  
   * <span data-ttu-id="72834-121">**Nombre de la base de datos**: el nombre que se usa para hacer referencia a Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="72834-121">**Database name**: The name that is used to reference the SQL Data Warehouse.</span></span>  <span data-ttu-id="72834-122">Debe ser exclusivo en el servidor.</span><span class="sxs-lookup"><span data-stu-id="72834-122">It must be unique to the server.</span></span>
   * <span data-ttu-id="72834-123">**Rendimiento**: se recomienda empezar con 400 [DWU][DWU].</span><span class="sxs-lookup"><span data-stu-id="72834-123">**Performance**: We recommend starting with 400 [DWUs][DWU].</span></span> <span data-ttu-id="72834-124">Puede mover el control deslizante hacia la izquierda o la derecha para ajustar el rendimiento de su almacén de datos, o bien para reducirlo o escalarlo verticalmente una vez creado.</span><span class="sxs-lookup"><span data-stu-id="72834-124">You can move the slider to the left or right to adjust the performance of your data warehouse, or scale up or down after creation.</span></span>  <span data-ttu-id="72834-125">Para aprender más sobre las DWU, consulte la documentación sobre el [escalado](sql-data-warehouse-manage-compute-overview.md) o nuestra [página de precios][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="72834-125">To learn more about DWUs, see our documentation on [scaling](sql-data-warehouse-manage-compute-overview.md) or our [pricing page][SQL Data Warehouse pricing].</span></span>
   * <span data-ttu-id="72834-126">**Suscripción**: seleccione la [suscripción] a la que se facturará esta instancia de Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="72834-126">**Subscription**: Select the [subscription] that this SQL Data Warehouse will bill to.</span></span>
   * <span data-ttu-id="72834-127">**Grupo de recursos**: los [grupos de recursos][Resource group] son contenedores diseñados para ayudarle a administrar una colección de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="72834-127">**Resource group**: [Resource groups][Resource group] are containers designed to help you manage a collection of Azure resources.</span></span> <span data-ttu-id="72834-128">Más información sobre los [grupos de recursos](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="72834-128">Learn more about [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="72834-129">**Selección del origen**: haga clic en **Seleccionar origen** > **Ejemplo**.</span><span class="sxs-lookup"><span data-stu-id="72834-129">**Select source**: Click **Select source** > **Sample**.</span></span> <span data-ttu-id="72834-130">Azure rellena automáticamente la opción **Seleccionar muestra** con AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="72834-130">Azure automatically populates the **Select sample** option with AdventureWorksDW.</span></span>

   > [!NOTE]
   > <span data-ttu-id="72834-131">La intercalación predeterminada para un Almacenamiento de datos SQL es SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="72834-131">The default collation for a SQL Data Warehouse is SQL_Latin1_General_CP1_CI_AS.</span></span> <span data-ttu-id="72834-132">Si se necesita una intercalación distinta, puede utilizar [T-SQL][T-SQL] para crear la base de datos con otra intercalación.</span><span class="sxs-lookup"><span data-stu-id="72834-132">If a different collation is needed, [T-SQL][T-SQL] can be used to create the database with a different collation.</span></span>
   >
   >

1. <span data-ttu-id="72834-133">Haga clic en **Crear** para crear su instancia de Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="72834-133">Click **Create** to create your SQL Data Warehouse.</span></span>
2. <span data-ttu-id="72834-134">Espere unos minutos.</span><span class="sxs-lookup"><span data-stu-id="72834-134">Wait for a few minutes.</span></span> <span data-ttu-id="72834-135">Cuando el almacén de datos está listo, debería volver al [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="72834-135">When your data warehouse is ready, you should be returned to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="72834-136">Encontrará Almacenamiento de datos SQL en el panel, entre las bases de datos SQL o en el grupo de recursos que usó para crearlo.</span><span class="sxs-lookup"><span data-stu-id="72834-136">You can find your SQL Data Warehouse on your dashboard, listed under your SQL Databases, or in the resource group that you used to create it.</span></span>

    ![Vista del portal](./media/sql-data-warehouse-get-started-provision/database-portal-view.png)

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="72834-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="72834-138">Next steps</span></span>
<span data-ttu-id="72834-139">Ahora que ha creado una instancia de Almacenamiento de datos SQL, está listo para [conectarse](sql-data-warehouse-connect-overview.md) y empezar a realizar consultas.</span><span class="sxs-lookup"><span data-stu-id="72834-139">Now that you have created a SQL Data Warehouse, you are ready to [Connect](sql-data-warehouse-connect-overview.md) and begin querying.</span></span>

<span data-ttu-id="72834-140">Para cargar datos en Almacenamiento de datos SQL, consulte la [información general sobre la carga](sql-data-warehouse-overview-load.md).</span><span class="sxs-lookup"><span data-stu-id="72834-140">To load data into SQL Data Warehouse, see the [loading overview](sql-data-warehouse-overview-load.md).</span></span>

<span data-ttu-id="72834-141">Si está intentando migrar una base de datos existente a SQL Data Warehouse, consulte [ Información general sobre migración](sql-data-warehouse-overview-migrate.md) o use la [utilidad de migración](sql-data-warehouse-migrate-migration-utility.md).</span><span class="sxs-lookup"><span data-stu-id="72834-141">If you are trying to migrate an existing database to SQL Data Warehouse, see the [Migration overview](sql-data-warehouse-overview-migrate.md) or use [Migration Utility](sql-data-warehouse-migrate-migration-utility.md).</span></span>

<span data-ttu-id="72834-142">Las reglas de firewall también se pueden configurar mediante Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="72834-142">Firewall rules can also be configured using Transact-SQL.</span></span> <span data-ttu-id="72834-143">Para más información, consulte [sp_set_firewall_rule][sp_set_firewall_rule] y [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span><span class="sxs-lookup"><span data-stu-id="72834-143">For more information, see [sp_set_firewall_rule][sp_set_firewall_rule] and [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span></span>

<span data-ttu-id="72834-144">También es una buena idea echar un vistazo a los [procedimientos recomendados][Best practices].</span><span class="sxs-lookup"><span data-stu-id="72834-144">It's also a great idea to look at the [Best practices][Best practices].</span></span>

<!--Article references-->
[Create an Azure SQL database in the Azure portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[resource groups]: ../azure-resource-manager/resource-group-template-deploy-portal.md
[Best practices]: sql-data-warehouse-best-practices.md
[DWU]: sql-data-warehouse-overview-what-is.md
<span data-ttu-id="72834-145">[suscripción]: ../azure-glossary-cloud-terminology.md#subscription</span><span class="sxs-lookup"><span data-stu-id="72834-145">[subscription]: ../azure-glossary-cloud-terminology.md#subscription</span></span>
[resource group]: ../azure-glossary-cloud-terminology.md#resource-group
[T-SQL]: ./sql-data-warehouse-get-started-create-database-tsql.md

<!--MSDN references-->
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
