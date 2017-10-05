---
title: "Poner en correlación eventos con el tiempo con Storm y HBase en HDInsight"
description: "Aprenda a poner en correlación los eventos que llegan en distintos momentos con Storm y HBase en HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 17d11479-2d02-4790-8d29-05fb38351479
ms.service: hdinsight
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 06630096383601e48e8f69f8553314cee42f5f3e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="correlate-events-that-arrive-at-different-times-using-storm-and-hbase"></a><span data-ttu-id="3c64b-103">Correlación de eventos que llegan a diferentes horas con Storm y HBase</span><span class="sxs-lookup"><span data-stu-id="3c64b-103">Correlate events that arrive at different times using Storm and HBase</span></span>

<span data-ttu-id="3c64b-104">Si utiliza un almacén de datos persistente con Apache Storm, puede poner en correlación entradas de datos que llegan en distintos momentos.</span><span class="sxs-lookup"><span data-stu-id="3c64b-104">By using a persistent data store with Apache Storm, you can correlate data entries that arrive at different times.</span></span> <span data-ttu-id="3c64b-105">Por ejemplo, puede vincular eventos de inicio y cierre de sesión de una sesión de usuario para calcular cuánto tiempo duró la sesión.</span><span class="sxs-lookup"><span data-stu-id="3c64b-105">For example, linking login and logout events for a user session to calculate how long the session lasted.</span></span>

<span data-ttu-id="3c64b-106">En este documento, obtendrá información sobre cómo crear una topología básica de Storm de C# que realice un seguimiento de los eventos de inicio y cierre de sesión de las sesiones de usuario y calcule la duración de la sesión.</span><span class="sxs-lookup"><span data-stu-id="3c64b-106">In this document, you learn how to create a basic C# Storm topology that tracks login and logout events for user sessions, and calculates the duration of the session.</span></span> <span data-ttu-id="3c64b-107">La topología utiliza HBase como un almacén de datos persistente.</span><span class="sxs-lookup"><span data-stu-id="3c64b-107">The topology uses HBase as a persistent data store.</span></span> <span data-ttu-id="3c64b-108">HBase también permite realizar consultas por lotes en los datos históricos para generar información adicional.</span><span class="sxs-lookup"><span data-stu-id="3c64b-108">HBase also allows you to perform batch queries on the historical data to produce additional insights.</span></span> <span data-ttu-id="3c64b-109">Por ejemplo, la cantidad de sesiones de usuario que se iniciaron o terminaron durante un período de tiempo específico.</span><span class="sxs-lookup"><span data-stu-id="3c64b-109">For example, how many user sessions were started or ended during a specific time period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c64b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3c64b-110">Prerequisites</span></span>

* <span data-ttu-id="3c64b-111">Visual Studio y las herramientas de HDInsight para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3c64b-111">Visual Studio and the HDInsight tools for Visual Studio.</span></span> <span data-ttu-id="3c64b-112">Para más información, vea [Introducción al uso de las herramientas de HDInsight para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3c64b-112">For more information, see [Get started using the HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="3c64b-113">Apache Storm en clústeres de HDInsight (Windows)</span><span class="sxs-lookup"><span data-stu-id="3c64b-113">Apache Storm on HDInsight cluster (Windows-based).</span></span>

  > [!WARNING]
  > <span data-ttu-id="3c64b-114">Aunque se admiten topologías SCP.NET en clústeres de Storm basados en Linux creados después del 28/10/2016, el SDK de HBase para el paquete de .NET disponible a partir del 28/10/2016 no funciona correctamente en HDInsight basado en Linux</span><span class="sxs-lookup"><span data-stu-id="3c64b-114">While SCP.NET topologies are supported on Linux-based Storm clusters created after 10/28/2016, the HBase SDK for .NET package available as of 10/28/2016 does not work correctly on Linux-based HDInsight</span></span>

* <span data-ttu-id="3c64b-115">Apache HBase en un clúster de HDInsight (basado en Linux o Windows).</span><span class="sxs-lookup"><span data-stu-id="3c64b-115">Apache HBase on HDInsight cluster (Linux or Windows-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="3c64b-116">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="3c64b-116">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3c64b-117">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="3c64b-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="3c64b-118">[Java](https://java.com) 1.7 o superior en el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="3c64b-118">[Java](https://java.com) 1.7 or greater on your development environment.</span></span> <span data-ttu-id="3c64b-119">Java se utiliza para empaquetar la topología cuando se envía al clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3c64b-119">Java is used to package the topology when it is submitted to the HDInsight cluster.</span></span>

  * <span data-ttu-id="3c64b-120">La variable de entorno **JAVA_HOME** debe señalar al directorio que contiene Java.</span><span class="sxs-lookup"><span data-stu-id="3c64b-120">The **JAVA_HOME** environment variable must point to the directory that contains Java.</span></span>
  * <span data-ttu-id="3c64b-121">El directorio **%JAVA_HOME%/bin** debe estar en la ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="3c64b-121">The **%JAVA_HOME%/bin** directory must be in the path</span></span>

## <a name="architecture"></a><span data-ttu-id="3c64b-122">Arquitectura</span><span class="sxs-lookup"><span data-stu-id="3c64b-122">Architecture</span></span>

![Diagrama del flujo de datos a través de la topología](./media/hdinsight-storm-correlation-topology/correlationtopology.png)

<span data-ttu-id="3c64b-124">La correlación de eventos requiere un identificador común para el origen del evento.</span><span class="sxs-lookup"><span data-stu-id="3c64b-124">Correlating events requires a common identifier for the event source.</span></span> <span data-ttu-id="3c64b-125">Por ejemplo, un id. de usuario, un id. de sesión u otra parte de los datos que a) sea única y (b) se incluya en todos los datos enviados a Storm.</span><span class="sxs-lookup"><span data-stu-id="3c64b-125">For example, a user ID, session ID, or other piece of data that is a) unique and b) included in all data sent to Storm.</span></span> <span data-ttu-id="3c64b-126">En este ejemplo se utiliza un valor GUID para representar un identificador de sesión.</span><span class="sxs-lookup"><span data-stu-id="3c64b-126">This example uses a GUID value to represent a session ID.</span></span>

<span data-ttu-id="3c64b-127">Este ejemplo consta de dos clústeres de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="3c64b-127">This example consists of two HDInsight clusters:</span></span>

* <span data-ttu-id="3c64b-128">HBase: almacén de datos persistente para los datos históricos</span><span class="sxs-lookup"><span data-stu-id="3c64b-128">HBase: persistent data store for historical data</span></span>
* <span data-ttu-id="3c64b-129">Storm: se utiliza para introducir datos de entrada</span><span class="sxs-lookup"><span data-stu-id="3c64b-129">Storm: used to ingest incoming data</span></span>

<span data-ttu-id="3c64b-130">Los datos se generan aleatoriamente mediante la topología de Storm y constan de los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="3c64b-130">The data is randomly generated by the Storm topology, and consists of the following items:</span></span>

* <span data-ttu-id="3c64b-131">Id. de sesión: un GUID que identifica de forma única cada sesión</span><span class="sxs-lookup"><span data-stu-id="3c64b-131">Session ID: a GUID that uniquely identifies each session</span></span>
* <span data-ttu-id="3c64b-132">Evento: evento de INICIO o FINALIZACIÓN.</span><span class="sxs-lookup"><span data-stu-id="3c64b-132">Event: a START or END event.</span></span> <span data-ttu-id="3c64b-133">En este ejemplo, INICIO siempre tiene lugar antes de la FINALIZACIÓN</span><span class="sxs-lookup"><span data-stu-id="3c64b-133">For this example, START always occurs before END</span></span>
* <span data-ttu-id="3c64b-134">Hora: hora del evento.</span><span class="sxs-lookup"><span data-stu-id="3c64b-134">Time: the time of the event.</span></span>

<span data-ttu-id="3c64b-135">Estos datos se procesan y almacenan en HBase.</span><span class="sxs-lookup"><span data-stu-id="3c64b-135">This data is processed and stored in HBase.</span></span>

### <a name="storm-topology"></a><span data-ttu-id="3c64b-136">Topología de Storm</span><span class="sxs-lookup"><span data-stu-id="3c64b-136">Storm topology</span></span>

<span data-ttu-id="3c64b-137">Cuando se inicia una sesión, la topología recibe un evento de **INICIO** y este se registra en HBase.</span><span class="sxs-lookup"><span data-stu-id="3c64b-137">When a session starts, a **START** event is received by the topology and logged to HBase.</span></span> <span data-ttu-id="3c64b-138">Cuando se recibe el evento de **FIN**, la topología recupera el evento de **INICIO** y calcula el tiempo entre los dos eventos.</span><span class="sxs-lookup"><span data-stu-id="3c64b-138">When an **END** event is received, the topology retrieves the **START** event and calculates the time between the two events.</span></span> <span data-ttu-id="3c64b-139">Después, este valor de **Duración** se almacena en HBase junto con la información del evento de **FIN**.</span><span class="sxs-lookup"><span data-stu-id="3c64b-139">This **Duration** value is then stored in HBase along with the **END** event information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3c64b-140">Aunque esta topología muestra el patrón básico, una solución de producción debería tener diseño para los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="3c64b-140">While this topology demonstrates the basic pattern, a production solution would need to take design for the following scenarios:</span></span>
>
> * <span data-ttu-id="3c64b-141">Eventos que llegan sin orden</span><span class="sxs-lookup"><span data-stu-id="3c64b-141">Events arriving out of order</span></span>
> * <span data-ttu-id="3c64b-142">Eventos duplicados</span><span class="sxs-lookup"><span data-stu-id="3c64b-142">Duplicate events</span></span>
> * <span data-ttu-id="3c64b-143">Eventos quitados</span><span class="sxs-lookup"><span data-stu-id="3c64b-143">Dropped events</span></span>

<span data-ttu-id="3c64b-144">La topología de ejemplo consta de los siguientes componentes:</span><span class="sxs-lookup"><span data-stu-id="3c64b-144">The sample topology is composed of the following components:</span></span>

* <span data-ttu-id="3c64b-145">Session.cs: simula una sesión de usuario al crear un identificador de sesión aleatorio, una hora de inicio y una duración de la sesión.</span><span class="sxs-lookup"><span data-stu-id="3c64b-145">Session.cs: simulates a user session by creating a random session ID, start time, and how long the session lasts.</span></span>

* <span data-ttu-id="3c64b-146">Spout.cs: crea 100 sesiones, emite un evento de INICIO, espera el tiempo de espera aleatorio para cada sesión y, después, emite un evento de FINALIZACIÓN.</span><span class="sxs-lookup"><span data-stu-id="3c64b-146">Spout.cs: creates 100 sessions, emits a START event, waits the random timeout for each session, and then emits an END event.</span></span> <span data-ttu-id="3c64b-147">A continuación, recicla las sesiones finalizadas para generar otras nuevas.</span><span class="sxs-lookup"><span data-stu-id="3c64b-147">Then recycles ended sessions to generate new ones.</span></span>

* <span data-ttu-id="3c64b-148">HBaseLookupBolt.cs: usa el identificador de sesión para buscar información de sesión de HBase.</span><span class="sxs-lookup"><span data-stu-id="3c64b-148">HBaseLookupBolt.cs: uses the session ID to look up session information from HBase.</span></span> <span data-ttu-id="3c64b-149">Cuando se procesa un evento de FINALIZACIÓN, busca el evento de INICIO correspondiente y calcula la duración de la sesión.</span><span class="sxs-lookup"><span data-stu-id="3c64b-149">When an END event is processed, it finds the corresponding START event and calculates the duration of the session.</span></span>

* <span data-ttu-id="3c64b-150">HBaseBolt.cs: almacena información en HBase.</span><span class="sxs-lookup"><span data-stu-id="3c64b-150">HBaseBolt.cs: Stores information into HBase.</span></span>

* <span data-ttu-id="3c64b-151">TypeHelper.cs: ayuda con la conversión de tipos al leer desde HBase o escribir en él.</span><span class="sxs-lookup"><span data-stu-id="3c64b-151">TypeHelper.cs: Helps with type conversion when reading from/writing to HBase.</span></span>

### <a name="hbase-schema"></a><span data-ttu-id="3c64b-152">Esquema de HBase</span><span class="sxs-lookup"><span data-stu-id="3c64b-152">HBase schema</span></span>

<span data-ttu-id="3c64b-153">En HBase, los datos se almacenan en una tabla con la configuración y el esquema siguiente:</span><span class="sxs-lookup"><span data-stu-id="3c64b-153">In HBase, the data is stored in a table with the following schema/settings:</span></span>

* <span data-ttu-id="3c64b-154">Clave de fila: el identificador de sesión se utiliza como clave para las filas de esta tabla.</span><span class="sxs-lookup"><span data-stu-id="3c64b-154">Row key: the session ID is used as the key for rows in this table.</span></span>

* <span data-ttu-id="3c64b-155">Familia de columnas: el nombre de familia es 'cf'.</span><span class="sxs-lookup"><span data-stu-id="3c64b-155">Column family: the family name is 'cf'.</span></span> <span data-ttu-id="3c64b-156">Las columnas almacenadas en esta familia son:</span><span class="sxs-lookup"><span data-stu-id="3c64b-156">Columns stored in this family are:</span></span>

  * <span data-ttu-id="3c64b-157">evento: INICIO o FINALIZACIÓN.</span><span class="sxs-lookup"><span data-stu-id="3c64b-157">event: START or END.</span></span>

  * <span data-ttu-id="3c64b-158">hora: hora en milisegundos en la que se produjo el evento.</span><span class="sxs-lookup"><span data-stu-id="3c64b-158">time: the time in milliseconds that the event occurred.</span></span>

  * <span data-ttu-id="3c64b-159">duración: la duración entre los eventos de INICIO y FINALIZACIÓN.</span><span class="sxs-lookup"><span data-stu-id="3c64b-159">duration: the length between START and END event.</span></span>

* <span data-ttu-id="3c64b-160">VERSIONES: la familia "cf" se establece para conservar 5 versiones de cada fila.</span><span class="sxs-lookup"><span data-stu-id="3c64b-160">VERSIONS: the 'cf' family is set to retain 5 versions of each row.</span></span>

  > [!NOTE]
  > <span data-ttu-id="3c64b-161">Las versiones son un registro de los valores anteriores almacenados para una clave de fila específica.</span><span class="sxs-lookup"><span data-stu-id="3c64b-161">Versions are a log of previous values stored for a specific row key.</span></span> <span data-ttu-id="3c64b-162">De forma predeterminada, HBase solo devuelve el valor de la versión más reciente de una fila.</span><span class="sxs-lookup"><span data-stu-id="3c64b-162">By default, HBase only returns the value for the most recent version of a row.</span></span> <span data-ttu-id="3c64b-163">En este caso, se utiliza la misma fila para todos los eventos (INICIO y FINALIZACIÓN). Cada versión de una fila se identifica mediante el valor de marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="3c64b-163">In this case, the same row is used for all events (START, END.) each version of a row is identified by the timestamp value.</span></span> <span data-ttu-id="3c64b-164">Las versiones proporcionan una vista histórica de los eventos registrados para un identificador concreto.</span><span class="sxs-lookup"><span data-stu-id="3c64b-164">Versions provide a historical view of events logged for a specific ID.</span></span>

## <a name="download-the-project"></a><span data-ttu-id="3c64b-165">Descarga del proyecto</span><span class="sxs-lookup"><span data-stu-id="3c64b-165">Download the project</span></span>

<span data-ttu-id="3c64b-166">Se puede descargar un proyecto de ejemplo en [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span><span class="sxs-lookup"><span data-stu-id="3c64b-166">The sample project can be downloaded from [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span></span>

<span data-ttu-id="3c64b-167">Esta descarga contiene los proyectos de C# siguientes:</span><span class="sxs-lookup"><span data-stu-id="3c64b-167">This download contains the following C# projects:</span></span>

* <span data-ttu-id="3c64b-168">CorrelationTopology: topología de Storm de C# que emite aleatoriamente eventos de inicio y finalización para las sesiones de usuario.</span><span class="sxs-lookup"><span data-stu-id="3c64b-168">CorrelationTopology: C# Storm topology that randomly emits start and end events for user sessions.</span></span> <span data-ttu-id="3c64b-169">Cada sesión dura entre 1 y 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="3c64b-169">Each session lasts between 1 and 5 minutes.</span></span>

* <span data-ttu-id="3c64b-170">SessionInfo: aplicación de consola de C# que crea la tabla de HBase y proporciona consultas de ejemplo para devolver información acerca de los datos de sesión almacenados.</span><span class="sxs-lookup"><span data-stu-id="3c64b-170">SessionInfo: C# console application that creates the HBase table, and provides example queries to return information about stored session data.</span></span>

## <a name="create-the-table"></a><span data-ttu-id="3c64b-171">Cree la tabla</span><span class="sxs-lookup"><span data-stu-id="3c64b-171">Create the table</span></span>

1. <span data-ttu-id="3c64b-172">Abra el proyecto **SessionInfo** en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3c64b-172">Open the **SessionInfo** project in Visual Studio.</span></span>

2. <span data-ttu-id="3c64b-173">En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto **SessionInfo** y seleccione **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="3c64b-173">In **Solution Explorer**, right-click the **SessionInfo** project and select **Properties**.</span></span>

    ![Captura de pantalla del menú con propiedades seleccionadas](./media/hdinsight-storm-correlation-topology/selectproperties.png)

3. <span data-ttu-id="3c64b-175">Seleccione **Configuración**y, a continuación, establezca los valores siguientes:</span><span class="sxs-lookup"><span data-stu-id="3c64b-175">Select **Settings**, then set the following values:</span></span>

   * <span data-ttu-id="3c64b-176">HBaseClusterURL: la dirección URL del clúster de HBase.</span><span class="sxs-lookup"><span data-stu-id="3c64b-176">HBaseClusterURL: the URL to your HBase cluster.</span></span> <span data-ttu-id="3c64b-177">Por ejemplo, https://myhbasecluster.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="3c64b-177">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="3c64b-178">HBaseClusterUserName: cuenta de usuario de administrador/HTTP para el clúster</span><span class="sxs-lookup"><span data-stu-id="3c64b-178">HBaseClusterUserName: the admin/HTTP user account for your cluster</span></span>

   * <span data-ttu-id="3c64b-179">HBaseClusterPassword: contraseña de la cuenta de usuario de administrador/HTTP</span><span class="sxs-lookup"><span data-stu-id="3c64b-179">HBaseClusterPassword: the password for the admin/HTTP user account</span></span>

   * <span data-ttu-id="3c64b-180">HBaseTableName: nombre de la tabla que se debe utilizar con este ejemplo</span><span class="sxs-lookup"><span data-stu-id="3c64b-180">HBaseTableName: the name of the table to use with this example</span></span>

   * <span data-ttu-id="3c64b-181">HBaseTableColumnFamily: nombre de la familia de columnas</span><span class="sxs-lookup"><span data-stu-id="3c64b-181">HBaseTableColumnFamily: The column family name</span></span>

     ![Imagen del cuadro de diálogo de configuración](./media/hdinsight-storm-correlation-topology/settings.png)

4. <span data-ttu-id="3c64b-183">Ejecute la solución.</span><span class="sxs-lookup"><span data-stu-id="3c64b-183">Run the solution.</span></span> <span data-ttu-id="3c64b-184">Cuando se le pida, seleccione la tecla 'c' para crear la tabla en el clúster de HBase.</span><span class="sxs-lookup"><span data-stu-id="3c64b-184">When prompted, select the 'c' key to create the table on your HBase cluster.</span></span>

## <a name="build-and-deploy-the-storm-topology"></a><span data-ttu-id="3c64b-185">Compilar e implementar la topología de Storm</span><span class="sxs-lookup"><span data-stu-id="3c64b-185">Build and deploy the Storm topology</span></span>

1. <span data-ttu-id="3c64b-186">Abra la solución **CorrelationTopology** en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3c64b-186">Open the **CorrelationTopology** solution in Visual Studio.</span></span>

2. <span data-ttu-id="3c64b-187">En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto **CorrelationTopology** y seleccione Propiedades.</span><span class="sxs-lookup"><span data-stu-id="3c64b-187">In **Solution Explorer**, right-click the **CorrelationTopology** project and select properties.</span></span>

3. <span data-ttu-id="3c64b-188">En la ventana de propiedades, seleccione **Configuración** y escriba los valores de configuración para este proyecto.</span><span class="sxs-lookup"><span data-stu-id="3c64b-188">In the properties window, select **Settings** and enter the configuration values for this project.</span></span> <span data-ttu-id="3c64b-189">Los cinco primeros valores son los mismos usados en el proyecto **SessionInfo**:</span><span class="sxs-lookup"><span data-stu-id="3c64b-189">The first 5 are the same values used by the **SessionInfo** project:</span></span>

   * <span data-ttu-id="3c64b-190">HBaseClusterURL: la dirección URL del clúster de HBase.</span><span class="sxs-lookup"><span data-stu-id="3c64b-190">HBaseClusterURL: the URL to your HBase cluster.</span></span> <span data-ttu-id="3c64b-191">Por ejemplo, https://myhbasecluster.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="3c64b-191">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="3c64b-192">HBaseClusterUserName: cuenta de usuario de administrador/HTTP para el clúster.</span><span class="sxs-lookup"><span data-stu-id="3c64b-192">HBaseClusterUserName: the admin/HTTP user account for your cluster.</span></span>

   * <span data-ttu-id="3c64b-193">HBaseClusterPassword: contraseña de la cuenta de usuario de administrador/HTTP.</span><span class="sxs-lookup"><span data-stu-id="3c64b-193">HBaseClusterPassword: the password for the admin/HTTP user account.</span></span>

   * <span data-ttu-id="3c64b-194">HBaseTableName: nombre de la tabla que se debe utilizar con este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3c64b-194">HBaseTableName: the name of the table to use with this example.</span></span> <span data-ttu-id="3c64b-195">Este valor es el mismo nombre de tabla que se usa en el proyecto SessionInfo.</span><span class="sxs-lookup"><span data-stu-id="3c64b-195">This value is the same table name as used in the SessionInfo project.</span></span>

   * <span data-ttu-id="3c64b-196">HBaseTableColumnFamily: nombre de la familia de columnas.</span><span class="sxs-lookup"><span data-stu-id="3c64b-196">HBaseTableColumnFamily: The column family name.</span></span> <span data-ttu-id="3c64b-197">Este valor es el mismo nombre de familia de columnas que se usa en el proyecto SessionInfo.</span><span class="sxs-lookup"><span data-stu-id="3c64b-197">This value is the same column family name as used in the SessionInfo project.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="3c64b-198">No cambie HBaseTableColumnNames, ya que los valores predeterminados son los nombres que utiliza **SessionInfo** para recuperar los datos.</span><span class="sxs-lookup"><span data-stu-id="3c64b-198">Do not change the HBaseTableColumnNames, as the defaults are the names used by **SessionInfo** to retrieve data.</span></span>

4. <span data-ttu-id="3c64b-199">Guarde las propiedades y, a continuación, compile el proyecto.</span><span class="sxs-lookup"><span data-stu-id="3c64b-199">Save the properties, then build the project.</span></span>

5. <span data-ttu-id="3c64b-200">En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto y seleccione **Submit to Storm on HDInsight** (Enviar a Storm en HDInsight).</span><span class="sxs-lookup"><span data-stu-id="3c64b-200">In **Solution Explorer**, right-click the project and select **Submit to Storm on HDInsight**.</span></span> <span data-ttu-id="3c64b-201">Si se le solicita, introduzca las credenciales de su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c64b-201">If prompted, enter the credentials for your Azure subscription.</span></span>

   ![Imagen del envío al elemento de menú de Storm](./media/hdinsight-storm-correlation-topology/submittostorm.png)

6. <span data-ttu-id="3c64b-203">En el cuadro de diálogo **Enviar topología** , seleccione el clúster de Storm en el que quiere implementar esta topología.</span><span class="sxs-lookup"><span data-stu-id="3c64b-203">In the **Submit Topology** dialog, select the Storm cluster you want to deploy this topology to.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3c64b-204">La primera vez que envíe una topología, es posible que se tarde unos segundos en recuperar el nombre de los clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3c64b-204">The first time you submit a topology, it may take a few seconds to retrieve the name of your HDInsight clusters.</span></span>

7. <span data-ttu-id="3c64b-205">Una vez que se haya cargado y enviado la topología al clúster, se abrirá **Vista de topología de Storm** y se mostrará la topología en ejecución.</span><span class="sxs-lookup"><span data-stu-id="3c64b-205">Once the topology has been uploaded and submitted to the cluster, the **Storm Topology View** opens and displays the running topology.</span></span> <span data-ttu-id="3c64b-206">Para actualizar los datos, seleccione **CorrelationTopology** y pulse el botón de actualización de la parte superior derecha de la página.</span><span class="sxs-lookup"><span data-stu-id="3c64b-206">To refresh the data, select the **CorrelationTopology** and use the refresh button at the top right of the page.</span></span>

   ![Imagen de la vista de topología](./media/hdinsight-storm-correlation-topology/topologyview.png)

   <span data-ttu-id="3c64b-208">Cuando la topología comience a generar datos, el valor de la columna **Emitida** se incrementará.</span><span class="sxs-lookup"><span data-stu-id="3c64b-208">When the topology begins generating data, the value in the **Emitted** column increments.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3c64b-209">Si la **Vista de topología de Storm** no se abre automáticamente, siga estos pasos para abrirla:</span><span class="sxs-lookup"><span data-stu-id="3c64b-209">If the **Storm Topology View** does not open automatically, use the following steps to open it:</span></span>
   >
   > 1. <span data-ttu-id="3c64b-210">Desde el **Explorador de soluciones**, expanda **Azure** y **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="3c64b-210">In **Solution Explorer**, expand **Azure**, and then expand **HDInsight**.</span></span>
   > 2. <span data-ttu-id="3c64b-211">Haga clic con el botón derecho en el clúster de Storm que está ejecutando la topología y, después, seleccione **Ver topologías de Storm**</span><span class="sxs-lookup"><span data-stu-id="3c64b-211">Right-click the Storm cluster that the topology is running on, and then select **View Storm Topologies**</span></span>

## <a name="query-the-data"></a><span data-ttu-id="3c64b-212">Consultar los datos</span><span class="sxs-lookup"><span data-stu-id="3c64b-212">Query the data</span></span>

<span data-ttu-id="3c64b-213">Una vez que se han emitido los datos, siga los pasos siguientes para consultar los datos.</span><span class="sxs-lookup"><span data-stu-id="3c64b-213">Once data has been emitted, use the following steps to query the data.</span></span>

1. <span data-ttu-id="3c64b-214">Vuelva al proyecto **SessionInfo** .</span><span class="sxs-lookup"><span data-stu-id="3c64b-214">Return to the **SessionInfo** project.</span></span> <span data-ttu-id="3c64b-215">Si no está ejecutando, inicie una nueva instancia de este.</span><span class="sxs-lookup"><span data-stu-id="3c64b-215">If not running, start a new instance of it.</span></span>

2. <span data-ttu-id="3c64b-216">Cuando se le pida, seleccione **s** para buscar el evento de INICIO.</span><span class="sxs-lookup"><span data-stu-id="3c64b-216">When prompted, select **s** to search for START event.</span></span> <span data-ttu-id="3c64b-217">Se le pedirá que escriba una hora de inicio y finalización para definir un intervalo de tiempo. Solo se devolverán los eventos que se encuentren entre estas dos horas.</span><span class="sxs-lookup"><span data-stu-id="3c64b-217">You are prompted to enter a start and end time to define a time range - only events between these two times are returned.</span></span>

    <span data-ttu-id="3c64b-218">Utilice el siguiente formato al introducir las horas de inicio y finalización: HH: MM y 'am' o 'pm'.</span><span class="sxs-lookup"><span data-stu-id="3c64b-218">Use the following format when entering the start and end times: HH:MM and 'am' or 'pm'.</span></span> <span data-ttu-id="3c64b-219">Por ejemplo, 11:20 pm.</span><span class="sxs-lookup"><span data-stu-id="3c64b-219">For example, 11:20pm.</span></span>

    <span data-ttu-id="3c64b-220">Para devolver los eventos registrados, use una hora de inicio anterior a la implementación de la topología de Storm y una hora de finalización actual.</span><span class="sxs-lookup"><span data-stu-id="3c64b-220">To return logged events, use a start time from before the Storm topology was deployed, and an end time of now.</span></span> <span data-ttu-id="3c64b-221">Los datos devueltos contienen entradas similares al siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="3c64b-221">The return data contains entries similar to the following text:</span></span>

        Session e6992b3e-79be-4991-afcf-5cb47dd1c81c started at 6/5/2015 6:10:15 PM. Timestamp = 1433527820737

<span data-ttu-id="3c64b-222">La búsqueda de eventos de FINALIZACIÓN funciona igual que para los eventos de INICIO.</span><span class="sxs-lookup"><span data-stu-id="3c64b-222">Searching for END events works the same as START events.</span></span> <span data-ttu-id="3c64b-223">Sin embargo, los eventos de FINALIZACIÓN se generan aleatoriamente entre 1 y 5 minutos después del evento de INICIO.</span><span class="sxs-lookup"><span data-stu-id="3c64b-223">However, END events are generated randomly between 1 and 5 minutes after the START event.</span></span> <span data-ttu-id="3c64b-224">Es posible que tenga que probar algunos intervalos de tiempo para encontrar los eventos de FINALIZACIÓN.</span><span class="sxs-lookup"><span data-stu-id="3c64b-224">You may have to try a few time ranges to find the END events.</span></span> <span data-ttu-id="3c64b-225">Los eventos de FINALIZACIÓN también contendrán la duración de la sesión; la diferencia entre la hora de INICIO del evento y la hora de FINALIZACIÓN del evento.</span><span class="sxs-lookup"><span data-stu-id="3c64b-225">END events also contain the duration of the session - the difference between the START event time and END event time.</span></span> <span data-ttu-id="3c64b-226">Este es un ejemplo de datos de eventos de FINALIZACIÓN:</span><span class="sxs-lookup"><span data-stu-id="3c64b-226">Here is an example of data for END events:</span></span>

    Session fc9fa8e6-6892-4073-93b3-a587040d892e lasted 2 minutes, and ended at 6/5/2015 6:12:15 PM

> [!NOTE]
> <span data-ttu-id="3c64b-227">Aunque especifique los valores de tiempo en la hora local, la consulta devolverá las horas en UTC.</span><span class="sxs-lookup"><span data-stu-id="3c64b-227">While the time values you enter are in local time, the time returned from the query is in UTC.</span></span>

## <a name="stop-the-topology"></a><span data-ttu-id="3c64b-228">Detención de la topología</span><span class="sxs-lookup"><span data-stu-id="3c64b-228">Stop the topology</span></span>

<span data-ttu-id="3c64b-229">Cuando esté listo para detener la topología, vuelva al proyecto **CorrelationTopology** proyecto en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3c64b-229">When you are ready to stop the topology, return to the **CorrelationTopology** project in Visual Studio.</span></span> <span data-ttu-id="3c64b-230">En la **Storm Topology View** (Vista de topologías de Storm), seleccione la topología y, a continuación, utilice el botón **Kill** (Terminar) situado en la parte superior de la vista de topología.</span><span class="sxs-lookup"><span data-stu-id="3c64b-230">In the **Storm Topology View**, select the topology and then use the **Kill** button at the top of the topology view.</span></span>

## <a name="delete-your-cluster"></a><span data-ttu-id="3c64b-231">Eliminación del clúster</span><span class="sxs-lookup"><span data-stu-id="3c64b-231">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="3c64b-232">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3c64b-232">Next steps</span></span>

<span data-ttu-id="3c64b-233">Para obtener más ejemplos de Storm, vea [Topologías de ejemplo para Storm en HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="3c64b-233">For more Storm examples, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
