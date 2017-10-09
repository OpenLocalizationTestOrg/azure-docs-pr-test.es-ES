---
title: eventos de aaaCorrelate con el tiempo con Storm y HBase en HDInsight
description: "Obtenga información acerca de cómo toocorrelate eventos que llegan en distintos momentos mediante Storm y HBase en HDInsight."
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
ms.openlocfilehash: f915eef77bbda5b02bfd02ad0b5a4923ff2f4f26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="correlate-events-that-arrive-at-different-times-using-storm-and-hbase"></a><span data-ttu-id="ce8a5-103">Correlación de eventos que llegan a diferentes horas con Storm y HBase</span><span class="sxs-lookup"><span data-stu-id="ce8a5-103">Correlate events that arrive at different times using Storm and HBase</span></span>

<span data-ttu-id="ce8a5-104">Si utiliza un almacén de datos persistente con Apache Storm, puede poner en correlación entradas de datos que llegan en distintos momentos.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-104">By using a persistent data store with Apache Storm, you can correlate data entries that arrive at different times.</span></span> <span data-ttu-id="ce8a5-105">Por ejemplo, la vinculación de eventos de inicio de sesión y cierre de sesión de un toocalculate de sesión de usuario cómo sesión de hello tiempo duró.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-105">For example, linking login and logout events for a user session toocalculate how long hello session lasted.</span></span>

<span data-ttu-id="ce8a5-106">En este documento, aprenderá cómo toocreate una topología básica de C# Storm que realiza el seguimiento de eventos de inicio y cierre de sesión para sesiones de usuario y calcula la duración de Hola de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-106">In this document, you learn how toocreate a basic C# Storm topology that tracks login and logout events for user sessions, and calculates hello duration of hello session.</span></span> <span data-ttu-id="ce8a5-107">topología de Hello usa HBase como un almacén de datos persistente.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-107">hello topology uses HBase as a persistent data store.</span></span> <span data-ttu-id="ce8a5-108">HBase también le permite tooperform de consultas por lotes en la información adicional de hello datos históricos tooproduce.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-108">HBase also allows you tooperform batch queries on hello historical data tooproduce additional insights.</span></span> <span data-ttu-id="ce8a5-109">Por ejemplo, la cantidad de sesiones de usuario que se iniciaron o terminaron durante un período de tiempo específico.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-109">For example, how many user sessions were started or ended during a specific time period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce8a5-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ce8a5-110">Prerequisites</span></span>

* <span data-ttu-id="ce8a5-111">Visual Studio y hello HDInsight tools para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-111">Visual Studio and hello HDInsight tools for Visual Studio.</span></span> <span data-ttu-id="ce8a5-112">Para obtener más información, consulte [Introducción al uso de herramientas de HDInsight de Hola para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ce8a5-112">For more information, see [Get started using hello HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="ce8a5-113">Apache Storm en clústeres de HDInsight (Windows)</span><span class="sxs-lookup"><span data-stu-id="ce8a5-113">Apache Storm on HDInsight cluster (Windows-based).</span></span>

  > [!WARNING]
  > <span data-ttu-id="ce8a5-114">Aunque se admiten topologías SCP.NET en clústeres basados en Linux aluvión creados después de 10/28/2016, hello HBase SDK para el paquete de .NET disponible a partir del 28/10/2016 no funciona correctamente en HDInsight basados en Linux</span><span class="sxs-lookup"><span data-stu-id="ce8a5-114">While SCP.NET topologies are supported on Linux-based Storm clusters created after 10/28/2016, hello HBase SDK for .NET package available as of 10/28/2016 does not work correctly on Linux-based HDInsight</span></span>

* <span data-ttu-id="ce8a5-115">Apache HBase en un clúster de HDInsight (basado en Linux o Windows).</span><span class="sxs-lookup"><span data-stu-id="ce8a5-115">Apache HBase on HDInsight cluster (Linux or Windows-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="ce8a5-116">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-116">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ce8a5-117">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="ce8a5-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="ce8a5-118">[Java](https://java.com) 1.7 o superior en el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-118">[Java](https://java.com) 1.7 or greater on your development environment.</span></span> <span data-ttu-id="ce8a5-119">Java es toopackage usado Hola topología cuando llega el clúster de HDInsight de toohello enviado.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-119">Java is used toopackage hello topology when it is submitted toohello HDInsight cluster.</span></span>

  * <span data-ttu-id="ce8a5-120">Hola **JAVA_HOME** entorno debe variable punto toohello el directorio que contiene Java.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-120">hello **JAVA_HOME** environment variable must point toohello directory that contains Java.</span></span>
  * <span data-ttu-id="ce8a5-121">Hola **%JAVA_HOME%/bin** directorio debe estar en la ruta de acceso de Hola</span><span class="sxs-lookup"><span data-stu-id="ce8a5-121">hello **%JAVA_HOME%/bin** directory must be in hello path</span></span>

## <a name="architecture"></a><span data-ttu-id="ce8a5-122">Arquitectura</span><span class="sxs-lookup"><span data-stu-id="ce8a5-122">Architecture</span></span>

![Diagrama de flujo de datos de Hola a través de la topología de Hola](./media/hdinsight-storm-correlation-topology/correlationtopology.png)

<span data-ttu-id="ce8a5-124">Correlacionar eventos requiere un identificador común para el origen del evento de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-124">Correlating events requires a common identifier for hello event source.</span></span> <span data-ttu-id="ce8a5-125">Por ejemplo, un identificador de usuario, Id. de sesión u otro dispositivo de datos que sea un) único y b) incluidos en tooStorm de todos los datos enviados.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-125">For example, a user ID, session ID, or other piece of data that is a) unique and b) included in all data sent tooStorm.</span></span> <span data-ttu-id="ce8a5-126">Este ejemplo utiliza un toorepresent de valor GUID un identificador de sesión.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-126">This example uses a GUID value toorepresent a session ID.</span></span>

<span data-ttu-id="ce8a5-127">Este ejemplo consta de dos clústeres de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ce8a5-127">This example consists of two HDInsight clusters:</span></span>

* <span data-ttu-id="ce8a5-128">HBase: almacén de datos persistente para los datos históricos</span><span class="sxs-lookup"><span data-stu-id="ce8a5-128">HBase: persistent data store for historical data</span></span>
* <span data-ttu-id="ce8a5-129">Storm: utilizar los datos entrantes tooingest</span><span class="sxs-lookup"><span data-stu-id="ce8a5-129">Storm: used tooingest incoming data</span></span>

<span data-ttu-id="ce8a5-130">Hello datos generados aleatoriamente por topología aluvión de Hola y consta de hello siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="ce8a5-130">hello data is randomly generated by hello Storm topology, and consists of hello following items:</span></span>

* <span data-ttu-id="ce8a5-131">Id. de sesión: un GUID que identifica de forma única cada sesión</span><span class="sxs-lookup"><span data-stu-id="ce8a5-131">Session ID: a GUID that uniquely identifies each session</span></span>
* <span data-ttu-id="ce8a5-132">Evento: evento de INICIO o FINALIZACIÓN.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-132">Event: a START or END event.</span></span> <span data-ttu-id="ce8a5-133">En este ejemplo, INICIO siempre tiene lugar antes de la FINALIZACIÓN</span><span class="sxs-lookup"><span data-stu-id="ce8a5-133">For this example, START always occurs before END</span></span>
* <span data-ttu-id="ce8a5-134">: Hola: hora del evento Hola.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-134">Time: hello time of hello event.</span></span>

<span data-ttu-id="ce8a5-135">Estos datos se procesan y almacenan en HBase.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-135">This data is processed and stored in HBase.</span></span>

### <a name="storm-topology"></a><span data-ttu-id="ce8a5-136">Topología de Storm</span><span class="sxs-lookup"><span data-stu-id="ce8a5-136">Storm topology</span></span>

<span data-ttu-id="ce8a5-137">Cuando se inicia una sesión, un **iniciar** evento recibe topología hello y registra tooHBase.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-137">When a session starts, a **START** event is received by hello topology and logged tooHBase.</span></span> <span data-ttu-id="ce8a5-138">Cuando un **final** recibe el evento, la topología de hello recupera hello **iniciar** eventos y calcula el tiempo de hello entre eventos de hello dos.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-138">When an **END** event is received, hello topology retrieves hello **START** event and calculates hello time between hello two events.</span></span> <span data-ttu-id="ce8a5-139">Esto **duración** valor, a continuación, se almacena en HBase junto con hello **final** información del evento.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-139">This **Duration** value is then stored in HBase along with hello **END** event information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ce8a5-140">Mientras esta topología muestra el patrón básico de hello, una solución de producción necesitaría tootake diseño para hello los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="ce8a5-140">While this topology demonstrates hello basic pattern, a production solution would need tootake design for hello following scenarios:</span></span>
>
> * <span data-ttu-id="ce8a5-141">Eventos que llegan sin orden</span><span class="sxs-lookup"><span data-stu-id="ce8a5-141">Events arriving out of order</span></span>
> * <span data-ttu-id="ce8a5-142">Eventos duplicados</span><span class="sxs-lookup"><span data-stu-id="ce8a5-142">Duplicate events</span></span>
> * <span data-ttu-id="ce8a5-143">Eventos quitados</span><span class="sxs-lookup"><span data-stu-id="ce8a5-143">Dropped events</span></span>

<span data-ttu-id="ce8a5-144">topología de ejemplo de Hola se compone de Hola de los componentes siguientes:</span><span class="sxs-lookup"><span data-stu-id="ce8a5-144">hello sample topology is composed of hello following components:</span></span>

* <span data-ttu-id="ce8a5-145">Session.cs: simula una sesión de usuario mediante la creación de un identificador de sesión aleatorio, inicio Hola de tiempo y el tiempo de sesión dura.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-145">Session.cs: simulates a user session by creating a random session ID, start time, and how long hello session lasts.</span></span>

* <span data-ttu-id="ce8a5-146">Spout.cs: crea 100 sesiones, emite un evento de inicio, espera el tiempo de espera aleatorio de Hola para cada sesión y, a continuación, emite un evento de fin.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-146">Spout.cs: creates 100 sessions, emits a START event, waits hello random timeout for each session, and then emits an END event.</span></span> <span data-ttu-id="ce8a5-147">A continuación, recicla finalizó sesiones toogenerate nuevos.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-147">Then recycles ended sessions toogenerate new ones.</span></span>

* <span data-ttu-id="ce8a5-148">HBaseLookupBolt.cs: usa toolook de Id. de sesión de hello información de sesión de HBase.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-148">HBaseLookupBolt.cs: uses hello session ID toolook up session information from HBase.</span></span> <span data-ttu-id="ce8a5-149">Cuando se procesa un evento de fin, busca los eventos de inicio correspondiente de Hola y calcula la duración de Hola de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-149">When an END event is processed, it finds hello corresponding START event and calculates hello duration of hello session.</span></span>

* <span data-ttu-id="ce8a5-150">HBaseBolt.cs: almacena información en HBase.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-150">HBaseBolt.cs: Stores information into HBase.</span></span>

* <span data-ttu-id="ce8a5-151">TypeHelper.cs: Ayuda con la conversión de tipos al leer / escribir tooHBase.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-151">TypeHelper.cs: Helps with type conversion when reading from/writing tooHBase.</span></span>

### <a name="hbase-schema"></a><span data-ttu-id="ce8a5-152">Esquema de HBase</span><span class="sxs-lookup"><span data-stu-id="ce8a5-152">HBase schema</span></span>

<span data-ttu-id="ce8a5-153">En HBase, datos de Hola se almacenan en una tabla con hello después de esquema y configuración:</span><span class="sxs-lookup"><span data-stu-id="ce8a5-153">In HBase, hello data is stored in a table with hello following schema/settings:</span></span>

* <span data-ttu-id="ce8a5-154">Clave de fila: Hola identificador de sesión es utilizado como clave de Hola para las filas de esta tabla.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-154">Row key: hello session ID is used as hello key for rows in this table.</span></span>

* <span data-ttu-id="ce8a5-155">Familia de columna: nombre de familia de hello es 'cf'.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-155">Column family: hello family name is 'cf'.</span></span> <span data-ttu-id="ce8a5-156">Las columnas almacenadas en esta familia son:</span><span class="sxs-lookup"><span data-stu-id="ce8a5-156">Columns stored in this family are:</span></span>

  * <span data-ttu-id="ce8a5-157">evento: INICIO o FINALIZACIÓN.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-157">event: START or END.</span></span>

  * <span data-ttu-id="ce8a5-158">tiempo: tiempo de hello en milisegundos que Hola evento se ha producido.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-158">time: hello time in milliseconds that hello event occurred.</span></span>

  * <span data-ttu-id="ce8a5-159">duración: Hola longitud entre eventos de inicio y finalización.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-159">duration: hello length between START and END event.</span></span>

* <span data-ttu-id="ce8a5-160">Las versiones: familia de hello 'cf' se establece tooretain 5 versiones de cada fila.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-160">VERSIONS: hello 'cf' family is set tooretain 5 versions of each row.</span></span>

  > [!NOTE]
  > <span data-ttu-id="ce8a5-161">Las versiones son un registro de los valores anteriores almacenados para una clave de fila específica.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-161">Versions are a log of previous values stored for a specific row key.</span></span> <span data-ttu-id="ce8a5-162">De forma predeterminada, HBase sólo devuelve valor hello para la versión más reciente de Hola de una fila.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-162">By default, HBase only returns hello value for hello most recent version of a row.</span></span> <span data-ttu-id="ce8a5-163">En este caso, hello misma fila se utiliza para todos los eventos (inicio, fin.) de que cada versión de una fila se identifica mediante el valor de marca de tiempo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-163">In this case, hello same row is used for all events (START, END.) each version of a row is identified by hello timestamp value.</span></span> <span data-ttu-id="ce8a5-164">Las versiones proporcionan una vista histórica de los eventos registrados para un identificador concreto.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-164">Versions provide a historical view of events logged for a specific ID.</span></span>

## <a name="download-hello-project"></a><span data-ttu-id="ce8a5-165">Descargar proyecto Hola</span><span class="sxs-lookup"><span data-stu-id="ce8a5-165">Download hello project</span></span>

<span data-ttu-id="ce8a5-166">proyecto de ejemplo de Hola puede descargarse desde [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span><span class="sxs-lookup"><span data-stu-id="ce8a5-166">hello sample project can be downloaded from [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span></span>

<span data-ttu-id="ce8a5-167">Esta descarga contiene Hola después de proyectos de C#:</span><span class="sxs-lookup"><span data-stu-id="ce8a5-167">This download contains hello following C# projects:</span></span>

* <span data-ttu-id="ce8a5-168">CorrelationTopology: topología de Storm de C# que emite aleatoriamente eventos de inicio y finalización para las sesiones de usuario.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-168">CorrelationTopology: C# Storm topology that randomly emits start and end events for user sessions.</span></span> <span data-ttu-id="ce8a5-169">Cada sesión dura entre 1 y 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-169">Each session lasts between 1 and 5 minutes.</span></span>

* <span data-ttu-id="ce8a5-170">SessionInfo: C# aplicación de consola que crea la tabla HBase de Hola y proporciona consultas de ejemplo tooreturn información acerca de los datos de sesión almacenada.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-170">SessionInfo: C# console application that creates hello HBase table, and provides example queries tooreturn information about stored session data.</span></span>

## <a name="create-hello-table"></a><span data-ttu-id="ce8a5-171">Crear tabla de Hola</span><span class="sxs-lookup"><span data-stu-id="ce8a5-171">Create hello table</span></span>

1. <span data-ttu-id="ce8a5-172">Abra hello **SessionInfo** proyecto en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-172">Open hello **SessionInfo** project in Visual Studio.</span></span>

2. <span data-ttu-id="ce8a5-173">En **el Explorador de soluciones**, contextual hello **SessionInfo** de proyecto y seleccione **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-173">In **Solution Explorer**, right-click hello **SessionInfo** project and select **Properties**.</span></span>

    ![Captura de pantalla del menú con propiedades seleccionadas](./media/hdinsight-storm-correlation-topology/selectproperties.png)

3. <span data-ttu-id="ce8a5-175">Seleccione **configuración**, a continuación, después de hello de conjunto de valores:</span><span class="sxs-lookup"><span data-stu-id="ce8a5-175">Select **Settings**, then set hello following values:</span></span>

   * <span data-ttu-id="ce8a5-176">HBaseClusterURL: clúster de HBase de tooyour de dirección URL Hola.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-176">HBaseClusterURL: hello URL tooyour HBase cluster.</span></span> <span data-ttu-id="ce8a5-177">Por ejemplo, https://myhbasecluster.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-177">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="ce8a5-178">HBaseClusterUserName: cuenta de usuario de administrador/HTTP hello para el clúster</span><span class="sxs-lookup"><span data-stu-id="ce8a5-178">HBaseClusterUserName: hello admin/HTTP user account for your cluster</span></span>

   * <span data-ttu-id="ce8a5-179">HBaseClusterPassword: contraseña Hola de cuenta de usuario de administrador/HTTP Hola</span><span class="sxs-lookup"><span data-stu-id="ce8a5-179">HBaseClusterPassword: hello password for hello admin/HTTP user account</span></span>

   * <span data-ttu-id="ce8a5-180">HBaseTableName: nombre Hola de hello tabla toouse con este ejemplo</span><span class="sxs-lookup"><span data-stu-id="ce8a5-180">HBaseTableName: hello name of hello table toouse with this example</span></span>

   * <span data-ttu-id="ce8a5-181">HBaseTableColumnFamily: nombre de familia de columna hello</span><span class="sxs-lookup"><span data-stu-id="ce8a5-181">HBaseTableColumnFamily: hello column family name</span></span>

     ![Imagen del cuadro de diálogo de configuración](./media/hdinsight-storm-correlation-topology/settings.png)

4. <span data-ttu-id="ce8a5-183">Ejecutar soluciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-183">Run hello solution.</span></span> <span data-ttu-id="ce8a5-184">Cuando se le pida, seleccione tabla de hello 'c' toocreate clave hello en el clúster de HBase.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-184">When prompted, select hello 'c' key toocreate hello table on your HBase cluster.</span></span>

## <a name="build-and-deploy-hello-storm-topology"></a><span data-ttu-id="ce8a5-185">Compilar e implementar la topología de Storm Hola</span><span class="sxs-lookup"><span data-stu-id="ce8a5-185">Build and deploy hello Storm topology</span></span>

1. <span data-ttu-id="ce8a5-186">Abra hello **CorrelationTopology** solución en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-186">Open hello **CorrelationTopology** solution in Visual Studio.</span></span>

2. <span data-ttu-id="ce8a5-187">En **el Explorador de soluciones**, contextual hello **CorrelationTopology** del proyecto y seleccione Propiedades.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-187">In **Solution Explorer**, right-click hello **CorrelationTopology** project and select properties.</span></span>

3. <span data-ttu-id="ce8a5-188">En la ventana de propiedades de hello, seleccione **configuración** y escriba los valores de configuración de Hola para este proyecto.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-188">In hello properties window, select **Settings** and enter hello configuration values for this project.</span></span> <span data-ttu-id="ce8a5-189">Hello 5 primeros son Hola mismos valores usan por hello **SessionInfo** proyecto:</span><span class="sxs-lookup"><span data-stu-id="ce8a5-189">hello first 5 are hello same values used by hello **SessionInfo** project:</span></span>

   * <span data-ttu-id="ce8a5-190">HBaseClusterURL: clúster de HBase de tooyour de dirección URL Hola.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-190">HBaseClusterURL: hello URL tooyour HBase cluster.</span></span> <span data-ttu-id="ce8a5-191">Por ejemplo, https://myhbasecluster.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-191">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="ce8a5-192">HBaseClusterUserName: cuenta de usuario Hola admin/HTTP para el clúster.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-192">HBaseClusterUserName: hello admin/HTTP user account for your cluster.</span></span>

   * <span data-ttu-id="ce8a5-193">HBaseClusterPassword: la contraseña de Hola de cuenta de usuario de administrador/HTTP Hola.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-193">HBaseClusterPassword: hello password for hello admin/HTTP user account.</span></span>

   * <span data-ttu-id="ce8a5-194">HBaseTableName: nombre de Hola de hello tabla toouse con este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-194">HBaseTableName: hello name of hello table toouse with this example.</span></span> <span data-ttu-id="ce8a5-195">Este valor es Hola mismo nombre de la tabla como se utiliza en el proyecto de SessionInfo Hola.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-195">This value is hello same table name as used in hello SessionInfo project.</span></span>

   * <span data-ttu-id="ce8a5-196">HBaseTableColumnFamily: nombre de familia Hola columna.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-196">HBaseTableColumnFamily: hello column family name.</span></span> <span data-ttu-id="ce8a5-197">Este valor es Hola mismo nombre de familia de la columna tal y como se usan en hello SessionInfo proyecto.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-197">This value is hello same column family name as used in hello SessionInfo project.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="ce8a5-198">No cambie hello HBaseTableColumnNames, tal y como valores predeterminados de hello son nombres Hola utilizados por **SessionInfo** tooretrieve datos.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-198">Do not change hello HBaseTableColumnNames, as hello defaults are hello names used by **SessionInfo** tooretrieve data.</span></span>

4. <span data-ttu-id="ce8a5-199">Guardar las propiedades de hello, a continuación, compile el proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-199">Save hello properties, then build hello project.</span></span>

5. <span data-ttu-id="ce8a5-200">En **el Explorador de soluciones**, haga clic en proyecto de Hola y seleccione **enviar tooStorm en HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-200">In **Solution Explorer**, right-click hello project and select **Submit tooStorm on HDInsight**.</span></span> <span data-ttu-id="ce8a5-201">Si se le pide, escriba credenciales de hello para la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-201">If prompted, enter hello credentials for your Azure subscription.</span></span>

   ![Imagen del programa Hola a enviar el elemento de menú toostorm](./media/hdinsight-storm-correlation-topology/submittostorm.png)

6. <span data-ttu-id="ce8a5-203">Hola **topología enviar** cuadro de diálogo, clúster de Storm Hola seleccione desea toodeploy esta topología.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-203">In hello **Submit Topology** dialog, select hello Storm cluster you want toodeploy this topology to.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ce8a5-204">Hello primera vez que envíe una topología, puede tardar unos segundos nombre de hello tooretrieve los clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-204">hello first time you submit a topology, it may take a few seconds tooretrieve hello name of your HDInsight clusters.</span></span>

7. <span data-ttu-id="ce8a5-205">Una vez topología Hola clúster toohello cargados y enviados, Hola **aluvión de la vista de topología** se abre y muestra hello ejecutando topología.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-205">Once hello topology has been uploaded and submitted toohello cluster, hello **Storm Topology View** opens and displays hello running topology.</span></span> <span data-ttu-id="ce8a5-206">datos de hello toorefresh, seleccione hello **CorrelationTopology** y use el botón de actualización de hello en hello parte superior derecha de la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-206">toorefresh hello data, select hello **CorrelationTopology** and use hello refresh button at hello top right of hello page.</span></span>

   ![Imagen de la vista de topología de Hola](./media/hdinsight-storm-correlation-topology/topologyview.png)

   <span data-ttu-id="ce8a5-208">Cuando la topología de hello comienza generar datos, Hola valor Hola **emitida** incrementos de columna.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-208">When hello topology begins generating data, hello value in hello **Emitted** column increments.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ce8a5-209">Si hello **vista de topología de Storm** no se abre automáticamente, use Hola siguientes tooopen de pasos:</span><span class="sxs-lookup"><span data-stu-id="ce8a5-209">If hello **Storm Topology View** does not open automatically, use hello following steps tooopen it:</span></span>
   >
   > 1. <span data-ttu-id="ce8a5-210">Desde el **Explorador de soluciones**, expanda **Azure** y **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-210">In **Solution Explorer**, expand **Azure**, and then expand **HDInsight**.</span></span>
   > 2. <span data-ttu-id="ce8a5-211">Clúster de Storm Hola de menú contextual que Hola topología se ejecutan en y, a continuación, seleccione **vista aluvión de topologías**</span><span class="sxs-lookup"><span data-stu-id="ce8a5-211">Right-click hello Storm cluster that hello topology is running on, and then select **View Storm Topologies**</span></span>

## <a name="query-hello-data"></a><span data-ttu-id="ce8a5-212">Consultar datos de Hola</span><span class="sxs-lookup"><span data-stu-id="ce8a5-212">Query hello data</span></span>

<span data-ttu-id="ce8a5-213">Una vez que se ha emitido los datos, utilice Hola seguir los pasos tooquery Hola datos.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-213">Once data has been emitted, use hello following steps tooquery hello data.</span></span>

1. <span data-ttu-id="ce8a5-214">Devolver toohello **SessionInfo** proyecto.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-214">Return toohello **SessionInfo** project.</span></span> <span data-ttu-id="ce8a5-215">Si no está ejecutando, inicie una nueva instancia de este.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-215">If not running, start a new instance of it.</span></span>

2. <span data-ttu-id="ce8a5-216">Cuando se le pida, seleccione **s** toosearch para eventos de inicio.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-216">When prompted, select **s** toosearch for START event.</span></span> <span data-ttu-id="ce8a5-217">Está tooenter solicitada un inicio y finalización tiempo toodefine un intervalo de tiempo - se devuelven sólo los eventos entre estos dos veces.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-217">You are prompted tooenter a start and end time toodefine a time range - only events between these two times are returned.</span></span>

    <span data-ttu-id="ce8a5-218">Dar formato al escribir inicio Hola siguiente Hola de uso y de finalización: hh: mm y 'm' o 'CP'.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-218">Use hello following format when entering hello start and end times: HH:MM and 'am' or 'pm'.</span></span> <span data-ttu-id="ce8a5-219">Por ejemplo, 11:20 pm.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-219">For example, 11:20pm.</span></span>

    <span data-ttu-id="ce8a5-220">tooreturn registran eventos, use una hora de inicio de antes de hello aluvión de topología implementó y una hora de finalización de ahora.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-220">tooreturn logged events, use a start time from before hello Storm topology was deployed, and an end time of now.</span></span> <span data-ttu-id="ce8a5-221">datos de valor devuelto de Hello contienen entradas toohello similar siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="ce8a5-221">hello return data contains entries similar toohello following text:</span></span>

        Session e6992b3e-79be-4991-afcf-5cb47dd1c81c started at 6/5/2015 6:10:15 PM. Timestamp = 1433527820737

<span data-ttu-id="ce8a5-222">Buscando Hola de final eventos funciona igual como eventos de inicio.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-222">Searching for END events works hello same as START events.</span></span> <span data-ttu-id="ce8a5-223">Sin embargo, los eventos de fin se generan aleatoriamente entre 1 y 5 minutos después de evento de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-223">However, END events are generated randomly between 1 and 5 minutes after hello START event.</span></span> <span data-ttu-id="ce8a5-224">Puede que tenga tootry eventos de fin de hello toofind de intervalos de tiempo unos.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-224">You may have tootry a few time ranges toofind hello END events.</span></span> <span data-ttu-id="ce8a5-225">Eventos de fin también contienen durante Hola Hola sesión - diferencia Hola entre la hora del evento de inicio de Hola y hora de finalización del evento.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-225">END events also contain hello duration of hello session - hello difference between hello START event time and END event time.</span></span> <span data-ttu-id="ce8a5-226">Este es un ejemplo de datos de eventos de FINALIZACIÓN:</span><span class="sxs-lookup"><span data-stu-id="ce8a5-226">Here is an example of data for END events:</span></span>

    Session fc9fa8e6-6892-4073-93b3-a587040d892e lasted 2 minutes, and ended at 6/5/2015 6:12:15 PM

> [!NOTE]
> <span data-ttu-id="ce8a5-227">Aunque son valores de tiempo de Hola que especifica en hora local, hora de hello procedente de la consulta de hello está en UTC.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-227">While hello time values you enter are in local time, hello time returned from hello query is in UTC.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="ce8a5-228">Detener la topología de Hola</span><span class="sxs-lookup"><span data-stu-id="ce8a5-228">Stop hello topology</span></span>

<span data-ttu-id="ce8a5-229">Cuando esté listo toostop topología de hello, devolver toohello **CorrelationTopology** proyecto en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-229">When you are ready toostop hello topology, return toohello **CorrelationTopology** project in Visual Studio.</span></span> <span data-ttu-id="ce8a5-230">Hola **vista de topología de Storm**, seleccione la topología de hello y, a continuación, usar hello **Kill** situado en la parte superior de Hola de vista de topología de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce8a5-230">In hello **Storm Topology View**, select hello topology and then use hello **Kill** button at hello top of hello topology view.</span></span>

## <a name="delete-your-cluster"></a><span data-ttu-id="ce8a5-231">Eliminación del clúster</span><span class="sxs-lookup"><span data-stu-id="ce8a5-231">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="ce8a5-232">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ce8a5-232">Next steps</span></span>

<span data-ttu-id="ce8a5-233">Para obtener más ejemplos de Storm, vea [Topologías de ejemplo para Storm en HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="ce8a5-233">For more Storm examples, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
