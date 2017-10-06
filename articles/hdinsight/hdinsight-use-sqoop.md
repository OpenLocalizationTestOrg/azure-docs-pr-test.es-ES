---
title: los trabajos de aaaRun Sqoop de Apache con Azure HDInsight (Hadoop) | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse PowerShell de Azure desde un toorun de estación de trabajo Sqoop importar y exportar entre un clúster de Hadoop y una base de datos de SQL Azure."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 2fdcc6b7-6ad5-4397-a30b-e7e389b66c7a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: bdac507704937d77921c9c13d70aa2434c7e3be4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-sqoop-with-hadoop-in-hdinsight"></a>Uso de Sqoop con Hadoop en HDInsight
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Obtenga información acerca de cómo toouse Sqoop en HDInsight tooimport y exportación entre el clúster de HDInsight y la base de datos SQL de Azure o la base de datos de SQL Server.

Aunque Hadoop es una opción natural para el procesamiento de datos no estructurados y semiestructurados, como registros y los archivos, también puede haber una necesidad de datos tooprocess estructurado que se almacenan en bases de datos relacionales.

[Sqoop] [ sqoop-user-guide-1.4.4] es una herramienta diseñada tootransfer datos entre clústeres de Hadoop y bases de datos relacionales. Puede usar lo tooimport datos desde un sistema de administración de bases de datos relacionales (RDBMS), como SQL Server, MySQL u Oracle en el sistema de archivos distribuido de Hadoop de hello (HDFS), transforme datos hello Hadoop MapReduce o subárbol y, a continuación, exportar datos de hello en un RDBMS. En este tutorial, usará una base de datos de SQL Server como base de datos relacional.

¿Para las versiones de Sqoop que son compatibles con clústeres de HDInsight, consulte [cuáles son las novedades en las versiones de clúster Hola proporcionadas por HDInsight?][hdinsight-versions]

## <a name="understand-hello-scenario"></a>Comprender el escenario de Hola

El clúster de HDInsight incluye algunos datos de ejemplo. Use Hola siguiendo dos ejemplos:

* Un archivo registro log4j, ubicado en */example/data/sample.log*. Hola después de registros extraído de archivo hello:
  
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
* Una tabla de Hive denominada *hivesampletable*, que las referencias Hola ubicado en el archivo de datos */hive/warehouse/hivesampletable*. Hola tabla contiene algunos datos de dispositivos móviles. 
  
  | Campo | Tipo de datos |
  | --- | --- |
  | clientid |string |
  | querytime |string |
  | market |string |
  | deviceplatform |string |
  | devicemake |string |
  | devicemodel |string |
  | state |string |
  | country |string |
  | querydwelltime |double |
  | sessionid |bigint |
  | sessionpagevieworder |bigint |

En primer lugar, exportar *sample.log* y *hivesampletable* toohello base de datos de SQL Azure o tooSQL Server y, a continuación, importar Hola que contenga datos de dispositivos móviles de hello hacer copia tooHDInsight mediante Hola ruta de acceso siguiente:

    /tutorials/usesqoop/importeddata

## <a name="create-cluster-and-sql-database"></a>Creación del clúster y la base de datos SQL
Esta sección muestra cómo toocreate un clúster, una base de datos de SQL y esquemas de base de datos SQL de Hola para ejecución Hola tutorial mediante Hola portal de Azure y una plantilla de Azure Resource Manager. Hola plantilla puede encontrarse en [plantillas de inicio rápido de Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/). plantilla de administrador de recursos de Hello llama a un bacpac paquete toodeploy Hola tabla esquemas tooSQL base de datos.  paquete de Hello bacpac se encuentra en un contenedor de blobs públicos, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac. Si desea toouse un contenedor privado para los archivos de bacpac de hello, utilice Hola después de valores de hello plantilla:
   
        "storageKeyType": "Primary",
        "storageKey": "<TheAzureStorageAccountKey>",

Si prefiere hello base de datos SQL y clúster de hello toocreate de toouse PowerShell de Azure, consulte [Apéndice A](#appendix-a---a-powershell-sample).

1. Haga clic en hello después imagen tooopen una plantilla de administrador de recursos en hello portal de Azure.         
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-sql-database%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-use-sqoop/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   

2. Escriba Hola propiedades siguientes:

    - **Suscripción**: escriba su suscripción de Azure.
    - **Grupo de recursos**: cree un nuevo grupo de recursos de Azure o seleccione uno existente.  Un grupo de recursos tiene fines administrativos.  Es un contenedor de objetos.
    - **Ubicación**: seleccione una región.
    - **ClusterName**: escriba un nombre para el clúster de Hadoop de Hola.
    - **Nombre de inicio de sesión y la contraseña del clúster**: nombre de inicio de sesión predeterminado de hello es administrador.
    - **Nombre de usuario y contraseña de SSH**.
    - **Nombre y contraseña de inicio de sesión en el servidor de la base de datos SQL**.
    - **_artifacts ubicación**: usar el valor predeterminado de Hola a menos que desee toouse su propio archivo lo en una ubicación diferente.
    - **_artifacts Location Sas Token** (Token Sas de ubicación de _artefactos): deje este valor en blanco.
    - **Nombre de archivo de Bacpac**: usar el valor predeterminado de Hola a menos que desee toouse su propio archivo lo.
     
     Hola después valores está codificados en la sección de variables de hello:
     
     | Nombre de la cuenta de almacenamiento predeterminada | <CluterName>store |
     | --- | --- |
     | Nombre del servidor de base de datos SQL de Azure |<ClusterName>dbserver |
     | Nombre de la base de datos SQL de Azure |<ClusterName>db |
     
     Escriba estos valores.  Se necesita más adelante en el tutorial Hola.

3. Haga clic en **Aceptar** parámetros de hello toosave.

4. de hello **implementación personalizada** hoja, haga clic en **grupo de recursos** desplegable cuadro y, a continuación, haga clic en **New** toocreate un nuevo grupo de recursos. grupo de recursos de Hello es un contenedor que agrupa los clúster de hello, cuenta de almacenamiento dependientes de hello y otro recurso vinculado.

5. Haga clic en **Términos legales** y en **Crear**.

6. Haga clic en **Crear**. Verá un icono nuevo llamado Envío de implementación para la implementación de plantilla. Se tarda aproximadamente clúster de aproximadamente 20 minutos toocreate hello y base de datos SQL.

Si elige toouse de base de datos SQL de Azure existente o Microsoft SQL Server

* **La base de datos SQL Azure**: debe configurar una regla de firewall para hello acceso de tooallow de servidor de base de datos de SQL Azure desde la estación de trabajo. Para obtener instrucciones sobre cómo crear una base de datos de SQL Azure y cómo configurar firewall de hello, consulte [Introducción al uso de la base de datos SQL de Azure][sqldatabase-get-started]. 
  
  > [!NOTE]
  > De forma predeterminada, una base de datos SQL de Azure permite realizar conexiones desde servicios de Azure, como HDInsight de Azure. Si se deshabilita esta configuración de firewall, necesita tooenable desde Hola portal de Azure. Para obtener instrucciones sobre la creación de una base de datos de Azure SQL Database y la configuración de las reglas de firewall, consulte [Creación y configuración de SQL Database][sqldatabase-create-configue].
  > 
  > 
* **SQL Server**: si el clúster de HDInsight está en hello misma red virtual en Azure como SQL Server, puede usar los pasos de hello en este artículo tooimport y exportación tooa SQL Server base de datos.
  
  > [!NOTE]
  > HDInsight solo admite redes virtuales basadas en la ubicación y actualmente no funciona con redes virtuales basadas en grupos de afinidad.
  > 
  > 
  
  * toocreate y configurar una red virtual, consulte [crear una red virtual con el portal de Azure hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).
    
    * Cuando se utiliza SQL Server en el centro de datos, debe configurar la red virtual de hello como *sitio a sitio* o *point-to-site*.
      
      > [!NOTE]
      > Para **point-to-site** redes virtuales, SQL Server deben disponer de cliente VPN Hola aplicación de configuración, que está disponible en hello **panel** de la configuración de red virtual de Azure.
      > 
      > 
    * Cuando se utiliza SQL Server en una máquina virtual de Azure, se puede utilizar cualquier configuración de red virtual si la máquina virtual de hello hospeda SQL Server es miembro del programa Hola a misma red virtual que HDInsight.
  * toocreate un clúster de HDInsight en una red virtual, vea [Hadoop crear clústeres de HDInsight con opciones personalizadas](hdinsight-hadoop-provision-linux-clusters.md)
    
    > [!NOTE]
    > SQL Server también debe permitir la autenticación. Debe usar un servidor de SQL Server hello toocomplete de inicio de sesión de los pasos de este artículo.
    > 
    > 

## <a name="run-sqoop-jobs"></a>Ejecución de trabajos de Sqoop
HDInsight puede ejecutar trabajos de Sqoop mediante una variedad de métodos. Usar hello después toodecide tabla qué método es adecuado para usted, a continuación, siga el vínculo de Hola para ver un tutorial.

| **Utilícelo** si desea... | ...un shell **interactivo** | ...procesamiento por**lotes** | ...con este **sistema operativo de clúster** | ...desde este **sistema operativo de cliente** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-use-sqoop-mac-linux.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X o Windows |
| [.NET SDK para Hadoop](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |&nbsp; |✔ |Linux o Windows |Windows (por ahora) |
| [Azure PowerShell](hdinsight-hadoop-use-sqoop-powershell.md) |&nbsp; |✔ |Linux o Windows |Windows |

## <a name="limitations"></a>Limitaciones
* La exportación masiva - basados en Linux con HDInsight, Hola Sqoop conector utilizado tooexport datos tooMicrosoft SQL Server o base de datos de SQL Azure no es compatible con las inserciones masivas.
* Procesamiento por lotes: con HDInsight basados en Linux, cuando se usa hello `-batch` cambiar cuando se realizan inserciones, Sqoop varias inserciones en lugar de procesamiento por lotes las operaciones de inserción de Hola.

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprendido cómo toouse Sqoop. toolearn más información, vea:

* [Uso de Hive con HDInsight](hdinsight-use-hive.md)
* [Uso de Pig con HDInsight](hdinsight-use-pig.md)
* [Uso de Oozie con HDInsight][hdinsight-use-oozie]: use la acción de Sqoop en un flujo de trabajo de Oozie.
* [Analizar datos de retrasos de vuelos con HDInsight][hdinsight-analyze-flight-data]: usar Hive tooanalyze flight retrasar datos y, a continuación, usar base de datos de Sqoop tooexport datos tooan SQL Azure.
* [Cargar datos tooHDInsight][hdinsight-upload-data]: dar con otros métodos para cargar el almacenamiento de blobs de datos tooHDInsight o SQL Azure.

## <a name="appendix-a---a-powershell-sample"></a>Apéndice A - un ejemplo de PowerShell
ejemplo de Hola a PowerShell realiza Hola pasos:

1. Conectar tooAzure.
2. Cree un grupo de recursos de Azure. Para obtener más información, consulte [Uso de Azure PowerShell con el Administrador de recursos de Azure](../powershell-azure-resource-manager.md)
3. Cree un servidor de Base de datos SQL de Azure, una base de datos SQL de Azure y dos tablas. 
   
    Si utiliza SQL Server en su lugar, use hello las instrucciones toocreate Hola tablas siguientes:
   
        CREATE TABLE [dbo].[log4jlogs](
         [t1] [nvarchar](50),
         [t2] [nvarchar](50),
         [t3] [nvarchar](50),
         [t4] [nvarchar](50),
         [t5] [nvarchar](50),
         [t6] [nvarchar](50),
         [t7] [nvarchar](50))
   
        CREATE TABLE [dbo].[mobiledata](
         [clientid] [nvarchar](50),
         [querytime] [nvarchar](50),
         [market] [nvarchar](50),
         [deviceplatform] [nvarchar](50),
         [devicemake] [nvarchar](50),
         [devicemodel] [nvarchar](50),
         [state] [nvarchar](50),
         [country] [nvarchar](50),
         [querydwelltime] [float],
         [sessionid] [bigint],
         [sessionpagevieworder][bigint])
   
    tablas y base de datos de hello más fácil manera tooexamine hello es toouse Visual Studio. servidor de base de datos de Hola y base de datos de Hola se pueden examinar con hello portal de Azure.
4. Cree un clúster de HDInsight.
   
    clúster de hello tooexamine, puede usar Hola portal de Azure o Azure PowerShell.
5. Preprocesar archivo de datos de origen de hello.
   
    En este tutorial, exporte un archivo de registro log4j (un archivo delimitado) y una base de datos de Hive tabla tooan SQL Azure. Hello archivo delimitado se denomina */example/data/sample.log*. Anteriormente en el tutorial de hello, ha visto algunos ejemplos de log4j registros. En el archivo de registro de hello, hay algunas líneas vacías y algunos toothese similar de líneas:
   
        java.lang.Exception: 2012-02-03 20:11:35 SampleClass2 [FATAL] unrecoverable system problem at id 609774657
            at com.osa.mocklogger.MockLogger$2.run(MockLogger.java:83)
   
    Esto es correcto para obtener ejemplos que utilizan estos datos, pero debemos eliminar estas excepciones antes de que podemos importar en la base de datos de SQL Azure de Hola o SQL Server. Se produce un error en la exportación de Sqoop si se produce una cadena vacía o una línea con un menor elementos que número Hola de campos definidos en la tabla de base de datos de SQL Azure Hola. tabla de Hello log4jlogs tiene 7 campos de tipo de cadena.
   
    Este procedimiento crea un nuevo archivo en clúster de hello: tutorials/usesqoop/data/sample.log. archivo de datos modificados de hello tooexamine, puede usar Hola portal de Azure, una herramienta de explorador de almacenamiento de Azure o Azure PowerShell. [Empezar a trabajar con HDInsight] [ hdinsight-get-started] tiene un código de ejemplo para usar Azure PowerShell toodownload un archivo y mostrar el contenido del archivo de Hola.
6. Exportar una base de datos de SQL Azure de datos archivo toohello.
   
    archivo de código fuente de Hello es tutorials/usesqoop/data/sample.log. tabla de Hola donde datos hello están toois exportados denomina log4jlogs.
   
   > [!NOTE]
   > Distinto de información de la cadena de conexión, deberían funcionar pasos hello en esta sección para una base de datos de SQL Azure o SQL Server. Estos pasos se han probado con hello siguiente configuración:
   > 
   > * **Configuración de red virtual de Azure point-to-site**: una red virtual conectado hello HDInsight clúster tooa SQL Server en un centro de datos privado. Vea [configurar una VPN de punto a sitio en el Portal de administración de Hola](../vpn-gateway/vpn-gateway-point-to-site-create.md) para obtener más información.
   > * **HDInsight de Azure 3.1:**consulte [Creación de clústeres de Hadoop basados en Windows en HDInsight](hdinsight-hadoop-provision-linux-clusters.md) para obtener más información sobre cómo crear un clúster en una red virtual.
   > * **SQL Server 2014**: configurar autenticación tooallow y tooconnect de paquete de configuración cliente VPN de hello ejecución segura toohello de red virtual.
   > 
   > 
7. Exportar una base de datos de Hive tabla toohello SQL Azure.
8. Importe el clúster de HDInsight de hello mobiledata tabla toohello.
   
    archivo de datos modificados de hello tooexamine, puede usar Hola portal de Azure, una herramienta de explorador de almacenamiento de Azure o Azure PowerShell.  [Empezar a trabajar con HDInsight] [ hdinsight-get-started] tiene un código de ejemplo sobre el uso de PowerShell de Azure toodownload un archivo y mostrar el contenido del archivo de Hola.

### <a name="hello-powershell-sample"></a>ejemplo de Hola a PowerShell
    # Prepare an Azure SQL database toobe used by hello Sqoop tutorial

    #region - provide hello following values

    $subscriptionID = "<Enter your Azure Subscription ID>"

    $sqlDatabaseLogin = "<Enter a SQL Database Login name>" #SQL Database server login
    $sqlDatabasePassword = "<Enter a Password>"

    $httpUserName = "admin"  #HDInsight cluster username
    $httpPassword = "<Enter a Password>"

    # used for creating Azure service names
    $nameToken = "<Enter an alias>" 
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")
    #endregion

    #region - variables

    # Resource group variables
    $resourceGroupName = $namePrefix + "rg"
    $location = "East US 2" # used by all Azure services defined in this tutorial

    # SQL database varialbes
    $sqlDatabaseServerName = $namePrefix + "sqldbserver"
    $sqlDatabaseName = $namePrefix + "sqldb"
    $sqlDatabaseConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $sqlDatabaseMaxSizeGB = 10

    # Used for retrieving external IP address and creating firewall rules
    $ipAddressRestService = "http://bot.whatismyipaddress.com"
    $fireWallRuleName = "UseSqoop"

    # Used for creating tables and clustered indexes
    $cmdCreateLog4jTable = "CREATE TABLE [dbo].[log4jlogs](
        [t1] [nvarchar](50),
        [t2] [nvarchar](50),
        [t3] [nvarchar](50),
        [t4] [nvarchar](50),
        [t5] [nvarchar](50),
        [t6] [nvarchar](50),
        [t7] [nvarchar](50))"

    $cmdCreateLog4jClusteredIndex = "CREATE CLUSTERED INDEX log4jlogs_clustered_index on log4jlogs(t1)"

    $cmdCreateMobileTable = " CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder][bigint])"

    $cmdCreateMobileDataClusteredIndex = "CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)"

    # HDInsight variables
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - Create Azure resouce group
    Write-Host "`nCreating an Azure resource group ..." -ForegroundColor Green
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    }
    #endregion

    #region - Create Azure SQL database server
    Write-Host "`nCreating an Azure SQL Database server ..." -ForegroundColor Green
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServerName -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServerName = (New-AzureRmSqlServer `
                                    -ResourceGroupName $resourceGroupName `
                                    -ServerName $sqlDatabaseServerName `
                                    -SqlAdministratorCredentials $credential `
                                    -Location $location).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServerName." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-workstation" `
            -StartIpAddress $workstationIPAddress `
            -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-Azureservices" `
            -StartIpAddress "0.0.0.0" `
            -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database
    Write-Host "`nCreating an Azure SQL database ..." -ForegroundColor Green

    try {
        Get-AzureRmSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName `
            -Edition "Standard" `
            -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region - Create tables
    Write-Host "Creating hello log4jlogs table and hello mobiledata table ..." -ForegroundColor Green

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create hello log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jTable
    $ret = $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateLog4jClusteredIndex
    $cmd.ExecuteNonQuery()

    # Create hello mobiledata table and index
    $cmd.CommandText = $cmdCreateMobileTable
    $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateMobileDataClusteredIndex
    $cmd.ExecuteNonQuery()

    $conn.close()

    #endregion


    #region - Create HDInsight cluster

    Write-Host "Creating hello HDInsight cluster and hello dependent services ..." -ForegroundColor Green

    # Create hello default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

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
        -DefaultStorageContainer $defaultBlobContainerName 

    # Validate hello cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - pre-process hello source file

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define hello connection string
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing hello source and destination blob.
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $sourceBlob = $storageContainer.GetBlockBlobReference($sourceBlobName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)

    # Define a MemoryStream and a StreamReader for reading from hello source file
    $stream = New-Object System.IO.MemoryStream
    $stream = $sourceBlob.OpenRead()
    $sReader = New-Object System.IO.StreamReader($stream)

    # Define a MemoryStream and a StreamWriter for writing into hello destination file
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    # Pre-process hello source blob
    $exString = "java.lang.Exception:"
    while(-Not $sReader.EndOfStream){
        $line = $sReader.ReadLine()
        $split = $line.Split(" ")

        # remove hello "java.lang.Exception" from hello first element of hello array
        # for example: java.lang.Exception: 2012-02-03 19:11:02 SampleClass8 [WARN] problem finding id 153454612
        if ($split[0] -eq $exString){
            #create a new ArrayList tooremove $split[0]
            $newArray = [System.Collections.ArrayList] $split
            $newArray.Remove($exString)

            # update $split and $line
            $split = $newArray
            $line = $newArray -join(" ")
        }

        # remove hello lines that has less than 7 elements
        if ($split.count -ge 7){
            write-host $line
            $writeStream.WriteLine($line)
        }
    }

    # Write toohello destination blob
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    #endregion

    #region - export a log file from hello cluster toohello SQL database

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    $tableName_log4j = "log4jlogs"

    # Connection string for Azure SQL Database.
    # Comment if using SQL Server
    $connectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"
    # Connection string for SQL Server.
    # Uncomment if using SQL Server.
    #$connectionString = "jdbc:sqlserver://$sqlDatabaseServerName;user=$sqlDatabaseLogin;password=$sqlDatabasePassword;database=$sqlDatabaseName"

    $exportDir_log4j = "/tutorials/usesqoop/data"

    # Submit a Sqoop job
    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_log4j --export-dir $exportDir_log4j --input-fields-terminated-by \0x20 -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose
    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardError
    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardOutput

    #endregion

    #region - export a Hive table

    $tableName_mobile = "mobiledata"
    $exportDir_mobile = "/hive/warehouse/hivesampletable"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_mobile --export-dir $exportDir_mobile --fields-terminated-by \t -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion

    #region - import a database

    $targetDir_mobile = "/tutorials/usesqoop/importeddata/"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "import --connect $connectionString --table $tableName_mobile --target-dir $targetDir_mobile --fields-terminated-by \t --lines-terminated-by \n -m 1"

    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion



[azure-management-portal]: https://portal.azure.com/

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database/sql-database-get-started.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
