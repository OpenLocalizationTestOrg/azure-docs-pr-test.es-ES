---
title: "Análisis de los datos de los sensores con Apache Storm y HBase | Microsoft Docs"
description: "Obtenga información acerca de cómo conectarse a Apache Storm con una red virtual. Utilice Storm con HBase para procesar los datos de sensores de un centro de eventos y visualizarlos con D3.js."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a9a1ac8e-5708-4833-b965-e453815e671f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/09/2017
ms.author: larryfr
ms.openlocfilehash: 0d1cc959c87bd64ed728f8b56c9b9156fa492a8b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a><span data-ttu-id="99e1e-104">Análisis de datos de sensores con Apache Storm, Centro de eventos y HBase en HDInsight (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="99e1e-104">Analyze sensor data with Apache Storm, Event Hub, and HBase in HDInsight (Hadoop)</span></span>

<span data-ttu-id="99e1e-105">Aprenda a usar Apache Storm en HDInsight para procesar datos de sensores desde Centro de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="99e1e-105">Learn how to use Apache Storm on HDInsight to process sensor data from Azure Event Hub.</span></span> <span data-ttu-id="99e1e-106">Los datos se almacenan entonces en Apache HBase en HDInsight y se visualizan mediante D3.js.</span><span class="sxs-lookup"><span data-stu-id="99e1e-106">The data is then stored into Apache HBase on HDInsight, and visualized using D3.js.</span></span>

<span data-ttu-id="99e1e-107">La plantilla de Azure Resource Manager utilizada en este documento muestra cómo crear varios recursos de Azure en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="99e1e-107">The Azure Resource Manager template used in this document demonstrates how to create multiple Azure resources in a resource group.</span></span> <span data-ttu-id="99e1e-108">Esta plantilla crea una red virtual de Azure, dos clústeres de HDInsight (Storm y HBase) y una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="99e1e-108">The template creates an Azure Virtual Network, two HDInsight clusters (Storm and HBase) and an Azure Web App.</span></span> <span data-ttu-id="99e1e-109">Se realiza automáticamente una implementación de node.js de un panel web en tiempo real en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="99e1e-109">A node.js implementation of a real-time web dashboard is automatically deployed to the web app.</span></span>

> [!NOTE]
> <span data-ttu-id="99e1e-110">La información y el ejemplo de este documento requieren la versión 3.6 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="99e1e-110">The information in this document and example in this document require HDInsight version 3.6.</span></span>
>
> <span data-ttu-id="99e1e-111">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="99e1e-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="99e1e-112">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="99e1e-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99e1e-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="99e1e-113">Prerequisites</span></span>

* <span data-ttu-id="99e1e-114">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="99e1e-114">An Azure subscription.</span></span>
* <span data-ttu-id="99e1e-115">[Node.js](http://nodejs.org/): se utiliza para obtener una vista previa del panel web en el entorno de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="99e1e-115">[Node.js](http://nodejs.org/): Used to preview the web dashboard locally on your development environment.</span></span>
* <span data-ttu-id="99e1e-116">[Java y JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): se utiliza para desarrollar la topología de Storm.</span><span class="sxs-lookup"><span data-stu-id="99e1e-116">[Java and the JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): Used to develop the Storm topology.</span></span>
* <span data-ttu-id="99e1e-117">[Maven](http://maven.apache.org/what-is-maven.html): se usa para crear y compilar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="99e1e-117">[Maven](http://maven.apache.org/what-is-maven.html): Used to build and compile the project.</span></span>
* <span data-ttu-id="99e1e-118">[Git](http://git-scm.com/): se utiliza para descargar el proyecto de GitHub.</span><span class="sxs-lookup"><span data-stu-id="99e1e-118">[Git](http://git-scm.com/): Used to download the project from GitHub.</span></span>
* <span data-ttu-id="99e1e-119">Un cliente **SSH** : se usa para conectarse a los clústeres de HDInsight basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="99e1e-119">An **SSH** client: Used to connect to the Linux-based HDInsight clusters.</span></span> <span data-ttu-id="99e1e-120">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="99e1e-120">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="99e1e-121">No necesita un clúster existente de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="99e1e-121">You do not need an existing HDInsight cluster.</span></span> <span data-ttu-id="99e1e-122">En los pasos de este documento se crean los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="99e1e-122">The steps in this document create the following resources:</span></span>
> 
> * <span data-ttu-id="99e1e-123">Una red virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="99e1e-123">An Azure Virtual Network</span></span>
> * <span data-ttu-id="99e1e-124">Un clúster de Storm en HDInsight (dos nodos de trabajo basados en Linux)</span><span class="sxs-lookup"><span data-stu-id="99e1e-124">A Storm on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="99e1e-125">Un clúster de HBase en HDInsight (dos nodos de trabajo basados en Linux)</span><span class="sxs-lookup"><span data-stu-id="99e1e-125">An HBase on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="99e1e-126">Una aplicación web de Azure que hospeda el panel web</span><span class="sxs-lookup"><span data-stu-id="99e1e-126">An Azure Web App that hosts the web dashboard</span></span>

## <a name="architecture"></a><span data-ttu-id="99e1e-127">Arquitectura</span><span class="sxs-lookup"><span data-stu-id="99e1e-127">Architecture</span></span>

![diagrama de arquitectura](./media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

<span data-ttu-id="99e1e-129">Este ejemplo consta de los siguientes componentes:</span><span class="sxs-lookup"><span data-stu-id="99e1e-129">This example consists of the following components:</span></span>

* <span data-ttu-id="99e1e-130">**Centros de eventos de Azure**: contiene datos que se recopilan de los sensores.</span><span class="sxs-lookup"><span data-stu-id="99e1e-130">**Azure Event Hubs**: Contains data that is collected from sensors.</span></span>
* <span data-ttu-id="99e1e-131">**Storm en HDInsight**: ofrece procesamiento en tiempo real de datos desde el Centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="99e1e-131">**Storm on HDInsight**: Provides real-time processing of data from Event Hub.</span></span>
* <span data-ttu-id="99e1e-132">**HBase en HDInsight**: proporciona un almacén de datos NoSQL persistente para los datos después de haberse procesado en Storm.</span><span class="sxs-lookup"><span data-stu-id="99e1e-132">**HBase on HDInsight**: Provides a persistent NoSQL data store for data after it has been processed by Storm.</span></span>
* <span data-ttu-id="99e1e-133">**Servicio de Red virtual de Azure**: habilita las comunicaciones seguras entre el Storm en HDInsight y HBase en clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="99e1e-133">**Azure Virtual Network service**: Enables secure communications between the Storm on HDInsight and HBase on HDInsight clusters.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="99e1e-134">Se requiere una red virtual cuando se usa la API de cliente Java de HBase.</span><span class="sxs-lookup"><span data-stu-id="99e1e-134">A virtual network is required when using the Java HBase client API.</span></span> <span data-ttu-id="99e1e-135">No está expuesta a través de la puerta de enlace pública para los clústeres de HBase.</span><span class="sxs-lookup"><span data-stu-id="99e1e-135">It is not exposed over the public gateway for HBase clusters.</span></span> <span data-ttu-id="99e1e-136">La instalación de clústeres de HBase y Storm en la misma red virtual permite que el clúster de Storm (o cualquier otro sistema de la red virtual) acceda directamente a HBase mediante la API de cliente.</span><span class="sxs-lookup"><span data-stu-id="99e1e-136">Installing HBase and Storm clusters into the same virtual network allows the Storm cluster (or any other system on the virtual network) to directly access HBase using client API.</span></span>

* <span data-ttu-id="99e1e-137">**Sitio web del panel**: un panel de ejemplo que muestra datos en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="99e1e-137">**Dashboard website**: An example dashboard that charts data in real time.</span></span>
  
  * <span data-ttu-id="99e1e-138">El sitio web se implementa en Node.js.</span><span class="sxs-lookup"><span data-stu-id="99e1e-138">The website is implemented in Node.js.</span></span>
  * <span data-ttu-id="99e1e-139">[Socket.io](http://socket.io/) se usa para la comunicación en tiempo real entre la topología Storm y el sitio web.</span><span class="sxs-lookup"><span data-stu-id="99e1e-139">[Socket.io](http://socket.io/) is used for real-time communication between the Storm topology and the website.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="99e1e-140">Usar Socket.io para comunicaciones es un detalle de implementación.</span><span class="sxs-lookup"><span data-stu-id="99e1e-140">Using Socket.io for communication is an implementation detail.</span></span> <span data-ttu-id="99e1e-141">Puede usar cualquier marco de comunicaciones, como SignalR o WebSockets sin procesar.</span><span class="sxs-lookup"><span data-stu-id="99e1e-141">You can use any communications framework, such as raw WebSockets or SignalR.</span></span>

  * <span data-ttu-id="99e1e-142">[D3.js](http://d3js.org/) se usa para representar los datos que se envían al sitio web.</span><span class="sxs-lookup"><span data-stu-id="99e1e-142">[D3.js](http://d3js.org/) is used to graph the data that is sent to the website.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="99e1e-143">Como no hay ningún método compatible para crear un clúster de HDInsight para Storm y HBase, se requieren dos clústeres</span><span class="sxs-lookup"><span data-stu-id="99e1e-143">Two clusters are required, as there is no supported method to create one HDInsight cluster for both Storm and HBase.</span></span>

<span data-ttu-id="99e1e-144">La topología lee datos del Centro de eventos mediante la clase [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) y escribe los datos en HBase usando la clase [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html).</span><span class="sxs-lookup"><span data-stu-id="99e1e-144">The topology reads data from Event Hub by using the [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) class, and writes data into HBase using the [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) class.</span></span> <span data-ttu-id="99e1e-145">La comunicación con el sitio web se logra mediante [client.java socket.io](https://github.com/nkzawa/socket.io-client.java).</span><span class="sxs-lookup"><span data-stu-id="99e1e-145">Communication with the website is accomplished by using [socket.io-client.java](https://github.com/nkzawa/socket.io-client.java).</span></span>

<span data-ttu-id="99e1e-146">En el diagrama siguiente se explica el diseño de la topología:</span><span class="sxs-lookup"><span data-stu-id="99e1e-146">The following diagram explains the layout of the topology:</span></span>

![diagrama de topología](./media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> <span data-ttu-id="99e1e-148">Este diagrama es una vista simplificada de la topología.</span><span class="sxs-lookup"><span data-stu-id="99e1e-148">This diagram is a simplified view of the topology.</span></span> <span data-ttu-id="99e1e-149">Por cada partición del Centro de eventos se crea una instancia de cada componente.</span><span class="sxs-lookup"><span data-stu-id="99e1e-149">An instance of each component is created for each partition in your Event Hub.</span></span> <span data-ttu-id="99e1e-150">Estas instancias se distribuyen entre los nodos del clúster y los datos se enrutan entre ellos como sigue:</span><span class="sxs-lookup"><span data-stu-id="99e1e-150">These instances are distributed across the nodes in the cluster, and data is routed between them as follows:</span></span>
> 
> * <span data-ttu-id="99e1e-151">Se equilibran las cargas de los datos del spout al analizador.</span><span class="sxs-lookup"><span data-stu-id="99e1e-151">Data from the spout to the parser is load balanced.</span></span>
> * <span data-ttu-id="99e1e-152">Los datos del analizador al panel y HBase se agrupan por identificador de dispositivo, para que los mensajes del mismo dispositivo fluyan siempre al mismo componente.</span><span class="sxs-lookup"><span data-stu-id="99e1e-152">Data from the parser to the Dashboard and HBase is grouped by Device ID, so that messages from the same device always flow to the same component.</span></span>

### <a name="topology-components"></a><span data-ttu-id="99e1e-153">Componentes de la topología</span><span class="sxs-lookup"><span data-stu-id="99e1e-153">Topology components</span></span>

* <span data-ttu-id="99e1e-154">**Event Hubs Spout**: el spout se proporciona como parte de Apache Storm versión 0.10.0 y posteriores.</span><span class="sxs-lookup"><span data-stu-id="99e1e-154">**Event Hub Spout**: The spout is provided as part of Apache Storm version 0.10.0 and higher.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="99e1e-155">El spout de Event Hubs utilizado en este ejemplo requiere un clúster de Storm en HDInsight versión 3.5 o 3.6.</span><span class="sxs-lookup"><span data-stu-id="99e1e-155">The Event Hub spout used in this example requires a Storm on HDInsight cluster version 3.5 or 3.6.</span></span>

* <span data-ttu-id="99e1e-156">**ParserBolt.java**: los datos que emite el spout son JSON sin procesar y, en ocasiones, se emite más de un evento a la vez.</span><span class="sxs-lookup"><span data-stu-id="99e1e-156">**ParserBolt.java**: The data that is emitted by the spout is raw JSON, and occasionally more than one event is emitted at a time.</span></span> <span data-ttu-id="99e1e-157">Este bolt lee los datos que emite el spout y analiza el mensaje JSON.</span><span class="sxs-lookup"><span data-stu-id="99e1e-157">This bolt reads the data emitted by the spout and parses the JSON message.</span></span> <span data-ttu-id="99e1e-158">A continuación, el bolt envía los datos como tupla con varios campos.</span><span class="sxs-lookup"><span data-stu-id="99e1e-158">The bolt then emits the data as a tuple that contains multiple fields.</span></span>
* <span data-ttu-id="99e1e-159">**DashboardBolt.java**: este componente muestra cómo usar la biblioteca de cliente de Socket.io para Java para enviar datos en tiempo real al panel web.</span><span class="sxs-lookup"><span data-stu-id="99e1e-159">**DashboardBolt.java**: This component demonstrates how to use the Socket.io client library for Java to send data in real time to the web dashboard.</span></span>
* <span data-ttu-id="99e1e-160">**no hbase.yaml**: la definición de la topología utilizada con la ejecución en modo local.</span><span class="sxs-lookup"><span data-stu-id="99e1e-160">**no-hbase.yaml**: The topology definition used when running in local mode.</span></span> <span data-ttu-id="99e1e-161">No usa componentes de HBase.</span><span class="sxs-lookup"><span data-stu-id="99e1e-161">It does not use HBase components.</span></span>
* <span data-ttu-id="99e1e-162">**with-hbase.yaml**: la definición de la topología utilizada con la ejecución de la topología en el clúster.</span><span class="sxs-lookup"><span data-stu-id="99e1e-162">**with-hbase.yaml**: The topology definition used when running the topology on the cluster.</span></span> <span data-ttu-id="99e1e-163">Usa componentes de HBase.</span><span class="sxs-lookup"><span data-stu-id="99e1e-163">It does use HBase components.</span></span>
* <span data-ttu-id="99e1e-164">**dev.properties**: la información de configuración del spout de Event Hubs, el bolt de HBase y los componentes del panel.</span><span class="sxs-lookup"><span data-stu-id="99e1e-164">**dev.properties**: The configuration information for the Event Hub spout, HBase bolt, and dashboard components.</span></span>

## <a name="prepare-your-environment"></a><span data-ttu-id="99e1e-165">Preparación del entorno</span><span class="sxs-lookup"><span data-stu-id="99e1e-165">Prepare your environment</span></span>

<span data-ttu-id="99e1e-166">Antes de usar este ejemplo, debe crear un Centro de eventos de Azure, desde el que lee la topología de Storm.</span><span class="sxs-lookup"><span data-stu-id="99e1e-166">Before you use this example, you must create an Azure Event Hub, which the Storm topology reads from.</span></span>

### <a name="configure-event-hub"></a><span data-ttu-id="99e1e-167">Configuración del centro de eventos</span><span class="sxs-lookup"><span data-stu-id="99e1e-167">Configure Event Hub</span></span>

<span data-ttu-id="99e1e-168">Centro de eventos es el origen de datos para este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="99e1e-168">Event Hub is the data source for this example.</span></span> <span data-ttu-id="99e1e-169">Use los pasos siguientes para crear un centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="99e1e-169">Use the following steps to create an Event Hub.</span></span>

1. <span data-ttu-id="99e1e-170">En [Azure Portal](https://portal.azure.com), seleccione **+ Nuevo** -> **Internet de las cosas** -> **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-170">From the [Azure portal](https://portal.azure.com), select **+ New** -> **Internet of Things** -> **Event Hubs**.</span></span>
2. <span data-ttu-id="99e1e-171">En la sección **Crear espacio de nombres**, realice las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="99e1e-171">In the **Create Namespace** section, perform the following tasks:</span></span>
   
   1. <span data-ttu-id="99e1e-172">Escriba un valor en **Nombre** para el espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="99e1e-172">Enter a **Name** for the namespace.</span></span>
   2. <span data-ttu-id="99e1e-173">Seleccione un plan de tarifa.</span><span class="sxs-lookup"><span data-stu-id="99e1e-173">Select a pricing tier.</span></span> <span data-ttu-id="99e1e-174">**Básico** es suficiente para este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="99e1e-174">**Basic** is sufficient for this example.</span></span>
   3. <span data-ttu-id="99e1e-175">Seleccione la suscripción de Azure que va a usar en **Suscripción** .</span><span class="sxs-lookup"><span data-stu-id="99e1e-175">Select the Azure **Subscription** to use.</span></span>
   4. <span data-ttu-id="99e1e-176">Seleccione un grupo de recursos existente o cree uno.</span><span class="sxs-lookup"><span data-stu-id="99e1e-176">Either select an existing resource group or create a new one.</span></span>
   5. <span data-ttu-id="99e1e-177">Seleccione un valor en **Ubicación** para el centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="99e1e-177">Select the **Location** for the Event Hub.</span></span>
   6. <span data-ttu-id="99e1e-178">Seleccione **Anclar al panel** y luego haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-178">Select **Pin to dashboard**, and then click **Create**.</span></span>

3. <span data-ttu-id="99e1e-179">Cuando se completa el proceso de creación, se muestra la información de Event Hubs para el espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="99e1e-179">When the creation process completes, the Event Hubs information for your namespace is displayed.</span></span> <span data-ttu-id="99e1e-180">Desde ahí, seleccione **+ Agregar Centro de eventos**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-180">From here, select **+ Add Event Hub**.</span></span> <span data-ttu-id="99e1e-181">En la sección **Crear centro de eventos**, escriba el nombre **sensordata** y seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-181">In the **Create Event Hub** section, enter a name of **sensordata**, and then select **Create**.</span></span> <span data-ttu-id="99e1e-182">Deje los demás campos con los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="99e1e-182">Leave the other fields at the default values.</span></span>
4. <span data-ttu-id="99e1e-183">En la vista de Event Hubs para el espacio de nombres, seleccione **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-183">From the Event Hubs view for your namespace, select **Event Hubs**.</span></span> <span data-ttu-id="99e1e-184">Seleccione la entrada **sensordata** .</span><span class="sxs-lookup"><span data-stu-id="99e1e-184">Select the **sensordata** entry.</span></span>
5. <span data-ttu-id="99e1e-185">En el centro de eventos de sensordata, seleccione **Directivas de acceso compartido**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-185">From the sensordata Event Hub, select **Shared access policies**.</span></span> <span data-ttu-id="99e1e-186">Use el vínculo **+ Agregar** para agregar las siguientes directivas:</span><span class="sxs-lookup"><span data-stu-id="99e1e-186">Use the **+ Add** link to add the following policies:</span></span>

    | <span data-ttu-id="99e1e-187">Nombre de la directiva</span><span class="sxs-lookup"><span data-stu-id="99e1e-187">Policy name</span></span> | <span data-ttu-id="99e1e-188">Notificaciones</span><span class="sxs-lookup"><span data-stu-id="99e1e-188">Claims</span></span> |
    | ----- | ----- |
    | <span data-ttu-id="99e1e-189">devices</span><span class="sxs-lookup"><span data-stu-id="99e1e-189">devices</span></span> | <span data-ttu-id="99e1e-190">Enviar</span><span class="sxs-lookup"><span data-stu-id="99e1e-190">Send</span></span> |
    | <span data-ttu-id="99e1e-191">storm</span><span class="sxs-lookup"><span data-stu-id="99e1e-191">storm</span></span> | <span data-ttu-id="99e1e-192">Escuchar</span><span class="sxs-lookup"><span data-stu-id="99e1e-192">Listen</span></span> |

1. <span data-ttu-id="99e1e-193">Seleccione ambas directivas y tome nota del valor en **CLAVE PRINCIPAL** .</span><span class="sxs-lookup"><span data-stu-id="99e1e-193">Select both policies and make a note of the **PRIMARY KEY** value.</span></span> <span data-ttu-id="99e1e-194">Necesitará el valor de ambas directivas en pasos posteriores.</span><span class="sxs-lookup"><span data-stu-id="99e1e-194">You need the value for both policies in future steps.</span></span>

## <a name="download-and-configure-the-project"></a><span data-ttu-id="99e1e-195">Descarga y configuración del proyecto</span><span class="sxs-lookup"><span data-stu-id="99e1e-195">Download and configure the project</span></span>

<span data-ttu-id="99e1e-196">Use lo siguiente para descargar el proyecto de GitHub.</span><span class="sxs-lookup"><span data-stu-id="99e1e-196">Use the following to download the project from GitHub.</span></span>

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

<span data-ttu-id="99e1e-197">Cuando se haya completado el comando, tendrá la siguiente estructura de directorios:</span><span class="sxs-lookup"><span data-stu-id="99e1e-197">After the command completes, you have the following directory structure:</span></span>

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains the topology
            resources/
                log4j2.xml - set logging to minimal.
                no-hbase.yaml - topology definition without hbase components.
                with-hbase.yaml - topology definition with hbase components.
            src/main/java/com/microsoft/examples/bolts/
                ParserBolt.java - parses JSON data into tuples
                DashboardBolt.java - sends data over Socket.IO to the web dashboard.
        dashboard/nodejs/ - this is the node.js web dashboard.
        SendEvents/ - utilities to send fake sensor data.

> [!NOTE]
> <span data-ttu-id="99e1e-198">Este documento no profundiza en los detalles sobre el código incluido en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="99e1e-198">This document does not go in to full details of the code included in this example.</span></span> <span data-ttu-id="99e1e-199">Sin embargo, se comenta el código completo.</span><span class="sxs-lookup"><span data-stu-id="99e1e-199">However, the code is fully commented.</span></span>

<span data-ttu-id="99e1e-200">Para configurar el proyecto para leer desde Event Hubs, abra el archivo `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` y agregue la información de la instancia de Event Hubs a las líneas siguientes:</span><span class="sxs-lookup"><span data-stu-id="99e1e-200">To configure the project to read from Event Hub, open the `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` file and add your Event Hub information to the following lines:</span></span>

```bash
eventhub.read.policy.name: your_read_policy_name
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: your_event_hub_name
eventhub.partitions: 2
```

## <a name="compile-and-test-locally"></a><span data-ttu-id="99e1e-201">Compilación y pruebas locales</span><span class="sxs-lookup"><span data-stu-id="99e1e-201">Compile and test locally</span></span>

> [!IMPORTANT]
> <span data-ttu-id="99e1e-202">Para el uso local de la topología se necesita un entorno de desarrollo de Storm en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="99e1e-202">Using the topology locally requires a working Storm development environment.</span></span> <span data-ttu-id="99e1e-203">Para más información, consulte [Setting up a development environment](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) (Configuración de un entorno de desarrollo) en Apache.org.</span><span class="sxs-lookup"><span data-stu-id="99e1e-203">For more information, see [Setting up a Storm development environment](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) at Apache.org.</span></span>

> [!WARNING]
> <span data-ttu-id="99e1e-204">Si utiliza un entorno de desarrollo de Windows, puede recibir `java.io.IOException` al ejecutar la topología de manera local.</span><span class="sxs-lookup"><span data-stu-id="99e1e-204">If you are using a Windows development environment, you may receive a `java.io.IOException` when running the topology locally.</span></span> <span data-ttu-id="99e1e-205">Si es así, ejecute la topología en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="99e1e-205">If so, move on to running the topology on HDInsight.</span></span>

<span data-ttu-id="99e1e-206">Antes de las pruebas, debe iniciar el panel para ver el resultado de la topología y generar datos para almacenarlos en el Centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="99e1e-206">Before testing, you must start the dashboard to view the output of the topology and generate data to store in Event Hub.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="99e1e-207">El componente HBase de esta topología no está activo cuando se prueba localmente.</span><span class="sxs-lookup"><span data-stu-id="99e1e-207">The HBase component of this topology is not active when testing locally.</span></span> <span data-ttu-id="99e1e-208">No se puede acceder a la API de Java para el clúster de HBase desde fuera de la red virtual de Azure con los clústeres.</span><span class="sxs-lookup"><span data-stu-id="99e1e-208">The Java API for the HBase cluster cannot be accessed from outside the Azure Virtual Network that contains the clusters.</span></span>

### <a name="start-the-web-application"></a><span data-ttu-id="99e1e-209">Inicio de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="99e1e-209">Start the web application</span></span>

1. <span data-ttu-id="99e1e-210">Abra un símbolo del sistema y cambie los directorios a `hdinsight-eventhub-example/dashboard`.</span><span class="sxs-lookup"><span data-stu-id="99e1e-210">Open a command prompt and change directories to `hdinsight-eventhub-example/dashboard`.</span></span> <span data-ttu-id="99e1e-211">Use el siguiente comando para instalar las dependencias necesarias para la aplicación web:</span><span class="sxs-lookup"><span data-stu-id="99e1e-211">Use the following command to install the dependencies needed by the web application:</span></span>
   
    ```bash
    npm install
    ```

2. <span data-ttu-id="99e1e-212">Use el comando siguiente para iniciar la aplicación web:</span><span class="sxs-lookup"><span data-stu-id="99e1e-212">Use the following command to start the web application:</span></span>
   
    ```bash
    node server.js
    ```
   
    <span data-ttu-id="99e1e-213">Verá un mensaje similar al texto siguiente:</span><span class="sxs-lookup"><span data-stu-id="99e1e-213">You see a message similar to the following text:</span></span>
   
        Server listening at port 3000

3. <span data-ttu-id="99e1e-214">Abra un explorador web y escriba `http://localhost:3000/` como dirección.</span><span class="sxs-lookup"><span data-stu-id="99e1e-214">Open a web browser and enter `http://localhost:3000/` as the address.</span></span> <span data-ttu-id="99e1e-215">Aparece una página similar a la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="99e1e-215">A page similar to the following image is displayed:</span></span>
   
    ![panel web](./media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    <span data-ttu-id="99e1e-217">Deje abierto este símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="99e1e-217">Leave this command prompt open.</span></span> <span data-ttu-id="99e1e-218">Después de las pruebas, presione CTRL+C para detener el servidor web.</span><span class="sxs-lookup"><span data-stu-id="99e1e-218">After testing, use Ctrl-C to stop the web server.</span></span>

### <a name="generate-data"></a><span data-ttu-id="99e1e-219">Generación de datos</span><span class="sxs-lookup"><span data-stu-id="99e1e-219">Generate data</span></span>

> [!NOTE]
> <span data-ttu-id="99e1e-220">Los pasos de esta sección usan Node.js para que se puedan utilizar en cualquier plataforma.</span><span class="sxs-lookup"><span data-stu-id="99e1e-220">The steps in this section use Node.js so that they can be used on any platform.</span></span> <span data-ttu-id="99e1e-221">Para ejemplos de otros lenguajes, consulte el directorio `SendEvents`.</span><span class="sxs-lookup"><span data-stu-id="99e1e-221">For other language examples, see the `SendEvents` directory.</span></span>

1. <span data-ttu-id="99e1e-222">Abra un nuevo símbolo del sistema, shell o terminal y cambie los directorios a `hdinsight-eventhub-example/SendEvents/nodejs`.</span><span class="sxs-lookup"><span data-stu-id="99e1e-222">Open a new prompt, shell, or terminal, and change directories to `hdinsight-eventhub-example/SendEvents/nodejs`.</span></span> <span data-ttu-id="99e1e-223">Use el comando siguiente para instalar las dependencias que necesita la aplicación:</span><span class="sxs-lookup"><span data-stu-id="99e1e-223">To install the dependencies needed by the application, use the following command:</span></span>

    ```bash
    npm install
    ```

2. <span data-ttu-id="99e1e-224">Abra el archivo `app.js` en un editor de texto y agregue la información de la instancia de Event Hubs que obtuvo anteriormente:</span><span class="sxs-lookup"><span data-stu-id="99e1e-224">Open the `app.js` file in a text editor and add the Event Hub information you obtained earlier:</span></span>
   
    ```javascript
    // ServiceBus Namespace
    var namespace = 'YourNamespace';
    // Event Hub Name
    var hubname ='sensordata';
    // Shared access Policy name and key (from Event Hub configuration)
    var my_key_name = 'devices';
    var my_key = 'YourKey';
    ```
   
   > [!NOTE]
   > <span data-ttu-id="99e1e-225">En este ejemplo se da por hecho que ha usado `sensordata` como nombre de la instancia de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="99e1e-225">This example assumes that you have used `sensordata` as the name of your Event Hub.</span></span> <span data-ttu-id="99e1e-226">Y `devices` como nombre de la directiva con la notificación `Send`.</span><span class="sxs-lookup"><span data-stu-id="99e1e-226">And that `devices` as the name of the policy that has a `Send` claim.</span></span>

3. <span data-ttu-id="99e1e-227">Use el siguiente comando para insertar entradas nuevas en el Centro de eventos:</span><span class="sxs-lookup"><span data-stu-id="99e1e-227">Use the following command to insert new entries in Event Hub:</span></span>
   
    ```bash
    node app.js
    ```
   
    <span data-ttu-id="99e1e-228">Verá varias líneas de salida que contienen los datos enviados al Centro de eventos:</span><span class="sxs-lookup"><span data-stu-id="99e1e-228">You see several lines of output that contain the data sent to Event Hub:</span></span>
   
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"0","Temperature":7}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"1","Temperature":39}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"2","Temperature":86}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"3","Temperature":29}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"4","Temperature":30}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"5","Temperature":5}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"6","Temperature":24}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"7","Temperature":40}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"8","Temperature":43}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"9","Temperature":84}

### <a name="build-and-start-the-topology"></a><span data-ttu-id="99e1e-229">Compilación e inicio de la topología</span><span class="sxs-lookup"><span data-stu-id="99e1e-229">Build and start the topology</span></span>

1. <span data-ttu-id="99e1e-230">Abra un símbolo del sistema nuevo y cambie los directorios a `hdinsight-eventhub-example/TemperatureMonitor`.</span><span class="sxs-lookup"><span data-stu-id="99e1e-230">Open a new command prompt and change directories to `hdinsight-eventhub-example/TemperatureMonitor`.</span></span> <span data-ttu-id="99e1e-231">Para compilar y empaquetar la topología, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="99e1e-231">To build and package the topology, use the following command:</span></span> 

    ```bash
    mvn clean package
    ```

2. <span data-ttu-id="99e1e-232">Para iniciar la topología en modo local, use el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="99e1e-232">To start the topology in local mode, use the following command:</span></span>

    ```bash
    storm jar target/TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local --filter dev.properties resources/no-hbase.yaml
    ```

    * <span data-ttu-id="99e1e-233">`--local` inicia la topología en modo local.</span><span class="sxs-lookup"><span data-stu-id="99e1e-233">`--local` starts the topology in local mode.</span></span>
    * <span data-ttu-id="99e1e-234">`--filter`usa el archivo `dev.properties` para rellenar los parámetros de la definición de topología.</span><span class="sxs-lookup"><span data-stu-id="99e1e-234">`--filter` uses the `dev.properties` file to populate parameters in the topology definition.</span></span>
    * <span data-ttu-id="99e1e-235">`resources/no-hbase.yaml` usa la definición de la topología `no-hbase.yaml`.</span><span class="sxs-lookup"><span data-stu-id="99e1e-235">`resources/no-hbase.yaml` uses the `no-hbase.yaml` topology definition.</span></span>
 
   <span data-ttu-id="99e1e-236">Una vez iniciada, la topología lee entradas del centro de eventos y las envía al panel que se ejecuta en la máquina local.</span><span class="sxs-lookup"><span data-stu-id="99e1e-236">Once started, the topology reads entries from Event Hub, and sends them to the dashboard running on your local machine.</span></span> <span data-ttu-id="99e1e-237">Debe ver que aparecen líneas en el panel web, parecidas a las de la imagen siguiente:</span><span class="sxs-lookup"><span data-stu-id="99e1e-237">You should see lines appear in the web dashboard, similar to the following image:</span></span>
   
    ![panel con datos](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. <span data-ttu-id="99e1e-239">Mientras se ejecuta el panel, use el comando `node app.js` de los pasos anteriores para enviar datos nuevos a los Centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="99e1e-239">While the dashboard is running, use the `node app.js` command from the previous steps to send new data to Event Hubs.</span></span> <span data-ttu-id="99e1e-240">Dado que los valores de temperatura se generan aleatoriamente, el gráfico debe actualizarse para mostrar cambios importantes en la temperatura.</span><span class="sxs-lookup"><span data-stu-id="99e1e-240">Because the temperature values are randomly generated, the graph should update to show large changes in temperature.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="99e1e-241">Debe estar en el directorio **hdinsight-eventhub-example/SendEvents/Nodejs** cuando use el comando `node app.js`.</span><span class="sxs-lookup"><span data-stu-id="99e1e-241">You must be in the **hdinsight-eventhub-example/SendEvents/Nodejs** directory when using the `node app.js` command.</span></span>

3. <span data-ttu-id="99e1e-242">Después de comprobar que el panel se actualiza, presione Ctrl+C para detener la topología.</span><span class="sxs-lookup"><span data-stu-id="99e1e-242">After verifying that the dashboard updates, stop the topology using Ctrl+C.</span></span> <span data-ttu-id="99e1e-243">También puede presionar CTRL+C para detener el servidor web local.</span><span class="sxs-lookup"><span data-stu-id="99e1e-243">You can use Ctrl+C to stop the local web server also.</span></span>

## <a name="create-a-storm-and-hbase-cluster"></a><span data-ttu-id="99e1e-244">Creación de un clúster de Storm y HBase</span><span class="sxs-lookup"><span data-stu-id="99e1e-244">Create a Storm and HBase cluster</span></span>

<span data-ttu-id="99e1e-245">En los pasos descritos en esta sección se usa una [plantilla de Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) para crear una red virtual de Azure y, en ella, un clúster de Storm y HBase.</span><span class="sxs-lookup"><span data-stu-id="99e1e-245">The steps in this section use an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) to create an Azure Virtual Network and a Storm and HBase cluster on the virtual network.</span></span> <span data-ttu-id="99e1e-246">La plantilla también crea una aplicación web de Azure e implementa una copia del panel en ella.</span><span class="sxs-lookup"><span data-stu-id="99e1e-246">The template also creates an Azure Web App and deploys a copy of the dashboard into it.</span></span>

> [!NOTE]
> <span data-ttu-id="99e1e-247">Se utiliza una red virtual para que la topología que se ejecuta en el clúster de Storm pueda comunicarse directamente con el clúster de HBase usando la API Java de HBase.</span><span class="sxs-lookup"><span data-stu-id="99e1e-247">A virtual network is used so that the topology running on the Storm cluster can directly communicate with the HBase cluster using the HBase Java API.</span></span>

<span data-ttu-id="99e1e-248">La plantilla de Resource Manager que se usa en este documento se encuentra en un contenedor de blobs público de **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-248">The Resource Manager template used in this document is located in a public blob container at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span></span>

1. <span data-ttu-id="99e1e-249">Haga clic en el botón siguiente para iniciar sesión en Azure y abrir la plantilla de Resource Manager en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="99e1e-249">Click the following button to sign in to Azure and open the Resource Manager template in the Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.6.json" target="_blank"><img src="./media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. <span data-ttu-id="99e1e-250">En la sección **Custom deployment** (Implementación personalizada), escriba los valores siguientes:</span><span class="sxs-lookup"><span data-stu-id="99e1e-250">From the **Custom deployment** section, enter the following values:</span></span>
   
    ![Parámetros de HDInsight](./media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * <span data-ttu-id="99e1e-252">**Nombre base del clúster**: este valor se utiliza como nombre base para los clústeres Storm y HBase.</span><span class="sxs-lookup"><span data-stu-id="99e1e-252">**Base Cluster Name**: This value is used as the base name for the Storm and HBase clusters.</span></span> <span data-ttu-id="99e1e-253">Por ejemplo, si escribe **abc**, se creará un clúster de Storm denominado **storm-abc** y un clúster de HBase denominado **hbase-abc**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-253">For example, entering **abc** creates a Storm cluster named **storm-abc** and an HBase cluster named **hbase-abc**.</span></span>
   * <span data-ttu-id="99e1e-254">**Nombre de usuario de inicio de sesión del clúster**: nombre de usuario del administrador de los clústeres Storm y HBase.</span><span class="sxs-lookup"><span data-stu-id="99e1e-254">**Cluster Login User Name**: The admin user name for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="99e1e-255">**Contraseña de inicio de sesión de clúster**: contraseña del usuario administrador para los clústeres Storm y HBase.</span><span class="sxs-lookup"><span data-stu-id="99e1e-255">**Cluster Login Password**: The admin user password for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="99e1e-256">**Nombre de usuario SSH**: usuario de SSH para crear los clústeres de Storm y HBase.</span><span class="sxs-lookup"><span data-stu-id="99e1e-256">**SSH User Name**: The SSH user to create for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="99e1e-257">**Contraseña SSH**: contraseña del usuario SSH para los clústeres de Storm y HBase.</span><span class="sxs-lookup"><span data-stu-id="99e1e-257">**SSH Password**: The password for the SSH user for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="99e1e-258">**Ubicación**: región en la que se crearán los clústeres.</span><span class="sxs-lookup"><span data-stu-id="99e1e-258">**Location**: The region that the clusters are created in.</span></span>
     
     <span data-ttu-id="99e1e-259">Haga clic en **Aceptar** para guardar los parámetros.</span><span class="sxs-lookup"><span data-stu-id="99e1e-259">Click **OK** to save the parameters.</span></span>

3. <span data-ttu-id="99e1e-260">Use la sección **Datos básicos** para crear un grupo de recursos o seleccionar uno existente.</span><span class="sxs-lookup"><span data-stu-id="99e1e-260">Use the **Basics** section to create a resource group or select an existing one.</span></span>
4. <span data-ttu-id="99e1e-261">En el menú desplegable **Ubicación del grupo de recursos**, seleccione la misma ubicación que seleccionó para el parámetro **Ubicación** de la sección **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-261">In the **Resource group location** dropdown menu, select the same location as you selected for the **Location** parameter in the **Settings** section.</span></span>
5. <span data-ttu-id="99e1e-262">Consulte los términos y condiciones y seleccione **Acepto los términos y condiciones indicados anteriormente**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-262">Read the terms and conditions, and then select **I agree to the terms and conditions stated above**.</span></span>
6. <span data-ttu-id="99e1e-263">Por último, active **Anclar al panel** y seleccione **Adquirir**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-263">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="99e1e-264">Se tarda aproximadamente 20 minutos en crear los clústeres.</span><span class="sxs-lookup"><span data-stu-id="99e1e-264">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="99e1e-265">Cuando se hayan creado los recursos, se muestra la información sobre el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="99e1e-265">Once the resources have been created, information about the resource group is displayed.</span></span>

![Grupo de recursos de la red virtual y clústeres](./media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="99e1e-267">Observe que los nombres de los clústeres de HDInsight son **storm-BASENAME** y **hbase-BASENAME**, donde BASENAME es el nombre proporcionado a la plantilla.</span><span class="sxs-lookup"><span data-stu-id="99e1e-267">Notice that the names of the HDInsight clusters are **storm-BASENAME** and **hbase-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="99e1e-268">Estos nombres se utilizarán más adelante al establecer la conexión con los clústeres.</span><span class="sxs-lookup"><span data-stu-id="99e1e-268">You use these names in a later step when connecting to the clusters.</span></span> <span data-ttu-id="99e1e-269">Observe también que el nombre del sitio del panel es **basename-dashboard**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-269">Also note that the name of the dashboard site is **basename-dashboard**.</span></span> <span data-ttu-id="99e1e-270">Este valor se usa más adelante en este documento.</span><span class="sxs-lookup"><span data-stu-id="99e1e-270">This value is used later in this document.</span></span>

## <a name="configure-the-dashboard-bolt"></a><span data-ttu-id="99e1e-271">Configuración del bolt del panel</span><span class="sxs-lookup"><span data-stu-id="99e1e-271">Configure the Dashboard bolt</span></span>

<span data-ttu-id="99e1e-272">Para enviar datos al panel implementado como aplicación web, debe modificar la línea siguiente en el archivo `dev.properties`:</span><span class="sxs-lookup"><span data-stu-id="99e1e-272">To send data to the dashboard deployed as a web app, you must modify the following line in the `dev.properties`file:</span></span>

```yaml
dashboard.uri: http://localhost:3000
```

<span data-ttu-id="99e1e-273">Cambie `http://localhost:3000` por `http://BASENAME-dashboard.azurewebsites.net` y guarde el archivo.</span><span class="sxs-lookup"><span data-stu-id="99e1e-273">Change `http://localhost:3000` to `http://BASENAME-dashboard.azurewebsites.net` and save the file.</span></span> <span data-ttu-id="99e1e-274">Reemplace **BASENAME** por el nombre base proporcionado en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="99e1e-274">Replace **BASENAME** with the base name you provided in the previous step.</span></span> <span data-ttu-id="99e1e-275">También puede utilizar el grupo de recursos que creó anteriormente para seleccionar el panel y ver la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="99e1e-275">You can also use the resource group created previously to select the dashboard and view the URL.</span></span>

## <a name="create-the-hbase-table"></a><span data-ttu-id="99e1e-276">Creación de la tabla de HBase</span><span class="sxs-lookup"><span data-stu-id="99e1e-276">Create the HBase table</span></span>

<span data-ttu-id="99e1e-277">Para almacenar datos en HBase, primero hay que crear una tabla.</span><span class="sxs-lookup"><span data-stu-id="99e1e-277">To store data in HBase, we must first create a table.</span></span> <span data-ttu-id="99e1e-278">Se crean previamente los recursos en los que Storm necesita escribir, ya que crear recursos desde dentro de una topología de Storm puede dar lugar a que varias instancias intenten crear el mismo recurso.</span><span class="sxs-lookup"><span data-stu-id="99e1e-278">Pre-create resources that Storm needs to write to, as trying to create resources from inside a Storm topology can result in multiple instances trying to create the same resource.</span></span> <span data-ttu-id="99e1e-279">Cree los recursos fuera de la topología y use Storm para leer o escribir y para el análisis.</span><span class="sxs-lookup"><span data-stu-id="99e1e-279">Create the resources outside the topology and use Storm for reading/writing and analytics.</span></span>

1. <span data-ttu-id="99e1e-280">Use SSH para conectarse al clúster de HBase con el usuario y la contraseña de SSH suministrados a la plantilla durante la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="99e1e-280">Use SSH to connect to the HBase cluster using the SSH user and password you supplied to the template during cluster creation.</span></span> <span data-ttu-id="99e1e-281">Por ejemplo, si se conecta con el comando `ssh` , debe usar la sintaxis siguiente:</span><span class="sxs-lookup"><span data-stu-id="99e1e-281">For example, if connecting using the `ssh` command, you would use the following syntax:</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```
   
    <span data-ttu-id="99e1e-282">Reemplace `sshuser` por el nombre de usuario SSH que proporcionó al crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="99e1e-282">Replace `sshuser` with the SSH user name you provided when creating the cluster.</span></span> <span data-ttu-id="99e1e-283">Reemplace `clustername` por el nombre del clúster de HBase.</span><span class="sxs-lookup"><span data-stu-id="99e1e-283">Replace `clustername` with the HBase cluster name.</span></span>

2. <span data-ttu-id="99e1e-284">En la sesión SSH, inicie el shell de HBase.</span><span class="sxs-lookup"><span data-stu-id="99e1e-284">From the SSH session, start the HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="99e1e-285">Una vez cargado el shell, verá un símbolo del sistema de `hbase(main):001:0>`.</span><span class="sxs-lookup"><span data-stu-id="99e1e-285">Once the shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="99e1e-286">En el shell de HBase, escriba el comando siguiente para crear una tabla en la que se almacenarán los datos de los sensores:</span><span class="sxs-lookup"><span data-stu-id="99e1e-286">From the HBase shell, enter the following command to create a table to store the sensor data:</span></span>
   
    ```hbase
    create 'SensorData', 'cf'
    ```

4. <span data-ttu-id="99e1e-287">Compruebe que se ha creado la tabla con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="99e1e-287">Verify that the table has been created by using the following command:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="99e1e-288">Esto devuelve información similar al siguiente ejemplo, que indica que hay 0 filas en la tabla.</span><span class="sxs-lookup"><span data-stu-id="99e1e-288">This returns information similar to the following example, indicating that there are 0 rows in the table.</span></span>
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. <span data-ttu-id="99e1e-289">Escriba `exit` para salir del shell de HBase:</span><span class="sxs-lookup"><span data-stu-id="99e1e-289">Enter `exit` to exit the HBase shell:</span></span>

## <a name="configure-the-hbase-bolt"></a><span data-ttu-id="99e1e-290">Configuración del bolt de HBase</span><span class="sxs-lookup"><span data-stu-id="99e1e-290">Configure the HBase bolt</span></span>

<span data-ttu-id="99e1e-291">Para escribir en HBase desde el clúster de Storm, debe proporcionar el bolt de HBase con los detalles de configuración de su clúster de HBase.</span><span class="sxs-lookup"><span data-stu-id="99e1e-291">To write to HBase from the Storm cluster, you must provide the HBase bolt with the configuration details of your HBase cluster.</span></span>

1. <span data-ttu-id="99e1e-292">Utilice uno de los ejemplos siguientes para recuperar el cuórum de Zookeeper para el clúster de HBase:</span><span class="sxs-lookup"><span data-stu-id="99e1e-292">Use one of the following examples to retrieve the Zookeeper quorum for your HBase cluster:</span></span>

    ```bash
    CLUSTERNAME='your_HDInsight_cluster_name'
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HBASE/components/HBASE_MASTER" | jq '.metrics.hbase.master.ZookeeperQuorum'
    ```

    > [!NOTE]
    > <span data-ttu-id="99e1e-293">Reemplace `your_HDInsight_cluster_name` por el nombre del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="99e1e-293">Replace `your_HDInsight_cluster_name` with the name of your HDInsight cluster.</span></span> <span data-ttu-id="99e1e-294">Para más información acerca de cómo instalar la utilidad `jq`, consulte [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="99e1e-294">For more information on installing the `jq` utility, see [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span></span>
    >
    > <span data-ttu-id="99e1e-295">Cuando se le solicite, escriba la contraseña de inicio de sesión del administrador de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="99e1e-295">When prompted, enter the password for the HDInsight admin login.</span></span>

    ```powershell
    $clusterName = 'your_HDInsight_cluster_name`
    $creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HBASE/components/HBASE_MASTER" -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.metrics.hbase.master.ZookeeperQuorum
    ```

    > [!NOTE]
    > <span data-ttu-id="99e1e-296">Reemplace \`your_HDInsight_cluster_name por el nombre del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="99e1e-296">Replace \`your_HDInsight_cluster_name with the name of your HDInsight cluster.</span></span> <span data-ttu-id="99e1e-297">Cuando se le solicite, escriba la contraseña de inicio de sesión del administrador de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="99e1e-297">When prompted, enter the password for the HDInsight admin login.</span></span>
    >
    > <span data-ttu-id="99e1e-298">Este ejemplo requiere Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="99e1e-298">This example requires Azure PowerShell.</span></span> <span data-ttu-id="99e1e-299">Para información acerca de cómo usar Azure PowerShell, consulte el artículo de [introducción a Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6).</span><span class="sxs-lookup"><span data-stu-id="99e1e-299">For more information on using Azure PowerShell, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)</span></span>

    <span data-ttu-id="99e1e-300">La información que se devuelve de estos ejemplos es similar al texto siguiente:</span><span class="sxs-lookup"><span data-stu-id="99e1e-300">The information returned by these examples is similar to the following text:</span></span>

    `zk2-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk0-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk3-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181`

    <span data-ttu-id="99e1e-301">Esta información la usa Storm para comunicarse con el clúster de HBase.</span><span class="sxs-lookup"><span data-stu-id="99e1e-301">This information is used by Storm to communicate with the HBase cluster.</span></span>

2. <span data-ttu-id="99e1e-302">Modifique el archivo `dev.properties` y agregue la información de cuórum de Zookeeper a la línea siguiente:</span><span class="sxs-lookup"><span data-stu-id="99e1e-302">Modify the `dev.properties` file and add the Zookeeper quorum information to the following line:</span></span>

    ```yaml
    hbase.zookeeper.quorum: your_hbase_quorum
    ```

## <a name="build-package-and-deploy-the-solution-to-hdinsight"></a><span data-ttu-id="99e1e-303">Compilación, empaquetado e implementación de la solución en HDInsight</span><span class="sxs-lookup"><span data-stu-id="99e1e-303">Build, package, and deploy the solution to HDInsight</span></span>

<span data-ttu-id="99e1e-304">En el entorno de desarrollo, siga estos pasos para implementar la topología de Storm en el clúster de storm.</span><span class="sxs-lookup"><span data-stu-id="99e1e-304">In your development environment, use the following steps to deploy the Storm topology to the storm cluster.</span></span>

1. <span data-ttu-id="99e1e-305">Desde el directorio `TemperatureMonitor`, use el comando siguiente para realizar una nueva compilación y crear un paquete JAR a partir del proyecto:</span><span class="sxs-lookup"><span data-stu-id="99e1e-305">From the `TemperatureMonitor` directory, use the following command to perform a new build and create a JAR package from your project:</span></span>
   
        mvn clean package
   
    <span data-ttu-id="99e1e-306">Este comando crea un archivo denominado `TemperatureMonitor-1.0-SNAPSHOT.jar in the ` en el directorio de destino del proyecto.</span><span class="sxs-lookup"><span data-stu-id="99e1e-306">This command creates a file named `TemperatureMonitor-1.0-SNAPSHOT.jar in the `target\` directory of your project.</span></span>

2. <span data-ttu-id="99e1e-307">Use scp para cargar los archivos `TemperatureMonitor-1.0-SNAPSHOT.jar` y `dev.properties` en el clúster de Storm.</span><span class="sxs-lookup"><span data-stu-id="99e1e-307">Use scp to upload the `TemperatureMonitor-1.0-SNAPSHOT.jar` and `dev.properties` files to your Storm cluster.</span></span> <span data-ttu-id="99e1e-308">En el ejemplo siguiente, reemplace `sshuser` por el usuario de SSH que proporcionó al crear el clúster y `clustername` por el nombre del clúster de Storm.</span><span class="sxs-lookup"><span data-stu-id="99e1e-308">In the following example, replace `sshuser` with the SSH user you provided when creating the cluster, and `clustername` with the name of your Storm cluster.</span></span> <span data-ttu-id="99e1e-309">Cuando se le solicite, escriba la contraseña del usuario de SSH.</span><span class="sxs-lookup"><span data-stu-id="99e1e-309">When prompted, enter the password for the SSH user.</span></span>
   
    ```bash
    scp target/TemperatureMonitor-1.0-SNAPSHOT.jar dev.properties sshuser@clustername-ssh.azurehdinsight.net:
    ```

   > [!NOTE]
   > <span data-ttu-id="99e1e-310">Los archivos pueden tardar unos minutos en cargarse.</span><span class="sxs-lookup"><span data-stu-id="99e1e-310">It may take several minutes to upload the files.</span></span>

    <span data-ttu-id="99e1e-311">Para más información sobre cómo usar los comandos `scp` y `ssh` con HDInsight, consulte el artículo sobre el [uso de SSH con HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="99e1e-311">For more information on using the `scp` and `ssh` commands with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

3. <span data-ttu-id="99e1e-312">Una vez cargado el archivo, conéctese al clúster de Storm mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="99e1e-312">Once the file has been uploaded, connect to the Storm cluster using SSH.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="99e1e-313">Reemplace `sshuser` por el nombre de usuario de SSH.</span><span class="sxs-lookup"><span data-stu-id="99e1e-313">Replace `sshuser` with the SSH user name.</span></span> <span data-ttu-id="99e1e-314">Reemplace `clustername` por el nombre de usuario de Storm.</span><span class="sxs-lookup"><span data-stu-id="99e1e-314">Replace `clustername` with the Storm cluster name.</span></span>

4. <span data-ttu-id="99e1e-315">Para comenzar la topología, use el comando siguiente desde la sesión SSH:</span><span class="sxs-lookup"><span data-stu-id="99e1e-315">To start the topology, use the following command from the SSH session:</span></span>
   
    ```bash
    storm jar TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote --filter dev.properties -R /with-hbase.yaml
    ```

    * <span data-ttu-id="99e1e-316">`--remote` envía la topología al servicio Nimbus, que la distribuye en los nodos de supervisión del clúster.</span><span class="sxs-lookup"><span data-stu-id="99e1e-316">`--remote` submits the topology to the Nimbus service, which distributes it to the supervisor nodes in the cluster.</span></span>
    * <span data-ttu-id="99e1e-317">`--filter`usa el archivo `dev.properties` para rellenar los parámetros de la definición de topología.</span><span class="sxs-lookup"><span data-stu-id="99e1e-317">`--filter` uses the `dev.properties` file to populate parameters in the topology definition.</span></span>
    * <span data-ttu-id="99e1e-318">`-R /with-hbase.yaml` usa la topología `with-hbase.yaml` que se incluye en el paquete.</span><span class="sxs-lookup"><span data-stu-id="99e1e-318">`-R /with-hbase.yaml` uses the `with-hbase.yaml` topology included in the package.</span></span>

5. <span data-ttu-id="99e1e-319">Cuando se haya iniciado la topología, abra un explorador con el sitio web publicado en Azure y  use el comando `node app.js` para enviar datos a un Centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="99e1e-319">After the topology has started, open a browser to the website you published on Azure, then use the `node app.js` command to send data to Event Hub.</span></span> <span data-ttu-id="99e1e-320">Debería ver que el panel web se actualiza para mostrar la información.</span><span class="sxs-lookup"><span data-stu-id="99e1e-320">You should see the web dashboard update to display the information.</span></span>
   
    ![dashboard](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a><span data-ttu-id="99e1e-322">Visualización de datos de HBase</span><span class="sxs-lookup"><span data-stu-id="99e1e-322">View HBase data</span></span>

<span data-ttu-id="99e1e-323">Utilice los pasos siguientes para conectarse a HBase y compruebe que se hayan escrito los datos en la tabla:</span><span class="sxs-lookup"><span data-stu-id="99e1e-323">Use the following steps to connect to HBase and verify that the data has been written to the table:</span></span>

1. <span data-ttu-id="99e1e-324">Use SSH para conectarse al clúster de HBase.</span><span class="sxs-lookup"><span data-stu-id="99e1e-324">Use SSH to connect to the HBase cluster.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="99e1e-325">Reemplace `sshuser` por el nombre de usuario de SSH.</span><span class="sxs-lookup"><span data-stu-id="99e1e-325">Replace `sshuser` with the SSH user name.</span></span> <span data-ttu-id="99e1e-326">Reemplace `clustername` por el nombre del clúster de HBase.</span><span class="sxs-lookup"><span data-stu-id="99e1e-326">Replace `clustername` with the HBase cluster name.</span></span>

2. <span data-ttu-id="99e1e-327">En la sesión SSH, inicie el shell de HBase.</span><span class="sxs-lookup"><span data-stu-id="99e1e-327">From the SSH session, start the HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="99e1e-328">Una vez cargado el shell, verá un símbolo del sistema de `hbase(main):001:0>`.</span><span class="sxs-lookup"><span data-stu-id="99e1e-328">Once the shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="99e1e-329">Vea las filas de la tabla:</span><span class="sxs-lookup"><span data-stu-id="99e1e-329">View rows from the table:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="99e1e-330">Este comando devuelve información similar al siguiente texto, que indica que hay datos en la tabla.</span><span class="sxs-lookup"><span data-stu-id="99e1e-330">This command returns information similar to the following text, indicating that there is data in the table.</span></span>
   
        hbase(main):002:0> scan 'SensorData'
        ROW                             COLUMN+CELL
        \x00\x00\x00\x00               column=cf:temperature, timestamp=1467290788277, value=\x00\x00\x00\x04
        \x00\x00\x00\x00               column=cf:timestamp, timestamp=1467290788277, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x01               column=cf:temperature, timestamp=1467290788348, value=\x00\x00\x00M
        \x00\x00\x00\x01               column=cf:timestamp, timestamp=1467290788348, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x02               column=cf:temperature, timestamp=1467290788268, value=\x00\x00\x00R
        \x00\x00\x00\x02               column=cf:timestamp, timestamp=1467290788268, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x03               column=cf:temperature, timestamp=1467290788269, value=\x00\x00\x00#
        \x00\x00\x00\x03               column=cf:timestamp, timestamp=1467290788269, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x04               column=cf:temperature, timestamp=1467290788356, value=\x00\x00\x00>
        \x00\x00\x00\x04               column=cf:timestamp, timestamp=1467290788356, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x05               column=cf:temperature, timestamp=1467290788326, value=\x00\x00\x00\x0D
        \x00\x00\x00\x05               column=cf:timestamp, timestamp=1467290788326, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x06               column=cf:temperature, timestamp=1467290788253, value=\x00\x00\x009
        \x00\x00\x00\x06               column=cf:timestamp, timestamp=1467290788253, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x07               column=cf:temperature, timestamp=1467290788229, value=\x00\x00\x00\x12
        \x00\x00\x00\x07               column=cf:timestamp, timestamp=1467290788229, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x08               column=cf:temperature, timestamp=1467290788336, value=\x00\x00\x00\x16
        \x00\x00\x00\x08               column=cf:timestamp, timestamp=1467290788336, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x09               column=cf:temperature, timestamp=1467290788246, value=\x00\x00\x001
        \x00\x00\x00\x09               column=cf:timestamp, timestamp=1467290788246, value=2015-02-10T14:43.05.00320Z
        10 row(s) in 0.1800 seconds
   
   > [!NOTE]
   > <span data-ttu-id="99e1e-331">Esta operación de detección solo devuelve un máximo de 10 filas de la tabla.</span><span class="sxs-lookup"><span data-stu-id="99e1e-331">This scan operation returns a maximum of 10 rows from the table.</span></span>

## <a name="delete-your-clusters"></a><span data-ttu-id="99e1e-332">Eliminación de los clústeres</span><span class="sxs-lookup"><span data-stu-id="99e1e-332">Delete your clusters</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="99e1e-333">Para eliminar los clústeres, el almacenamiento y la aplicación web al mismo tiempo, elimine el grupo de recursos que los contiene.</span><span class="sxs-lookup"><span data-stu-id="99e1e-333">To delete the clusters, storage, and web app at one time, delete the resource group that contains them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99e1e-334">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="99e1e-334">Next steps</span></span>

<span data-ttu-id="99e1e-335">Para obtener más ejemplos de topologías de Storm con HDInsight, vea [Topologías y componentes de ejemplo de Storm para Apache Storm en HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="99e1e-335">For more examples of Storm topologies with HDInsight, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md)</span></span>

<span data-ttu-id="99e1e-336">Para obtener más información sobre Apache Storm, consulte el sitio de [Apache Storm](https://storm.incubator.apache.org/) .</span><span class="sxs-lookup"><span data-stu-id="99e1e-336">For more information about Apache Storm, see the [Apache Storm](https://storm.incubator.apache.org/) site.</span></span>

<span data-ttu-id="99e1e-337">Para obtener más información sobre HBase con HDInsight, consulte [Información general de HBase de HDInsight](hdinsight-hbase-overview.md).</span><span class="sxs-lookup"><span data-stu-id="99e1e-337">For more information about HBase on HDInsight, see the [HBase with HDInsight Overview](hdinsight-hbase-overview.md).</span></span>

<span data-ttu-id="99e1e-338">Para obtener más información sobre Socket.io, consulte el sitio de [socket.io](http://socket.io/) .</span><span class="sxs-lookup"><span data-stu-id="99e1e-338">For more information about Socket.io, see the [socket.io](http://socket.io/) site.</span></span>

<span data-ttu-id="99e1e-339">Para obtener más información sobre D3.js, consulte [D3.js: documentos controlados por datos](http://d3js.org/).</span><span class="sxs-lookup"><span data-stu-id="99e1e-339">For more information about D3.js, see [D3.js - Data Driven Documents](http://d3js.org/).</span></span>

<span data-ttu-id="99e1e-340">Para obtener información sobre la creación de topologías en Java, consulte [Desarrollo de topologías de Java para Apache Storm en HDInsight](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="99e1e-340">For information about creating topologies in Java, see [Develop Java topologies for Apache Storm on HDInsight](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="99e1e-341">Para obtener información sobre la creación de topologías en .NET, consulte [Desarrollo de topologías de C# para Apache Storm en HDInsight mediante Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="99e1e-341">For information about creating topologies in .NET, see [Develop C# topologies for Apache Storm on HDInsight using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

[azure-portal]: https://portal.azure.com
