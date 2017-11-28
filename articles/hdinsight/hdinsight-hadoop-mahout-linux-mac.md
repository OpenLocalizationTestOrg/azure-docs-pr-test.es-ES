---
title: "Generación de recomendaciones mediante Mahout y HDInsight (SSH): Azure| Microsoft Docs"
description: "Aprenda a usar la biblioteca de aprendizaje automático de Apache Mahout para generar recomendaciones de películas con HDInsight (Hadoop)."
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
ms.openlocfilehash: 28450d72f19a5467d88bc787d11f6c37c5afbf9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-linux-based-hadoop-in-hdinsight-ssh"></a><span data-ttu-id="15fad-103">Generación de recomendaciones de películas mediante Apache Mahout con Hadoop en HDInsight basado en Linux</span><span class="sxs-lookup"><span data-stu-id="15fad-103">Generate movie recommendations by using Apache Mahout with Linux-based Hadoop in HDInsight (SSH)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="15fad-104">Aprenda a usar la biblioteca de aprendizaje automático de [Apache Mahout](http://mahout.apache.org) con HDInsight de Azure para generar recomendaciones de películas con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="15fad-104">Learn how to use the [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight to generate movie recommendations.</span></span>

<span data-ttu-id="15fad-105">Mahout es una biblioteca de [aprendizaje automático][ml] para Apache Hadoop.</span><span class="sxs-lookup"><span data-stu-id="15fad-105">Mahout is a [machine learning][ml] library for Apache Hadoop.</span></span> <span data-ttu-id="15fad-106">Mahout contiene algoritmos para el procesamiento de datos, como filtrado, clasificación y agrupación en clústeres.</span><span class="sxs-lookup"><span data-stu-id="15fad-106">Mahout contains algorithms for processing data, such as filtering, classification, and clustering.</span></span> <span data-ttu-id="15fad-107">En este artículo, se usa un motor de recomendaciones para generar recomendaciones de películas que se basan en películas que sus amigos han visto.</span><span class="sxs-lookup"><span data-stu-id="15fad-107">In this article, you use a recommendation engine to generate movie recommendations that are based on movies your friends have seen.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15fad-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="15fad-108">Prerequisites</span></span>

* <span data-ttu-id="15fad-109">Un clúster de HDInsight basado en Linux</span><span class="sxs-lookup"><span data-stu-id="15fad-109">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="15fad-110">Para obtener información sobre cómo crear uno, consulte [Introducción al uso de Hadoop en HDInsight basado en Linux][getstarted].</span><span class="sxs-lookup"><span data-stu-id="15fad-110">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="15fad-111">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="15fad-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="15fad-112">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="15fad-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="15fad-113">Un cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="15fad-113">An SSH client.</span></span> <span data-ttu-id="15fad-114">Para más información, vea el documento [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="15fad-114">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="mahout-versioning"></a><span data-ttu-id="15fad-115">Control de versiones de Mahout</span><span class="sxs-lookup"><span data-stu-id="15fad-115">Mahout versioning</span></span>

<span data-ttu-id="15fad-116">Para más información sobre la versión de Mahout en HDInsight, consulte [Versiones de HDInsight y componentes de Hadoop](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="15fad-116">For more information about the version of Mahout in HDInsight, see [HDInsight versions and Hadoop components](hdinsight-component-versioning.md).</span></span>

## <span data-ttu-id="15fad-117"><a name="recommendations"></a>Descripción de recomendaciones</span><span class="sxs-lookup"><span data-stu-id="15fad-117"><a name="recommendations"></a>Understanding recommendations</span></span>

<span data-ttu-id="15fad-118">Una de las funciones que proporciona Mahout es un motor de recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="15fad-118">One of the functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="15fad-119">Este motor acepta datos en formato de `userID`, `itemId` y `prefValue` (la preferencia por el elemento).</span><span class="sxs-lookup"><span data-stu-id="15fad-119">This engine accepts data in the format of `userID`, `itemId`, and `prefValue` (the preference for the item).</span></span> <span data-ttu-id="15fad-120">Mahout puede realizar entonces análisis de ocurrencias conjuntas para determinar: *los usuarios que tienen predilección por un elemento también la tienen por estos otros elementos*.</span><span class="sxs-lookup"><span data-stu-id="15fad-120">Mahout can then perform co-occurance analysis to determine: *users who have a preference for an item also have a preference for these other items*.</span></span> <span data-ttu-id="15fad-121">Mahout determinará los usuarios con preferencias de elementos similares, lo que se puede usar para realizar recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="15fad-121">Mahout then determines users with like-item preferences, which can be used to make recommendations.</span></span>

<span data-ttu-id="15fad-122">El siguiente flujo de trabajo es un ejemplo simplificado que usa datos de películas:</span><span class="sxs-lookup"><span data-stu-id="15fad-122">The following workflow is a simplified example that uses movie data:</span></span>

* <span data-ttu-id="15fad-123">**Ocurrencia conjunta**: a José, Alicia y Roberto les gusta *La Guerra de las galaxias*, *El imperio contraataca* y *El retorno del Jedi*.</span><span class="sxs-lookup"><span data-stu-id="15fad-123">**Co-occurance**: Joe, Alice, and Bob all liked *Star Wars*, *The Empire Strikes Back*, and *Return of the Jedi*.</span></span> <span data-ttu-id="15fad-124">Mahout determina que a los usuarios que les gusta alguna de estas películas también les gustan las otras dos.</span><span class="sxs-lookup"><span data-stu-id="15fad-124">Mahout determines that users who like any one of these movies also like the other two.</span></span>

* <span data-ttu-id="15fad-125">**Ocurrencia conjunta**: a Roberto y Alicia también les gusta *La amenaza fantasma*, *El ataque de los clones* y *La venganza de los Sith*.</span><span class="sxs-lookup"><span data-stu-id="15fad-125">**Co-occurance**: Bob and Alice also liked *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span></span> <span data-ttu-id="15fad-126">Mahout determina que los usuarios a los que les gustan las tres películas anteriores también les gustan estas tres.</span><span class="sxs-lookup"><span data-stu-id="15fad-126">Mahout determines that users who liked the previous three movies also like these three movies.</span></span>

* <span data-ttu-id="15fad-127">**Recomendación basada en similitud**: como a José le gustan las tres primeras películas, Mahout examina películas que a otros usuarios con preferencias similares les han gustado, pero que José no ha visto (gustado/valorado).</span><span class="sxs-lookup"><span data-stu-id="15fad-127">**Similarity recommendation**: Because Joe liked the first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="15fad-128">En este caso, Mahout recomendaría *La amenaza fantasma*, *El ataque de los clones* y *La venganza de los Sith*.</span><span class="sxs-lookup"><span data-stu-id="15fad-128">In this case, Mahout recommends *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span></span>

### <a name="understanding-the-data"></a><span data-ttu-id="15fad-129">Descripción de los datos</span><span class="sxs-lookup"><span data-stu-id="15fad-129">Understanding the data</span></span>

<span data-ttu-id="15fad-130">Para su comodidad, [GroupLens Research][movielens] proporciona calificaciones de películas en un formato compatible con Mahout.</span><span class="sxs-lookup"><span data-stu-id="15fad-130">Conveniently, [GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="15fad-131">Estos datos están disponibles en el almacenamiento predeterminado del clúster en `/HdiSamples/HdiSamples/MahoutMovieData`.</span><span class="sxs-lookup"><span data-stu-id="15fad-131">This data is available on your cluster's default storage at `/HdiSamples/HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="15fad-132">Hay dos archivos, `moviedb.txt` y `user-ratings.txt`.</span><span class="sxs-lookup"><span data-stu-id="15fad-132">There are two files, `moviedb.txt` and `user-ratings.txt`.</span></span> <span data-ttu-id="15fad-133">El archivo user-ratings.txt se usa durante el análisis, mientras el archivo moviedb.txt se usa para proporcionar información de texto descriptiva al mostrar los resultados del análisis.</span><span class="sxs-lookup"><span data-stu-id="15fad-133">The user-ratings.txt file is used during analysis, while moviedb.txt is used to provide user-friendly text information when displaying the results of the analysis.</span></span>

<span data-ttu-id="15fad-134">Los datos del archivo user-ratings.txt tienen una estructura de `userID`, `movieID`, `userRating` y `timestamp`, que nos indica qué valoración le dio cada usuario a una película.</span><span class="sxs-lookup"><span data-stu-id="15fad-134">The data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="15fad-135">A continuación se muestra un ejemplo de los datos:</span><span class="sxs-lookup"><span data-stu-id="15fad-135">Here is an example of the data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

## <a name="run-the-analysis"></a><span data-ttu-id="15fad-136">Ejecutar el análisis</span><span class="sxs-lookup"><span data-stu-id="15fad-136">Run the analysis</span></span>

<span data-ttu-id="15fad-137">Desde una conexión SSH al clúster, use el siguiente comando para ejecutar el trabajo de recomendación:</span><span class="sxs-lookup"><span data-stu-id="15fad-137">From an SSH connection to the cluster, use the following command to run the recommendation job:</span></span>

```bash
mahout recommenditembased -s SIMILARITY_COOCCURRENCE -i /HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt -o /example/data/mahoutout --tempDir /temp/mahouttemp
```

> [!NOTE]
> <span data-ttu-id="15fad-138">El trabajo puede tardar varios minutos en completarse y puede ejecutar varios trabajos de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="15fad-138">The job may take several minutes to complete, and may run multiple MapReduce jobs.</span></span>

## <a name="view-the-output"></a><span data-ttu-id="15fad-139">Visualización de la salida</span><span class="sxs-lookup"><span data-stu-id="15fad-139">View the output</span></span>

1. <span data-ttu-id="15fad-140">Cuando finalice el trabajo, use el siguiente comando para ver la salida generada.</span><span class="sxs-lookup"><span data-stu-id="15fad-140">Once the job completes, use the following command to view the generated output:</span></span>

    ```bash
    hdfs dfs -text /example/data/mahoutout/part-r-00000
    ```

    <span data-ttu-id="15fad-141">La salida tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="15fad-141">The output appears as follows:</span></span>

        1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
        2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
        3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
        4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

    <span data-ttu-id="15fad-142">La primera columna es `userID`.</span><span class="sxs-lookup"><span data-stu-id="15fad-142">The first column is the `userID`.</span></span> <span data-ttu-id="15fad-143">Los valores contenidos en '[' y ']' son `movieId`:`recommendationScore`.</span><span class="sxs-lookup"><span data-stu-id="15fad-143">The values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

2. <span data-ttu-id="15fad-144">Puede usar el resultado, junto con el archivo moviedb.txt, para ofrecer más información sobre recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="15fad-144">You can use the output, along with the moviedb.txt, to provide more information on the recommendations.</span></span> <span data-ttu-id="15fad-145">En primer lugar, necesitamos copiar los archivos de manera local con los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="15fad-145">First, we need to copy the files locally using the following commands:</span></span>

    ```bash
    hdfs dfs -get /example/data/mahoutout/part-r-00000 recommendations.txt
    hdfs dfs -get /HdiSamples/HdiSamples/MahoutMovieData/* .
    ```

    <span data-ttu-id="15fad-146">Este comando copia los datos de salida a un archivo llamado **recommendations.txt** en el directorio actual, junto con los archivos de datos de la película.</span><span class="sxs-lookup"><span data-stu-id="15fad-146">This command copies the output data to a file named **recommendations.txt** in the current directory, along with the movie data files.</span></span>

3. <span data-ttu-id="15fad-147">Use el siguiente comando para crear un script de Python que busca nombres de película para los datos en la salida de recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="15fad-147">Use the following command to create a Python script that looks up movie names for the data in the recommendations output:</span></span>

    ```bash
    nano show_recommendations.py
    ```

    <span data-ttu-id="15fad-148">Cuando se abra el editor, use el siguiente texto como contenido del archivo:</span><span class="sxs-lookup"><span data-stu-id="15fad-148">When the editor opens, use the following text as the contents of the file:</span></span>

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

    <span data-ttu-id="15fad-149">Presione **Ctrl-X**, **Y** y, finalmente, **Entrar** para guardar los datos.</span><span class="sxs-lookup"><span data-stu-id="15fad-149">Press **Ctrl-X**, **Y**, and finally **Enter** to save the data.</span></span>

4. <span data-ttu-id="15fad-150">Ejecute el script de Python.</span><span class="sxs-lookup"><span data-stu-id="15fad-150">Run the Python script.</span></span> <span data-ttu-id="15fad-151">El siguiente comando da por hecho que está en el directorio donde se descargaron todos los archivos:</span><span class="sxs-lookup"><span data-stu-id="15fad-151">The following command assumes you are in the directory where all the files were downloaded:</span></span>

    ```bash
    python show_recommendations.py 4 user-ratings.txt moviedb.txt recommendations.txt
    ```

    <span data-ttu-id="15fad-152">Este comando busca las recomendaciones generadas para el usuario con el identificador 4.</span><span class="sxs-lookup"><span data-stu-id="15fad-152">This command looks at the recommendations generated for user ID 4.</span></span>

    * <span data-ttu-id="15fad-153">El archivo **user-ratings.txt** se usa para recuperar películas han recibido valoraciones.</span><span class="sxs-lookup"><span data-stu-id="15fad-153">The **user-ratings.txt** file is used to retrieve movies that have been rated.</span></span>

    * <span data-ttu-id="15fad-154">El archivo **moviedb.txt** se usa para recuperar los nombres de las películas.</span><span class="sxs-lookup"><span data-stu-id="15fad-154">The **moviedb.txt** file is used to retrieve the names of the movies.</span></span>

    * <span data-ttu-id="15fad-155">El archivo **recommendations.txt** se usa para recuperar las recomendaciones de películas para este usuario.</span><span class="sxs-lookup"><span data-stu-id="15fad-155">The **recommendations.txt** is used to retrieve the movie recommendations for this user.</span></span>

     <span data-ttu-id="15fad-156">La salida de este comando será similar al siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="15fad-156">The output from this command is similar to the following text:</span></span>

        <span data-ttu-id="15fad-157">Seven Years in Tibet (1997), score=5.0   Indiana Jones and the Last Crusade (1989), score=5.0   Jaws (1975), score=5.0   Sense and Sensibility (1995), score=5.0   Independence Day (ID4) (1996), score=5.0   My Best Friend's Wedding (1997), score=5.0   Jerry Maguire (1996), score=5.0   Scream 2 (1997), score=5.0   Time to Kill, A (1996), score=5.0</span><span class="sxs-lookup"><span data-stu-id="15fad-157">Seven Years in Tibet (1997), score=5.0   Indiana Jones and the Last Crusade (1989), score=5.0   Jaws (1975), score=5.0   Sense and Sensibility (1995), score=5.0   Independence Day (ID4) (1996), score=5.0   My Best Friend's Wedding (1997), score=5.0   Jerry Maguire (1996), score=5.0   Scream 2 (1997), score=5.0   Time to Kill, A (1996), score=5.0</span></span>

## <a name="delete-temporary-data"></a><span data-ttu-id="15fad-158">Eliminar datos temporales</span><span class="sxs-lookup"><span data-stu-id="15fad-158">Delete temporary data</span></span>

<span data-ttu-id="15fad-159">Los trabajos de Mahout no eliminan los datos temporales creados durante el procesamiento del trabajo.</span><span class="sxs-lookup"><span data-stu-id="15fad-159">Mahout jobs do not remove temporary data that is created while processing the job.</span></span> <span data-ttu-id="15fad-160">El parámetro `--tempDir` se especifica en el trabajo de ejemplo para aislar los archivos temporales en una ruta de acceso específica de forma que sea fácil eliminarlos.</span><span class="sxs-lookup"><span data-stu-id="15fad-160">The `--tempDir` parameter is specified in the example job to isolate the temporary files into a specific path for easy deletion.</span></span> <span data-ttu-id="15fad-161">Para quitar los archivos temporales, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="15fad-161">To remove the temp files, use the following command:</span></span>

```bash
hdfs dfs -rm -f -r /temp/mahouttemp
```

> [!WARNING]
> <span data-ttu-id="15fad-162">Si desea volver a ejecutar el comando, también debe eliminar el directorio de salida.</span><span class="sxs-lookup"><span data-stu-id="15fad-162">If you want to run the command again, you must also delete the output directory.</span></span> <span data-ttu-id="15fad-163">Use lo siguiente para eliminar este directorio:</span><span class="sxs-lookup"><span data-stu-id="15fad-163">Use the following to delete this directory:</span></span>
>
> `hdfs dfs -rm -f -r /example/data/mahoutout`


## <a name="next-steps"></a><span data-ttu-id="15fad-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="15fad-164">Next steps</span></span>

<span data-ttu-id="15fad-165">Ahora que ha aprendido a usar a Mahout, descubra otras formas de trabajar con datos en HDInsight:</span><span class="sxs-lookup"><span data-stu-id="15fad-165">Now that you have learned how to use Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="15fad-166">Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="15fad-166">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="15fad-167">Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="15fad-167">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="15fad-168">MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="15fad-168">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

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
