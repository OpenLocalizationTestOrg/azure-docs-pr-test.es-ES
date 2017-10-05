---
title: "Paso 3: Creación de un nuevo experimento de Machine Learning | Microsoft Docs"
description: "Paso 3 del tutorial Desarrollo de una solución predictiva: crear un nuevo experimento de aprendizaje en Estudio de aprendizaje automático de Azure."
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
ms.openlocfilehash: cd410316910bce76f5c915c06e83b24c034481b7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a><span data-ttu-id="b2114-103">Paso 3 del tutorial: Creación de un nuevo experimento de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="b2114-103">Walkthrough Step 3: Create a new Azure Machine Learning experiment</span></span>
<span data-ttu-id="b2114-104">Este es el tercer paso del tutorial [Desarrollo de una solución de análisis predictiva para la evaluación del riesgo de crédito en Aprendizaje automático de Azure](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="b2114-104">This is the third step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="b2114-105">Creación de un área de trabajo de Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="b2114-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="b2114-106">Carga de los datos existentes</span><span class="sxs-lookup"><span data-stu-id="b2114-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. <span data-ttu-id="b2114-107">**Crear un experimento nuevo**</span><span class="sxs-lookup"><span data-stu-id="b2114-107">**Create a new experiment**</span></span>
4. [<span data-ttu-id="b2114-108">Entrenamiento y evaluación de los modelos</span><span class="sxs-lookup"><span data-stu-id="b2114-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="b2114-109">Implementación del servicio web</span><span class="sxs-lookup"><span data-stu-id="b2114-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="b2114-110">Acceso al servicio web</span><span class="sxs-lookup"><span data-stu-id="b2114-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="b2114-111">El siguiente paso de este tutorial es crear un experimento en Machine Learning Studio que utilice el conjunto de datos cargado.</span><span class="sxs-lookup"><span data-stu-id="b2114-111">The next step in this walkthrough is to create an experiment in Machine Learning Studio that uses the dataset we uploaded.</span></span>  

1. <span data-ttu-id="b2114-112">En Estudio de aprendizaje automático, haga clic en **+NUEVO** en la parte inferior de la ventana.</span><span class="sxs-lookup"><span data-stu-id="b2114-112">In Studio, click **+NEW** at the bottom of the window.</span></span>
2. <span data-ttu-id="b2114-113">Seleccione **EXPERIMENTO**y luego "Experimento en blanco".</span><span class="sxs-lookup"><span data-stu-id="b2114-113">Select **EXPERIMENT**, and then select "Blank Experiment".</span></span> 

    ![Creación de un nuevo experimento][0]

2. <span data-ttu-id="b2114-115">Seleccione el nombre del experimento predeterminado en la parte superior del lienzo y cámbielo por uno significativo.</span><span class="sxs-lookup"><span data-stu-id="b2114-115">Select the default experiment name at the top of the canvas and rename it to something meaningful.</span></span>

    ![Renombrar el experimento][5]
   
   > [!TIP]
   > <span data-ttu-id="b2114-117">Se recomienda rellenar los campos **Resumen** y **Descripción** del experimento en el panel **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="b2114-117">It's a good practice to fill in **Summary** and **Description** for the experiment in the **Properties** pane.</span></span> <span data-ttu-id="b2114-118">Estas propiedades ofrecen la oportunidad para documentar el experimento para que cualquier persona que lo vea posteriormente entienda sus objetivos y la metodología.</span><span class="sxs-lookup"><span data-stu-id="b2114-118">These properties give you the chance to document the experiment so that anyone who looks at it later will understand your goals and methodology.</span></span>
   > 
   > ![Propiedades del experimento][6]
   > 
3. <span data-ttu-id="b2114-120">En la paleta de módulos, a la izquierda del lienzo de experimentos, expanda **Conjuntos de datos guardados**.</span><span class="sxs-lookup"><span data-stu-id="b2114-120">In the module palette to the left of the experiment canvas, expand **Saved Datasets**.</span></span>
4. <span data-ttu-id="b2114-121">Busque el conjunto de datos que ha creado en **Mis conjuntos de datos** y arrástrelo al lienzo.</span><span class="sxs-lookup"><span data-stu-id="b2114-121">Find the dataset you created under **My Datasets** and drag it onto the canvas.</span></span> <span data-ttu-id="b2114-122">También puede buscar el conjunto de datos escribiendo su nombre en el cuadro **Buscar** que está encima de la paleta.</span><span class="sxs-lookup"><span data-stu-id="b2114-122">You can also find the dataset by entering the name in the **Search** box above the palette.</span></span>  

    ![Agregar el conjunto de datos al experimento][7]

## <a name="prepare-the-data"></a><span data-ttu-id="b2114-124">Preparación de los datos</span><span class="sxs-lookup"><span data-stu-id="b2114-124">Prepare the data</span></span>
<span data-ttu-id="b2114-125">Para ver las primeras 100 filas de datos y alguna información estadística de todo el conjunto de datos: haga clic en el puerto de salida del conjunto de datos (el círculo pequeño de la parte inferior) y seleccione **Visualizar**.</span><span class="sxs-lookup"><span data-stu-id="b2114-125">You can view the first 100 rows of the data and some statistical information for the whole dataset: Click the output port of the dataset (the small circle at the bottom) and select **Visualize**.</span></span>  

<span data-ttu-id="b2114-126">Dado que el archivo de datos no incluye encabezados de columna, Estudio de aprendizaje automático ha proporcionado encabezados genéricos (Col1, Col2, *etc.*).</span><span class="sxs-lookup"><span data-stu-id="b2114-126">Because the data file didn't come with column headings, Studio has provided generic headings (Col1, Col2, *etc.*).</span></span> <span data-ttu-id="b2114-127">No es esencial que los encabezados sean perfectos para crear un modelo, pero facilitan el trabajo con los datos del experimento.</span><span class="sxs-lookup"><span data-stu-id="b2114-127">Good headings aren't essential to creating a model, but they make it easier to work with the data in the experiment.</span></span> <span data-ttu-id="b2114-128">Además, cuando finalmente se publique este modelo en un servicio web, los encabezados ayudarán al usuario del servicio a identificar las columnas.</span><span class="sxs-lookup"><span data-stu-id="b2114-128">Also, when we eventually publish this model in a web service, the headings help identify the columns to the user of the service.</span></span>  

<span data-ttu-id="b2114-129">Se pueden agregar encabezados de columna mediante el módulo [Edit Metadata][edit-metadata] (Editar metadatos).</span><span class="sxs-lookup"><span data-stu-id="b2114-129">We can add column headings using the [Edit Metadata][edit-metadata] module.</span></span>
<span data-ttu-id="b2114-130">Use el módulo [Edit Metadata][edit-metadata] (Editar metadatos) para cambiar los metadatos asociados a un conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="b2114-130">You use the [Edit Metadata][edit-metadata] module to change metadata associated with a dataset.</span></span> <span data-ttu-id="b2114-131">En este caso, se usa para proporcionar nombres más descriptivos para los encabezados de las columnas.</span><span class="sxs-lookup"><span data-stu-id="b2114-131">In this case, we use it to provide more friendly names for column headings.</span></span> 

<span data-ttu-id="b2114-132">Para usar [Edit Metadata][edit-metadata] (Editar metadatos), especifique primero las columnas que desea modificar (en este caso, todas). A continuación, especifique la acción que desea realizar en esas columnas (en este caso, cambiar los encabezados de las columnas).</span><span class="sxs-lookup"><span data-stu-id="b2114-132">To use [Edit Metadata][edit-metadata], you first specify which columns to modify (in this case, all of them.) Next, you specify the action to be performed on those columns (in this case, changing column headings.)</span></span>

1. <span data-ttu-id="b2114-133">En la paleta de módulos, escriba "metadatos" en el cuadro **Buscar** .</span><span class="sxs-lookup"><span data-stu-id="b2114-133">In the module palette, type "metadata" in the **Search** box.</span></span> <span data-ttu-id="b2114-134">El módulo [Edit Metadata][edit-metadata] (Editar metadatos) aparece en la lista de módulos.</span><span class="sxs-lookup"><span data-stu-id="b2114-134">The [Edit Metadata][edit-metadata] appears in the module list.</span></span>

2. <span data-ttu-id="b2114-135">Haga clic en el módulo [Edit Metadata][edit-metadata] (Editar metadatos), arrástrelo al lienzo y colóquelo bajo el conjunto de datos agregado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b2114-135">Click and drag the [Edit Metadata][edit-metadata] module onto the canvas and drop it below the dataset we added earlier.</span></span>

3. <span data-ttu-id="b2114-136">Conecte el conjunto de datos al módulo [Edit Metadata][edit-metadata] (Editar metadatos): haga clic en el puerto de salida del conjunto de datos (el círculo pequeño de la parte inferior del conjunto de datos), arrastre el puerto de entrada del módulo [Edit Metadata][edit-metadata] (Editar metadatos) (el círculo pequeño de la parte superior del módulo) y luego suelte el botón del ratón.</span><span class="sxs-lookup"><span data-stu-id="b2114-136">Connect the dataset to the [Edit Metadata][edit-metadata]: click the output port of the dataset (the small circle at the bottom of the dataset), drag to the input port of [Edit Metadata][edit-metadata] (the small circle at the top of the module), then release the mouse button.</span></span> <span data-ttu-id="b2114-137">El conjunto de datos y el módulo permanecen conectados aunque se desplace por el lienzo.</span><span class="sxs-lookup"><span data-stu-id="b2114-137">The dataset and module remain connected even if you move either around on the canvas.</span></span>
   
   <span data-ttu-id="b2114-138">El experimento debería tener ahora un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="b2114-138">The experiment should now look something like this:</span></span>  
   
   ![Agregar metadatos de edición][1]
   
   <span data-ttu-id="b2114-140">El signo de exclamación rojo indica que no hemos configurado aún las propiedades de este módulo.</span><span class="sxs-lookup"><span data-stu-id="b2114-140">The red exclamation mark indicates that we haven't set the properties for this module yet.</span></span> <span data-ttu-id="b2114-141">Lo haremos a continuación.</span><span class="sxs-lookup"><span data-stu-id="b2114-141">We'll do that next.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="b2114-142">Puede agregar un comentario a un módulo; para ello, haga doble clic en el módulo y escriba texto.</span><span class="sxs-lookup"><span data-stu-id="b2114-142">You can add a comment to a module by double-clicking the module and entering text.</span></span> <span data-ttu-id="b2114-143">Esto puede ayudarle a ver de un vistazo lo que el módulo hace en el experimento.</span><span class="sxs-lookup"><span data-stu-id="b2114-143">This can help you see at a glance what the module is doing in your experiment.</span></span> <span data-ttu-id="b2114-144">En este caso, haga doble clic en el módulo [Edit Metadata][edit-metadata] (Editar metadatos) y escriba el comentario "Agregar encabezados de columna".</span><span class="sxs-lookup"><span data-stu-id="b2114-144">In this case, double-click the [Edit Metadata][edit-metadata] module and type the comment "Add column headings".</span></span> <span data-ttu-id="b2114-145">Haga clic en cualquier lugar del lienzo para cerrar el cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="b2114-145">Click anywhere else on the canvas to close the text box.</span></span> <span data-ttu-id="b2114-146">Para mostrar el comentario, haga clic en la flecha abajo en el módulo.</span><span class="sxs-lookup"><span data-stu-id="b2114-146">To display the comment, click the down-arrow on the module.</span></span>
   > 
   > ![Modificación del módulo de metadatos con el comentario agregado][8]
   > 
4. <span data-ttu-id="b2114-148">Seleccione [Editar metadatos][edit-metadata] y, en el panel **Propiedades** a la derecha del lienzo, haga clic en **Launch column selector** (Iniciar el selector de columnas).</span><span class="sxs-lookup"><span data-stu-id="b2114-148">Select [Edit Metadata][edit-metadata], and in the **Properties** pane to the right of the canvas, click **Launch column selector**.</span></span>

5. <span data-ttu-id="b2114-149">En el cuadro de diálogo **Seleccionar columnas**, elija todas las filas de **Columnas disponibles** y haga clic en > para moverlas a **Columnas seleccionadas**.</span><span class="sxs-lookup"><span data-stu-id="b2114-149">In the **Select columns** dialog, select all the rows in **Available Columns** and click > to move them to **Selected Columns**.</span></span>
   <span data-ttu-id="b2114-150">El cuadro de diálogo debe ser similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="b2114-150">The dialog should look like this:</span></span>

   ![Selector de columnas con todas las columnas seleccionadas][2]

6. <span data-ttu-id="b2114-152">Haga clic en la marca de verificación **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b2114-152">Click the **OK** check mark.</span></span>

7. <span data-ttu-id="b2114-153">En el panel **Propiedades**, busque el parámetro **Nuevo nombre de columna**.</span><span class="sxs-lookup"><span data-stu-id="b2114-153">Back in the **Properties** pane, look for the **New column names** parameter.</span></span> <span data-ttu-id="b2114-154">En este campo, escriba la lista de nombres de las 21 columnas del conjunto de datos, separadas por comas y en el orden de las columnas.</span><span class="sxs-lookup"><span data-stu-id="b2114-154">In this field, enter a list of names for the 21 columns in the dataset, separated by commas and in column order.</span></span> <span data-ttu-id="b2114-155">Puede obtener los nombres de las columnas en la documentación del conjunto de datos en el sitio web de UCI o, para mayor comodidad, puede copiar y pegar la siguiente lista:</span><span class="sxs-lookup"><span data-stu-id="b2114-155">You can obtain the columns names from the dataset documentation on the UCI website, or for convenience you can copy and paste the following list:</span></span>  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   <span data-ttu-id="b2114-156">El panel Propiedades tiene un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="b2114-156">The Properties pane looks like this:</span></span>
   
   ![Propiedades de los metadatos de edición][3]

> [!TIP]
> <span data-ttu-id="b2114-158">Si desea comprobar los encabezados de columna, ejecute el experimento (haga clic en **EJECUTAR** debajo del lienzo del experimento).</span><span class="sxs-lookup"><span data-stu-id="b2114-158">If you want to verify the column headings, run the experiment (click **RUN** below the experiment canvas).</span></span> <span data-ttu-id="b2114-159">Cuando termine de ejecutarse —aparece una marca de verificación verde en [Edit Metadata][edit-metadata] (Editar metadatos)—, haga clic en el puerto de salida del módulo [Edit Metadata][edit-metadata] (Editar metadatos) y seleccione **Visualizar**.</span><span class="sxs-lookup"><span data-stu-id="b2114-159">When it finishes running (a green check mark appears on [Edit Metadata][edit-metadata]), click the output port of the [Edit Metadata][edit-metadata] module, and select **Visualize**.</span></span> <span data-ttu-id="b2114-160">Puede ver el resultado de cualquier módulo igual que visualiza el progreso de los datos a lo largo del experimento.</span><span class="sxs-lookup"><span data-stu-id="b2114-160">You can view the output of any module in the same way to view the progress of the data through the experiment.</span></span>
> 
> 

## <a name="create-training-and-test-datasets"></a><span data-ttu-id="b2114-161">Creación de conjuntos de datos de entrenamiento y prueba</span><span class="sxs-lookup"><span data-stu-id="b2114-161">Create training and test datasets</span></span>
<span data-ttu-id="b2114-162">Se necesitan algunos datos para entrenar el modelo y otros tantos para probarlo.</span><span class="sxs-lookup"><span data-stu-id="b2114-162">We need some data to train the model and some to test it.</span></span>
<span data-ttu-id="b2114-163">De este modo, en el siguiente paso del experimento, se divide el conjunto de datos en dos conjuntos de datos independientes: uno para el entrenamiento de nuestro modelo y el otro para probarlo.</span><span class="sxs-lookup"><span data-stu-id="b2114-163">So in the next step of the experiment, we split the dataset into two separate datasets: one for training our model and one for testing it.</span></span>

<span data-ttu-id="b2114-164">Para ello, se usa el módulo [Split Data][split] (Dividir datos).</span><span class="sxs-lookup"><span data-stu-id="b2114-164">To do this, we use the [Split Data][split] module.</span></span>  

1. <span data-ttu-id="b2114-165">Busque el módulo [Split Data][split] (Dividir datos), arrástrelo al lienzo y conéctelo al módulo [Edit Metadata][edit-metadata] (Editar metadatos).</span><span class="sxs-lookup"><span data-stu-id="b2114-165">Find the [Split Data][split] module, drag it onto the canvas, and connect it to the [Edit Metadata][edit-metadata] module.</span></span>

2. <span data-ttu-id="b2114-166">De manera predeterminada, la proporción de división es 0,5 y se establece el parámetro **División aleatoria** .</span><span class="sxs-lookup"><span data-stu-id="b2114-166">By default, the split ratio is 0.5 and the **Randomized split** parameter is set.</span></span> <span data-ttu-id="b2114-167">Esto significa que una mitad aleatoria de los datos sale a través de un puerto del módulo [Split Data][split] (Dividir datos) y la otra mitad, por el otro.</span><span class="sxs-lookup"><span data-stu-id="b2114-167">This means that a random half of the data is output through one port of the [Split Data][split] module, and half through the other.</span></span> <span data-ttu-id="b2114-168">Puede cambiar estos parámetros, así como el parámetro **Valor de inicialización aleatorio**, para cambiar la división entre datos de entrenamiento y de prueba.</span><span class="sxs-lookup"><span data-stu-id="b2114-168">You can adjust these parameters, as well as the **Random seed** parameter, to change the split between training and testing data.</span></span> <span data-ttu-id="b2114-169">En este ejemplo, se deja tal cual.</span><span class="sxs-lookup"><span data-stu-id="b2114-169">For this example, we leave them as-is.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="b2114-170">La propiedad **Fraction of rows in the first output dataset** (Fracción de filas del primer conjunto de datos de salida) determina la cantidad de datos que salen a través del puerto de salida de la *izquierda*.</span><span class="sxs-lookup"><span data-stu-id="b2114-170">The property **Fraction of rows in the first output dataset** determines how much of the data is output through the *left* output port.</span></span> <span data-ttu-id="b2114-171">Por ejemplo, si establece la proporción en 0,7, el 70 % de los datos sale por el puerto de la izquierda y el 30 % por el puerto de la derecha.</span><span class="sxs-lookup"><span data-stu-id="b2114-171">For instance, if you set the ratio to 0.7, then 70% of the data is output through the left port and 30% through the right port.</span></span>  
   > 
   > 

3. <span data-ttu-id="b2114-172">Haga doble clic en el módulo [Split Data][split] (Dividir datos) y escriba el comentario "Dividir 50% de los datos de entrenamiento y pruebas".</span><span class="sxs-lookup"><span data-stu-id="b2114-172">Double-click the [Split Data][split] module and enter the comment, "Training/testing data split 50%".</span></span> 

<span data-ttu-id="b2114-173">Se pueden utilizar las salidas del módulo [Split Data][split] (Dividir datos) como deseemos, pero se va a optar por utilizar la salida de la izquierda como datos de entrenamiento y la salida de la derecha como datos de pruebas.</span><span class="sxs-lookup"><span data-stu-id="b2114-173">We can use the outputs of the [Split Data][split] module however we like, but let's choose to use the left output as training data and the right output as testing data.</span></span>  

<span data-ttu-id="b2114-174">Como se menciona en el [paso anterior](machine-learning-walkthrough-2-upload-data.md), el costo de clasificar erróneamente un riesgo de crédito alto como bajo es cinco veces más alto que el costo de clasificar erróneamente un riesgo de crédito bajo como alto.</span><span class="sxs-lookup"><span data-stu-id="b2114-174">As mentioned in the [previous step](machine-learning-walkthrough-2-upload-data.md), the cost of misclassifying a high credit risk as low is five times higher than the cost of misclassifying a low credit risk as high.</span></span> <span data-ttu-id="b2114-175">Para tener esto en cuenta, se debe generar un nuevo conjunto de datos que refleje esta función de costo.</span><span class="sxs-lookup"><span data-stu-id="b2114-175">To account for this, we generate a new dataset that reflects this cost function.</span></span> <span data-ttu-id="b2114-176">En el nuevo conjunto de datos, cada ejemplo de alto riesgo se replica cinco veces, mientras que el ejemplo de bajo riesgo no se replica.</span><span class="sxs-lookup"><span data-stu-id="b2114-176">In the new dataset, each high risk example is replicated five times, while each low risk example is not replicated.</span></span>   

<span data-ttu-id="b2114-177">Podemos conseguir esta replicación mediante el código R:</span><span class="sxs-lookup"><span data-stu-id="b2114-177">We can do this replication using R code:</span></span>  

1. <span data-ttu-id="b2114-178">Busque el módulo [Execute R Script][execute-r-script] (Ejecutar script R) y arrástrelo al lienzo del experimento.</span><span class="sxs-lookup"><span data-stu-id="b2114-178">Find and drag the [Execute R Script][execute-r-script] module onto the experiment canvas.</span></span> 

2. <span data-ttu-id="b2114-179">Conecte el puerto de salida de la izquierda del módulo [Split Data][split] (Dividir datos) al primer puerto de entrada ("Dataset1") del módulo [Execute R Script][execute-r-script] (Ejecutar script R).</span><span class="sxs-lookup"><span data-stu-id="b2114-179">Connect the left output port of the [Split Data][split] module to the first input port ("Dataset1") of the [Execute R Script][execute-r-script] module.</span></span>

3. <span data-ttu-id="b2114-180">Haga doble clic en el módulo [Execute R Script][execute-r-script] (Ejecutar script R) y escriba el comentario "Establecer ajuste de costos".</span><span class="sxs-lookup"><span data-stu-id="b2114-180">Double-click the [Execute R Script][execute-r-script] module and enter the comment, "Set cost adjustment".</span></span>

4. <span data-ttu-id="b2114-181">En el panel **Propiedades**, elimine el texto predeterminado del parámetro **Script R** y escriba este script:</span><span class="sxs-lookup"><span data-stu-id="b2114-181">In the **Properties** pane, delete the default text in the **R Script** parameter and enter this script:</span></span>
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![Script R en el módulo Execute R Script (Ejecutar script R)][9]

<span data-ttu-id="b2114-183">Hay que hacer esta misma operación de replicación para cada salida del módulo [Split Data][split] (Dividir datos) para que los datos de entrenamiento y prueba tengan el mismo ajuste con relación al costo.</span><span class="sxs-lookup"><span data-stu-id="b2114-183">We need to do this same replication operation for each output of the [Split Data][split] module so that the training and testing data have the same cost adjustment.</span></span> <span data-ttu-id="b2114-184">La forma más sencilla de hacerlo consiste en duplicar el módulo [Execute R Script][execute-r-script] (Ejecutar script R) que se acaba de crear y conectarlo al otro puerto de salida del módulo [Split Data][split] (Dividir datos).</span><span class="sxs-lookup"><span data-stu-id="b2114-184">The easiest way to do this is by duplicating the [Execute R Script][execute-r-script] module we just made and connecting it to the other output port of the [Split Data][split] module.</span></span>

1. <span data-ttu-id="b2114-185">Haga clic con el botón derecho en el módulo [Execute R Script][execute-r-script] (Ejecutar script R) y seleccione **Copiar**.</span><span class="sxs-lookup"><span data-stu-id="b2114-185">Right-click the [Execute R Script][execute-r-script] module and select **Copy**.</span></span>

2. <span data-ttu-id="b2114-186">Haga clic con el botón secundario en el lienzo del experimento y seleccione **Pegar**.</span><span class="sxs-lookup"><span data-stu-id="b2114-186">Right-click the experiment canvas and select **Paste**.</span></span>

3. <span data-ttu-id="b2114-187">Arrastre el nuevo módulo a la posición correspondiente y luego conecte el puerto de salida de la derecha del módulo [Split Data][split] (Dividir datos) al primer puerto de entrada de este nuevo módulo [Execute R Script][execute-r-script] (Ejecutar script R).</span><span class="sxs-lookup"><span data-stu-id="b2114-187">Drag the new module into position, and then connect the right output port of the [Split Data][split] module to the first input port of this new [Execute R Script][execute-r-script] module.</span></span> 

4. <span data-ttu-id="b2114-188">En la parte inferior del lienzo, haga clic en **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="b2114-188">At the bottom of the canvas, click **Run**.</span></span> 

> [!TIP]
> <span data-ttu-id="b2114-189">La copia del módulo Ejecutar script R contiene el mismo script que el módulo original.</span><span class="sxs-lookup"><span data-stu-id="b2114-189">The copy of the Execute R Script module contains the same script as the original module.</span></span> <span data-ttu-id="b2114-190">Al copiar y pegar un módulo en el lienzo, la copia retiene todas las propiedades del original.</span><span class="sxs-lookup"><span data-stu-id="b2114-190">When you copy and paste a module on the canvas, the copy retains all the properties of the original.</span></span>  
> 
> 

<span data-ttu-id="b2114-191">Nuestro experimento tiene ahora un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="b2114-191">Our experiment now looks something like this:</span></span>

![Adding Split module and R scripts][4]

<span data-ttu-id="b2114-193">Para obtener más información sobre cómo usar los scripts de R en sus experimentos, consulte [Extender el experimento con R](machine-learning-extend-your-experiment-with-r.md).</span><span class="sxs-lookup"><span data-stu-id="b2114-193">For more information on using R scripts in your experiments, see [Extend your experiment with R](machine-learning-extend-your-experiment-with-r.md).</span></span>

<span data-ttu-id="b2114-194">**A continuación: [Entrenamiento y evaluación de los modelos](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span><span class="sxs-lookup"><span data-stu-id="b2114-194">**Next: [Train and evaluate the models](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span></span>

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
