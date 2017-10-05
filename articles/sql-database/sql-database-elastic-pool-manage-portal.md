---
title: "Azure Portal: Creación y administración de un grupo elástico de SQL Database | Microsoft Docs"
description: "Aprenda a usar la inteligencia integrada de Azure Portal y SQL Database para administrar y supervisar un grupo elástico escalable, así como para identificar su tamaño más adecuado, con el objetivo de optimizar el rendimiento de las bases de datos y administrar los costes."
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
ms.openlocfilehash: 4ffd1db31f42967dc7f07aa979898dddbb333641
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-an-elastic-pool-with-the-azure-portal"></a><span data-ttu-id="a9709-103">Creación y administración de un grupo elástico con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a9709-103">Create and manage an elastic pool with the Azure portal</span></span>
<span data-ttu-id="a9709-104">En este tema se muestra cómo crear y administrar [grupos elásticos](sql-database-elastic-pool.md) escalables con Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a9709-104">This topic shows you how to create and manage scalable [elastic pools](sql-database-elastic-pool.md) with the Azure portal.</span></span> <span data-ttu-id="a9709-105">También puede crear y administrar un grupo elástico de Azure con [PowerShell](sql-database-elastic-pool-manage-powershell.md), la API de REST o [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="a9709-105">You can also create and manage an Azure elastic pool with [PowerShell](sql-database-elastic-pool-manage-powershell.md), the REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="a9709-106">También puede crear y mover bases de datos dentro y fuera de los grupos elásticos mediante [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="a9709-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

## <a name="create-an-elastic-pool"></a><span data-ttu-id="a9709-107">Creación de un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="a9709-107">Create an elastic pool</span></span> 

<span data-ttu-id="a9709-108">Hay dos maneras de crear un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="a9709-108">There are two ways you can create an elastic pool.</span></span> <span data-ttu-id="a9709-109">Puede partir de cero si conoce la configuración deseada del grupo, o comenzar con una recomendación del servicio.</span><span class="sxs-lookup"><span data-stu-id="a9709-109">You can do it from scratch if you know the pool setup you want, or start with a recommendation from the service.</span></span> <span data-ttu-id="a9709-110">Base de datos SQL es una base de datos inteligente que recomienda la configuración de grupo elástico más rentable, en función de los datos de telemetría de uso pasados de las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="a9709-110">SQL Database has built-in intelligence that recommends an elastic pool setup if it's more cost-efficient for you based on the past usage telemetry for your databases.</span></span>

<span data-ttu-id="a9709-111">Puede crear varios grupos a un servidor, pero no puede agregar bases de datos de servidores diferentes al mismo grupo.</span><span class="sxs-lookup"><span data-stu-id="a9709-111">You can create multiple pools on a server, but you can't add databases from different servers into the same pool.</span></span> 

> [!NOTE]
> <span data-ttu-id="a9709-112">Los grupos elásticos están disponibles con carácter general (GA) en todas las regiones de Azure excepto oeste de la India, donde actualmente se encuentran en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="a9709-112">Elastic pools are generally available (GA) in all Azure regions except West India where it is currently in preview.</span></span>  <span data-ttu-id="a9709-113">La disponibilidad general de grupos elásticos en esta región se producirá tan pronto como sea posible.</span><span class="sxs-lookup"><span data-stu-id="a9709-113">GA of elastic pools in this region will occur as soon as possible.</span></span>
>

### <a name="step-1-create-an-elastic-pool"></a><span data-ttu-id="a9709-114">Paso 1: Crear un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="a9709-114">Step 1: Create an elastic pool</span></span>

<span data-ttu-id="a9709-115">Crear un grupo elástico a partir de una hoja de **servidor** que ya existe en el portal es la forma más sencilla de mover bases de datos existentes a un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="a9709-115">Creating an elastic pool from an existing **server** blade in the portal is the easiest way to move existing databases into an elastic pool.</span></span>

> [!NOTE]
> <span data-ttu-id="a9709-116">También puede crear un grupo elástico si busca **grupo elástico de SQL** en **Marketplace** o hace clic en **+Agregar** en la hoja para examinar **Grupos elásticos de SQL**.</span><span class="sxs-lookup"><span data-stu-id="a9709-116">You can also create an elastic pool by searching **SQL elastic pool** in the **Marketplace** or clicking **+Add** in the **SQL elastic pools** browse blade.</span></span> <span data-ttu-id="a9709-117">Puede especificar un servidor nuevo o existente por medio de este flujo de trabajo de aprovisionamiento de grupo.</span><span class="sxs-lookup"><span data-stu-id="a9709-117">You are able to specify a new or existing server through this pool provisioning workflow.</span></span>
>
>

1. <span data-ttu-id="a9709-118">En [Azure Portal](http://portal.azure.com/), haga clic en **Más servicios** **>** **Servidores SQL Server** y, luego, en el servidor que contiene las bases de datos que desea agregar a un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="a9709-118">In the [Azure portal](http://portal.azure.com/), click **More services** **>** **SQL servers**, and then click the server that contains the databases you want to add to an elastic pool.</span></span>
2. <span data-ttu-id="a9709-119">Haga clic en **Grupo nuevo**.</span><span class="sxs-lookup"><span data-stu-id="a9709-119">Click **New pool**.</span></span>

    ![Adición de un grupo a un servidor](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    <span data-ttu-id="a9709-121">**O**</span><span class="sxs-lookup"><span data-stu-id="a9709-121">**-OR-**</span></span>

    <span data-ttu-id="a9709-122">Quizá vea un mensaje que indica que existen grupos elásticos recomendados para el servidor.</span><span class="sxs-lookup"><span data-stu-id="a9709-122">You may see a message saying there are recommended elastic pools for the server.</span></span> <span data-ttu-id="a9709-123">Haga clic en el mensaje para ver los grupos recomendados según la telemetría de uso histórica de base de datos y, después, en el nivel para ver más detalles y personalizar el grupo.</span><span class="sxs-lookup"><span data-stu-id="a9709-123">Click the message to see the recommended pools based on historical database usage telemetry, and then click the tier to see more details and customize the pool.</span></span> <span data-ttu-id="a9709-124">Consulte [Descripción de las recomendaciones de grupos](#understand-elastic-pool-recommendations) más adelante en este tema para ver cómo se realiza la recomendación.</span><span class="sxs-lookup"><span data-stu-id="a9709-124">See [Understand pool recommendations](#understand-elastic-pool-recommendations) later in this topic for how the recommendation is made.</span></span>

    ![grupo recomendado](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. <span data-ttu-id="a9709-126">Aparece la hoja del **grupo elástico**, que es donde va a especificar la configuración del grupo.</span><span class="sxs-lookup"><span data-stu-id="a9709-126">The **elastic pool** blade appears, which is where you specify the settings for your pool.</span></span> <span data-ttu-id="a9709-127">Si hizo clic en **Grupo nuevo** en el paso anterior, el plan de tarifa es **Estándar** de forma predeterminada y aún no hay bases de datos seleccionadas.</span><span class="sxs-lookup"><span data-stu-id="a9709-127">If you clicked **New pool** in the previous step, the pricing tier is **Standard** by default and no databases is selected.</span></span> <span data-ttu-id="a9709-128">Puede crear un grupo vacío o especificar un conjunto de bases de datos existentes de ese servidor para moverlas al grupo.</span><span class="sxs-lookup"><span data-stu-id="a9709-128">You can create an empty pool, or specify a set of existing databases from that server to move into the pool.</span></span> <span data-ttu-id="a9709-129">Si va a crear un grupo recomendado, ya estarán llenos el plan de tarifa recomendado, la configuración de rendimiento y la lista de bases de datos, aunque todavía puede hacer cambios.</span><span class="sxs-lookup"><span data-stu-id="a9709-129">If you are creating a recommended pool, the recommended pricing tier, performance settings, and list of databases are prepopulated, but you can still change them.</span></span>

    ![Configuración de grupos elásticos](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. <span data-ttu-id="a9709-131">Especifique un nombre para el grupo elástico o deje el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="a9709-131">Specify a name for the elastic pool, or leave it as the default.</span></span>

### <a name="step-2-choose-a-pricing-tier"></a><span data-ttu-id="a9709-132">Paso 2: Elegir un plan de tarifa</span><span class="sxs-lookup"><span data-stu-id="a9709-132">Step 2: Choose a pricing tier</span></span>

<span data-ttu-id="a9709-133">El plan de tarifa del grupo determina las características disponibles para las bases de datos elásticas del grupo, además de la cantidad máxima de eDTU (eDTU MÁX.) y el almacenamiento (GB) disponibles para cada base de datos.</span><span class="sxs-lookup"><span data-stu-id="a9709-133">The pool's pricing tier determines the features available to the elastics in the pool, and the maximum number of eDTUs (eDTU MAX), and storage (GBs) available to each database.</span></span> <span data-ttu-id="a9709-134">Para más detalles, consulte Niveles de servicio.</span><span class="sxs-lookup"><span data-stu-id="a9709-134">For details, see Service Tiers.</span></span>

<span data-ttu-id="a9709-135">Para cambiar el plan de tarifa del grupo, haga clic en **Plan de tarifa**, en el plan de tarifa que prefiera y en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="a9709-135">To change the pricing tier for the pool, click **Pricing tier**, click the pricing tier you want, and then click **Select**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a9709-136">Después de elegirlo y hacer clic en **Aceptar** en el último paso para confirmar los cambios, no podrá cambiar el plan de tarifa del grupo.</span><span class="sxs-lookup"><span data-stu-id="a9709-136">After you choose the pricing tier and commit your changes by clicking **OK** in the last step, you won't be able to change the pricing tier of the pool.</span></span> <span data-ttu-id="a9709-137">Para cambiar el plan de tarifa de un grupo elástico existente, cree un grupo elástico en el plan de tarifa que quiera y migre las bases de datos al nuevo grupo.</span><span class="sxs-lookup"><span data-stu-id="a9709-137">To change the pricing tier for an existing elastic pool, create an elastic pool in the desired pricing tier and migrate the databases to this new pool.</span></span>
>

![Seleccione un nivel de precios.](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-the-pool"></a><span data-ttu-id="a9709-139">Paso 3: Configurar el grupo</span><span class="sxs-lookup"><span data-stu-id="a9709-139">Step 3: Configure the pool</span></span>

<span data-ttu-id="a9709-140">Después de establecer el plan de tarifa, haga clic en Configurar grupo donde agregar bases de datos, establezca las eDTU y el almacenamiento (GB del grupo) y el lugar en que se establecen las eDTU mínima y máxima para las bases de datos elásticas del grupo.</span><span class="sxs-lookup"><span data-stu-id="a9709-140">After setting the pricing tier, click Configure pool where you add databases, set pool eDTUs and storage (pool GBs), and where you set the min and max eDTUs for the elastics in the pool.</span></span>

1. <span data-ttu-id="a9709-141">Haga clic en **Configurar grupo**</span><span class="sxs-lookup"><span data-stu-id="a9709-141">Click **Configure pool**</span></span>
2. <span data-ttu-id="a9709-142">Seleccione las bases de datos que desea agregar al grupo.</span><span class="sxs-lookup"><span data-stu-id="a9709-142">Select the databases you want to add to the pool.</span></span> <span data-ttu-id="a9709-143">Este paso es opcional al crear el grupo.</span><span class="sxs-lookup"><span data-stu-id="a9709-143">This step is optional while creating the pool.</span></span> <span data-ttu-id="a9709-144">Se pueden agregar bases de datos una vez creado el grupo.</span><span class="sxs-lookup"><span data-stu-id="a9709-144">Databases can be added after the pool has been created.</span></span>
    <span data-ttu-id="a9709-145">Para agregar bases de datos, haga clic en **Agregar base de datos**, en las bases de datos que quiera agregar y en el botón **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="a9709-145">To add databases, click **Add database**, click the databases that you want to add, and then click the **Select** button.</span></span>

    ![Agregar bases de datos](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    <span data-ttu-id="a9709-147">Si está trabajando con bases de datos que tienen suficiente telemetría de historial de uso, el gráfico **Estimated eDTU and GB usage** (Uso estimado de eDTU y GB) y el gráfico de barras **Actual eDTU usage** (Uso real de eDTU) se actualizan para ayudarle a tomar decisiones de configuración.</span><span class="sxs-lookup"><span data-stu-id="a9709-147">If the databases you're working with have enough historical usage telemetry, the **Estimated eDTU and GB usage** graph and the **Actual eDTU usage** bar chart update to help you make configuration decisions.</span></span> <span data-ttu-id="a9709-148">Además, el servicio puede proporcionar un mensaje de recomendación que le ayuda a ajustar el tamaño correcto del grupo.</span><span class="sxs-lookup"><span data-stu-id="a9709-148">Also, the service may give you a recommendation message to help you right-size the pool.</span></span> <span data-ttu-id="a9709-149">Consulte [Recomendaciones dinámicas](#understand-elastic-pool-recommendations).</span><span class="sxs-lookup"><span data-stu-id="a9709-149">See [Dynamic Recommendations](#understand-elastic-pool-recommendations).</span></span>

3. <span data-ttu-id="a9709-150">Use los controles de la página **Configurar grupo** para explorar las opciones y configurar el grupo.</span><span class="sxs-lookup"><span data-stu-id="a9709-150">Use the controls on the **Configure pool** page to explore settings and configure your pool.</span></span> <span data-ttu-id="a9709-151">Consulte los [límites de los grupos elásticos](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) para ver más información sobre los límites de cada nivel de servicio y las [consideraciones sobre precios y rendimiento para los grupos elásticos](sql-database-elastic-pool.md) para ver instrucciones detalladas sobre el ajuste de tamaño correcto de un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="a9709-151">See [Elastic pools limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for more detail about limits for each service tier, and see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md) for detailed guidance on right-sizing an elastic pool.</span></span> <span data-ttu-id="a9709-152">Para más información sobre la configuración del grupo, consulte las [propiedades del grupo elástico](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span><span class="sxs-lookup"><span data-stu-id="a9709-152">For more information about pool settings, see [Elastic pool properties](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span></span>

    ![Configuración de grupos elásticos](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. <span data-ttu-id="a9709-154">Haga clic en **Seleccionar** in the **Configure Pool** después de cambiar la configuración.</span><span class="sxs-lookup"><span data-stu-id="a9709-154">Click **Select** in the **Configure Pool** blade after changing settings.</span></span>
5. <span data-ttu-id="a9709-155">Haga clic en **Aceptar** para crear el grupo.</span><span class="sxs-lookup"><span data-stu-id="a9709-155">Click **OK** to create the pool.</span></span>

## <a name="understand-elastic-pool-recommendations"></a><span data-ttu-id="a9709-156">Descripción de las recomendaciones de grupos elásticos</span><span class="sxs-lookup"><span data-stu-id="a9709-156">Understand elastic pool recommendations</span></span>

<span data-ttu-id="a9709-157">El servicio Base de datos SQL evalúa el historial de uso y recomienda uno o varios grupos cuando sea más económico que usar bases de datos únicas.</span><span class="sxs-lookup"><span data-stu-id="a9709-157">The SQL Database service evaluates usage history and recommends one or more pools when it is more cost-effective than using single databases.</span></span> <span data-ttu-id="a9709-158">Cada recomendación se configura con un subconjunto único de las bases de datos del servidor que mejor se ajustan al grupo.</span><span class="sxs-lookup"><span data-stu-id="a9709-158">Each recommendation is configured with a unique subset of the server's databases that best fit the pool.</span></span>

![grupo recomendado](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

<span data-ttu-id="a9709-160">La recomendación de grupo consta de:</span><span class="sxs-lookup"><span data-stu-id="a9709-160">The pool recommendation comprises:</span></span>

- <span data-ttu-id="a9709-161">Un plan de tarifa del grupo (Básico, Estándar, Premium o Premium RS)</span><span class="sxs-lookup"><span data-stu-id="a9709-161">A pricing tier for the pool (Basic, Standard, Premium, or Premium RS)</span></span>
- <span data-ttu-id="a9709-162">Las **eDTU del grupo** adecuadas (también denominadas eDTU máx. por grupo)</span><span class="sxs-lookup"><span data-stu-id="a9709-162">Appropriate **POOL eDTUs** (also called Max eDTUs per pool)</span></span>
- <span data-ttu-id="a9709-163">Las **eDTU máx.** y **eDTU mín.** por base de datos</span><span class="sxs-lookup"><span data-stu-id="a9709-163">The **eDTU MAX** and **eDTU Min** per database</span></span>
- <span data-ttu-id="a9709-164">La lista de bases de datos recomendadas para el grupo</span><span class="sxs-lookup"><span data-stu-id="a9709-164">The list of recommended databases for the pool</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a9709-165">El servicio tiene en cuenta los últimos 30 días de telemetría al recomendar grupos.</span><span class="sxs-lookup"><span data-stu-id="a9709-165">The service takes the last 30 days of telemetry into account when recommending pools.</span></span> <span data-ttu-id="a9709-166">Para que una base de datos se considere una candidata para un grupo elástico, debe tener una existencia mínima de 7 días.</span><span class="sxs-lookup"><span data-stu-id="a9709-166">For a database to be considered as a candidate for an elastic pool, it must exist for at least 7 days.</span></span> <span data-ttu-id="a9709-167">Las bases de datos que ya están en un grupo elástico no se consideran candidatas para las recomendaciones de grupos elásticos.</span><span class="sxs-lookup"><span data-stu-id="a9709-167">Databases that are already in an elastic pool are not considered as candidates for elastic pool recommendations.</span></span>
>

<span data-ttu-id="a9709-168">El servicio evalúa las necesidades de recursos y la rentabilidad de mover las bases de datos únicas de cada nivel de servicio a grupos del mismo nivel.</span><span class="sxs-lookup"><span data-stu-id="a9709-168">The service evaluates resource needs and cost effectiveness of moving the single databases in each service tier into pools of the same tier.</span></span> <span data-ttu-id="a9709-169">Por ejemplo, se evalúan todas las bases de datos Standard en un servidor para que quepan en un bloque de bases de datos elásticas Standard.</span><span class="sxs-lookup"><span data-stu-id="a9709-169">For example, all Standard databases on a server are assessed for their fit into a Standard Elastic Pool.</span></span> <span data-ttu-id="a9709-170">Esto significa que el servicio no hace recomendaciones entre niveles como, por ejemplo, mover una base de datos Standard a un grupo Premium.</span><span class="sxs-lookup"><span data-stu-id="a9709-170">This means the service does not make cross-tier recommendations such as moving a Standard database into a Premium pool.</span></span>

<span data-ttu-id="a9709-171">Después de agregar las bases de datos al grupo, las recomendaciones se generarán dinámicamente basándose en el historial de uso de las bases de datos que se han seleccionado.</span><span class="sxs-lookup"><span data-stu-id="a9709-171">After adding databases to the pool, recommendations are dynamically generated based on the historical usage of the databases you have selected.</span></span> <span data-ttu-id="a9709-172">Estas recomendaciones se muestran en el gráfico de uso de eDTU y GB, y en un mensaje emergente de recomendación en la parte superior de la hoja **Configurar grupo**.</span><span class="sxs-lookup"><span data-stu-id="a9709-172">These recommendations are shown in the eDTU and GB usage chart and in a recommendation banner at the top of the **Configure pool** blade.</span></span> <span data-ttu-id="a9709-173">Estas recomendaciones están pensadas para ayudarle a crear un grupo elástico optimizado para sus bases de datos concretas.</span><span class="sxs-lookup"><span data-stu-id="a9709-173">These recommendations are intended to assist you in creating an elastic pool optimized for your specific databases.</span></span>

![Recomendaciones dinámicas](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

## <a name="manage-and-monitor-an-elastic-pool"></a><span data-ttu-id="a9709-175">Administración y supervisión de un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="a9709-175">Manage and monitor an elastic pool</span></span>

<span data-ttu-id="a9709-176">Puede utilizar Azure Portal para supervisar y administrar un grupo elástico y las bases de datos de este.</span><span class="sxs-lookup"><span data-stu-id="a9709-176">You can use the Azure portal to monitor and manage an elastic pool and the databases in the pool.</span></span> <span data-ttu-id="a9709-177">En el portal, puede supervisar el uso de un grupo elástico y las bases de datos dentro de ese grupo.</span><span class="sxs-lookup"><span data-stu-id="a9709-177">From the portal, you can monitor the utilization of an elastic pool and the databases within that pool.</span></span> <span data-ttu-id="a9709-178">También puede realizar un conjunto de cambios en el grupo elástico y enviar todos los cambios a la vez.</span><span class="sxs-lookup"><span data-stu-id="a9709-178">You can also make a set of changes to your elastic pool and submit all changes at the same time.</span></span> <span data-ttu-id="a9709-179">Estos cambios incluyen agregar o quitar bases de datos, cambiar la configuración del grupo elástico o cambiar la configuración de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="a9709-179">These changes include adding or removing databases, changing your elastic pool settings, or changing your database settings.</span></span>

<span data-ttu-id="a9709-180">El siguiente gráfico muestra un grupo elástico de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a9709-180">The following graphic shows an example elastic pool.</span></span> <span data-ttu-id="a9709-181">La vista incluye:</span><span class="sxs-lookup"><span data-stu-id="a9709-181">The view includes:</span></span>

*  <span data-ttu-id="a9709-182">Los gráficos para supervisar el uso de recursos del grupo elástico y las bases de datos contenidas en el grupo.</span><span class="sxs-lookup"><span data-stu-id="a9709-182">Charts for monitoring resource usage of both the elastic pool and the databases contained in the pool.</span></span>
*  <span data-ttu-id="a9709-183">El botón **Configurar grupo** para realizar cambios en el grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="a9709-183">The **Configure** pool button to make changes to the elastic pool.</span></span>
*  <span data-ttu-id="a9709-184">El botón **Crear base de datos** que crea una base de datos y la agrega al grupo elástico actual.</span><span class="sxs-lookup"><span data-stu-id="a9709-184">The **Create database** button that creates a database and adds it to the current elastic pool.</span></span>
*  <span data-ttu-id="a9709-185">Los trabajos elásticos que le ayudarán a administran un gran número de bases de datos mediante la ejecución de scripts de Transact SQL en todas las bases de datos de una lista.</span><span class="sxs-lookup"><span data-stu-id="a9709-185">Elastic jobs that help you manage large numbers of databases by running Transact SQL scripts against all databases in a list.</span></span>

![Vista Grupo][2]

<span data-ttu-id="a9709-187">Puede ir a un grupo concreto para ver su utilización de recursos.</span><span class="sxs-lookup"><span data-stu-id="a9709-187">You can go to a particular pool to see its resource utilization.</span></span> <span data-ttu-id="a9709-188">De forma predeterminada, el grupo está configurado para mostrar el almacenamiento y el uso de eDTU durante la última hora.</span><span class="sxs-lookup"><span data-stu-id="a9709-188">By default, the pool is configured to show storage and eDTU usage for the last hour.</span></span> <span data-ttu-id="a9709-189">El gráfico puede configurarse para mostrar métricas diferentes en varias ventanas de tiempo.</span><span class="sxs-lookup"><span data-stu-id="a9709-189">The chart can be configured to show different metrics over various time windows.</span></span>

1. <span data-ttu-id="a9709-190">Seleccione un grupo elástico con el que trabajar.</span><span class="sxs-lookup"><span data-stu-id="a9709-190">Select an elastic pool to work with.</span></span>
2. <span data-ttu-id="a9709-191">En **Supervisión de grupo elástico** hay un gráfico con la etiqueta **Uso de recursos**.</span><span class="sxs-lookup"><span data-stu-id="a9709-191">Under **Elastic Pool Monitoring** is a chart labeled **Resource utilization**.</span></span> <span data-ttu-id="a9709-192">Haga clic en el gráfico.</span><span class="sxs-lookup"><span data-stu-id="a9709-192">Click the chart.</span></span>

    ![Supervisión de grupo elástico][3]

    <span data-ttu-id="a9709-194">Se abre la hoja **Métrica**, donde se muestra una vista detallada de las métricas especificadas en la ventana de tiempo especificada.</span><span class="sxs-lookup"><span data-stu-id="a9709-194">The **Metric** blade opens, showing a detailed view of the specified metrics over the specified time window.</span></span>   

    ![Cuadro de métricas][9]

### <a name="to-customize-the-chart-display"></a><span data-ttu-id="a9709-196">Personalización de la visualización del gráfico</span><span class="sxs-lookup"><span data-stu-id="a9709-196">To customize the chart display</span></span>

<span data-ttu-id="a9709-197">Puede editar el gráfico y la hoja de métricas para mostrar otras métricas, como el porcentaje de CPU, el porcentaje de E/S de datos y el porcentaje de E/S de registro usados.</span><span class="sxs-lookup"><span data-stu-id="a9709-197">You can edit the chart and the metric blade to display other metrics such as CPU percentage, data IO percentage, and log IO percentage used.</span></span>

1. <span data-ttu-id="a9709-198">En la hoja de métricas, haga clic en **Editar**.</span><span class="sxs-lookup"><span data-stu-id="a9709-198">On the metric blade, click **Edit**.</span></span>

    ![Haga clic en Editar.][6]

2. <span data-ttu-id="a9709-200">En la hoja **Editar gráfico**, seleccione un intervalo de tiempo (última hora, hoy o última semana) o haga clic en **personalizado** para seleccionar cualquier intervalo de fechas dentro de las últimas dos semanas.</span><span class="sxs-lookup"><span data-stu-id="a9709-200">In the **Edit Chart** blade, select a time range (past hour, today, or past week), or click **custom** to select any date range in the last two weeks.</span></span> <span data-ttu-id="a9709-201">Seleccione el tipo de gráfico (de barras o líneas) y, después, seleccione los recursos que se supervisarán.</span><span class="sxs-lookup"><span data-stu-id="a9709-201">Select the chart type (bar or line), then select the resources to monitor.</span></span>

   > [!Note]
   > <span data-ttu-id="a9709-202">Solo las métricas con la misma unidad de medida se pueden mostrar en el gráfico al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="a9709-202">Only metrics with the same unit of measure can be displayed in the chart at the same time.</span></span> <span data-ttu-id="a9709-203">Por ejemplo, si selecciona el "porcentaje de eDTU", solo podrá seleccionar otras métricas con porcentaje como unidad de medida.</span><span class="sxs-lookup"><span data-stu-id="a9709-203">For example, if you select "eDTU percentage" then you can only select other metrics with percentage as the unit of measure.</span></span>
   >

    ![Haga clic en Editar.](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. <span data-ttu-id="a9709-205">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a9709-205">Then click **OK**.</span></span>

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a><span data-ttu-id="a9709-206">Administración y supervisión de bases de datos en un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="a9709-206">Manage and monitor databases in an elastic pool</span></span>

<span data-ttu-id="a9709-207">También se pueden supervisar bases de datos individuales en caso de un problema potencial.</span><span class="sxs-lookup"><span data-stu-id="a9709-207">Individual databases can also be monitored for potential trouble.</span></span>

1. <span data-ttu-id="a9709-208">En **Supervisión de base de datos elástica**hay un gráfico que muestra las métricas para cinco bases de datos.</span><span class="sxs-lookup"><span data-stu-id="a9709-208">Under **Elastic Database Monitoring**, there is a chart that displays metrics for five databases.</span></span> <span data-ttu-id="a9709-209">De forma predeterminada, el gráfico muestra las 5 bases de datos principales en el grupo por uso promedio de eDTU durante la última hora.</span><span class="sxs-lookup"><span data-stu-id="a9709-209">By default, the chart displays the top 5 databases in the pool by average eDTU usage in the past hour.</span></span> <span data-ttu-id="a9709-210">Haga clic en el gráfico.</span><span class="sxs-lookup"><span data-stu-id="a9709-210">Click the chart.</span></span>

    ![Supervisión de grupo elástico][4]

2. <span data-ttu-id="a9709-212">Aparece la hoja **Database Resource Utilization** (Uso de recursos de bases de datos).</span><span class="sxs-lookup"><span data-stu-id="a9709-212">The **Database Resource Utilization** blade appears.</span></span> <span data-ttu-id="a9709-213">Esto proporciona una vista detallada del uso de las bases de datos en el grupo.</span><span class="sxs-lookup"><span data-stu-id="a9709-213">This provides a detailed view of the database usage in the pool.</span></span> <span data-ttu-id="a9709-214">Mediante la cuadrícula situada en la parte inferior de la hoja, puede seleccionar las bases de datos del grupo para mostrar su uso en el gráfico (hasta cinco bases de datos).</span><span class="sxs-lookup"><span data-stu-id="a9709-214">Using the grid in the lower part of the blade, you can select any databases in the pool to display its usage in the chart (up to 5 databases).</span></span> <span data-ttu-id="a9709-215">También puede personalizar la ventana de tiempo y métricas que se muestra en el gráfico; para ello, haga clic en **Editar gráfico**.</span><span class="sxs-lookup"><span data-stu-id="a9709-215">You can also customize the metrics and time window displayed in the chart by clicking **Edit chart**.</span></span>

    ![Hoja de utilización de recursos de base de datos][8]

### <a name="to-customize-the-view"></a><span data-ttu-id="a9709-217">Personalización de la vista</span><span class="sxs-lookup"><span data-stu-id="a9709-217">To customize the view</span></span>

1. <span data-ttu-id="a9709-218">En la hoja **Database Resource Utilization** (Uso de recursos de bases de datos), haga clic en **Editar gráfico**.</span><span class="sxs-lookup"><span data-stu-id="a9709-218">In the **Database resource utilization** blade, click **Edit chart**.</span></span>

    ![Clic en Editar gráfico](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. <span data-ttu-id="a9709-220">En la hoja **Editar gráfico**, seleccione un intervalo de tiempo (última hora o 24 horas) o haga clic en **Personalizado** para seleccionar otro día dentro de las últimas dos semanas que se mostrará.</span><span class="sxs-lookup"><span data-stu-id="a9709-220">In the **Edit** chart blade, select a time range (past hour or past 24 hours), or click **custom** to select a different day in the past 2 weeks to display.</span></span>

    ![Clic en Personalizado](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. <span data-ttu-id="a9709-222">Haga clic en la lista desplegable **Compare databases by** (Comparar bases de datos por) para seleccionar otra métrica que se usará al comparar bases de datos.</span><span class="sxs-lookup"><span data-stu-id="a9709-222">Click the **Compare databases by** dropdown to select a different metric to use when comparing databases.</span></span>

    ![Edición del gráfico](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="to-select-databases-to-monitor"></a><span data-ttu-id="a9709-224">Selección de las bases de datos que se supervisarán</span><span class="sxs-lookup"><span data-stu-id="a9709-224">To select databases to monitor</span></span>

<span data-ttu-id="a9709-225">En la lista de bases de datos en la hoja **Database Resource Utilization** (Uso de recursos de bases de datos) puede encontrar bases de datos específicas consultando las páginas de la lista o escribiendo el nombre de una base de datos.</span><span class="sxs-lookup"><span data-stu-id="a9709-225">In the database list in the **Database Resource Utilization** blade, you can find particular databases by looking through the pages in the list or by typing in the name of a database.</span></span> <span data-ttu-id="a9709-226">Utilice la casilla para seleccionar la base de datos.</span><span class="sxs-lookup"><span data-stu-id="a9709-226">Use the checkbox to select the database.</span></span>

![Búsqueda de las bases de datos que se supervisarán][7]


## <a name="add-an-alert-to-an-elastic-pool-resource"></a><span data-ttu-id="a9709-228">Adición de una alerta a un recurso de grupos elásticos</span><span class="sxs-lookup"><span data-stu-id="a9709-228">Add an alert to an elastic pool resource</span></span>

<span data-ttu-id="a9709-229">Puede agregar reglas a un grupo elástico que envía correos electrónicos a personas o cadenas de alerta a puntos de conexión de URL cuando el grupo elástico alcanza un umbral de uso que establezca.</span><span class="sxs-lookup"><span data-stu-id="a9709-229">You can add rules to an elastic pool that send email to people or alert strings to URL endpoints when the elastic pool hits a utilization threshold that you set up.</span></span>

<span data-ttu-id="a9709-230">**Para agregar una alerta para cualquier recurso, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="a9709-230">**To add an alert to any resource:**</span></span>

1. <span data-ttu-id="a9709-231">Haga clic en el gráfico **Uso de recursos** para abrir la hoja **Métrica**, haga clic en **Agregar alerta** y rellene la información de la hoja **Agregar una regla de alerta** (el campo **Recurso** se establece automáticamente en el grupo con el que está trabajando).</span><span class="sxs-lookup"><span data-stu-id="a9709-231">Click the **Resource utilization** chart to open the **Metric** blade, click **Add alert**, and then fill out the information in the **Add an alert rule** blade (**Resource** is automatically set up to be the pool you're working with).</span></span>
2. <span data-ttu-id="a9709-232">Escriba un **nombre** y una **descripción** que identifique la alerta de cara a usted y a los destinatarios.</span><span class="sxs-lookup"><span data-stu-id="a9709-232">Type a **Name** and **Description** that identifies the alert to you and the recipients.</span></span>
3. <span data-ttu-id="a9709-233">Elija en la lista la **Métrica** para la que quiera que se generen alertas.</span><span class="sxs-lookup"><span data-stu-id="a9709-233">Choose a **Metric** that you want to alert from the list.</span></span>

    <span data-ttu-id="a9709-234">El gráfico muestra dinámicamente el uso de recursos relativos a esa métrica a fin de ayudarle a elegir un umbral.</span><span class="sxs-lookup"><span data-stu-id="a9709-234">The chart dynamically shows resource utilization for that metric to help you choose a threshold.</span></span>

4. <span data-ttu-id="a9709-235">Elija una **condición** (mayor que, menor que, etc.) y un **umbral**.</span><span class="sxs-lookup"><span data-stu-id="a9709-235">Choose a **Condition** (greater than, less than, etc.) and a **Threshold**.</span></span>
5. <span data-ttu-id="a9709-236">Elija un **Período** de tiempo que debe cumplir la regla de métrica antes de que se desencadene la alerta.</span><span class="sxs-lookup"><span data-stu-id="a9709-236">Choose a **Period** of time that the metric rule must be satisfied before the alert triggers.</span></span>
6. <span data-ttu-id="a9709-237">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a9709-237">Click **OK**.</span></span>

<span data-ttu-id="a9709-238">Para más información, consulte cómo [crear alertas de SQL Database en Azure Portal](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a9709-238">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="a9709-239">Movimiento de una base de datos a un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="a9709-239">Move a database into an elastic pool</span></span>

<span data-ttu-id="a9709-240">Puede agregar o quitar las bases de datos de un grupo existente.</span><span class="sxs-lookup"><span data-stu-id="a9709-240">You can add or remove databases from an existing pool.</span></span> <span data-ttu-id="a9709-241">Las bases de datos pueden encontrarse en otros grupos.</span><span class="sxs-lookup"><span data-stu-id="a9709-241">The databases can be in other pools.</span></span> <span data-ttu-id="a9709-242">Sin embargo, solo puede agregar bases de datos que estén en el mismo servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="a9709-242">However, you can only add databases that are on the same logical server.</span></span>

1. <span data-ttu-id="a9709-243">En la hoja del grupo, en la opción **Bases de datos elásticas**, haga clic en **Configurar grupo**.</span><span class="sxs-lookup"><span data-stu-id="a9709-243">In the blade for the pool, under **Elastic databases** click **Configure pool**.</span></span>

    ![Haga clic en Configurar grupo.][1]

2. <span data-ttu-id="a9709-245">En la hoja **Configurar grupo**, haga clic en **Agregar al grupo**.</span><span class="sxs-lookup"><span data-stu-id="a9709-245">In the **Configure pool** blade, click **Add to pool**.</span></span>

    ![Haga clic en Agregar para agregar al grupo.](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. <span data-ttu-id="a9709-247">En la hoja **Agregar bases de datos** , seleccione las bases de datos que agregará al grupo.</span><span class="sxs-lookup"><span data-stu-id="a9709-247">In the **Add databases** blade, select the database or databases to add to the pool.</span></span> <span data-ttu-id="a9709-248">Después, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="a9709-248">Then click **Select**.</span></span>

    ![Seleccione las bases de datos que desea agregar.](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    <span data-ttu-id="a9709-250">La hoja **Configurar grupo** muestra ahora la base de datos que ha seleccionado para agregarla, con el estado establecido como **Pendiente**.</span><span class="sxs-lookup"><span data-stu-id="a9709-250">The **Configure pool** blade now lists the database you selected to be added, with its status set to **Pending**.</span></span>

    ![Adiciones de grupo pendientes.](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. <span data-ttu-id="a9709-252">En la hoja **Configurar grupo**, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a9709-252">In the **Configure pool blade**, click **Save**.</span></span>

    ![Haga clic en Guardar](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="a9709-254">Movimiento de una base de datos fuera de un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="a9709-254">Move a database out of an elastic pool</span></span>

1. <span data-ttu-id="a9709-255">En la hoja **Configurar grupo** , seleccione las bases de datos que quitará.</span><span class="sxs-lookup"><span data-stu-id="a9709-255">In the **Configure pool** blade, select the database or databases to remove.</span></span>

    ![lista de bases de datos](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. <span data-ttu-id="a9709-257">Haga clic en **Quitar del grupo**.</span><span class="sxs-lookup"><span data-stu-id="a9709-257">Click **Remove from pool**.</span></span>

    ![lista de bases de datos](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    <span data-ttu-id="a9709-259">La hoja **Configurar grupo** muestra ahora la base de datos que ha seleccionado para quitarla, con el estado establecido como **Pendiente**.</span><span class="sxs-lookup"><span data-stu-id="a9709-259">The **Configure pool** blade now lists the database you selected to be removed with its status set to **Pending**.</span></span>

    ![Adición de base de datos de vista previa y eliminación](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. <span data-ttu-id="a9709-261">En la hoja **Configurar grupo**, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a9709-261">In the **Configure pool blade**, click **Save**.</span></span>

    ![Haga clic en Guardar](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="a9709-263">Cambio de la configuración de rendimiento de un grupo elástico</span><span class="sxs-lookup"><span data-stu-id="a9709-263">Change performance settings of an elastic pool</span></span>

<span data-ttu-id="a9709-264">Cuando supervise el uso de recursos de un grupo elástico, es posible que descubra que son necesarios algunos ajustes.</span><span class="sxs-lookup"><span data-stu-id="a9709-264">As you monitor the resource utilization of an elastic pool, you may discover that some adjustments are needed.</span></span> <span data-ttu-id="a9709-265">Quizás el grupo necesita un cambio en los límites de almacenamiento o rendimiento.</span><span class="sxs-lookup"><span data-stu-id="a9709-265">Maybe the pool needs a change in the performance or storage limits.</span></span> <span data-ttu-id="a9709-266">Posiblemente desee cambiar la configuración de la base de datos en el grupo.</span><span class="sxs-lookup"><span data-stu-id="a9709-266">Possibly you want to change the database settings in the pool.</span></span> <span data-ttu-id="a9709-267">Puede cambiar la configuración del grupo en cualquier momento para obtener el mejor equilibrio entre rendimiento y costo.</span><span class="sxs-lookup"><span data-stu-id="a9709-267">You can change the setup of the pool at any time to get the best balance of performance and cost.</span></span> <span data-ttu-id="a9709-268">Consulte [¿Cuándo se debe utilizar un grupo elástico?](sql-database-elastic-pool.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="a9709-268">See [When should an elastic pool be used?](sql-database-elastic-pool.md) for more information.</span></span>

<span data-ttu-id="a9709-269">Para cambiar los límites de almacenamiento o eDTU por grupo y las eDTU por base de datos:</span><span class="sxs-lookup"><span data-stu-id="a9709-269">To change the eDTUs or storage limits per pool, and eDTUs per database:</span></span>

1. <span data-ttu-id="a9709-270">Abra la hoja **Configurar grupo** .</span><span class="sxs-lookup"><span data-stu-id="a9709-270">Open the **Configure pool** blade.</span></span>

    <span data-ttu-id="a9709-271">En **Configuración de grupo elástico**, utilice el control deslizante para cambiar la configuración del grupo.</span><span class="sxs-lookup"><span data-stu-id="a9709-271">Under **elastic pool settings**, use either slider to change the pool settings.</span></span>

    ![Uso de recursos de grupos elásticos](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. <span data-ttu-id="a9709-273">Cuando se cambia la configuración, la pantalla muestra el coste estimado mensual del cambio.</span><span class="sxs-lookup"><span data-stu-id="a9709-273">When the setting changes, the display shows the estimated monthly cost of the change.</span></span>

    ![Actualización de un grupo elástico y nuevo coste mensual](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="a9709-275">Latencia de las operaciones de grupos elásticos</span><span class="sxs-lookup"><span data-stu-id="a9709-275">Latency of elastic pool operations</span></span>
* <span data-ttu-id="a9709-276">El cambio del número mínimo de eDTU por base de datos o del máximo de eDTU por base de datos suele completarse en cinco minutos o menos.</span><span class="sxs-lookup"><span data-stu-id="a9709-276">Changing the min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="a9709-277">El cambio de eDTU por grupo depende de la cantidad total de espacio que usen todas las bases de datos del grupo.</span><span class="sxs-lookup"><span data-stu-id="a9709-277">Changing the eDTUs per pool depends on the total amount of space used by all databases in the pool.</span></span> <span data-ttu-id="a9709-278">Los cambios tienen un duración media de 90 minutos o menos por cada 100 GB.</span><span class="sxs-lookup"><span data-stu-id="a9709-278">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="a9709-279">Por ejemplo, si el espacio total que usan todas las bases de datos del grupo es de 200 GB, la latencia esperada para cambiar las eDTU de grupo por grupo es de 3 horas o menos.</span><span class="sxs-lookup"><span data-stu-id="a9709-279">For example, if the total space used by all databases in the pool is 200 GB, then the expected latency for changing the pool eDTU per pool is 3 hours or less.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9709-280">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a9709-280">Next steps</span></span>

- <span data-ttu-id="a9709-281">Para entender qué es un grupo elástico, consulte [Grupo elástico de SQL Database](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="a9709-281">To understand what an elastic pool is, see [SQL Database elastic pool](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="a9709-282">Para una guía sobre cómo usar grupos elásticos, consulte las [consideraciones de precio y rendimiento para grupos elásticos](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="a9709-282">For guidance on using elastic pools, see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="a9709-283">Para usar trabajos elásticos para ejecutar scripts de Transact-SQL con cualquier número de bases de datos en el grupo, consulte [Introducción a los trabajos elásticos](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a9709-283">To use elastic jobs to run Transact-SQL scripts against any number of databases in the pool, see [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span>
- <span data-ttu-id="a9709-284">Para consultar en cualquier número de bases de datos del grupo, consulte [Introducción a las consultas elásticas](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a9709-284">To query across any number of databases in the pool, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
- <span data-ttu-id="a9709-285">Para más información sobre las transacciones de cualquier número de bases de datos del grupo, consulte [Transacciones elásticas](sql-database-elastic-transactions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a9709-285">For transactions any number of databases in the pool, see [Elastic transactions](sql-database-elastic-transactions-overview.md).</span></span>


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
