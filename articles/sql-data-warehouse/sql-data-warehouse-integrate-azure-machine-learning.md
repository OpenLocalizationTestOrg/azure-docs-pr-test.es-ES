---
title: "Aprendizaje automático de Azure con el almacenamiento de datos de SQL aaaUse | Documentos de Microsoft"
description: "Tutorial para usar Aprendizaje automático de Azure con Almacenamiento de datos SQL de Azure para el desarrollo de soluciones."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: barbkess
editor: 
ms.assetid: ac6bc731-6add-47a9-b3fe-68996e656f4d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: fdfe8c936d2bb7a02163a0bbf6435e1ebd518d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a><span data-ttu-id="d9d0d-103">Uso de Aprendizaje automático de Azure con Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="d9d0d-103">Use Azure Machine Learning with SQL Data Warehouse</span></span>
<span data-ttu-id="d9d0d-104">Aprendizaje automático de Azure es un servicio de análisis predictivos completamente administrado que puede usar modelos de predicción toocreate con sus datos en el almacén de datos de SQL y, a continuación, publicar como servicios web listos para su consumo.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-104">Azure Machine Learning is a fully managed predictive analytics service that you can use toocreate predictive models against your data in SQL Data Warehouse, and then publish as ready-to-consume web services.</span></span> <span data-ttu-id="d9d0d-105">Puede aprender aspectos básicos de Hola de análisis predictivo y aprendizaje automático leyendo [tooMachine de introducción de aprendizaje en Azure][Introduction tooMachine Learning on Azure].</span><span class="sxs-lookup"><span data-stu-id="d9d0d-105">You can learn hello basics of predictive analytics and machine learning by reading [Introduction tooMachine Learning on Azure][Introduction tooMachine Learning on Azure].</span></span>  <span data-ttu-id="d9d0d-106">Puede obtener información sobre cómo entrenar toocreate, puntuarlos y probar un modelo de aprendizaje automático con hello [crear experimento tutorial][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="d9d0d-106">You can then learn how toocreate, train, score and test a machine learning model using hello [Create experiment tutorial][Create experiment tutorial].</span></span>

<span data-ttu-id="d9d0d-107">En este artículo, aprenderá cómo hello toodo sigue utilizando hello [estudio de aprendizaje automático de Azure][Azure Machine Learning Studio]:</span><span class="sxs-lookup"><span data-stu-id="d9d0d-107">In this article, you will learn how toodo hello following using hello [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span></span>

* <span data-ttu-id="d9d0d-108">Leer datos de la base de datos toocreate, entrenar y puntuar un modelo de predicción</span><span class="sxs-lookup"><span data-stu-id="d9d0d-108">Read data from your database toocreate, train and score a predictive model</span></span>
* <span data-ttu-id="d9d0d-109">Escribir la base de datos de tooyour de datos</span><span class="sxs-lookup"><span data-stu-id="d9d0d-109">Write data tooyour database</span></span>

## <a name="read-data-from-sql-data-warehouse"></a><span data-ttu-id="d9d0d-110">Lectura de datos desde Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="d9d0d-110">Read data from SQL Data Warehouse</span></span>
<span data-ttu-id="d9d0d-111">Se debe leer datos de la tabla Product en la base de datos de hello AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-111">We will read data from Product table in hello AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="d9d0d-112">Paso 1</span><span class="sxs-lookup"><span data-stu-id="d9d0d-112">Step 1</span></span>
<span data-ttu-id="d9d0d-113">Inicie un experimento de nuevo haciendo clic en + nuevo final Hola de hello ventana de estudio de aprendizaje automático, seleccione EXPERIMENTO y, a continuación, seleccione experimentar en blanco.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-113">Start a new experiment by clicking +NEW at hello bottom of hello Machine Learning Studio window, select EXPERIMENT, and then select Blank Experiment.</span></span> <span data-ttu-id="d9d0d-114">Predeterminado de hello seleccione experimentar nombre en parte superior de hello del lienzo de Hola y cambie su nombre toosomething significativo, por ejemplo, predicción de precio de bicicleta.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-114">Select hello default experiment name at hello top of hello canvas and rename it toosomething meaningful, for example, Bicycle price prediction.</span></span>

### <a name="step-2"></a><span data-ttu-id="d9d0d-115">Paso 2</span><span class="sxs-lookup"><span data-stu-id="d9d0d-115">Step 2</span></span>
<span data-ttu-id="d9d0d-116">Busque el módulo de lector de hello en la paleta de Hola de conjuntos de datos y los módulos de izquierda Hola del lienzo del experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-116">Look for hello Reader module in hello palette of datasets and modules on hello left of hello experiment canvas.</span></span> <span data-ttu-id="d9d0d-117">Arrastre el lienzo del experimento de hello módulo toohello.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-117">Drag hello module toohello experiment canvas.</span></span>
![][drag_reader]

### <a name="step-3"></a><span data-ttu-id="d9d0d-118">Paso 3</span><span class="sxs-lookup"><span data-stu-id="d9d0d-118">Step 3</span></span>
<span data-ttu-id="d9d0d-119">Seleccionar módulo de lector de Hola y rellenar el panel de propiedades de Hola.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-119">Select hello Reader module and fill out hello properties pane.</span></span>

1. <span data-ttu-id="d9d0d-120">Seleccione la base de datos de SQL Azure como Hola origen de datos.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-120">Select Azure SQL Database as hello Data Source.</span></span>
2. <span data-ttu-id="d9d0d-121">Nombre del servidor de base de datos: nombre del servidor de tipo hello.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-121">Database server name: Type hello server name.</span></span> <span data-ttu-id="d9d0d-122">Puede usar hello [portal de Azure] [ Azure portal] toofind esto.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-122">You can use hello [Azure portal][Azure portal] toofind this.</span></span>

![][server_name]

1. <span data-ttu-id="d9d0d-123">Nombre de base de datos: nombre de una base de datos que acaba de especificar el servidor de Hola Hola de tipo.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-123">Database name: Type hello name of a database on hello server you just specified.</span></span>
2. <span data-ttu-id="d9d0d-124">Nombre de cuenta de usuario de servidor: escriba el nombre de usuario de Hola de una cuenta que tenga permisos de acceso de la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-124">Server user account name:  Type hello user name of an account that has access permissions for hello database.</span></span>
3. <span data-ttu-id="d9d0d-125">Contraseña de cuenta de usuario de servidor: proporcionar contraseña Hola Hola cuenta de usuario especificada.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-125">Server user account password: Provide hello password for hello specified user account.</span></span>
4. <span data-ttu-id="d9d0d-126">Aceptar cualquier certificado de servidor: Utilice esta opción (menos segura) si desea tooskip revisar certificado de sitio de hello antes de leer los datos.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-126">Accept any server certificate: Use this option (less secure) if you want tooskip reviewing hello site certificate before you read your data.</span></span>
5. <span data-ttu-id="d9d0d-127">Consulta de base de datos: escriba una instrucción SQL que describe datos de Hola que desee tooread.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-127">Database query: Enter a SQL statement that describes hello data you want tooread.</span></span> <span data-ttu-id="d9d0d-128">En este caso, se debe leer datos de tabla Product mediante Hola después de consulta.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-128">In this case, we will read data from Product table using hello following query.</span></span>

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a><span data-ttu-id="d9d0d-129">Paso 4</span><span class="sxs-lookup"><span data-stu-id="d9d0d-129">Step 4</span></span>
1. <span data-ttu-id="d9d0d-130">Ejecute el experimento de hello haciendo clic en ejecutar en el lienzo del experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-130">Run hello experiment by clicking Run under hello experiment canvas.</span></span>
2. <span data-ttu-id="d9d0d-131">Cuando finaliza el experimento de hello, módulo de lector de hello tendrá un tooindicate de marca de verificación verde que se ha completado correctamente.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-131">When hello experiment finishes, hello Reader module will have a green check mark tooindicate that it has completed successfully.</span></span> <span data-ttu-id="d9d0d-132">Tenga en cuenta también Hola ha terminado de estado de ejecución en la esquina superior derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-132">Notice also hello Finished running status in hello upper-right corner.</span></span>

![][run]

1. <span data-ttu-id="d9d0d-133">toosee Hola datos importados, haga clic en el puerto de salida de hello en parte inferior de hello del conjunto de datos de automóviles de Hola y seleccione visualizar.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-133">toosee hello imported data, click hello output port at hello bottom of hello automobile dataset and select Visualize.</span></span>

## <a name="create-train-and-score-a-model"></a><span data-ttu-id="d9d0d-134">Creación, entrenamiento y puntuación de un modelo</span><span class="sxs-lookup"><span data-stu-id="d9d0d-134">Create, train and score a model</span></span>
<span data-ttu-id="d9d0d-135">Ahora puede utilizar este conjunto de datos para:</span><span class="sxs-lookup"><span data-stu-id="d9d0d-135">Now you can use this dataset to:</span></span>

* <span data-ttu-id="d9d0d-136">Crear un modelo: procesar datos y definir características</span><span class="sxs-lookup"><span data-stu-id="d9d0d-136">Create a Model: Process data and define features</span></span>
* <span data-ttu-id="d9d0d-137">Entrenar el modelo de hello: elegir y aplicar un algoritmo de aprendizaje</span><span class="sxs-lookup"><span data-stu-id="d9d0d-137">Train hello model: Choose and apply a learning algorithm</span></span>
* <span data-ttu-id="d9d0d-138">Puntuación y prueba Hola modelo: predecir nuevo precio de bicicleta</span><span class="sxs-lookup"><span data-stu-id="d9d0d-138">Score and test hello model: Predict new bicycle price</span></span>

![][model]

<span data-ttu-id="d9d0d-139">más información acerca de cómo toocreate, entrenar, puntuarlos y probar un Hola de uso del modelo de aprendizaje automático de toolearn [crear experimento tutorial][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="d9d0d-139">toolearn more about how toocreate, train, score and test a machine learning model use hello [Create experiment tutorial][Create experiment tutorial].</span></span>

## <a name="write-data-tooazure-sql-data-warehouse"></a><span data-ttu-id="d9d0d-140">Escribir datos tooAzure almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="d9d0d-140">Write data tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="d9d0d-141">Tabla de tooProductPriceForecast de conjunto de resultados de Hola se escribirán en la base de datos de hello AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-141">We will write hello result set tooProductPriceForecast table in hello AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="d9d0d-142">Paso 1</span><span class="sxs-lookup"><span data-stu-id="d9d0d-142">Step 1</span></span>
<span data-ttu-id="d9d0d-143">Busque el módulo de escritor de hello en la paleta de Hola de conjuntos de datos y los módulos izquierda Hola del lienzo del experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-143">Look for hello Writer module in hello palette of datasets and modules on hello left of hello experiment canvas.</span></span> <span data-ttu-id="d9d0d-144">Arrastre el lienzo del experimento de hello módulo toohello.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-144">Drag hello module toohello experiment canvas.</span></span>

![][drag_writer]

### <a name="step-2"></a><span data-ttu-id="d9d0d-145">Paso 2</span><span class="sxs-lookup"><span data-stu-id="d9d0d-145">Step 2</span></span>
<span data-ttu-id="d9d0d-146">Seleccionar módulo de escritor de Hola y rellenar el panel de propiedades de Hola.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-146">Select hello Writer module and fill out hello properties pane.</span></span>

1. <span data-ttu-id="d9d0d-147">Seleccionar base de datos de SQL Azure como Hola destino de datos.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-147">Select Azure SQL Database as hello Data Destination.</span></span>
2. <span data-ttu-id="d9d0d-148">Nombre del servidor de base de datos: nombre del servidor de tipo hello.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-148">Database server name: Type hello server name.</span></span> <span data-ttu-id="d9d0d-149">Puede usar hello [portal de Azure] [ Azure portal] toofind esto.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-149">You can use hello [Azure portal][Azure portal] toofind this.</span></span>
3. <span data-ttu-id="d9d0d-150">Nombre de base de datos: nombre de una base de datos que acaba de especificar el servidor de Hola Hola de tipo.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-150">Database name: Type hello name of a database on hello server you just specified.</span></span>
4. <span data-ttu-id="d9d0d-151">Nombre de cuenta de usuario de servidor: escriba el nombre de usuario de Hola de una cuenta que tenga permisos de escritura para la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-151">Server user account name:  Type hello user name of an account that has write permissions for hello database.</span></span>
5. <span data-ttu-id="d9d0d-152">Contraseña de cuenta de usuario de servidor: proporcionar contraseña Hola Hola cuenta de usuario especificada.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-152">Server user account password: Provide hello password for hello specified user account.</span></span>
6. <span data-ttu-id="d9d0d-153">Aceptar cualquier certificado de servidor (no seguro): seleccione esta opción si no desea certificado de hello tooview.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-153">Accept any server certificate (insecure): Select this option if you don’t want tooview hello certificate.</span></span>
7. <span data-ttu-id="d9d0d-154">Lista separada por comas de toobe columnas guardado: proporcione una lista de columnas de conjunto de datos o el resultado de hello que desea toooutput.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-154">Comma-separated list of columns toobe saved: Provide a list of hello dataset or result columns that you want toooutput.</span></span>
8. <span data-ttu-id="d9d0d-155">Nombre de la tabla de datos: especifique Hola nombre de tabla de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-155">Data table name: Specify hello name of hello data table.</span></span>
9. <span data-ttu-id="d9d0d-156">Lista separada por comas de las columnas de la datatable: especificar toouse de nombres de columna de hello en nueva tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-156">Comma-separated list of datatable columns:  Specify hello column names toouse in hello new table.</span></span> <span data-ttu-id="d9d0d-157">Hello nombres de columna pueden ser diferentes de Hola que en el conjunto de datos de origen de hello, pero debe incluir Hola el mismo número de columnas aquí que se define para la tabla de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-157">hello column names can be different from hello ones in hello source dataset, but you must list hello same number of columns here that you define for hello output table.</span></span>
10. <span data-ttu-id="d9d0d-158">Número de filas escritas por cada operación de SQL Azure: puede configurar Hola número de filas que se escriben tooa base de datos SQL en una sola operación.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-158">Number of rows written per SQL Azure operation: You can configure hello number of rows that are written tooa SQL database in one operation.</span></span>

![][writer_properties]

### <a name="step-3"></a><span data-ttu-id="d9d0d-159">Paso 3</span><span class="sxs-lookup"><span data-stu-id="d9d0d-159">Step 3</span></span>
1. <span data-ttu-id="d9d0d-160">Ejecute el experimento de hello haciendo clic en ejecutar en el lienzo del experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-160">Run hello experiment by clicking Run under hello experiment canvas.</span></span>
2. <span data-ttu-id="d9d0d-161">Cuando finaliza el experimento de hello, todos los módulos tendrá un tooindicate de marca de verificación verde que completó correctamente.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-161">When hello experiment finishes, all modules will have a green check mark tooindicate that they completed successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9d0d-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d9d0d-162">Next steps</span></span>
<span data-ttu-id="d9d0d-163">Para obtener más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo de Almacenamiento de datos SQL][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="d9d0d-163">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[drag_reader]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-reader.png
[server_name]: ./media/sql-data-warehouse-integrate-azure-machine-learning/dw-server-name.png
[reader_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-reader-properties.png
[run]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-finished-running.png
[model]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-create-train-score-model.png
[drag_writer]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-writer.png
[writer_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-writer-properties.png

<!--Article references-->

[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Create experiment tutorial]: https://azure.microsoft.com/documentation/articles/machine-learning-create-experiment/
[Introduction toomachine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/
