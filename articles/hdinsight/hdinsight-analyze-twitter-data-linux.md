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
# <a name="analyze-twitter-data-using-hive-and-hadoop-on-hdinsight"></a>Análisis de datos de Twitter con Hive y Hadoop en HDInsight

Obtenga información acerca de cómo toouse Apache Hive tooprocess datos de Twitter. resultado de Hello es una lista de usuarios de Twitter que envían Hola tweets mayoría que contienen una palabra determinada.

> [!IMPORTANT]
> pasos de Hello en este documento se han probado en 3.6 de HDInsight.
>
> Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="get-hello-data"></a>Obtener datos de Hola

Twitter permite hello tooretrieve [datos para cada tweet](https://dev.twitter.com/docs/platform-objects/tweets) como un documento de JavaScript Object Notation (JSON) a través de una API de REST. [OAuth](http://oauth.net) es necesario para la autenticación toohello API.

### <a name="create-a-twitter-application"></a>Crear una aplicación de Twitter

1. Desde un explorador web, inicie sesión en demasiado[https://apps.twitter.com/](https://apps.twitter.com/). Haga clic en hello **Regístrese ahora** vincular si no tienes una cuenta de Twitter.

2. Haga clic en **Crear nueva aplicación**.

3. Especifique los campos **Name** (Nombre), **Description** (Descripción), **Website** (Sitio web). Se pueden realizar hasta una dirección URL para hello **sitio Web** campo. Hello en la tabla siguiente muestra algunos toouse de valores de ejemplo:

   | Campo | Valor |
   |:--- |:--- |
   | Nombre |MyHDInsightApp |
   | Description |MyHDInsightApp |
   | Website |http://www.myhdinsightapp.com |

4. Active **Yes, I agree** (Acepto) y, a continuación, haga clic en **Create your Twitter application** (Crear la aplicación de Twitter).

5. Haga clic en hello **permisos** permiso predeterminado de pestaña hello es **de sólo lectura**.

6. Haga clic en hello **claves y Tokens de acceso** ficha.

7. Haga clic en **Create my access token**(Crear mi token de acceso).

8. Haga clic en **prueba OAuth** en la esquina superior derecha de Hola de página Hola.

9. Rellene los campos **consumer key** (clave del consumidor), **Consumer secret** (Secreto del consumidor), **Access token** (Token de acceso) y **Access token secret** (Secreto del token de acceso).

### <a name="download-tweets"></a>Descarga de tweets

Hola después código Python descarga 10.000 tweets de Twitter y guardarlos con el nombre de archivo de tooa **tweets.txt**.

> [!NOTE]
> Hola pasos se realiza en clúster de HDInsight de hello, puesto que ya está instalado Python.

1. Conecte el clúster de HDInsight de toohello mediante SSH:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Siguiente de hello use comandos tooinstall [Tweepy](http://www.tweepy.org/), [Progressbar](https://pypi.python.org/pypi/progressbar/2.2)y otros paquetes necesarios:

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

4. Comando de uso Hola siguiente toocreate un archivo denominado **gettweets.py**:

   ```bash
   nano gettweets.py
   ```

5. Hola de uso después de texto como contenido de Hola de hello **gettweets.py** archivo:

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
    > Reemplace el texto de marcador de posición de hello para hello siguientes elementos con información de Hola desde su aplicación de twitter:
    >
    > * `consumer_secret`
    > * `consumer_key`
    > * `access_token`
    > * `access_token_secret`

6. Use **Ctrl + X**, a continuación, **Y** archivo de hello toosave.

7. Usar hello siguiente archivo de comandos toorun hello y descargar tweets:

    ```bash
    python gettweets.py
    ```

    Aparece un indicador de progreso. Cuenta % too100 como Hola tweets se descargan.

   > [!NOTE]
   > Si está tardando mucho tiempo para tooadvance de barra de progreso de hello, debe cambiar temas tendencias de hello filtro tootrack. Cuando hay muchas tweets sobre tema hello en el filtro, puede obtener rápidamente Hola 10000 tweets necesarios.

### <a name="upload-hello-data"></a>Cargar datos de Hola

almacenamiento de tooHDInsight de datos de tooupload hello, Hola de uso siguientes comandos:

   ```bash
   hdfs dfs -mkdir -p /tutorials/twitter/data
   hdfs dfs -put tweets.txt /tutorials/twitter/data/tweets.txt
```

Estos comandos almacenan datos de hello en una ubicación que pueden tener acceso todos los nodos de clúster de Hola.

## <a name="run-hello-hiveql-job"></a>Ejecutar trabajo de HiveQL Hola

1. Usar hello siguiente comando toocreate un archivo que contiene instrucciones de HiveQL:

   ```bash
   nano twitter.hql
   ```

    Usar hello después de texto como contenido de Hola de archivo hello:

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

2. Presione **Ctrl + X**, a continuación, presione **Y** archivo de hello toosave.
3. Usar hello después comando toorun hello que hiveql contenido en el archivo hello:

   ```bash
   beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i twitter.hql
   ```

    Este comando se ejecuta Hola Hola **twitter.hql** archivo. Una vez completada la consulta de hello, verá un `jdbc:hive2//localhost:10001/>` símbolo del sistema.

4. Desde el símbolo del sistema de hello beeline, usar hello después tooverify de consulta que se importaron datos:

   ```hiveql
   SELECT name, screen_name, count(1) as cc
       FROM tweets
       WHERE text like "%Azure%"
       GROUP BY name,screen_name
       ORDER BY cc DESC LIMIT 10;
   ```

    Esta consulta devuelve un máximo de 10 tweets que contienen la palabra Hola **Azure** en texto de mensaje de Hola.

## <a name="next-steps"></a>Pasos siguientes

Ha aprendido cómo tootransform un conjunto de datos no estructurado de JSON en una tabla de Hive estructurada. toolearn más información acerca de Hive en HDInsight, vea Hola siguientes documentos:

* [Introducción a HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Análisis de la información de retraso de vuelos con HDInsight](hdinsight-analyze-flight-delay-data-linux.md)

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter
