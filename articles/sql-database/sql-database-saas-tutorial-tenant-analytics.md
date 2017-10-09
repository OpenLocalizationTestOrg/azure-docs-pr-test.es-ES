---
title: "consultas de análisis de aaaRun en varias bases de datos SQL de Azure | Documentos de Microsoft"
description: "Extracción de datos de las bases de datos de inquilino en una base de datos de análisis para el análisis sin conexión"
keywords: tutorial de base de datos sql
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: billgib; sstein
ms.openlocfilehash: f2664e4aafd2fecc98d20d229342bca19b0b08c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="extract-data-from-tenant-databases-into-an-analytics-database-for-offline-analysis"></a><span data-ttu-id="b903c-104">Extracción de datos de las bases de datos de inquilino en una base de datos de análisis para el análisis sin conexión</span><span class="sxs-lookup"><span data-stu-id="b903c-104">Extract data from tenant databases into an analytics database for offline analysis</span></span>

<span data-ttu-id="b903c-105">En este tutorial, utilice un consultas de toorun de trabajo elástica en cada base de datos de inquilinos.</span><span class="sxs-lookup"><span data-stu-id="b903c-105">In this tutorial, you use an elastic job toorun queries against each tenant database.</span></span> <span data-ttu-id="b903c-106">trabajo de Hello extrae datos de ventas de vale y los carga en una base de datos de análisis (o el almacenamiento de datos) para el análisis.</span><span class="sxs-lookup"><span data-stu-id="b903c-106">hello job extracts ticket sales data and loads it into an analytics database (or data warehouse) for analysis.</span></span> <span data-ttu-id="b903c-107">Hola base de datos de análisis es, a continuación, consultar información tooextract desde estos datos de operaciones diarios de todos los inquilinos.</span><span class="sxs-lookup"><span data-stu-id="b903c-107">hello analytics database is then queried tooextract insights from this day-to-day operational data of all tenants.</span></span>


<span data-ttu-id="b903c-108">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="b903c-108">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b903c-109">Crear base de datos de análisis de inquilinos de Hola</span><span class="sxs-lookup"><span data-stu-id="b903c-109">Create hello tenant analytics database</span></span>
> * <span data-ttu-id="b903c-110">Crear un trabajo programado tooretrieve de datos y rellenar la base de datos de análisis de Hola</span><span class="sxs-lookup"><span data-stu-id="b903c-110">Create a scheduled job tooretrieve data and populate hello analytics database</span></span>

<span data-ttu-id="b903c-111">toocomplete este tutorial, asegúrese de hello seguro siguiendo los requisitos previos se cumplen:</span><span class="sxs-lookup"><span data-stu-id="b903c-111">toocomplete this tutorial, make sure hello following prerequisites are met:</span></span>

* <span data-ttu-id="b903c-112">se implementa la aplicación de SaaS Wingtip Hello.</span><span class="sxs-lookup"><span data-stu-id="b903c-112">hello Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="b903c-113">vea toodeploy en menos de cinco minutos, [implementar y explorar la aplicación de SaaS Wingtip hello](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="b903c-113">toodeploy in less than five minutes, see [Deploy and explore hello Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="b903c-114">Azure PowerShell está instalado.</span><span class="sxs-lookup"><span data-stu-id="b903c-114">Azure PowerShell is installed.</span></span> <span data-ttu-id="b903c-115">Para más información, consulte [Introducción a Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="b903c-115">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>
* <span data-ttu-id="b903c-116">se instala la versión más reciente de Hola de SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="b903c-116">hello latest version of SQL Server Management Studio (SSMS) is installed.</span></span> [<span data-ttu-id="b903c-117">Descarga e instalación de SSMS</span><span class="sxs-lookup"><span data-stu-id="b903c-117">Download and Install SSMS</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

## <a name="tenant-operational-analytics-pattern"></a><span data-ttu-id="b903c-118">Patrón de análisis operativos de inquilino</span><span class="sxs-lookup"><span data-stu-id="b903c-118">Tenant Operational Analytics pattern</span></span>

<span data-ttu-id="b903c-119">Una de las grandes oportunidades de hello con aplicaciones de SaaS es toouse Hola inquilino completo que se almacena en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="b903c-119">One of hello great opportunities with SaaS applications is toouse hello rich tenant data that is stored in hello cloud.</span></span> <span data-ttu-id="b903c-120">Utilice esta información sobre toogain los datos en la operación de Hola y el uso de la aplicación y los inquilinos.</span><span class="sxs-lookup"><span data-stu-id="b903c-120">Use this data toogain insights into hello operation and usage of your application, and your tenants.</span></span> <span data-ttu-id="b903c-121">Estos datos pueden guiarle característica desarrollo, las mejoras de facilidad de uso y otras mejoras en la aplicación hello y plataforma.</span><span class="sxs-lookup"><span data-stu-id="b903c-121">This data can guide feature development, usability improvements, and other investments in hello app and platform.</span></span> <span data-ttu-id="b903c-122">Es fácil obtener acceso a estos datos cuando se encuentran en una sola base de datos multiinquilino, pero no es tan fácil cuando se distribuyen a escala en miles de bases de datos.</span><span class="sxs-lookup"><span data-stu-id="b903c-122">Accessing this data when it's in a single multi-tenant database is easy, but not so easy when distributed at scale across potentially thousands of databases.</span></span> <span data-ttu-id="b903c-123">Tooaccessing de un enfoque estos datos son toouse elástico trabajos, lo que permite resultados de la consulta devuelve resultados de toobe de ejecución de trabajo capturados en una base de datos de salida y la tabla.</span><span class="sxs-lookup"><span data-stu-id="b903c-123">One approach tooaccessing this data is toouse Elastic jobs, which enable result-returning query results from job execution toobe captured in an output database and table.</span></span>

## <a name="get-hello-wingtip-application-scripts"></a><span data-ttu-id="b903c-124">Obtener scripts de la aplicación hello Wingtip</span><span class="sxs-lookup"><span data-stu-id="b903c-124">Get hello Wingtip application scripts</span></span>

<span data-ttu-id="b903c-125">Hello Wingtip SaaS scripts y código fuente de aplicación están disponibles en hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repositorio de github.</span><span class="sxs-lookup"><span data-stu-id="b903c-125">hello Wingtip SaaS scripts and application source code are available in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="b903c-126">[Pasos de secuencias de comandos de toodownload Hola Wingtip SaaS](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span><span class="sxs-lookup"><span data-stu-id="b903c-126">[Steps toodownload hello Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="deploy-a-database-for-tenant-analytics-results"></a><span data-ttu-id="b903c-127">Implementar una base de datos para resultados de análisis de inquilino</span><span class="sxs-lookup"><span data-stu-id="b903c-127">Deploy a database for tenant analytics results</span></span>

<span data-ttu-id="b903c-128">Este tutorial requiere toohave que un Hola de toocapture implementada de la base de datos resultante de la ejecución del trabajo de scripts que contienen consultas que devuelven resultados.</span><span class="sxs-lookup"><span data-stu-id="b903c-128">This tutorial requires you toohave a database deployed toocapture hello results from job execution of scripts, which contain results-returning queries.</span></span> <span data-ttu-id="b903c-129">Vamos a crear una base de datos denominada tenantanalytics con este fin.</span><span class="sxs-lookup"><span data-stu-id="b903c-129">Let's create a database called tenantanalytics for this purpose.</span></span>

1. <span data-ttu-id="b903c-130">Abra... \\Módulos de aprendizaje\\análisis operativos\\inquilino análisis\\*demostración TenantAnalyticsDB.ps1* en hello *PowerShell ISE* y establecer Hola siguiente valor:</span><span class="sxs-lookup"><span data-stu-id="b903c-130">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in hello *PowerShell ISE* and set hello following value:</span></span>
   * <span data-ttu-id="b903c-131">**$DemoScenario** = **2***Deploy operational analytics database*</span><span class="sxs-lookup"><span data-stu-id="b903c-131">**$DemoScenario** = **2** *Deploy operational analytics database*</span></span>
1. <span data-ttu-id="b903c-132">Presione **F5** script de demostración de hello toorun (esa Hola llamadas *TenantAnalyticsDB.ps1 implementar* secuencia de comandos) que crea la base de datos de análisis de inquilinos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b903c-132">Press **F5** toorun hello demo script (that calls hello *Deploy-TenantAnalyticsDB.ps1* script) which creates hello tenant analytics database.</span></span>

## <a name="create-some-data-for-hello-demo"></a><span data-ttu-id="b903c-133">Crear algunos datos de demostración de hello</span><span class="sxs-lookup"><span data-stu-id="b903c-133">Create some data for hello demo</span></span>

1. <span data-ttu-id="b903c-134">Abra... \\Módulos de aprendizaje\\análisis operativos\\inquilino análisis\\*demostración TenantAnalyticsDB.ps1* en hello *PowerShell ISE* y establecer Hola siguiente valor:</span><span class="sxs-lookup"><span data-stu-id="b903c-134">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in hello *PowerShell ISE* and set hello following value:</span></span>
   * <span data-ttu-id="b903c-135">**$DemoScenario** = **1***Purchase tickets for events at all venues*</span><span class="sxs-lookup"><span data-stu-id="b903c-135">**$DemoScenario** = **1** *Purchase tickets for events at all venues*</span></span>
1. <span data-ttu-id="b903c-136">Presione **F5** toorun Hola script y crear incidencia de historial de compras.</span><span class="sxs-lookup"><span data-stu-id="b903c-136">Press **F5** toorun hello script and create ticket purchasing history.</span></span>


## <a name="create-a-scheduled-job-tooretrieve-tenant-analytics-about-ticket-purchases"></a><span data-ttu-id="b903c-137">Crear un análisis de inquilino de trabajo programado tooretrieve sobre la compra de vales</span><span class="sxs-lookup"><span data-stu-id="b903c-137">Create a scheduled job tooretrieve tenant analytics about ticket purchases</span></span>

<span data-ttu-id="b903c-138">Este script crea una información de compra de vales de trabajo tooretrieve de todos los inquilinos.</span><span class="sxs-lookup"><span data-stu-id="b903c-138">This script creates a job tooretrieve ticket purchase information from all tenants.</span></span> <span data-ttu-id="b903c-139">Después de haber agregado en una sola tabla, puede obtener enriquecidas métricas precisos sobre vale compras patrones a través de los inquilinos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b903c-139">Once aggregated into a single table, you can gain rich insightful metrics about ticket purchasing patterns across hello tenants.</span></span>

1. <span data-ttu-id="b903c-140">Abra SSMS y conéctese toohello catálogo -&lt;usuario&gt;. database.windows.net server</span><span class="sxs-lookup"><span data-stu-id="b903c-140">Open SSMS and connect toohello catalog-&lt;user&gt;.database.windows.net server</span></span>
1. <span data-ttu-id="b903c-141">Abra ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*.</span><span class="sxs-lookup"><span data-stu-id="b903c-141">Open ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="b903c-142">Modificar &lt;usuario&gt;, usar el nombre de usuario hello usa al implementar la aplicación de SaaS Wingtip hello en parte superior de Hola de script de Hola, **sp\_agregar\_destino\_grupo\_miembro** y **sp\_agregar\_paso de trabajo**</span><span class="sxs-lookup"><span data-stu-id="b903c-142">Modify &lt;User&gt;, use hello user name used when you deployed hello Wingtip SaaS app at hello top of hello script, **sp\_add\_target\_group\_member** and **sp\_add\_jobstep**</span></span>
1. <span data-ttu-id="b903c-143">Haga clic en, seleccione **conexión**y conecte toohello catálogo -&lt;usuario&gt;. database.windows.net server, si aún no está conectado</span><span class="sxs-lookup"><span data-stu-id="b903c-143">Right click, select **Connection**, and connect toohello catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="b903c-144">Asegúrese de que está conectado toohello **jobaccount** base de datos del sistema y presione **F5** para ejecutar el script de Hola</span><span class="sxs-lookup"><span data-stu-id="b903c-144">Ensure you are connected toohello **jobaccount** database and press **F5** to run hello script</span></span>

* <span data-ttu-id="b903c-145">**SP\_agregar\_destino\_grupo** crea el nombre del grupo de destino de hello *TenantGroup*, ahora tenemos tooadd miembros de destino.</span><span class="sxs-lookup"><span data-stu-id="b903c-145">**sp\_add\_target\_group** creates hello target group name *TenantGroup*, now we need tooadd target members.</span></span>
* <span data-ttu-id="b903c-146">**SP\_agregar\_destino\_grupo\_miembro** agrega un *server* tipo de miembro que considere todas las bases de datos dentro de ese servidor (tenga en cuenta esto es hello customer1 - destino &lt;Usuario&gt; servidor que contiene las bases de datos del inquilino de Hola) en tiempo de trabajo de ejecución debe incluirse en el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b903c-146">**sp\_add\_target\_group\_member** adds a *server* target member type, which deems all databases within that server (note this is hello customer1-&lt;User&gt; server containing hello tenant databases) at time of job execution should be included in hello job.</span></span>
* <span data-ttu-id="b903c-147">**sp\_add\_job** crea un trabajo programado semanal denominado "Ticket Purchases from all Tenants".</span><span class="sxs-lookup"><span data-stu-id="b903c-147">**sp\_add\_job** creates a new weekly scheduled job called “Ticket Purchases from all Tenants”</span></span>
* <span data-ttu-id="b903c-148">**SP\_agregar\_jobstep** crea toda la información de hello vale compra de paso de trabajo de Hola que contiene tooretrieve de texto de comando de T-SQL de todos los inquilinos y Hola copia devolver el conjunto de resultados en una tabla denominada  *AllTicketsPurchasesfromAllTenants*</span><span class="sxs-lookup"><span data-stu-id="b903c-148">**sp\_add\_jobstep** creates hello job step containing T-SQL command text tooretrieve all hello ticket purchase information from all tenants and copy hello returning result set into a table called *AllTicketsPurchasesfromAllTenants*</span></span>
* <span data-ttu-id="b903c-149">Hola restantes en el script de Hola muestran existencia Hola de objetos de Hola y supervisar la ejecución de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b903c-149">hello remaining views in hello script display hello existence of hello objects and monitor job execution.</span></span> <span data-ttu-id="b903c-150">Revise el valor de estado de Hola de hello **ciclo de vida** estado de la columna toomonitor Hola.</span><span class="sxs-lookup"><span data-stu-id="b903c-150">Review hello status value from hello **lifecycle** column toomonitor hello status.</span></span> <span data-ttu-id="b903c-151">Una vez, se realizó correctamente, trabajo de hello ha finalizado correctamente en todas las bases de datos de inquilino y hello dos bases de datos adicionales que contengan Hola hacen referencia a tabla.</span><span class="sxs-lookup"><span data-stu-id="b903c-151">Once, Succeeded, hello job has successfully finished on all tenant databases and hello two additional databases containing hello reference table.</span></span>

<span data-ttu-id="b903c-152">Script de Hola se ejecute correctamente debe dar lugar a resultados similares:</span><span class="sxs-lookup"><span data-stu-id="b903c-152">Successfully running hello script should result in similar results:</span></span>

![results](media/sql-database-saas-tutorial-tenant-analytics/ticket-purchases-job.png)

## <a name="create-a-job-tooretrieve-a-summary-count-of-ticket-purchases-from-all-tenants"></a><span data-ttu-id="b903c-154">Crear un tooretrieve de trabajo un recuento de resumen del vale de compra a todos los inquilinos</span><span class="sxs-lookup"><span data-stu-id="b903c-154">Create a job tooretrieve a summary count of ticket purchases from all tenants</span></span>

<span data-ttu-id="b903c-155">Este script crea una suma de tooretrieve de trabajo de todas las compras de vales de todos los inquilinos.</span><span class="sxs-lookup"><span data-stu-id="b903c-155">This script creates a job tooretrieve sum of all ticket purchases from all tenants.</span></span>

1. <span data-ttu-id="b903c-156">Abra SSMS y conéctese toohello *catálogo -&lt;usuario&gt;. database.windows.net* server</span><span class="sxs-lookup"><span data-stu-id="b903c-156">Open SSMS and connect toohello *catalog-&lt;User&gt;.database.windows.net* server</span></span>
1. <span data-ttu-id="b903c-157">Archivo de hello abrir... \\Módulos de aprendizaje\\aprovisionar y catálogo\\análisis operativos\\inquilino análisis\\*TicketPurchasesfromAllTenants.sql de resultados*</span><span class="sxs-lookup"><span data-stu-id="b903c-157">Open hello file …\\Learning Modules\\Provision and Catalog\\Operational Analytics\\Tenant Analytics\\*Results-TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="b903c-158">Modificar &lt;usuario&gt;, usar el nombre de usuario hello usa al implementar la aplicación de SaaS Wingtip hello en un script de Hola, en hello **sp\_agregar\_jobstep** procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="b903c-158">Modify &lt;User&gt;, use hello user name used when you deployed hello Wingtip SaaS app in hello script, in hello **sp\_add\_jobstep** stored procedure</span></span>
1. <span data-ttu-id="b903c-159">Haga clic en, seleccione **conexión**y conecte toohello catálogo -&lt;usuario&gt;. database.windows.net server, si aún no está conectado</span><span class="sxs-lookup"><span data-stu-id="b903c-159">Right click, select **Connection**, and connect toohello catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="b903c-160">Asegúrese de que está conectado toohello **tenantanalytics** base de datos del sistema y presione **F5** para ejecutar el script de Hola</span><span class="sxs-lookup"><span data-stu-id="b903c-160">Ensure you are connected toohello **tenantanalytics** database and press **F5** to run hello script</span></span>

<span data-ttu-id="b903c-161">Script de Hola se ejecute correctamente debe dar lugar a resultados similares:</span><span class="sxs-lookup"><span data-stu-id="b903c-161">Successfully running hello script should result in similar results:</span></span>

![results](media/sql-database-saas-tutorial-tenant-analytics/total-sales.png)



* <span data-ttu-id="b903c-163">**sp\_add\_job** crea un trabajo programado semanal denominado "ResultsTicketsOrders".</span><span class="sxs-lookup"><span data-stu-id="b903c-163">**sp\_add\_job** creates a new weekly scheduled job called “ResultsTicketsOrders”</span></span>

* <span data-ttu-id="b903c-164">**SP\_agregar\_jobstep** crea toda la información de hello vale compra de paso de trabajo de Hola que contiene tooretrieve de texto de comando de T-SQL de todos los inquilinos y devolver el conjunto de resultados en una tabla denominada CountofTicketOrders de Hola de copia</span><span class="sxs-lookup"><span data-stu-id="b903c-164">**sp\_add\_jobstep** creates hello job step containing T-SQL command text tooretrieve all hello ticket purchase information from all tenants and copy hello returning result set into a table called CountofTicketOrders</span></span>

* <span data-ttu-id="b903c-165">Hola restantes en el script de Hola muestran existencia Hola de objetos de Hola y supervisar la ejecución de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b903c-165">hello remaining views in hello script display hello existence of hello objects and monitor job execution.</span></span> <span data-ttu-id="b903c-166">Revise el valor de estado de Hola de hello **ciclo de vida** estado de la columna toomonitor Hola.</span><span class="sxs-lookup"><span data-stu-id="b903c-166">Review hello status value from hello **lifecycle** column toomonitor hello status.</span></span> <span data-ttu-id="b903c-167">Una vez, se realizó correctamente, trabajo de hello ha finalizado correctamente en todas las bases de datos de inquilino y hello dos bases de datos adicionales que contengan Hola hacen referencia a tabla.</span><span class="sxs-lookup"><span data-stu-id="b903c-167">Once, Succeeded, hello job has successfully finished on all tenant databases and hello two additional databases containing hello reference table.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b903c-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b903c-168">Next steps</span></span>

<span data-ttu-id="b903c-169">En este tutorial, ha aprendido cómo:</span><span class="sxs-lookup"><span data-stu-id="b903c-169">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b903c-170">Implementar una base de datos de análisis de inquilinos</span><span class="sxs-lookup"><span data-stu-id="b903c-170">Deploy a tenant analytics database</span></span>
> * <span data-ttu-id="b903c-171">Crear un trabajo programado tooretrieve los datos analíticos a través de los inquilinos</span><span class="sxs-lookup"><span data-stu-id="b903c-171">Create a scheduled job tooretrieve analytical data across tenants</span></span>

<span data-ttu-id="b903c-172">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="b903c-172">Congratulations!</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b903c-173">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="b903c-173">Additional resources</span></span>

* <span data-ttu-id="b903c-174">Adicionales [tutoriales que parten Hola aplicación Wingtip SaaS](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span><span class="sxs-lookup"><span data-stu-id="b903c-174">Additional [tutorials that build upon hello Wingtip SaaS application](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span></span>
* [<span data-ttu-id="b903c-175">Trabajos elásticos</span><span class="sxs-lookup"><span data-stu-id="b903c-175">Elastic Jobs</span></span>](sql-database-elastic-jobs-overview.md)
