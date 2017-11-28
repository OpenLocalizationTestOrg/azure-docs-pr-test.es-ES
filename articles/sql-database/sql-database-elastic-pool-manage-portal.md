---
title: "Azure Portal: Creación y administración de un grupo elástico de SQL Database | Microsoft Docs"
description: "Obtenga información acerca de cómo toouse Hola portal de Azure y toomanage de inteligencia incorporada de la base de datos de SQL, supervisar y ajustar un grupo elástico escalable toooptimize base de datos de rendimiento y costo de administrar."
keywords: 
services: sql-database
documentationcenter: 
author: ninarn
manager: jhubbard
editor: cgronlun
ms.assetid: 3dc9b7a3-4b10-423a-8e44-9174aca5cf3d
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 06/06/2016
ms.author: ninarn
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: e0de952bc0c91177f64c04363630783d72435741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-hello-azure-portal"></a><span data-ttu-id="74525-103">Crear y administrar un grupo elástico con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="74525-103">Create and manage an elastic pool with hello Azure portal</span></span>
<span data-ttu-id="74525-104">Este tema muestra cómo toocreate y administrar escalable [grupos elásticos](sql-database-elastic-pool.md) con hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="74525-104">This topic shows you how toocreate and manage scalable [elastic pools](sql-database-elastic-pool.md) with hello Azure portal.</span></span> <span data-ttu-id="74525-105">También puede crear y administrar un grupo elástico Azure con [PowerShell](sql-database-elastic-pool-manage-powershell.md), API de REST de Hola o [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="74525-105">You can also create and manage an Azure elastic pool with [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="74525-106">También puede crear y mover bases de datos dentro y fuera de los grupos elásticos mediante [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="74525-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

## <a name="create-an-elastic-pool"></a><span data-ttu-id="74525-107">Creación de un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="74525-107">Create an elastic pool</span></span> 

<span data-ttu-id="74525-108">Hay dos maneras de crear un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="74525-108">There are two ways you can create an elastic pool.</span></span> <span data-ttu-id="74525-109">Puede hacerlo desde el principio si sabe Hola grupo el programa de instalación que desee, o inicia con una recomendación de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="74525-109">You can do it from scratch if you know hello pool setup you want, or start with a recommendation from hello service.</span></span> <span data-ttu-id="74525-110">Base de datos de SQL tiene inteligencia incorporada que recomienda el programa de instalación de un grupo elástico si es más rentable en función de hello más allá de telemetría de uso para las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="74525-110">SQL Database has built-in intelligence that recommends an elastic pool setup if it's more cost-efficient for you based on hello past usage telemetry for your databases.</span></span>

<span data-ttu-id="74525-111">Puede crear varios grupos en un servidor, pero no se puede agregar las bases de datos de distintos servidores en hello mismo grupo.</span><span class="sxs-lookup"><span data-stu-id="74525-111">You can create multiple pools on a server, but you can't add databases from different servers into hello same pool.</span></span> 

> [!NOTE]
> <span data-ttu-id="74525-112">Los grupos elásticos están disponibles con carácter general (GA) en todas las regiones de Azure excepto oeste de la India, donde actualmente se encuentran en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="74525-112">Elastic pools are generally available (GA) in all Azure regions except West India where it is currently in preview.</span></span>  <span data-ttu-id="74525-113">La disponibilidad general de grupos elásticos en esta región se producirá tan pronto como sea posible.</span><span class="sxs-lookup"><span data-stu-id="74525-113">GA of elastic pools in this region will occur as soon as possible.</span></span>
>

### <a name="step-1-create-an-elastic-pool"></a><span data-ttu-id="74525-114">Paso 1: Crear un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="74525-114">Step 1: Create an elastic pool</span></span>

<span data-ttu-id="74525-115">Crear un grupo elástico de existente **server** hoja en el portal de hello es hello más fáciles manera toomove bases de datos existentes en un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="74525-115">Creating an elastic pool from an existing **server** blade in hello portal is hello easiest way toomove existing databases into an elastic pool.</span></span>

> [!NOTE]
> <span data-ttu-id="74525-116">También puede crear un grupo elástico mediante una búsqueda **grupo elástico de SQL** en hello **Marketplace** o haga clic en **+ agregar** en hello **grupos elásticos SQL**examinar hoja.</span><span class="sxs-lookup"><span data-stu-id="74525-116">You can also create an elastic pool by searching **SQL elastic pool** in hello **Marketplace** or clicking **+Add** in hello **SQL elastic pools** browse blade.</span></span> <span data-ttu-id="74525-117">Es capaz de toospecify un servidor nuevo o existente a través de este flujo de trabajo de aprovisionamiento del bloque.</span><span class="sxs-lookup"><span data-stu-id="74525-117">You are able toospecify a new or existing server through this pool provisioning workflow.</span></span>
>
>

1. <span data-ttu-id="74525-118">Hola [portal de Azure](http://portal.azure.com/), haga clic en **más servicios**  **>**  **servidores SQL Server**y, a continuación, haga clic en servidor de Hola que contiene Hola bases de datos desea que el grupo elástico de tooadd tooan.</span><span class="sxs-lookup"><span data-stu-id="74525-118">In hello [Azure portal](http://portal.azure.com/), click **More services** **>** **SQL servers**, and then click hello server that contains hello databases you want tooadd tooan elastic pool.</span></span>
2. <span data-ttu-id="74525-119">Haga clic en **Grupo nuevo**.</span><span class="sxs-lookup"><span data-stu-id="74525-119">Click **New pool**.</span></span>

    ![Agregar grupo tooa servidor](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    <span data-ttu-id="74525-121">**O**</span><span class="sxs-lookup"><span data-stu-id="74525-121">**-OR-**</span></span>

    <span data-ttu-id="74525-122">Es posible que vea un mensaje que indica que no existe se recomiendan grupos elásticos para servidor hello.</span><span class="sxs-lookup"><span data-stu-id="74525-122">You may see a message saying there are recommended elastic pools for hello server.</span></span> <span data-ttu-id="74525-123">Haga clic en hello toosee Hola mensaje que recomienda pools basándose en la telemetría de uso de la base de datos históricos y, a continuación, haga clic en toosee de nivel de hello más detalles y personalizar el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="74525-123">Click hello message toosee hello recommended pools based on historical database usage telemetry, and then click hello tier toosee more details and customize hello pool.</span></span> <span data-ttu-id="74525-124">Vea [comprender las recomendaciones de grupos](#understand-elastic-pool-recommendations) más adelante en este tema para cómo Hola actuación.</span><span class="sxs-lookup"><span data-stu-id="74525-124">See [Understand pool recommendations](#understand-elastic-pool-recommendations) later in this topic for how hello recommendation is made.</span></span>

    ![grupo recomendado](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. <span data-ttu-id="74525-126">Hola **grupo elástico** aparece hoja, que es donde se especifican los valores de hello para el grupo.</span><span class="sxs-lookup"><span data-stu-id="74525-126">hello **elastic pool** blade appears, which is where you specify hello settings for your pool.</span></span> <span data-ttu-id="74525-127">Si hace clic en **nuevo grupo** en el paso anterior de hello, hello tarifa es **estándar** está seleccionada de forma predeterminada y ninguna base de datos.</span><span class="sxs-lookup"><span data-stu-id="74525-127">If you clicked **New pool** in hello previous step, hello pricing tier is **Standard** by default and no databases is selected.</span></span> <span data-ttu-id="74525-128">Puede crear un grupo vacío o especificar un conjunto de bases de datos de ese toomove de servidor en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="74525-128">You can create an empty pool, or specify a set of existing databases from that server toomove into hello pool.</span></span> <span data-ttu-id="74525-129">Si va a crear un grupo recomendado, Hola recomienda tarifa, configuración de rendimiento y se completan automáticamente la lista de bases de datos, pero todavía se pueden cambiar.</span><span class="sxs-lookup"><span data-stu-id="74525-129">If you are creating a recommended pool, hello recommended pricing tier, performance settings, and list of databases are prepopulated, but you can still change them.</span></span>

    ![Configuración de grupos elásticos](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. <span data-ttu-id="74525-131">Especifique un nombre para el grupo elástico hello, o déjela como valor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="74525-131">Specify a name for hello elastic pool, or leave it as hello default.</span></span>

### <a name="step-2-choose-a-pricing-tier"></a><span data-ttu-id="74525-132">Paso 2: Elegir un plan de tarifa</span><span class="sxs-lookup"><span data-stu-id="74525-132">Step 2: Choose a pricing tier</span></span>

<span data-ttu-id="74525-133">Hello tarifa del grupo determina Hola características elastics toohello disponibles en el grupo de Hola y Hola número máximo de Edtu (eDTU máx.) y la base de datos de almacenamiento (GB) tooeach disponibles.</span><span class="sxs-lookup"><span data-stu-id="74525-133">hello pool's pricing tier determines hello features available toohello elastics in hello pool, and hello maximum number of eDTUs (eDTU MAX), and storage (GBs) available tooeach database.</span></span> <span data-ttu-id="74525-134">Para más detalles, consulte Niveles de servicio.</span><span class="sxs-lookup"><span data-stu-id="74525-134">For details, see Service Tiers.</span></span>

<span data-ttu-id="74525-135">nivel de precios toochange hello para el grupo de hello, haga clic en **tarifa**, haga clic en hello tarifa que desee y, a continuación, haga clic en **seleccione**.</span><span class="sxs-lookup"><span data-stu-id="74525-135">toochange hello pricing tier for hello pool, click **Pricing tier**, click hello pricing tier you want, and then click **Select**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="74525-136">Después de elegir el nivel de precios de Hola y confirmar los cambios, haga clic en **Aceptar** en último paso hello, no será hello toochange capaz de tarifa del grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="74525-136">After you choose hello pricing tier and commit your changes by clicking **OK** in hello last step, you won't be able toochange hello pricing tier of hello pool.</span></span> <span data-ttu-id="74525-137">toochange Hola a nivel de precios para un grupo elástico existente, crear un grupo elástico en el nivel de precios deseada de Hola y migrar toothis nuevo grupo de bases de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="74525-137">toochange hello pricing tier for an existing elastic pool, create an elastic pool in hello desired pricing tier and migrate hello databases toothis new pool.</span></span>
>

![Seleccione un nivel de precios.](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-hello-pool"></a><span data-ttu-id="74525-139">Paso 3: Configurar grupo de Hola</span><span class="sxs-lookup"><span data-stu-id="74525-139">Step 3: Configure hello pool</span></span>

<span data-ttu-id="74525-140">Después de establecer el nivel de precios de hello, haga clic en Configurar grupo que agregar las bases de datos, Edtu de grupo de conjunto y almacenamiento (GB de grupo), y donde establecer hello Edtu min y max para elastics hello en grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="74525-140">After setting hello pricing tier, click Configure pool where you add databases, set pool eDTUs and storage (pool GBs), and where you set hello min and max eDTUs for hello elastics in hello pool.</span></span>

1. <span data-ttu-id="74525-141">Haga clic en **Configurar grupo**</span><span class="sxs-lookup"><span data-stu-id="74525-141">Click **Configure pool**</span></span>
2. <span data-ttu-id="74525-142">Seleccione las bases de datos de hello desea tooadd toohello grupo.</span><span class="sxs-lookup"><span data-stu-id="74525-142">Select hello databases you want tooadd toohello pool.</span></span> <span data-ttu-id="74525-143">Este paso es opcional al crear el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="74525-143">This step is optional while creating hello pool.</span></span> <span data-ttu-id="74525-144">Las bases de datos pueden agregarse una vez creado el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="74525-144">Databases can be added after hello pool has been created.</span></span>
    <span data-ttu-id="74525-145">Haga clic en bases de datos de tooadd, **Agregar base de datos**, haga clic en las bases de datos de Hola que desee tooadd y, a continuación, haga clic en hello **seleccione** botón.</span><span class="sxs-lookup"><span data-stu-id="74525-145">tooadd databases, click **Add database**, click hello databases that you want tooadd, and then click hello **Select** button.</span></span>

    ![Agregar bases de datos](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    <span data-ttu-id="74525-147">Si las bases de datos de Hola que trabaja tienen suficiente telemetría históricas de uso, Hola **estimado de eDTU y GB uso** hello y gráfico **uso de eDTU real** toohelp de actualización de gráfico de barras realizar configuración decisiones.</span><span class="sxs-lookup"><span data-stu-id="74525-147">If hello databases you're working with have enough historical usage telemetry, hello **Estimated eDTU and GB usage** graph and hello **Actual eDTU usage** bar chart update toohelp you make configuration decisions.</span></span> <span data-ttu-id="74525-148">Además, servicio de hello puede proporcionarle un toohelp de mensaje de recomendación, ajustar Hola grupo.</span><span class="sxs-lookup"><span data-stu-id="74525-148">Also, hello service may give you a recommendation message toohelp you right-size hello pool.</span></span> <span data-ttu-id="74525-149">Consulte [Recomendaciones dinámicas](#understand-elastic-pool-recommendations).</span><span class="sxs-lookup"><span data-stu-id="74525-149">See [Dynamic Recommendations](#understand-elastic-pool-recommendations).</span></span>

3. <span data-ttu-id="74525-150">Usar controles de hello en hello **Configurar grupo** tooexplore configuración de página y configurar el grupo de servidores.</span><span class="sxs-lookup"><span data-stu-id="74525-150">Use hello controls on hello **Configure pool** page tooexplore settings and configure your pool.</span></span> <span data-ttu-id="74525-151">Consulte los [límites de los grupos elásticos](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) para ver más información sobre los límites de cada nivel de servicio y las [consideraciones sobre precios y rendimiento para los grupos elásticos](sql-database-elastic-pool.md) para ver instrucciones detalladas sobre el ajuste de tamaño correcto de un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="74525-151">See [Elastic pools limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for more detail about limits for each service tier, and see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md) for detailed guidance on right-sizing an elastic pool.</span></span> <span data-ttu-id="74525-152">Para más información sobre la configuración del grupo, consulte las [propiedades del grupo elástico](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span><span class="sxs-lookup"><span data-stu-id="74525-152">For more information about pool settings, see [Elastic pool properties](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span></span>

    ![Configuración de grupos elásticos](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. <span data-ttu-id="74525-154">Haga clic en **seleccione** en hello **Configurar grupo** hoja después de cambiar la configuración.</span><span class="sxs-lookup"><span data-stu-id="74525-154">Click **Select** in hello **Configure Pool** blade after changing settings.</span></span>
5. <span data-ttu-id="74525-155">Haga clic en **Aceptar** grupo de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="74525-155">Click **OK** toocreate hello pool.</span></span>

## <a name="understand-elastic-pool-recommendations"></a><span data-ttu-id="74525-156">Descripción de las recomendaciones de grupos elásticos</span><span class="sxs-lookup"><span data-stu-id="74525-156">Understand elastic pool recommendations</span></span>

<span data-ttu-id="74525-157">Hola servicio de base de datos SQL se evalúa como el historial de uso y recomienda uno o más grupos cuando resulta más rentable que las bases de datos único.</span><span class="sxs-lookup"><span data-stu-id="74525-157">hello SQL Database service evaluates usage history and recommends one or more pools when it is more cost-effective than using single databases.</span></span> <span data-ttu-id="74525-158">Cada recomendación se configura con un subconjunto de las bases de datos del servidor de Hola que mejor se ajustan grupo Hola único.</span><span class="sxs-lookup"><span data-stu-id="74525-158">Each recommendation is configured with a unique subset of hello server's databases that best fit hello pool.</span></span>

![grupo recomendado](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

<span data-ttu-id="74525-160">recomendación de grupo de Hello consta de:</span><span class="sxs-lookup"><span data-stu-id="74525-160">hello pool recommendation comprises:</span></span>

- <span data-ttu-id="74525-161">Un nivel de precios para el grupo de hello (Basic, Standard, Premium o Premium RS)</span><span class="sxs-lookup"><span data-stu-id="74525-161">A pricing tier for hello pool (Basic, Standard, Premium, or Premium RS)</span></span>
- <span data-ttu-id="74525-162">Las **eDTU del grupo** adecuadas (también denominadas eDTU máx. por grupo)</span><span class="sxs-lookup"><span data-stu-id="74525-162">Appropriate **POOL eDTUs** (also called Max eDTUs per pool)</span></span>
- <span data-ttu-id="74525-163">Hola **eDTU máxima** y **eDTU mín.** por base de datos</span><span class="sxs-lookup"><span data-stu-id="74525-163">hello **eDTU MAX** and **eDTU Min** per database</span></span>
- <span data-ttu-id="74525-164">lista de Hola de bases de datos recomendados para el grupo de Hola</span><span class="sxs-lookup"><span data-stu-id="74525-164">hello list of recommended databases for hello pool</span></span>

> [!IMPORTANT]
> <span data-ttu-id="74525-165">servicio de Hello tiene últimos 30 días de telemetría de hello en cuenta al recomendar grupos.</span><span class="sxs-lookup"><span data-stu-id="74525-165">hello service takes hello last 30 days of telemetry into account when recommending pools.</span></span> <span data-ttu-id="74525-166">Para toobe de base de datos que se consideran como candidata para un grupo elástico, debe existir para al menos 7 días.</span><span class="sxs-lookup"><span data-stu-id="74525-166">For a database toobe considered as a candidate for an elastic pool, it must exist for at least 7 days.</span></span> <span data-ttu-id="74525-167">Las bases de datos que ya están en un grupo elástico no se consideran candidatas para las recomendaciones de grupos elásticos.</span><span class="sxs-lookup"><span data-stu-id="74525-167">Databases that are already in an elastic pool are not considered as candidates for elastic pool recommendations.</span></span>
>

<span data-ttu-id="74525-168">servicio de Hello evalúa las necesidades de recursos y rentabilidad de hello móvil único bases de datos en cada nivel de servicio en grupos de hello mismo nivel.</span><span class="sxs-lookup"><span data-stu-id="74525-168">hello service evaluates resource needs and cost effectiveness of moving hello single databases in each service tier into pools of hello same tier.</span></span> <span data-ttu-id="74525-169">Por ejemplo, se evalúan todas las bases de datos Standard en un servidor para que quepan en un bloque de bases de datos elásticas Standard.</span><span class="sxs-lookup"><span data-stu-id="74525-169">For example, all Standard databases on a server are assessed for their fit into a Standard Elastic Pool.</span></span> <span data-ttu-id="74525-170">Esto significa servicio hello no hace recomendaciones de nivel entre como mover una base de datos estándar en un grupo de Premium.</span><span class="sxs-lookup"><span data-stu-id="74525-170">This means hello service does not make cross-tier recommendations such as moving a Standard database into a Premium pool.</span></span>

<span data-ttu-id="74525-171">Después de agregar el grupo de servidores de bases de datos toohello, las recomendaciones se generan dinámicamente según el uso históricos Hola de bases de datos de Hola que seleccionó.</span><span class="sxs-lookup"><span data-stu-id="74525-171">After adding databases toohello pool, recommendations are dynamically generated based on hello historical usage of hello databases you have selected.</span></span> <span data-ttu-id="74525-172">Estas recomendaciones se muestran en hello eDTU y GB gráfico de uso y de un encabezado de recomendación en parte superior de Hola de hello **Configurar grupo** hoja.</span><span class="sxs-lookup"><span data-stu-id="74525-172">These recommendations are shown in hello eDTU and GB usage chart and in a recommendation banner at hello top of hello **Configure pool** blade.</span></span> <span data-ttu-id="74525-173">Estas recomendaciones son tooassist previsto en la creación de un grupo elástico optimizado para las bases de datos específicos.</span><span class="sxs-lookup"><span data-stu-id="74525-173">These recommendations are intended tooassist you in creating an elastic pool optimized for your specific databases.</span></span>

![Recomendaciones dinámicas](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

## <a name="manage-and-monitor-an-elastic-pool"></a><span data-ttu-id="74525-175">Administración y supervisión de un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="74525-175">Manage and monitor an elastic pool</span></span>

<span data-ttu-id="74525-176">Puede usar hello toomonitor de portal de Azure y administrar bases de datos de hello en el grupo de Hola y un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="74525-176">You can use hello Azure portal toomonitor and manage an elastic pool and hello databases in hello pool.</span></span> <span data-ttu-id="74525-177">Desde el portal de hello, puede supervisar el uso de Hola de un grupo elástico y bases de datos de hello dentro de ese grupo.</span><span class="sxs-lookup"><span data-stu-id="74525-177">From hello portal, you can monitor hello utilization of an elastic pool and hello databases within that pool.</span></span> <span data-ttu-id="74525-178">También puede realizar un conjunto de cambios grupo elástico tooyour y enviar todos los cambios realizados en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="74525-178">You can also make a set of changes tooyour elastic pool and submit all changes at hello same time.</span></span> <span data-ttu-id="74525-179">Estos cambios incluyen agregar o quitar bases de datos, cambiar la configuración del grupo elástico o cambiar la configuración de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="74525-179">These changes include adding or removing databases, changing your elastic pool settings, or changing your database settings.</span></span>

<span data-ttu-id="74525-180">Hola siguiente gráfico muestra un grupo elástico de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="74525-180">hello following graphic shows an example elastic pool.</span></span> <span data-ttu-id="74525-181">vista de Hello incluye:</span><span class="sxs-lookup"><span data-stu-id="74525-181">hello view includes:</span></span>

*  <span data-ttu-id="74525-182">Gráficos para supervisar el uso de recursos de grupo elástico de Hola y bases de datos de hello contenidas en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="74525-182">Charts for monitoring resource usage of both hello elastic pool and hello databases contained in hello pool.</span></span>
*  <span data-ttu-id="74525-183">Hola **configurar** grupo botón toomake cambia toohello de grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="74525-183">hello **Configure** pool button toomake changes toohello elastic pool.</span></span>
*  <span data-ttu-id="74525-184">Hola **crear base de datos** botón que crea una base de datos y lo agrega el grupo elástico de toohello actual.</span><span class="sxs-lookup"><span data-stu-id="74525-184">hello **Create database** button that creates a database and adds it toohello current elastic pool.</span></span>
*  <span data-ttu-id="74525-185">Los trabajos elásticos que le ayudarán a administran un gran número de bases de datos mediante la ejecución de scripts de Transact SQL en todas las bases de datos de una lista.</span><span class="sxs-lookup"><span data-stu-id="74525-185">Elastic jobs that help you manage large numbers of databases by running Transact SQL scripts against all databases in a list.</span></span>

![Vista Grupo][2]

<span data-ttu-id="74525-187">Puede ir tooa determinado grupo toosee su utilización de recursos.</span><span class="sxs-lookup"><span data-stu-id="74525-187">You can go tooa particular pool toosee its resource utilization.</span></span> <span data-ttu-id="74525-188">De forma predeterminada, el grupo de hello es uso de eDTU y almacenamiento de tooshow configurado para hello última hora.</span><span class="sxs-lookup"><span data-stu-id="74525-188">By default, hello pool is configured tooshow storage and eDTU usage for hello last hour.</span></span> <span data-ttu-id="74525-189">gráfico de Hello puede ser tooshow configurado diferentes métricas sobre varias ventanas de tiempo.</span><span class="sxs-lookup"><span data-stu-id="74525-189">hello chart can be configured tooshow different metrics over various time windows.</span></span>

1. <span data-ttu-id="74525-190">Seleccione un toowork grupo elástico con.</span><span class="sxs-lookup"><span data-stu-id="74525-190">Select an elastic pool toowork with.</span></span>
2. <span data-ttu-id="74525-191">En **Supervisión de grupo elástico** hay un gráfico con la etiqueta **Uso de recursos**.</span><span class="sxs-lookup"><span data-stu-id="74525-191">Under **Elastic Pool Monitoring** is a chart labeled **Resource utilization**.</span></span> <span data-ttu-id="74525-192">Haga clic en el gráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="74525-192">Click hello chart.</span></span>

    ![Supervisión de grupo elástico][3]

    <span data-ttu-id="74525-194">Hola **métrica** abre la hoja, que muestra una vista detallada de Hola especificados métricas en el período de tiempo especificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="74525-194">hello **Metric** blade opens, showing a detailed view of hello specified metrics over hello specified time window.</span></span>   

    ![Cuadro de métricas][9]

### <a name="toocustomize-hello-chart-display"></a><span data-ttu-id="74525-196">presentación de gráfico de hello toocustomize</span><span class="sxs-lookup"><span data-stu-id="74525-196">toocustomize hello chart display</span></span>

<span data-ttu-id="74525-197">Puede editar gráfico de Hola y Hola hoja métrica toodisplay otras métricas como porcentaje de CPU, porcentaje de E/S de datos y porcentaje de E/S de registro utilizado.</span><span class="sxs-lookup"><span data-stu-id="74525-197">You can edit hello chart and hello metric blade toodisplay other metrics such as CPU percentage, data IO percentage, and log IO percentage used.</span></span>

1. <span data-ttu-id="74525-198">En la hoja de métricas de hello, haga clic en **editar**.</span><span class="sxs-lookup"><span data-stu-id="74525-198">On hello metric blade, click **Edit**.</span></span>

    ![Haga clic en Editar.][6]

2. <span data-ttu-id="74525-200">Hola **Editar gráfico** hoja, seleccione un intervalo de tiempo (más allá de la hora, en la actualidad, o más allá de la semana), o haga clic en **personalizado** tooselect cualquier intervalo de fechas en hello dos últimas semanas.</span><span class="sxs-lookup"><span data-stu-id="74525-200">In hello **Edit Chart** blade, select a time range (past hour, today, or past week), or click **custom** tooselect any date range in hello last two weeks.</span></span> <span data-ttu-id="74525-201">Seleccionar tipo de gráfico de hello (barra o línea), a continuación, seleccione Hola recursos toomonitor.</span><span class="sxs-lookup"><span data-stu-id="74525-201">Select hello chart type (bar or line), then select hello resources toomonitor.</span></span>

   > [!Note]
   > <span data-ttu-id="74525-202">Solo el gráfico de métricas con hello misma unidad de medida se pueden mostrar en hello en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="74525-202">Only metrics with hello same unit of measure can be displayed in hello chart at hello same time.</span></span> <span data-ttu-id="74525-203">Por ejemplo, si selecciona "porcentaje de eDTU" solo puede seleccionar otras métricas de porcentaje como unidad de medida de Hola.</span><span class="sxs-lookup"><span data-stu-id="74525-203">For example, if you select "eDTU percentage" then you can only select other metrics with percentage as hello unit of measure.</span></span>
   >

    ![Haga clic en Editar.](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. <span data-ttu-id="74525-205">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="74525-205">Then click **OK**.</span></span>

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a><span data-ttu-id="74525-206">Administración y supervisión de bases de datos en un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="74525-206">Manage and monitor databases in an elastic pool</span></span>

<span data-ttu-id="74525-207">También se pueden supervisar bases de datos individuales en caso de un problema potencial.</span><span class="sxs-lookup"><span data-stu-id="74525-207">Individual databases can also be monitored for potential trouble.</span></span>

1. <span data-ttu-id="74525-208">En **Supervisión de base de datos elástica**hay un gráfico que muestra las métricas para cinco bases de datos.</span><span class="sxs-lookup"><span data-stu-id="74525-208">Under **Elastic Database Monitoring**, there is a chart that displays metrics for five databases.</span></span> <span data-ttu-id="74525-209">De forma predeterminada, Hola gráfico muestra hello principales 5 bases de datos en bloque de hello mediante el uso de eDTU promedio en hello última hora.</span><span class="sxs-lookup"><span data-stu-id="74525-209">By default, hello chart displays hello top 5 databases in hello pool by average eDTU usage in hello past hour.</span></span> <span data-ttu-id="74525-210">Haga clic en el gráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="74525-210">Click hello chart.</span></span>

    ![Supervisión de grupo elástico][4]

2. <span data-ttu-id="74525-212">Hola **utilización de recursos de base de datos** aparece hoja.</span><span class="sxs-lookup"><span data-stu-id="74525-212">hello **Database Resource Utilization** blade appears.</span></span> <span data-ttu-id="74525-213">Esto proporciona una vista detallada de uso de la base de datos de hello en bloque de Hola.</span><span class="sxs-lookup"><span data-stu-id="74525-213">This provides a detailed view of hello database usage in hello pool.</span></span> <span data-ttu-id="74525-214">Con la cuadrícula de hello en parte inferior de Hola de hoja de hello, puede seleccionar las bases de datos en hello grupo toodisplay su uso en el gráfico de hello (seguridad de bases de datos de too5).</span><span class="sxs-lookup"><span data-stu-id="74525-214">Using hello grid in hello lower part of hello blade, you can select any databases in hello pool toodisplay its usage in hello chart (up too5 databases).</span></span> <span data-ttu-id="74525-215">También puede personalizar la ventana de métricas y la hora de hello muestra en el gráfico de hello haciendo clic en **Editar gráfico**.</span><span class="sxs-lookup"><span data-stu-id="74525-215">You can also customize hello metrics and time window displayed in hello chart by clicking **Edit chart**.</span></span>

    ![Hoja de utilización de recursos de base de datos][8]

### <a name="toocustomize-hello-view"></a><span data-ttu-id="74525-217">vista de hello toocustomize</span><span class="sxs-lookup"><span data-stu-id="74525-217">toocustomize hello view</span></span>

1. <span data-ttu-id="74525-218">Hola **utilización de recursos de la base de datos** hoja, haga clic en **Editar gráfico**.</span><span class="sxs-lookup"><span data-stu-id="74525-218">In hello **Database resource utilization** blade, click **Edit chart**.</span></span>

    ![Clic en Editar gráfico](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. <span data-ttu-id="74525-220">Hola **editar** hoja de gráfico, seleccione un intervalo de tiempo (más allá de hora o más allá de 24 horas) o haga clic en **personalizado** tooselect día diferente en hello más allá de toodisplay de 2 semanas.</span><span class="sxs-lookup"><span data-stu-id="74525-220">In hello **Edit** chart blade, select a time range (past hour or past 24 hours), or click **custom** tooselect a different day in hello past 2 weeks toodisplay.</span></span>

    ![Clic en Personalizado](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. <span data-ttu-id="74525-222">Haga clic en hello **comparar las bases de datos** tooselect un toouse métrica diferentes al comparar las bases de datos de lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="74525-222">Click hello **Compare databases by** dropdown tooselect a different metric toouse when comparing databases.</span></span>

    ![Editar gráfico de Hola](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a><span data-ttu-id="74525-224">tooselect toomonitor de bases de datos</span><span class="sxs-lookup"><span data-stu-id="74525-224">tooselect databases toomonitor</span></span>

<span data-ttu-id="74525-225">En la lista de bases de datos de Hola Hola **utilización de recursos de base de datos** hoja, puede encontrar las bases de datos determinadas consultando a través de páginas de hello en lista de Hola o escribiendo en nombre de Hola de una base de datos.</span><span class="sxs-lookup"><span data-stu-id="74525-225">In hello database list in hello **Database Resource Utilization** blade, you can find particular databases by looking through hello pages in hello list or by typing in hello name of a database.</span></span> <span data-ttu-id="74525-226">Base de datos de uso Hola casilla tooselect Hola.</span><span class="sxs-lookup"><span data-stu-id="74525-226">Use hello checkbox tooselect hello database.</span></span>

![Busque toomonitor de bases de datos][7]


## <a name="add-an-alert-tooan-elastic-pool-resource"></a><span data-ttu-id="74525-228">Agregar un recurso de grupo elástico tooan alerta</span><span class="sxs-lookup"><span data-stu-id="74525-228">Add an alert tooan elastic pool resource</span></span>

<span data-ttu-id="74525-229">Puede agregar el grupo elástico de reglas tooan que envíe correo electrónico de alerta o toopeople cadenas tooURL los puntos de conexión al grupo elástico Hola alcanza un umbral de uso que configuró.</span><span class="sxs-lookup"><span data-stu-id="74525-229">You can add rules tooan elastic pool that send email toopeople or alert strings tooURL endpoints when hello elastic pool hits a utilization threshold that you set up.</span></span>

<span data-ttu-id="74525-230">**tooadd un recurso de tooany alerta:**</span><span class="sxs-lookup"><span data-stu-id="74525-230">**tooadd an alert tooany resource:**</span></span>

1. <span data-ttu-id="74525-231">Haga clic en hello **utilización de recursos** Hola de gráfico tooopen **métrica** hoja, haga clic en **Agregar alerta**y, a continuación, rellene la información de Hola Hola **agregar una alerta regla** hoja (**recursos** se configura automáticamente de grupo de hello toobe trabaja con).</span><span class="sxs-lookup"><span data-stu-id="74525-231">Click hello **Resource utilization** chart tooopen hello **Metric** blade, click **Add alert**, and then fill out hello information in hello **Add an alert rule** blade (**Resource** is automatically set up toobe hello pool you're working with).</span></span>
2. <span data-ttu-id="74525-232">Escriba un **nombre** y **descripción** que identifica tooyou alerta hello y destinatarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="74525-232">Type a **Name** and **Description** that identifies hello alert tooyou and hello recipients.</span></span>
3. <span data-ttu-id="74525-233">Elija un **métrica** que desea tooalert de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="74525-233">Choose a **Metric** that you want tooalert from hello list.</span></span>

    <span data-ttu-id="74525-234">gráfico de Hello dinámicamente muestra la utilización de recursos para esa métrica toohelp que elija un umbral.</span><span class="sxs-lookup"><span data-stu-id="74525-234">hello chart dynamically shows resource utilization for that metric toohelp you choose a threshold.</span></span>

4. <span data-ttu-id="74525-235">Elija una **condición** (mayor que, menor que, etc.) y un **umbral**.</span><span class="sxs-lookup"><span data-stu-id="74525-235">Choose a **Condition** (greater than, less than, etc.) and a **Threshold**.</span></span>
5. <span data-ttu-id="74525-236">Elija un **período** de tiempo que Hola métrica regla debe cumplirse antes de desencadenadores de alerta de Hola.</span><span class="sxs-lookup"><span data-stu-id="74525-236">Choose a **Period** of time that hello metric rule must be satisfied before hello alert triggers.</span></span>
6. <span data-ttu-id="74525-237">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="74525-237">Click **OK**.</span></span>

<span data-ttu-id="74525-238">Para más información, consulte cómo [crear alertas de SQL Database en Azure Portal](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="74525-238">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="74525-239">Movimiento de una base de datos a un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="74525-239">Move a database into an elastic pool</span></span>

<span data-ttu-id="74525-240">Puede agregar o quitar las bases de datos de un grupo existente.</span><span class="sxs-lookup"><span data-stu-id="74525-240">You can add or remove databases from an existing pool.</span></span> <span data-ttu-id="74525-241">las bases de datos de Hello pueden estar en otros grupos.</span><span class="sxs-lookup"><span data-stu-id="74525-241">hello databases can be in other pools.</span></span> <span data-ttu-id="74525-242">Sin embargo, solo puede agregar bases de datos que están en Hola mismo servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="74525-242">However, you can only add databases that are on hello same logical server.</span></span>

1. <span data-ttu-id="74525-243">En la hoja de hello para el grupo de hello, en **bases de datos elásticas** haga clic en **Configurar grupo**.</span><span class="sxs-lookup"><span data-stu-id="74525-243">In hello blade for hello pool, under **Elastic databases** click **Configure pool**.</span></span>

    ![Haga clic en Configurar grupo.][1]

2. <span data-ttu-id="74525-245">Hola **Configurar grupo** hoja, haga clic en **agregar toopool**.</span><span class="sxs-lookup"><span data-stu-id="74525-245">In hello **Configure pool** blade, click **Add toopool**.</span></span>

    ![Haga clic en Agregar toopool](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. <span data-ttu-id="74525-247">Hola **agregar bases de datos** hoja, base de datos de hello select o el grupo de servidores de bases de datos tooadd toohello.</span><span class="sxs-lookup"><span data-stu-id="74525-247">In hello **Add databases** blade, select hello database or databases tooadd toohello pool.</span></span> <span data-ttu-id="74525-248">Después, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="74525-248">Then click **Select**.</span></span>

    ![Seleccione las bases de datos tooadd](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    <span data-ttu-id="74525-250">Hola **Configurar grupo** hoja ahora listas Hola base de datos seleccionada toobe agregado, con su estado establecido demasiado**pendiente**.</span><span class="sxs-lookup"><span data-stu-id="74525-250">hello **Configure pool** blade now lists hello database you selected toobe added, with its status set too**Pending**.</span></span>

    ![Adiciones de grupo pendientes.](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. <span data-ttu-id="74525-252">Hola **hoja de grupo configurar**, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="74525-252">In hello **Configure pool blade**, click **Save**.</span></span>

    ![Haga clic en Guardar](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="74525-254">Movimiento de una base de datos fuera de un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="74525-254">Move a database out of an elastic pool</span></span>

1. <span data-ttu-id="74525-255">Hola **Configurar grupo** hoja, base de datos seleccione Hola o tooremove de las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="74525-255">In hello **Configure pool** blade, select hello database or databases tooremove.</span></span>

    ![lista de bases de datos](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. <span data-ttu-id="74525-257">Haga clic en **Quitar del grupo**.</span><span class="sxs-lookup"><span data-stu-id="74525-257">Click **Remove from pool**.</span></span>

    ![lista de bases de datos](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    <span data-ttu-id="74525-259">Hola **Configurar grupo** hoja ahora listas Hola base de datos seleccionada toobe quitado junto con su estado establecido demasiado**pendiente**.</span><span class="sxs-lookup"><span data-stu-id="74525-259">hello **Configure pool** blade now lists hello database you selected toobe removed with its status set too**Pending**.</span></span>

    ![Adición de base de datos de vista previa y eliminación](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. <span data-ttu-id="74525-261">Hola **hoja de grupo configurar**, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="74525-261">In hello **Configure pool blade**, click **Save**.</span></span>

    ![Haga clic en Guardar](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="74525-263">Cambio de la configuración de rendimiento de un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="74525-263">Change performance settings of an elastic pool</span></span>

<span data-ttu-id="74525-264">Al supervisar la utilización de recursos de Hola de un grupo elástico, es posible que descubra que no se necesitan algunos ajustes.</span><span class="sxs-lookup"><span data-stu-id="74525-264">As you monitor hello resource utilization of an elastic pool, you may discover that some adjustments are needed.</span></span> <span data-ttu-id="74525-265">Quizá grupo Hola necesita un cambio en los límites de rendimiento o almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="74525-265">Maybe hello pool needs a change in hello performance or storage limits.</span></span> <span data-ttu-id="74525-266">Posiblemente desee toochange configuración de base de datos de hello en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="74525-266">Possibly you want toochange hello database settings in hello pool.</span></span> <span data-ttu-id="74525-267">Puede cambiar el programa de instalación de Hola de grupo de Hola en cualquier momento tooget Hola mejor equilibrio entre rendimiento y costo.</span><span class="sxs-lookup"><span data-stu-id="74525-267">You can change hello setup of hello pool at any time tooget hello best balance of performance and cost.</span></span> <span data-ttu-id="74525-268">Consulte [¿Cuándo se debe utilizar un grupo elástico?](sql-database-elastic-pool.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="74525-268">See [When should an elastic pool be used?](sql-database-elastic-pool.md) for more information.</span></span>

<span data-ttu-id="74525-269">toochange hello Edtu o almacenamiento limita por grupo y Edtu por base de datos:</span><span class="sxs-lookup"><span data-stu-id="74525-269">toochange hello eDTUs or storage limits per pool, and eDTUs per database:</span></span>

1. <span data-ttu-id="74525-270">Abra hello **Configurar grupo** hoja.</span><span class="sxs-lookup"><span data-stu-id="74525-270">Open hello **Configure pool** blade.</span></span>

    <span data-ttu-id="74525-271">En **configuración de grupo elástico**, use cualquier configuración del grupo de control deslizante toochange Hola.</span><span class="sxs-lookup"><span data-stu-id="74525-271">Under **elastic pool settings**, use either slider toochange hello pool settings.</span></span>

    ![Uso de recursos de grupos elásticos](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. <span data-ttu-id="74525-273">Cuando se cambia la configuración de hello, hello muestra hello mensual costo estimado de cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="74525-273">When hello setting changes, hello display shows hello estimated monthly cost of hello change.</span></span>

    ![Actualización de un grupo elástico y nuevo coste mensual](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="74525-275">Latencia de las operaciones de grupos elásticos</span><span class="sxs-lookup"><span data-stu-id="74525-275">Latency of elastic pool operations</span></span>
* <span data-ttu-id="74525-276">Cambiar normalmente Hola min Edtu por base de datos o el número máximo de Edtu por base de datos completa en 5 minutos o menos.</span><span class="sxs-lookup"><span data-stu-id="74525-276">Changing hello min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="74525-277">Cambiar hello Edtu por grupo de depende de la cantidad total de Hola de espacio utilizado por todas las bases de datos de grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="74525-277">Changing hello eDTUs per pool depends on hello total amount of space used by all databases in hello pool.</span></span> <span data-ttu-id="74525-278">Los cambios tienen un duración media de 90 minutos o menos por cada 100 GB.</span><span class="sxs-lookup"><span data-stu-id="74525-278">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="74525-279">Por ejemplo, si utiliza el espacio total de Hola por todas las bases de datos de grupo de hello es de 200 GB, Hola espera latencia para cambiar hello eDTU del grupo por grupo es de 3 horas o menos.</span><span class="sxs-lookup"><span data-stu-id="74525-279">For example, if hello total space used by all databases in hello pool is 200 GB, then hello expected latency for changing hello pool eDTU per pool is 3 hours or less.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74525-280">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="74525-280">Next steps</span></span>

- <span data-ttu-id="74525-281">toounderstand qué un grupo elástico, consulte [grupo elástico de base de datos SQL](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="74525-281">toounderstand what an elastic pool is, see [SQL Database elastic pool](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="74525-282">Para una guía sobre cómo usar grupos elásticos, consulte las [consideraciones de precio y rendimiento para grupos elásticos](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="74525-282">For guidance on using elastic pools, see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="74525-283">secuencias de comandos de toouse trabajos elástico toorun Transact-SQL frente a cualquier número de bases de datos en el grupo de hello, vea [información general de los trabajos elástico](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="74525-283">toouse elastic jobs toorun Transact-SQL scripts against any number of databases in hello pool, see [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span>
- <span data-ttu-id="74525-284">tooquery a través de cualquier número de bases de datos en el grupo de hello, consulte [información general sobre consultas elástico](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="74525-284">tooquery across any number of databases in hello pool, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
- <span data-ttu-id="74525-285">Para las transacciones de cualquier número de bases de datos en el grupo de hello, consulte [transacciones elásticas](sql-database-elastic-transactions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="74525-285">For transactions any number of databases in hello pool, see [Elastic transactions](sql-database-elastic-transactions-overview.md).</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-pool-manage-portal/configure-pool.png
[2]: ./media/sql-database-elastic-pool-manage-portal/basic.png
[3]: ./media/sql-database-elastic-pool-manage-portal/basic-2.png
[4]: ./media/sql-database-elastic-pool-manage-portal/basic-3.png
[5]: ./media/sql-database-elastic-pool-manage-portal/elastic-jobs.png
[6]: ./media/sql-database-elastic-pool-manage-portal/edit-metric.png
[7]: ./media/sql-database-elastic-pool-manage-portal/select-dbs.png
[8]: ./media/sql-database-elastic-pool-manage-portal/db-utilization.png
[9]: ./media/sql-database-elastic-pool-manage-portal/metric.png
