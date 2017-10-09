---
title: "aaaCreate y administrar los trabajos elásticos mediante PowerShell | Documentos de Microsoft"
description: Usar PowerShell toomanage grupos de base de datos de SQL Azure
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 737d8d13-5632-4e18-9cb0-4d3b8a19e495
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f6c18aecfa7e8c0b102a3b7cd2f266f5542ae400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a>Creación y administración de trabajos elásticos de SQL Database mediante PowerShell (versión preliminar)

Hola PowerShell APIs de **trabajos de base de datos elástica** (en versión preliminar), le permiten definir un grupo de bases de datos con el que se ejecutarán las secuencias de comandos. Este artículo se muestra cómo toocreate y administrar **trabajos de base de datos elástica** mediante cmdlets de PowerShell. Consulte [Información general sobre trabajos elásticos](sql-database-elastic-jobs-overview.md). 

## <a name="prerequisites"></a>Requisitos previos
* Una suscripción de Azure. Para obtener una prueba gratuita, vea [Prueba gratuita de un mes](https://azure.microsoft.com/pricing/free-trial/).
* Un conjunto de bases de datos creadas con herramientas de base de datos elástica Hola. Consulte [Introducción a las herramientas de base de datos elástica](sql-database-elastic-scale-get-started.md).
* Azure PowerShell. Para obtener información detallada, vea [cómo tooinstall y configurar Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).
* **Trabajos de base de datos elástica** : consulte [Installing Trabajos de base de datos elástica](sql-database-elastic-jobs-service-installation.md)

### <a name="select-your-azure-subscription"></a>Selección de su suscripción a Azure
suscripción de hello tooselect necesita su Id. de suscripción (**- SubscriptionId**) o el nombre de la suscripción (**- SubscriptionName**). Si tiene varias suscripciones se puede ejecutar hello **AzureRmSubscription Get** información de suscripción del conjunto de resultados de hello deseada de Hola de cmdlet y copia. Una vez que tenga información de su suscripción, ejecutar Hola después commandlet tooset esta suscripción como valor predeterminado de hello, es decir Hola destino para crear y administrar trabajos:

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

Hola [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) se recomienda para uso toodevelop y ejecutar los scripts de PowerShell frente a los trabajos de base de datos elástica Hola.

## <a name="elastic-database-jobs-objects"></a>Objetos de Trabajos de base de datos elástica
Hola siguiente tabla se enumeran todos los tipos de objeto de Hola de **trabajos de base de datos elástica** junto con su descripción y relevante APIs PowerShell.

<table style="width:100%">
  <tr>
    <th>Tipo de objeto</th>
    <th>Description</th>
    <th>API de PowerShell relacionadas</th>
  </tr>
  <tr>
    <td>Credential:</td>
    <td>Toouse de nombre de usuario y contraseña al conectar toodatabases para la ejecución de secuencias de comandos o aplicación de dacpac. <p>Hola contraseña se cifra antes de enviar tooand almacenar en la base de datos de hello trabajos elástico de base de datos.  servicio de trabajos elástico de base de datos a través de la credencial de hello creado y cargado desde un script de instalación de Hola Hola descifra Hola contraseña.</td>
    <td><p>Get-AzureSqlJobCredential</p>
    <p>New-AzureSqlJobCredential</p><p>Set-AzureSqlJobCredential</p></td></td>
  </tr>

  <tr>
    <td>Script</td>
    <td>Script de Transact-SQL toobe utilizado para la ejecución a través de las bases de datos.  script de Hola debe ser idempotente toobe creados desde servicio Hola volverá a intentar la ejecución del script de Hola tras errores.
    </td>
    <td>
    <p>Get-AzureSqlJobContent</p>
    <p>Get-AzureSqlJobContentDefinition</p>
    <p>New-AzureSqlJobContent</p>
    <p>Set-AzureSqlJobContentDefinition</p>
    </td>
  </tr>

  <tr>
    <td>DACPAC</td>
    <td><a href="https://msdn.microsoft.com/library/ee210546.aspx">Aplicación de capa de datos </a> toobe aplicada entre bases de datos del paquete.

    </td>
    <td>
    <p>Get-AzureSqlJobContent</p>
    <p>New-AzureSqlJobContent</p>
    <p>Set-AzureSqlJobContentDefinition</p>
    </td>
  </tr>
  <tr>
    <td>Destino de la base de datos</td>
    <td>Base de datos y servidor nombre señalador tooan base de datos de SQL Azure.

    </td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>New-AzureSqlJobTarget</p>
    </td>
  </tr>
  <tr>
    <td>Destino de mapa de particiones</td>
    <td>Combinación de un destino de la base de datos y una credencial toobe utiliza toodetermine la información almacenada dentro de un mapa de particiones de base de datos elástica.
    </td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>New-AzureSqlJobTarget</p>
    <p>Set-AzureSqlJobTarget</p>
    </td>
  </tr>
<tr>
    <td>Destino de colección personalizada</td>
    <td>Usar grupo definido de toocollectively de las bases de datos para la ejecución.</td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>New-AzureSqlJobTarget</p>
    </td>
  </tr>
<tr>
    <td>Destino secundario de colección personalizada</td>
    <td>Destino de base de datos al que se hace referencia en una colección personalizada.</td>
    <td>
    <p>Add-AzureSqlJobChildTarget</p>
    <p>Remove-AzureSqlJobChildTarget</p>
    </td>
  </tr>

<tr>
    <td>Trabajo</td>
    <td>
    <p>Definición de parámetros para un trabajo que pueden ser utilizados tootrigger ejecución o toofulfill una programación.</p>
    </td>
    <td>
    <p>Get-AzureSqlJob</p>
    <p>New-AzureSqlJob</p>
    <p>Set-AzureSqlJob</p>
    </td>
  </tr>

<tr>
    <td>Ejecución de trabajos</td>
    <td>
    <p>Contenedor de tareas de toofulfill es necesario ejecutar una secuencia de comandos o aplicar un destino de tooa DACPAC con credenciales para las conexiones de base de datos con errores se controla en la directiva de ejecución de acuerdo tooan.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecution</p>
    <p>Start-AzureSqlJobExecution</p>
    <p>Stop-AzureSqlJobExecution</p>
    <p>Wait-AzureSqlJobExecution</p>
  </tr>

<tr>
    <td>Ejecución de tareas de trabajo</td>
    <td>
    <p>Unidad única de trabajo toofulfill un trabajo.</p>
    <p>Si una tarea de trabajo no es capaz de toosuccessfully ejecutar, se registrará el mensaje de excepción resultante de Hola y se creará una nueva tarea de trabajo coincidente y ejecutan en toohello según lo especificado directiva de ejecución.</p></p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecution</p>
    <p>Start-AzureSqlJobExecution</p>
    <p>Stop-AzureSqlJobExecution</p>
    <p>Wait-AzureSqlJobExecution</p>
  </tr>

<tr>
    <td>Directiva de ejecución de trabajos</td>
    <td>
    <p>Controla los tiempos de espera, los límites de reintentos y los intervalos entre reintentos de la ejecución de trabajos.</p>
    <p>Trabajos de base de datos elástica incluye una directiva de ejecución de trabajos predeterminada que, básicamente, producirá un número infinito de reintentos de errores de tareas de trabajo con retroceso exponencial de intervalos entre reintentos.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecutionPolicy</p>
    <p>New-AzureSqlJobExecutionPolicy</p>
    <p>Set-AzureSqlJobExecutionPolicy</p>
    </td>
  </tr>

<tr>
    <td>Schedule</td>
    <td>
    <p>Tiempo según la especificación de contexto de ejecución tootake en un intervalo de repetición o de una sola vez.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobSchedule</p>
    <p>New-AzureSqlJobSchedule</p>
    <p>Set-AzureSqlJobSchedule</p>
    </td>
  </tr>

<tr>
    <td>Desencadenadores de trabajo</td>
    <td>
    <p>Una asignación entre un trabajo y programación tootrigger ejecución de un trabajo según la programación de toohello.</p>
    </td>
    <td>
    <p>New-AzureSqlJobTrigger</p>
    <p>Remove-AzureSqlJobTrigger</p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a>Tipos de grupo de trabajos de base de datos elástica admitidos
trabajo de Hello ejecuta scripts Transact-SQL (T-SQL) o una aplicación de DACPACs a través de un grupo de bases de datos. Un trabajo una vez enviado toobe ejecutado a través de un grupo de bases de datos, trabajo Hola "expande" hello en los trabajos secundarios donde cada uno realiza Hola solicitó la ejecución en una base de datos en el grupo de Hola. 

Hay dos tipos de grupos que puede crear: 

* [Mapa de particiones](sql-database-elastic-scale-shard-map-management.md) grupo: cuando un trabajo está tootarget enviado un mapa de particiones, Hola consulta toodetermine de mapa de particiones de hello su conjunto actual de particiones y, a continuación, crea secundarios trabajos para cada partición en el mapa de particiones de Hola.
* Grupo Colección personalizada: conjunto personalizado de bases de datos. Cuando un trabajo está destinado a una colección personalizada, crea a secundarios trabajos para cada base de datos actualmente en la colección personalizada hello.

## <a name="tooset-hello-elastic-database-jobs-connection"></a>Hola tooset conexión de base de datos elástica trabajos
Una conexión debe establecer toohello trabajos de toobe *base de datos de control* toousing anterior Hola trabajos API. Si ejecuta este cmdlet, desencadena una toopop de ventana de credencial de solicitar el nombre de usuario de Hola y la contraseña que creó durante la instalación de los trabajos de base de datos elástica. En todos los ejemplos que se ofrecen en este tema se da por hecho que este primer paso ya se realizó.

Abrir otra conexión toohello elástico de base de datos de trabajos:

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-hello-elastic-database-jobs"></a>Credenciales cifradas dentro de los trabajos de base de datos elástica Hola
Las credenciales de la base de datos se pueden insertar en los trabajos de hello *base de datos de control* con su contraseña cifrada. Es necesario toostore credenciales tooenable trabajos toobe ejecutado en un momento posterior, (uso de las programaciones de trabajo).

Cifrado funciona a través de un certificado creado como parte del script de instalación de Hola. crea el script de instalación de Hola y certificado de Hola de cargas en hello servicio de nube de Azure para el descifrado de hello almacena contraseñas cifradas. Hola servicio de nube de Azure más adelante guarda la clave pública de hello en los trabajos de hello *base de datos de control* que permite Hola API de PowerShell o el Portal de Azure clásico interfaz tooencrypt una contraseña proporcionada sin necesidad de certificado de Hola toobe instalado localmente.

las contraseñas de credencial de Hello son cifrada y segura de los usuarios con objetos de trabajos de base de datos de tooElastic de acceso de solo lectura. Pero es posible que un usuario malintencionado con acceso de lectura y escritura tooElastic trabajos de base de datos objetos tooextract una contraseña. Las credenciales son toobe diseñada reutilizar en las ejecuciones del trabajo. Las credenciales se pasan las bases de datos de tootarget al establecer conexiones. Actualmente no hay ninguna restricción en bases de datos de destino de hello utilizadas para cada credencial, un usuario malintencionado podría agregar un destino de la base de datos para una base de datos bajo el control del usuario malintencionado Hola. usuario de Hello posteriormente pudo iniciar un trabajo que se dirige a la contraseña del esta base de datos toogain Hola credencial.

Los procedimientos recomendados de seguridad para Trabajos de base de datos elástica son:

* Limitar el uso de las personas de hello API tootrusted.
* Las credenciales deben tener Hola tarea de mínimos privilegios necesarios tooperform hello trabajo.  Puede ver más información en este artículo de MSDN sobre SQL Server, [Autorización y permisos](https://msdn.microsoft.com/library/bb669084.aspx) .

### <a name="toocreate-an-encrypted-credential-for-job-execution-across-databases"></a>toocreate una credencial para la ejecución de trabajos entre bases de datos cifrada
toocreate un nuevo cifrado de credenciales, hello [ **cmdlet Get-Credential** ](https://technet.microsoft.com/library/hh849815.aspx) pide un nombre de usuario y una contraseña que se pueden pasar toohello [ **AzureSqlJobCredential de nuevo cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="tooupdate-credentials"></a>credenciales de tooupdate
Cuando cambien las contraseñas, usar hello [ **cmdlet Set-AzureSqlJobCredential** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) conjunto hello y **CredentialName** parámetro.

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="toodefine-an-elastic-database-shard-map-target"></a>toodefine un destino de asignación de particiones de bases de datos elásticas
tooexecute un trabajo en todas las bases de datos en un conjunto de particiones (creado con [biblioteca de cliente de base de datos elástica](sql-database-elastic-database-client-library.md)), utiliza un mapa de particiones como destino de la base de datos de Hola. Este ejemplo requiere una aplicación particionada creada mediante la biblioteca de cliente de base de datos elástica Hola. Consulte [Introducción a las herramientas de Base de datos elástica](sql-database-elastic-scale-get-started.md).

base de datos de administrador de asignación de Hello particiones se debe establecer como destino de la base de datos y, a continuación, mapa de particiones específicas de hello debe especificarse como un destino.

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a>Crear un script T-SQL para su ejecución transversal en las bases de datos
Al crear scripts de T-SQL para su ejecución, se recomienda encarecidamente toobuild les toobe [idempotente](https://en.wikipedia.org/wiki/Idempotence) y resistentes a los errores. Trabajos de base de datos elásticos volverá a intentar la ejecución de una secuencia de comandos cada vez que la ejecución encuentra un error, independientemente de clasificación de Hola de error de Hola.

Hola de uso [ **cmdlet New-AzureSqlJobContent** ](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate guardar un script para su ejecución y establezca hello **- ContentName** y **- CommandText**parámetros.

    $scriptName = "Create a TestTable"

    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
        CREATE TABLE TestTable(
            TestTableId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="create-a-new-script-from-a-file"></a>Creación de un script desde un archivo
Si Hola script T-SQL se define dentro de un archivo, use este script de Hola tooimport:

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path tooSQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="tooupdate-a-t-sql-script-for-execution-across-databases"></a>secuencia de comandos de tooupdate un instrucción T-SQL para su ejecución en bases de datos
Estas actualizaciones de secuencia de comandos de PowerShell Hola texto de comando de T-SQL para un script existente.

Conjunto Hola siguiendo definición toobe conjunto de variables tooreflect Hola deseado script:

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column tooTestTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
    CREATE TABLE TestTable(
        TestTableId INT PRIMARY KEY IDENTITY,
        InsertionTime DATETIME2
    );
    END
    GO

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN
    ALTER TABLE TestTable
    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO"

### <a name="tooupdate-hello-definition-tooan-existing-script"></a>tooupdate Hola definición tooan secuencia de comandos existente
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="toocreate-a-job-tooexecute-a-script-across-a-shard-map"></a>toocreate un tooexecute de trabajo una secuencia de comandos a través de un mapa de particiones
El siguiente script de PowerShell inicia un trabajo para la ejecución de un script en cada partición de un mapa de particiones de escala elástica.

Hola conjunto después Hola de variables tooreflect había deseado script y destino:

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="tooexecute-a-job"></a>tooexecute un trabajo
Este script de PowerShell ejecuta un trabajo existente:

Hola de actualización después de la variable tooreflect Hola deseado toohave de nombre de trabajo ejecuta:

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="tooretrieve-hello-state-of-a-single-job-execution"></a>estado de hello tooretrieve una única ejecución de trabajo
Hola de uso [ **cmdlet Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) conjunto hello y **JobExecutionId** estado de hello tooview los parámetros de ejecución del trabajo.

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

Use Hola mismo **Get AzureSqlJobExecution** cmdlet con hello **IncludeChildren** estado de hello tooview los parámetros de las ejecuciones de trabajo secundarios, es decir Hola estado específico para cada ejecución del trabajo en todas base de datos de destino de trabajo de Hola.

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="tooview-hello-state-across-multiple-job-executions"></a>estado de hello tooview a través de varias ejecuciones del trabajo
Hola [ **cmdlet Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) tiene varios parámetros opcionales que pueden ser utilizado toodisplay múltiples ejecuciones del trabajo, filtradas mediante parámetros de hello proporcionado. siguiente Hello muestra algunas de hello formas toouse AzureSqlJobExecution Get:

Recuperar todas las ejecuciones de trabajos activos de nivel superior:

    Get-AzureSqlJobExecution

Recuperar todas las ejecuciones de trabajos de nivel superior, incluidas las ejecuciones de trabajos inactivos:

    Get-AzureSqlJobExecution -IncludeInactive

Recuperar todas las ejecuciones de trabajos secundarios de un identificador de ejecución de trabajos proporcionado, incluidas las ejecuciones de trabajos inactivos:

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

Recuperar todas las ejecuciones de trabajos creadas con una combinación de programación y trabajo, incluidos los trabajos inactivos:

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

Recuperar todos los trabajos que se destinan a un mapa de particiones especificado, incluidos los trabajos inactivos:

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

Recuperar todos los trabajos que se destinan a una colección personalizada especificada, incluidos los trabajos inactivos:

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

Recuperar la lista de Hola de ejecuciones de la tarea de trabajo dentro de la ejecución de un trabajo específico:

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

Recuperar los detalles de ejecución de tareas de trabajo:

Hola siguiente script de PowerShell puede ser utilizados tooview Hola detalles de una ejecución de la tarea de trabajo, que es especialmente útil al depurar errores de ejecución.

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="tooretrieve-failures-within-job-task-executions"></a>errores de tooretrieve dentro de las ejecuciones de tareas de trabajo
Hola **JobTaskExecution objeto** incluye una propiedad para el ciclo de vida de Hola de tarea hello junto con una propiedad de mensaje. Si se produce un error en una ejecución de la tarea de trabajo, propiedad de ciclo de vida de Hola se establecerá demasiado*error* y se establecerá la propiedad de mensaje de Hola toohello mensaje de excepción resultante y la pila. Si un trabajo no es correcta, es importante tooview detalles de Hola de tareas de trabajo que no se realizó correctamente para un trabajo determinado.

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="toowait-for-a-job-execution-toocomplete"></a>toowait para un toocomplete de ejecución de trabajo
Hola siguiente script de PowerShell puede ser usado toowait para un toocomplete de tareas de trabajo:

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

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

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a>Actualización de una directiva de ejecución personalizada
Tooupdate de directiva de ejecución de actualización Hola deseado:

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a>Cancelación de un trabajo
Trabajos de base de datos elástica admite solicitudes de cancelación de trabajos.  Si los trabajos de base de datos elástica detecta una solicitud de cancelación de un trabajo que se está ejecutando actualmente, tratará de trabajo de hello toostop.

Trabajos de base de datos elástica puede realizar una cancelación de dos formas distintas:

1. Cancelar están ejecutando tareas actualmente: si se detecta una cancelación mientras una tarea se está ejecutando actualmente, se intentará una cancelación dentro de hello ejecutando el aspecto de la tarea hello.  Por ejemplo: si hay una consulta de ejecución prolongada que se están llevando a cabo cuando se intenta realizar una cancelación, habrá una consulta de hello toocancel intento.
2. Cancelación de reintentos: si se detecta una cancelación por subproceso de control de hello antes de que se inicia una tarea para su ejecución, el subproceso de control de Hola se evitar iniciar tarea hello y declarar solicitud hello como cancelada.

Si se solicita una cancelación de trabajo para un trabajo primario, se respetará la solicitud de cancelación de Hola de trabajo primario de Hola y para todos los trabajos secundarios.

toosubmit una solicitud de cancelación, utilice hello [ **cmdlet Stop-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) conjunto hello y **JobExecutionId** parámetro.

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="toodelete-a-job-and-job-history-asynchronously"></a>toodelete un trabajo y el historial de trabajos de forma asincrónica
Trabajos de base de datos elástica admite la eliminación asincrónica de trabajos. Un trabajo se puede marcar para su eliminación y sistema de hello eliminará trabajo hello y su historial de trabajo una vez han completado todas las ejecuciones del trabajo para el trabajo de Hola. sistema de Hello no cancelará automáticamente las ejecuciones del trabajo activo.  

Invocar [ **Stop AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel ejecuciones de trabajo activo.

eliminación de trabajo tootrigger, use hello [ **cmdlet Remove-AzureSqlJob** ](/powershell/module/elasticdatabasejobs/remove-azuresqljob) conjunto hello y **JobName** parámetro.

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="toocreate-a-custom-database-target"></a>toocreate un destino de la base de datos personalizada
Puede definir bases de datos de destino personalizadas para la ejecución directa o para su inclusión en un grupo personalizado de bases de datos. Por ejemplo, porque **grupos elásticos** están aún no admiten directamente mediante PowerShell APIs, puede crear un destino de la base de datos personalizada y el destino de la colección de base de datos personalizada que abarca todas las bases de datos de hello en el grupo de Hola.

Establecer Hola siguiendo la información de base de datos de las variables tooreflect Hola deseado:

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="toocreate-a-custom-database-collection-target"></a>toocreate un destino de recopilación de la base de datos personalizada
Hola de uso [ **New-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) toodefine cmdlet una ejecución de tooenable del destino de colección personalizada de la base de datos a través de varios destinos de la base de datos definido. Después de crear un grupo de base de datos, se pueden asociadas con el destino de colección personalizada hello las bases de datos.

Establecer Hola siguiente configuración de destino de colección personalizada deseada de variables tooreflect hello:

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="tooadd-databases-tooa-custom-database-collection-target"></a>destino de colección de base de datos personalizada tooa de tooadd las bases de datos
tooadd una recopilación personalizada específica de tooa de base de datos use hello [ **agregar AzureSqlJobChildTarget** ](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a>Revise las bases de datos de hello dentro de un destino de colección de la base de datos personalizada
Hola de uso [ **Get AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) bases de datos de cmdlet tooretrieve Hola secundarios dentro de un destino de colección de la base de datos personalizada. 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a>Crear una secuencia de comandos de un tooexecute de trabajo a través de un destino de recopilación de la base de datos personalizada
Hola de uso [ **New-AzureSqlJob** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) toocreate cmdlet un trabajo para un grupo de bases de datos definidas por un destino de recopilación de la base de datos personalizada. Trabajos de base de datos elásticos expandirán trabajo hello en varios puestos de secundarios cada base de datos correspondiente de tooa asociados con el destino de colección de base de datos personalizada hello y asegúrese de que se ejecuta el script de Hola en cada base de datos. Una vez más, es importante que los scripts son idempotentes toobe resistente tooretries.

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a>Recopilación de datos de una base de datos a otra
Puede usar un tooexecute una consulta de trabajo a través de un grupo de bases de datos y tabla específica de hello resultados tooa de envío. tabla de Hello puede consultarse después Hola hechos toosee Hola resultados de la consulta de cada base de datos. Esto proporciona un método asincrónico tooexecute una consulta entre varias bases de datos. Los intentos incorrectos se controlan automáticamente mediante reintentos.

tabla de destino especificado de Hola se creará automáticamente si aún no existe. nueva tabla de Hello coincide con esquema Hola de hello devolvió un conjunto de resultados. Si una secuencia de comandos devuelve varios conjuntos de resultados, trabajos de base de datos elástica sólo enviará la primera tabla de destino toohello Hola.

Hola siguiente script de PowerShell ejecuta una secuencia de comandos y recopila los resultados en una tabla especificada. Este script presupone que se creó un script T-SQL que genera un único conjunto de resultados y que se creó una colección de bases de datos personalizada de destino.

Este script utiliza hello [ **Get AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet. Establecer los parámetros de hello para la secuencia de comandos, las credenciales y de destino de ejecución:

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

### <a name="toocreate-and-start-a-job-for-data-collection-scenarios"></a>toocreate e iniciar un trabajo para escenarios de recopilación de datos
Este script utiliza hello [ **inicio AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.

    $job = New-AzureSqlJob -JobName $jobName 
    -CredentialName $executionCredentialName 
    -ContentName $scriptName 
    -ResultSetDestinationServerName $destinationServerName 
    -ResultSetDestinationDatabaseName $destinationDatabaseName 
    -ResultSetDestinationSchemaName $destinationSchemaName 
    -ResultSetDestinationTableName $destinationTableName 
    -ResultSetDestinationCredentialName $destinationCredentialName 
    -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution

## <a name="tooschedule-a-job-execution-trigger"></a>tooschedule un desencadenador de ejecución de trabajo
Hola siguiente script de PowerShell puede ser utilizado toocreate una programación periódica. Este script usa un intervalo de minutos, pero [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) también admite los parámetros -DayInterval, -HourInterval, -MonthInterval y -WeekInterval. Se pueden crear programaciones que se ejecutan una sola vez pasando -OneTime.

Creación de una programación:

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="tootrigger-a-job-executed-on-a-time-schedule"></a>tootrigger un trabajo que se ejecuta según una programación de tiempo
Un desencadenador de trabajo puede ser toohave definido una programación de tiempo de trabajo ejecuta correspondiente tooa. Hola siguiente script de PowerShell pueden toocreate usa un desencadenador de trabajo.

Use [AzureSqlJobTrigger New](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) y conjunto Hola siguiendo las variables toocorrespond toohello deseado trabajo y una programación:

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="tooremove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a>tooremove un trabajo de toostop asociación programada de ejecutarse en programación
se puede quitar toodiscontinue recurrente de ejecución del trabajo a través de un desencadenador de trabajo, el desencadenador de trabajo de Hola. Quitar un toostop de desencadenador de trabajo un trabajo del que se está ejecutando correspondiente programación tooa con hello [ **cmdlet Remove-AzureSqlJobTrigger**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-tooa-time-schedule"></a>Recuperar la programación de tiempo de trabajo desencadenadores tooa enlazado
Hola siguiente script de PowerShell puede tooobtain usado y mostrar programación de tiempo determinado de hello trabajo desencadenadores tooa registrados.

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="tooretrieve-job-triggers-bound-tooa-job"></a>desencadenadores de trabajo tooretrieve enlazados tooa trabajo
Use [AzureSqlJobTrigger Get](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain y mostrar programaciones que contiene un trabajo registrado.

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="toocreate-a-data-tier-application-dacpac-for-execution-across-databases"></a>toocreate una aplicación de capa de datos (DACPAC) para la ejecución a través de las bases de datos
vea toocreate un DACPAC [Data-Tier applications](https://msdn.microsoft.com/library/ee210546.aspx). toodeploy un DACPAC, usar hello [cmdlet New-AzureSqlJobContent](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent). Hola DACPAC debe ser accesible toohello servicio. Es recomendable tooupload una tooAzure DACPAC creado almacenamiento y crear un [firma de acceso compartido](../storage/common/storage-dotnet-shared-access-signature-part-1.md) para hello DACPAC.

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="tooupdate-a-data-tier-application-dacpac-for-execution-across-databases"></a>tooupdate una aplicación de capa de datos (DACPAC) para la ejecución a través de las bases de datos
Dacpac existente registrado en un período trabajos elástico de base de datos puede ser actualizada toopoint toonew URI. Hola de uso [ **cmdlet Set-AzureSqlJobContentDefinition** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate hello DACPAC URI en una existente registrado DACPAC:

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="toocreate-a-job-tooapply-a-data-tier-application-dacpac-across-databases"></a>toocreate una tooapply una aplicación de capa de datos (DACPAC) a través de las bases de datos de trabajo
Una vez creado un DACPAC en trabajos elástico de base de datos, un trabajo puede crearse tooapply hello DACPAC a través de un grupo de bases de datos. Hola siguiente script de PowerShell pueden toocreate usa un trabajo DACPAC a través de una colección personalizada de las bases de datos:

    $jobName = "{Job Name}"
    $dacpacName = "{Dacpac Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget 
    -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob 
    -JobName $jobName 
    -CredentialName $credentialName 
    -ContentName $dacpacName -TargetId $target.TargetId
    Write-Output $job 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-powershell/cmd-prompt.png
[2]: ./media/sql-database-elastic-jobs-powershell/portal.png
<!--anchors-->
