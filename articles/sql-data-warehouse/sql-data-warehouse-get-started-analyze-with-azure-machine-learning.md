---
title: "datos de aaaAnalyze con aprendizaje automático de Azure | Documentos de Microsoft"
description: "Usar aprendizaje toobuild un modelo basado en datos almacenados en el almacén de datos de SQL Azure de aprendizaje de automático predictivo."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 95635460-150f-4a50-be9c-5ddc5797f8a9
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 03/02/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 337a2cd77aaad4467683827c56e5015b262b2554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-with-azure-machine-learning"></a><span data-ttu-id="5b9e9-103">Análisis de datos con Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="5b9e9-103">Analyze data with Azure Machine Learning</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5b9e9-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="5b9e9-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="5b9e9-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5b9e9-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="5b9e9-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5b9e9-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="5b9e9-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="5b9e9-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="5b9e9-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="5b9e9-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="5b9e9-109">Este tutorial usa aprendizaje toobuild un modelo basado en datos almacenados en el almacén de datos de SQL Azure de aprendizaje de automático predictivo.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-109">This tutorial uses Azure Machine Learning toobuild a predictive machine learning model based on data stored in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="5b9e9-110">En concreto, esto crea una campaña de marketing de Adventure Works, tienda de bicicletas de hello, predecir si un cliente es toobuy probablemente una bicicleta o no.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-110">Specifically, this builds a targeted marketing campaign for Adventure Works, hello bike shop, by predicting if a customer is likely toobuy a bike or not.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="5b9e9-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5b9e9-111">Prerequisites</span></span>
<span data-ttu-id="5b9e9-112">toostep a través de este tutorial, necesitará:</span><span class="sxs-lookup"><span data-stu-id="5b9e9-112">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="5b9e9-113">Una instancia de Almacenamiento de datos SQL con la base de datos de ejemplo AdventureWorksDW previamente cargada.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-113">A SQL Data Warehouse pre-loaded with AdventureWorksDW sample data.</span></span> <span data-ttu-id="5b9e9-114">tooprovision, vea [crear un almacén de datos de SQL] [ Create a SQL Data Warehouse] y elegir los datos de ejemplo de Hola tooload.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-114">tooprovision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose tooload hello sample data.</span></span> <span data-ttu-id="5b9e9-115">Si ya tiene un almacenamiento de datos pero no tiene datos de ejemplo, puede [cargar manualmente los datos de ejemplo][load sample data manually].</span><span class="sxs-lookup"><span data-stu-id="5b9e9-115">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-get-hello-data"></a><span data-ttu-id="5b9e9-116">1. Obtener datos de Hola</span><span class="sxs-lookup"><span data-stu-id="5b9e9-116">1. Get hello data</span></span>
<span data-ttu-id="5b9e9-117">datos de Hello están en la vista de dbo.vTargetMail de hello en la base de datos de hello AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-117">hello data is in hello dbo.vTargetMail view in hello AdventureWorksDW database.</span></span> <span data-ttu-id="5b9e9-118">tooread estos datos:</span><span class="sxs-lookup"><span data-stu-id="5b9e9-118">tooread this data:</span></span>

1. <span data-ttu-id="5b9e9-119">Inicie sesión en [Azure Machine Learning Studio][Azure Machine Learning studio] y haga clic en mis experimentos.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-119">Sign into [Azure Machine Learning studio][Azure Machine Learning studio] and click on my experiments.</span></span>
2. <span data-ttu-id="5b9e9-120">Haga clic en **+NUEVO** y seleccione **Experimento en blanco**.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-120">Click **+NEW** and select **Blank Experiment**.</span></span>
3. <span data-ttu-id="5b9e9-121">Escriba un nombre para el experimento: Targeted Marketing.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-121">Enter a name for your experiment: Targeted Marketing.</span></span>
4. <span data-ttu-id="5b9e9-122">Hola arrastre **lector** módulo desde el panel módulos de hello en el lienzo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-122">Drag hello **Reader** module from hello modules pane into hello canvas.</span></span>
5. <span data-ttu-id="5b9e9-123">Especifique los detalles de hello de la base de datos de almacenamiento de datos SQL en el panel de propiedades de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-123">Specify hello details of your SQL Data Warehouse database in hello Properties pane.</span></span>
6. <span data-ttu-id="5b9e9-124">Especifique la base de datos de hello **consulta** tooread datos de saludo de interés.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-124">Specify hello database **query** tooread hello data of interest.</span></span>

```sql
SELECT [CustomerKey]
  ,[GeographyKey]
  ,[CustomerAlternateKey]
  ,[MaritalStatus]
  ,[Gender]
  ,cast ([YearlyIncome] as int) as SalaryYear
  ,[TotalChildren]
  ,[NumberChildrenAtHome]
  ,[EnglishEducation]
  ,[EnglishOccupation]
  ,[HouseOwnerFlag]
  ,[NumberCarsOwned]
  ,[CommuteDistance]
  ,[Region]
  ,[Age]
  ,[BikeBuyer]
FROM [dbo].[vTargetMail]
```

<span data-ttu-id="5b9e9-125">Ejecute el experimento de hello haciendo clic en **ejecutar** en el lienzo del experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-125">Run hello experiment by clicking **Run** under hello experiment canvas.</span></span>
<span data-ttu-id="5b9e9-126">![Ejecute el experimento de Hola][1]</span><span class="sxs-lookup"><span data-stu-id="5b9e9-126">![Run hello experiment][1]</span></span>

<span data-ttu-id="5b9e9-127">Una vez experimento Hola termina de ejecutarse correctamente, haga clic en el puerto de salida de hello en parte inferior de Hola de módulo de lector de Hola y seleccione **visualizar** toosee Hola importó los datos.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-127">After hello experiment finishes running successfully, click hello output port at hello bottom of hello Reader module and select **Visualize** toosee hello imported data.</span></span>
<span data-ttu-id="5b9e9-128">![Ver los datos importados][3]</span><span class="sxs-lookup"><span data-stu-id="5b9e9-128">![View imported data][3]</span></span>

## <a name="2-clean-hello-data"></a><span data-ttu-id="5b9e9-129">2. Datos limpios Hola</span><span class="sxs-lookup"><span data-stu-id="5b9e9-129">2. Clean hello data</span></span>
<span data-ttu-id="5b9e9-130">datos de hello tooclean, quite algunas columnas que no son relevantes para el modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-130">tooclean hello data, drop some columns that are not relevant for hello model.</span></span> <span data-ttu-id="5b9e9-131">toodo esto:</span><span class="sxs-lookup"><span data-stu-id="5b9e9-131">toodo this:</span></span>

1. <span data-ttu-id="5b9e9-132">Hola arrastre **proyectar columnas** módulo en el lienzo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-132">Drag hello **Project Columns** module into hello canvas.</span></span>
2. <span data-ttu-id="5b9e9-133">Haga clic en **selector de columna de inicio** en toospecify de panel de propiedades de hello qué columnas desea toodrop.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-133">Click **Launch column selector** in hello Properties pane toospecify which columns you wish toodrop.</span></span>
   <span data-ttu-id="5b9e9-134">![Columnas del proyecto][4]</span><span class="sxs-lookup"><span data-stu-id="5b9e9-134">![Project Columns][4]</span></span>
3. <span data-ttu-id="5b9e9-135">Excluya dos columnas: CustomerAlternateKey y GeographyKey.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-135">Exclude two columns: CustomerAlternateKey and GeographyKey.</span></span>
   <span data-ttu-id="5b9e9-136">![Quitar las columnas innecesariass][5]</span><span class="sxs-lookup"><span data-stu-id="5b9e9-136">![Remove unnecessary columns][5]</span></span>

## <a name="3-build-hello-model"></a><span data-ttu-id="5b9e9-137">3. Generar modelo Hola</span><span class="sxs-lookup"><span data-stu-id="5b9e9-137">3. Build hello model</span></span>
<span data-ttu-id="5b9e9-138">Dividiremos Hola datos 80: 20: 80% tootrain un modelo de aprendizaje automático y 20% tootest Hola modelo.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-138">We will split hello data 80-20: 80% tootrain a machine learning model and 20% tootest hello model.</span></span> <span data-ttu-id="5b9e9-139">Se hará uso de algoritmos de "Dos clases" hello para este problema de clasificación binaria.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-139">We will make use of hello “Two-Class” algorithms for this binary classification problem.</span></span>

1. <span data-ttu-id="5b9e9-140">Hola arrastre **división** módulo en el lienzo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-140">Drag hello **Split** module into hello canvas.</span></span>
2. <span data-ttu-id="5b9e9-141">Escriba 0,8 de fracción de filas de hello primera salida dataset en el panel de propiedades de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-141">Enter 0.8 for Fraction of rows in hello first output dataset in hello Properties pane.</span></span>
   <span data-ttu-id="5b9e9-142">![Dividir los datos en conjunto de entrenamiento y prueba][6]</span><span class="sxs-lookup"><span data-stu-id="5b9e9-142">![Split data into training and test set][6]</span></span>
3. <span data-ttu-id="5b9e9-143">Hola arrastre **árbol de decisión impulsado de dos clases** módulo en el lienzo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-143">Drag hello **Two-Class Boosted Decision Tree** module into hello canvas.</span></span>
4. <span data-ttu-id="5b9e9-144">Hola arrastre **entrenar modelo** módulo a Hola lienzo y especificar las entradas de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-144">Drag hello **Train Model** module into hello canvas and specify hello inputs.</span></span> <span data-ttu-id="5b9e9-145">A continuación, haga clic en **selector de columna de inicio** en el panel de propiedades de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-145">Then, click **Launch column selector** in hello Properties pane.</span></span>
   * <span data-ttu-id="5b9e9-146">Primera entrada: el algoritmo de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-146">First input: ML algorithm.</span></span>
   * <span data-ttu-id="5b9e9-147">Segunda entrada: datos tootrain Hola algoritmo.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-147">Second input: Data tootrain hello algorithm on.</span></span>
     <span data-ttu-id="5b9e9-148">![Conectar el módulo entrenar modelo de Hola][7]</span><span class="sxs-lookup"><span data-stu-id="5b9e9-148">![Connect hello Train Model module][7]</span></span>
5. <span data-ttu-id="5b9e9-149">Seleccione hello **BikeBuyer** columna Hola toopredict de columna.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-149">Select hello **BikeBuyer** column as hello column toopredict.</span></span>
   <span data-ttu-id="5b9e9-150">![Seleccionar columna toopredict][8]</span><span class="sxs-lookup"><span data-stu-id="5b9e9-150">![Select Column toopredict][8]</span></span>

## <a name="4-score-hello-model"></a><span data-ttu-id="5b9e9-151">4. Modelo de Hola de puntuación</span><span class="sxs-lookup"><span data-stu-id="5b9e9-151">4. Score hello model</span></span>
<span data-ttu-id="5b9e9-152">Ahora, se probará cómo se comporta el modelo de hello en datos de prueba.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-152">Now, we will test how hello model performs on test data.</span></span> <span data-ttu-id="5b9e9-153">Se comparará el algoritmo de Hola de nuestra opción con un toosee algoritmo diferente que funciona mejor.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-153">We will compare hello algorithm of our choice with a different algorithm toosee which performs better.</span></span>

1. <span data-ttu-id="5b9e9-154">Arrastre **puntuar modelo** módulo en el lienzo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-154">Drag **Score Model** module into hello canvas.</span></span>
    <span data-ttu-id="5b9e9-155">Primera entrada: entrenar modelo segunda entrada: datos de prueba ![modelo Hola de puntuación][9]</span><span class="sxs-lookup"><span data-stu-id="5b9e9-155">First input: Trained model Second input: Test data ![Score hello model][9]</span></span>
2. <span data-ttu-id="5b9e9-156">Hola arrastre **máquina del punto de Bayes de dos clases** en el lienzo del experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-156">Drag hello **Two-Class Bayes Point Machine** into hello experiment canvas.</span></span> <span data-ttu-id="5b9e9-157">Compararemos cómo realiza este algoritmo de comparación toohello árbol de decisión impulsado de dos clases.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-157">We will compare how this algorithm performs in comparison toohello Two-Class Boosted Decision Tree.</span></span>
3. <span data-ttu-id="5b9e9-158">Copiar y pegar Hola módulos entrenar modelo y el modelo de puntuación de hello del lienzo.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-158">Copy and Paste hello modules Train Model and Score Model in hello canvas.</span></span>
4. <span data-ttu-id="5b9e9-159">Hola arrastre **evaluar modelo** módulo en algoritmos de hello lienzo toocompare Hola dos.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-159">Drag hello **Evaluate Model** module into hello canvas toocompare hello two algorithms.</span></span>
5. <span data-ttu-id="5b9e9-160">**Ejecutar** Hola experimento.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-160">**Run** hello experiment.</span></span>
   <span data-ttu-id="5b9e9-161">![Ejecute el experimento de Hola][10]</span><span class="sxs-lookup"><span data-stu-id="5b9e9-161">![Run hello experiment][10]</span></span>
6. <span data-ttu-id="5b9e9-162">Haga clic en el puerto de salida de hello en parte inferior de Hola de módulo de evaluar modelo hello y haga clic en visualizar.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-162">Click hello output port at hello bottom of hello Evaluate Model module and click Visualize.</span></span>
   <span data-ttu-id="5b9e9-163">![Visualizar los resultados de evaluación][11]</span><span class="sxs-lookup"><span data-stu-id="5b9e9-163">![Visualize evaluation results][11]</span></span>

<span data-ttu-id="5b9e9-164">métricas de Hello proporcionadas son curva ROC hello, diagrama de retirada de precisión y curva de elevación.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-164">hello metrics provided are hello ROC curve, precision-recall diagram and lift curve.</span></span> <span data-ttu-id="5b9e9-165">Examinar estas métricas, podemos ver ese modelo primera Hola funcionaba mejor de Hola a otra.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-165">Looking at these metrics, we can see that hello first model performed better than hello second one.</span></span> <span data-ttu-id="5b9e9-166">toolook en hello qué Hola primer modelo predicha, haga clic en el puerto de salida de hello puntuar modelo y haga clic en visualizar.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-166">toolook at hello what hello first model predicted, click on output port of hello Score Model and click Visualize.</span></span>
<span data-ttu-id="5b9e9-167">![Visualizar los resultados de puntuación][12]</span><span class="sxs-lookup"><span data-stu-id="5b9e9-167">![Visualize score results][12]</span></span>

<span data-ttu-id="5b9e9-168">Verá que dos columnas más agregan conjunto de datos de prueba de tooyour.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-168">You will see two more columns added tooyour test dataset.</span></span>

* <span data-ttu-id="5b9e9-169">Probabilidades con puntuación: probabilidad de Hola que es un cliente compre una bicicleta.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-169">Scored Probabilities: hello likelihood that a customer is a bike buyer.</span></span>
* <span data-ttu-id="5b9e9-170">Etiquetas con puntuación: Hola clasificación realizado modelo hello: bicicleta (1) o no (0).</span><span class="sxs-lookup"><span data-stu-id="5b9e9-170">Scored Labels: hello classification done by hello model – bike buyer (1) or not (0).</span></span> <span data-ttu-id="5b9e9-171">Este umbral de probabilidad para etiquetar se establece too50% y se puede ajustar.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-171">This probability threshold for labeling is set too50% and can be adjusted.</span></span>

<span data-ttu-id="5b9e9-172">Comparando Hola columna BikeBuyer (real) con las etiquetas con puntuación de hello (predicción), puede ver la medida ha realizado el modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-172">Comparing hello column BikeBuyer (actual) with hello Scored Labels (prediction), you can see how well hello model has performed.</span></span> <span data-ttu-id="5b9e9-173">Como los pasos siguientes, puede usar este predicciones de toomake de modelo para los nuevos clientes y publicar este modelo como un servicio web o escribir resultados atrás tooSQL almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="5b9e9-173">As next steps, you can use this model toomake predictions for new customers and publish this model as a web service or write results back tooSQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b9e9-174">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5b9e9-174">Next steps</span></span>
<span data-ttu-id="5b9e9-175">toolearn más información acerca de crear modelos de aprendizaje de automático predictivo consulte demasiado[tooMachine de introducción de aprendizaje en Azure][Introduction tooMachine Learning on Azure].</span><span class="sxs-lookup"><span data-stu-id="5b9e9-175">toolearn more about building predictive machine learning models, refer too[Introduction tooMachine Learning on Azure][Introduction tooMachine Learning on Azure].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img1_reader.png
[2]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img2_visualize.png
[3]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img3_readerdata.png
[4]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img4_projectcolumns.png
[5]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img5_columnselector.png
[6]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img6_split.png
[7]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img7_train.png
[8]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img8_traincolumnselector.png
[9]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img9_score.png
[10]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img10_evaluate.png
[11]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img11_evalresults.png
[12]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img12_scoreresults.png


<!--Article references-->
[Azure Machine Learning studio]:https://studio.azureml.net/
[Introduction tooMachine Learning on Azure]:https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
