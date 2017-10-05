---
title: "Instalación y uso de Giraph en HDInsight (Hadoop): Azure | Microsoft Docs"
description: "Aprenda a instalar Giraph en clústeres de HDInsight basados en Linux mediante acciones de script. Las acciones de script le permiten personalizar el clúster durante la creación; así, puede cambiar la configuración del clúster o instalar utilidades y servicios."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9fcac906-8f06-4002-9fe8-473e42f8fd0f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 6e2f6983e00f874420f7f0907dbc68185f0af713
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-to-process-large-scale-graphs"></a><span data-ttu-id="9f630-104">Instalar Giraph en clústeres de Hadoop de HDInsight y usar Giraph para procesar gráficos a gran escala</span><span class="sxs-lookup"><span data-stu-id="9f630-104">Install Giraph on HDInsight Hadoop clusters, and use Giraph to process large-scale graphs</span></span>

<span data-ttu-id="9f630-105">Aprenda a instalar Apache Giraph en un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9f630-105">Learn how to install Apache Giraph on an HDInsight cluster.</span></span> <span data-ttu-id="9f630-106">La característica de acción de script de HDInsight le permite personalizar el clúster mediante la ejecución de un script de Bash.</span><span class="sxs-lookup"><span data-stu-id="9f630-106">The script action feature of HDInsight allows you to customize your cluster by running a bash script.</span></span> <span data-ttu-id="9f630-107">Se pueden usar scripts para personalizar los clústeres durante y después de la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="9f630-107">Scripts can be used to customize clusters during and after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9f630-108">Los pasos descritos en este documento requieren un clúster de HDInsight que use Linux.</span><span class="sxs-lookup"><span data-stu-id="9f630-108">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="9f630-109">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="9f630-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9f630-110">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="9f630-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="9f630-111"><a name="whatis"></a>¿Qué es Giraph?</span><span class="sxs-lookup"><span data-stu-id="9f630-111"><a name="whatis"></a>What is Giraph</span></span>

<span data-ttu-id="9f630-112">[Apache Giraph](http://giraph.apache.org/) permite realizar un procesamiento gráfico mediante Hadoop, y se puede usar con HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="9f630-112">[Apache Giraph](http://giraph.apache.org/) allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="9f630-113">Los gráficos modelan las relaciones entre los objetos.</span><span class="sxs-lookup"><span data-stu-id="9f630-113">Graphs model relationships between objects.</span></span> <span data-ttu-id="9f630-114">Por ejemplo, las conexiones entre los enrutadores de una red de gran tamaño, como Internet, o las relaciones entre las personas en las redes sociales.</span><span class="sxs-lookup"><span data-stu-id="9f630-114">For example, the connections between routers on a large network like the Internet, or relationships between people on social networks.</span></span> <span data-ttu-id="9f630-115">El procesamiento gráfico le permite razonar sobre las relaciones entre los objetos de un gráfico. En este sentido, le ayuda por ejemplo a:</span><span class="sxs-lookup"><span data-stu-id="9f630-115">Graph processing allows you to reason about the relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="9f630-116">Identificar los posibles amigos según las relaciones actuales.</span><span class="sxs-lookup"><span data-stu-id="9f630-116">Identifying potential friends based on your current relationships.</span></span>

* <span data-ttu-id="9f630-117">Identificar la ruta más corta entre dos equipos de una red.</span><span class="sxs-lookup"><span data-stu-id="9f630-117">Identifying the shortest route between two computers in a network.</span></span>

* <span data-ttu-id="9f630-118">Calcular la posición de las páginas web.</span><span class="sxs-lookup"><span data-stu-id="9f630-118">Calculating the page rank of webpages.</span></span>

> [!WARNING]
> <span data-ttu-id="9f630-119">Los componentes proporcionados con el clúster de HDInsight son totalmente compatibles. Además, el soporte técnico de Microsoft le ayuda a aislar y resolver problemas relacionados con estos componentes.</span><span class="sxs-lookup"><span data-stu-id="9f630-119">Components provided with the HDInsight cluster are fully supported - Microsoft Support helps to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="9f630-120">Los componentes personalizados, como Giraph, reciben soporte técnico comercialmente razonable para ayudarlo a solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="9f630-120">Custom components, such as Giraph, receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="9f630-121">El soporte técnico de Microsoft podría solucionar este problema.</span><span class="sxs-lookup"><span data-stu-id="9f630-121">Microsoft Support may be able to resolving the issue.</span></span> <span data-ttu-id="9f630-122">Si no es así, debe consultar las comunidades de código abierto donde grandes expertos en esa tecnología.</span><span class="sxs-lookup"><span data-stu-id="9f630-122">If not, you must consult open source communities where deep expertise for that technology is found.</span></span> <span data-ttu-id="9f630-123">Por ejemplo, hay diversos sitios de la comunidad que se pueden usar, como el [foro de MSDN para HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="9f630-123">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="9f630-124">Los proyectos de Apache también tienen sitios de proyecto en [http://apache.org](http://apache.org) (por ejemplo, [Hadoop](http://hadoop.apache.org/)).</span><span class="sxs-lookup"><span data-stu-id="9f630-124">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>


## <a name="what-the-script-does"></a><span data-ttu-id="9f630-125">Funcionamiento del script</span><span class="sxs-lookup"><span data-stu-id="9f630-125">What the script does</span></span>

<span data-ttu-id="9f630-126">Este script realiza las acciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="9f630-126">This script performs the following actions:</span></span>

* <span data-ttu-id="9f630-127">Instala Giraph en `/usr/hdp/current/giraph`</span><span class="sxs-lookup"><span data-stu-id="9f630-127">Installs Giraph to `/usr/hdp/current/giraph`</span></span>

* <span data-ttu-id="9f630-128">Copia el archivo `giraph-examples.jar` en el almacenamiento predeterminado (WASB) del clúster: `/example/jars/giraph-examples.jar`</span><span class="sxs-lookup"><span data-stu-id="9f630-128">Copies the `giraph-examples.jar` file to default storage (WASB) for your cluster: `/example/jars/giraph-examples.jar`</span></span>

## <span data-ttu-id="9f630-129"><a name="install"></a>Instalación de Giraph mediante acciones de script</span><span class="sxs-lookup"><span data-stu-id="9f630-129"><a name="install"></a>Install Giraph using Script Actions</span></span>

<span data-ttu-id="9f630-130">En la siguiente ubicación se encuentra disponible un script de ejemplo para instalar Giraph en un clúster de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9f630-130">A sample script to install Giraph on an HDInsight cluster is available at the following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

<span data-ttu-id="9f630-131">Esta sección proporciona instrucciones sobre cómo usar el script de ejemplo al crear el clúster mediante el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9f630-131">This section provides instructions on how to use the sample script while creating the cluster by using the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="9f630-132">Se puede aplicar una acción de script mediante cualquiera de los siguientes métodos:</span><span class="sxs-lookup"><span data-stu-id="9f630-132">A script action can be applied using any of the following methods:</span></span>
> * <span data-ttu-id="9f630-133">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f630-133">Azure PowerShell</span></span>
> * <span data-ttu-id="9f630-134">La CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="9f630-134">The Azure CLI</span></span>
> * <span data-ttu-id="9f630-135">El SDK de .NET para HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f630-135">The HDInsight .NET SDK</span></span>
> * <span data-ttu-id="9f630-136">Plantillas del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="9f630-136">Azure Resource Manager templates</span></span>
> 
> <span data-ttu-id="9f630-137">También puede aplicar acciones de script a clústeres que ya se estén ejecutando.</span><span class="sxs-lookup"><span data-stu-id="9f630-137">You can also apply script actions to already running clusters.</span></span> <span data-ttu-id="9f630-138">Para obtener más información, consulte [Personalización de clústeres de HDInsight mediante la acción de scripts](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="9f630-138">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="9f630-139">Comience a crear un clúster siguiendo los pasos que se describen en [Creación de clústeres de HDInsight basados en Linux](hdinsight-hadoop-create-linux-clusters-portal.md), pero no complete la operación.</span><span class="sxs-lookup"><span data-stu-id="9f630-139">Start creating a cluster by using the steps in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md), but do not complete creation.</span></span>

2. <span data-ttu-id="9f630-140">En la hoja **Configuración opcional**, seleccione **Acciones de script** y proporcione la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="9f630-140">On the **Optional Configuration** blade, select **Script Actions**, and provide the following information:</span></span>

   * <span data-ttu-id="9f630-141">**NOMBRE**: escriba un nombre descriptivo para la acción de script.</span><span class="sxs-lookup"><span data-stu-id="9f630-141">**NAME**: Enter a friendly name for the script action.</span></span>

   * <span data-ttu-id="9f630-142">**URI del SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="9f630-142">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span></span>

   * <span data-ttu-id="9f630-143">**PRINCIPAL**: active esta entrada.</span><span class="sxs-lookup"><span data-stu-id="9f630-143">**HEAD**: Check this entry</span></span>

   * <span data-ttu-id="9f630-144">**TRABAJO**: deje esta opción desactivada.</span><span class="sxs-lookup"><span data-stu-id="9f630-144">**WORKER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="9f630-145">**ZOOKEEPER**: deje esta opción desactivada.</span><span class="sxs-lookup"><span data-stu-id="9f630-145">**ZOOKEEPER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="9f630-146">**PARÁMETROS**: deje este campo en blanco.</span><span class="sxs-lookup"><span data-stu-id="9f630-146">**PARAMETERS**: Leave this field blank</span></span>

3. <span data-ttu-id="9f630-147">En la parte inferior de **Acciones de scripts**, use el botón **Seleccionar** para guardar la configuración.</span><span class="sxs-lookup"><span data-stu-id="9f630-147">At the bottom of the **Script Actions**, use the **Select** button to save the configuration.</span></span> <span data-ttu-id="9f630-148">Por último, use el botón **Seleccionar** situado en la parte inferior de la hoja **Configuración opcional** para guardar la información de configuración opcional.</span><span class="sxs-lookup"><span data-stu-id="9f630-148">Finally, use the **Select** button at the bottom of the **Optional Configuration** blade to save the optional configuration information.</span></span>

4. <span data-ttu-id="9f630-149">Continúe creando el clúster, tal como se describe en [Creación de clústeres de HDInsight basados en Linux](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9f630-149">Continue creating the cluster as described in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

## <span data-ttu-id="9f630-150"><a name="usegiraph"></a>¿Cómo uso Giraph en HDInsight?</span><span class="sxs-lookup"><span data-stu-id="9f630-150"><a name="usegiraph"></a>How do I use Giraph in HDInsight?</span></span>

<span data-ttu-id="9f630-151">Después de que se ha creado el clúster, use estos pasos para ejecutar el ejemplo SimpleShortestPathsComputation incluido con Giraph.</span><span class="sxs-lookup"><span data-stu-id="9f630-151">Once the cluster has been created, use the following steps to run the SimpleShortestPathsComputation example included with Giraph.</span></span> <span data-ttu-id="9f630-152">En este ejemplo se usa la implementación de [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) básica para buscar la ruta más corta entre los objetos de un gráfico.</span><span class="sxs-lookup"><span data-stu-id="9f630-152">This example uses the basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementation for finding the shortest path between objects in a graph.</span></span>

1. <span data-ttu-id="9f630-153">Conéctese al clúster de HDInsight con SSH:</span><span class="sxs-lookup"><span data-stu-id="9f630-153">Connect to the HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="9f630-154">Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="9f630-154">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="9f630-155">Use el comando siguiente para crear un archivo denominado **tiny_graph.txt**:</span><span class="sxs-lookup"><span data-stu-id="9f630-155">Use the following command to create a file named **tiny_graph.txt**:</span></span>

    ```bash
    nano tiny_graph.txt
    ```

    <span data-ttu-id="9f630-156">Use el texto siguiente como contenido de este archivo:</span><span class="sxs-lookup"><span data-stu-id="9f630-156">Use the following text as the contents of this file:</span></span>

    ```text
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    <span data-ttu-id="9f630-157">Estos datos describen una relación entre los objetos de un gráfico dirigido, mediante el formato `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span><span class="sxs-lookup"><span data-stu-id="9f630-157">This data describes a relationship between objects in a directed graph, by using the format `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span></span> <span data-ttu-id="9f630-158">Cada línea representa una relación entre un objeto `source_id` y uno varios objetos `dest_id`.</span><span class="sxs-lookup"><span data-stu-id="9f630-158">Each line represents a relationship between a `source_id` object and one or more `dest_id` objects.</span></span> <span data-ttu-id="9f630-159">El valor `edge_value` se puede considerar como la fuerza o la distancia de la conexión entre `source_id` y `dest\_id`.</span><span class="sxs-lookup"><span data-stu-id="9f630-159">The `edge_value` can be thought of as the strength or distance of the connection between `source_id` and `dest\_id`.</span></span>

    <span data-ttu-id="9f630-160">Extrapolados, y usando el valor (o peso) como la distancia entre los objetos, los datos podrían parecerse al siguiente diagrama:</span><span class="sxs-lookup"><span data-stu-id="9f630-160">Drawn out, and using the value (or weight) as the distance between objects, the data might look like the following diagram:</span></span>

    ![tiny_graph.txt drawn as circles with lines of varying distance between](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. <span data-ttu-id="9f630-162">Para guardar el archivo, presione **Ctrl+X**, a continuación, **Y**; finalmente, **Entrar** para aceptar el nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="9f630-162">To save the file, use **Ctrl+X**, then **Y**, and finally **Enter** to accept the file name.</span></span>

4. <span data-ttu-id="9f630-163">Use la siguiente instrucción para almacenar los datos en el almacenamiento principal del clúster de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9f630-163">Use the following to store the data into primary storage for your HDInsight cluster:</span></span>

    ```bash
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. <span data-ttu-id="9f630-164">Ejecute el ejemplo SimpleShortestPathsComputation con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="9f630-164">Run the SimpleShortestPathsComputation example using the following command:</span></span>

    ```bash
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    <span data-ttu-id="9f630-165">Los parámetros que se usan con este comando se describen en la tabla siguiente:</span><span class="sxs-lookup"><span data-stu-id="9f630-165">The parameters used with this command are described in the following table:</span></span>

   | <span data-ttu-id="9f630-166">Parámetro</span><span class="sxs-lookup"><span data-stu-id="9f630-166">Parameter</span></span> | <span data-ttu-id="9f630-167">Qué hace</span><span class="sxs-lookup"><span data-stu-id="9f630-167">What it does</span></span> |
   | --- | --- |
   | `jar` |<span data-ttu-id="9f630-168">El archivo jar que contiene los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="9f630-168">The jar file containing the examples.</span></span> |
   | `org.apache.giraph.GiraphRunner` |<span data-ttu-id="9f630-169">La clase que se usa para iniciar los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="9f630-169">The class used to start the examples.</span></span> |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |<span data-ttu-id="9f630-170">El ejemplo que se usa.</span><span class="sxs-lookup"><span data-stu-id="9f630-170">The example that is used.</span></span> <span data-ttu-id="9f630-171">En este caso, calcula la ruta más corta entre el identificador 1 y los restantes identificadores del gráfico.</span><span class="sxs-lookup"><span data-stu-id="9f630-171">In this example, it computes the shortest path between ID 1 and all other IDs in the graph.</span></span> |
   | `-ca mapred.job.tracker` |<span data-ttu-id="9f630-172">El nodo principal del clúster.</span><span class="sxs-lookup"><span data-stu-id="9f630-172">The headnode for the cluster.</span></span> |
   | `-vif` |<span data-ttu-id="9f630-173">El formato de entrada que se va a usar para los datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="9f630-173">The input format to use for the input data.</span></span> |
   | `-vip` |<span data-ttu-id="9f630-174">El archivo de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="9f630-174">The input data file.</span></span> |
   | `-vof` |<span data-ttu-id="9f630-175">El formato de salida.</span><span class="sxs-lookup"><span data-stu-id="9f630-175">The output format.</span></span> <span data-ttu-id="9f630-176">En este caso, el identificador y el valor como texto sin formato.</span><span class="sxs-lookup"><span data-stu-id="9f630-176">In this example, ID and value as plain text.</span></span> |
   | `-op` |<span data-ttu-id="9f630-177">La ubicación de salida.</span><span class="sxs-lookup"><span data-stu-id="9f630-177">The output location.</span></span> |
   | `-w 2` |<span data-ttu-id="9f630-178">El número de trabajados que se usan.</span><span class="sxs-lookup"><span data-stu-id="9f630-178">The number of workers to use.</span></span> <span data-ttu-id="9f630-179">En este ejemplo, 2.</span><span class="sxs-lookup"><span data-stu-id="9f630-179">In this example, 2.</span></span> |

    <span data-ttu-id="9f630-180">Para obtener más información sobre estos y otros parámetros que se usan en los ejemplos de Giraph, consulte la [guía de inicio rápido de Giraph](http://giraph.apache.org/quick_start.html).</span><span class="sxs-lookup"><span data-stu-id="9f630-180">For more information on these, and other parameters used with Giraph samples, see the [Giraph quickstart](http://giraph.apache.org/quick_start.html).</span></span>

6. <span data-ttu-id="9f630-181">Una vez finalizado el trabajo, los resultados se almacenarán en dos archivos de salida en el directorio **wasb:///example/out/shotestpaths**.</span><span class="sxs-lookup"><span data-stu-id="9f630-181">Once the job has finished, the results are stored in the **/example/out/shotestpaths** directory.</span></span> <span data-ttu-id="9f630-182">Los nombres de los archivos de salida empezarán por **part-m-** y terminarán en un número que indica el primer, segundo, etc., archivo.</span><span class="sxs-lookup"><span data-stu-id="9f630-182">The output file names begin with **part-m-** and end with a number indicating the first, second, etc. file.</span></span> <span data-ttu-id="9f630-183">Para ver la salida, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="9f630-183">Use the following command to view the output:</span></span>

    ```bash
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    <span data-ttu-id="9f630-184">El resultado debe ser similar al siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="9f630-184">The output should appear similar to the following text:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="9f630-185">El ejemplo SimpleShortestPathComputation se ha codificado de forma rígida para comenzar por el identificador de objeto 1 y encontrar la ruta más corta a los demás objetos.</span><span class="sxs-lookup"><span data-stu-id="9f630-185">The SimpleShortestPathComputation example is hard coded to start with object ID 1 and find the shortest path to other objects.</span></span> <span data-ttu-id="9f630-186">La salida tiene el formato de `destination_id` y `distance`.</span><span class="sxs-lookup"><span data-stu-id="9f630-186">The output is in the format of `destination_id` and `distance`.</span></span> <span data-ttu-id="9f630-187">`distance` es el valor (o peso) de los bordes recorridos entre el identificador de objeto 1 y el identificador de destino.</span><span class="sxs-lookup"><span data-stu-id="9f630-187">The `distance` is the value (or weight) of the edges traveled between object ID 1 and the target ID.</span></span>

    <span data-ttu-id="9f630-188">Visualizando estos datos, puede verificar los resultados recorriendo las rutas más cortas entre el identificador 1 y todos los demás objetos.</span><span class="sxs-lookup"><span data-stu-id="9f630-188">Visualizing this data, you can verify the results by traveling the shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="9f630-189">La ruta más corta entre el identificador 1 y el identificador 4 es 5.</span><span class="sxs-lookup"><span data-stu-id="9f630-189">The shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="9f630-190">Este valor es la distancia total entre el <span style="color:orange">identificador 1 y 3</span>, y, a continuación, el <span style="color:red">identificador 3 y 4</span>.</span><span class="sxs-lookup"><span data-stu-id="9f630-190">This value is the total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Drawing of objects as circles with shortest paths drawn between](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a><span data-ttu-id="9f630-192">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9f630-192">Next steps</span></span>

* <span data-ttu-id="9f630-193">[Instalación y uso de Hue en clústeres de HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="9f630-193">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span>

* <span data-ttu-id="9f630-194">[Instalación de Solr en clústeres de HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="9f630-194">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span>
