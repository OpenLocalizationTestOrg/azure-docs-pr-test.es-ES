---
title: aaaInstall y usar Giraph en HDInsight (Hadoop) - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo usar acciones de Script de clústeres de tooinstall Giraph en HDInsight basados en Linux. Acciones de script permiten clúster de hello toocustomize durante la creación, cambiando la configuración de clúster o instalar utilidades y servicios."
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
ms.openlocfilehash: 0f195b65cebf5e24d1808ef33b95b4d362555521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-tooprocess-large-scale-graphs"></a><span data-ttu-id="5b356-104">Instalar Giraph en clústeres de Hadoop de HDInsight y usar gráficos de Giraph tooprocess a gran escala</span><span class="sxs-lookup"><span data-stu-id="5b356-104">Install Giraph on HDInsight Hadoop clusters, and use Giraph tooprocess large-scale graphs</span></span>

<span data-ttu-id="5b356-105">Obtenga información acerca de cómo tooinstall Giraph Apache en un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5b356-105">Learn how tooinstall Apache Giraph on an HDInsight cluster.</span></span> <span data-ttu-id="5b356-106">característica de acción de secuencia de comandos de Hola de HDInsight le permite toocustomize el clúster mediante la ejecución de una secuencia de comandos de bash.</span><span class="sxs-lookup"><span data-stu-id="5b356-106">hello script action feature of HDInsight allows you toocustomize your cluster by running a bash script.</span></span> <span data-ttu-id="5b356-107">Las secuencias de comandos pueden ser usado toocustomize clústeres durante y después de crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="5b356-107">Scripts can be used toocustomize clusters during and after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5b356-108">pasos de Hello en este documento requieren un clúster de HDInsight que usa Linux.</span><span class="sxs-lookup"><span data-stu-id="5b356-108">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="5b356-109">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="5b356-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5b356-110">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="5b356-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="5b356-111"><a name="whatis"></a>¿Qué es Giraph?</span><span class="sxs-lookup"><span data-stu-id="5b356-111"><a name="whatis"></a>What is Giraph</span></span>

<span data-ttu-id="5b356-112">[Apache Giraph](http://giraph.apache.org/) permite gráfico tooperform procesamiento por medio de Hadoop y puede utilizarse con HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="5b356-112">[Apache Giraph](http://giraph.apache.org/) allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="5b356-113">Los gráficos modelan las relaciones entre los objetos.</span><span class="sxs-lookup"><span data-stu-id="5b356-113">Graphs model relationships between objects.</span></span> <span data-ttu-id="5b356-114">Por ejemplo, las conexiones de hello entre enrutadores de una red de gran tamaño como Hola Internet o las relaciones entre usuarios de redes sociales.</span><span class="sxs-lookup"><span data-stu-id="5b356-114">For example, hello connections between routers on a large network like hello Internet, or relationships between people on social networks.</span></span> <span data-ttu-id="5b356-115">Procesamiento de gráficos le permite tooreason acerca de las relaciones de hello entre los objetos en un gráfico, como:</span><span class="sxs-lookup"><span data-stu-id="5b356-115">Graph processing allows you tooreason about hello relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="5b356-116">Identificar los posibles amigos según las relaciones actuales.</span><span class="sxs-lookup"><span data-stu-id="5b356-116">Identifying potential friends based on your current relationships.</span></span>

* <span data-ttu-id="5b356-117">Identifica la ruta más corta de hello entre dos equipos en una red.</span><span class="sxs-lookup"><span data-stu-id="5b356-117">Identifying hello shortest route between two computers in a network.</span></span>

* <span data-ttu-id="5b356-118">Calcular la clasificación de la página de Hola de páginas Web.</span><span class="sxs-lookup"><span data-stu-id="5b356-118">Calculating hello page rank of webpages.</span></span>

> [!WARNING]
> <span data-ttu-id="5b356-119">Componentes suministrados con clúster de HDInsight de hello son totalmente compatibles: Microsoft Support le ayuda a tooisolate y resolver los problemas relacionados toothese componentes.</span><span class="sxs-lookup"><span data-stu-id="5b356-119">Components provided with hello HDInsight cluster are fully supported - Microsoft Support helps tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="5b356-120">Componentes personalizados, como Giraph, reciban soporte comercialmente razonable toohelp toofurther solucionar el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b356-120">Custom components, such as Giraph, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="5b356-121">Microsoft Support puede ser capaz de tooresolving problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b356-121">Microsoft Support may be able tooresolving hello issue.</span></span> <span data-ttu-id="5b356-122">Si no es así, debe consultar las comunidades de código abierto donde grandes expertos en esa tecnología.</span><span class="sxs-lookup"><span data-stu-id="5b356-122">If not, you must consult open source communities where deep expertise for that technology is found.</span></span> <span data-ttu-id="5b356-123">Por ejemplo, hay diversos sitios de la comunidad que se pueden usar, como el [foro de MSDN para HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Los proyectos de Apache también tienen sitios de proyecto en [http://apache.org](http://apache.org) (por ejemplo, [Hadoop](http://hadoop.apache.org/)).</span><span class="sxs-lookup"><span data-stu-id="5b356-123">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>


## <a name="what-hello-script-does"></a><span data-ttu-id="5b356-124">El script de Hola hace</span><span class="sxs-lookup"><span data-stu-id="5b356-124">What hello script does</span></span>

<span data-ttu-id="5b356-125">Este script realiza Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="5b356-125">This script performs hello following actions:</span></span>

* <span data-ttu-id="5b356-126">Instala Giraph demasiado`/usr/hdp/current/giraph`</span><span class="sxs-lookup"><span data-stu-id="5b356-126">Installs Giraph too`/usr/hdp/current/giraph`</span></span>

* <span data-ttu-id="5b356-127">Hola copias `giraph-examples.jar` almacenamiento de archivos toodefault (WASB) para el clúster:`/example/jars/giraph-examples.jar`</span><span class="sxs-lookup"><span data-stu-id="5b356-127">Copies hello `giraph-examples.jar` file toodefault storage (WASB) for your cluster: `/example/jars/giraph-examples.jar`</span></span>

## <span data-ttu-id="5b356-128"><a name="install"></a>Instalación de Giraph mediante acciones de script</span><span class="sxs-lookup"><span data-stu-id="5b356-128"><a name="install"></a>Install Giraph using Script Actions</span></span>

<span data-ttu-id="5b356-129">Tooinstall de secuencia de comandos de ejemplo Giraph en un clúster de HDInsight está disponible en hello ubicación siguiente:</span><span class="sxs-lookup"><span data-stu-id="5b356-129">A sample script tooinstall Giraph on an HDInsight cluster is available at hello following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

<span data-ttu-id="5b356-130">Esta sección proporciona instrucciones sobre cómo toouse Hola script de ejemplo al crear el clúster de Hola utilizando Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="5b356-130">This section provides instructions on how toouse hello sample script while creating hello cluster by using hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="5b356-131">Una acción de secuencia de comandos se puede aplicar mediante cualquiera de los siguientes métodos de hello:</span><span class="sxs-lookup"><span data-stu-id="5b356-131">A script action can be applied using any of hello following methods:</span></span>
> * <span data-ttu-id="5b356-132">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b356-132">Azure PowerShell</span></span>
> * <span data-ttu-id="5b356-133">Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="5b356-133">hello Azure CLI</span></span>
> * <span data-ttu-id="5b356-134">Hola HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="5b356-134">hello HDInsight .NET SDK</span></span>
> * <span data-ttu-id="5b356-135">Plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5b356-135">Azure Resource Manager templates</span></span>
> 
> <span data-ttu-id="5b356-136">También puede aplicar tooalready de acciones de script clústeres en ejecución.</span><span class="sxs-lookup"><span data-stu-id="5b356-136">You can also apply script actions tooalready running clusters.</span></span> <span data-ttu-id="5b356-137">Para obtener más información, consulte [Personalización de clústeres de HDInsight mediante la acción de scripts](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5b356-137">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="5b356-138">Empezar a crear un clúster mediante el uso de pasos de hello en [clústeres de HDInsight basados en Linux crear](hdinsight-hadoop-create-linux-clusters-portal.md), pero no se completó la creación.</span><span class="sxs-lookup"><span data-stu-id="5b356-138">Start creating a cluster by using hello steps in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md), but do not complete creation.</span></span>

2. <span data-ttu-id="5b356-139">En hello **configuración opcional** hoja, seleccione **acciones de Script**y proporcionar Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="5b356-139">On hello **Optional Configuration** blade, select **Script Actions**, and provide hello following information:</span></span>

   * <span data-ttu-id="5b356-140">**NOMBRE**: escriba un nombre descriptivo para la acción de secuencia de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b356-140">**NAME**: Enter a friendly name for hello script action.</span></span>

   * <span data-ttu-id="5b356-141">**URI del SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="5b356-141">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span></span>

   * <span data-ttu-id="5b356-142">**PRINCIPAL**: active esta entrada.</span><span class="sxs-lookup"><span data-stu-id="5b356-142">**HEAD**: Check this entry</span></span>

   * <span data-ttu-id="5b356-143">**TRABAJO**: deje esta opción desactivada.</span><span class="sxs-lookup"><span data-stu-id="5b356-143">**WORKER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="5b356-144">**ZOOKEEPER**: deje esta opción desactivada.</span><span class="sxs-lookup"><span data-stu-id="5b356-144">**ZOOKEEPER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="5b356-145">**PARÁMETROS**: deje este campo en blanco.</span><span class="sxs-lookup"><span data-stu-id="5b356-145">**PARAMETERS**: Leave this field blank</span></span>

3. <span data-ttu-id="5b356-146">Final de Hola de hello **acciones de Script**, usar hello **seleccione** configuración del botón toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="5b356-146">At hello bottom of hello **Script Actions**, use hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="5b356-147">Por último, utilice hello **seleccione** situado en la parte inferior de Hola de hello **configuración opcional** información de configuración opcional de hoja toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="5b356-147">Finally, use hello **Select** button at hello bottom of hello **Optional Configuration** blade toosave hello optional configuration information.</span></span>

4. <span data-ttu-id="5b356-148">Continuar con la creación de clúster de hello tal y como se describe en [clústeres de HDInsight basados en Linux crear](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5b356-148">Continue creating hello cluster as described in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

## <span data-ttu-id="5b356-149"><a name="usegiraph"></a>¿Cómo uso Giraph en HDInsight?</span><span class="sxs-lookup"><span data-stu-id="5b356-149"><a name="usegiraph"></a>How do I use Giraph in HDInsight?</span></span>

<span data-ttu-id="5b356-150">Una vez que se haya creado el clúster de hello, utilice Hola pasos toorun hello SimpleShortestPathsComputation ejemplo incluido con Giraph siguiente.</span><span class="sxs-lookup"><span data-stu-id="5b356-150">Once hello cluster has been created, use hello following steps toorun hello SimpleShortestPathsComputation example included with Giraph.</span></span> <span data-ttu-id="5b356-151">Este ejemplo utiliza básica hello [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementación para buscar la ruta de acceso más corta de hello entre los objetos de un gráfico.</span><span class="sxs-lookup"><span data-stu-id="5b356-151">This example uses hello basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementation for finding hello shortest path between objects in a graph.</span></span>

1. <span data-ttu-id="5b356-152">Conecte el clúster de HDInsight de toohello mediante SSH:</span><span class="sxs-lookup"><span data-stu-id="5b356-152">Connect toohello HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="5b356-153">Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5b356-153">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="5b356-154">Comando de uso Hola siguiente toocreate un archivo denominado **tiny_graph.txt**:</span><span class="sxs-lookup"><span data-stu-id="5b356-154">Use hello following command toocreate a file named **tiny_graph.txt**:</span></span>

    ```bash
    nano tiny_graph.txt
    ```

    <span data-ttu-id="5b356-155">Usar hello después de texto como contenido de Hola de este archivo:</span><span class="sxs-lookup"><span data-stu-id="5b356-155">Use hello following text as hello contents of this file:</span></span>

    ```text
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    <span data-ttu-id="5b356-156">Estos datos describen una relación entre los objetos de un gráfico dirigido, con formato de hello `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span><span class="sxs-lookup"><span data-stu-id="5b356-156">This data describes a relationship between objects in a directed graph, by using hello format `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span></span> <span data-ttu-id="5b356-157">Cada línea representa una relación entre un objeto `source_id` y uno varios objetos `dest_id`.</span><span class="sxs-lookup"><span data-stu-id="5b356-157">Each line represents a relationship between a `source_id` object and one or more `dest_id` objects.</span></span> <span data-ttu-id="5b356-158">Hola `edge_value` puede considerarse como la intensidad de Hola o distancia de conexión de hello entre `source_id` y `dest\_id`.</span><span class="sxs-lookup"><span data-stu-id="5b356-158">hello `edge_value` can be thought of as hello strength or distance of hello connection between `source_id` and `dest\_id`.</span></span>

    <span data-ttu-id="5b356-159">Dibujar, y con el valor de hello (o peso) como la distancia de hello entre objetos, datos de hello podrían parecerse Hola siguiente diagrama:</span><span class="sxs-lookup"><span data-stu-id="5b356-159">Drawn out, and using hello value (or weight) as hello distance between objects, hello data might look like hello following diagram:</span></span>

    ![tiny_graph.txt drawn as circles with lines of varying distance between](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. <span data-ttu-id="5b356-161">archivo de hello toosave, use **CTRL+x**, a continuación, **Y**y, finalmente, **ENTRAR** tooaccept nombre de archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b356-161">toosave hello file, use **Ctrl+X**, then **Y**, and finally **Enter** tooaccept hello file name.</span></span>

4. <span data-ttu-id="5b356-162">Usar hello seguir los datos de hello toostore en el almacenamiento principal para el clúster de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="5b356-162">Use hello following toostore hello data into primary storage for your HDInsight cluster:</span></span>

    ```bash
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. <span data-ttu-id="5b356-163">Ejecutar el ejemplo de SimpleShortestPathsComputation Hola Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="5b356-163">Run hello SimpleShortestPathsComputation example using hello following command:</span></span>

    ```bash
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    <span data-ttu-id="5b356-164">en hello en la tabla siguiente se describen los parámetros de Hello utilizados con este comando:</span><span class="sxs-lookup"><span data-stu-id="5b356-164">hello parameters used with this command are described in hello following table:</span></span>

   | <span data-ttu-id="5b356-165">Parámetro</span><span class="sxs-lookup"><span data-stu-id="5b356-165">Parameter</span></span> | <span data-ttu-id="5b356-166">Qué hace</span><span class="sxs-lookup"><span data-stu-id="5b356-166">What it does</span></span> |
   | --- | --- |
   | `jar` |<span data-ttu-id="5b356-167">archivo de Hello jar que contiene ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="5b356-167">hello jar file containing hello examples.</span></span> |
   | `org.apache.giraph.GiraphRunner` |<span data-ttu-id="5b356-168">clase Hello utiliza los ejemplos de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="5b356-168">hello class used toostart hello examples.</span></span> |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |<span data-ttu-id="5b356-169">ejemplo de Hola que se utiliza.</span><span class="sxs-lookup"><span data-stu-id="5b356-169">hello example that is used.</span></span> <span data-ttu-id="5b356-170">En este ejemplo, calcula la ruta de acceso más corta de hello entre el identificador 1 y todos los otros identificadores en el gráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b356-170">In this example, it computes hello shortest path between ID 1 and all other IDs in hello graph.</span></span> |
   | `-ca mapred.job.tracker` |<span data-ttu-id="5b356-171">nodo principal de Hello para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b356-171">hello headnode for hello cluster.</span></span> |
   | `-vif` |<span data-ttu-id="5b356-172">Hola toouse de formato de entrada de datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b356-172">hello input format toouse for hello input data.</span></span> |
   | `-vip` |<span data-ttu-id="5b356-173">archivo de datos de entrada de Hello.</span><span class="sxs-lookup"><span data-stu-id="5b356-173">hello input data file.</span></span> |
   | `-vof` |<span data-ttu-id="5b356-174">formato de salida de Hello.</span><span class="sxs-lookup"><span data-stu-id="5b356-174">hello output format.</span></span> <span data-ttu-id="5b356-175">En este caso, el identificador y el valor como texto sin formato.</span><span class="sxs-lookup"><span data-stu-id="5b356-175">In this example, ID and value as plain text.</span></span> |
   | `-op` |<span data-ttu-id="5b356-176">ubicación de salida de Hello.</span><span class="sxs-lookup"><span data-stu-id="5b356-176">hello output location.</span></span> |
   | `-w 2` |<span data-ttu-id="5b356-177">número de Hola de trabajadores toouse.</span><span class="sxs-lookup"><span data-stu-id="5b356-177">hello number of workers toouse.</span></span> <span data-ttu-id="5b356-178">En este ejemplo, 2.</span><span class="sxs-lookup"><span data-stu-id="5b356-178">In this example, 2.</span></span> |

    <span data-ttu-id="5b356-179">Para obtener más información sobre estos y otros parámetros que se usan con Giraph ejemplos, vea hello [inicio rápido de Giraph](http://giraph.apache.org/quick_start.html).</span><span class="sxs-lookup"><span data-stu-id="5b356-179">For more information on these, and other parameters used with Giraph samples, see hello [Giraph quickstart](http://giraph.apache.org/quick_start.html).</span></span>

6. <span data-ttu-id="5b356-180">Una vez que haya finalizado el trabajo de hello, resultados de Hola se almacenan en hello **/example/out/shotestpaths** directory.</span><span class="sxs-lookup"><span data-stu-id="5b356-180">Once hello job has finished, hello results are stored in hello **/example/out/shotestpaths** directory.</span></span> <span data-ttu-id="5b356-181">Hello nombres de archivo de salida comienzan por **parte-m -** y terminar con un número que indica hello en primer lugar, en segundo lugar, el archivo de etc..</span><span class="sxs-lookup"><span data-stu-id="5b356-181">hello output file names begin with **part-m-** and end with a number indicating hello first, second, etc. file.</span></span> <span data-ttu-id="5b356-182">Usar hello siguiendo la salida del comando tooview hello:</span><span class="sxs-lookup"><span data-stu-id="5b356-182">Use hello following command tooview hello output:</span></span>

    ```bash
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    <span data-ttu-id="5b356-183">salida de Hello debe aparecer toohello similar siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="5b356-183">hello output should appear similar toohello following text:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="5b356-184">ejemplo de Hola a SimpleShortestPathComputation es toostart codificado con objeto de identificador 1 y buscar objetos de tooother de ruta de acceso más cortos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b356-184">hello SimpleShortestPathComputation example is hard coded toostart with object ID 1 and find hello shortest path tooother objects.</span></span> <span data-ttu-id="5b356-185">salida de Hello está en formato de Hola de `destination_id` y `distance`.</span><span class="sxs-lookup"><span data-stu-id="5b356-185">hello output is in hello format of `destination_id` and `distance`.</span></span> <span data-ttu-id="5b356-186">Hola `distance` es el valor de hello (o peso) de los bordes de hello recorridos entre objeto identificador 1 y Hola Id. de destino.</span><span class="sxs-lookup"><span data-stu-id="5b356-186">hello `distance` is hello value (or weight) of hello edges traveled between object ID 1 and hello target ID.</span></span>

    <span data-ttu-id="5b356-187">Visualizar estos datos, puede comprobar los resultados de Hola por las rutas de acceso más cortas de hello en viaje entre el identificador 1 y todos los demás objetos.</span><span class="sxs-lookup"><span data-stu-id="5b356-187">Visualizing this data, you can verify hello results by traveling hello shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="5b356-188">Hola ruta de acceso más corta entre el identificador 1 y 4 de identificador es 5.</span><span class="sxs-lookup"><span data-stu-id="5b356-188">hello shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="5b356-189">Este valor es la distancia total de hello entre <span style="color:orange">identificador 1 y 3</span>y, a continuación, <span style="color:red">identificador 3 y 4</span>.</span><span class="sxs-lookup"><span data-stu-id="5b356-189">This value is hello total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Drawing of objects as circles with shortest paths drawn between](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a><span data-ttu-id="5b356-191">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5b356-191">Next steps</span></span>

* <span data-ttu-id="5b356-192">[Instalación y uso de Hue en clústeres de HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5b356-192">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span>

* <span data-ttu-id="5b356-193">[Instalación de Solr en clústeres de HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5b356-193">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span>
