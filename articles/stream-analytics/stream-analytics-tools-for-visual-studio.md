---
title: Uso de herramientas de Azure Stream Analytics para Visual Studio | Microsoft Docs
description: "Tutorial de introducción de las herramientas de Azure Stream Analytics para Visual Studio"
keywords: visual studio
documentationcenter: 
services: stream-analytics
author: 
manager: 
editor: 
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 
ms.author: 
ms.openlocfilehash: 618c1055795a75e0ed71dacddba3e076f81f4946
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a><span data-ttu-id="fb515-104">Uso de herramientas de Azure Stream Analytics para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fb515-104">Use Azure Stream Analytics Tools for Visual Studio</span></span>
## <a name="introduction"></a><span data-ttu-id="fb515-105">Introducción</span><span class="sxs-lookup"><span data-stu-id="fb515-105">Introduction</span></span>
<span data-ttu-id="fb515-106">En este tutorial, aprenderá a usar herramientas de Azure Stream Analytics para Visual Studio para crear, probar localmente, administrar y depurar los trabajos de Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="fb515-106">In this tutorial, you learn how to use Azure Stream Analytics Tools for Visual Studio to create, author, test locally, manage, and debug your Stream Analytics jobs.</span></span> 

<span data-ttu-id="fb515-107">Después de completar este tutorial, estará capacitado para lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fb515-107">After completing this tutorial, you will be able to:</span></span>
* <span data-ttu-id="fb515-108">Familiarícese con las herramientas de Stream Analytics para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fb515-108">Familiarize yourself with Stream Analytics Tools for Visual Studio.</span></span>
* <span data-ttu-id="fb515-109">Configurar e implementar un trabajo de Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="fb515-109">Configure and deploy a Stream Analytics job.</span></span>
* <span data-ttu-id="fb515-110">Probar el trabajo localmente con datos de ejemplo local.</span><span class="sxs-lookup"><span data-stu-id="fb515-110">Test your job locally with local sample data.</span></span>
* <span data-ttu-id="fb515-111">Usar la supervisión para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="fb515-111">Use monitoring to troubleshoot issues.</span></span>
* <span data-ttu-id="fb515-112">Exportar los trabajos existentes a proyectos.</span><span class="sxs-lookup"><span data-stu-id="fb515-112">Export existing jobs to projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb515-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fb515-113">Prerequisites</span></span>
<span data-ttu-id="fb515-114">Para completar este tutorial, debe cumplir los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="fb515-114">To complete this tutorial, you need the following prerequisites:</span></span>
* <span data-ttu-id="fb515-115">Complete los pasos anteriores a "Creación de un trabajo de Stream Analytics" del [tutorial Compilación de una solución de IoT con Stream Analytics](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="fb515-115">Finish the steps that precede "Create a Stream Analytics job" in the [Build an IoT solution by using Stream Analytics tutorial](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span></span> 
* <span data-ttu-id="fb515-116">Use Visual Studio 2015, Visual Studio 2013 Update 4 o Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="fb515-116">Use Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012.</span></span> <span data-ttu-id="fb515-117">Se admiten las ediciones Enterprise (Ultimate y Premium), Professional y Community.</span><span class="sxs-lookup"><span data-stu-id="fb515-117">Enterprise (Ultimate/Premium), Professional, and Community editions are supported.</span></span> <span data-ttu-id="fb515-118">No se admite la edición Express.</span><span class="sxs-lookup"><span data-stu-id="fb515-118">Express edition is not supported.</span></span> <span data-ttu-id="fb515-119">Visual Studio 2017 no se admite.</span><span class="sxs-lookup"><span data-stu-id="fb515-119">Visual Studio 2017 is not supported.</span></span> 
* <span data-ttu-id="fb515-120">Use Azure SDK para .NET versión 2.7.1 o posterior.</span><span class="sxs-lookup"><span data-stu-id="fb515-120">Use the Azure SDK for .NET version 2.7.1 or later.</span></span> <span data-ttu-id="fb515-121">Instálelo con el [Instalador de plataforma web](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="fb515-121">Install it by using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="fb515-122">Instale las [herramientas de Stream Analytics para Visual Studio](http://aka.ms/asatoolsvs).</span><span class="sxs-lookup"><span data-stu-id="fb515-122">Install the [Stream Analytics Tools for Visual Studio](http://aka.ms/asatoolsvs).</span></span>

## <a name="create-a-stream-analytics-project"></a><span data-ttu-id="fb515-123">Creación de un trabajo de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fb515-123">Create a Stream Analytics project</span></span>
1. <span data-ttu-id="fb515-124">En Visual Studio, haga clic en el menú **Archivo** y seleccione **Nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="fb515-124">In Visual Studio, click the **File** menu and select **New Project**.</span></span> 

2. <span data-ttu-id="fb515-125">Seleccione **Stream Analytics** en la lista de plantillas de la izquierda y, después, haga clic en **Azure Stream Analytics Application** (Aplicación de Azure Stream Analytics).</span><span class="sxs-lookup"><span data-stu-id="fb515-125">In the templates list on the left, select **Stream Analytics** and then click **Azure Stream Analytics Application**.</span></span>

3. <span data-ttu-id="fb515-126">Escriba el **Nombre**, **Ubicación** y **Nombre de la solución** del proyecto como lo hace para otros proyectos.</span><span class="sxs-lookup"><span data-stu-id="fb515-126">Enter the project **Name**, **Location**, and **Solution name** as you do for other projects.</span></span>

    ![Ventana Nuevo proyecto](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    <span data-ttu-id="fb515-128">Un proyecto de **peaje** se ha generado en el **Explorador de soluciones**.</span><span class="sxs-lookup"><span data-stu-id="fb515-128">A **Toll** project is generated in **Solution Explorer**.</span></span>

    ![El proyecto de peaje se ha generado en el Explorador de soluciones](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-the-correct-subscription"></a><span data-ttu-id="fb515-130">Elegir la suscripción correcta</span><span class="sxs-lookup"><span data-stu-id="fb515-130">Choose the correct subscription</span></span>
1. <span data-ttu-id="fb515-131">En Visual Studio, haga clic en el menú **Ver** y abra el **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="fb515-131">In Visual Studio, click the **View** menu and open **Server Explorer**.</span></span>

2. <span data-ttu-id="fb515-132">Inicie sesión con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="fb515-132">Sign in with your Azure Account.</span></span> 

## <a name="define-the-input-sources"></a><span data-ttu-id="fb515-133">Definir los orígenes de entrada</span><span class="sxs-lookup"><span data-stu-id="fb515-133">Define the input sources</span></span>
1.  <span data-ttu-id="fb515-134">En el **Explorador de soluciones**, expanda el nodo **Inputs** y cambie el nombre de **Input.json** a **EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="fb515-134">In **Solution Explorer**, expand the **Inputs** node and rename **Input.json** to **EntryStream.json**.</span></span> <span data-ttu-id="fb515-135">Haga doble clic en **EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="fb515-135">Double-click **EntryStream.json**.</span></span>
2.  <span data-ttu-id="fb515-136">Ahora, el **Alias de entrada** es **EntryStream**.</span><span class="sxs-lookup"><span data-stu-id="fb515-136">The **Input Alias** is now **EntryStream**.</span></span> <span data-ttu-id="fb515-137">El alias de entrada se usa en el script de consulta.</span><span class="sxs-lookup"><span data-stu-id="fb515-137">The input alias is used in the query script.</span></span> 
3.  <span data-ttu-id="fb515-138">En **Tipo de origen**, seleccione **Flujo de datos**.</span><span class="sxs-lookup"><span data-stu-id="fb515-138">In **Source Type**, select **Data Stream**.</span></span>
4.  <span data-ttu-id="fb515-139">En **Origen**, seleccione **Centro de eventos**.</span><span class="sxs-lookup"><span data-stu-id="fb515-139">In **Source**, select **Event Hub**.</span></span>
5.  <span data-ttu-id="fb515-140">En **Espacio de nombres de Service Bus**, seleccione la opción **TollData**.</span><span class="sxs-lookup"><span data-stu-id="fb515-140">In **Service Bus Namespace**, select the **TollData** option.</span></span>
6.  <span data-ttu-id="fb515-141">En **Nombre del centro de eventos**, seleccione **entrada**.</span><span class="sxs-lookup"><span data-stu-id="fb515-141">In **Event Hub Name**, select **entry**.</span></span>
7.  <span data-ttu-id="fb515-142">En **Nombre de la directiva del centro de eventos**, seleccione **RootManageSharedAccessKey** (el valor predeterminado).</span><span class="sxs-lookup"><span data-stu-id="fb515-142">In **Event Hub Policy Name**, select **RootManageSharedAccessKey** (the default value).</span></span>
8.  <span data-ttu-id="fb515-143">En **Formato de serialización de eventos**, seleccione **Json**.</span><span class="sxs-lookup"><span data-stu-id="fb515-143">In **Event Serialization Format**, select **Json**.</span></span> 
9.  <span data-ttu-id="fb515-144">En **Codificación**, seleccione **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="fb515-144">In **Encoding**, select **UTF8**.</span></span> <span data-ttu-id="fb515-145">Su configuración debe ser similar a la siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="fb515-145">Your settings should look like the following screenshot:</span></span>

    ![Ventana de entrada](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. <span data-ttu-id="fb515-147">Para finalizar el asistente, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fb515-147">To finish the wizard, click **Save**.</span></span> <span data-ttu-id="fb515-148">Ahora puede agregar otra fuente de entrada para crear la secuencia de salida.</span><span class="sxs-lookup"><span data-stu-id="fb515-148">Now you can add another input source to create the exit stream.</span></span> <span data-ttu-id="fb515-149">Haga clic con el botón derecho en el nodo **Inputs** y seleccione **Nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="fb515-149">Right-click the **Inputs** node, and select **New Item**.</span></span>

    ![Nuevo elemento](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. <span data-ttu-id="fb515-151">En la ventana, seleccione **Azure Stream Analytics Input** (Entrada de Azure Stream Analytics) y cambie el **nombre** a **ExitStream.json**.</span><span class="sxs-lookup"><span data-stu-id="fb515-151">In the window, select **Azure Stream Analytics Input**, and change the **Name** to **ExitStream.json**.</span></span> <span data-ttu-id="fb515-152">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="fb515-152">Click **Add**.</span></span>

    ![Ventana Agregar nuevo elemento](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. <span data-ttu-id="fb515-154">Haga doble clic en **ExitStream.json** en el proyecto y siga los mismos pasos que para el flujo de entrada.</span><span class="sxs-lookup"><span data-stu-id="fb515-154">Double-click **ExitStream.json** in the project, and follow the same steps as you did for the entry stream.</span></span> <span data-ttu-id="fb515-155">Asegúrese de especificar **exit** para el **Nombre del centro de eventos** como se muestra en la siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="fb515-155">Be sure to enter **exit** for the **Event Hub Name** as shown in the following screenshot:</span></span>

    ![Ventana ExitStream](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    <span data-ttu-id="fb515-157">Ahora ha definido dos flujos de entrada:</span><span class="sxs-lookup"><span data-stu-id="fb515-157">Now you have defined two input streams:</span></span>

    ![Flujos de entrada y salida](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    <span data-ttu-id="fb515-159">Después, agregue la entrada de datos de referencia para el archivo de blob que contiene los datos de registro de los vehículos.</span><span class="sxs-lookup"><span data-stu-id="fb515-159">Next, add reference data input for the blob file that contains car registration data.</span></span>

13. <span data-ttu-id="fb515-160">Haga clic con el botón derecho en el nodo **Inputs** del proyecto y, después, siga los mismos pasos que realizó para las entradas de secuencias.</span><span class="sxs-lookup"><span data-stu-id="fb515-160">Right-click the **Inputs** node in the project, and then follow the same steps as you did for the stream inputs.</span></span> <span data-ttu-id="fb515-161">En **Alias de entrada**, escriba **Registro** y en **Tipo de origen**, seleccione **Datos de referencia**.</span><span class="sxs-lookup"><span data-stu-id="fb515-161">In **Input Alias**, enter **Registration**, and in **Source Type**, select **Reference data**.</span></span>

    ![Ventana Registro](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. <span data-ttu-id="fb515-163">En **Cuenta de almacenamiento**, seleccione la opción **tolldata**.</span><span class="sxs-lookup"><span data-stu-id="fb515-163">In **Storage Account**, select the **tolldata** option.</span></span> <span data-ttu-id="fb515-164">En **Contenedor**, seleccione **tolldata** y, en **Patrón de ruta de acceso**, escriba **registration.json**.</span><span class="sxs-lookup"><span data-stu-id="fb515-164">In **Container**, select **tolldata**, and in **Path Pattern**, enter **registration.json**.</span></span> <span data-ttu-id="fb515-165">Este nombre de archivo distingue mayúsculas de minúsculas, por lo que asegúrese de escribirlo en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="fb515-165">This file name is case sensitive and should be lowercase.</span></span>
15. <span data-ttu-id="fb515-166">Para finalizar el asistente, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fb515-166">To finish the wizard, click **Save**.</span></span>

<span data-ttu-id="fb515-167">Ahora todas las entradas están definidas.</span><span class="sxs-lookup"><span data-stu-id="fb515-167">Now all the inputs are defined.</span></span>

## <a name="define-the-output"></a><span data-ttu-id="fb515-168">Definir la salida</span><span class="sxs-lookup"><span data-stu-id="fb515-168">Define the output</span></span>
1.  <span data-ttu-id="fb515-169">En el **Explorador de soluciones**, expanda el nodo **Inputs** y haga doble clic en **Output.json**.</span><span class="sxs-lookup"><span data-stu-id="fb515-169">In **Solution Explorer**, expand the **Inputs** node and double-click **Output.json**.</span></span>

2.  <span data-ttu-id="fb515-170">En **Alias de salida**, escriba **salida**.</span><span class="sxs-lookup"><span data-stu-id="fb515-170">In **Output Alias**, enter **output**.</span></span> 
3.  <span data-ttu-id="fb515-171">En **Receptor**, seleccione **SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="fb515-171">In **Sink**, select **SQL Database**.</span></span>
4.  <span data-ttu-id="fb515-172">En **Base de datos**, seleccione **TollDataDB**.</span><span class="sxs-lookup"><span data-stu-id="fb515-172">In **Database**, select **TollDataDB**.</span></span>
5.  <span data-ttu-id="fb515-173">En **Nombre de usuario**, escriba **tolladmin**.</span><span class="sxs-lookup"><span data-stu-id="fb515-173">In **User Name**, enter **tolladmin**.</span></span> 
6.  <span data-ttu-id="fb515-174">En **Contraseña**, escriba **123toll!**.</span><span class="sxs-lookup"><span data-stu-id="fb515-174">In **Password**, enter **123toll!**.</span></span>
7.  <span data-ttu-id="fb515-175">En **Tabla**, escriba **TollDataRefJoin**.</span><span class="sxs-lookup"><span data-stu-id="fb515-175">In **Table**, enter **TollDataRefJoin**.</span></span>
8.  <span data-ttu-id="fb515-176">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fb515-176">Click **Save**.</span></span>

    ![Ventana de salida](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a><span data-ttu-id="fb515-178">Creación de una consulta de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fb515-178">Create a Stream Analytics query</span></span>
<span data-ttu-id="fb515-179">Este tutorial intenta responder varias preguntas de empresa que están relacionadas con los datos de peaje.</span><span class="sxs-lookup"><span data-stu-id="fb515-179">This tutorial attempts to answer several business questions that are related to toll data.</span></span> <span data-ttu-id="fb515-180">También crea consultas de Stream Analytics que pueden usarse en Stream Analytics para proporcionar respuestas relevantes.</span><span class="sxs-lookup"><span data-stu-id="fb515-180">It also constructs Stream Analytics queries that can be used in Stream Analytics to provide relevant answers.</span></span>
<span data-ttu-id="fb515-181">Antes de iniciar el primer trabajo de Stream Analytics, veamos un escenario sencillo y la sintaxis de consulta.</span><span class="sxs-lookup"><span data-stu-id="fb515-181">Before you start your first Stream Analytics job, let’s explore a simple scenario and the query syntax.</span></span>

### <a name="introduction-to-the-stream-analytics-query-language"></a><span data-ttu-id="fb515-182">Introducción al lenguaje de consulta de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fb515-182">Introduction to the Stream Analytics query language</span></span>
<span data-ttu-id="fb515-183">Supongamos que necesita contar el número de vehículos que entran en una cabina de peaje.</span><span class="sxs-lookup"><span data-stu-id="fb515-183">Let’s say that you need to count the number of vehicles that enter a toll booth.</span></span> <span data-ttu-id="fb515-184">Como este ejemplo es una secuencia continua de eventos, tendrá que definir un período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="fb515-184">Because this example is a continuous stream of events, you have to define a period of time.</span></span> <span data-ttu-id="fb515-185">Cambie la pregunta a "¿Cuántos vehículos entran en una cabina de peaje cada tres minutos?".</span><span class="sxs-lookup"><span data-stu-id="fb515-185">Modify the question to be “How many vehicles enter a toll booth every three minutes?”</span></span> <span data-ttu-id="fb515-186">Este modo para contar datos se conoce normalmente como "tumbling count".</span><span class="sxs-lookup"><span data-stu-id="fb515-186">This way to count data is commonly referred to as the tumbling count.</span></span>

<span data-ttu-id="fb515-187">Veamos la consulta de Stream Analytics que responde a esta pregunta:</span><span class="sxs-lookup"><span data-stu-id="fb515-187">Look at the Stream Analytics query that answers this question:</span></span>

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

<span data-ttu-id="fb515-188">Stream Analytics usa un lenguaje de consulta que es similar a SQL y agrega algunas extensiones para especificar aspectos de la consulta relacionados con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="fb515-188">Stream Analytics uses a query language that's like SQL and adds a few extensions to specify time-related aspects of the query.</span></span>

<span data-ttu-id="fb515-189">Para obtener más información, vea las construcciones de [Administración del tiempo](https://msdn.microsoft.com/library/azure/mt582045.aspx) y [Ventanas](https://msdn.microsoft.com/library/azure/dn835019.aspx) que se usan en una consulta en MSDN.</span><span class="sxs-lookup"><span data-stu-id="fb515-189">For more information, see [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructs used in the query from MSDN.</span></span>

<span data-ttu-id="fb515-190">Ahora que ha escrito su primera consulta de Stream Analytics, es hora de probarla.</span><span class="sxs-lookup"><span data-stu-id="fb515-190">Now that you have written your first Stream Analytics query, it's time to test it.</span></span> <span data-ttu-id="fb515-191">Use los archivos de datos de ejemplo situados en su carpeta TollApp en la ruta de acceso siguiente:</span><span class="sxs-lookup"><span data-stu-id="fb515-191">Use the sample data files located in your TollApp folder in the following path:</span></span>

<span data-ttu-id="fb515-192">..\TollApp\TollApp\Data</span><span class="sxs-lookup"><span data-stu-id="fb515-192">..\TollApp\TollApp\Data</span></span>

<span data-ttu-id="fb515-193">Esta carpeta contiene los archivos siguientes:</span><span class="sxs-lookup"><span data-stu-id="fb515-193">This folder contains the following files:</span></span>
*   <span data-ttu-id="fb515-194">Entry.json</span><span class="sxs-lookup"><span data-stu-id="fb515-194">Entry.json</span></span>
*   <span data-ttu-id="fb515-195">Exit.json</span><span class="sxs-lookup"><span data-stu-id="fb515-195">Exit.json</span></span>
*   <span data-ttu-id="fb515-196">registration.json</span><span class="sxs-lookup"><span data-stu-id="fb515-196">Registration.json</span></span>

## <a name="count-the-number-of-vehicles-entering-a-toll-booth"></a><span data-ttu-id="fb515-197">Recuento del número de vehículos que entran en una cabina de peaje</span><span class="sxs-lookup"><span data-stu-id="fb515-197">Count the number of vehicles entering a toll booth</span></span>
<span data-ttu-id="fb515-198">En el proyecto, haga doble clic en **Script.asaql** para abrir el script en el **Editor de consultas**.</span><span class="sxs-lookup"><span data-stu-id="fb515-198">In the project, double-click **Script.asaql** to open the script in the **Query Editor**.</span></span> <span data-ttu-id="fb515-199">Copie y pegue el script de la sección anterior en el editor.</span><span class="sxs-lookup"><span data-stu-id="fb515-199">Copy and paste the script in the previous section into the editor.</span></span> <span data-ttu-id="fb515-200">El editor de consultas admite IntelliSense, colores para la sintaxis y el marcador de errores.</span><span class="sxs-lookup"><span data-stu-id="fb515-200">The Query Editor supports IntelliSense, syntax coloring, and the error marker.</span></span>

![Editor de consultas](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a><span data-ttu-id="fb515-202">Probar las consultas de Stream Analytics localmente</span><span class="sxs-lookup"><span data-stu-id="fb515-202">Test Stream Analytics queries locally</span></span>

1. <span data-ttu-id="fb515-203">Para compilar la consulta para ver si hay un error de sintaxis, haga clic con el botón derecho en el proyecto y seleccione **Compilar**.</span><span class="sxs-lookup"><span data-stu-id="fb515-203">To compile the query to see if there is a syntax error, right-click the project and select **Build**.</span></span> 

2. <span data-ttu-id="fb515-204">Para validar esta consulta con los datos de ejemplo, puede usar datos de ejemplo locales.</span><span class="sxs-lookup"><span data-stu-id="fb515-204">To validate this query against sample data, you can use local sample data.</span></span> <span data-ttu-id="fb515-205">Haga clic con el botón derecho en la entrada y seleccione **Agregar entrada local**.</span><span class="sxs-lookup"><span data-stu-id="fb515-205">Right-click the input, and select **Add local input**.</span></span>

    ![Agregar entrada local](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. <span data-ttu-id="fb515-207">En la ventana emergente, seleccione los datos de ejemplo de la ruta de acceso local.</span><span class="sxs-lookup"><span data-stu-id="fb515-207">In the pop-up window, select the sample data from your local path.</span></span> <span data-ttu-id="fb515-208">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fb515-208">Click **Save**.</span></span>

    ![Agregar ventana de entrada local](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    <span data-ttu-id="fb515-210">Un archivo denominado **local_EntryStream.json** se agrega automáticamente a la carpeta Inputs.</span><span class="sxs-lookup"><span data-stu-id="fb515-210">A file named **local_EntryStream.json** is automatically added to your inputs folder.</span></span>

    ![Archivo agregado a la carpeta Inputs](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. <span data-ttu-id="fb515-212">En el **Editor de consultas**, haga clic en **Ejecutar localmente**.</span><span class="sxs-lookup"><span data-stu-id="fb515-212">In the **Query Editor**, click **Run Locally**.</span></span> <span data-ttu-id="fb515-213">O bien, puede presionar la tecla F5.</span><span class="sxs-lookup"><span data-stu-id="fb515-213">Or you can press the F5 key.</span></span>

    ![Ejecución en modo local](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![Resultado de la ejecución local](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    <span data-ttu-id="fb515-216">Pulse cualquier tecla para ver el resultado en la ventana **Resultado de la ejecución local de ASA** en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fb515-216">Press any key to view the output in the **ASA Local Run Result** window in Visual Studio.</span></span> 

    ![Ventana Resultado de la ejecución local de ASA](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. <span data-ttu-id="fb515-218">Haga clic en **Abrir carpeta de resultados** para comprobar que los archivos de salida están en formato CSV y JSON.</span><span class="sxs-lookup"><span data-stu-id="fb515-218">Click **Open Result Folder** to check the output files both in CSV and JSON format.</span></span>

    ![Resultado de abrir la carpeta de resultados](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-the-input-data"></a><span data-ttu-id="fb515-220">Usar los datos de entrada como ejemplo</span><span class="sxs-lookup"><span data-stu-id="fb515-220">Sample the input data</span></span>
<span data-ttu-id="fb515-221">También puede usar los datos de entrada de orígenes de entrada como ejemplo en un archivo local.</span><span class="sxs-lookup"><span data-stu-id="fb515-221">You can also sample input data from input sources to a local file.</span></span> 
1. <span data-ttu-id="fb515-222">Haga clic con el botón derecho en el archivo de configuración de entrada y seleccione **Datos de ejemplo**.</span><span class="sxs-lookup"><span data-stu-id="fb515-222">Right-click the input config file, and select **Sample Data**.</span></span> 

   ![Datos de ejemplo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    <span data-ttu-id="fb515-224">Por el momento solo puede usar como ejemplo el centro de eventos o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="fb515-224">You can sample only event hub or IoT hub for now.</span></span> <span data-ttu-id="fb515-225">No se admiten otros orígenes de entrada.</span><span class="sxs-lookup"><span data-stu-id="fb515-225">Other input sources are not supported.</span></span>

2. <span data-ttu-id="fb515-226">En la ventana emergente, escriba la ruta de acceso local que se ha usado para guardar los datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="fb515-226">In the pop-up window, enter the local path used to save the sample data.</span></span> <span data-ttu-id="fb515-227">Haga clic en **Ejemplo**.</span><span class="sxs-lookup"><span data-stu-id="fb515-227">Click **Sample**.</span></span>

    ![Ventana de datos de ejemplo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    <span data-ttu-id="fb515-229">Puede ver el progreso en la ventana **Salida**.</span><span class="sxs-lookup"><span data-stu-id="fb515-229">You can see the progress in the **Output** window.</span></span> 

    ![Ventana de salida](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-to-azure"></a><span data-ttu-id="fb515-231">Enviar una consulta de Stream Analytics a Azure</span><span class="sxs-lookup"><span data-stu-id="fb515-231">Submit a Stream Analytics query to Azure</span></span>
1. <span data-ttu-id="fb515-232">En el **Editor de consultas**, haga clic en **Enviar a Azure** en el editor de scripts.</span><span class="sxs-lookup"><span data-stu-id="fb515-232">In the **Query Editor**, click **Submit To Azure** in the script editor.</span></span>

    ![Enviar a Azure](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. <span data-ttu-id="fb515-234">Seleccione **Crear un trabajo de Azure Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="fb515-234">Select **Create a New Azure Stream Analytics Job**.</span></span> <span data-ttu-id="fb515-235">Escriba el **Nombre del trabajo** y seleccione la **Suscripción** correcta.</span><span class="sxs-lookup"><span data-stu-id="fb515-235">Enter the **Job Name**, and select the correct **Subscription**.</span></span> <span data-ttu-id="fb515-236">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="fb515-236">Click **Submit**.</span></span>

    ![Ventana Enviar trabajo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a><span data-ttu-id="fb515-238">Iniciar un trabajo</span><span class="sxs-lookup"><span data-stu-id="fb515-238">Start a job</span></span>
<span data-ttu-id="fb515-239">Ahora que se ha creado el trabajo, se abre automáticamente la vista de trabajo.</span><span class="sxs-lookup"><span data-stu-id="fb515-239">Now that your job is created, the job view is automatically opened.</span></span> 
1. <span data-ttu-id="fb515-240">Para iniciar el trabajo, haga clic en el botón de **flecha verde**.</span><span class="sxs-lookup"><span data-stu-id="fb515-240">To start the job, click the **green arrow** button.</span></span>

    ![Iniciar un trabajo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. <span data-ttu-id="fb515-242">Seleccione la configuración predeterminada y haga clic en **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="fb515-242">Select the default setting, and click **Start**.</span></span>
 
    ![Ventana Iniciar trabajo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    <span data-ttu-id="fb515-244">El **estado** del trabajo cambia a **En ejecución** y aparecen **Eventos de entrada** y **Eventos de salida**.</span><span class="sxs-lookup"><span data-stu-id="fb515-244">The job **Status** changes to **Running**, and **Input Events** and **Output Events** appear.</span></span>

    ![Estado de ejecución en Resumen del trabajo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-the-results-in-visual-studio"></a><span data-ttu-id="fb515-246">Comprobación de los resultados en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fb515-246">Check the results in Visual Studio</span></span>
1. <span data-ttu-id="fb515-247">En Visual Studio, abra el **Explorador de servidores** y haga clic con el botón derecho en la tabla **TollDataRefJoin**.</span><span class="sxs-lookup"><span data-stu-id="fb515-247">In Visual Studio, open **Server Explorer** and right-click the **TollDataRefJoin** table.</span></span>
2. <span data-ttu-id="fb515-248">Seleccione **Mostrar datos de tabla** para ver el resultado del trabajo.</span><span class="sxs-lookup"><span data-stu-id="fb515-248">Select **Show Table Data** to see the output of your job.</span></span>
   
    ![Selección de Mostrar datos de tabla en el Explorador de servidores](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-the-job-metrics"></a><span data-ttu-id="fb515-250">Ver las métricas de trabajo</span><span class="sxs-lookup"><span data-stu-id="fb515-250">View the job metrics</span></span>
<span data-ttu-id="fb515-251">En **Job Metrics** (Métricas de trabajo) se pueden encontrar algunas estadísticas básicas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="fb515-251">Some basic job statistics can be found in **Job Metrics**.</span></span> 

![Ventana Métricas de trabajo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-the-job-in-server-explorer"></a><span data-ttu-id="fb515-253">Mostrar el trabajo en el Explorador de servidores</span><span class="sxs-lookup"><span data-stu-id="fb515-253">List the job in Server Explorer</span></span>
<span data-ttu-id="fb515-254">En el **Explorador de servidores**, haga clic en **Trabajos de Stream Analytics** y, después, haga clic en **Actualizar**.</span><span class="sxs-lookup"><span data-stu-id="fb515-254">In **Server Explorer**, click **Stream Analytics Jobs** and then click **Refresh**.</span></span> <span data-ttu-id="fb515-255">El trabajo aparece en **Trabajos de Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="fb515-255">The job appears under **Stream Analytics jobs**.</span></span>

![Los trabajos de Stream Analytics aparecen en el Explorador de servidores](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-the-job-view"></a><span data-ttu-id="fb515-257">Abrir la vista de trabajo</span><span class="sxs-lookup"><span data-stu-id="fb515-257">Open the job view</span></span>
<span data-ttu-id="fb515-258">Para abrir la vista de trabajos, expanda el nodo de trabajos y haga doble clic en el nodo **Vista de trabajos**.</span><span class="sxs-lookup"><span data-stu-id="fb515-258">To open the job view, expand your job node and double-click the **Job View** node.</span></span>

![Nodo Vista de trabajos](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-to-a-project"></a><span data-ttu-id="fb515-260">Exportación de un trabajo existente a un proyecto</span><span class="sxs-lookup"><span data-stu-id="fb515-260">Export an existing job to a project</span></span>
<span data-ttu-id="fb515-261">Hay dos maneras de exportar un trabajo existente a un proyecto.</span><span class="sxs-lookup"><span data-stu-id="fb515-261">There are two ways you can export an existing job to a project.</span></span>

<span data-ttu-id="fb515-262">En el **Explorador de servidores**, haga clic con el botón derecho en el nodo de trabajos en el nodo **Trabajos de Stream Analytics** y seleccione **Exportar a un nuevo proyecto de Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="fb515-262">In **Server Explorer**, right-click the job node in the **Stream Analytics Jobs** node and select **Export to New Stream Analytics Project**.</span></span>

![Exportar a un nuevo proyecto de Stream Analytics](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

<span data-ttu-id="fb515-264">El proyecto se genera en el **Explorador de soluciones**.</span><span class="sxs-lookup"><span data-stu-id="fb515-264">The project is generated in **Solution Explorer**.</span></span>

![Proyecto generado en el Explorador de soluciones](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
<span data-ttu-id="fb515-266">También puede usar la vista de trabajos y hacer clic en **Generar proyecto**.</span><span class="sxs-lookup"><span data-stu-id="fb515-266">You also can use the job view, and click **Generate Project**.</span></span>

![Generar el proyecto](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a><span data-ttu-id="fb515-268">Problemas conocidos y limitaciones</span><span class="sxs-lookup"><span data-stu-id="fb515-268">Known issues and limitations</span></span>
 
- <span data-ttu-id="fb515-269">No hay ninguna compatibilidad para la salida de Power BI y la salida de Azure Date Lake Store.</span><span class="sxs-lookup"><span data-stu-id="fb515-269">There is no support for Power BI output and Azure Date Lake Store output.</span></span>
- <span data-ttu-id="fb515-270">No hay ninguna compatibilidad con el editor para agregar o cambiar las funciones definidas por el usuario de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="fb515-270">There is no editor support for adding or changing JavaScript user-defined functions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb515-271">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fb515-271">Next steps</span></span>
* [<span data-ttu-id="fb515-272">Introducción al Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="fb515-272">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="fb515-273">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fb515-273">Get started by using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="fb515-274">Escalación de trabajos de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="fb515-274">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="fb515-275">Referencia del lenguaje de consulta de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fb515-275">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="fb515-276">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fb515-276">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
