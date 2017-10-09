---
title: aaaUse C# con MapReduce en Hadoop en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse C# toocreate MapReduce soluciones con Hadoop en HDInsight de Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.custom: hdinsightactive
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: dd8b684e74155bc1a37d4ab8d6f9033276ef5aa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-with-mapreduce-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="0d9ce-103">Uso de C# con el streaming de MapReduce en Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="0d9ce-103">Use C# with MapReduce streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="0d9ce-104">Obtenga información acerca de cómo toouse C# toocreate una solución de MapReduce en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-104">Learn how toouse C# toocreate a MapReduce solution on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0d9ce-105">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-105">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0d9ce-106">Para obtener más información, consulte el artículo relativo al [control de versiones de componentes de HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="0d9ce-106">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="0d9ce-107">Streaming de Hadoop es una utilidad que le permite toorun MapReduce trabajos mediante un script o un archivo ejecutable.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-107">Hadoop streaming is a utility that allows you toorun MapReduce jobs using a script or executable.</span></span> <span data-ttu-id="0d9ce-108">En este ejemplo, .NET es tooimplement usado Hola asignador y reductor para una solución de recuento de palabras.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-108">In this example, .NET is used tooimplement hello mapper and reducer for a word count solution.</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="0d9ce-109">.NET en HDInsight</span><span class="sxs-lookup"><span data-stu-id="0d9ce-109">.NET on HDInsight</span></span>

<span data-ttu-id="0d9ce-110">__HDInsight basados en Linux__ clústeres uso [Mono (https://mono-project.com)](https://mono-project.com) toorun aplicaciones. NET.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-110">__Linux-based HDInsight__ clusters use [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="0d9ce-111">La versión 4.2.1 de Mono está incluida en la versión 3.5 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-111">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="0d9ce-112">Para obtener más información sobre la versión de Hola de Mono incluido con HDInsight, vea [versiones de componentes de HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="0d9ce-112">For more information on hello version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="0d9ce-113">toouse una versión específica de Mono, vea hello [instalación o una actualización Mono](hdinsight-hadoop-install-mono.md) documento.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-113">toouse a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="0d9ce-114">Si desea conocer más detalles sobre la compatibilidad entre Mono y las versiones de .NET Framework, consulte la página en la que se trata la [compatibilidad de Mono](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="0d9ce-114">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

## <a name="how-hadoop-streaming-works"></a><span data-ttu-id="0d9ce-115">Funcionamiento del streaming de Hadoop</span><span class="sxs-lookup"><span data-stu-id="0d9ce-115">How Hadoop streaming works</span></span>

<span data-ttu-id="0d9ce-116">proceso básico de Hello utilizado para la transmisión por secuencias en este documento es como sigue:</span><span class="sxs-lookup"><span data-stu-id="0d9ce-116">hello basic process used for streaming in this document is as follows:</span></span>

1. <span data-ttu-id="0d9ce-117">Hadoop pasa STDIN asignador de datos de toohello (mapper.exe en este ejemplo).</span><span class="sxs-lookup"><span data-stu-id="0d9ce-117">Hadoop passes data toohello mapper (mapper.exe in this example) on STDIN.</span></span>
2. <span data-ttu-id="0d9ce-118">el asignador de Hello procesa los datos de Hola y emite tooSTDOUT de pares clave/valor delimitado por tabuladores.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-118">hello mapper processes hello data, and emits tab-delimited key/value pairs tooSTDOUT.</span></span>
3. <span data-ttu-id="0d9ce-119">salida de Hello lee hadoop y, a continuación, pasar STDIN toohello reductor (reducer.exe en este ejemplo).</span><span class="sxs-lookup"><span data-stu-id="0d9ce-119">hello output is read by Hadoop, and then passed toohello reducer (reducer.exe in this example) on STDIN.</span></span>
4. <span data-ttu-id="0d9ce-120">reductor de Hello lee los pares de clave/valor Hola delimitado por tabuladores, procesa los datos de hello y, a continuación, emite el resultado de hello como pares de clave/valor delimitado por tabulaciones en STDOUT.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-120">hello reducer reads hello tab-delimited key/value pairs, processes hello data, and then emits hello result as tab-delimited key/value pairs on STDOUT.</span></span>
5. <span data-ttu-id="0d9ce-121">salida de Hello lee hadoop y escribe toohello directorio de salida.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-121">hello output is read by Hadoop and written toohello output directory.</span></span>

<span data-ttu-id="0d9ce-122">Para obtener más información sobre el streaming, consulte la página relativa al [streaming de Hadoop (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span><span class="sxs-lookup"><span data-stu-id="0d9ce-122">For more information on streaming, see [Hadoop Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d9ce-123">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0d9ce-123">Prerequisites</span></span>

* <span data-ttu-id="0d9ce-124">Estar familiarizado con la escritura y la compilación del código C# orientado a .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-124">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span> <span data-ttu-id="0d9ce-125">Hola pasos de este documento, use Visual Studio de 2017.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-125">hello steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="0d9ce-126">Un clúster de toohello de los archivos .exe de manera tooupload.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-126">A way tooupload .exe files toohello cluster.</span></span> <span data-ttu-id="0d9ce-127">Hello pasos en este documento utilizan Hola Data Lake Tools por Visual Studio tooupload Hola archivos tooprimary almacenamiento de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-127">hello steps in this document use hello Data Lake Tools for Visual Studio tooupload hello files tooprimary storage for hello cluster.</span></span>

* <span data-ttu-id="0d9ce-128">Azure PowerShell o un cliente de SSH.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-128">Azure PowerShell or a SSH client.</span></span>

* <span data-ttu-id="0d9ce-129">Hadoop en un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-129">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="0d9ce-130">Para obtener más información sobre cómo crear un clúster, consulte [Creación de un clúster de HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="0d9ce-130">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="create-hello-mapper"></a><span data-ttu-id="0d9ce-131">Crear un asignador de Hola</span><span class="sxs-lookup"><span data-stu-id="0d9ce-131">Create hello mapper</span></span>

<span data-ttu-id="0d9ce-132">En Visual Studio, cree una nueva __aplicación de consola__ denominada __mapper__.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-132">In Visual Studio, create a new __Console application__ named __mapper__.</span></span> <span data-ttu-id="0d9ce-133">Usar hello después el código de aplicación hello:</span><span class="sxs-lookup"><span data-stu-id="0d9ce-133">Use hello following code for hello application:</span></span>

```csharp
using System;
using System.Text.RegularExpressions;

namespace mapper
{
    class Program
    {
        static void Main(string[] args)
        {
            string line;
            //Hadoop passes data toohello mapper on STDIN
            while((line = Console.ReadLine()) != null)
            {
                // We only want words, so strip out punctuation, numbers, etc.
                var onlyText = Regex.Replace(line, @"\.|;|:|,|[0-9]|'", "");
                // Split at whitespace.
                var words = Regex.Matches(onlyText, @"[\w]+");
                // Loop over hello words
                foreach(var word in words)
                {
                    //Emit tab-delimited key/value pairs.
                    //In this case, a word and a count of 1.
                    Console.WriteLine("{0}\t1",word);
                }
            }
        }
    }
}
```

<span data-ttu-id="0d9ce-134">Después de crear la aplicación hello, genérelo hello tooproduce `/bin/Debug/mapper.exe` archivo en el directorio del proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-134">After creating hello application, build it tooproduce hello `/bin/Debug/mapper.exe` file in hello project directory.</span></span>

## <a name="create-hello-reducer"></a><span data-ttu-id="0d9ce-135">Crear reductor Hola</span><span class="sxs-lookup"><span data-stu-id="0d9ce-135">Create hello reducer</span></span>

<span data-ttu-id="0d9ce-136">En Visual Studio, cree una nueva __aplicación de consola__ denominada __reducer__.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-136">In Visual Studio, create a new __Console application__ named __reducer__.</span></span> <span data-ttu-id="0d9ce-137">Usar hello después el código de aplicación hello:</span><span class="sxs-lookup"><span data-stu-id="0d9ce-137">Use hello following code for hello application:</span></span>

```csharp
using System;
using System.Collections.Generic;

namespace reducer
{
    class Program
    {
        static void Main(string[] args)
        {
            //Dictionary for holding a count of words
            Dictionary<string, int> words = new Dictionary<string, int>();

            string line;
            //Read from STDIN
            while ((line = Console.ReadLine()) != null)
            {
                // Data from Hadoop is tab-delimited key/value pairs
                var sArr = line.Split('\t');
                // Get hello word
                string word = sArr[0];
                // Get hello count
                int count = Convert.ToInt32(sArr[1]);

                //Do we already have a count for hello word?
                if(words.ContainsKey(word))
                {
                    //If so, increment hello count
                    words[word] += count;
                } else
                {
                    //Add hello key toohello collection
                    words.Add(word, count);
                }
            }
            //Finally, emit each word and count
            foreach (var word in words)
            {
                //Emit tab-delimited key/value pairs.
                //In this case, a word and a count of 1.
                Console.WriteLine("{0}\t{1}", word.Key, word.Value);
            }
        }
    }
}
```

<span data-ttu-id="0d9ce-138">Después de crear la aplicación hello, genérelo hello tooproduce `/bin/Debug/reducer.exe` archivo en el directorio del proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-138">After creating hello application, build it tooproduce hello `/bin/Debug/reducer.exe` file in hello project directory.</span></span>

## <a name="upload-toostorage"></a><span data-ttu-id="0d9ce-139">Cargar toostorage</span><span class="sxs-lookup"><span data-stu-id="0d9ce-139">Upload toostorage</span></span>

1. <span data-ttu-id="0d9ce-140">En Visual Studio, abra el **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-140">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="0d9ce-141">Expanda **Azure** y, después, haga lo mismo con **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-141">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="0d9ce-142">Si se le solicitan, escriba sus credenciales de suscripción de Azure y, a continuación, haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-142">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="0d9ce-143">Expanda el clúster de HDInsight de Hola que desee toodeploy para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-143">Expand hello HDInsight cluster that you wish toodeploy this application to.</span></span> <span data-ttu-id="0d9ce-144">Una entrada con el texto hello __(cuenta de almacenamiento predeterminada)__ aparece.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-144">An entry with hello text __(Default Storage Account)__ is listed.</span></span>

    ![Explorador de servidores mostrando la cuenta de almacenamiento de hello para el clúster de Hola](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="0d9ce-146">Si se puede expandir esta entrada, que usa un __cuenta de almacenamiento de Azure__ como almacenamiento predeterminado para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-146">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for hello cluster.</span></span> <span data-ttu-id="0d9ce-147">archivos de Hola de tooview en almacenamiento predeterminado de Hola para clúster hello, expanda la entrada de hello y, a continuación, haga doble clic en hello __(contenedor predeterminado)__.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-147">tooview hello files on hello default storage for hello cluster, expand hello entry and then double-click hello __(Default Container)__.</span></span>

    * <span data-ttu-id="0d9ce-148">Si no se puede expandir esta entrada, que usa __almacén de Azure Data Lake__ como almacenamiento predeterminado de hello para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-148">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as hello default storage for hello cluster.</span></span> <span data-ttu-id="0d9ce-149">archivos de hello tooview en almacenamiento predeterminado de hello para el clúster de hello, haga doble clic en hello __(cuenta de almacenamiento predeterminada)__ entrada.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-149">tooview hello files on hello default storage for hello cluster, double-click hello __(Default Storage Account)__ entry.</span></span>

5. <span data-ttu-id="0d9ce-150">archivos .exe de tooupload hello, use uno de los siguientes métodos de hello:</span><span class="sxs-lookup"><span data-stu-id="0d9ce-150">tooupload hello .exe files, use one of hello following methods:</span></span>

    * <span data-ttu-id="0d9ce-151">Si usa un __cuenta de almacenamiento de Azure__, haga clic en el icono de carga de hello y, a continuación, examinar toohello **bin\debug** carpeta para hello **asignador** proyecto.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-151">If using an __Azure Storage Account__, click hello upload icon, and then browse toohello **bin\debug** folder for hello **mapper** project.</span></span> <span data-ttu-id="0d9ce-152">Por último, seleccione hello **mapper.exe** de archivo y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-152">Finally, select hello **mapper.exe** file and click **Ok**.</span></span>

        ![icono para cargar](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="0d9ce-154">Si usa __almacén de Azure Data Lake__, haga clic en un área vacía en lista de archivos de hello y, a continuación, seleccione __cargar__.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-154">If using __Azure Data Lake Store__, right-click an empty area in hello file listing, and then select __Upload__.</span></span> <span data-ttu-id="0d9ce-155">Por último, seleccione hello **mapper.exe** de archivo y haga clic en **abiertos**.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-155">Finally, select hello **mapper.exe** file and click **Open**.</span></span>

    <span data-ttu-id="0d9ce-156">Una vez Hola __mapper.exe__ carga haya finalizado, el proceso de carga de repetición Hola para hello __reducer.exe__ archivo.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-156">Once hello __mapper.exe__ upload has finished, repeat hello upload process for hello __reducer.exe__ file.</span></span>

## <a name="run-a-job-using-an-ssh-session"></a><span data-ttu-id="0d9ce-157">Ejecución de un trabajo mediante una sesión de SSH</span><span class="sxs-lookup"><span data-stu-id="0d9ce-157">Run a job: Using an SSH session</span></span>

1. <span data-ttu-id="0d9ce-158">Use el clúster de HDInsight de toohello tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-158">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="0d9ce-159">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0d9ce-159">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="0d9ce-160">Use uno de hello siguiendo el trabajo de MapReduce de hello toostart de comando:</span><span class="sxs-lookup"><span data-stu-id="0d9ce-160">Use one of hello following command toostart hello MapReduce job:</span></span>

    * <span data-ttu-id="0d9ce-161">Si utiliza __Data Lake Store__ como almacenamiento predeterminado:</span><span class="sxs-lookup"><span data-stu-id="0d9ce-161">If using __Data Lake Store__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files adl:///mapper.exe,adl:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```
    
    * <span data-ttu-id="0d9ce-162">Si emplea __Azure Storage__ como almacenamiento predeterminado:</span><span class="sxs-lookup"><span data-stu-id="0d9ce-162">If using __Azure Storage__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files wasb:///mapper.exe,wasb:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```

    <span data-ttu-id="0d9ce-163">Hola lista siguiente describe lo que hace cada parámetro:</span><span class="sxs-lookup"><span data-stu-id="0d9ce-163">hello following list describes what each parameter does:</span></span>

    * <span data-ttu-id="0d9ce-164">`hadoop-streaming.jar`: archivo jar de Hola que contiene la funcionalidad de MapReduce de streaming de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-164">`hadoop-streaming.jar`: hello jar file that contains hello streaming MapReduce functionality.</span></span>
    * <span data-ttu-id="0d9ce-165">`-files`: Agrega hello `mapper.exe` y `reducer.exe` trabajo toothis de archivos.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-165">`-files`: Adds hello `mapper.exe` and `reducer.exe` files toothis job.</span></span> <span data-ttu-id="0d9ce-166">Hola `adl:///` o `wasb:///` antes de cada archivo es la raíz de toohello de ruta de acceso de Hola de almacenamiento predeterminado para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-166">hello `adl:///` or `wasb:///` before each file is hello path toohello root of default storage for hello cluster.</span></span>
    * <span data-ttu-id="0d9ce-167">`-mapper`: Especifica el archivo que implementa el asignador de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-167">`-mapper`: Specifies which file implements hello mapper.</span></span>
    * <span data-ttu-id="0d9ce-168">`-reducer`: Especifica qué archivo implementa reductor Hola.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-168">`-reducer`: Specifies which file implements hello reducer.</span></span>
    * <span data-ttu-id="0d9ce-169">`-input`: Hola los datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-169">`-input`: hello input data.</span></span>
    * <span data-ttu-id="0d9ce-170">`-output`: directorio de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-170">`-output`: hello output directory.</span></span>

3. <span data-ttu-id="0d9ce-171">Cuando se completa el trabajo de MapReduce hello, utilice Hola siguiendo los resultados de Hola tooview:</span><span class="sxs-lookup"><span data-stu-id="0d9ce-171">Once hello MapReduce job completes, use hello following tooview hello results:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="0d9ce-172">Hello texto siguiente es un ejemplo de datos de hello devueltos por este comando:</span><span class="sxs-lookup"><span data-stu-id="0d9ce-172">hello following text is an example of hello data returned by this command:</span></span>

        you     1128
        young   38
        younger 1
        youngest        1
        your    338
        yours   4
        yourself        34
        yourselves      3
        youth   17

## <a name="run-a-job-using-powershell"></a><span data-ttu-id="0d9ce-173">Ejecución de un trabajo mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="0d9ce-173">Run a job: Using PowerShell</span></span>

<span data-ttu-id="0d9ce-174">Use Hola después toorun de secuencia de comandos de PowerShell un trabajo MapReduce y descargar los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-174">Use hello following PowerShell script toorun a MapReduce job and download hello results.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]

<span data-ttu-id="0d9ce-175">Este script le nombre de cuenta de inicio de sesión de clúster de hello y una contraseña, junto con el nombre de clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-175">This script prompts you for hello cluster login account name and password, along with hello HDInsight cluster name.</span></span> <span data-ttu-id="0d9ce-176">Cuando se completa el trabajo de hello, salida de hello es descargado toohello `output.txt` archivo en secuencia de comandos de hello directory Hola se ejecutó desde.</span><span class="sxs-lookup"><span data-stu-id="0d9ce-176">Once hello job completes, hello output is downloaded toohello `output.txt` file in hello directory hello script is ran from.</span></span> <span data-ttu-id="0d9ce-177">Hello texto siguiente es un ejemplo de datos de Hola Hola `output.txt` archivo:</span><span class="sxs-lookup"><span data-stu-id="0d9ce-177">hello following text is an example of hello data in hello `output.txt` file:</span></span>

    you     1128
    young   38
    younger 1
    youngest        1
    your    338
    yours   4
    yourself        34
    yourselves      3
    youth   17

## <a name="next-steps"></a><span data-ttu-id="0d9ce-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0d9ce-178">Next steps</span></span>

<span data-ttu-id="0d9ce-179">Para obtener más información sobre el uso de MapReduce con HDInsight, consulte [Uso de MapReduce con HDInsight](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="0d9ce-179">For more information on using MapReduce with HDInsight, see [Use MapReduce with HDInsight](hdinsight-use-mapreduce.md).</span></span>

<span data-ttu-id="0d9ce-180">Para obtener información sobre la utilización de C# con Hive y Pig, consulte el artículo referente al [uso de una función de C# definida por el usuario con Hive y Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="0d9ce-180">For information on using C# with Hive and Pig, see [Use a C# user defined function with Hive and Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span></span>

<span data-ttu-id="0d9ce-181">Para obtener información sobre cómo emplear C# con Storm en HDInsight, consulte el artículo relativo al [desarrollo de topologías de C# para Storm en HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="0d9ce-181">For information on using C# with Storm on HDInsight, see [Develop C# topologies for Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>