---
title: "aaaDeploy y administrar topologías de Apache Storm en HDInsight basados en Linux | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toodeploy, supervisar y administrar topologías de Apache Storm con hello aluvión de panel en HDInsight basados en Linux. Utilice herramientas de Hadoop para Visual Studio"
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
ms.openlocfilehash: 3a1edb773089cc596fea423710aa88cf83c7b841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a><span data-ttu-id="5668a-104">Implementación y administración de topologías de Apache Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="5668a-104">Deploy and manage Apache Storm topologies on HDInsight</span></span>

<span data-ttu-id="5668a-105">En este documento, información sobre conceptos básicos de Hola de administración y supervisión de topologías de Storm ejecutando Storm en clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5668a-105">In this document, learn hello basics of managing and monitoring Storm topologies running on Storm on HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5668a-106">Hello pasos de este artículo requieren una tormenta basadas en Linux en clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5668a-106">hello steps in this article require a Linux-based Storm on HDInsight cluster.</span></span> <span data-ttu-id="5668a-107">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="5668a-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5668a-108">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="5668a-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 
>
> <span data-ttu-id="5668a-109">Para obtener información sobre la implementación y la supervisar de topologías en HDInsight basado en Windows, vea [Implementar y administrar topologías de Apache Storm en HDInsight basado en Windows](hdinsight-storm-deploy-monitor-topology.md)</span><span class="sxs-lookup"><span data-stu-id="5668a-109">For information on deploying and monitoring topologies on Windows-based HDInsight, see [Deploy and manage Apache Storm topologies on Windows-based HDInsight](hdinsight-storm-deploy-monitor-topology.md)</span></span>


## <a name="prerequisites"></a><span data-ttu-id="5668a-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5668a-110">Prerequisites</span></span>

* <span data-ttu-id="5668a-111">**Clúster de Storm basado en Linux en HDInsight**: consulte [Introducción a Apache Storm en HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) para conocer los pasos para crear un clúster.</span><span class="sxs-lookup"><span data-stu-id="5668a-111">**A Linux-based Storm on HDInsight cluster**: see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) for steps on creating a cluster</span></span>

* <span data-ttu-id="5668a-112">**Familiaridad con SSH y SCP** (opcional): para obtener más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5668a-112">(Optional) **Familiarity with SSH and SCP**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="5668a-113">(Opcional) **Visual Studio**: Azure SDK 2.5.1 o versiones más recientes y Hola Data Lake Tools para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5668a-113">(Optional) **Visual Studio**: Azure SDK 2.5.1 or newer and hello Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="5668a-114">Para más información, consulte [Introducción al uso de Herramientas de Data Lake para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5668a-114">For more information, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    <span data-ttu-id="5668a-115">Uno de hello después de versiones de Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="5668a-115">One of hello following versions of Visual Studio:</span></span>

  * <span data-ttu-id="5668a-116">Visual Studio 2012 con [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="5668a-116">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

  * <span data-ttu-id="5668a-117">Visual Studio 2013 con [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) o [Visual Studio Community 2013](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="5668a-117">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>
  * [<span data-ttu-id="5668a-118">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="5668a-118">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/)

  * <span data-ttu-id="5668a-119">Visual Studio 2015 (cualquier edición)</span><span class="sxs-lookup"><span data-stu-id="5668a-119">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="5668a-120">Visual Studio 2017 (cualquier edición).</span><span class="sxs-lookup"><span data-stu-id="5668a-120">Visual Studio 2017 (any edition).</span></span> <span data-ttu-id="5668a-121">Data Lake Tools para Visual Studio de 2017 se instalan como parte del programa Hola a cargas de trabajo de Azure.</span><span class="sxs-lookup"><span data-stu-id="5668a-121">Data Lake Tools for Visual Studio 2017 are installed as part of hello Azure Workload.</span></span>

## <a name="submit-a-topology-visual-studio"></a><span data-ttu-id="5668a-122">Envío de una topología: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5668a-122">Submit a topology: Visual Studio</span></span>

<span data-ttu-id="5668a-123">Herramientas de HDInsight de Hello puede ser toosubmit usa C# o híbrida topologías tooyour clúster de Storm.</span><span class="sxs-lookup"><span data-stu-id="5668a-123">hello HDInsight Tools can be used toosubmit C# or hybrid topologies tooyour Storm cluster.</span></span> <span data-ttu-id="5668a-124">Hola pasos usa una aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="5668a-124">hello following steps use a sample application.</span></span> <span data-ttu-id="5668a-125">Para obtener información acerca de cómo crear sus propios topologías mediante las herramientas de HDInsight de hello, consulte [C# desarrollar topologías con hello HDInsight Tools para Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="5668a-125">For information about creating your own topologies by using hello HDInsight Tools, see [Develop C# topologies using hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

1. <span data-ttu-id="5668a-126">Si no ha instalado ya Hola versión más reciente de las herramientas de Data Lake Hola para Visual Studio, consulte [Introducción al uso de Data Lake Tools para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5668a-126">If you have not already installed hello latest version of hello Data Lake tools for Visual Studio, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="5668a-127">Hola Data Lake Tools para Visual Studio se denominaba hello HDInsight Tools para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5668a-127">hello Data Lake Tools for Visual Studio were formerly called hello HDInsight Tools for Visual Studio.</span></span>
    >
    > <span data-ttu-id="5668a-128">Data Lake Tools para Visual Studio se incluyen en hello __cargas de trabajo de Azure__ para Visual Studio de 2017.</span><span class="sxs-lookup"><span data-stu-id="5668a-128">Data Lake Tools for Visual Studio are included in hello __Azure Workload__ for Visual Studio 2017.</span></span>

2. <span data-ttu-id="5668a-129">Abra Visual Studio, seleccione **Archivo** > **Nuevo** > **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="5668a-129">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="5668a-130">Hola **nuevo proyecto** cuadro de diálogo, expanda **instalado** > **plantillas**y, a continuación, seleccione **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="5668a-130">In hello **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="5668a-131">En la lista Hola de plantillas, seleccione **aluvión de ejemplo**.</span><span class="sxs-lookup"><span data-stu-id="5668a-131">From hello list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="5668a-132">En parte inferior de Hola Hola del cuadro de diálogo, escriba un nombre para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="5668a-132">At hello bottom of hello dialog box, type a name for hello application.</span></span>

    ![imagen](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. <span data-ttu-id="5668a-134">En **el Explorador de soluciones**, haga clic en proyecto de Hola y seleccione **enviar tooStorm en HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="5668a-134">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5668a-135">Si se le solicite, escriba las credenciales de inicio de sesión de hello para la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="5668a-135">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="5668a-136">Si tiene más de una suscripción, inicie sesión en toohello uno que contiene el aluvión en clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5668a-136">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="5668a-137">Seleccione el aluvión en clúster de HDInsight de hello **clúster de Storm** lista desplegable y, a continuación, seleccione **enviar**.</span><span class="sxs-lookup"><span data-stu-id="5668a-137">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="5668a-138">Puede supervisar si el envío de hello es correcto mediante hello **salida** ventana.</span><span class="sxs-lookup"><span data-stu-id="5668a-138">You can monitor whether hello submission is successful by using hello **Output** window.</span></span>

## <a name="submit-a-topology-ssh-and-hello-storm-command"></a><span data-ttu-id="5668a-139">Enviar una topología: SSH y hello Storm comando</span><span class="sxs-lookup"><span data-stu-id="5668a-139">Submit a topology: SSH and hello Storm command</span></span>

1. <span data-ttu-id="5668a-140">Use el clúster de HDInsight de toohello tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="5668a-140">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="5668a-141">Reemplace **nombre de usuario** nombre hello del inicio de sesión SSH.</span><span class="sxs-lookup"><span data-stu-id="5668a-141">Replace **USERNAME** hello name of your SSH login.</span></span> <span data-ttu-id="5668a-142">Reemplace **CLUSTERNAME** por el nombre del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5668a-142">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="5668a-143">Para obtener más información sobre cómo utilizar SSH tooconnect tooyour HDInsight de clúster, consulte [utilizar SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5668a-143">For more information on using SSH tooconnect tooyour HDInsight cluster, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="5668a-144">Usar hello después comando toostart una topología de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5668a-144">Use hello following command toostart an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    <span data-ttu-id="5668a-145">Este comando inicia la topología de WordCount de ejemplo de Hola en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-145">This command starts hello example WordCount topology on hello cluster.</span></span> <span data-ttu-id="5668a-146">Esta topología generar de forma aleatoria las frases y repetición de Hola de recuento de cada palabra en las frases de Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-146">This topology randomly generate sentences and count hello occurrence of each word in hello sentences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5668a-147">Al enviar el clúster de topología toohello, primero debe copiar archivo jar de Hola que contiene el clúster de hello antes de usar hello `storm` comando.</span><span class="sxs-lookup"><span data-stu-id="5668a-147">When submitting topology toohello cluster, you must first copy hello jar file containing hello cluster before using hello `storm` command.</span></span> <span data-ttu-id="5668a-148">clúster de toohello de toocopy Hola archivos, puede usar hello `scp` comando.</span><span class="sxs-lookup"><span data-stu-id="5668a-148">toocopy hello file toohello cluster, you can use hello `scp` command.</span></span> <span data-ttu-id="5668a-149">Por ejemplo: `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="5668a-149">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
   >
   > <span data-ttu-id="5668a-150">ejemplo de WordCount Hello y otros ejemplos de inicio de storm, ya están incluidas en el clúster en `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="5668a-150">hello WordCount example, and other storm starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

## <a name="submit-a-topology-programmatically"></a><span data-ttu-id="5668a-151">Envío de una topología: de manera programática</span><span class="sxs-lookup"><span data-stu-id="5668a-151">Submit a topology: programmatically</span></span>

<span data-ttu-id="5668a-152">Mediante programación, puede implementar un tooStorm topología en HDInsight comunicándose con hello servicio Nimbus hospedado en el clúster.</span><span class="sxs-lookup"><span data-stu-id="5668a-152">You can programmatically deploy a topology tooStorm on HDInsight by communicating with hello Nimbus service hosted in your cluster.</span></span> <span data-ttu-id="5668a-153">[https://github.com/Azure-Samples/hdinsight-Java-Deploy-Storm-Topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) proporciona un ejemplo de aplicación Java que muestra cómo toodeploy e iniciar una topología a través del servicio Nimbus Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) provides an example Java application that demonstrates how toodeploy and start a topology through hello Nimbus service.</span></span>

## <a name="monitor-and-manage-visual-studio"></a><span data-ttu-id="5668a-154">Supervisión y administración: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5668a-154">Monitor and manage: Visual Studio</span></span>

<span data-ttu-id="5668a-155">Cuando una topología se ha enviado correctamente con Visual Studio, Hola **aluvión de topologías** de hello clúster aparece en la vista.</span><span class="sxs-lookup"><span data-stu-id="5668a-155">When a topology has been successfully submitted using Visual Studio, hello **Storm Topologies** view for hello cluster appears.</span></span> <span data-ttu-id="5668a-156">Seleccione topología Hola de hello mostrar tooview información acerca de hello ejecutando topología.</span><span class="sxs-lookup"><span data-stu-id="5668a-156">Select hello topology from hello list tooview information about hello running topology.</span></span>

![supervisión de visual studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> <span data-ttu-id="5668a-158">También puede ver las **topologías de Storm** en el **Explorador de servidores** expandiendo **Azure** > **HDInsight** y, después, haciendo clic con el botón derecho en un clúster de Storm en HDInsight y seleccionando **View Storm Topologies** (Ver topologías de Storm).</span><span class="sxs-lookup"><span data-stu-id="5668a-158">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

<span data-ttu-id="5668a-159">Seleccione la forma de Hola Hola spouts o tornillos tooview información acerca de estos componentes.</span><span class="sxs-lookup"><span data-stu-id="5668a-159">Select hello shape for hello spouts or bolts tooview information about these components.</span></span> <span data-ttu-id="5668a-160">Se abrirá una ventana nueva para cada elemento seleccionado.</span><span class="sxs-lookup"><span data-stu-id="5668a-160">A new window opens for each item selected.</span></span>

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="5668a-161">Desactivar y reactivar</span><span class="sxs-lookup"><span data-stu-id="5668a-161">Deactivate and reactivate</span></span>

<span data-ttu-id="5668a-162">Al desactivar una topología se pone en pausa hasta que se elimine o se reactive.</span><span class="sxs-lookup"><span data-stu-id="5668a-162">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="5668a-163">tooperform estas operaciones, usar hello __desactivar__ y __reactivar__ botones en la parte superior de Hola de hello __resumen de la topología__.</span><span class="sxs-lookup"><span data-stu-id="5668a-163">tooperform these operations, use hello __Deactivate__ and __Reactivate__ buttons at hello top of hello __Topology Summary__.</span></span>

### <a name="rebalance"></a><span data-ttu-id="5668a-164">Reequilibrar</span><span class="sxs-lookup"><span data-stu-id="5668a-164">Rebalance</span></span>

<span data-ttu-id="5668a-165">Reequilibrio una topología permite Hola sistema toorevise Hola el paralelismo de topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-165">Rebalancing a topology allows hello system toorevise hello parallelism of hello topology.</span></span> <span data-ttu-id="5668a-166">Por ejemplo, si se han cambiado el tamaño Hola clúster tooadd más notas, reequilibrio permite una topología de nuevos nodos de toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-166">For example, if you have resized hello cluster tooadd more notes, rebalancing allows a topology toosee hello new nodes.</span></span>

<span data-ttu-id="5668a-167">toorebalance una topología, usar hello __reequilibrar__ situado en la parte superior de Hola de hello __resumen de la topología__.</span><span class="sxs-lookup"><span data-stu-id="5668a-167">toorebalance a topology, use hello __Rebalance__ button at hello top of hello __Topology Summary__.</span></span>

> [!WARNING]
> <span data-ttu-id="5668a-168">Reequilibrio primero una topología desactiva la topología de hello, redistribuye los trabajadores uniformemente en el clúster de hello y, luego, por último devuelve estado toohello Hola topología en que estaba antes de producirse el equilibrio.</span><span class="sxs-lookup"><span data-stu-id="5668a-168">Rebalancing a topology first deactivates hello topology, then redistributes workers evenly across hello cluster, then finally returns hello topology toohello state it was in before rebalancing occurred.</span></span> <span data-ttu-id="5668a-169">Por lo que si la topología de hello estaba activo, vuelve activo.</span><span class="sxs-lookup"><span data-stu-id="5668a-169">So if hello topology was active, it becomes active again.</span></span> <span data-ttu-id="5668a-170">Si se desactivó, seguirá desactivada.</span><span class="sxs-lookup"><span data-stu-id="5668a-170">If it was deactivated, it remains deactivated.</span></span>

### <a name="kill-a-topology"></a><span data-ttu-id="5668a-171">Terminación de una topología</span><span class="sxs-lookup"><span data-stu-id="5668a-171">Kill a topology</span></span>

<span data-ttu-id="5668a-172">Topologías de Storm continúan ejecutándose hasta que se hayan detenido o se elimina el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-172">Storm topologies continue running until they are stopped or hello cluster is deleted.</span></span> <span data-ttu-id="5668a-173">toostop una topología, usar hello __Kill__ situado en la parte superior de Hola de hello __resumen de la topología__.</span><span class="sxs-lookup"><span data-stu-id="5668a-173">toostop a topology, use hello __Kill__ button at hello top of hello __Topology Summary__.</span></span>

## <a name="monitor-and-manage-ssh-and-hello-storm-command"></a><span data-ttu-id="5668a-174">Supervisar y administrar: SSH y hello Storm comando</span><span class="sxs-lookup"><span data-stu-id="5668a-174">Monitor and manage: SSH and hello Storm command</span></span>

<span data-ttu-id="5668a-175">Hola `storm` utilidad le permite toowork con topologías en ejecución desde la línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-175">hello `storm` utility allows you toowork with running topologies from hello command line.</span></span> <span data-ttu-id="5668a-176">Use `storm -h` para obtener una lista completa de comandos.</span><span class="sxs-lookup"><span data-stu-id="5668a-176">Use `storm -h` for a full list of commands.</span></span>

### <a name="list-topologies"></a><span data-ttu-id="5668a-177">Topologías de lista</span><span class="sxs-lookup"><span data-stu-id="5668a-177">List topologies</span></span>

<span data-ttu-id="5668a-178">Usar hello después a toolist comando todas las topologías de ejecución:</span><span class="sxs-lookup"><span data-stu-id="5668a-178">Use hello following command toolist all running topologies:</span></span>

    storm list

<span data-ttu-id="5668a-179">Este comando devuelve información toohello similar siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="5668a-179">This command returns information similar toohello following text:</span></span>

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="5668a-180">Desactivar y reactivar</span><span class="sxs-lookup"><span data-stu-id="5668a-180">Deactivate and reactivate</span></span>

<span data-ttu-id="5668a-181">Al desactivar una topología se pone en pausa hasta que se elimine o se reactive.</span><span class="sxs-lookup"><span data-stu-id="5668a-181">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="5668a-182">Usar hello después toodeactivate de comando y volver a activar:</span><span class="sxs-lookup"><span data-stu-id="5668a-182">Use hello following command toodeactivate and reactivate:</span></span>

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a><span data-ttu-id="5668a-183">Eliminar una topología de ejecución</span><span class="sxs-lookup"><span data-stu-id="5668a-183">Kill a running topology</span></span>

<span data-ttu-id="5668a-184">Las topologías de Storm, una vez iniciadas, se siguen ejecutando hasta que se detengan.</span><span class="sxs-lookup"><span data-stu-id="5668a-184">Storm topologies, once started, continue running until stopped.</span></span> <span data-ttu-id="5668a-185">toostop una topología, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="5668a-185">toostop a topology, use hello following command:</span></span>

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a><span data-ttu-id="5668a-186">Reequilibrar</span><span class="sxs-lookup"><span data-stu-id="5668a-186">Rebalance</span></span>

<span data-ttu-id="5668a-187">Reequilibrio una topología permite Hola sistema toorevise Hola el paralelismo de topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-187">Rebalancing a topology allows hello system toorevise hello parallelism of hello topology.</span></span> <span data-ttu-id="5668a-188">Por ejemplo, si se han cambiado el tamaño Hola clúster tooadd más notas, reequilibrio permite una topología de nuevos nodos de toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-188">For example, if you have resized hello cluster tooadd more notes, rebalancing allows a topology toosee hello new nodes.</span></span>

> [!WARNING]
> <span data-ttu-id="5668a-189">Reequilibrio primero una topología desactiva la topología de hello, redistribuye los trabajadores uniformemente en el clúster de hello y, luego, por último devuelve estado toohello Hola topología en que estaba antes de producirse el equilibrio.</span><span class="sxs-lookup"><span data-stu-id="5668a-189">Rebalancing a topology first deactivates hello topology, then redistributes workers evenly across hello cluster, then finally returns hello topology toohello state it was in before rebalancing occurred.</span></span> <span data-ttu-id="5668a-190">Por lo que si la topología de hello estaba activo, vuelve activo.</span><span class="sxs-lookup"><span data-stu-id="5668a-190">So if hello topology was active, it becomes active again.</span></span> <span data-ttu-id="5668a-191">Si se desactivó, seguirá desactivada.</span><span class="sxs-lookup"><span data-stu-id="5668a-191">If it was deactivated, it remains deactivated.</span></span>

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a><span data-ttu-id="5668a-192">Supervisión y administración: IU de Storm</span><span class="sxs-lookup"><span data-stu-id="5668a-192">Monitor and manage: Storm UI</span></span>

<span data-ttu-id="5668a-193">Hola aluvión de interfaz de usuario proporciona una interfaz web para trabajar con topologías en ejecución y se incluye en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5668a-193">hello Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span> <span data-ttu-id="5668a-194">Hola tooview aluvión de interfaz de usuario, utilice un tooopen de explorador web **https://CLUSTERNAME.azurehdinsight.net/stormui**, donde **CLUSTERNAME** es Hola nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="5668a-194">tooview hello Storm UI, use a web browser tooopen **https://CLUSTERNAME.azurehdinsight.net/stormui**, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="5668a-195">Si se le solicita tooprovide un nombre de usuario y una contraseña, escriba Administrador de clústeres de hello (admin) y la contraseña que ha utilizado al crear clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-195">If asked tooprovide a user name and password, enter hello cluster administrator (admin) and password that you used when creating hello cluster.</span></span>

### <a name="main-page"></a><span data-ttu-id="5668a-196">Página principal</span><span class="sxs-lookup"><span data-stu-id="5668a-196">Main page</span></span>

<span data-ttu-id="5668a-197">página principal de Hola de hello aluvión de interfaz de usuario proporciona Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="5668a-197">hello main page of hello Storm UI provides hello following information:</span></span>

* <span data-ttu-id="5668a-198">**Resumen de clúster**: información básica sobre el clúster de Storm Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-198">**Cluster summary**: Basic information about hello Storm cluster.</span></span>
* <span data-ttu-id="5668a-199">**Resumen de las topologías**: una lista de las topologías en ejecución.</span><span class="sxs-lookup"><span data-stu-id="5668a-199">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="5668a-200">Usar vínculos de hello en esta sección tooview obtener más información acerca de las topologías específicas.</span><span class="sxs-lookup"><span data-stu-id="5668a-200">Use hello links in this section tooview more information about specific topologies.</span></span>
* <span data-ttu-id="5668a-201">**Resumen de supervisor**: obtener información sobre el supervisor de Storm Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-201">**Supervisor summary**: Information about hello Storm supervisor.</span></span>
* <span data-ttu-id="5668a-202">**Configuración de Nimbus**: configuración de Nimbus para clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-202">**Nimbus configuration**: Nimbus configuration for hello cluster.</span></span>

### <a name="topology-summary"></a><span data-ttu-id="5668a-203">Resumen de las topologías</span><span class="sxs-lookup"><span data-stu-id="5668a-203">Topology summary</span></span>

<span data-ttu-id="5668a-204">Si selecciona un vínculo de hello **resumen de la topología** sección muestra hello después de obtener información acerca de la topología de hello:</span><span class="sxs-lookup"><span data-stu-id="5668a-204">Selecting a link from hello **Topology summary** section displays hello following information about hello topology:</span></span>

* <span data-ttu-id="5668a-205">**Resumen de la topología**: información básica acerca de la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-205">**Topology summary**: Basic information about hello topology.</span></span>
* <span data-ttu-id="5668a-206">**Acciones de topología**: acciones de administración que puede realizar para la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-206">**Topology actions**: Management actions that you can perform for hello topology.</span></span>

  * <span data-ttu-id="5668a-207">**Activar**: reanuda el procesamiento de una topología desactivada.</span><span class="sxs-lookup"><span data-stu-id="5668a-207">**Activate**: Resumes processing of a deactivated topology.</span></span>
  * <span data-ttu-id="5668a-208">**Desactivar**: pausa una topología en ejecución.</span><span class="sxs-lookup"><span data-stu-id="5668a-208">**Deactivate**: Pauses a running topology.</span></span>
  * <span data-ttu-id="5668a-209">**Reequilibrar**: ajusta el paralelismo de Hola de topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-209">**Rebalance**: Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="5668a-210">Debe volver a equilibrar las topologías de ejecución después de que haya cambiado Hola número de nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-210">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="5668a-211">Esta operación permite Hola topología tooadjust paralelismo toocompensate para hello aumenta o reduce el número de nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-211">This operation allows hello topology tooadjust parallelism toocompensate for hello increased or decreased number of nodes in hello cluster.</span></span>

    <span data-ttu-id="5668a-212">Para obtener más información, consulte <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">descripción paralelismo Hola de una topología de Storm</a>.</span><span class="sxs-lookup"><span data-stu-id="5668a-212">For more information, see <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Understanding hello parallelism of a Storm topology</a>.</span></span>
  * <span data-ttu-id="5668a-213">**Kill**: termine una topología de Storm después Hola especifica el tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="5668a-213">**Kill**: Terminates a Storm topology after hello specified timeout.</span></span>
* <span data-ttu-id="5668a-214">**Estadísticas de topología**: estadísticas acerca de la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-214">**Topology stats**: Statistics about hello topology.</span></span> <span data-ttu-id="5668a-215">tooset Hola franja temporal para hello restantes entradas en la página de hello, usar los vínculos de Hola de hello **ventana** columna.</span><span class="sxs-lookup"><span data-stu-id="5668a-215">tooset hello timeframe for hello remaining entries on hello page, use hello links in hello **Window** column.</span></span>
* <span data-ttu-id="5668a-216">**Spouts**: Hola spouts utilizados por la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-216">**Spouts**: hello spouts used by hello topology.</span></span> <span data-ttu-id="5668a-217">Usar vínculos de hello en esta sección tooview obtener más información sobre spouts específicos.</span><span class="sxs-lookup"><span data-stu-id="5668a-217">Use hello links in this section tooview more information about specific spouts.</span></span>
* <span data-ttu-id="5668a-218">**Tornillos**: Hola tornillos utilizados por la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-218">**Bolts**: hello bolts used by hello topology.</span></span> <span data-ttu-id="5668a-219">Usar vínculos de hello en esta sección tooview obtener más información acerca de los tornillos específicos.</span><span class="sxs-lookup"><span data-stu-id="5668a-219">Use hello links in this section tooview more information about specific bolts.</span></span>
* <span data-ttu-id="5668a-220">**Configuración de la topología**: configuración de Hola de topología de hello seleccionado.</span><span class="sxs-lookup"><span data-stu-id="5668a-220">**Topology configuration**: hello configuration of hello selected topology.</span></span>

### <a name="spout-and-bolt-summary"></a><span data-ttu-id="5668a-221">Resumen de spouts y bolts</span><span class="sxs-lookup"><span data-stu-id="5668a-221">Spout and Bolt summary</span></span>

<span data-ttu-id="5668a-222">Seleccionar un pitorro de hello **Spouts** o **tornillos** secciones muestra hello después de obtener información sobre el elemento Hola seleccionado:</span><span class="sxs-lookup"><span data-stu-id="5668a-222">Selecting a spout from hello **Spouts** or **Bolts** sections displays hello following information about hello selected item:</span></span>

* <span data-ttu-id="5668a-223">**Resumen de componentes**: información básica sobre pitorro Hola o rayo.</span><span class="sxs-lookup"><span data-stu-id="5668a-223">**Component summary**: Basic information about hello spout or bolt.</span></span>
* <span data-ttu-id="5668a-224">**Estadísticas de pitorro/rayo**: estadísticas sobre Hola apetezca charlar o el tornillo.</span><span class="sxs-lookup"><span data-stu-id="5668a-224">**Spout/Bolt stats**: Statistics about hello spout or bolt.</span></span> <span data-ttu-id="5668a-225">tooset Hola franja temporal para hello restantes entradas en la página de hello, usar los vínculos de Hola de hello **ventana** columna.</span><span class="sxs-lookup"><span data-stu-id="5668a-225">tooset hello timeframe for hello remaining entries on hello page, use hello links in hello **Window** column.</span></span>
* <span data-ttu-id="5668a-226">**Estadísticas de entrada** (solo tornillo): utilizados por el rayo Hola de flujos de entrada de información acerca de Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-226">**Input stats** (bolt only): Information about hello input streams consumed by hello bolt.</span></span>
* <span data-ttu-id="5668a-227">**Estadísticas de salida**: información sobre los flujos de hello emitidos por esta apetezca charlar o el tornillo.</span><span class="sxs-lookup"><span data-stu-id="5668a-227">**Output stats**: Information about hello streams emitted by this spout or bolt.</span></span>
* <span data-ttu-id="5668a-228">**Ejecutor**: información sobre instancias de Hola de pitorro Hola o rayo.</span><span class="sxs-lookup"><span data-stu-id="5668a-228">**Executors**: Information about hello instances of hello spout or bolt.</span></span> <span data-ttu-id="5668a-229">Seleccione hello **puerto** entrada para un tooview ejecutor específico un registro de información de diagnóstico generados para esta instancia.</span><span class="sxs-lookup"><span data-stu-id="5668a-229">Select hello **Port** entry for a specific executor tooview a log of diagnostic information produced for this instance.</span></span>
* <span data-ttu-id="5668a-230">**Errores**: cualquier información de error de este spout o bolt.</span><span class="sxs-lookup"><span data-stu-id="5668a-230">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="monitor-and-manage-rest-api"></a><span data-ttu-id="5668a-231">Supervisión y administración: API de REST</span><span class="sxs-lookup"><span data-stu-id="5668a-231">Monitor and manage: REST API</span></span>

<span data-ttu-id="5668a-232">Hola aluvión de interfaz de usuario se basa en hello API de REST, para que pueda realizar la administración y funcionalidad de supervisión mediante el uso de API de REST de hello similares.</span><span class="sxs-lookup"><span data-stu-id="5668a-232">hello Storm UI is built on top of hello REST API, so you can perform similar management and monitoring functionality by using hello REST API.</span></span> <span data-ttu-id="5668a-233">Puede usar herramientas personalizadas de toocreate de API de REST de Hola para administrar y supervisar las topologías de Storm.</span><span class="sxs-lookup"><span data-stu-id="5668a-233">You can use hello REST API toocreate custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="5668a-234">Para más información, vea la [API de REST de la IU de Storm](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span><span class="sxs-lookup"><span data-stu-id="5668a-234">For more information, see [Storm UI REST API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span></span> <span data-ttu-id="5668a-235">Hello siguiente información es específica toousing hello API de REST con Apache Storm en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5668a-235">hello following information is specific toousing hello REST API with Apache Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5668a-236">Hola aluvión de API de REST no esté disponible públicamente en internet de Hola y debe tener acceso utilizando un SSH túnel toohello HDInsight nodo principal del clúster.</span><span class="sxs-lookup"><span data-stu-id="5668a-236">hello Storm REST API is not publicly available over hello internet, and must be accessed using an SSH tunnel toohello HDInsight cluster head node.</span></span> <span data-ttu-id="5668a-237">Para obtener información sobre cómo crear y usar un túnel SSH, consulte [tooaccess uso de SSH túnel Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie y otras interfaces de usuario web](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="5668a-237">For information on creating and using an SSH tunnel, see [Use SSH Tunneling tooaccess Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

### <a name="base-uri"></a><span data-ttu-id="5668a-238">URI base</span><span class="sxs-lookup"><span data-stu-id="5668a-238">Base URI</span></span>

<span data-ttu-id="5668a-239">Hello URI base para la API de REST de hello en clústeres de HDInsight basados en Linux está disponible en el nodo principal de hello en **https://HEADNODEFQDN:8744/api/v1/**.</span><span class="sxs-lookup"><span data-stu-id="5668a-239">hello base URI for hello REST API on Linux-based HDInsight clusters is available on hello head node at **https://HEADNODEFQDN:8744/api/v1/**.</span></span> <span data-ttu-id="5668a-240">nombre de dominio de Hello del nodo principal de Hola se genera durante la creación del clúster y no es estático.</span><span class="sxs-lookup"><span data-stu-id="5668a-240">hello domain name of hello head node is generated during cluster creation and is not static.</span></span>

<span data-ttu-id="5668a-241">Puede encontrar el nombre de dominio completo (FQDN) de hello para el nodo principal del clúster Hola de varias maneras diferentes:</span><span class="sxs-lookup"><span data-stu-id="5668a-241">You can find hello fully qualified domain name (FQDN) for hello cluster head node in several different ways:</span></span>

* <span data-ttu-id="5668a-242">**Desde una sesión de SSH**: Use el comando de hello `headnode -f` desde un clúster de toohello de sesión SSH.</span><span class="sxs-lookup"><span data-stu-id="5668a-242">**From an SSH session**: Use hello command `headnode -f` from an SSH session toohello cluster.</span></span>
* <span data-ttu-id="5668a-243">**Desde Ambari Web**: seleccione **servicios** desde la parte superior de la página de Hola Hola, a continuación, seleccione **Storm**.</span><span class="sxs-lookup"><span data-stu-id="5668a-243">**From Ambari Web**: Select **Services** from hello top of hello page, then select **Storm**.</span></span> <span data-ttu-id="5668a-244">De hello **resumen** ficha, seleccione **aluvión de interfaz de usuario de servidor**.</span><span class="sxs-lookup"><span data-stu-id="5668a-244">From hello **Summary** tab, select **Storm UI Server**.</span></span> <span data-ttu-id="5668a-245">Hola FQDN del nodo de Hola que está ejecutando Hola aluvión de interfaz de usuario y la API de REST está al principio de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-245">hello FQDN of hello node that hello Storm UI and REST API is running is at hello top of hello page.</span></span>
* <span data-ttu-id="5668a-246">**A través de API de REST de Ambari**: Use el comando de hello `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` tooretrieve información sobre el nodo Hola Hola aluvión de interfaz de usuario y la API de REST se ejecutan en.</span><span class="sxs-lookup"><span data-stu-id="5668a-246">**From Ambari REST API**: Use hello command `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` tooretrieve information about hello node that hello Storm UI and REST API are running on.</span></span> <span data-ttu-id="5668a-247">Reemplace **contraseña** con la contraseña de administrador de hello para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-247">Replace **PASSWORD** with hello admin password for hello cluster.</span></span> <span data-ttu-id="5668a-248">Reemplace **CLUSTERNAME** con el nombre del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-248">Replace **CLUSTERNAME** with hello cluster name.</span></span> <span data-ttu-id="5668a-249">En la respuesta de hello, entrada de "host_name" hello contiene Hola FQDN del nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-249">In hello response, hello "host_name" entry contains hello FQDN of hello node.</span></span>

### <a name="authentication"></a><span data-ttu-id="5668a-250">Autenticación</span><span class="sxs-lookup"><span data-stu-id="5668a-250">Authentication</span></span>

<span data-ttu-id="5668a-251">Toohello de las solicitudes que se debe usar la API de REST **la autenticación básica**, por lo que usar el nombre del Administrador de clúster de HDInsight de hello y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="5668a-251">Requests toohello REST API must use **basic authentication**, so you use hello HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="5668a-252">Dado que la autenticación básica se envía mediante el uso de texto no cifrado, debe **siempre** utilizar comunicaciones HTTPS a toosecure con clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-252">Because basic authentication is sent by using clear text, you should **always** use HTTPS toosecure communications with hello cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="5668a-253">Valores devueltos</span><span class="sxs-lookup"><span data-stu-id="5668a-253">Return values</span></span>

<span data-ttu-id="5668a-254">Información que se devuelve de hello API de REST solo pueden ser utilizable desde dentro de clúster de Hola o máquinas virtuales en Hola misma red Virtual de Azure como clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-254">Information that is returned from hello REST API may only be usable from within hello cluster or virtual machines on hello same Azure Virtual Network as hello cluster.</span></span> <span data-ttu-id="5668a-255">Por ejemplo, devuelve para servidores de Zookeeper de nombre de dominio completo hello (FQDN) no es ser accesible desde Internet Hola.</span><span class="sxs-lookup"><span data-stu-id="5668a-255">For example, hello fully qualified domain name (FQDN) returned for Zookeeper servers is not be accessible from hello Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5668a-256">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5668a-256">Next Steps</span></span>

<span data-ttu-id="5668a-257">Ahora que ha aprendido cómo topologías toodeploy y monitor mediante el uso de Hola aluvión de panel, obtenga información acerca de cómo demasiado[topologías de basados en Java desarrollar con Maven](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="5668a-257">Now that you've learned how toodeploy and monitor topologies by using hello Storm Dashboard, learn how too[Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="5668a-258">Para obtener una lista con más topologías de ejemplo, consulte [Topologías de ejemplo para Storm en HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="5668a-258">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
