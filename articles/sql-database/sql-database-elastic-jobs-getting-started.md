---
title: "aaaGetting a trabajar con trabajos de base de datos elástica | Documentos de Microsoft"
description: "¿Cómo toouse trabajos de base de datos elástica"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 2540de0e-2235-4cdd-9b6a-b841adba00e5
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: bc5894d2df4235738ab961db4f69c11cdf786cc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-elastic-database-jobs"></a><span data-ttu-id="f22de-103">Introducción a Trabajos de base de datos elástica</span><span class="sxs-lookup"><span data-stu-id="f22de-103">Getting started with Elastic Database jobs</span></span>
<span data-ttu-id="f22de-104">Trabajos de base de datos elásticos (versión preliminar) para la base de datos de SQL Azure le permite tooreliability ejecutar scripts de T-SQL que abarcan varias bases de datos al reintentar automáticamente y que garantice la proporciona la finalización eventual.</span><span class="sxs-lookup"><span data-stu-id="f22de-104">Elastic Database jobs (preview) for Azure SQL Database allows you tooreliability execute T-SQL scripts that span multiple databases while automatically retrying and providing eventual completion guarantees.</span></span> <span data-ttu-id="f22de-105">Para obtener más información acerca de la característica de trabajo de base de datos elástica hello, vea hello [página de información general sobre la característica](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f22de-105">For more information about hello Elastic Database job feature, please see hello [feature overview page](sql-database-elastic-jobs-overview.md).</span></span>

<span data-ttu-id="f22de-106">Ejemplo de Hola se encuentra en este tema amplían [Introducción a las herramientas de base de datos elástica](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f22de-106">This topic extends hello sample found in [Getting started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span> <span data-ttu-id="f22de-107">Cuando haya completado, tendrá que: Obtenga información acerca de cómo toocreate y administrar los trabajos que administración un grupo de bases de datos relacionadas.</span><span class="sxs-lookup"><span data-stu-id="f22de-107">When completed, you will: learn how toocreate and manage jobs that manage a group of related databases.</span></span> <span data-ttu-id="f22de-108">No es necesario toouse Hola escala elástica herramientas en orden tootake máximo Hola ventajas de trabajos elásticos.</span><span class="sxs-lookup"><span data-stu-id="f22de-108">It is not required toouse hello Elastic Scale tools in order tootake advantage of hello benefits of Elastic jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f22de-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f22de-109">Prerequisites</span></span>
<span data-ttu-id="f22de-110">Descargue y ejecute hello [cómo empezar a usar el ejemplo de herramientas de la base de datos elástica](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f22de-110">Download and run hello [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a><span data-ttu-id="f22de-111">Crear un mapa de particiones administrador mediante la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="f22de-111">Create a shard map manager using hello sample app</span></span>
<span data-ttu-id="f22de-112">A continuación creará un mapa de particiones administrador junto con varias particiones, seguido por la inserción de datos en particiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="f22de-112">Here you will create a shard map manager along with several shards, followed by insertion of data into hello shards.</span></span> <span data-ttu-id="f22de-113">Si ya tiene particiones configurado con datos particionados en ellos, puede omitir Hola pasos y mover toohello próxima sección.</span><span class="sxs-lookup"><span data-stu-id="f22de-113">If you already have shards set up with sharded data in them, you can skip hello following steps and move toohello next section.</span></span>

1. <span data-ttu-id="f22de-114">Compile y ejecute hello **Introducción a las herramientas de base de datos elástica** aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="f22de-114">Build and run hello **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="f22de-115">Siga los pasos de hello hasta el paso 7 de la sección de hello [descargue y ejecute la aplicación de ejemplo de Hola](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="f22de-115">Follow hello steps until step 7 in hello section [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="f22de-116">Al final de saludo del paso 7, verá Hola después de símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="f22de-116">At hello end of Step 7, you will see hello following command prompt:</span></span>

   ![símbolo del sistema](./media/sql-database-elastic-query-getting-started/cmd-prompt.png)

2. <span data-ttu-id="f22de-118">En la ventana de comandos de hello, escriba "1" y presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="f22de-118">In hello command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="f22de-119">Esto crea el Administrador de mapa de particiones de Hola y agrega dos particiones toohello servidor.</span><span class="sxs-lookup"><span data-stu-id="f22de-119">This creates hello shard map manager, and adds two shards toohello server.</span></span> <span data-ttu-id="f22de-120">A continuación, escriba "3" y pulse **Entrar**; repita esta acción cuatro veces.</span><span class="sxs-lookup"><span data-stu-id="f22de-120">Then type "3" and press **Enter**; repeat this action four times.</span></span> <span data-ttu-id="f22de-121">De esta forma, se insertan las filas de datos de ejemplo en sus particiones.</span><span class="sxs-lookup"><span data-stu-id="f22de-121">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="f22de-122">Hola [Portal de Azure](https://portal.azure.com) debe mostrar tres nuevas bases de datos:</span><span class="sxs-lookup"><span data-stu-id="f22de-122">hello [Azure Portal](https://portal.azure.com) should show three new databases:</span></span>

   ![Confirmación de Visual Studio](./media/sql-database-elastic-query-getting-started/portal.png)

   <span data-ttu-id="f22de-124">En este momento, se creará una colección de base de datos personalizada que refleja todas las bases de datos de hello en mapa de particiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="f22de-124">At this point, we will create a custom database collection that reflects all hello databases in hello shard map.</span></span> <span data-ttu-id="f22de-125">Esto nos permitirá toocreate y ejecutar un trabajo que agregar una nueva tabla en particiones.</span><span class="sxs-lookup"><span data-stu-id="f22de-125">This will allow us toocreate and execute a job that add a new table across shards.</span></span>

<span data-ttu-id="f22de-126">Aquí, se haría normalmente crea un destino de mapa de particiones, mediante hello **AzureSqlJobTarget New** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f22de-126">Here we would usually create a shard map target, using hello **New-AzureSqlJobTarget** cmdlet.</span></span> <span data-ttu-id="f22de-127">base de datos de administrador de asignación de Hello particiones debe establecerse como un destino de la base de datos y, a continuación, se especifica el mapa de particiones específicas de hello como destino.</span><span class="sxs-lookup"><span data-stu-id="f22de-127">hello shard map manager database must be set as a database target and then hello specific shard map is specified as a target.</span></span> <span data-ttu-id="f22de-128">En su lugar, estamos continuo tooenumerate todas las bases de datos de hello en el servidor de Hola y agregar hello las bases de datos toohello nueva colección personalizada con la excepción de Hola de base de datos maestra.</span><span class="sxs-lookup"><span data-stu-id="f22de-128">Instead, we are going tooenumerate all hello databases in hello server and add hello databases toohello new custom collection with hello exception of master database.</span></span>

## <a name="creates-a-custom-collection-and-add-all-databases-in-hello-server-toohello-custom-collection-target-with-hello-exception-of-master"></a><span data-ttu-id="f22de-129">Crea una colección personalizada y agregue todas las bases de datos de destino de colección personalizada de hello server toohello con la excepción de Hola de master.</span><span class="sxs-lookup"><span data-stu-id="f22de-129">Creates a custom collection and add all databases in hello server toohello custom collection target with hello exception of master.</span></span>
   ```
    $customCollectionName = "dbs_in_server"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $ResourceGroupName = "ddove_samples"
    $ServerName = "samples"
    $dbsinserver = Get-AzureRMSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName
    $dbsinserver | %{
    $currentdb = $_.DatabaseName
    $ErrorActionPreference = "Stop"
    Write-Output ""

    Try
    {
       New-AzureSqlJobTarget -ServerName $ServerName -DatabaseName $currentdb | Write-Output
    }
    Catch
    {
        $ErrorMessage = $_.Exception.Message
        $ErrorCategory = $_.CategoryInfo.Reason

        if ($ErrorCategory -eq 'UniqueConstraintViolatedException')
        {
             Write-Host $currentdb "is already a database target."
        }

        else
        {
            throw $_
        }

    }

    Try
    {
        if ($currentdb -eq "master")
        {
            Write-Host $currentdb "will not be added custom collection target" $CustomCollectionName "."
        }

        else
        {
            Add-AzureSqlJobChildTarget -CustomCollectionName $CustomCollectionName -ServerName $ServerName -DatabaseName $currentdb
            Write-Host $currentdb "was added to" $CustomCollectionName "."
        }

    }
    Catch
    {
        $ErrorMessage = $_.Exception.Message
        $ErrorCategory = $_.CategoryInfo.Reason

        if ($ErrorCategory -eq 'UniqueConstraintViolatedException')
        {
             Write-Host $currentdb "is already in hello custom collection target" $CustomCollectionName"."
        }

        else
        {
            throw $_
        }
    }
    $ErrorActionPreference = "Continue"
   }
   ```
## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="f22de-130">Crear un script T-SQL para su ejecución transversal en las bases de datos</span><span class="sxs-lookup"><span data-stu-id="f22de-130">Create a T-SQL Script for execution across databases</span></span>
   ```
    $scriptName = "NewTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'Test')
    BEGIN
        CREATE TABLE Test(
            TestId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO Test(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script
   ```

## <a name="create-hello-job-tooexecute-a-script-across-hello-custom-group-of-databases"></a><span data-ttu-id="f22de-131">Crear un script de Hola tooexecute de trabajo en grupo personalizado de Hola de bases de datos</span><span class="sxs-lookup"><span data-stu-id="f22de-131">Create hello job tooexecute a script across hello custom group of databases</span></span>

   ```
    $jobName = "create on server dbs"
    $scriptName = "NewTable"
    $customCollectionName = "dbs_in_server"
    $credentialName = "ddove66"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="execute-hello-job"></a><span data-ttu-id="f22de-132">Ejecutar trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="f22de-132">Execute hello job</span></span>
<span data-ttu-id="f22de-133">Hola siguiente script de PowerShell puede ser usado tooexecute un trabajo existente:</span><span class="sxs-lookup"><span data-stu-id="f22de-133">hello following PowerShell script can be used tooexecute an existing job:</span></span>

<span data-ttu-id="f22de-134">Hola de actualización después de la variable tooreflect Hola deseado toohave de nombre de trabajo ejecuta:</span><span class="sxs-lookup"><span data-stu-id="f22de-134">Update hello following variable tooreflect hello desired job name toohave executed:</span></span>

   ```
    $jobName = "create on server dbs"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="retrieve-hello-state-of-a-single-job-execution"></a><span data-ttu-id="f22de-135">Recuperar el estado de Hola de ejecución de un trabajo único</span><span class="sxs-lookup"><span data-stu-id="f22de-135">Retrieve hello state of a single job execution</span></span>
<span data-ttu-id="f22de-136">Use Hola mismo **Get AzureSqlJobExecution** cmdlet con hello **IncludeChildren** estado de hello tooview los parámetros de las ejecuciones de trabajo secundarios, es decir Hola estado específico para cada ejecución del trabajo en todas base de datos de destino de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f22de-136">Use hello same **Get-AzureSqlJobExecution** cmdlet with hello **IncludeChildren** parameter tooview hello state of child job executions, namely hello specific state for each job execution against each database targeted by hello job.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions
   ```

## <a name="view-hello-state-across-multiple-job-executions"></a><span data-ttu-id="f22de-137">Vista de estado de Hola a través de varias ejecuciones del trabajo</span><span class="sxs-lookup"><span data-stu-id="f22de-137">View hello state across multiple job executions</span></span>
<span data-ttu-id="f22de-138">Hola **AzureSqlJobExecution Get** cmdlet tiene varios parámetros opcionales que pueden ser utilizado toodisplay múltiples ejecuciones del trabajo, filtradas mediante parámetros de hello proporcionado.</span><span class="sxs-lookup"><span data-stu-id="f22de-138">hello **Get-AzureSqlJobExecution** cmdlet has multiple optional parameters that can be used toodisplay multiple job executions, filtered through hello provided parameters.</span></span> <span data-ttu-id="f22de-139">siguiente Hello muestra algunas de hello formas toouse AzureSqlJobExecution Get:</span><span class="sxs-lookup"><span data-stu-id="f22de-139">hello following demonstrates some of hello possible ways toouse Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="f22de-140">Recuperar todas las ejecuciones de trabajos activos de nivel superior:</span><span class="sxs-lookup"><span data-stu-id="f22de-140">Retrieve all active top level job executions:</span></span>

   ```
    Get-AzureSqlJobExecution
   ```

<span data-ttu-id="f22de-141">Recuperar todas las ejecuciones de trabajos de nivel superior, incluidas las ejecuciones de trabajos inactivos:</span><span class="sxs-lookup"><span data-stu-id="f22de-141">Retrieve all top level job executions, including inactive job executions:</span></span>

   ```
    Get-AzureSqlJobExecution -IncludeInactive
   ```

<span data-ttu-id="f22de-142">Recuperar todas las ejecuciones de trabajos secundarios de un identificador de ejecución de trabajos proporcionado, incluidas las ejecuciones de trabajos inactivos:</span><span class="sxs-lookup"><span data-stu-id="f22de-142">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

   ```
    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren
   ```

<span data-ttu-id="f22de-143">Recuperar todas las ejecuciones de trabajos creadas con una combinación de programación y trabajo, incluidos los trabajos inactivos:</span><span class="sxs-lookup"><span data-stu-id="f22de-143">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive
   ```

<span data-ttu-id="f22de-144">Recuperar todos los trabajos que se destinan a un mapa de particiones especificado, incluidos los trabajos inactivos:</span><span class="sxs-lookup"><span data-stu-id="f22de-144">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

   ```
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="f22de-145">Recuperar todos los trabajos que se destinan a una colección personalizada especificada, incluidos los trabajos inactivos:</span><span class="sxs-lookup"><span data-stu-id="f22de-145">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

   ```
    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="f22de-146">Recuperar la lista de Hola de ejecuciones de la tarea de trabajo dentro de la ejecución de un trabajo específico:</span><span class="sxs-lookup"><span data-stu-id="f22de-146">Retrieve hello list of job task executions within a specific job execution:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions
   ```

<span data-ttu-id="f22de-147">Recuperar los detalles de ejecución de tareas de trabajo:</span><span class="sxs-lookup"><span data-stu-id="f22de-147">Retrieve job task execution details:</span></span>

<span data-ttu-id="f22de-148">Hola siguiente script de PowerShell puede ser utilizados tooview Hola detalles de una ejecución de la tarea de trabajo, que es especialmente útil al depurar errores de ejecución.</span><span class="sxs-lookup"><span data-stu-id="f22de-148">hello following PowerShell script can be used tooview hello details of a job task execution, which is particularly useful when debugging execution failures.</span></span>
   ```
    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution
   ```

## <a name="retrieve-failures-within-job-task-executions"></a><span data-ttu-id="f22de-149">Recuperación de errores dentro de las ejecuciones de tareas de trabajo</span><span class="sxs-lookup"><span data-stu-id="f22de-149">Retrieve failures within job task executions</span></span>
<span data-ttu-id="f22de-150">objeto de Hello JobTaskExecution incluye una propiedad para saludo del ciclo de vida de la tarea hello junto con una propiedad de mensaje.</span><span class="sxs-lookup"><span data-stu-id="f22de-150">hello JobTaskExecution object includes a property for hello Lifecycle of hello task along with a Message property.</span></span> <span data-ttu-id="f22de-151">Si se produce un error en una ejecución de la tarea de trabajo, se establecerá Hola del ciclo de vida propiedad demasiado*error* y propiedad de mensaje Hola se establecerá toohello mensaje de excepción resultante y la pila.</span><span class="sxs-lookup"><span data-stu-id="f22de-151">If a job task execution failed, hello Lifecycle property will be set too*Failed* and hello Message property will be set toohello resulting exception message and its stack.</span></span> <span data-ttu-id="f22de-152">Si un trabajo no es correcta, es importante tooview detalles de Hola de tareas de trabajo que no se realizó correctamente para un trabajo determinado.</span><span class="sxs-lookup"><span data-stu-id="f22de-152">If a job did not succeed, it is important tooview hello details of job tasks that did not succeed for a given job.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions)
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }
   ```

## <a name="waiting-for-a-job-execution-toocomplete"></a><span data-ttu-id="f22de-153">Esperando un toocomplete de ejecución de trabajo</span><span class="sxs-lookup"><span data-stu-id="f22de-153">Waiting for a job execution toocomplete</span></span>
<span data-ttu-id="f22de-154">Hola siguiente script de PowerShell puede ser usado toowait para un toocomplete de tareas de trabajo:</span><span class="sxs-lookup"><span data-stu-id="f22de-154">hello following PowerShell script can be used toowait for a job task toocomplete:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="f22de-155">Crear una directiva de ejecución personalizada</span><span class="sxs-lookup"><span data-stu-id="f22de-155">Create a custom execution policy</span></span>
<span data-ttu-id="f22de-156">Trabajos de base de datos elástica admite la creación de directivas de ejecución personalizadas que se pueden aplicar al iniciar trabajos.</span><span class="sxs-lookup"><span data-stu-id="f22de-156">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="f22de-157">Actualmente, las directivas de ejecución permiten definir:</span><span class="sxs-lookup"><span data-stu-id="f22de-157">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="f22de-158">Nombre: Identificador de directiva de ejecución de Hola.</span><span class="sxs-lookup"><span data-stu-id="f22de-158">Name: Identifier for hello execution policy.</span></span>
* <span data-ttu-id="f22de-159">Tiempo de espera del trabajo: tiempo total antes de que Trabajos de base de datos elástica cancele un trabajo.</span><span class="sxs-lookup"><span data-stu-id="f22de-159">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="f22de-160">Intervalo de reintento inicial: Intervalo toowait antes del primer reintento.</span><span class="sxs-lookup"><span data-stu-id="f22de-160">Initial Retry Interval: Interval toowait before first retry.</span></span>
* <span data-ttu-id="f22de-161">Intervalo de reintento máximo: Límite de toouse de intervalos de reintento.</span><span class="sxs-lookup"><span data-stu-id="f22de-161">Maximum Retry Interval: Cap of retry intervals toouse.</span></span>
* <span data-ttu-id="f22de-162">Coeficiente de retroceso de intervalo de reintento: Coeficiente utiliza el siguiente intervalo de saludo de toocalculate entre los reintentos.</span><span class="sxs-lookup"><span data-stu-id="f22de-162">Retry Interval Backoff Coefficient: Coefficient used toocalculate hello next interval between retries.</span></span>  <span data-ttu-id="f22de-163">Hello se utiliza siguiente fórmula: (intervalo de reintentos inicial) * Math.pow ((coeficiente de retroceso de intervalo), (número de intentos de) - 2).</span><span class="sxs-lookup"><span data-stu-id="f22de-163">hello following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span>
* <span data-ttu-id="f22de-164">Número máximo de intentos: número máximo de Hola de tooperform de intentos de reintento de un trabajo.</span><span class="sxs-lookup"><span data-stu-id="f22de-164">Maximum Attempts: hello maximum number of retry attempts tooperform within a job.</span></span>

<span data-ttu-id="f22de-165">Directiva de ejecución de Hello predeterminada utiliza Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="f22de-165">hello default execution policy uses hello following values:</span></span>

* <span data-ttu-id="f22de-166">Nombre: directiva de ejecución predeterminada</span><span class="sxs-lookup"><span data-stu-id="f22de-166">Name: Default execution policy</span></span>
* <span data-ttu-id="f22de-167">Tiempo de espera del trabajo: 1 semana</span><span class="sxs-lookup"><span data-stu-id="f22de-167">Job Timeout: 1 week</span></span>
* <span data-ttu-id="f22de-168">Intervalo de reintento inicial: 100 milisegundos</span><span class="sxs-lookup"><span data-stu-id="f22de-168">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="f22de-169">Intervalo máximo de reintento: 30 minutos</span><span class="sxs-lookup"><span data-stu-id="f22de-169">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="f22de-170">Coeficiente de intervalo de reintento: 2</span><span class="sxs-lookup"><span data-stu-id="f22de-170">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="f22de-171">Número máximo de intentos: 2.147.483.647</span><span class="sxs-lookup"><span data-stu-id="f22de-171">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="f22de-172">Crear directiva de ejecución de hello deseado:</span><span class="sxs-lookup"><span data-stu-id="f22de-172">Create hello desired execution policy:</span></span>

   ```
    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy
   ```

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="f22de-173">Actualización de una directiva de ejecución personalizada</span><span class="sxs-lookup"><span data-stu-id="f22de-173">Update a custom execution policy</span></span>
<span data-ttu-id="f22de-174">Tooupdate de directiva de ejecución de actualización Hola deseado:</span><span class="sxs-lookup"><span data-stu-id="f22de-174">Update hello desired execution policy tooupdate:</span></span>

   ```
    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy
   ```

## <a name="cancel-a-job"></a><span data-ttu-id="f22de-175">Cancelación de un trabajo</span><span class="sxs-lookup"><span data-stu-id="f22de-175">Cancel a job</span></span>
<span data-ttu-id="f22de-176">Trabajos de base de datos elástica admite solicitudes de cancelación de trabajos.</span><span class="sxs-lookup"><span data-stu-id="f22de-176">Elastic Database Jobs supports jobs cancellation requests.</span></span>  <span data-ttu-id="f22de-177">Si los trabajos de base de datos elástica detecta una solicitud de cancelación de un trabajo que se está ejecutando actualmente, tratará de trabajo de hello toostop.</span><span class="sxs-lookup"><span data-stu-id="f22de-177">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt toostop hello job.</span></span>

<span data-ttu-id="f22de-178">Trabajos de base de datos elástica puede realizar una cancelación de dos formas distintas:</span><span class="sxs-lookup"><span data-stu-id="f22de-178">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="f22de-179">Cancelar ejecutando tareas: si se detecta una cancelación mientras una tarea se está ejecutando actualmente, se intentará una cancelación dentro de hello ejecutando el aspecto de la tarea hello.</span><span class="sxs-lookup"><span data-stu-id="f22de-179">Canceling Currently Executing Tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within hello currently executing aspect of hello task.</span></span>  <span data-ttu-id="f22de-180">Por ejemplo: si hay una consulta de ejecución prolongada que se están llevando a cabo cuando se intenta realizar una cancelación, habrá una consulta de hello toocancel intento.</span><span class="sxs-lookup"><span data-stu-id="f22de-180">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt toocancel hello query.</span></span>
2. <span data-ttu-id="f22de-181">Cancelación de tareas de reintentos: Si se detecta una cancelación por subproceso de control de hello antes de que se inicia una tarea para su ejecución, subproceso de control de hello evitará Iniciar tarea hello y declarar solicitud hello como cancelada.</span><span class="sxs-lookup"><span data-stu-id="f22de-181">Canceling Task Retries: If a cancellation is detected by hello control thread before a task is launched for execution, hello control thread will avoid launching hello task and declare hello request as canceled.</span></span>

<span data-ttu-id="f22de-182">Si se solicita una cancelación de trabajo para un trabajo primario, se respetará la solicitud de cancelación de Hola de trabajo primario de Hola y para todos los trabajos secundarios.</span><span class="sxs-lookup"><span data-stu-id="f22de-182">If a job cancellation is requested for a parent job, hello cancellation request will be honored for hello parent job and for all of its child jobs.</span></span>

<span data-ttu-id="f22de-183">toosubmit una solicitud de cancelación, utilice hello **Stop AzureSqlJobExecution** cmdlet conjunto hello y **JobExecutionId** parámetro.</span><span class="sxs-lookup"><span data-stu-id="f22de-183">toosubmit a cancellation request, use hello **Stop-AzureSqlJobExecution** cmdlet and set hello **JobExecutionId** parameter.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="delete-a-job-by-name-and-hello-jobs-history"></a><span data-ttu-id="f22de-184">Eliminar un trabajo por nombre y el historial del trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="f22de-184">Delete a job by name and hello job's history</span></span>
<span data-ttu-id="f22de-185">Trabajos de base de datos elástica admite la eliminación asincrónica de trabajos.</span><span class="sxs-lookup"><span data-stu-id="f22de-185">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="f22de-186">Un trabajo se puede marcar para su eliminación y sistema de hello eliminará trabajo hello y su historial de trabajo una vez han completado todas las ejecuciones del trabajo para el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f22de-186">A job can be marked for deletion and hello system will delete hello job and all its job history after all job executions have completed for hello job.</span></span> <span data-ttu-id="f22de-187">sistema de Hello no cancelará automáticamente las ejecuciones del trabajo activo.</span><span class="sxs-lookup"><span data-stu-id="f22de-187">hello system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="f22de-188">En su lugar, Stop-AzureSqlJobExecution debe ser invocado toocancel ejecuciones de trabajo activo.</span><span class="sxs-lookup"><span data-stu-id="f22de-188">Instead, Stop-AzureSqlJobExecution must be invoked toocancel active job executions.</span></span>

<span data-ttu-id="f22de-189">eliminación de trabajo tootrigger, use hello **Remove-AzureSqlJob** cmdlet conjunto hello y **JobName** parámetro.</span><span class="sxs-lookup"><span data-stu-id="f22de-189">tootrigger job deletion, use hello **Remove-AzureSqlJob** cmdlet and set hello **JobName** parameter.</span></span>

   ```
    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName
   ```

## <a name="create-a-custom-database-target"></a><span data-ttu-id="f22de-190">Creación de un destino de base de datos personalizada</span><span class="sxs-lookup"><span data-stu-id="f22de-190">Create a custom database target</span></span>
<span data-ttu-id="f22de-191">En Trabajos de base de datos elástica, se pueden definir destinos de base de datos personalizada que sirven para su ejecución directa o para su inclusión en un grupo de base de datos personalizada.</span><span class="sxs-lookup"><span data-stu-id="f22de-191">Custom database targets can be defined in Elastic Database jobs which can be used either for execution directly or for inclusion within a custom database group.</span></span> <span data-ttu-id="f22de-192">Puesto que **grupos elásticos** no son aún directamente compatibles a través de PowerShell APIs de hello, basta con crear un destino de base de datos personalizada y un destino de colección de base de datos personalizada que abarca todas las bases de datos de hello en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f22de-192">Since **elastic pools** are not yet directly supported via hello PowerShell APIs, you simply create a custom database target and custom database collection target which encompasses all hello databases in hello pool.</span></span>

<span data-ttu-id="f22de-193">Establecer Hola siguiendo la información de base de datos de las variables tooreflect Hola deseado:</span><span class="sxs-lookup"><span data-stu-id="f22de-193">Set hello following variables tooreflect hello desired database information:</span></span>

   ```
    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName
   ```

## <a name="create-a-custom-database-collection-target"></a><span data-ttu-id="f22de-194">Creación de un destino de colección de bases de datos personalizada</span><span class="sxs-lookup"><span data-stu-id="f22de-194">Create a custom database collection target</span></span>
<span data-ttu-id="f22de-195">Un destino de recopilación de la base de datos personalizada puede ser definido tooenable ejecución a través de varios destinos de la base de datos definido.</span><span class="sxs-lookup"><span data-stu-id="f22de-195">A custom database collection target can be defined tooenable execution across multiple defined database targets.</span></span> <span data-ttu-id="f22de-196">Después de crea un grupo de base de datos, las bases de datos pueden ser destino de colección personalizada toohello asociado.</span><span class="sxs-lookup"><span data-stu-id="f22de-196">After a database group is created, databases can be associated toohello custom collection target.</span></span>

<span data-ttu-id="f22de-197">Establecer Hola siguiente configuración de destino de colección personalizada deseada de variables tooreflect hello:</span><span class="sxs-lookup"><span data-stu-id="f22de-197">Set hello following variables tooreflect hello desired custom collection target configuration:</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="add-databases-tooa-custom-database-collection-target"></a><span data-ttu-id="f22de-198">Agregar destino de colección de bases de datos tooa base de datos personalizada</span><span class="sxs-lookup"><span data-stu-id="f22de-198">Add databases tooa custom database collection target</span></span>
<span data-ttu-id="f22de-199">Destinos de la base de datos se pueden asociados con la base de datos personalizada colección destinos toocreate un grupo de bases de datos.</span><span class="sxs-lookup"><span data-stu-id="f22de-199">Database targets can be associated with custom database collection targets toocreate a group of databases.</span></span> <span data-ttu-id="f22de-200">Cada vez que se crea un trabajo que tiene un destino de colección de la base de datos personalizada, será grupo toohello asociados de tootarget expandido Hola bases de datos en tiempo de Hola de ejecución.</span><span class="sxs-lookup"><span data-stu-id="f22de-200">Whenever a job is created that targets a custom database collection target, it will be expanded tootarget hello databases associated toohello group at hello time of execution.</span></span>

<span data-ttu-id="f22de-201">Agregar la recopilación personalizado específico tooa Hola deseado de base de datos:</span><span class="sxs-lookup"><span data-stu-id="f22de-201">Add hello desired database tooa specific custom collection:</span></span>

   ```
    $serverName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName
   ```

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="f22de-202">Revise las bases de datos de hello dentro de un destino de colección de la base de datos personalizada</span><span class="sxs-lookup"><span data-stu-id="f22de-202">Review hello databases within a custom database collection target</span></span>
<span data-ttu-id="f22de-203">Hola de uso **AzureSqlJobTarget Get** bases de datos de cmdlet tooretrieve Hola secundarios dentro de un destino de colección de la base de datos personalizada.</span><span class="sxs-lookup"><span data-stu-id="f22de-203">Use hello **Get-AzureSqlJobTarget** cmdlet tooretrieve hello child databases within a custom database collection target.</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets
   ```

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="f22de-204">Crear una secuencia de comandos de un tooexecute de trabajo a través de un destino de recopilación de la base de datos personalizada</span><span class="sxs-lookup"><span data-stu-id="f22de-204">Create a job tooexecute a script across a custom database collection target</span></span>
<span data-ttu-id="f22de-205">Hola de uso **AzureSqlJob New** cmdlet toocreate un trabajo para un grupo de bases de datos definidas por un destino de recopilación de la base de datos personalizada.</span><span class="sxs-lookup"><span data-stu-id="f22de-205">Use hello **New-AzureSqlJob** cmdlet toocreate a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="f22de-206">Trabajos de base de datos elásticos expandirán trabajo hello en varios puestos de secundarios cada base de datos correspondiente de tooa asociados con el destino de colección de base de datos personalizada hello y asegúrese de que se ejecuta el script de Hola en cada base de datos.</span><span class="sxs-lookup"><span data-stu-id="f22de-206">Elastic Database jobs will expand hello job into multiple child jobs each corresponding tooa database associated with hello custom database collection target and ensure that hello script is executed against each database.</span></span> <span data-ttu-id="f22de-207">Una vez más, es importante que los scripts son idempotentes toobe resistente tooretries.</span><span class="sxs-lookup"><span data-stu-id="f22de-207">Again, it is important that scripts are idempotent toobe resilient tooretries.</span></span>

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="data-collection-across-databases"></a><span data-ttu-id="f22de-208">Recopilación de datos de una base de datos a otra</span><span class="sxs-lookup"><span data-stu-id="f22de-208">Data collection across databases</span></span>
<span data-ttu-id="f22de-209">**Trabajos de base de datos elásticos** permite ejecutar una consulta a través de un grupo de bases de datos y envía la tabla Hola resultados tooa base de datos especificada.</span><span class="sxs-lookup"><span data-stu-id="f22de-209">**Elastic Database jobs** supports executing a query across a group of databases and sends hello results tooa specified database’s table.</span></span> <span data-ttu-id="f22de-210">tabla de Hello puede consultarse después Hola hechos toosee Hola resultados de la consulta de cada base de datos.</span><span class="sxs-lookup"><span data-stu-id="f22de-210">hello table can be queried after hello fact toosee hello query’s results from each database.</span></span> <span data-ttu-id="f22de-211">Esto proporciona un mecanismo asincrónico tooexecute una consulta entre varias bases de datos.</span><span class="sxs-lookup"><span data-stu-id="f22de-211">This provides an asynchronous mechanism tooexecute a query across many databases.</span></span> <span data-ttu-id="f22de-212">Casos de error como una de las bases de datos de hello está disponible en este momento se controlan automáticamente a través de reintentos.</span><span class="sxs-lookup"><span data-stu-id="f22de-212">Failure cases such as one of hello databases being temporarily unavailable are handled automatically via retries.</span></span>

<span data-ttu-id="f22de-213">tabla de destino especificado de Hola se crearán automáticamente si aún no existe, esquema coincidente de Hola de hello devuelve el conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="f22de-213">hello specified destination table will be automatically created if it does not yet exist, matching hello schema of hello returned result set.</span></span> <span data-ttu-id="f22de-214">Si la ejecución de un script devuelve varios conjuntos de resultados, los trabajos de base de datos elástica sólo enviará Hola primera tabla de destino de una toohello proporcionado.</span><span class="sxs-lookup"><span data-stu-id="f22de-214">If a script execution returns multiple result sets, Elastic Database jobs will only send hello first one toohello provided destination table.</span></span>

<span data-ttu-id="f22de-215">Hola siguiente script de PowerShell puede ser utilizado tooexecute una secuencia de comandos recopilar sus resultados en una tabla especificada.</span><span class="sxs-lookup"><span data-stu-id="f22de-215">hello following PowerShell script can be used tooexecute a script collecting its results into a specified table.</span></span> <span data-ttu-id="f22de-216">Este script presupone que se creó un script T-SQL que genera un único conjunto de resultados y se creó un destino de la colección de bases de datos personalizada.</span><span class="sxs-lookup"><span data-stu-id="f22de-216">This script assumes that a T-SQL script has been created which outputs a single result set and a custom database collection target has been created.</span></span>

<span data-ttu-id="f22de-217">Establecer Hola sigue la secuencia de comandos de tooreflect Hola deseado, credenciales y de destino de ejecución:</span><span class="sxs-lookup"><span data-stu-id="f22de-217">Set hello following tooreflect hello desired script, credentials, and execution target:</span></span>

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $executionCredentialName = "{Execution Credential Name}"
    $customCollectionName = "{Custom Collection Name}"
    $destinationCredentialName = "{Destination Credential Name}"
    $destinationServerName = "{Destination Server Name}"
    $destinationDatabaseName = "{Destination Database Name}"
    $destinationSchemaName = "{Destination Schema Name}"
    $destinationTableName = "{Destination Table Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="create-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="f22de-218">Creación e inicio de un trabajo en escenarios de recolección de datos</span><span class="sxs-lookup"><span data-stu-id="f22de-218">Create and start a job for data collection scenarios</span></span>
   ```
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $executionCredentialName -ContentName $scriptName -ResultSetDestinationServerName $destinationServerName -ResultSetDestinationDatabaseName $destinationDatabaseName -ResultSetDestinationSchemaName $destinationSchemaName -ResultSetDestinationTableName $destinationTableName -ResultSetDestinationCredentialName $destinationCredentialName -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="create-a-schedule-for-job-execution-using-a-job-trigger"></a><span data-ttu-id="f22de-219">Creación de una programación para la ejecución de trabajos con un desencadenador de trabajo</span><span class="sxs-lookup"><span data-stu-id="f22de-219">Create a schedule for job execution using a job trigger</span></span>
<span data-ttu-id="f22de-220">Hola siguiente script de PowerShell puede ser utilizado toocreate una programación recurrente.</span><span class="sxs-lookup"><span data-stu-id="f22de-220">hello following PowerShell script can be used toocreate a reoccurring schedule.</span></span> <span data-ttu-id="f22de-221">Este script usa un intervalo de un minuto, pero New-AzureSqlJobSchedule también admite los parámetros -DayInterval, -HourInterval, -MonthInterval y -WeekInterval.</span><span class="sxs-lookup"><span data-stu-id="f22de-221">This script uses a one minute interval, but New-AzureSqlJobSchedule also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="f22de-222">Se pueden crear programaciones que se ejecutan una sola vez pasando -OneTime.</span><span class="sxs-lookup"><span data-stu-id="f22de-222">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="f22de-223">Creación de una programación:</span><span class="sxs-lookup"><span data-stu-id="f22de-223">Create a new schedule:</span></span>
   ```
    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule -MinuteInterval $minuteInterval -ScheduleName $scheduleName -StartTime $startTime
    Write-Output $schedule
   ```

### <a name="create-a-job-trigger-toohave-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="f22de-224">Crear un trabajo que se ejecuta según una programación de tiempo de un toohave de desencadenador de trabajo</span><span class="sxs-lookup"><span data-stu-id="f22de-224">Create a job trigger toohave a job executed on a time schedule</span></span>
<span data-ttu-id="f22de-225">Un desencadenador de trabajo puede ser toohave definido una programación de tiempo de trabajo ejecuta correspondiente tooa.</span><span class="sxs-lookup"><span data-stu-id="f22de-225">A job trigger can be defined toohave a job executed according tooa time schedule.</span></span> <span data-ttu-id="f22de-226">Hola siguiente script de PowerShell pueden toocreate usa un desencadenador de trabajo.</span><span class="sxs-lookup"><span data-stu-id="f22de-226">hello following PowerShell script can be used toocreate a job trigger.</span></span>

<span data-ttu-id="f22de-227">Hola conjunto después de las variables toocorrespond toohello había deseado de trabajo y una programación:</span><span class="sxs-lookup"><span data-stu-id="f22de-227">Set hello following variables toocorrespond toohello desired job and schedule:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
    Write-Output $jobTrigger
   ```

### <a name="remove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a><span data-ttu-id="f22de-228">Quitar un trabajo de toostop de asociación programada de ejecución en la programación</span><span class="sxs-lookup"><span data-stu-id="f22de-228">Remove a scheduled association toostop job from executing on schedule</span></span>
<span data-ttu-id="f22de-229">se puede quitar toodiscontinue recurrente de ejecución del trabajo a través de un desencadenador de trabajo, el desencadenador de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f22de-229">toodiscontinue reoccurring job execution through a job trigger, hello job trigger can be removed.</span></span>
<span data-ttu-id="f22de-230">Quitar un toostop de desencadenador de trabajo un trabajo del que se está ejecutando correspondiente programación tooa con hello **Remove-AzureSqlJobTrigger** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f22de-230">Remove a job trigger toostop a job from being executed according tooa schedule using hello **Remove-AzureSqlJobTrigger** cmdlet.</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
   ```

## <a name="import-elastic-database-query-results-tooexcel"></a><span data-ttu-id="f22de-231">Importar tooExcel de resultados de consulta de base de datos elástica</span><span class="sxs-lookup"><span data-stu-id="f22de-231">Import elastic database query results tooExcel</span></span>
 <span data-ttu-id="f22de-232">Puede importar los resultados de Hola desde un consulta tooan del archivo de Excel.</span><span class="sxs-lookup"><span data-stu-id="f22de-232">You can import hello results from of a query tooan Excel file.</span></span>

1. <span data-ttu-id="f22de-233">Inicie Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="f22de-233">Launch Excel 2013.</span></span>
2. <span data-ttu-id="f22de-234">Navegue toohello **datos** la cinta de opciones.</span><span class="sxs-lookup"><span data-stu-id="f22de-234">Navigate toohello **Data** ribbon.</span></span>
3. <span data-ttu-id="f22de-235">Haga clic en **Desde otros orígenes** y luego en **Desde SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="f22de-235">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Importación de Excel desde otros orígenes](./media/sql-database-elastic-query-getting-started/exel-sources.png)

4. <span data-ttu-id="f22de-237">Hola **Asistente para la conexión de datos** escriba credenciales de inicio de sesión y nombre de servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="f22de-237">In hello **Data Connection Wizard** type hello server name and login credentials.</span></span> <span data-ttu-id="f22de-238">A continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="f22de-238">Then click **Next**.</span></span>
5. <span data-ttu-id="f22de-239">En el cuadro de diálogo de hello **base de datos de hello Select que contiene datos de Hola que desee**, seleccione hello **ElasticDBQuery** base de datos.</span><span class="sxs-lookup"><span data-stu-id="f22de-239">In hello dialog box **Select hello database that contains hello data you want**, select hello **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="f22de-240">Seleccione hello **clientes** de tabla en la vista de lista de Hola y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="f22de-240">Select hello **Customers** table in hello list view and click **Next**.</span></span> <span data-ttu-id="f22de-241">Haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="f22de-241">Then click **Finish**.</span></span>
7. <span data-ttu-id="f22de-242">Hola **importar datos** formulario, en **Seleccione cómo desea que tooview estos datos en el libro**, seleccione **tabla** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f22de-242">In hello **Import Data** form, under **Select how you want tooview this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="f22de-243">Todas las filas de Hola **clientes** tabla, almacenado en particiones diferentes rellenar la hoja de Excel de Hola.</span><span class="sxs-lookup"><span data-stu-id="f22de-243">All hello rows from **Customers** table, stored in different shards populate hello Excel sheet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f22de-244">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f22de-244">Next steps</span></span>
<span data-ttu-id="f22de-245">Ahora puede usar las funciones de datos de Excel.</span><span class="sxs-lookup"><span data-stu-id="f22de-245">You can now use Excel’s data functions.</span></span> <span data-ttu-id="f22de-246">Usar cadena de conexión de hello con el nombre del servidor, nombre de base de datos y las credenciales tooconnect su BI y datos integración herramientas toohello elástico consultar base de datos.</span><span class="sxs-lookup"><span data-stu-id="f22de-246">Use hello connection string with your server name, database name and credentials tooconnect your BI and data integration tools toohello elastic query database.</span></span> <span data-ttu-id="f22de-247">Asegúrese de que SQL Server se admite como origen de datos para la herramienta.</span><span class="sxs-lookup"><span data-stu-id="f22de-247">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="f22de-248">Consulte toohello consultar elástico base de datos y tablas externas al igual que cualquier otra base de datos de SQL Server y las tablas de SQL Server que se conectará toowith la herramienta.</span><span class="sxs-lookup"><span data-stu-id="f22de-248">Refer toohello elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect toowith your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="f22de-249">Coste</span><span class="sxs-lookup"><span data-stu-id="f22de-249">Cost</span></span>
<span data-ttu-id="f22de-250">No hay ningún cargo adicional para usar la característica de consulta de base de datos elástica Hola.</span><span class="sxs-lookup"><span data-stu-id="f22de-250">There is no additional charge for using hello Elastic Database query feature.</span></span> <span data-ttu-id="f22de-251">Sin embargo, en este momento, esta característica está disponible únicamente en bases de datos premium como un punto de conexión, pero pueden ser particiones de Hola de cualquier nivel de servicio.</span><span class="sxs-lookup"><span data-stu-id="f22de-251">However, at this time this feature is available only on premium databases as an end point, but hello shards can be of any service tier.</span></span>

<span data-ttu-id="f22de-252">Para obtener información sobre los precios, consulte [Detalles de precios de Base de datos SQL](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="f22de-252">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
