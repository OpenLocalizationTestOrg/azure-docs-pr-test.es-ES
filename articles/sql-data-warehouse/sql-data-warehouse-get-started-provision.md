---
title: aaaCreate un almacenamiento de datos de SQL en hello portal de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un almacenamiento de datos de SQL Azure en Hola portal de Azure"
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
ms.openlocfilehash: f5be6e3f2936e3af9d099854a468f8ce66fd8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-sql-data-warehouse"></a><span data-ttu-id="67e9b-103">Creación de una instancia de Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="67e9b-103">Create an Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="67e9b-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="67e9b-104">Azure portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="67e9b-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="67e9b-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="67e9b-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="67e9b-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="67e9b-107">Este tutorial usa hello toocreate portal Azure un almacenamiento de datos de SQL que contiene una base de datos de ejemplo AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="67e9b-107">This tutorial uses hello Azure portal toocreate a SQL Data Warehouse that contains an AdventureWorksDW sample database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67e9b-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="67e9b-108">Prerequisites</span></span>
<span data-ttu-id="67e9b-109">tooget iniciado, debe:</span><span class="sxs-lookup"><span data-stu-id="67e9b-109">tooget started, you need:</span></span>

* <span data-ttu-id="67e9b-110">**Cuenta de Azure**: visite [evaluación gratuita de Azure] [ Azure Free Trial] o [créditos de Azure de MSDN] [ MSDN Azure Credits] toocreate una cuenta.</span><span class="sxs-lookup"><span data-stu-id="67e9b-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="67e9b-111">**Servidor de SQL Azure**: vea [crear una base de datos de SQL Azure con hello portal de Azure] [ Create an Azure SQL database in hello Azure portal] para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="67e9b-111">**Azure SQL server**:  See [Create an Azure SQL database with hello Azure portal][Create an Azure SQL database in hello Azure portal] for more details.</span></span>

> [!NOTE]
> <span data-ttu-id="67e9b-112">La creación de una instancia de Almacenamiento de datos SQL puede dar lugar a un nuevo servicio facturable.</span><span class="sxs-lookup"><span data-stu-id="67e9b-112">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="67e9b-113">Consulte [Precios de SQL Data Warehouse][SQL Data Warehouse pricing] para más información.</span><span class="sxs-lookup"><span data-stu-id="67e9b-113">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="67e9b-114">Creación de Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="67e9b-114">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="67e9b-115">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="67e9b-115">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="67e9b-116">Haga clic en **+ Nuevo** > **Bases de datos** > **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="67e9b-116">Click **+ New** > **Databases** > **SQL Data Warehouse**.</span></span>

    ![Crear](./media/sql-data-warehouse-get-started-provision/create-sample.gif)
3. <span data-ttu-id="67e9b-118">Hola **almacenamiento de datos SQL** hoja, rellene la información de hello necesaria, a continuación, presione toocreate 'Create'.</span><span class="sxs-lookup"><span data-stu-id="67e9b-118">In hello **SQL Data Warehouse** blade, fill in hello information needed, then press 'Create' toocreate.</span></span>

    ![Crear base de datos](./media/sql-data-warehouse-get-started-provision/create-database.png)

   * <span data-ttu-id="67e9b-120">**Servidor**: se recomienda que seleccione primero su servidor.</span><span class="sxs-lookup"><span data-stu-id="67e9b-120">**Server**: We recommend you select your server first.</span></span>  
   * <span data-ttu-id="67e9b-121">**Nombre de base de datos**: nombre de Hola Hola tooreference usa almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="67e9b-121">**Database name**: hello name that is used tooreference hello SQL Data Warehouse.</span></span>  <span data-ttu-id="67e9b-122">Debe ser toohello único servidor.</span><span class="sxs-lookup"><span data-stu-id="67e9b-122">It must be unique toohello server.</span></span>
   * <span data-ttu-id="67e9b-123">**Rendimiento**: se recomienda empezar con 400 [DWU][DWU].</span><span class="sxs-lookup"><span data-stu-id="67e9b-123">**Performance**: We recommend starting with 400 [DWUs][DWU].</span></span> <span data-ttu-id="67e9b-124">Puede mover hello toohello de control deslizante izquierdo o derecho de rendimiento de hello tooadjust del almacén de datos o de escala hacia arriba o hacia abajo después de la creación.</span><span class="sxs-lookup"><span data-stu-id="67e9b-124">You can move hello slider toohello left or right tooadjust hello performance of your data warehouse, or scale up or down after creation.</span></span>  <span data-ttu-id="67e9b-125">toolearn más información acerca de a Dwu, consulte la documentación en [escalado](sql-data-warehouse-manage-compute-overview.md) o nuestro [página de precios][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="67e9b-125">toolearn more about DWUs, see our documentation on [scaling](sql-data-warehouse-manage-compute-overview.md) or our [pricing page][SQL Data Warehouse pricing].</span></span>
   * <span data-ttu-id="67e9b-126">**Suscripción**: Hola seleccione [suscripción] que se facturar este almacén de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="67e9b-126">**Subscription**: Select hello [subscription] that this SQL Data Warehouse will bill to.</span></span>
   * <span data-ttu-id="67e9b-127">**Grupo de recursos**: [grupos de recursos] [ Resource group] son toohelp contenedores diseñados administrar una colección de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="67e9b-127">**Resource group**: [Resource groups][Resource group] are containers designed toohelp you manage a collection of Azure resources.</span></span> <span data-ttu-id="67e9b-128">Más información sobre los [grupos de recursos](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="67e9b-128">Learn more about [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="67e9b-129">**Selección del origen**: haga clic en **Seleccionar origen** > **Ejemplo**.</span><span class="sxs-lookup"><span data-stu-id="67e9b-129">**Select source**: Click **Select source** > **Sample**.</span></span> <span data-ttu-id="67e9b-130">Azure rellena automáticamente hello **ejemplo seleccione** opción con AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="67e9b-130">Azure automatically populates hello **Select sample** option with AdventureWorksDW.</span></span>

   > [!NOTE]
   > <span data-ttu-id="67e9b-131">intercalación predeterminada de Hola para un almacenamiento de datos de SQL es SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="67e9b-131">hello default collation for a SQL Data Warehouse is SQL_Latin1_General_CP1_CI_AS.</span></span> <span data-ttu-id="67e9b-132">Si se necesita una intercalación diferente, [T-SQL] [ T-SQL] puede ser la base de datos de uso toocreate Hola con una intercalación diferente.</span><span class="sxs-lookup"><span data-stu-id="67e9b-132">If a different collation is needed, [T-SQL][T-SQL] can be used toocreate hello database with a different collation.</span></span>
   >
   >

1. <span data-ttu-id="67e9b-133">Haga clic en **crear** toocreate de almacenamiento de los datos SQL.</span><span class="sxs-lookup"><span data-stu-id="67e9b-133">Click **Create** toocreate your SQL Data Warehouse.</span></span>
2. <span data-ttu-id="67e9b-134">Espere unos minutos.</span><span class="sxs-lookup"><span data-stu-id="67e9b-134">Wait for a few minutes.</span></span> <span data-ttu-id="67e9b-135">Una vez preparado el almacenamiento de datos, se debe devolver toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="67e9b-135">When your data warehouse is ready, you should be returned toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="67e9b-136">Puede encontrar el almacenamiento de datos de SQL en el panel, aparecen en las bases de datos SQL, o en recursos de hello grupo utilizó toocreate lo.</span><span class="sxs-lookup"><span data-stu-id="67e9b-136">You can find your SQL Data Warehouse on your dashboard, listed under your SQL Databases, or in hello resource group that you used toocreate it.</span></span>

    ![Vista del portal](./media/sql-data-warehouse-get-started-provision/database-portal-view.png)

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="67e9b-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="67e9b-138">Next steps</span></span>
<span data-ttu-id="67e9b-139">Ahora que ha creado un almacén de datos de SQL, está listo demasiado[conectar](sql-data-warehouse-connect-overview.md) y empezar a consultar.</span><span class="sxs-lookup"><span data-stu-id="67e9b-139">Now that you have created a SQL Data Warehouse, you are ready too[Connect](sql-data-warehouse-connect-overview.md) and begin querying.</span></span>

<span data-ttu-id="67e9b-140">tooload de datos en almacenamiento de datos de SQL, vea hello [cargar información general sobre](sql-data-warehouse-overview-load.md).</span><span class="sxs-lookup"><span data-stu-id="67e9b-140">tooload data into SQL Data Warehouse, see hello [loading overview](sql-data-warehouse-overview-load.md).</span></span>

<span data-ttu-id="67e9b-141">Si está tratando de toomigrate un tooSQL existente de la base de datos almacén de datos, vea hello [Introducción a la migración](sql-data-warehouse-overview-migrate.md) o use [utilidad de migración](sql-data-warehouse-migrate-migration-utility.md).</span><span class="sxs-lookup"><span data-stu-id="67e9b-141">If you are trying toomigrate an existing database tooSQL Data Warehouse, see hello [Migration overview](sql-data-warehouse-overview-migrate.md) or use [Migration Utility](sql-data-warehouse-migrate-migration-utility.md).</span></span>

<span data-ttu-id="67e9b-142">Las reglas de firewall también se pueden configurar mediante Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="67e9b-142">Firewall rules can also be configured using Transact-SQL.</span></span> <span data-ttu-id="67e9b-143">Para más información, consulte [sp_set_firewall_rule][sp_set_firewall_rule] y [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span><span class="sxs-lookup"><span data-stu-id="67e9b-143">For more information, see [sp_set_firewall_rule][sp_set_firewall_rule] and [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span></span>

<span data-ttu-id="67e9b-144">También es un toolook buena idea en hello [prácticas recomendadas][Best practices].</span><span class="sxs-lookup"><span data-stu-id="67e9b-144">It's also a great idea toolook at hello [Best practices][Best practices].</span></span>

<!--Article references-->
[Create an Azure SQL database in hello Azure portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[resource groups]: ../azure-resource-manager/resource-group-template-deploy-portal.md
[Best practices]: sql-data-warehouse-best-practices.md
[DWU]: sql-data-warehouse-overview-what-is.md
[suscripción]: ../azure-glossary-cloud-terminology.md#subscription
[resource group]: ../azure-glossary-cloud-terminology.md#resource-group
[T-SQL]: ./sql-data-warehouse-get-started-create-database-tsql.md

<!--MSDN references-->
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
