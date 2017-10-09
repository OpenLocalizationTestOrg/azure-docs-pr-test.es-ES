---
title: "Paso 4: Entrenar y evaluar modelos de análisis predictivos de hello | Documentos de Microsoft"
description: "Paso 4 de hello desarrollar un tutorial de solución de predicción: entrenar, puntuarlos y evaluar varios modelos en estudio de aprendizaje automático de Azure."
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
ms.openlocfilehash: d86d7c5ae7524f71fe44d985db67c4618b7965a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-hello-predictive-analytic-models"></a><span data-ttu-id="4a5f4-103">Paso 4 del tutorial: Entrenar y evaluar modelos de análisis predictivos de Hola</span><span class="sxs-lookup"><span data-stu-id="4a5f4-103">Walkthrough Step 4: Train and evaluate hello predictive analytic models</span></span>
<span data-ttu-id="4a5f4-104">Este tema contiene el cuarto paso del tutorial de hello, de hello [desarrollar una solución de análisis predictivos en aprendizaje automático de Azure](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="4a5f4-104">This topic contains hello fourth step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="4a5f4-105">Creación de un área de trabajo de Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="4a5f4-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="4a5f4-106">Carga de los datos existentes</span><span class="sxs-lookup"><span data-stu-id="4a5f4-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="4a5f4-107">Crear un experimento nuevo</span><span class="sxs-lookup"><span data-stu-id="4a5f4-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. <span data-ttu-id="4a5f4-108">**Entrenar y evaluar modelos de Hola**</span><span class="sxs-lookup"><span data-stu-id="4a5f4-108">**Train and evaluate hello models**</span></span>
5. [<span data-ttu-id="4a5f4-109">Implementar el servicio Web de Hola</span><span class="sxs-lookup"><span data-stu-id="4a5f4-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="4a5f4-110">Acceder al servicio Web Hola</span><span class="sxs-lookup"><span data-stu-id="4a5f4-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="4a5f4-111">Una de las ventajas de hello del uso de estudio de aprendizaje automático de Azure para crear modelos de aprendizaje automático está Hola capacidad tootry más de un tipo de modelo a la vez en un experimento único y comparar resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-111">One of hello benefits of using Azure Machine Learning Studio for creating machine learning models is hello ability tootry more than one type of model at a time in a single experiment and compare hello results.</span></span> <span data-ttu-id="4a5f4-112">Este tipo de experimentación le ayuda a encontrar Hola mejor solución para su problema.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-112">This type of experimentation helps you find hello best solution for your problem.</span></span>

<span data-ttu-id="4a5f4-113">En el experimento de hello desarrollamos en este tutorial, se creará dos tipos diferentes de modelos y, a continuación, comparar su puntuación toodecide resultados qué algoritmo queremos toouse en nuestro experimento final.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-113">In hello experiment we're developing in this walkthrough, we'll create two different types of models and then compare their scoring results toodecide which algorithm we want toouse in our final experiment.</span></span>  

<span data-ttu-id="4a5f4-114">Existen varios modelos entre los que se puede elegir.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-114">There are various models we could choose from.</span></span> <span data-ttu-id="4a5f4-115">modelos de hello toosee disponibles, expanda hello **aprendizaje automático** nodo en la paleta de módulo de hello y, a continuación, expanda **inicializar modelo** y nodos de hello situado debajo de él.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-115">toosee hello models available, expand hello **Machine Learning** node in hello module palette, and then expand **Initialize Model** and hello nodes beneath it.</span></span> <span data-ttu-id="4a5f4-116">Para fines de Hola de este experimento, se seleccionará hello [máquina de vectores de soporte de dos clases] [ two-class-support-vector-machine] (SVM) hello y [árbol de decisión impulsado de dos clases] [ two-class-boosted-decision-tree] módulos.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-116">For hello purposes of this experiment, we'll select hello [Two-Class Support Vector Machine][two-class-support-vector-machine] (SVM) and hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] modules.</span></span>    

> [!TIP]
> <span data-ttu-id="4a5f4-117">tooget decidir qué algoritmo de aprendizaje automático mejor se adapte a problema concreto de Hola que está tratando de toosolve, consulte [cómo toochoose algoritmos de aprendizaje automático de Microsoft Azure](machine-learning-algorithm-choice.md).</span><span class="sxs-lookup"><span data-stu-id="4a5f4-117">tooget help deciding which Machine Learning algorithm best suits hello particular problem you're trying toosolve, see [How toochoose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span></span>
> 
> 

## <a name="train-hello-models"></a><span data-ttu-id="4a5f4-118">Entrenar modelos de Hola</span><span class="sxs-lookup"><span data-stu-id="4a5f4-118">Train hello models</span></span>

<span data-ttu-id="4a5f4-119">Vamos a agregar ambos hello [árbol de decisión impulsado de dos clases] [ two-class-boosted-decision-tree] módulo y [máquina de vectores de soporte de dos clases] [ two-class-support-vector-machine] módulo en este experimentar.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-119">We'll add both hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module and [Two-Class Support Vector Machine][two-class-support-vector-machine] module in this experiment.</span></span>

### <a name="two-class-boosted-decision-tree"></a><span data-ttu-id="4a5f4-120">Árbol de decisión ampliado de dos clases</span><span class="sxs-lookup"><span data-stu-id="4a5f4-120">Two-Class Boosted Decision Tree</span></span>

<span data-ttu-id="4a5f4-121">En primer lugar, vamos a configurar el modelo de árbol de decisión impulsado de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-121">First, let's set up hello boosted decision tree model.</span></span>

1. <span data-ttu-id="4a5f4-122">Buscar hello [árbol de decisión impulsado de dos clases] [ two-class-boosted-decision-tree] módulo en la paleta de módulo de Hola y lo arrastra al lienzo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-122">Find hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module in hello module palette and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="4a5f4-123">Buscar hello [entrenar modelo] [ train-model] módulo, arrástrelo al lienzo de Hola y, a continuación, conecte la salida de hello de hello [árbol de decisión impulsado de dos clases] [ two-class-boosted-decision-tree]toohello módulo deja el puerto de entrada de hello [entrenar modelo] [ train-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-123">Find hello [Train Model][train-model] module, drag it onto hello canvas, and then connect hello output of hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module toohello left input port of hello [Train Model][train-model] module.</span></span>
   
   <span data-ttu-id="4a5f4-124">Hola [árbol de decisión impulsado de dos clases] [ two-class-boosted-decision-tree] módulo inicializa modelo genérico de hello, y [entrenar modelo] [ train-model] utiliza datos de entrenamiento modelo de hello tootrain.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-124">hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module initializes hello generic model, and [Train Model][train-model] uses training data tootrain hello model.</span></span> 

3. <span data-ttu-id="4a5f4-125">Conecte Hola salida izquierdo de la izquierda de hello [ejecutar Script de R] [ execute-r-script] puerto de Hola de entrada de módulo toohello derecha [entrenar modelo] [ train-model] módulo (se decidió en [paso 3](machine-learning-walkthrough-3-create-new-experiment.md) de tutorial toouse Hola los datos procedentes de la parte izquierda de módulo de dividir datos de hello para el entrenamiento de hello).</span><span class="sxs-lookup"><span data-stu-id="4a5f4-125">Connect hello left output of hello left [Execute R Script][execute-r-script] module toohello right input port of hello [Train Model][train-model] module (we decided in [Step 3](machine-learning-walkthrough-3-create-new-experiment.md) of this walkthrough toouse hello data coming from hello left side of hello Split Data module for training).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="4a5f4-126">No se necesita dos entradas de hello y otro de salidas de Hola de hello [ejecutar Script de R] [ execute-r-script] módulo para este experimento, por lo que podemos o dejarlos adjuntas.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-126">We don't need two of hello inputs and one of hello outputs of hello [Execute R Script][execute-r-script] module for this experiment, so we can leave them unattached.</span></span> 
   > 
   > 

<span data-ttu-id="4a5f4-127">Esta parte del experimento de hello ahora es algo parecido a esto:</span><span class="sxs-lookup"><span data-stu-id="4a5f4-127">This portion of hello experiment now looks something like this:</span></span>  

![Training a model][1]

<span data-ttu-id="4a5f4-129">Ahora necesitamos hello tootell [entrenar modelo] [ train-model] módulo que queremos que cada valor de riesgo de crédito Hola modelo toopredict Hola.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-129">Now we need tootell hello [Train Model][train-model] module that we want hello model toopredict hello Credit Risk value.</span></span>

1. <span data-ttu-id="4a5f4-130">Seleccione hello [entrenar modelo] [ train-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-130">Select hello [Train Model][train-model] module.</span></span> <span data-ttu-id="4a5f4-131">Hola **propiedades** panel, haga clic en **selector de columna de inicio**.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-131">In hello **Properties** pane, click **Launch column selector**.</span></span>

2. <span data-ttu-id="4a5f4-132">Hola **seleccionar una sola columna** cuadro de diálogo, escriba "riesgo de crédito" en el campo de búsqueda de hello en **columnas disponibles**, seleccione "Riesgo de crédito" a continuación y haga clic en el botón de flecha derecha de hello ( **>** ) toomove "Del crédito riesgo" demasiado**columnas seleccionadas**.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-132">In hello **Select a single column** dialog, type "credit risk" in hello search field under **Available Columns**, select "Credit risk" below, and click hello right arrow button (**>**) toomove "Credit risk" too**Selected Columns**.</span></span> 

    ![Seleccionar columna de riesgo del crédito de hello para el módulo entrenar modelo de Hola][0]

3. <span data-ttu-id="4a5f4-134">Haga clic en hello **Aceptar** marca de verificación.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-134">Click hello **OK** check mark.</span></span>

### <a name="two-class-support-vector-machine"></a><span data-ttu-id="4a5f4-135">Máquina de vectores de soporte de dos clases</span><span class="sxs-lookup"><span data-stu-id="4a5f4-135">Two-Class Support Vector Machine</span></span>

<span data-ttu-id="4a5f4-136">A continuación, configuramos modelo SVM de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-136">Next, we set up hello SVM model.</span></span>  

<span data-ttu-id="4a5f4-137">En primer lugar, una breve explicación sobre SVM.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-137">First, a little explanation about SVM.</span></span> <span data-ttu-id="4a5f4-138">Los árboles de decisión ampliados funcionan bien con características de todo tipo.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-138">Boosted decision trees work well with features of any type.</span></span> <span data-ttu-id="4a5f4-139">Sin embargo, puesto que el módulo SVM de hello genera un clasificador lineal, modelo de Hola que genera tiene error de prueba recomendado hello cuando todas las características numéricas tienen Hola misma escala.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-139">However, since hello SVM module generates a linear classifier, hello model that it generates has hello best test error when all numeric features have hello same scale.</span></span> <span data-ttu-id="4a5f4-140">tooconvert numérico todas las características toohello mismo escalar, se usa una transformación de "Tanh" (con hello [Normalizar datos] [ normalize-data] módulo).</span><span class="sxs-lookup"><span data-stu-id="4a5f4-140">tooconvert all numeric features toohello same scale, we use a "Tanh" transformation (with hello [Normalize Data][normalize-data] module).</span></span> <span data-ttu-id="4a5f4-141">Esto transforma los números en el intervalo [0,1] Hola.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-141">This transforms our numbers into hello [0,1] range.</span></span> <span data-ttu-id="4a5f4-142">módulo SVM de Hello convierte la cadena características toocategorical características y, a continuación, toobinary 0/1, por lo que no necesita transformar toomanually funciones de cadena.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-142">hello SVM module converts string features toocategorical features and then toobinary 0/1 features, so we don't need toomanually transform string features.</span></span> <span data-ttu-id="4a5f4-143">Además, no es aconsejable columna riesgo del crédito de hello tootransform (columna 21): es numérico, pero es valor Hola nos estamos entrenamiento Hola toopredict de modelo, por lo que necesitamos tooleave por su cuenta.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-143">Also, we don't want tootransform hello Credit Risk column (column 21) - it's numeric, but it's hello value we're training hello model toopredict, so we need tooleave it alone.</span></span>  

<span data-ttu-id="4a5f4-144">tooset modelo de SVM de hello, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="4a5f4-144">tooset up hello SVM model, do hello following:</span></span>

1. <span data-ttu-id="4a5f4-145">Buscar hello [máquina de vectores de soporte de dos clases] [ two-class-support-vector-machine] módulo en la paleta de módulo de Hola y lo arrastra al lienzo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-145">Find hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module in hello module palette and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="4a5f4-146">Menú contextual hello [entrenar modelo] [ train-model] módulo, seleccione **copia**y, a continuación, haga clic en el lienzo de Hola y seleccione **pegar**.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-146">Right-click hello [Train Model][train-model] module, select **Copy**, and then right-click hello canvas and select **Paste**.</span></span> <span data-ttu-id="4a5f4-147">Hola copia de hello [entrenar modelo] [ train-model] módulo tiene Hola misma selección de columna como Hola original.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-147">hello copy of hello [Train Model][train-model] module has hello same column selection as hello original.</span></span>

3. <span data-ttu-id="4a5f4-148">Conecte la salida de hello de hello [máquina de vectores de soporte de dos clases] [ two-class-support-vector-machine] toohello módulo izquierdo puerto de entrada de hello segundo [entrenar modelo] [ train-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-148">Connect hello output of hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module toohello left input port of hello second [Train Model][train-model] module.</span></span>

4. <span data-ttu-id="4a5f4-149">Buscar hello [Normalizar datos] [ normalize-data] módulo y lo arrastra al lienzo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-149">Find hello [Normalize Data][normalize-data] module and drag it onto hello canvas.</span></span>

5. <span data-ttu-id="4a5f4-150">Conecte Hola salida izquierdo de la izquierda de hello [ejecutar Script de R] [ execute-r-script] entrada toohello de módulo de este módulo (Observe que Hola de puerto de salida de un módulo puede ser toomore conectado a un módulo de otro).</span><span class="sxs-lookup"><span data-stu-id="4a5f4-150">Connect hello left output of hello left [Execute R Script][execute-r-script] module toohello input of this module (notice that hello output port of a module may be connected toomore than one other module).</span></span>

6. <span data-ttu-id="4a5f4-151">Conectar Hola dejado el puerto de salida de hello [Normalizar datos] [ normalize-data] módulo toohello derecha de entrada de puerto de hello en segundo lugar [entrenar modelo] [ train-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-151">Connect hello left output port of hello [Normalize Data][normalize-data] module toohello right input port of hello second [Train Model][train-model] module.</span></span>

<span data-ttu-id="4a5f4-152">Esta parte de nuestro experimento debería tener ahora un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="4a5f4-152">This portion of our experiment should now look something like this:</span></span>  

![Modelo de entrenamiento Hola segundo][2]  

<span data-ttu-id="4a5f4-154">Configurar ahora hello [Normalizar datos] [ normalize-data] módulo:</span><span class="sxs-lookup"><span data-stu-id="4a5f4-154">Now configure hello [Normalize Data][normalize-data] module:</span></span>

1. <span data-ttu-id="4a5f4-155">Haga clic en hello tooselect [Normalizar datos] [ normalize-data] módulo.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-155">Click tooselect hello [Normalize Data][normalize-data] module.</span></span> <span data-ttu-id="4a5f4-156">Hola **propiedades** panel, seleccione **Tanh** para hello **método de transformación** parámetro.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-156">In hello **Properties** pane, select **Tanh** for hello **Transformation method** parameter.</span></span>

2. <span data-ttu-id="4a5f4-157">Haga clic en **selector de columna de inicio**, seleccione "No hay columnas" para **comenzar con**, seleccione **Include** en la primera lista desplegable de hello, seleccione **el tipo de columna**en Hola segunda lista desplegable y seleccione **numérico** en lista desplegable terceros de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-157">Click **Launch column selector**, select "No columns" for **Begin With**, select **Include** in hello first dropdown, select **column type** in hello second dropdown, and select **Numeric** in hello third dropdown.</span></span> <span data-ttu-id="4a5f4-158">Especifica que todas las columnas numéricas de hello (y numérico único) se transforman.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-158">This specifies that all hello numeric columns (and only numeric) are transformed.</span></span>

3. <span data-ttu-id="4a5f4-159">Haga clic en Hola toohello de signo más (+) derecha de esta fila - Esto crea una fila de listas desplegables.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-159">Click hello plus sign (+) toohello right of this row - this creates a row of dropdowns.</span></span> <span data-ttu-id="4a5f4-160">Seleccione **excluir** en la primera lista desplegable de hello, seleccione **nombres de columna** en Hola segunda lista desplegable y escriba "Riesgo de crédito" en el campo de texto hello.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-160">Select **Exclude** in hello first dropdown, select **column names** in hello second dropdown, and enter "Credit risk" in hello text field.</span></span> <span data-ttu-id="4a5f4-161">Esto especifica que se debe omitir esa columna de riesgo de crédito hello (necesitamos toodo esto porque esta columna es numérica y así se transformaría si no excluirla).</span><span class="sxs-lookup"><span data-stu-id="4a5f4-161">This specifies that hello Credit Risk column should be ignored (we need toodo this because this column is numeric and so would be transformed if we didn't exclude it).</span></span>

4. <span data-ttu-id="4a5f4-162">Haga clic en hello **Aceptar** marca de verificación.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-162">Click hello **OK** check mark.</span></span>  

    ![Seleccione las columnas para el módulo de hello Normalizar datos][5]

<span data-ttu-id="4a5f4-164">Hola [Normalizar datos] [ normalize-data] módulo ahora es conjunto tooperform una transformación Tanh en todas las columnas numéricas excepto Hola riesgo de crédito.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-164">hello [Normalize Data][normalize-data] module is now set tooperform a Tanh transformation on all numeric columns except for hello Credit Risk column.</span></span>  

## <a name="score-and-evaluate-hello-models"></a><span data-ttu-id="4a5f4-165">Puntuar y evaluar modelos de Hola</span><span class="sxs-lookup"><span data-stu-id="4a5f4-165">Score and evaluate hello models</span></span>

<span data-ttu-id="4a5f4-166">Usamos Hola comprobación de datos que se distinguiendo entre hello [dividir datos] [ split] tooscore módulo nuestros modelos entrenados.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-166">We use hello testing data that was separated out by hello [Split Data][split] module tooscore our trained models.</span></span> <span data-ttu-id="4a5f4-167">A continuación, se puedan comparar resultados de Hola de hello dos modelos toosee que genera los mejores resultados.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-167">We can then compare hello results of hello two models toosee which generated better results.</span></span>  

### <a name="add-hello-score-model-modules"></a><span data-ttu-id="4a5f4-168">Agregar módulos de modelo de puntuación de Hola</span><span class="sxs-lookup"><span data-stu-id="4a5f4-168">Add hello Score Model modules</span></span>

1. <span data-ttu-id="4a5f4-169">Buscar hello [puntuar modelo] [ score-model] módulo y lo arrastra al lienzo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-169">Find hello [Score Model][score-model] module and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="4a5f4-170">Conectar hello [entrenar modelo] [ train-model] módulo que se ha conectado toohello [árbol de decisión impulsado de dos clases] [ two-class-boosted-decision-tree] entrada izquierda de módulo toohello puerto de hello [puntuar modelo] [ score-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-170">Connect hello [Train Model][train-model] module that's connected toohello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module toohello left input port of hello [Score Model][score-model] module.</span></span>

3. <span data-ttu-id="4a5f4-171">Conectar derecha hello [ejecutar Script de R] [ execute-r-script] puerto de Hola de entrada de módulo (nuestros datos de prueba) toohello derecha [puntuar modelo] [ score-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-171">Connect hello right [Execute R Script][execute-r-script] module (our testing data) toohello right input port of hello [Score Model][score-model] module.</span></span>

    ![Módulo Score Model (Puntuar modelo) conectado][6]
   
   <span data-ttu-id="4a5f4-173">Hola [puntuar modelo] [ score-model] módulo ahora puede aprovechar la información de crédito de Hola de hello datos, se debe ejecutar utilizando el modelo de hello, de prueba y comparar las predicciones de hello genera el modelo de hello con hello real riesgo de crédito columna de datos de prueba de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-173">hello [Score Model][score-model] module can now take hello credit information from hello testing data, run it through hello model, and compare hello predictions hello model generates with hello actual credit risk column in hello testing data.</span></span>

4. <span data-ttu-id="4a5f4-174">Copie y pegue hello [puntuar modelo] [ score-model] toocreate módulo una segunda copia.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-174">Copy and paste hello [Score Model][score-model] module toocreate a second copy.</span></span>

5. <span data-ttu-id="4a5f4-175">Conecte la salida de hello de modelo SVM de hello (es decir, el puerto de hello de la salida de hello [entrenar modelo] [ train-model] módulo que se ha conectado toohello [máquina de vectores de soporte de dos clases] [ two-class-support-vector-machine] módulo) toohello de entrada de puerto de hello en segundo lugar [puntuar modelo] [ score-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-175">Connect hello output of hello SVM model (that is, hello output port of hello [Train Model][train-model] module that's connected toohello [Two-Class Support Vector Machine][two-class-support-vector-machine] module) toohello input port of hello second [Score Model][score-model] module.</span></span>

6. <span data-ttu-id="4a5f4-176">Para el modelo de SVM de hello, tenemos toodo Hola los mismos datos de prueba de toohello de transformación igual que hicimos toohello datos de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-176">For hello SVM model, we have toodo hello same transformation toohello test data as we did toohello training data.</span></span> <span data-ttu-id="4a5f4-177">Por lo tanto, copiar y pegar hello [Normalizar datos] [ normalize-data] toocreate módulo una segunda copia y conéctelo derecha toohello [ejecutar Script de R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-177">So copy and paste hello [Normalize Data][normalize-data] module toocreate a second copy and connect it toohello right [Execute R Script][execute-r-script] module.</span></span>

7. <span data-ttu-id="4a5f4-178">Conecte la salida de izquierdo de Hola de hello en segundo lugar [Normalizar datos] [ normalize-data] módulo toohello derecha de entrada de puerto de hello en segundo lugar [puntuar modelo] [ score-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-178">Connect hello left output of hello second [Normalize Data][normalize-data] module toohello right input port of hello second [Score Model][score-model] module.</span></span>

    ![Ambos módulos Score Model (Puntuar modelo) conectados][7]

### <a name="add-hello-evaluate-model-module"></a><span data-ttu-id="4a5f4-180">Agregar módulo de hello evaluar modelo</span><span class="sxs-lookup"><span data-stu-id="4a5f4-180">Add hello Evaluate Model module</span></span>

<span data-ttu-id="4a5f4-181">tooevaluate Hola dos resultados de puntuación y compararlos, usamos un [evaluar modelo] [ evaluate-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-181">tooevaluate hello two scoring results and compare them, we use an [Evaluate Model][evaluate-model] module.</span></span>  

1. <span data-ttu-id="4a5f4-182">Buscar hello [evaluar modelo] [ evaluate-model] módulo y lo arrastra al lienzo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-182">Find hello [Evaluate Model][evaluate-model] module and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="4a5f4-183">Conecte los puertos de salida de hello de hello [puntuar modelo] [ score-model] módulo asociado Hola impulsado puerto de hello de entrada izquierda toohello de modelo de árbol de decisión [evaluar modelo] [ evaluate-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-183">Connect hello output port of hello [Score Model][score-model] module associated with hello boosted decision tree model toohello left input port of hello [Evaluate Model][evaluate-model] module.</span></span>

3. <span data-ttu-id="4a5f4-184">Conectar Hola otro [puntuar modelo] [ score-model] puerto de entrada de módulo toohello derecha.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-184">Connect hello other [Score Model][score-model] module toohello right input port.</span></span>  

    ![Módulo Evaluate Model (Evaluar modelo) conectado][8]

### <a name="run-hello-experiment-and-check-hello-results"></a><span data-ttu-id="4a5f4-186">Ejecute el experimento de Hola y comprobar los resultados de Hola</span><span class="sxs-lookup"><span data-stu-id="4a5f4-186">Run hello experiment and check hello results</span></span>

<span data-ttu-id="4a5f4-187">toorun Hola experimento, haga clic en hello **ejecutar** botón a continuación lienzo Hola.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-187">toorun hello experiment, click hello **RUN** button below hello canvas.</span></span> <span data-ttu-id="4a5f4-188">Esto puede tardar unos minutos.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-188">It may take a few minutes.</span></span> <span data-ttu-id="4a5f4-189">Se muestra un indicador de giro en cada módulo que se está ejecutando y, a continuación, una marca de verificación verde muestra cuando finalice el módulo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-189">A spinning indicator on each module shows that it's running, and then a green check mark shows when hello module is finished.</span></span> <span data-ttu-id="4a5f4-190">Cuando todos los módulos de hello tienen una marca de verificación, experimento Hola ha terminado de ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-190">When all hello modules have a check mark, hello experiment has finished running.</span></span>

<span data-ttu-id="4a5f4-191">el experimento de Hello ahora debería ser similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="4a5f4-191">hello experiment should now look something like this:</span></span>  

![Evaluating both models][3]

<span data-ttu-id="4a5f4-193">resultados de hello toocheck, haga clic en puerto de salida de hello de hello [evaluar modelo] [ evaluate-model] módulo y seleccione **visualizar**.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-193">toocheck hello results, click hello output port of hello [Evaluate Model][evaluate-model] module and select **Visualize**.</span></span>  

<span data-ttu-id="4a5f4-194">Hola [evaluar modelo] [ evaluate-model] módulo genera un par de curvas y las métricas que le permiten resultados de Hola de toocompare de hello dos modelos de puntuación.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-194">hello [Evaluate Model][evaluate-model] module produces a pair of curves and metrics that allow you toocompare hello results of hello two scored models.</span></span> <span data-ttu-id="4a5f4-195">Puede ver los resultados de hello como característica de operador de receptor (ROC) curvas, curvas de precisión/recuperación o curvas de elevación.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-195">You can view hello results as Receiver Operator Characteristic (ROC) curves, Precision/Recall curves, or Lift curves.</span></span> <span data-ttu-id="4a5f4-196">Datos adicionales que se muestra incluyen una matriz de confusión, valores acumulativos de área de hello en curva de hello (AUC) y otras métricas.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-196">Additional data displayed includes a confusion matrix, cumulative values for hello area under hello curve (AUC), and other metrics.</span></span> <span data-ttu-id="4a5f4-197">Puede cambiar el valor de umbral de Hola por móvil control deslizante izquierdo o derecho de Hola y ver cómo afecta al conjunto de Hola de métricas.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-197">You can change hello threshold value by moving hello slider left or right and see how it affects hello set of metrics.</span></span>  

<span data-ttu-id="4a5f4-198">toohello derecha del gráfico de hello, haga clic en **conjunto de datos puntuado** o **puntúan toocompare de conjunto de datos** toohighlight Hola asociado curva y toodisplay Hola asociados métricas a continuación.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-198">toohello right of hello graph, click **Scored dataset** or **Scored dataset toocompare** toohighlight hello associated curve and toodisplay hello associated metrics below.</span></span> <span data-ttu-id="4a5f4-199">En la leyenda de Hola para curvas de hello, "Conjunto de datos puntuado" corresponde toohello dejado el puerto de entrada de hello [evaluar modelo] [ evaluate-model] módulo - en nuestro caso, este es el modelo de árbol de decisión impulsado de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-199">In hello legend for hello curves, "Scored dataset" corresponds toohello left input port of hello [Evaluate Model][evaluate-model] module - in our case, this is hello boosted decision tree model.</span></span> <span data-ttu-id="4a5f4-200">"Toocompare de conjunto de datos de puntuación" corresponde toohello puerto de entrada derecha - modelo SVM de hello en nuestro caso.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-200">"Scored dataset toocompare" corresponds toohello right input port - hello SVM model in our case.</span></span> <span data-ttu-id="4a5f4-201">Al hacer clic en una de estas etiquetas, se resalta la curva de Hola para dicho modelo y se muestran las métricas de hello correspondiente, tal y como se muestra en el siguiente gráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-201">When you click one of these labels, hello curve for that model is highlighted and hello corresponding metrics are displayed, as shown in hello following graphic.</span></span>  

![ROC curves for models][4]

<span data-ttu-id="4a5f4-203">Mediante el examen de estos valores, puede decidir qué modelo es más cercano toogiving que Hola resultados que está buscando.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-203">By examining these values, you can decide which model is closest toogiving you hello results you're looking for.</span></span> <span data-ttu-id="4a5f4-204">Puede volver atrás y repita el experimento cambiando los valores de parámetro en modelos diferentes de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-204">You can go back and iterate on your experiment by changing parameter values in hello different models.</span></span> 

<span data-ttu-id="4a5f4-205">Hola y ciencia de interpretar estos resultados y optimizar el rendimiento del modelo hello es ámbito de hello fuera de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-205">hello science and art of interpreting these results and tuning hello model performance is outside hello scope of this walkthrough.</span></span> <span data-ttu-id="4a5f4-206">Para obtener ayuda adicional, puede leer Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="4a5f4-206">For additional help, you might read hello following articles:</span></span>
- [<span data-ttu-id="4a5f4-207">¿Cómo tooevaluate modelo rendimiento aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="4a5f4-207">How tooevaluate model performance in Azure Machine Learning</span></span>](machine-learning-evaluate-model-performance.md)
- [<span data-ttu-id="4a5f4-208">Elegir parámetros toooptimize sus algoritmos de aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="4a5f4-208">Choose parameters toooptimize your algorithms in Azure Machine Learning</span></span>](machine-learning-algorithm-parameters-optimize.md)
- [<span data-ttu-id="4a5f4-209">Cómo interpretar los resultados del modelo de Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4a5f4-209">Interpret model results in Azure Machine Learning</span></span>](machine-learning-interpret-model-results.md)

> [!TIP]
> <span data-ttu-id="4a5f4-210">Cada vez que ejecute el experimento de hello un registro de esa iteración se mantiene en hello historial de ejecución.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-210">Each time you run hello experiment a record of that iteration is kept in hello Run History.</span></span> <span data-ttu-id="4a5f4-211">Puede ver estas iteraciones y devolver tooany de ellos, haciendo clic en **ver el historial de ejecución** por debajo del lienzo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-211">You can view these iterations, and return tooany of them, by clicking **VIEW RUN HISTORY** below hello canvas.</span></span> <span data-ttu-id="4a5f4-212">También puede hacer clic en **ejecutar anterior** en hello **propiedades** Hola de iteración de panel tooreturn toohello inmediatamente anterior a uno que tenga abiertos.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-212">You can also click **Prior Run** in hello **Properties** pane tooreturn toohello iteration immediately preceding hello one you have open.</span></span>
> 
> <span data-ttu-id="4a5f4-213">Puede realizar una copia de alguna iteración del experimento, haga clic en **SAVE AS** por debajo del lienzo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-213">You can make a copy of any iteration of your experiment by clicking **SAVE AS** below hello canvas.</span></span> 
> <span data-ttu-id="4a5f4-214">Usar del experimento de hello **resumen** y **descripción** propiedades tookeep un registro de lo que probó en las iteraciones de experimento.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-214">Use hello experiment's **Summary** and **Description** properties tookeep a record of what you've tried in your experiment iterations.</span></span>
> 
> <span data-ttu-id="4a5f4-215">Consulte [Administración de iteraciones de experimentos en Estudio de aprendizaje automático de Azure](machine-learning-manage-experiment-iterations.md)para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="4a5f4-215">For more details, see [Manage experiment iterations in Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span></span>  
> 
> 

- - -
<span data-ttu-id="4a5f4-216">**Siguiente: [implementar el servicio web de Hola](machine-learning-walkthrough-5-publish-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="4a5f4-216">**Next: [Deploy hello web service](machine-learning-walkthrough-5-publish-web-service.md)**</span></span>

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
