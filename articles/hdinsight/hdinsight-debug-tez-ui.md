---
title: 'aaaUse Tez UI con HDInsight basados en Windows: Azure | Documentos de Microsoft'
description: "Obtenga información acerca de cómo trabajos toouse hello Tez UI toodebug Tez en HDInsight HDInsight basados en Windows."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a55bccb9-7c32-4ff2-b654-213a2354bd5c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 7ae21242ee1f8dc34a8501bed1ca995480885540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-tez-ui-toodebug-tez-jobs-on-windows-based-hdinsight"></a><span data-ttu-id="413cc-103">Usar hello Tez UI toodebug Tez trabajos de HDInsight basados en Windows</span><span class="sxs-lookup"><span data-stu-id="413cc-103">Use hello Tez UI toodebug Tez Jobs on Windows-based HDInsight</span></span>
<span data-ttu-id="413cc-104">Hola Tez UI es una página web que pueden ser utilizados trabajos toounderstand y depuración que utilizan Tez como motor de ejecución de hello en clústeres de HDInsight basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="413cc-104">hello Tez UI is a web page that can be used toounderstand and debug jobs that use Tez as hello execution engine on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="413cc-105">Hola Tez UI permite trabajo de hello toovisualize como un gráfico de elementos conectados, profundizar en cada elemento y recuperar las estadísticas y la información de registro.</span><span class="sxs-lookup"><span data-stu-id="413cc-105">hello Tez UI allows you toovisualize hello job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="413cc-106">pasos de Hello en este documento requieren un clúster de HDInsight que usa Windows.</span><span class="sxs-lookup"><span data-stu-id="413cc-106">hello steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="413cc-107">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="413cc-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="413cc-108">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="413cc-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="413cc-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="413cc-109">Prerequisites</span></span>
* <span data-ttu-id="413cc-110">Un clúster de HDInsight basado en Windows</span><span class="sxs-lookup"><span data-stu-id="413cc-110">A Windows-based HDInsight cluster.</span></span> <span data-ttu-id="413cc-111">Para obtener información sobre cómo crear un clúster, consulte [Introducción al uso de HDInsight basado en Windows](hdinsight-hadoop-tutorial-get-started-windows.md).</span><span class="sxs-lookup"><span data-stu-id="413cc-111">For steps on creating a new cluster, see [Get started using Windows-based HDInsight](hdinsight-hadoop-tutorial-get-started-windows.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="413cc-112">Hola Tez UI solo está disponible en los clústeres de HDInsight basados en Windows creados después del 8 de febrero de 2016.</span><span class="sxs-lookup"><span data-stu-id="413cc-112">hello Tez UI is only available on Windows-based HDInsight clusters created after February 8th, 2016.</span></span>
  >
  >
* <span data-ttu-id="413cc-113">Un cliente de escritorio remoto basado en Windows.</span><span class="sxs-lookup"><span data-stu-id="413cc-113">A Windows-based Remote Desktop client.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="413cc-114">Descripción de Tez</span><span class="sxs-lookup"><span data-stu-id="413cc-114">Understanding Tez</span></span>
<span data-ttu-id="413cc-115">Tez es un marco de trabajo extensible para el procesamiento de datos en Hadoop que proporciona una mayor velocidad que el procesamiento tradicional de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="413cc-115">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="413cc-116">Para los clústeres de HDInsight basados en Windows, es un motor opcional que puede habilitar para Hive mediante Hola siguiente comando como parte de la consulta de Hive:</span><span class="sxs-lookup"><span data-stu-id="413cc-116">For Windows-based HDInsight clusters, it is an optional engine that you can enable for Hive by using hello following command as part of your Hive query:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="413cc-117">Una vez trabajo tooTez enviado, crea un dirigen acíclico gráfico (DAG) que describe el orden de Hola de ejecución de acciones de hello requerido trabajo Hola.</span><span class="sxs-lookup"><span data-stu-id="413cc-117">When work is submitted tooTez, it creates a Directed Acyclic Graph (DAG) that describes hello order of execution of hello actions required by hello job.</span></span> <span data-ttu-id="413cc-118">Acciones individuales se denominan vértices y ejecutar una parte del programa Hola trabajo completo.</span><span class="sxs-lookup"><span data-stu-id="413cc-118">Individual actions are called vertices, and execute a piece of hello overall job.</span></span> <span data-ttu-id="413cc-119">ejecución real de Hola de trabajo de hello descrita por un vértice se denomina una tarea y se puede distribuir en varios nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="413cc-119">hello actual execution of hello work described by a vertex is called a task, and may be distributed across multiple nodes in hello cluster.</span></span>

### <a name="understanding-hello-tez-ui"></a><span data-ttu-id="413cc-120">Hola descripción Tez UI</span><span class="sxs-lookup"><span data-stu-id="413cc-120">Understanding hello Tez UI</span></span>
<span data-ttu-id="413cc-121">Hola Tez UI es que una página web proporciona información sobre los procesos que se ejecutan o tienen previamente se ejecutó con una Tez.</span><span class="sxs-lookup"><span data-stu-id="413cc-121">hello Tez UI is a web page provides information on processes that are running, or have previously ran using Tez.</span></span> <span data-ttu-id="413cc-122">Le permite tooview Hola DAG generado por Tez, cómo se distribuyen a través de clústeres, los contadores, como la memoria utilizada por la información de error, las tareas y vértices.</span><span class="sxs-lookup"><span data-stu-id="413cc-122">It allows you tooview hello DAG generated by Tez, how it is distributed across clusters, counters such as memory used by tasks and vertices, and error information.</span></span> <span data-ttu-id="413cc-123">Puede ofrecer información útil en hello los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="413cc-123">It may offer useful information in hello following scenarios:</span></span>

* <span data-ttu-id="413cc-124">Supervisión de los procesos de larga ejecución, ver progreso de asignación de Hola y reduzcan las tareas.</span><span class="sxs-lookup"><span data-stu-id="413cc-124">Monitoring long-running processes, viewing hello progress of map and reduce tasks.</span></span>
* <span data-ttu-id="413cc-125">Analizar datos históricos para procesos correctos o con error toolearn cómo se puede mejorar el procesamiento o por qué se produjo un error.</span><span class="sxs-lookup"><span data-stu-id="413cc-125">Analyzing historical data for successful or failed processes toolearn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="413cc-126">Generar un DAG</span><span class="sxs-lookup"><span data-stu-id="413cc-126">Generate a DAG</span></span>
<span data-ttu-id="413cc-127">Hola Tez UI solo contendrá datos si un trabajo que utiliza Hola Tez motor se está ejecutando actualmente o se ha quedado en hello anterior.</span><span class="sxs-lookup"><span data-stu-id="413cc-127">hello Tez UI will only contain data if a job that uses hello Tez engine is currently running, or has been ran in hello past.</span></span> <span data-ttu-id="413cc-128">Las consultas de Hive sencillas normalmente se pueden resolver sin usar Tez, pero las consultas más complejas con filtrado, agrupación, ordenación, uniones, etc. suelen requerir Tez.</span><span class="sxs-lookup"><span data-stu-id="413cc-128">Simple Hive queries can usually be resolved without using Tez, however more complex queries that do filtering, grouping, ordering, joins, etc. will usually require Tez.</span></span>

<span data-ttu-id="413cc-129">Usar hello siguiendo los pasos toorun una consulta de Hive que va a ejecutar mediante Tez.</span><span class="sxs-lookup"><span data-stu-id="413cc-129">Use hello following steps toorun a Hive query that will execute using Tez.</span></span>

1. <span data-ttu-id="413cc-130">En un explorador web, vaya toohttps://CLUSTERNAME.azurehdinsight.net, donde **CLUSTERNAME** es Hola nombre de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="413cc-130">In a web browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span>
2. <span data-ttu-id="413cc-131">En menú de hello al principio de Hola de página de hello, seleccione hello **Editor de Hive**.</span><span class="sxs-lookup"><span data-stu-id="413cc-131">From hello menu at hello top of hello page, select hello **Hive Editor**.</span></span> <span data-ttu-id="413cc-132">Se mostrará una página con la siguiente consulta de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="413cc-132">This will display a page with hello following example query.</span></span>

        Select * from hivesampletable

    <span data-ttu-id="413cc-133">Borrar la consulta de ejemplo de Hola y reemplazarlo por siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="413cc-133">Erase hello example query and replace it with hello following.</span></span>

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. <span data-ttu-id="413cc-134">Seleccione hello **enviar** botón.</span><span class="sxs-lookup"><span data-stu-id="413cc-134">Select hello **Submit** button.</span></span> <span data-ttu-id="413cc-135">Hola **sesión de trabajo** sección final Hola de página Hola mostrará el estado de Hola de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="413cc-135">hello **Job Session** section at hello bottom of hello page will display hello status of hello query.</span></span> <span data-ttu-id="413cc-136">Una vez Hola cambios de estado demasiado**completado**, seleccione hello **ver detalles** vincular tooview Hola resultados.</span><span class="sxs-lookup"><span data-stu-id="413cc-136">Once hello status changes too**Completed**, select hello **View Details** link tooview hello results.</span></span> <span data-ttu-id="413cc-137">Hola **salida del trabajo** debe ser similar siguiente toohello:</span><span class="sxs-lookup"><span data-stu-id="413cc-137">hello **Job Output** should be similar toohello following:</span></span>

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-hello-tez-ui"></a><span data-ttu-id="413cc-138">Usar hello Tez UI</span><span class="sxs-lookup"><span data-stu-id="413cc-138">Use hello Tez UI</span></span>
> [!NOTE]
> <span data-ttu-id="413cc-139">Hola Tez UI solo está disponible en el escritorio de Hola Hola principal de nodos de clúster, por lo que debe usar nodos principales del escritorio remoto tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="413cc-139">hello Tez UI is only available from hello desktop of hello cluster head nodes, so you must use Remote Desktop tooconnect toohello head nodes.</span></span>
>
>

1. <span data-ttu-id="413cc-140">De hello [portal de Azure](https://portal.azure.com), seleccione el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="413cc-140">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span> <span data-ttu-id="413cc-141">Desde la parte superior de la hoja de HDInsight de Hola Hola seleccione hello **escritorio remoto** icono.</span><span class="sxs-lookup"><span data-stu-id="413cc-141">From hello top of hello HDInsight blade, select hello **Remote Desktop** icon.</span></span> <span data-ttu-id="413cc-142">Esto mostrará la hoja de escritorio remoto de Hola</span><span class="sxs-lookup"><span data-stu-id="413cc-142">This will display hello remote desktop blade</span></span>

    ![Icono de Escritorio remoto](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. <span data-ttu-id="413cc-144">En la hoja de escritorio remoto de hello, seleccione **conectar** nodo principal del clúster de toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="413cc-144">From hello Remote Desktop blade, select **Connect** tooconnect toohello cluster head node.</span></span> <span data-ttu-id="413cc-145">Cuando se le pida, use Hola clúster usuario nombre y la contraseña tooauthenticate Hola conexión a Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="413cc-145">When prompted, use hello cluster Remote Desktop user name and password tooauthenticate hello connection.</span></span>

    ![Icono de conexión a Escritorio remoto](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > <span data-ttu-id="413cc-147">Si no ha habilitado la conectividad de escritorio remoto, proporcione un nombre de usuario, una contraseña y una fecha de expiración, seleccione **habilitar** tooenable escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="413cc-147">If you have not enabled Remote Desktop connectivity, provide a user name, password, and expiration date, then select **Enable** tooenable Remote Desktop.</span></span> <span data-ttu-id="413cc-148">Una vez que se ha habilitado, utilice hello tooconnect de pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="413cc-148">Once it has been enabled, use hello previous steps tooconnect.</span></span>
   >
   >
3. <span data-ttu-id="413cc-149">Una vez conectado, abra Internet Explorer en el escritorio remoto hello, icono de engranaje seleccione hello en superior Hola derecha del explorador de hello y, a continuación, seleccione **ver la configuración de compatibilidad**.</span><span class="sxs-lookup"><span data-stu-id="413cc-149">Once connected, open Internet Explorer on hello remote desktop, select hello gear icon in hello upper right of hello browser, and then select **Compatibility View Settings**.</span></span>
4. <span data-ttu-id="413cc-150">Desde la parte inferior de Hola de **ver la configuración de compatibilidad**, desactive casilla de verificación de Hola para **mostrar sitios de intranet en la vista de compatibilidad** y **listas de compatibilidad de usar Microsoft**, y, a continuación, seleccione **cerrar**.</span><span class="sxs-lookup"><span data-stu-id="413cc-150">From hello bottom of **Compatibility View Settings**, clear hello check box for **Display intranet sites in Compatibility View** and **Use Microsoft compatibility lists**, and then select **Close**.</span></span>
5. <span data-ttu-id="413cc-151">En Internet Explorer, vaya toohttp://headnodehost:8188/tezui / #/.</span><span class="sxs-lookup"><span data-stu-id="413cc-151">In Internet Explorer, browse toohttp://headnodehost:8188/tezui/#/.</span></span> <span data-ttu-id="413cc-152">Esto mostrará hello Tez UI</span><span class="sxs-lookup"><span data-stu-id="413cc-152">This will display hello Tez UI</span></span>

    ![Interfaz de usuario de Tez](./media/hdinsight-debug-tez-ui/tezui.png)

    <span data-ttu-id="413cc-154">Cuando se cargue hello Tez UI, verá una lista de grupos dag que se están ejecutando actualmente, o bien haber ejecutado en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="413cc-154">When hello Tez UI loads, you will see a list of DAGs that are currently running, or have been ran on hello cluster.</span></span> <span data-ttu-id="413cc-155">vista predeterminada de Hello incluye Hola Dag Name, Id., remitente, estado, hora de inicio, hora de finalización, duración, Id. de aplicación y cola.</span><span class="sxs-lookup"><span data-stu-id="413cc-155">hello default view includes hello Dag Name, Id, Submitter, Status, Start Time, End Time, Duration, Application ID, and Queue.</span></span> <span data-ttu-id="413cc-156">Mediante el icono de engranaje de hello en hello derecha de la página de hello, se pueden agregar más columnas.</span><span class="sxs-lookup"><span data-stu-id="413cc-156">More columns can be added using hello gear icon at hello right of hello page.</span></span>

    <span data-ttu-id="413cc-157">Si tiene sólo una entrada, será para consulta de Hola que se ejecutó en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="413cc-157">If you have only one entry, it will be for hello query that you ran in hello previous section.</span></span> <span data-ttu-id="413cc-158">Si tiene varias entradas, puede buscar mediante la especificación de criterios de búsqueda en los campos de hello anteriormente Hola dag y luego aciertos **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="413cc-158">If you have multiple entries, you can search by entering search criteria in hello fields above hello DAGs, then hit **Enter**.</span></span>
6. <span data-ttu-id="413cc-159">Seleccione hello **Dag Name** para entrada de DAG de hello más reciente.</span><span class="sxs-lookup"><span data-stu-id="413cc-159">Select hello **Dag Name** for hello most recent DAG entry.</span></span> <span data-ttu-id="413cc-160">Se mostrará información acerca de hello DAG, así como toodownload de opción de hello un archivo zip de archivos JSON que contienen información sobre Hola DAG.</span><span class="sxs-lookup"><span data-stu-id="413cc-160">This will display information about hello DAG, as well as hello option toodownload a zip of JSON files that contain information about hello DAG.</span></span>

    ![Detalles del DAG](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. <span data-ttu-id="413cc-162">Por encima de hello **DAG detalles** son varios vínculos que pueden ser utilizados toodisplay saber Hola DAG.</span><span class="sxs-lookup"><span data-stu-id="413cc-162">Above hello **DAG Details** are several links that can be used toodisplay information about hello DAG.</span></span>

   * <span data-ttu-id="413cc-163">**Contadores del DAG** muestra información de los contadores de este DAG.</span><span class="sxs-lookup"><span data-stu-id="413cc-163">**DAG Counters** displays counters information for this DAG.</span></span>
   * <span data-ttu-id="413cc-164">**Vista gráfica** muestra una representación gráfica de este DAG.</span><span class="sxs-lookup"><span data-stu-id="413cc-164">**Graphical View** displays a graphical representation of this DAG.</span></span>
   * <span data-ttu-id="413cc-165">**Todos los vértices** muestra una lista de vértices de hello en este DAG.</span><span class="sxs-lookup"><span data-stu-id="413cc-165">**All Vertices** displays a list of hello vertices in this DAG.</span></span>
   * <span data-ttu-id="413cc-166">**Todas las tareas** muestra una lista de tareas de Hola para todos los vértices en este DAG.</span><span class="sxs-lookup"><span data-stu-id="413cc-166">**All Tasks** displays a list of hello tasks for all vertices in this DAG.</span></span>
   * <span data-ttu-id="413cc-167">**Todos los TaskAttempts** muestra información acerca de hello intenta toorun tareas para este DAG.</span><span class="sxs-lookup"><span data-stu-id="413cc-167">**All TaskAttempts** displays information about hello attempts toorun tasks for this DAG.</span></span>

     > [!NOTE]
     > <span data-ttu-id="413cc-168">Si se desplaza la presentación de la columna de Hola de vértices, tareas y TaskAttempts, tenga en cuenta que hay vínculos tooview **contadores** y **ver o descargar los registros de** para cada fila.</span><span class="sxs-lookup"><span data-stu-id="413cc-168">If you scroll hello column display for Vertices, Tasks and TaskAttempts, notice that there are links tooview **counters** and **view or download logs** for each row.</span></span>
     >
     >

     <span data-ttu-id="413cc-169">Si se produjo un error en el trabajo de hello, Hola DAG detalles mostrará un estado de error, junto con vínculos tooinformation acerca de la tarea que tuvo el saludo.</span><span class="sxs-lookup"><span data-stu-id="413cc-169">If there was a failure with hello job, hello DAG Details will display a status of FAILED, along with links tooinformation about hello failed task.</span></span> <span data-ttu-id="413cc-170">Información de diagnóstico se mostrará debajo de los detalles de hello DAG.</span><span class="sxs-lookup"><span data-stu-id="413cc-170">Diagnostics information will be displayed beneath hello DAG details.</span></span>
8. <span data-ttu-id="413cc-171">Seleccione **Vista gráfica**.</span><span class="sxs-lookup"><span data-stu-id="413cc-171">Select **Graphical View**.</span></span> <span data-ttu-id="413cc-172">Esto muestra una representación gráfica de hello DAG.</span><span class="sxs-lookup"><span data-stu-id="413cc-172">This displays a graphical representation of hello DAG.</span></span> <span data-ttu-id="413cc-173">Puede colocar mouse Hola sobre cada vértice en hello ver toodisplay información acerca de él.</span><span class="sxs-lookup"><span data-stu-id="413cc-173">You can place hello mouse over each vertex in hello view toodisplay information about it.</span></span>

    ![Vista gráfica](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. <span data-ttu-id="413cc-175">Al hacer clic en un vértice cargará hello **detalles de vértices** para ese elemento.</span><span class="sxs-lookup"><span data-stu-id="413cc-175">Clicking on a vertex will load hello **Vertex Details** for that item.</span></span> <span data-ttu-id="413cc-176">Haga clic en hello **mapa 1** detalles de toodisplay de vértices para este elemento.</span><span class="sxs-lookup"><span data-stu-id="413cc-176">Click on hello **Map 1** vertex toodisplay details for this item.</span></span> <span data-ttu-id="413cc-177">Seleccione **confirmar** navegación de hello tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="413cc-177">Select **Confirm** tooconfirm hello navigation.</span></span>

    ![Detalles del vértice](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. <span data-ttu-id="413cc-179">Tenga en cuenta que ahora tiene vínculos al principio de Hola de página de Hola que son las tareas y toovertices relacionados.</span><span class="sxs-lookup"><span data-stu-id="413cc-179">Note that you now have links at hello top of hello page that are related toovertices and tasks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="413cc-180">También puede llegar a esta página volviendo demasiado**DAG detalles**, seleccione **detalles de vértices**y, a continuación, seleccionando hello **mapa 1** vértices.</span><span class="sxs-lookup"><span data-stu-id="413cc-180">You can also arrive at this page by going back too**DAG Details**, selecting **Vertex Details**, and then selecting hello **Map 1** vertex.</span></span>
    >
    >

    * <span data-ttu-id="413cc-181">**Contadores del vértice** muestra información de los contadores de este vértice.</span><span class="sxs-lookup"><span data-stu-id="413cc-181">**Vertex Counters** displays counter information for this vertex.</span></span>
    * <span data-ttu-id="413cc-182">**Tareas** muestra las tareas de este vértice.</span><span class="sxs-lookup"><span data-stu-id="413cc-182">**Tasks** displays tasks for this vertex.</span></span>
    * <span data-ttu-id="413cc-183">**Intentos de tareas** muestra información acerca de las tareas de toorun de intentos para este vértice.</span><span class="sxs-lookup"><span data-stu-id="413cc-183">**Task Attempts** displays information about attempts toorun tasks for this vertex.</span></span>
    * <span data-ttu-id="413cc-184">**Orígenes y receptores** muestra los orígenes de datos y los receptores de este vértice.</span><span class="sxs-lookup"><span data-stu-id="413cc-184">**Sources & Sinks** displays data sources and sinks for this vertex.</span></span>

      > [!NOTE]
      > <span data-ttu-id="413cc-185">Como con el menú anterior de hello, puede desplazarse a la visualización de columnas de Hola para tareas, los intentos de tarea y orígenes de & Sinks__ toodisplay vincula toomore información para cada elemento.</span><span class="sxs-lookup"><span data-stu-id="413cc-185">As with hello previous menu, you can scroll hello column display for Tasks, Task Attempts, and Sources & Sinks__ toodisplay links toomore information for each item.</span></span>
      >
      >
11. <span data-ttu-id="413cc-186">Seleccione **tareas**, y, a continuación, seleccione Hola denominado **00_000000**.</span><span class="sxs-lookup"><span data-stu-id="413cc-186">Select **Tasks**, and then select hello item named **00_000000**.</span></span> <span data-ttu-id="413cc-187">De este modo se mostrarán los **Detalles de la tarea** de esta tarea.</span><span class="sxs-lookup"><span data-stu-id="413cc-187">This will display **Task Details** for this task.</span></span> <span data-ttu-id="413cc-188">En esta pantalla, puede ver los **Contadores de tarea** y los **Intentos de tarea**.</span><span class="sxs-lookup"><span data-stu-id="413cc-188">From this screen, you can view **Task Counters** and **Task Attempts**.</span></span>

    ![Detalles de la tarea](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a><span data-ttu-id="413cc-190">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="413cc-190">Next Steps</span></span>
<span data-ttu-id="413cc-191">Ahora que ha aprendido cómo ver hello toouse Tez, obtenga más información sobre [utilizando Hive en HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="413cc-191">Now that you have learned how toouse hello Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="413cc-192">Para obtener más información técnica sobre Tez, consulte hello [Tez página en Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="413cc-192">For more detailed technical information on Tez, see hello [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>
