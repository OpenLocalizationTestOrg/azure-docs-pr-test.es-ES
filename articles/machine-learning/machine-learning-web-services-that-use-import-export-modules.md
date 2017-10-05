---
title: "Uso de importación y exportación de datos en servicios web Azure Machine Learning | Microsoft Docs"
description: "Aprenda a usar los módulos de importación y exportación de datos para enviar y recibir datos de un servicio web."
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
ms.openlocfilehash: 123c8c2b1c5bae268b2a61c185743f2c3920175e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="deploying-azure-ml-web-services-that-use-data-import-and-data-export-modules"></a><span data-ttu-id="32c5e-103">Implementación de servicios web del aprendizaje automático de Azure que usan módulos de importación y exportación de datos</span><span class="sxs-lookup"><span data-stu-id="32c5e-103">Deploying Azure ML web services that use Data Import and Data Export modules</span></span>

<span data-ttu-id="32c5e-104">Cuando se crea un experimento predictivo, normalmente se agregan una entrada y una salida de servicio web.</span><span class="sxs-lookup"><span data-stu-id="32c5e-104">When you create a predictive experiment, you typically add a web service input and output.</span></span> <span data-ttu-id="32c5e-105">Al implementar el experimento, los consumidores pueden enviar y recibir datos desde el servicio web a través de las entradas y salidas.</span><span class="sxs-lookup"><span data-stu-id="32c5e-105">When you deploy the experiment, consumers can send and receive data from the web service through the inputs and outputs.</span></span> <span data-ttu-id="32c5e-106">En algunas aplicaciones, los datos del consumidor pueden estar disponibles desde una fuente de datos o ya residir en un origen de datos externo, como el Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="32c5e-106">For some applications, a consumer's data may be available from a data feed or already reside in an external data source such as Azure Blob storage.</span></span> <span data-ttu-id="32c5e-107">En estos casos, no se requiere que lean y escriban datos mediante entradas y salidas del servicio web.</span><span class="sxs-lookup"><span data-stu-id="32c5e-107">In these cases, they do not need read and write data using web service inputs and outputs.</span></span> <span data-ttu-id="32c5e-108">En su lugar, pueden utilizar el servicio de ejecución por lotes (BES) para leer los datos del origen de datos mediante un módulo de importación de datos y escribir los resultados de puntuación en una ubicación de datos diferente mediante un módulo de exportación de datos.</span><span class="sxs-lookup"><span data-stu-id="32c5e-108">They can, instead, use the Batch Execution Service (BES) to read data from the data source using an Import Data module and write the scoring results to a different data location using an Export Data module.</span></span>

<span data-ttu-id="32c5e-109">Los módulos de importación y exportación de datos pueden realizar operaciones de lectura y escritura en diversas ubicaciones de datos, como una dirección URL web a través de HTTP, una consulta de Hive, una base de datos de Azure SQL, Azure Table Storage, Azure Blob Storage, un proveedor de fuentes de distribución de datos o una base de datos SQL local.</span><span class="sxs-lookup"><span data-stu-id="32c5e-109">The Import Data and Export data modules, can read from and write to various data locations such as a Web URL via HTTP, a Hive Query, an Azure SQL database, Azure Table storage, Azure Blob storage, a Data Feed provide, or an on-premises SQL database.</span></span>

<span data-ttu-id="32c5e-110">En este tema se usa la muestra "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" (Muestra 5: Entrenar, probar, evaluar para clasificación binaria: Conjunto de datos para adultos) y presupone que el conjunto de datos ya se ha cargado en una tabla de SQL de Azure denominada censusdata.</span><span class="sxs-lookup"><span data-stu-id="32c5e-110">This topic uses the "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample and assumes the dataset has already been loaded into an Azure SQL table named censusdata.</span></span>

## <a name="create-the-training-experiment"></a><span data-ttu-id="32c5e-111">Creación del experimento de entrenamiento</span><span class="sxs-lookup"><span data-stu-id="32c5e-111">Create the training experiment</span></span>
<span data-ttu-id="32c5e-112">Al abrir la muestra "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" (Muestra 5: Entrenar, probar, evaluar para clasificación binaria: Conjunto de datos para adultos), se usa el conjunto de datos de clasificación binaria de ingresos en el censo adultos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="32c5e-112">When you open the "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" sample it uses the sample Adult Census Income Binary Classification dataset.</span></span> <span data-ttu-id="32c5e-113">Asimismo, el experimento en el lienzo tendrá una apariencia similar a la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="32c5e-113">And the experiment in the canvas will look similar to the following image:</span></span>

![Configuración inicial del experimento.](./media/machine-learning-web-services-that-use-import-export-modules/initial-look-of-experiment.png)

<span data-ttu-id="32c5e-115">Para leer los datos de la tabla de SQL de Azure:</span><span class="sxs-lookup"><span data-stu-id="32c5e-115">To read the data from the Azure SQL table:</span></span>

1. <span data-ttu-id="32c5e-116">Elimine el módulo del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="32c5e-116">Delete the dataset module.</span></span>
2. <span data-ttu-id="32c5e-117">En el cuadro de búsqueda de componentes, escriba import.</span><span class="sxs-lookup"><span data-stu-id="32c5e-117">In the components search box, type import.</span></span>
3. <span data-ttu-id="32c5e-118">En la lista de resultados, agregue un módulo *Importar datos* al lienzo del experimento.</span><span class="sxs-lookup"><span data-stu-id="32c5e-118">From the results list, add an *Import Data* module to the experiment canvas.</span></span>
4. <span data-ttu-id="32c5e-119">Conecte la salida del módulo *Import Data* (Importar datos) a la entrada del módulo *Clean Missing Data* (Limpiar datos que faltan).</span><span class="sxs-lookup"><span data-stu-id="32c5e-119">Connect output of the *Import Data* module the input of the *Clean Missing Data* module.</span></span>
5. <span data-ttu-id="32c5e-120">En el panel de propiedades, seleccione **Base de datos SQL de Azure** in the **Origen de datos** .</span><span class="sxs-lookup"><span data-stu-id="32c5e-120">In properties pane, select **Azure SQL Database** in the **Data Source** dropdown.</span></span>
6. <span data-ttu-id="32c5e-121">En los campos **Nombre del servidor de base de datos**, **Nombre de base de datos**, **Nombre de usuario** y **Contraseña**, escriba la información apropiada para la base de datos.</span><span class="sxs-lookup"><span data-stu-id="32c5e-121">In the **Database server name**, **Database name**, **User name**, and **Password** fields, enter the appropriate information for your database.</span></span>
7. <span data-ttu-id="32c5e-122">En el campo Consulta de base de datos, escriba la siguiente consulta.</span><span class="sxs-lookup"><span data-stu-id="32c5e-122">In the Database query field, enter the following query.</span></span>
   
     <span data-ttu-id="32c5e-123">select [age],</span><span class="sxs-lookup"><span data-stu-id="32c5e-123">select [age],</span></span>
   
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
     <span data-ttu-id="32c5e-124">from dbo.censusdata;</span><span class="sxs-lookup"><span data-stu-id="32c5e-124">from dbo.censusdata;</span></span>
8. <span data-ttu-id="32c5e-125">En la parte inferior del lienzo del experimento, haga clic en **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="32c5e-125">At the bottom of the experiment canvas, click **Run**.</span></span>

## <a name="create-the-predictive-experiment"></a><span data-ttu-id="32c5e-126">Creación del experimento predictivo</span><span class="sxs-lookup"><span data-stu-id="32c5e-126">Create the predictive experiment</span></span>
<span data-ttu-id="32c5e-127">A continuación, configure el experimento predictivo desde el que se implementa el servicio web.</span><span class="sxs-lookup"><span data-stu-id="32c5e-127">Next you set up the predictive experiment from which you deploy your web service.</span></span>

1. <span data-ttu-id="32c5e-128">En la parte inferior del lienzo del experimento, haga clic en **Set Up Web Service** (Configurar servicio web) y seleccione **Predictive Web Service [Recommended]** (Servicio web predictivo [recomendado]).</span><span class="sxs-lookup"><span data-stu-id="32c5e-128">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Predictive Web Service [Recommended]**.</span></span>
2. <span data-ttu-id="32c5e-129">Quite los módulos *Web Service Input* (Entrada del servicio web) y *Web Service Output* (Salida del servicio web) del experimento predictivo.</span><span class="sxs-lookup"><span data-stu-id="32c5e-129">Remove the *Web Service Input* and *Web Service Output modules* from the predictive experiment.</span></span> 
3. <span data-ttu-id="32c5e-130">En el cuadro de búsqueda de componentes, escriba export.</span><span class="sxs-lookup"><span data-stu-id="32c5e-130">In the components search box, type export.</span></span>
4. <span data-ttu-id="32c5e-131">En la lista de resultados, agregue un módulo *Exportar datos* al lienzo del experimento.</span><span class="sxs-lookup"><span data-stu-id="32c5e-131">From the results list, add an *Export Data* module to the experiment canvas.</span></span>
5. <span data-ttu-id="32c5e-132">Conecte la salida del módulo *Score Model* (Puntuar modelo) a la entrada del módulo *Export Data* (Exportar datos).</span><span class="sxs-lookup"><span data-stu-id="32c5e-132">Connect output of the *Score Model* module the input of the *Export Data* module.</span></span> 
6. <span data-ttu-id="32c5e-133">En el panel de propiedades, seleccione **Base de datos SQL de Azure** en el menú desplegable Origen de datos.</span><span class="sxs-lookup"><span data-stu-id="32c5e-133">In properties pane, select **Azure SQL Database** in the data destination dropdown.</span></span>
7. <span data-ttu-id="32c5e-134">En los campos **Nombre del servidor de base de datos**, **Nombre de base de datos**, **Server user account name** (Nombre de la cuenta de usuario del servidor) y **Server user account password** (Contraseña de la cuenta de usuario del servidor) escriba la información apropiada para la base de datos.</span><span class="sxs-lookup"><span data-stu-id="32c5e-134">In the **Database server name**, **Database name**, **Server user account name**, and **Server user account password** fields, enter the appropriate information for your database.</span></span>
8. <span data-ttu-id="32c5e-135">En el campo **Comma separated list of columns to be saved** (Lista de elementos separados por comas de las columnas que guardar) escriba Scored Labels.</span><span class="sxs-lookup"><span data-stu-id="32c5e-135">In the **Comma separated list of columns to be saved** field, type Scored Labels.</span></span>
9. <span data-ttu-id="32c5e-136">En el campo **Data table name**(Nombre de tabla de datos), escriba dbo.ScoredLabels.</span><span class="sxs-lookup"><span data-stu-id="32c5e-136">In the **Data table name field**, type dbo.ScoredLabels.</span></span> <span data-ttu-id="32c5e-137">Si la tabla no existe, se crea cuando se ejecuta el experimento o se llama al servicio web.</span><span class="sxs-lookup"><span data-stu-id="32c5e-137">If the table does not exist, it is created when the experiment is run or the web service is called.</span></span>
10. <span data-ttu-id="32c5e-138">En el campo **Comma separated list of datatable columns** (Lista de elementos separados por comas de las columnas de tablas de datos) escriba ScoredLabels.</span><span class="sxs-lookup"><span data-stu-id="32c5e-138">In the **Comma separated list of datatable columns** field, type ScoredLabels.</span></span>

<span data-ttu-id="32c5e-139">Cuando se escribe una aplicación que llama al servicio web final, puede especificar una consulta de entrada diferente u otra tabla de destino en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="32c5e-139">When you write an application that calls the final web service, you may want to specify a different input query or destination table at run time.</span></span> <span data-ttu-id="32c5e-140">Para configurar estas entradas y salidas, utilice la característica de parámetros del servicio web para establecer la propiedad *Origen de datos* del módulo *Importar datos* y la propiedad de destino de datos del módulo *Exportar datos*.</span><span class="sxs-lookup"><span data-stu-id="32c5e-140">To configure these inputs and outputs, use the Web Service Parameters feature to set the *Import Data* module *Data source* property and the *Export Data* mode data destination property.</span></span>  <span data-ttu-id="32c5e-141">Para obtener más información sobre los parámetros del servicio Web, consulte la entrada [AzureML Web Service Parameters](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) (Parámetros del servicio web AzureML) en Cortana Intelligence and Machine Learning Blog (blog de aprendizaje automático e inteligencia de Cortana).</span><span class="sxs-lookup"><span data-stu-id="32c5e-141">For more information on Web Service Parameters, see the [AzureML Web Service Parameters entry](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) on the Cortana Intelligence and Machine Learning Blog.</span></span>

<span data-ttu-id="32c5e-142">Para configurar los parámetros del servicio web para la consulta de importación y la tabla de destino:</span><span class="sxs-lookup"><span data-stu-id="32c5e-142">To configure the Web Service Parameters for the import query and the destination table:</span></span>

1. <span data-ttu-id="32c5e-143">En el panel de propiedades del módulo *Import Data* (Importar datos), haga clic en el icono situado en la parte superior derecha del campo **Consulta de base de datos** y seleccione **Set as web service parameter** (Establecer como parámetro de servicio web).</span><span class="sxs-lookup"><span data-stu-id="32c5e-143">In the properties pane for the *Import Data* module, click the icon at the top right of the **Database query** field and select **Set as web service parameter**.</span></span>
2. <span data-ttu-id="32c5e-144">En el panel de propiedades del módulo *Export Data* (Exportar datos), haga clic en el icono situado en la parte superior derecha del campo **Nombre de la tabla de datos** y seleccione **Set as web service parameter** (Establecer como parámetro de servicio web).</span><span class="sxs-lookup"><span data-stu-id="32c5e-144">In the properties pane for the *Export Data* module, click the icon at the top right of the **Data table name** field and select **Set as web service parameter**.</span></span>
3. <span data-ttu-id="32c5e-145">En la parte inferior del panel de propiedades del módulo *Exportar datos* , en la sección **Parámetros del servicio web** , haga clic en Consulta de base de datos y cambie el nombre por Query.</span><span class="sxs-lookup"><span data-stu-id="32c5e-145">At the bottom of the *Export Data* module properties pane, in the **Web Service Parameters** section, click Database query and rename it Query.</span></span>
4. <span data-ttu-id="32c5e-146">Haga clic en **Nombre de la tabla de datos** y cambie el nombre por **Table**.</span><span class="sxs-lookup"><span data-stu-id="32c5e-146">Click **Data table name** and rename it **Table**.</span></span>

<span data-ttu-id="32c5e-147">Cuando haya terminado, el experimento debería tener un aspecto similar a la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="32c5e-147">When you are done, your experiment should look similar to the following image:</span></span>

![Aspecto final del experimento.](./media/machine-learning-web-services-that-use-import-export-modules/experiment-with-import-data-added.png)

<span data-ttu-id="32c5e-149">Ahora puede implementar el experimento predictivo como servicio web.</span><span class="sxs-lookup"><span data-stu-id="32c5e-149">Now you can deploy the experiment as a web service.</span></span>

## <a name="deploy-the-web-service"></a><span data-ttu-id="32c5e-150">Implementación del servicio web</span><span class="sxs-lookup"><span data-stu-id="32c5e-150">Deploy the web service</span></span>
<span data-ttu-id="32c5e-151">Puede realizar la implementación en un servicio web clásico o nuevo.</span><span class="sxs-lookup"><span data-stu-id="32c5e-151">You can deploy to either a Classic or New web service.</span></span>

### <a name="deploy-a-classic-web-service"></a><span data-ttu-id="32c5e-152">Implementación de un servicio web clásico</span><span class="sxs-lookup"><span data-stu-id="32c5e-152">Deploy a Classic Web Service</span></span>
<span data-ttu-id="32c5e-153">Para realizar la implementación como un servicio web clásico y crear una aplicación para usarla:</span><span class="sxs-lookup"><span data-stu-id="32c5e-153">To deploy as a Classic Web Service and create an application to consume it:</span></span>

1. <span data-ttu-id="32c5e-154">En la parte inferior del lienzo del experimento, haga clic en Ejecutar.</span><span class="sxs-lookup"><span data-stu-id="32c5e-154">At the bottom of the experiment canvas, click Run.</span></span>
2. <span data-ttu-id="32c5e-155">Cuando la ejecución haya terminado, haga clic en **Deploy Web Service** (Implementar servicio web) y seleccione **Deploy Web Service [Classic]** (Implementar servicio web [clásico]).</span><span class="sxs-lookup"><span data-stu-id="32c5e-155">When the run has completed, click **Deploy Web Service** and select **Deploy Web Service [Classic]**.</span></span>
3. <span data-ttu-id="32c5e-156">En el panel del servicio web, busque la clave de API.</span><span class="sxs-lookup"><span data-stu-id="32c5e-156">On the web service dashboard, locate your API key.</span></span> <span data-ttu-id="32c5e-157">Copie y guárdela para usarla más adelante.</span><span class="sxs-lookup"><span data-stu-id="32c5e-157">Copy and save it to use later.</span></span>
4. <span data-ttu-id="32c5e-158">En la tabla **Default Endpoint** (Punto de conexión predeterminado), haga clic en el vínculo **Ejecución de lotes** para abrir la página de Ayuda de API.</span><span class="sxs-lookup"><span data-stu-id="32c5e-158">In the **Default Endpoint** table, click the **Batch Execution** link to open the API Help Page.</span></span>
5. <span data-ttu-id="32c5e-159">Cree una nueva aplicación de consola de C# en Visual Studio: **Nuevo** > **Proyecto** > **Visual C#** > **Escritorio clásico de Windows** > **Aplicación de consola (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="32c5e-159">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
6. <span data-ttu-id="32c5e-160">En la página de Ayuda de API, busque la sección **Sample Code** (Ejemplo de código) en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="32c5e-160">On the API Help Page, find the **Sample Code** section at the bottom of the page.</span></span>
7. <span data-ttu-id="32c5e-161">Copie y pegue el ejemplo de código de C# en el archivo Program.cs y quite todas las referencias al Almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="32c5e-161">Copy and paste the C# sample code into your Program.cs file, and remove all references to the blob storage.</span></span>
8. <span data-ttu-id="32c5e-162">Actualice el valor de la variable *apiKey* con la clave de API guardada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="32c5e-162">Update the value of the *apiKey* variable with the API key saved earlier.</span></span>
9. <span data-ttu-id="32c5e-163">Busque la declaración de solicitud y actualice los valores de los parámetros del servicio web que se pasan a los módulos *Import Data* (Importar datos) y *Export Data* (Exportar datos).</span><span class="sxs-lookup"><span data-stu-id="32c5e-163">Locate the request declaration and update the values of Web Service Parameters that are passed to the *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="32c5e-164">En este caso, utilice la consulta original, pero defina un nuevo nombre de tabla.</span><span class="sxs-lookup"><span data-stu-id="32c5e-164">In this case, you use the original query, but define a new table name.</span></span>
   
        var request = new BatchExecutionRequest() 
        {           
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable2" },
            }
        };
10. <span data-ttu-id="32c5e-165">Ejecute la aplicación.</span><span class="sxs-lookup"><span data-stu-id="32c5e-165">Run the application.</span></span> 

<span data-ttu-id="32c5e-166">Al término de la ejecución, se agrega una nueva tabla a la base de datos que contiene los resultados de puntuación.</span><span class="sxs-lookup"><span data-stu-id="32c5e-166">On completion of the run, a new table is added to the database containing the scoring results.</span></span>

### <a name="deploy-a-new-web-service"></a><span data-ttu-id="32c5e-167">Implementación de servicios web nuevos</span><span class="sxs-lookup"><span data-stu-id="32c5e-167">Deploy a New Web Service</span></span>

> [!NOTE] 
> <span data-ttu-id="32c5e-168">Para implementar un nuevo servicio web, debe tener permisos suficientes en la suscripción en la que lo implementa.</span><span class="sxs-lookup"><span data-stu-id="32c5e-168">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="32c5e-169">Para obtener más información, consulte [Administración de un servicio web mediante el portal Servicios web Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="32c5e-169">For more information, see [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="32c5e-170">Para realizar la implementación como un servicio web nuevo y crear una aplicación para usarla:</span><span class="sxs-lookup"><span data-stu-id="32c5e-170">To deploy as a New Web Service and create an application to consume it:</span></span>

1. <span data-ttu-id="32c5e-171">En la parte inferior del lienzo del experimento, haga clic en **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="32c5e-171">At the bottom of the experiment canvas, click **Run**.</span></span>
2. <span data-ttu-id="32c5e-172">Cuando la ejecución haya terminado, haga clic en **Deploy Web Service** (Implementar servicio web) y seleccione **Deploy Web Service [New]** (Implementar servicio web [nuevo]).</span><span class="sxs-lookup"><span data-stu-id="32c5e-172">When the run has completed, click **Deploy Web Service** and select **Deploy Web Service [New]**.</span></span>
3. <span data-ttu-id="32c5e-173">En la página Deploy Experiment (Implementar experimento), escriba un nombre para el servicio web, seleccione un plan de precios y haga clic en **Implementar**.</span><span class="sxs-lookup"><span data-stu-id="32c5e-173">On the Deploy Experiment page, enter a name for your web service, and select a pricing plan, then click **Deploy**.</span></span>
4. <span data-ttu-id="32c5e-174">En la página **Inicio rápido**, haga clic en **Consume** (Consumir).</span><span class="sxs-lookup"><span data-stu-id="32c5e-174">On the **Quickstart** page, click **Consume**.</span></span>
5. <span data-ttu-id="32c5e-175">En la sección **Sample Code** (Ejemplo de código), haga clic en **Lote**.</span><span class="sxs-lookup"><span data-stu-id="32c5e-175">In the **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="32c5e-176">Cree una nueva aplicación de consola de C# en Visual Studio: **Nuevo** > **Proyecto** > **Visual C#** > **Escritorio clásico de Windows** > **Aplicación de consola (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="32c5e-176">In Visual Studio, create a C# console application: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
7. <span data-ttu-id="32c5e-177">Copie y pegue el ejemplo de código de C# en el archivo Program.cs.</span><span class="sxs-lookup"><span data-stu-id="32c5e-177">Copy and paste the C# sample code into your Program.cs file.</span></span>
8. <span data-ttu-id="32c5e-178">Actualice el valor de la variable *apiKey* con la **clave principal** ubicada en la sección **Basic consumption info** (Información básica de consumo).</span><span class="sxs-lookup"><span data-stu-id="32c5e-178">Update the value of the *apiKey* variable with the **Primary Key** located in the **Basic consumption info** section.</span></span>
9. <span data-ttu-id="32c5e-179">Busque la declaración *scoreRequest* y actualice los valores de los parámetros del servicio web que se pasan a los módulos *Import Data* (Importar datos) y *Export Data* (Exportar datos).</span><span class="sxs-lookup"><span data-stu-id="32c5e-179">Locate the *scoreRequest* declaration and update the values of Web Service Parameters that are passed to the *Import Data* and *Export Data* modules.</span></span> <span data-ttu-id="32c5e-180">En este caso, utilice la consulta original, pero defina un nuevo nombre de tabla.</span><span class="sxs-lookup"><span data-stu-id="32c5e-180">In this case, you use the original query, but define a new table name.</span></span>
   
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
10. <span data-ttu-id="32c5e-181">Ejecute la aplicación.</span><span class="sxs-lookup"><span data-stu-id="32c5e-181">Run the application.</span></span> 

