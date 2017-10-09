---
title: aaaProcess eventos desde los centros de eventos con Storm - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooprocess los datos de los centros de eventos de Azure con una topología de C# Storm crean en Visual Studio, mediante el uso de hello herramientas de HDInsight para Visual Studio."
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
ms.openlocfilehash: 30cd910d80eba066f283197bcbbaf11145bc5524
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a><span data-ttu-id="8ebf7-103">Procesamiento de eventos desde Centros de eventos de Azure con Storm en HDInsight (C#)</span><span class="sxs-lookup"><span data-stu-id="8ebf7-103">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>

<span data-ttu-id="8ebf7-104">Obtenga información acerca de cómo toowork con concentradores de eventos de Azure desde Apache Storm en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-104">Learn how toowork with Azure Event Hubs from Apache Storm on HDInsight.</span></span> <span data-ttu-id="8ebf7-105">Este documento usa una tormenta de C# topología tooread y escritura de datos desde los centros de Evbent</span><span class="sxs-lookup"><span data-stu-id="8ebf7-105">This document uses a C# Storm topology tooread and write data from Evbent Hubs</span></span>

> [!NOTE]
> <span data-ttu-id="8ebf7-106">Para ver una versión en Java de este proyecto, consulte [Procesamiento de eventos desde Azure Event Hubs con Storm en HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="8ebf7-106">For a Java version of this project, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="scpnet"></a><span data-ttu-id="8ebf7-107">SCP.NET</span><span class="sxs-lookup"><span data-stu-id="8ebf7-107">SCP.NET</span></span>

<span data-ttu-id="8ebf7-108">pasos de Hello en este documento utiliza SCP.NET, un paquete de NuGet que resulta fácil toocreate C# topologías y componentes para su uso con Storm en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-108">hello steps in this document use SCP.NET, a NuGet package that makes it easy toocreate C# topologies and components for use with Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ebf7-109">Aunque Hola los pasos de este documento se basan en un entorno de desarrollo de Windows con Visual Studio, proyecto compilado Hola puede ser enviado tooa Storm en clúster de HDInsight que usa Linux.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-109">While hello steps in this document rely on a Windows development environment with Visual Studio, hello compiled project can be submitted tooa Storm on HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="8ebf7-110">Solo los clústeres basados en Linux creados después del 28 de octubre de 2016 admiten topologías SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-110">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="8ebf7-111">3.4 de HDInsight y topologías de Mono toorun C# de mayor uso.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-111">HDInsight 3.4 and greater use Mono toorun C# topologies.</span></span> <span data-ttu-id="8ebf7-112">ejemplo de Hola usado en este documento funciona con 3.6 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-112">hello example used in this document works with HDInsight 3.6.</span></span> <span data-ttu-id="8ebf7-113">Si tiene previsto crear sus propias soluciones de .NET para HDInsight, comprobar hello [compatibilidad Mono](http://www.mono-project.com/docs/about-mono/compatibility/) documento para detectar posibles incompatibilidades.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-113">If you plan on creating your own .NET solutions for HDInsight, check hello [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>

### <a name="cluster-versioning"></a><span data-ttu-id="8ebf7-114">Control de versiones de clúster</span><span class="sxs-lookup"><span data-stu-id="8ebf7-114">Cluster versioning</span></span>

<span data-ttu-id="8ebf7-115">Hola paquete Microsoft.SCP.Net.SDK NuGet se utiliza para el proyecto debe coincidir con la versión principal de Hola de Storm instalado en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-115">hello Microsoft.SCP.Net.SDK NuGet package you use for your project must match hello major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="8ebf7-116">Las versiones de HDInsight 3.5 y 3.6 usan Storm 1.x, por lo que debe usar la versión 1.0.x.x de SCP.NET con estos clústeres.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-116">HDInsight versions 3.5 and 3.6 use Storm 1.x, so you must use SCP.NET version 1.0.x.x with these clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ebf7-117">ejemplo de Hola en este documento espera un 3.5 HDInsight o clúster 3,6.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-117">hello example in this document expects an HDInsight 3.5 or 3.6 cluster.</span></span>
>
> <span data-ttu-id="8ebf7-118">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-118">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="8ebf7-119">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="8ebf7-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="8ebf7-120">Las topologías de C# también deben tener como destino .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-120">C# topologies must also target .NET 4.5.</span></span>

## <a name="how-toowork-with-event-hubs"></a><span data-ttu-id="8ebf7-121">¿Cómo toowork con concentradores de eventos</span><span class="sxs-lookup"><span data-stu-id="8ebf7-121">How toowork with Event Hubs</span></span>

<span data-ttu-id="8ebf7-122">Microsoft proporciona un conjunto de componentes de Java que pueden ser utilizado toocommunicate con concentradores de eventos de una topología de Storm.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-122">Microsoft provides a set of Java components that can be used toocommunicate with Event Hubs from a Storm topology.</span></span> <span data-ttu-id="8ebf7-123">Puede encontrar Hola Java (JAR) archivo que contiene una versión compatible de HDInsight 3.6 de estos componentes en [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span><span class="sxs-lookup"><span data-stu-id="8ebf7-123">You can find hello Java archive (JAR) file that contains an HDInsight 3.6 compatible version of these components at [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ebf7-124">Mientras que los componentes de hello están escritos en Java, puede utilizarlos fácilmente de una topología de C#.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-124">While hello components are written in Java, you can easily use them from a C# topology.</span></span>

<span data-ttu-id="8ebf7-125">en este ejemplo se utiliza Hola de los componentes siguientes:</span><span class="sxs-lookup"><span data-stu-id="8ebf7-125">hello following components are used in this example:</span></span>

* <span data-ttu-id="8ebf7-126">__EventHubSpout__: lee datos de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-126">__EventHubSpout__: Reads data from Event Hubs.</span></span>
* <span data-ttu-id="8ebf7-127">__EventHubBolt__: escribe tooEvent centros de datos.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-127">__EventHubBolt__: Writes data tooEvent Hubs.</span></span>
* <span data-ttu-id="8ebf7-128">__EventHubSpoutConfig__: usar tooconfigure EventHubSpout.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-128">__EventHubSpoutConfig__: Used tooconfigure EventHubSpout.</span></span>
* <span data-ttu-id="8ebf7-129">__EventHubBoltConfig__: usar tooconfigure EventHubBolt.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-129">__EventHubBoltConfig__: Used tooconfigure EventHubBolt.</span></span>

### <a name="example-spout-usage"></a><span data-ttu-id="8ebf7-130">Ejemplo de uso de spout</span><span class="sxs-lookup"><span data-stu-id="8ebf7-130">Example spout usage</span></span>

<span data-ttu-id="8ebf7-131">SCP.NET proporciona métodos para agregar una topología de tooyour EventHubSpout.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-131">SCP.NET provides methods for adding an EventHubSpout tooyour topology.</span></span> <span data-ttu-id="8ebf7-132">Estos métodos que sea más fácil tooadd un pitorro que el uso de métodos genéricos de Hola para agregar un componente de Java.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-132">These methods make it easier tooadd a spout than using hello generic methods for adding a Java component.</span></span> <span data-ttu-id="8ebf7-133">Hello en el ejemplo siguiente se muestra cómo toocreate un pitorro utilizando Hola __SetEventHubSpout__ y **EventHubSpoutConfig** métodos proporcionados por SCP.NET:</span><span class="sxs-lookup"><span data-stu-id="8ebf7-133">hello following example demonstrates how toocreate a spout by using hello __SetEventHubSpout__ and **EventHubSpoutConfig** methods provided by SCP.NET:</span></span>

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

<span data-ttu-id="8ebf7-134">ejemplo de Hola anterior crea un nuevo componente de pitorro denominado __EventHubSpout__y configura toocommunicate con un concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-134">hello previous example creates a new spout component named __EventHubSpout__, and configures it toocommunicate with an event hub.</span></span> <span data-ttu-id="8ebf7-135">Sugerencia de paralelismo de Hello para el componente de Hola se establece toohello número de particiones en el centro de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-135">hello parallelism hint for hello component is set toohello number of partitions in hello event hub.</span></span> <span data-ttu-id="8ebf7-136">Esta configuración permite Storm toocreate una instancia del componente de Hola para cada partición.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-136">This setting allows Storm toocreate an instance of hello component for each partition.</span></span>

### <a name="example-bolt-usage"></a><span data-ttu-id="8ebf7-137">Ejemplo de uso de bolt</span><span class="sxs-lookup"><span data-stu-id="8ebf7-137">Example bolt usage</span></span>

<span data-ttu-id="8ebf7-138">Hola de uso **JavaComponmentConstructor** método toocreate una instancia de rayo Hola.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-138">Use hello **JavaComponmentConstructor** method toocreate an instance of hello bolt.</span></span> <span data-ttu-id="8ebf7-139">Hello ejemplo siguiente se muestra cómo toocreate y configurar una nueva instancia de hello **EventHubBolt**:</span><span class="sxs-lookup"><span data-stu-id="8ebf7-139">hello following example demonstrates how toocreate and configure a new instance of hello **EventHubBolt**:</span></span>

```csharp
// Java construcvtor for hello Event Hub Bolt
JavaComponentConstructor constructor = JavaComponentConstructor.CreateFromClojureExpr(
    String.Format(@"(org.apache.storm.eventhubs.bolt.EventHubBolt. (org.apache.storm.eventhubs.bolt.EventHubBoltConfig. " +
        @"""{0}"" ""{1}"" ""{2}"" ""{3}"" ""{4}"" {5}))",
        ConfigurationManager.AppSettings["EventHubPolicyName"],
        ConfigurationManager.AppSettings["EventHubPolicyKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        "servicebus.windows.net",
        ConfigurationManager.AppSettings["EventHubName"],
        "true"));

// Set hello bolt toosubscribe toodata from hello spout
topologyBuilder.SetJavaBolt(
    "eventhubbolt",
    constructor,
    partitionCount)
        .shuffleGrouping("Spout");
```

> [!NOTE]
> <span data-ttu-id="8ebf7-140">Este ejemplo utiliza una expresión de Clojure pasada como una cadena, en lugar de usar **JavaComponentConstructor** toocreate una **EventHubBoltConfig**, tal y como ejemplo de Hola pitorro hacía.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-140">This example uses a Clojure expression passed as a string, instead of using **JavaComponentConstructor** toocreate an **EventHubBoltConfig**, as hello spout example did.</span></span> <span data-ttu-id="8ebf7-141">Cualquiera de estos métodos funciona.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-141">Either method works.</span></span> <span data-ttu-id="8ebf7-142">Utilice el método de Hola que se siente tooyou mejor.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-142">Use hello method that feels best tooyou.</span></span>

## <a name="download-hello-completed-project"></a><span data-ttu-id="8ebf7-143">Descargar proyecto Hola completado</span><span class="sxs-lookup"><span data-stu-id="8ebf7-143">Download hello completed project</span></span>

<span data-ttu-id="8ebf7-144">Puede descargar una versión completa de proyecto Hola creada en este tutorial de [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="8ebf7-144">You can download a complete version of hello project created in this tutorial from [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span> <span data-ttu-id="8ebf7-145">Sin embargo, todavía necesita opciones de configuración de tooprovide siguiendo los pasos de hello en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-145">However, you still need tooprovide configuration settings by following hello steps in this tutorial.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="8ebf7-146">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8ebf7-146">Prerequisites</span></span>

* <span data-ttu-id="8ebf7-147">Una [instancia de Apache Storm en un clúster de HDInsight, versión 3.5 o 3.6](hdinsight-apache-storm-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8ebf7-147">An [Apache Storm on HDInsight cluster version 3.5 or 3.6](hdinsight-apache-storm-tutorial-get-started.md).</span></span>

    > [!WARNING]
    > <span data-ttu-id="8ebf7-148">ejemplo de Hola usado en este documento requiere Storm en HDInsight versión 3.5 o 3.6.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-148">hello example used in this document requires Storm on HDInsight version 3.5 or 3.6.</span></span> <span data-ttu-id="8ebf7-149">Esto no funciona con versiones anteriores de HDInsight, debido a cambios de nombre de clase toobreaking.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-149">This does not work with older versions of HDInsight, due toobreaking class name changes.</span></span> <span data-ttu-id="8ebf7-150">Para obtener una versión de este ejemplo que funcione con clústeres anteriores, vea [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span><span class="sxs-lookup"><span data-stu-id="8ebf7-150">For a version of this example that works with older clusters, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span></span>

* <span data-ttu-id="8ebf7-151">Un [centro de eventos de Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="8ebf7-151">An [Azure event hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="8ebf7-152">Hola [Azure SDK para .NET](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="8ebf7-152">hello [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>

* <span data-ttu-id="8ebf7-153">Hola [HDInsight tools para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8ebf7-153">hello [HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="8ebf7-154">Java JDK 1.8 o posterior en el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-154">Java JDK 1.8 or later on your development environment.</span></span> <span data-ttu-id="8ebf7-155">Las descargas de JDK están disponibles en [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="8ebf7-155">JDK downloads are available from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>

  * <span data-ttu-id="8ebf7-156">Hola **JAVA_HOME** entorno debe variable punto toohello el directorio que contiene Java.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-156">hello **JAVA_HOME** environment variable must point toohello directory that contains Java.</span></span>
  * <span data-ttu-id="8ebf7-157">Hola **%JAVA_HOME%/bin** directorio debe estar en la ruta de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-157">hello **%JAVA_HOME%/bin** directory must be in hello path.</span></span>

## <a name="download-hello-event-hubs-components"></a><span data-ttu-id="8ebf7-158">Descargar los componentes de los centros de eventos de Hola</span><span class="sxs-lookup"><span data-stu-id="8ebf7-158">Download hello Event Hubs components</span></span>

<span data-ttu-id="8ebf7-159">Descarga Hola centros de eventos apetezca charlar y el tornillo del componente de [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span><span class="sxs-lookup"><span data-stu-id="8ebf7-159">Download hello Event Hubs spout and bolt component from [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

<span data-ttu-id="8ebf7-160">Cree un directorio denominado `eventhubspout`y guarde el archivo de hello en el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-160">Create a directory named `eventhubspout`, and save hello file into hello directory.</span></span>

## <a name="configure-event-hubs"></a><span data-ttu-id="8ebf7-161">Configuración de Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="8ebf7-161">Configure Event Hubs</span></span>

<span data-ttu-id="8ebf7-162">Centros de eventos es el origen de datos de Hola para este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-162">Event Hubs is hello data source for this example.</span></span> <span data-ttu-id="8ebf7-163">Utilice la información de hello en la sección "Crear un concentrador de eventos" de Hola de [empezar a trabajar con concentradores de eventos](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="8ebf7-163">Use hello information in hello "Create an event hub" section of [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

1. <span data-ttu-id="8ebf7-164">Una vez creado el concentrador de eventos de hello, ver hello **EventHub** hoja en hello Azure portal y, a continuación, seleccione **directivas de acceso compartido**.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-164">After hello event hub has been created, view hello **EventHub** blade in hello Azure portal, and select **Shared access policies**.</span></span> <span data-ttu-id="8ebf7-165">Seleccione **+ agregar** hello tooadd las siguientes directivas:</span><span class="sxs-lookup"><span data-stu-id="8ebf7-165">Select **+ Add** tooadd hello following policies:</span></span>

   | <span data-ttu-id="8ebf7-166">Nombre</span><span class="sxs-lookup"><span data-stu-id="8ebf7-166">Name</span></span> | <span data-ttu-id="8ebf7-167">Permisos</span><span class="sxs-lookup"><span data-stu-id="8ebf7-167">Permissions</span></span> |
   | --- | --- |
   | <span data-ttu-id="8ebf7-168">escritor</span><span class="sxs-lookup"><span data-stu-id="8ebf7-168">writer</span></span> |<span data-ttu-id="8ebf7-169">Los métodos Send</span><span class="sxs-lookup"><span data-stu-id="8ebf7-169">Send</span></span> |
   | <span data-ttu-id="8ebf7-170">lector</span><span class="sxs-lookup"><span data-stu-id="8ebf7-170">reader</span></span> |<span data-ttu-id="8ebf7-171">Escuchar</span><span class="sxs-lookup"><span data-stu-id="8ebf7-171">Listen</span></span> |

    ![Captura de pantalla de la ventana Directivas de acceso compartido](./media/hdinsight-storm-develop-csharp-event-hub-topology/sas.png)

2. <span data-ttu-id="8ebf7-173">Seleccione hello **lector** y **escritor** directivas.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-173">Select hello **reader** and **writer** policies.</span></span> <span data-ttu-id="8ebf7-174">Copie y guarde el valor de clave principal de Hola para las dos directivas, ya que estos valores se usan más adelante.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-174">Copy and save hello primary key value for both policies, as these values are used later.</span></span>

## <a name="configure-hello-eventhubwriter"></a><span data-ttu-id="8ebf7-175">Configurar hello EventHubWriter</span><span class="sxs-lookup"><span data-stu-id="8ebf7-175">Configure hello EventHubWriter</span></span>

1. <span data-ttu-id="8ebf7-176">Si no ha instalado ya Hola versión más reciente de las herramientas de HDInsight de Hola para Visual Studio, consulte [Introducción al uso de herramientas de HDInsight para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8ebf7-176">If you have not already installed hello latest version of hello HDInsight tools for Visual Studio, see [Get started using HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="8ebf7-177">Descargue la solución Hola de [eventhub-storm-híbrida](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="8ebf7-177">Download hello solution from [eventhub-storm-hybrid](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

3. <span data-ttu-id="8ebf7-178">Hola **EventHubWriter** proyecto, abra hello **App.config** archivo.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-178">In hello **EventHubWriter** project, open hello **App.config** file.</span></span> <span data-ttu-id="8ebf7-179">Utilice información de Hola de concentrador de eventos de Hola que configuró toofill anterior en el valor de Hola para hello siguiendo las claves:</span><span class="sxs-lookup"><span data-stu-id="8ebf7-179">Use hello information from hello event hub that you configured earlier toofill in hello value for hello following keys:</span></span>

   | <span data-ttu-id="8ebf7-180">Clave</span><span class="sxs-lookup"><span data-stu-id="8ebf7-180">Key</span></span> | <span data-ttu-id="8ebf7-181">Valor</span><span class="sxs-lookup"><span data-stu-id="8ebf7-181">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="8ebf7-182">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="8ebf7-182">EventHubPolicyName</span></span> |<span data-ttu-id="8ebf7-183">sistema de escritura (si utiliza un nombre diferente para la directiva de hello con *enviar* permiso, utilizarlo en su lugar.)</span><span class="sxs-lookup"><span data-stu-id="8ebf7-183">writer (If you used a different name for hello policy with *Send* permission, use it instead.)</span></span> |
   | <span data-ttu-id="8ebf7-184">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="8ebf7-184">EventHubPolicyKey</span></span> |<span data-ttu-id="8ebf7-185">clave de Hello para la directiva de sistema de escritura de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-185">hello key for hello writer policy.</span></span> |
   | <span data-ttu-id="8ebf7-186">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="8ebf7-186">EventHubNamespace</span></span> |<span data-ttu-id="8ebf7-187">Hola espacio de nombres que contiene el centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-187">hello namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="8ebf7-188">EventHubName</span><span class="sxs-lookup"><span data-stu-id="8ebf7-188">EventHubName</span></span> |<span data-ttu-id="8ebf7-189">Nombre del centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-189">Your event hub name.</span></span> |
   | <span data-ttu-id="8ebf7-190">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="8ebf7-190">EventHubPartitionCount</span></span> |<span data-ttu-id="8ebf7-191">número de Hola de particiones en el centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-191">hello number of partitions in your event hub.</span></span> |

4. <span data-ttu-id="8ebf7-192">Guarde y cierre hello **App.config** archivo.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-192">Save and close hello **App.config** file.</span></span>

## <a name="configure-hello-eventhubreader"></a><span data-ttu-id="8ebf7-193">Configurar hello EventHubReader</span><span class="sxs-lookup"><span data-stu-id="8ebf7-193">Configure hello EventHubReader</span></span>

1. <span data-ttu-id="8ebf7-194">Abra hello **EventHubReader** proyecto.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-194">Open hello **EventHubReader** project.</span></span>

2. <span data-ttu-id="8ebf7-195">Abra hello **App.config** archivo para hello **EventHubReader**.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-195">Open hello **App.config** file for hello **EventHubReader**.</span></span> <span data-ttu-id="8ebf7-196">Utilice información de Hola de concentrador de eventos de Hola que configuró toofill anterior en el valor de Hola para hello siguiendo las claves:</span><span class="sxs-lookup"><span data-stu-id="8ebf7-196">Use hello information from hello event hub that you configured earlier toofill in hello value for hello following keys:</span></span>

   | <span data-ttu-id="8ebf7-197">Clave</span><span class="sxs-lookup"><span data-stu-id="8ebf7-197">Key</span></span> | <span data-ttu-id="8ebf7-198">Valor</span><span class="sxs-lookup"><span data-stu-id="8ebf7-198">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="8ebf7-199">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="8ebf7-199">EventHubPolicyName</span></span> |<span data-ttu-id="8ebf7-200">lector (si utiliza un nombre diferente para la directiva de hello con *escuchar* permiso, utilizarlo en su lugar.)</span><span class="sxs-lookup"><span data-stu-id="8ebf7-200">reader (If you used a different name for hello policy with *listen* permission, use it instead.)</span></span> |
   | <span data-ttu-id="8ebf7-201">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="8ebf7-201">EventHubPolicyKey</span></span> |<span data-ttu-id="8ebf7-202">clave de Hola para directiva de lector de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-202">hello key for hello reader policy.</span></span> |
   | <span data-ttu-id="8ebf7-203">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="8ebf7-203">EventHubNamespace</span></span> |<span data-ttu-id="8ebf7-204">Hola espacio de nombres que contiene el centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-204">hello namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="8ebf7-205">EventHubName</span><span class="sxs-lookup"><span data-stu-id="8ebf7-205">EventHubName</span></span> |<span data-ttu-id="8ebf7-206">Nombre del centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-206">Your event hub name.</span></span> |
   | <span data-ttu-id="8ebf7-207">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="8ebf7-207">EventHubPartitionCount</span></span> |<span data-ttu-id="8ebf7-208">número de Hola de particiones en el centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-208">hello number of partitions in your event hub.</span></span> |

3. <span data-ttu-id="8ebf7-209">Guarde y cierre hello **App.config** archivo.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-209">Save and close hello **App.config** file.</span></span>

## <a name="deploy-hello-topologies"></a><span data-ttu-id="8ebf7-210">Implementar topologías de Hola</span><span class="sxs-lookup"><span data-stu-id="8ebf7-210">Deploy hello topologies</span></span>

1. <span data-ttu-id="8ebf7-211">De **el Explorador de soluciones**, contextual hello **EventHubReader** de proyecto y seleccione **enviar tooStorm en HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-211">From **Solution Explorer**, right-click hello **EventHubReader** project, and select **Submit tooStorm on HDInsight**.</span></span>

    ![Captura de pantalla del explorador de soluciones, con enviar tooStorm en HDInsight resaltado](./media/hdinsight-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. <span data-ttu-id="8ebf7-213">En hello **topología enviar** cuadro de diálogo, seleccione la **clúster de Storm**.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-213">On hello **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="8ebf7-214">Expanda **configuraciones adicionales**, seleccione **las rutas de acceso de Java**, seleccione **...** y un directorio de hello select que contiene el archivo JAR de Hola que ha descargado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-214">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select hello directory that contains hello JAR file that you downloaded earlier.</span></span> <span data-ttu-id="8ebf7-215">Finalmente, haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-215">Finally, click **Submit**.</span></span>

    ![Captura de pantalla del cuadro de diálogo Enviar topología](./media/hdinsight-storm-develop-csharp-event-hub-topology/submit.png)

3. <span data-ttu-id="8ebf7-217">Cuando se ha enviado la topología de hello, Hola **aluvión de topologías Visor** aparece.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-217">When hello topology has been submitted, hello **Storm Topologies Viewer** appears.</span></span> <span data-ttu-id="8ebf7-218">tooview información acerca de la topología de hello, seleccione hello **EventHubReader** topología en el panel izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-218">tooview information about hello topology, select hello **EventHubReader** topology in hello left pane.</span></span>

    ![Captura de pantalla del Visor de topologías de Storm](./media/hdinsight-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. <span data-ttu-id="8ebf7-220">De **el Explorador de soluciones**, contextual hello **EventHubWriter** de proyecto y seleccione **enviar tooStorm en HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-220">From **Solution Explorer**, right-click hello **EventHubWriter** project, and select **Submit tooStorm on HDInsight**.</span></span>

5. <span data-ttu-id="8ebf7-221">En hello **topología enviar** cuadro de diálogo, seleccione la **clúster de Storm**.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-221">On hello **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="8ebf7-222">Expanda **configuraciones adicionales**, seleccione **las rutas de acceso de Java**, seleccione **...** , y el directorio de hello select que contiene el archivo JAR de Hola descargó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-222">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select hello directory that contains hello JAR file you downloaded earlier.</span></span> <span data-ttu-id="8ebf7-223">Finalmente, haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-223">Finally, click **Submit**.</span></span>

6. <span data-ttu-id="8ebf7-224">Cuando se ha enviado la topología de hello, actualice la lista de topología de Hola Hola **aluvión de topologías Visor** tooverify que todas estas topologías se ejecutan en el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-224">When hello topology has been submitted, refresh hello topology list in hello **Storm Topologies Viewer** tooverify that both topologies are running on hello cluster.</span></span>

7. <span data-ttu-id="8ebf7-225">En **aluvión de topologías Visor**, seleccione hello **EventHubReader** topología.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-225">In **Storm Topologies Viewer**, select hello **EventHubReader** topology.</span></span>

8. <span data-ttu-id="8ebf7-226">componente de hello tooopen resumen rayo de hello, haga doble clic en hello **LogBolt** componente en el diagrama de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-226">tooopen hello component summary for hello bolt, double-click hello **LogBolt** component in hello diagram.</span></span>

9. <span data-ttu-id="8ebf7-227">Hola **ejecutor** sección, seleccione uno de los vínculos de Hola Hola **puerto** columna.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-227">In hello **Executors** section, select one of hello links in hello **Port** column.</span></span> <span data-ttu-id="8ebf7-228">Esto muestra la información registrada por el componente de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-228">This displays information logged by hello component.</span></span> <span data-ttu-id="8ebf7-229">información de Hello optimizado es similar toohello siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="8ebf7-229">hello logged information is similar toohello following text:</span></span>

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-hello-topologies"></a><span data-ttu-id="8ebf7-230">Detener las topologías de Hola</span><span class="sxs-lookup"><span data-stu-id="8ebf7-230">Stop hello topologies</span></span>

<span data-ttu-id="8ebf7-231">topologías de hello toostop, seleccione cada topología de hello **Visor de la topología de Storm**, a continuación, haga clic en **Kill**.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-231">toostop hello topologies, select each topology in hello **Storm Topology Viewer**, then click **Kill**.</span></span>

![Captura de pantalla del Visor de topologías de Storm con el botón Eliminar resaltado](./media/hdinsight-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="8ebf7-233">Eliminación del clúster</span><span class="sxs-lookup"><span data-stu-id="8ebf7-233">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="8ebf7-234">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8ebf7-234">Next steps</span></span>

<span data-ttu-id="8ebf7-235">En este documento, ha aprendido cómo toouse Hola Java y centros de eventos apetezca charlar un tornillo desde un toowork de topología de C# con datos en los centros de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ebf7-235">In this document, you have learned how toouse hello Java Event Hubs spout and bolt from a C# topology toowork with data in Azure Event Hubs.</span></span> <span data-ttu-id="8ebf7-236">toolearn más información acerca de la creación de topologías de C#, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="8ebf7-236">toolearn more about creating C# topologies, see hello following:</span></span>

* [<span data-ttu-id="8ebf7-237">Desarrollo de topologías de C# para Apache Storm en HDInsight con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8ebf7-237">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="8ebf7-238">Guía de programación de SCP</span><span class="sxs-lookup"><span data-stu-id="8ebf7-238">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)
* [<span data-ttu-id="8ebf7-239">Topologías de ejemplo para Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="8ebf7-239">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
