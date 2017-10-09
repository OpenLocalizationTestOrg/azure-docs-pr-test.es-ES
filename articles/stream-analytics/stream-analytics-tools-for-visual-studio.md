---
title: "Herramientas de análisis de transmisiones de Azure para Visual Studio aaaUse | Documentos de Microsoft"
description: "Tutorial: Introducción para hello Azure Stream Analytics Tools para Visual Studio"
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
ms.openlocfilehash: bda8e548040509a6f29f1b713268bc38f73228fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a><span data-ttu-id="ee00d-104">Uso de herramientas de Azure Stream Analytics para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ee00d-104">Use Azure Stream Analytics Tools for Visual Studio</span></span>
## <a name="introduction"></a><span data-ttu-id="ee00d-105">Introducción</span><span class="sxs-lookup"><span data-stu-id="ee00d-105">Introduction</span></span>
<span data-ttu-id="ee00d-106">En este tutorial, aprenderá cómo análisis de flujo de toouse Azure Tools para Visual Studio toocreate, crear, probar localmente, administrar y depurar los trabajos de análisis de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="ee00d-106">In this tutorial, you learn how toouse Azure Stream Analytics Tools for Visual Studio toocreate, author, test locally, manage, and debug your Stream Analytics jobs.</span></span> 

<span data-ttu-id="ee00d-107">Después de completar este tutorial, estará capacitado para lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ee00d-107">After completing this tutorial, you will be able to:</span></span>
* <span data-ttu-id="ee00d-108">Familiarícese con las herramientas de Stream Analytics para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ee00d-108">Familiarize yourself with Stream Analytics Tools for Visual Studio.</span></span>
* <span data-ttu-id="ee00d-109">Configurar e implementar un trabajo de Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="ee00d-109">Configure and deploy a Stream Analytics job.</span></span>
* <span data-ttu-id="ee00d-110">Probar el trabajo localmente con datos de ejemplo local.</span><span class="sxs-lookup"><span data-stu-id="ee00d-110">Test your job locally with local sample data.</span></span>
* <span data-ttu-id="ee00d-111">Usar la supervisión de tootroubleshoot de problemas.</span><span class="sxs-lookup"><span data-stu-id="ee00d-111">Use monitoring tootroubleshoot issues.</span></span>
* <span data-ttu-id="ee00d-112">Exportar tooprojects de trabajos existente.</span><span class="sxs-lookup"><span data-stu-id="ee00d-112">Export existing jobs tooprojects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee00d-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ee00d-113">Prerequisites</span></span>
<span data-ttu-id="ee00d-114">toocomplete este tutorial, necesita Hola siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="ee00d-114">toocomplete this tutorial, you need hello following prerequisites:</span></span>
* <span data-ttu-id="ee00d-115">Complete los pasos de Hola que preceden a "Crear un trabajo de análisis de transmisiones" Hola [compila una solución de IoT mediante tutorial de análisis de transmisiones](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="ee00d-115">Finish hello steps that precede "Create a Stream Analytics job" in hello [Build an IoT solution by using Stream Analytics tutorial](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span></span> 
* <span data-ttu-id="ee00d-116">Use Visual Studio 2015, Visual Studio 2013 Update 4 o Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="ee00d-116">Use Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012.</span></span> <span data-ttu-id="ee00d-117">Se admiten las ediciones Enterprise (Ultimate y Premium), Professional y Community.</span><span class="sxs-lookup"><span data-stu-id="ee00d-117">Enterprise (Ultimate/Premium), Professional, and Community editions are supported.</span></span> <span data-ttu-id="ee00d-118">No se admite la edición Express.</span><span class="sxs-lookup"><span data-stu-id="ee00d-118">Express edition is not supported.</span></span> <span data-ttu-id="ee00d-119">Visual Studio 2017 no se admite.</span><span class="sxs-lookup"><span data-stu-id="ee00d-119">Visual Studio 2017 is not supported.</span></span> 
* <span data-ttu-id="ee00d-120">Hola utilice Azure SDK para .NET versión 2.7.1 o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="ee00d-120">Use hello Azure SDK for .NET version 2.7.1 or later.</span></span> <span data-ttu-id="ee00d-121">Instalar mediante hello [instalador de plataforma Web](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="ee00d-121">Install it by using hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="ee00d-122">Instalar hello [herramientas de análisis de secuencia para Visual Studio](http://aka.ms/asatoolsvs).</span><span class="sxs-lookup"><span data-stu-id="ee00d-122">Install hello [Stream Analytics Tools for Visual Studio](http://aka.ms/asatoolsvs).</span></span>

## <a name="create-a-stream-analytics-project"></a><span data-ttu-id="ee00d-123">Creación de un trabajo de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ee00d-123">Create a Stream Analytics project</span></span>
1. <span data-ttu-id="ee00d-124">En Visual Studio, haga clic en hello **archivo** menú y seleccione **nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-124">In Visual Studio, click hello **File** menu and select **New Project**.</span></span> 

2. <span data-ttu-id="ee00d-125">En lista de plantillas de Hola Hola izquierda, seleccione **análisis de transmisiones** y, a continuación, haga clic en **aplicación de Azure Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-125">In hello templates list on hello left, select **Stream Analytics** and then click **Azure Stream Analytics Application**.</span></span>

3. <span data-ttu-id="ee00d-126">Escriba proyecto hello **nombre**, **ubicación**, y **nombre de la solución** tal como hace para otros proyectos.</span><span class="sxs-lookup"><span data-stu-id="ee00d-126">Enter hello project **Name**, **Location**, and **Solution name** as you do for other projects.</span></span>

    ![Ventana Nuevo proyecto](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    <span data-ttu-id="ee00d-128">Un proyecto de **peaje** se ha generado en el **Explorador de soluciones**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-128">A **Toll** project is generated in **Solution Explorer**.</span></span>

    ![El proyecto de peaje se ha generado en el Explorador de soluciones](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-hello-correct-subscription"></a><span data-ttu-id="ee00d-130">Elija la suscripción correcta Hola</span><span class="sxs-lookup"><span data-stu-id="ee00d-130">Choose hello correct subscription</span></span>
1. <span data-ttu-id="ee00d-131">En Visual Studio, haga clic en hello **vista** menú y abra **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-131">In Visual Studio, click hello **View** menu and open **Server Explorer**.</span></span>

2. <span data-ttu-id="ee00d-132">Inicie sesión con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="ee00d-132">Sign in with your Azure Account.</span></span> 

## <a name="define-hello-input-sources"></a><span data-ttu-id="ee00d-133">Definir orígenes de entrada de Hola</span><span class="sxs-lookup"><span data-stu-id="ee00d-133">Define hello input sources</span></span>
1.  <span data-ttu-id="ee00d-134">En **el Explorador de soluciones**, expanda hello **entradas** nodo y el nombre **Input.json** demasiado**EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-134">In **Solution Explorer**, expand hello **Inputs** node and rename **Input.json** too**EntryStream.json**.</span></span> <span data-ttu-id="ee00d-135">Haga doble clic en **EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-135">Double-click **EntryStream.json**.</span></span>
2.  <span data-ttu-id="ee00d-136">Hola **Alias de entrada** es ahora **EntryStream**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-136">hello **Input Alias** is now **EntryStream**.</span></span> <span data-ttu-id="ee00d-137">alias de Hola de entrada se utiliza en la secuencia de comandos de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee00d-137">hello input alias is used in hello query script.</span></span> 
3.  <span data-ttu-id="ee00d-138">En **Tipo de origen**, seleccione **Flujo de datos**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-138">In **Source Type**, select **Data Stream**.</span></span>
4.  <span data-ttu-id="ee00d-139">En **Origen**, seleccione **Centro de eventos**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-139">In **Source**, select **Event Hub**.</span></span>
5.  <span data-ttu-id="ee00d-140">En **Namespace de Bus de servicio**, seleccione hello **TollData** opción.</span><span class="sxs-lookup"><span data-stu-id="ee00d-140">In **Service Bus Namespace**, select hello **TollData** option.</span></span>
6.  <span data-ttu-id="ee00d-141">En **Nombre del centro de eventos**, seleccione **entrada**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-141">In **Event Hub Name**, select **entry**.</span></span>
7.  <span data-ttu-id="ee00d-142">En **nombre de directiva de centro de eventos**, seleccione **RootManageSharedAccessKey** (Hola el valor predeterminado).</span><span class="sxs-lookup"><span data-stu-id="ee00d-142">In **Event Hub Policy Name**, select **RootManageSharedAccessKey** (hello default value).</span></span>
8.  <span data-ttu-id="ee00d-143">En **Formato de serialización de eventos**, seleccione **Json**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-143">In **Event Serialization Format**, select **Json**.</span></span> 
9.  <span data-ttu-id="ee00d-144">En **Codificación**, seleccione **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-144">In **Encoding**, select **UTF8**.</span></span> <span data-ttu-id="ee00d-145">La configuración debe ser similar Hola siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="ee00d-145">Your settings should look like hello following screenshot:</span></span>

    ![Ventana de entrada](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. <span data-ttu-id="ee00d-147">Asistente de hello toofinish, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-147">toofinish hello wizard, click **Save**.</span></span> <span data-ttu-id="ee00d-148">Ahora puede agregar otro flujo de salida de hello de toocreate de origen de entrada.</span><span class="sxs-lookup"><span data-stu-id="ee00d-148">Now you can add another input source toocreate hello exit stream.</span></span> <span data-ttu-id="ee00d-149">Menú contextual hello **entradas** nodo y seleccione **nuevo elemento**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-149">Right-click hello **Inputs** node, and select **New Item**.</span></span>

    ![Nuevo elemento](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. <span data-ttu-id="ee00d-151">En la ventana de hello, seleccione **entrada de análisis de flujo de Azure**y cambiar hello **nombre** demasiado**ExitStream.json**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-151">In hello window, select **Azure Stream Analytics Input**, and change hello **Name** too**ExitStream.json**.</span></span> <span data-ttu-id="ee00d-152">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-152">Click **Add**.</span></span>

    ![Ventana Agregar nuevo elemento](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. <span data-ttu-id="ee00d-154">Haga doble clic en **ExitStream.json** proyecto Hola y Hola seguimiento mismo pasos tal y como lo hizo para el flujo de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee00d-154">Double-click **ExitStream.json** in hello project, and follow hello same steps as you did for hello entry stream.</span></span> <span data-ttu-id="ee00d-155">Ser seguro tooenter **salir** para hello **nombre centro de eventos** tal y como se muestra en la siguiente captura de pantalla de hello:</span><span class="sxs-lookup"><span data-stu-id="ee00d-155">Be sure tooenter **exit** for hello **Event Hub Name** as shown in hello following screenshot:</span></span>

    ![Ventana ExitStream](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    <span data-ttu-id="ee00d-157">Ahora ha definido dos flujos de entrada:</span><span class="sxs-lookup"><span data-stu-id="ee00d-157">Now you have defined two input streams:</span></span>

    ![Flujos de entrada y salida](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    <span data-ttu-id="ee00d-159">A continuación, agregue la entrada de datos de referencia para el archivo de blob de Hola que contiene datos de registro del automóvil.</span><span class="sxs-lookup"><span data-stu-id="ee00d-159">Next, add reference data input for hello blob file that contains car registration data.</span></span>

13. <span data-ttu-id="ee00d-160">Menú contextual hello **entradas** nodo Hola proyecto y, a continuación, Hola seguimiento mismo pasos tal y como lo hizo para las entradas de la secuencia de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee00d-160">Right-click hello **Inputs** node in hello project, and then follow hello same steps as you did for hello stream inputs.</span></span> <span data-ttu-id="ee00d-161">En **Alias de entrada**, escriba **Registro** y en **Tipo de origen**, seleccione **Datos de referencia**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-161">In **Input Alias**, enter **Registration**, and in **Source Type**, select **Reference data**.</span></span>

    ![Ventana Registro](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. <span data-ttu-id="ee00d-163">En **cuenta de almacenamiento**, seleccione hello **tolldata** opción.</span><span class="sxs-lookup"><span data-stu-id="ee00d-163">In **Storage Account**, select hello **tolldata** option.</span></span> <span data-ttu-id="ee00d-164">En **Contenedor**, seleccione **tolldata** y, en **Patrón de ruta de acceso**, escriba **registration.json**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-164">In **Container**, select **tolldata**, and in **Path Pattern**, enter **registration.json**.</span></span> <span data-ttu-id="ee00d-165">Este nombre de archivo distingue mayúsculas de minúsculas, por lo que asegúrese de escribirlo en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="ee00d-165">This file name is case sensitive and should be lowercase.</span></span>
15. <span data-ttu-id="ee00d-166">Asistente de hello toofinish, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-166">toofinish hello wizard, click **Save**.</span></span>

<span data-ttu-id="ee00d-167">Ahora se definen todas las entradas de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee00d-167">Now all hello inputs are defined.</span></span>

## <a name="define-hello-output"></a><span data-ttu-id="ee00d-168">Definir la salida de hello</span><span class="sxs-lookup"><span data-stu-id="ee00d-168">Define hello output</span></span>
1.  <span data-ttu-id="ee00d-169">En **el Explorador de soluciones**, expanda hello **entradas** nodo y haga doble clic en **Output.json**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-169">In **Solution Explorer**, expand hello **Inputs** node and double-click **Output.json**.</span></span>

2.  <span data-ttu-id="ee00d-170">En **Alias de salida**, escriba **salida**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-170">In **Output Alias**, enter **output**.</span></span> 
3.  <span data-ttu-id="ee00d-171">En **Receptor**, seleccione **SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-171">In **Sink**, select **SQL Database**.</span></span>
4.  <span data-ttu-id="ee00d-172">En **Base de datos**, seleccione **TollDataDB**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-172">In **Database**, select **TollDataDB**.</span></span>
5.  <span data-ttu-id="ee00d-173">En **Nombre de usuario**, escriba **tolladmin**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-173">In **User Name**, enter **tolladmin**.</span></span> 
6.  <span data-ttu-id="ee00d-174">En **Contraseña**, escriba **123toll!**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-174">In **Password**, enter **123toll!**.</span></span>
7.  <span data-ttu-id="ee00d-175">En **Tabla**, escriba **TollDataRefJoin**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-175">In **Table**, enter **TollDataRefJoin**.</span></span>
8.  <span data-ttu-id="ee00d-176">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-176">Click **Save**.</span></span>

    ![Ventana de salida](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a><span data-ttu-id="ee00d-178">Creación de una consulta de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ee00d-178">Create a Stream Analytics query</span></span>
<span data-ttu-id="ee00d-179">Este tutorial trata tooanswer varias cuestiones empresariales que están relacionados tootoll datos.</span><span class="sxs-lookup"><span data-stu-id="ee00d-179">This tutorial attempts tooanswer several business questions that are related tootoll data.</span></span> <span data-ttu-id="ee00d-180">Además, crea las consultas de análisis de transmisiones que se pueden usar en las respuestas de análisis de transmisiones tooprovide relevantes.</span><span class="sxs-lookup"><span data-stu-id="ee00d-180">It also constructs Stream Analytics queries that can be used in Stream Analytics tooprovide relevant answers.</span></span>
<span data-ttu-id="ee00d-181">Antes de empezar su primer trabajo de análisis de transmisiones, vamos a examinar una sintaxis de consulta simple hello y escenario.</span><span class="sxs-lookup"><span data-stu-id="ee00d-181">Before you start your first Stream Analytics job, let’s explore a simple scenario and hello query syntax.</span></span>

### <a name="introduction-toohello-stream-analytics-query-language"></a><span data-ttu-id="ee00d-182">Introducción toohello lenguaje de consulta de análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="ee00d-182">Introduction toohello Stream Analytics query language</span></span>
<span data-ttu-id="ee00d-183">Supongamos que necesita el número de hello toocount de vehículos que entran en una cabina de peaje.</span><span class="sxs-lookup"><span data-stu-id="ee00d-183">Let’s say that you need toocount hello number of vehicles that enter a toll booth.</span></span> <span data-ttu-id="ee00d-184">Dado que este ejemplo es una secuencia continua de eventos, deberá toodefine un período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="ee00d-184">Because this example is a continuous stream of events, you have toodefine a period of time.</span></span> <span data-ttu-id="ee00d-185">Modificar hello toobe de pregunta "¿cuántos vehículos escriba una cabina de peaje cada tres minutos?"</span><span class="sxs-lookup"><span data-stu-id="ee00d-185">Modify hello question toobe “How many vehicles enter a toll booth every three minutes?”</span></span> <span data-ttu-id="ee00d-186">Este toocount de manera son ser datos conoce el recuento de saltos de tamaño constante de hello tooas.</span><span class="sxs-lookup"><span data-stu-id="ee00d-186">This way toocount data is commonly referred tooas hello tumbling count.</span></span>

<span data-ttu-id="ee00d-187">Un vistazo a la consulta de análisis de transmisiones de Hola que responda a esta pregunta:</span><span class="sxs-lookup"><span data-stu-id="ee00d-187">Look at hello Stream Analytics query that answers this question:</span></span>

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

<span data-ttu-id="ee00d-188">Análisis de transmisiones usa un lenguaje de consulta que es similar a SQL y agrega algunas extensiones toospecify relacionados con el tiempo aspectos de hello consulta.</span><span class="sxs-lookup"><span data-stu-id="ee00d-188">Stream Analytics uses a query language that's like SQL and adds a few extensions toospecify time-related aspects of hello query.</span></span>

<span data-ttu-id="ee00d-189">Para obtener más información, consulte [administración del tiempo](https://msdn.microsoft.com/library/azure/mt582045.aspx) y [ventana](https://msdn.microsoft.com/library/azure/dn835019.aspx) construcciones que se usan en consultas de Hola de MSDN.</span><span class="sxs-lookup"><span data-stu-id="ee00d-189">For more information, see [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructs used in hello query from MSDN.</span></span>

<span data-ttu-id="ee00d-190">Ahora que ha escrito la primera consulta de análisis de transmisiones, es el tiempo tootest lo.</span><span class="sxs-lookup"><span data-stu-id="ee00d-190">Now that you have written your first Stream Analytics query, it's time tootest it.</span></span> <span data-ttu-id="ee00d-191">Utilizar archivos de datos de ejemplo de Hola ubicados en la carpeta TollApp Hola siguiendo la ruta de acceso:</span><span class="sxs-lookup"><span data-stu-id="ee00d-191">Use hello sample data files located in your TollApp folder in hello following path:</span></span>

<span data-ttu-id="ee00d-192">..\TollApp\TollApp\Data</span><span class="sxs-lookup"><span data-stu-id="ee00d-192">..\TollApp\TollApp\Data</span></span>

<span data-ttu-id="ee00d-193">Esta carpeta contiene Hola siguientes archivos:</span><span class="sxs-lookup"><span data-stu-id="ee00d-193">This folder contains hello following files:</span></span>
*   <span data-ttu-id="ee00d-194">Entry.json</span><span class="sxs-lookup"><span data-stu-id="ee00d-194">Entry.json</span></span>
*   <span data-ttu-id="ee00d-195">Exit.json</span><span class="sxs-lookup"><span data-stu-id="ee00d-195">Exit.json</span></span>
*   <span data-ttu-id="ee00d-196">registration.json</span><span class="sxs-lookup"><span data-stu-id="ee00d-196">Registration.json</span></span>

## <a name="count-hello-number-of-vehicles-entering-a-toll-booth"></a><span data-ttu-id="ee00d-197">Número de Hola de vehículos puestos una cabina de peaje</span><span class="sxs-lookup"><span data-stu-id="ee00d-197">Count hello number of vehicles entering a toll booth</span></span>
<span data-ttu-id="ee00d-198">En el proyecto de hello, haga doble clic en **Script.asaql** tooopen script de Hola Hola **Editor de consultas**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-198">In hello project, double-click **Script.asaql** tooopen hello script in hello **Query Editor**.</span></span> <span data-ttu-id="ee00d-199">Copie y pegue el script de Hola en la sección anterior de hello en editor de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee00d-199">Copy and paste hello script in hello previous section into hello editor.</span></span> <span data-ttu-id="ee00d-200">Hola Editor de consultas admite IntelliSense, colorear la sintaxis y el marcador de error de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee00d-200">hello Query Editor supports IntelliSense, syntax coloring, and hello error marker.</span></span>

![Editor de consultas](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a><span data-ttu-id="ee00d-202">Probar las consultas de Stream Analytics localmente</span><span class="sxs-lookup"><span data-stu-id="ee00d-202">Test Stream Analytics queries locally</span></span>

1. <span data-ttu-id="ee00d-203">toocompile Hola consulta toosee si se produce un error de sintaxis, haga clic en proyecto de Hola y seleccione **generar**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-203">toocompile hello query toosee if there is a syntax error, right-click hello project and select **Build**.</span></span> 

2. <span data-ttu-id="ee00d-204">toovalidate esta consulta con datos de ejemplo, puede usar datos de ejemplo local.</span><span class="sxs-lookup"><span data-stu-id="ee00d-204">toovalidate this query against sample data, you can use local sample data.</span></span> <span data-ttu-id="ee00d-205">Haga clic en la entrada de Hola y seleccione **Agregar entrada local**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-205">Right-click hello input, and select **Add local input**.</span></span>

    ![Agregar entrada local](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. <span data-ttu-id="ee00d-207">En la ventana emergente de hello, seleccione datos de ejemplo de Hola desde la ruta de acceso local.</span><span class="sxs-lookup"><span data-stu-id="ee00d-207">In hello pop-up window, select hello sample data from your local path.</span></span> <span data-ttu-id="ee00d-208">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-208">Click **Save**.</span></span>

    ![Agregar ventana de entrada local](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    <span data-ttu-id="ee00d-210">Un archivo denominado **local_EntryStream.json** se agrega automáticamente la carpeta de entradas de tooyour.</span><span class="sxs-lookup"><span data-stu-id="ee00d-210">A file named **local_EntryStream.json** is automatically added tooyour inputs folder.</span></span>

    ![Carpeta de archivos de tooinputs agregado](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. <span data-ttu-id="ee00d-212">Hola **Editor de consultas**, haga clic en **ejecutar localmente**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-212">In hello **Query Editor**, click **Run Locally**.</span></span> <span data-ttu-id="ee00d-213">O bien, puede presionar la tecla F5 de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee00d-213">Or you can press hello F5 key.</span></span>

    ![Ejecución en modo local](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![Resultado de la ejecución local](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    <span data-ttu-id="ee00d-216">Presione cualquier resultado de hello tooview clave Hola **ASA Local ejecutar resultado** ventana de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ee00d-216">Press any key tooview hello output in hello **ASA Local Run Result** window in Visual Studio.</span></span> 

    ![Ventana Resultado de la ejecución local de ASA](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. <span data-ttu-id="ee00d-218">Haga clic en **abrir la carpeta de resultados** archivos de salida de hello toocheck tanto en formato CSV y JSON.</span><span class="sxs-lookup"><span data-stu-id="ee00d-218">Click **Open Result Folder** toocheck hello output files both in CSV and JSON format.</span></span>

    ![Resultado de abrir la carpeta de resultados](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-hello-input-data"></a><span data-ttu-id="ee00d-220">Datos de entrada de ejemplo Hola</span><span class="sxs-lookup"><span data-stu-id="ee00d-220">Sample hello input data</span></span>
<span data-ttu-id="ee00d-221">También puede datos de entrada de ejemplo de archivo local tooa de orígenes de entrada.</span><span class="sxs-lookup"><span data-stu-id="ee00d-221">You can also sample input data from input sources tooa local file.</span></span> 
1. <span data-ttu-id="ee00d-222">Haga clic en el archivo de configuración de entrada de Hola y seleccione **datos de ejemplo**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-222">Right-click hello input config file, and select **Sample Data**.</span></span> 

   ![Datos de ejemplo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    <span data-ttu-id="ee00d-224">Por el momento solo puede usar como ejemplo el centro de eventos o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ee00d-224">You can sample only event hub or IoT hub for now.</span></span> <span data-ttu-id="ee00d-225">No se admiten otros orígenes de entrada.</span><span class="sxs-lookup"><span data-stu-id="ee00d-225">Other input sources are not supported.</span></span>

2. <span data-ttu-id="ee00d-226">En la ventana emergente de hello, escriba datos de ejemplo de Hola utiliza la ruta de acceso local toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="ee00d-226">In hello pop-up window, enter hello local path used toosave hello sample data.</span></span> <span data-ttu-id="ee00d-227">Haga clic en **Ejemplo**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-227">Click **Sample**.</span></span>

    ![Ventana de datos de ejemplo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    <span data-ttu-id="ee00d-229">Puede ver el progreso Hola Hola **salida** ventana.</span><span class="sxs-lookup"><span data-stu-id="ee00d-229">You can see hello progress in hello **Output** window.</span></span> 

    ![Ventana de salida](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-tooazure"></a><span data-ttu-id="ee00d-231">Enviar una tooAzure de consultas de análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="ee00d-231">Submit a Stream Analytics query tooAzure</span></span>
1. <span data-ttu-id="ee00d-232">Hola **Editor de consultas**, haga clic en **enviar tooAzure** en el editor de script de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee00d-232">In hello **Query Editor**, click **Submit tooAzure** in hello script editor.</span></span>

    ![Enviar tooAzure](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. <span data-ttu-id="ee00d-234">Seleccione **Crear un trabajo de Azure Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-234">Select **Create a New Azure Stream Analytics Job**.</span></span> <span data-ttu-id="ee00d-235">Escriba hello **nombre del trabajo**, seleccione hello correcto y **suscripción**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-235">Enter hello **Job Name**, and select hello correct **Subscription**.</span></span> <span data-ttu-id="ee00d-236">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-236">Click **Submit**.</span></span>

    ![Ventana Enviar trabajo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a><span data-ttu-id="ee00d-238">Iniciar un trabajo</span><span class="sxs-lookup"><span data-stu-id="ee00d-238">Start a job</span></span>
<span data-ttu-id="ee00d-239">Ahora que se crea el trabajo, se abre automáticamente la vista de trabajos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee00d-239">Now that your job is created, hello job view is automatically opened.</span></span> 
1. <span data-ttu-id="ee00d-240">Hola toostart de trabajo, haga clic en hello **flecha verde** botón.</span><span class="sxs-lookup"><span data-stu-id="ee00d-240">toostart hello job, click hello **green arrow** button.</span></span>

    ![Iniciar un trabajo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. <span data-ttu-id="ee00d-242">Seleccione la configuración predeterminada de Hola y haga clic en **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-242">Select hello default setting, and click **Start**.</span></span>
 
    ![Ventana Iniciar trabajo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    <span data-ttu-id="ee00d-244">trabajo de Hello **estado** cambia demasiado**ejecutando**, y **eventos de entrada** y **eventos de salida** aparecen.</span><span class="sxs-lookup"><span data-stu-id="ee00d-244">hello job **Status** changes too**Running**, and **Input Events** and **Output Events** appear.</span></span>

    ![Estado de ejecución en Resumen del trabajo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-hello-results-in-visual-studio"></a><span data-ttu-id="ee00d-246">Comprobar los resultados de hello en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ee00d-246">Check hello results in Visual Studio</span></span>
1. <span data-ttu-id="ee00d-247">En Visual Studio, abra **Explorador de servidores** contextual hello y **TollDataRefJoin** tabla.</span><span class="sxs-lookup"><span data-stu-id="ee00d-247">In Visual Studio, open **Server Explorer** and right-click hello **TollDataRefJoin** table.</span></span>
2. <span data-ttu-id="ee00d-248">Seleccione **mostrar datos de tabla** toosee salida de hello de su trabajo.</span><span class="sxs-lookup"><span data-stu-id="ee00d-248">Select **Show Table Data** toosee hello output of your job.</span></span>
   
    ![Selección de Mostrar datos de tabla en el Explorador de servidores](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-hello-job-metrics"></a><span data-ttu-id="ee00d-250">Visualice las métricas de trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="ee00d-250">View hello job metrics</span></span>
<span data-ttu-id="ee00d-251">En **Job Metrics** (Métricas de trabajo) se pueden encontrar algunas estadísticas básicas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="ee00d-251">Some basic job statistics can be found in **Job Metrics**.</span></span> 

![Ventana Métricas de trabajo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-hello-job-in-server-explorer"></a><span data-ttu-id="ee00d-253">Trabajo de Hola de lista en el Explorador de servidores</span><span class="sxs-lookup"><span data-stu-id="ee00d-253">List hello job in Server Explorer</span></span>
<span data-ttu-id="ee00d-254">En el **Explorador de servidores**, haga clic en **Trabajos de Stream Analytics** y, después, haga clic en **Actualizar**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-254">In **Server Explorer**, click **Stream Analytics Jobs** and then click **Refresh**.</span></span> <span data-ttu-id="ee00d-255">trabajo de Hello aparece bajo **trabajos de análisis de transmisiones**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-255">hello job appears under **Stream Analytics jobs**.</span></span>

![Los trabajos de Stream Analytics aparecen en el Explorador de servidores](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-hello-job-view"></a><span data-ttu-id="ee00d-257">Vista de trabajos de hello abierto</span><span class="sxs-lookup"><span data-stu-id="ee00d-257">Open hello job view</span></span>
<span data-ttu-id="ee00d-258">vista de trabajos de hello tooopen, expanda el nodo de trabajo y haga doble clic hello **trabajo vista** nodo.</span><span class="sxs-lookup"><span data-stu-id="ee00d-258">tooopen hello job view, expand your job node and double-click hello **Job View** node.</span></span>

![Nodo Vista de trabajos](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-tooa-project"></a><span data-ttu-id="ee00d-260">Exportar un proyecto de tooa de trabajo existente</span><span class="sxs-lookup"><span data-stu-id="ee00d-260">Export an existing job tooa project</span></span>
<span data-ttu-id="ee00d-261">Hay dos maneras puede exportar un proyecto de tooa de trabajo existente.</span><span class="sxs-lookup"><span data-stu-id="ee00d-261">There are two ways you can export an existing job tooa project.</span></span>

<span data-ttu-id="ee00d-262">En **Explorador de servidores**, nodo de trabajo contextual Hola Hola **trabajos de análisis de transmisiones** nodo y seleccione **exportar tooNew proyecto de análisis de transmisiones**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-262">In **Server Explorer**, right-click hello job node in hello **Stream Analytics Jobs** node and select **Export tooNew Stream Analytics Project**.</span></span>

![Exportar tooNew proyecto de análisis de transmisiones](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

<span data-ttu-id="ee00d-264">se genera el proyecto de Hello en **el Explorador de soluciones**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-264">hello project is generated in **Solution Explorer**.</span></span>

![Proyecto generado en el Explorador de soluciones](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
<span data-ttu-id="ee00d-266">También puede usar la vista de trabajos de Hola y haga clic en **generar proyecto**.</span><span class="sxs-lookup"><span data-stu-id="ee00d-266">You also can use hello job view, and click **Generate Project**.</span></span>

![Generar el proyecto](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a><span data-ttu-id="ee00d-268">Problemas conocidos y limitaciones</span><span class="sxs-lookup"><span data-stu-id="ee00d-268">Known issues and limitations</span></span>
 
- <span data-ttu-id="ee00d-269">No hay ninguna compatibilidad para la salida de Power BI y la salida de Azure Date Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ee00d-269">There is no support for Power BI output and Azure Date Lake Store output.</span></span>
- <span data-ttu-id="ee00d-270">No hay ninguna compatibilidad con el editor para agregar o cambiar las funciones definidas por el usuario de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ee00d-270">There is no editor support for adding or changing JavaScript user-defined functions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee00d-271">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ee00d-271">Next steps</span></span>
* [<span data-ttu-id="ee00d-272">Introducción tooAzure análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="ee00d-272">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="ee00d-273">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ee00d-273">Get started by using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="ee00d-274">Escalación de trabajos de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="ee00d-274">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="ee00d-275">Referencia del lenguaje de consulta de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="ee00d-275">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="ee00d-276">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ee00d-276">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
