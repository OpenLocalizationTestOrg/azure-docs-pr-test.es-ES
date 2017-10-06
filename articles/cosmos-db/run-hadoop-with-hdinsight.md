---
title: aaaRun un Hadoop de trabajo utilizando la base de datos de Azure Cosmos y HDInsight | Documentos de Microsoft
description: "Obtenga información acerca de cómo toorun un simple Hive, Pig y MapReduce de trabajo con la base de datos de Azure Cosmos y HDInsight de Azure."
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 06f0ea9d-07cb-4593-a9c5-ab912b62ac42
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 06/08/2017
ms.author: denlee
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2e27499f2c4ba951af9a1ade1bcc9c1b6d298fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="Azure Cosmos DB-HDInsight"></a>Ejecución de un trabajo de Apache Hive, Pig o Hadoop con Cosmos DB y HDInsight
Este tutorial muestra cómo toorun [Apache Hive][apache-hive], [Apache Pig][apache-pig], y [Apache Hadoop] [ apache-hadoop] Trabajos MapReduce en HDInsight de Azure con el conector de Hadoop de Cosmos DB. Conector de Hadoop de COSMOS de DB permite tooact de base de datos de Cosmos como un origen y un receptor para trabajos de Hive, Pig y MapReduce. Este tutorial usará DB Cosmos como origen de datos de Hola y de destino para trabajos de Hadoop.

Después de completar este tutorial, estará hello tooanswer pueda siguientes preguntas:

* ¿Cómo se cargan datos desde Cosmos DB mediante un trabajo de MapReduce, Pig o Hive?
* ¿Cómo se almacenan datos en Cosmos DB mediante un trabajo de MapReduce, Pig o Hive?

Se recomienda introducción, inspeccionando Hola después de vídeo, donde se ejecuta a través de un trabajo de Hive mediante DB Cosmos y HDInsight.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

A continuación, devolver artículo toothis, donde recibirá Hola información detallada sobre cómo ejecutar trabajos de análisis en los datos de la base de datos de Cosmos.

> [!TIP]
> Este tutorial presupone que se tiene experiencia previa con Apache Hadoop, Hive o Pig Si es nuevo tooApache Hadoop, Hive y Pig, recomendamos visitar hello [documentación de Apache Hadoop][apache-hadoop-doc]. Asimismo, el tutorial también presupone que se tiene experiencia previa con Cosmos DB además de una cuenta en este servicio. Si usted es tooCosmos nueva base de datos o no tiene una cuenta de base de datos de Cosmos, consulte nuestro [Introducción] [ getting-started] página.
>
>

¿No tiene tiempo toocomplete Hola tutorial y sólo desea scripts de PowerShell de ejemplo completo de tooget Hola de Hive, Pig y MapReduce? No hay problema, obténgalos [aquí][hdinsight-samples]. descarga de Hello también contiene archivos de hql, pig y java de Hola para estos ejemplos.

## <a name="NewestVersion"></a>Versión más reciente
<table border='1'>
    <tr><th>Versión del conector de Hadoop</th>
        <td>1.2.0</td></tr>
    <tr><th>URI de script</th>
        <td>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</td></tr>
    <tr><th>Fecha de modificación</th>
        <td>26/04/2016</td></tr>
    <tr><th>Versiones compatibles de HDInsight</th>
        <td>3.1, 3.2</td></tr>
    <tr><th>Registro de cambios</th>
        <td>Actualizar base de datos de Azure Cosmos Java SDK too1.6.0</br>
            Se ha agregado compatibilidad con las colecciones divididas como origen y receptor.</br>
        </td></tr>
</table>

## <a name="Prerequisites"></a>Requisitos previos
Antes de seguir las instrucciones de hello en este tutorial, asegúrese de que tiene Hola siguientes:

* Una cuenta de Cosmos DB, una base de datos y una colección con documentos dentro. Para más información, consulte [Introducción a Cosmos DB][getting-started]. Importar datos de ejemplo a la cuenta de base de datos de Cosmos con hello [herramienta de importación de base de datos de Cosmos][import-data].
* Capacidad de proceso. Las lecturas y escrituras de HDInsight se tienen en cuenta a la hora de calcular las unidades de solicitud asignadas a las colecciones.
* Capacidad para un procedimiento almacenado adicional dentro de cada colección de salida. procedimientos almacenado de Hola se usan para transferir los documentos resultantes.
* Capacidad para documentos resultantes de Hola de trabajos de Hive, Pig y MapReduce Hola.
* [*Opcional*] Capacidad para una colección adicional.

> [!WARNING]
> En orden tooavoid Hola la creación de una nueva colección durante alguno de los trabajos de hello, puede imprimir Hola resultados toostdout, guardar el contenedor de hello salida tooyour WASB o especifique una recopilación ya existente. En caso de hello de especificar una colección existente, se crearán nuevos documentos dentro de la colección de Hola y documentos ya existentes solo se verán afectados si se produce un conflicto en *identificadores*. **Conector de Hello sobrescribirá automáticamente documentos existentes con los conflictos de identificador**. Puede desactivar esta característica estableciendo Hola upsert opción toofalse. Si es false upsert y se produce un conflicto, se producirá un error de trabajo de Hadoop de hello; informar de un error de conflicto de identificador.
>
>

## <a name="ProvisionHDInsight"></a>Paso 1: Creación de un nuevo clúster de HDInsight
Este tutorial usa la acción de secuencia de comandos de hello Azure Portal toocustomize su clúster de HDInsight. En este tutorial, usaremos hello Azure Portal toocreate su clúster de HDInsight. Para obtener instrucciones sobre cómo los cmdlets de PowerShell de toouse o hello HDInsight .NET SDK, visite la [HDInsight personalizar clústeres mediante la acción de secuencia de comandos] [ hdinsight-custom-provision] artículo.

1. Inicie sesión en toohello [Portal de Azure][azure-portal].
2. Haga clic en **+ nuevo** en la parte superior de Hola de hello barra de navegación izquierda, busque **HDInsight** en la barra de búsqueda superior hello en la nueva hoja de Hola.
3. **HDInsight** publicados por **Microsoft** aparecerá en la parte superior de Hola de resultados de Hola. Haga clic en él y luego en **rear**.
4. En el nuevo HDInsight clúster Hola Crear hoja, escriba su **nombre del clúster** y seleccione hello **suscripción** desea tooprovision este recurso en.

    <table border='1'>
        <tr><td>Nombre del clúster</td><td>Clúster de Hola de nombre.<br/>
El nombre DNS debe empezar y terminar con un carácter alfanumérico y puede contener guiones.<br/>
campo de Hello debe ser una cadena comprendida entre 3 y 63 caracteres.</td></tr>
        <tr><td>Subscription Name</td>
            <td>Si tiene más de una suscripción de Azure, seleccione la suscripción de Hola que va a hospedar el clúster de HDInsight. </td></tr>
    </table>
5.Haga clic en **Seleccionar tipo de clúster** y Hola conjunto después propiedades toohello los valores especificados.

    <table border='1'>
        <tr><td>Tipo de clúster</td><td><strong>Hadoop</strong></td></tr>
        <tr><td>Nivel de clúster</td><td><strong>Estándar</strong></td></tr>
        <tr><td>Sistema operativo</td><td><strong>Windows</strong></td></tr>
        <tr><td>Versión</td><td>Versión más reciente</td></tr>
    </table>

    Ahora, haga clic en **SELECCIONAR**.

    ![Proporcionar detalles del clúster inicial de HDInsight de Hadoop][image-customprovision-page1]
6. Haga clic en **credenciales** tooset su inicio de sesión y credenciales de acceso remoto. Elija su **nombre de usuario de inicio de sesión del clúster** y **contraseña de inicio de sesión del clúster**.

    Si desea tooremote en el clúster, seleccione *Sí* final Hola de hoja de Hola y proporcione un nombre de usuario y una contraseña.
7. Haga clic en **origen de datos** tooset acceso de la ubicación principal para los datos. Elija hello **método de selección de** y especificar una cuenta de almacenamiento ya existente o cree uno nuevo.
8. Hola la misma hoja en, especifique un **contenedor predeterminado** y un **ubicación**. A continuación, haga clic en **SELECCIONAR**.

   > [!NOTE]
   > Seleccione una región de la cuenta de base de datos de Cosmos para mejorar el rendimiento de ubicación cerrar tooyour
   >
   >
9. Haga clic en **precios** tooselect Hola número y tipo de nodos. Puede mantener configuración predeterminada de Hola y escala Hola número de nodos de trabajo más adelante.
10. Haga clic en **configuración opcional**, a continuación, **acciones de Script** Hola hoja de configuración opcional.

     En acciones de secuencia de comandos, escriba Hola después información toocustomize su clúster de HDInsight.

     <table border='1'>
         <tr><th>Propiedad</th><th>Valor</th></tr>
         <tr><td>Nombre</td>
             <td>Especifique un nombre para la acción de secuencia de comandos de Hola.</td></tr>
         <tr><td>Identificador URI de script</td>
             <td>Especifique Hola URI toohello script que es invocado toocustomize Hola clúster.</br></br>
Especifique esta información: </br> <strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</td></tr>
         <tr><td>Principal</td>
             <td>Haga clic en Hola casilla toorun Hola script de PowerShell en el nodo principal de Hola.</br></br>
             <strong>Active esta casilla</strong>.</td></tr>
         <tr><td>Trabajo</td>
             <td>Haga clic en el script de PowerShell de hello casilla toorun hello en el nodo de trabajo Hola.</br></br>
             <strong>Active esta casilla</strong>.</td></tr>
         <tr><td>Zookeeper</td>
             <td>Haga clic en el script de PowerShell de hello casilla toorun hello en hello Zookeeper.</br></br>
             <strong>No es necesario</strong>.
             </td></tr>
         <tr><td>parameters</td>
             <td>Especificar parámetros de hello, si así lo requiere el script de Hola.</br></br>
             <strong>No se necesita ningún parámetro</strong>.</td></tr>
     </table>
11. Cree un **grupo de recursos** o use uno existente en su suscripción de Azure.
12. Ahora, compruebe **Pin toodashboard** tootrack su implementación y haga clic en **crear**!

## <a name="InstallCmdlets"></a>Paso 2: Instalación y configuración de Azure PowerShell
1. Instale Azure PowerShell. Puede encontrar instrucciones [aquí][powershell-install-configure].

   > [!NOTE]
   > En el caso de las consultas de Hive, use el Editor de Hive en línea de HDInsight. toodo por lo tanto, inicie sesión en toohello [Portal de Azure][azure-portal], haga clic en **HDInsight** tooview de panel izquierdo hello en una lista de los clústeres de HDInsight. Haga clic en el clúster de Hola que desea que las consultas de Hive toorun en y, a continuación, haga clic en **consola de consultas**.
   >
   >
2. Abra hello Azure PowerShell Integrated Scripting Environment:

   * En un equipo que ejecute Windows 8 o Windows Server 2012 o posterior, también puede usar integrada de hello búsqueda. En la pantalla de inicio de bienvenida, escriba **powershell ise** y haga clic en **ENTRAR**.
   * En un equipo que ejecuta una versión anterior a Windows 8 o Windows Server 2012, utilice el menú de inicio de Hola. En el menú de inicio de hello, escriba **símbolo** en el cuadro de búsqueda de hello, luego, en lista de Hola de resultados, haga clic en **símbolo**. Hola símbolo del sistema, escriba **powershell_ise** y haga clic en **ENTRAR**.
3. Agregue su cuenta de Azure.

   1. Hola panel de consola, escriba **Add-AzureAccount** y haga clic en **ENTRAR**.
   2. Escriba Hola dirección de correo electrónico asociada a su suscripción de Azure y haga clic en **continuar**.
   3. Escribir contraseña de hello para la suscripción de Azure.
   4. Haga clic en **Iniciar sesión**.
4. Hola después diagrama identifica partes importantes de Hola de su entorno de Scripting de PowerShell de Azure.

    ![Diagrama de Azure PowerShell][azure-powershell-diagram]

## <a name="RunHive"></a>Paso 3: Ejecución de un trabajo de Hive con Cosmos DB y HDInsight
> [!IMPORTANT]
> Todas las variables indicadas con < > deben rellenarse con los valores de configuración adecuados.
>
>

1. Establecer Hola después de las variables en el panel de scripts de PowerShell.

        # Provide Azure subscription name, hello Azure Storage account and container that is used for hello default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide hello HDInsight cluster name where you want toorun hello Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p>Comencemos a construir la cadena de consulta. Escribiremos una consulta de Hive que toma las marcas de hora generada por el sistema (_ts) y los identificadores únicos (_rid) de una colección de base de datos de Azure Cosmos todos los documentos, cuenta todos los documentos por minuto de hello y, a continuación, vuelve a almacenar resultados de hello en una nueva colección de base de datos de Azure Cosmos.</p>

    <p>En primer lugar se crea una tabla de Hive a partir de la colección de Azure Cosmos DB. Agregar Hola siguiente fragmento de código toohello panel de scripts de PowerShell <strong>después</strong> fragmento de código de hello de #1. Asegúrese de que incluir Hola opcional DocumentDB.query parámetro t recorte nuestros documentos toojust _ts y _rid.</p>

   > [!NOTE]
   > **La denominación de DocumentDB.inputCollections no era un error.** Sí, se pueden agregar varias colecciones como una entrada: </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> hello collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB hello query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. A continuación, vamos a crear una tabla de Hive para la recopilación de salida de hello. propiedades de documento de salida de Hello será mes hello, día, hora, minuto y número total de Hola de repeticiones.

   > [!NOTE]
   > **Una vez más, la denominación de DocumentDB.outputCollections no era un error.** Sí, se pueden agregar varias colecciones como una salida: </br>
   > "*DocumentDB.outputCollections*"="*\<Nombre de la colección de salida de DocumentDB 1\>*,*\<Nombre de la colección de salida de DocumentDB 2\>*" </br> nombres de la colección de Hola se separan sin espacios en blanco, con solo una sola coma. </br></br>
   > Documentos se distribuirán en cadena en varias colecciones. Un lote de documentos se almacenará en una colección y, a continuación, un segundo lote de documentos se almacenará en la recolección siguiente de Hola y así sucesivamente.
   >
   >

       # Create a Hive table for hello output data tooDocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. Por último, vamos a documentos de hello recuento por mes, día, hora y minuto e insertar resultados hello en hello habían salida tabla de Hive.

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. Agregar Hola siguientes toocreate de fragmento de script una definición de trabajo de Hive de consulta anterior Hola.

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    También puede usar hello - archivo cambiar toospecify un archivo de script de HiveQL en HDFS.
4. Agregue Hola después de la hora de inicio de fragmento de código toosave hello y enviar el trabajo de Hive Hola.

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. Agregar Hola después toowait para toocomplete de trabajo de Hive Hola.

        # Wait for hello Hive job toocomplete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. Agregue Hola siguientes tooprint Hola estándar hello y salida de inicio y finalización.

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. **Ejecute** el nuevo script. **Haga clic en** verde Hola ejecutar botón.
8. Hola resultados de la comprobación. Inicio de sesión en hello [Portal de Azure][azure-portal].

   1. Haga clic en <strong>examinar</strong> en el panel del lado izquierdo de Hola. </br>
   2. Haga clic en <strong>todo</strong> en hello superior derecha del panel de exploración de Hola. </br>
   3. Busque y haga clic en <strong>Cuentas de Azure Cosmos DB</strong>. </br>
   4. A continuación, busque su <strong>cuenta de base de datos de Azure Cosmos</strong>, a continuación, <strong>base de datos de base de datos de Azure Cosmos</strong> y su <strong>colección de base de datos de Azure Cosmos</strong> asociados con la colección de salida de hello especificada en la consulta de Hive.</br>
   5. Por último, haga clic en <strong>Explorador de documentos</strong>, debajo de <strong>Herramientas de desarrollo</strong>.</br></p>

   Verá los resultados de saludo de la consulta de Hive.

   ![Resultados de la consulta de Hive][image-hive-query-results]

## <a name="RunPig"></a>Paso 4: Ejecución de un trabajo de Pig con Cosmos DB y HDInsight
> [!IMPORTANT]
> Todas las variables indicadas con < > deben rellenarse con los valores de configuración adecuados.
>
>

1. Establecer Hola después de las variables en el panel de scripts de PowerShell.

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want toorun hello Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p>Comencemos a construir la cadena de consulta. Escribiremos una consulta de Pig que toma las marcas de hora generada por el sistema (_ts) y los identificadores únicos (_rid) de una colección de base de datos de Azure Cosmos todos los documentos, cuenta todos los documentos por minuto de hello y, a continuación, vuelve a almacenar resultados de hello en una nueva colección de base de datos de Azure Cosmos.</p>
    <p>En primer lugar, cargue documentos de Cosmos DB en HDInsight. Agregar Hola siguiente fragmento de código toohello panel de scripts de PowerShell <strong>después</strong> fragmento de código de hello de #1. Asegúrese de que tooadd una DocumentDB de consulta toohello opcional documentos consulta parámetro tootrim nuestros documentos toojust _ts y _rid.</p>

   > [!NOTE]
   > Sí, se pueden agregar varias colecciones como una entrada: </br>
   > "*\<Nombre de la colección de salida de DocumentDB 1\>*,*\<Nombre de la colección de salida de DocumentDB 2\>*"</br> nombres de la colección de Hola se separan sin espacios en blanco, con solo una sola coma. </b>
   >
   >

    Documentos se distribuirán en cadena en varias colecciones. Un lote de documentos se almacenará en una colección y, a continuación, un segundo lote de documentos se almacenará en la recolección siguiente de Hola y así sucesivamente.

        # Load data from Cosmos DB. Pass DocumentDB query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. A continuación, vamos a concuerdan documentos Hola por mes de hello, día, hora, minuto y número total de Hola de repeticiones.

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. Por último, vamos a almacenar resultados de hello en nuestra nueva colección de salida.

   > [!NOTE]
   > Sí, se pueden agregar varias colecciones como una salida: </br>
   > "\<Nombre de la colección de salida de DocumentDB 1\>,\<Nombre de la colección de salida de DocumentDB 2\>"</br> nombres de la colección de Hola se separan sin espacios en blanco, con solo una sola coma.</br>
   > Documenta will ser distribuida round robin en hello varias colecciones. Un lote de documentos se almacenará en una colección y, a continuación, un segundo lote de documentos se almacenará en la recolección siguiente de Hola y así sucesivamente.
   >
   >

        # Store output data tooCosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. Agregar Hola siguientes toocreate de fragmento de script una definición de trabajo de Pig de consulta anterior Hola.

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    También puede usar hello - archivo cambiar toospecify un archivo de script de Pig en HDFS.
6. Agregue Hola después de la hora de inicio de fragmento de código toosave hello y enviar el trabajo de Pig Hola.

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. Agregar Hola después toowait para toocomplete de trabajo de Pig Hola.

        # Wait for hello Pig job toocomplete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. Agregue Hola siguientes tooprint Hola estándar hello y salida de inicio y finalización.

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. **Ejecute** el nuevo script. **Haga clic en** verde Hola ejecutar botón.
10. Hola resultados de la comprobación. Inicio de sesión en hello [Portal de Azure][azure-portal].

    1. Haga clic en <strong>examinar</strong> en el panel del lado izquierdo de Hola. </br>
    2. Haga clic en <strong>todo</strong> en hello superior derecha del panel de exploración de Hola. </br>
    3. Busque y haga clic en <strong>Cuentas de Azure Cosmos DB</strong>. </br>
    4. A continuación, busque su <strong>cuenta de base de datos de Azure Cosmos</strong>, a continuación, <strong>base de datos de base de datos de Azure Cosmos</strong> y su <strong>colección de base de datos de Azure Cosmos</strong> asociados con la colección de salida de hello especificada en la consulta de Pig.</br>
    5. Por último, haga clic en <strong>Explorador de documentos</strong>, debajo de <strong>Herramientas de desarrollo</strong>.</br></p>

    Verá los resultados de saludo de la consulta de Pig.

    ![Resultados de la consulta de Pig][image-pig-query-results]

## <a name="RunMapReduce"></a>Paso 5: Ejecución de un trabajo de MapReduce con Azure Cosmos DB y HDInsight
1. Establecer Hola después de las variables en el panel de scripts de PowerShell.

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. Se deberá ejecutar un trabajo de MapReduce que cuenta Hola número de repeticiones de cada propiedad de documento de la colección de la base de datos de Azure Cosmos. Agregue este fragmento de script **después** fragmento Hola anterior.

        # Define hello MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > TallyProperties v01.jar incluye instalación personalizada de Hola de hello Cosmos conector de Hadoop de base de datos.
   >
   >
3. Agregar Hola siguiendo el trabajo de MapReduce de comando toosubmit Hola.

        # Save hello start time and submit hello job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    Además toohello definición del trabajo MapReduce, también proporcionar nombre del clúster de HDInsight de Hola donde desee trabajo de MapReduce toorun hello y credenciales de Hola. Hola Start-AzureHDInsightJob es una llamada desincronizada. finalización de hello toocheck de trabajo de hello, use hello *Wait-AzureHDInsightJob* cmdlet.
4. Agregar Hola después toocheck comando producido algún error en el trabajo en ejecución Hola MapReduce.

        # Get hello job output and print hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. **Ejecute** el nuevo script. **Haga clic en** verde Hola ejecutar botón.
6. Hola resultados de la comprobación. Inicio de sesión en hello [Portal de Azure][azure-portal].

   1. Haga clic en <strong>examinar</strong> en el panel del lado izquierdo de Hola.
   2. Haga clic en <strong>todo</strong> en hello superior derecha del panel de exploración de Hola.
   3. Busque y haga clic en <strong>Cuentas de Azure Cosmos DB</strong>.
   4. A continuación, busque su <strong>cuenta de base de datos de Azure Cosmos</strong>, a continuación, <strong>base de datos de base de datos de Azure Cosmos</strong> y su <strong>colección de base de datos de Azure Cosmos</strong> asociados con la colección de salida de hello especificada en el trabajo de MapReduce.
   5. Por último, haga clic en <strong>Explorador de documentos</strong>, debajo de <strong>Herramientas de desarrollo</strong>.

      Verá resultados Hola de su trabajo de MapReduce.

      ![Resultados de la consulta de MapReduce][image-mapreduce-query-results]

## <a name="NextSteps"></a>Pasos siguientes
¡Enhorabuena! Acaba de ejecutar sus primeros trabajos de Hive, Pig y MapReduce con Azure Cosmos DB y HDInsight.

El conector de Hadoop tiene el código abierto. Si le interesa, puede contribuir en [GitHub][github].

toolearn más información, vea Hola siguientes artículos:

* [Desarrollo de una aplicación Java con DocumentDB][documentdb-java-application]
* [Desarrollo de programas MapReduce de Java para Hadoop en HDInsight][hdinsight-develop-deploy-java-mapreduce]
* [Empezar a trabajar con Hadoop Hive en el uso de auriculares móviles de tooanalyze de HDInsight][hdinsight-get-started]
* [Uso de MapReduce con HDInsight][hdinsight-use-mapreduce]
* [Uso de Hive con HDInsight][hdinsight-use-hive]
* [Uso de Pig con HDInsight][hdinsight-use-pig]
* [Personalización de los clústeres de HDInsight mediante la acción de script][hdinsight-hadoop-customize-cluster]

[apache-hadoop]: http://hadoop.apache.org/
[apache-hadoop-doc]: http://hadoop.apache.org/docs/current/
[apache-hive]: http://hive.apache.org/
[apache-pig]: http://pig.apache.org/
[getting-started]: documentdb-get-started.md

[azure-portal]: https://portal.azure.com/
[azure-powershell-diagram]: ./media/run-hadoop-with-hdinsight/azurepowershell-diagram-med.png

[hdinsight-samples]: http://portalcontent.blob.core.windows.net/samples/documentdb-hdinsight-samples.zip
[github]: https://github.com/Azure/azure-documentdb-hadoop
[documentdb-java-application]: documentdb-java-application.md
[import-data]: import-data.md

[hdinsight-custom-provision]: ../hdinsight/hdinsight-provision-clusters.md
[hdinsight-develop-deploy-java-mapreduce]: ../hdinsight/hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-hadoop-customize-cluster]: ../hdinsight/hdinsight-hadoop-customize-cluster.md
[hdinsight-get-started]: ../hdinsight/hdinsight-hadoop-tutorial-get-started-windows.md
[hdinsight-storage]: ../hdinsight/hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: ../hdinsight/hdinsight-use-hive.md
[hdinsight-use-mapreduce]: ../hdinsight/hdinsight-use-mapreduce.md
[hdinsight-use-pig]: ../hdinsight/hdinsight-use-pig.md

[image-customprovision-page1]: ./media/run-hadoop-with-hdinsight/customprovision-page1.png
[image-hive-query-results]: ./media/run-hadoop-with-hdinsight/hivequeryresults.PNG
[image-mapreduce-query-results]: ./media/run-hadoop-with-hdinsight/mapreducequeryresults.PNG
[image-pig-query-results]: ./media/run-hadoop-with-hdinsight/pigqueryresults.PNG

[powershell-install-configure]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0
