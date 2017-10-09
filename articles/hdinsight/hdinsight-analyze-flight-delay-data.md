---
title: datos de retrasos de vuelos aaaAnalyze con Hadoop en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse una Windows PowerShell script toocreate un clúster de HDInsight, ejecute un trabajo de Hive, ejecutar un trabajo de Sqoop y eliminar el clúster de Hola."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00e26aa9-82fb-4dbe-b87d-ffe8e39a5412
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 6ebaee65d9b270e5dc2141dd1265011d372f497d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-in-hdinsight"></a>Análisis de datos de retraso de vuelos con Hive en HDInsight
Hive ofrece un modo de ejecutar trabajos de MapReduce de Hadoop mediante un lenguaje de scripting de tipo SQL, denominado *[HiveQL][hadoop-hiveql]*, que se puede usar para resumir, consultar y analizar grandes volúmenes de datos.

> [!IMPORTANT]
> Hello pasos de este documento requieren un clúster de HDInsight basados en Windows. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Para conocer el procedimiento que funciona con un clúster basado en Linux, vea [Análisis de datos de retraso de vuelos con Hive en HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md)

Una de las principales ventajas de Hola de HDInsight de Azure es la separación de Hola de almacenamiento de datos y el cálculo. HDInsight usa el almacenamiento de blobs de Azure para almacenar datos. Un trabajo típico implica tres partes:

1. **Almacenar los datos en el almacenamiento de blobs de Azure.**  Por ejemplo, los datos meteorológicos, datos de sensores, registros web y, en este caso, datos de retraso de vuelos se guardan en el almacenamiento de blobs de Azure.
2. **Ejecutar trabajos.** Cuando se trata de datos en tiempo de tooprocess hello, ejecutar un script de Windows PowerShell (o una aplicación cliente) toocreate un clúster de HDInsight, ejecutar trabajos y eliminar el clúster de Hola. trabajos de Hello guardar datos de salida tooAzure almacenamiento de blobs. datos de salida de Hello se conservan incluso después de que se elimina el clúster de Hola. De este modo, solo paga por lo que ha consumido.
3. **Recuperar la salida de hello desde el almacenamiento de blobs de Azure**, o en este tutorial, exportar base de datos de SQL Azure de hello datos tooan.

Hello siguiente diagrama ilustra el escenario de Hola y la estructura de Hola de este tutorial:

![HDI.FlightDelays.flow][img-hdi-flightdelays-flow]

Tenga en cuenta que los números de hello en el diagrama de hello corresponden toohello títulos de sección. **M** hace referencia al proceso principal Hola. **Un** hace referencia al contenido de hello en el apéndice de hello.

parte principal de Hola de tutorial de hello muestra cómo toouse una Windows PowerShell script tooperform Hola siguientes tareas:

* Cree un clúster de HDInsight.
* Ejecutar un trabajo de Hive en retrasos promedio de hello clúster toocalculate en aeropuertos. datos de retrasos de vuelos de Hola se almacenan en una cuenta de almacenamiento de blobs de Azure.
* Ejecute Sqoop trabajo tooexport Hola Hive trabajo salida tooan Azure base de datos SQL.
* Eliminar el clúster de HDInsight de Hola.

Apéndices hello, encontrará instrucciones de Hola para cargar datos de retrasos de vuelos, crear o cargar una cadena de consulta de Hive y preparar la base de datos de SQL Azure de hello para el trabajo de Sqoop Hola.

> [!NOTE]
> pasos de Hello en este documento son los clústeres de HDInsight de tooWindows-based específicos. Para conocer el procedimiento que funciona con un clúster basado en Linux, vea [Análisis de datos de retraso de vuelos con Hive en HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md)

### <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este tutorial, debe tener Hola siguientes elementos:

* **Una suscripción de Azure**. Consulte [Obtención de una versión de evaluación gratuita](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Una estación de trabajo con Azure PowerShell**.

    > [!IMPORTANT]
    > La compatibilidad con Azure PowerShell para administrar recursos de HDInsight mediante Azure Service Manager está **en desuso** y dejó de estar disponible por completo el 1 de enero de 2017. Hola pasos de este documento use Hola nuevos cmdlets de HDInsight que funcionan con el Administrador de recursos de Azure.
    >
    > Siga los pasos de hello en [instalar y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs) versión más reciente de hello tooinstall de PowerShell de Azure. Si tiene scripts de ese toobe necesidad de modifica toouse Hola nuevos cmdlets que funcionan con el Administrador de recursos de Azure, consulte [tooAzure desarrollo basado en el Administrador de recursos de migración de las herramientas de clústeres de HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) para obtener más información.

**Archivos usados en este tutorial**

Este tutorial usa hello en rendimiento de datos de vuelo airline de [investigación y administración de tecnología innovadora, centro de estadísticas de transporte o RITA][rita-website].
Una copia del programa Hola a datos ha sido cargado tooan contenedor de almacenamiento de blobs de Azure con permiso de acceso de Blob público Hola.
Una parte de la secuencia de comandos de PowerShell copia datos de Hola de contenedor de blobs de predeterminado toohello contenedor de blob público Hola del clúster. Hola HiveQL script también está copia toohello mismo contenedor de Blob.
Si desea que toolearn cómo tooget/cargar Hola datos tooyour posee cuenta de almacenamiento y cómo toocreate/cargar hello HiveQL script archivo, consulte [Apéndice A](#appendix-a) y [Apéndice B](#appendix-b).

Hello siguiente tabla enumeran Hola archivos utilizados en este tutorial:

<table border="1">
<tr><th>Archivos</th><th>Descripción</th></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/flightdelays.hql</td><td>archivo de script de HiveQL Hello usa Hola trabajo de Hive. Esta secuencia de comandos ha sido cargado tooan cuenta de almacenamiento de blobs de Azure con acceso público de Hola. <a href="#appendix-b">Apéndice B</a> contiene instrucciones sobre la preparación y carga de esta cuenta de almacenamiento de blobs de Azure propia de archivo tooyour.</td></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data</td><td>Datos de entrada para el trabajo de Hive Hola. datos de Hello ha sido cargado tooan cuenta de almacenamiento de blobs de Azure con acceso público de Hola. <a href="#appendix-a">Apéndice a:</a> contiene instrucciones sobre obtención de datos de Hola y cargar la cuenta de almacenamiento de hello datos tooyour propio Blob de Azure.</td></tr>
<tr><td>\tutorials\flightdelays\output</td><td>ruta de acceso de salida de Hello para el trabajo de Hive Hola. contenedor de Hello predeterminado se utiliza para almacenar los datos de salida de hello.</td></tr>
<tr><td>\tutorials\flightdelays\jobstatus</td><td>carpeta de estado del trabajo de Hive Hello en contenedor predeterminado de Hola.</td></tr>
</table>

## <a name="create-cluster-and-run-hivesqoop-jobs"></a>Creación de clústeres y ejecución de trabajos de Hive/Sqoop
Hadoop MapReduce se está procesando por lotes. Hello toorun mayoría de forma eficaz un trabajo de Hive es toocreate un clúster para el trabajo de Hola y eliminar el trabajo de hello después de que se complete el trabajo de Hola. Hello secuencia de comandos siguiente cubre todo proceso de Hola.
Para obtener más información sobre la creación de un clúster de HDInsight y la ejecución de trabajos de Hive, consulte [Creación de clústeres de Hadoop en HDInsight][hdinsight-provision] y [Uso de Hive con HDInsight][hdinsight-use-hive].

**consultas de Hive de hello toorun PowerShell de Azure**

1. Cree una tabla de hello y base de datos de SQL Azure para la salida de trabajo de Sqoop Hola siguiendo las instrucciones de hello en [Apéndice C](#appendix-c).
2. Abra Windows PowerShell ISE y ejecute hello siguiente secuencia de comandos:

    ```powershell
    $subscriptionID = "<Azure Subscription ID>"
    $nameToken = "<Enter an Alias>"

    ###########################################
    # You must configure hello follwing variables
    # for an existing Azure SQL Database
    ###########################################
    $existingSqlDatabaseServerName = "<Azure SQL Database Server>"
    $existingSqlDatabaseLogin = "<Azure SQL Database Server Login>"
    $existingSqlDatabasePassword = "<Azure SQL Database Server login password>"
    $existingSqlDatabaseName = "<Azure SQL Database name>"

    $localFolder = "E:\Tutorials\Downloads\" # A temp location for copying files.
    $azcopyPath = "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy" # depends on hello version, hello folder can be different

    ###########################################
    # (Optional) configure hello following variables
    ###########################################

    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2"

    $HDInsightClusterName = $namePrefix + "hdi"
    $httpUserName = "admin"
    $httpPassword = "<Enter hello Password>"

    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $HDInsightClusterName # use hello cluster name

    $existingSqlDatabaseTableName = "AvgDelays"
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$existingSqlDatabaseServerName.database.windows.net;user=$existingSqlDatabaseLogin@$existingSqlDatabaseServerName;password=$existingSqlDatabaseLogin;database=$existingSqlDatabaseName"

    $hqlScriptFile = "/tutorials/flightdelays/flightdelays.hql"

    $jobStatusFolder = "/tutorials/flightdelays/jobstatus"

    ###########################################
    # Login
    ###########################################
    try{
        $acct = Get-AzureRmSubscription
    }
    catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionID $subscriptionID

    ###########################################
    # Create a new HDInsight cluster
    ###########################################

    # Create ARM group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create hello default storage account
    New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName -Location $location -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer -Name $defaultBlobContainerName -Context $defaultStorageAccountContext

    # Create hello HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $existingDefaultBlobContainerName

    ###########################################
    # Prepare hello HiveQL script and source data
    ###########################################

    # Create hello temp location
    New-Item -Path $localFolder -ItemType Directory -Force

    # Download hello sample file from Azure Blob storage
    $context = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous
    $blobs = Get-AzureStorageBlob -Container "flightdelay" -Context $context
    #$blobs | Get-AzureStorageBlobContent -Context $context -Destination $localFolder

    # Upload data toodefault container

    $azcopycmd = "cmd.exe /C '$azcopyPath\azcopy.exe' /S /Source:'$localFolder' /Dest:'https://$defaultStorageAccountName.blob.core.windows.net/$defaultBlobContainerName/tutorials/flightdelays' /DestKey:$defaultStorageAccountKey"

    Invoke-Expression -Command:$azcopycmd

    ###########################################
    # Submit hello Hive job
    ###########################################
    Use-AzureRmHDInsightCluster -ClusterName $HDInsightClusterName -HttpCredential $httpCredential
    $response = Invoke-AzureRmHDInsightHiveJob `
                    -Files $hqlScriptFile `
                    -DefaultContainer $defaultBlobContainerName `
                    -DefaultStorageAccountName $defaultStorageAccountName `
                    -DefaultStorageAccountKey $defaultStorageAccountKey `
                    -StatusFolder $jobStatusFolder

    write-Host $response

    ###########################################
    # Submit hello Sqoop job
    ###########################################
    $exportDir = "wasb://$defaultBlobContainerName@$defaultStorageAccountName.blob.core.windows.net/tutorials/flightdelays/output"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
                    -Command "export --connect $sqlDatabaseConnectionString --table $sqlDatabaseTableName --export-dir $exportDir --fields-terminated-by \001 "
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ResourceGroupName $resourceGroupName `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -HttpCredential $httpCredential `
        -WaitTimeoutInSeconds 3600 `
        -Job $sqoopJob.JobId

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -DefaultContainer $existingDefaultBlobContainerName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    ###########################################
    # Delete hello cluster
    ###########################################
    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName
    ```
3. Conectar la base de datos SQL tooyour y vea retrasos de vuelos promedio por ciudad en la tabla de Hola AvgDelays:

    ![HDI.FlightDelays.AvgDelays.Dataset][image-hdi-flightdelays-avgdelays-dataset]

- - -

## <a id="appendix-a"></a>Apéndice A - carga vuelo retraso datos tooAzure almacenamiento de blobs
Cargar archivo de datos de hello y los archivos de script de HiveQL Hola (vea [Apéndice B](#appendix-b)) requiere cierta planeación. idea de Hello es archivos de datos de toostore hello y archivo de HiveQL hello antes de crear un clúster de HDInsight y ejecutar el trabajo de Hive Hola. Tiene dos opciones:

* **Use Hola misma cuenta de almacenamiento de Azure que se usará por clúster de HDInsight de hello como sistema de archivos predeterminado de Hola.** Porque clúster de HDInsight de hello disponen de tecla de acceso de cuenta de almacenamiento de hello, no es necesario toomake ningún cambio adicional.
* **Usar una cuenta de almacenamiento de Azure diferente de hello sistema de archivos de predeterminado de clúster de HDInsight.** Si éste es el caso de hello, debe modificar la parte de la creación de hello de hello Windows PowerShell script se encuentra en [HDInsight crear clúster y ejecución de los trabajos de Hive y Sqoop](#runjob) toolink Hola cuenta de almacenamiento como una cuenta de almacenamiento adicional. Para instrucciones, vea [Creación de clústeres de Hadoop en HDInsight][hdinsight-provision]. clúster de HDInsight de Hello, a continuación, conoce la clave de acceso de Hola para hello cuenta de almacenamiento.

> [!NOTE]
> Hola ruta de acceso de almacenamiento de blobs para hello archivo de datos está codificado en el archivo de script de HiveQL Hola. Debe actualizarse en consecuencia.

**datos del vuelo hello toodownload**

1. Examinar demasiado[investigación y administración de tecnología innovadora, centro de transporte estadísticas][rita-website].
2. En página de hello, seleccione Hola siguientes valores:

    <table border="1">
    <tr><th>Nombre</th><th>Valor</th></tr>
    <tr><td>Filter Year</td><td>2013 </td></tr>
    <tr><td>Filter Period</td><td>January</td></tr>
    <tr><td>Fields</td><td>*Year*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *Origin*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (borrar todos los demás campos)</td></tr>
    </table>
3. Haga clic en **Descargar**.
4. Descomprima Hola archivo toohello **C:\Tutorials\FlightDelay\2013Data** carpeta. Cada archivo es un archivo CSV y tiene un tamaño aproximado de 60 GB.
5. Cambiar el nombre de toohello de archivo de hello del mes de Hola que contiene datos de. Por ejemplo, archivo de Hola que contiene datos de enero de saludo se denominará *January.csv*.
6. Repita toodownload un archivo de los pasos 2 y 5 para cada uno de hello 12 meses de 2013. Necesitará un mínimo de un tutorial de hello toorun de archivo.

**tooupload Hola vuelo retraso datos tooAzure almacenamiento de blobs**

1. Preparar los parámetros de hello:

    <table border="1">
    <tr><th>Nombre de la variable</th><th>Notas</th></tr>
    <tr><td>$storageAccountName</td><td>Hola donde desea que los datos de Hola de tooupload de cuenta de almacenamiento de Azure.</td></tr>
    <tr><td>$blobContainerName</td><td>Hola donde desea tooupload Hola datos para el contenedor de blobs.</td></tr>
    </table>
2. Abra Azure PowerShell ISE.
3. Pegue Hola siguiente secuencia de comandos en el panel de scripts de hello:

    ```powershell
    [CmdletBinding()]
    Param(

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #Region - Variables
    $localFolder = "C:\Tutorials\FlightDelay\2013Data"  # hello source folder
    $destFolder = "tutorials/flightdelay/2013data"     #hello blob name prefix for hello files toobe uploaded
    #EndRegion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #Region - Copy hello file from local workstation tooAzure Blob storage
    if (test-path -Path $localFolder)
    {
        foreach ($item in Get-ChildItem -Path $localFolder){
            $fileName = "$localFolder\$item"
            $blobName = "$destFolder/$item"

            Write-Host "Copying $fileName too$blobName" -ForegroundColor Green

            Set-AzureStorageBlobContent -File $fileName -Container $blobContainerName -Blob $blobName -Context $storageContext
        }
    }
    else
    {
        Write-Host "hello source folder on hello workstation doesn't exist" -ForegroundColor Red
    }

    # List hello uploaded files on HDInsight
    Get-AzureStorageBlob -Container $blobContainerName  -Context $storageContext -Prefix $destFolder
    #EndRegion
    ```
4. Presione **F5** secuencia de comandos de toorun Hola.

Si elige un método diferente para cargar archivos de hello toouse, asegúrese de ruta de acceso de archivo de hello es tutoriales/flightdelay/datos. sintaxis de Hello para tener acceso a archivos de hello es:

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/tutorials/flightdelay/data

ruta de acceso de Hello tutoriales/flightdelay/datos es carpeta virtual de hello creado al cargar archivos de Hola. Compruebe que haya 12 archivos, uno para cada mes.

> [!NOTE]
> Debe actualizar tooread de consulta de Hive Hola desde nueva ubicación de Hola.
>
> Debe configurar Hola contenedor acceso permiso toobe público o enlazar toohello cuenta de almacenamiento Hola clúster de HDInsight. En caso contrario, la cadena de consulta de Hive de Hola no estará tooaccess capaz de archivos de datos de Hola.

- - -

## <a id="appendix-b"></a>Apéndice B: Creación y carga de un script de HiveQL
Uso de PowerShell de Azure, puede ejecutar varias instrucciones de HiveQL uno a una hora u Hola paquete HiveQL instrucción en un archivo de script. Esta sección muestra cómo toocreate un script de HiveQL Hola de carga de script y el almacenamiento de blobs de tooAzure mediante Azure PowerShell. Subárbol requiere hello HiveQL scripts toobe almacenado en el almacenamiento de blobs de Azure.

Hola script de HiveQL llevará a cabo siguiente hello:

1. **Quitar tabla de hello delays_raw**, en caso de hello tabla ya existe.
2. **Crear tabla de Hive externo de hello delays_raw** que apuntan toohello ubicación de almacenamiento de blobs con archivos de retraso de vuelos de Hola. Esta consulta especifica que los campos están delimitados por "," y que las líneas terminan en "\n". Esto supone un problema cuando los valores de campo contienen comas porque Hive no puede diferenciar entre una coma que es un delimitador de campo y otra que forma parte de un valor de campo (que es el caso de hello en valores de campo de origen\_CITY\_nombre y DEST\_ Ciudad\_nombre). tooaddress, Hola consulta crea columnas TEMP datos toohold incorrectamente se división en las columnas.
3. **Quitar tabla de retrasos de hello**, en caso de hello tabla ya existe.
4. **Crear tabla de retrasos de hello**. Resulta útil tooclean los datos de hello antes de su posterior procesamiento. Esta consulta crea una nueva tabla, *retrasos*, de tabla de delays_raw Hola. Tenga en cuenta que no se copian las columnas TEMP de hello (como se mencionó anteriormente) y ese hello **subcadena** función es tooremove utilizado comillas de datos de Hola.
5. **Proceso Hola tiempo promedio retraso y grupos Hola los resultados por nombre de ciudad.** También dará como resultado el almacenamiento de información de hello resultados tooBlob. Tenga en cuenta esa consulta Hola quitará apóstrofos de datos de Hola y excluirá filas donde valor hello **weather_delay** es null. Esto es necesario porque Sqoop, que se usa más adelante en este tutorial, no trata estos valores correctamente de forma predeterminada.

Para obtener una lista completa de comandos de HiveQL hello, consulte [lenguaje de definición de datos de Hive][hadoop-hiveql]. Cada comando de HiveQL debe terminar con un punto y coma.

**un archivo de script de HiveQL toocreate**

1. Preparar los parámetros de hello:

    <table border="1">
    <tr><th>Nombre de la variable</th><th>Notas</th></tr>
    <tr><td>$storageAccountName</td><td>Hola cuenta de almacenamiento de Azure donde desea tooupload hello HiveQL script.</td></tr>
    <tr><td>$blobContainerName</td><td>Hola donde desea que el script de HiveQL tooupload hello para el contenedor de blobs.</td></tr>
    </table>
2. Abra Azure PowerShell ISE.
3. Copie y pegue la siguiente secuencia de comandos en el panel de scripts de Hola de hello:

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Blob storage variables
        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #region - Define variables
    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    # hello HiveQL script file is exported as this file before it's uploaded tooBlob storage
    $hqlLocalFileName = "e:\tutorials\flightdelay\flightdelays.hql"

    # hello HiveQL script file will be uploaded tooBlob storage as this blob name
    $hqlBlobName = "tutorials/flightdelay/flightdelays.hql"

    # These two constants are used by hello HiveQL script file
    #$srcDataFolder = "tutorials/flightdelay/data"
    $dstDataFolder = "/tutorials/flightdelay/output"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #region - Validate hello file and file path

    # Check if a file with hello same file name already exists on hello workstation
    Write-Host "`nvalidating hello folder structure on hello workstation for saving hello HQL script file ..."  -ForegroundColor Green
    if (test-path $hqlLocalFileName){

        $isDelete = Read-Host 'hello file, ' $hqlLocalFileName ', exists.  Do you want toooverwirte it? (Y/N)'

        if ($isDelete.ToLower() -ne "y")
        {
            Exit
        }
    }

    # Create hello folder if it doesn't exist
    $folder = split-path $hqlLocalFileName
    if (-not (test-path $folder))
    {
        Write-Host "`nCreating folder, $folder ..." -ForegroundColor Green

        new-item $folder -ItemType directory
    }
    #end region

    #region - Write hello Hive script into a local file
    Write-Host "`nWriting hello Hive script into a file on your workstation ..." `
                -ForegroundColor Green

    $hqlDropDelaysRaw = "DROP TABLE delays_raw;"

    $hqlCreateDelaysRaw = "CREATE EXTERNAL TABLE delays_raw (" +
            "YEAR string, " +
            "FL_DATE string, " +
            "UNIQUE_CARRIER string, " +
            "CARRIER string, " +
            "FL_NUM string, " +
            "ORIGIN_AIRPORT_ID string, " +
            "ORIGIN string, " +
            "ORIGIN_CITY_NAME string, " +
            "ORIGIN_CITY_NAME_TEMP string, " +
            "ORIGIN_STATE_ABR string, " +
            "DEST_AIRPORT_ID string, " +
            "DEST string, " +
            "DEST_CITY_NAME string, " +
            "DEST_CITY_NAME_TEMP string, " +
            "DEST_STATE_ABR string, " +
            "DEP_DELAY_NEW float, " +
            "ARR_DELAY_NEW float, " +
            "CARRIER_DELAY float, " +
            "WEATHER_DELAY float, " +
            "NAS_DELAY float, " +
            "SECURITY_DELAY float, " +
            "LATE_AIRCRAFT_DELAY float) " +
        "ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' " +
        "LINES TERMINATED BY '\n' " +
        "STORED AS TEXTFILE " +
        "LOCATION 'wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data';"

    $hqlDropDelays = "DROP TABLE delays;"

    $hqlCreateDelays = "CREATE TABLE delays AS " +
        "SELECT YEAR AS year, " +
            "FL_DATE AS flight_date, " +
            "substring(UNIQUE_CARRIER, 2, length(UNIQUE_CARRIER) -1) AS unique_carrier, " +
            "substring(CARRIER, 2, length(CARRIER) -1) AS carrier, " +
            "substring(FL_NUM, 2, length(FL_NUM) -1) AS flight_num, " +
            "ORIGIN_AIRPORT_ID AS origin_airport_id, " +
            "substring(ORIGIN, 2, length(ORIGIN) -1) AS origin_airport_code, " +
            "substring(ORIGIN_CITY_NAME, 2) AS origin_city_name, " +
            "substring(ORIGIN_STATE_ABR, 2, length(ORIGIN_STATE_ABR) -1)  AS origin_state_abr, " +
            "DEST_AIRPORT_ID AS dest_airport_id, " +
            "substring(DEST, 2, length(DEST) -1) AS dest_airport_code, " +
            "substring(DEST_CITY_NAME,2) AS dest_city_name, " +
            "substring(DEST_STATE_ABR, 2, length(DEST_STATE_ABR) -1) AS dest_state_abr, " +
            "DEP_DELAY_NEW AS dep_delay_new, " +
            "ARR_DELAY_NEW AS arr_delay_new, " +
            "CARRIER_DELAY AS carrier_delay, " +
            "WEATHER_DELAY AS weather_delay, " +
            "NAS_DELAY AS nas_delay, " +
            "SECURITY_DELAY AS security_delay, " +
            "LATE_AIRCRAFT_DELAY AS late_aircraft_delay " +
        "FROM delays_raw;"

    $hqlInsertLocal = "INSERT OVERWRITE DIRECTORY '$dstDataFolder' " +
        "SELECT regexp_replace(origin_city_name, '''', ''), " +
            "avg(weather_delay) " +
        "FROM delays " +
        "WHERE weather_delay IS NOT NULL " +
        "GROUP BY origin_city_name;"

    $hqlScript = $hqlDropDelaysRaw + $hqlCreateDelaysRaw + $hqlDropDelays + $hqlCreateDelays + $hqlInsertLocal

    $hqlScript | Out-File $hqlLocalFileName -Encoding ascii -Force
    #endregion

    #region - Upload hello Hive script toohello default Blob container
    Write-Host "`nUploading hello Hive script toohello default Blob container ..." -ForegroundColor Green

    # Create a storage context object
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Upload hello file from local workstation tooBlob storage
    Set-AzureStorageBlobContent -File $hqlLocalFileName -Container $blobContainerName -Blob $hqlBlobName -Context $destContext
    #endregion

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

    Estas son las variables de hello utilizadas en el script de Hola:

   * **$hqlLocalFileName** -script de Hola guarda el archivo de script de Hola HiveQL localmente antes de cargarlo tooBlob almacenamiento. Éste es el nombre de archivo de Hola. es el valor predeterminado de Hello <u>C:\tutorials\flightdelay\flightdelays.hql</u>.
   * **$hqlBlobName** -se trata de hello HiveQL script blob nombre del archivo utilizado en hello almacenamiento de blobs de Azure. valor predeterminado de Hello es tutorials/flightdelay/flightdelays.hql. Dado que se escribirán archivo hello directamente tooAzure almacenamiento de blobs, no hay un "/" al principio de hello del nombre de blob de Hola. Si desea que el archivo de hello tooaccess desde almacenamiento de blobs, deberá tooadd un "/" al principio de Hola Hola del nombre de archivo.
   * **$srcDataFolder** y **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"

- - -
## <a id="appendix-c"></a>Apéndice C - preparar una base de datos de SQL Azure para hello salida del trabajo de Sqoop
**base de datos SQL tooprepare Hola (combinar esto con hello Sqoop script)**

1. Preparar los parámetros de hello:

    <table border="1">
    <tr><th>Nombre de la variable</th><th>Notas</th></tr>
    <tr><td>$sqlDatabaseServerName</td><td>nombre de Hola del servidor de base de datos de SQL Azure Hola. Escriba nada toocreate un nuevo servidor.</td></tr>
    <tr><td>$sqlDatabaseUsername</td><td>nombre de inicio de sesión Hello para el servidor de base de datos de SQL Azure Hola. Si $sqlDatabaseServerName es un servidor existente, el inicio de sesión de Hola y la contraseña de inicio de sesión son tooauthenticate usado con el servidor de Hola. En caso contrario, son toocreate usa un nuevo servidor.</td></tr>
    <tr><td>$sqlDatabasePassword</td><td>contraseña de inicio de sesión de Hello para el servidor de base de datos de SQL Azure Hola.</td></tr>
    <tr><td>$sqlDatabaseLocation</td><td>Este valor se usa solo cuando se crea un nuevo servidor de base de datos de Azure.</td></tr>
    <tr><td>$sqlDatabaseName</td><td>base de datos SQL de Hello utiliza tabla AvgDelays de toocreate hello para el trabajo de Sqoop Hola. Si se deja en blanco, se creará una base de datos denominada HDISqoop. nombre de la tabla de Hola para hello salida del trabajo de Sqoop es AvgDelays. </td></tr>
    </table>
2. Abra Azure PowerShell ISE.
3. Copie y pegue la siguiente secuencia de comandos en el panel de scripts de Hola de hello:

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Resource group variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure resource group name. It will be created if it doesn't exist.")]
        [String]$resourceGroupName,

        # SQL database server variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database Server Name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseServer,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user.")]
        [String]$sqlDatabaseLogin,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user password.")]
        [String]$sqlDatabasePassword,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello region toocreate hello Database in.")]
        [String]$sqlDatabaseLocation,   #For example, West US.

        # SQL database variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello database name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseName # specify hello database name if you have one created. Otherwise use "" toohave hello script create one for you.
    )

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Constants and variables

    # IP address REST service used for retrieving external IP address and creating firewall rules
    [String]$ipAddressRestService = "http://bot.whatismyipaddress.com"
    [String]$fireWallRuleName = "FlightDelay"

    # SQL database variables
    [String]$sqlDatabaseMaxSizeGB = 10

    #SQL query string for creating AvgDelays table
    [String]$sqlDatabaseTableName = "AvgDelays"
    [String]$sqlCreateAvgDelaysTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [origin_city_name] [nvarchar](50) NOT NULL,
                [weather_delay] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
                [origin_city_name] ASC
            )
            )"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #region - Create and validate Azure resouce group
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $sqlDatabaseLocation
    }

    #EndRegion

    #region - Create and validate Azure SQL database server
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServer -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServer = (New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -SqlAdministratorCredentials $credential -Location $sqlDatabaseLocation).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServer." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-workstation" -StartIpAddress $workstationIPAddress -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-Azureservices" -StartIpAddress "0.0.0.0" -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database

    try {
        Get-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName -Edition "Standard" -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region -  Execute an SQL command toocreate hello AvgDelays table

    Write-Host "`nCreating SQL Database table ..."  -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = $sqlCreateAvgDelaysTable
    $cmd.executenonquery()

    $conn.close()

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

   > [!NOTE]
   > Hello secuencia de comandos utiliza un servicio de representational state Transfer (REST) de transferencia, http://bot.whatismyipaddress.com, tooretrieve su dirección IP externa. dirección IP de Hola se usa para crear una regla de firewall para el servidor de base de datos SQL.

    Estas son algunas variables utilizadas en el script de Hola:

   * **$ipAddressRestService** -valor predeterminado de hello es http://bot.whatismyipaddress.com. Es un Es un servicio de REST de direcciones IP públicas para obtener la dirección IP externa. Puede usar los servicios que desee. dirección IP externa Hola recuperado a través del servicio Hola será toocreate usa una regla de firewall para el servidor de base de datos SQL de Azure, para que se puede tener acceso a base de datos de Hola desde su estación de trabajo (mediante un script de Windows PowerShell).
   * **$fireWallRuleName** -este es el nombre de Hola Hola de regla de firewall para el servidor de base de datos de SQL Azure Hola. es el nombre predeterminado de Hello <u>FlightDelay</u>. Puede cambiarlo si lo desea.
   * **$sqlDatabaseMaxSizeGB** : este valor se usa solo cuando se crea un nuevo servidor de Base de datos SQL de Azure. valor predeterminado de Hello es de 10GB. 10 GB es suficiente para este tutorial.
   * **$sqlDatabaseName** : este valor se usa solo cuando se crea una nueva Base de datos SQL de Azure. valor predeterminado de Hello es HDISqoop. Si cambia el nombre, debe actualizar script de Windows PowerShell de Sqoop de hello en consecuencia.
4. Presione **F5** secuencia de comandos de toorun Hola.
5. Validar salida de script de Hola. Asegúrese de que el script de Hola se ejecutó correctamente.

## <a id="nextsteps"></a> Pasos siguientes
Ahora que comprende cómo tooupload una tooAzure archivo almacenamiento de blobs, cómo tabla toopopulate un subárbol mediante Hola datos desde el almacenamiento de blobs de Azure, ¿cómo toorun Hive consultas y cómo toouse Sqoop tooexport datos de base de datos de SQL Azure HDFS tooan. toolearn más información, vea Hola siguientes artículos:

* [Introducción a HDInsight][hdinsight-get-started]
* [Uso de Hive con HDInsight][hdinsight-use-hive]
* [Uso de Oozie con HDInsight][hdinsight-use-oozie]
* [Uso de Sqoop con HDInsight][hdinsight-use-sqoop]
* [Uso de Pig con HDInsight][hdinsight-use-pig]
* [Desarrollo de programas MapReduce de Java para HDInsight][hdinsight-develop-mapreduce]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[rita-website]: http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time
[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[hadoop-hiveql]: https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL
[hadoop-shell-commands]: http://hadoop.apache.org/docs/r0.18.3/hdfs_shell.html

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx

[image-hdi-flightdelays-avgdelays-dataset]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.AvgDelays.DataSet.png
[img-hdi-flightdelays-run-hive-job-output]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.RunHiveJob.Output.png
[img-hdi-flightdelays-flow]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.Flow.png
