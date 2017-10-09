---
title: datos del sensor aaaAnalyze con Apache Storm y HBase | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconnect tooApache Storm con una red virtual. Usar Storm con los datos de sensor de HBase tooprocess de un centro de eventos y visualizar con D3.js."
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
ms.openlocfilehash: e54fe9ffc720b0089f90e302b24a9438bd43999a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a><span data-ttu-id="e5117-104">Análisis de datos de sensores con Apache Storm, Centro de eventos y HBase en HDInsight (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="e5117-104">Analyze sensor data with Apache Storm, Event Hub, and HBase in HDInsight (Hadoop)</span></span>

<span data-ttu-id="e5117-105">Obtenga información acerca de cómo toouse Apache Storm en los datos de sensor tooprocess de HDInsight de concentrador de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="e5117-105">Learn how toouse Apache Storm on HDInsight tooprocess sensor data from Azure Event Hub.</span></span> <span data-ttu-id="e5117-106">datos de Hello, a continuación, se almacenan en Apache HBase en HDInsight y visualizan mediante D3.js.</span><span class="sxs-lookup"><span data-stu-id="e5117-106">hello data is then stored into Apache HBase on HDInsight, and visualized using D3.js.</span></span>

<span data-ttu-id="e5117-107">plantilla de Azure Resource Manager Hola usado en este documento se muestra cómo toocreate varios recursos de Azure en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e5117-107">hello Azure Resource Manager template used in this document demonstrates how toocreate multiple Azure resources in a resource group.</span></span> <span data-ttu-id="e5117-108">plantilla de Hello crea una red Virtual de Azure, dos clústeres de HDInsight (Storm y HBase) y una aplicación Web de Azure.</span><span class="sxs-lookup"><span data-stu-id="e5117-108">hello template creates an Azure Virtual Network, two HDInsight clusters (Storm and HBase) and an Azure Web App.</span></span> <span data-ttu-id="e5117-109">Una implementación de node.js de un panel web en tiempo real está implementado automáticamente toohello web app.</span><span class="sxs-lookup"><span data-stu-id="e5117-109">A node.js implementation of a real-time web dashboard is automatically deployed toohello web app.</span></span>

> [!NOTE]
> <span data-ttu-id="e5117-110">información de Hello en el documento y el ejemplo de este documento requieren HDInsight versión 3.6.</span><span class="sxs-lookup"><span data-stu-id="e5117-110">hello information in this document and example in this document require HDInsight version 3.6.</span></span>
>
> <span data-ttu-id="e5117-111">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="e5117-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e5117-112">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="e5117-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5117-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e5117-113">Prerequisites</span></span>

* <span data-ttu-id="e5117-114">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="e5117-114">An Azure subscription.</span></span>
* <span data-ttu-id="e5117-115">[Node.js](http://nodejs.org/): panel de toopreview usado hello web localmente en el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="e5117-115">[Node.js](http://nodejs.org/): Used toopreview hello web dashboard locally on your development environment.</span></span>
* <span data-ttu-id="e5117-116">[Hello JDK 1.7 y Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html): usar topología de Storm hello toodevelop.</span><span class="sxs-lookup"><span data-stu-id="e5117-116">[Java and hello JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): Used toodevelop hello Storm topology.</span></span>
* <span data-ttu-id="e5117-117">[Maven](http://maven.apache.org/what-is-maven.html): proyecto de hello toobuild y compilación utilizado.</span><span class="sxs-lookup"><span data-stu-id="e5117-117">[Maven](http://maven.apache.org/what-is-maven.html): Used toobuild and compile hello project.</span></span>
* <span data-ttu-id="e5117-118">[GIT](http://git-scm.com/): proyecto de hello toodownload usado desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="e5117-118">[Git](http://git-scm.com/): Used toodownload hello project from GitHub.</span></span>
* <span data-ttu-id="e5117-119">Un **SSH** cliente: usar clústeres de HDInsight basados en Linux toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="e5117-119">An **SSH** client: Used tooconnect toohello Linux-based HDInsight clusters.</span></span> <span data-ttu-id="e5117-120">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e5117-120">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="e5117-121">No necesita un clúster existente de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5117-121">You do not need an existing HDInsight cluster.</span></span> <span data-ttu-id="e5117-122">pasos de Hello en este documento para crear Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e5117-122">hello steps in this document create hello following resources:</span></span>
> 
> * <span data-ttu-id="e5117-123">Una red virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="e5117-123">An Azure Virtual Network</span></span>
> * <span data-ttu-id="e5117-124">Un clúster de Storm en HDInsight (dos nodos de trabajo basados en Linux)</span><span class="sxs-lookup"><span data-stu-id="e5117-124">A Storm on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="e5117-125">Un clúster de HBase en HDInsight (dos nodos de trabajo basados en Linux)</span><span class="sxs-lookup"><span data-stu-id="e5117-125">An HBase on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="e5117-126">Una aplicación Web de Azure que hospeda el panel de hello web</span><span class="sxs-lookup"><span data-stu-id="e5117-126">An Azure Web App that hosts hello web dashboard</span></span>

## <a name="architecture"></a><span data-ttu-id="e5117-127">Arquitectura</span><span class="sxs-lookup"><span data-stu-id="e5117-127">Architecture</span></span>

![diagrama de arquitectura](./media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

<span data-ttu-id="e5117-129">Este ejemplo consta de Hola de los componentes siguientes:</span><span class="sxs-lookup"><span data-stu-id="e5117-129">This example consists of hello following components:</span></span>

* <span data-ttu-id="e5117-130">**Centros de eventos de Azure**: contiene datos que se recopilan de los sensores.</span><span class="sxs-lookup"><span data-stu-id="e5117-130">**Azure Event Hubs**: Contains data that is collected from sensors.</span></span>
* <span data-ttu-id="e5117-131">**Storm en HDInsight**: ofrece procesamiento en tiempo real de datos desde el Centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="e5117-131">**Storm on HDInsight**: Provides real-time processing of data from Event Hub.</span></span>
* <span data-ttu-id="e5117-132">**HBase en HDInsight**: proporciona un almacén de datos NoSQL persistente para los datos después de haberse procesado en Storm.</span><span class="sxs-lookup"><span data-stu-id="e5117-132">**HBase on HDInsight**: Provides a persistent NoSQL data store for data after it has been processed by Storm.</span></span>
* <span data-ttu-id="e5117-133">**Servicio de red Virtual de Azure**: permite proteger las comunicaciones entre hello Storm en HDInsight y HBase en clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5117-133">**Azure Virtual Network service**: Enables secure communications between hello Storm on HDInsight and HBase on HDInsight clusters.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="e5117-134">Una red virtual se requiere cuando se usa la API de cliente de hello HBase de Java.</span><span class="sxs-lookup"><span data-stu-id="e5117-134">A virtual network is required when using hello Java HBase client API.</span></span> <span data-ttu-id="e5117-135">No se expone a través de puerta de enlace pública de Hola para clústeres de HBase.</span><span class="sxs-lookup"><span data-stu-id="e5117-135">It is not exposed over hello public gateway for HBase clusters.</span></span> <span data-ttu-id="e5117-136">Clústeres de HBase instalación y Storm en hello misma red virtual permite Hola clúster de Storm (o cualquier otro sistema en la red virtual de hello) toodirectly tener acceso a HBase mediante la API de cliente.</span><span class="sxs-lookup"><span data-stu-id="e5117-136">Installing HBase and Storm clusters into hello same virtual network allows hello Storm cluster (or any other system on hello virtual network) toodirectly access HBase using client API.</span></span>

* <span data-ttu-id="e5117-137">**Sitio web del panel**: un panel de ejemplo que muestra datos en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="e5117-137">**Dashboard website**: An example dashboard that charts data in real time.</span></span>
  
  * <span data-ttu-id="e5117-138">sitio Web de Hola se implementa en Node.js.</span><span class="sxs-lookup"><span data-stu-id="e5117-138">hello website is implemented in Node.js.</span></span>
  * <span data-ttu-id="e5117-139">[Socket.IO](http://socket.io/) se utiliza para la comunicación en tiempo real entre topología aluvión de Hola y Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-139">[Socket.io](http://socket.io/) is used for real-time communication between hello Storm topology and hello website.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="e5117-140">Usar Socket.io para comunicaciones es un detalle de implementación.</span><span class="sxs-lookup"><span data-stu-id="e5117-140">Using Socket.io for communication is an implementation detail.</span></span> <span data-ttu-id="e5117-141">Puede usar cualquier marco de comunicaciones, como SignalR o WebSockets sin procesar.</span><span class="sxs-lookup"><span data-stu-id="e5117-141">You can use any communications framework, such as raw WebSockets or SignalR.</span></span>

  * <span data-ttu-id="e5117-142">[D3.js](http://d3js.org/) toograph usado Hola datos que se envía el sitio Web de toohello.</span><span class="sxs-lookup"><span data-stu-id="e5117-142">[D3.js](http://d3js.org/) is used toograph hello data that is sent toohello website.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e5117-143">Dos clústeres son necesarios, ya que no existe ningún método admitido toocreate un HDInsight clúster de Storm y HBase.</span><span class="sxs-lookup"><span data-stu-id="e5117-143">Two clusters are required, as there is no supported method toocreate one HDInsight cluster for both Storm and HBase.</span></span>

<span data-ttu-id="e5117-144">Hello topología lee datos desde el concentrador de eventos mediante hello [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) clase y escribe los datos en HBase mediante hello [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) clase.</span><span class="sxs-lookup"><span data-stu-id="e5117-144">hello topology reads data from Event Hub by using hello [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) class, and writes data into HBase using hello [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) class.</span></span> <span data-ttu-id="e5117-145">Comunicación con el sitio Web de Hola se logra mediante [socket.io client.java](https://github.com/nkzawa/socket.io-client.java).</span><span class="sxs-lookup"><span data-stu-id="e5117-145">Communication with hello website is accomplished by using [socket.io-client.java](https://github.com/nkzawa/socket.io-client.java).</span></span>

<span data-ttu-id="e5117-146">Hola después diagrama explica diseño Hola de topología de hello:</span><span class="sxs-lookup"><span data-stu-id="e5117-146">hello following diagram explains hello layout of hello topology:</span></span>

![diagrama de topología](./media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> <span data-ttu-id="e5117-148">Este diagrama es una vista simplificada de topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-148">This diagram is a simplified view of hello topology.</span></span> <span data-ttu-id="e5117-149">Por cada partición del Centro de eventos se crea una instancia de cada componente.</span><span class="sxs-lookup"><span data-stu-id="e5117-149">An instance of each component is created for each partition in your Event Hub.</span></span> <span data-ttu-id="e5117-150">Estas instancias se distribuyen en nodos de hello en clúster de Hola y datos se enrutan entre ellos los siguientes:</span><span class="sxs-lookup"><span data-stu-id="e5117-150">These instances are distributed across hello nodes in hello cluster, and data is routed between them as follows:</span></span>
> 
> * <span data-ttu-id="e5117-151">Datos del analizador de hello pitorro toohello tiene una carga equilibrada.</span><span class="sxs-lookup"><span data-stu-id="e5117-151">Data from hello spout toohello parser is load balanced.</span></span>
> * <span data-ttu-id="e5117-152">Datos de hello analizador toohello panel y HBase están agrupados por Id. de dispositivo, para que los mensajes de Hola mismo dispositivo siempre flujo toohello mismo componente.</span><span class="sxs-lookup"><span data-stu-id="e5117-152">Data from hello parser toohello Dashboard and HBase is grouped by Device ID, so that messages from hello same device always flow toohello same component.</span></span>

### <a name="topology-components"></a><span data-ttu-id="e5117-153">Componentes de la topología</span><span class="sxs-lookup"><span data-stu-id="e5117-153">Topology components</span></span>

* <span data-ttu-id="e5117-154">**Concentrador de eventos apetezca charlar**: pitorro Hola se proporciona como parte de la versión de Apache Storm 0.10.0 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="e5117-154">**Event Hub Spout**: hello spout is provided as part of Apache Storm version 0.10.0 and higher.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="e5117-155">pitorro de concentrador de eventos de Hello utilizado en este ejemplo requiere una tormenta de la versión de clúster de HDInsight 3.5 o 3.6.</span><span class="sxs-lookup"><span data-stu-id="e5117-155">hello Event Hub spout used in this example requires a Storm on HDInsight cluster version 3.5 or 3.6.</span></span>

* <span data-ttu-id="e5117-156">**ParserBolt.java**: Hola datos que se emiten por pitorro Hola JSON sin formato y en ocasiones más de un evento se genera cada vez.</span><span class="sxs-lookup"><span data-stu-id="e5117-156">**ParserBolt.java**: hello data that is emitted by hello spout is raw JSON, and occasionally more than one event is emitted at a time.</span></span> <span data-ttu-id="e5117-157">Este rayo lee datos Hola emitidos por hello apetezca charlar y analiza el mensaje de bienvenida de JSON.</span><span class="sxs-lookup"><span data-stu-id="e5117-157">This bolt reads hello data emitted by hello spout and parses hello JSON message.</span></span> <span data-ttu-id="e5117-158">tornillo de Hello, a continuación, emite los datos de hello como una tupla que contiene varios campos.</span><span class="sxs-lookup"><span data-stu-id="e5117-158">hello bolt then emits hello data as a tuple that contains multiple fields.</span></span>
* <span data-ttu-id="e5117-159">**DashboardBolt.java**: este componente muestra cómo toouse Hola Socket.io biblioteca de cliente para los datos de toosend de Java en el panel en tiempo real toohello web.</span><span class="sxs-lookup"><span data-stu-id="e5117-159">**DashboardBolt.java**: This component demonstrates how toouse hello Socket.io client library for Java toosend data in real time toohello web dashboard.</span></span>
* <span data-ttu-id="e5117-160">**no hbase.yaml**: Hola definición de topología que se usa cuando se ejecuta en modo local.</span><span class="sxs-lookup"><span data-stu-id="e5117-160">**no-hbase.yaml**: hello topology definition used when running in local mode.</span></span> <span data-ttu-id="e5117-161">No usa componentes de HBase.</span><span class="sxs-lookup"><span data-stu-id="e5117-161">It does not use HBase components.</span></span>
* <span data-ttu-id="e5117-162">**con hbase.yaml**: Hola definición de topología que se usa al ejecutar la topología de hello en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-162">**with-hbase.yaml**: hello topology definition used when running hello topology on hello cluster.</span></span> <span data-ttu-id="e5117-163">Usa componentes de HBase.</span><span class="sxs-lookup"><span data-stu-id="e5117-163">It does use HBase components.</span></span>
* <span data-ttu-id="e5117-164">**dev.Properties**: Hola información de configuración para pitorro de concentrador de eventos de hello, HBase rayo y componentes de panel.</span><span class="sxs-lookup"><span data-stu-id="e5117-164">**dev.properties**: hello configuration information for hello Event Hub spout, HBase bolt, and dashboard components.</span></span>

## <a name="prepare-your-environment"></a><span data-ttu-id="e5117-165">Preparación del entorno</span><span class="sxs-lookup"><span data-stu-id="e5117-165">Prepare your environment</span></span>

<span data-ttu-id="e5117-166">Antes de utilizar este ejemplo, debe crear un concentrador de eventos de Azure, lee qué topología de Storm Hola de.</span><span class="sxs-lookup"><span data-stu-id="e5117-166">Before you use this example, you must create an Azure Event Hub, which hello Storm topology reads from.</span></span>

### <a name="configure-event-hub"></a><span data-ttu-id="e5117-167">Configuración del centro de eventos</span><span class="sxs-lookup"><span data-stu-id="e5117-167">Configure Event Hub</span></span>

<span data-ttu-id="e5117-168">Centro de eventos es el origen de datos de Hola para este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e5117-168">Event Hub is hello data source for this example.</span></span> <span data-ttu-id="e5117-169">Usar hello siguiendo los pasos toocreate un concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="e5117-169">Use hello following steps toocreate an Event Hub.</span></span>

1. <span data-ttu-id="e5117-170">De hello [portal de Azure](https://portal.azure.com), seleccione **+ nuevo** -> **Internet de las cosas** -> **centros de eventos**.</span><span class="sxs-lookup"><span data-stu-id="e5117-170">From hello [Azure portal](https://portal.azure.com), select **+ New** -> **Internet of Things** -> **Event Hubs**.</span></span>
2. <span data-ttu-id="e5117-171">Hola **crear Namespace** sección, lleve a cabo Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="e5117-171">In hello **Create Namespace** section, perform hello following tasks:</span></span>
   
   1. <span data-ttu-id="e5117-172">Escriba un **nombre** para el espacio de nombres de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-172">Enter a **Name** for hello namespace.</span></span>
   2. <span data-ttu-id="e5117-173">Seleccione un plan de tarifa.</span><span class="sxs-lookup"><span data-stu-id="e5117-173">Select a pricing tier.</span></span> <span data-ttu-id="e5117-174">**Básico** es suficiente para este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e5117-174">**Basic** is sufficient for this example.</span></span>
   3. <span data-ttu-id="e5117-175">Seleccione hello Azure **suscripción** toouse.</span><span class="sxs-lookup"><span data-stu-id="e5117-175">Select hello Azure **Subscription** toouse.</span></span>
   4. <span data-ttu-id="e5117-176">Seleccione un grupo de recursos existente o cree uno.</span><span class="sxs-lookup"><span data-stu-id="e5117-176">Either select an existing resource group or create a new one.</span></span>
   5. <span data-ttu-id="e5117-177">Seleccione hello **ubicación** para hello concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="e5117-177">Select hello **Location** for hello Event Hub.</span></span>
   6. <span data-ttu-id="e5117-178">Seleccione **Pin toodashboard**y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="e5117-178">Select **Pin toodashboard**, and then click **Create**.</span></span>

3. <span data-ttu-id="e5117-179">Cuando se completa el proceso de creación de hello, se muestra información de los centros de eventos para el espacio de nombres de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-179">When hello creation process completes, hello Event Hubs information for your namespace is displayed.</span></span> <span data-ttu-id="e5117-180">Desde ahí, seleccione **+ Agregar Centro de eventos**.</span><span class="sxs-lookup"><span data-stu-id="e5117-180">From here, select **+ Add Event Hub**.</span></span> <span data-ttu-id="e5117-181">Hola **crear centro de eventos** sección, escriba un nombre de **sensordata**y, a continuación, seleccione **crear**.</span><span class="sxs-lookup"><span data-stu-id="e5117-181">In hello **Create Event Hub** section, enter a name of **sensordata**, and then select **Create**.</span></span> <span data-ttu-id="e5117-182">Deje Hola otros campos en los valores predeterminados de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-182">Leave hello other fields at hello default values.</span></span>
4. <span data-ttu-id="e5117-183">Hola los centros de eventos permite ver el espacio de nombres, seleccione **centros de eventos**.</span><span class="sxs-lookup"><span data-stu-id="e5117-183">From hello Event Hubs view for your namespace, select **Event Hubs**.</span></span> <span data-ttu-id="e5117-184">Seleccione hello **sensordata** entrada.</span><span class="sxs-lookup"><span data-stu-id="e5117-184">Select hello **sensordata** entry.</span></span>
5. <span data-ttu-id="e5117-185">En hello sensordata concentrador de eventos, seleccione **directivas de acceso compartido**.</span><span class="sxs-lookup"><span data-stu-id="e5117-185">From hello sensordata Event Hub, select **Shared access policies**.</span></span> <span data-ttu-id="e5117-186">Hola de uso **+ agregar** Hola de vínculo tooadd las siguientes directivas:</span><span class="sxs-lookup"><span data-stu-id="e5117-186">Use hello **+ Add** link tooadd hello following policies:</span></span>

    | <span data-ttu-id="e5117-187">Nombre de la directiva</span><span class="sxs-lookup"><span data-stu-id="e5117-187">Policy name</span></span> | <span data-ttu-id="e5117-188">Notificaciones</span><span class="sxs-lookup"><span data-stu-id="e5117-188">Claims</span></span> |
    | ----- | ----- |
    | <span data-ttu-id="e5117-189">devices</span><span class="sxs-lookup"><span data-stu-id="e5117-189">devices</span></span> | <span data-ttu-id="e5117-190">Enviar</span><span class="sxs-lookup"><span data-stu-id="e5117-190">Send</span></span> |
    | <span data-ttu-id="e5117-191">storm</span><span class="sxs-lookup"><span data-stu-id="e5117-191">storm</span></span> | <span data-ttu-id="e5117-192">Escuchar</span><span class="sxs-lookup"><span data-stu-id="e5117-192">Listen</span></span> |

1. <span data-ttu-id="e5117-193">Seleccione las dos directivas y tome nota de hello **PRIMARY KEY** valor.</span><span class="sxs-lookup"><span data-stu-id="e5117-193">Select both policies and make a note of hello **PRIMARY KEY** value.</span></span> <span data-ttu-id="e5117-194">Se necesita el valor de Hola para ambas directivas en pasos futuros.</span><span class="sxs-lookup"><span data-stu-id="e5117-194">You need hello value for both policies in future steps.</span></span>

## <a name="download-and-configure-hello-project"></a><span data-ttu-id="e5117-195">Descargar y configurar el proyecto de Hola</span><span class="sxs-lookup"><span data-stu-id="e5117-195">Download and configure hello project</span></span>

<span data-ttu-id="e5117-196">Usar hello siguiendo el proyecto de hello toodownload de GitHub.</span><span class="sxs-lookup"><span data-stu-id="e5117-196">Use hello following toodownload hello project from GitHub.</span></span>

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

<span data-ttu-id="e5117-197">Una vez completado el comando de hello, deberá Hola siguiendo la estructura de directorios:</span><span class="sxs-lookup"><span data-stu-id="e5117-197">After hello command completes, you have hello following directory structure:</span></span>

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains hello topology
            resources/
                log4j2.xml - set logging toominimal.
                no-hbase.yaml - topology definition without hbase components.
                with-hbase.yaml - topology definition with hbase components.
            src/main/java/com/microsoft/examples/bolts/
                ParserBolt.java - parses JSON data into tuples
                DashboardBolt.java - sends data over Socket.IO toohello web dashboard.
        dashboard/nodejs/ - this is hello node.js web dashboard.
        SendEvents/ - utilities toosend fake sensor data.

> [!NOTE]
> <span data-ttu-id="e5117-198">Este documento no entra en detalles de toofull de código de hello incluido en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e5117-198">This document does not go in toofull details of hello code included in this example.</span></span> <span data-ttu-id="e5117-199">Sin embargo, el código de hello totalmente se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="e5117-199">However, hello code is fully commented.</span></span>

<span data-ttu-id="e5117-200">tooconfigure Hola proyecto tooread de concentrador de eventos, abra hello `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` de archivos y agregar su toohello de información de concentrador de eventos siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="e5117-200">tooconfigure hello project tooread from Event Hub, open hello `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` file and add your Event Hub information toohello following lines:</span></span>

```bash
eventhub.read.policy.name: your_read_policy_name
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: your_event_hub_name
eventhub.partitions: 2
```

## <a name="compile-and-test-locally"></a><span data-ttu-id="e5117-201">Compilación y pruebas locales</span><span class="sxs-lookup"><span data-stu-id="e5117-201">Compile and test locally</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e5117-202">Con la topología de hello localmente, requiere un entorno de desarrollo de Storm en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="e5117-202">Using hello topology locally requires a working Storm development environment.</span></span> <span data-ttu-id="e5117-203">Para más información, consulte [Setting up a development environment](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) (Configuración de un entorno de desarrollo) en Apache.org.</span><span class="sxs-lookup"><span data-stu-id="e5117-203">For more information, see [Setting up a Storm development environment](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) at Apache.org.</span></span>

> [!WARNING]
> <span data-ttu-id="e5117-204">Si está utilizando un entorno de desarrollo de Windows, puede recibir un `java.io.IOException` cuando se ejecuta localmente topología Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-204">If you are using a Windows development environment, you may receive a `java.io.IOException` when running hello topology locally.</span></span> <span data-ttu-id="e5117-205">Si es así, mueva topología de hello toorunning en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5117-205">If so, move on toorunning hello topology on HDInsight.</span></span>

<span data-ttu-id="e5117-206">Antes de probar, debe iniciar Hola panel tooview Hola salida de topología de Hola y generar datos toostore en el concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="e5117-206">Before testing, you must start hello dashboard tooview hello output of hello topology and generate data toostore in Event Hub.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e5117-207">componente de HBase Hola de esta topología no está activa cuando se prueba localmente.</span><span class="sxs-lookup"><span data-stu-id="e5117-207">hello HBase component of this topology is not active when testing locally.</span></span> <span data-ttu-id="e5117-208">Hola API Java para el clúster de HBase Hola no son accesibles desde el exterior Hola red Virtual de Azure que contiene los clústeres de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-208">hello Java API for hello HBase cluster cannot be accessed from outside hello Azure Virtual Network that contains hello clusters.</span></span>

### <a name="start-hello-web-application"></a><span data-ttu-id="e5117-209">Iniciar la aplicación web de hello</span><span class="sxs-lookup"><span data-stu-id="e5117-209">Start hello web application</span></span>

1. <span data-ttu-id="e5117-210">Abra un símbolo del sistema y cambie los directorios demasiado`hdinsight-eventhub-example/dashboard`.</span><span class="sxs-lookup"><span data-stu-id="e5117-210">Open a command prompt and change directories too`hdinsight-eventhub-example/dashboard`.</span></span> <span data-ttu-id="e5117-211">Usar hello después dependencias Hola comando tooinstall que sea necesarios mediante la aplicación web de hello:</span><span class="sxs-lookup"><span data-stu-id="e5117-211">Use hello following command tooinstall hello dependencies needed by hello web application:</span></span>
   
    ```bash
    npm install
    ```

2. <span data-ttu-id="e5117-212">Usar hello tras la aplicación web de comando toostart hello:</span><span class="sxs-lookup"><span data-stu-id="e5117-212">Use hello following command toostart hello web application:</span></span>
   
    ```bash
    node server.js
    ```
   
    <span data-ttu-id="e5117-213">Vea un toohello similar de mensaje siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="e5117-213">You see a message similar toohello following text:</span></span>
   
        Server listening at port 3000

3. <span data-ttu-id="e5117-214">Abra un explorador web y escriba `http://localhost:3000/` como dirección de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-214">Open a web browser and enter `http://localhost:3000/` as hello address.</span></span> <span data-ttu-id="e5117-215">Se muestra un toohello similar de página después de la imagen:</span><span class="sxs-lookup"><span data-stu-id="e5117-215">A page similar toohello following image is displayed:</span></span>
   
    ![panel web](./media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    <span data-ttu-id="e5117-217">Deje abierto este símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="e5117-217">Leave this command prompt open.</span></span> <span data-ttu-id="e5117-218">Después de realizar pruebas, usar servidor web de Ctrl-C toostop Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-218">After testing, use Ctrl-C toostop hello web server.</span></span>

### <a name="generate-data"></a><span data-ttu-id="e5117-219">Generación de datos</span><span class="sxs-lookup"><span data-stu-id="e5117-219">Generate data</span></span>

> [!NOTE]
> <span data-ttu-id="e5117-220">Hello pasos de esta sección usan Node.js para que pueden usarse en cualquier plataforma.</span><span class="sxs-lookup"><span data-stu-id="e5117-220">hello steps in this section use Node.js so that they can be used on any platform.</span></span> <span data-ttu-id="e5117-221">Para obtener ejemplos de idioma, vea hello `SendEvents` directory.</span><span class="sxs-lookup"><span data-stu-id="e5117-221">For other language examples, see hello `SendEvents` directory.</span></span>

1. <span data-ttu-id="e5117-222">Abra un nuevo símbolo del sistema, el shell o terminal y cambie los directorios demasiado`hdinsight-eventhub-example/SendEvents/nodejs`.</span><span class="sxs-lookup"><span data-stu-id="e5117-222">Open a new prompt, shell, or terminal, and change directories too`hdinsight-eventhub-example/SendEvents/nodejs`.</span></span> <span data-ttu-id="e5117-223">dependencias de hello tooinstall aplicación Hola, necesarios usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e5117-223">tooinstall hello dependencies needed by hello application, use hello following command:</span></span>

    ```bash
    npm install
    ```

2. <span data-ttu-id="e5117-224">Abra hello `app.js` un archivo en un editor de texto y agregue Hola información de concentrador de eventos ha obtenido antes:</span><span class="sxs-lookup"><span data-stu-id="e5117-224">Open hello `app.js` file in a text editor and add hello Event Hub information you obtained earlier:</span></span>
   
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
   > <span data-ttu-id="e5117-225">En este ejemplo se da por supuesto que ha usado `sensordata` como nombre de Hola de su centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="e5117-225">This example assumes that you have used `sensordata` as hello name of your Event Hub.</span></span> <span data-ttu-id="e5117-226">Y que `devices` como nombre de Hola de directiva de Hola que tiene un `Send` de notificación.</span><span class="sxs-lookup"><span data-stu-id="e5117-226">And that `devices` as hello name of hello policy that has a `Send` claim.</span></span>

3. <span data-ttu-id="e5117-227">Usar hello después comando tooinsert las nuevas entradas de concentrador de eventos:</span><span class="sxs-lookup"><span data-stu-id="e5117-227">Use hello following command tooinsert new entries in Event Hub:</span></span>
   
    ```bash
    node app.js
    ```
   
    <span data-ttu-id="e5117-228">Ve varias líneas de salida que contienen datos de hello envían tooEvent concentrador:</span><span class="sxs-lookup"><span data-stu-id="e5117-228">You see several lines of output that contain hello data sent tooEvent Hub:</span></span>
   
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

### <a name="build-and-start-hello-topology"></a><span data-ttu-id="e5117-229">Compile y comience la topología de Hola</span><span class="sxs-lookup"><span data-stu-id="e5117-229">Build and start hello topology</span></span>

1. <span data-ttu-id="e5117-230">Abra un símbolo del sistema nuevo y cambie los directorios demasiado`hdinsight-eventhub-example/TemperatureMonitor`.</span><span class="sxs-lookup"><span data-stu-id="e5117-230">Open a new command prompt and change directories too`hdinsight-eventhub-example/TemperatureMonitor`.</span></span> <span data-ttu-id="e5117-231">toobuild y paquete Hola topología, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e5117-231">toobuild and package hello topology, use hello following command:</span></span> 

    ```bash
    mvn clean package
    ```

2. <span data-ttu-id="e5117-232">toostart Hola topología en modo local, usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e5117-232">toostart hello topology in local mode, use hello following command:</span></span>

    ```bash
    storm jar target/TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local --filter dev.properties resources/no-hbase.yaml
    ```

    * <span data-ttu-id="e5117-233">`--local`topología de Hola se inicia en modo local.</span><span class="sxs-lookup"><span data-stu-id="e5117-233">`--local` starts hello topology in local mode.</span></span>
    * <span data-ttu-id="e5117-234">`--filter`hello usa `dev.properties` toopopulate parámetros de archivo de definición de la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-234">`--filter` uses hello `dev.properties` file toopopulate parameters in hello topology definition.</span></span>
    * <span data-ttu-id="e5117-235">`resources/no-hbase.yaml`hello usa `no-hbase.yaml` definición de topología.</span><span class="sxs-lookup"><span data-stu-id="e5117-235">`resources/no-hbase.yaml` uses hello `no-hbase.yaml` topology definition.</span></span>
 
   <span data-ttu-id="e5117-236">Una vez iniciado, topología Hola lee las entradas de concentrador de eventos y los envía panel toohello ejecutando en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="e5117-236">Once started, hello topology reads entries from Event Hub, and sends them toohello dashboard running on your local machine.</span></span> <span data-ttu-id="e5117-237">Debe ver líneas aparezcan en el panel de hello web, similar toohello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="e5117-237">You should see lines appear in hello web dashboard, similar toohello following image:</span></span>
   
    ![panel con datos](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. <span data-ttu-id="e5117-239">Mientras se ejecuta el panel de hello, usar hello `node app.js` toosend nuevos datos tooEvent centros de los pasos del comando de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="e5117-239">While hello dashboard is running, use hello `node app.js` command from hello previous steps toosend new data tooEvent Hubs.</span></span> <span data-ttu-id="e5117-240">Dado que los valores de temperatura de Hola se generan de forma aleatoria, gráfico de hello debe actualizar tooshow grandes cambios de temperatura.</span><span class="sxs-lookup"><span data-stu-id="e5117-240">Because hello temperature values are randomly generated, hello graph should update tooshow large changes in temperature.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e5117-241">Debe estar en hello **hdinsight-eventhub-ejemplo/SendEvents/Nodejs** directory al utilizar hello `node app.js` comando.</span><span class="sxs-lookup"><span data-stu-id="e5117-241">You must be in hello **hdinsight-eventhub-example/SendEvents/Nodejs** directory when using hello `node app.js` command.</span></span>

3. <span data-ttu-id="e5117-242">Después de comprobar las actualizaciones de ese panel hello, stop Hola topología mediante Ctrl + C.</span><span class="sxs-lookup"><span data-stu-id="e5117-242">After verifying that hello dashboard updates, stop hello topology using Ctrl+C.</span></span> <span data-ttu-id="e5117-243">También puede utilizar el servidor web local de Ctrl + C toostop Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-243">You can use Ctrl+C toostop hello local web server also.</span></span>

## <a name="create-a-storm-and-hbase-cluster"></a><span data-ttu-id="e5117-244">Creación de un clúster de Storm y HBase</span><span class="sxs-lookup"><span data-stu-id="e5117-244">Create a Storm and HBase cluster</span></span>

<span data-ttu-id="e5117-245">Hola los pasos de esta sección utilizan un [plantilla de Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) toocreate un clúster de red Virtual de Azure y una tormenta y HBase en red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-245">hello steps in this section use an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) toocreate an Azure Virtual Network and a Storm and HBase cluster on hello virtual network.</span></span> <span data-ttu-id="e5117-246">plantilla de Hello también crea una aplicación Web de Azure e implementa una copia del panel de hello en él.</span><span class="sxs-lookup"><span data-stu-id="e5117-246">hello template also creates an Azure Web App and deploys a copy of hello dashboard into it.</span></span>

> [!NOTE]
> <span data-ttu-id="e5117-247">Se utiliza una red virtual para que la topología de hello ejecutando en el clúster de Storm Hola puede comunicarse directamente con el clúster de HBase de hello mediante Hola API de Java de HBase.</span><span class="sxs-lookup"><span data-stu-id="e5117-247">A virtual network is used so that hello topology running on hello Storm cluster can directly communicate with hello HBase cluster using hello HBase Java API.</span></span>

<span data-ttu-id="e5117-248">plantilla de administrador de recursos de Hello usado en este documento se encuentra en un contenedor de blob público en **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span><span class="sxs-lookup"><span data-stu-id="e5117-248">hello Resource Manager template used in this document is located in a public blob container at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span></span>

1. <span data-ttu-id="e5117-249">Haga clic en hello siguientes toosign de botón en tooAzure y plantilla de administrador de recursos abiertos Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e5117-249">Click hello following button toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.6.json" target="_blank"><img src="./media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="e5117-250">De hello **implementación personalizada** sección, escriba Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="e5117-250">From hello **Custom deployment** section, enter hello following values:</span></span>
   
    ![Parámetros de HDInsight](./media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * <span data-ttu-id="e5117-252">**Nombre de clúster base**: este valor se utiliza como nombre de base de Hola para clústeres de Storm y HBase Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-252">**Base Cluster Name**: This value is used as hello base name for hello Storm and HBase clusters.</span></span> <span data-ttu-id="e5117-253">Por ejemplo, si escribe **abc**, se creará un clúster de Storm denominado **storm-abc** y un clúster de HBase denominado **hbase-abc**.</span><span class="sxs-lookup"><span data-stu-id="e5117-253">For example, entering **abc** creates a Storm cluster named **storm-abc** and an HBase cluster named **hbase-abc**.</span></span>
   * <span data-ttu-id="e5117-254">**Nombre de usuario de inicio de sesión del clúster**: nombre de usuario de administrador de Hola para clústeres de Storm y HBase Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-254">**Cluster Login User Name**: hello admin user name for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="e5117-255">**Contraseña de inicio de sesión del clúster**: contraseña de usuario de administrador de Hola para clústeres de Storm y HBase de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-255">**Cluster Login Password**: hello admin user password for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="e5117-256">**Nombre de usuario SSH**: Hola toocreate de usuario SSH para clústeres de Storm y HBase Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-256">**SSH User Name**: hello SSH user toocreate for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="e5117-257">**Contraseña SSH**: contraseña de hello para el usuario SSH de Hola para clústeres de Storm y HBase Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-257">**SSH Password**: hello password for hello SSH user for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="e5117-258">**Ubicación**: región Hola que se crean los clústeres de hello en.</span><span class="sxs-lookup"><span data-stu-id="e5117-258">**Location**: hello region that hello clusters are created in.</span></span>
     
     <span data-ttu-id="e5117-259">Haga clic en **Aceptar** parámetros de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="e5117-259">Click **OK** toosave hello parameters.</span></span>

3. <span data-ttu-id="e5117-260">Hola de uso **Fundamentos** sección toocreate un grupo de recursos o seleccione uno existente.</span><span class="sxs-lookup"><span data-stu-id="e5117-260">Use hello **Basics** section toocreate a resource group or select an existing one.</span></span>
4. <span data-ttu-id="e5117-261">Hola **ubicación del grupo de recursos** menú desplegable, seleccione Hola indicarlo tal y como se ha seleccionado para hello **ubicación** parámetro Hola **configuración** sección.</span><span class="sxs-lookup"><span data-stu-id="e5117-261">In hello **Resource group location** dropdown menu, select hello same location as you selected for hello **Location** parameter in hello **Settings** section.</span></span>
5. <span data-ttu-id="e5117-262">Lea Hola términos y condiciones y, a continuación, seleccione **muestro mi conformidad toohello términos y condiciones indicadas anteriormente**.</span><span class="sxs-lookup"><span data-stu-id="e5117-262">Read hello terms and conditions, and then select **I agree toohello terms and conditions stated above**.</span></span>
6. <span data-ttu-id="e5117-263">Finalmente, compruebe **Pin toodashboard** y, a continuación, seleccione **compra**.</span><span class="sxs-lookup"><span data-stu-id="e5117-263">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="e5117-264">Tarda aproximadamente 20 minutos toocreate clústeres Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-264">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="e5117-265">Una vez que se han creado Hola recursos, se muestra información sobre el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-265">Once hello resources have been created, information about hello resource group is displayed.</span></span>

![Grupo de recursos de red virtual de Hola y clústeres](./media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="e5117-267">Tenga en cuenta que los nombres de Hola de clústeres de HDInsight de hello **BASENAME storm** y **hbase BASENAME**, donde BASENAME es el nombre hello proporcionado toohello plantilla.</span><span class="sxs-lookup"><span data-stu-id="e5117-267">Notice that hello names of hello HDInsight clusters are **storm-BASENAME** and **hbase-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="e5117-268">Utilice estos nombres en un paso posterior al conectarse a clústeres de toohello.</span><span class="sxs-lookup"><span data-stu-id="e5117-268">You use these names in a later step when connecting toohello clusters.</span></span> <span data-ttu-id="e5117-269">También tenga en cuenta que Hola nombre del sitio de escritorio de hello es **basename panel**.</span><span class="sxs-lookup"><span data-stu-id="e5117-269">Also note that hello name of hello dashboard site is **basename-dashboard**.</span></span> <span data-ttu-id="e5117-270">Este valor se usa más adelante en este documento.</span><span class="sxs-lookup"><span data-stu-id="e5117-270">This value is used later in this document.</span></span>

## <a name="configure-hello-dashboard-bolt"></a><span data-ttu-id="e5117-271">Configurar rayo de panel de Hola</span><span class="sxs-lookup"><span data-stu-id="e5117-271">Configure hello Dashboard bolt</span></span>

<span data-ttu-id="e5117-272">panel de toosend datos toohello implementado como una aplicación web, debe modificar Hola línea siguiente en hello `dev.properties`archivo:</span><span class="sxs-lookup"><span data-stu-id="e5117-272">toosend data toohello dashboard deployed as a web app, you must modify hello following line in hello `dev.properties`file:</span></span>

```yaml
dashboard.uri: http://localhost:3000
```

<span data-ttu-id="e5117-273">Cambio `http://localhost:3000` demasiado`http://BASENAME-dashboard.azurewebsites.net` y guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="e5117-273">Change `http://localhost:3000` too`http://BASENAME-dashboard.azurewebsites.net` and save hello file.</span></span> <span data-ttu-id="e5117-274">Reemplace **BASENAME** con el nombre de base de hello proporcionado en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-274">Replace **BASENAME** with hello base name you provided in hello previous step.</span></span> <span data-ttu-id="e5117-275">También puede utilizar el grupo de recursos de hello creado previamente tooselect Hola panel y ver Hola una URL.</span><span class="sxs-lookup"><span data-stu-id="e5117-275">You can also use hello resource group created previously tooselect hello dashboard and view hello URL.</span></span>

## <a name="create-hello-hbase-table"></a><span data-ttu-id="e5117-276">Crear tabla de hello HBase</span><span class="sxs-lookup"><span data-stu-id="e5117-276">Create hello HBase table</span></span>

<span data-ttu-id="e5117-277">toostore datos en HBase, primero que debemos crear una tabla.</span><span class="sxs-lookup"><span data-stu-id="e5117-277">toostore data in HBase, we must first create a table.</span></span> <span data-ttu-id="e5117-278">Crear previamente los recursos que necesita de Storm toowrite a, tal y como se pueden dar lugar a tratar de recursos de toocreate desde dentro de una topología de Storm en varias instancias intentar toocreate Hola mismo recurso.</span><span class="sxs-lookup"><span data-stu-id="e5117-278">Pre-create resources that Storm needs toowrite to, as trying toocreate resources from inside a Storm topology can result in multiple instances trying toocreate hello same resource.</span></span> <span data-ttu-id="e5117-279">Crear recursos de hello fuera la topología de Hola y usar aluvión de lectura/escritura y análisis.</span><span class="sxs-lookup"><span data-stu-id="e5117-279">Create hello resources outside hello topology and use Storm for reading/writing and analytics.</span></span>

1. <span data-ttu-id="e5117-280">Use el clúster de HBase SSH tooconnect toohello mediante SSH hello y la contraseña que proporcionó toohello plantilla durante la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="e5117-280">Use SSH tooconnect toohello HBase cluster using hello SSH user and password you supplied toohello template during cluster creation.</span></span> <span data-ttu-id="e5117-281">Por ejemplo, si se conecta con hello `ssh` comando, usaría Hola según la sintaxis:</span><span class="sxs-lookup"><span data-stu-id="e5117-281">For example, if connecting using hello `ssh` command, you would use hello following syntax:</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```
   
    <span data-ttu-id="e5117-282">Reemplace `sshuser` con el nombre de usuario SSH de Hola que proporcionó al crear el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-282">Replace `sshuser` with hello SSH user name you provided when creating hello cluster.</span></span> <span data-ttu-id="e5117-283">Reemplace `clustername` con el nombre del clúster de HBase Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-283">Replace `clustername` with hello HBase cluster name.</span></span>

2. <span data-ttu-id="e5117-284">De sesión SSH de hello, inicie el shell de HBase Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-284">From hello SSH session, start hello HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="e5117-285">Una vez que ha cargado el shell de hello, verá un `hbase(main):001:0>` símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="e5117-285">Once hello shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="e5117-286">En el Hola shell de HBase, escriba Hola después comando toocreate una tabla toostore Hola sensor de datos:</span><span class="sxs-lookup"><span data-stu-id="e5117-286">From hello HBase shell, enter hello following command toocreate a table toostore hello sensor data:</span></span>
   
    ```hbase
    create 'SensorData', 'cf'
    ```

4. <span data-ttu-id="e5117-287">Comprobar que esa tabla Hola se ha creado mediante el uso de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e5117-287">Verify that hello table has been created by using hello following command:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="e5117-288">Esto devuelve información similar toohello siguiente ejemplo, que indica que hay 0 filas en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-288">This returns information similar toohello following example, indicating that there are 0 rows in hello table.</span></span>
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. <span data-ttu-id="e5117-289">Escriba `exit` tooexit Hola shell de HBase:</span><span class="sxs-lookup"><span data-stu-id="e5117-289">Enter `exit` tooexit hello HBase shell:</span></span>

## <a name="configure-hello-hbase-bolt"></a><span data-ttu-id="e5117-290">Configurar rayo de hello HBase</span><span class="sxs-lookup"><span data-stu-id="e5117-290">Configure hello HBase bolt</span></span>

<span data-ttu-id="e5117-291">toowrite tooHBase de clúster de Storm hello, debe proporcionar rayo de HBase Hola con detalles de configuración de Hola de su clúster de HBase.</span><span class="sxs-lookup"><span data-stu-id="e5117-291">toowrite tooHBase from hello Storm cluster, you must provide hello HBase bolt with hello configuration details of your HBase cluster.</span></span>

1. <span data-ttu-id="e5117-292">Use uno de hello después ejemplos tooretrieve hello Zookeeper quórum en el clúster de HBase:</span><span class="sxs-lookup"><span data-stu-id="e5117-292">Use one of hello following examples tooretrieve hello Zookeeper quorum for your HBase cluster:</span></span>

    ```bash
    CLUSTERNAME='your_HDInsight_cluster_name'
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HBASE/components/HBASE_MASTER" | jq '.metrics.hbase.master.ZookeeperQuorum'
    ```

    > [!NOTE]
    > <span data-ttu-id="e5117-293">Reemplace `your_HDInsight_cluster_name` con el nombre de Hola de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5117-293">Replace `your_HDInsight_cluster_name` with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="e5117-294">Para obtener más información acerca de cómo instalar hello `jq` utilidad, vea [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="e5117-294">For more information on installing hello `jq` utility, see [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span></span>
    >
    > <span data-ttu-id="e5117-295">Cuando se le solicite, escriba la contraseña de hello para el inicio de sesión de hello HDInsight admin.</span><span class="sxs-lookup"><span data-stu-id="e5117-295">When prompted, enter hello password for hello HDInsight admin login.</span></span>

    ```powershell
    $clusterName = 'your_HDInsight_cluster_name`
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HBASE/components/HBASE_MASTER" -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.metrics.hbase.master.ZookeeperQuorum
    ```

    > [!NOTE]
    > <span data-ttu-id="e5117-296">Reemplace ' your_HDInsight_cluster_name con el nombre de Hola de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5117-296">Replace \`your_HDInsight_cluster_name with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="e5117-297">Cuando se le solicite, escriba la contraseña de hello para el inicio de sesión de hello HDInsight admin.</span><span class="sxs-lookup"><span data-stu-id="e5117-297">When prompted, enter hello password for hello HDInsight admin login.</span></span>
    >
    > <span data-ttu-id="e5117-298">Este ejemplo requiere Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e5117-298">This example requires Azure PowerShell.</span></span> <span data-ttu-id="e5117-299">Para información acerca de cómo usar Azure PowerShell, consulte el artículo de [introducción a Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6).</span><span class="sxs-lookup"><span data-stu-id="e5117-299">For more information on using Azure PowerShell, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)</span></span>

    <span data-ttu-id="e5117-300">información de Hello devuelta por estos ejemplos es similar toohello siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="e5117-300">hello information returned by these examples is similar toohello following text:</span></span>

    `zk2-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk0-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk3-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181`

    <span data-ttu-id="e5117-301">Esta información se usa por Storm toocommunicate con clúster de HBase Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-301">This information is used by Storm toocommunicate with hello HBase cluster.</span></span>

2. <span data-ttu-id="e5117-302">Modificar hello `dev.properties` de archivos y agregar información de quórum de hello Zookeeper toohello después de línea:</span><span class="sxs-lookup"><span data-stu-id="e5117-302">Modify hello `dev.properties` file and add hello Zookeeper quorum information toohello following line:</span></span>

    ```yaml
    hbase.zookeeper.quorum: your_hbase_quorum
    ```

## <a name="build-package-and-deploy-hello-solution-toohdinsight"></a><span data-ttu-id="e5117-303">Compilar, empaquetar e implementar Hola solución tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="e5117-303">Build, package, and deploy hello solution tooHDInsight</span></span>

<span data-ttu-id="e5117-304">En el entorno de desarrollo, use Hola después de clúster de storm toohello de pasos toodeploy Hola Storm topología.</span><span class="sxs-lookup"><span data-stu-id="e5117-304">In your development environment, use hello following steps toodeploy hello Storm topology toohello storm cluster.</span></span>

1. <span data-ttu-id="e5117-305">De hello `TemperatureMonitor` directorio, use siguiente de hello tooperform una nueva compilación de comandos y cree un paquete JAR desde el proyecto:</span><span class="sxs-lookup"><span data-stu-id="e5117-305">From hello `TemperatureMonitor` directory, use hello following command tooperform a new build and create a JAR package from your project:</span></span>
   
        mvn clean package
   
    <span data-ttu-id="e5117-306">Este comando crea un archivo denominado `TemperatureMonitor-1.0-SNAPSHOT.jar in hello ` en el directorio de destino del proyecto.</span><span class="sxs-lookup"><span data-stu-id="e5117-306">This command creates a file named `TemperatureMonitor-1.0-SNAPSHOT.jar in hello `target\` directory of your project.</span></span>

2. <span data-ttu-id="e5117-307">Hola de uso scp tooupload `TemperatureMonitor-1.0-SNAPSHOT.jar` y `dev.properties` clúster de Storm tooyour de archivos.</span><span class="sxs-lookup"><span data-stu-id="e5117-307">Use scp tooupload hello `TemperatureMonitor-1.0-SNAPSHOT.jar` and `dev.properties` files tooyour Storm cluster.</span></span> <span data-ttu-id="e5117-308">Hola siguiente ejemplo, reemplace `sshuser` con el usuario SSH de Hola que proporcionó al crear el clúster de hello, y `clustername` con el nombre de Hola de su clúster de Storm.</span><span class="sxs-lookup"><span data-stu-id="e5117-308">In hello following example, replace `sshuser` with hello SSH user you provided when creating hello cluster, and `clustername` with hello name of your Storm cluster.</span></span> <span data-ttu-id="e5117-309">Cuando se le solicite, escriba la contraseña de hello para el usuario SSH Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-309">When prompted, enter hello password for hello SSH user.</span></span>
   
    ```bash
    scp target/TemperatureMonitor-1.0-SNAPSHOT.jar dev.properties sshuser@clustername-ssh.azurehdinsight.net:
    ```

   > [!NOTE]
   > <span data-ttu-id="e5117-310">Archivos de hello tooupload puede tardar varios minutos.</span><span class="sxs-lookup"><span data-stu-id="e5117-310">It may take several minutes tooupload hello files.</span></span>

    <span data-ttu-id="e5117-311">Para obtener más información sobre el uso de hello `scp` y `ssh` comandos con HDInsight, vea [utilizar SSH con HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="e5117-311">For more information on using hello `scp` and `ssh` commands with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

3. <span data-ttu-id="e5117-312">Una vez que se ha cargado el archivo hello, conecte el clúster de Storm toohello mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="e5117-312">Once hello file has been uploaded, connect toohello Storm cluster using SSH.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="e5117-313">Reemplace `sshuser` con el nombre de usuario SSH de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-313">Replace `sshuser` with hello SSH user name.</span></span> <span data-ttu-id="e5117-314">Reemplace `clustername` con el nombre de clúster de Storm Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-314">Replace `clustername` with hello Storm cluster name.</span></span>

4. <span data-ttu-id="e5117-315">toostart Hola topología, usar hello siguiente comando desde la sesión de SSH de hello:</span><span class="sxs-lookup"><span data-stu-id="e5117-315">toostart hello topology, use hello following command from hello SSH session:</span></span>
   
    ```bash
    storm jar TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote --filter dev.properties -R /with-hbase.yaml
    ```

    * <span data-ttu-id="e5117-316">`--remote`Hola topología toohello servicio Nimbus, que distribuye toohello nodos de supervisor en clúster de Hola se envía.</span><span class="sxs-lookup"><span data-stu-id="e5117-316">`--remote` submits hello topology toohello Nimbus service, which distributes it toohello supervisor nodes in hello cluster.</span></span>
    * <span data-ttu-id="e5117-317">`--filter`hello usa `dev.properties` toopopulate parámetros de archivo de definición de la topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-317">`--filter` uses hello `dev.properties` file toopopulate parameters in hello topology definition.</span></span>
    * <span data-ttu-id="e5117-318">`-R /with-hbase.yaml`hello usa `with-hbase.yaml` topología incluida en el paquete de saludo.</span><span class="sxs-lookup"><span data-stu-id="e5117-318">`-R /with-hbase.yaml` uses hello `with-hbase.yaml` topology included in hello package.</span></span>

5. <span data-ttu-id="e5117-319">Después de que ha iniciado la topología de hello, abrir un sitio Web de toohello de explorador publica en Azure, a continuación, use hello `node app.js` comando toosend datos tooEvent concentrador.</span><span class="sxs-lookup"><span data-stu-id="e5117-319">After hello topology has started, open a browser toohello website you published on Azure, then use hello `node app.js` command toosend data tooEvent Hub.</span></span> <span data-ttu-id="e5117-320">Debería ver la información de hello web panel actualización toodisplay Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-320">You should see hello web dashboard update toodisplay hello information.</span></span>
   
    ![dashboard](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a><span data-ttu-id="e5117-322">Visualización de datos de HBase</span><span class="sxs-lookup"><span data-stu-id="e5117-322">View HBase data</span></span>

<span data-ttu-id="e5117-323">Usar hello siguiendo los pasos tooconnect tooHBase y compruebe que se ha escrito datos hello toohello tabla:</span><span class="sxs-lookup"><span data-stu-id="e5117-323">Use hello following steps tooconnect tooHBase and verify that hello data has been written toohello table:</span></span>

1. <span data-ttu-id="e5117-324">Use el clúster de HBase de toohello tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="e5117-324">Use SSH tooconnect toohello HBase cluster.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="e5117-325">Reemplace `sshuser` con el nombre de usuario SSH de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-325">Replace `sshuser` with hello SSH user name.</span></span> <span data-ttu-id="e5117-326">Reemplace `clustername` con el nombre del clúster de HBase Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-326">Replace `clustername` with hello HBase cluster name.</span></span>

2. <span data-ttu-id="e5117-327">De sesión SSH de hello, inicie el shell de HBase Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-327">From hello SSH session, start hello HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="e5117-328">Una vez que ha cargado el shell de hello, verá un `hbase(main):001:0>` símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="e5117-328">Once hello shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="e5117-329">Ver las filas de tabla de hello:</span><span class="sxs-lookup"><span data-stu-id="e5117-329">View rows from hello table:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="e5117-330">Este comando devuelve información similar toohello después de texto, que indica que no hay datos en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-330">This command returns information similar toohello following text, indicating that there is data in hello table.</span></span>
   
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
   > <span data-ttu-id="e5117-331">Esta operación de búsqueda devuelve un máximo de 10 filas de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="e5117-331">This scan operation returns a maximum of 10 rows from hello table.</span></span>

## <a name="delete-your-clusters"></a><span data-ttu-id="e5117-332">Eliminación de los clústeres</span><span class="sxs-lookup"><span data-stu-id="e5117-332">Delete your clusters</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="e5117-333">clústeres de hello toodelete, el almacenamiento y la aplicación web al mismo tiempo, eliminar grupo de recursos de Hola que los contiene.</span><span class="sxs-lookup"><span data-stu-id="e5117-333">toodelete hello clusters, storage, and web app at one time, delete hello resource group that contains them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5117-334">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e5117-334">Next steps</span></span>

<span data-ttu-id="e5117-335">Para obtener más ejemplos de topologías de Storm con HDInsight, vea [Topologías y componentes de ejemplo de Storm para Apache Storm en HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="e5117-335">For more examples of Storm topologies with HDInsight, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md)</span></span>

<span data-ttu-id="e5117-336">Para obtener más información acerca de Apache Storm, vea hello [Apache Storm](https://storm.incubator.apache.org/) sitio.</span><span class="sxs-lookup"><span data-stu-id="e5117-336">For more information about Apache Storm, see hello [Apache Storm](https://storm.incubator.apache.org/) site.</span></span>

<span data-ttu-id="e5117-337">Para obtener más información acerca de HBase en HDInsight, vea hello [HBase visión general de HDInsight](hdinsight-hbase-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e5117-337">For more information about HBase on HDInsight, see hello [HBase with HDInsight Overview](hdinsight-hbase-overview.md).</span></span>

<span data-ttu-id="e5117-338">Para obtener más información sobre Socket.io, vea hello [socket.io](http://socket.io/) sitio.</span><span class="sxs-lookup"><span data-stu-id="e5117-338">For more information about Socket.io, see hello [socket.io](http://socket.io/) site.</span></span>

<span data-ttu-id="e5117-339">Para obtener más información sobre D3.js, consulte [D3.js: documentos controlados por datos](http://d3js.org/).</span><span class="sxs-lookup"><span data-stu-id="e5117-339">For more information about D3.js, see [D3.js - Data Driven Documents](http://d3js.org/).</span></span>

<span data-ttu-id="e5117-340">Para obtener información sobre la creación de topologías en Java, consulte [Desarrollo de topologías de Java para Apache Storm en HDInsight](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="e5117-340">For information about creating topologies in Java, see [Develop Java topologies for Apache Storm on HDInsight](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="e5117-341">Para obtener información sobre la creación de topologías en .NET, consulte [Desarrollo de topologías de C# para Apache Storm en HDInsight mediante Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="e5117-341">For information about creating topologies in .NET, see [Develop C# topologies for Apache Storm on HDInsight using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

[azure-portal]: https://portal.azure.com
