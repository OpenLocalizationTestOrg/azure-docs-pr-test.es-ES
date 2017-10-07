---
title: "Kit de herramientas para IntelliJ - aplicaciones de depuración remota en HDInsight Spark aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo usar herramientas de HDInsight en el Kit de herramientas de Azure para aplicaciones de depuración de tooremotely IntelliJ ejecutan en clústeres de HDInsight Spark a través de vpn."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 55fb454f-c7dc-46de-a978-e242e9a94f4c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ad67d23bf609d0a7afb38b2acb110062f8b27b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toodebug-applications-remotely-on-hdinsight-spark-through-vpn"></a><span data-ttu-id="9b030-103">Usar el Kit de herramientas de Azure IntelliJ toodebug para aplicaciones de forma remota en HDInsight Spark a través de VPN</span><span class="sxs-lookup"><span data-stu-id="9b030-103">Use Azure Toolkit for IntelliJ toodebug applications remotely on HDInsight Spark through VPN</span></span>

<span data-ttu-id="9b030-104">Se recomienda manera Hola de depurar remotamente a través de spark applicaltion ssh.</span><span class="sxs-lookup"><span data-stu-id="9b030-104">We recommend hello way of debugging spark applicaltion remotely through ssh.</span></span> <span data-ttu-id="9b030-105">Para obtener instrucciones, vea [Depuración de aplicaciones de Spark de forma remota en un clúster de HDInsight con el kit de herramientas de Azure para IntelliJ mediante SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="9b030-105">For instructions, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

<span data-ttu-id="9b030-106">Este artículo proporciona instrucciones paso a paso acerca de cómo toouse Hola herramientas de HDInsight en el Kit de herramientas de Azure para IntelliJ toosubmit un trabajo de Spark en HDInsight Spark clúster y, a continuación, depurarlo de forma remota desde el equipo de escritorio.</span><span class="sxs-lookup"><span data-stu-id="9b030-106">This article provides step-by-step guidance on how toouse hello HDInsight Tools in Azure Toolkit for IntelliJ toosubmit a Spark job on HDInsight Spark cluster and then debug it remotely from your desktop computer.</span></span> <span data-ttu-id="9b030-107">toodo por lo tanto, debe realizar Hola siguiendo los pasos de alto nivel:</span><span class="sxs-lookup"><span data-stu-id="9b030-107">toodo so, you must perform hello following high-level steps:</span></span>

1. <span data-ttu-id="9b030-108">Creación de una red virtual de Azure de sitio a sitio o de punto a sitio.</span><span class="sxs-lookup"><span data-stu-id="9b030-108">Create a site-to-site or point-to-site Azure Virtual Network.</span></span> <span data-ttu-id="9b030-109">pasos de Hello en este documento se supone que usa una red de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="9b030-109">hello steps in this document assume that you use a site-to-site network.</span></span>
2. <span data-ttu-id="9b030-110">Crear un clúster de Spark en HDInsight de Azure que forma parte de hello sitio a sitio red Virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="9b030-110">Create a Spark cluster in Azure HDInsight that is part of hello site-to-site Azure Virtual Network.</span></span>
3. <span data-ttu-id="9b030-111">Compruebe la conectividad de hello entre el nodo principal del clúster de Hola y el escritorio.</span><span class="sxs-lookup"><span data-stu-id="9b030-111">Verify hello connectivity between hello cluster headnode and your desktop.</span></span>
4. <span data-ttu-id="9b030-112">Creación de una aplicación Scala en IntelliJ IDEA y configuración para la depuración remota.</span><span class="sxs-lookup"><span data-stu-id="9b030-112">Create a Scala application in IntelliJ IDEA and configure it for remote debugging.</span></span>
5. <span data-ttu-id="9b030-113">Ejecutar y depurar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="9b030-113">Run and debug hello application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b030-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9b030-114">Prerequisites</span></span>
* <span data-ttu-id="9b030-115">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="9b030-115">An Azure subscription.</span></span> <span data-ttu-id="9b030-116">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="9b030-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="9b030-117">Un clúster de Apache Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9b030-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="9b030-118">Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="9b030-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="9b030-119">Kit de desarrollo de Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="9b030-119">Oracle Java Development kit.</span></span> <span data-ttu-id="9b030-120">Puede instalarlo desde [aquí](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="9b030-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="9b030-121">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="9b030-121">IntelliJ IDEA.</span></span> <span data-ttu-id="9b030-122">En este artículo se usa la versión 2017.1.</span><span class="sxs-lookup"><span data-stu-id="9b030-122">This article uses version 2017.1.</span></span> <span data-ttu-id="9b030-123">Puede instalarlo desde [aquí](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="9b030-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>
* <span data-ttu-id="9b030-124">Herramientas de HDInsight del kit de herramientas de Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="9b030-124">HDInsight Tools in Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="9b030-125">Herramientas de HDInsight para IntelliJ están disponibles como parte del Kit de herramientas de Azure para IntelliJ Hola.</span><span class="sxs-lookup"><span data-stu-id="9b030-125">HDInsight tools for IntelliJ are available as part of hello Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="9b030-126">Para obtener instrucciones sobre cómo tooinstall Hola Kit de herramientas de Azure, consulte [instalar hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="9b030-126">For instructions on how tooinstall hello Azure Toolkit, see [Installing hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>
* <span data-ttu-id="9b030-127">Inicie sesión en la suscripción de Azure desde IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="9b030-127">Log into your Azure Subscription from IntelliJ IDEA.</span></span> <span data-ttu-id="9b030-128">Siga las instrucciones de hello [aquí](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="9b030-128">Follow hello instructions [here](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
* <span data-ttu-id="9b030-129">Mientras se ejecuta la aplicación Scala Spark para la depuración remota en un equipo Windows, podría obtener una excepción, como se explica en [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356) que se produce debido a falta de tooa WinUtils.exe en Windows.</span><span class="sxs-lookup"><span data-stu-id="9b030-129">While running Spark Scala application for remote debugging on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) that occurs due tooa missing WinUtils.exe on Windows.</span></span> <span data-ttu-id="9b030-130">toowork solucionar este error, debe [descargar ejecutable hello desde aquí](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) como ubicación de tooa **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="9b030-130">toowork around this error, you must [download hello executable from here](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="9b030-131">A continuación, debe agregar una variable de entorno **HADOOP_HOME** y establezca el valor de Hola de variable de hello demasiado**C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="9b030-131">You must then add an environment variable **HADOOP_HOME** and set hello value of hello variable too**C\WinUtils**.</span></span>

## <a name="step-1-create-an-azure-virtual-network"></a><span data-ttu-id="9b030-132">Paso 1: Creación de una red virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="9b030-132">Step 1: Create an Azure Virtual Network</span></span>
<span data-ttu-id="9b030-133">Siga las instrucciones de Hola de hello debajo de vínculos toocreate una red Virtual de Azure y, a continuación, compruebe la conectividad de hello entre escritorio hello y red Virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="9b030-133">Follow hello instructions from hello below links toocreate an Azure Virtual Network and then verify hello connectivity between hello desktop and Azure Virtual Network.</span></span>

* [<span data-ttu-id="9b030-134">Creación de una red virtual con una conexión VPN de sitio a sitio mediante el Portal de Azure y Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9b030-134">Create a VNet with a site-to-site VPN connection using Azure Portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [<span data-ttu-id="9b030-135">Creación de una red virtual con una conexión VPN de sitio a sitio mediante Azure Resource Manager y PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b030-135">Create a VNet with a site-to-site VPN connection using PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [<span data-ttu-id="9b030-136">Configurar una red virtual de sitio de punto de conexión tooa con PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b030-136">Configure a point-to-site connection tooa virtual network using PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a><span data-ttu-id="9b030-137">Paso 2: Creación de un clúster de Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b030-137">Step 2: Create an HDInsight Spark cluster</span></span>
<span data-ttu-id="9b030-138">También debe crear un clúster de Apache Spark en HDInsight de Azure que forma parte del programa Hola a red Virtual de Azure que ha creado.</span><span class="sxs-lookup"><span data-stu-id="9b030-138">You should also create an Apache Spark cluster on Azure HDInsight that is part of hello Azure Virtual Network that you created.</span></span> <span data-ttu-id="9b030-139">Use Hola información disponible en [basados en Linux crear clústeres de HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="9b030-139">Use hello information available at [Create Linux-based clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="9b030-140">Como parte de la configuración opcional, seleccione Hola red Virtual de Azure que creó en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b030-140">As part of optional configuration, select hello Azure Virtual Network that you created in hello previous step.</span></span>

## <a name="step-3-verify-hello-connectivity-between-hello-cluster-headnode-and-your-desktop"></a><span data-ttu-id="9b030-141">Paso 3: Comprobar la conectividad de hello entre el nodo principal del clúster de Hola y el escritorio</span><span class="sxs-lookup"><span data-stu-id="9b030-141">Step 3: Verify hello connectivity between hello cluster headnode and your desktop</span></span>
1. <span data-ttu-id="9b030-142">Obtener dirección IP de Hola de nodo principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b030-142">Get hello IP address of hello headnode.</span></span> <span data-ttu-id="9b030-143">Abra Ambari UI para clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="9b030-143">Open Ambari UI for hello cluster.</span></span> <span data-ttu-id="9b030-144">En la hoja de clúster de hello, haga clic en **panel**.</span><span class="sxs-lookup"><span data-stu-id="9b030-144">From hello cluster blade, click **Dashboard**.</span></span>

    ![Buscar dirección IP del nodo principal](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. <span data-ttu-id="9b030-146">En hello Ambari UI, desde la esquina superior derecha de hello, haga clic en **Hosts**.</span><span class="sxs-lookup"><span data-stu-id="9b030-146">From hello Ambari UI, from hello top-right corner, click **Hosts**.</span></span>

    ![Buscar dirección IP del nodo principal](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. <span data-ttu-id="9b030-148">Debería ver una lista de nodos principales, nodos de trabajo y nodos de Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="9b030-148">You should see a list of headnodes, worker nodes, and zookeeper nodes.</span></span> <span data-ttu-id="9b030-149">Hola headnodes tienen hello **hn*** prefijo.</span><span class="sxs-lookup"><span data-stu-id="9b030-149">hello headnodes have hello **hn*** prefix.</span></span> <span data-ttu-id="9b030-150">Haga clic en el nodo principal primera Hola.</span><span class="sxs-lookup"><span data-stu-id="9b030-150">Click hello first headnode.</span></span>

    ![Buscar dirección IP del nodo principal](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. <span data-ttu-id="9b030-152">Final de Hola de página de Hola que se abre desde hello **resumen** cuadro de dirección IP de hello copia del nodo principal de Hola y el nombre de host de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b030-152">At hello bottom of hello page that opens, from hello **Summary** box, copy hello IP address of hello headnode and hello host name.</span></span>

    ![Buscar dirección IP del nodo principal](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. <span data-ttu-id="9b030-154">Incluir dirección IP de Hola y el nombre de host de Hola de hello nodo principal toohello **hosts** archivo hello equipo desde donde desea toorun y depurar de forma remota los trabajos de Spark Hola.</span><span class="sxs-lookup"><span data-stu-id="9b030-154">Include hello IP address and hello host name of hello headnode toohello **hosts** file on hello computer from where you want toorun and remotely debug hello Spark jobs.</span></span> <span data-ttu-id="9b030-155">Esto le permitirá toocommunicate con el nodo principal de hello mediante la dirección IP de hello, así como el nombre de host de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b030-155">This will enable you toocommunicate with hello headnode using hello IP address as well as hello hostname.</span></span>

   1. <span data-ttu-id="9b030-156">Abra el Bloc de notas con permisos elevados.</span><span class="sxs-lookup"><span data-stu-id="9b030-156">Open a notepad with elevated permissions.</span></span> <span data-ttu-id="9b030-157">En el menú archivo de hello, haga clic en **abiertos** y, a continuación, navegue toohello ubicación del archivo de hosts de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b030-157">From hello file menu, click **Open** and then navigate toohello location of hello hosts file.</span></span> <span data-ttu-id="9b030-158">En un equipo Windows, es `C:\Windows\System32\Drivers\etc\hosts`.</span><span class="sxs-lookup"><span data-stu-id="9b030-158">On a Windows computer, it is `C:\Windows\System32\Drivers\etc\hosts`.</span></span>
   2. <span data-ttu-id="9b030-159">Agregar Hola después toohello **hosts** archivo.</span><span class="sxs-lookup"><span data-stu-id="9b030-159">Add hello following toohello **hosts** file.</span></span>

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. <span data-ttu-id="9b030-160">Desde equipo Hola había conectado toohello red Virtual de Azure que se usa por clúster de HDInsight de hello, compruebe que puede hacer ping en ambos headnodes Hola utilizando la dirección IP de hello, así como el nombre de host de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b030-160">From hello computer that you connected toohello Azure Virtual Network that is used by hello HDInsight cluster, verify that you can ping both hello headnodes using hello IP address as well as hello hostname.</span></span>
7. <span data-ttu-id="9b030-161">SSH en el nodo principal de clúster de hello mediante instrucciones de hello en [clúster de HDInsight de tooan conectar mediante SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="9b030-161">SSH into hello cluster headnode using hello instructions at [Connect tooan HDInsight cluster using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="9b030-162">Desde el nodo principal del clúster de hello, haga ping a dirección IP de Hola de equipo de escritorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b030-162">From hello cluster headnode, ping hello IP address of hello desktop computer.</span></span> <span data-ttu-id="9b030-163">Debe probar conectividad tooboth Hola IP direcciones asignadas toohello equipo, uno para la conexión de red de Hola y Hola otro para hello red Virtual de Azure que Hola equipo está conectado a.</span><span class="sxs-lookup"><span data-stu-id="9b030-163">You should test connectivity tooboth hello IP addresses assigned toohello computer, one for hello network connection and hello other for hello Azure Virtual Network that hello computer is connected to.</span></span>
8. <span data-ttu-id="9b030-164">Repita los pasos de Hola para hello y otro nodo principal.</span><span class="sxs-lookup"><span data-stu-id="9b030-164">Repeat hello steps for hello other headnode as well.</span></span>

## <a name="step-4-create-a-spark-scala-application-using-hello-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a><span data-ttu-id="9b030-165">Paso 4: Crear una aplicación de Spark Scala mediante herramientas de HDInsight de hello en el Kit de herramientas de Azure para IntelliJ y configurarlo para la depuración remota</span><span class="sxs-lookup"><span data-stu-id="9b030-165">Step 4: Create a Spark Scala application using hello HDInsight Tools in Azure Toolkit for IntelliJ and configure it for remote debugging</span></span>
1. <span data-ttu-id="9b030-166">Inicie IntelliJ IDEA y cree un nuevo proyecto.</span><span class="sxs-lookup"><span data-stu-id="9b030-166">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="9b030-167">En el cuadro de diálogo de proyecto nuevo hello, asegúrese de Hola siguientes opciones y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="9b030-167">In hello new project dialog box, make hello following choices, and then click **Next**.</span></span>

    ![Crear aplicación Spark en Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * <span data-ttu-id="9b030-169">En el panel izquierdo de hello, seleccione **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="9b030-169">From hello left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="9b030-170">En el panel derecho de hello, seleccione **Spark en HDInsight (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="9b030-170">From hello right pane, select **Spark on HDInsight (Scala)**.</span></span>
   * <span data-ttu-id="9b030-171">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="9b030-171">Click **Next**.</span></span>
2. <span data-ttu-id="9b030-172">En la siguiente ventana de hello, proporcionar Hola siguiendo los detalles del proyecto y, a continuación, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="9b030-172">In hello next window, provide hello following project details, and then click **Finish**.</span></span>  
   - <span data-ttu-id="9b030-173">Proporcione un nombre de proyecto y la ubicación del proyecto.</span><span class="sxs-lookup"><span data-stu-id="9b030-173">Provide a project name and project location.</span></span>
   - <span data-ttu-id="9b030-174">En **Project SDK** (SDK de proyecto), use Java 1.8 para el clúster Spark 2.x o Java 1.7 para el clúster Spark 1.x.</span><span class="sxs-lookup"><span data-stu-id="9b030-174">For **Project SDK**, Use Java 1.8 for spark 2.x cluster, Java 1.7 for spark 1.x cluster.</span></span>
   - <span data-ttu-id="9b030-175">En **Spark Version** (Versión de Spark), el Asistente para crear un proyecto de Scala integra la versión correcta del SDK de Spark y el SDK de Scala.</span><span class="sxs-lookup"><span data-stu-id="9b030-175">For **Spark Version**, Scala project creation wizard integrates proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="9b030-176">Si la versión de clúster de spark hello es 2.0 inferior, elija inspirará 1.x.</span><span class="sxs-lookup"><span data-stu-id="9b030-176">If hello spark cluster version is lower 2.0, choose spark 1.x.</span></span> <span data-ttu-id="9b030-177">En caso contrario, debe seleccionar spark2.x.</span><span class="sxs-lookup"><span data-stu-id="9b030-177">Otherwise, you should select spark2.x.</span></span> <span data-ttu-id="9b030-178">Este ejemplo utiliza Spark2.0.2 (Scala 2.11.8).</span><span class="sxs-lookup"><span data-stu-id="9b030-178">This example uses Spark2.0.2(Scala 2.11.8).</span></span>
       <span data-ttu-id="9b030-179">![Creación de una aplicación Spark en Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span><span class="sxs-lookup"><span data-stu-id="9b030-179">![Create Spark Scala application](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span></span>
  
3. <span data-ttu-id="9b030-180">proyecto de Spark Hola creará automáticamente un artefacto.</span><span class="sxs-lookup"><span data-stu-id="9b030-180">hello Spark project will automatically create an artifact for you.</span></span> <span data-ttu-id="9b030-181">artefacto de hello toosee, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="9b030-181">toosee hello artifact, follow these steps.</span></span>

   1. <span data-ttu-id="9b030-182">De hello **archivo** menú, haga clic en **estructura del proyecto**.</span><span class="sxs-lookup"><span data-stu-id="9b030-182">From hello **File** menu, click **Project Structure**.</span></span>
   2. <span data-ttu-id="9b030-183">Hola **estructura del proyecto** cuadro de diálogo, haga clic en **artefactos** artefacto de predeterminado de hello toosee que se crea.</span><span class="sxs-lookup"><span data-stu-id="9b030-183">In hello **Project Structure** dialog box, click **Artifacts** toosee hello default artifact that is created.</span></span>
   <span data-ttu-id="9b030-184">![Crear un JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span><span class="sxs-lookup"><span data-stu-id="9b030-184">![Create JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span></span>

      <span data-ttu-id="9b030-185">También puede crear su propios artefacto bly al hacer clic en hello ** + ** icono, resaltado en la imagen de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="9b030-185">You can also create your own artifact bly clicking on hello **+** icon, highlighted in hello image above.</span></span>

4. <span data-ttu-id="9b030-186">Agregar proyecto de bibliotecas tooyour.</span><span class="sxs-lookup"><span data-stu-id="9b030-186">Add libraries tooyour project.</span></span> <span data-ttu-id="9b030-187">tooadd una biblioteca, haga clic en nombre de proyecto de hello en el árbol del proyecto de hello y, a continuación, haga clic en **configuración para abrir el módulo**.</span><span class="sxs-lookup"><span data-stu-id="9b030-187">tooadd a library, right-click hello project name in hello project tree, and then click **Open Module Settings**.</span></span> <span data-ttu-id="9b030-188">Hola **estructura del proyecto** cuadro de diálogo, en el panel izquierdo de hello, haga clic en **bibliotecas**, haga clic en el símbolo de hello (+) y, a continuación, haga clic en **de Maven**.</span><span class="sxs-lookup"><span data-stu-id="9b030-188">In hello **Project Structure** dialog box, from hello left pane, click **Libraries**, click hello (+) symbol, and then click **From Maven**.</span></span>

    ![Agregar biblioteca](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    <span data-ttu-id="9b030-190">Hola **Download Library desde el repositorio de Maven** diálogo cuadro, buscar y agregar Hola siguiendo las bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="9b030-190">In hello **Download Library from Maven Repository** dialog box, search and add hello following libraries.</span></span>

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. <span data-ttu-id="9b030-191">Copia `yarn-site.xml` y `core-site.xml` de hello nodo principal del clúster y Agregar proyecto toohello.</span><span class="sxs-lookup"><span data-stu-id="9b030-191">Copy `yarn-site.xml` and `core-site.xml` from hello cluster headnode and add it toohello project.</span></span> <span data-ttu-id="9b030-192">Usar hello siguientes archivos de comandos toocopy Hola.</span><span class="sxs-lookup"><span data-stu-id="9b030-192">Use hello following commands toocopy hello files.</span></span> <span data-ttu-id="9b030-193">Puede usar [Cygwin](https://cygwin.com/install.html) siguiente de hello toorun `scp` comandos toocopy archivos de Hola de hello headnodes de clúster.</span><span class="sxs-lookup"><span data-stu-id="9b030-193">You can use [Cygwin](https://cygwin.com/install.html) toorun hello following `scp` commands toocopy hello files from hello cluster headnodes.</span></span>

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    <span data-ttu-id="9b030-194">Porque ya se han agregado Hola clúster nodo principal IP direcciones y nombres de host fo Hola archivo hosts en el escritorio de hello, podemos usar hello **scp** comandos Hola siguiente manera.</span><span class="sxs-lookup"><span data-stu-id="9b030-194">Because we already added hello cluster headnode IP address and hostnames fo hello hosts file on hello desktop, we can use hello **scp** commands in hello following manner.</span></span>

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    <span data-ttu-id="9b030-195">Agregar un proyecto tooyour de estos archivos, cópielos en hello **/src** carpeta en el árbol del proyecto, por ejemplo `<your project directory>\src`.</span><span class="sxs-lookup"><span data-stu-id="9b030-195">Add these files tooyour project by copying them under hello **/src** folder in your project tree, for example `<your project directory>\src`.</span></span>
6. <span data-ttu-id="9b030-196">Hola de actualización `core-site.xml` hello toomake después de cambios.</span><span class="sxs-lookup"><span data-stu-id="9b030-196">Update hello `core-site.xml` toomake hello following changes.</span></span>

   1. <span data-ttu-id="9b030-197">`core-site.xml`incluye las cuentas de almacenamiento de toohello clave Hola cifrado asociada con el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b030-197">`core-site.xml` includes hello encrypted key toohello storage account associated with hello cluster.</span></span> <span data-ttu-id="9b030-198">Hola `core-site.xml` que ha agregado el proyecto toohello, replace Hola clave cifrada con la clave de almacenamiento real de hello asociado a la cuenta de almacenamiento predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b030-198">In hello `core-site.xml` that you added toohello project, replace hello encrypted key with hello actual storage key associated with hello default storage account.</span></span> <span data-ttu-id="9b030-199">Consulte [Administración de la cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="9b030-199">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. <span data-ttu-id="9b030-200">Quitar Hola siguientes entradas de hello `core-site.xml`.</span><span class="sxs-lookup"><span data-stu-id="9b030-200">Remove hello following entries from hello `core-site.xml`.</span></span>

           <property>
                 <name>fs.azure.account.keyprovider.hdistoragecentral.blob.core.windows.net</name>
                 <value>org.apache.hadoop.fs.azure.ShellDecryptionKeyProvider</value>
           </property>

           <property>
                 <name>fs.azure.shellkeyprovider.script</name>
                 <value>/usr/lib/python2.7/dist-packages/hdinsight_common/decrypt.sh</value>
           </property>

           <property>
                 <name>net.topology.script.file.name</name>
                 <value>/etc/hadoop/conf/topology_script.py</value>
           </property>
   3. <span data-ttu-id="9b030-201">Guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="9b030-201">Save hello file.</span></span>
7. <span data-ttu-id="9b030-202">Agregar clase de hello principal para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9b030-202">Add hello Main class for your application.</span></span> <span data-ttu-id="9b030-203">De hello **el Explorador de proyectos**, haga clic en **src**, seleccione demasiado**New**y, a continuación, haga clic en **Scala clase**.</span><span class="sxs-lookup"><span data-stu-id="9b030-203">From hello **Project Explorer**, right-click **src**, point too**New**, and then click **Scala class**.</span></span>

    ![Agregar código fuente](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. <span data-ttu-id="9b030-205">Hola **crear nueva clase Scala** diálogo cuadro, proporcione un nombre para **tipo** seleccione **objeto**y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9b030-205">In hello **Create New Scala Class** dialog box, provide a name, for **Kind** select **Object**, and then click **OK**.</span></span>

    ![Agregar código fuente](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. <span data-ttu-id="9b030-207">Hola `MyClusterAppMain.scala` de archivo, pegue el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="9b030-207">In hello `MyClusterAppMain.scala` file, paste hello following code.</span></span> <span data-ttu-id="9b030-208">Este código crea el contexto de Spark Hola e inicia un `executeJob` método de hello `SparkSample` objeto.</span><span class="sxs-lookup"><span data-stu-id="9b030-208">This code creates hello Spark context and launches an `executeJob` method from hello `SparkSample` object.</span></span>

        import org.apache.spark.{SparkConf, SparkContext}

        object SparkSampleMain {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkSample")
                                      .set("spark.hadoop.validateOutputSpecs", "false")
            val sc = new SparkContext(conf)

            SparkSample.executeJob(sc,
                                   "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
                                   "wasb:///HVACOut")
          }
        }

10. <span data-ttu-id="9b030-209">Repita los pasos 8 y 9 anteriormente tooadd llama a un nuevo objeto Scala `SparkSample`.</span><span class="sxs-lookup"><span data-stu-id="9b030-209">Repeat steps 8 and 9 above tooadd a new Scala object called `SparkSample`.</span></span> <span data-ttu-id="9b030-210">clase toothis agregar Hola siguiente código.</span><span class="sxs-lookup"><span data-stu-id="9b030-210">toothis class add hello following code.</span></span> <span data-ttu-id="9b030-211">Este código lee los datos de Hola de hello HVAC.csv (disponible en todos los clústeres de HDInsight Spark), se recuperan las filas de Hola que sólo tienen un dígito en la columna séptimo Hola Hola CSV y escribe la salida de hello demasiado**/HVACOut** en el valor predeterminado de Hola contenedor de almacenamiento de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b030-211">This code reads hello data from hello HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that only have one digit in hello seventh column in hello CSV, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find hello rows which have only one digit in hello 7th column in hello CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. <span data-ttu-id="9b030-212">Repita los pasos 8 y 9 anteriormente tooadd una nueva clase denominada `RemoteClusterDebugging`.</span><span class="sxs-lookup"><span data-stu-id="9b030-212">Repeat steps 8 and 9 above tooadd a new class called `RemoteClusterDebugging`.</span></span> <span data-ttu-id="9b030-213">Esta clase implementa el marco de pruebas de Spark Hola que se usa para depurar aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9b030-213">This class implements hello Spark test framework that is used for debugging applications.</span></span> <span data-ttu-id="9b030-214">Agregar Hola después código toohello `RemoteClusterDebugging` clase.</span><span class="sxs-lookup"><span data-stu-id="9b030-214">Add hello following code toohello `RemoteClusterDebugging` class.</span></span>

        import org.apache.spark.{SparkConf, SparkContext}
        import org.scalatest.FunSuite

        class RemoteClusterDebugging extends FunSuite {

         test("Remote run") {
           val conf = new SparkConf().setAppName("SparkSample")
                                     .setMaster("yarn-client")
                                     .set("spark.yarn.am.extraJavaOptions", "-Dhdp.version=2.4")
                                     .set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")
                                     .setJars(Seq("""C:\workspace\IdeaProjects\MyClusterApp\out\artifacts\MyClusterApp_DefaultArtifact\default_artifact.jar"""))
                                     .set("spark.hadoop.validateOutputSpecs", "false")
           val sc = new SparkContext(conf)

           SparkSample.executeJob(sc,
             "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
             "wasb:///HVACOut")
         }
        }

     <span data-ttu-id="9b030-215">Par de cosas importantes toonote aquí:</span><span class="sxs-lookup"><span data-stu-id="9b030-215">Couple of important things toonote here:</span></span>

   * <span data-ttu-id="9b030-216">Para `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, asegúrese de que está disponible en el almacenamiento de clúster de hello en la ruta de acceso especificada de Hola Hola ensamblado Spark JAR.</span><span class="sxs-lookup"><span data-stu-id="9b030-216">For `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, make sure hello Spark assembly JAR is available on hello cluster storage at hello specified path.</span></span>
   * <span data-ttu-id="9b030-217">Para `setJars`, especificar ubicación de Hola donde se creará el archivo jar de artefacto de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b030-217">For `setJars`, specify hello location where hello artifact jar will be created.</span></span> <span data-ttu-id="9b030-218">Normalmente es `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span><span class="sxs-lookup"><span data-stu-id="9b030-218">Typically it is `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span></span>
12. <span data-ttu-id="9b030-219">Hola `RemoteClusterDebugging` de clases, haga clic en hello `test` palabra clave y seleccione **crear configuración de RemoteClusterDebugging**.</span><span class="sxs-lookup"><span data-stu-id="9b030-219">In hello `RemoteClusterDebugging` class, right-click hello `test` keyword and select **Create RemoteClusterDebugging Configuration**.</span></span>

    ![Crear configuración remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. <span data-ttu-id="9b030-221">En el cuadro de diálogo de hello, proporcione un nombre para la configuración de Hola y seleccione hello **probar tipo** como **nombre de la prueba**.</span><span class="sxs-lookup"><span data-stu-id="9b030-221">In hello dialog box, provide a name for hello configuration, and select hello **Test kind** as **Test name**.</span></span> <span data-ttu-id="9b030-222">Deje los demás valores predeterminados y haga clic en **Apply** (Aplicar) y en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="9b030-222">Leave all other values as default, click **Apply**, and then click **OK**.</span></span>

    ![Crear configuración remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. <span data-ttu-id="9b030-224">Ahora debería ver un **ejecutar remoto** configuración de lista desplegable en la barra de menús de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b030-224">You should now see a **Remote Run** configuration drop-down in hello menu bar.</span></span>

    ![Crear configuración remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-hello-application-in-debug-mode"></a><span data-ttu-id="9b030-226">Paso 5: Ejecutar la aplicación hello en modo de depuración</span><span class="sxs-lookup"><span data-stu-id="9b030-226">Step 5: Run hello application in debug mode</span></span>
1. <span data-ttu-id="9b030-227">En el proyecto IntelliJ IDEA, abra `SparkSample.scala` y crear un rdd1 de punto de interrupción siguiente too'val'.</span><span class="sxs-lookup"><span data-stu-id="9b030-227">In your IntelliJ IDEA project, open `SparkSample.scala` and create a breakpoint next too\`val rdd1'.</span></span> <span data-ttu-id="9b030-228">En el menú emergente de Hola para crear un punto de interrupción, seleccione **línea en la función executeJob**.</span><span class="sxs-lookup"><span data-stu-id="9b030-228">In hello pop-up menu for creating a breakpoint, select **line in function executeJob**.</span></span>

    ![Agregar un punto de interrupción](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. <span data-ttu-id="9b030-230">Haga clic en hello **depurar ejecutar** botón siguiente toohello **ejecutar remoto** toostart de lista desplegable de configuración ejecutando la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="9b030-230">Click hello **Debug Run** button next toohello **Remote Run** configuration drop-down toostart running hello application.</span></span>

    ![Ejecutar programa hello en modo de depuración](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. <span data-ttu-id="9b030-232">Cuando la ejecución del programa Hola alcanza el punto de interrupción de hello, debería ver un **depurador** ficha en el panel inferior de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b030-232">When hello program execution reaches hello breakpoint, you should see a **Debugger** tab in hello bottom pane.</span></span>

    ![Ejecutar programa hello en modo de depuración](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. <span data-ttu-id="9b030-234">Haga clic en hello (**+**) tooadd icono una inspección como se muestra en la imagen de hello siguiente.</span><span class="sxs-lookup"><span data-stu-id="9b030-234">Click hello (**+**) icon tooadd a watch as shown in hello image below.</span></span>

    ![Ejecutar programa hello en modo de depuración](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    <span data-ttu-id="9b030-236">Aquí, porque se interrumpió la aplicación hello antes de la variable de hello `rdd1` se creó con esta inspección podemos ver lo que se Hola primeras 5 filas en la variable de hello `rdd`.</span><span class="sxs-lookup"><span data-stu-id="9b030-236">Here, because hello application broke before hello variable `rdd1` was created, using this watch we can see what are hello first 5 rows in hello variable `rdd`.</span></span> <span data-ttu-id="9b030-237">Presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="9b030-237">Press **ENTER**.</span></span>

    ![Ejecutar programa hello en modo de depuración](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    <span data-ttu-id="9b030-239">Lo que ve en la imagen de hello anterior es que en tiempo de ejecución, puede consultar terabytes de datos y de depuración cómo progresa de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="9b030-239">What you see in hello image above is that at runtime, you could query terrabytes of data and debug how your application progresses.</span></span> <span data-ttu-id="9b030-240">Por ejemplo, en la salida de hello se muestra en la imagen de hello anterior, puede ver que Hola primera fila de salida de hello es un encabezado.</span><span class="sxs-lookup"><span data-stu-id="9b030-240">For example, in hello output shown in hello image above, you can see that hello first row of hello output is a header.</span></span> <span data-ttu-id="9b030-241">En función de esto, puede modificar la fila de encabezado de aplicación código tooskip Hola si es necesario.</span><span class="sxs-lookup"><span data-stu-id="9b030-241">Based on this, you can modify your application code tooskip hello header row if required.</span></span>
5. <span data-ttu-id="9b030-242">Ahora puede hacer clic hello **reanudar programa** tooproceed icono con la ejecución de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9b030-242">You can now click hello **Resume Program** icon tooproceed with your application run.</span></span>

    ![Ejecutar programa hello en modo de depuración](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. <span data-ttu-id="9b030-244">Si finaliza correctamente la aplicación hello, debería ver un resultado similar Hola siguiente.</span><span class="sxs-lookup"><span data-stu-id="9b030-244">If hello application completes successfully, you should see an output like hello following.</span></span>

    ![Ejecutar programa hello en modo de depuración](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <span data-ttu-id="9b030-246"><a name="seealso"></a>Otras referencias</span><span class="sxs-lookup"><span data-stu-id="9b030-246"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="9b030-247">Introducción a Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="9b030-247">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="9b030-248">Demostración</span><span class="sxs-lookup"><span data-stu-id="9b030-248">Demo</span></span>
* <span data-ttu-id="9b030-249">Creación del proyecto Scala (vídeo): [Creación de aplicaciones Scala de Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) (en inglés)</span><span class="sxs-lookup"><span data-stu-id="9b030-249">Create Scala Project (Video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="9b030-250">Depuración remota (vídeo): [Use Azure Toolkit IntelliJ toodebug Spark para aplicaciones de forma remota en clúster de HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="9b030-250">Remote Debug (Video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="9b030-251">Escenarios</span><span class="sxs-lookup"><span data-stu-id="9b030-251">Scenarios</span></span>
* [<span data-ttu-id="9b030-252">Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI</span><span class="sxs-lookup"><span data-stu-id="9b030-252">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="9b030-253">Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="9b030-253">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="9b030-254">Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos</span><span class="sxs-lookup"><span data-stu-id="9b030-254">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="9b030-255">Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real</span><span class="sxs-lookup"><span data-stu-id="9b030-255">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="9b030-256">Análisis del registro del sitio web con Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b030-256">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="9b030-257">Creación y ejecución de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="9b030-257">Create and run applications</span></span>
* [<span data-ttu-id="9b030-258">Crear una aplicación independiente con Scala</span><span class="sxs-lookup"><span data-stu-id="9b030-258">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="9b030-259">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="9b030-259">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="9b030-260">Herramientas y extensiones</span><span class="sxs-lookup"><span data-stu-id="9b030-260">Tools and extensions</span></span>
* [<span data-ttu-id="9b030-261">Usar herramientas de HDInsight en el Kit de herramientas de Azure para IntelliJ toocreate y enviar Spark Scala aplicaciones</span><span class="sxs-lookup"><span data-stu-id="9b030-261">Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="9b030-262">Usar el Kit de herramientas de Azure para aplicaciones de Spark IntelliJ toodebug forma remota a través de SSH</span><span class="sxs-lookup"><span data-stu-id="9b030-262">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="9b030-263">Uso de las herramientas de HDInsight para IntelliJ con Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="9b030-263">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="9b030-264">Usar herramientas de HDInsight en el Kit de herramientas de Azure para aplicaciones de Eclipse toocreate Spark</span><span class="sxs-lookup"><span data-stu-id="9b030-264">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="9b030-265">Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b030-265">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="9b030-266">Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b030-266">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="9b030-267">Uso de paquetes externos con cuadernos de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="9b030-267">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="9b030-268">Instale Jupyter en el equipo y conecte tooan clúster de HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="9b030-268">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="9b030-269">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="9b030-269">Manage resources</span></span>
* [<span data-ttu-id="9b030-270">Administrar los recursos de clúster de hello Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="9b030-270">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="9b030-271">Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="9b030-271">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
