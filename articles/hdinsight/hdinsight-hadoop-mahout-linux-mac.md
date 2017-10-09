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
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-linux-based-hadoop-in-hdinsight-ssh"></a><span data-ttu-id="a47e1-103">Generación de recomendaciones de películas mediante Apache Mahout con Hadoop en HDInsight basado en Linux</span><span class="sxs-lookup"><span data-stu-id="a47e1-103">Generate movie recommendations by using Apache Mahout with Linux-based Hadoop in HDInsight (SSH)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="a47e1-104">Obtenga información acerca de cómo hello toouse [Mahout Apache](http://mahout.apache.org) biblioteca de aprendizaje de máquina con recomendaciones de película toogenerate de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="a47e1-104">Learn how toouse hello [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight toogenerate movie recommendations.</span></span>

<span data-ttu-id="a47e1-105">Mahout es una biblioteca de [aprendizaje automático][ml] para Apache Hadoop.</span><span class="sxs-lookup"><span data-stu-id="a47e1-105">Mahout is a [machine learning][ml] library for Apache Hadoop.</span></span> <span data-ttu-id="a47e1-106">Mahout contiene algoritmos para el procesamiento de datos, como filtrado, clasificación y agrupación en clústeres.</span><span class="sxs-lookup"><span data-stu-id="a47e1-106">Mahout contains algorithms for processing data, such as filtering, classification, and clustering.</span></span> <span data-ttu-id="a47e1-107">En este artículo, use una recomendación motor toogenerate película las recomendaciones que se basan en las películas que han visto sus amigos.</span><span class="sxs-lookup"><span data-stu-id="a47e1-107">In this article, you use a recommendation engine toogenerate movie recommendations that are based on movies your friends have seen.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a47e1-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a47e1-108">Prerequisites</span></span>

* <span data-ttu-id="a47e1-109">Un clúster de HDInsight basado en Linux</span><span class="sxs-lookup"><span data-stu-id="a47e1-109">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="a47e1-110">Para obtener información sobre cómo crear uno, consulte [Introducción al uso de Hadoop en HDInsight basado en Linux][getstarted].</span><span class="sxs-lookup"><span data-stu-id="a47e1-110">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a47e1-111">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="a47e1-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a47e1-112">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="a47e1-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="a47e1-113">Un cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="a47e1-113">An SSH client.</span></span> <span data-ttu-id="a47e1-114">Para obtener más información, vea hello [utilizar SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.</span><span class="sxs-lookup"><span data-stu-id="a47e1-114">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="mahout-versioning"></a><span data-ttu-id="a47e1-115">Control de versiones de Mahout</span><span class="sxs-lookup"><span data-stu-id="a47e1-115">Mahout versioning</span></span>

<span data-ttu-id="a47e1-116">Para obtener más información acerca de la versión de Hola de Mahout en HDInsight, vea [HDInsight Hadoop componentes y las versiones](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="a47e1-116">For more information about hello version of Mahout in HDInsight, see [HDInsight versions and Hadoop components](hdinsight-component-versioning.md).</span></span>

## <span data-ttu-id="a47e1-117"><a name="recommendations"></a>Descripción de recomendaciones</span><span class="sxs-lookup"><span data-stu-id="a47e1-117"><a name="recommendations"></a>Understanding recommendations</span></span>

<span data-ttu-id="a47e1-118">Una de las funciones hello proporcionada por Mahout es un motor de recomendación.</span><span class="sxs-lookup"><span data-stu-id="a47e1-118">One of hello functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="a47e1-119">Este motor acepta datos en formato de Hola de `userID`, `itemId`, y `prefValue` (Hola preferencias para el elemento de hello).</span><span class="sxs-lookup"><span data-stu-id="a47e1-119">This engine accepts data in hello format of `userID`, `itemId`, and `prefValue` (hello preference for hello item).</span></span> <span data-ttu-id="a47e1-120">Mahout, a continuación, puede realizar ocurrencia coadministradores analysis toodetermine: *los usuarios que tienen una preferencia para un elemento también tienen una preferencia para estos otros elementos*.</span><span class="sxs-lookup"><span data-stu-id="a47e1-120">Mahout can then perform co-occurance analysis toodetermine: *users who have a preference for an item also have a preference for these other items*.</span></span> <span data-ttu-id="a47e1-121">Mahout, a continuación, determina los usuarios con las preferencias de elemento de tipo, que pueden ser usado toomake recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="a47e1-121">Mahout then determines users with like-item preferences, which can be used toomake recommendations.</span></span>

<span data-ttu-id="a47e1-122">Hola siguiente flujo de trabajo es un ejemplo sencillo que usa datos de la película:</span><span class="sxs-lookup"><span data-stu-id="a47e1-122">hello following workflow is a simplified example that uses movie data:</span></span>

* <span data-ttu-id="a47e1-123">**Ocurrencia coadministradores**: Joe, Alice y Bob querido todos los *estrella guerras*, *Hola Empire plenos volver*, y *devolución de hello Jedi*.</span><span class="sxs-lookup"><span data-stu-id="a47e1-123">**Co-occurance**: Joe, Alice, and Bob all liked *Star Wars*, *hello Empire Strikes Back*, and *Return of hello Jedi*.</span></span> <span data-ttu-id="a47e1-124">Mahout determina que los usuarios que como cualquiera de estas películas también como Hola otros dos.</span><span class="sxs-lookup"><span data-stu-id="a47e1-124">Mahout determines that users who like any one of these movies also like hello other two.</span></span>

* <span data-ttu-id="a47e1-125">**Ocurrencia coadministradores**: Roberto y Alicia también gustó *Hola fantasma amenaza*, *ataque de Clones de hello*, y *Revenge de hello Sith*.</span><span class="sxs-lookup"><span data-stu-id="a47e1-125">**Co-occurance**: Bob and Alice also liked *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span> <span data-ttu-id="a47e1-126">Mahout determina que los usuarios que gustó películas de tres anterior hello también como estos tres películas.</span><span class="sxs-lookup"><span data-stu-id="a47e1-126">Mahout determines that users who liked hello previous three movies also like these three movies.</span></span>

* <span data-ttu-id="a47e1-127">**Recomendación de similitud**: Joe porque gustó Hola tres primeros de películas, Mahout examina películas que otros usuarios que tengan preferencias similares gustó, pero no observarán Joe (gustó/clasificación).</span><span class="sxs-lookup"><span data-stu-id="a47e1-127">**Similarity recommendation**: Because Joe liked hello first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="a47e1-128">En este caso, se recomienda Mahout *Hola fantasma amenaza*, *ataque de Clones de hello*, y *Revenge de hello Sith*.</span><span class="sxs-lookup"><span data-stu-id="a47e1-128">In this case, Mahout recommends *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span>

### <a name="understanding-hello-data"></a><span data-ttu-id="a47e1-129">Descripción de los datos de Hola</span><span class="sxs-lookup"><span data-stu-id="a47e1-129">Understanding hello data</span></span>

<span data-ttu-id="a47e1-130">Para su comodidad, [GroupLens Research][movielens] proporciona calificaciones de películas en un formato compatible con Mahout.</span><span class="sxs-lookup"><span data-stu-id="a47e1-130">Conveniently, [GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="a47e1-131">Estos datos están disponibles en el almacenamiento predeterminado del clúster en `/HdiSamples/HdiSamples/MahoutMovieData`.</span><span class="sxs-lookup"><span data-stu-id="a47e1-131">This data is available on your cluster's default storage at `/HdiSamples/HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="a47e1-132">Hay dos archivos, `moviedb.txt` y `user-ratings.txt`.</span><span class="sxs-lookup"><span data-stu-id="a47e1-132">There are two files, `moviedb.txt` and `user-ratings.txt`.</span></span> <span data-ttu-id="a47e1-133">archivo de usuario ratings.txt Hello se usa durante el análisis, mientras moviedb.txt es información de texto descriptivo de tooprovide usado al mostrar los resultados de Hola de análisis de Hola.</span><span class="sxs-lookup"><span data-stu-id="a47e1-133">hello user-ratings.txt file is used during analysis, while moviedb.txt is used tooprovide user-friendly text information when displaying hello results of hello analysis.</span></span>

<span data-ttu-id="a47e1-134">datos de usuario ratings.txt Hello tienen una estructura de `userID`, `movieID`, `userRating`, y `timestamp`, que nos dice cómo alta cada usuario calificado una película.</span><span class="sxs-lookup"><span data-stu-id="a47e1-134">hello data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="a47e1-135">Este es un ejemplo de Hola datos:</span><span class="sxs-lookup"><span data-stu-id="a47e1-135">Here is an example of hello data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

## <a name="run-hello-analysis"></a><span data-ttu-id="a47e1-136">Ejecutar el análisis de Hola</span><span class="sxs-lookup"><span data-stu-id="a47e1-136">Run hello analysis</span></span>

<span data-ttu-id="a47e1-137">Desde un clúster de toohello de conexión de SSH, use Hola siguiendo el trabajo de comando toorun Hola recomendación:</span><span class="sxs-lookup"><span data-stu-id="a47e1-137">From an SSH connection toohello cluster, use hello following command toorun hello recommendation job:</span></span>

```bash
mahout recommenditembased -s SIMILARITY_COOCCURRENCE -i /HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt -o /example/data/mahoutout --tempDir /temp/mahouttemp
```

> [!NOTE]
> <span data-ttu-id="a47e1-138">Hola trabajo puede tardar varios toocomplete minutos y puede ejecutar varios trabajos de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="a47e1-138">hello job may take several minutes toocomplete, and may run multiple MapReduce jobs.</span></span>

## <a name="view-hello-output"></a><span data-ttu-id="a47e1-139">Ver la salida de hello</span><span class="sxs-lookup"><span data-stu-id="a47e1-139">View hello output</span></span>

1. <span data-ttu-id="a47e1-140">Cuando se completa el trabajo de hello, utilice Hola siguiendo la salida del comando tooview Hola generado:</span><span class="sxs-lookup"><span data-stu-id="a47e1-140">Once hello job completes, use hello following command tooview hello generated output:</span></span>

    ```bash
    hdfs dfs -text /example/data/mahoutout/part-r-00000
    ```

    <span data-ttu-id="a47e1-141">salida de Hello aparece como sigue:</span><span class="sxs-lookup"><span data-stu-id="a47e1-141">hello output appears as follows:</span></span>

        1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
        2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
        3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
        4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

    <span data-ttu-id="a47e1-142">Hola primera columna es hello `userID`.</span><span class="sxs-lookup"><span data-stu-id="a47e1-142">hello first column is hello `userID`.</span></span> <span data-ttu-id="a47e1-143">Hola valores contenidos en ' [' y ']' son `movieId`:`recommendationScore`.</span><span class="sxs-lookup"><span data-stu-id="a47e1-143">hello values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

2. <span data-ttu-id="a47e1-144">Puede usar salida de hello, junto con moviedb.txt hello, tooprovide obtener más información acerca de las recomendaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="a47e1-144">You can use hello output, along with hello moviedb.txt, tooprovide more information on hello recommendations.</span></span> <span data-ttu-id="a47e1-145">En primer lugar, necesitamos archivos de hello toocopy localmente mediante Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="a47e1-145">First, we need toocopy hello files locally using hello following commands:</span></span>

    ```bash
    hdfs dfs -get /example/data/mahoutout/part-r-00000 recommendations.txt
    hdfs dfs -get /HdiSamples/HdiSamples/MahoutMovieData/* .
    ```

    <span data-ttu-id="a47e1-146">Este comando copias Hola archivo de tooa de datos de salida denominado **recommendations.txt** en directorio actual de hello, junto con los archivos de datos de película Hola.</span><span class="sxs-lookup"><span data-stu-id="a47e1-146">This command copies hello output data tooa file named **recommendations.txt** in hello current directory, along with hello movie data files.</span></span>

3. <span data-ttu-id="a47e1-147">Usar hello después comando toocreate un script de Python que busca nombres de película para datos de hello en la salida de hello recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="a47e1-147">Use hello following command toocreate a Python script that looks up movie names for hello data in hello recommendations output:</span></span>

    ```bash
    nano show_recommendations.py
    ```

    <span data-ttu-id="a47e1-148">Cuando se abre el editor de hello, utilice Hola después de texto como contenido de Hola de archivo hello:</span><span class="sxs-lookup"><span data-stu-id="a47e1-148">When hello editor opens, use hello following text as hello contents of hello file:</span></span>

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

    <span data-ttu-id="a47e1-149">Presione **Ctrl-X**, **Y**y, finalmente, **ENTRAR** toosave datos de saludo.</span><span class="sxs-lookup"><span data-stu-id="a47e1-149">Press **Ctrl-X**, **Y**, and finally **Enter** toosave hello data.</span></span>

4. <span data-ttu-id="a47e1-150">Ejecutar script de Python Hola.</span><span class="sxs-lookup"><span data-stu-id="a47e1-150">Run hello Python script.</span></span> <span data-ttu-id="a47e1-151">Hello siguiente comando presupone que está en directorio de Hola donde se hayan descargado todos los archivos de hello:</span><span class="sxs-lookup"><span data-stu-id="a47e1-151">hello following command assumes you are in hello directory where all hello files were downloaded:</span></span>

    ```bash
    python show_recommendations.py 4 user-ratings.txt moviedb.txt recommendations.txt
    ```

    <span data-ttu-id="a47e1-152">Este comando examina las recomendaciones de hello generadas para 4 Id. de usuario.</span><span class="sxs-lookup"><span data-stu-id="a47e1-152">This command looks at hello recommendations generated for user ID 4.</span></span>

    * <span data-ttu-id="a47e1-153">Hola **ratings.txt usuario** archivo es utilizado tooretrieve películas que se han clasificado.</span><span class="sxs-lookup"><span data-stu-id="a47e1-153">hello **user-ratings.txt** file is used tooretrieve movies that have been rated.</span></span>

    * <span data-ttu-id="a47e1-154">Hola **moviedb.txt** archivo es utilizado tooretrieve Hola nombres de películas de Hola.</span><span class="sxs-lookup"><span data-stu-id="a47e1-154">hello **moviedb.txt** file is used tooretrieve hello names of hello movies.</span></span>

    * <span data-ttu-id="a47e1-155">Hola **recommendations.txt** es tooretrieve usa las recomendaciones de la película de Hola para este usuario.</span><span class="sxs-lookup"><span data-stu-id="a47e1-155">hello **recommendations.txt** is used tooretrieve hello movie recommendations for this user.</span></span>

     <span data-ttu-id="a47e1-156">Hola de salida de este comando es similar toohello siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="a47e1-156">hello output from this command is similar toohello following text:</span></span>

        <span data-ttu-id="a47e1-157">Puntuación de siete años en Tíbet (1997), = 5.0 hello Crusade última (1989) y Indiana Jones puntuación = 5.0 Jaws (1975), puntuación = 5.0 sentido y sensibilidad (1995), puntuación = 5.0 día de la independencia (ID4) (1996), puntuación = 5.0 mi mejor amigo bodas (1997), puntuación = 5.0 Jerry Maguire (1996 ), puntuación = 5.0 Scream 2 (1997), puntuación = 5.0 tiempo tooKill, (1996), puntuación = 5.0</span><span class="sxs-lookup"><span data-stu-id="a47e1-157">Seven Years in Tibet (1997), score=5.0   Indiana Jones and hello Last Crusade (1989), score=5.0   Jaws (1975), score=5.0   Sense and Sensibility (1995), score=5.0   Independence Day (ID4) (1996), score=5.0   My Best Friend's Wedding (1997), score=5.0   Jerry Maguire (1996), score=5.0   Scream 2 (1997), score=5.0   Time tooKill, A (1996), score=5.0</span></span>

## <a name="delete-temporary-data"></a><span data-ttu-id="a47e1-158">Eliminar datos temporales</span><span class="sxs-lookup"><span data-stu-id="a47e1-158">Delete temporary data</span></span>

<span data-ttu-id="a47e1-159">Trabajos de Mahout no quite los datos temporales que se crean al procesar el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a47e1-159">Mahout jobs do not remove temporary data that is created while processing hello job.</span></span> <span data-ttu-id="a47e1-160">Hola `--tempDir` parámetro se especifica en archivos temporales de hello ejemplo trabajo tooisolate hello en una ruta de acceso específica para su eliminación fácil.</span><span class="sxs-lookup"><span data-stu-id="a47e1-160">hello `--tempDir` parameter is specified in hello example job tooisolate hello temporary files into a specific path for easy deletion.</span></span> <span data-ttu-id="a47e1-161">archivos temporales de tooremove hello, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a47e1-161">tooremove hello temp files, use hello following command:</span></span>

```bash
hdfs dfs -rm -f -r /temp/mahouttemp
```

> [!WARNING]
> <span data-ttu-id="a47e1-162">Si desea volver a comandos de hello toorun, también debe eliminar el directorio de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="a47e1-162">If you want toorun hello command again, you must also delete hello output directory.</span></span> <span data-ttu-id="a47e1-163">Usar hello después toodelete este directorio:</span><span class="sxs-lookup"><span data-stu-id="a47e1-163">Use hello following toodelete this directory:</span></span>
>
> `hdfs dfs -rm -f -r /example/data/mahoutout`


## <a name="next-steps"></a><span data-ttu-id="a47e1-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a47e1-164">Next steps</span></span>

<span data-ttu-id="a47e1-165">Ahora que ha aprendido cómo toouse Mahout, descubra otras formas de trabajar con datos en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a47e1-165">Now that you have learned how toouse Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="a47e1-166">Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="a47e1-166">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="a47e1-167">Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="a47e1-167">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="a47e1-168">MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="a47e1-168">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

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
