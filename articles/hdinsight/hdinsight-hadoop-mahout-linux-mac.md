---
title: las recomendaciones de aaaGenerate mediante Mahout y HDInsight (SSH) - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola máquina Apache Mahout aprendizaje recomendaciones de película toogenerate de biblioteca con HDInsight (Hadoop)."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c78ec37c-9a8c-4bb6-9e38-0bdb9e89fbd7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: fedac9ceb4268f8421bce4623a5ad271041b8b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-linux-based-hadoop-in-hdinsight-ssh"></a>Generación de recomendaciones de películas mediante Apache Mahout con Hadoop en HDInsight basado en Linux

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

Obtenga información acerca de cómo hello toouse [Mahout Apache](http://mahout.apache.org) biblioteca de aprendizaje de máquina con recomendaciones de película toogenerate de HDInsight de Azure.

Mahout es una biblioteca de [aprendizaje automático][ml] para Apache Hadoop. Mahout contiene algoritmos para el procesamiento de datos, como filtrado, clasificación y agrupación en clústeres. En este artículo, use una recomendación motor toogenerate película las recomendaciones que se basan en las películas que han visto sus amigos.

## <a name="prerequisites"></a>Requisitos previos

* Un clúster de HDInsight basado en Linux Para obtener información sobre cómo crear uno, consulte [Introducción al uso de Hadoop en HDInsight basado en Linux][getstarted].

> [!IMPORTANT]
> Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Un cliente SSH. Para obtener más información, vea hello [utilizar SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.

## <a name="mahout-versioning"></a>Control de versiones de Mahout

Para obtener más información acerca de la versión de Hola de Mahout en HDInsight, vea [HDInsight Hadoop componentes y las versiones](hdinsight-component-versioning.md).

## <a name="recommendations"></a>Descripción de recomendaciones

Una de las funciones hello proporcionada por Mahout es un motor de recomendación. Este motor acepta datos en formato de Hola de `userID`, `itemId`, y `prefValue` (Hola preferencias para el elemento de hello). Mahout, a continuación, puede realizar ocurrencia coadministradores analysis toodetermine: *los usuarios que tienen una preferencia para un elemento también tienen una preferencia para estos otros elementos*. Mahout, a continuación, determina los usuarios con las preferencias de elemento de tipo, que pueden ser usado toomake recomendaciones.

Hola siguiente flujo de trabajo es un ejemplo sencillo que usa datos de la película:

* **Ocurrencia coadministradores**: Joe, Alice y Bob querido todos los *estrella guerras*, *Hola Empire plenos volver*, y *devolución de hello Jedi*. Mahout determina que los usuarios que como cualquiera de estas películas también como Hola otros dos.

* **Ocurrencia coadministradores**: Roberto y Alicia también gustó *Hola fantasma amenaza*, *ataque de Clones de hello*, y *Revenge de hello Sith*. Mahout determina que los usuarios que gustó películas de tres anterior hello también como estos tres películas.

* **Recomendación de similitud**: Joe porque gustó Hola tres primeros de películas, Mahout examina películas que otros usuarios que tengan preferencias similares gustó, pero no observarán Joe (gustó/clasificación). En este caso, se recomienda Mahout *Hola fantasma amenaza*, *ataque de Clones de hello*, y *Revenge de hello Sith*.

### <a name="understanding-hello-data"></a>Descripción de los datos de Hola

Para su comodidad, [GroupLens Research][movielens] proporciona calificaciones de películas en un formato compatible con Mahout. Estos datos están disponibles en el almacenamiento predeterminado del clúster en `/HdiSamples/HdiSamples/MahoutMovieData`.

Hay dos archivos, `moviedb.txt` y `user-ratings.txt`. archivo de usuario ratings.txt Hello se usa durante el análisis, mientras moviedb.txt es información de texto descriptivo de tooprovide usado al mostrar los resultados de Hola de análisis de Hola.

datos de usuario ratings.txt Hello tienen una estructura de `userID`, `movieID`, `userRating`, y `timestamp`, que nos dice cómo alta cada usuario calificado una película. Este es un ejemplo de Hola datos:

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

## <a name="run-hello-analysis"></a>Ejecutar el análisis de Hola

Desde un clúster de toohello de conexión de SSH, use Hola siguiendo el trabajo de comando toorun Hola recomendación:

```bash
mahout recommenditembased -s SIMILARITY_COOCCURRENCE -i /HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt -o /example/data/mahoutout --tempDir /temp/mahouttemp
```

> [!NOTE]
> Hola trabajo puede tardar varios toocomplete minutos y puede ejecutar varios trabajos de MapReduce.

## <a name="view-hello-output"></a>Ver la salida de hello

1. Cuando se completa el trabajo de hello, utilice Hola siguiendo la salida del comando tooview Hola generado:

    ```bash
    hdfs dfs -text /example/data/mahoutout/part-r-00000
    ```

    salida de Hello aparece como sigue:

        1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
        2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
        3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
        4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

    Hola primera columna es hello `userID`. Hola valores contenidos en ' [' y ']' son `movieId`:`recommendationScore`.

2. Puede usar salida de hello, junto con moviedb.txt hello, tooprovide obtener más información acerca de las recomendaciones de Hola. En primer lugar, necesitamos archivos de hello toocopy localmente mediante Hola siguientes comandos:

    ```bash
    hdfs dfs -get /example/data/mahoutout/part-r-00000 recommendations.txt
    hdfs dfs -get /HdiSamples/HdiSamples/MahoutMovieData/* .
    ```

    Este comando copias Hola archivo de tooa de datos de salida denominado **recommendations.txt** en directorio actual de hello, junto con los archivos de datos de película Hola.

3. Usar hello después comando toocreate un script de Python que busca nombres de película para datos de hello en la salida de hello recomendaciones:

    ```bash
    nano show_recommendations.py
    ```

    Cuando se abre el editor de hello, utilice Hola después de texto como contenido de Hola de archivo hello:

   ```python
   #!/usr/bin/env python

   import sys

   if len(sys.argv) != 5:
        print "Arguments: userId userDataFilename movieFilename recommendationFilename"
        sys.exit(1)

   userId, userDataFilename, movieFilename, recommendationFilename = sys.argv[1:]

   print "Reading Movies Descriptions"
   movieFile = open(movieFilename)
   movieById = {}
   for line in movieFile:
       tokens = line.split("|")
       movieById[tokens[0]] = tokens[1:]
   movieFile.close()

   print "Reading Rated Movies"
   userDataFile = open(userDataFilename)
   ratedMovieIds = []
   for line in userDataFile:
       tokens = line.split("\t")
       if tokens[0] == userId:
           ratedMovieIds.append((tokens[1],tokens[2]))
   userDataFile.close()

   print "Reading Recommendations"
   recommendationFile = open(recommendationFilename)
   recommendations = []
   for line in recommendationFile:
       tokens = line.split("\t")
       if tokens[0] == userId:
           movieIdAndScores = tokens[1].strip("[]\n").split(",")
           recommendations = [ movieIdAndScore.split(":") for movieIdAndScore in movieIdAndScores ]
           break
   recommendationFile.close()

   print "Rated Movies"
   print "------------------------"
   for movieId, rating in ratedMovieIds:
       print "%s, rating=%s" % (movieById[movieId][0], rating)
   print "------------------------"

   print "Recommended Movies"
   print "------------------------"
   for movieId, score in recommendations:
       print "%s, score=%s" % (movieById[movieId][0], score)
   print "------------------------"
   ```

    Presione **Ctrl-X**, **Y**y, finalmente, **ENTRAR** toosave datos de saludo.

4. Ejecutar script de Python Hola. Hello siguiente comando presupone que está en directorio de Hola donde se hayan descargado todos los archivos de hello:

    ```bash
    python show_recommendations.py 4 user-ratings.txt moviedb.txt recommendations.txt
    ```

    Este comando examina las recomendaciones de hello generadas para 4 Id. de usuario.

    * Hola **ratings.txt usuario** archivo es utilizado tooretrieve películas que se han clasificado.

    * Hola **moviedb.txt** archivo es utilizado tooretrieve Hola nombres de películas de Hola.

    * Hola **recommendations.txt** es tooretrieve usa las recomendaciones de la película de Hola para este usuario.

     Hola de salida de este comando es similar toohello siguiente texto:

        Puntuación de siete años en Tíbet (1997), = 5.0 hello Crusade última (1989) y Indiana Jones puntuación = 5.0 Jaws (1975), puntuación = 5.0 sentido y sensibilidad (1995), puntuación = 5.0 día de la independencia (ID4) (1996), puntuación = 5.0 mi mejor amigo bodas (1997), puntuación = 5.0 Jerry Maguire (1996 ), puntuación = 5.0 Scream 2 (1997), puntuación = 5.0 tiempo tooKill, (1996), puntuación = 5.0

## <a name="delete-temporary-data"></a>Eliminar datos temporales

Trabajos de Mahout no quite los datos temporales que se crean al procesar el trabajo de Hola. Hola `--tempDir` parámetro se especifica en archivos temporales de hello ejemplo trabajo tooisolate hello en una ruta de acceso específica para su eliminación fácil. archivos temporales de tooremove hello, utilice Hola siguiente comando:

```bash
hdfs dfs -rm -f -r /temp/mahouttemp
```

> [!WARNING]
> Si desea volver a comandos de hello toorun, también debe eliminar el directorio de salida de hello. Usar hello después toodelete este directorio:
>
> `hdfs dfs -rm -f -r /example/data/mahoutout`


## <a name="next-steps"></a>Pasos siguientes

Ahora que ha aprendido cómo toouse Mahout, descubra otras formas de trabajar con datos en HDInsight:

* [Hive con HDInsight](hdinsight-use-hive.md)
* [Pig con HDInsight](hdinsight-use-pig.md)
* [MapReduce con HDInsight](hdinsight-use-mapreduce.md)

[build]: http://mahout.apache.org/developers/buildingmahout.html
[movielens]: http://grouplens.org/datasets/movielens/
[100k]: http://files.grouplens.org/datasets/movielens/ml-100k.zip
[getstarted]: hdinsight-hadoop-linux-tutorial-get-started.md
[upload]: hdinsight-upload-data.md
[ml]: http://en.wikipedia.org/wiki/Machine_learning
[forest]: http://en.wikipedia.org/wiki/Random_forest
[enableremote]: ./media/hdinsight-mahout/enableremote.png
[connect]: ./media/hdinsight-mahout/connect.png
[hadoopcli]: ./media/hdinsight-mahout/hadoopcli.png
[tools]: https://github.com/Blackmist/hdinsight-tools
