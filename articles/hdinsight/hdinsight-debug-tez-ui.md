---
title: Uso de la interfaz de usuario de Tez con HDInsight basado en Windows - Azure | Microsoft Docs
description: "Obtener más información sobre cómo usar la interfaz de usuario de Tez para depurar trabajos de Tez en HDInsight basado en Windows"
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
ms.openlocfilehash: 3889fa1c3523eb0330cbe3b7640fd8590a5ceadf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-tez-ui-to-debug-tez-jobs-on-windows-based-hdinsight"></a><span data-ttu-id="0ed1f-103">Usar la interfaz de usuario de Tez para depurar trabajos de Tez en HDInsight basado en Windows</span><span class="sxs-lookup"><span data-stu-id="0ed1f-103">Use the Tez UI to debug Tez Jobs on Windows-based HDInsight</span></span>
<span data-ttu-id="0ed1f-104">La interfaz de usuario de Tez es una página web que se puede usar para comprender y depurar los trabajos que usan Tez como motor de ejecución en clústeres de HDInsight basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-104">The Tez UI is a web page that can be used to understand and debug jobs that use Tez as the execution engine on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="0ed1f-105">La interfaz de usuario de Tez permite visualizar el trabajo como un gráfico de elementos conectados, profundizar en cada elemento y recuperar las estadísticas y la información de registro.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-105">The Tez UI allows you to visualize the job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0ed1f-106">Los pasos de este documento requieren un clúster de HDInsight que use Windows.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-106">The steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="0ed1f-107">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0ed1f-108">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="0ed1f-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ed1f-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0ed1f-109">Prerequisites</span></span>
* <span data-ttu-id="0ed1f-110">Un clúster de HDInsight basado en Windows</span><span class="sxs-lookup"><span data-stu-id="0ed1f-110">A Windows-based HDInsight cluster.</span></span> <span data-ttu-id="0ed1f-111">Para obtener información sobre cómo crear un clúster, consulte [Introducción al uso de HDInsight basado en Windows](hdinsight-hadoop-tutorial-get-started-windows.md).</span><span class="sxs-lookup"><span data-stu-id="0ed1f-111">For steps on creating a new cluster, see [Get started using Windows-based HDInsight](hdinsight-hadoop-tutorial-get-started-windows.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="0ed1f-112">La interfaz de usuario de Tez solo está disponible en los clústeres de HDInsight basado en Windows creados después del 8 de febrero de 2016.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-112">The Tez UI is only available on Windows-based HDInsight clusters created after February 8th, 2016.</span></span>
  >
  >
* <span data-ttu-id="0ed1f-113">Un cliente de escritorio remoto basado en Windows.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-113">A Windows-based Remote Desktop client.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="0ed1f-114">Descripción de Tez</span><span class="sxs-lookup"><span data-stu-id="0ed1f-114">Understanding Tez</span></span>
<span data-ttu-id="0ed1f-115">Tez es un marco de trabajo extensible para el procesamiento de datos en Hadoop que proporciona una mayor velocidad que el procesamiento tradicional de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-115">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="0ed1f-116">Para los clústeres de HDInsight basado en Windows, es un motor opcional que se puede habilitar para Hive mediante el comando siguiente como parte de la consulta de Hive:</span><span class="sxs-lookup"><span data-stu-id="0ed1f-116">For Windows-based HDInsight clusters, it is an optional engine that you can enable for Hive by using the following command as part of your Hive query:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="0ed1f-117">Cuando se envía un trabajo a Tez, este crea un grafo acíclico dirigido (DAG) que describe el orden de ejecución de las acciones requeridas por el trabajo.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-117">When work is submitted to Tez, it creates a Directed Acyclic Graph (DAG) that describes the order of execution of the actions required by the job.</span></span> <span data-ttu-id="0ed1f-118">Las acciones individuales se denominan vértices y ejecutan una parte del trabajo total.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-118">Individual actions are called vertices, and execute a piece of the overall job.</span></span> <span data-ttu-id="0ed1f-119">La ejecución real del trabajo descrito por un vértice se denomina tarea, y puede distribuirse por varios nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-119">The actual execution of the work described by a vertex is called a task, and may be distributed across multiple nodes in the cluster.</span></span>

### <a name="understanding-the-tez-ui"></a><span data-ttu-id="0ed1f-120">Descripción de la interfaz de usuario de Tez</span><span class="sxs-lookup"><span data-stu-id="0ed1f-120">Understanding the Tez UI</span></span>
<span data-ttu-id="0ed1f-121">La interfaz de usuario de Tez es una página web que proporciona información sobre los procesos que se están ejecutando o que se ejecutaron previamente mediante Tez.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-121">The Tez UI is a web page provides information on processes that are running, or have previously ran using Tez.</span></span> <span data-ttu-id="0ed1f-122">Permite ver el DAG generado por Tez, la manera en que se distribuye por los clústeres, contadores como la memoria usada por tareas y vértices, e información de error.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-122">It allows you to view the DAG generated by Tez, how it is distributed across clusters, counters such as memory used by tasks and vertices, and error information.</span></span> <span data-ttu-id="0ed1f-123">Puede ofrecer información útil en los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="0ed1f-123">It may offer useful information in the following scenarios:</span></span>

* <span data-ttu-id="0ed1f-124">Supervisión de procesos de ejecución prolongada, visualización del progreso de asignación y reducción de las tareas.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-124">Monitoring long-running processes, viewing the progress of map and reduce tasks.</span></span>
* <span data-ttu-id="0ed1f-125">Análisis de datos históricos de procesos correctos o con errores para obtener información sobre cómo se puede mejorar el procesamiento o sobre la causa del error.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-125">Analyzing historical data for successful or failed processes to learn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="0ed1f-126">Generar un DAG</span><span class="sxs-lookup"><span data-stu-id="0ed1f-126">Generate a DAG</span></span>
<span data-ttu-id="0ed1f-127">La interfaz de usuario de Tez solo contendrá datos si se está ejecutando actualmente un trabajo que usa el motor de Tez, o bien si se ejecutó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-127">The Tez UI will only contain data if a job that uses the Tez engine is currently running, or has been ran in the past.</span></span> <span data-ttu-id="0ed1f-128">Las consultas de Hive sencillas normalmente se pueden resolver sin usar Tez, pero las consultas más complejas con filtrado, agrupación, ordenación, uniones, etc. suelen requerir Tez.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-128">Simple Hive queries can usually be resolved without using Tez, however more complex queries that do filtering, grouping, ordering, joins, etc. will usually require Tez.</span></span>

<span data-ttu-id="0ed1f-129">Siga los pasos que se indican a continuación para realizar una consulta de Hive que se ejecutará mediante Tez.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-129">Use the following steps to run a Hive query that will execute using Tez.</span></span>

1. <span data-ttu-id="0ed1f-130">En un explorador web, vaya a https://CLUSTERNAME.azurehdinsight.net, donde **CLUSTERNAME** es el nombre de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-130">In a web browser, navigate to https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span>
2. <span data-ttu-id="0ed1f-131">En el menú que aparece en la parte superior de la página, seleccione el **Editor de Hive**.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-131">From the menu at the top of the page, select the **Hive Editor**.</span></span> <span data-ttu-id="0ed1f-132">Se mostrará una página con la siguiente consulta de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-132">This will display a page with the following example query.</span></span>

        Select * from hivesampletable

    <span data-ttu-id="0ed1f-133">Borre la consulta de ejemplo y reemplácela por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-133">Erase the example query and replace it with the following.</span></span>

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. <span data-ttu-id="0ed1f-134">Seleccione el botón **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-134">Select the **Submit** button.</span></span> <span data-ttu-id="0ed1f-135">En la sección **Sesión de trabajo** que aparece en la parte inferior de la página se mostrará el estado de la consulta.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-135">The **Job Session** section at the bottom of the page will display the status of the query.</span></span> <span data-ttu-id="0ed1f-136">Cuando el estado cambie a **Completado**, seleccione el vínculo **Ver detalles** para ver los resultados.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-136">Once the status changes to **Completed**, select the **View Details** link to view the results.</span></span> <span data-ttu-id="0ed1f-137">La **Salida del trabajo** debe ser similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="0ed1f-137">The **Job Output** should be similar to the following:</span></span>

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-the-tez-ui"></a><span data-ttu-id="0ed1f-138">Usar la interfaz de usuario de Tez</span><span class="sxs-lookup"><span data-stu-id="0ed1f-138">Use the Tez UI</span></span>
> [!NOTE]
> <span data-ttu-id="0ed1f-139">La interfaz de usuario de Tez solo está disponible en el escritorio de los nodos principales del clúster, por lo que debe usar Escritorio remoto para conectarse a los nodos principales.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-139">The Tez UI is only available from the desktop of the cluster head nodes, so you must use Remote Desktop to connect to the head nodes.</span></span>
>
>

1. <span data-ttu-id="0ed1f-140">En el [Portal de Azure](https://portal.azure.com), seleccione el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-140">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span> <span data-ttu-id="0ed1f-141">En la parte superior de la hoja de HDInsight, seleccione el icono **Escritorio remoto**.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-141">From the top of the HDInsight blade, select the **Remote Desktop** icon.</span></span> <span data-ttu-id="0ed1f-142">Esto mostrará la hoja de Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-142">This will display the remote desktop blade</span></span>

    ![Icono de Escritorio remoto](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. <span data-ttu-id="0ed1f-144">En la hoja Escritorio remoto, seleccione **Conectar** para conectarse al nodo principal del clúster.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-144">From the Remote Desktop blade, select **Connect** to connect to the cluster head node.</span></span> <span data-ttu-id="0ed1f-145">Cuando se le solicite, use el nombre de usuario y la contraseña de Escritorio remoto del clúster para autenticar la conexión.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-145">When prompted, use the cluster Remote Desktop user name and password to authenticate the connection.</span></span>

    ![Icono de conexión a Escritorio remoto](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > <span data-ttu-id="0ed1f-147">Si no ha habilitado la conectividad de Escritorio remoto, proporcione un nombre de usuario, una contraseña y una fecha de expiración, y luego seleccione **Habilitar** para habilitar Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-147">If you have not enabled Remote Desktop connectivity, provide a user name, password, and expiration date, then select **Enable** to enable Remote Desktop.</span></span> <span data-ttu-id="0ed1f-148">Una vez habilitado, siga los pasos anteriores para conectarse.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-148">Once it has been enabled, use the previous steps to connect.</span></span>
   >
   >
3. <span data-ttu-id="0ed1f-149">Cuando se haya conectado, abra Internet Explorer en el escritorio remoto, seleccione el icono de engranaje en la esquina superior derecha del explorador y seleccione **Configuración de Vista de compatibilidad**.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-149">Once connected, open Internet Explorer on the remote desktop, select the gear icon in the upper right of the browser, and then select **Compatibility View Settings**.</span></span>
4. <span data-ttu-id="0ed1f-150">En la parte inferior de **Configuración de Vista de compatibilidad**, desactive la casilla **Mostrar sitios de la intranet en Vista de compatibilidad** y **Usar listas de compatibilidad de Microsoft** y, luego, seleccione **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-150">From the bottom of **Compatibility View Settings**, clear the check box for **Display intranet sites in Compatibility View** and **Use Microsoft compatibility lists**, and then select **Close**.</span></span>
5. <span data-ttu-id="0ed1f-151">En Internet Explorer, vaya a http://headnodehost:8188/tezui/#/.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-151">In Internet Explorer, browse to http://headnodehost:8188/tezui/#/.</span></span> <span data-ttu-id="0ed1f-152">Esta acción mostrará la interfaz de usuario de Tez.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-152">This will display the Tez UI</span></span>

    ![Interfaz de usuario de Tez](./media/hdinsight-debug-tez-ui/tezui.png)

    <span data-ttu-id="0ed1f-154">Cuando se cargue la interfaz de usuario de Tez, verá una lista de DAG que se están ejecutando actualmente o que se ejecutaron anteriormente en el clúster.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-154">When the Tez UI loads, you will see a list of DAGs that are currently running, or have been ran on the cluster.</span></span> <span data-ttu-id="0ed1f-155">La vista predeterminada incluye el nombre del DAG, el identificador, el remitente, el estado, la hora de inicio, la hora de finalización, la duración, el identificador de la aplicación y la cola.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-155">The default view includes the Dag Name, Id, Submitter, Status, Start Time, End Time, Duration, Application ID, and Queue.</span></span> <span data-ttu-id="0ed1f-156">Puede agregar más columnas mediante el icono de engranaje que se encuentra a la derecha de la página.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-156">More columns can be added using the gear icon at the right of the page.</span></span>

    <span data-ttu-id="0ed1f-157">Si solo tiene una entrada, será la de la consulta que ejecutó en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-157">If you have only one entry, it will be for the query that you ran in the previous section.</span></span> <span data-ttu-id="0ed1f-158">Si tiene varias entradas, puede realizar una búsqueda; para ello, especifique criterios de búsqueda en los campos situados encima de los DAG y presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-158">If you have multiple entries, you can search by entering search criteria in the fields above the DAGs, then hit **Enter**.</span></span>
6. <span data-ttu-id="0ed1f-159">Seleccione el **Nombre del DAG** de la entrada de DAG más reciente.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-159">Select the **Dag Name** for the most recent DAG entry.</span></span> <span data-ttu-id="0ed1f-160">Se mostrará información sobre el DAG, así como la opción de descargar un archivo ZIP con archivos JSON que contienen información sobre el DAG.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-160">This will display information about the DAG, as well as the option to download a zip of JSON files that contain information about the DAG.</span></span>

    ![Detalles del DAG](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. <span data-ttu-id="0ed1f-162">Encima de **Detalles del DAG** aparecen varios vínculos que pueden usarse para mostrar información sobre el DAG.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-162">Above the **DAG Details** are several links that can be used to display information about the DAG.</span></span>

   * <span data-ttu-id="0ed1f-163">**Contadores del DAG** muestra información de los contadores de este DAG.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-163">**DAG Counters** displays counters information for this DAG.</span></span>
   * <span data-ttu-id="0ed1f-164">**Vista gráfica** muestra una representación gráfica de este DAG.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-164">**Graphical View** displays a graphical representation of this DAG.</span></span>
   * <span data-ttu-id="0ed1f-165">**Todos los vértices** muestra una lista de los vértices de este DAG.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-165">**All Vertices** displays a list of the vertices in this DAG.</span></span>
   * <span data-ttu-id="0ed1f-166">**Todas las tareas** muestra una lista de las tareas de todos los vértices de este DAG.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-166">**All Tasks** displays a list of the tasks for all vertices in this DAG.</span></span>
   * <span data-ttu-id="0ed1f-167">**Todos los intentos de tarea** muestra información sobre los intentos de ejecutar las tareas de este DAG.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-167">**All TaskAttempts** displays information about the attempts to run tasks for this DAG.</span></span>

     > [!NOTE]
     > <span data-ttu-id="0ed1f-168">Si se desplaza por la presentación en columnas de Vértices, Tareas e Intentos de tarea, verá que hay vínculos para ver los **contadores** y para **ver o descargar los registros** de cada fila.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-168">If you scroll the column display for Vertices, Tasks and TaskAttempts, notice that there are links to view **counters** and **view or download logs** for each row.</span></span>
     >
     >

     <span data-ttu-id="0ed1f-169">Si se produjo un error en el trabajo, los detalles del DAG mostrarán un estado de error, junto con vínculos a información sobre la tarea con error.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-169">If there was a failure with the job, the DAG Details will display a status of FAILED, along with links to information about the failed task.</span></span> <span data-ttu-id="0ed1f-170">Debajo de los detalles del DAG, se mostrará información de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-170">Diagnostics information will be displayed beneath the DAG details.</span></span>
8. <span data-ttu-id="0ed1f-171">Seleccione **Vista gráfica**.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-171">Select **Graphical View**.</span></span> <span data-ttu-id="0ed1f-172">Muestra una representación gráfica del DAG.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-172">This displays a graphical representation of the DAG.</span></span> <span data-ttu-id="0ed1f-173">Puede colocar el mouse sobre cada vértice de la vista para mostrar su información.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-173">You can place the mouse over each vertex in the view to display information about it.</span></span>

    ![Vista gráfica](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. <span data-ttu-id="0ed1f-175">Al hacer clic en un vértice, se cargarán los **Detalles del vértice** de ese elemento.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-175">Clicking on a vertex will load the **Vertex Details** for that item.</span></span> <span data-ttu-id="0ed1f-176">Haga clic en el vértice **Asignación 1** para mostrar los detalles de ese elemento.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-176">Click on the **Map 1** vertex to display details for this item.</span></span> <span data-ttu-id="0ed1f-177">Seleccione **Confirmar** para confirmar la navegación.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-177">Select **Confirm** to confirm the navigation.</span></span>

    ![Detalles del vértice](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. <span data-ttu-id="0ed1f-179">Observe que ahora aparecen vínculos en la parte superior de la página que están relacionados con las tareas y los vértices.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-179">Note that you now have links at the top of the page that are related to vertices and tasks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0ed1f-180">Para llegar a esta página, puede regresar a **Detalles del DAG**, seleccionar **Detalles del vértice** y seleccionar el vértice **Asignación 1**.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-180">You can also arrive at this page by going back to **DAG Details**, selecting **Vertex Details**, and then selecting the **Map 1** vertex.</span></span>
    >
    >

    * <span data-ttu-id="0ed1f-181">**Contadores del vértice** muestra información de los contadores de este vértice.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-181">**Vertex Counters** displays counter information for this vertex.</span></span>
    * <span data-ttu-id="0ed1f-182">**Tareas** muestra las tareas de este vértice.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-182">**Tasks** displays tasks for this vertex.</span></span>
    * <span data-ttu-id="0ed1f-183">**Intentos de tarea** muestra información sobre los intentos de ejecutar las tareas de este vértice.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-183">**Task Attempts** displays information about attempts to run tasks for this vertex.</span></span>
    * <span data-ttu-id="0ed1f-184">**Orígenes y receptores** muestra los orígenes de datos y los receptores de este vértice.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-184">**Sources & Sinks** displays data sources and sinks for this vertex.</span></span>

      > [!NOTE]
      > <span data-ttu-id="0ed1f-185">Al igual que en el menú anterior, puede desplazarse por la presentación de columna de Tareas, Intentos de tarea y Orígenes y receptores para que aparezcan vínculos a información adicional sobre cada elemento.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-185">As with the previous menu, you can scroll the column display for Tasks, Task Attempts, and Sources & Sinks__ to display links to more information for each item.</span></span>
      >
      >
11. <span data-ttu-id="0ed1f-186">Seleccione **Tareas** y luego seleccione el elemento llamado **00_000000**.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-186">Select **Tasks**, and then select the item named **00_000000**.</span></span> <span data-ttu-id="0ed1f-187">De este modo se mostrarán los **Detalles de la tarea** de esta tarea.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-187">This will display **Task Details** for this task.</span></span> <span data-ttu-id="0ed1f-188">En esta pantalla, puede ver los **Contadores de tarea** y los **Intentos de tarea**.</span><span class="sxs-lookup"><span data-stu-id="0ed1f-188">From this screen, you can view **Task Counters** and **Task Attempts**.</span></span>

    ![Detalles de la tarea](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a><span data-ttu-id="0ed1f-190">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0ed1f-190">Next Steps</span></span>
<span data-ttu-id="0ed1f-191">Ahora que ha aprendido a usar la vista de Tez, obtenga más información sobre el [Uso de Hive en HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="0ed1f-191">Now that you have learned how to use the Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="0ed1f-192">Para obtener información técnica más detallada sobre Tez, consulte la [página de Tez en Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="0ed1f-192">For more detailed technical information on Tez, see the [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>
