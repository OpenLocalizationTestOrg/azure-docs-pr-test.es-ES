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
# <a name="getting-started-with-elastic-database-jobs"></a>Introducción a Trabajos de base de datos elástica
Trabajos de base de datos elásticos (versión preliminar) para la base de datos de SQL Azure le permite tooreliability ejecutar scripts de T-SQL que abarcan varias bases de datos al reintentar automáticamente y que garantice la proporciona la finalización eventual. Para obtener más información acerca de la característica de trabajo de base de datos elástica hello, vea hello [página de información general sobre la característica](sql-database-elastic-jobs-overview.md).

Ejemplo de Hola se encuentra en este tema amplían [Introducción a las herramientas de base de datos elástica](sql-database-elastic-scale-get-started.md). Cuando haya completado, tendrá que: Obtenga información acerca de cómo toocreate y administrar los trabajos que administración un grupo de bases de datos relacionadas. No es necesario toouse Hola escala elástica herramientas en orden tootake máximo Hola ventajas de trabajos elásticos.

## <a name="prerequisites"></a>Requisitos previos
Descargue y ejecute hello [cómo empezar a usar el ejemplo de herramientas de la base de datos elástica](sql-database-elastic-scale-get-started.md).

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a>Crear un mapa de particiones administrador mediante la aplicación de ejemplo de Hola
A continuación creará un mapa de particiones administrador junto con varias particiones, seguido por la inserción de datos en particiones de Hola. Si ya tiene particiones configurado con datos particionados en ellos, puede omitir Hola pasos y mover toohello próxima sección.

1. Compile y ejecute hello **Introducción a las herramientas de base de datos elástica** aplicación de ejemplo. Siga los pasos de hello hasta el paso 7 de la sección de hello [descargue y ejecute la aplicación de ejemplo de Hola](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app). Al final de saludo del paso 7, verá Hola después de símbolo del sistema:

   ![símbolo del sistema](./media/sql-database-elastic-query-getting-started/cmd-prompt.png)

2. En la ventana de comandos de hello, escriba "1" y presione **ENTRAR**. Esto crea el Administrador de mapa de particiones de Hola y agrega dos particiones toohello servidor. A continuación, escriba "3" y pulse **Entrar**; repita esta acción cuatro veces. De esta forma, se insertan las filas de datos de ejemplo en sus particiones.
3. Hola [Portal de Azure](https://portal.azure.com) debe mostrar tres nuevas bases de datos:

   ![Confirmación de Visual Studio](./media/sql-database-elastic-query-getting-started/portal.png)

   En este momento, se creará una colección de base de datos personalizada que refleja todas las bases de datos de hello en mapa de particiones de Hola. Esto nos permitirá toocreate y ejecutar un trabajo que agregar una nueva tabla en particiones.

Aquí, se haría normalmente crea un destino de mapa de particiones, mediante hello **AzureSqlJobTarget New** cmdlet. base de datos de administrador de asignación de Hello particiones debe establecerse como un destino de la base de datos y, a continuación, se especifica el mapa de particiones específicas de hello como destino. En su lugar, estamos continuo tooenumerate todas las bases de datos de hello en el servidor de Hola y agregar hello las bases de datos toohello nueva colección personalizada con la excepción de Hola de base de datos maestra.

## <a name="creates-a-custom-collection-and-add-all-databases-in-hello-server-toohello-custom-collection-target-with-hello-exception-of-master"></a>Crea una colección personalizada y agregue todas las bases de datos de destino de colección personalizada de hello server toohello con la excepción de Hola de master.
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
## <a name="create-a-t-sql-script-for-execution-across-databases"></a>Crear un script T-SQL para su ejecución transversal en las bases de datos
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

## <a name="create-hello-job-tooexecute-a-script-across-hello-custom-group-of-databases"></a>Crear un script de Hola tooexecute de trabajo en grupo personalizado de Hola de bases de datos

   ```
    $jobName = "create on server dbs"
    $scriptName = "NewTable"
    $customCollectionName = "dbs_in_server"
    $credentialName = "ddove66"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="execute-hello-job"></a>Ejecutar trabajo de Hola
Hola siguiente script de PowerShell puede ser usado tooexecute un trabajo existente:

Hola de actualización después de la variable tooreflect Hola deseado toohave de nombre de trabajo ejecuta:

   ```
    $jobName = "create on server dbs"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="retrieve-hello-state-of-a-single-job-execution"></a>Recuperar el estado de Hola de ejecución de un trabajo único
Use Hola mismo **Get AzureSqlJobExecution** cmdlet con hello **IncludeChildren** estado de hello tooview los parámetros de las ejecuciones de trabajo secundarios, es decir Hola estado específico para cada ejecución del trabajo en todas base de datos de destino de trabajo de Hola.

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions
   ```

## <a name="view-hello-state-across-multiple-job-executions"></a>Vista de estado de Hola a través de varias ejecuciones del trabajo
Hola **AzureSqlJobExecution Get** cmdlet tiene varios parámetros opcionales que pueden ser utilizado toodisplay múltiples ejecuciones del trabajo, filtradas mediante parámetros de hello proporcionado. siguiente Hello muestra algunas de hello formas toouse AzureSqlJobExecution Get:

Recuperar todas las ejecuciones de trabajos activos de nivel superior:

   ```
    Get-AzureSqlJobExecution
   ```

Recuperar todas las ejecuciones de trabajos de nivel superior, incluidas las ejecuciones de trabajos inactivos:

   ```
    Get-AzureSqlJobExecution -IncludeInactive
   ```

Recuperar todas las ejecuciones de trabajos secundarios de un identificador de ejecución de trabajos proporcionado, incluidas las ejecuciones de trabajos inactivos:

   ```
    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren
   ```

Recuperar todas las ejecuciones de trabajos creadas con una combinación de programación y trabajo, incluidos los trabajos inactivos:

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive
   ```

Recuperar todos los trabajos que se destinan a un mapa de particiones especificado, incluidos los trabajos inactivos:

   ```
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

Recuperar todos los trabajos que se destinan a una colección personalizada especificada, incluidos los trabajos inactivos:

   ```
    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

Recuperar la lista de Hola de ejecuciones de la tarea de trabajo dentro de la ejecución de un trabajo específico:

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions
   ```

Recuperar los detalles de ejecución de tareas de trabajo:

Hola siguiente script de PowerShell puede ser utilizados tooview Hola detalles de una ejecución de la tarea de trabajo, que es especialmente útil al depurar errores de ejecución.
   ```
    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution
   ```

## <a name="retrieve-failures-within-job-task-executions"></a>Recuperación de errores dentro de las ejecuciones de tareas de trabajo
objeto de Hello JobTaskExecution incluye una propiedad para saludo del ciclo de vida de la tarea hello junto con una propiedad de mensaje. Si se produce un error en una ejecución de la tarea de trabajo, se establecerá Hola del ciclo de vida propiedad demasiado*error* y propiedad de mensaje Hola se establecerá toohello mensaje de excepción resultante y la pila. Si un trabajo no es correcta, es importante tooview detalles de Hola de tareas de trabajo que no se realizó correctamente para un trabajo determinado.

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

## <a name="waiting-for-a-job-execution-toocomplete"></a>Esperando un toocomplete de ejecución de trabajo
Hola siguiente script de PowerShell puede ser usado toowait para un toocomplete de tareas de trabajo:

   ```
    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="create-a-custom-execution-policy"></a>Crear una directiva de ejecución personalizada
Trabajos de base de datos elástica admite la creación de directivas de ejecución personalizadas que se pueden aplicar al iniciar trabajos.

Actualmente, las directivas de ejecución permiten definir:

* Nombre: Identificador de directiva de ejecución de Hola.
* Tiempo de espera del trabajo: tiempo total antes de que Trabajos de base de datos elástica cancele un trabajo.
* Intervalo de reintento inicial: Intervalo toowait antes del primer reintento.
* Intervalo de reintento máximo: Límite de toouse de intervalos de reintento.
* Coeficiente de retroceso de intervalo de reintento: Coeficiente utiliza el siguiente intervalo de saludo de toocalculate entre los reintentos.  Hello se utiliza siguiente fórmula: (intervalo de reintentos inicial) * Math.pow ((coeficiente de retroceso de intervalo), (número de intentos de) - 2).
* Número máximo de intentos: número máximo de Hola de tooperform de intentos de reintento de un trabajo.

Directiva de ejecución de Hello predeterminada utiliza Hola siguientes valores:

* Nombre: directiva de ejecución predeterminada
* Tiempo de espera del trabajo: 1 semana
* Intervalo de reintento inicial: 100 milisegundos
* Intervalo máximo de reintento: 30 minutos
* Coeficiente de intervalo de reintento: 2
* Número máximo de intentos: 2.147.483.647

Crear directiva de ejecución de hello deseado:

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

### <a name="update-a-custom-execution-policy"></a>Actualización de una directiva de ejecución personalizada
Tooupdate de directiva de ejecución de actualización Hola deseado:

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

## <a name="cancel-a-job"></a>Cancelación de un trabajo
Trabajos de base de datos elástica admite solicitudes de cancelación de trabajos.  Si los trabajos de base de datos elástica detecta una solicitud de cancelación de un trabajo que se está ejecutando actualmente, tratará de trabajo de hello toostop.

Trabajos de base de datos elástica puede realizar una cancelación de dos formas distintas:

1. Cancelar ejecutando tareas: si se detecta una cancelación mientras una tarea se está ejecutando actualmente, se intentará una cancelación dentro de hello ejecutando el aspecto de la tarea hello.  Por ejemplo: si hay una consulta de ejecución prolongada que se están llevando a cabo cuando se intenta realizar una cancelación, habrá una consulta de hello toocancel intento.
2. Cancelación de tareas de reintentos: Si se detecta una cancelación por subproceso de control de hello antes de que se inicia una tarea para su ejecución, subproceso de control de hello evitará Iniciar tarea hello y declarar solicitud hello como cancelada.

Si se solicita una cancelación de trabajo para un trabajo primario, se respetará la solicitud de cancelación de Hola de trabajo primario de Hola y para todos los trabajos secundarios.

toosubmit una solicitud de cancelación, utilice hello **Stop AzureSqlJobExecution** cmdlet conjunto hello y **JobExecutionId** parámetro.

   ```
    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="delete-a-job-by-name-and-hello-jobs-history"></a>Eliminar un trabajo por nombre y el historial del trabajo de Hola
Trabajos de base de datos elástica admite la eliminación asincrónica de trabajos. Un trabajo se puede marcar para su eliminación y sistema de hello eliminará trabajo hello y su historial de trabajo una vez han completado todas las ejecuciones del trabajo para el trabajo de Hola. sistema de Hello no cancelará automáticamente las ejecuciones del trabajo activo.  

En su lugar, Stop-AzureSqlJobExecution debe ser invocado toocancel ejecuciones de trabajo activo.

eliminación de trabajo tootrigger, use hello **Remove-AzureSqlJob** cmdlet conjunto hello y **JobName** parámetro.

   ```
    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName
   ```

## <a name="create-a-custom-database-target"></a>Creación de un destino de base de datos personalizada
En Trabajos de base de datos elástica, se pueden definir destinos de base de datos personalizada que sirven para su ejecución directa o para su inclusión en un grupo de base de datos personalizada. Puesto que **grupos elásticos** no son aún directamente compatibles a través de PowerShell APIs de hello, basta con crear un destino de base de datos personalizada y un destino de colección de base de datos personalizada que abarca todas las bases de datos de hello en el grupo de Hola.

Establecer Hola siguiendo la información de base de datos de las variables tooreflect Hola deseado:

   ```
    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName
   ```

## <a name="create-a-custom-database-collection-target"></a>Creación de un destino de colección de bases de datos personalizada
Un destino de recopilación de la base de datos personalizada puede ser definido tooenable ejecución a través de varios destinos de la base de datos definido. Después de crea un grupo de base de datos, las bases de datos pueden ser destino de colección personalizada toohello asociado.

Establecer Hola siguiente configuración de destino de colección personalizada deseada de variables tooreflect hello:

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="add-databases-tooa-custom-database-collection-target"></a>Agregar destino de colección de bases de datos tooa base de datos personalizada
Destinos de la base de datos se pueden asociados con la base de datos personalizada colección destinos toocreate un grupo de bases de datos. Cada vez que se crea un trabajo que tiene un destino de colección de la base de datos personalizada, será grupo toohello asociados de tootarget expandido Hola bases de datos en tiempo de Hola de ejecución.

Agregar la recopilación personalizado específico tooa Hola deseado de base de datos:

   ```
    $serverName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName
   ```

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a>Revise las bases de datos de hello dentro de un destino de colección de la base de datos personalizada
Hola de uso **AzureSqlJobTarget Get** bases de datos de cmdlet tooretrieve Hola secundarios dentro de un destino de colección de la base de datos personalizada.

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets
   ```

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a>Crear una secuencia de comandos de un tooexecute de trabajo a través de un destino de recopilación de la base de datos personalizada
Hola de uso **AzureSqlJob New** cmdlet toocreate un trabajo para un grupo de bases de datos definidas por un destino de recopilación de la base de datos personalizada. Trabajos de base de datos elásticos expandirán trabajo hello en varios puestos de secundarios cada base de datos correspondiente de tooa asociados con el destino de colección de base de datos personalizada hello y asegúrese de que se ejecuta el script de Hola en cada base de datos. Una vez más, es importante que los scripts son idempotentes toobe resistente tooretries.

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="data-collection-across-databases"></a>Recopilación de datos de una base de datos a otra
**Trabajos de base de datos elásticos** permite ejecutar una consulta a través de un grupo de bases de datos y envía la tabla Hola resultados tooa base de datos especificada. tabla de Hello puede consultarse después Hola hechos toosee Hola resultados de la consulta de cada base de datos. Esto proporciona un mecanismo asincrónico tooexecute una consulta entre varias bases de datos. Casos de error como una de las bases de datos de hello está disponible en este momento se controlan automáticamente a través de reintentos.

tabla de destino especificado de Hola se crearán automáticamente si aún no existe, esquema coincidente de Hola de hello devuelve el conjunto de resultados. Si la ejecución de un script devuelve varios conjuntos de resultados, los trabajos de base de datos elástica sólo enviará Hola primera tabla de destino de una toohello proporcionado.

Hola siguiente script de PowerShell puede ser utilizado tooexecute una secuencia de comandos recopilar sus resultados en una tabla especificada. Este script presupone que se creó un script T-SQL que genera un único conjunto de resultados y se creó un destino de la colección de bases de datos personalizada.

Establecer Hola sigue la secuencia de comandos de tooreflect Hola deseado, credenciales y de destino de ejecución:

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

### <a name="create-and-start-a-job-for-data-collection-scenarios"></a>Creación e inicio de un trabajo en escenarios de recolección de datos
   ```
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $executionCredentialName -ContentName $scriptName -ResultSetDestinationServerName $destinationServerName -ResultSetDestinationDatabaseName $destinationDatabaseName -ResultSetDestinationSchemaName $destinationSchemaName -ResultSetDestinationTableName $destinationTableName -ResultSetDestinationCredentialName $destinationCredentialName -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="create-a-schedule-for-job-execution-using-a-job-trigger"></a>Creación de una programación para la ejecución de trabajos con un desencadenador de trabajo
Hola siguiente script de PowerShell puede ser utilizado toocreate una programación recurrente. Este script usa un intervalo de un minuto, pero New-AzureSqlJobSchedule también admite los parámetros -DayInterval, -HourInterval, -MonthInterval y -WeekInterval. Se pueden crear programaciones que se ejecutan una sola vez pasando -OneTime.

Creación de una programación:
   ```
    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule -MinuteInterval $minuteInterval -ScheduleName $scheduleName -StartTime $startTime
    Write-Output $schedule
   ```

### <a name="create-a-job-trigger-toohave-a-job-executed-on-a-time-schedule"></a>Crear un trabajo que se ejecuta según una programación de tiempo de un toohave de desencadenador de trabajo
Un desencadenador de trabajo puede ser toohave definido una programación de tiempo de trabajo ejecuta correspondiente tooa. Hola siguiente script de PowerShell pueden toocreate usa un desencadenador de trabajo.

Hola conjunto después de las variables toocorrespond toohello había deseado de trabajo y una programación:

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
    Write-Output $jobTrigger
   ```

### <a name="remove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a>Quitar un trabajo de toostop de asociación programada de ejecución en la programación
se puede quitar toodiscontinue recurrente de ejecución del trabajo a través de un desencadenador de trabajo, el desencadenador de trabajo de Hola.
Quitar un toostop de desencadenador de trabajo un trabajo del que se está ejecutando correspondiente programación tooa con hello **Remove-AzureSqlJobTrigger** cmdlet.

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
   ```

## <a name="import-elastic-database-query-results-tooexcel"></a>Importar tooExcel de resultados de consulta de base de datos elástica
 Puede importar los resultados de Hola desde un consulta tooan del archivo de Excel.

1. Inicie Excel 2013.
2. Navegue toohello **datos** la cinta de opciones.
3. Haga clic en **Desde otros orígenes** y luego en **Desde SQL Server**.

   ![Importación de Excel desde otros orígenes](./media/sql-database-elastic-query-getting-started/exel-sources.png)

4. Hola **Asistente para la conexión de datos** escriba credenciales de inicio de sesión y nombre de servidor de Hola. A continuación, haga clic en **Siguiente**.
5. En el cuadro de diálogo de hello **base de datos de hello Select que contiene datos de Hola que desee**, seleccione hello **ElasticDBQuery** base de datos.
6. Seleccione hello **clientes** de tabla en la vista de lista de Hola y haga clic en **siguiente**. Haga clic en **Finalizar**.
7. Hola **importar datos** formulario, en **Seleccione cómo desea que tooview estos datos en el libro**, seleccione **tabla** y haga clic en **Aceptar**.

Todas las filas de Hola **clientes** tabla, almacenado en particiones diferentes rellenar la hoja de Excel de Hola.

## <a name="next-steps"></a>Pasos siguientes
Ahora puede usar las funciones de datos de Excel. Usar cadena de conexión de hello con el nombre del servidor, nombre de base de datos y las credenciales tooconnect su BI y datos integración herramientas toohello elástico consultar base de datos. Asegúrese de que SQL Server se admite como origen de datos para la herramienta. Consulte toohello consultar elástico base de datos y tablas externas al igual que cualquier otra base de datos de SQL Server y las tablas de SQL Server que se conectará toowith la herramienta.

### <a name="cost"></a>Coste
No hay ningún cargo adicional para usar la característica de consulta de base de datos elástica Hola. Sin embargo, en este momento, esta característica está disponible únicamente en bases de datos premium como un punto de conexión, pero pueden ser particiones de Hola de cualquier nivel de servicio.

Para obtener información sobre los precios, consulte [Detalles de precios de Base de datos SQL](https://azure.microsoft.com/pricing/details/sql-database/).

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
