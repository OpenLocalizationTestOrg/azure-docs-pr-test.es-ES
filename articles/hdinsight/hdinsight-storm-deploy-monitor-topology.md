---
title: "Implementación y administración de topologías de Apache Storm en HDInsight | Microsoft Docs"
description: "Aprenda a implementar, supervisar y administrar topologías de Apache Storm mediante el panel de Storm en HDInsight. Utilice herramientas de Hadoop para Visual Studio"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5e542072-f014-42aa-82d6-2694a76df520
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 34072574f83b51280e60e2f8766c6c5d5a33c307
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a><span data-ttu-id="551c1-104">Implementación y administración de topologías de Apache Storm en HDInsight basado en Windows</span><span class="sxs-lookup"><span data-stu-id="551c1-104">Deploy and manage Apache Storm topologies on Windows-based HDInsight</span></span>

<span data-ttu-id="551c1-105">El panel de Storm permite implementar y ejecutar fácilmente topologías de Apache Storm en el clúster de HDInsight mediante el explorador web.</span><span class="sxs-lookup"><span data-stu-id="551c1-105">The Storm Dashboard allows you to easily deploy and run Apache Storm topologies to your HDInsight cluster by using your web browser.</span></span> <span data-ttu-id="551c1-106">También puede utilizar el panel para supervisar y administrar topologías de ejecución.</span><span class="sxs-lookup"><span data-stu-id="551c1-106">You can also use the dashboard to monitor and manage running topologies.</span></span> <span data-ttu-id="551c1-107">Si utiliza Visual Studio, las herramientas de HDInsight para Visual Studio proporcionan características similares en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="551c1-107">If you use Visual Studio, the HDInsight Tools for Visual Studio provide similar features in Visual Studio.</span></span>

<span data-ttu-id="551c1-108">El panel de Storm y las características de Storm de las herramientas de HDInsight dependen de la API de REST de Storm, que se puede usar para crear sus propias soluciones de supervisión y administración.</span><span class="sxs-lookup"><span data-stu-id="551c1-108">The Storm Dashboard and the Storm features in the HDInsight Tools rely on the Storm REST API, which can be used to create your own monitoring and management solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="551c1-109">Para los pasos de este documento se necesita un clúster de Storm en HDInsight que usa Windows como sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="551c1-109">The steps in this document require a Storm on HDInsight cluster that uses Windows as the operating system.</span></span> <span data-ttu-id="551c1-110">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="551c1-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="551c1-111">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="551c1-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="551c1-112">Para más información sobre la implementación y la administración de topologías de Storm con un clúster de HDInsight que usa Linux, consulte [Implementación y administración de topologías de Apache Storm en HDInsight basado en Linux](hdinsight-storm-deploy-monitor-topology-linux.md).</span><span class="sxs-lookup"><span data-stu-id="551c1-112">For information on deploying and managing Storm topologies with an HDInsight cluster that uses Linux, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="551c1-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="551c1-113">Prerequisites</span></span>

* <span data-ttu-id="551c1-114">**Apache Storm en HDInsight**: consulte [Introducción a Apache Storm en HDInsight](hdinsight-apache-storm-tutorial-get-started.md) para conocer los pasos para la creación de un clúster.</span><span class="sxs-lookup"><span data-stu-id="551c1-114">**Apache Storm on HDInsight** - see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started.md) for steps on creating a cluster.</span></span>

* <span data-ttu-id="551c1-115">Para el **panel de Storm**: un explorador web moderno que admite HTML5.</span><span class="sxs-lookup"><span data-stu-id="551c1-115">For the **Storm Dashboard**: A modern web browser that supports HTML5.</span></span>

* <span data-ttu-id="551c1-116">Para **Visual Studio** : Azure SDK 2.5.1 o versiones más recientes y las herramientas de HDInsight para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="551c1-116">For **Visual Studio** - Azure SDK 2.5.1 or newer and the HDInsight Tools for Visual Studio.</span></span> <span data-ttu-id="551c1-117">Consulte [Introducción a las herramientas de HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) para Visual Studio para instalar y configurar las herramientas de HDInsight para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="551c1-117">See [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) to install and configure the HDInsight tools for Visual Studio.</span></span>

    <span data-ttu-id="551c1-118">Una de las siguientes versiones de Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="551c1-118">One of the following versions of Visual Studio:</span></span>

  * <span data-ttu-id="551c1-119">Visual Studio 2012 con la actualización 4</span><span class="sxs-lookup"><span data-stu-id="551c1-119">Visual Studio 2012 with Update 4</span></span>

  * <span data-ttu-id="551c1-120">Visual Studio 2013 con la actualización 4 o Visual Studio Community 2013</span><span class="sxs-lookup"><span data-stu-id="551c1-120">Visual Studio 2013 with Update 4 or Visual Studio 2013 Community</span></span>

  * <span data-ttu-id="551c1-121">Visual Studio 2015 (cualquier edición)</span><span class="sxs-lookup"><span data-stu-id="551c1-121">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="551c1-122">Visual Studio 2017 (cualquier edición)</span><span class="sxs-lookup"><span data-stu-id="551c1-122">Visual Studio 2017 (any edition)</span></span>

## <a name="storm-dashboard"></a><span data-ttu-id="551c1-123">panel de Storm</span><span class="sxs-lookup"><span data-stu-id="551c1-123">Storm Dashboard</span></span>

<span data-ttu-id="551c1-124">El panel de Storm es una página web disponible en el clúster de Storm.</span><span class="sxs-lookup"><span data-stu-id="551c1-124">The Storm Dashboard is a web page available on your Storm cluster.</span></span> <span data-ttu-id="551c1-125">La dirección URL es **https://&lt;clustername>.azurehdinsight.net/**, donde **clustername** es el nombre del clúster de Storm en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="551c1-125">The URL is **https://&lt;clustername>.azurehdinsight.net/**, where **clustername** is the name of your Storm on HDInsight cluster.</span></span>

<span data-ttu-id="551c1-126">En la parte superior del panel de Storm, seleccione **Enviar topología**.</span><span class="sxs-lookup"><span data-stu-id="551c1-126">From the top of the Storm Dashboard, select **Submit Topology**.</span></span> <span data-ttu-id="551c1-127">Siga las instrucciones de la página para ejecutar una topología de muestra o cargar y ejecutar una topología que haya creado.</span><span class="sxs-lookup"><span data-stu-id="551c1-127">Follow the instructions on the page to run a sample topology or to upload and run a topology that you created.</span></span>

![la página de envío de topología][storm-dashboard-submit]

### <a name="storm-ui"></a><span data-ttu-id="551c1-129">UI de Storm</span><span class="sxs-lookup"><span data-stu-id="551c1-129">Storm UI</span></span>

<span data-ttu-id="551c1-130">En el panel de Storm, seleccione el vínculo **IU de Storm** .</span><span class="sxs-lookup"><span data-stu-id="551c1-130">From the Storm Dashboard, select the **Storm UI** link.</span></span> <span data-ttu-id="551c1-131">Se muestra información sobre el clúster, así como las topologías que estén en ejecución.</span><span class="sxs-lookup"><span data-stu-id="551c1-131">This displays information about the cluster, in addition to any running topologies.</span></span>

![la interfaz de usuario de storm][storm-dashboard-ui]

> [!NOTE]
> <span data-ttu-id="551c1-133">Con algunas versiones de Internet Explorer, es posible que descubra que la interfaz de usuario de Strom no se actualiza después de visitarla por primera vez.</span><span class="sxs-lookup"><span data-stu-id="551c1-133">With some versions of Internet Explorer, you may discover that the Storm UI does not refresh after you have first visited it.</span></span> <span data-ttu-id="551c1-134">Por ejemplo, puede que no se muestren las topologías nuevas que haya enviado o puede que se muestre una topología como activa, aunque anteriormente la desactivase.</span><span class="sxs-lookup"><span data-stu-id="551c1-134">For example, it may not show the new topologies you submitted, or it may show a topology as active when you previously deactivated it.</span></span> <span data-ttu-id="551c1-135">Microsoft conoce este problema y está trabajando para conseguir una solución.</span><span class="sxs-lookup"><span data-stu-id="551c1-135">Microsoft is aware of this issue and is working on a solution.</span></span>

#### <a name="main-page"></a><span data-ttu-id="551c1-136">Página principal</span><span class="sxs-lookup"><span data-stu-id="551c1-136">Main page</span></span>

<span data-ttu-id="551c1-137">La página principal de la interfaz de usuario de Storm ofrece la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="551c1-137">The main page of the Storm UI provides the following information:</span></span>

* <span data-ttu-id="551c1-138">**Resumen del clúster**: información básica sobre el clúster de Storm.</span><span class="sxs-lookup"><span data-stu-id="551c1-138">**Cluster summary**: Basic information about the Storm cluster.</span></span>

* <span data-ttu-id="551c1-139">**Resumen de las topologías**: una lista de las topologías en ejecución.</span><span class="sxs-lookup"><span data-stu-id="551c1-139">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="551c1-140">Use los vínculos de esta sección para obtener más información sobre las topologías específicas.</span><span class="sxs-lookup"><span data-stu-id="551c1-140">Use the links in this section to view more information about specific topologies.</span></span>

* <span data-ttu-id="551c1-141">**Resumen de supervisor**: información acerca del supervisor de Storm.</span><span class="sxs-lookup"><span data-stu-id="551c1-141">**Supervisor summary**: Information about the Storm supervisor.</span></span>

* <span data-ttu-id="551c1-142">**Configuración de Nimbus**: configuración de Nimbus del clúster.</span><span class="sxs-lookup"><span data-stu-id="551c1-142">**Nimbus configuration**: Nimbus configuration for the cluster.</span></span>

#### <a name="topology-summary"></a><span data-ttu-id="551c1-143">Resumen de las topologías</span><span class="sxs-lookup"><span data-stu-id="551c1-143">Topology summary</span></span>

<span data-ttu-id="551c1-144">Si selecciona un vínculo desde la sección **Resumen de la topología** , se mostrará la siguiente información sobre la topología.</span><span class="sxs-lookup"><span data-stu-id="551c1-144">Selecting a link from the **Topology summary** section displays the following information about the topology:</span></span>

* <span data-ttu-id="551c1-145">**Resumen de la topología**: información básica sobre la topología.</span><span class="sxs-lookup"><span data-stu-id="551c1-145">**Topology summary**: Basic information about the topology.</span></span>

* <span data-ttu-id="551c1-146">**Acciones de topología**: acciones de administración que puede realizar para la topología.</span><span class="sxs-lookup"><span data-stu-id="551c1-146">**Topology actions**: Management actions that you can perform for the topology.</span></span>

  * <span data-ttu-id="551c1-147">**Activar**: reanuda el procesamiento de una topología desactivada.</span><span class="sxs-lookup"><span data-stu-id="551c1-147">**Activate**: Resumes processing of a deactivated topology.</span></span>

  * <span data-ttu-id="551c1-148">**Desactivar**: pausa una topología en ejecución.</span><span class="sxs-lookup"><span data-stu-id="551c1-148">**Deactivate**: Pauses a running topology.</span></span>

  * <span data-ttu-id="551c1-149">**Reequilibrar**: ajusta el paralelismo de la topología.</span><span class="sxs-lookup"><span data-stu-id="551c1-149">**Rebalance**: Adjusts the parallelism of the topology.</span></span> <span data-ttu-id="551c1-150">Debe volver a equilibrar las topologías en ejecución después de haber cambiado el número de nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="551c1-150">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span></span> <span data-ttu-id="551c1-151">Esto permite que la topología ajuste el paralelismo para compensar el mayor o menor número de nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="551c1-151">This allows the topology to adjust parallelism to compensate for the increased or decreased number of nodes in the cluster.</span></span>

      <span data-ttu-id="551c1-152">Para obtener más información, consulte [Understanding the parallelism of a Storm topology (Descripción del paralelismo de una topología de Storm) (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="551c1-152">For more information, see [Understanding the parallelism of a Storm topology (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

  * <span data-ttu-id="551c1-153">**Eliminar**: finaliza una topología de Storm tras el tiempo de espera especificado.</span><span class="sxs-lookup"><span data-stu-id="551c1-153">**Kill**: Terminates a Storm topology after the specified timeout.</span></span>

* <span data-ttu-id="551c1-154">**Estadísticas de topología**: estadísticas sobre la topología.</span><span class="sxs-lookup"><span data-stu-id="551c1-154">**Topology stats**: Statistics about the topology.</span></span> <span data-ttu-id="551c1-155">Use los vínculos de la columna **Ventana** para establecer el plazo de tiempo para las entradas restantes en la página.</span><span class="sxs-lookup"><span data-stu-id="551c1-155">Use the links in the **Window** column to set the timeframe for the remaining entries on the page.</span></span>

* <span data-ttu-id="551c1-156">**Spouts**: los spouts que usa la topología.</span><span class="sxs-lookup"><span data-stu-id="551c1-156">**Spouts**: The spouts used by the topology.</span></span> <span data-ttu-id="551c1-157">Use los vínculos de esta sección para obtener más información acerca de spouts específicos.</span><span class="sxs-lookup"><span data-stu-id="551c1-157">Use the links in this section to view more information about specific spouts.</span></span>

* <span data-ttu-id="551c1-158">**Bolts**: los bolts que usa la topología.</span><span class="sxs-lookup"><span data-stu-id="551c1-158">**Bolts**: The bolts used by the topology.</span></span> <span data-ttu-id="551c1-159">Use los vínculos de esta sección para obtener más información acerca de bolts específicos.</span><span class="sxs-lookup"><span data-stu-id="551c1-159">Use the links in this section to view more information about specific bolts.</span></span>

* <span data-ttu-id="551c1-160">**Configuración de la topología**: la configuración de la topología seleccionada.</span><span class="sxs-lookup"><span data-stu-id="551c1-160">**Topology configuration**: The configuration of the selected topology.</span></span>

#### <a name="spout-and-bolt-summary"></a><span data-ttu-id="551c1-161">Resumen de spouts y bolts</span><span class="sxs-lookup"><span data-stu-id="551c1-161">Spout and Bolt summary</span></span>

<span data-ttu-id="551c1-162">Si se selecciona un spout en la sección **Spouts** o **Bolts**, se muestra la siguiente información sobre el elemento seleccionado:</span><span class="sxs-lookup"><span data-stu-id="551c1-162">Selecting a spout from the **Spouts** or **Bolts** sections displays the following information about the selected item:</span></span>

* <span data-ttu-id="551c1-163">**Resumen de componentes**: información básica acerca del spout o bolt.</span><span class="sxs-lookup"><span data-stu-id="551c1-163">**Component summary**: Basic information about the spout or bolt.</span></span>

* <span data-ttu-id="551c1-164">**Estadísticas de spouts/bolts**: estadísticas sobre el spout o bolt.</span><span class="sxs-lookup"><span data-stu-id="551c1-164">**Spout/Bolt stats**: Statistics about the spout or bolt.</span></span> <span data-ttu-id="551c1-165">Use los vínculos de la columna **Ventana** para establecer el plazo de tiempo para las entradas restantes en la página.</span><span class="sxs-lookup"><span data-stu-id="551c1-165">Use the links in the **Window** column to set the timeframe for the remaining entries on the page.</span></span>

* <span data-ttu-id="551c1-166">**Estadísticas de entrada** (solo bolt): información sobre las secuencias de entrada consumidas por el bolt.</span><span class="sxs-lookup"><span data-stu-id="551c1-166">**Input stats** (bolt only): Information about the input streams consumed by the bolt.</span></span>

* <span data-ttu-id="551c1-167">**Estadísticas de salida**: información sobre las secuencias emitidas por este spout o bolt</span><span class="sxs-lookup"><span data-stu-id="551c1-167">**Output stats**: Information about the streams emitted by this spout or bolt.</span></span>

* <span data-ttu-id="551c1-168">**Ejecutores**: información sobre las instancias del spout o bolt.</span><span class="sxs-lookup"><span data-stu-id="551c1-168">**Executors**: Information about the instances of the spout or bolt.</span></span> <span data-ttu-id="551c1-169">Seleccione la entrada **Puerto** de un ejecutor específico para ver un registro de información de diagnóstico generado por esta instancia.</span><span class="sxs-lookup"><span data-stu-id="551c1-169">Select the **Port** entry for a specific executor to view a log of diagnostic information produced for this instance.</span></span>

* <span data-ttu-id="551c1-170">**Errores**: cualquier información de error de este spout o bolt.</span><span class="sxs-lookup"><span data-stu-id="551c1-170">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="hdinsight-tools-for-visual-studio"></a><span data-ttu-id="551c1-171">Herramientas de HDInsight para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="551c1-171">HDInsight Tools for Visual Studio</span></span>

<span data-ttu-id="551c1-172">Las herramientas de HDInsight puede utilizarse para enviar las topologías de C# o híbridas al clúster de Storm.</span><span class="sxs-lookup"><span data-stu-id="551c1-172">The HDInsight Tools can be used to submit C# or hybrid topologies to your Storm cluster.</span></span> <span data-ttu-id="551c1-173">Los pasos siguientes usan una aplicación de muestra.</span><span class="sxs-lookup"><span data-stu-id="551c1-173">The following steps use a sample application.</span></span> <span data-ttu-id="551c1-174">Para obtener información sobre cómo crear sus propias topologías con las herramientas de HDInsight, consulte [Desarrollo de las topologías de C# mediante las herramientas de HDInsight para Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="551c1-174">For information about creating your own topologies by using the HDInsight Tools, see [Develop C# topologies using the HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="551c1-175">Utilice los siguientes pasos para implementar una muestra en el clúster de Storm en HDInsight y, a continuación, ver y administrar la topología.</span><span class="sxs-lookup"><span data-stu-id="551c1-175">Use the following steps to deploy a sample to your Storm on HDInsight cluster, then view and manage the topology.</span></span>

1. <span data-ttu-id="551c1-176">Si todavía no tiene instalada la versión más reciente de las herramientas de HDInsight para Visual Studio, consulte [Introducción al uso de las herramientas de HDInsight para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="551c1-176">If you have not already installed the latest version of the HDInsight Tools for Visual Studio, see [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="551c1-177">Abra Visual Studio, seleccione **Archivo** > **Nuevo** > **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="551c1-177">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="551c1-178">En el cuadro de diálogo **Nuevo proyecto**, expanda **Instalado** > **Plantillas** y seleccione **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="551c1-178">In the **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="551c1-179">En la lista de plantillas, seleccione **Muestra de Storm**.</span><span class="sxs-lookup"><span data-stu-id="551c1-179">From the list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="551c1-180">En la parte inferior del cuadro de diálogo, escriba un nombre para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="551c1-180">At the bottom of the dialog box, type a name for the application.</span></span>

    ![imagen](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. <span data-ttu-id="551c1-182">En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto y seleccione **Submit to Storm on HDInsight** (Enviar a Storm en HDInsight).</span><span class="sxs-lookup"><span data-stu-id="551c1-182">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="551c1-183">Si se le solicita, introduzca las credenciales de inicio de sesión de su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="551c1-183">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="551c1-184">Si tiene más de una suscripción, inicie sesión en la que contenga el clúster de Storm en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="551c1-184">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="551c1-185">Seleccione el clúster de Storm en HDInsight desde el menú desplegable **Storm Cluster** (Clúster de Storm y seleccione **Submit** (Enviar).</span><span class="sxs-lookup"><span data-stu-id="551c1-185">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="551c1-186">Puede supervisar si el envío es correcto mediante la ventana **Salida** .</span><span class="sxs-lookup"><span data-stu-id="551c1-186">You can monitor whether the submission is successful by using the **Output** window.</span></span>

6. <span data-ttu-id="551c1-187">Cuando la topología se envíe correctamente, deben aparecer las **topologías de Storm** del clúster.</span><span class="sxs-lookup"><span data-stu-id="551c1-187">When the topology has been successfully submitted, the **Storm Topologies** for the cluster should appear.</span></span> <span data-ttu-id="551c1-188">Seleccione la topología de la lista para ver información acerca de la topología de ejecución.</span><span class="sxs-lookup"><span data-stu-id="551c1-188">Select the topology from the list to view information about the running topology.</span></span>

    ![supervisión de visual studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > <span data-ttu-id="551c1-190">También puede ver las **topologías de Storm** en el **Explorador de servidores** expandiendo **Azure** > **HDInsight** y, después, haciendo clic con el botón derecho en un clúster de Storm en HDInsight y seleccionando **View Storm Topologies** (Ver topologías de Storm).</span><span class="sxs-lookup"><span data-stu-id="551c1-190">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

    <span data-ttu-id="551c1-191">Seleccione la forma de los spouts o bolts para ver información sobre estos componentes.</span><span class="sxs-lookup"><span data-stu-id="551c1-191">Select the shape for the spouts or bolts to view information about these components.</span></span> <span data-ttu-id="551c1-192">Se abrirá una ventana nueva para cada elemento seleccionado.</span><span class="sxs-lookup"><span data-stu-id="551c1-192">A new window opens for each item selected.</span></span>

   > [!NOTE]
   > <span data-ttu-id="551c1-193">El nombre de la topología es el nombre de clase de la topología (en este caso, `HelloWord`) con una marca de tiempo adjunta.</span><span class="sxs-lookup"><span data-stu-id="551c1-193">The name of the topology is the class name of the topology (in this case, `HelloWord`,) with a timestamp appended.</span></span>

7. <span data-ttu-id="551c1-194">Desde la vista **Topology Summary** (Resumen de la topología), seleccione **Kill** (Terminar) para detener la topología.</span><span class="sxs-lookup"><span data-stu-id="551c1-194">From the **Topology Summary** view, select **Kill** to stop the topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="551c1-195">Las topologías de Storm continúan ejecutándose hasta que se detengan o se elimine el clúster.</span><span class="sxs-lookup"><span data-stu-id="551c1-195">Storm topologies continue running until they are stopped or the cluster is deleted.</span></span>


## <a name="rest-api"></a><span data-ttu-id="551c1-196">API de REST</span><span class="sxs-lookup"><span data-stu-id="551c1-196">REST API</span></span>

<span data-ttu-id="551c1-197">La interfaz de usuario de Storm se basa en la API de REST, lo que permite realizar una funcionalidad similar de administración y supervisión mediante la API de REST.</span><span class="sxs-lookup"><span data-stu-id="551c1-197">The Storm UI is built on top of the REST API, so you can perform similar management and monitoring functionality by using the REST API.</span></span> <span data-ttu-id="551c1-198">Puede usar la API de REST para crear herramientas personalizadas para administrar y supervisar las topologías de Storm.</span><span class="sxs-lookup"><span data-stu-id="551c1-198">You can use the REST API to create custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="551c1-199">Para más información, vea la [API de REST de la IU de Storm](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span><span class="sxs-lookup"><span data-stu-id="551c1-199">For more information, see [Storm UI REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span></span> <span data-ttu-id="551c1-200">La siguiente información es específica para usar la API de REST con Apache Storm en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="551c1-200">The following information is specific to using the REST API with Apache Storm on HDInsight.</span></span>

### <a name="base-uri"></a><span data-ttu-id="551c1-201">URI base</span><span class="sxs-lookup"><span data-stu-id="551c1-201">Base URI</span></span>

<span data-ttu-id="551c1-202">El URI de base para la API de REST en los clústeres de HDInsight es **https://&lt;clustername>.azurehdinsight.net/stormui/api/v1/**, donde **clustername** es el nombre del clúster de Storm en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="551c1-202">The base URI for the REST API on HDInsight clusters is **https://&lt;clustername>.azurehdinsight.net/stormui/api/v1/**, where **clustername** is the name of your Storm on HDInsight cluster.</span></span>

### <a name="authentication"></a><span data-ttu-id="551c1-203">Autenticación</span><span class="sxs-lookup"><span data-stu-id="551c1-203">Authentication</span></span>

<span data-ttu-id="551c1-204">Las solicitudes a la API de REST deben usar la **autenticación básica**; use el nombre y la contraseña de administrador del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="551c1-204">Requests to the REST API must use **basic authentication**, so you use the HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="551c1-205">Dado que la autenticación básica se envía mediante texto no cifrado, **siempre** debe usar HTTPS para proteger las comunicaciones con el clúster.</span><span class="sxs-lookup"><span data-stu-id="551c1-205">Because basic authentication is sent by using clear text, you should **always** use HTTPS to secure communications with the cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="551c1-206">Valores devueltos</span><span class="sxs-lookup"><span data-stu-id="551c1-206">Return values</span></span>

<span data-ttu-id="551c1-207">La información que se devuelve de la API de REST solo se puede utilizar desde dentro del clúster o de máquinas virtuales en la misma red virtual de Azure que el clúster.</span><span class="sxs-lookup"><span data-stu-id="551c1-207">Information that is returned from the REST API may only be usable from within the cluster or virtual machines on the same Azure Virtual Network as the cluster.</span></span> <span data-ttu-id="551c1-208">Por ejemplo, no se puede obtener el acceso desde Internet al nombre de dominio completo (FQDN) devuelto para servidores de Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="551c1-208">For example, the fully qualified domain name (FQDN) returned for Zookeeper servers are not be accessible from the Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="551c1-209">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="551c1-209">Next Steps</span></span>

<span data-ttu-id="551c1-210">Ahora que ha aprendido cómo implementar y supervisar las topologías mediante el panel Storm, aprenda cómo:</span><span class="sxs-lookup"><span data-stu-id="551c1-210">Now that you've learned how to deploy and monitor topologies by using the Storm Dashboard, learn how to:</span></span>

* [<span data-ttu-id="551c1-211">Ejecutar topologías de C# mediante las herramientas de HDInsight para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="551c1-211">Develop C# topologies using the HDInsight Tools for Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [<span data-ttu-id="551c1-212">Desarrollar topologías basadas en Java con Maven</span><span class="sxs-lookup"><span data-stu-id="551c1-212">Develop Java-based topologies using Maven</span></span>](hdinsight-storm-develop-java-topology.md)

<span data-ttu-id="551c1-213">Para obtener una lista con más topologías de ejemplo, consulte [Topologías de ejemplo para Storm en HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="551c1-213">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png
