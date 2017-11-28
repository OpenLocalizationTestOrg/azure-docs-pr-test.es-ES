---
title: "Paso 4: Entrenamiento y evaluación de los modelos de análisis predictivo | Microsoft Docs"
description: "Paso 4 del tutorial Desarrollo de una solución predictiva: entrenamiento, puntuación y evaluación de múltiples modelos en Estudio de aprendizaje automático de Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: d905f6b3-9201-4117-b769-5f9ed5ee1cac
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 58d46dd1464ec0a3fc9639f78d4429e0e778c2bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-the-predictive-analytic-models"></a><span data-ttu-id="bce88-103">Paso 4 del tutorial: Entrenamiento y evaluación de los modelos de análisis predictivo</span><span class="sxs-lookup"><span data-stu-id="bce88-103">Walkthrough Step 4: Train and evaluate the predictive analytic models</span></span>
<span data-ttu-id="bce88-104">Este tema contiene el cuarto paso del tutorial [Desarrollo de una solución de análisis predictivo en Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="bce88-104">This topic contains the fourth step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="bce88-105">Creación de un área de trabajo de Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="bce88-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="bce88-106">Carga de los datos existentes</span><span class="sxs-lookup"><span data-stu-id="bce88-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="bce88-107">Crear un experimento nuevo</span><span class="sxs-lookup"><span data-stu-id="bce88-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. <span data-ttu-id="bce88-108">**Entrenamiento y evaluación de los modelos**</span><span class="sxs-lookup"><span data-stu-id="bce88-108">**Train and evaluate the models**</span></span>
5. [<span data-ttu-id="bce88-109">Implementación del servicio web</span><span class="sxs-lookup"><span data-stu-id="bce88-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="bce88-110">Acceso al servicio web</span><span class="sxs-lookup"><span data-stu-id="bce88-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="bce88-111">Una de las ventajas del uso de Azure Machine Learning Studio para crear modelos de aprendizaje automático es la capacidad para probar más de un tipo de modelo a la vez en un solo experimento y comparar los resultados.</span><span class="sxs-lookup"><span data-stu-id="bce88-111">One of the benefits of using Azure Machine Learning Studio for creating machine learning models is the ability to try more than one type of model at a time in a single experiment and compare the results.</span></span> <span data-ttu-id="bce88-112">Este tipo de experimentación ayuda a encontrar la mejor solución al problema.</span><span class="sxs-lookup"><span data-stu-id="bce88-112">This type of experimentation helps you find the best solution for your problem.</span></span>

<span data-ttu-id="bce88-113">En el experimento que vamos a crear en este tutorial, crearemos dos tipos diferentes de modelos y después compararemos los resultados de su puntuación para decidir cuál de ellos utilizaremos en nuestro experimento final.</span><span class="sxs-lookup"><span data-stu-id="bce88-113">In the experiment we're developing in this walkthrough, we'll create two different types of models and then compare their scoring results to decide which algorithm we want to use in our final experiment.</span></span>  

<span data-ttu-id="bce88-114">Existen varios modelos entre los que se puede elegir.</span><span class="sxs-lookup"><span data-stu-id="bce88-114">There are various models we could choose from.</span></span> <span data-ttu-id="bce88-115">Para ver cuáles están disponibles, expanda el nodo **Machine Learning** de la paleta de módulos y luego expanda **Initialize Model** (Inicializar modelo) y los nodos que incluye.</span><span class="sxs-lookup"><span data-stu-id="bce88-115">To see the models available, expand the **Machine Learning** node in the module palette, and then expand **Initialize Model** and the nodes beneath it.</span></span> <span data-ttu-id="bce88-116">Teniendo en cuenta el objetivo de este experimento, se seleccionan los módulos [Two-Class Support Vector Machine][two-class-support-vector-machine] (Máquina de vectores de soporte de dos clases, SVM) y [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] (Árbol de decisión ampliados de dos clases).</span><span class="sxs-lookup"><span data-stu-id="bce88-116">For the purposes of this experiment, we'll select the [Two-Class Support Vector Machine][two-class-support-vector-machine] (SVM) and the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] modules.</span></span>    

> [!TIP]
> <span data-ttu-id="bce88-117">Para obtener ayuda para decidir qué algoritmo de Aprendizaje automático se adapta mejor al problema concreto que trata de solucionar, vea [Cómo elegir algoritmos para Aprendizaje automático de Microsoft Azure](machine-learning-algorithm-choice.md).</span><span class="sxs-lookup"><span data-stu-id="bce88-117">To get help deciding which Machine Learning algorithm best suits the particular problem you're trying to solve, see [How to choose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span></span>
> 
> 

## <a name="train-the-models"></a><span data-ttu-id="bce88-118">Entrenamiento de los modelos</span><span class="sxs-lookup"><span data-stu-id="bce88-118">Train the models</span></span>

<span data-ttu-id="bce88-119">Se van a agregar tanto el módulo [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] (Árbol de decisión ampliados de dos clases) como el módulo [Two-Class Support Vector Machine][two-class-support-vector-machine] (Máquina de vectores de soporte de dos clases) en este experimento.</span><span class="sxs-lookup"><span data-stu-id="bce88-119">We'll add both the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module and [Two-Class Support Vector Machine][two-class-support-vector-machine] module in this experiment.</span></span>

### <a name="two-class-boosted-decision-tree"></a><span data-ttu-id="bce88-120">Árbol de decisión ampliado de dos clases</span><span class="sxs-lookup"><span data-stu-id="bce88-120">Two-Class Boosted Decision Tree</span></span>

<span data-ttu-id="bce88-121">En primer lugar, se va a configurar el modelo del árbol de decisión ampliado.</span><span class="sxs-lookup"><span data-stu-id="bce88-121">First, let's set up the boosted decision tree model.</span></span>

1. <span data-ttu-id="bce88-122">Busque el módulo [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] (Árbol de decisión ampliados de dos clases) en la paleta de módulos y arrástrelo al lienzo.</span><span class="sxs-lookup"><span data-stu-id="bce88-122">Find the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module in the module palette and drag it onto the canvas.</span></span>

2. <span data-ttu-id="bce88-123">Busque el módulo [Train Model][train-model] (Entrenar modelo), arrástrelo al lienzo y conecte la salida del módulo [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] (Árbol de decisión ampliados de dos clases) al puerto de entrada izquierdo del módulo [Train Model][train-model] (Entrenar modelo).</span><span class="sxs-lookup"><span data-stu-id="bce88-123">Find the [Train Model][train-model] module, drag it onto the canvas, and then connect the output of the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module to the left input port of the [Train Model][train-model] module.</span></span>
   
   <span data-ttu-id="bce88-124">El módulo [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] (Árbol de decisión ampliados de dos clases) inicializa el modelo genérico, y [Train Model][train-model] (Entrenar modelo) usa los datos de entrenamiento para entrenar el modelo.</span><span class="sxs-lookup"><span data-stu-id="bce88-124">The [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module initializes the generic model, and [Train Model][train-model] uses training data to train the model.</span></span> 

3. <span data-ttu-id="bce88-125">Conecte la salida izquierda al módulo [Execute R Script][execute-r-script] (Ejecutar script R) al puerto de entrada de la derecha del módulo [Train Model][train-model] (Entrenar modelo); en el [paso 3](machine-learning-walkthrough-3-create-new-experiment.md) de este tutorial se decidió usar los datos procedentes del lado izquierdo del módulo Split Data (Dividir datos) para el entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="bce88-125">Connect the left output of the left [Execute R Script][execute-r-script] module to the right input port of the [Train Model][train-model] module (we decided in [Step 3](machine-learning-walkthrough-3-create-new-experiment.md) of this walkthrough to use the data coming from the left side of the Split Data module for training).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="bce88-126">No se necesitan dos de las entradas y una de las salidas del módulo [Execute R Script][execute-r-script] (Ejecutar script R) para este experimento, así que se pueden dejar desconectadas.</span><span class="sxs-lookup"><span data-stu-id="bce88-126">We don't need two of the inputs and one of the outputs of the [Execute R Script][execute-r-script] module for this experiment, so we can leave them unattached.</span></span> 
   > 
   > 

<span data-ttu-id="bce88-127">Esta parte del experimento tiene ahora un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="bce88-127">This portion of the experiment now looks something like this:</span></span>  

![Training a model][1]

<span data-ttu-id="bce88-129">Ahora es necesario indicar al módulo [Entrenar modelo][train-model] que se desea que el modelo prediga el valor del riesgo de crédito.</span><span class="sxs-lookup"><span data-stu-id="bce88-129">Now we need to tell the [Train Model][train-model] module that we want the model to predict the Credit Risk value.</span></span>

1. <span data-ttu-id="bce88-130">Seleccione el módulo [Train Model][train-model] (Entrenar modelo).</span><span class="sxs-lookup"><span data-stu-id="bce88-130">Select the [Train Model][train-model] module.</span></span> <span data-ttu-id="bce88-131">En el panel **Propiedades**, haga clic en **Launch column selector** (Iniciar el selector de columnas).</span><span class="sxs-lookup"><span data-stu-id="bce88-131">In the **Properties** pane, click **Launch column selector**.</span></span>

2. <span data-ttu-id="bce88-132">En el cuadro de diálogo **Select a single column** (Seleccionar una sola columna), escriba "riesgo de crédito" en el campo de búsqueda en **Columnas disponibles**, seleccione "Riesgo de crédito" a continuación y haga clic en el botón de la flecha derecha (**>**) para mover "Riesgo de crédito" a **Columnas seleccionadas**.</span><span class="sxs-lookup"><span data-stu-id="bce88-132">In the **Select a single column** dialog, type "credit risk" in the search field under **Available Columns**, select "Credit risk" below, and click the right arrow button (**>**) to move "Credit risk" to **Selected Columns**.</span></span> 

    ![Seleccione la columna de riesgo de crédito para el módulo Entrenar modelo][0]

3. <span data-ttu-id="bce88-134">Haga clic en la marca de verificación **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="bce88-134">Click the **OK** check mark.</span></span>

### <a name="two-class-support-vector-machine"></a><span data-ttu-id="bce88-135">Máquina de vectores de soporte de dos clases</span><span class="sxs-lookup"><span data-stu-id="bce88-135">Two-Class Support Vector Machine</span></span>

<span data-ttu-id="bce88-136">A continuación, se debe configurar el modelo SVM.</span><span class="sxs-lookup"><span data-stu-id="bce88-136">Next, we set up the SVM model.</span></span>  

<span data-ttu-id="bce88-137">En primer lugar, una breve explicación sobre SVM.</span><span class="sxs-lookup"><span data-stu-id="bce88-137">First, a little explanation about SVM.</span></span> <span data-ttu-id="bce88-138">Los árboles de decisión ampliados funcionan bien con características de todo tipo.</span><span class="sxs-lookup"><span data-stu-id="bce88-138">Boosted decision trees work well with features of any type.</span></span> <span data-ttu-id="bce88-139">Sin embargo, dado que el módulo SVM genera un clasificador lineal, el modelo que genera tiene el mejor error de prueba cuando todas las características numéricas tienen la misma escala.</span><span class="sxs-lookup"><span data-stu-id="bce88-139">However, since the SVM module generates a linear classifier, the model that it generates has the best test error when all numeric features have the same scale.</span></span> <span data-ttu-id="bce88-140">Para convertir todas las características numéricas a la misma escala, se utiliza una transformación "Tanh", con el módulo [Normalize Data][normalize-data] (Normalizar datos).</span><span class="sxs-lookup"><span data-stu-id="bce88-140">To convert all numeric features to the same scale, we use a "Tanh" transformation (with the [Normalize Data][normalize-data] module).</span></span> <span data-ttu-id="bce88-141">Esto transforma los números en el intervalo [0,1].</span><span class="sxs-lookup"><span data-stu-id="bce88-141">This transforms our numbers into the [0,1] range.</span></span> <span data-ttu-id="bce88-142">El módulo SVM convierte las características de cadena en características categóricas y luego a características binarias 0/1. Por lo tanto, no hace falta transformar manualmente las características de cadena.</span><span class="sxs-lookup"><span data-stu-id="bce88-142">The SVM module converts string features to categorical features and then to binary 0/1 features, so we don't need to manually transform string features.</span></span> <span data-ttu-id="bce88-143">Además, no queremos transformar la columna Riesgo de crédito (columna 21): es numérica, pero es el valor sobre cuya predicción estamos entrenando al modelo; por tanto, es necesario dejarla tal cual.</span><span class="sxs-lookup"><span data-stu-id="bce88-143">Also, we don't want to transform the Credit Risk column (column 21) - it's numeric, but it's the value we're training the model to predict, so we need to leave it alone.</span></span>  

<span data-ttu-id="bce88-144">Para configurar el modelo SVM, realice lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="bce88-144">To set up the SVM model, do the following:</span></span>

1. <span data-ttu-id="bce88-145">Busque el módulo [Two-Class Support Vector Machine][two-class-support-vector-machine] (Máquina de vectores de soporte de dos clases) en la paleta de módulos y arrástrelo al lienzo.</span><span class="sxs-lookup"><span data-stu-id="bce88-145">Find the [Two-Class Support Vector Machine][two-class-support-vector-machine] module in the module palette and drag it onto the canvas.</span></span>

2. <span data-ttu-id="bce88-146">Haga clic con el botón derecho en el módulo [Train Model][train-model] (Entrenar modelo), seleccione **Copiar**, haga clic con el botón derecho en el lienzo y seleccione **Pegar**.</span><span class="sxs-lookup"><span data-stu-id="bce88-146">Right-click the [Train Model][train-model] module, select **Copy**, and then right-click the canvas and select **Paste**.</span></span> <span data-ttu-id="bce88-147">La copia del módulo [Train Model][train-model] (Entrenar modelo) tiene la misma selección de columnas que el original.</span><span class="sxs-lookup"><span data-stu-id="bce88-147">The copy of the [Train Model][train-model] module has the same column selection as the original.</span></span>

3. <span data-ttu-id="bce88-148">Conecte la salida del módulo [Máquina de vectores de soporte de dos clases][two-class-support-vector-machine] al puerto de entrada izquierdo del módulo [Entrenar modelo][train-model].</span><span class="sxs-lookup"><span data-stu-id="bce88-148">Connect the output of the [Two-Class Support Vector Machine][two-class-support-vector-machine] module to the left input port of the second [Train Model][train-model] module.</span></span>

4. <span data-ttu-id="bce88-149">Busque el módulo [Normalizar datos][normalize-data] y arrástrelo al lienzo.</span><span class="sxs-lookup"><span data-stu-id="bce88-149">Find the [Normalize Data][normalize-data] module and drag it onto the canvas.</span></span>

5. <span data-ttu-id="bce88-150">Conecte la salida de la izquierda del módulo [Ejecutar script R][execute-r-script] de la izquierda a la entrada de este módulo (tenga en cuenta que el puerto de salida de un módulo puede estar conectado a más de un módulo distinto).</span><span class="sxs-lookup"><span data-stu-id="bce88-150">Connect the left output of the left [Execute R Script][execute-r-script] module to the input of this module (notice that the output port of a module may be connected to more than one other module).</span></span>

6. <span data-ttu-id="bce88-151">Conecte el puerto de salida izquierdo del módulo [Normalize Data][normalize-data] (Normalizar datos) al puerto de salida derecho del segundo módulo [Train Model][train-model] (Entrenar modelo).</span><span class="sxs-lookup"><span data-stu-id="bce88-151">Connect the left output port of the [Normalize Data][normalize-data] module to the right input port of the second [Train Model][train-model] module.</span></span>

<span data-ttu-id="bce88-152">Esta parte de nuestro experimento debería tener ahora un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="bce88-152">This portion of our experiment should now look something like this:</span></span>  

![Training the second model][2]  

<span data-ttu-id="bce88-154">Configure ahora el módulo [Normalize Data][normalize-data] (Normalizar datos):</span><span class="sxs-lookup"><span data-stu-id="bce88-154">Now configure the [Normalize Data][normalize-data] module:</span></span>

1. <span data-ttu-id="bce88-155">Haga clic para seleccionar el módulo [Normalize Data][normalize-data] (Normalizar datos).</span><span class="sxs-lookup"><span data-stu-id="bce88-155">Click to select the [Normalize Data][normalize-data] module.</span></span> <span data-ttu-id="bce88-156">En el panel **Propiedades**, seleccione **Tanh** para el parámetro **Transformation method** (Método de transformación).</span><span class="sxs-lookup"><span data-stu-id="bce88-156">In the **Properties** pane, select **Tanh** for the **Transformation method** parameter.</span></span>

2. <span data-ttu-id="bce88-157">Haga clic en **Launch column selector** (Iniciar el selector de columnas), seleccione "No columns" (Sin columnas) en **Comenzar con**, seleccione **Incluir** en el primer menú desplegable, **Tipo de columna** en el segundo y **Numérica** en el tercero.</span><span class="sxs-lookup"><span data-stu-id="bce88-157">Click **Launch column selector**, select "No columns" for **Begin With**, select **Include** in the first dropdown, select **column type** in the second dropdown, and select **Numeric** in the third dropdown.</span></span> <span data-ttu-id="bce88-158">Esto especifica que todas las columnas numéricas (y solo numéricas) se deben transformar.</span><span class="sxs-lookup"><span data-stu-id="bce88-158">This specifies that all the numeric columns (and only numeric) are transformed.</span></span>

3. <span data-ttu-id="bce88-159">Haga clic en el signo más (+) a la derecha de esta fila (de esta forma, se crea una fila de menús desplegables).</span><span class="sxs-lookup"><span data-stu-id="bce88-159">Click the plus sign (+) to the right of this row - this creates a row of dropdowns.</span></span> <span data-ttu-id="bce88-160">Seleccione **Excluir** en la primera lista desplegable y **Nombres de columna** en la segunda, y escriba "Riesgo de crédito" en el campo de texto.</span><span class="sxs-lookup"><span data-stu-id="bce88-160">Select **Exclude** in the first dropdown, select **column names** in the second dropdown, and enter "Credit risk" in the text field.</span></span> <span data-ttu-id="bce88-161">Especifica que se debe ignorar la columna Riesgo de crédito (debemos hacerlo porque se trata de una columna numérica y, de lo contrario, se transformaría).</span><span class="sxs-lookup"><span data-stu-id="bce88-161">This specifies that the Credit Risk column should be ignored (we need to do this because this column is numeric and so would be transformed if we didn't exclude it).</span></span>

4. <span data-ttu-id="bce88-162">Haga clic en la marca de verificación **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="bce88-162">Click the **OK** check mark.</span></span>  

    ![Seleccionar columnas para el módulo Normalize Data (Normalizar datos)][5]

<span data-ttu-id="bce88-164">El módulo [Normalize Data][normalize-data] (Normalizar datos) está configurado ahora para realizar una transformación Tanh en todas las columnas numéricas excepto en la columna de riesgo de crédito.</span><span class="sxs-lookup"><span data-stu-id="bce88-164">The [Normalize Data][normalize-data] module is now set to perform a Tanh transformation on all numeric columns except for the Credit Risk column.</span></span>  

## <a name="score-and-evaluate-the-models"></a><span data-ttu-id="bce88-165">Puntuación y evaluación de modelos</span><span class="sxs-lookup"><span data-stu-id="bce88-165">Score and evaluate the models</span></span>

<span data-ttu-id="bce88-166">Se utilizan los datos de prueba que se separaron mediante el módulo [Split Data][split] (Dividir datos) para puntuar los modelos entrenados.</span><span class="sxs-lookup"><span data-stu-id="bce88-166">We use the testing data that was separated out by the [Split Data][split] module to score our trained models.</span></span> <span data-ttu-id="bce88-167">A continuación podremos comparar los resultados de los dos modelos para ver cuál de ellos generó mejores resultados.</span><span class="sxs-lookup"><span data-stu-id="bce88-167">We can then compare the results of the two models to see which generated better results.</span></span>  

### <a name="add-the-score-model-modules"></a><span data-ttu-id="bce88-168">Agregar los módulos Score Model (Puntuar modelo)</span><span class="sxs-lookup"><span data-stu-id="bce88-168">Add the Score Model modules</span></span>

1. <span data-ttu-id="bce88-169">Busque el módulo [Score Model][score-model] (Puntuar modelo) y arrástrelo al lienzo.</span><span class="sxs-lookup"><span data-stu-id="bce88-169">Find the [Score Model][score-model] module and drag it onto the canvas.</span></span>

2. <span data-ttu-id="bce88-170">Conecte el módulo [Train Model][train-model] (Entrenar modelo) que está conectado al módulo [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] (Árbol de decisión ampliado de dos clases) al puerto de entrada izquierdo del módulo [Score Model][score-model] (Puntuar modelo).</span><span class="sxs-lookup"><span data-stu-id="bce88-170">Connect the [Train Model][train-model] module that's connected to the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module to the left input port of the [Score Model][score-model] module.</span></span>

3. <span data-ttu-id="bce88-171">Conecte el módulo derecho [Execute R Script][execute-r-script] (Ejecutar script R) (los datos de prueba) al puerto de entrada derecho del módulo [Score Model][score-model] (Puntuar modelo).</span><span class="sxs-lookup"><span data-stu-id="bce88-171">Connect the right [Execute R Script][execute-r-script] module (our testing data) to the right input port of the [Score Model][score-model] module.</span></span>

    ![Módulo Score Model (Puntuar modelo) conectado][6]
   
   <span data-ttu-id="bce88-173">El módulo [Score Model][score-model] (Puntuar modelo) ahora puede utilizar la información de crédito de los datos de prueba, ejecutarla a través del modelo y comparar las predicciones que el modelo genera con la columna de riesgo de crédito real de los datos de prueba.</span><span class="sxs-lookup"><span data-stu-id="bce88-173">The [Score Model][score-model] module can now take the credit information from the testing data, run it through the model, and compare the predictions the model generates with the actual credit risk column in the testing data.</span></span>

4. <span data-ttu-id="bce88-174">Copie y pegue el módulo [Score Model][score-model] (Puntuar modelo) para crear una segunda copia.</span><span class="sxs-lookup"><span data-stu-id="bce88-174">Copy and paste the [Score Model][score-model] module to create a second copy.</span></span>

5. <span data-ttu-id="bce88-175">Conecte la salida del modelo SVM; es decir, el puerto de salida del módulo [Train Model][train-model] (Entrenar modelo) que está conectado al módulo [Two-Class Support Vector Machine][two-class-support-vector-machine] (Máquina de vectores de soporte de dos clases) al puerto de entrada del segundo módulo [Score Model][score-model] (Puntuar modelo).</span><span class="sxs-lookup"><span data-stu-id="bce88-175">Connect the output of the SVM model (that is, the output port of the [Train Model][train-model] module that's connected to the [Two-Class Support Vector Machine][two-class-support-vector-machine] module) to the input port of the second [Score Model][score-model] module.</span></span>

6. <span data-ttu-id="bce88-176">En cuanto al modelo SVM, tenemos que realizar la misma transformación en los datos de prueba que la que realizamos con los datos de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="bce88-176">For the SVM model, we have to do the same transformation to the test data as we did to the training data.</span></span> <span data-ttu-id="bce88-177">Así pues, copie y pegue el módulo [Normalize Data][normalize-data] (Normalizar datos) para crear una segunda copia y conéctelo al módulo derecho [Execute R Script][execute-r-script] (Ejecutar script R).</span><span class="sxs-lookup"><span data-stu-id="bce88-177">So copy and paste the [Normalize Data][normalize-data] module to create a second copy and connect it to the right [Execute R Script][execute-r-script] module.</span></span>

7. <span data-ttu-id="bce88-178">Conecte la salida izquierda del segundo módulo [Normalize Data][normalize-data] (Normalizar datos) al puerto de salida derecho del segundo módulo [Score Model][score-model] (Puntuar modelo).</span><span class="sxs-lookup"><span data-stu-id="bce88-178">Connect the left output of the second [Normalize Data][normalize-data] module to the right input port of the second [Score Model][score-model] module.</span></span>

    ![Ambos módulos Score Model (Puntuar modelo) conectados][7]

### <a name="add-the-evaluate-model-module"></a><span data-ttu-id="bce88-180">Agregar el módulo Evaluate Model (Evaluar modelo)</span><span class="sxs-lookup"><span data-stu-id="bce88-180">Add the Evaluate Model module</span></span>

<span data-ttu-id="bce88-181">Para evaluar los dos resultados de puntuación y compararlos, se usa un módulo [Evaluate Model][evaluate-model] (Evaluar modelo).</span><span class="sxs-lookup"><span data-stu-id="bce88-181">To evaluate the two scoring results and compare them, we use an [Evaluate Model][evaluate-model] module.</span></span>  

1. <span data-ttu-id="bce88-182">Busque el módulo [Evaluate Model][evaluate-model] (Evaluar modelo) y arrástrelo al lienzo.</span><span class="sxs-lookup"><span data-stu-id="bce88-182">Find the [Evaluate Model][evaluate-model] module and drag it onto the canvas.</span></span>

2. <span data-ttu-id="bce88-183">Conecte el puerto de salida del módulo [Score Model][score-model] (Puntuar modelo) asociado al modelo del árbol de decisión ampliado al puerto de entrada izquierdo del módulo [Evaluate Model][evaluate-model] (Evaluar modelo).</span><span class="sxs-lookup"><span data-stu-id="bce88-183">Connect the output port of the [Score Model][score-model] module associated with the boosted decision tree model to the left input port of the [Evaluate Model][evaluate-model] module.</span></span>

3. <span data-ttu-id="bce88-184">Conecte el otro módulo [Score Model][score-model] (Puntuar modelo) al puerto de entrada derecho.</span><span class="sxs-lookup"><span data-stu-id="bce88-184">Connect the other [Score Model][score-model] module to the right input port.</span></span>  

    ![Módulo Evaluate Model (Evaluar modelo) conectado][8]

### <a name="run-the-experiment-and-check-the-results"></a><span data-ttu-id="bce88-186">Ejecutar el experimento y comprobar los resultados</span><span class="sxs-lookup"><span data-stu-id="bce88-186">Run the experiment and check the results</span></span>

<span data-ttu-id="bce88-187">Para ejecutar el experimento, haga clic en el botón **EJECUTAR** bajo el lienzo.</span><span class="sxs-lookup"><span data-stu-id="bce88-187">To run the experiment, click the **RUN** button below the canvas.</span></span> <span data-ttu-id="bce88-188">Esto puede tardar unos minutos.</span><span class="sxs-lookup"><span data-stu-id="bce88-188">It may take a few minutes.</span></span> <span data-ttu-id="bce88-189">Aparece un indicador giratorio en cada módulo para indicar que está en ejecución y, cuando el módulo acaba, aparece una marca de verificación de color verde.</span><span class="sxs-lookup"><span data-stu-id="bce88-189">A spinning indicator on each module shows that it's running, and then a green check mark shows when the module is finished.</span></span> <span data-ttu-id="bce88-190">Cuando todos los módulos tengan una marca de verificación, habrá finalizado la ejecución del experimento.</span><span class="sxs-lookup"><span data-stu-id="bce88-190">When all the modules have a check mark, the experiment has finished running.</span></span>

<span data-ttu-id="bce88-191">El experimento debería tener ahora un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="bce88-191">The experiment should now look something like this:</span></span>  

![Evaluating both models][3]

<span data-ttu-id="bce88-193">Para comprobar los resultados, haga clic en el puerto de salida del módulo [Evaluate Model][evaluate-model] (Evaluar modelo) y seleccione **Visualizar**.</span><span class="sxs-lookup"><span data-stu-id="bce88-193">To check the results, click the output port of the [Evaluate Model][evaluate-model] module and select **Visualize**.</span></span>  

<span data-ttu-id="bce88-194">El módulo [Evaluate Model][evaluate-model] (Evaluar modelo) produce un par de curvas y métricas que permiten comparar los resultados de los dos modelos de puntuación.</span><span class="sxs-lookup"><span data-stu-id="bce88-194">The [Evaluate Model][evaluate-model] module produces a pair of curves and metrics that allow you to compare the results of the two scored models.</span></span> <span data-ttu-id="bce88-195">Puede ver los resultados como curvas de características operativas del receptor (ROC), curvas de precisión/exhaustividad o curvas de elevación.</span><span class="sxs-lookup"><span data-stu-id="bce88-195">You can view the results as Receiver Operator Characteristic (ROC) curves, Precision/Recall curves, or Lift curves.</span></span> <span data-ttu-id="bce88-196">También se muestran otros datos como la matriz de confusión y los valores del área bajo la curva (AUC) acumulados, entre otras métricas.</span><span class="sxs-lookup"><span data-stu-id="bce88-196">Additional data displayed includes a confusion matrix, cumulative values for the area under the curve (AUC), and other metrics.</span></span> <span data-ttu-id="bce88-197">También puede cambiar el valor del umbral moviendo el control deslizante a la izquierda o a la derecha, y comprobar cómo afecta esta acción al conjunto de métricas.</span><span class="sxs-lookup"><span data-stu-id="bce88-197">You can change the threshold value by moving the slider left or right and see how it affects the set of metrics.</span></span>  

<span data-ttu-id="bce88-198">A la derecha del gráfico, haga clic en **Scored dataset** (Conjunto de datos puntuados) o en **Scored dataset to compare** (Conjunto de datos puntuados para comparar) con el fin de resaltar la curva asociada y mostrar debajo las métricas asociadas.</span><span class="sxs-lookup"><span data-stu-id="bce88-198">To the right of the graph, click **Scored dataset** or **Scored dataset to compare** to highlight the associated curve and to display the associated metrics below.</span></span> <span data-ttu-id="bce88-199">En la leyenda de las curvas, "Conjunto de datos puntuados" corresponde al puerto de entrada izquierdo del módulo [Evaluate Model][evaluate-model] (Evaluar modelo); en este caso, se trata del modelo del árbol de decisión ampliado.</span><span class="sxs-lookup"><span data-stu-id="bce88-199">In the legend for the curves, "Scored dataset" corresponds to the left input port of the [Evaluate Model][evaluate-model] module - in our case, this is the boosted decision tree model.</span></span> <span data-ttu-id="bce88-200">"Conjunto de datos puntuados para comparar" corresponde al puerto de entrada derecho (el modelo SVM en nuestro caso).</span><span class="sxs-lookup"><span data-stu-id="bce88-200">"Scored dataset to compare" corresponds to the right input port - the SVM model in our case.</span></span> <span data-ttu-id="bce88-201">Al hacer clic en una de estas etiquetas, la curva del modelo correspondiente se resalta y muestra las métricas correspondientes tal y como se muestra en el gráfico siguiente.</span><span class="sxs-lookup"><span data-stu-id="bce88-201">When you click one of these labels, the curve for that model is highlighted and the corresponding metrics are displayed, as shown in the following graphic.</span></span>  

![ROC curves for models][4]

<span data-ttu-id="bce88-203">Si examina estos valores, podrá decidir cuál es el modelo que más se acerca a ofrecerle los resultados que busca.</span><span class="sxs-lookup"><span data-stu-id="bce88-203">By examining these values, you can decide which model is closest to giving you the results you're looking for.</span></span> <span data-ttu-id="bce88-204">Puede volver y repetir el experimento cambiando valores de parámetros en los diferentes modelos.</span><span class="sxs-lookup"><span data-stu-id="bce88-204">You can go back and iterate on your experiment by changing parameter values in the different models.</span></span> 

<span data-ttu-id="bce88-205">La ciencia y el arte de interpretar estos resultados y de ajustar el rendimiento del modelo están fuera del ámbito de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="bce88-205">The science and art of interpreting these results and tuning the model performance is outside the scope of this walkthrough.</span></span> <span data-ttu-id="bce88-206">Para obtener ayuda adicional, puede leer los artículos siguientes:</span><span class="sxs-lookup"><span data-stu-id="bce88-206">For additional help, you might read the following articles:</span></span>
- [<span data-ttu-id="bce88-207">Evaluación del rendimiento de un modelo en Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="bce88-207">How to evaluate model performance in Azure Machine Learning</span></span>](machine-learning-evaluate-model-performance.md)
- [<span data-ttu-id="bce88-208">Cómo elegir parámetros para optimizar los algoritmos de Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="bce88-208">Choose parameters to optimize your algorithms in Azure Machine Learning</span></span>](machine-learning-algorithm-parameters-optimize.md)
- [<span data-ttu-id="bce88-209">Cómo interpretar los resultados del modelo de Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="bce88-209">Interpret model results in Azure Machine Learning</span></span>](machine-learning-interpret-model-results.md)

> [!TIP]
> <span data-ttu-id="bce88-210">Cada vez que ejecute el experimento, se guardará un registro de esa iteración en el Historial de ejecuciones.</span><span class="sxs-lookup"><span data-stu-id="bce88-210">Each time you run the experiment a record of that iteration is kept in the Run History.</span></span> <span data-ttu-id="bce88-211">Puede ver estas iteraciones y volver a cualquiera de ellas haciendo clic en **VER HISTORIAL DE EJECUCIÓN** bajo el lienzo.</span><span class="sxs-lookup"><span data-stu-id="bce88-211">You can view these iterations, and return to any of them, by clicking **VIEW RUN HISTORY** below the canvas.</span></span> <span data-ttu-id="bce88-212">También puede hacer clic en **Prior Run** (Ejecución anterior) en el panel **Propiedades** para volver a la iteración inmediatamente anterior a la que ha abierto.</span><span class="sxs-lookup"><span data-stu-id="bce88-212">You can also click **Prior Run** in the **Properties** pane to return to the iteration immediately preceding the one you have open.</span></span>
> 
> <span data-ttu-id="bce88-213">Puede hacer una copia de cualquier iteración de su experimento si hace clic en **GUARDAR COMO** bajo el lienzo.</span><span class="sxs-lookup"><span data-stu-id="bce88-213">You can make a copy of any iteration of your experiment by clicking **SAVE AS** below the canvas.</span></span> 
> <span data-ttu-id="bce88-214">Utilice las propiedades **Resumen** y **Descripción** para mantener un registro de lo que ha tratado de hacer en las iteraciones del experimento.</span><span class="sxs-lookup"><span data-stu-id="bce88-214">Use the experiment's **Summary** and **Description** properties to keep a record of what you've tried in your experiment iterations.</span></span>
> 
> <span data-ttu-id="bce88-215">Consulte [Administración de iteraciones de experimentos en Estudio de aprendizaje automático de Azure](machine-learning-manage-experiment-iterations.md)para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="bce88-215">For more details, see [Manage experiment iterations in Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span></span>  
> 
> 

- - -
<span data-ttu-id="bce88-216">**Siguiente: [Implementación del servicio web](machine-learning-walkthrough-5-publish-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="bce88-216">**Next: [Deploy the web service](machine-learning-walkthrough-5-publish-web-service.md)**</span></span>

[0]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/train-model-select-column.png
[1]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/experiment-with-train-model.png
[2]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/svm-model-added.png
[3]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/final-experiment.png
[4]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/roc-curves.png
[5]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/normalize-data-select-column.png
[6]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/score-model-connected.png
[7]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/both-score-models-added.png
[8]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/evaluate-model-added.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
