---
title: Uso de Azure Machine Learning con SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: c19860c6b5b1c15d1e29ddc67f9cf9ad4618725b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a><span data-ttu-id="b7fb1-103">Uso de Aprendizaje automático de Azure con Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="b7fb1-103">Use Azure Machine Learning with SQL Data Warehouse</span></span>
<span data-ttu-id="b7fb1-104">Aprendizaje automático de Azure es un servicio de análisis predictivo completamente administrado que puede usar para crear modelos predictivos con sus datos en Almacenamiento de datos SQL y publicarlos después como servicios web listos para su consumo.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-104">Azure Machine Learning is a fully managed predictive analytics service that you can use to create predictive models against your data in SQL Data Warehouse, and then publish as ready-to-consume web services.</span></span> <span data-ttu-id="b7fb1-105">Para aprender los conceptos básicos del análisis predictivo y el aprendizaje automático, lea [Introducción a Machine Learning en Azure][Introduction to Machine Learning on Azure].</span><span class="sxs-lookup"><span data-stu-id="b7fb1-105">You can learn the basics of predictive analytics and machine learning by reading [Introduction to Machine Learning on Azure][Introduction to Machine Learning on Azure].</span></span>  <span data-ttu-id="b7fb1-106">Puede aprender a crear, entrenar, puntuar y probar un modelo de aprendizaje automático con el [Tutorial para crear un experimento][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="b7fb1-106">You can then learn how to create, train, score and test a machine learning model using the [Create experiment tutorial][Create experiment tutorial].</span></span>

<span data-ttu-id="b7fb1-107">En este artículo, aprenderá cómo hacer lo siguiente utilizando [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span><span class="sxs-lookup"><span data-stu-id="b7fb1-107">In this article, you will learn how to do the following using the [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span></span>

* <span data-ttu-id="b7fb1-108">Leer datos de la base de datos para crear, entrenar y puntuar un modelo predictivo</span><span class="sxs-lookup"><span data-stu-id="b7fb1-108">Read data from your database to create, train and score a predictive model</span></span>
* <span data-ttu-id="b7fb1-109">Escribir datos en la base de datos</span><span class="sxs-lookup"><span data-stu-id="b7fb1-109">Write data to your database</span></span>

## <a name="read-data-from-sql-data-warehouse"></a><span data-ttu-id="b7fb1-110">Lectura de datos desde Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="b7fb1-110">Read data from SQL Data Warehouse</span></span>
<span data-ttu-id="b7fb1-111">Leeremos datos desde la tabla Producto en la base de datos AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-111">We will read data from Product table in the AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="b7fb1-112">Paso 1</span><span class="sxs-lookup"><span data-stu-id="b7fb1-112">Step 1</span></span>
<span data-ttu-id="b7fb1-113">Inicie un experimento nuevo haciendo clic en +NUEVO en la parte inferior de la ventana de Estudio de aprendizaje automático, seleccione EXPERIMENTO y luego Experimento en blanco.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-113">Start a new experiment by clicking +NEW at the bottom of the Machine Learning Studio window, select EXPERIMENT, and then select Blank Experiment.</span></span> <span data-ttu-id="b7fb1-114">Seleccione el nombre del experimento predeterminado en la parte superior del lienzo y cámbielo por uno significativo, por ejemplo, Predicción del precio de bicicletas.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-114">Select the default experiment name at the top of the canvas and rename it to something meaningful, for example, Bicycle price prediction.</span></span>

### <a name="step-2"></a><span data-ttu-id="b7fb1-115">Paso 2</span><span class="sxs-lookup"><span data-stu-id="b7fb1-115">Step 2</span></span>
<span data-ttu-id="b7fb1-116">Busque el módulo Lector en la paleta de conjuntos de datos y módulos que aparece a la izquierda del lienzo de experimentos.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-116">Look for the Reader module in the palette of datasets and modules on the left of the experiment canvas.</span></span> <span data-ttu-id="b7fb1-117">Arrastre el módulo al lienzo de experimentos.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-117">Drag the module to the experiment canvas.</span></span>
![][drag_reader]

### <a name="step-3"></a><span data-ttu-id="b7fb1-118">Paso 3</span><span class="sxs-lookup"><span data-stu-id="b7fb1-118">Step 3</span></span>
<span data-ttu-id="b7fb1-119">Seleccione el módulo Lector y rellene el panel de propiedades.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-119">Select the Reader module and fill out the properties pane.</span></span>

1. <span data-ttu-id="b7fb1-120">Seleccione Base de datos SQL de Azure como el origen de datos.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-120">Select Azure SQL Database as the Data Source.</span></span>
2. <span data-ttu-id="b7fb1-121">Nombre del servidor de base de datos: escriba el nombre del servidor.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-121">Database server name: Type the server name.</span></span> <span data-ttu-id="b7fb1-122">Para encontrarlo, puede usar [Azure Portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="b7fb1-122">You can use the [Azure portal][Azure portal] to find this.</span></span>

![][server_name]

1. <span data-ttu-id="b7fb1-123">Nombre de la base de datos: escriba el nombre de la base de datos en el servidor que acaba de especificar.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-123">Database name: Type the name of a database on the server you just specified.</span></span>
2. <span data-ttu-id="b7fb1-124">Nombre de la cuenta de usuario del servidor: escriba el nombre de usuario de una cuenta con permisos de acceso a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-124">Server user account name:  Type the user name of an account that has access permissions for the database.</span></span>
3. <span data-ttu-id="b7fb1-125">Contraseña de la cuenta de usuario de servidor: proporcione la contraseña de la cuenta de usuario especificada.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-125">Server user account password: Provide the password for the specified user account.</span></span>
4. <span data-ttu-id="b7fb1-126">Aceptar cualquier certificado de servidor: use esta opción (menos segura) si desea omitir la revisión del certificado de sitio antes de leer los datos.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-126">Accept any server certificate: Use this option (less secure) if you want to skip reviewing the site certificate before you read your data.</span></span>
5. <span data-ttu-id="b7fb1-127">Consulta de base de datos: escriba una instrucción SQL que describa los datos que desea leer.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-127">Database query: Enter a SQL statement that describes the data you want to read.</span></span> <span data-ttu-id="b7fb1-128">En este caso, leeremos datos desde la tabla Producto con la siguiente consulta.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-128">In this case, we will read data from Product table using the following query.</span></span>

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a><span data-ttu-id="b7fb1-129">Paso 4</span><span class="sxs-lookup"><span data-stu-id="b7fb1-129">Step 4</span></span>
1. <span data-ttu-id="b7fb1-130">Ejecute el experimento; para ello, haga clic en Ejecutar bajo el lienzo de experimentos.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-130">Run the experiment by clicking Run under the experiment canvas.</span></span>
2. <span data-ttu-id="b7fb1-131">Cuando el experimento finalice, el módulo Lector tendrá una marca de verificación verde para indicar que se completó correctamente.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-131">When the experiment finishes, the Reader module will have a green check mark to indicate that it has completed successfully.</span></span> <span data-ttu-id="b7fb1-132">Observe también el estado Ejecución finalizada en la esquina superior derecha.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-132">Notice also the Finished running status in the upper-right corner.</span></span>

![][run]

1. <span data-ttu-id="b7fb1-133">Para ver los datos importados, haga clic en el puerto de salida en la parte inferior del conjunto de datos de automóvil y seleccione Visualizar.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-133">To see the imported data, click the output port at the bottom of the automobile dataset and select Visualize.</span></span>

## <a name="create-train-and-score-a-model"></a><span data-ttu-id="b7fb1-134">Creación, entrenamiento y puntuación de un modelo</span><span class="sxs-lookup"><span data-stu-id="b7fb1-134">Create, train and score a model</span></span>
<span data-ttu-id="b7fb1-135">Ahora puede utilizar este conjunto de datos para:</span><span class="sxs-lookup"><span data-stu-id="b7fb1-135">Now you can use this dataset to:</span></span>

* <span data-ttu-id="b7fb1-136">Crear un modelo: procesar datos y definir características</span><span class="sxs-lookup"><span data-stu-id="b7fb1-136">Create a Model: Process data and define features</span></span>
* <span data-ttu-id="b7fb1-137">Entrenar el modelo: elegir y aplicar un algoritmo de aprendizaje</span><span class="sxs-lookup"><span data-stu-id="b7fb1-137">Train the model: Choose and apply a learning algorithm</span></span>
* <span data-ttu-id="b7fb1-138">Puntuar y probar el modelo: predecir el nuevo precio de bicicleta</span><span class="sxs-lookup"><span data-stu-id="b7fb1-138">Score and test the model: Predict new bicycle price</span></span>

![][model]

<span data-ttu-id="b7fb1-139">Puede aprender a crear, entrenar, puntuar y probar un modelo de aprendizaje automático con el [Tutorial para crear un experimento][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="b7fb1-139">To learn more about how to create, train, score and test a machine learning model use the [Create experiment tutorial][Create experiment tutorial].</span></span>

## <a name="write-data-to-azure-sql-data-warehouse"></a><span data-ttu-id="b7fb1-140">Escritura de datos en Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="b7fb1-140">Write data to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="b7fb1-141">Escribiremos el conjunto de resultados en la tabla ProductPriceForecast de la base de datos AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-141">We will write the result set to ProductPriceForecast table in the AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="b7fb1-142">Paso 1</span><span class="sxs-lookup"><span data-stu-id="b7fb1-142">Step 1</span></span>
<span data-ttu-id="b7fb1-143">Busque el módulo Redactor en la paleta de conjuntos de datos y módulos que aparece a la izquierda del lienzo de experimentos.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-143">Look for the Writer module in the palette of datasets and modules on the left of the experiment canvas.</span></span> <span data-ttu-id="b7fb1-144">Arrastre el módulo al lienzo de experimentos.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-144">Drag the module to the experiment canvas.</span></span>

![][drag_writer]

### <a name="step-2"></a><span data-ttu-id="b7fb1-145">Paso 2</span><span class="sxs-lookup"><span data-stu-id="b7fb1-145">Step 2</span></span>
<span data-ttu-id="b7fb1-146">Seleccione el módulo Redactor y rellene el panel de propiedades.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-146">Select the Writer module and fill out the properties pane.</span></span>

1. <span data-ttu-id="b7fb1-147">Seleccione Base de datos SQL de Azure como el destino de los datos.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-147">Select Azure SQL Database as the Data Destination.</span></span>
2. <span data-ttu-id="b7fb1-148">Nombre del servidor de base de datos: escriba el nombre del servidor.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-148">Database server name: Type the server name.</span></span> <span data-ttu-id="b7fb1-149">Para encontrarlo, puede usar [Azure Portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="b7fb1-149">You can use the [Azure portal][Azure portal] to find this.</span></span>
3. <span data-ttu-id="b7fb1-150">Nombre de la base de datos: escriba el nombre de la base de datos en el servidor que acaba de especificar.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-150">Database name: Type the name of a database on the server you just specified.</span></span>
4. <span data-ttu-id="b7fb1-151">Nombre de la cuenta de usuario del servidor: escriba el nombre de usuario de una cuenta con permisos de escritura para la base de datos.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-151">Server user account name:  Type the user name of an account that has write permissions for the database.</span></span>
5. <span data-ttu-id="b7fb1-152">Contraseña de la cuenta de usuario de servidor: proporcione la contraseña de la cuenta de usuario especificada.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-152">Server user account password: Provide the password for the specified user account.</span></span>
6. <span data-ttu-id="b7fb1-153">Aceptar cualquier certificado de servidor (no seguro): seleccione esta opción si no desea ver el certificado.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-153">Accept any server certificate (insecure): Select this option if you don’t want to view the certificate.</span></span>
7. <span data-ttu-id="b7fb1-154">Lista separada por comas de las columnas que se guardarán: proporcione una lista de las columnas de resultados o conjuntos de datos que desea obtener.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-154">Comma-separated list of columns to be saved: Provide a list of the dataset or result columns that you want to output.</span></span>
8. <span data-ttu-id="b7fb1-155">Nombre de la tabla de datos: especifique el nombre de la tabla de datos.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-155">Data table name: Specify the name of the data table.</span></span>
9. <span data-ttu-id="b7fb1-156">Lista separada por comas de las columnas de la tabla de datos: especifique los nombres de las columnas que se usarán en la tabla nueva.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-156">Comma-separated list of datatable columns:  Specify the column names to use in the new table.</span></span> <span data-ttu-id="b7fb1-157">Los nombres de las columnas pueden ser distintos a los nombres del conjunto de datos de origen, pero debe aquí debe indicar el mismo número de columnas que define en la tabla de salida.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-157">The column names can be different from the ones in the source dataset, but you must list the same number of columns here that you define for the output table.</span></span>
10. <span data-ttu-id="b7fb1-158">Número de filas escritas por operación de SQL Azure: puede configurar el número de filas que se escriben en una base de datos SQL en una operación.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-158">Number of rows written per SQL Azure operation: You can configure the number of rows that are written to a SQL database in one operation.</span></span>

![][writer_properties]

### <a name="step-3"></a><span data-ttu-id="b7fb1-159">Paso 3</span><span class="sxs-lookup"><span data-stu-id="b7fb1-159">Step 3</span></span>
1. <span data-ttu-id="b7fb1-160">Ejecute el experimento; para ello, haga clic en Ejecutar bajo el lienzo de experimentos.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-160">Run the experiment by clicking Run under the experiment canvas.</span></span>
2. <span data-ttu-id="b7fb1-161">Cuando el experimento finalice, todos los módulos tendrán una marca de verificación verde para indicar que se han implementado correctamente.</span><span class="sxs-lookup"><span data-stu-id="b7fb1-161">When the experiment finishes, all modules will have a green check mark to indicate that they completed successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7fb1-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b7fb1-162">Next steps</span></span>
<span data-ttu-id="b7fb1-163">Para obtener más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo de Almacenamiento de datos SQL][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="b7fb1-163">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
[Introduction to machine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/
