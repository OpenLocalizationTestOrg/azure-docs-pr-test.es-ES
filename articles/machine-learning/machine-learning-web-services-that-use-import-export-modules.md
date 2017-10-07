---
title: "aaaUsing datos de importación y exportación en los servicios web de aprendizaje automático de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Hola toosend de módulos de importación de datos y exportar datos y recibir datos de un servicio web."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3a7ac351-ebd3-43a1-8c5d-18223903d08e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 176380259b15cb338ede61c7f28ba2296b35dd52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-azure-ml-web-services-that-use-data-import-and-data-export-modules"></a><span data-ttu-id="a3d3b-103">Implementación de servicios web del aprendizaje automático de Azure que usan módulos de importación y exportación de datos</span><span class="sxs-lookup"><span data-stu-id="a3d3b-103">Deploying Azure ML web services that use Data Import and Data Export modules</span></span>

<span data-ttu-id="a3d3b-104">Cuando se crea un experimento predictivo, normalmente se agregan una entrada y una salida de servicio web.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-104">When you create a predictive experiment, you typically add a web service input and output.</span></span> <span data-ttu-id="a3d3b-105">Cuando se implementa el experimento de hello, los consumidores pueden enviar y recibir datos del servicio web de Hola a través de hello entradas y salidas.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-105">When you deploy hello experiment, consumers can send and receive data from hello web service through hello inputs and outputs.</span></span> <span data-ttu-id="a3d3b-106">En algunas aplicaciones, los datos del consumidor pueden estar disponibles desde una fuente de datos o ya residir en un origen de datos externo, como el Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-106">For some applications, a consumer's data may be available from a data feed or already reside in an external data source such as Azure Blob storage.</span></span> <span data-ttu-id="a3d3b-107">En estos casos, no se requiere que lean y escriban datos mediante entradas y salidas del servicio web.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-107">In these cases, they do not need read and write data using web service inputs and outputs.</span></span> <span data-ttu-id="a3d3b-108">En su lugar, puede usar datos de tooread de servicio de ejecución de lotes (BES) de Hola Hola origen de datos mediante un módulo de importación de datos y escribir hello tooa ubicación de datos diferente mediante un módulo de exportar datos de resultados de puntuación.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-108">They can, instead, use hello Batch Execution Service (BES) tooread data from hello data source using an Import Data module and write hello scoring results tooa different data location using an Export Data module.</span></span>

<span data-ttu-id="a3d3b-109">Hello importar datos y módulos de exportación de datos, puede leer y escribir datos toovarious proporcionan ubicaciones como una dirección URL Web a través de HTTP, una consulta de Hive, una base de datos SQL de Azure, almacenamiento de tabla de Azure, almacenamiento de blobs de Azure, una fuente de datos o una base de datos SQL local.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-109">hello Import Data and Export data modules, can read from and write toovarious data locations such as a Web URL via HTTP, a Hive Query, an Azure SQL database, Azure Table storage, Azure Blob storage, a Data Feed provide, or an on-premises SQL database.</span></span>

<span data-ttu-id="a3d3b-110">En este tema usa Hola "ejemplo 5: entrenar, prueba, evaluar para clasificación binaria: conjunto de datos Adult" de ejemplo y se da por supuesto Hola conjunto de datos ya se han cargado en una tabla de SQL Azure denominada censusdata.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-110">This topic uses hello "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample and assumes hello dataset has already been loaded into an Azure SQL table named censusdata.</span></span>

## <a name="create-hello-training-experiment"></a><span data-ttu-id="a3d3b-111">Crear experimento de entrenamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="a3d3b-111">Create hello training experiment</span></span>
<span data-ttu-id="a3d3b-112">Cuando abre Hola "ejemplo 5: entrenar, prueba, evaluar para clasificación binaria: conjunto de datos Adult" ejemplo de conjunto de datos utiliza Hola ejemplo clasificación binaria de ingresos del censo para adultos.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-112">When you open hello "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample it uses hello sample Adult Census Income Binary Classification dataset.</span></span> <span data-ttu-id="a3d3b-113">Y experimento hello en el lienzo de hello tendrá un aspecto similar toohello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="a3d3b-113">And hello experiment in hello canvas will look similar toohello following image:</span></span>

![Configuración inicial del experimento de Hola.](./media/machine-learning-web-services-that-use-import-export-modules/initial-look-of-experiment.png)

<span data-ttu-id="a3d3b-115">datos de hello tooread de tabla de SQL Azure hello:</span><span class="sxs-lookup"><span data-stu-id="a3d3b-115">tooread hello data from hello Azure SQL table:</span></span>

1. <span data-ttu-id="a3d3b-116">Eliminar el módulo de conjunto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-116">Delete hello dataset module.</span></span>
2. <span data-ttu-id="a3d3b-117">En el cuadro de búsqueda de componentes de hello, tipo de importación.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-117">In hello components search box, type import.</span></span>
3. <span data-ttu-id="a3d3b-118">Desde la lista de resultados de hello, agregar un *importar datos* toohello módulo experimentar lienzo.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-118">From hello results list, add an *Import Data* module toohello experiment canvas.</span></span>
4. <span data-ttu-id="a3d3b-119">Conecte la salida de hello *importar datos* entrada de módulo Hola de hello *limpiar datos que faltan* módulo.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-119">Connect output of hello *Import Data* module hello input of hello *Clean Missing Data* module.</span></span>
5. <span data-ttu-id="a3d3b-120">En el panel Propiedades, seleccione **base de datos de SQL Azure** en hello **origen de datos** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-120">In properties pane, select **Azure SQL Database** in hello **Data Source** dropdown.</span></span>
6. <span data-ttu-id="a3d3b-121">Hola **el nombre del servidor de base de datos**, **nombre de base de datos**, **nombre de usuario**, y **contraseña** campos, especifique la información adecuada de Hola para la base de datos.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-121">In hello **Database server name**, **Database name**, **User name**, and **Password** fields, enter hello appropriate information for your database.</span></span>
7. <span data-ttu-id="a3d3b-122">En el campo de consulta de base de datos de hello, escriba Hola después de consulta.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-122">In hello Database query field, enter hello following query.</span></span>
   
     <span data-ttu-id="a3d3b-123">select [age],</span><span class="sxs-lookup"><span data-stu-id="a3d3b-123">select [age],</span></span>
   
        [workclass],
        [fnlwgt],
        [education],
        [education-num],
        [marital-status],
        [occupation],
        [relationship],
        [race],
        [sex],
        [capital-gain],
        [capital-loss],
        [hours-per-week],
        [native-country],
        [income]
     <span data-ttu-id="a3d3b-124">from dbo.censusdata;</span><span class="sxs-lookup"><span data-stu-id="a3d3b-124">from dbo.censusdata;</span></span>
8. <span data-ttu-id="a3d3b-125">En la parte inferior de hello del lienzo del experimento de hello, haga clic en **ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-125">At hello bottom of hello experiment canvas, click **Run**.</span></span>

## <a name="create-hello-predictive-experiment"></a><span data-ttu-id="a3d3b-126">Crear experimento predictivo Hola</span><span class="sxs-lookup"><span data-stu-id="a3d3b-126">Create hello predictive experiment</span></span>
<span data-ttu-id="a3d3b-127">Después de que configurar experimento predictivo Hola desde el que implementa el servicio web.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-127">Next you set up hello predictive experiment from which you deploy your web service.</span></span>

1. <span data-ttu-id="a3d3b-128">En la parte inferior de hello del lienzo del experimento de hello, haga clic en **configurar el servicio de Web** y seleccione **predictivo Web Service [recomendado]**.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-128">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Predictive Web Service [Recommended]**.</span></span>
2. <span data-ttu-id="a3d3b-129">Quitar hello *proporcionados por el servicio Web* y *módulos de salida del servicio Web* de experimento predictivo Hola.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-129">Remove hello *Web Service Input* and *Web Service Output modules* from hello predictive experiment.</span></span> 
3. <span data-ttu-id="a3d3b-130">En el cuadro de búsqueda de componentes de hello, tipo de exportación.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-130">In hello components search box, type export.</span></span>
4. <span data-ttu-id="a3d3b-131">Desde la lista de resultados de hello, agregar un *exportar datos* toohello módulo experimentar lienzo.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-131">From hello results list, add an *Export Data* module toohello experiment canvas.</span></span>
5. <span data-ttu-id="a3d3b-132">Conecte la salida de hello *puntuar modelo* entrada de módulo Hola de hello *exportar datos* módulo.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-132">Connect output of hello *Score Model* module hello input of hello *Export Data* module.</span></span> 
6. <span data-ttu-id="a3d3b-133">En el panel Propiedades, seleccione **base de datos de SQL Azure** en la lista desplegable destino de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-133">In properties pane, select **Azure SQL Database** in hello data destination dropdown.</span></span>
7. <span data-ttu-id="a3d3b-134">Hola **el nombre del servidor de base de datos**, **nombre de base de datos**, **nombre de cuenta de usuario de servidor**, y **contraseña de cuenta de usuario de servidor** campos, escriba información adecuada de Hello para la base de datos.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-134">In hello **Database server name**, **Database name**, **Server user account name**, and **Server user account password** fields, enter hello appropriate information for your database.</span></span>
8. <span data-ttu-id="a3d3b-135">Hola **lista de toobe columnas guarda separada por comas** , escriba la puntuación de etiquetas.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-135">In hello **Comma separated list of columns toobe saved** field, type Scored Labels.</span></span>
9. <span data-ttu-id="a3d3b-136">Hola **campo de nombre de tabla de datos**, escriba dbo. ScoredLabels.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-136">In hello **Data table name field**, type dbo.ScoredLabels.</span></span> <span data-ttu-id="a3d3b-137">Si la tabla hello no existe, se crea cuando se ejecuta el experimento de Hola o se llama servicio de web de Hola.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-137">If hello table does not exist, it is created when hello experiment is run or hello web service is called.</span></span>
10. <span data-ttu-id="a3d3b-138">Hola **lista de columnas de tabla de datos separada por comas** campo, escriba ScoredLabels.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-138">In hello **Comma separated list of datatable columns** field, type ScoredLabels.</span></span>

<span data-ttu-id="a3d3b-139">Cuando se escribe una aplicación que llama Hola servicio web final, puede que desee toospecify una tabla de consulta o el destino entrada diferente en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-139">When you write an application that calls hello final web service, you may want toospecify a different input query or destination table at run time.</span></span> <span data-ttu-id="a3d3b-140">tooconfigure estas entradas y salidas, utilice Hola Hola de tooset de característica de parámetros de servicio Web *importar datos* módulo *origen de datos* hello y propiedad *exportar datos* modo propiedad de destino de datos.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-140">tooconfigure these inputs and outputs, use hello Web Service Parameters feature tooset hello *Import Data* module *Data source* property and hello *Export Data* mode data destination property.</span></span>  <span data-ttu-id="a3d3b-141">Para obtener más información sobre los parámetros del servicio Web, vea hello [entrada de parámetros de servicio Web de aprendizaje automático de Azure](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) en hello Intelligence Cortana y el Blog de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-141">For more information on Web Service Parameters, see hello [AzureML Web Service Parameters entry](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) on hello Cortana Intelligence and Machine Learning Blog.</span></span>

<span data-ttu-id="a3d3b-142">tooconfigure Hola parámetros de servicio Web de consulta de importación de Hola y tabla de destino de hello:</span><span class="sxs-lookup"><span data-stu-id="a3d3b-142">tooconfigure hello Web Service Parameters for hello import query and hello destination table:</span></span>

1. <span data-ttu-id="a3d3b-143">En panel de propiedades de Hola de hello *importar datos* módulo, haga clic en el icono de hello en hello parte superior derecha de hello **consulta de base de datos** campo y seleccione **establecer como parámetro del servicio web**.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-143">In hello properties pane for hello *Import Data* module, click hello icon at hello top right of hello **Database query** field and select **Set as web service parameter**.</span></span>
2. <span data-ttu-id="a3d3b-144">En panel de propiedades de Hola de hello *exportar datos* módulo, haga clic en el icono de hello en hello parte superior derecha de hello **nombre de la tabla de datos** campo y seleccione **establecer como parámetro del servicio web**.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-144">In hello properties pane for hello *Export Data* module, click hello icon at hello top right of hello **Data table name** field and select **Set as web service parameter**.</span></span>
3. <span data-ttu-id="a3d3b-145">En parte inferior de Hola de hello *exportar datos* panel de propiedades de módulo, en hello **parámetros de servicio Web** sección, haga clic en la consulta de base de datos y cambie su consulta.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-145">At hello bottom of hello *Export Data* module properties pane, in hello **Web Service Parameters** section, click Database query and rename it Query.</span></span>
4. <span data-ttu-id="a3d3b-146">Haga clic en **Nombre de la tabla de datos** y cambie el nombre por **Table**.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-146">Click **Data table name** and rename it **Table**.</span></span>

<span data-ttu-id="a3d3b-147">Cuando haya terminado, su experimento debería ser similar toohello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="a3d3b-147">When you are done, your experiment should look similar toohello following image:</span></span>

![Aspecto final del experimento.](./media/machine-learning-web-services-that-use-import-export-modules/experiment-with-import-data-added.png)

<span data-ttu-id="a3d3b-149">Ahora puede implementar Hola experimento como un servicio web.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-149">Now you can deploy hello experiment as a web service.</span></span>

## <a name="deploy-hello-web-service"></a><span data-ttu-id="a3d3b-150">Implementar el servicio web de Hola</span><span class="sxs-lookup"><span data-stu-id="a3d3b-150">Deploy hello web service</span></span>
<span data-ttu-id="a3d3b-151">Puede implementar tooeither un servicio web clásico o nuevo.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-151">You can deploy tooeither a Classic or New web service.</span></span>

### <a name="deploy-a-classic-web-service"></a><span data-ttu-id="a3d3b-152">Implementación de un servicio web clásico</span><span class="sxs-lookup"><span data-stu-id="a3d3b-152">Deploy a Classic Web Service</span></span>
<span data-ttu-id="a3d3b-153">toodeploy como un servicio Web clásico y crear una aplicación tooconsume:</span><span class="sxs-lookup"><span data-stu-id="a3d3b-153">toodeploy as a Classic Web Service and create an application tooconsume it:</span></span>

1. <span data-ttu-id="a3d3b-154">En parte inferior de hello del lienzo del experimento de hello, haga clic en ejecutar.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-154">At hello bottom of hello experiment canvas, click Run.</span></span>
2. <span data-ttu-id="a3d3b-155">Cuando haya finalizado Hola ejecutar, haga clic en **implementar el servicio de Web** y seleccione **implementar servicio Web [estándar]**.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-155">When hello run has completed, click **Deploy Web Service** and select **Deploy Web Service [Classic]**.</span></span>
3. <span data-ttu-id="a3d3b-156">En el panel de servicio web de hello, busque la clave de API.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-156">On hello web service dashboard, locate your API key.</span></span> <span data-ttu-id="a3d3b-157">Copie y guarde toouse más tarde.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-157">Copy and save it toouse later.</span></span>
4. <span data-ttu-id="a3d3b-158">Hola **punto de conexión predeterminado** de tabla, haga clic en hello **ejecución por lotes** Hola de vínculo tooopen página de Ayuda de API.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-158">In hello **Default Endpoint** table, click hello **Batch Execution** link tooopen hello API Help Page.</span></span>
5. <span data-ttu-id="a3d3b-159">Cree una nueva aplicación de consola de C# en Visual Studio: **Nuevo** > **Proyecto** > **Visual C#** > **Escritorio clásico de Windows** > **Aplicación de consola (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-159">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
6. <span data-ttu-id="a3d3b-160">En la página de Ayuda de la API de hello, encontrar Hola **código de ejemplo** sección final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-160">On hello API Help Page, find hello **Sample Code** section at hello bottom of hello page.</span></span>
7. <span data-ttu-id="a3d3b-161">Copie y pegue Hola código de ejemplo de C# en el archivo Program.cs y quitar el almacenamiento de blobs de toohello de todas las referencias.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-161">Copy and paste hello C# sample code into your Program.cs file, and remove all references toohello blob storage.</span></span>
8. <span data-ttu-id="a3d3b-162">Actualizar el valor de Hola de hello *apiKey* variable con clave Hola API que guardó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-162">Update hello value of hello *apiKey* variable with hello API key saved earlier.</span></span>
9. <span data-ttu-id="a3d3b-163">Busque Hola declaración y actualización Hola valores de solicitud de parámetros de servicio Web que se pasan toohello *importar datos* y *exportar datos* módulos.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-163">Locate hello request declaration and update hello values of Web Service Parameters that are passed toohello *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="a3d3b-164">En este caso, utilice la consulta original de hello, pero define un nuevo nombre de tabla.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-164">In this case, you use hello original query, but define a new table name.</span></span>
   
        var request = new BatchExecutionRequest() 
        {           
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable2" },
            }
        };
10. <span data-ttu-id="a3d3b-165">Ejecute la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-165">Run hello application.</span></span> 

<span data-ttu-id="a3d3b-166">En la realización de hello ejecutar, se agrega una nueva tabla toohello base de datos que contiene los resultados de puntuación de Hola.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-166">On completion of hello run, a new table is added toohello database containing hello scoring results.</span></span>

### <a name="deploy-a-new-web-service"></a><span data-ttu-id="a3d3b-167">Implementación de servicios web nuevos</span><span class="sxs-lookup"><span data-stu-id="a3d3b-167">Deploy a New Web Service</span></span>

> [!NOTE] 
> <span data-ttu-id="a3d3b-168">toodeploy un nuevo servicio web debe tener permisos suficientes en hello suscripción toowhich que implementar el servicio web de Hola.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-168">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="a3d3b-169">Para obtener más información, consulte [administrar un servicio Web mediante el portal de servicios Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="a3d3b-169">For more information, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="a3d3b-170">toodeploy como un nuevo servicio Web y crear una aplicación tooconsume:</span><span class="sxs-lookup"><span data-stu-id="a3d3b-170">toodeploy as a New Web Service and create an application tooconsume it:</span></span>

1. <span data-ttu-id="a3d3b-171">En la parte inferior de hello del lienzo del experimento de hello, haga clic en **ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-171">At hello bottom of hello experiment canvas, click **Run**.</span></span>
2. <span data-ttu-id="a3d3b-172">Cuando haya finalizado Hola ejecutar, haga clic en **implementar el servicio de Web** y seleccione **implementar [New] servicio Web**.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-172">When hello run has completed, click **Deploy Web Service** and select **Deploy Web Service [New]**.</span></span>
3. <span data-ttu-id="a3d3b-173">En página de experimento implementar hello, escriba un nombre para el servicio web y seleccione un plan de precios y, a continuación, haga clic en **implementar**.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-173">On hello Deploy Experiment page, enter a name for your web service, and select a pricing plan, then click **Deploy**.</span></span>
4. <span data-ttu-id="a3d3b-174">En hello **inicio rápido** página, haga clic en **usar**.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-174">On hello **Quickstart** page, click **Consume**.</span></span>
5. <span data-ttu-id="a3d3b-175">Hola **código de ejemplo** sección, haga clic en **por lotes**.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-175">In hello **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="a3d3b-176">Cree una nueva aplicación de consola de C# en Visual Studio: **Nuevo** > **Proyecto** > **Visual C#** > **Escritorio clásico de Windows** > **Aplicación de consola (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-176">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
7. <span data-ttu-id="a3d3b-177">Copie y pegue el código de ejemplo de Hola C# en el archivo Program.cs.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-177">Copy and paste hello C# sample code into your Program.cs file.</span></span>
8. <span data-ttu-id="a3d3b-178">Actualizar el valor de Hola de hello *apiKey* variable con hello **Primary Key** ubicado en hello **información básica de consumo** sección.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-178">Update hello value of hello *apiKey* variable with hello **Primary Key** located in hello **Basic consumption info** section.</span></span>
9. <span data-ttu-id="a3d3b-179">Busque hello *scoreRequest* declaración y actualizar valores de hello de parámetros de servicio Web que se pasan toohello *importar datos* y *exportar datos* módulos.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-179">Locate hello *scoreRequest* declaration and update hello values of Web Service Parameters that are passed toohello *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="a3d3b-180">En este caso, utilice la consulta original de hello, pero define un nuevo nombre de tabla.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-180">In this case, you use hello original query, but define a new table name.</span></span>
   
        var scoreRequest = new
        {       
            Inputs = new Dictionary<string, StringTable>()
            {
            },
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable3" },
            }
        };
10. <span data-ttu-id="a3d3b-181">Ejecute la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-181">Run hello application.</span></span> 

