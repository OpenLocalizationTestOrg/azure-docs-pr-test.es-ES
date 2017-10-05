---
title: "Kit de herramientas de Azure para IntelliJ: depuración de aplicaciones de forma remota en Spark de HDInsight | Microsoft Docs"
description: "Aprenda a usar las herramientas de HDInsight del kit de herramientas de Azure para IntelliJ para depurar de forma remota aplicaciones que se ejecutan en clústeres de HDInsight Spark mediante VPN."
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
ms.openlocfilehash: 5ce282aac94d0f22ea587cbe4005819310e23b1f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-toolkit-for-intellij-to-debug-applications-remotely-on-hdinsight-spark-through-vpn"></a><span data-ttu-id="defe1-103">Uso del kit de herramientas de Azure para IntelliJ para depurar aplicaciones de forma remota en HDInsight Spark mediante VPN</span><span class="sxs-lookup"><span data-stu-id="defe1-103">Use Azure Toolkit for IntelliJ to debug applications remotely on HDInsight Spark through VPN</span></span>

<span data-ttu-id="defe1-104">Se recomienda el modo de depuración remota de la aplicación Spark mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="defe1-104">We recommend the way of debugging spark applicaltion remotely through ssh.</span></span> <span data-ttu-id="defe1-105">Para obtener instrucciones, vea [Depuración de aplicaciones de Spark de forma remota en un clúster de HDInsight con el kit de herramientas de Azure para IntelliJ mediante SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="defe1-105">For instructions, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

<span data-ttu-id="defe1-106">En este artículo se proporcionan instrucciones paso a paso para usar las herramientas de HDInsight del kit de herramientas de Azure para IntelliJ para enviar un trabajo de Spark en un clúster de HDInsight Spark y depurarlo de forma remota desde el equipo de escritorio.</span><span class="sxs-lookup"><span data-stu-id="defe1-106">This article provides step-by-step guidance on how to use the HDInsight Tools in Azure Toolkit for IntelliJ to submit a Spark job on HDInsight Spark cluster and then debug it remotely from your desktop computer.</span></span> <span data-ttu-id="defe1-107">Para ello, debe realizar los siguientes pasos de alto nivel:</span><span class="sxs-lookup"><span data-stu-id="defe1-107">To do so, you must perform the following high-level steps:</span></span>

1. <span data-ttu-id="defe1-108">Creación de una red virtual de Azure de sitio a sitio o de punto a sitio.</span><span class="sxs-lookup"><span data-stu-id="defe1-108">Create a site-to-site or point-to-site Azure Virtual Network.</span></span> <span data-ttu-id="defe1-109">Para los pasos descritos en este documento, se da por supuesto que usa una red de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="defe1-109">The steps in this document assume that you use a site-to-site network.</span></span>
2. <span data-ttu-id="defe1-110">Creación de un clúster de Spark en HDInsight de Azure que forma parte de la red virtual de Azure de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="defe1-110">Create a Spark cluster in Azure HDInsight that is part of the site-to-site Azure Virtual Network.</span></span>
3. <span data-ttu-id="defe1-111">Comprobación de la conectividad entre el nodo principal del clúster y el escritorio.</span><span class="sxs-lookup"><span data-stu-id="defe1-111">Verify the connectivity between the cluster headnode and your desktop.</span></span>
4. <span data-ttu-id="defe1-112">Creación de una aplicación Scala en IntelliJ IDEA y configuración para la depuración remota.</span><span class="sxs-lookup"><span data-stu-id="defe1-112">Create a Scala application in IntelliJ IDEA and configure it for remote debugging.</span></span>
5. <span data-ttu-id="defe1-113">Ejecución y depuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="defe1-113">Run and debug the application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="defe1-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="defe1-114">Prerequisites</span></span>
* <span data-ttu-id="defe1-115">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="defe1-115">An Azure subscription.</span></span> <span data-ttu-id="defe1-116">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="defe1-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="defe1-117">Un clúster de Apache Spark en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="defe1-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="defe1-118">Para obtener instrucciones, vea [Creación de clústeres Apache Spark en HDInsight de Azure](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="defe1-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="defe1-119">Kit de desarrollo de Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="defe1-119">Oracle Java Development kit.</span></span> <span data-ttu-id="defe1-120">Puede instalarlo desde [aquí](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="defe1-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="defe1-121">IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="defe1-121">IntelliJ IDEA.</span></span> <span data-ttu-id="defe1-122">En este artículo se usa la versión 2017.1.</span><span class="sxs-lookup"><span data-stu-id="defe1-122">This article uses version 2017.1.</span></span> <span data-ttu-id="defe1-123">Puede instalarlo desde [aquí](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="defe1-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>
* <span data-ttu-id="defe1-124">Herramientas de HDInsight del kit de herramientas de Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="defe1-124">HDInsight Tools in Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="defe1-125">Las herramientas de HDInsight para IntelliJ están disponibles como parte del kit de herramientas de Azure para IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="defe1-125">HDInsight tools for IntelliJ are available as part of the Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="defe1-126">Para obtener instrucciones sobre cómo instalar el kit de herramientas de Azure, consulte [Instalación del kit de herramientas de Azure para IntelliJ](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="defe1-126">For instructions on how to install the Azure Toolkit, see [Installing the Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>
* <span data-ttu-id="defe1-127">Inicie sesión en la suscripción de Azure desde IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="defe1-127">Log into your Azure Subscription from IntelliJ IDEA.</span></span> <span data-ttu-id="defe1-128">Siga las instrucciones que se describen [aquí](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="defe1-128">Follow the instructions [here](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
* <span data-ttu-id="defe1-129">Mientras se ejecuta la aplicación Scala Spark para la depuración remota en un equipo Windows, puede obtener una excepción, como se explica en [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) , que se produce por la ausencia del archivo WinUtils.exe en Windows.</span><span class="sxs-lookup"><span data-stu-id="defe1-129">While running Spark Scala application for remote debugging on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356) that occurs due to a missing WinUtils.exe on Windows.</span></span> <span data-ttu-id="defe1-130">Para solucionar este error, debe [descargar el archivo ejecutable desde aquí](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) y guardarlo en una ubicación como **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="defe1-130">To work around this error, you must [download the executable from here](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="defe1-131">Después, debe agregar una variable de entorno **HADOOP_HOME** y establecer el valor de la variable en **C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="defe1-131">You must then add an environment variable **HADOOP_HOME** and set the value of the variable to **C\WinUtils**.</span></span>

## <a name="step-1-create-an-azure-virtual-network"></a><span data-ttu-id="defe1-132">Paso 1: Creación de una red virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="defe1-132">Step 1: Create an Azure Virtual Network</span></span>
<span data-ttu-id="defe1-133">Siga las instrucciones de los vínculos a continuación para crear una red virtual de Azure y comprobar la conectividad entre ella y el escritorio.</span><span class="sxs-lookup"><span data-stu-id="defe1-133">Follow the instructions from the below links to create an Azure Virtual Network and then verify the connectivity between the desktop and Azure Virtual Network.</span></span>

* [<span data-ttu-id="defe1-134">Creación de una red virtual con una conexión VPN de sitio a sitio mediante el Portal de Azure y Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="defe1-134">Create a VNet with a site-to-site VPN connection using Azure Portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [<span data-ttu-id="defe1-135">Creación de una red virtual con una conexión VPN de sitio a sitio mediante Azure Resource Manager y PowerShell</span><span class="sxs-lookup"><span data-stu-id="defe1-135">Create a VNet with a site-to-site VPN connection using PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [<span data-ttu-id="defe1-136">Configuración de una conexión punto a sitio a una red virtual mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="defe1-136">Configure a point-to-site connection to a virtual network using PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a><span data-ttu-id="defe1-137">Paso 2: Creación de un clúster de Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="defe1-137">Step 2: Create an HDInsight Spark cluster</span></span>
<span data-ttu-id="defe1-138">También debe crear un clúster de Apache Spark en HDInsight de Azure que forme parte de la red virtual de Azure que ha creado.</span><span class="sxs-lookup"><span data-stu-id="defe1-138">You should also create an Apache Spark cluster on Azure HDInsight that is part of the Azure Virtual Network that you created.</span></span> <span data-ttu-id="defe1-139">Use la información disponible en [Creación de clústeres de Hadoop basados en Linux en HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="defe1-139">Use the information available at [Create Linux-based clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="defe1-140">Como parte de la configuración opcional, seleccione la red virtual de Azure que creó en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="defe1-140">As part of optional configuration, select the Azure Virtual Network that you created in the previous step.</span></span>

## <a name="step-3-verify-the-connectivity-between-the-cluster-headnode-and-your-desktop"></a><span data-ttu-id="defe1-141">Paso 3: Comprobación de la conectividad entre el nodo principal del clúster y el escritorio</span><span class="sxs-lookup"><span data-stu-id="defe1-141">Step 3: Verify the connectivity between the cluster headnode and your desktop</span></span>
1. <span data-ttu-id="defe1-142">Obtenga la dirección IP del nodo principal.</span><span class="sxs-lookup"><span data-stu-id="defe1-142">Get the IP address of the headnode.</span></span> <span data-ttu-id="defe1-143">Abra la IU de Ambari para el clúster.</span><span class="sxs-lookup"><span data-stu-id="defe1-143">Open Ambari UI for the cluster.</span></span> <span data-ttu-id="defe1-144">En la hoja del clúster, haga clic en **Panel de inicio**.</span><span class="sxs-lookup"><span data-stu-id="defe1-144">From the cluster blade, click **Dashboard**.</span></span>

    ![Buscar dirección IP del nodo principal](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. <span data-ttu-id="defe1-146">En la IU de Ambari, en la esquina superior derecha, haga clic en **Hosts**.</span><span class="sxs-lookup"><span data-stu-id="defe1-146">From the Ambari UI, from the top-right corner, click **Hosts**.</span></span>

    ![Buscar dirección IP del nodo principal](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. <span data-ttu-id="defe1-148">Debería ver una lista de nodos principales, nodos de trabajo y nodos de Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="defe1-148">You should see a list of headnodes, worker nodes, and zookeeper nodes.</span></span> <span data-ttu-id="defe1-149">Los nodos principales tienen el prefijo **hn***.</span><span class="sxs-lookup"><span data-stu-id="defe1-149">The headnodes have the **hn*** prefix.</span></span> <span data-ttu-id="defe1-150">Haga clic en el primer nodo principal.</span><span class="sxs-lookup"><span data-stu-id="defe1-150">Click the first headnode.</span></span>

    ![Buscar dirección IP del nodo principal](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. <span data-ttu-id="defe1-152">En la parte inferior de la página que se abre, en el cuadro **Summary** (Resumen), copie la dirección IP del nodo principal y el nombre de host.</span><span class="sxs-lookup"><span data-stu-id="defe1-152">At the bottom of the page that opens, from the **Summary** box, copy the IP address of the headnode and the host name.</span></span>

    ![Buscar dirección IP del nodo principal](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. <span data-ttu-id="defe1-154">Incluya la dirección IP y el nombre de host del nodo principal en el archivo de **hosts** en el equipo desde el que desee ejecutar y depurar de forma remota los trabajos de Spark.</span><span class="sxs-lookup"><span data-stu-id="defe1-154">Include the IP address and the host name of the headnode to the **hosts** file on the computer from where you want to run and remotely debug the Spark jobs.</span></span> <span data-ttu-id="defe1-155">Esto le permitirá comunicarse con el nodo principal mediante la dirección IP, así como el nombre de host.</span><span class="sxs-lookup"><span data-stu-id="defe1-155">This will enable you to communicate with the headnode using the IP address as well as the hostname.</span></span>

   1. <span data-ttu-id="defe1-156">Abra el Bloc de notas con permisos elevados.</span><span class="sxs-lookup"><span data-stu-id="defe1-156">Open a notepad with elevated permissions.</span></span> <span data-ttu-id="defe1-157">En el menú Archivo, haga clic en **Abrir** y vaya a la ubicación del archivo de hosts.</span><span class="sxs-lookup"><span data-stu-id="defe1-157">From the file menu, click **Open** and then navigate to the location of the hosts file.</span></span> <span data-ttu-id="defe1-158">En un equipo Windows, es `C:\Windows\System32\Drivers\etc\hosts`.</span><span class="sxs-lookup"><span data-stu-id="defe1-158">On a Windows computer, it is `C:\Windows\System32\Drivers\etc\hosts`.</span></span>
   2. <span data-ttu-id="defe1-159">Agregue lo siguiente al archivo de **hosts** .</span><span class="sxs-lookup"><span data-stu-id="defe1-159">Add the following to the **hosts** file.</span></span>

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. <span data-ttu-id="defe1-160">En el equipo conectado a la red virtual de Azure que el clúster de HDInsight usa, compruebe que pueda hacer ping a ambos nodos principales mediante la dirección IP, así como el nombre de host.</span><span class="sxs-lookup"><span data-stu-id="defe1-160">From the computer that you connected to the Azure Virtual Network that is used by the HDInsight cluster, verify that you can ping both the headnodes using the IP address as well as the hostname.</span></span>
7. <span data-ttu-id="defe1-161">Conéctese mediante SSH con el nodo principal del clúster según las instrucciones en [Conexión a un clúster de HDInsight basado en Linux](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="defe1-161">SSH into the cluster headnode using the instructions at [Connect to an HDInsight cluster using SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="defe1-162">En el nodo principal del clúster, haga ping a la dirección IP del equipo de escritorio.</span><span class="sxs-lookup"><span data-stu-id="defe1-162">From the cluster headnode, ping the IP address of the desktop computer.</span></span> <span data-ttu-id="defe1-163">Debe probar la conectividad a ambas direcciones IP asignadas al equipo, una para la conexión de red y otro para la red virtual de Azure a la que está conectado el equipo.</span><span class="sxs-lookup"><span data-stu-id="defe1-163">You should test connectivity to both the IP addresses assigned to the computer, one for the network connection and the other for the Azure Virtual Network that the computer is connected to.</span></span>
8. <span data-ttu-id="defe1-164">Repita los pasos también para el otro nodo principal.</span><span class="sxs-lookup"><span data-stu-id="defe1-164">Repeat the steps for the other headnode as well.</span></span>

## <a name="step-4-create-a-spark-scala-application-using-the-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a><span data-ttu-id="defe1-165">Paso 4: Creación de una aplicación Scala Spark mediante las herramientas de HDInsight del kit de herramientas de Azure para IntelliJ y configuración para la depuración remota</span><span class="sxs-lookup"><span data-stu-id="defe1-165">Step 4: Create a Spark Scala application using the HDInsight Tools in Azure Toolkit for IntelliJ and configure it for remote debugging</span></span>
1. <span data-ttu-id="defe1-166">Inicie IntelliJ IDEA y cree un nuevo proyecto.</span><span class="sxs-lookup"><span data-stu-id="defe1-166">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="defe1-167">En el cuadro de diálogo del nuevo proyecto, realice las siguientes selecciones y después haga clic en **Next**(Siguiente).</span><span class="sxs-lookup"><span data-stu-id="defe1-167">In the new project dialog box, make the following choices, and then click **Next**.</span></span>

    ![Crear aplicación Spark en Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * <span data-ttu-id="defe1-169">En el panel izquierdo, seleccione **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="defe1-169">From the left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="defe1-170">En el panel derecho, seleccione **Spark on HDInsight (Scala)**(Spark en HDInsight [Scala]).</span><span class="sxs-lookup"><span data-stu-id="defe1-170">From the right pane, select **Spark on HDInsight (Scala)**.</span></span>
   * <span data-ttu-id="defe1-171">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="defe1-171">Click **Next**.</span></span>
2. <span data-ttu-id="defe1-172">En la ventana siguiente, proporcione los detalles de proyecto siguientes y, a continuación, haga clic en **Finish** (Finalizar).</span><span class="sxs-lookup"><span data-stu-id="defe1-172">In the next window, provide the following project details, and then click **Finish**.</span></span>  
   - <span data-ttu-id="defe1-173">Proporcione un nombre de proyecto y la ubicación del proyecto.</span><span class="sxs-lookup"><span data-stu-id="defe1-173">Provide a project name and project location.</span></span>
   - <span data-ttu-id="defe1-174">En **Project SDK** (SDK de proyecto), use Java 1.8 para el clúster Spark 2.x o Java 1.7 para el clúster Spark 1.x.</span><span class="sxs-lookup"><span data-stu-id="defe1-174">For **Project SDK**, Use Java 1.8 for spark 2.x cluster, Java 1.7 for spark 1.x cluster.</span></span>
   - <span data-ttu-id="defe1-175">En **Spark Version** (Versión de Spark), el Asistente para crear un proyecto de Scala integra la versión correcta del SDK de Spark y el SDK de Scala.</span><span class="sxs-lookup"><span data-stu-id="defe1-175">For **Spark Version**, Scala project creation wizard integrates proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="defe1-176">Si la versión del clúster de Spark es inferior a la 2.0, elija Spark 1.x.</span><span class="sxs-lookup"><span data-stu-id="defe1-176">If the spark cluster version is lower 2.0, choose spark 1.x.</span></span> <span data-ttu-id="defe1-177">En caso contrario, debe seleccionar spark2.x.</span><span class="sxs-lookup"><span data-stu-id="defe1-177">Otherwise, you should select spark2.x.</span></span> <span data-ttu-id="defe1-178">Este ejemplo utiliza Spark2.0.2 (Scala 2.11.8).</span><span class="sxs-lookup"><span data-stu-id="defe1-178">This example uses Spark2.0.2(Scala 2.11.8).</span></span>
       <span data-ttu-id="defe1-179">![Creación de una aplicación Spark en Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span><span class="sxs-lookup"><span data-stu-id="defe1-179">![Create Spark Scala application](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)</span></span>
  
3. <span data-ttu-id="defe1-180">El proyecto Spark creará automáticamente un artefacto.</span><span class="sxs-lookup"><span data-stu-id="defe1-180">The Spark project will automatically create an artifact for you.</span></span> <span data-ttu-id="defe1-181">Para ver el artefacto, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="defe1-181">To see the artifact, follow these steps.</span></span>

   1. <span data-ttu-id="defe1-182">En el menú **File** (Archivo), haga clic en **Project Structure** (Estructura del proyecto).</span><span class="sxs-lookup"><span data-stu-id="defe1-182">From the **File** menu, click **Project Structure**.</span></span>
   2. <span data-ttu-id="defe1-183">En el cuadro de diálogo **Project Structure** (Estructura del proyecto), haga clic en **Artifacts** (Artefactos) para ver el artefacto predeterminado que se crea.</span><span class="sxs-lookup"><span data-stu-id="defe1-183">In the **Project Structure** dialog box, click **Artifacts** to see the default artifact that is created.</span></span>
   <span data-ttu-id="defe1-184">![Crear un JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span><span class="sxs-lookup"><span data-stu-id="defe1-184">![Create JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)</span></span>

      <span data-ttu-id="defe1-185">También puede crear su propio artefacto haciendo clic en el icono **+** (resaltado en la imagen anterior).</span><span class="sxs-lookup"><span data-stu-id="defe1-185">You can also create your own artifact bly clicking on the **+** icon, highlighted in the image above.</span></span>

4. <span data-ttu-id="defe1-186">Agregue bibliotecas al proyecto.</span><span class="sxs-lookup"><span data-stu-id="defe1-186">Add libraries to your project.</span></span> <span data-ttu-id="defe1-187">Para agregar una biblioteca, haga clic con el botón derecho en el nombre del proyecto en el árbol y después haga clic en **Open Module Settings**(Abrir configuración de módulo).</span><span class="sxs-lookup"><span data-stu-id="defe1-187">To add a library, right-click the project name in the project tree, and then click **Open Module Settings**.</span></span> <span data-ttu-id="defe1-188">En el cuadro de diálogo **Project Structure** (Estructura del proyecto) del panel izquierdo, haga clic en **Libraries** (Bibliotecas), en el símbolo (+) y en **From Maven** (Desde Maven).</span><span class="sxs-lookup"><span data-stu-id="defe1-188">In the **Project Structure** dialog box, from the left pane, click **Libraries**, click the (+) symbol, and then click **From Maven**.</span></span>

    ![Agregar biblioteca](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    <span data-ttu-id="defe1-190">En el cuadro de diálogo **Download Library from Maven Repository** (Descargar biblioteca desde repositorio de Maven), busque y agregue las siguientes bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="defe1-190">In the **Download Library from Maven Repository** dialog box, search and add the following libraries.</span></span>

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. <span data-ttu-id="defe1-191">Copie `yarn-site.xml` y `core-site.xml` del nodo principal del clúster y agréguelos al proyecto.</span><span class="sxs-lookup"><span data-stu-id="defe1-191">Copy `yarn-site.xml` and `core-site.xml` from the cluster headnode and add it to the project.</span></span> <span data-ttu-id="defe1-192">Use los comandos siguientes para copiar los archivos.</span><span class="sxs-lookup"><span data-stu-id="defe1-192">Use the following commands to copy the files.</span></span> <span data-ttu-id="defe1-193">Puede usar [Cygwin](https://cygwin.com/install.html) para ejecutar los siguientes comandos `scp` y copiar los archivos desde los nodos principales del clúster.</span><span class="sxs-lookup"><span data-stu-id="defe1-193">You can use [Cygwin](https://cygwin.com/install.html) to run the following `scp` commands to copy the files from the cluster headnodes.</span></span>

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    <span data-ttu-id="defe1-194">Como ya se han agregado la dirección IP y los nombres de host del nodo principal del clúster al archivo de hosts del escritorio, se pueden usar los comandos **scp** de la siguiente manera.</span><span class="sxs-lookup"><span data-stu-id="defe1-194">Because we already added the cluster headnode IP address and hostnames fo the hosts file on the desktop, we can use the **scp** commands in the following manner.</span></span>

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    <span data-ttu-id="defe1-195">Para agregar estos archivos a su proyecto, cópielos en la carpeta **/src** del árbol; por ejemplo, `<your project directory>\src`.</span><span class="sxs-lookup"><span data-stu-id="defe1-195">Add these files to your project by copying them under the **/src** folder in your project tree, for example `<your project directory>\src`.</span></span>
6. <span data-ttu-id="defe1-196">Actualice `core-site.xml` con los siguientes cambios.</span><span class="sxs-lookup"><span data-stu-id="defe1-196">Update the `core-site.xml` to make the following changes.</span></span>

   1. <span data-ttu-id="defe1-197">`core-site.xml` incluye la clave cifrada para la cuenta de almacenamiento asociada con el clúster.</span><span class="sxs-lookup"><span data-stu-id="defe1-197">`core-site.xml` includes the encrypted key to the storage account associated with the cluster.</span></span> <span data-ttu-id="defe1-198">En el archivo `core-site.xml` que agregó al proyecto, reemplace la clave cifrada por la clave de almacenamiento real asociada a la cuenta de almacenamiento predeterminada.</span><span class="sxs-lookup"><span data-stu-id="defe1-198">In the `core-site.xml` that you added to the project, replace the encrypted key with the actual storage key associated with the default storage account.</span></span> <span data-ttu-id="defe1-199">Consulte [Administración de la cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="defe1-199">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. <span data-ttu-id="defe1-200">Quite las siguientes entradas del archivo `core-site.xml`.</span><span class="sxs-lookup"><span data-stu-id="defe1-200">Remove the following entries from the `core-site.xml`.</span></span>

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
   3. <span data-ttu-id="defe1-201">Guarde el archivo .</span><span class="sxs-lookup"><span data-stu-id="defe1-201">Save the file.</span></span>
7. <span data-ttu-id="defe1-202">Agregue la clase Main para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="defe1-202">Add the Main class for your application.</span></span> <span data-ttu-id="defe1-203">En **Project Explorer** (Explorador de proyectos), haga clic con el botón derecho en **src**, elija **New** (Nueva) y haga clic en **Scala class** (Clase de Scala).</span><span class="sxs-lookup"><span data-stu-id="defe1-203">From the **Project Explorer**, right-click **src**, point to **New**, and then click **Scala class**.</span></span>

    ![Agregar código fuente](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. <span data-ttu-id="defe1-205">En el cuadro de diálogo **Create New Scala Class** (Crear nueva clase de Scala), proporcione un nombre, seleccione **Object** (Objeto) en **Kind** (Variante) y haga clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="defe1-205">In the **Create New Scala Class** dialog box, provide a name, for **Kind** select **Object**, and then click **OK**.</span></span>

    ![Agregar código fuente](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. <span data-ttu-id="defe1-207">En el archivo `MyClusterAppMain.scala` , pegue el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="defe1-207">In the `MyClusterAppMain.scala` file, paste the following code.</span></span> <span data-ttu-id="defe1-208">Con este código se crea el contexto de Spark y se inicia un método `executeJob` desde el objeto `SparkSample`.</span><span class="sxs-lookup"><span data-stu-id="defe1-208">This code creates the Spark context and launches an `executeJob` method from the `SparkSample` object.</span></span>

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

10. <span data-ttu-id="defe1-209">Repita los pasos 8 y 9 anteriores para agregar un nuevo objeto de Scala llamado `SparkSample`.</span><span class="sxs-lookup"><span data-stu-id="defe1-209">Repeat steps 8 and 9 above to add a new Scala object called `SparkSample`.</span></span> <span data-ttu-id="defe1-210">Agregue el siguiente código a esta clase.</span><span class="sxs-lookup"><span data-stu-id="defe1-210">To this class add the following code.</span></span> <span data-ttu-id="defe1-211">Este código lee los datos de HVAC.csv (disponible en todos los clústeres de Spark de HDInsight), recupera las filas que solo tienen un dígito en la séptima columna del CSV y escribe el resultado en **/HVACOut** bajo el contenedor de almacenamiento predeterminado para el clúster.</span><span class="sxs-lookup"><span data-stu-id="defe1-211">This code reads the data from the HVAC.csv (available on all HDInsight Spark clusters), retrieves the rows that only have one digit in the seventh column in the CSV, and writes the output to **/HVACOut** under the default storage container for the cluster.</span></span>

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find the rows which have only one digit in the 7th column in the CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. <span data-ttu-id="defe1-212">Repita los pasos 8 y 9 anteriores para agregar una nueva clase llamada `RemoteClusterDebugging`.</span><span class="sxs-lookup"><span data-stu-id="defe1-212">Repeat steps 8 and 9 above to add a new class called `RemoteClusterDebugging`.</span></span> <span data-ttu-id="defe1-213">Esta clase implementa el marco de pruebas de Spark que se usa para depurar aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="defe1-213">This class implements the Spark test framework that is used for debugging applications.</span></span> <span data-ttu-id="defe1-214">Agregue el siguiente código a la clase `RemoteClusterDebugging` .</span><span class="sxs-lookup"><span data-stu-id="defe1-214">Add the following code to the `RemoteClusterDebugging` class.</span></span>

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

     <span data-ttu-id="defe1-215">Hay un par de cosas importantes que se deben tener en cuenta aquí:</span><span class="sxs-lookup"><span data-stu-id="defe1-215">Couple of important things to note here:</span></span>

   * <span data-ttu-id="defe1-216">Para `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, asegúrese de que el archivo JAR del ensamblado Spark está disponible en el almacenamiento de clúster de la ruta especificada.</span><span class="sxs-lookup"><span data-stu-id="defe1-216">For `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, make sure the Spark assembly JAR is available on the cluster storage at the specified path.</span></span>
   * <span data-ttu-id="defe1-217">Para `setJars`, especifique la ubicación donde se creará el archivo JAR de artefacto.</span><span class="sxs-lookup"><span data-stu-id="defe1-217">For `setJars`, specify the location where the artifact jar will be created.</span></span> <span data-ttu-id="defe1-218">Normalmente es `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span><span class="sxs-lookup"><span data-stu-id="defe1-218">Typically it is `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.</span></span>
12. <span data-ttu-id="defe1-219">En la clase `RemoteClusterDebugging`, haga clic con el botón derecho en la palabra clave `test` y seleccione **Create RemoteClusterDebugging Configuration** (Crear configuración de RemoteClusterDebugging).</span><span class="sxs-lookup"><span data-stu-id="defe1-219">In the `RemoteClusterDebugging` class, right-click the `test` keyword and select **Create RemoteClusterDebugging Configuration**.</span></span>

    ![Crear configuración remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. <span data-ttu-id="defe1-221">En el cuadro de diálogo, especifique un nombre para la configuración y seleccione **Test name** (Nombre de prueba) para **Test kind** (Tipo de prueba).</span><span class="sxs-lookup"><span data-stu-id="defe1-221">In the dialog box, provide a name for the configuration, and select the **Test kind** as **Test name**.</span></span> <span data-ttu-id="defe1-222">Deje los demás valores predeterminados y haga clic en **Apply** (Aplicar) y en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="defe1-222">Leave all other values as default, click **Apply**, and then click **OK**.</span></span>

    ![Crear configuración remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. <span data-ttu-id="defe1-224">Ahora se debería ver un menú desplegable de configuración **Remote Run** (Ejecución remota) en la barra de menús.</span><span class="sxs-lookup"><span data-stu-id="defe1-224">You should now see a **Remote Run** configuration drop-down in the menu bar.</span></span>

    ![Crear configuración remota](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-the-application-in-debug-mode"></a><span data-ttu-id="defe1-226">Paso 5: Ejecución de la aplicación en modo de depuración</span><span class="sxs-lookup"><span data-stu-id="defe1-226">Step 5: Run the application in debug mode</span></span>
1. <span data-ttu-id="defe1-227">En el proyecto de IntelliJ IDEA, abra `SparkSample.scala` y cree un punto de interrupción junto a "val rdd1".</span><span class="sxs-lookup"><span data-stu-id="defe1-227">In your IntelliJ IDEA project, open `SparkSample.scala` and create a breakpoint next to \`val rdd1'.</span></span> <span data-ttu-id="defe1-228">En el menú emergente para crear un punto de interrupción, seleccione **line in function executeJob**(línea en función executeJob).</span><span class="sxs-lookup"><span data-stu-id="defe1-228">In the pop-up menu for creating a breakpoint, select **line in function executeJob**.</span></span>

    ![Agregar un punto de interrupción](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. <span data-ttu-id="defe1-230">Haga clic en el botón **Debug Run** (Depurar ejecución) situado junto al menú desplegable de configuración **Remote Run** (Ejecución remota) para comenzar a ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="defe1-230">Click the **Debug Run** button next to the **Remote Run** configuration drop-down to start running the application.</span></span>

    ![Ejecutar el programa en modo de depuración](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. <span data-ttu-id="defe1-232">Cuando la ejecución del programa alcance el punto de interrupción, debería ver una pestaña **Debugger** (Depurador) en el panel inferior.</span><span class="sxs-lookup"><span data-stu-id="defe1-232">When the program execution reaches the breakpoint, you should see a **Debugger** tab in the bottom pane.</span></span>

    ![Ejecutar el programa en modo de depuración](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. <span data-ttu-id="defe1-234">Haga clic en el icono (**+**) para agregar una inspección como se muestra en la siguiente imagen.</span><span class="sxs-lookup"><span data-stu-id="defe1-234">Click the (**+**) icon to add a watch as shown in the image below.</span></span>

    ![Ejecutar el programa en modo de depuración](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    <span data-ttu-id="defe1-236">Aquí, como la aplicación se interrumpió antes de que se creara la variable `rdd1`, con esta inspección se ve cuáles son las cinco primeras filas de la variable `rdd`.</span><span class="sxs-lookup"><span data-stu-id="defe1-236">Here, because the application broke before the variable `rdd1` was created, using this watch we can see what are the first 5 rows in the variable `rdd`.</span></span> <span data-ttu-id="defe1-237">Presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="defe1-237">Press **ENTER**.</span></span>

    ![Ejecutar el programa en modo de depuración](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    <span data-ttu-id="defe1-239">Lo que se ve en la imagen anterior es que, en tiempo de ejecución, se pueden consultar terabytes de datos y depurar la ejecución de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="defe1-239">What you see in the image above is that at runtime, you could query terrabytes of data and debug how your application progresses.</span></span> <span data-ttu-id="defe1-240">Por ejemplo, en el resultado que se muestra en la imagen anterior, se ve que la primera fila es un encabezado.</span><span class="sxs-lookup"><span data-stu-id="defe1-240">For example, in the output shown in the image above, you can see that the first row of the output is a header.</span></span> <span data-ttu-id="defe1-241">Según esto, puede modificar el código de la aplicación para omitir la fila de encabezado si es necesario.</span><span class="sxs-lookup"><span data-stu-id="defe1-241">Based on this, you can modify your application code to skip the header row if required.</span></span>
5. <span data-ttu-id="defe1-242">Ahora puede hacer clic en el icono **Resume Program** (Reanudar programa) para continuar con la ejecución de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="defe1-242">You can now click the **Resume Program** icon to proceed with your application run.</span></span>

    ![Ejecutar el programa en modo de depuración](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. <span data-ttu-id="defe1-244">Si la aplicación se completa correctamente, debería ver resultados parecidos a los siguientes.</span><span class="sxs-lookup"><span data-stu-id="defe1-244">If the application completes successfully, you should see an output like the following.</span></span>

    ![Ejecutar el programa en modo de depuración](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <span data-ttu-id="defe1-246"><a name="seealso"></a>Otras referencias</span><span class="sxs-lookup"><span data-stu-id="defe1-246"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="defe1-247">Introducción a Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="defe1-247">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="defe1-248">Demostración</span><span class="sxs-lookup"><span data-stu-id="defe1-248">Demo</span></span>
* <span data-ttu-id="defe1-249">Creación del proyecto Scala (vídeo): [Creación de aplicaciones Scala de Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) (en inglés)</span><span class="sxs-lookup"><span data-stu-id="defe1-249">Create Scala Project (Video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="defe1-250">Depuración remota (vídeo): [Uso del kit de herramientas de Azure para IntelliJ para depurar de forma remota aplicaciones Spark en clústeres de HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) (en inglés)</span><span class="sxs-lookup"><span data-stu-id="defe1-250">Remote Debug (Video): [Use Azure Toolkit for IntelliJ to debug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="defe1-251">Escenarios</span><span class="sxs-lookup"><span data-stu-id="defe1-251">Scenarios</span></span>
* [<span data-ttu-id="defe1-252">Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI</span><span class="sxs-lookup"><span data-stu-id="defe1-252">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="defe1-253">Creación de aplicaciones de Aprendizaje automático con Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="defe1-253">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="defe1-254">Spark con aprendizaje automático: uso de Spark en HDInsight para predecir los resultados de la inspección de alimentos</span><span class="sxs-lookup"><span data-stu-id="defe1-254">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="defe1-255">Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real</span><span class="sxs-lookup"><span data-stu-id="defe1-255">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="defe1-256">Análisis del registro del sitio web con Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="defe1-256">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="defe1-257">Creación y ejecución de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="defe1-257">Create and run applications</span></span>
* [<span data-ttu-id="defe1-258">Crear una aplicación independiente con Scala</span><span class="sxs-lookup"><span data-stu-id="defe1-258">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="defe1-259">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="defe1-259">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="defe1-260">Herramientas y extensiones</span><span class="sxs-lookup"><span data-stu-id="defe1-260">Tools and extensions</span></span>
* [<span data-ttu-id="defe1-261">Uso de las herramientas de HDInsight del kit de herramientas de Azure para IntelliJ con el fin de crear y enviar aplicaciones Spark en Scala</span><span class="sxs-lookup"><span data-stu-id="defe1-261">Use HDInsight Tools in Azure Toolkit for IntelliJ to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="defe1-262">Uso del kit de herramientas de Azure para IntelliJ para depurar de forma remota aplicaciones Spark mediante SSH</span><span class="sxs-lookup"><span data-stu-id="defe1-262">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="defe1-263">Uso de las herramientas de HDInsight para IntelliJ con Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="defe1-263">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="defe1-264">Uso de las herramientas de HDInsight del kit de herramientas de Azure para Eclipse con el fin de crear aplicaciones Spark</span><span class="sxs-lookup"><span data-stu-id="defe1-264">Use HDInsight Tools in Azure Toolkit for Eclipse to create Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="defe1-265">Uso de cuadernos de Zeppelin con un clúster Spark en HDInsight</span><span class="sxs-lookup"><span data-stu-id="defe1-265">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="defe1-266">Kernels disponibles para el cuaderno de Jupyter en el clúster Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="defe1-266">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="defe1-267">Uso de paquetes externos con cuadernos de Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="defe1-267">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="defe1-268">Instalación de un cuaderno de Jupyter Notebook en el equipo y conexión al clúster de Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="defe1-268">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="defe1-269">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="defe1-269">Manage resources</span></span>
* [<span data-ttu-id="defe1-270">Administración de recursos para el clúster Apache Spark en HDInsight de Azure</span><span class="sxs-lookup"><span data-stu-id="defe1-270">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="defe1-271">Track and debug jobs running on an Apache Spark cluster in HDInsight (Seguimiento y depuración de trabajos que se ejecutan en un clúster de Apache Spark en HDInsight)</span><span class="sxs-lookup"><span data-stu-id="defe1-271">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
