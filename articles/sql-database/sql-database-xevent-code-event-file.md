---
title: "Código de archivo de evento de XEvent para SQL Database | Microsoft Docs"
description: "Brinda PowerShell y Transact-SQL para un ejemplo de código de dos fases que muestra el destino de archivo de evento en un evento extendido en Base de datos SQL de Azure. Almacenamiento de Azure es una parte necesaria en este escenario."
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
ms.openlocfilehash: e8c7a9af11ac4c22be00426337ab7c8b8ff0860f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="event-file-target-code-for-extended-events-in-sql-database"></a><span data-ttu-id="f6e6f-104">Código de destino del archivo de evento para eventos extendidos en Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="f6e6f-104">Event File target code for extended events in SQL Database</span></span>

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="f6e6f-105">Desea tener un ejemplo de código completo de una manera eficaz para capturar y notificar información de un evento extendido.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-105">You want a complete code sample for a robust way to capture and report information for an extended event.</span></span>

<span data-ttu-id="f6e6f-106">En Microsoft SQL Server, el [destino de archivo de evento](http://msdn.microsoft.com/library/ff878115.aspx) se usa para almacenar las salidas de evento en un archivo del disco duro local.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-106">In Microsoft SQL Server, the [Event File target](http://msdn.microsoft.com/library/ff878115.aspx) is used to store event outputs into a local hard drive file.</span></span> <span data-ttu-id="f6e6f-107">Sin embargo, esos archivos no están disponibles para Base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-107">But such files are not available to Azure SQL Database.</span></span> <span data-ttu-id="f6e6f-108">En su lugar, usamos el servicio de Almacenamiento de Azure para admitir el destino de archivo de evento.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-108">Instead we use the Azure Storage service to support the Event File target.</span></span>

<span data-ttu-id="f6e6f-109">En este tema se presenta un ejemplo de código de dos fases:</span><span class="sxs-lookup"><span data-stu-id="f6e6f-109">This topic presents a two-phase code sample:</span></span>

* <span data-ttu-id="f6e6f-110">PowerShell, para crear un contenedor de Almacenamiento de Azure en la nube.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-110">PowerShell, to create an Azure Storage container in the cloud.</span></span>
* <span data-ttu-id="f6e6f-111">Transact-SQL:</span><span class="sxs-lookup"><span data-stu-id="f6e6f-111">Transact-SQL:</span></span>
  
  * <span data-ttu-id="f6e6f-112">Para asignar el contenedor de Almacenamiento de Azure a un destino de archivo de evento.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-112">To assign the Azure Storage container to an Event File target.</span></span>
  * <span data-ttu-id="f6e6f-113">Para crear e iniciar la sesión del evento, etc.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-113">To create and start the event session, and so on.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6e6f-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f6e6f-114">Prerequisites</span></span>

* <span data-ttu-id="f6e6f-115">Una cuenta y una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-115">An Azure account and subscription.</span></span> <span data-ttu-id="f6e6f-116">Puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f6e6f-116">You can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f6e6f-117">Cualquier base de datos donde pueda crear una tabla.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-117">Any database you can create a table in.</span></span>
  
  * <span data-ttu-id="f6e6f-118">De manera opcional, puede [crear una base de datos de **AdventureWorksLT** de demostración](sql-database-get-started.md) en cuestión de minutos.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-118">Optionally you can [create an **AdventureWorksLT** demonstration database](sql-database-get-started.md) in minutes.</span></span>
* <span data-ttu-id="f6e6f-119">SQL Server Management Studio (ssms.exe), idealmente la versión de actualización mensual más reciente.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-119">SQL Server Management Studio (ssms.exe), ideally its latest monthly update version.</span></span> 
  <span data-ttu-id="f6e6f-120">Puede descargar la versión más reciente de ssms.exe desde:</span><span class="sxs-lookup"><span data-stu-id="f6e6f-120">You can download the latest ssms.exe from:</span></span>
  
  * <span data-ttu-id="f6e6f-121">El tema titulado [Descarga de SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="f6e6f-121">Topic titled [Download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>
  * [<span data-ttu-id="f6e6f-122">Un vínculo directo a la descarga.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-122">A direct link to the download.</span></span>](http://go.microsoft.com/fwlink/?linkid=616025)
* <span data-ttu-id="f6e6f-123">Debe tener instalados los [módulos de Azure PowerShell](http://go.microsoft.com/?linkid=9811175) .</span><span class="sxs-lookup"><span data-stu-id="f6e6f-123">You must have the [Azure PowerShell modules](http://go.microsoft.com/?linkid=9811175) installed.</span></span>
  
  * <span data-ttu-id="f6e6f-124">Los módulos brindan comandos como - **New-AzureStorageAccount**.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-124">The modules provide commands such as - **New-AzureStorageAccount**.</span></span>

## <a name="phase-1-powershell-code-for-azure-storage-container"></a><span data-ttu-id="f6e6f-125">Fase 1: código de PowerShell para el contenedor de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="f6e6f-125">Phase 1: PowerShell code for Azure Storage container</span></span>

<span data-ttu-id="f6e6f-126">Esta es la fase 1 del ejemplo de código de dos fases.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-126">This PowerShell is phase 1 of the two-phase code sample.</span></span>

<span data-ttu-id="f6e6f-127">El script comienza con comandos que realizan una limpieza después de una posible ejecución anterior y se puede volver a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-127">The script starts with commands to clean up after a possible previous run, and is rerunnable.</span></span>

1. <span data-ttu-id="f6e6f-128">Pegue el script de PowerShell en un editor de texto simple, como Notepad.exe, y guárdelo como archivo con extensión **.ps1**.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-128">Paste the PowerShell script into a simple text editor such as Notepad.exe, and save the script as a file with the extension **.ps1**.</span></span>
2. <span data-ttu-id="f6e6f-129">Inicie PowerShell ISE como administrador.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-129">Start PowerShell ISE as an Administrator.</span></span>
3. <span data-ttu-id="f6e6f-130">En el símbolo del sistema, escriba</span><span class="sxs-lookup"><span data-stu-id="f6e6f-130">At the prompt, type</span></span><br/>`Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser`<br/><span data-ttu-id="f6e6f-131">y, luego, presione Entrar.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-131">and then press Enter.</span></span>
4. <span data-ttu-id="f6e6f-132">En PowerShell ISE, abra el archivo **.ps1** .</span><span class="sxs-lookup"><span data-stu-id="f6e6f-132">In PowerShell ISE, open your **.ps1** file.</span></span> <span data-ttu-id="f6e6f-133">Ejecute el script.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-133">Run the script.</span></span>
5. <span data-ttu-id="f6e6f-134">El script primero inicia una ventana nueva donde se inicia sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-134">The script first starts a new window in which you log in to Azure.</span></span>
   
   * <span data-ttu-id="f6e6f-135">Si vuelve a ejecutar el script sin interrumpir la sesión, tiene la opción conveniente de marcar el comando **Add-AzureAccount** como comentario.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-135">If you rerun the script without disrupting your session, you have the convenient option of commenting out the **Add-AzureAccount** command.</span></span>

![PowerShell ISE, con el módulo de Azure instalado, está preparado para ejecutar el script.][30_powershell_ise]


### <a name="powershell-code"></a><span data-ttu-id="f6e6f-137">Código de PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6e6f-137">PowerShell code</span></span>

```powershell
## TODO: Before running, find all 'TODO' and make each edit!!

#--------------- 1 -----------------------


# You can comment out or skip this Add-AzureAccount
# command after the first run.
# Current PowerShell environment retains the successful outcome.

'Expect a pop-up window in which you log in to Azure.'


Add-AzureAccount

#-------------- 2 ------------------------


'
TODO: Edit the values assigned to these variables, especially the first few!
'

# Ensure the current date is between
# the Expiry and Start time values that you edit here.

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


# The ending display lists your Azure subscriptions.
# One should match the $subscriptionName value you assigned
#   earlier in this PowerShell script. 

'Choose an existing subscription for the current PowerShell environment.'


Select-AzureSubscription -SubscriptionName $subscriptionName


#-------------- 4 ------------------------


'
Clean up the old Azure Storage Account after any previous run, 
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
Get the primary access key for your storage account.
'


$primaryAccessKey_ForStorageAccount = `
    (Get-AzureStorageKey `
        -StorageAccountName $storageAccountName).Primary

"`$primaryAccessKey_ForStorageAccount = $primaryAccessKey_ForStorageAccount"

'Azure Storage Account cmdlet completed.
Remainder of PowerShell .ps1 script continues.
'

#--------------- 6 -----------------------


# The context will be needed to create a container within the storage account.

'Create a context object from the storage account and its primary access key.
'

$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey  $primaryAccessKey_ForStorageAccount


'Create a container within the storage account.
'


$containerObjectInStorageAccount = New-AzureStorageContainer `
    -Name    $containerName `
    -Context $context


'Create a security policy to be applied to the SAS token.
'

New-AzureStorageContainerStoredAccessPolicy `
    -Container  $containerName `
    -Context    $context `
    -Policy     $policySasToken `
    -Permission $policySasPermission `
    -ExpiryTime $policySasExpiryTime `
    -StartTime  $policySasStartTime 

'
Generate a SAS token for the container.
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


'Display the values that YOU must edit into the Transact-SQL script next!:
'

"storageAccountName: $storageAccountName"
"containerName:      $containerName"
"sasTokenWithPolicy: $sasTokenWithPolicy"

'
REMINDER: sasTokenWithPolicy here might start with "?" character, which you must exclude from Transact-SQL.
'

'
(Later, return here to delete your Azure Storage account. See the preceding - Remove-AzureStorageAccount -StorageAccountName $storageAccountName)'

'
Now shift to the Transact-SQL portion of the two-part code sample!'

# EOFile
```


<span data-ttu-id="f6e6f-138">Anote los valores con nombre que el script de PowerShell imprime cuando finaliza.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-138">Take note of the few named values that the PowerShell script prints when it ends.</span></span> <span data-ttu-id="f6e6f-139">Debe editar esos valores en el script de Transact-SQL que sigue en la fase 2.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-139">You must edit those values into the Transact-SQL script that follows as phase 2.</span></span>

## <a name="phase-2-transact-sql-code-that-uses-azure-storage-container"></a><span data-ttu-id="f6e6f-140">Fase 2: código de Transact-SQL que usa el contenedor de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="f6e6f-140">Phase 2: Transact-SQL code that uses Azure Storage container</span></span>

* <span data-ttu-id="f6e6f-141">En la fase 1 de este ejemplo de código, ejecutó un script de PowerShell para crear un contenedor de Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-141">In phase 1 of this code sample, you ran a PowerShell script to create an Azure Storage container.</span></span>
* <span data-ttu-id="f6e6f-142">A continuación, en la fase 2, el siguiente script de Transact-SQL debe usar el contenedor.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-142">Next in phase 2, the following Transact-SQL script must use the container.</span></span>

<span data-ttu-id="f6e6f-143">El script comienza con comandos que realizan una limpieza después de una posible ejecución anterior y se puede volver a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-143">The script starts with commands to clean up after a possible previous run, and is rerunnable.</span></span>

<span data-ttu-id="f6e6f-144">El script de PowerShell imprimió algunos valores con nombre cuando finalizó.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-144">The PowerShell script printed a few named values when it ended.</span></span> <span data-ttu-id="f6e6f-145">Debe editar el script de Transact-SQL para que use esos valores.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-145">You must edit the Transact-SQL script to use those values.</span></span> <span data-ttu-id="f6e6f-146">Busque **TODO** en el script de Transact-SQL para ubicar los puntos de edición.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-146">Find **TODO** in the Transact-SQL script to locate the edit points.</span></span>

1. <span data-ttu-id="f6e6f-147">Abra SQL Server Management Studio (ssms.exe).</span><span class="sxs-lookup"><span data-stu-id="f6e6f-147">Open SQL Server Management Studio (ssms.exe).</span></span>
2. <span data-ttu-id="f6e6f-148">Conéctese a la base de datos de Base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-148">Connect to your Azure SQL Database database.</span></span>
3. <span data-ttu-id="f6e6f-149">Haga clic para abrir un nuevo panel de consulta.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-149">Click to open a new query pane.</span></span>
4. <span data-ttu-id="f6e6f-150">Pegue el siguiente script de Transact-SQL en el panel de consulta.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-150">Paste the following Transact-SQL script into the query pane.</span></span>
5. <span data-ttu-id="f6e6f-151">Busque cada **TODO** en el script y haga las ediciones correspondientes.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-151">Find every **TODO** in the script and make the appropriate edits.</span></span>
6. <span data-ttu-id="f6e6f-152">Guarde y, luego, ejecute el script.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-152">Save, and then run the script.</span></span>


> [!WARNING]
> <span data-ttu-id="f6e6f-153">El valor de clave SAS generado con el script de PowerShell anterior podría comenzar con un carácter "?" (signo de interrogación).</span><span class="sxs-lookup"><span data-stu-id="f6e6f-153">The SAS key value generated by the preceding PowerShell script might begin with a '?' (question mark).</span></span> <span data-ttu-id="f6e6f-154">Al utilizar la clave SAS en el siguiente script de T-SQL, debe *quitar el carácter "?" inicial*.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-154">When you use the SAS key in the following T-SQL script, you must *remove the leading '?'*.</span></span> <span data-ttu-id="f6e6f-155">De lo contrario, podrían bloquearse su trabajo por motivos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-155">Otherwise your efforts might be blocked by security.</span></span>


### <a name="transact-sql-code"></a><span data-ttu-id="f6e6f-156">Código Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="f6e6f-156">Transact-SQL code</span></span>

```sql
---- TODO: First, run the PowerShell portion of this two-part code sample.
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
        -- TODO: Assign AzureStorageAccount name, and the associated Container name.
        WHERE name = 'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent')
BEGIN
    DROP DATABASE SCOPED CREDENTIAL
        -- TODO: Assign AzureStorageAccount name, and the associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent] ;
END
GO


CREATE
    DATABASE SCOPED
    CREDENTIAL
        -- use '.blob.',   and not '.queue.' or '.table.' etc.
        -- TODO: Assign AzureStorageAccount name, and the associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    WITH
        IDENTITY = 'SHARED ACCESS SIGNATURE',  -- "SAS" token.
        -- TODO: Paste in the long SasToken string here for Secret, but exclude any leading '?'.
        SECRET = 'sv=2014-02-14&sr=c&si=gmpolicysastoken&sig=EjAqjo6Nu5xMLEZEkMkLbeF7TD9v1J8DNB2t8gOKTts%3D'
    ;
GO


------  Step 3.  Create (define) an event session.  --------
------  The event session has an event with an action,
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
            -- TODO: Assign AzureStorageAccount name, and the associated Container name.
            -- Also, tweak the .xel file name at end, if you like.
            SET filename =
                'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent/anyfilenamexel242b.xel'
            )
    WITH
        (MAX_MEMORY = 10 MB,
        MAX_DISPATCH_LATENCY = 3 SECONDS)
    ;
GO


------  Step 4.  Start the event session.  ----------------
------  Issue the SQL Update statements that will be traced.
------  Then stop the session.

------  Note: If the target fails to attach,
------  the session must be stopped and restarted.

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


-------------- Step 5.  Select the results. ----------

SELECT
        *, 'CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS!' as [CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS],
        CAST(event_data AS XML) AS [event_data_XML]  -- TODO: In ssms.exe results grid, double-click this cell!
    FROM
        sys.fn_xe_file_target_read_file
            (
                -- TODO: Fill in Storage Account name, and the associated Container name.
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
    -- TODO: Assign AzureStorageAccount name, and the associated Container name.
    [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    ;
GO

DROP TABLE gmTabEmployee;
GO

PRINT 'Use PowerShell Remove-AzureStorageAccount to delete your Azure Storage account!';
GO
```


<span data-ttu-id="f6e6f-157">Si el destino no se adjunta cuando ejecuta el script, debe detener la sesión de evento y reiniciarla:</span><span class="sxs-lookup"><span data-stu-id="f6e6f-157">If the target fails to attach when you run, you must stop and restart the event session:</span></span>

```sql
ALTER EVENT SESSION ... STATE = STOP;
GO
ALTER EVENT SESSION ... STATE = START;
GO
```


## <a name="output"></a><span data-ttu-id="f6e6f-158">Salida</span><span class="sxs-lookup"><span data-stu-id="f6e6f-158">Output</span></span>

<span data-ttu-id="f6e6f-159">Cuando se complete el script de Transact-SQL, haga clic en una celda bajo el encabezado de la columna **event_data_XML**.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-159">When the Transact-SQL script completes, click a cell under the **event_data_XML** column header.</span></span> <span data-ttu-id="f6e6f-160">Aparece un elemento **<event>** que muestra una instrucción UPDATE.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-160">One **<event>** element is displayed which shows one UPDATE statement.</span></span>

<span data-ttu-id="f6e6f-161">Este es un elemento **<event>** que se generó durante la prueba:</span><span class="sxs-lookup"><span data-stu-id="f6e6f-161">Here is one **<event>** element that was generated during testing:</span></span>


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


<span data-ttu-id="f6e6f-162">El script Transact-SQL anterior utiliza la siguiente función de sistema para leer el archivo event_file:</span><span class="sxs-lookup"><span data-stu-id="f6e6f-162">The preceding Transact-SQL script used the following system function to read the event_file:</span></span>

* [<span data-ttu-id="f6e6f-163">sys.fn_xe_file_target_read_file (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="f6e6f-163">sys.fn_xe_file_target_read_file (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/cc280743.aspx)

<span data-ttu-id="f6e6f-164">En la siguiente página encontrará una explicación de las opciones avanzadas de la visualización de datos de eventos extendidos:</span><span class="sxs-lookup"><span data-stu-id="f6e6f-164">An explanation of advanced options for the viewing of data from extended events is available at:</span></span>

* [<span data-ttu-id="f6e6f-165">Advanced Viewing of Target Data from Extended Events (Visualización avanzada de datos de destino de eventos extendidos)</span><span class="sxs-lookup"><span data-stu-id="f6e6f-165">Advanced Viewing of Target Data from Extended Events</span></span>](http://msdn.microsoft.com/library/mt752502.aspx)


## <a name="converting-the-code-sample-to-run-on-sql-server"></a><span data-ttu-id="f6e6f-166">Conversión del ejemplo de código para ejecutarlo en SQL Server</span><span class="sxs-lookup"><span data-stu-id="f6e6f-166">Converting the code sample to run on SQL Server</span></span>

<span data-ttu-id="f6e6f-167">Suponga que desea ejecutar el ejemplo de Transact-SQL anterior en Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-167">Suppose you wanted to run the preceding Transact-SQL sample on Microsoft SQL Server.</span></span>

* <span data-ttu-id="f6e6f-168">Para mantener la simplicidad, desearía reemplazar completamente el uso del contenedor de Azure Storage por un archivo simple como **C:\myeventdata.xel**.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-168">For simplicity, you would want to completely replace use of the Azure Storage container with a simple file such as **C:\myeventdata.xel**.</span></span> <span data-ttu-id="f6e6f-169">El archivo se escribiría en el disco duro local del equipo donde se hospeda SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-169">The file would be written to the local hard drive of the computer that hosts SQL Server.</span></span>
* <span data-ttu-id="f6e6f-170">No necesitaría ningún tipo de instrucción Transact-SQL para **CREATE MASTER KEY** y **CREATE CREDENTIAL**.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-170">You would not need any kind of Transact-SQL statements for **CREATE MASTER KEY** and **CREATE CREDENTIAL**.</span></span>
* <span data-ttu-id="f6e6f-171">En la instrucción **CREATE EVENT SESSION**, en su cláusula **ADD TARGET**, reemplazaría el valor Http asignado en **filename=** por una cadena de ruta de acceso completa como **C:\myfile.xel**.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-171">In the **CREATE EVENT SESSION** statement, in its **ADD TARGET** clause, you would replace the Http value assigned made to **filename=** with a full path string like **C:\myfile.xel**.</span></span>
  
  * <span data-ttu-id="f6e6f-172">No es necesario utilizar ninguna cuenta de Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="f6e6f-172">No Azure Storage account need be involved.</span></span>

## <a name="more-information"></a><span data-ttu-id="f6e6f-173">Más información</span><span class="sxs-lookup"><span data-stu-id="f6e6f-173">More information</span></span>

<span data-ttu-id="f6e6f-174">Si desea obtener más información sobre las cuentas y los contenedores del servicio de Almacenamiento de Azure, consulte:</span><span class="sxs-lookup"><span data-stu-id="f6e6f-174">For more info about accounts and containers in the Azure Storage service, see:</span></span>

* [<span data-ttu-id="f6e6f-175">Uso del almacenamiento de blobs de .NET</span><span class="sxs-lookup"><span data-stu-id="f6e6f-175">How to use Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="f6e6f-176">Asignar nombres y hacer referencia a contenedores, blobs y metadatos</span><span class="sxs-lookup"><span data-stu-id="f6e6f-176">Naming and Referencing Containers, Blobs, and Metadata</span></span>](http://msdn.microsoft.com/library/azure/dd135715.aspx)
* [<span data-ttu-id="f6e6f-177">Trabajar con el contenedor raíz</span><span class="sxs-lookup"><span data-stu-id="f6e6f-177">Working with the Root Container</span></span>](http://msdn.microsoft.com/library/azure/ee395424.aspx)
* [<span data-ttu-id="f6e6f-178">Lección 1: Crear una directiva de acceso almacenada y una firma de acceso compartido en un contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="f6e6f-178">Lesson 1: Create a stored access policy and a shared access signature on an Azure container</span></span>](http://msdn.microsoft.com/library/dn466430.aspx)
  * [<span data-ttu-id="f6e6f-179">Lección 2: Crear una credencial de SQL Server con una firma de acceso compartido</span><span class="sxs-lookup"><span data-stu-id="f6e6f-179">Lesson 2: Create a SQL Server credential using a shared access signature</span></span>](http://msdn.microsoft.com/library/dn466435.aspx)

<!--
Image references.
-->

[30_powershell_ise]: ./media/sql-database-xevent-code-event-file/event-file-powershell-ise-b30.png

