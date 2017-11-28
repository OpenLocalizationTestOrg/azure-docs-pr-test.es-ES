---
title: "Implementación y administración de topologías de Apache Storm en HDInsight basado en Linux | Microsoft Docs"
description: "Aprenda a implementar, supervisar y administrar topologías de Apache Storm mediante el panel de Storm en HDInsight basado en Linux. Utilice herramientas de Hadoop para Visual Studio"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 35086e62-d6d8-4ccf-8cae-00073464a1e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: b9e82463030807d2674594e73f762fe93515d423
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a><span data-ttu-id="cc0bb-104">Implementación y administración de topologías de Apache Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="cc0bb-104">Deploy and manage Apache Storm topologies on HDInsight</span></span>

<span data-ttu-id="cc0bb-105">En este documento, aprenderá los aspectos básicos de administración y supervisión de las topologías de Storm que se ejecutan en clústeres de Storm en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-105">In this document, learn the basics of managing and monitoring Storm topologies running on Storm on HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc0bb-106">Para realizar los pasos que se describen en este artículo se requiere un clúster de Storm basado en Linux en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-106">The steps in this article require a Linux-based Storm on HDInsight cluster.</span></span> <span data-ttu-id="cc0bb-107">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="cc0bb-108">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="cc0bb-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 
>
> <span data-ttu-id="cc0bb-109">Para obtener información sobre la implementación y la supervisar de topologías en HDInsight basado en Windows, vea [Implementar y administrar topologías de Apache Storm en HDInsight basado en Windows](hdinsight-storm-deploy-monitor-topology.md)</span><span class="sxs-lookup"><span data-stu-id="cc0bb-109">For information on deploying and monitoring topologies on Windows-based HDInsight, see [Deploy and manage Apache Storm topologies on Windows-based HDInsight](hdinsight-storm-deploy-monitor-topology.md)</span></span>


## <a name="prerequisites"></a><span data-ttu-id="cc0bb-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cc0bb-110">Prerequisites</span></span>

* <span data-ttu-id="cc0bb-111">**Clúster de Storm basado en Linux en HDInsight**: consulte [Introducción a Apache Storm en HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) para conocer los pasos para crear un clúster.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-111">**A Linux-based Storm on HDInsight cluster**: see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) for steps on creating a cluster</span></span>

* <span data-ttu-id="cc0bb-112">**Familiaridad con SSH y SCP** (opcional): para obtener más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="cc0bb-112">(Optional) **Familiarity with SSH and SCP**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="cc0bb-113">(Opcional) **Visual Studio**: SDK de Azure 2.5.1 o versiones más recientes y Herramientas de Data Lake para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-113">(Optional) **Visual Studio**: Azure SDK 2.5.1 or newer and the Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="cc0bb-114">Para más información, consulte [Introducción al uso de Herramientas de Data Lake para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cc0bb-114">For more information, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    <span data-ttu-id="cc0bb-115">Una de las siguientes versiones de Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="cc0bb-115">One of the following versions of Visual Studio:</span></span>

  * <span data-ttu-id="cc0bb-116">Visual Studio 2012 con [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="cc0bb-116">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

  * <span data-ttu-id="cc0bb-117">Visual Studio 2013 con [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) o [Visual Studio Community 2013](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="cc0bb-117">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>
  * [<span data-ttu-id="cc0bb-118">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="cc0bb-118">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/)

  * <span data-ttu-id="cc0bb-119">Visual Studio 2015 (cualquier edición)</span><span class="sxs-lookup"><span data-stu-id="cc0bb-119">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="cc0bb-120">Visual Studio 2017 (cualquier edición).</span><span class="sxs-lookup"><span data-stu-id="cc0bb-120">Visual Studio 2017 (any edition).</span></span> <span data-ttu-id="cc0bb-121">Herramientas de Data Lake para Visual Studio 2017 se instalan como parte de la carga de trabajo de Azure.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-121">Data Lake Tools for Visual Studio 2017 are installed as part of the Azure Workload.</span></span>

## <a name="submit-a-topology-visual-studio"></a><span data-ttu-id="cc0bb-122">Envío de una topología: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cc0bb-122">Submit a topology: Visual Studio</span></span>

<span data-ttu-id="cc0bb-123">Las herramientas de HDInsight puede utilizarse para enviar las topologías de C# o híbridas al clúster de Storm.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-123">The HDInsight Tools can be used to submit C# or hybrid topologies to your Storm cluster.</span></span> <span data-ttu-id="cc0bb-124">Los pasos siguientes usan una aplicación de muestra.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-124">The following steps use a sample application.</span></span> <span data-ttu-id="cc0bb-125">Para obtener información sobre cómo crear sus propias topologías con las herramientas de HDInsight, consulte [Desarrollo de las topologías de C# mediante las herramientas de HDInsight para Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="cc0bb-125">For information about creating your own topologies by using the HDInsight Tools, see [Develop C# topologies using the HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

1. <span data-ttu-id="cc0bb-126">Si todavía no tiene instalada la versión más reciente de las herramientas de Data Lake para Visual Studio, consulte [Introducción al uso de Herramientas de Data Lake para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cc0bb-126">If you have not already installed the latest version of the Data Lake tools for Visual Studio, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="cc0bb-127">Herramientas de Data Lake para Visual Studio anteriormente se llamaban Herramientas de HDInsight para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-127">The Data Lake Tools for Visual Studio were formerly called the HDInsight Tools for Visual Studio.</span></span>
    >
    > <span data-ttu-id="cc0bb-128">Herramientas de Data Lake para Visual Studio están incluidas en la __carga de trabajo de Azure__ para Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-128">Data Lake Tools for Visual Studio are included in the __Azure Workload__ for Visual Studio 2017.</span></span>

2. <span data-ttu-id="cc0bb-129">Abra Visual Studio, seleccione **Archivo** > **Nuevo** > **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-129">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="cc0bb-130">En el cuadro de diálogo **Nuevo proyecto**, expanda **Instalado** > **Plantillas** y seleccione **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-130">In the **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="cc0bb-131">En la lista de plantillas, seleccione **Muestra de Storm**.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-131">From the list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="cc0bb-132">En la parte inferior del cuadro de diálogo, escriba un nombre para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-132">At the bottom of the dialog box, type a name for the application.</span></span>

    ![imagen](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. <span data-ttu-id="cc0bb-134">En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto y seleccione **Submit to Storm on HDInsight** (Enviar a Storm en HDInsight).</span><span class="sxs-lookup"><span data-stu-id="cc0bb-134">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cc0bb-135">Si se le solicita, introduzca las credenciales de inicio de sesión de su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-135">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="cc0bb-136">Si tiene más de una suscripción, inicie sesión en la que contenga el clúster de Storm en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-136">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="cc0bb-137">Seleccione el clúster de Storm en HDInsight desde el menú desplegable **Storm Cluster** (Clúster de Storm y seleccione **Submit** (Enviar).</span><span class="sxs-lookup"><span data-stu-id="cc0bb-137">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="cc0bb-138">Puede supervisar si el envío es correcto mediante la ventana **Salida** .</span><span class="sxs-lookup"><span data-stu-id="cc0bb-138">You can monitor whether the submission is successful by using the **Output** window.</span></span>

## <a name="submit-a-topology-ssh-and-the-storm-command"></a><span data-ttu-id="cc0bb-139">Envío de una topología: SSH y el comando Storm</span><span class="sxs-lookup"><span data-stu-id="cc0bb-139">Submit a topology: SSH and the Storm command</span></span>

1. <span data-ttu-id="cc0bb-140">Use SSH para conectarse al clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-140">Use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="cc0bb-141">Reemplace **USERNAME** por el nombre de su inicio de sesión de SSH.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-141">Replace **USERNAME** the name of your SSH login.</span></span> <span data-ttu-id="cc0bb-142">Reemplace **CLUSTERNAME** por el nombre del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-142">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="cc0bb-143">Para obtener más información sobre cómo establecer una conexión mediante SSH a su clúster de HDInsight, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="cc0bb-143">For more information on using SSH to connect to your HDInsight cluster, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="cc0bb-144">Use el comando siguiente para iniciar una topología de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cc0bb-144">Use the following command to start an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    <span data-ttu-id="cc0bb-145">Este comando inicia la topología WordCount de ejemplo en el clúster.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-145">This command starts the example WordCount topology on the cluster.</span></span> <span data-ttu-id="cc0bb-146">Esta topología generará frases de forma aleatoria y contará la aparición de cada palabra en las oraciones.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-146">This topology randomly generate sentences and count the occurrence of each word in the sentences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cc0bb-147">Al enviar la topología al clúster, primero debe copiar el archivo jar que contiene el clúster antes de usar el comando `storm`.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-147">When submitting topology to the cluster, you must first copy the jar file containing the cluster before using the `storm` command.</span></span> <span data-ttu-id="cc0bb-148">Para copiar el archivo en el clúster, puede usar el comando `scp`.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-148">To copy the file to the cluster, you can use the `scp` command.</span></span> <span data-ttu-id="cc0bb-149">Por ejemplo: `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="cc0bb-149">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
   >
   > <span data-ttu-id="cc0bb-150">El ejemplo de WordCount, y otros ejemplos de inicio de Storm, ya están incluidos en el clúster en `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-150">The WordCount example, and other storm starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

## <a name="submit-a-topology-programmatically"></a><span data-ttu-id="cc0bb-151">Envío de una topología: de manera programática</span><span class="sxs-lookup"><span data-stu-id="cc0bb-151">Submit a topology: programmatically</span></span>

<span data-ttu-id="cc0bb-152">Mediante programación, puede implementar una topología en Storm en HDInsight estableciendo una comunicación con el servicio Nimbus hospedado en el clúster.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-152">You can programmatically deploy a topology to Storm on HDInsight by communicating with the Nimbus service hosted in your cluster.</span></span> <span data-ttu-id="cc0bb-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) proporciona un ejemplo de aplicación de Java que muestra cómo implementar e iniciar una topología a través del servicio Nimbus.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) provides an example Java application that demonstrates how to deploy and start a topology through the Nimbus service.</span></span>

## <a name="monitor-and-manage-visual-studio"></a><span data-ttu-id="cc0bb-154">Supervisión y administración: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cc0bb-154">Monitor and manage: Visual Studio</span></span>

<span data-ttu-id="cc0bb-155">Cuando una topología se envía correctamente con Visual Studio, aparece la vista **Topologías de Storm** del clúster.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-155">When a topology has been successfully submitted using Visual Studio, the **Storm Topologies** view for the cluster appears.</span></span> <span data-ttu-id="cc0bb-156">Seleccione la topología de la lista para ver información acerca de la topología de ejecución.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-156">Select the topology from the list to view information about the running topology.</span></span>

![supervisión de visual studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> <span data-ttu-id="cc0bb-158">También puede ver las **topologías de Storm** en el **Explorador de servidores** expandiendo **Azure** > **HDInsight** y, después, haciendo clic con el botón derecho en un clúster de Storm en HDInsight y seleccionando **View Storm Topologies** (Ver topologías de Storm).</span><span class="sxs-lookup"><span data-stu-id="cc0bb-158">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

<span data-ttu-id="cc0bb-159">Seleccione la forma de los spouts o bolts para ver información sobre estos componentes.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-159">Select the shape for the spouts or bolts to view information about these components.</span></span> <span data-ttu-id="cc0bb-160">Se abrirá una ventana nueva para cada elemento seleccionado.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-160">A new window opens for each item selected.</span></span>

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="cc0bb-161">Desactivar y reactivar</span><span class="sxs-lookup"><span data-stu-id="cc0bb-161">Deactivate and reactivate</span></span>

<span data-ttu-id="cc0bb-162">Al desactivar una topología se pone en pausa hasta que se elimine o se reactive.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-162">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="cc0bb-163">Para realizar estas operaciones, use los botones __Desactivar__ y __Reactivar__ que se encuentra en la parte superior del __Resumen de las topologías__.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-163">To perform these operations, use the __Deactivate__ and __Reactivate__ buttons at the top of the __Topology Summary__.</span></span>

### <a name="rebalance"></a><span data-ttu-id="cc0bb-164">Reequilibrar</span><span class="sxs-lookup"><span data-stu-id="cc0bb-164">Rebalance</span></span>

<span data-ttu-id="cc0bb-165">El reequilibrio de una topología permite que el sistema revise el paralelismo de la topología.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-165">Rebalancing a topology allows the system to revise the parallelism of the topology.</span></span> <span data-ttu-id="cc0bb-166">Por ejemplo, si cambió el tamaño del clúster para agregar más notas, el reequilibrio permite que una topología vea los nodos nuevos.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-166">For example, if you have resized the cluster to add more notes, rebalancing allows a topology to see the new nodes.</span></span>

<span data-ttu-id="cc0bb-167">Para reequilibrar una topología, use el botón __Reequilibrar__ que se encuentra en la parte superior del __Resumen de las topologías__.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-167">To rebalance a topology, use the __Rebalance__ button at the top of the __Topology Summary__.</span></span>

> [!WARNING]
> <span data-ttu-id="cc0bb-168">El reequilibrio de una topología desactiva primero la topología, redistribuye los trabajadores de manera uniforme en el clúster y luego devuelve finalmente la topología al estado en el que se encontraba antes de que se produjera el reequilibrio.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-168">Rebalancing a topology first deactivates the topology, then redistributes workers evenly across the cluster, then finally returns the topology to the state it was in before rebalancing occurred.</span></span> <span data-ttu-id="cc0bb-169">Por tanto, si la topología estaba activa, se activa de nuevo.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-169">So if the topology was active, it becomes active again.</span></span> <span data-ttu-id="cc0bb-170">Si se desactivó, seguirá desactivada.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-170">If it was deactivated, it remains deactivated.</span></span>

### <a name="kill-a-topology"></a><span data-ttu-id="cc0bb-171">Terminación de una topología</span><span class="sxs-lookup"><span data-stu-id="cc0bb-171">Kill a topology</span></span>

<span data-ttu-id="cc0bb-172">Las topologías de Storm continúan ejecutándose hasta que se detengan o se elimine el clúster.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-172">Storm topologies continue running until they are stopped or the cluster is deleted.</span></span> <span data-ttu-id="cc0bb-173">Para detener una topología, use el botón __Terminar__ que se encuentra en la parte superior del __Resumen de las topologías__.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-173">To stop a topology, use the __Kill__ button at the top of the __Topology Summary__.</span></span>

## <a name="monitor-and-manage-ssh-and-the-storm-command"></a><span data-ttu-id="cc0bb-174">Supervisión y administración: SSH y el comando Storm</span><span class="sxs-lookup"><span data-stu-id="cc0bb-174">Monitor and manage: SSH and the Storm command</span></span>

<span data-ttu-id="cc0bb-175">La utilidad `storm` le permite trabajar con topologías en ejecución desde la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-175">The `storm` utility allows you to work with running topologies from the command line.</span></span> <span data-ttu-id="cc0bb-176">Use `storm -h` para obtener una lista completa de comandos.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-176">Use `storm -h` for a full list of commands.</span></span>

### <a name="list-topologies"></a><span data-ttu-id="cc0bb-177">Topologías de lista</span><span class="sxs-lookup"><span data-stu-id="cc0bb-177">List topologies</span></span>

<span data-ttu-id="cc0bb-178">Use el siguiente comando para enumerar todas las topologías en ejecución:</span><span class="sxs-lookup"><span data-stu-id="cc0bb-178">Use the following command to list all running topologies:</span></span>

    storm list

<span data-ttu-id="cc0bb-179">Este comando devuelve información similar al texto siguiente:</span><span class="sxs-lookup"><span data-stu-id="cc0bb-179">This command returns information similar to the following text:</span></span>

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="cc0bb-180">Desactivar y reactivar</span><span class="sxs-lookup"><span data-stu-id="cc0bb-180">Deactivate and reactivate</span></span>

<span data-ttu-id="cc0bb-181">Al desactivar una topología se pone en pausa hasta que se elimine o se reactive.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-181">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="cc0bb-182">Use el comando siguiente para desactivar y reactivar:</span><span class="sxs-lookup"><span data-stu-id="cc0bb-182">Use the following command to deactivate and reactivate:</span></span>

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a><span data-ttu-id="cc0bb-183">Eliminar una topología de ejecución</span><span class="sxs-lookup"><span data-stu-id="cc0bb-183">Kill a running topology</span></span>

<span data-ttu-id="cc0bb-184">Las topologías de Storm, una vez iniciadas, se siguen ejecutando hasta que se detengan.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-184">Storm topologies, once started, continue running until stopped.</span></span> <span data-ttu-id="cc0bb-185">Para detener una topología, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="cc0bb-185">To stop a topology, use the following command:</span></span>

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a><span data-ttu-id="cc0bb-186">Reequilibrar</span><span class="sxs-lookup"><span data-stu-id="cc0bb-186">Rebalance</span></span>

<span data-ttu-id="cc0bb-187">El reequilibrio de una topología permite que el sistema revise el paralelismo de la topología.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-187">Rebalancing a topology allows the system to revise the parallelism of the topology.</span></span> <span data-ttu-id="cc0bb-188">Por ejemplo, si cambió el tamaño del clúster para agregar más notas, el reequilibrio permite que una topología vea los nodos nuevos.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-188">For example, if you have resized the cluster to add more notes, rebalancing allows a topology to see the new nodes.</span></span>

> [!WARNING]
> <span data-ttu-id="cc0bb-189">El reequilibrio de una topología desactiva primero la topología, redistribuye los trabajadores de manera uniforme en el clúster y luego devuelve finalmente la topología al estado en el que se encontraba antes de que se produjera el reequilibrio.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-189">Rebalancing a topology first deactivates the topology, then redistributes workers evenly across the cluster, then finally returns the topology to the state it was in before rebalancing occurred.</span></span> <span data-ttu-id="cc0bb-190">Por tanto, si la topología estaba activa, se activa de nuevo.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-190">So if the topology was active, it becomes active again.</span></span> <span data-ttu-id="cc0bb-191">Si se desactivó, seguirá desactivada.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-191">If it was deactivated, it remains deactivated.</span></span>

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a><span data-ttu-id="cc0bb-192">Supervisión y administración: IU de Storm</span><span class="sxs-lookup"><span data-stu-id="cc0bb-192">Monitor and manage: Storm UI</span></span>

<span data-ttu-id="cc0bb-193">La interfaz de usuario de Storm ofrece una interfaz web para trabajar con topologías en ejecución y se incluye en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-193">The Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span> <span data-ttu-id="cc0bb-194">Para ver la IU de Storm, use un explorador web para abrir **https://CLUSTERNAME.azurehdinsight.net/stormui**, donde **CLUSTERNAME** es el nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-194">To view the Storm UI, use a web browser to open **https://CLUSTERNAME.azurehdinsight.net/stormui**, where **CLUSTERNAME** is the name of your cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="cc0bb-195">Si se le pide que ofrezca un nombre de usuario y una contraseña, escriba el administrador de clústeres (admin) y la contraseña que usó al crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-195">If asked to provide a user name and password, enter the cluster administrator (admin) and password that you used when creating the cluster.</span></span>

### <a name="main-page"></a><span data-ttu-id="cc0bb-196">Página principal</span><span class="sxs-lookup"><span data-stu-id="cc0bb-196">Main page</span></span>

<span data-ttu-id="cc0bb-197">La página principal de la interfaz de usuario de Storm ofrece la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="cc0bb-197">The main page of the Storm UI provides the following information:</span></span>

* <span data-ttu-id="cc0bb-198">**Resumen del clúster**: información básica sobre el clúster de Storm.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-198">**Cluster summary**: Basic information about the Storm cluster.</span></span>
* <span data-ttu-id="cc0bb-199">**Resumen de las topologías**: una lista de las topologías en ejecución.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-199">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="cc0bb-200">Use los vínculos de esta sección para obtener más información sobre las topologías específicas.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-200">Use the links in this section to view more information about specific topologies.</span></span>
* <span data-ttu-id="cc0bb-201">**Resumen de supervisor**: información acerca del supervisor de Storm.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-201">**Supervisor summary**: Information about the Storm supervisor.</span></span>
* <span data-ttu-id="cc0bb-202">**Configuración de Nimbus**: configuración de Nimbus del clúster.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-202">**Nimbus configuration**: Nimbus configuration for the cluster.</span></span>

### <a name="topology-summary"></a><span data-ttu-id="cc0bb-203">Resumen de las topologías</span><span class="sxs-lookup"><span data-stu-id="cc0bb-203">Topology summary</span></span>

<span data-ttu-id="cc0bb-204">Si selecciona un vínculo desde la sección **Resumen de la topología** , se mostrará la siguiente información sobre la topología.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-204">Selecting a link from the **Topology summary** section displays the following information about the topology:</span></span>

* <span data-ttu-id="cc0bb-205">**Resumen de la topología**: información básica sobre la topología.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-205">**Topology summary**: Basic information about the topology.</span></span>
* <span data-ttu-id="cc0bb-206">**Acciones de topología**: acciones de administración que puede realizar para la topología.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-206">**Topology actions**: Management actions that you can perform for the topology.</span></span>

  * <span data-ttu-id="cc0bb-207">**Activar**: reanuda el procesamiento de una topología desactivada.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-207">**Activate**: Resumes processing of a deactivated topology.</span></span>
  * <span data-ttu-id="cc0bb-208">**Desactivar**: pausa una topología en ejecución.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-208">**Deactivate**: Pauses a running topology.</span></span>
  * <span data-ttu-id="cc0bb-209">**Reequilibrar**: ajusta el paralelismo de la topología.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-209">**Rebalance**: Adjusts the parallelism of the topology.</span></span> <span data-ttu-id="cc0bb-210">Debe volver a equilibrar las topologías en ejecución después de haber cambiado el número de nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-210">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span></span> <span data-ttu-id="cc0bb-211">Esta operación permite que la topología ajuste el paralelismo para compensar el mayor o menor número de nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-211">This operation allows the topology to adjust parallelism to compensate for the increased or decreased number of nodes in the cluster.</span></span>

    <span data-ttu-id="cc0bb-212">Para más información, consulte la entrada de blog <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Understanding the parallelism of a Storm topology</a>.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-212">For more information, see <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Understanding the parallelism of a Storm topology</a>.</span></span>
  * <span data-ttu-id="cc0bb-213">**Eliminar**: finaliza una topología de Storm tras el tiempo de espera especificado.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-213">**Kill**: Terminates a Storm topology after the specified timeout.</span></span>
* <span data-ttu-id="cc0bb-214">**Estadísticas de topología**: estadísticas sobre la topología.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-214">**Topology stats**: Statistics about the topology.</span></span> <span data-ttu-id="cc0bb-215">Para establecer el período de las entradas restantes en la página, use los vínculos que se encuentran en la columna **Ventana**.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-215">To set the timeframe for the remaining entries on the page, use the links in the **Window** column.</span></span>
* <span data-ttu-id="cc0bb-216">**Spouts**: los spouts que usa la topología.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-216">**Spouts**: The spouts used by the topology.</span></span> <span data-ttu-id="cc0bb-217">Use los vínculos de esta sección para obtener más información acerca de spouts específicos.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-217">Use the links in this section to view more information about specific spouts.</span></span>
* <span data-ttu-id="cc0bb-218">**Bolts**: los bolts que usa la topología.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-218">**Bolts**: The bolts used by the topology.</span></span> <span data-ttu-id="cc0bb-219">Use los vínculos de esta sección para obtener más información acerca de bolts específicos.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-219">Use the links in this section to view more information about specific bolts.</span></span>
* <span data-ttu-id="cc0bb-220">**Configuración de la topología**: la configuración de la topología seleccionada.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-220">**Topology configuration**: The configuration of the selected topology.</span></span>

### <a name="spout-and-bolt-summary"></a><span data-ttu-id="cc0bb-221">Resumen de spouts y bolts</span><span class="sxs-lookup"><span data-stu-id="cc0bb-221">Spout and Bolt summary</span></span>

<span data-ttu-id="cc0bb-222">Si se selecciona un spout en la sección **Spouts** o **Bolts**, se muestra la siguiente información sobre el elemento seleccionado:</span><span class="sxs-lookup"><span data-stu-id="cc0bb-222">Selecting a spout from the **Spouts** or **Bolts** sections displays the following information about the selected item:</span></span>

* <span data-ttu-id="cc0bb-223">**Resumen de componentes**: información básica acerca del spout o bolt.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-223">**Component summary**: Basic information about the spout or bolt.</span></span>
* <span data-ttu-id="cc0bb-224">**Estadísticas de spouts/bolts**: estadísticas sobre el spout o bolt.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-224">**Spout/Bolt stats**: Statistics about the spout or bolt.</span></span> <span data-ttu-id="cc0bb-225">Para establecer el período de las entradas restantes en la página, use los vínculos que se encuentran en la columna **Ventana**.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-225">To set the timeframe for the remaining entries on the page, use the links in the **Window** column.</span></span>
* <span data-ttu-id="cc0bb-226">**Estadísticas de entrada** (solo bolt): información sobre las secuencias de entrada consumidas por el bolt.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-226">**Input stats** (bolt only): Information about the input streams consumed by the bolt.</span></span>
* <span data-ttu-id="cc0bb-227">**Estadísticas de salida**: información sobre las secuencias emitidas por este spout o bolt</span><span class="sxs-lookup"><span data-stu-id="cc0bb-227">**Output stats**: Information about the streams emitted by this spout or bolt.</span></span>
* <span data-ttu-id="cc0bb-228">**Ejecutores**: información sobre las instancias del spout o bolt.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-228">**Executors**: Information about the instances of the spout or bolt.</span></span> <span data-ttu-id="cc0bb-229">Seleccione la entrada **Puerto** de un ejecutor específico para ver un registro de información de diagnóstico generado por esta instancia.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-229">Select the **Port** entry for a specific executor to view a log of diagnostic information produced for this instance.</span></span>
* <span data-ttu-id="cc0bb-230">**Errores**: cualquier información de error de este spout o bolt.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-230">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="monitor-and-manage-rest-api"></a><span data-ttu-id="cc0bb-231">Supervisión y administración: API de REST</span><span class="sxs-lookup"><span data-stu-id="cc0bb-231">Monitor and manage: REST API</span></span>

<span data-ttu-id="cc0bb-232">La interfaz de usuario de Storm se basa en la API de REST, lo que permite realizar una funcionalidad similar de administración y supervisión mediante la API de REST.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-232">The Storm UI is built on top of the REST API, so you can perform similar management and monitoring functionality by using the REST API.</span></span> <span data-ttu-id="cc0bb-233">Puede usar la API de REST para crear herramientas personalizadas para administrar y supervisar las topologías de Storm.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-233">You can use the REST API to create custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="cc0bb-234">Para más información, vea la [API de REST de la IU de Storm](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span><span class="sxs-lookup"><span data-stu-id="cc0bb-234">For more information, see [Storm UI REST API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span></span> <span data-ttu-id="cc0bb-235">La siguiente información es específica para usar la API de REST con Apache Storm en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-235">The following information is specific to using the REST API with Apache Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc0bb-236">La API de REST de Storm no está públicamente disponible a través de Internet y debe tener acceso mediante un túnel SSH en el nodo principal del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-236">The Storm REST API is not publicly available over the internet, and must be accessed using an SSH tunnel to the HDInsight cluster head node.</span></span> <span data-ttu-id="cc0bb-237">Para información sobre la creación y el uso de un túnel SSH, consulte [Uso de la tunelización SSH para tener acceso a la interfaz de usuario web de Ambari, ResourceManager, JobHistory, NameNode, Oozie y otras interfaces de usuario web](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="cc0bb-237">For information on creating and using an SSH tunnel, see [Use SSH Tunneling to access Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

### <a name="base-uri"></a><span data-ttu-id="cc0bb-238">URI base</span><span class="sxs-lookup"><span data-stu-id="cc0bb-238">Base URI</span></span>

<span data-ttu-id="cc0bb-239">El URI base de la API de REST en los clústeres de HDInsight basado en Linux está disponible en el nodo principal en **https://HEADNODEFQDN:8744/api/v1/**.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-239">The base URI for the REST API on Linux-based HDInsight clusters is available on the head node at **https://HEADNODEFQDN:8744/api/v1/**.</span></span> <span data-ttu-id="cc0bb-240">El nombre de dominio del nodo principal se genera durante la creación de clúster y no es estático.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-240">The domain name of the head node is generated during cluster creation and is not static.</span></span>

<span data-ttu-id="cc0bb-241">Puede encontrar el nombre de dominio completo (FQDN) del nodo principal del clúster de varias maneras distintas:</span><span class="sxs-lookup"><span data-stu-id="cc0bb-241">You can find the fully qualified domain name (FQDN) for the cluster head node in several different ways:</span></span>

* <span data-ttu-id="cc0bb-242">**Desde una sesión de SSH**: use el comando `headnode -f` desde una sesión SSH al clúster.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-242">**From an SSH session**: Use the command `headnode -f` from an SSH session to the cluster.</span></span>
* <span data-ttu-id="cc0bb-243">**Desde Web de Ambari**: seleccione **Servicios** en la parte superior de la pantalla y, luego, seleccione **Storm**.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-243">**From Ambari Web**: Select **Services** from the top of the page, then select **Storm**.</span></span> <span data-ttu-id="cc0bb-244">En la pestaña **Resumen**, seleccione **Storm UI Server** (Servidor de IU de Storm).</span><span class="sxs-lookup"><span data-stu-id="cc0bb-244">From the **Summary** tab, select **Storm UI Server**.</span></span> <span data-ttu-id="cc0bb-245">El FQDN del nodo donde se ejecutan IU de Storm y la API de REST está en la parte superior de la página.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-245">The FQDN of the node that the Storm UI and REST API is running is at the top of the page.</span></span>
* <span data-ttu-id="cc0bb-246">**Desde la API de REST de Ambari**: use el comando `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` para recuperar información sobre el nodo en que se ejecutan la IU de Storm y la API de REST.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-246">**From Ambari REST API**: Use the command `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` to retrieve information about the node that the Storm UI and REST API are running on.</span></span> <span data-ttu-id="cc0bb-247">Reemplace **PASSWORD** por la contraseña de administrador del clúster.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-247">Replace **PASSWORD** with the admin password for the cluster.</span></span> <span data-ttu-id="cc0bb-248">Reemplace **CLUSTERNAME** por el nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-248">Replace **CLUSTERNAME** with the cluster name.</span></span> <span data-ttu-id="cc0bb-249">En la respuesta, la entrada "host_name" contiene el FQDN del nodo.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-249">In the response, the "host_name" entry contains the FQDN of the node.</span></span>

### <a name="authentication"></a><span data-ttu-id="cc0bb-250">Autenticación</span><span class="sxs-lookup"><span data-stu-id="cc0bb-250">Authentication</span></span>

<span data-ttu-id="cc0bb-251">Las solicitudes a la API de REST deben usar la **autenticación básica**; use el nombre y la contraseña de administrador del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-251">Requests to the REST API must use **basic authentication**, so you use the HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="cc0bb-252">Dado que la autenticación básica se envía mediante texto no cifrado, **siempre** debe usar HTTPS para proteger las comunicaciones con el clúster.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-252">Because basic authentication is sent by using clear text, you should **always** use HTTPS to secure communications with the cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="cc0bb-253">Valores devueltos</span><span class="sxs-lookup"><span data-stu-id="cc0bb-253">Return values</span></span>

<span data-ttu-id="cc0bb-254">La información que se devuelve de la API de REST solo se puede utilizar desde dentro del clúster o de máquinas virtuales en la misma red virtual de Azure que el clúster.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-254">Information that is returned from the REST API may only be usable from within the cluster or virtual machines on the same Azure Virtual Network as the cluster.</span></span> <span data-ttu-id="cc0bb-255">Por ejemplo, no se puede obtener el acceso desde Internet al nombre de dominio completo (FQDN) devuelto para servidores de Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="cc0bb-255">For example, the fully qualified domain name (FQDN) returned for Zookeeper servers is not be accessible from the Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc0bb-256">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cc0bb-256">Next Steps</span></span>

<span data-ttu-id="cc0bb-257">Ahora que aprendió a implementar y supervisar topologías mediante el panel de Storm, aprenda a [Desarrollar topologías basadas en Java mediante Maven](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="cc0bb-257">Now that you've learned how to deploy and monitor topologies by using the Storm Dashboard, learn how to [Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="cc0bb-258">Para obtener una lista con más topologías de ejemplo, consulte [Topologías de ejemplo para Storm en HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="cc0bb-258">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
