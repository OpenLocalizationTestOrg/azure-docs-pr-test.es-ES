---
title: grupos de aaaManage de bases de datos SQL de Azure | Documentos de Microsoft
description: "Tutorial sobre la creación y administración de un trabajo elástico."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: f858344d-085b-4022-935e-1b5fa20adbac
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: a73c4fb24c332fae0e917c18272724cccd56f29a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-scaled-out-azure-sql-databases-using-elastic-jobs-preview"></a><span data-ttu-id="aae23-103">Creación y administración de Bases de datos SQL de Azure escaladas horizontalmente con trabajos elásticos (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="aae23-103">Create and manage scaled out Azure SQL Databases using elastic jobs (preview)</span></span>


<span data-ttu-id="aae23-104">**trabajos de base de datos elástica** simplifican la administración de grupos de bases de datos al ejecutar operaciones administrativas, como cambios de esquemas, administración de credenciales, actualizaciones de datos de referencias, recopilación de datos de rendimiento o recopilación de telemetría del inquilino (cliente).</span><span class="sxs-lookup"><span data-stu-id="aae23-104">**Elastic Database jobs** simplify management of groups of databases by executing administrative operations such as schema changes, credentials management, reference data updates, performance data collection or tenant (customer) telemetry collection.</span></span> <span data-ttu-id="aae23-105">Trabajos elásticos de base de datos está actualmente disponible a través de hello portal de Azure y cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aae23-105">Elastic Database jobs is currently available through hello Azure portal and PowerShell cmdlets.</span></span> <span data-ttu-id="aae23-106">Sin embargo, Hola funcionalidad reducida de superficies de portal de Azure limitadas tooexecution en todas las bases de datos en un [grupo elástico (versión preliminar)](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="aae23-106">However, hello Azure portal surfaces reduced functionality limited tooexecution across all databases in an [elastic pool (preview)](sql-database-elastic-pool.md).</span></span> <span data-ttu-id="aae23-107">establecen características adicionales de tooaccess y ejecución de secuencias de comandos en un grupo de bases de datos como un conjunto definido de forma personalizada o una partición (creado con [biblioteca de cliente de base de datos elástica](sql-database-elastic-scale-introduction.md)), consulte [crear y administrar trabajos usando PowerShell](sql-database-elastic-jobs-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="aae23-107">tooaccess additional features and execution of scripts across a group of databases including a custom-defined collection or a shard set (created using [Elastic Database client library](sql-database-elastic-scale-introduction.md)), see [Creating and managing jobs using PowerShell](sql-database-elastic-jobs-powershell.md).</span></span> <span data-ttu-id="aae23-108">Para obtener más información, vea [Información general sobre Trabajos de base de datos elástica](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aae23-108">For more information about jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="aae23-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="aae23-109">Prerequisites</span></span>
* <span data-ttu-id="aae23-110">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="aae23-110">An Azure subscription.</span></span> <span data-ttu-id="aae23-111">Para obtener una versión de evaluación gratuita, consulte [Versión de evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="aae23-111">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="aae23-112">Un grupo elástico.</span><span class="sxs-lookup"><span data-stu-id="aae23-112">An elastic pool.</span></span> <span data-ttu-id="aae23-113">Consulte [Acerca de los grupos elásticos](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="aae23-113">See [About elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="aae23-114">Instalación de componentes del servicio de trabajo de bases de datos elásticas.</span><span class="sxs-lookup"><span data-stu-id="aae23-114">Installation of elastic database job service components.</span></span> <span data-ttu-id="aae23-115">Vea [instalar el servicio de trabajo de base de datos elástica hello](sql-database-elastic-jobs-service-installation.md).</span><span class="sxs-lookup"><span data-stu-id="aae23-115">See [Installing hello elastic database job service](sql-database-elastic-jobs-service-installation.md).</span></span>

## <a name="creating-jobs"></a><span data-ttu-id="aae23-116">Creación de trabajos</span><span class="sxs-lookup"><span data-stu-id="aae23-116">Creating jobs</span></span>
1. <span data-ttu-id="aae23-117">Con hello [portal de Azure](https://portal.azure.com), en un grupo de trabajo elástico de base de datos existente, haga clic en **crear trabajo**.</span><span class="sxs-lookup"><span data-stu-id="aae23-117">Using hello [Azure portal](https://portal.azure.com), from an existing elastic database job pool, click **Create job**.</span></span>
2. <span data-ttu-id="aae23-118">Escriba en nombre de usuario de Hola y la contraseña de administrador de base de datos de hello (creado durante la instalación de trabajos) para la base de datos de control de trabajos de hello (almacenamiento de los metadatos para los trabajos).</span><span class="sxs-lookup"><span data-stu-id="aae23-118">Type in hello username and password of hello database administrator (created at installation of Jobs) for hello jobs control database (metadata storage for jobs).</span></span>
   
    ![Trabajo de Hola de nombre, escriba o pegue en el código y haga clic en ejecutar][1]
3. <span data-ttu-id="aae23-120">Hola **crear trabajo** hoja, escriba un nombre para el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="aae23-120">In hello **Create Job** blade, type a name for hello job.</span></span>
4. <span data-ttu-id="aae23-121">Escriba Hola usuario nombre y la contraseña tooconnect toohello destino bases de datos con permisos suficientes para toosucceed de ejecución de secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="aae23-121">Type hello user name and password tooconnect toohello target databases with sufficient permissions for script execution toosucceed.</span></span>
5. <span data-ttu-id="aae23-122">Pegue o escriba en el script de Hola T-SQL.</span><span class="sxs-lookup"><span data-stu-id="aae23-122">Paste or type in hello T-SQL script.</span></span>
6. <span data-ttu-id="aae23-123">Haga clic en **Guardar** y, a continuación, en **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="aae23-123">Click **Save** and then click **Run**.</span></span>
   
    ![Creación y ejecución de trabajos][5]

## <a name="run-idempotent-jobs"></a><span data-ttu-id="aae23-125">Ejecución de trabajos idempotentes</span><span class="sxs-lookup"><span data-stu-id="aae23-125">Run idempotent jobs</span></span>
<span data-ttu-id="aae23-126">Cuando se ejecuta una secuencia de comandos en un conjunto de bases de datos, debe asegurarse de que el script de Hola es idempotente.</span><span class="sxs-lookup"><span data-stu-id="aae23-126">When you run a script against a set of databases, you must be sure that hello script is idempotent.</span></span> <span data-ttu-id="aae23-127">Es decir, Hola script debe ser capaz de toorun varias veces, incluso si no ha superado antes en un estado incompleto.</span><span class="sxs-lookup"><span data-stu-id="aae23-127">That is, hello script must be able toorun multiple times, even if it has failed before in an incomplete state.</span></span> <span data-ttu-id="aae23-128">Por ejemplo, cuando se produce un error en una secuencia de comandos, el trabajo de Hola se reintentará de forma automática hasta que lo consiga (dentro de los límites, como Reintentar Hola lógica finalmente dejarán de hello Reintentar).</span><span class="sxs-lookup"><span data-stu-id="aae23-128">For example, when a script fails, hello job will be automatically retried until it succeeds (within limits, as hello retry logic will eventually cease hello retrying).</span></span> <span data-ttu-id="aae23-129">Hola forma toodo toouse Hola se trata una cláusula "IF EXISTS" y eliminar cualquier instancia se encuentra antes de crear un nuevo objeto.</span><span class="sxs-lookup"><span data-stu-id="aae23-129">hello way toodo this is toouse hello an "IF EXISTS" clause and delete any found instance before creating a new object.</span></span> <span data-ttu-id="aae23-130">A continuación se muestra un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="aae23-130">An example is shown here:</span></span>

    IF EXISTS (SELECT name FROM sys.indexes
            WHERE name = N'IX_ProductVendor_VendorID')
    DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;
    GO
    CREATE INDEX IX_ProductVendor_VendorID
    ON Purchasing.ProductVendor (VendorID);

<span data-ttu-id="aae23-131">De manera alternativa, puede usar una cláusula "IF NOT EXISTS" antes de crear una nueva instancia:</span><span class="sxs-lookup"><span data-stu-id="aae23-131">Alternatively, use an "IF NOT EXISTS" clause before creating a new instance:</span></span>

    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
     CREATE TABLE TestTable(
      TestTableId INT PRIMARY KEY IDENTITY,
      InsertionTime DATETIME2
     );
    END
    GO

    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO

<span data-ttu-id="aae23-132">Esta secuencia de comandos, a continuación, actualiza la tabla Hola creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="aae23-132">This script then updates hello table created previously.</span></span>

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN

    ALTER TABLE TestTable

    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO


## <a name="checking-job-status"></a><span data-ttu-id="aae23-133">Comprobación del estado del trabajo</span><span class="sxs-lookup"><span data-stu-id="aae23-133">Checking job status</span></span>
<span data-ttu-id="aae23-134">Tras iniciar un trabajo, puede comprobar su progreso.</span><span class="sxs-lookup"><span data-stu-id="aae23-134">After a job has begun, you can check on its progress.</span></span>

1. <span data-ttu-id="aae23-135">En la página de grupo elástico de hello, haga clic en **administrar trabajos**.</span><span class="sxs-lookup"><span data-stu-id="aae23-135">From hello elastic pool page, click **Manage jobs**.</span></span>
   
    ![Haga clic en "Administrar trabajos".][2]
2. <span data-ttu-id="aae23-137">Haga clic en hello nombre (a) de un trabajo.</span><span class="sxs-lookup"><span data-stu-id="aae23-137">Click on hello name (a) of a job.</span></span> <span data-ttu-id="aae23-138">Hola **estado** puede ser "Completed" o "Error".</span><span class="sxs-lookup"><span data-stu-id="aae23-138">hello **STATUS** can be "Completed" or "Failed."</span></span> <span data-ttu-id="aae23-139">Detalles del trabajo de Hello aparecen (b) con su fecha y hora de creación y en ejecución.</span><span class="sxs-lookup"><span data-stu-id="aae23-139">hello job's details appear (b) with its date and time of creation and running.</span></span> <span data-ttu-id="aae23-140">lista de Hello (c) por debajo de Hola que muestra el progreso de Hola de script de Hola en cada base de datos en el grupo de hello, que se facilite su información de fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="aae23-140">hello list (c) below hello that shows hello progress of hello script against each database in hello pool, giving its date and time details.</span></span>
   
    ![Comprobación de un trabajo finalizado][3]

## <a name="checking-failed-jobs"></a><span data-ttu-id="aae23-142">Comprobación de trabajos con errores</span><span class="sxs-lookup"><span data-stu-id="aae23-142">Checking failed jobs</span></span>
<span data-ttu-id="aae23-143">Si se produce un error en un trabajo, puede encontrar un registro de su ejecución.</span><span class="sxs-lookup"><span data-stu-id="aae23-143">If a job fails, a log of its execution can found.</span></span> <span data-ttu-id="aae23-144">Haga clic en Hola Hola error trabajo toosee sus detalles.</span><span class="sxs-lookup"><span data-stu-id="aae23-144">Click hello name of hello failed job toosee its details.</span></span>

![Comprobación de un trabajo con error][4]

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-create-and-manage/screen-1.png
[2]: ./media/sql-database-elastic-jobs-create-and-manage/click-manage-jobs.png
[3]: ./media/sql-database-elastic-jobs-create-and-manage/running-jobs.png
[4]: ./media/sql-database-elastic-jobs-create-and-manage/failed.png
[5]: ./media/sql-database-elastic-jobs-create-and-manage/screen-2.png


