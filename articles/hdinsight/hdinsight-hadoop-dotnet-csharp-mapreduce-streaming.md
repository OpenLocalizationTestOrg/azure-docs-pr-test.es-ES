---
title: Uso de C# con MapReduce en Hadoop en HDInsight (Azure) | Microsoft Docs
description: "Descubra cómo utilizar C# para crear soluciones de MapReduce con Hadoop en Azure HDInsight."
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
ms.openlocfilehash: adb454e56378a800c671614735aec78b6851aeb2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="use-c-with-mapreduce-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="62b7c-103">Uso de C# con el streaming de MapReduce en Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="62b7c-103">Use C# with MapReduce streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="62b7c-104">Descubra cómo utilizar C# para crear una solución de MapReduce en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="62b7c-104">Learn how to use C# to create a MapReduce solution on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="62b7c-105">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="62b7c-105">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="62b7c-106">Para obtener más información, consulte el artículo relativo al [control de versiones de componentes de HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="62b7c-106">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="62b7c-107">El streaming de Hadoop es una utilidad que permite ejecutar trabajos de MapReduce mediante un script o ejecutable.</span><span class="sxs-lookup"><span data-stu-id="62b7c-107">Hadoop streaming is a utility that allows you to run MapReduce jobs using a script or executable.</span></span> <span data-ttu-id="62b7c-108">En este ejemplo, se emplea .NET para implementar el asignador y reductor en una solución de recuento de palabras.</span><span class="sxs-lookup"><span data-stu-id="62b7c-108">In this example, .NET is used to implement the mapper and reducer for a word count solution.</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="62b7c-109">.NET en HDInsight</span><span class="sxs-lookup"><span data-stu-id="62b7c-109">.NET on HDInsight</span></span>

<span data-ttu-id="62b7c-110">Los clústeres de __HDInsight basado en Linux__ se sirven de [Mono (https://mono-project.com)](https://mono-project.com) para ejecutar aplicaciones .NET.</span><span class="sxs-lookup"><span data-stu-id="62b7c-110">__Linux-based HDInsight__ clusters use [Mono (https://mono-project.com)](https://mono-project.com) to run .NET applications.</span></span> <span data-ttu-id="62b7c-111">La versión 4.2.1 de Mono está incluida en la versión 3.5 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="62b7c-111">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="62b7c-112">Para obtener más información sobre la versión de Mono incluida en HDInsight, consulte el artículo relativo a las [versiones de componentes de HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="62b7c-112">For more information on the version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="62b7c-113">Para usar una versión específica de Mono, consulte el documento [Instalación o actualización de Mono](hdinsight-hadoop-install-mono.md).</span><span class="sxs-lookup"><span data-stu-id="62b7c-113">To use a specific version of Mono, see the [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="62b7c-114">Si desea conocer más detalles sobre la compatibilidad entre Mono y las versiones de .NET Framework, consulte la página en la que se trata la [compatibilidad de Mono](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="62b7c-114">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

## <a name="how-hadoop-streaming-works"></a><span data-ttu-id="62b7c-115">Funcionamiento del streaming de Hadoop</span><span class="sxs-lookup"><span data-stu-id="62b7c-115">How Hadoop streaming works</span></span>

<span data-ttu-id="62b7c-116">A continuación se expone el proceso básico que se emplea para realizar streaming en este documento:</span><span class="sxs-lookup"><span data-stu-id="62b7c-116">The basic process used for streaming in this document is as follows:</span></span>

1. <span data-ttu-id="62b7c-117">Hadoop transfiere datos al asignador (mapper.exe en este ejemplo) en STDIN.</span><span class="sxs-lookup"><span data-stu-id="62b7c-117">Hadoop passes data to the mapper (mapper.exe in this example) on STDIN.</span></span>
2. <span data-ttu-id="62b7c-118">El asignador procesa los datos y envía pares clave-valor delimitados por tabulaciones a STDOUT.</span><span class="sxs-lookup"><span data-stu-id="62b7c-118">The mapper processes the data, and emits tab-delimited key/value pairs to STDOUT.</span></span>
3. <span data-ttu-id="62b7c-119">Hadoop lee los resultados, que, a continuación, se transfieren al reductor (reducer.exe en este ejemplo) en STDIN.</span><span class="sxs-lookup"><span data-stu-id="62b7c-119">The output is read by Hadoop, and then passed to the reducer (reducer.exe in this example) on STDIN.</span></span>
4. <span data-ttu-id="62b7c-120">El reductor lee los pares clave-valor delimitados por tabulaciones, procesa los datos y, después, envía el resultado en forma de pares clave-valor delimitados por tabulaciones en STDOUT.</span><span class="sxs-lookup"><span data-stu-id="62b7c-120">The reducer reads the tab-delimited key/value pairs, processes the data, and then emits the result as tab-delimited key/value pairs on STDOUT.</span></span>
5. <span data-ttu-id="62b7c-121">Hadoop lee los resultados, que, a continuación, se escriben en el directorio de salida.</span><span class="sxs-lookup"><span data-stu-id="62b7c-121">The output is read by Hadoop and written to the output directory.</span></span>

<span data-ttu-id="62b7c-122">Para obtener más información sobre el streaming, consulte la página relativa al [streaming de Hadoop (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span><span class="sxs-lookup"><span data-stu-id="62b7c-122">For more information on streaming, see [Hadoop Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62b7c-123">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="62b7c-123">Prerequisites</span></span>

* <span data-ttu-id="62b7c-124">Estar familiarizado con la escritura y la compilación del código C# orientado a .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="62b7c-124">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span> <span data-ttu-id="62b7c-125">En los pasos descritos en este documento se utiliza Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="62b7c-125">The steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="62b7c-126">Una forma de cargar archivos .exe en el clúster.</span><span class="sxs-lookup"><span data-stu-id="62b7c-126">A way to upload .exe files to the cluster.</span></span> <span data-ttu-id="62b7c-127">En los pasos descritos en este documento se emplean las herramientas Data Lake para Visual Studio para cargar los archivos en el almacenamiento principal del clúster.</span><span class="sxs-lookup"><span data-stu-id="62b7c-127">The steps in this document use the Data Lake Tools for Visual Studio to upload the files to primary storage for the cluster.</span></span>

* <span data-ttu-id="62b7c-128">Azure PowerShell o un cliente de SSH.</span><span class="sxs-lookup"><span data-stu-id="62b7c-128">Azure PowerShell or a SSH client.</span></span>

* <span data-ttu-id="62b7c-129">Hadoop en un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="62b7c-129">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="62b7c-130">Para obtener más información sobre cómo crear un clúster, consulte [Creación de un clúster de HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="62b7c-130">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="create-the-mapper"></a><span data-ttu-id="62b7c-131">Creación del asignador</span><span class="sxs-lookup"><span data-stu-id="62b7c-131">Create the mapper</span></span>

<span data-ttu-id="62b7c-132">En Visual Studio, cree una nueva __aplicación de consola__ denominada __mapper__.</span><span class="sxs-lookup"><span data-stu-id="62b7c-132">In Visual Studio, create a new __Console application__ named __mapper__.</span></span> <span data-ttu-id="62b7c-133">Use el código siguiente para la aplicación:</span><span class="sxs-lookup"><span data-stu-id="62b7c-133">Use the following code for the application:</span></span>

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
            //Hadoop passes data to the mapper on STDIN
            while((line = Console.ReadLine()) != null)
            {
                // We only want words, so strip out punctuation, numbers, etc.
                var onlyText = Regex.Replace(line, @"\.|;|:|,|[0-9]|'", "");
                // Split at whitespace.
                var words = Regex.Matches(onlyText, @"[\w]+");
                // Loop over the words
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

<span data-ttu-id="62b7c-134">Después de crear la aplicación, compílela para generar el archivo `/bin/Debug/mapper.exe` en el directorio del proyecto.</span><span class="sxs-lookup"><span data-stu-id="62b7c-134">After creating the application, build it to produce the `/bin/Debug/mapper.exe` file in the project directory.</span></span>

## <a name="create-the-reducer"></a><span data-ttu-id="62b7c-135">Creación del reductor</span><span class="sxs-lookup"><span data-stu-id="62b7c-135">Create the reducer</span></span>

<span data-ttu-id="62b7c-136">En Visual Studio, cree una nueva __aplicación de consola__ denominada __reducer__.</span><span class="sxs-lookup"><span data-stu-id="62b7c-136">In Visual Studio, create a new __Console application__ named __reducer__.</span></span> <span data-ttu-id="62b7c-137">Use el código siguiente para la aplicación:</span><span class="sxs-lookup"><span data-stu-id="62b7c-137">Use the following code for the application:</span></span>

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
                // Get the word
                string word = sArr[0];
                // Get the count
                int count = Convert.ToInt32(sArr[1]);

                //Do we already have a count for the word?
                if(words.ContainsKey(word))
                {
                    //If so, increment the count
                    words[word] += count;
                } else
                {
                    //Add the key to the collection
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

<span data-ttu-id="62b7c-138">Después de crear la aplicación, compílela para generar el archivo `/bin/Debug/reducer.exe` en el directorio del proyecto.</span><span class="sxs-lookup"><span data-stu-id="62b7c-138">After creating the application, build it to produce the `/bin/Debug/reducer.exe` file in the project directory.</span></span>

## <a name="upload-to-storage"></a><span data-ttu-id="62b7c-139">Carga en el almacenamiento</span><span class="sxs-lookup"><span data-stu-id="62b7c-139">Upload to storage</span></span>

1. <span data-ttu-id="62b7c-140">En Visual Studio, abra el **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="62b7c-140">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="62b7c-141">Expanda **Azure** y, después, haga lo mismo con **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="62b7c-141">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="62b7c-142">Si se le solicitan, escriba sus credenciales de suscripción de Azure y, a continuación, haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="62b7c-142">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="62b7c-143">Expanda el clúster de HDInsight en el que desee implementar esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="62b7c-143">Expand the HDInsight cluster that you wish to deploy this application to.</span></span> <span data-ttu-id="62b7c-144">Aparecerá una entrada con el texto __(Cuenta de almacenamiento predeterminada)__ en la lista.</span><span class="sxs-lookup"><span data-stu-id="62b7c-144">An entry with the text __(Default Storage Account)__ is listed.</span></span>

    ![Explorador de servidores en el que se muestra la cuenta de almacenamiento para el clúster](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="62b7c-146">Si se puede expandir esta entrada, significa que está utilizando una __cuenta de Azure Storage__ como almacenamiento predeterminado para el clúster.</span><span class="sxs-lookup"><span data-stu-id="62b7c-146">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for the cluster.</span></span> <span data-ttu-id="62b7c-147">Para ver los archivos incluidos en el almacenamiento predeterminado del clúster, expanda la entrada y, a continuación, haga doble clic en __(Contenedor predeterminado)__.</span><span class="sxs-lookup"><span data-stu-id="62b7c-147">To view the files on the default storage for the cluster, expand the entry and then double-click the __(Default Container)__.</span></span>

    * <span data-ttu-id="62b7c-148">Si, por el contrario, no puede expandirse, quiere decir que está usando __Azure Data Lake Store__ como almacenamiento predeterminado para el clúster.</span><span class="sxs-lookup"><span data-stu-id="62b7c-148">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as the default storage for the cluster.</span></span> <span data-ttu-id="62b7c-149">Para ver los archivos incluidos en el almacenamiento predeterminado del clúster, haga doble clic en la entrada __(Cuenta de almacenamiento predeterminada)__.</span><span class="sxs-lookup"><span data-stu-id="62b7c-149">To view the files on the default storage for the cluster, double-click the __(Default Storage Account)__ entry.</span></span>

5. <span data-ttu-id="62b7c-150">Para cargar los archivos .exe, siga uno de estos métodos:</span><span class="sxs-lookup"><span data-stu-id="62b7c-150">To upload the .exe files, use one of the following methods:</span></span>

    * <span data-ttu-id="62b7c-151">Si utiliza una __cuenta de Azure Storage__, haga clic en el icono de carga y, a continuación, navegue hasta la carpeta **bin\debug** para localizar el proyecto **mapper**.</span><span class="sxs-lookup"><span data-stu-id="62b7c-151">If using an __Azure Storage Account__, click the upload icon, and then browse to the **bin\debug** folder for the **mapper** project.</span></span> <span data-ttu-id="62b7c-152">Por último, seleccione el archivo **mapper.exe** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="62b7c-152">Finally, select the **mapper.exe** file and click **Ok**.</span></span>

        ![icono para cargar](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="62b7c-154">Si usa __Azure Data Lake Store__, haga clic con el botón derecho en un área vacía de la lista de archivos y, después, elija __Cargar__.</span><span class="sxs-lookup"><span data-stu-id="62b7c-154">If using __Azure Data Lake Store__, right-click an empty area in the file listing, and then select __Upload__.</span></span> <span data-ttu-id="62b7c-155">Por último, seleccione el archivo **mapper.exe** y haga clic en **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="62b7c-155">Finally, select the **mapper.exe** file and click **Open**.</span></span>

    <span data-ttu-id="62b7c-156">Una vez que la carga del archivo __mapper.exe__ haya finalizado, repita el proceso de carga con el archivo __reducer.exe__.</span><span class="sxs-lookup"><span data-stu-id="62b7c-156">Once the __mapper.exe__ upload has finished, repeat the upload process for the __reducer.exe__ file.</span></span>

## <a name="run-a-job-using-an-ssh-session"></a><span data-ttu-id="62b7c-157">Ejecución de un trabajo mediante una sesión de SSH</span><span class="sxs-lookup"><span data-stu-id="62b7c-157">Run a job: Using an SSH session</span></span>

1. <span data-ttu-id="62b7c-158">Use SSH para conectarse al clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="62b7c-158">Use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="62b7c-159">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="62b7c-159">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="62b7c-160">Use uno de los siguientes comandos para iniciar el trabajo de MapReduce:</span><span class="sxs-lookup"><span data-stu-id="62b7c-160">Use one of the following command to start the MapReduce job:</span></span>

    * <span data-ttu-id="62b7c-161">Si utiliza __Data Lake Store__ como almacenamiento predeterminado:</span><span class="sxs-lookup"><span data-stu-id="62b7c-161">If using __Data Lake Store__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files adl:///mapper.exe,adl:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```
    
    * <span data-ttu-id="62b7c-162">Si emplea __Azure Storage__ como almacenamiento predeterminado:</span><span class="sxs-lookup"><span data-stu-id="62b7c-162">If using __Azure Storage__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files wasb:///mapper.exe,wasb:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```

    <span data-ttu-id="62b7c-163">En la lista siguiente, se describen las funciones de cada parámetro:</span><span class="sxs-lookup"><span data-stu-id="62b7c-163">The following list describes what each parameter does:</span></span>

    * <span data-ttu-id="62b7c-164">`hadoop-streaming.jar`: el archivo .jar que contiene la funcionalidad de streaming de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="62b7c-164">`hadoop-streaming.jar`: The jar file that contains the streaming MapReduce functionality.</span></span>
    * <span data-ttu-id="62b7c-165">`-files`: agrega los archivos `mapper.exe` y `reducer.exe` al trabajo.</span><span class="sxs-lookup"><span data-stu-id="62b7c-165">`-files`: Adds the `mapper.exe` and `reducer.exe` files to this job.</span></span> <span data-ttu-id="62b7c-166">El texto `adl:///` o `wasb:///` que aparece antes de cada archivo es la ruta a la raíz del almacenamiento predeterminado del clúster.</span><span class="sxs-lookup"><span data-stu-id="62b7c-166">The `adl:///` or `wasb:///` before each file is the path to the root of default storage for the cluster.</span></span>
    * <span data-ttu-id="62b7c-167">`-mapper`: especifica el archivo que implementa el asignador.</span><span class="sxs-lookup"><span data-stu-id="62b7c-167">`-mapper`: Specifies which file implements the mapper.</span></span>
    * <span data-ttu-id="62b7c-168">`-reducer`: indica qué archivo implementa el reductor.</span><span class="sxs-lookup"><span data-stu-id="62b7c-168">`-reducer`: Specifies which file implements the reducer.</span></span>
    * <span data-ttu-id="62b7c-169">`-input`: los datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="62b7c-169">`-input`: The input data.</span></span>
    * <span data-ttu-id="62b7c-170">`-output`: el directorio de salida.</span><span class="sxs-lookup"><span data-stu-id="62b7c-170">`-output`: The output directory.</span></span>

3. <span data-ttu-id="62b7c-171">Una vez completado el trabajo de MapReduce, use lo siguiente para ver los resultados:</span><span class="sxs-lookup"><span data-stu-id="62b7c-171">Once the MapReduce job completes, use the following to view the results:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="62b7c-172">Este texto es un ejemplo de los datos que devuelve este comando:</span><span class="sxs-lookup"><span data-stu-id="62b7c-172">The following text is an example of the data returned by this command:</span></span>

        you     1128
        young   38
        younger 1
        youngest        1
        your    338
        yours   4
        yourself        34
        yourselves      3
        youth   17

## <a name="run-a-job-using-powershell"></a><span data-ttu-id="62b7c-173">Ejecución de un trabajo mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="62b7c-173">Run a job: Using PowerShell</span></span>

<span data-ttu-id="62b7c-174">Sírvase del siguiente script de PowerShell para ejecutar un trabajo de MapReduce y descargar los resultados.</span><span class="sxs-lookup"><span data-stu-id="62b7c-174">Use the following PowerShell script to run a MapReduce job and download the results.</span></span>

<span data-ttu-id="62b7c-175">[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]</span><span class="sxs-lookup"><span data-stu-id="62b7c-175">[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]</span></span>

<span data-ttu-id="62b7c-176">Este script le solicitará el nombre de la cuenta de inicio de sesión y la contraseña del clúster, junto con el nombre del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="62b7c-176">This script prompts you for the cluster login account name and password, along with the HDInsight cluster name.</span></span> <span data-ttu-id="62b7c-177">Tras finalizar el trabajo, el resultado se descargará en el archivo `output.txt` del directorio desde el que se ejecute el script.</span><span class="sxs-lookup"><span data-stu-id="62b7c-177">Once the job completes, the output is downloaded to the `output.txt` file in the directory the script is ran from.</span></span> <span data-ttu-id="62b7c-178">A continuación, se muestra un ejemplo de los datos que contiene el archivo `output.txt`:</span><span class="sxs-lookup"><span data-stu-id="62b7c-178">The following text is an example of the data in the `output.txt` file:</span></span>

    you     1128
    young   38
    younger 1
    youngest        1
    your    338
    yours   4
    yourself        34
    yourselves      3
    youth   17

## <a name="next-steps"></a><span data-ttu-id="62b7c-179">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="62b7c-179">Next steps</span></span>

<span data-ttu-id="62b7c-180">Para obtener más información sobre el uso de MapReduce con HDInsight, consulte [Uso de MapReduce con HDInsight](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="62b7c-180">For more information on using MapReduce with HDInsight, see [Use MapReduce with HDInsight](hdinsight-use-mapreduce.md).</span></span>

<span data-ttu-id="62b7c-181">Para obtener información sobre la utilización de C# con Hive y Pig, consulte el artículo referente al [uso de una función de C# definida por el usuario con Hive y Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="62b7c-181">For information on using C# with Hive and Pig, see [Use a C# user defined function with Hive and Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span></span>

<span data-ttu-id="62b7c-182">Para obtener información sobre cómo emplear C# con Storm en HDInsight, consulte el artículo relativo al [desarrollo de topologías de C# para Storm en HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="62b7c-182">For information on using C# with Storm on HDInsight, see [Develop C# topologies for Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>