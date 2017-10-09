---
title: ejemplos de inicio de aaaStorm en Apache Storm en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toodo análisis de grandes cantidades de datos y procesar los datos en tiempo real con Apache Storm y Hola ejemplos de inicio de storm en HDInsight."
keywords: storm-starter, ejemplo de apache storm
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: d710dcac-35d1-4c27-a8d6-acaf8146b485
ms.service: hdinsight
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: bb6d6549e67ca5b557f0692f98c89692a87267b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
#<a name="get-started-with-apache-storm-on-hdinsight-using-hello-storm-starter-examples"></a><span data-ttu-id="b5784-104">Introducción a Apache Storm en HDInsight con ejemplos de hello storm-inicio</span><span class="sxs-lookup"><span data-stu-id="b5784-104">Get started with Apache Storm on HDInsight using hello storm-starter examples</span></span>

<span data-ttu-id="b5784-105">Obtenga información acerca de cómo toouse Apache Storm en HDInsight utilizando Hola ejemplos storm starter.</span><span class="sxs-lookup"><span data-stu-id="b5784-105">Learn how toouse Apache Storm in HDInsight using hello storm-starter examples.</span></span>

<span data-ttu-id="b5784-106">Apache Storm es un sistema de cálculo distribuido, escalable, con tolerancia a errores y en tiempo real para el procesamiento de secuencias de datos.</span><span class="sxs-lookup"><span data-stu-id="b5784-106">Apache Storm is a scalable, fault-tolerant, distributed, real-time computation system for processing streams of data.</span></span> <span data-ttu-id="b5784-107">Con Storm en HDInsight de Azure, puede crear un clúster de Storm basado en la nube que realice análisis en tiempo real de grandes cantidades de datos en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="b5784-107">With Storm on Azure HDInsight, you can create a cloud-based Storm cluster that performs big data analytics in real time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b5784-108">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="b5784-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b5784-109">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="b5784-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5784-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b5784-110">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="b5784-111">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="b5784-111">**An Azure subscription**.</span></span> <span data-ttu-id="b5784-112">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="b5784-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="b5784-113">**Familiaridad con SSH y SCP**.</span><span class="sxs-lookup"><span data-stu-id="b5784-113">**Familiarity with SSH and SCP**.</span></span> <span data-ttu-id="b5784-114">Para obtener más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b5784-114">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-a-storm-cluster"></a><span data-ttu-id="b5784-115">Creación de un clúster de Storm</span><span class="sxs-lookup"><span data-stu-id="b5784-115">Create a Storm cluster</span></span>

<span data-ttu-id="b5784-116">Usar hello siguiendo los pasos toocreate una tormenta en clúster de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b5784-116">Use hello following steps toocreate a Storm on HDInsight cluster:</span></span>

1. <span data-ttu-id="b5784-117">De hello [portal de Azure](https://portal.azure.com), seleccione **+ nuevo**, **Intelligence + análisis**y, a continuación, seleccione **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="b5784-117">From hello [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>

    ![Creación de un clúster de HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. <span data-ttu-id="b5784-119">De hello **Fundamentos** hoja, escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="b5784-119">From hello **Basics** blade, enter hello following information:</span></span>

    * <span data-ttu-id="b5784-120">**Nombre del clúster**: nombre de Hola Hola del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b5784-120">**Cluster Name**: hello name of hello HDInsight cluster.</span></span>
    * <span data-ttu-id="b5784-121">**Suscripción**: seleccione Hola suscripción toouse.</span><span class="sxs-lookup"><span data-stu-id="b5784-121">**Subscription**: Select hello subscription toouse.</span></span>
    * <span data-ttu-id="b5784-122">**Nombre de usuario de inicio de sesión del clúster** y **contraseña de inicio de sesión de clúster**: inicio de sesión de hello al tener acceso a los clústeres de Hola a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b5784-122">**Cluster login username** and **Cluster login password**: hello login when accessing hello cluster over HTTPS.</span></span> <span data-ttu-id="b5784-123">Utilice estos servicios de tooaccess de credenciales como Hola interfaz de usuario de Ambari Web o API de REST.</span><span class="sxs-lookup"><span data-stu-id="b5784-123">You use these credentials tooaccess services such as hello Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="b5784-124">**Secure Shell (SSH) username**: inicio de sesión de hello usado al acceder a clúster hello mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="b5784-124">**Secure Shell (SSH) username**: hello login used when accessing hello cluster over SSH.</span></span> <span data-ttu-id="b5784-125">De forma predeterminada contraseña hello es Hola igual que la contraseña de inicio de sesión de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5784-125">By default hello password is hello same as hello cluster login password.</span></span>
    * <span data-ttu-id="b5784-126">**Grupo de recursos**: clúster hello toocreate de grupo de recursos de hello en.</span><span class="sxs-lookup"><span data-stu-id="b5784-126">**Resource Group**: hello resource group toocreate hello cluster in.</span></span>
    * <span data-ttu-id="b5784-127">**Ubicación**: Hola región de Azure toocreate Hola clúster.</span><span class="sxs-lookup"><span data-stu-id="b5784-127">**Location**: hello Azure region toocreate hello cluster in.</span></span>

    ![Seleccione la suscripción.](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. <span data-ttu-id="b5784-129">Seleccione **clúster tipo**, y, a continuación, Hola de conjunto de valores de hello **configuración de clúster** hoja:</span><span class="sxs-lookup"><span data-stu-id="b5784-129">Select **Cluster type**, and then set hello following values on hello **Cluster configuration** blade:</span></span>

    * <span data-ttu-id="b5784-130">**Tipo de clúster**: Storm</span><span class="sxs-lookup"><span data-stu-id="b5784-130">**Cluster Type**: Storm</span></span>

    * <span data-ttu-id="b5784-131">**Sistema operativo**: Linux</span><span class="sxs-lookup"><span data-stu-id="b5784-131">**Operating system**: Linux</span></span>

    * <span data-ttu-id="b5784-132">**Versión**: Storm 1.1.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="b5784-132">**Version**: Storm 1.1.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="b5784-133">**Nivel de clúster**: estándar</span><span class="sxs-lookup"><span data-stu-id="b5784-133">**Cluster Tier**: Standard</span></span>

    <span data-ttu-id="b5784-134">Por último, utilice hello **seleccione** botón toosave configuración.</span><span class="sxs-lookup"><span data-stu-id="b5784-134">Finally, use hello **Select** button toosave settings.</span></span>

    ![Seleccionar el tipo de clúster](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="b5784-136">Después de seleccionar el tipo de clúster de hello, usar hello __seleccione__ tooset Hola clúster tipo de botón.</span><span class="sxs-lookup"><span data-stu-id="b5784-136">After selecting hello cluster type, use hello __Select__ button tooset hello cluster type.</span></span> <span data-ttu-id="b5784-137">A continuación, usar hello __siguiente__ configuración básica del botón toofinish.</span><span class="sxs-lookup"><span data-stu-id="b5784-137">Next, use hello __Next__ button toofinish basic configuration.</span></span>

5. <span data-ttu-id="b5784-138">De hello **almacenamiento** hoja, seleccione o cree una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b5784-138">From hello **Storage** blade, select or create a Storage account.</span></span> <span data-ttu-id="b5784-139">Para conocer los pasos hello en este documento, deje Hola otros campos en esta hoja en valores predeterminados de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5784-139">For hello steps in this document, leave hello other fields on this blade at hello default values.</span></span> <span data-ttu-id="b5784-140">Hola de uso __siguiente__ configuración de almacenamiento de toosave de botón.</span><span class="sxs-lookup"><span data-stu-id="b5784-140">Use hello __Next__ button toosave storage configuration.</span></span>

    ![Establecer la configuración de cuenta de almacenamiento de Hola para HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. <span data-ttu-id="b5784-142">De hello **resumen** hoja, revisar la configuración de hello para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5784-142">From hello **Summary** blade, review hello configuration for hello cluster.</span></span> <span data-ttu-id="b5784-143">Hola de uso __editar__ vincula toochange cualquier configuración que no sean correcta.</span><span class="sxs-lookup"><span data-stu-id="b5784-143">Use hello __Edit__ links toochange any settings that are incorrect.</span></span> <span data-ttu-id="b5784-144">Por último, utilice el clúster de the__Create__ botón toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="b5784-144">Finally, use the__Create__ button toocreate hello cluster.</span></span>

    ![Resumen de configuración del clúster](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > <span data-ttu-id="b5784-146">Puede durar de clúster de too20 minutos toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="b5784-146">It can take up too20 minutes toocreate hello cluster.</span></span>

## <a name="run-a-storm-starter-sample-on-hdinsight"></a><span data-ttu-id="b5784-147">Ejecución de un ejemplo de Storm-Starter en HDInsight</span><span class="sxs-lookup"><span data-stu-id="b5784-147">Run a storm-starter sample on HDInsight</span></span>

1. <span data-ttu-id="b5784-148">Conecte el clúster de HDInsight de toohello mediante SSH:</span><span class="sxs-lookup"><span data-stu-id="b5784-148">Connect toohello HDInsight cluster using SSH:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="b5784-149">Si utiliza un toosecure de contraseña de su cuenta de usuario SSH, son tooenter solicitada se.</span><span class="sxs-lookup"><span data-stu-id="b5784-149">If you used a password toosecure your SSH user account, you are prompted tooenter it.</span></span> <span data-ttu-id="b5784-150">Si utiliza una clave pública, que necesita utilizar hello `-i` parámetro toospecify Hola clave privada correspondiente.</span><span class="sxs-lookup"><span data-stu-id="b5784-150">If you used a public key, you may need use hello `-i` parameter toospecify hello matching private key.</span></span> <span data-ttu-id="b5784-151">Por ejemplo: `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="b5784-151">For example, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

    <span data-ttu-id="b5784-152">Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b5784-152">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="b5784-153">Usar hello después comando toostart una topología de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b5784-153">Use hello following command toostart an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > <span data-ttu-id="b5784-154">En versiones anteriores de HDInsight, nombre de clase de Hola de topología de hello es `storm.starter.WordCountTopology` en lugar de `org.apache.storm.starter.WordCountTopology`.</span><span class="sxs-lookup"><span data-stu-id="b5784-154">On previous versions of HDInsight, hello class name of hello topology is `storm.starter.WordCountTopology` instead of `org.apache.storm.starter.WordCountTopology`.</span></span>

    <span data-ttu-id="b5784-155">Este comando inicia la topología de WordCount de ejemplo de Hola en clúster de hello, con un nombre descriptivo de 'wordcount'.</span><span class="sxs-lookup"><span data-stu-id="b5784-155">This command starts hello example WordCount topology on hello cluster, with a friendly name of 'wordcount'.</span></span> <span data-ttu-id="b5784-156">Genera aleatoriamente frases y repetición de Hola de recuento de cada palabra en las frases de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5784-156">It randomly generates sentences and count hello occurrence of each word in hello sentences.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b5784-157">Al enviar su propio clúster de toohello topologías, primero debe copiar archivo jar de Hola que contiene el clúster de hello antes de usar hello `storm` comando.</span><span class="sxs-lookup"><span data-stu-id="b5784-157">When submitting your own topologies toohello cluster, you must first copy hello jar file containing hello cluster before using hello `storm` command.</span></span> <span data-ttu-id="b5784-158">Hola de uso `scp` archivo de comandos toocopy Hola.</span><span class="sxs-lookup"><span data-stu-id="b5784-158">Use hello `scp` command toocopy hello file.</span></span> <span data-ttu-id="b5784-159">Por ejemplo: `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="b5784-159">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
    >
    > <span data-ttu-id="b5784-160">ejemplo de WordCount Hello y otros ejemplos de storm starter, ya están incluidas en el clúster en `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="b5784-160">hello WordCount example, and other storm-starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

<span data-ttu-id="b5784-161">Si está interesado en Ver origen Hola para obtener ejemplos de inicio aluvión de hello, puede encontrar código de hello en [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span><span class="sxs-lookup"><span data-stu-id="b5784-161">If you are interested in viewing hello source for hello storm-starter examples, you can find hello code at [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span></span> <span data-ttu-id="b5784-162">Este vínculo es para Storm 1.1.x, que se proporciona con HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="b5784-162">This link is for Storm 1.1.x, which is provided with HDInsight 3.6.</span></span> <span data-ttu-id="b5784-163">Para otras versiones de Storm, usar hello __bifurcación__ situado en la parte superior de Hola de hello página tooselect una versión diferente de Storm.</span><span class="sxs-lookup"><span data-stu-id="b5784-163">For other versions of Storm, use hello __Branch__ button at hello top of hello page tooselect a different Storm version.</span></span>

## <a name="monitor-hello-topology"></a><span data-ttu-id="b5784-164">Topología de Hola de Monitor</span><span class="sxs-lookup"><span data-stu-id="b5784-164">Monitor hello topology</span></span>

<span data-ttu-id="b5784-165">Hola aluvión de interfaz de usuario proporciona una interfaz web para trabajar con topologías en ejecución y se incluye en el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b5784-165">hello Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span>

<span data-ttu-id="b5784-166">Usar hello después de la topología de hello toomonitor pasos con hello aluvión de interfaz de usuario:</span><span class="sxs-lookup"><span data-stu-id="b5784-166">Use hello following steps toomonitor hello topology using hello Storm UI:</span></span>

1. <span data-ttu-id="b5784-167">Hola toodisplay aluvión de interfaz de usuario, abra un web explorador toohttps://CLUSTERNAME.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="b5784-167">toodisplay hello Storm UI, open a web browser toohttps://CLUSTERNAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="b5784-168">Reemplace **CLUSTERNAME** con nombre hello del clúster.</span><span class="sxs-lookup"><span data-stu-id="b5784-168">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b5784-169">Si se le solicita tooprovide un nombre de usuario y una contraseña, escriba Administrador de clústeres de hello (admin) y la contraseña que ha utilizado al crear clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="b5784-169">If asked tooprovide a user name and password, enter hello cluster administrator (admin) and password that you used when creating hello cluster.</span></span>

2. <span data-ttu-id="b5784-170">En **resumen de la topología**, seleccione hello **wordcount** entrada Hola **nombre** columna.</span><span class="sxs-lookup"><span data-stu-id="b5784-170">Under **Topology summary**, select hello **wordcount** entry in hello **Name** column.</span></span> <span data-ttu-id="b5784-171">Se muestra información acerca de la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5784-171">Information about hello topology is displayed.</span></span>

    ![Panel de Storm con la información de topología de WordCount de Storm-Starter.](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    <span data-ttu-id="b5784-173">Esta página proporciona Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="b5784-173">This page provides hello following information:</span></span>

    * <span data-ttu-id="b5784-174">**Estadísticas de topología** -información básica sobre el rendimiento de la topología de hello, que se organizan en las ventanas de tiempo.</span><span class="sxs-lookup"><span data-stu-id="b5784-174">**Topology stats** - Basic information on hello topology performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="b5784-175">Al seleccionar un período de tiempo de hora específica ventana cambios hello para la información que se muestra en otras secciones de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5784-175">Selecting a specific time window changes hello time window for information displayed in other sections of hello page.</span></span>

    * <span data-ttu-id="b5784-176">**Spouts** -información básica sobre spouts, incluido el último error de hello devuelto por cada pitorro.</span><span class="sxs-lookup"><span data-stu-id="b5784-176">**Spouts** - Basic information about spouts, including hello last error returned by each spout.</span></span>

    * <span data-ttu-id="b5784-177">**Bolts** : información básica sobre bolts.</span><span class="sxs-lookup"><span data-stu-id="b5784-177">**Bolts** - Basic information about bolts.</span></span>

    * <span data-ttu-id="b5784-178">**Configuración de la topología** -información detallada sobre la configuración de la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5784-178">**Topology configuration** - Detailed information about hello topology configuration.</span></span>

    <span data-ttu-id="b5784-179">Esta página también proporciona las acciones que pueden realizarse en la topología de hello:</span><span class="sxs-lookup"><span data-stu-id="b5784-179">This page also provides actions that can be taken on hello topology:</span></span>

    * <span data-ttu-id="b5784-180">**Activar** : reanuda el procesamiento de una topología desactivada.</span><span class="sxs-lookup"><span data-stu-id="b5784-180">**Activate** - Resumes processing of a deactivated topology.</span></span>

    * <span data-ttu-id="b5784-181">**Desactivar** : pausa una topología en ejecución.</span><span class="sxs-lookup"><span data-stu-id="b5784-181">**Deactivate** - Pauses a running topology.</span></span>

    * <span data-ttu-id="b5784-182">**Reequilibrar** -ajusta paralelismo Hola de topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5784-182">**Rebalance** - Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="b5784-183">Debe volver a equilibrar las topologías de ejecución después de que haya cambiado Hola número de nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5784-183">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="b5784-184">Reequilibrio ajusta toocompensate de paralelismo para número aumenta o disminuye de Hola de nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5784-184">Rebalancing adjusts parallelism toocompensate for hello increased/decreased number of nodes in hello cluster.</span></span> <span data-ttu-id="b5784-185">Para obtener más información, consulte [descripción paralelismo Hola de una topología de Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="b5784-185">For more information, see [Understanding hello parallelism of a Storm topology](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

    * <span data-ttu-id="b5784-186">**Kill** -termine una topología de Storm después Hola especifica el tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="b5784-186">**Kill** - Terminates a Storm topology after hello specified timeout.</span></span>

3. <span data-ttu-id="b5784-187">En esta página, seleccione una entrada de hello **Spouts** o **tornillos** sección.</span><span class="sxs-lookup"><span data-stu-id="b5784-187">From this page, select an entry from hello **Spouts** or **Bolts** section.</span></span> <span data-ttu-id="b5784-188">Se muestra información acerca del componente seleccionado Hola.</span><span class="sxs-lookup"><span data-stu-id="b5784-188">Information about hello selected component is displayed.</span></span>

    ![Panel de Storm con información acerca de los componentes seleccionados.](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    <span data-ttu-id="b5784-190">Esta página muestra hello siguiente información:</span><span class="sxs-lookup"><span data-stu-id="b5784-190">This page displays hello following information:</span></span>

    * <span data-ttu-id="b5784-191">**Estadísticas de pitorro/rayo** -información básica sobre el rendimiento de componente de hello, que se organizan en las ventanas de tiempo.</span><span class="sxs-lookup"><span data-stu-id="b5784-191">**Spout/Bolt stats** - Basic information on hello component performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="b5784-192">Al seleccionar un período de tiempo de hora específica ventana cambios hello para la información que se muestra en otras secciones de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5784-192">Selecting a specific time window changes hello time window for information displayed in other sections of hello page.</span></span>

    * <span data-ttu-id="b5784-193">**Estadísticas de entrada** (solo tornillo): información sobre los componentes que generan datos utilizados por el rayo Hola.</span><span class="sxs-lookup"><span data-stu-id="b5784-193">**Input stats** (bolt only) - Information on components that produce data consumed by hello bolt.</span></span>

    * <span data-ttu-id="b5784-194">**Estadísticas de salida** : información sobre los datos que emite este bolt.</span><span class="sxs-lookup"><span data-stu-id="b5784-194">**Output stats** - Information on data emitted by this bolt.</span></span>

    * <span data-ttu-id="b5784-195">**Ejecutores** : información sobre las instancias de este componente.</span><span class="sxs-lookup"><span data-stu-id="b5784-195">**Executors** - Information on instances of this component.</span></span>

    * <span data-ttu-id="b5784-196">**Errores** : errores que ha generado este componente.</span><span class="sxs-lookup"><span data-stu-id="b5784-196">**Errors** - Errors produced by this component.</span></span>

4. <span data-ttu-id="b5784-197">Al ver los detalles de Hola de un pitorro o rayo, seleccione una entrada de hello **puerto** columna Hola **ejecutor** sección tooview detalles para una instancia específica del componente de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5784-197">When viewing hello details of a spout or bolt, select an entry from hello **Port** column in hello **Executors** section tooview details for a specific instance of hello component.</span></span>

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    <span data-ttu-id="b5784-198">En este ejemplo, hello word **siete** se ha producido 1493957 veces.</span><span class="sxs-lookup"><span data-stu-id="b5784-198">In this example, hello word **seven** has occurred 1493957 times.</span></span> <span data-ttu-id="b5784-199">Este recuento indica cuántas veces se ha encontrado la palabra Hola desde que se inició esta topología.</span><span class="sxs-lookup"><span data-stu-id="b5784-199">This count is how many times hello word has been encountered since this topology was started.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="b5784-200">Detener la topología de Hola</span><span class="sxs-lookup"><span data-stu-id="b5784-200">Stop hello topology</span></span>

<span data-ttu-id="b5784-201">Devolver toohello **resumen de la topología** página topología de recuento de palabras de hello y, a continuación, seleccione hello **Kill** botón de hello **acciones de topología** sección.</span><span class="sxs-lookup"><span data-stu-id="b5784-201">Return toohello **Topology summary** page for hello word-count topology, and then select hello **Kill** button from hello **Topology actions** section.</span></span> <span data-ttu-id="b5784-202">Cuando se le solicite, escriba 10 para hello segundos toowait antes de detener la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5784-202">When prompted, enter 10 for hello seconds toowait before stopping hello topology.</span></span> <span data-ttu-id="b5784-203">Después de tiempo de espera de hello, topología Hola ya no aparece cuando visiten hello **aluvión de interfaz de usuario** sección del panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5784-203">After hello timeout period, hello topology no longer appears when you visit hello **Storm UI** section of hello dashboard.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="b5784-204">Eliminar el clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="b5784-204">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="b5784-205">Si experimenta un problema con la creación de clústeres de HDInsight, consulte los [requisitos de control de acceso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="b5784-205">If you run into an issue with creating HDInsight cluster, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <span data-ttu-id="b5784-206"><a id="next"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b5784-206"><a id="next"></a>Next steps</span></span>

<span data-ttu-id="b5784-207">En este tutorial Apache Storm, ha aprendido conceptos básicos de hello sobre cómo trabajar con Storm en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b5784-207">In this Apache Storm tutorial, you learned hello basics of working with Storm on HDInsight.</span></span> <span data-ttu-id="b5784-208">A continuación, obtenga información acerca de cómo demasiado[topologías de basados en Java desarrollar con Maven](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="b5784-208">Next, learn how too[Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="b5784-209">Si ya está familiarizado con el desarrollo de topologías basados en Java y desea toodeploy una tooHDInsight topología existente, consulte [implementar y administrar topologías de Apache Storm en HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b5784-209">If you're already familiar with developing Java-based topologies and want toodeploy an existing topology tooHDInsight, see [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span></span>

<span data-ttu-id="b5784-210">Si es desarrollador de. NET, puede crear topologías de C# o C#/Java híbridas con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b5784-210">If you are a .NET developer, you can create C# or hybrid C#/Java topologies using Visual Studio.</span></span> <span data-ttu-id="b5784-211">Para más información, consulte [Desarrollo de topologías de C# para Apache Storm en HDInsight con herramientas de Hadoop para Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="b5784-211">For more information, see [Develop C# topologies for Apache Storm on HDInsight using Hadoop tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="b5784-212">Para las topologías de ejemplo que pueden utilizarse con Storm en HDInsight, vea hello en los ejemplos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b5784-212">For example topologies that can be used with Storm on HDInsight, see hello following examples:</span></span>

* [<span data-ttu-id="b5784-213">Topologías de ejemplo para Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="b5784-213">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
