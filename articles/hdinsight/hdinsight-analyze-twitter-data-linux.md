---
title: aaaAnalyze datos de Twitter con Apache Hive - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse usar Hive y Hadoop en HDInsight tootransform datos sin procesar de TWitter en una tabla de Hive permite realizar búsqueda."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e1e249ed-5f57-40d6-b3bc-a1b4d9a871d3
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 02c4d027c7bbf390ac1c3724c14f8d549ea5195e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-twitter-data-using-hive-and-hadoop-on-hdinsight"></a><span data-ttu-id="e33ec-103">Análisis de datos de Twitter con Hive y Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="e33ec-103">Analyze Twitter data using Hive and Hadoop on HDInsight</span></span>

<span data-ttu-id="e33ec-104">Obtenga información acerca de cómo toouse Apache Hive tooprocess datos de Twitter.</span><span class="sxs-lookup"><span data-stu-id="e33ec-104">Learn how toouse Apache Hive tooprocess Twitter data.</span></span> <span data-ttu-id="e33ec-105">resultado de Hello es una lista de usuarios de Twitter que envían Hola tweets mayoría que contienen una palabra determinada.</span><span class="sxs-lookup"><span data-stu-id="e33ec-105">hello result is a list of Twitter users who sent hello most tweets that contain a certain word.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e33ec-106">pasos de Hello en este documento se han probado en 3.6 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e33ec-106">hello steps in this document were tested on HDInsight 3.6.</span></span>
>
> <span data-ttu-id="e33ec-107">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="e33ec-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e33ec-108">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="e33ec-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="get-hello-data"></a><span data-ttu-id="e33ec-109">Obtener datos de Hola</span><span class="sxs-lookup"><span data-stu-id="e33ec-109">Get hello data</span></span>

<span data-ttu-id="e33ec-110">Twitter permite hello tooretrieve [datos para cada tweet](https://dev.twitter.com/docs/platform-objects/tweets) como un documento de JavaScript Object Notation (JSON) a través de una API de REST.</span><span class="sxs-lookup"><span data-stu-id="e33ec-110">Twitter allows you tooretrieve hello [data for each tweet](https://dev.twitter.com/docs/platform-objects/tweets) as a JavaScript Object Notation (JSON) document through a REST API.</span></span> <span data-ttu-id="e33ec-111">[OAuth](http://oauth.net) es necesario para la autenticación toohello API.</span><span class="sxs-lookup"><span data-stu-id="e33ec-111">[OAuth](http://oauth.net) is required for authentication toohello API.</span></span>

### <a name="create-a-twitter-application"></a><span data-ttu-id="e33ec-112">Crear una aplicación de Twitter</span><span class="sxs-lookup"><span data-stu-id="e33ec-112">Create a Twitter application</span></span>

1. <span data-ttu-id="e33ec-113">Desde un explorador web, inicie sesión en demasiado[https://apps.twitter.com/](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="e33ec-113">From a web browser, sign in too[https://apps.twitter.com/](https://apps.twitter.com/).</span></span> <span data-ttu-id="e33ec-114">Haga clic en hello **Regístrese ahora** vincular si no tienes una cuenta de Twitter.</span><span class="sxs-lookup"><span data-stu-id="e33ec-114">Click hello **Sign-up now** link if you don't have a Twitter account.</span></span>

2. <span data-ttu-id="e33ec-115">Haga clic en **Crear nueva aplicación**.</span><span class="sxs-lookup"><span data-stu-id="e33ec-115">Click **Create New App**.</span></span>

3. <span data-ttu-id="e33ec-116">Especifique los campos **Name** (Nombre), **Description** (Descripción), **Website** (Sitio web).</span><span class="sxs-lookup"><span data-stu-id="e33ec-116">Enter **Name**, **Description**, **Website**.</span></span> <span data-ttu-id="e33ec-117">Se pueden realizar hasta una dirección URL para hello **sitio Web** campo.</span><span class="sxs-lookup"><span data-stu-id="e33ec-117">You can make up a URL for hello **Website** field.</span></span> <span data-ttu-id="e33ec-118">Hello en la tabla siguiente muestra algunos toouse de valores de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e33ec-118">hello following table shows some sample values toouse:</span></span>

   | <span data-ttu-id="e33ec-119">Campo</span><span class="sxs-lookup"><span data-stu-id="e33ec-119">Field</span></span> | <span data-ttu-id="e33ec-120">Valor</span><span class="sxs-lookup"><span data-stu-id="e33ec-120">Value</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="e33ec-121">Nombre</span><span class="sxs-lookup"><span data-stu-id="e33ec-121">Name</span></span> |<span data-ttu-id="e33ec-122">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="e33ec-122">MyHDInsightApp</span></span> |
   | <span data-ttu-id="e33ec-123">Description</span><span class="sxs-lookup"><span data-stu-id="e33ec-123">Description</span></span> |<span data-ttu-id="e33ec-124">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="e33ec-124">MyHDInsightApp</span></span> |
   | <span data-ttu-id="e33ec-125">Website</span><span class="sxs-lookup"><span data-stu-id="e33ec-125">Website</span></span> |<span data-ttu-id="e33ec-126">http://www.myhdinsightapp.com</span><span class="sxs-lookup"><span data-stu-id="e33ec-126">http://www.myhdinsightapp.com</span></span> |

4. <span data-ttu-id="e33ec-127">Active **Yes, I agree** (Acepto) y, a continuación, haga clic en **Create your Twitter application** (Crear la aplicación de Twitter).</span><span class="sxs-lookup"><span data-stu-id="e33ec-127">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>

5. <span data-ttu-id="e33ec-128">Haga clic en hello **permisos** permiso predeterminado de pestaña hello es **de sólo lectura**.</span><span class="sxs-lookup"><span data-stu-id="e33ec-128">Click hello **Permissions** tab. hello default permission is **Read only**.</span></span>

6. <span data-ttu-id="e33ec-129">Haga clic en hello **claves y Tokens de acceso** ficha.</span><span class="sxs-lookup"><span data-stu-id="e33ec-129">Click hello **Keys and Access Tokens** tab.</span></span>

7. <span data-ttu-id="e33ec-130">Haga clic en **Create my access token**(Crear mi token de acceso).</span><span class="sxs-lookup"><span data-stu-id="e33ec-130">Click **Create my access token**.</span></span>

8. <span data-ttu-id="e33ec-131">Haga clic en **prueba OAuth** en la esquina superior derecha de Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="e33ec-131">Click **Test OAuth** in hello upper-right corner of hello page.</span></span>

9. <span data-ttu-id="e33ec-132">Rellene los campos **consumer key** (clave del consumidor), **Consumer secret** (Secreto del consumidor), **Access token** (Token de acceso) y **Access token secret** (Secreto del token de acceso).</span><span class="sxs-lookup"><span data-stu-id="e33ec-132">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span></span>

### <a name="download-tweets"></a><span data-ttu-id="e33ec-133">Descarga de tweets</span><span class="sxs-lookup"><span data-stu-id="e33ec-133">Download tweets</span></span>

<span data-ttu-id="e33ec-134">Hola después código Python descarga 10.000 tweets de Twitter y guardarlos con el nombre de archivo de tooa **tweets.txt**.</span><span class="sxs-lookup"><span data-stu-id="e33ec-134">hello following Python code downloads 10,000 tweets from Twitter and save them tooa file named **tweets.txt**.</span></span>

> [!NOTE]
> <span data-ttu-id="e33ec-135">Hola pasos se realiza en clúster de HDInsight de hello, puesto que ya está instalado Python.</span><span class="sxs-lookup"><span data-stu-id="e33ec-135">hello following steps are performed on hello HDInsight cluster, since Python is already installed.</span></span>

1. <span data-ttu-id="e33ec-136">Conecte el clúster de HDInsight de toohello mediante SSH:</span><span class="sxs-lookup"><span data-stu-id="e33ec-136">Connect toohello HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="e33ec-137">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e33ec-137">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="e33ec-138">Siguiente de hello use comandos tooinstall [Tweepy](http://www.tweepy.org/), [Progressbar](https://pypi.python.org/pypi/progressbar/2.2)y otros paquetes necesarios:</span><span class="sxs-lookup"><span data-stu-id="e33ec-138">Use hello following commands tooinstall [Tweepy](http://www.tweepy.org/), [Progressbar](https://pypi.python.org/pypi/progressbar/2.2), and other required packages:</span></span>

   ```bash
   sudo apt install python-dev libffi-dev libssl-dev
   sudo apt remove python-openssl
   pip install virtualenv
   mkdir gettweets
   cd gettweets
   virtualenv gettweets
   source gettweets/bin/activate
   pip install tweepy progressbar pyOpenSSL requests[security]
   ```

4. <span data-ttu-id="e33ec-139">Comando de uso Hola siguiente toocreate un archivo denominado **gettweets.py**:</span><span class="sxs-lookup"><span data-stu-id="e33ec-139">Use hello following command toocreate a file named **gettweets.py**:</span></span>

   ```bash
   nano gettweets.py
   ```

5. <span data-ttu-id="e33ec-140">Hola de uso después de texto como contenido de Hola de hello **gettweets.py** archivo:</span><span class="sxs-lookup"><span data-stu-id="e33ec-140">Use hello following text as hello contents of hello **gettweets.py** file:</span></span>

   ```python
   #!/usr/bin/python

   from tweepy import Stream, OAuthHandler
   from tweepy.streaming import StreamListener
   from progressbar import ProgressBar, Percentage, Bar
   import json
   import sys

   #Twitter app information
   consumer_secret='Your consumer secret'
   consumer_key='Your consumer key'
   access_token='Your access token'
   access_token_secret='Your access token secret'

   #hello number of tweets we want tooget
   max_tweets=10000

   #Create hello listener class that receives and saves tweets
   class listener(StreamListener):
       #On init, set hello counter toozero and create a progress bar
       def __init__(self, api=None):
           self.num_tweets = 0
           self.pbar = ProgressBar(widgets=[Percentage(), Bar()], maxval=max_tweets).start()

       #When data is received, do this
       def on_data(self, data):
           #Append hello tweet toohello 'tweets.txt' file
           with open('tweets.txt', 'a') as tweet_file:
               tweet_file.write(data)
               #Increment hello number of tweets
               self.num_tweets += 1
               #Check toosee if we have hit max_tweets and exit if so
               if self.num_tweets >= max_tweets:
                   self.pbar.finish()
                   sys.exit(0)
               else:
                   #increment hello progress bar
                   self.pbar.update(self.num_tweets)
           return True

       #Handle any errors that may occur
       def on_error(self, status):
           print status

   #Get hello OAuth token
   auth = OAuthHandler(consumer_key, consumer_secret)
   auth.set_access_token(access_token, access_token_secret)
   #Use hello listener class for stream processing
   twitterStream = Stream(auth, listener())
   #Filter for these topics
   twitterStream.filter(track=["azure","cloud","hdinsight"])
   ```

    > [!IMPORTANT]
    > <span data-ttu-id="e33ec-141">Reemplace el texto de marcador de posición de hello para hello siguientes elementos con información de Hola desde su aplicación de twitter:</span><span class="sxs-lookup"><span data-stu-id="e33ec-141">Replace hello placeholder text for hello following items with hello information from your twitter application:</span></span>
    >
    > * `consumer_secret`
    > * `consumer_key`
    > * `access_token`
    > * `access_token_secret`

6. <span data-ttu-id="e33ec-142">Use **Ctrl + X**, a continuación, **Y** archivo de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="e33ec-142">Use **Ctrl + X**, then **Y** toosave hello file.</span></span>

7. <span data-ttu-id="e33ec-143">Usar hello siguiente archivo de comandos toorun hello y descargar tweets:</span><span class="sxs-lookup"><span data-stu-id="e33ec-143">Use hello following command toorun hello file and download tweets:</span></span>

    ```bash
    python gettweets.py
    ```

    <span data-ttu-id="e33ec-144">Aparece un indicador de progreso.</span><span class="sxs-lookup"><span data-stu-id="e33ec-144">A progress indicator appears.</span></span> <span data-ttu-id="e33ec-145">Cuenta % too100 como Hola tweets se descargan.</span><span class="sxs-lookup"><span data-stu-id="e33ec-145">It counts up too100% as hello tweets are downloaded.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e33ec-146">Si está tardando mucho tiempo para tooadvance de barra de progreso de hello, debe cambiar temas tendencias de hello filtro tootrack.</span><span class="sxs-lookup"><span data-stu-id="e33ec-146">If it is taking a long time for hello progress bar tooadvance, you should change hello filter tootrack trending topics.</span></span> <span data-ttu-id="e33ec-147">Cuando hay muchas tweets sobre tema hello en el filtro, puede obtener rápidamente Hola 10000 tweets necesarios.</span><span class="sxs-lookup"><span data-stu-id="e33ec-147">When there are many tweets about hello topic in your filter, you can quickly get hello 10000 tweets needed.</span></span>

### <a name="upload-hello-data"></a><span data-ttu-id="e33ec-148">Cargar datos de Hola</span><span class="sxs-lookup"><span data-stu-id="e33ec-148">Upload hello data</span></span>

<span data-ttu-id="e33ec-149">almacenamiento de tooHDInsight de datos de tooupload hello, Hola de uso siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="e33ec-149">tooupload hello data tooHDInsight storage, use hello following commands:</span></span>

   ```bash
   hdfs dfs -mkdir -p /tutorials/twitter/data
   hdfs dfs -put tweets.txt /tutorials/twitter/data/tweets.txt
```

<span data-ttu-id="e33ec-150">Estos comandos almacenan datos de hello en una ubicación que pueden tener acceso todos los nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="e33ec-150">These commands store hello data in a location that all nodes in hello cluster can access.</span></span>

## <a name="run-hello-hiveql-job"></a><span data-ttu-id="e33ec-151">Ejecutar trabajo de HiveQL Hola</span><span class="sxs-lookup"><span data-stu-id="e33ec-151">Run hello HiveQL job</span></span>

1. <span data-ttu-id="e33ec-152">Usar hello siguiente comando toocreate un archivo que contiene instrucciones de HiveQL:</span><span class="sxs-lookup"><span data-stu-id="e33ec-152">Use hello following command toocreate a file containing HiveQL statements:</span></span>

   ```bash
   nano twitter.hql
   ```

    <span data-ttu-id="e33ec-153">Usar hello después de texto como contenido de Hola de archivo hello:</span><span class="sxs-lookup"><span data-stu-id="e33ec-153">Use hello following text as hello contents of hello file:</span></span>

   ```hiveql
   set hive.exec.dynamic.partition = true;
   set hive.exec.dynamic.partition.mode = nonstrict;
   -- Drop table, if it exists
   DROP TABLE tweets_raw;
   -- Create it, pointing toward hello tweets logged from Twitter
   CREATE EXTERNAL TABLE tweets_raw (
       json_response STRING
   )
   STORED AS TEXTFILE LOCATION '/tutorials/twitter/data';
   -- Drop and recreate hello destination table
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
   -- Select tweets from hello imported data, parse hello JSON,
   -- and insert into hello tweets table
   FROM tweets_raw
   INSERT OVERWRITE TABLE tweets
   SELECT
       cast(get_json_object(json_response, '$.id_str') as BIGINT),
       get_json_object(json_response, '$.created_at'),
       concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
       substr (get_json_object(json_response, '$.created_at'),27,4)),
       substr (get_json_object(json_response, '$.created_at'),27,4),
       case substr (get_json_object(json_response,    '$.created_at'),5,3)
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
   ```

2. <span data-ttu-id="e33ec-154">Presione **Ctrl + X**, a continuación, presione **Y** archivo de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="e33ec-154">Press **Ctrl + X**, then press **Y** toosave hello file.</span></span>
3. <span data-ttu-id="e33ec-155">Usar hello después comando toorun hello que hiveql contenido en el archivo hello:</span><span class="sxs-lookup"><span data-stu-id="e33ec-155">Use hello following command toorun hello HiveQL contained in hello file:</span></span>

   ```bash
   beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i twitter.hql
   ```

    <span data-ttu-id="e33ec-156">Este comando se ejecuta Hola Hola **twitter.hql** archivo.</span><span class="sxs-lookup"><span data-stu-id="e33ec-156">This command runs hello hello **twitter.hql** file.</span></span> <span data-ttu-id="e33ec-157">Una vez completada la consulta de hello, verá un `jdbc:hive2//localhost:10001/>` símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="e33ec-157">Once hello query completes, you see a `jdbc:hive2//localhost:10001/>` prompt.</span></span>

4. <span data-ttu-id="e33ec-158">Desde el símbolo del sistema de hello beeline, usar hello después tooverify de consulta que se importaron datos:</span><span class="sxs-lookup"><span data-stu-id="e33ec-158">From hello beeline prompt, use hello following query tooverify that data was imported:</span></span>

   ```hiveql
   SELECT name, screen_name, count(1) as cc
       FROM tweets
       WHERE text like "%Azure%"
       GROUP BY name,screen_name
       ORDER BY cc DESC LIMIT 10;
   ```

    <span data-ttu-id="e33ec-159">Esta consulta devuelve un máximo de 10 tweets que contienen la palabra Hola **Azure** en texto de mensaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="e33ec-159">This query returns a maximum of 10 tweets that contain hello word **Azure** in hello message text.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e33ec-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e33ec-160">Next steps</span></span>

<span data-ttu-id="e33ec-161">Ha aprendido cómo tootransform un conjunto de datos no estructurado de JSON en una tabla de Hive estructurada.</span><span class="sxs-lookup"><span data-stu-id="e33ec-161">You have learned how tootransform an unstructured JSON dataset into a structured Hive table.</span></span> <span data-ttu-id="e33ec-162">toolearn más información acerca de Hive en HDInsight, vea Hola siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="e33ec-162">toolearn more about Hive on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="e33ec-163">Introducción a HDInsight</span><span class="sxs-lookup"><span data-stu-id="e33ec-163">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="e33ec-164">Análisis de la información de retraso de vuelos con HDInsight</span><span class="sxs-lookup"><span data-stu-id="e33ec-164">Analyze flight delay data using HDInsight</span></span>](hdinsight-analyze-flight-delay-data-linux.md)

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter
