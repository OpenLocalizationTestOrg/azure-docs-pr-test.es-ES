---
title: "Paso 3: Creación de un nuevo experimento de Machine Learning | Microsoft Docs"
description: "Paso 3 del programa Hola a desarrollar un solución de predicción Tutorial: crear un nuevo experimento de entrenamiento en estudio de aprendizaje automático de Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 660e3c27-55ef-4c33-a4e9-dff4d1224630
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 4697d461a205c50c8d2aa6a3bd56697840cb30f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a><span data-ttu-id="4b89a-103">Paso 3 del tutorial: Creación de un nuevo experimento de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="4b89a-103">Walkthrough Step 3: Create a new Azure Machine Learning experiment</span></span>
<span data-ttu-id="4b89a-104">Esto es Hola tercer paso del tutorial de hello, [desarrollar una solución de análisis predictivos en aprendizaje automático de Azure](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="4b89a-104">This is hello third step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="4b89a-105">Creación de un área de trabajo de Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="4b89a-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="4b89a-106">Carga de los datos existentes</span><span class="sxs-lookup"><span data-stu-id="4b89a-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. <span data-ttu-id="4b89a-107">**Crear un experimento nuevo**</span><span class="sxs-lookup"><span data-stu-id="4b89a-107">**Create a new experiment**</span></span>
4. [<span data-ttu-id="4b89a-108">Entrenar y evaluar modelos de Hola</span><span class="sxs-lookup"><span data-stu-id="4b89a-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="4b89a-109">Implementar el servicio Web de Hola</span><span class="sxs-lookup"><span data-stu-id="4b89a-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="4b89a-110">Acceder al servicio Web Hola</span><span class="sxs-lookup"><span data-stu-id="4b89a-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="4b89a-111">Hola siguiente paso en este tutorial es toocreate un experimento en estudio de aprendizaje automático que utiliza el conjunto de datos de Hola que se cargan.</span><span class="sxs-lookup"><span data-stu-id="4b89a-111">hello next step in this walkthrough is toocreate an experiment in Machine Learning Studio that uses hello dataset we uploaded.</span></span>  

1. <span data-ttu-id="4b89a-112">En Studio, haga clic en **+ nuevo** final Hola de ventana hello.</span><span class="sxs-lookup"><span data-stu-id="4b89a-112">In Studio, click **+NEW** at hello bottom of hello window.</span></span>
2. <span data-ttu-id="4b89a-113">Seleccione **EXPERIMENTO**y luego "Experimento en blanco".</span><span class="sxs-lookup"><span data-stu-id="4b89a-113">Select **EXPERIMENT**, and then select "Blank Experiment".</span></span> 

    ![Creación de un nuevo experimento][0]

2. <span data-ttu-id="4b89a-115">Predeterminado de hello seleccione experimentar nombre en parte superior de hello del lienzo de Hola y cambie su nombre toosomething significativo.</span><span class="sxs-lookup"><span data-stu-id="4b89a-115">Select hello default experiment name at hello top of hello canvas and rename it toosomething meaningful.</span></span>

    ![Renombrar el experimento][5]
   
   > [!TIP]
   > <span data-ttu-id="4b89a-117">Es una buena práctica toofill **resumen** y **descripción** para experimento Hola Hola **propiedades** panel.</span><span class="sxs-lookup"><span data-stu-id="4b89a-117">It's a good practice toofill in **Summary** and **Description** for hello experiment in hello **Properties** pane.</span></span> <span data-ttu-id="4b89a-118">Estos proporcionan propiedades Hola experimento de hello toodocument oportunidad para que cualquier persona que examina más adelante puedan comprender los objetivos y la metodología.</span><span class="sxs-lookup"><span data-stu-id="4b89a-118">These properties give you hello chance toodocument hello experiment so that anyone who looks at it later will understand your goals and methodology.</span></span>
   > 
   > ![Propiedades del experimento][6]
   > 
3. <span data-ttu-id="4b89a-120">En hello módulo paleta toohello izquierda del lienzo del experimento de hello expanda **conjuntos de datos guardados**.</span><span class="sxs-lookup"><span data-stu-id="4b89a-120">In hello module palette toohello left of hello experiment canvas, expand **Saved Datasets**.</span></span>
4. <span data-ttu-id="4b89a-121">Conjunto de datos de Hola de búsqueda que ha creado en **Mis conjuntos de datos** y lo arrastra al lienzo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b89a-121">Find hello dataset you created under **My Datasets** and drag it onto hello canvas.</span></span> <span data-ttu-id="4b89a-122">También puede encontrar el conjunto de datos de hello escribiendo el nombre de Hola Hola **búsqueda** cuadro situado encima de la paleta de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b89a-122">You can also find hello dataset by entering hello name in hello **Search** box above hello palette.</span></span>  

    ![Agregar toohello experimento de hello conjunto de datos][7]

## <a name="prepare-hello-data"></a><span data-ttu-id="4b89a-124">Preparar los datos de Hola</span><span class="sxs-lookup"><span data-stu-id="4b89a-124">Prepare hello data</span></span>
<span data-ttu-id="4b89a-125">Puede ver hello las 100 primeras filas de datos de Hola y determinados datos estadísticos para hello todo el conjunto de datos: haga clic en el puerto de salida de hello del conjunto de datos de hello (Hola pequeño círculo final Hola) y seleccione **visualizar**.</span><span class="sxs-lookup"><span data-stu-id="4b89a-125">You can view hello first 100 rows of hello data and some statistical information for hello whole dataset: Click hello output port of hello dataset (hello small circle at hello bottom) and select **Visualize**.</span></span>  

<span data-ttu-id="4b89a-126">Porque el archivo de datos de hello no incluye encabezados de columna, Studio ha proporcionado encabezados genéricos (Col1, Col2, *etc.*).</span><span class="sxs-lookup"><span data-stu-id="4b89a-126">Because hello data file didn't come with column headings, Studio has provided generic headings (Col1, Col2, *etc.*).</span></span> <span data-ttu-id="4b89a-127">Encabezados de buena no son esencial toocreating un modelo, pero hacen que sea más fácil toowork con datos de hello en el experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b89a-127">Good headings aren't essential toocreating a model, but they make it easier toowork with hello data in hello experiment.</span></span> <span data-ttu-id="4b89a-128">Además, cuando finalmente se publica este modelo en un servicio web, encabezados de hello ayudar a identificar Hola columnas toohello usuario del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b89a-128">Also, when we eventually publish this model in a web service, hello headings help identify hello columns toohello user of hello service.</span></span>  

<span data-ttu-id="4b89a-129">Podemos agregar encabezados de columna con hello [editar metadatos] [ edit-metadata] módulo.</span><span class="sxs-lookup"><span data-stu-id="4b89a-129">We can add column headings using hello [Edit Metadata][edit-metadata] module.</span></span>
<span data-ttu-id="4b89a-130">Usar hello [editar metadatos] [ edit-metadata] módulo toochange metadatos asociados a un conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="4b89a-130">You use hello [Edit Metadata][edit-metadata] module toochange metadata associated with a dataset.</span></span> <span data-ttu-id="4b89a-131">En este caso, usamos lo tooprovide nombres más descriptivos para los encabezados de columna.</span><span class="sxs-lookup"><span data-stu-id="4b89a-131">In this case, we use it tooprovide more friendly names for column headings.</span></span> 

<span data-ttu-id="4b89a-132">toouse [editar metadatos][edit-metadata], especifique primero qué toomodify columnas (en este caso, todas ellas.) A continuación, especificar Hola acción toobe realizada en esas columnas (en este caso, cambiar los encabezados de columna.)</span><span class="sxs-lookup"><span data-stu-id="4b89a-132">toouse [Edit Metadata][edit-metadata], you first specify which columns toomodify (in this case, all of them.) Next, you specify hello action toobe performed on those columns (in this case, changing column headings.)</span></span>

1. <span data-ttu-id="4b89a-133">En la paleta de módulo de hello, escriba "metadatos" Hola **búsqueda** cuadro.</span><span class="sxs-lookup"><span data-stu-id="4b89a-133">In hello module palette, type "metadata" in hello **Search** box.</span></span> <span data-ttu-id="4b89a-134">Hola [editar metadatos] [ edit-metadata] aparece en la lista de módulos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b89a-134">hello [Edit Metadata][edit-metadata] appears in hello module list.</span></span>

2. <span data-ttu-id="4b89a-135">Haga clic y arrastre hello [editar metadatos] [ edit-metadata] módulo en hello lienzo y colóquela debajo de conjunto de datos de Hola se agregó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4b89a-135">Click and drag hello [Edit Metadata][edit-metadata] module onto hello canvas and drop it below hello dataset we added earlier.</span></span>

3. <span data-ttu-id="4b89a-136">Conectar Hola dataset toohello [editar metadatos][edit-metadata]: haga clic en el puerto de salida de hello del conjunto de datos de hello (Hola pequeño círculo final Hola del conjunto de datos de hello), arrastre toohello el puerto de entrada de [editar metadatos ] [ edit-metadata] (Hola pequeño círculo en parte superior de hello del módulo de hello), a continuación, suelte el botón del mouse de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b89a-136">Connect hello dataset toohello [Edit Metadata][edit-metadata]: click hello output port of hello dataset (hello small circle at hello bottom of hello dataset), drag toohello input port of [Edit Metadata][edit-metadata] (hello small circle at hello top of hello module), then release hello mouse button.</span></span> <span data-ttu-id="4b89a-137">módulo y un conjunto de hello permanecen conectadas aun cuando que se recorre ya sea en el lienzo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b89a-137">hello dataset and module remain connected even if you move either around on hello canvas.</span></span>
   
   <span data-ttu-id="4b89a-138">el experimento de Hello ahora debería ser similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="4b89a-138">hello experiment should now look something like this:</span></span>  
   
   ![Agregar metadatos de edición][1]
   
   <span data-ttu-id="4b89a-140">marca de exclamación Hola rojo indica que no hemos configurado aún las propiedades de Hola para este módulo.</span><span class="sxs-lookup"><span data-stu-id="4b89a-140">hello red exclamation mark indicates that we haven't set hello properties for this module yet.</span></span> <span data-ttu-id="4b89a-141">Lo haremos a continuación.</span><span class="sxs-lookup"><span data-stu-id="4b89a-141">We'll do that next.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="4b89a-142">Puede agregar un módulo tooa comentario haciendo doble clic en módulo de Hola y de escritura de texto.</span><span class="sxs-lookup"><span data-stu-id="4b89a-142">You can add a comment tooa module by double-clicking hello module and entering text.</span></span> <span data-ttu-id="4b89a-143">Esto puede ayudarle a ver de un vistazo qué módulo Hola está haciendo en el experimento.</span><span class="sxs-lookup"><span data-stu-id="4b89a-143">This can help you see at a glance what hello module is doing in your experiment.</span></span> <span data-ttu-id="4b89a-144">En este caso, haga doble clic en hello [editar metadatos] [ edit-metadata] módulo y tipo hello comentario "Agregar encabezados de columna".</span><span class="sxs-lookup"><span data-stu-id="4b89a-144">In this case, double-click hello [Edit Metadata][edit-metadata] module and type hello comment "Add column headings".</span></span> <span data-ttu-id="4b89a-145">Haga clic en ningún otro lugar en cuadro de texto de hello lienzo tooclose Hola.</span><span class="sxs-lookup"><span data-stu-id="4b89a-145">Click anywhere else on hello canvas tooclose hello text box.</span></span> <span data-ttu-id="4b89a-146">toodisplay Hola comentario, haga clic en la flecha abajo de hello en el módulo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b89a-146">toodisplay hello comment, click hello down-arrow on hello module.</span></span>
   > 
   > ![Modificación del módulo de metadatos con el comentario agregado][8]
   > 
4. <span data-ttu-id="4b89a-148">Seleccione [editar metadatos][edit-metadata]y en hello **propiedades** toohello del panel derecho del lienzo de hello, haga clic en **selector de columna de inicio**.</span><span class="sxs-lookup"><span data-stu-id="4b89a-148">Select [Edit Metadata][edit-metadata], and in hello **Properties** pane toohello right of hello canvas, click **Launch column selector**.</span></span>

5. <span data-ttu-id="4b89a-149">Hola **seleccionar columnas** cuadro de diálogo, seleccione todas las filas de Hola **columnas disponibles** y haga clic en > toomove ellos demasiado**columnas seleccionadas**.</span><span class="sxs-lookup"><span data-stu-id="4b89a-149">In hello **Select columns** dialog, select all hello rows in **Available Columns** and click > toomove them too**Selected Columns**.</span></span>
   <span data-ttu-id="4b89a-150">cuadro de diálogo de Hello debería tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="4b89a-150">hello dialog should look like this:</span></span>

   ![Selector de columnas con todas las columnas seleccionadas][2]

6. <span data-ttu-id="4b89a-152">Haga clic en hello **Aceptar** marca de verificación.</span><span class="sxs-lookup"><span data-stu-id="4b89a-152">Click hello **OK** check mark.</span></span>

7. <span data-ttu-id="4b89a-153">Nuevo en hello **propiedades** panel, busque hello **nuevos nombres de columna** parámetro.</span><span class="sxs-lookup"><span data-stu-id="4b89a-153">Back in hello **Properties** pane, look for hello **New column names** parameter.</span></span> <span data-ttu-id="4b89a-154">En este campo, escriba una lista de nombres para hello 21 columnas de conjunto de datos de hello, separados por comas y en orden de las columnas.</span><span class="sxs-lookup"><span data-stu-id="4b89a-154">In this field, enter a list of names for hello 21 columns in hello dataset, separated by commas and in column order.</span></span> <span data-ttu-id="4b89a-155">Puede obtener los nombres de las columnas de Hola de documentación de conjunto de datos de hello en el sitio Web UCI hello, o para su comodidad puede copiar y pegar Hola lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="4b89a-155">You can obtain hello columns names from hello dataset documentation on hello UCI website, or for convenience you can copy and paste hello following list:</span></span>  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   <span data-ttu-id="4b89a-156">panel de propiedades de Hello tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="4b89a-156">hello Properties pane looks like this:</span></span>
   
   ![Propiedades de los metadatos de edición][3]

> [!TIP]
> <span data-ttu-id="4b89a-158">Si desea que los encabezados de columna de hello tooverify, ejecute el experimento de hello (haga clic en **ejecutar** por debajo del lienzo del experimento de hello).</span><span class="sxs-lookup"><span data-stu-id="4b89a-158">If you want tooverify hello column headings, run hello experiment (click **RUN** below hello experiment canvas).</span></span> <span data-ttu-id="4b89a-159">Cuando finaliza la ejecución (aparece una marca de verificación verde en [editar metadatos][edit-metadata]), haga clic en el puerto de salida de hello de hello [editar metadatos] [ edit-metadata] módulo y seleccione **visualizar**.</span><span class="sxs-lookup"><span data-stu-id="4b89a-159">When it finishes running (a green check mark appears on [Edit Metadata][edit-metadata]), click hello output port of hello [Edit Metadata][edit-metadata] module, and select **Visualize**.</span></span> <span data-ttu-id="4b89a-160">Puede ver la salida de hello de cualquier módulo Hola mismo progreso de hello tooview de forma de datos de Hola a través de experimento Hola.</span><span class="sxs-lookup"><span data-stu-id="4b89a-160">You can view hello output of any module in hello same way tooview hello progress of hello data through hello experiment.</span></span>
> 
> 

## <a name="create-training-and-test-datasets"></a><span data-ttu-id="4b89a-161">Creación de conjuntos de datos de entrenamiento y prueba</span><span class="sxs-lookup"><span data-stu-id="4b89a-161">Create training and test datasets</span></span>
<span data-ttu-id="4b89a-162">Necesitamos algunos modelos de datos tootrain hello y algunos tootest se.</span><span class="sxs-lookup"><span data-stu-id="4b89a-162">We need some data tootrain hello model and some tootest it.</span></span>
<span data-ttu-id="4b89a-163">Por lo que en el paso siguiente de hello del experimento de hello, dividiremos Hola conjunto de datos en dos conjuntos de datos independientes: uno para el entrenamiento de nuestro modelo y otro para probarlo.</span><span class="sxs-lookup"><span data-stu-id="4b89a-163">So in hello next step of hello experiment, we split hello dataset into two separate datasets: one for training our model and one for testing it.</span></span>

<span data-ttu-id="4b89a-164">toodo, usamos hello [dividir datos] [ split] módulo.</span><span class="sxs-lookup"><span data-stu-id="4b89a-164">toodo this, we use hello [Split Data][split] module.</span></span>  

1. <span data-ttu-id="4b89a-165">Buscar hello [dividir datos] [ split] módulo, arrástrelo al lienzo de Hola y conéctela toohello [editar metadatos] [ edit-metadata] módulo.</span><span class="sxs-lookup"><span data-stu-id="4b89a-165">Find hello [Split Data][split] module, drag it onto hello canvas, and connect it toohello [Edit Metadata][edit-metadata] module.</span></span>

2. <span data-ttu-id="4b89a-166">De forma predeterminada, relación de división de hello es 0,5 y hello **división aleatorio** parámetro está establecido.</span><span class="sxs-lookup"><span data-stu-id="4b89a-166">By default, hello split ratio is 0.5 and hello **Randomized split** parameter is set.</span></span> <span data-ttu-id="4b89a-167">Esto significa que una mitad aleatoria de datos de hello es la salida a través de un puerto de hello [dividir datos] [ split] mitad hello a otro y módulo.</span><span class="sxs-lookup"><span data-stu-id="4b89a-167">This means that a random half of hello data is output through one port of hello [Split Data][split] module, and half through hello other.</span></span> <span data-ttu-id="4b89a-168">Puede ajustar estos parámetros, así como Hola **valor de inicialización aleatorio** parámetro, hello toochange dividido entre los datos de pruebas y entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="4b89a-168">You can adjust these parameters, as well as hello **Random seed** parameter, toochange hello split between training and testing data.</span></span> <span data-ttu-id="4b89a-169">En este ejemplo, se deja tal cual.</span><span class="sxs-lookup"><span data-stu-id="4b89a-169">For this example, we leave them as-is.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="4b89a-170">Hola propiedad **fracción de filas de hello en primer lugar de conjunto de datos de salida** determina la cantidad de datos de hello salida a través de hello es *izquierdo* puerto de salida.</span><span class="sxs-lookup"><span data-stu-id="4b89a-170">hello property **Fraction of rows in hello first output dataset** determines how much of hello data is output through hello *left* output port.</span></span> <span data-ttu-id="4b89a-171">Por ejemplo, si establece too0.7 de proporción de hello, salida a través de hello dejado de puerto y 30% a través del puerto derecha hello es 70% de los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b89a-171">For instance, if you set hello ratio too0.7, then 70% of hello data is output through hello left port and 30% through hello right port.</span></span>  
   > 
   > 

3. <span data-ttu-id="4b89a-172">Haga doble clic en hello [dividir datos] [ split] módulo y escriba el comentario de hello, "datos de entrenamiento y prueba división 50%".</span><span class="sxs-lookup"><span data-stu-id="4b89a-172">Double-click hello [Split Data][split] module and enter hello comment, "Training/testing data split 50%".</span></span> 

<span data-ttu-id="4b89a-173">Podemos usar salidas Hola de hello [dividir datos] [ split] módulo sin embargo nos gusta, pero vamos a seleccionar toouse Hola izquierdo se muestran como datos de entrenamiento y Hola directamente los datos como pruebas de salida.</span><span class="sxs-lookup"><span data-stu-id="4b89a-173">We can use hello outputs of hello [Split Data][split] module however we like, but let's choose toouse hello left output as training data and hello right output as testing data.</span></span>  

<span data-ttu-id="4b89a-174">Como se mencionó en hello [paso anterior](machine-learning-walkthrough-2-upload-data.md), costo de Hola de clasifique mal un riesgo de crédito alta como baja es cinco veces mayor que el costo de Hola de clasifique mal un riesgo de crédito baja como high.</span><span class="sxs-lookup"><span data-stu-id="4b89a-174">As mentioned in hello [previous step](machine-learning-walkthrough-2-upload-data.md), hello cost of misclassifying a high credit risk as low is five times higher than hello cost of misclassifying a low credit risk as high.</span></span> <span data-ttu-id="4b89a-175">tooaccount para esto, se genera un nuevo conjunto de datos que refleja esta función de costo.</span><span class="sxs-lookup"><span data-stu-id="4b89a-175">tooaccount for this, we generate a new dataset that reflects this cost function.</span></span> <span data-ttu-id="4b89a-176">Hola nuevo conjunto de datos, cada ejemplo de alto riesgo se replica cinco veces, mientras no se replica en cada ejemplo de bajo riesgo.</span><span class="sxs-lookup"><span data-stu-id="4b89a-176">In hello new dataset, each high risk example is replicated five times, while each low risk example is not replicated.</span></span>   

<span data-ttu-id="4b89a-177">Podemos conseguir esta replicación mediante el código R:</span><span class="sxs-lookup"><span data-stu-id="4b89a-177">We can do this replication using R code:</span></span>  

1. <span data-ttu-id="4b89a-178">Busque y arrastre hello [ejecutar Script de R] [ execute-r-script] módulo al lienzo del experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b89a-178">Find and drag hello [Execute R Script][execute-r-script] module onto hello experiment canvas.</span></span> 

2. <span data-ttu-id="4b89a-179">Conectar Hola dejado el puerto de salida de hello [dividir datos] [ split] toohello módulo primera entrada de puerto ("Dataset1") del programa Hola a [ejecutar Script de R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="4b89a-179">Connect hello left output port of hello [Split Data][split] module toohello first input port ("Dataset1") of hello [Execute R Script][execute-r-script] module.</span></span>

3. <span data-ttu-id="4b89a-180">Haga doble clic en hello [ejecutar Script de R] [ execute-r-script] módulo y escriba el comentario de hello, "Ajuste del coste de conjunto".</span><span class="sxs-lookup"><span data-stu-id="4b89a-180">Double-click hello [Execute R Script][execute-r-script] module and enter hello comment, "Set cost adjustment".</span></span>

4. <span data-ttu-id="4b89a-181">Hola **propiedades** panel, el texto de eliminación Hola predeterminado en hello **Script de R** parámetro y escriba esta secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="4b89a-181">In hello **Properties** pane, delete hello default text in hello **R Script** parameter and enter this script:</span></span>
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![Script de R en el módulo ejecutar Script de R de Hola][9]

<span data-ttu-id="4b89a-183">Necesitamos toodo esta misma operación de replicación para cada salida de hello [dividir datos] [ split] ajuste del módulo para ese Hola de entrenamiento y de datos de prueba ha Hola mismo costo.</span><span class="sxs-lookup"><span data-stu-id="4b89a-183">We need toodo this same replication operation for each output of hello [Split Data][split] module so that hello training and testing data have hello same cost adjustment.</span></span> <span data-ttu-id="4b89a-184">Hola toodo de manera más sencilla es duplicando hello [ejecutar Script de R] [ execute-r-script] módulo se acaba de crear y conectar toohello salida otro puerto de hello [dividir datos de] [ split] módulo.</span><span class="sxs-lookup"><span data-stu-id="4b89a-184">hello easiest way toodo this is by duplicating hello [Execute R Script][execute-r-script] module we just made and connecting it toohello other output port of hello [Split Data][split] module.</span></span>

1. <span data-ttu-id="4b89a-185">Menú contextual hello [ejecutar Script de R] [ execute-r-script] módulo y seleccione **copia**.</span><span class="sxs-lookup"><span data-stu-id="4b89a-185">Right-click hello [Execute R Script][execute-r-script] module and select **Copy**.</span></span>

2. <span data-ttu-id="4b89a-186">Haga clic en el lienzo del experimento de Hola y seleccione **pegar**.</span><span class="sxs-lookup"><span data-stu-id="4b89a-186">Right-click hello experiment canvas and select **Paste**.</span></span>

3. <span data-ttu-id="4b89a-187">Arrastre el nuevo módulo de hello en su posición y, a continuación, conecte el puerto de salida derecho de Hola de hello [dividir datos] [ split] toohello módulo primera entrada de puerto de este nuevo [ejecutar Script de R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="4b89a-187">Drag hello new module into position, and then connect hello right output port of hello [Split Data][split] module toohello first input port of this new [Execute R Script][execute-r-script] module.</span></span> 

4. <span data-ttu-id="4b89a-188">En la parte inferior de hello del lienzo de hello, haga clic en **ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="4b89a-188">At hello bottom of hello canvas, click **Run**.</span></span> 

> [!TIP]
> <span data-ttu-id="4b89a-189">copia de Hola de módulo ejecutar Script de R de hello contiene Hola mismo script como módulo original de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b89a-189">hello copy of hello Execute R Script module contains hello same script as hello original module.</span></span> <span data-ttu-id="4b89a-190">Al copiar y pegar un módulo en el lienzo de hello, copia de hello conserva todas las propiedades de Hola de hello original.</span><span class="sxs-lookup"><span data-stu-id="4b89a-190">When you copy and paste a module on hello canvas, hello copy retains all hello properties of hello original.</span></span>  
> 
> 

<span data-ttu-id="4b89a-191">Nuestro experimento tiene ahora un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="4b89a-191">Our experiment now looks something like this:</span></span>

![Adding Split module and R scripts][4]

<span data-ttu-id="4b89a-193">Para obtener más información sobre cómo usar los scripts de R en sus experimentos, consulte [Extender el experimento con R](machine-learning-extend-your-experiment-with-r.md).</span><span class="sxs-lookup"><span data-stu-id="4b89a-193">For more information on using R scripts in your experiments, see [Extend your experiment with R](machine-learning-extend-your-experiment-with-r.md).</span></span>

<span data-ttu-id="4b89a-194">**Siguiente: [entrenar y evaluar modelos de Hola](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span><span class="sxs-lookup"><span data-stu-id="4b89a-194">**Next: [Train and evaluate hello models](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span></span>

[0]: ./media/machine-learning-walkthrough-3-create-new-experiment/create-new-experiment.png
[5]: ./media/machine-learning-walkthrough-3-create-new-experiment/rename-experiment.png
[6]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-properties.png
[7]: ./media/machine-learning-walkthrough-3-create-new-experiment/add-dataset-to-experiment.png
[8]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-with-comment.png
[9]: ./media/machine-learning-walkthrough-3-create-new-experiment/execute-r-script.png
[1]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-with-edit-metadata-module.png
[2]: ./media/machine-learning-walkthrough-3-create-new-experiment/select-columns.png
[3]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-properties.png
[4]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
