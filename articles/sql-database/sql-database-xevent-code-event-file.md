---
title: "aaaXEvent código de archivo de eventos de base de datos SQL | Documentos de Microsoft"
description: "Proporciona PowerShell y Transact-SQL para obtener un ejemplo de código en dos fases que muestra el destino de archivo de eventos de hello en un evento extendido en la base de datos de SQL Azure. Almacenamiento de Azure es una parte necesaria en este escenario."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: bbb10ecc-739f-4159-b844-12b4be161231
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: genemi
ms.openlocfilehash: 4457bd3250f4644b54da2f7daddb9da12070e93a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="event-file-target-code-for-extended-events-in-sql-database"></a>Código de destino del archivo de evento para eventos extendidos en Base de datos SQL

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

Un ejemplo de código completo que desea para una manera segura toocapture y notificar información para un evento extendido.

En Microsoft SQL Server, Hola [destino de archivo de evento](http://msdn.microsoft.com/library/ff878115.aspx) es salidas de evento toostore usado en un archivo de disco duro local. Pero estos archivos no están disponible tooAzure base de datos SQL. En su lugar, usamos el destino de archivo de eventos de hello almacenamiento de Azure servicio toosupport Hola.

En este tema se presenta un ejemplo de código de dos fases:

* PowerShell, toocreate un contenedor de almacenamiento de Azure en la nube de Hola.
* Transact-SQL:
  
  * destino de archivo de eventos de la tooan de contenedor de almacenamiento de Azure con tooassign Hola.
  * toocreate e inicie sesión de eventos de hello y así sucesivamente.

## <a name="prerequisites"></a>Requisitos previos

* Una cuenta y una suscripción de Azure. Puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Cualquier base de datos donde pueda crear una tabla.
  
  * De manera opcional, puede [crear una base de datos de **AdventureWorksLT** de demostración](sql-database-get-started.md) en cuestión de minutos.
* SQL Server Management Studio (ssms.exe), idealmente la versión de actualización mensual más reciente. 
  Puede descargar hello ssms.exe más reciente desde:
  
  * El tema titulado [Descarga de SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).
  * [Una descarga de toohello vínculo directo.](http://go.microsoft.com/fwlink/?linkid=616025)
* Debe tener hello [módulos de PowerShell de Azure](http://go.microsoft.com/?linkid=9811175) instalado.
  
  * módulos de Hello proporcionan comandos como - **AzureStorageAccount nuevo**.

## <a name="phase-1-powershell-code-for-azure-storage-container"></a>Fase 1: código de PowerShell para el contenedor de Almacenamiento de Azure

Este PowerShell es la fase 1 hello en dos fases del ejemplo de código.

script de Hola se inicia con comandos tooclean después de ejecutar una posible anterior y es rerunnable.

1. Pegue el script de PowerShell de hello en un editor de texto sencillo como Notepad.exe y guarde el script de Hola como un archivo con extensión hello **. ps1**.
2. Inicie PowerShell ISE como administrador.
3. En el símbolo del sistema de hello, escriba<br/>`Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser`<br/>y, luego, presione Entrar.
4. En PowerShell ISE, abra el archivo **.ps1** . Ejecutar script de Hola.
5. script de Hola inicia una nueva ventana en la que iniciar sesión en tooAzure por primera vez.
   
   * Si vuelve a ejecutar el script de Hola sin interrumpir la sesión, tendrá posibilidad cómoda de Hola de comentar hello **Add-AzureAccount** comando.

![PowerShell ISE, con Azure módulo instalado, script toorun listo.][30_powershell_ise]


### <a name="powershell-code"></a>Código de PowerShell

```powershell
## TODO: Before running, find all 'TODO' and make each edit!!

#--------------- 1 -----------------------


# You can comment out or skip this Add-AzureAccount
# command after hello first run.
# Current PowerShell environment retains hello successful outcome.

'Expect a pop-up window in which you log in tooAzure.'


Add-AzureAccount

#-------------- 2 ------------------------


'
TODO: Edit hello values assigned toothese variables, especially hello first few!
'

# Ensure hello current date is between
# hello Expiry and Start time values that you edit here.

$subscriptionName    = 'YOUR_SUBSCRIPTION_NAME'
$policySasExpiryTime = '2016-01-28T23:44:56Z'
$policySasStartTime  = '2015-08-01'


$storageAccountName     = 'gmstorageaccountxevent'
$storageAccountLocation = 'West US'
$contextName            = 'gmcontext'
$containerName          = 'gmcontainerxevent'
$policySasToken         = 'gmpolicysastoken'


# Leave this value alone, as 'rwl'.
$policySasPermission = 'rwl'

#--------------- 3 -----------------------


# hello ending display lists your Azure subscriptions.
# One should match hello $subscriptionName value you assigned
#   earlier in this PowerShell script. 

'Choose an existing subscription for hello current PowerShell environment.'


Select-AzureSubscription -SubscriptionName $subscriptionName


#-------------- 4 ------------------------


'
Clean up hello old Azure Storage Account after any previous run, 
before continuing this new run.'


If ($storageAccountName)
{
    Remove-AzureStorageAccount -StorageAccountName $storageAccountName
}

#--------------- 5 -----------------------

[System.DateTime]::Now.ToString()

'
Create a storage account. 
This might take several minutes, will beep when ready.
  ...PLEASE WAIT...'

New-AzureStorageAccount `
    -StorageAccountName $storageAccountName `
    -Location           $storageAccountLocation

[System.DateTime]::Now.ToString()

[System.Media.SystemSounds]::Beep.Play()


'
Get hello primary access key for your storage account.
'


$primaryAccessKey_ForStorageAccount = `
    (Get-AzureStorageKey `
        -StorageAccountName $storageAccountName).Primary

"`$primaryAccessKey_ForStorageAccount = $primaryAccessKey_ForStorageAccount"

'Azure Storage Account cmdlet completed.
Remainder of PowerShell .ps1 script continues.
'

#--------------- 6 -----------------------


# hello context will be needed toocreate a container within hello storage account.

'Create a context object from hello storage account and its primary access key.
'

$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey  $primaryAccessKey_ForStorageAccount


'Create a container within hello storage account.
'


$containerObjectInStorageAccount = New-AzureStorageContainer `
    -Name    $containerName `
    -Context $context


'Create a security policy toobe applied toohello SAS token.
'

New-AzureStorageContainerStoredAccessPolicy `
    -Container  $containerName `
    -Context    $context `
    -Policy     $policySasToken `
    -Permission $policySasPermission `
    -ExpiryTime $policySasExpiryTime `
    -StartTime  $policySasStartTime 

'
Generate a SAS token for hello container.
'
Try
{
    $sasTokenWithPolicy = New-AzureStorageContainerSASToken `
        -Name    $containerName `
        -Context $context `
        -Policy  $policySasToken
}
Catch 
{
    $Error[0].Exception.ToString()
}

#-------------- 7 ------------------------


'Display hello values that YOU must edit into hello Transact-SQL script next!:
'

"storageAccountName: $storageAccountName"
"containerName:      $containerName"
"sasTokenWithPolicy: $sasTokenWithPolicy"

'
REMINDER: sasTokenWithPolicy here might start with "?" character, which you must exclude from Transact-SQL.
'

'
(Later, return here toodelete your Azure Storage account. See hello preceding - Remove-AzureStorageAccount -StorageAccountName $storageAccountName)'

'
Now shift toohello Transact-SQL portion of hello two-part code sample!'

# EOFile
```


Tome nota de hello pocos valores con nombre que se imprime el script de PowerShell de hello cuando termina. Debe modificar esos valores en hello secuencia de comandos de Transact-SQL que sigue a la fase 2.

## <a name="phase-2-transact-sql-code-that-uses-azure-storage-container"></a>Fase 2: código de Transact-SQL que usa el contenedor de Almacenamiento de Azure

* En la fase 1 de este ejemplo de código, que ejecutó un toocreate de secuencia de comandos de PowerShell un contenedor de almacenamiento de Azure.
* A continuación en la fase 2, hello siguiente script de Transact-SQL debe utilizar Hola contenedor.

script de Hola se inicia con comandos tooclean después de ejecutar una posible anterior y es rerunnable.

Hola script de PowerShell imprime unos pocos valores con nombre cuando se terminó. Debe editar toouse de script de Transact-SQL de hello esos valores. Buscar **tareas** Hola de hello Transact-SQL script toolocate puntos de edición.

1. Abra SQL Server Management Studio (ssms.exe).
2. Conectar la base de datos de base de datos de SQL Azure tooyour.
3. Haga clic en tooopen un nuevo panel de consulta.
4. Pegue Hola siguiente secuencia de comandos de Transact-SQL en el panel de consulta de Hola.
5. Buscar cada **tareas** en Hola script y realice modificaciones adecuado de Hola.
6. Guarde y, a continuación, ejecute el script de Hola.


> [!WARNING]
> valor de clave de SAS generado por hello precede el script de PowerShell de Hola debería comenzar con un '?' (signo de interrogación). Cuando se utiliza la clave SAS de Hola Hola siguiente secuencia de comandos de T-SQL, debe *quitar inicial de hello '?'* . De lo contrario, podrían bloquearse su trabajo por motivos de seguridad.


### <a name="transact-sql-code"></a>Código Transact-SQL

```sql
---- TODO: First, run hello PowerShell portion of this two-part code sample.
---- TODO: Second, find every 'TODO' in this Transact-SQL file, and edit each.

---- Transact-SQL code for Event File target on Azure SQL Database.


SET NOCOUNT ON;
GO


----  Step 1.  Establish one little table, and  ---------
----  insert one row of data.


IF EXISTS
    (SELECT * FROM sys.objects
        WHERE type = 'U' and name = 'gmTabEmployee')
BEGIN
    DROP TABLE gmTabEmployee;
END
GO


CREATE TABLE gmTabEmployee
(
    EmployeeGuid         uniqueIdentifier   not null  default newid()  primary key,
    EmployeeId           int                not null  identity(1,1),
    EmployeeKudosCount   int                not null  default 0,
    EmployeeDescr        nvarchar(256)          null
);
GO


INSERT INTO gmTabEmployee ( EmployeeDescr )
    VALUES ( 'Jane Doe' );
GO


------  Step 2.  Create key, and  ------------
------  Create credential (your Azure Storage container must already exist).


IF NOT EXISTS
    (SELECT * FROM sys.symmetric_keys
        WHERE symmetric_key_id = 101)
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '0C34C960-6621-4682-A123-C7EA08E3FC46' -- Or any newid().
END
GO


IF EXISTS
    (SELECT * FROM sys.database_scoped_credentials
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        WHERE name = 'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent')
BEGIN
    DROP DATABASE SCOPED CREDENTIAL
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent] ;
END
GO


CREATE
    DATABASE SCOPED
    CREDENTIAL
        -- use '.blob.',   and not '.queue.' or '.table.' etc.
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    WITH
        IDENTITY = 'SHARED ACCESS SIGNATURE',  -- "SAS" token.
        -- TODO: Paste in hello long SasToken string here for Secret, but exclude any leading '?'.
        SECRET = 'sv=2014-02-14&sr=c&si=gmpolicysastoken&sig=EjAqjo6Nu5xMLEZEkMkLbeF7TD9v1J8DNB2t8gOKTts%3D'
    ;
GO


------  Step 3.  Create (define) an event session.  --------
------  hello event session has an event with an action,
------  and a has a target.

IF EXISTS
    (SELECT * from sys.database_event_sessions
        WHERE name = 'gmeventsessionname240b')
BEGIN
    DROP
        EVENT SESSION
            gmeventsessionname240b
        ON DATABASE;
END
GO


CREATE
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE

    ADD EVENT
        sqlserver.sql_statement_starting
            (
            ACTION (sqlserver.sql_text)
            WHERE statement LIKE 'UPDATE gmTabEmployee%'
            )
    ADD TARGET
        package0.event_file
            (
            -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
            -- Also, tweak hello .xel file name at end, if you like.
            SET filename =
                'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent/anyfilenamexel242b.xel'
            )
    WITH
        (MAX_MEMORY = 10 MB,
        MAX_DISPATCH_LATENCY = 3 SECONDS)
    ;
GO


------  Step 4.  Start hello event session.  ----------------
------  Issue hello SQL Update statements that will be traced.
------  Then stop hello session.

------  Note: If hello target fails tooattach,
------  hello session must be stopped and restarted.

ALTER
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE
    STATE = START;
GO


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM gmTabEmployee;

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe';

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 13
    WHERE EmployeeDescr = 'Jane Doe';

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM gmTabEmployee;
GO


ALTER
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE
    STATE = STOP;
GO


-------------- Step 5.  Select hello results. ----------

SELECT
        *, 'CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS!' as [CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS],
        CAST(event_data AS XML) AS [event_data_XML]  -- TODO: In ssms.exe results grid, double-click this cell!
    FROM
        sys.fn_xe_file_target_read_file
            (
                -- TODO: Fill in Storage Account name, and hello associated Container name.
                'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent/anyfilenamexel242b',
                null, null, null
            );
GO


-------------- Step 6.  Clean up. ----------

DROP
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE;
GO

DROP DATABASE SCOPED CREDENTIAL
    -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
    [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    ;
GO

DROP TABLE gmTabEmployee;
GO

PRINT 'Use PowerShell Remove-AzureStorageAccount toodelete your Azure Storage account!';
GO
```


Si el destino de hello falla tooattach cuando se ejecuta, deberá detener y reiniciar la sesión de eventos de Hola:

```sql
ALTER EVENT SESSION ... STATE = STOP;
GO
ALTER EVENT SESSION ... STATE = START;
GO
```


## <a name="output"></a>Salida

Cuando se completa el Hola script Transact-SQL, haga clic en una celda en hello **event_data_XML** encabezado de columna. Aparece un elemento **<event>** que muestra una instrucción UPDATE.

Este es un elemento **<event>** que se generó durante la prueba:


```xml
<event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T19:18:45.420Z">
  <data name="state">
    <value>0</value>
    <text>Normal</text>
  </data>
  <data name="line_number">
    <value>5</value>
  </data>
  <data name="offset">
    <value>148</value>
  </data>
  <data name="offset_end">
    <value>368</value>
  </data>
  <data name="statement">
    <value>UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe'</value>
  </data>
  <action name="sql_text" package="sqlserver">
    <value>

SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM gmTabEmployee;

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe';

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 13
    WHERE EmployeeDescr = 'Jane Doe';

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM gmTabEmployee;
</value>
  </action>
</event>
```


Hola Hola de script que se utiliza Transact-SQL anterior sigue sistema función tooread Hola event_file:

* [sys.fn_xe_file_target_read_file (Transact-SQL)](http://msdn.microsoft.com/library/cc280743.aspx)

Obtener una explicación de las opciones avanzadas de visualización de Hola de datos de eventos extendidos está disponible en:

* [Advanced Viewing of Target Data from Extended Events (Visualización avanzada de datos de destino de eventos extendidos)](http://msdn.microsoft.com/library/mt752502.aspx)


## <a name="converting-hello-code-sample-toorun-on-sql-server"></a>Convertir toorun de ejemplo de código de hello en SQL Server

Suponga que deseaba hello toorun anterior ejemplo de Transact-SQL en Microsoft SQL Server.

* Para simplificar, desearía toocompletely reemplazar uso del contenedor de almacenamiento de Azure Hola con un simple archivo como **C:\myeventdata.xel**. archivo Hello se escribiría toohello unidad de disco duro local del equipo de Hola que aloja SQL Server.
* No necesitaría ningún tipo de instrucción Transact-SQL para **CREATE MASTER KEY** y **CREATE CREDENTIAL**.
* Hola **CREATE EVENT SESSION** instrucción, en su **ADD TARGET** cláusula, podría reemplazar el valor de Http de hello asignado realizado demasiado**filename =** con una cadena de ruta de acceso completa como  **C:\myfile.xel**.
  
  * No es necesario utilizar ninguna cuenta de Almacenamiento de Azure.

## <a name="more-information"></a>Más información

Para obtener más información acerca de las cuentas y los contenedores de hello servicio de almacenamiento de Azure, vea:

* [¿Cómo toouse almacenamiento de blobs en .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [Asignar nombres y hacer referencia a contenedores, blobs y metadatos](http://msdn.microsoft.com/library/azure/dd135715.aspx)
* [Trabajar con hello contenedor raíz](http://msdn.microsoft.com/library/azure/ee395424.aspx)
* [Lección 1: Crear una directiva de acceso almacenada y una firma de acceso compartido en un contenedor de Azure](http://msdn.microsoft.com/library/dn466430.aspx)
  * [Lección 2: Crear una credencial de SQL Server con una firma de acceso compartido](http://msdn.microsoft.com/library/dn466435.aspx)

<!--
Image references.
-->

[30_powershell_ise]: ./media/sql-database-xevent-code-event-file/event-file-powershell-ise-b30.png

