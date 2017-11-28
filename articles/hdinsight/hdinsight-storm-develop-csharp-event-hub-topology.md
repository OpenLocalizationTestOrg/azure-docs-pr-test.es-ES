---
title: Procesamiento de eventos desde Event Hubs con Storm - Azure HDInsight | Microsoft Docs
description: "Aprenda a procesar datos desde Azure Event Hubs con una topología de C# Storm creada en Visual Studio mediante las herramientas de HDInsight para Visual Studio."
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 67f9d08c-eea0-401b-952b-db765655dad0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 4b6fd87b057d93175d3ef284238d77be3bdde61d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a><span data-ttu-id="c7ca0-103">Procesamiento de eventos de Azure Event Hubs con Storm en HDInsight (C#)</span><span class="sxs-lookup"><span data-stu-id="c7ca0-103">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>

<span data-ttu-id="c7ca0-104">Aprenda a trabajar con Azure Event Hubs desde Apache Storm en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-104">Learn how to work with Azure Event Hubs from Apache Storm on HDInsight.</span></span> <span data-ttu-id="c7ca0-105">Este documento usa una topología de C# Storm para leer y escribir datos desde Event Hubs</span><span class="sxs-lookup"><span data-stu-id="c7ca0-105">This document uses a C# Storm topology to read and write data from Evbent Hubs</span></span>

> [!NOTE]
> <span data-ttu-id="c7ca0-106">Para ver una versión en Java de este proyecto, consulte [Procesamiento de eventos desde Azure Event Hubs con Storm en HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="c7ca0-106">For a Java version of this project, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="scpnet"></a><span data-ttu-id="c7ca0-107">SCP.NET</span><span class="sxs-lookup"><span data-stu-id="c7ca0-107">SCP.NET</span></span>

<span data-ttu-id="c7ca0-108">Los pasos descritos en este documento usan SCP.NET, un paquete NuGet que facilita la creación de topologías y componentes de C# para su uso con Storm en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-108">The steps in this document use SCP.NET, a NuGet package that makes it easy to create C# topologies and components for use with Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7ca0-109">Aunque los pasos descritos en este documento se basan en un entorno de desarrollo de Windows con Visual Studio, el proyecto compilado se puede enviar a un clúster de Storm en HDInsight basado en Linux.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-109">While the steps in this document rely on a Windows development environment with Visual Studio, the compiled project can be submitted to a Storm on HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="c7ca0-110">Solo los clústeres basados en Linux creados después del 28 de octubre de 2016 admiten topologías SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-110">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="c7ca0-111">HDInsight 3.4 y versiones superiores usan Mono para ejecutar topologías de C#.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-111">HDInsight 3.4 and greater use Mono to run C# topologies.</span></span> <span data-ttu-id="c7ca0-112">El ejemplo usado en este documento funciona con HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-112">The example used in this document works with HDInsight 3.6.</span></span> <span data-ttu-id="c7ca0-113">Si tiene previsto crear sus propias soluciones de .NET para HDInsight, consulte el documento [compatibilidad de Mono](http://www.mono-project.com/docs/about-mono/compatibility/) para detectar posibles incompatibilidades.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-113">If you plan on creating your own .NET solutions for HDInsight, check the [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>

### <a name="cluster-versioning"></a><span data-ttu-id="c7ca0-114">Control de versiones de clúster</span><span class="sxs-lookup"><span data-stu-id="c7ca0-114">Cluster versioning</span></span>

<span data-ttu-id="c7ca0-115">El paquete de NuGet Microsoft.SCP.Net.SDK que se usa en el proyecto debe coincidir con la versión principal de Storm instalada en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-115">The Microsoft.SCP.Net.SDK NuGet package you use for your project must match the major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="c7ca0-116">Las versiones de HDInsight 3.5 y 3.6 usan Storm 1.x, por lo que debe usar la versión 1.0.x.x de SCP.NET con estos clústeres.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-116">HDInsight versions 3.5 and 3.6 use Storm 1.x, so you must use SCP.NET version 1.0.x.x with these clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7ca0-117">En el ejemplo de este documento se espera un clúster de HDInsight 3.5 o 3.6.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-117">The example in this document expects an HDInsight 3.5 or 3.6 cluster.</span></span>
>
> <span data-ttu-id="c7ca0-118">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-118">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c7ca0-119">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="c7ca0-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="c7ca0-120">Las topologías de C# también deben tener como destino .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-120">C# topologies must also target .NET 4.5.</span></span>

## <a name="how-to-work-with-event-hubs"></a><span data-ttu-id="c7ca0-121">Trabajo con Event Hubs</span><span class="sxs-lookup"><span data-stu-id="c7ca0-121">How to work with Event Hubs</span></span>

<span data-ttu-id="c7ca0-122">Microsoft proporciona un conjunto de componentes de Java que se pueden usar para la comunicación con Event Hubs desde una topología de Storm.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-122">Microsoft provides a set of Java components that can be used to communicate with Event Hubs from a Storm topology.</span></span> <span data-ttu-id="c7ca0-123">Puede encontrar el archivo de almacenamiento Java (JAR) que contiene una versión compatible de HDInsight 3.6 de estos componentes en [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span><span class="sxs-lookup"><span data-stu-id="c7ca0-123">You can find the Java archive (JAR) file that contains an HDInsight 3.6 compatible version of these components at [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7ca0-124">Si bien los componentes están escritos en Java, puede usarlos fácilmente desde una topología de C#.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-124">While the components are written in Java, you can easily use them from a C# topology.</span></span>

<span data-ttu-id="c7ca0-125">En este ejemplo se usan los componentes siguientes:</span><span class="sxs-lookup"><span data-stu-id="c7ca0-125">The following components are used in this example:</span></span>

* <span data-ttu-id="c7ca0-126">__EventHubSpout__: lee datos de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-126">__EventHubSpout__: Reads data from Event Hubs.</span></span>
* <span data-ttu-id="c7ca0-127">__EventHubBolt__: escribe datos en Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-127">__EventHubBolt__: Writes data to Event Hubs.</span></span>
* <span data-ttu-id="c7ca0-128">__EventHubSpoutConfig__: se usa para configurar EventHubSpout.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-128">__EventHubSpoutConfig__: Used to configure EventHubSpout.</span></span>
* <span data-ttu-id="c7ca0-129">__EventHubBoltConfig__: se usa para configurar EventHubBolt.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-129">__EventHubBoltConfig__: Used to configure EventHubBolt.</span></span>

### <a name="example-spout-usage"></a><span data-ttu-id="c7ca0-130">Ejemplo de uso de spout</span><span class="sxs-lookup"><span data-stu-id="c7ca0-130">Example spout usage</span></span>

<span data-ttu-id="c7ca0-131">SCP.NET proporciona métodos para agregar un objeto EventHubSpout a la topología.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-131">SCP.NET provides methods for adding an EventHubSpout to your topology.</span></span> <span data-ttu-id="c7ca0-132">Estos métodos hacen que sea más fácil agregar un spout que usar los métodos genéricos para agregar un componente Java.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-132">These methods make it easier to add a spout than using the generic methods for adding a Java component.</span></span> <span data-ttu-id="c7ca0-133">En el ejemplo siguiente se muestra cómo crear un spout mediante los métodos __SetEventHubSpout__ y **EventHubSpoutConfig** proporcionados por SCP.NET:</span><span class="sxs-lookup"><span data-stu-id="c7ca0-133">The following example demonstrates how to create a spout by using the __SetEventHubSpout__ and **EventHubSpoutConfig** methods provided by SCP.NET:</span></span>

```csharp
 topologyBuilder.SetEventHubSpout(
    "EventHubSpout",
    new EventHubSpoutConfig(
        ConfigurationManager.AppSettings["EventHubSharedAccessKeyName"],
        ConfigurationManager.AppSettings["EventHubSharedAccessKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        ConfigurationManager.AppSettings["EventHubEntityPath"],
        eventHubPartitions),
    eventHubPartitions);
```

<span data-ttu-id="c7ca0-134">En el ejemplo anterior se crea un nuevo componente de spout denominado __EventHubSpout__ y se configura para la comunicación con un centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-134">The previous example creates a new spout component named __EventHubSpout__, and configures it to communicate with an event hub.</span></span> <span data-ttu-id="c7ca0-135">La indicación de paralelismo del componente está establecida en el número de particiones del centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-135">The parallelism hint for the component is set to the number of partitions in the event hub.</span></span> <span data-ttu-id="c7ca0-136">Esta configuración permite a Storm crear una instancia del componente para cada partición.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-136">This setting allows Storm to create an instance of the component for each partition.</span></span>

### <a name="example-bolt-usage"></a><span data-ttu-id="c7ca0-137">Ejemplo de uso de bolt</span><span class="sxs-lookup"><span data-stu-id="c7ca0-137">Example bolt usage</span></span>

<span data-ttu-id="c7ca0-138">Use el método **JavaComponmentConstructor** para crear una instancia del bolt.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-138">Use the **JavaComponmentConstructor** method to create an instance of the bolt.</span></span> <span data-ttu-id="c7ca0-139">En el ejemplo siguiente se muestra cómo crear y configurar una nueva instancia **EventHubBolt**:</span><span class="sxs-lookup"><span data-stu-id="c7ca0-139">The following example demonstrates how to create and configure a new instance of the **EventHubBolt**:</span></span>

```csharp
// Java construcvtor for the Event Hub Bolt
JavaComponentConstructor constructor = JavaComponentConstructor.CreateFromClojureExpr(
    String.Format(@"(org.apache.storm.eventhubs.bolt.EventHubBolt. (org.apache.storm.eventhubs.bolt.EventHubBoltConfig. " +
        @"""{0}"" ""{1}"" ""{2}"" ""{3}"" ""{4}"" {5}))",
        ConfigurationManager.AppSettings["EventHubPolicyName"],
        ConfigurationManager.AppSettings["EventHubPolicyKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        "servicebus.windows.net",
        ConfigurationManager.AppSettings["EventHubName"],
        "true"));

// Set the bolt to subscribe to data from the spout
topologyBuilder.SetJavaBolt(
    "eventhubbolt",
    constructor,
    partitionCount)
        .shuffleGrouping("Spout");
```

> [!NOTE]
> <span data-ttu-id="c7ca0-140">En este ejemplo se usa una expresión Clojure pasada como una cadena en lugar de usar **JavaComponentConstructor** para crear un objeto **EventHubBoltConfig**, como se hizo en el ejemplo con el spout.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-140">This example uses a Clojure expression passed as a string, instead of using **JavaComponentConstructor** to create an **EventHubBoltConfig**, as the spout example did.</span></span> <span data-ttu-id="c7ca0-141">Cualquiera de estos métodos funciona.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-141">Either method works.</span></span> <span data-ttu-id="c7ca0-142">Use el método con el que se sienta mejor.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-142">Use the method that feels best to you.</span></span>

## <a name="download-the-completed-project"></a><span data-ttu-id="c7ca0-143">Descarga del proyecto finalizado</span><span class="sxs-lookup"><span data-stu-id="c7ca0-143">Download the completed project</span></span>

<span data-ttu-id="c7ca0-144">Puede descargar una versión completa del proyecto creado en este tutorial desde [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="c7ca0-144">You can download a complete version of the project created in this tutorial from [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span> <span data-ttu-id="c7ca0-145">Sin embargo, deberá proporcionar ajustes de configuración siguiendo los pasos de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-145">However, you still need to provide configuration settings by following the steps in this tutorial.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c7ca0-146">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c7ca0-146">Prerequisites</span></span>

* <span data-ttu-id="c7ca0-147">Una [instancia de Apache Storm en un clúster de HDInsight, versión 3.5 o 3.6](hdinsight-apache-storm-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c7ca0-147">An [Apache Storm on HDInsight cluster version 3.5 or 3.6](hdinsight-apache-storm-tutorial-get-started.md).</span></span>

    > [!WARNING]
    > <span data-ttu-id="c7ca0-148">El ejemplo usado en este documento requiere Storm en HDInsight versión 3.5 o 3.6.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-148">The example used in this document requires Storm on HDInsight version 3.5 or 3.6.</span></span> <span data-ttu-id="c7ca0-149">Esto no funciona con versiones anteriores de HDInsight debido a cambios de nombre de clase importantes.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-149">This does not work with older versions of HDInsight, due to breaking class name changes.</span></span> <span data-ttu-id="c7ca0-150">Para obtener una versión de este ejemplo que funcione con clústeres anteriores, vea [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span><span class="sxs-lookup"><span data-stu-id="c7ca0-150">For a version of this example that works with older clusters, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span></span>

* <span data-ttu-id="c7ca0-151">Un [centro de eventos de Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="c7ca0-151">An [Azure event hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="c7ca0-152">El [SDK de .NET para Azure](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c7ca0-152">The [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>

* <span data-ttu-id="c7ca0-153">Las [herramientas de HDInsight para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c7ca0-153">The [HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="c7ca0-154">Java JDK 1.8 o posterior en el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-154">Java JDK 1.8 or later on your development environment.</span></span> <span data-ttu-id="c7ca0-155">Las descargas de JDK están disponibles en [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="c7ca0-155">JDK downloads are available from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>

  * <span data-ttu-id="c7ca0-156">La variable de entorno **JAVA_HOME** debe señalar al directorio que contiene Java.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-156">The **JAVA_HOME** environment variable must point to the directory that contains Java.</span></span>
  * <span data-ttu-id="c7ca0-157">El directorio **%JAVA_HOME%/bin** debe estar en la ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-157">The **%JAVA_HOME%/bin** directory must be in the path.</span></span>

## <a name="download-the-event-hubs-components"></a><span data-ttu-id="c7ca0-158">Descarga de los componentes de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="c7ca0-158">Download the Event Hubs components</span></span>

<span data-ttu-id="c7ca0-159">Descargue el componente de spout y bolt de Event Hubs desde [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span><span class="sxs-lookup"><span data-stu-id="c7ca0-159">Download the Event Hubs spout and bolt component from [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

<span data-ttu-id="c7ca0-160">Cree un directorio denominado `eventhubspout` y guarde el archivo en él.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-160">Create a directory named `eventhubspout`, and save the file into the directory.</span></span>

## <a name="configure-event-hubs"></a><span data-ttu-id="c7ca0-161">Configuración de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="c7ca0-161">Configure Event Hubs</span></span>

<span data-ttu-id="c7ca0-162">Event Hubs es el origen de datos para este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-162">Event Hubs is the data source for this example.</span></span> <span data-ttu-id="c7ca0-163">Use la información de la sección "Creación de un espacio de nombres de Event Hubs y un centro de eventos" de [Introducción al envío de mensajes a Azure Event Hubs en .NET Standard](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="c7ca0-163">Use the information in the "Create an event hub" section of [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

1. <span data-ttu-id="c7ca0-164">Después de crear el centro de eventos, vea la hoja **EventHub** de Azure Portal y seleccione **Directivas de acceso compartido**.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-164">After the event hub has been created, view the **EventHub** blade in the Azure portal, and select **Shared access policies**.</span></span> <span data-ttu-id="c7ca0-165">Haga clic en **+ Agregar** para agregar las siguientes directivas:</span><span class="sxs-lookup"><span data-stu-id="c7ca0-165">Select **+ Add** to add the following policies:</span></span>

   | <span data-ttu-id="c7ca0-166">Nombre</span><span class="sxs-lookup"><span data-stu-id="c7ca0-166">Name</span></span> | <span data-ttu-id="c7ca0-167">Permisos</span><span class="sxs-lookup"><span data-stu-id="c7ca0-167">Permissions</span></span> |
   | --- | --- |
   | <span data-ttu-id="c7ca0-168">escritor</span><span class="sxs-lookup"><span data-stu-id="c7ca0-168">writer</span></span> |<span data-ttu-id="c7ca0-169">Los métodos Send</span><span class="sxs-lookup"><span data-stu-id="c7ca0-169">Send</span></span> |
   | <span data-ttu-id="c7ca0-170">lector</span><span class="sxs-lookup"><span data-stu-id="c7ca0-170">reader</span></span> |<span data-ttu-id="c7ca0-171">Escuchar</span><span class="sxs-lookup"><span data-stu-id="c7ca0-171">Listen</span></span> |

    ![Captura de pantalla de la ventana Directivas de acceso compartido](./media/hdinsight-storm-develop-csharp-event-hub-topology/sas.png)

2. <span data-ttu-id="c7ca0-173">Seleccione las directivas de **lectura** y **escritura**.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-173">Select the **reader** and **writer** policies.</span></span> <span data-ttu-id="c7ca0-174">Copie y guarde el valor de clave principal de ambas directivas, ya que estos valores se usan más adelante.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-174">Copy and save the primary key value for both policies, as these values are used later.</span></span>

## <a name="configure-the-eventhubwriter"></a><span data-ttu-id="c7ca0-175">Configuración de EventHubWriter</span><span class="sxs-lookup"><span data-stu-id="c7ca0-175">Configure the EventHubWriter</span></span>

1. <span data-ttu-id="c7ca0-176">Si todavía no tiene instalada la versión más reciente de las herramientas de HDInsight para Visual Studio, vea [Get started using HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) (Introducción al uso de las herramientas de HDInsight para Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="c7ca0-176">If you have not already installed the latest version of the HDInsight tools for Visual Studio, see [Get started using HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="c7ca0-177">Descargue la solución de [eventhub-storm-hybrid](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="c7ca0-177">Download the solution from [eventhub-storm-hybrid](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

3. <span data-ttu-id="c7ca0-178">En el proyecto **EventHubWriter**, abra el archivo **App.config**.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-178">In the **EventHubWriter** project, open the **App.config** file.</span></span> <span data-ttu-id="c7ca0-179">Use la información del centro de eventos que configuró anteriormente para rellenar el valor de las claves siguientes:</span><span class="sxs-lookup"><span data-stu-id="c7ca0-179">Use the information from the event hub that you configured earlier to fill in the value for the following keys:</span></span>

   | <span data-ttu-id="c7ca0-180">Clave</span><span class="sxs-lookup"><span data-stu-id="c7ca0-180">Key</span></span> | <span data-ttu-id="c7ca0-181">Valor</span><span class="sxs-lookup"><span data-stu-id="c7ca0-181">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="c7ca0-182">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="c7ca0-182">EventHubPolicyName</span></span> |<span data-ttu-id="c7ca0-183">escritura (si ha usado un nombre distinto para la directiva con el permiso *Envío*, úselo en su lugar).</span><span class="sxs-lookup"><span data-stu-id="c7ca0-183">writer (If you used a different name for the policy with *Send* permission, use it instead.)</span></span> |
   | <span data-ttu-id="c7ca0-184">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="c7ca0-184">EventHubPolicyKey</span></span> |<span data-ttu-id="c7ca0-185">Clave de la directiva de escritura.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-185">The key for the writer policy.</span></span> |
   | <span data-ttu-id="c7ca0-186">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="c7ca0-186">EventHubNamespace</span></span> |<span data-ttu-id="c7ca0-187">Espacio de nombres que contiene el centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-187">The namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="c7ca0-188">EventHubName</span><span class="sxs-lookup"><span data-stu-id="c7ca0-188">EventHubName</span></span> |<span data-ttu-id="c7ca0-189">Nombre del centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-189">Your event hub name.</span></span> |
   | <span data-ttu-id="c7ca0-190">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="c7ca0-190">EventHubPartitionCount</span></span> |<span data-ttu-id="c7ca0-191">Número de particiones del centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-191">The number of partitions in your event hub.</span></span> |

4. <span data-ttu-id="c7ca0-192">Guarde y cierre el archivo **App.config**.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-192">Save and close the **App.config** file.</span></span>

## <a name="configure-the-eventhubreader"></a><span data-ttu-id="c7ca0-193">Configuración de EventHubReader</span><span class="sxs-lookup"><span data-stu-id="c7ca0-193">Configure the EventHubReader</span></span>

1. <span data-ttu-id="c7ca0-194">Abra el proyecto **EventHubReader**.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-194">Open the **EventHubReader** project.</span></span>

2. <span data-ttu-id="c7ca0-195">Abra el archivo **App.config** para **EventHubReader**.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-195">Open the **App.config** file for the **EventHubReader**.</span></span> <span data-ttu-id="c7ca0-196">Use la información del centro de eventos que configuró anteriormente para rellenar el valor de las claves siguientes:</span><span class="sxs-lookup"><span data-stu-id="c7ca0-196">Use the information from the event hub that you configured earlier to fill in the value for the following keys:</span></span>

   | <span data-ttu-id="c7ca0-197">Clave</span><span class="sxs-lookup"><span data-stu-id="c7ca0-197">Key</span></span> | <span data-ttu-id="c7ca0-198">Valor</span><span class="sxs-lookup"><span data-stu-id="c7ca0-198">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="c7ca0-199">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="c7ca0-199">EventHubPolicyName</span></span> |<span data-ttu-id="c7ca0-200">lectura (si ha usado un nombre distinto para la directiva con el permiso *escucha*, úselo en su lugar).</span><span class="sxs-lookup"><span data-stu-id="c7ca0-200">reader (If you used a different name for the policy with *listen* permission, use it instead.)</span></span> |
   | <span data-ttu-id="c7ca0-201">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="c7ca0-201">EventHubPolicyKey</span></span> |<span data-ttu-id="c7ca0-202">Clave de la directiva de lectura.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-202">The key for the reader policy.</span></span> |
   | <span data-ttu-id="c7ca0-203">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="c7ca0-203">EventHubNamespace</span></span> |<span data-ttu-id="c7ca0-204">Espacio de nombres que contiene el centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-204">The namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="c7ca0-205">EventHubName</span><span class="sxs-lookup"><span data-stu-id="c7ca0-205">EventHubName</span></span> |<span data-ttu-id="c7ca0-206">Nombre del centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-206">Your event hub name.</span></span> |
   | <span data-ttu-id="c7ca0-207">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="c7ca0-207">EventHubPartitionCount</span></span> |<span data-ttu-id="c7ca0-208">Número de particiones del centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-208">The number of partitions in your event hub.</span></span> |

3. <span data-ttu-id="c7ca0-209">Guarde y cierre el archivo **App.config**.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-209">Save and close the **App.config** file.</span></span>

## <a name="deploy-the-topologies"></a><span data-ttu-id="c7ca0-210">Implementación de las topologías</span><span class="sxs-lookup"><span data-stu-id="c7ca0-210">Deploy the topologies</span></span>

1. <span data-ttu-id="c7ca0-211">En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto **EventHubReader** y seleccione **Enviar a Storm en HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-211">From **Solution Explorer**, right-click the **EventHubReader** project, and select **Submit to Storm on HDInsight**.</span></span>

    ![Captura de pantalla del Explorador de soluciones con Enviar a Storm en HDInsight resaltado](./media/hdinsight-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. <span data-ttu-id="c7ca0-213">En el cuadro de diálogo **Enviar topología**, seleccione el **clúster de Storm**.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-213">On the **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="c7ca0-214">Expanda **Configuraciones adicionales**, seleccione **Rutas de acceso del archivo Java**, elija **...** y luego seleccione el directorio que contiene el archivo JAR que descargó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-214">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select the directory that contains the JAR file that you downloaded earlier.</span></span> <span data-ttu-id="c7ca0-215">Finalmente, haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-215">Finally, click **Submit**.</span></span>

    ![Captura de pantalla del cuadro de diálogo Enviar topología](./media/hdinsight-storm-develop-csharp-event-hub-topology/submit.png)

3. <span data-ttu-id="c7ca0-217">Cuando se haya enviado la topología, aparecerá el **Visor de topologías de Storm**.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-217">When the topology has been submitted, the **Storm Topologies Viewer** appears.</span></span> <span data-ttu-id="c7ca0-218">Para ver información sobre la topología, seleccione la topología **EventHubReader** en el panel izquierdo.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-218">To view information about the topology, select the **EventHubReader** topology in the left pane.</span></span>

    ![Captura de pantalla del Visor de topologías de Storm](./media/hdinsight-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. <span data-ttu-id="c7ca0-220">En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto **EventHubWriter** y seleccione **Enviar a Storm en HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-220">From **Solution Explorer**, right-click the **EventHubWriter** project, and select **Submit to Storm on HDInsight**.</span></span>

5. <span data-ttu-id="c7ca0-221">En el cuadro de diálogo **Enviar topología**, seleccione el **clúster de Storm**.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-221">On the **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="c7ca0-222">Expanda **Configuraciones adicionales**, seleccione **Rutas de acceso del archivo Java**, elija **...** y seleccione el directorio que contiene el archivo JAR que descargó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-222">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select the directory that contains the JAR file you downloaded earlier.</span></span> <span data-ttu-id="c7ca0-223">Finalmente, haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-223">Finally, click **Submit**.</span></span>

6. <span data-ttu-id="c7ca0-224">Cuando se haya enviado la topología, actualice la lista de topologías en el **Visor de topologías de Storm** para comprobar que las dos se estén ejecutando en el clúster.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-224">When the topology has been submitted, refresh the topology list in the **Storm Topologies Viewer** to verify that both topologies are running on the cluster.</span></span>

7. <span data-ttu-id="c7ca0-225">En el **Visor de topologías de Storm**, seleccione la topología **EventHubReader**.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-225">In **Storm Topologies Viewer**, select the **EventHubReader** topology.</span></span>

8. <span data-ttu-id="c7ca0-226">Para abrir el resumen de componentes del bolt, haga doble clic en el componente **LogBolt** en el diagrama.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-226">To open the component summary for the bolt, double-click the **LogBolt** component in the diagram.</span></span>

9. <span data-ttu-id="c7ca0-227">En la sección **Executors** (Ejecutores), seleccione uno de los vínculos de la columna **Port** (Puerto).</span><span class="sxs-lookup"><span data-stu-id="c7ca0-227">In the **Executors** section, select one of the links in the **Port** column.</span></span> <span data-ttu-id="c7ca0-228">Esto muestra información registrada por el componente.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-228">This displays information logged by the component.</span></span> <span data-ttu-id="c7ca0-229">La información registrada es similar al texto siguiente:</span><span class="sxs-lookup"><span data-stu-id="c7ca0-229">The logged information is similar to the following text:</span></span>

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-the-topologies"></a><span data-ttu-id="c7ca0-230">Detención de las topologías</span><span class="sxs-lookup"><span data-stu-id="c7ca0-230">Stop the topologies</span></span>

<span data-ttu-id="c7ca0-231">Para detener las topologías, seleccione cada una en el **Visor de topologías de Storm** y haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-231">To stop the topologies, select each topology in the **Storm Topology Viewer**, then click **Kill**.</span></span>

![Captura de pantalla del Visor de topologías de Storm con el botón Eliminar resaltado](./media/hdinsight-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="c7ca0-233">Eliminación del clúster</span><span class="sxs-lookup"><span data-stu-id="c7ca0-233">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="c7ca0-234">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c7ca0-234">Next steps</span></span>

<span data-ttu-id="c7ca0-235">En este documento ha aprendido a usar el spout y el bolt de Java Event Hubs desde una topología de C# para trabajar con datos en Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="c7ca0-235">In this document, you have learned how to use the Java Event Hubs spout and bolt from a C# topology to work with data in Azure Event Hubs.</span></span> <span data-ttu-id="c7ca0-236">Para más información sobre cómo crear topologías de C#, vea lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c7ca0-236">To learn more about creating C# topologies, see the following:</span></span>

* [<span data-ttu-id="c7ca0-237">Desarrollo de topologías de C# para Apache Storm en HDInsight con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c7ca0-237">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="c7ca0-238">Guía de programación de SCP</span><span class="sxs-lookup"><span data-stu-id="c7ca0-238">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)
* [<span data-ttu-id="c7ca0-239">Topologías de ejemplo para Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7ca0-239">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
