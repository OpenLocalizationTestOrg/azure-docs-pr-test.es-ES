---
title: aaaAnalyze datos de Twitter con Hadoop en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hive tooanalyze Twitter datos en Hadoop en HDInsight toofind Hola frecuencia de uso de una palabra determinada."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 78e4ea33-9714-424d-ac07-3d60ecaebf2e
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 40c0a1afbc1fff10c070d22a99cd9d32d42f230a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-twitter-data-using-hive-in-hdinsight"></a>Análisis de datos de Twitter con Hive en HDInsight
Sitios Web sociales es una de las fuerzas principales de conducción hello para la adopción de grandes cantidades de datos. Las API públicas proporcionadas por sitios como Twitter constituyen un origen de datos muy útil para analizar y comprender las tendencias populares.
En este tutorial, se obtendrá tweets mediante el uso de una API de transmisión por secuencias de Twitter y, a continuación, usar Apache Hive en HDInsight de Azure tooget una lista de usuarios de Twitter que envían Hola tweets mayoría que contenía una palabra determinada.

> [!IMPORTANT]
> Hello pasos de este documento requieren un clúster de HDInsight basados en Windows. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Para clúster pasos tooa específicos basados en Linux, consulte [Twitter analizar datos con Hive en HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este tutorial, debe tener el siguiente hello:

* **Una estación de trabajo** con Powershell de Azure instalado y configurado.

    tooexecute secuencias de comandos de Windows PowerShell, debe ejecutar Azure PowerShell como administrador y establecer la directiva de ejecución de hello demasiado*RemoteSigned*. Consulte [Ejecución de scripts de Windows PowerShell][powershell-script].

    Antes de ejecutar scripts de Windows PowerShell, asegúrese de que están conectado tooyour suscripción de Azure mediante Hola siguiente cmdlet:

    ```powershell
    Login-AzureRmAccount
    ```

    Si tiene varias suscripciones de Azure, use Hola después de la suscripción actual de cmdlet tooset hello:

    ```powershell
    Select-AzureRmSubscription -SubscriptionID <Azure Subscription ID>
    ```

    > [!IMPORTANT]
    > La compatibilidad con Azure PowerShell para administrar recursos de HDInsight mediante Azure Service Manager está **en desuso** y dejó de estar disponible por completo el 1 de enero de 2017. Hola pasos de este documento use Hola nuevos cmdlets de HDInsight que funcionan con el Administrador de recursos de Azure.
    >
    > Siga los pasos de hello en [instalar y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs) versión más reciente de hello tooinstall de PowerShell de Azure. Si tiene scripts de ese toobe necesidad de modifica toouse Hola nuevos cmdlets que funcionan con el Administrador de recursos de Azure, consulte [tooAzure desarrollo basado en el Administrador de recursos de migración de las herramientas de clústeres de HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) para obtener más información.

* **Un clúster de HDInsight de Azure**. Para obtener instrucciones sobre el aprovisionamiento del clúster, consulte [Introducción al uso de HDInsight][hdinsight-get-started] o [Aprovisionamiento de clústeres de HDInsight][hdinsight-provision]. Necesitará el nombre de clúster de hello más adelante en el tutorial Hola.

Hello siguiente tabla enumeran Hola archivos utilizados en este tutorial:

| Archivos | Description |
| --- | --- |
| /tutorials/twitter/data/tweets.txt |datos de origen de Hello para el trabajo de Hive Hola. |
| /tutorials/twitter/output |carpeta de salida de Hello de trabajo de Hive Hola. Hola nombre de archivo de salida de trabajo de Hive de predeterminada es **000000_0**. |
| tutorials/twitter/twitter.hql |archivo de script de HiveQL Hola. |
| /tutorials/twitter/jobstatus |Hola estado del trabajo de Hadoop. |

## <a name="get-twitter-feed"></a>Obtención de una fuente de Twitter
En este tutorial, utilizará hello [API de transmisión por secuencias de Twitter][twitter-streaming-api]. Hola específico Twitter streaming API que se va a usar es [Estados/filtro][twitter-statuses-filter].

> [!NOTE]
> Un archivo que contiene 10.000 tweets y archivo de script de Hive hello (que se describe en la sección siguiente Hola) se han cargado en un contenedor de Blob público. Puede omitir esta sección si desea toouse Hola cargar archivos.

[TWEETS datos](https://dev.twitter.com/docs/platform-objects/tweets) se almacena en formato JavaScript Object Notation (JSON) de Hola que contiene una estructura anidada compleja. En lugar de escribir varias líneas de código con un lenguaje de programación convencional, puede transformar esta estructura anidada en una tabla de Hive para que se puedan realizar consultas a través de un lenguaje similar al Lenguaje de consulta estructurado (SQL) llamado HiveQL.

Twitter usa OAuth tooprovide autorizado acceso tooits API. OAuth es un protocolo de autenticación que permite a los usuarios tooapprove aplicaciones tooact en su nombre sin compartir su contraseña. Puede encontrar más información en [oauth.net](http://oauth.net/) u Hola excelente [tooOAuth de guía para principiantes](http://hueniverse.com/oauth/) desde Hueniverse.

Hola primer paso toouse OAuth es una nueva aplicación en el sitio para desarrolladores de Twitter hello toocreate.

**toocreate una aplicación de Twitter**

1. Inicie sesión en demasiado[https://apps.twitter.com/](https://apps.twitter.com/). Haga clic en hello **Regístrese ahora** vincular si no tienes una cuenta de Twitter.
2. Haga clic en **Crear nueva aplicación**.
3. Especifique los campos **Name** (Nombre), **Description** (Descripción), **Website** (Sitio web). Se pueden realizar hasta una dirección URL para hello **sitio Web** campo. Hello en la tabla siguiente muestra algunos toouse de valores de ejemplo:

   | Campo | Valor |
   | --- | --- |
   |  Nombre |MyHDInsightApp |
   |  Description |MyHDInsightApp |
   |  Website |http://www.myhdinsightapp.com |
4. Active **Yes, I agree** (Acepto) y, a continuación, haga clic en **Create your Twitter application** (Crear la aplicación de Twitter).
5. Haga clic en hello **permisos** permiso predeterminado de pestaña hello es **de sólo lectura**. Esto es suficiente para este tutorial.
6. Haga clic en hello **claves y Tokens de acceso** ficha.
7. Haga clic en **Create my access token**(Crear mi token de acceso).
8. Haga clic en **prueba OAuth** en la esquina superior derecha de Hola de página Hola.
9. Rellene los campos **consumer key** (clave del consumidor), **Consumer secret** (Secreto del consumidor), **Access token** (Token de acceso) y **Access token secret** (Secreto del token de acceso). Necesitará los valores de hello más adelante en el tutorial Hola.

En este tutorial, utilizará llamada de servicio web de Windows PowerShell toomake Hola. Para obtener un ejemplo de .NET C#, consulte [Análisis de opinión en Twitter en tiempo real con HBase en HDInsight][hdinsight-hbase-twitter-sentiment]. Hola otras llamadas a servicios web populares herramienta toomake es [ *Curl*][curl]. Puede descargar Curl [aquí][curl-download].

> [!NOTE]
> Cuando utiliza el comando de curl Hola de Windows, use comillas dobles en lugar de comillas simples para los valores de opción de Hola.

**tooget tweets**

1. Hola abrir Windows PowerShell Integrated Scripting Environment (ISE). (En la pantalla de inicio de Windows 8 de bienvenida, escriba **PowerShell_ISE** y, a continuación, haga clic en **Windows PowerShell ISE**. Consulte [Inicio de Windows PowerShell en Windows 8 y Windows][powershell-start]).
2. Copie Hola siguiente secuencia de comandos en el panel de scripts de hello:

    ```powershell
    #region - variables and constants
    $clusterName = "<HDInsightClusterName>" # Enter hello HDInsight cluster name

    # Enter hello OAuth information for your Twitter application
    $oauth_consumer_key = "<TwitterAppConsumerKey>";
    $oauth_consumer_secret = "<TwitterAppConsumerSecret>";
    $oauth_token = "<TwitterAppAccessToken>";
    $oauth_token_secret = "<TwitterAppAccessTokenSecret>";

    $destBlobName = "tutorials/twitter/data/tweets.txt" # This script saves hello tweets into this blob.

    $trackString = "Azure, Cloud, HDInsight" # This script gets hello tweets containing these keywords.
    $track = [System.Uri]::EscapeDataString($trackString);
    $lineMax = 10000  # hello script will get this number of tweets. It is about 3 minutes every 100 lines.
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    Login-AzureRmAccount
    #endregion

    #region - Create a block blob object for writing tweets into Blob storage
    Write-Host "Get hello default storage account name and Blob container name using hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -Name $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $storageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $containerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $storageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $containerName." -ForegroundColor Yellow

    Write-Host "Define hello Azure storage connection string ..." -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$storageAccountName;AccountKey=$storageAccountKey"
    Write-Host "`tThe connection string is $storageConnectionString." -ForegroundColor Yellow

    Write-Host "Create block blob object ..." -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($containerName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)
    #end region

    # region - Format OAuth strings
    Write-Host "Format oauth strings ..." -ForegroundColor Green
    $oauth_nonce = [System.Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes([System.DateTime]::Now.Ticks.ToString()));
    $ts = [System.DateTime]::UtcNow - [System.DateTime]::ParseExact("01/01/1970", "dd/MM/yyyy", $null)
    $oauth_timestamp = [System.Convert]::ToInt64($ts.TotalSeconds).ToString();

    $signature = "POST&";
    $signature += [System.Uri]::EscapeDataString("https://stream.twitter.com/1.1/statuses/filter.json") + "&";
    $signature += [System.Uri]::EscapeDataString("oauth_consumer_key=" + $oauth_consumer_key + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_nonce=" + $oauth_nonce + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_signature_method=HMAC-SHA1&");
    $signature += [System.Uri]::EscapeDataString("oauth_timestamp=" + $oauth_timestamp + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_token=" + $oauth_token + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_version=1.0&");
    $signature += [System.Uri]::EscapeDataString("track=" + $track);

    $signature_key = [System.Uri]::EscapeDataString($oauth_consumer_secret) + "&" + [System.Uri]::EscapeDataString($oauth_token_secret);

    $hmacsha1 = new-object System.Security.Cryptography.HMACSHA1;
    $hmacsha1.Key = [System.Text.Encoding]::ASCII.GetBytes($signature_key);
    $oauth_signature = [System.Convert]::ToBase64String($hmacsha1.ComputeHash([System.Text.Encoding]::ASCII.GetBytes($signature)));

    $oauth_authorization = 'OAuth ';
    $oauth_authorization += 'oauth_consumer_key="' + [System.Uri]::EscapeDataString($oauth_consumer_key) + '",';
    $oauth_authorization += 'oauth_nonce="' + [System.Uri]::EscapeDataString($oauth_nonce) + '",';
    $oauth_authorization += 'oauth_signature="' + [System.Uri]::EscapeDataString($oauth_signature) + '",';
    $oauth_authorization += 'oauth_signature_method="HMAC-SHA1",'
    $oauth_authorization += 'oauth_timestamp="' + [System.Uri]::EscapeDataString($oauth_timestamp) + '",'
    $oauth_authorization += 'oauth_token="' + [System.Uri]::EscapeDataString($oauth_token) + '",';
    $oauth_authorization += 'oauth_version="1.0"';

    $post_body = [System.Text.Encoding]::ASCII.GetBytes("track=" + $track);
    #endregion

    #region - Read tweets
    Write-Host "Create HTTP web request ..." -ForegroundColor Green
    [System.Net.HttpWebRequest] $request = [System.Net.WebRequest]::Create("https://stream.twitter.com/1.1/statuses/filter.json");
    $request.Method = "POST";
    $request.Headers.Add("Authorization", $oauth_authorization);
    $request.ContentType = "application/x-www-form-urlencoded";
    $body = $request.GetRequestStream();

    $body.write($post_body, 0, $post_body.length);
    $body.flush();
    $body.close();
    $response = $request.GetResponse() ;

    Write-Host "Start stream reading ..." -ForegroundColor Green

    Write-Host "Define a MemoryStream and a StreamWriter for writing ..." -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    $sReader = New-Object System.IO.StreamReader($response.GetResponseStream())

    $inrec = $sReader.ReadLine()
    $count = 0
    while (($inrec -ne $null) -and ($count -le $lineMax))
    {
        if ($inrec -ne "")
        {
            Write-Host "`n`t $count tweets received." -ForegroundColor Yellow

            $writeStream.WriteLine($inrec)
            $count ++
        }

        $inrec=$sReader.ReadLine()
    }
    #endregion

    #region - Write tweets tooBlob storage
    Write-Host "Write toohello destination blob ..." -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    $sReader.close()
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. Establecer variables de tooeight cinco primeros de hello en el script de Hola:

    Variable|Description
    ---|---
    $clusterName|Este es el nombre de Hola Hola del clúster de HDInsight donde desea que la aplicación de hello toorun.
    $oauth_consumer_key|Se trata de aplicación de Twitter de hello **clave de consumidor** anotó anteriormente cuando se creó la aplicación de Twitter de hello.
    $oauth_consumer_secret|Se trata de aplicación de Twitter de hello **secreto de consumidor** anotó anteriormente.
    $oauth_token|Se trata de aplicación de Twitter de hello **token de acceso** anotó anteriormente.
    $oauth_token_secret|Se trata de aplicación de Twitter de hello **secreto del token de acceso** anotó anteriormente.
    $destBlobName|Este es el nombre de blob de salida de hello. es el valor predeterminado de Hello **tutorials/twitter/data/tweets.txt**. Si cambia el valor predeterminado de hello, necesitará tooupdate scripts de Windows PowerShell de hello en consecuencia.
    $trackString|servicio web de Hello devolverá palabras clave de tweets toothese relacionados. es el valor predeterminado de Hello **HDInsight de Azure, en la nube,**. Si cambia el valor predeterminado de hello, actualizará los scripts de Windows PowerShell de hello en consecuencia.
    $lineMax|valor de Hello determina cuántos script de Hola tweets va a leer. Tarda aproximadamente tres minutos tooread 100 tweets. Puede establecer un número mayor, pero se tardará más toodownload de tiempo.

1. Presione **F5** secuencia de comandos de toorun Hola. Si experimenta problemas, como alternativa, seleccione todas las líneas de Hola y, a continuación, presione **F8**.
2. Verá un mensaje de que se ha completado la tarea al final de Hola de salida de hello. Los posibles mensajes de error aparecerán en rojo.

Como procedimiento de validación, puede comprobar el archivo de salida de hello, **/tutorials/twitter/data/tweets.txt**, en el almacenamiento de blobs de Azure mediante un explorador de almacenamiento de Azure o Azure PowerShell. Para obtener un script de ejemplo de Windows PowerShell de todos los archivos enumerados, consulte [Uso de Blob Storage con HDInsight][hdinsight-storage-powershell].

## <a name="create-hiveql-script"></a>Creación de un script de HiveQL
Uso de PowerShell de Azure, puede ejecutar varias instrucciones de HiveQL uno a una hora u Hola paquete HiveQL instrucción en un archivo de script. En este tutorial, creará un script de HiveQL. archivo de script de Hola debe ser tooAzure cargado el almacenamiento de blobs. En la siguiente sección hello, se ejecutará el archivo de script de Hola mediante Azure PowerShell.

> [!NOTE]
> archivo de script de Hive Hello y un archivo que contiene 10.000 tweets se han cargado en un contenedor de Blob público. Puede omitir esta sección si desea toouse Hola cargar archivos.

Hola script de HiveQL llevará a cabo siguiente hello:

1. **Quitar tabla de hello tweets_raw** en caso de hello tabla ya existe.
2. **Crear tabla de Hive de hello tweets_raw**. Esta sección temporal estructurado tabla contiene más datos de Hola para extraer, transformar y cargar el procesamiento de (datos ETL). Para obtener información sobre las particiones, consulte el [tutorial de Hive][apache-hive-tutorial].
3. **Cargar datos** desde la carpeta de origen hello /tutorials/twitter/data. conjunto de datos de Hello tweets grande en formato JSON anidado ahora se ha transformado en una estructura de tabla temporal de Hive.
4. **Colocar Hola tweets tabla** en caso de hello tabla ya existe.
5. **Crear tabla de tweets de hello**. Antes de poder realizar consultas en el conjunto de datos de hello tweets mediante el uso de Hive, debe toorun otro proceso ETL. Este proceso ETL define un esquema de tabla más detallado para los datos de hello almacenada en la tabla de "twitter_raw" Hola.
6. **Insertar tabla de sobrescritura**. Este script de Hive complejo se lanzará un conjunto de trabajos MapReduce largos por clúster de Hadoop de Hola. Según el tamaño de hello y conjunto de datos del clúster, puede tardar unos 10 minutos.
7. **Insertar directorio de sobrescritura**. Ejecutar un archivo de tooa de un conjunto de datos de hello consulta y de salida. Esta consulta devolverá una lista de usuarios de Twitter que envían tweets mayoría que contenía la palabra Hola "Azure".

**toocreate un subárbol de scripts y cargar tooAzure**

1. Abra Windows PowerShell ISE.
2. Copie Hola siguiente secuencia de comandos en el panel de scripts de hello:

    ```powershell
    #region - variables and constants
    $clusterName = "<Existing HDInsight Cluster Name>" # Enter your HDInsight cluster name
    $subscriptionID = "<Azure Subscription ID>"

    $sourceDataPath = "/tutorials/twitter/data"
    $outputPath = "/tutorials/twitter/output"
    $hqlScriptFile = "tutorials/twitter/twitter.hql"

    $hqlStatements = @"
    set hive.exec.dynamic.partition = true;
    set hive.exec.dynamic.partition.mode = nonstrict;

    DROP TABLE tweets_raw;
    CREATE EXTERNAL TABLE tweets_raw (
        json_response STRING
    )
    STORED AS TEXTFILE LOCATION '$sourceDataPath';

    DROP TABLE tweets;
    CREATE TABLE tweets
    (
        id BIGINT,
        created_at STRING,
        created_at_date STRING,
        created_at_year STRING,
        created_at_month STRING,
        created_at_day STRING,
        created_at_time STRING,
        in_reply_to_user_id_str STRING,
        text STRING,
        contributors STRING,
        retweeted STRING,
        truncated STRING,
        coordinates STRING,
        source STRING,
        retweet_count INT,
        url STRING,
        hashtags array<STRING>,
        user_mentions array<STRING>,
        first_hashtag STRING,
        first_user_mention STRING,
        screen_name STRING,
        name STRING,
        followers_count INT,
        listed_count INT,
        friends_count INT,
        lang STRING,
        user_location STRING,
        time_zone STRING,
        profile_image_url STRING,
        json_response STRING
    );

    FROM tweets_raw
    INSERT OVERWRITE TABLE tweets
    SELECT
        cast(get_json_object(json_response, '$.id_str') as BIGINT),
        get_json_object(json_response, '$.created_at'),
        concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
        substr (get_json_object(json_response, '$.created_at'),27,4)),
        substr (get_json_object(json_response, '$.created_at'),27,4),
        case substr (get_json_object(json_response, '$.created_at'),5,3)
            when "Jan" then "01"
            when "Feb" then "02"
            when "Mar" then "03"
            when "Apr" then "04"
            when "May" then "05"
            when "Jun" then "06"
            when "Jul" then "07"
            when "Aug" then "08"
            when "Sep" then "09"
            when "Oct" then "10"
            when "Nov" then "11"
            when "Dec" then "12" end,
        substr (get_json_object(json_response, '$.created_at'),9,2),
        substr (get_json_object(json_response, '$.created_at'),12,8),
        get_json_object(json_response, '$.in_reply_to_user_id_str'),
        get_json_object(json_response, '$.text'),
        get_json_object(json_response, '$.contributors'),
        get_json_object(json_response, '$.retweeted'),
        get_json_object(json_response, '$.truncated'),
        get_json_object(json_response, '$.coordinates'),
        get_json_object(json_response, '$.source'),
        cast (get_json_object(json_response, '$.retweet_count') as INT),
        get_json_object(json_response, '$.entities.display_url'),
        array(
            trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[1].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[2].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[3].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[4].text')))),
        array(
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[1].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[2].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[3].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[4].screen_name')))),
        trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
        trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
        get_json_object(json_response, '$.user.screen_name'),
        get_json_object(json_response, '$.user.name'),
        cast (get_json_object(json_response, '$.user.followers_count') as INT),
        cast (get_json_object(json_response, '$.user.listed_count') as INT),
        cast (get_json_object(json_response, '$.user.friends_count') as INT),
        get_json_object(json_response, '$.user.lang'),
        get_json_object(json_response, '$.user.location'),
        get_json_object(json_response, '$.user.time_zone'),
        get_json_object(json_response, '$.user.profile_image_url'),
        json_response
    WHERE (length(json_response) > 500);

    INSERT OVERWRITE DIRECTORY '$outputPath'
    SELECT name, screen_name, count(1) as cc
        FROM tweets
        WHERE text like "%Azure%"
        GROUP BY name,screen_name
        ORDER BY cc DESC LIMIT 10;
    "@
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #endregion

    #region - Create a block blob object for writing hello Hive script file
    Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

    Write-Host "Define hello connection string ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    Write-Host "Create block blob objects referencing hello hql script file" -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $hqlScriptBlob = $storageContainer.GetBlockBlobReference($hqlScriptFile)

    Write-Host "Define a MemoryStream and a StreamWriter for writing ... " -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream
    $writeStream.Writeline($hqlStatements)
    #endregion

    #region - Write hello Hive script file tooBlob storage
    Write-Host "Write toohello destination blob ... " -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $hqlScriptBlob.UploadFromStream($memStream)
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. Establecer primero dos variables de hello en el script de Hola:

   | Variable | Description |
   | --- | --- |
   |  $clusterName |Escriba nombre de clúster de HDInsight de Hola donde desea que la aplicación de hello toorun. |
   |  $subscriptionID |Especifique el identificador de su suscripción a Azure. |
   |  $sourceDataPath |Hola donde las consultas de Hive Hola leerá los datos de Hola desde la ubicación de almacenamiento de blobs de Azure. No es necesario toochange esta variable. |
   |  $outputPath |ubicación de almacenamiento de blobs de Azure donde las consultas de Hive Hola generará resultados Hola Hola. No es necesario toochange esta variable. |
   |  $hqlScriptFile |ubicación de Hola y el nombre del archivo de script de HiveQL de Hola Hola. No es necesario toochange esta variable. |
4. Presione **F5** secuencia de comandos de toorun Hola. Si experimenta problemas, como alternativa, seleccione todas las líneas de Hola y, a continuación, presione **F8**.
5. Verá un mensaje de que se ha completado la tarea al final de Hola de salida de hello. Los posibles mensajes de error aparecerán en rojo.

Como procedimiento de validación, puede comprobar el archivo de salida de hello, **/tutorials/twitter/twitter.hql**, en el almacenamiento de blobs de Azure mediante un explorador de almacenamiento de Azure o Azure PowerShell. Para obtener un script de ejemplo de Windows PowerShell de todos los archivos enumerados, consulte [Uso de Blob Storage con HDInsight][hdinsight-storage-powershell].

## <a name="process-twitter-data-by-using-hive"></a>Procesamiento de datos de Twitter mediante Hive
Ha terminado de todos los trabajos de preparación de Hola. Ahora, puede invocar el script de Hive de Hola y Hola resultados de la comprobación.

### <a name="submit-a-hive-job"></a>Envío de un trabajo de Hive
Usar hello siguiente secuencia de comandos de Windows PowerShell script toorun Hola Hive. Necesitará primera variable de tooset Hola.

> [!NOTE]
> Hola toouse tweets y Hola script de HiveQL que cargan en hello las dos últimas secciones, conjunto $hqlScriptFile too"/tutorials/twitter/twitter.hql". Hola toouse los que se han cargado tooa públicos de blobs para usted, establezca $hqlScriptFile demasiado"wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"
$httpUserName = "admin"
$httpUserPassword = "<HDInsight Cluster HTTP User Password>"

#use one of hello following
$hqlScriptFile = "wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql"
$hqlScriptFile = "/tutorials/twitter/twitter.hql"

$statusFolder = "/tutorials/twitter/jobstatus"
#endregion

$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value

$defaultBlobContainerName = $myCluster.DefaultStorageContainer

#region - Invoke Hive
Write-Host "Invoke Hive ... " -ForegroundColor Green

# Create hello HDInsight cluster
$pw = ConvertTo-SecureString -String $httpUserPassword -AsPlainText -Force
$httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

Use-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName -HttpCredential $httpCredential
$response = Invoke-AzureRmHDInsightHiveJob -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -file $hqlScriptFile -StatusFolder $statusFolder #-OutVariable $outVariable

Write-Host "Display hello standard error log ... " -ForegroundColor Green
$jobID = ($response | Select-String job_ | Select-Object -First 1) -replace ‘\s*$’ -replace ‘.*\s’
Get-AzureRmHDInsightJobOutput -ClusterName $clusterName -JobId $jobID -DefaultContainer $defaultBlobContainerName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -HttpCredential $httpCredential
#endregion
```

### <a name="check-hello-results"></a>Resultados de comprobación de Hola
Hola de uso después de la salida de trabajo de Windows PowerShell script toocheck Hola Hive. Deberá primero dos variables de tooset Hola.

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"

$blob = "tutorials/twitter/output/000000_0" # hello name of hello blob toobe downloaded.
#endregion

#region - Create an Azure storage context object
Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
$defaultBlobContainerName = $myCluster.DefaultStorageContainer

Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

Write-Host "Create a context object ... " -ForegroundColor Green
$storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
#endregion

#region - Download blob and display blob
Write-Host "Download hello blob ..." -ForegroundColor Green
cd $HOME
Get-AzureStorageBlobContent -Container $defaultBlobContainerName -Blob $blob -Context $storageContext -Force

Write-Host "Display hello output ..." -ForegroundColor Green
Write-Host "==================================" -ForegroundColor Green
cat "./$blob"
Write-Host "==================================" -ForegroundColor Green
#end region
```

> [!NOTE]
> tabla de Hive Hello usa \001 como Hola delimitador de campo. delimitador de Hello no está visible en la salida de hello.

Después de que los resultados del análisis Hola se han colocado en el almacenamiento de blobs de Azure, puede exportar Hola datos tooan Azure SQL database de SQL server, exportar Hola datos tooExcel mediante Power Query o conectar sus datos de toohello de aplicación mediante el uso de hello Hive el controlador ODBC. Para obtener más información, consulte [Sqoop de uso con HDInsight][hdinsight-use-sqoop], [analizar datos de retrasos de vuelos con HDInsight][hdinsight-analyze-flight-delay-data], [ Conectar Excel tooHDInsight con Power Query][hdinsight-power-query], y [tooHDInsight Excel conectarse con hello Microsoft Hive ODBC Driver][hdinsight-hive-odbc].

## <a name="next-steps"></a>Pasos siguientes
En este tutorial hemos visto cómo tootransform un conjunto de datos no estructurado de JSON en una estructura tooquery de tabla de Hive, explorar y analizar datos de Twitter mediante el uso de HDInsight de Azure. toolearn más información, vea:

* [Introducción a HDInsight][hdinsight-get-started]
* [Análisis de opinión en Twitter en tiempo real con HBase en HDInsight][hdinsight-hbase-twitter-sentiment]
* [Análisis de la información de retraso de vuelos con HDInsight][hdinsight-analyze-flight-delay-data]
* [Conectar Excel tooHDInsight con Power Query][hdinsight-power-query]
* [Conectar Excel tooHDInsight con hello Microsoft Hive ODBC Driver][hdinsight-hive-odbc]
* [Uso de Sqoop con HDInsight][hdinsight-use-sqoop]

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176961.aspx

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]:hdinsight-hadoop-use-blob-storage.md#access-blobs-using-azure-powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
