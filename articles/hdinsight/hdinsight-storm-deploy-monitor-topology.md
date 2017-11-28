---
title: "aaaDeploy y administrar topologías de Apache Storm en HDInsight | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toodeploy, supervisar y administrar topologías de Apache Storm con hello aluvión de panel en HDInsight. Utilice herramientas de Hadoop para Visual Studio"
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
ms.openlocfilehash: 05f05fe8dd519fe99fb771d36bfc3d28168ca85f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a><span data-ttu-id="cd409-104">Implementación y administración de topologías de Apache Storm en HDInsight basado en Windows</span><span class="sxs-lookup"><span data-stu-id="cd409-104">Deploy and manage Apache Storm topologies on Windows-based HDInsight</span></span>

<span data-ttu-id="cd409-105">Hola aluvión de panel permite tooeasily implementar y ejecutar el clúster de HDInsight de Apache Storm topologías tooyour utilizando el explorador web.</span><span class="sxs-lookup"><span data-stu-id="cd409-105">hello Storm Dashboard allows you tooeasily deploy and run Apache Storm topologies tooyour HDInsight cluster by using your web browser.</span></span> <span data-ttu-id="cd409-106">También puede utilizar Hola panel toomonitor y administrar topologías de ejecución.</span><span class="sxs-lookup"><span data-stu-id="cd409-106">You can also use hello dashboard toomonitor and manage running topologies.</span></span> <span data-ttu-id="cd409-107">Si utiliza Visual Studio, hello HDInsight Tools para Visual Studio proporciona características similares en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cd409-107">If you use Visual Studio, hello HDInsight Tools for Visual Studio provide similar features in Visual Studio.</span></span>

<span data-ttu-id="cd409-108">Hola aluvión de panel y las características de Storm Hola Hola HDInsight Tools dependen de hello API de REST de Storm, que puede ser usado toocreate sus propias soluciones de supervisión y administración.</span><span class="sxs-lookup"><span data-stu-id="cd409-108">hello Storm Dashboard and hello Storm features in hello HDInsight Tools rely on hello Storm REST API, which can be used toocreate your own monitoring and management solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cd409-109">pasos de Hello en este documento, es necesario un aluvión de clúster de HDInsight que usa Windows como sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd409-109">hello steps in this document require a Storm on HDInsight cluster that uses Windows as hello operating system.</span></span> <span data-ttu-id="cd409-110">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="cd409-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="cd409-111">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="cd409-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="cd409-112">Para más información sobre la implementación y la administración de topologías de Storm con un clúster de HDInsight que usa Linux, consulte [Implementación y administración de topologías de Apache Storm en HDInsight basado en Linux](hdinsight-storm-deploy-monitor-topology-linux.md).</span><span class="sxs-lookup"><span data-stu-id="cd409-112">For information on deploying and managing Storm topologies with an HDInsight cluster that uses Linux, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd409-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cd409-113">Prerequisites</span></span>

* <span data-ttu-id="cd409-114">**Apache Storm en HDInsight**: consulte [Introducción a Apache Storm en HDInsight](hdinsight-apache-storm-tutorial-get-started.md) para conocer los pasos para la creación de un clúster.</span><span class="sxs-lookup"><span data-stu-id="cd409-114">**Apache Storm on HDInsight** - see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started.md) for steps on creating a cluster.</span></span>

* <span data-ttu-id="cd409-115">Para hello **aluvión de panel**: un explorador web moderna que es compatible con HTML5.</span><span class="sxs-lookup"><span data-stu-id="cd409-115">For hello **Storm Dashboard**: A modern web browser that supports HTML5.</span></span>

* <span data-ttu-id="cd409-116">Para **Visual Studio** -Azure SDK 2.5.1 o versiones más recientes y Hola HDInsight Tools para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cd409-116">For **Visual Studio** - Azure SDK 2.5.1 or newer and hello HDInsight Tools for Visual Studio.</span></span> <span data-ttu-id="cd409-117">Vea [Introducción al uso de herramientas de HDInsight para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall y configurar las herramientas de HDInsight de Hola para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cd409-117">See [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall and configure hello HDInsight tools for Visual Studio.</span></span>

    <span data-ttu-id="cd409-118">Uno de hello después de versiones de Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="cd409-118">One of hello following versions of Visual Studio:</span></span>

  * <span data-ttu-id="cd409-119">Visual Studio 2012 con la actualización 4</span><span class="sxs-lookup"><span data-stu-id="cd409-119">Visual Studio 2012 with Update 4</span></span>

  * <span data-ttu-id="cd409-120">Visual Studio 2013 con la actualización 4 o Visual Studio Community 2013</span><span class="sxs-lookup"><span data-stu-id="cd409-120">Visual Studio 2013 with Update 4 or Visual Studio 2013 Community</span></span>

  * <span data-ttu-id="cd409-121">Visual Studio 2015 (cualquier edición)</span><span class="sxs-lookup"><span data-stu-id="cd409-121">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="cd409-122">Visual Studio 2017 (cualquier edición)</span><span class="sxs-lookup"><span data-stu-id="cd409-122">Visual Studio 2017 (any edition)</span></span>

## <a name="storm-dashboard"></a><span data-ttu-id="cd409-123">panel de Storm</span><span class="sxs-lookup"><span data-stu-id="cd409-123">Storm Dashboard</span></span>

<span data-ttu-id="cd409-124">Hola aluvión de panel es una página web disponibles en el clúster de Storm.</span><span class="sxs-lookup"><span data-stu-id="cd409-124">hello Storm Dashboard is a web page available on your Storm cluster.</span></span> <span data-ttu-id="cd409-125">dirección URL de Hello es **https://&lt;clustername >.azurehdinsight.net/**, donde **clustername** es Hola nombre de su Storm en clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd409-125">hello URL is **https://&lt;clustername>.azurehdinsight.net/**, where **clustername** is hello name of your Storm on HDInsight cluster.</span></span>

<span data-ttu-id="cd409-126">De arriba Hola de hello aluvión de panel, seleccione **topología enviar**.</span><span class="sxs-lookup"><span data-stu-id="cd409-126">From hello top of hello Storm Dashboard, select **Submit Topology**.</span></span> <span data-ttu-id="cd409-127">Siga las instrucciones de hello en hello página toorun una topología de ejemplo o tooupload y ejecute una topología que ha creado.</span><span class="sxs-lookup"><span data-stu-id="cd409-127">Follow hello instructions on hello page toorun a sample topology or tooupload and run a topology that you created.</span></span>

![Hola Enviar página topología][storm-dashboard-submit]

### <a name="storm-ui"></a><span data-ttu-id="cd409-129">UI de Storm</span><span class="sxs-lookup"><span data-stu-id="cd409-129">Storm UI</span></span>

<span data-ttu-id="cd409-130">En hello aluvión de panel, seleccione hello **aluvión de interfaz de usuario** vínculo.</span><span class="sxs-lookup"><span data-stu-id="cd409-130">From hello Storm Dashboard, select hello **Storm UI** link.</span></span> <span data-ttu-id="cd409-131">Esto muestra información sobre el clúster hello, en tooany adición ejecutando topologías.</span><span class="sxs-lookup"><span data-stu-id="cd409-131">This displays information about hello cluster, in addition tooany running topologies.</span></span>

![interfaz de usuario de Hello storm][storm-dashboard-ui]

> [!NOTE]
> <span data-ttu-id="cd409-133">Con algunas versiones de Internet Explorer, es posible que descubra que Hola que aluvión de interfaz de usuario no se actualiza después de que ha visitado en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="cd409-133">With some versions of Internet Explorer, you may discover that hello Storm UI does not refresh after you have first visited it.</span></span> <span data-ttu-id="cd409-134">Por ejemplo, no puede mostrar nuevas topologías de Hola que ha enviado o puede mostrar una topología como activo cuando se desactivado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cd409-134">For example, it may not show hello new topologies you submitted, or it may show a topology as active when you previously deactivated it.</span></span> <span data-ttu-id="cd409-135">Microsoft conoce este problema y está trabajando para conseguir una solución.</span><span class="sxs-lookup"><span data-stu-id="cd409-135">Microsoft is aware of this issue and is working on a solution.</span></span>

#### <a name="main-page"></a><span data-ttu-id="cd409-136">Página principal</span><span class="sxs-lookup"><span data-stu-id="cd409-136">Main page</span></span>

<span data-ttu-id="cd409-137">página principal de Hola de hello aluvión de interfaz de usuario proporciona Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="cd409-137">hello main page of hello Storm UI provides hello following information:</span></span>

* <span data-ttu-id="cd409-138">**Resumen de clúster**: información básica sobre el clúster de Storm Hola.</span><span class="sxs-lookup"><span data-stu-id="cd409-138">**Cluster summary**: Basic information about hello Storm cluster.</span></span>

* <span data-ttu-id="cd409-139">**Resumen de las topologías**: una lista de las topologías en ejecución.</span><span class="sxs-lookup"><span data-stu-id="cd409-139">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="cd409-140">Usar vínculos de hello en esta sección tooview obtener más información acerca de las topologías específicas.</span><span class="sxs-lookup"><span data-stu-id="cd409-140">Use hello links in this section tooview more information about specific topologies.</span></span>

* <span data-ttu-id="cd409-141">**Resumen de supervisor**: obtener información sobre el supervisor de Storm Hola.</span><span class="sxs-lookup"><span data-stu-id="cd409-141">**Supervisor summary**: Information about hello Storm supervisor.</span></span>

* <span data-ttu-id="cd409-142">**Configuración de Nimbus**: configuración de Nimbus para clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="cd409-142">**Nimbus configuration**: Nimbus configuration for hello cluster.</span></span>

#### <a name="topology-summary"></a><span data-ttu-id="cd409-143">Resumen de las topologías</span><span class="sxs-lookup"><span data-stu-id="cd409-143">Topology summary</span></span>

<span data-ttu-id="cd409-144">Si selecciona un vínculo de hello **resumen de la topología** sección muestra hello después de obtener información acerca de la topología de hello:</span><span class="sxs-lookup"><span data-stu-id="cd409-144">Selecting a link from hello **Topology summary** section displays hello following information about hello topology:</span></span>

* <span data-ttu-id="cd409-145">**Resumen de la topología**: información básica acerca de la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd409-145">**Topology summary**: Basic information about hello topology.</span></span>

* <span data-ttu-id="cd409-146">**Acciones de topología**: acciones de administración que puede realizar para la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd409-146">**Topology actions**: Management actions that you can perform for hello topology.</span></span>

  * <span data-ttu-id="cd409-147">**Activar**: reanuda el procesamiento de una topología desactivada.</span><span class="sxs-lookup"><span data-stu-id="cd409-147">**Activate**: Resumes processing of a deactivated topology.</span></span>

  * <span data-ttu-id="cd409-148">**Desactivar**: pausa una topología en ejecución.</span><span class="sxs-lookup"><span data-stu-id="cd409-148">**Deactivate**: Pauses a running topology.</span></span>

  * <span data-ttu-id="cd409-149">**Reequilibrar**: ajusta el paralelismo de Hola de topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd409-149">**Rebalance**: Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="cd409-150">Debe volver a equilibrar las topologías de ejecución después de que haya cambiado Hola número de nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd409-150">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="cd409-151">Esto permite Hola topología tooadjust paralelismo toocompensate para hello aumenta o reduce el número de nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd409-151">This allows hello topology tooadjust parallelism toocompensate for hello increased or decreased number of nodes in hello cluster.</span></span>

      <span data-ttu-id="cd409-152">Para obtener más información, consulte [descripción paralelismo Hola de una topología de Storm (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="cd409-152">For more information, see [Understanding hello parallelism of a Storm topology (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

  * <span data-ttu-id="cd409-153">**Kill**: termine una topología de Storm después Hola especifica el tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="cd409-153">**Kill**: Terminates a Storm topology after hello specified timeout.</span></span>

* <span data-ttu-id="cd409-154">**Estadísticas de topología**: estadísticas acerca de la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd409-154">**Topology stats**: Statistics about hello topology.</span></span> <span data-ttu-id="cd409-155">Use los vínculos de Hola Hola **ventana** período de tiempo de columna tooset Hola para hello restantes entradas en la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd409-155">Use hello links in hello **Window** column tooset hello timeframe for hello remaining entries on hello page.</span></span>

* <span data-ttu-id="cd409-156">**Spouts**: Hola spouts utilizados por la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd409-156">**Spouts**: hello spouts used by hello topology.</span></span> <span data-ttu-id="cd409-157">Usar vínculos de hello en esta sección tooview obtener más información sobre spouts específicos.</span><span class="sxs-lookup"><span data-stu-id="cd409-157">Use hello links in this section tooview more information about specific spouts.</span></span>

* <span data-ttu-id="cd409-158">**Tornillos**: Hola tornillos utilizados por la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd409-158">**Bolts**: hello bolts used by hello topology.</span></span> <span data-ttu-id="cd409-159">Usar vínculos de hello en esta sección tooview obtener más información acerca de los tornillos específicos.</span><span class="sxs-lookup"><span data-stu-id="cd409-159">Use hello links in this section tooview more information about specific bolts.</span></span>

* <span data-ttu-id="cd409-160">**Configuración de la topología**: configuración de Hola de topología de hello seleccionado.</span><span class="sxs-lookup"><span data-stu-id="cd409-160">**Topology configuration**: hello configuration of hello selected topology.</span></span>

#### <a name="spout-and-bolt-summary"></a><span data-ttu-id="cd409-161">Resumen de spouts y bolts</span><span class="sxs-lookup"><span data-stu-id="cd409-161">Spout and Bolt summary</span></span>

<span data-ttu-id="cd409-162">Seleccionar un pitorro de hello **Spouts** o **tornillos** secciones muestra hello después de obtener información sobre el elemento Hola seleccionado:</span><span class="sxs-lookup"><span data-stu-id="cd409-162">Selecting a spout from hello **Spouts** or **Bolts** sections displays hello following information about hello selected item:</span></span>

* <span data-ttu-id="cd409-163">**Resumen de componentes**: información básica sobre pitorro Hola o rayo.</span><span class="sxs-lookup"><span data-stu-id="cd409-163">**Component summary**: Basic information about hello spout or bolt.</span></span>

* <span data-ttu-id="cd409-164">**Estadísticas de pitorro/rayo**: estadísticas sobre Hola apetezca charlar o el tornillo.</span><span class="sxs-lookup"><span data-stu-id="cd409-164">**Spout/Bolt stats**: Statistics about hello spout or bolt.</span></span> <span data-ttu-id="cd409-165">Use los vínculos de Hola Hola **ventana** período de tiempo de columna tooset Hola para hello restantes entradas en la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd409-165">Use hello links in hello **Window** column tooset hello timeframe for hello remaining entries on hello page.</span></span>

* <span data-ttu-id="cd409-166">**Estadísticas de entrada** (solo tornillo): utilizados por el rayo Hola de flujos de entrada de información acerca de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd409-166">**Input stats** (bolt only): Information about hello input streams consumed by hello bolt.</span></span>

* <span data-ttu-id="cd409-167">**Estadísticas de salida**: información sobre los flujos de hello emitidos por esta apetezca charlar o el tornillo.</span><span class="sxs-lookup"><span data-stu-id="cd409-167">**Output stats**: Information about hello streams emitted by this spout or bolt.</span></span>

* <span data-ttu-id="cd409-168">**Ejecutor**: información sobre instancias de Hola de pitorro Hola o rayo.</span><span class="sxs-lookup"><span data-stu-id="cd409-168">**Executors**: Information about hello instances of hello spout or bolt.</span></span> <span data-ttu-id="cd409-169">Seleccione hello **puerto** entrada para un tooview ejecutor específico un registro de información de diagnóstico generados para esta instancia.</span><span class="sxs-lookup"><span data-stu-id="cd409-169">Select hello **Port** entry for a specific executor tooview a log of diagnostic information produced for this instance.</span></span>

* <span data-ttu-id="cd409-170">**Errores**: cualquier información de error de este spout o bolt.</span><span class="sxs-lookup"><span data-stu-id="cd409-170">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="hdinsight-tools-for-visual-studio"></a><span data-ttu-id="cd409-171">Herramientas de HDInsight para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cd409-171">HDInsight Tools for Visual Studio</span></span>

<span data-ttu-id="cd409-172">Herramientas de HDInsight de Hello puede ser toosubmit usa C# o híbrida topologías tooyour clúster de Storm.</span><span class="sxs-lookup"><span data-stu-id="cd409-172">hello HDInsight Tools can be used toosubmit C# or hybrid topologies tooyour Storm cluster.</span></span> <span data-ttu-id="cd409-173">Hola pasos usa una aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="cd409-173">hello following steps use a sample application.</span></span> <span data-ttu-id="cd409-174">Para obtener información acerca de cómo crear sus propios topologías mediante las herramientas de HDInsight de hello, consulte [C# desarrollar topologías con hello HDInsight Tools para Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="cd409-174">For information about creating your own topologies by using hello HDInsight Tools, see [Develop C# topologies using hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="cd409-175">Usar hello siguiendo los pasos toodeploy una tormenta de ejemplo tooyour en clúster de HDInsight, a continuación, ver y administrar la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd409-175">Use hello following steps toodeploy a sample tooyour Storm on HDInsight cluster, then view and manage hello topology.</span></span>

1. <span data-ttu-id="cd409-176">Si no ha instalado ya Hola versión más reciente de hello HDInsight Tools para Visual Studio, consulte [Introducción al uso de herramientas de HDInsight para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cd409-176">If you have not already installed hello latest version of hello HDInsight Tools for Visual Studio, see [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="cd409-177">Abra Visual Studio, seleccione **Archivo** > **Nuevo** > **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="cd409-177">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="cd409-178">Hola **nuevo proyecto** cuadro de diálogo, expanda **instalado** > **plantillas**y, a continuación, seleccione **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="cd409-178">In hello **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="cd409-179">En la lista Hola de plantillas, seleccione **aluvión de ejemplo**.</span><span class="sxs-lookup"><span data-stu-id="cd409-179">From hello list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="cd409-180">En parte inferior de Hola Hola del cuadro de diálogo, escriba un nombre para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="cd409-180">At hello bottom of hello dialog box, type a name for hello application.</span></span>

    ![imagen](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. <span data-ttu-id="cd409-182">En **el Explorador de soluciones**, haga clic en proyecto de Hola y seleccione **enviar tooStorm en HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="cd409-182">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cd409-183">Si se le solicite, escriba las credenciales de inicio de sesión de hello para la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="cd409-183">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="cd409-184">Si tiene más de una suscripción, inicie sesión en toohello uno que contiene el aluvión en clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd409-184">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="cd409-185">Seleccione el aluvión en clúster de HDInsight de hello **clúster de Storm** lista desplegable y, a continuación, seleccione **enviar**.</span><span class="sxs-lookup"><span data-stu-id="cd409-185">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="cd409-186">Puede supervisar si el envío de hello es correcto mediante hello **salida** ventana.</span><span class="sxs-lookup"><span data-stu-id="cd409-186">You can monitor whether hello submission is successful by using hello **Output** window.</span></span>

6. <span data-ttu-id="cd409-187">Cuando se ha enviado correctamente la topología de hello, Hola **aluvión de topologías** para clúster Hola debería aparecer.</span><span class="sxs-lookup"><span data-stu-id="cd409-187">When hello topology has been successfully submitted, hello **Storm Topologies** for hello cluster should appear.</span></span> <span data-ttu-id="cd409-188">Seleccione topología Hola de hello mostrar tooview información acerca de hello ejecutando topología.</span><span class="sxs-lookup"><span data-stu-id="cd409-188">Select hello topology from hello list tooview information about hello running topology.</span></span>

    ![supervisión de visual studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > <span data-ttu-id="cd409-190">También puede ver las **topologías de Storm** en el **Explorador de servidores** expandiendo **Azure** > **HDInsight** y, después, haciendo clic con el botón derecho en un clúster de Storm en HDInsight y seleccionando **View Storm Topologies** (Ver topologías de Storm).</span><span class="sxs-lookup"><span data-stu-id="cd409-190">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

    <span data-ttu-id="cd409-191">Seleccione la forma de Hola Hola spouts o tornillos tooview información acerca de estos componentes.</span><span class="sxs-lookup"><span data-stu-id="cd409-191">Select hello shape for hello spouts or bolts tooview information about these components.</span></span> <span data-ttu-id="cd409-192">Se abrirá una ventana nueva para cada elemento seleccionado.</span><span class="sxs-lookup"><span data-stu-id="cd409-192">A new window opens for each item selected.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cd409-193">nombre de Hola de topología de hello es el nombre de clase de Hola de topología de hello (en este caso, `HelloWord`,) con una marca de tiempo que se anexa.</span><span class="sxs-lookup"><span data-stu-id="cd409-193">hello name of hello topology is hello class name of hello topology (in this case, `HelloWord`,) with a timestamp appended.</span></span>

7. <span data-ttu-id="cd409-194">De hello **resumen de la topología** visualizarla, seleccione **Kill** topología de hello toostop.</span><span class="sxs-lookup"><span data-stu-id="cd409-194">From hello **Topology Summary** view, select **Kill** toostop hello topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cd409-195">Topologías de Storm continúan ejecutándose hasta que se hayan detenido o se elimina el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd409-195">Storm topologies continue running until they are stopped or hello cluster is deleted.</span></span>


## <a name="rest-api"></a><span data-ttu-id="cd409-196">API de REST</span><span class="sxs-lookup"><span data-stu-id="cd409-196">REST API</span></span>

<span data-ttu-id="cd409-197">Hola aluvión de interfaz de usuario se basa en hello API de REST, para que pueda realizar la administración y funcionalidad de supervisión mediante el uso de API de REST de hello similares.</span><span class="sxs-lookup"><span data-stu-id="cd409-197">hello Storm UI is built on top of hello REST API, so you can perform similar management and monitoring functionality by using hello REST API.</span></span> <span data-ttu-id="cd409-198">Puede usar herramientas personalizadas de toocreate de API de REST de Hola para administrar y supervisar las topologías de Storm.</span><span class="sxs-lookup"><span data-stu-id="cd409-198">You can use hello REST API toocreate custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="cd409-199">Para más información, vea la [API de REST de la IU de Storm](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span><span class="sxs-lookup"><span data-stu-id="cd409-199">For more information, see [Storm UI REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span></span> <span data-ttu-id="cd409-200">Hello siguiente información es específica toousing hello API de REST con Apache Storm en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd409-200">hello following information is specific toousing hello REST API with Apache Storm on HDInsight.</span></span>

### <a name="base-uri"></a><span data-ttu-id="cd409-201">URI base</span><span class="sxs-lookup"><span data-stu-id="cd409-201">Base URI</span></span>

<span data-ttu-id="cd409-202">Hola URI base para la API de REST de hello en clústeres de HDInsight es **https://&lt;clustername >.azurehdinsight.net/stormui/api/v1/**, donde **clustername** es el nombre de Hola de su Storm en Clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd409-202">hello base URI for hello REST API on HDInsight clusters is **https://&lt;clustername>.azurehdinsight.net/stormui/api/v1/**, where **clustername** is hello name of your Storm on HDInsight cluster.</span></span>

### <a name="authentication"></a><span data-ttu-id="cd409-203">Autenticación</span><span class="sxs-lookup"><span data-stu-id="cd409-203">Authentication</span></span>

<span data-ttu-id="cd409-204">Toohello de las solicitudes que se debe usar la API de REST **la autenticación básica**, por lo que usar el nombre del Administrador de clúster de HDInsight de hello y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="cd409-204">Requests toohello REST API must use **basic authentication**, so you use hello HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="cd409-205">Dado que la autenticación básica se envía mediante el uso de texto no cifrado, debe **siempre** utilizar comunicaciones HTTPS a toosecure con clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd409-205">Because basic authentication is sent by using clear text, you should **always** use HTTPS toosecure communications with hello cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="cd409-206">Valores devueltos</span><span class="sxs-lookup"><span data-stu-id="cd409-206">Return values</span></span>

<span data-ttu-id="cd409-207">Información que se devuelve de hello API de REST solo pueden ser utilizable desde dentro de clúster de Hola o máquinas virtuales en Hola misma red Virtual de Azure como clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd409-207">Information that is returned from hello REST API may only be usable from within hello cluster or virtual machines on hello same Azure Virtual Network as hello cluster.</span></span> <span data-ttu-id="cd409-208">Por ejemplo, nombre de dominio completo de hello (FQDN) devuelto para los servidores de Zookeeper no se pueden accesible desde Internet Hola.</span><span class="sxs-lookup"><span data-stu-id="cd409-208">For example, hello fully qualified domain name (FQDN) returned for Zookeeper servers are not be accessible from hello Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd409-209">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cd409-209">Next Steps</span></span>

<span data-ttu-id="cd409-210">Ahora que ha aprendido cómo topologías toodeploy y monitor mediante el uso de Hola aluvión de panel, obtenga información acerca de cómo:</span><span class="sxs-lookup"><span data-stu-id="cd409-210">Now that you've learned how toodeploy and monitor topologies by using hello Storm Dashboard, learn how to:</span></span>

* [<span data-ttu-id="cd409-211">Desarrollar las topologías de C# con hello HDInsight Tools para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cd409-211">Develop C# topologies using hello HDInsight Tools for Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [<span data-ttu-id="cd409-212">Desarrollar topologías basadas en Java con Maven</span><span class="sxs-lookup"><span data-stu-id="cd409-212">Develop Java-based topologies using Maven</span></span>](hdinsight-storm-develop-java-topology.md)

<span data-ttu-id="cd409-213">Para obtener una lista con más topologías de ejemplo, consulte [Topologías de ejemplo para Storm en HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="cd409-213">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png
