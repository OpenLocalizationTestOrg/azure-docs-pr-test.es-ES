---
title: "aaaA experimento sencillo en estudio de aprendizaje automático | Documentos de Microsoft"
description: "Este tutorial de aprendizaje automático le guiará a través de un sencillo experimento de ciencia de datos. Se podrá predecir precio Hola de un automóvil con un algoritmo de regresión."
keywords: "experimento,regresión lineal,algoritmos de aprendizaje automático,tutorial de aprendizaje automático,técnicas de modelado predictivo,experimento de ciencia de datos"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b6176bb2-3bb6-4ebf-84d1-3598ee6e01c6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: fb215851d380acf7d0f4934a426283369f9c4ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-tutorial-create-your-first-data-science-experiment-in-azure-machine-learning-studio"></a><span data-ttu-id="95488-105">Tutorial de aprendizaje automático: creación del primer experimento de ciencia de datos en Estudio de aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="95488-105">Machine learning tutorial: Create your first data science experiment in Azure Machine Learning Studio</span></span>

<span data-ttu-id="95488-106">Si nunca ha usado **Azure Machine Learning Studio** antes, este tutorial le ayudará.</span><span class="sxs-lookup"><span data-stu-id="95488-106">If you've never used **Azure Machine Learning Studio** before, this tutorial is for you.</span></span>

<span data-ttu-id="95488-107">En este tutorial, le mostraremos cómo toouse Studio para hello es la primera vez toocreate un experimento de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="95488-107">In this tutorial, we'll walk through how toouse Studio for hello first time toocreate a machine learning experiment.</span></span> <span data-ttu-id="95488-108">el experimento de Hello probará un modelo analítico que predice el precio de Hola de un automóvil en función de diferentes variables como marca y especificaciones técnicas.</span><span class="sxs-lookup"><span data-stu-id="95488-108">hello experiment will test an analytical model that predicts hello price of an automobile based on different variables such as make and technical specifications.</span></span>

> [!NOTE]
> <span data-ttu-id="95488-109">Este tutorial muestra conceptos básicos de Hola de módulos de cómo toodrag y colocar en el experimento, conéctelos, ejecutar el experimento de Hola y examine los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="95488-109">This tutorial shows you hello basics of how toodrag-and-drop modules onto your experiment, connect them together, run hello experiment, and look at hello results.</span></span> <span data-ttu-id="95488-110">No entraremos toodiscuss Hola tema general de aprendizaje automático o cómo tooselect y uso Hola 100 + datos y algoritmos manipulación módulos integrados incluidos en Studio.</span><span class="sxs-lookup"><span data-stu-id="95488-110">We're not going toodiscuss hello general topic of machine learning or how tooselect and use hello 100+ built-in algorithms and data manipulation modules included in Studio.</span></span>
>
><span data-ttu-id="95488-111">Si es nuevo aprendizaje toomachine, Hola serie de vídeos [ciencia de datos para principiantes](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) podría ser un buen lugar toostart.</span><span class="sxs-lookup"><span data-stu-id="95488-111">If you're new toomachine learning, hello video series [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) might be a good place toostart.</span></span> <span data-ttu-id="95488-112">Esta serie de vídeos es un aprendizaje de toomachine introducción excelente con conceptos y lenguaje cotidiano.</span><span class="sxs-lookup"><span data-stu-id="95488-112">This video series is a great introduction toomachine learning using everyday language and concepts.</span></span>
>
><span data-ttu-id="95488-113">Si está familiarizado con el aprendizaje automático, pero desea obtener información más general sobre estudio de aprendizaje automático y contiene los algoritmos de aprendizaje de automático de hello, aquí tiene algunos recursos buena:</span><span class="sxs-lookup"><span data-stu-id="95488-113">If you're familiar with machine learning, but you're looking for more general information about Machine Learning Studio, and hello machine learning algorithms it contains, here are some good resources:</span></span>
>
- [<span data-ttu-id="95488-114">¿Qué es Estudio de aprendizaje automático?</span><span class="sxs-lookup"><span data-stu-id="95488-114">What is Machine Learning Studio?</span></span>](machine-learning-what-is-ml-studio.md) <span data-ttu-id="95488-115">- Esta es una descripción de alto nivel de Studio.</span><span class="sxs-lookup"><span data-stu-id="95488-115">- This is a high-level overview of Studio.</span></span>
- <span data-ttu-id="95488-116">[Aspectos básicos con ejemplos de algoritmo de aprendizaje máquina](machine-learning-basics-infographic-with-algorithm-examples.md) -este infografía es útil si desea más información acerca de los distintos tipos de algoritmos de aprendizaje automático incluidos con estudio de aprendizaje automático de hello toolearn.</span><span class="sxs-lookup"><span data-stu-id="95488-116">[Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md) - This infographic is useful if you want toolearn more about hello different types of machine learning algorithms included with Machine Learning Studio.</span></span>
- <span data-ttu-id="95488-117">[Guía de aprendizaje de máquina](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) -esta guía ofrece información similar como hello infografía anterior, pero en un formato interactivo.</span><span class="sxs-lookup"><span data-stu-id="95488-117">[Machine Learning Guide](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) - This guide covers similar information as hello infographic above, but in an interactive format.</span></span>
- <span data-ttu-id="95488-118">[Equipos de hoja de referencia de algoritmo de aprendizaje](machine-learning-algorithm-cheat-sheet.md) y [cómo toochoose algoritmos de aprendizaje automático de Microsoft Azure](machine-learning-algorithm-choice.md) -este póster descargable y artículo complementario describe los algoritmos de Studio hello en profundidad.</span><span class="sxs-lookup"><span data-stu-id="95488-118">[Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md) and [How toochoose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md) - This downloadable poster and accompanying article discuss hello Studio algorithms in depth.</span></span>
- <span data-ttu-id="95488-119">[Estudio de aprendizaje automático: Algoritmo y ayuda del módulo](https://msdn.microsoft.com/library/azure/dn905974.aspx) -se trata de referencia completa de Hola para todos los módulos de estudio, incluidos los algoritmos de aprendizaje automático,</span><span class="sxs-lookup"><span data-stu-id="95488-119">[Machine Learning Studio: Algorithm and Module Help](https://msdn.microsoft.com/library/azure/dn905974.aspx) - This is hello complete reference for all Studio modules, including machine learning algorithms,</span></span>

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-does-machine-learning-studio-help"></a><span data-ttu-id="95488-120">¿Cómo funciona la ayuda de Estudio de aprendizaje automático?</span><span class="sxs-lookup"><span data-stu-id="95488-120">How does Machine Learning Studio help?</span></span>

<span data-ttu-id="95488-121">Estudio de aprendizaje automático resulta fácil tooset seguridad un experimento con módulos de arrastrar y colocar preprogramados con las técnicas de modelado de predicción.</span><span class="sxs-lookup"><span data-stu-id="95488-121">Machine Learning Studio makes it easy tooset up an experiment using drag-and-drop modules preprogrammed with predictive modeling techniques.</span></span>

<span data-ttu-id="95488-122">Mediante un área de trabajo visual e interactiva, se arrastran y colocan ***conjuntos de datos*** y ***módulos*** de análisis en un lienzo interactivo.</span><span class="sxs-lookup"><span data-stu-id="95488-122">Using an interactive, visual workspace, you drag-and-drop ***datasets*** and analysis ***modules*** onto an interactive canvas.</span></span> <span data-ttu-id="95488-123">Conéctelos tooform junto un ***experimentar*** que se ejecutan en estudio de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="95488-123">You connect them together tooform an ***experiment*** that you run in Machine Learning Studio.</span></span>
<span data-ttu-id="95488-124">Se ***crear un modelo de***, ***entrenar el modelo de hello***, y ***puntuación y prueba Hola modelo***.</span><span class="sxs-lookup"><span data-stu-id="95488-124">You ***create a model***, ***train hello model***, and ***score and test hello model***.</span></span>

<span data-ttu-id="95488-125">En el diseño del modelo, puede iterar edición experimento de Hola y ejecutarlo hasta que se proporciona Hola resultados que está buscando.</span><span class="sxs-lookup"><span data-stu-id="95488-125">You can iterate on your model design, editing hello experiment and running it until it gives you hello results you're looking for.</span></span> <span data-ttu-id="95488-126">Cuando el modelo está listo, puede publicarlo como un ***servicio web*** para que otros puedan enviarle nuevos datos y obtener a cambio predicciones.</span><span class="sxs-lookup"><span data-stu-id="95488-126">When your model is ready, you can publish it as a ***web service*** so that others can send it new data and get predictions in return.</span></span>

## <a name="open-machine-learning-studio"></a><span data-ttu-id="95488-127">Apertura de Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="95488-127">Open Machine Learning Studio</span></span>

<span data-ttu-id="95488-128">tooget trabajar con Studio, vaya demasiado[https://studio.azureml.net](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="95488-128">tooget started with Studio, go too[https://studio.azureml.net](https://studio.azureml.net).</span></span> <span data-ttu-id="95488-129">Si ya se ha registrado en Machine Learning Studio antes, haga clic en **Sign In** (Iniciar sesión).</span><span class="sxs-lookup"><span data-stu-id="95488-129">If you’ve signed into Machine Learning Studio before, click **Sign In**.</span></span> <span data-ttu-id="95488-130">De lo contrario, haga clic en **Sign up here** (Regístrese aquí) y elija entre opciones gratuitas y de pago.</span><span class="sxs-lookup"><span data-stu-id="95488-130">Otherwise, click **Sign up here** and choose between free and paid options.</span></span>

<span data-ttu-id="95488-131">![Inicie sesión en estudio de aprendizaje tooMachine][sign-in-to-studio]
</span><span class="sxs-lookup"><span data-stu-id="95488-131">![Sign in tooMachine Learning Studio][sign-in-to-studio]
</span></span><br/><span data-ttu-id="95488-132">
***Inicie sesión en estudio de aprendizaje tooMachine***</span><span class="sxs-lookup"><span data-stu-id="95488-132">
***Sign in tooMachine Learning Studio***</span></span>

## <a name="five-steps-toocreate-an-experiment"></a><span data-ttu-id="95488-133">Cinco pasos toocreate un experimento</span><span class="sxs-lookup"><span data-stu-id="95488-133">Five steps toocreate an experiment</span></span>

<span data-ttu-id="95488-134">En este tutorial de aprendizaje de máquina, podrá seguir cinco pasos básicos toobuild un experimento en estudio de aprendizaje automático toocreate, entrenar y puntuación el modelo:</span><span class="sxs-lookup"><span data-stu-id="95488-134">In this machine learning tutorial, you'll follow five basic steps toobuild an experiment in Machine Learning Studio toocreate, train, and score your model:</span></span>

- <span data-ttu-id="95488-135">**Crear un modelo**</span><span class="sxs-lookup"><span data-stu-id="95488-135">**Create a model**</span></span>
    - <span data-ttu-id="95488-136">[Paso 1: Obtener los datos]</span><span class="sxs-lookup"><span data-stu-id="95488-136">[Step 1: Get data]</span></span>
    - <span data-ttu-id="95488-137">[Paso 2: Preparar los datos de Hola]</span><span class="sxs-lookup"><span data-stu-id="95488-137">[Step 2: Prepare hello data]</span></span>
    - <span data-ttu-id="95488-138">[Paso 3: Definir las características]</span><span class="sxs-lookup"><span data-stu-id="95488-138">[Step 3: Define features]</span></span>
- <span data-ttu-id="95488-139">**Entrenar el modelo de Hola**</span><span class="sxs-lookup"><span data-stu-id="95488-139">**Train hello model**</span></span>
    - <span data-ttu-id="95488-140">[Paso 4: Elegir y aplicar un algoritmo de aprendizaje]</span><span class="sxs-lookup"><span data-stu-id="95488-140">[Step 4: Choose and apply a learning algorithm]</span></span>
- <span data-ttu-id="95488-141">**Modelo de Hola de puntuación y prueba**</span><span class="sxs-lookup"><span data-stu-id="95488-141">**Score and test hello model**</span></span>
    - <span data-ttu-id="95488-142">[Paso 5: Predecir los precios de los automóviles nuevos]</span><span class="sxs-lookup"><span data-stu-id="95488-142">[Step 5: Predict new automobile prices]</span></span>

[Paso 1: Obtener los datos]: #step-1-get-data
[Paso 2: Preparar los datos de Hola]: #step-2-prepare-the-data
[Paso 3: Definir las características]: #step-3-define-features
[Paso 4: Elegir y aplicar un algoritmo de aprendizaje]: #step-4-choose-and-apply-a-learning-algorithm
[Paso 5: Predecir los precios de los automóviles nuevos]: #step-5-predict-new-automobile-prices

> [!TIP] 
> <span data-ttu-id="95488-148">Puede encontrar una copia de trabajo de hello siguientes experimento en hello [Cortana Intelligence galería](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="95488-148">You can find a working copy of hello following experiment in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="95488-149">Vaya demasiado**[la ciencia de datos primer experimentar - predicción de precios de automóviles](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)**  y haga clic en **abierta en Studio** toodownload una copia del experimento de hello en el aprendizaje automático Área de trabajo de Studio.</span><span class="sxs-lookup"><span data-stu-id="95488-149">Go too**[Your first data science experiment - Automobile price prediction](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)** and click **Open in Studio** toodownload a copy of hello experiment into your Machine Learning Studio workspace.</span></span>


## <a name="step-1-get-data"></a><span data-ttu-id="95488-150">Paso 1: Obtener los datos</span><span class="sxs-lookup"><span data-stu-id="95488-150">Step 1: Get data</span></span>

<span data-ttu-id="95488-151">Hola primera cosa que necesita el aprendizaje automático de tooperform es datos.</span><span class="sxs-lookup"><span data-stu-id="95488-151">hello first thing you need tooperform machine learning is data.</span></span>
<span data-ttu-id="95488-152">Machine Learning Studio incluye varios conjuntos de datos que puede usar; otra opción es importarlos de diversos orígenes.</span><span class="sxs-lookup"><span data-stu-id="95488-152">There are several sample datasets included with Machine Learning Studio that you can use, or you can import data from many sources.</span></span> <span data-ttu-id="95488-153">En este ejemplo, vamos a usar el conjunto de datos de ejemplo de Hola, **datos de precios de automóviles (Raw)**, que se incluye en el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="95488-153">For this example, we'll use hello sample dataset, **Automobile price data (Raw)**, that's included in your workspace.</span></span>
<span data-ttu-id="95488-154">Este conjunto de datos incluye entradas para diversos automóviles individuales, por ejemplo, información sobre la marca, el modelo, las especificaciones técnicas y el precio.</span><span class="sxs-lookup"><span data-stu-id="95488-154">This dataset includes entries for various individual automobiles, including information such as make, model, technical specifications, and price.</span></span>

<span data-ttu-id="95488-155">Le mostramos cómo tooget Hola conjunto de datos en el experimento.</span><span class="sxs-lookup"><span data-stu-id="95488-155">Here's how tooget hello dataset into your experiment.</span></span>

1. <span data-ttu-id="95488-156">Cree un experimento de nuevo haciendo clic en **+ nuevo** en hello parte inferior de la ventana de estudio de aprendizaje automático de hello, seleccione **experimentar**y, a continuación, seleccione **experimentar en blanco**.</span><span class="sxs-lookup"><span data-stu-id="95488-156">Create a new experiment by clicking **+NEW** at hello bottom of hello Machine Learning Studio window, select **EXPERIMENT**, and then select **Blank Experiment**.</span></span>

2. <span data-ttu-id="95488-157">el experimento de Hello recibe un nombre predeterminado que puede ver en parte superior de hello del lienzo de Hola.</span><span class="sxs-lookup"><span data-stu-id="95488-157">hello experiment is given a default name that you can see at hello top of hello canvas.</span></span> <span data-ttu-id="95488-158">Seleccione este texto y cambie su nombre toosomething significativo, por ejemplo, **predicción de precios de automóviles**.</span><span class="sxs-lookup"><span data-stu-id="95488-158">Select this text and rename it toosomething meaningful, for example, **Automobile price prediction**.</span></span> <span data-ttu-id="95488-159">nombre de Hello no necesita toobe único.</span><span class="sxs-lookup"><span data-stu-id="95488-159">hello name doesn't need toobe unique.</span></span>

    ![Cambiar el nombre de experimento Hola][rename-experiment]

2. <span data-ttu-id="95488-161">toohello izquierda del lienzo del experimento de hello es una paleta de conjuntos de datos y los módulos.</span><span class="sxs-lookup"><span data-stu-id="95488-161">toohello left of hello experiment canvas is a palette of datasets and modules.</span></span> <span data-ttu-id="95488-162">Tipo de **automobile** en el cuadro de búsqueda de hello en la parte superior de Hola de este conjunto de datos Hola del toofind de paleta con la etiqueta **datos de precios de automóviles (Raw)**.</span><span class="sxs-lookup"><span data-stu-id="95488-162">Type **automobile** in hello Search box at hello top of this palette toofind hello dataset labeled **Automobile price data (Raw)**.</span></span> <span data-ttu-id="95488-163">Arrastre este lienzo del experimento toohello conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="95488-163">Drag this dataset toohello experiment canvas.</span></span>

    <span data-ttu-id="95488-164">![Buscar Hola automóviles dataset y arrástrelo al lienzo del experimento de Hola][type-automobile]
    </span><span class="sxs-lookup"><span data-stu-id="95488-164">![Find hello automobile dataset and drag it onto hello experiment canvas][type-automobile]
    </span></span><br/>
 <span data-ttu-id="95488-165">***Buscar Hola automóviles dataset y arrástrelo al lienzo del experimento de Hola***</span><span class="sxs-lookup"><span data-stu-id="95488-165">***Find hello automobile dataset and drag it onto hello experiment canvas***</span></span>

<span data-ttu-id="95488-166">toosee lo que estos datos parece, haga clic en el puerto de salida de hello en parte inferior de hello del conjunto de datos de automóviles de hello y, a continuación, seleccione **visualizar**.</span><span class="sxs-lookup"><span data-stu-id="95488-166">toosee what this data looks like, click hello output port at hello bottom of hello automobile dataset, and then select **Visualize**.</span></span>

<span data-ttu-id="95488-167">![Haga clic en el puerto de salida de hello y seleccione "Visualizar"][select-visualize]
</span><span class="sxs-lookup"><span data-stu-id="95488-167">![Click hello output port and select "Visualize"][select-visualize]
</span></span><br/><span data-ttu-id="95488-168">
***Haga clic en el puerto de salida de hello y seleccione "Visualizar"***</span><span class="sxs-lookup"><span data-stu-id="95488-168">
***Click hello output port and select "Visualize"***</span></span>

> [!TIP]
> <span data-ttu-id="95488-169">Conjuntos de datos y los módulos con entrada y puertos de salida representados por círculos pequeños - puertos de entrada en la parte superior de hello, salida puertos en la parte inferior de Hola.</span><span class="sxs-lookup"><span data-stu-id="95488-169">Datasets and modules have input and output ports represented by small circles - input ports at hello top, output ports at hello bottom.</span></span>
<span data-ttu-id="95488-170">toocreate un flujo de datos a través de su experimento, se conectará un puerto de salida del puerto de entrada de tooan de un módulo de otro.</span><span class="sxs-lookup"><span data-stu-id="95488-170">toocreate a flow of data through your experiment, you'll connect an output port of one module tooan input port of another.</span></span>
<span data-ttu-id="95488-171">En cualquier momento, puede hacer clic en puerto de salida de hello de un conjunto de datos o un módulo toosee qué datos hello es similar en ese momento en el flujo de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="95488-171">At any time, you can click hello output port of a dataset or module toosee what hello data looks like at that point in hello data flow.</span></span>

<span data-ttu-id="95488-172">En este conjunto de datos de ejemplo, cada instancia de un automóvil aparece como una fila y variables de hello asociadas a cada automóvil aparecen como columnas.</span><span class="sxs-lookup"><span data-stu-id="95488-172">In this sample dataset, each instance of an automobile appears as a row, and hello variables associated with each automobile appear as columns.</span></span> <span data-ttu-id="95488-173">Proporcionan las variables de Hola para un objeto automobile específico, vamos precio de hello tootry toopredict en la columna derecha (columna 26, titulada "price").</span><span class="sxs-lookup"><span data-stu-id="95488-173">Given hello variables for a specific automobile, we're going tootry toopredict hello price in far-right column (column 26, titled "price").</span></span>

<span data-ttu-id="95488-174">![Ver los datos de automóviles hello en la ventana de visualización de datos de hello][visualize-auto-data]
</span><span class="sxs-lookup"><span data-stu-id="95488-174">![View hello automobile data in hello data visualization window][visualize-auto-data]
</span></span><br/><span data-ttu-id="95488-175">
***Ver los datos de automóviles hello en la ventana de visualización de datos de hello***</span><span class="sxs-lookup"><span data-stu-id="95488-175">
***View hello automobile data in hello data visualization window***</span></span>

<span data-ttu-id="95488-176">Ventana de visualización de hello cerrar haciendo clic en hello "**x**" en la esquina superior derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="95488-176">Close hello visualization window by clicking hello "**x**" in hello upper-right corner.</span></span>

## <a name="step-2-prepare-hello-data"></a><span data-ttu-id="95488-177">Paso 2: Preparar los datos de Hola</span><span class="sxs-lookup"><span data-stu-id="95488-177">Step 2: Prepare hello data</span></span>

<span data-ttu-id="95488-178">Normalmente, un conjunto de datos requiere algún procesamiento previo antes de que se pueda analizar.</span><span class="sxs-lookup"><span data-stu-id="95488-178">A dataset usually requires some preprocessing before it can be analyzed.</span></span> <span data-ttu-id="95488-179">Por ejemplo, puede que haya observado Hola los valores presentes en las columnas de Hola de varias filas que faltan.</span><span class="sxs-lookup"><span data-stu-id="95488-179">For example, you might have noticed hello missing values present in hello columns of various rows.</span></span> <span data-ttu-id="95488-180">Estos valores que faltan necesitan toobe limpiarse, así que el modelo de hello puede analizar datos de hello correctamente.</span><span class="sxs-lookup"><span data-stu-id="95488-180">These missing values need toobe cleaned so hello model can analyze hello data correctly.</span></span> <span data-ttu-id="95488-181">En nuestro caso, quitaremos todas las filas que tengan valores ausentes.</span><span class="sxs-lookup"><span data-stu-id="95488-181">In our case, we'll remove any rows that have missing values.</span></span> <span data-ttu-id="95488-182">Además, Hola **pérdidas normalizadas** columna tiene una gran proporción de valores que faltan, por lo que se podrá excluir esa columna de modelo de Hola por completo.</span><span class="sxs-lookup"><span data-stu-id="95488-182">Also, hello **normalized-losses** column has a large proportion of missing values, so we'll exclude that column from hello model altogether.</span></span>

> [!TIP]
> <span data-ttu-id="95488-183">Hola limpiadora no tiene los valores de datos de entrada es un requisito previo para usar la mayoría de módulos de Hola.</span><span class="sxs-lookup"><span data-stu-id="95488-183">Cleaning hello missing values from input data is a prerequisite for using most of hello modules.</span></span>

<span data-ttu-id="95488-184">En primer lugar agregamos un módulo que quita hello **pérdidas normalizadas** columna completamente, y, a continuación, agregamos otro módulo que quita cualquier fila que tenga los datos que faltan.</span><span class="sxs-lookup"><span data-stu-id="95488-184">First we add a module that removes hello **normalized-losses** column completely, and then we add another module that removes any row that has missing data.</span></span>

1. <span data-ttu-id="95488-185">Tipo de **seleccionar columnas** en cuadro de búsqueda de hello en parte superior de Hola Hola de hello módulo paleta toofind [seleccionar columnas de conjunto de datos] [ select-columns] módulo, a continuación, arrastre el lienzo del experimento toohello .</span><span class="sxs-lookup"><span data-stu-id="95488-185">Type **select columns** in hello Search box at hello top of hello module palette toofind hello [Select Columns in Dataset][select-columns] module, then drag it toohello experiment canvas.</span></span> <span data-ttu-id="95488-186">Este módulo permite tooselect qué columnas de datos se desea tooinclude o excluir de Hola modelo.</span><span class="sxs-lookup"><span data-stu-id="95488-186">This module allows us tooselect which columns of data we want tooinclude or exclude in hello model.</span></span>

2. <span data-ttu-id="95488-187">Conecte los puertos de salida de hello de hello **datos de precios de automóviles (Raw)** toohello de conjunto de datos de entrada de puerto de hello [seleccionar columnas de conjunto de datos] [ select-columns] módulo.</span><span class="sxs-lookup"><span data-stu-id="95488-187">Connect hello output port of hello **Automobile price data (Raw)** dataset toohello input port of hello [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="95488-188">![Agregar Hola "Seleccionar columnas de conjunto de datos" módulo toohello experimento lienzo y conéctelo][type-select-columns]
    </span><span class="sxs-lookup"><span data-stu-id="95488-188">![Add hello "Select Columns in Dataset" module toohello experiment canvas and connect it][type-select-columns]
    </span></span><br/>
 <span data-ttu-id="95488-189">***Agregar Hola "Seleccionar columnas de conjunto de datos" módulo toohello experimento lienzo y conéctelo***</span><span class="sxs-lookup"><span data-stu-id="95488-189">***Add hello "Select Columns in Dataset" module toohello experiment canvas and connect it***</span></span>

3. <span data-ttu-id="95488-190">Haga clic en hello [seleccionar columnas de conjunto de datos] [ select-columns] módulo y haga clic en **selector de columna de inicio** en hello **propiedades** panel.</span><span class="sxs-lookup"><span data-stu-id="95488-190">Click hello [Select Columns in Dataset][select-columns] module and click **Launch column selector** in hello **Properties** pane.</span></span>

    - <span data-ttu-id="95488-191">Hola izquierda, haga clic en **con reglas**</span><span class="sxs-lookup"><span data-stu-id="95488-191">On hello left, click **With rules**</span></span>
    - <span data-ttu-id="95488-192">En **Empiezan por**, haga clic en **Todas las columnas**.</span><span class="sxs-lookup"><span data-stu-id="95488-192">Under **Begin With**, click **All columns**.</span></span> <span data-ttu-id="95488-193">Esto indica [seleccionar columnas de conjunto de datos] [ select-columns] toopass a través de todas las columnas de hello (excepto las columnas que estamos sobre tooexclude).</span><span class="sxs-lookup"><span data-stu-id="95488-193">This directs [Select Columns in Dataset][select-columns] toopass through all hello columns (except those columns we're about tooexclude).</span></span>
    - <span data-ttu-id="95488-194">Seleccionar en listas desplegables hello **excluir** y **nombres de columna**y, a continuación, haga clic en el cuadro de texto de Hola.</span><span class="sxs-lookup"><span data-stu-id="95488-194">From hello drop-downs, select **Exclude** and **column names**, and then click inside hello text box.</span></span> <span data-ttu-id="95488-195">A continuación, se mostrará una lista de columnas.</span><span class="sxs-lookup"><span data-stu-id="95488-195">A list of columns is displayed.</span></span> <span data-ttu-id="95488-196">Seleccione **pérdidas normalizadas**, y es agregado toohello cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="95488-196">Select **normalized-losses**, and it's added toohello text box.</span></span>
    - <span data-ttu-id="95488-197">Haga clic en el selector de columnas de hello tooclose botón de marca de verificación (Aceptar) hello (en Hola inferior derecha).</span><span class="sxs-lookup"><span data-stu-id="95488-197">Click hello check mark (OK) button tooclose hello column selector (on hello lower-right).</span></span>

    <span data-ttu-id="95488-198">![Iniciar el selector de columna de Hola y excluir Hola "pérdidas normalizadas" columna][launch-column-selector]
    </span><span class="sxs-lookup"><span data-stu-id="95488-198">![Launch hello column selector and exclude hello "normalized-losses" column][launch-column-selector]
    </span></span><br/>
 <span data-ttu-id="95488-199">***Iniciar el selector de columna de Hola y excluir Hola "pérdidas normalizadas" columna***</span><span class="sxs-lookup"><span data-stu-id="95488-199">***Launch hello column selector and exclude hello "normalized-losses" column***</span></span>

    <span data-ttu-id="95488-200">Panel de propiedades de hello ahora de **seleccionar columnas de conjunto de datos** indica que pasará a través de todas las columnas de conjunto de datos de hello excepto **pérdidas normalizadas**.</span><span class="sxs-lookup"><span data-stu-id="95488-200">Now hello properties pane for **Select Columns in Dataset** indicates that it will pass through all columns from hello dataset except **normalized-losses**.</span></span>

    <span data-ttu-id="95488-201">![panel de propiedades de Hello muestra que se excluye esa columna Hola "pérdidas normalizadas"][showing-excluded-column]
    </span><span class="sxs-lookup"><span data-stu-id="95488-201">![hello properties pane shows that hello "normalized-losses" column is excluded][showing-excluded-column]
    </span></span><br/>
 <span data-ttu-id="95488-202">***panel de propiedades de Hello muestra que se excluye esa columna Hola "pérdidas normalizadas"***</span><span class="sxs-lookup"><span data-stu-id="95488-202">***hello properties pane shows that hello "normalized-losses" column is excluded***</span></span>

    > [!TIP]
    <span data-ttu-id="95488-203">Puede agregar un módulo tooa comentario haciendo doble clic en módulo de Hola y de escritura de texto.</span><span class="sxs-lookup"><span data-stu-id="95488-203">You can add a comment tooa module by double-clicking hello module and entering text.</span></span> <span data-ttu-id="95488-204">Esto puede ayudarle a ver de un vistazo qué módulo Hola está haciendo en el experimento.</span><span class="sxs-lookup"><span data-stu-id="95488-204">This can help you see at a glance what hello module is doing in your experiment.</span></span> <span data-ttu-id="95488-205">En este caso, haga doble clic en hello [seleccionar columnas de conjunto de datos] [ select-columns] módulo y tipo Hola comentario "Exclude normaliza las pérdidas".</span><span class="sxs-lookup"><span data-stu-id="95488-205">In this case double-click hello [Select Columns in Dataset][select-columns] module and type hello comment "Exclude normalized losses."</span></span>
    >
    >


    <span data-ttu-id="95488-206">![Haga doble clic en un tooadd módulo un comentario][add-comment]
    </span><span class="sxs-lookup"><span data-stu-id="95488-206">![Double-click a module tooadd a comment][add-comment]
    </span></span><br/>
 <span data-ttu-id="95488-207">***Haga doble clic en un tooadd módulo un comentario***</span><span class="sxs-lookup"><span data-stu-id="95488-207">***Double-click a module tooadd a comment***</span></span>

3. <span data-ttu-id="95488-208">Hola arrastre [limpiar datos que faltan] [ clean-missing-data] toohello módulo experimentar lienzo y conéctelo toohello [seleccionar columnas de conjunto de datos] [ select-columns] módulo.</span><span class="sxs-lookup"><span data-stu-id="95488-208">Drag hello [Clean Missing Data][clean-missing-data] module toohello experiment canvas and connect it toohello [Select Columns in Dataset][select-columns] module.</span></span> <span data-ttu-id="95488-209">Hola **propiedades** panel, seleccione **quitar toda la fila** en **modo de limpieza**.</span><span class="sxs-lookup"><span data-stu-id="95488-209">In hello **Properties** pane, select **Remove entire row** under **Cleaning mode**.</span></span> <span data-ttu-id="95488-210">Esto indica [limpiar datos que faltan] [ clean-missing-data] tooclean datos de hello mediante la eliminación de filas que tienen valores que faltan.</span><span class="sxs-lookup"><span data-stu-id="95488-210">This directs [Clean Missing Data][clean-missing-data] tooclean hello data by removing rows that have any missing values.</span></span> <span data-ttu-id="95488-211">Haga doble clic en el módulo de Hola y escriba el comentario de Hola "Quitar filas que faltan de valor".</span><span class="sxs-lookup"><span data-stu-id="95488-211">Double-click hello module and type hello comment "Remove missing value rows."</span></span>

    <span data-ttu-id="95488-212">![Establecer el modo de limpieza Hola demasiado "quitar toda la fila" para el módulo de "Limpiar datos que faltan" hello][set-remove-entire-row]
    </span><span class="sxs-lookup"><span data-stu-id="95488-212">![Set hello cleaning mode too"Remove entire row" for hello "Clean Missing Data" module][set-remove-entire-row]
    </span></span><br/>
 <span data-ttu-id="95488-213">***Establecer el modo de limpieza Hola demasiado "quitar toda la fila" para el módulo de "Limpiar datos que faltan" hello***</span><span class="sxs-lookup"><span data-stu-id="95488-213">***Set hello cleaning mode too"Remove entire row" for hello "Clean Missing Data" module***</span></span>

4. <span data-ttu-id="95488-214">Ejecute el experimento de hello haciendo clic en **ejecutar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="95488-214">Run hello experiment by clicking **RUN** at hello bottom of hello page.</span></span>

    <span data-ttu-id="95488-215">Cuando el experimento de hello ha terminado de ejecutarse, todos los módulos de hello tienen un tooindicate de marca de verificación verde que finalizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="95488-215">When hello experiment has finished running, all hello modules have a green check mark tooindicate that they finished successfully.</span></span> <span data-ttu-id="95488-216">Tenga en cuenta también Hola **finalice la ejecución** estado en la esquina superior derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="95488-216">Notice also hello **Finished running** status in hello upper-right corner.</span></span>

<span data-ttu-id="95488-217">![Después de ejecutarlo, experimento Hola debe tener un aspecto similar al siguiente][early-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="95488-217">![After running it, hello experiment should look something like this][early-experiment-run]
</span></span><br/><span data-ttu-id="95488-218">
***Después de ejecutarlo, experimento Hola debe tener un aspecto similar al siguiente***</span><span class="sxs-lookup"><span data-stu-id="95488-218">
***After running it, hello experiment should look something like this***</span></span>

> [!TIP]
> <span data-ttu-id="95488-219">¿Por qué se se ejecutó experimento Hola ahora?</span><span class="sxs-lookup"><span data-stu-id="95488-219">Why did we run hello experiment now?</span></span> <span data-ttu-id="95488-220">Ejecución experimento hello, pasan las definiciones de columna de Hola para nuestros datos de conjunto de datos de hello, a través de hello [seleccionar columnas de conjunto de datos] [ select-columns] módulo y a través de hello [limpiar datos que faltan] [ clean-missing-data] módulo.</span><span class="sxs-lookup"><span data-stu-id="95488-220">By running hello experiment, hello column definitions for our data pass from hello dataset, through hello [Select Columns in Dataset][select-columns] module, and through hello [Clean Missing Data][clean-missing-data] module.</span></span> <span data-ttu-id="95488-221">Esto significa que los módulos que nos conectamos demasiado[limpiar datos que faltan] [ clean-missing-data] también tendrá la misma información.</span><span class="sxs-lookup"><span data-stu-id="95488-221">This means that any modules we connect too[Clean Missing Data][clean-missing-data] will also have this same information.</span></span>

<span data-ttu-id="95488-222">Todo lo que hemos realizado en el experimento de hello toothis punto es datos Hola limpia.</span><span class="sxs-lookup"><span data-stu-id="95488-222">All we have done in hello experiment up toothis point is clean hello data.</span></span> <span data-ttu-id="95488-223">Si desea que el conjunto de datos de tooview Hola limpiado, haga clic en hello dejado el puerto de salida de hello [limpiar datos que faltan] [ clean-missing-data] módulo y seleccione **visualizar**.</span><span class="sxs-lookup"><span data-stu-id="95488-223">If you want tooview hello cleaned dataset, click hello left output port of hello [Clean Missing Data][clean-missing-data] module and select **Visualize**.</span></span> <span data-ttu-id="95488-224">Tenga en cuenta que hello **pérdidas normalizadas** ya no se incluye la columna, y no falta ningún valor.</span><span class="sxs-lookup"><span data-stu-id="95488-224">Notice that hello **normalized-losses** column is no longer included, and there are no missing values.</span></span>

<span data-ttu-id="95488-225">Ahora que los datos de hello están limpios, estamos toospecify listo las características que se vayan a toouse en el modelo de predicción de Hola.</span><span class="sxs-lookup"><span data-stu-id="95488-225">Now that hello data is clean, we're ready toospecify what features we're going toouse in hello predictive model.</span></span>

## <a name="step-3-define-features"></a><span data-ttu-id="95488-226">Paso 3: Definir las características</span><span class="sxs-lookup"><span data-stu-id="95488-226">Step 3: Define features</span></span>

<span data-ttu-id="95488-227">En el aprendizaje automático, las *características* son propiedades mensurables individuales de algo que le interesa.</span><span class="sxs-lookup"><span data-stu-id="95488-227">In machine learning, *features* are individual measurable properties of something you’re interested in.</span></span> <span data-ttu-id="95488-228">En nuestro conjunto de datos, cada fila representa un automóvil y cada columna es una característica de ese automóvil.</span><span class="sxs-lookup"><span data-stu-id="95488-228">In our dataset, each row represents one automobile, and each column is a feature of that automobile.</span></span>

<span data-ttu-id="95488-229">Buscar un buen conjunto de características para crear un modelo de predicción requiere experimentación y conocimientos sobre el problema de Hola que desea toosolve.</span><span class="sxs-lookup"><span data-stu-id="95488-229">Finding a good set of features for creating a predictive model requires experimentation and knowledge about hello problem you want toosolve.</span></span> <span data-ttu-id="95488-230">Algunas características son mejores para predecir el destino de Hola que otros.</span><span class="sxs-lookup"><span data-stu-id="95488-230">Some features are better for predicting hello target than others.</span></span> <span data-ttu-id="95488-231">Además, algunas características tienen una correlación fuerte con otras y se pueden quitar.</span><span class="sxs-lookup"><span data-stu-id="95488-231">Also, some features have a strong correlation with other features and can be removed.</span></span> <span data-ttu-id="95488-232">Por ejemplo, mpg ciudad y autopista mpg están estrechamente relacionados por lo que podemos conservar uno y quitar Hola otro sin afectar sustancialmente a predicción Hola.</span><span class="sxs-lookup"><span data-stu-id="95488-232">For example, city-mpg and highway-mpg are closely related so we can keep one and remove hello other without significantly affecting hello prediction.</span></span>

<span data-ttu-id="95488-233">Vamos a crear un modelo que utiliza un subconjunto de características de hello en el conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="95488-233">Let's build a model that uses a subset of hello features in our dataset.</span></span> <span data-ttu-id="95488-234">Puede volver a verle y seleccionar diversas características, vuelva a ejecutar el experimento de Hola y vea si se pueden obtener mejores resultados.</span><span class="sxs-lookup"><span data-stu-id="95488-234">You can come back later and select different features, run hello experiment again, and see if you get better results.</span></span> <span data-ttu-id="95488-235">Pero toostart, probemos Hola siguientes características:</span><span class="sxs-lookup"><span data-stu-id="95488-235">But toostart, let's try hello following features:</span></span>

    make, body-style, wheel-base, engine-size, horsepower, peak-rpm, highway-mpg, price


1. <span data-ttu-id="95488-236">Arrastre otra [seleccionar columnas de conjunto de datos] [ select-columns] toohello módulo experimentar lienzo.</span><span class="sxs-lookup"><span data-stu-id="95488-236">Drag another [Select Columns in Dataset][select-columns] module toohello experiment canvas.</span></span> <span data-ttu-id="95488-237">Conectar Hola dejado el puerto de salida de hello [limpiar datos que faltan] [ clean-missing-data] entrada toohello de módulo de hello [seleccionar columnas de conjunto de datos] [ select-columns] módulo.</span><span class="sxs-lookup"><span data-stu-id="95488-237">Connect hello left output port of hello [Clean Missing Data][clean-missing-data] module toohello input of hello [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="95488-238">![Conectar Hola "Seleccionar columnas de conjunto de datos" toohello "Limpiar datos que faltan" módulo][connect-clean-to-select]
    </span><span class="sxs-lookup"><span data-stu-id="95488-238">![Connect hello "Select Columns in Dataset" module toohello "Clean Missing Data" module][connect-clean-to-select]
    </span></span><br/>
 <span data-ttu-id="95488-239">***Conectar Hola "Seleccionar columnas de conjunto de datos" toohello "Limpiar datos que faltan" módulo***</span><span class="sxs-lookup"><span data-stu-id="95488-239">***Connect hello "Select Columns in Dataset" module toohello "Clean Missing Data" module***</span></span>

2. <span data-ttu-id="95488-240">Haga doble clic en el módulo de Hola y escriba "Seleccionar características para la predicción."</span><span class="sxs-lookup"><span data-stu-id="95488-240">Double-click hello module and type "Select features for prediction."</span></span>

2. <span data-ttu-id="95488-241">Haga clic en **selector de columna de inicio** en hello **propiedades** panel.</span><span class="sxs-lookup"><span data-stu-id="95488-241">Click **Launch column selector** in hello **Properties** pane.</span></span>

3. <span data-ttu-id="95488-242">Haga clic en **With rules**(Con reglas).</span><span class="sxs-lookup"><span data-stu-id="95488-242">Click **With rules**.</span></span>

4. <span data-ttu-id="95488-243">En **Empezar por**, haga clic en **No columns** (Ninguna columna).</span><span class="sxs-lookup"><span data-stu-id="95488-243">Under **Begin With**, click **No columns**.</span></span> <span data-ttu-id="95488-244">En la fila de filtro de hello, seleccione **Include** y **nombres de columna** y seleccione la lista de nombres de columna en el cuadro de texto de Hola.</span><span class="sxs-lookup"><span data-stu-id="95488-244">In hello filter row, select **Include** and **column names** and select our list of column names in hello text box.</span></span> <span data-ttu-id="95488-245">Esto indica Hola módulo toonot paso a través de las columnas (funciones), salvo que especificamos Hola.</span><span class="sxs-lookup"><span data-stu-id="95488-245">This directs hello module toonot pass through any columns (features) except hello ones that we specify.</span></span>

5. <span data-ttu-id="95488-246">Haga clic en el botón de marca de verificación (Aceptar) Hola.</span><span class="sxs-lookup"><span data-stu-id="95488-246">Click hello check mark (OK) button.</span></span>

    <span data-ttu-id="95488-247">![Seleccione tooinclude de columnas (funciones) de hello en la predicción de Hola][select-columns-to-include]
    </span><span class="sxs-lookup"><span data-stu-id="95488-247">![Select hello columns (features) tooinclude in hello prediction][select-columns-to-include]
    </span></span><br/>
 <span data-ttu-id="95488-248">***Seleccione tooinclude de columnas (funciones) de hello en la predicción de Hola***</span><span class="sxs-lookup"><span data-stu-id="95488-248">***Select hello columns (features) tooinclude in hello prediction***</span></span>

<span data-ttu-id="95488-249">Esto genera un conjunto de datos filtrado que contiene características de hello solo que queremos toohello toopass vamos a usar en el paso siguiente Hola de algoritmo de aprendizaje.</span><span class="sxs-lookup"><span data-stu-id="95488-249">This produces a filtered dataset containing only hello features we want toopass toohello learning algorithm we'll use in hello next step.</span></span> <span data-ttu-id="95488-250">Posteriormente puede volver e intentarlo de nuevo con una selección diferente de características.</span><span class="sxs-lookup"><span data-stu-id="95488-250">Later, you can return and try again with a different selection of features.</span></span>

## <a name="step-4-choose-and-apply-a-learning-algorithm"></a><span data-ttu-id="95488-251">Paso 4: Elegir y aplicar un algoritmo de aprendizaje</span><span class="sxs-lookup"><span data-stu-id="95488-251">Step 4: Choose and apply a learning algorithm</span></span>

<span data-ttu-id="95488-252">Ahora que los datos de hello están listos, generar un modelo predictivo consta de entrenamiento y prueba.</span><span class="sxs-lookup"><span data-stu-id="95488-252">Now that hello data is ready, constructing a predictive model consists of training and testing.</span></span> <span data-ttu-id="95488-253">Vamos a usar nuestro modelo de datos tootrain hello y, a continuación, lo probaremos Hola modelo toosee cercanía es toopredict capaz de precios.</span><span class="sxs-lookup"><span data-stu-id="95488-253">We'll use our data tootrain hello model, and then we'll test hello model toosee how closely it's able toopredict prices.</span></span>
<!-- For now, don't worry about *why* we need tootrain and then test a model.-->

<span data-ttu-id="95488-254">*Clasificación* y *regresión* son dos tipos de algoritmos de aprendizaje automático supervisado.</span><span class="sxs-lookup"><span data-stu-id="95488-254">*Classification* and *regression* are two types of supervised machine learning algorithms.</span></span> <span data-ttu-id="95488-255">La clasificación permite predecir una respuesta a partir de un conjunto definido de categorías, como el color (rojo, azul o verde).</span><span class="sxs-lookup"><span data-stu-id="95488-255">Classification predicts an answer from a defined set of categories, such as a color (red, blue, or green).</span></span> <span data-ttu-id="95488-256">La regresión es toopredict usa un número.</span><span class="sxs-lookup"><span data-stu-id="95488-256">Regression is used toopredict a number.</span></span>

<span data-ttu-id="95488-257">Dado que deseamos toopredict precio, que es un número, vamos a usar un algoritmo de regresión.</span><span class="sxs-lookup"><span data-stu-id="95488-257">Because we want toopredict price, which is a number, we'll use a regression algorithm.</span></span> <span data-ttu-id="95488-258">En este ejemplo, vamos a usar un sencillo modelo de *regresión lineal*.</span><span class="sxs-lookup"><span data-stu-id="95488-258">For this example, we'll use a simple *linear regression* model.</span></span>

> [!TIP]
> <span data-ttu-id="95488-259">Si desea más información acerca de los distintos tipos de algoritmos de aprendizaje automático toolearn y cuando toouse usarlas, podría ver vídeo primera Hola Hola ciencia de datos para la serie de principiantes, [Hola cinco preguntas respuestas de ciencia de datos](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span><span class="sxs-lookup"><span data-stu-id="95488-259">If you want toolearn more about different types of machine learning algorithms and when toouse them, you might view hello first video in hello Data Science for Beginners series, [hello five questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span></span> <span data-ttu-id="95488-260">También puede mirar hello infografía [máquina aspectos básicos con ejemplos de algoritmo de aprendizaje](machine-learning-basics-infographic-with-algorithm-examples.md), o extraer del repositorio hello [máquina hoja de referencia de algoritmo de aprendizaje](machine-learning-algorithm-cheat-sheet.md).</span><span class="sxs-lookup"><span data-stu-id="95488-260">You might also look at hello infographic [Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md), or check out hello [Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md).</span></span>

<span data-ttu-id="95488-261">Se entrenar el modelo de hello proporcionando un conjunto de datos que incluye el precio de Hola.</span><span class="sxs-lookup"><span data-stu-id="95488-261">We train hello model by giving it a set of data that includes hello price.</span></span> <span data-ttu-id="95488-262">modelo de Hello examina datos hello y buscar correlaciones entre las características de un automóvil y su precio.</span><span class="sxs-lookup"><span data-stu-id="95488-262">hello model scans hello data and look for correlations between an automobile's features and its price.</span></span> <span data-ttu-id="95488-263">A continuación, se probará el modelo de hello: comenzaremos proporcionan un conjunto de características para automóviles con que estamos familiarizados y ver cómo cerrar modelo Hola procede precio conocido de toopredicting Hola.</span><span class="sxs-lookup"><span data-stu-id="95488-263">Then we'll test hello model - we'll give it a set of features for automobiles we're familiar with and see how close hello model comes toopredicting hello known price.</span></span>

<span data-ttu-id="95488-264">Vamos a usar nuestros datos para entrenar el modelo de Hola y probarla mediante la división de datos de hello en conjuntos de datos de prueba y entrenamiento de independiente.</span><span class="sxs-lookup"><span data-stu-id="95488-264">We'll use our data for both training hello model and testing it by splitting hello data into separate training and testing datasets.</span></span>

1. <span data-ttu-id="95488-265">Seleccione y arrastre hello [dividir datos] [ split] toohello módulo experimentar lienzo y conéctelo toohello última [seleccionar columnas de conjunto de datos] [ select-columns] módulo.</span><span class="sxs-lookup"><span data-stu-id="95488-265">Select and drag hello [Split Data][split] module toohello experiment canvas and connect it toohello last [Select Columns in Dataset][select-columns] module.</span></span>

2. <span data-ttu-id="95488-266">Haga clic en hello [dividir datos] [ split] tooselect de módulo se.</span><span class="sxs-lookup"><span data-stu-id="95488-266">Click hello [Split Data][split] module tooselect it.</span></span> <span data-ttu-id="95488-267">Buscar hello **fracción de filas de hello en primer lugar de conjunto de datos de salida** (Hola **propiedades** toohello del panel derecho del lienzo de hello) y lo ha configurado too0.75.</span><span class="sxs-lookup"><span data-stu-id="95488-267">Find hello **Fraction of rows in hello first output dataset** (in hello **Properties** pane toohello right of hello canvas) and set it too0.75.</span></span> <span data-ttu-id="95488-268">De esta manera, se podrá usar 75 por ciento hello tootrain Hola del modelo de datos y retener 25 por ciento para pruebas (más adelante, puede experimentar con diferentes porcentajes de uso).</span><span class="sxs-lookup"><span data-stu-id="95488-268">This way, we'll use 75 percent of hello data tootrain hello model, and hold back 25 percent for testing (later, you can experiment with using different percentages).</span></span>

    <span data-ttu-id="95488-269">![Hola conjunto dividir fracción de Hola "Dividir datos" módulo too0.75][set-split-data-percentage]
    </span><span class="sxs-lookup"><span data-stu-id="95488-269">![Set hello split fraction of hello "Split Data" module too0.75][set-split-data-percentage]
    </span></span><br/>
 <span data-ttu-id="95488-270">***Hola conjunto dividir fracción de Hola "Dividir datos" módulo too0.75***</span><span class="sxs-lookup"><span data-stu-id="95488-270">***Set hello split fraction of hello "Split Data" module too0.75***</span></span>

    > [!TIP]
    > <span data-ttu-id="95488-271">Cambiando hello **valor de inicialización aleatorio** parámetro, puede generar diferentes muestras para entrenar y probar de manera aleatoria.</span><span class="sxs-lookup"><span data-stu-id="95488-271">By changing hello **Random seed** parameter, you can produce different random samples for training and testing.</span></span> <span data-ttu-id="95488-272">Este parámetro controla Hola la propagación de generador de números seudoaleatorios Hola.</span><span class="sxs-lookup"><span data-stu-id="95488-272">This parameter controls hello seeding of hello pseudo-random number generator.</span></span>

2. <span data-ttu-id="95488-273">Ejecute el experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="95488-273">Run hello experiment.</span></span> <span data-ttu-id="95488-274">Cuando se ejecuta el experimento de hello, Hola [seleccionar columnas de conjunto de datos] [ select-columns] y [dividir datos] [ split] módulos pasan toohello de definiciones de columna módulos que iremos agregando a continuación.</span><span class="sxs-lookup"><span data-stu-id="95488-274">When hello experiment is run, hello [Select Columns in Dataset][select-columns] and [Split Data][split] modules pass column definitions toohello modules we'll be adding next.</span></span>  

3. <span data-ttu-id="95488-275">Hola tooselect algoritmo de aprendizaje expanda hello **de aprendizaje automático** categoría en hello módulo paleta toohello izquierda de hello lienzo y, a continuación, expanda **inicializar modelo**.</span><span class="sxs-lookup"><span data-stu-id="95488-275">tooselect hello learning algorithm, expand hello **Machine Learning** category in hello module palette toohello left of hello canvas, and then expand **Initialize Model**.</span></span> <span data-ttu-id="95488-276">Esto muestra varias categorías de módulos que pueden ser algoritmos de aprendizaje automático de tooinitialize usado.</span><span class="sxs-lookup"><span data-stu-id="95488-276">This displays several categories of modules that can be used tooinitialize machine learning algorithms.</span></span> <span data-ttu-id="95488-277">Para este experimento, seleccione hello [regresión lineal] [ linear-regression] módulo en hello **regresión** categoría y arrástrelo toohello lienzo del experimento.</span><span class="sxs-lookup"><span data-stu-id="95488-277">For this experiment, select hello [Linear Regression][linear-regression] module under hello **Regression** category, and drag it toohello experiment canvas.</span></span>
<span data-ttu-id="95488-278">(Se puede encontrar el módulo de hello escribiendo "regresión lineal" en el cuadro de búsqueda de paleta Hola.)</span><span class="sxs-lookup"><span data-stu-id="95488-278">(You can also find hello module by typing "linear regression" in hello palette Search box.)</span></span>

4. <span data-ttu-id="95488-279">Busque y arrastre hello [entrenar modelo] [ train-model] toohello módulo experimentar lienzo.</span><span class="sxs-lookup"><span data-stu-id="95488-279">Find and drag hello [Train Model][train-model] module toohello experiment canvas.</span></span> <span data-ttu-id="95488-280">Conecte la salida de hello de hello [regresión lineal] [ linear-regression] toohello módulo deja la entrada del programa Hola a [entrenar modelo] [ train-model] módulo y conecte Hola entrenamiento de salida de datos (puerto de la izquierda) de hello [dividir datos] [ split] entrada derecha de módulo toohello de hello [entrenar modelo] [ train-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="95488-280">Connect hello output of hello [Linear Regression][linear-regression] module toohello left input of hello [Train Model][train-model] module, and connect hello training data output (left port) of hello [Split Data][split] module toohello right input of hello [Train Model][train-model] module.</span></span>

    <span data-ttu-id="95488-281">![Conecte Hola "Entrenar modelo" módulo tooboth Hola "Regresión lineal" y "Dividir datos de" los módulos][connect-train-model]
    </span><span class="sxs-lookup"><span data-stu-id="95488-281">![Connect hello "Train Model" module tooboth hello "Linear Regression" and "Split Data" modules][connect-train-model]
    </span></span><br/>
 <span data-ttu-id="95488-282">***Conecte Hola "Entrenar modelo" módulo tooboth Hola "Regresión lineal" y "Dividir datos de" los módulos***</span><span class="sxs-lookup"><span data-stu-id="95488-282">***Connect hello "Train Model" module tooboth hello "Linear Regression" and "Split Data" modules***</span></span>

5. <span data-ttu-id="95488-283">Haga clic en hello [entrenar modelo] [ train-model] módulo, haga clic en **selector de columna de inicio** en hello **propiedades** panel y, a continuación, seleccione hello **precio** columna.</span><span class="sxs-lookup"><span data-stu-id="95488-283">Click hello [Train Model][train-model] module, click **Launch column selector** in hello **Properties** pane, and then select hello **price** column.</span></span> <span data-ttu-id="95488-284">Se trata de valor de Hola que nuestro modelo es toopredict continuo.</span><span class="sxs-lookup"><span data-stu-id="95488-284">This is hello value that our model is going toopredict.</span></span>

    <span data-ttu-id="95488-285">Seleccione hello **precio** columna en el selector de columnas de hello moviendo de hello **columnas disponibles** lista toohello **columnas seleccionadas** lista.</span><span class="sxs-lookup"><span data-stu-id="95488-285">You select hello **price** column in hello column selector by moving it from hello **Available columns** list toohello **Selected columns** list.</span></span>

    <span data-ttu-id="95488-286">![Seleccionar columna de precio de hello para el módulo de "Entrenar modelo" hello][select-price-column]
    </span><span class="sxs-lookup"><span data-stu-id="95488-286">![Select hello price column for hello "Train Model" module][select-price-column]
    </span></span><br/>
 <span data-ttu-id="95488-287">***Seleccionar columna de precio de hello para el módulo de "Entrenar modelo" hello***</span><span class="sxs-lookup"><span data-stu-id="95488-287">***Select hello price column for hello "Train Model" module***</span></span>

6. <span data-ttu-id="95488-288">Ejecute el experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="95488-288">Run hello experiment.</span></span>

<span data-ttu-id="95488-289">Ahora tenemos un modelo de regresión entrenado que puede ser usado tooscore nuevas automóviles toomake precio predicciones de datos.</span><span class="sxs-lookup"><span data-stu-id="95488-289">We now have a trained regression model that can be used tooscore new automobile data toomake price predictions.</span></span>

<span data-ttu-id="95488-290">![Después de ejecutar, experimento Hola ahora debe ser similar al siguiente][second-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="95488-290">![After running, hello experiment should now look something like this][second-experiment-run]
</span></span><br/><span data-ttu-id="95488-291">
***Después de ejecutar, experimento Hola ahora debe ser similar al siguiente***</span><span class="sxs-lookup"><span data-stu-id="95488-291">
***After running, hello experiment should now look something like this***</span></span>

## <a name="step-5-predict-new-automobile-prices"></a><span data-ttu-id="95488-292">Paso 5: Predecir los precios de los automóviles nuevos</span><span class="sxs-lookup"><span data-stu-id="95488-292">Step 5: Predict new automobile prices</span></span>

<span data-ttu-id="95488-293">Ahora que nos hemos entrenar modelo de hello con 75 por ciento de los datos, podemos utilizarla tooscore Hola otros 25 por ciento de la medida de hello datos toosee nuestras funciones de modelo.</span><span class="sxs-lookup"><span data-stu-id="95488-293">Now that we've trained hello model using 75 percent of our data, we can use it tooscore hello other 25 percent of hello data toosee how well our model functions.</span></span>

1. <span data-ttu-id="95488-294">Busque y arrastre hello [puntuar modelo] [ score-model] toohello módulo experimentar lienzo.</span><span class="sxs-lookup"><span data-stu-id="95488-294">Find and drag hello [Score Model][score-model] module toohello experiment canvas.</span></span> <span data-ttu-id="95488-295">Conecte la salida de hello de hello [entrenar modelo] [ train-model] toohello módulo dejado el puerto de entrada de [puntuar modelo][score-model].</span><span class="sxs-lookup"><span data-stu-id="95488-295">Connect hello output of hello [Train Model][train-model] module toohello left input port of [Score Model][score-model].</span></span> <span data-ttu-id="95488-296">Conecte Hola prueba datos salida (puerto derecha) de hello [dividir datos] [ split] puerto de entrada de módulo toohello derecha [puntuar modelo][score-model].</span><span class="sxs-lookup"><span data-stu-id="95488-296">Connect hello test data output (right port) of hello [Split Data][split] module toohello right input port of [Score Model][score-model].</span></span>

    <span data-ttu-id="95488-297">![Conecte Hola "Modelo de puntuación" módulo tooboth Hola "Entrenar modelo" y "Dividir datos de" los módulos][connect-score-model]
    </span><span class="sxs-lookup"><span data-stu-id="95488-297">![Connect hello "Score Model" module tooboth hello "Train Model" and "Split Data" modules][connect-score-model]
    </span></span><br/>
 <span data-ttu-id="95488-298">***Conecte Hola "Modelo de puntuación" módulo tooboth Hola "Entrenar modelo" y "Dividir datos de" los módulos***</span><span class="sxs-lookup"><span data-stu-id="95488-298">***Connect hello "Score Model" module tooboth hello "Train Model" and "Split Data" modules***</span></span>

2. <span data-ttu-id="95488-299">Ejecute el experimento de Hola y ver la salida de hello de hello [puntuar modelo] [ score-model] módulo (haga clic en el puerto de salida de hello de [puntuar modelo] [ score-model] y seleccione **Visualizar**).</span><span class="sxs-lookup"><span data-stu-id="95488-299">Run hello experiment and view hello output from hello [Score Model][score-model] module (click hello output port of [Score Model][score-model] and select **Visualize**).</span></span> <span data-ttu-id="95488-300">muestra del resultado de Hello Hola valores predichos por precio y Hola valores conocidos de datos de prueba de saludo.</span><span class="sxs-lookup"><span data-stu-id="95488-300">hello output shows hello predicted values for price and hello known values from hello test data.</span></span>  

    <span data-ttu-id="95488-301">![Salida de hello "Modelo de puntuación" módulo][score-model-output]
    </span><span class="sxs-lookup"><span data-stu-id="95488-301">![Output of hello "Score Model" module][score-model-output]
    </span></span><br/>
 <span data-ttu-id="95488-302">***Salida de hello "Modelo de puntuación" módulo***</span><span class="sxs-lookup"><span data-stu-id="95488-302">***Output of hello "Score Model" module***</span></span>

3. <span data-ttu-id="95488-303">Por último, probamos calidad Hola de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="95488-303">Finally, we test hello quality of hello results.</span></span> <span data-ttu-id="95488-304">Seleccione y arrastre hello [evaluar modelo] [ evaluate-model] toohello módulo experimentar lienzo y conecte la salida de hello de hello [puntuar modelo] [ score-model] toohello módulo dejado de entrada de [evaluar modelo][evaluate-model].</span><span class="sxs-lookup"><span data-stu-id="95488-304">Select and drag hello [Evaluate Model][evaluate-model] module toohello experiment canvas, and connect hello output of hello [Score Model][score-model] module toohello left input of [Evaluate Model][evaluate-model].</span></span>

    > [!TIP]
    > <span data-ttu-id="95488-305">Hay dos puertos de entrada en hello [evaluar modelo] [ evaluate-model] módulo porque puede ser usado toocompare dos modelos en paralelo.</span><span class="sxs-lookup"><span data-stu-id="95488-305">There are two input ports on hello [Evaluate Model][evaluate-model] module because it can be used toocompare two models side by side.</span></span> <span data-ttu-id="95488-306">Más adelante, puede agregar otro experimento de toohello de algoritmo y usar [evaluar modelo] [ evaluate-model] toosee cuál ofrece mejores resultados.</span><span class="sxs-lookup"><span data-stu-id="95488-306">Later, you can add another algorithm toohello experiment and use [Evaluate Model][evaluate-model] toosee which one gives better results.</span></span>

4. <span data-ttu-id="95488-307">Ejecute el experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="95488-307">Run hello experiment.</span></span>

<span data-ttu-id="95488-308">salida de hello tooview de hello [evaluar modelo] [ evaluate-model] módulo, haga clic en el puerto de salida de hello y, a continuación, seleccione **visualizar**.</span><span class="sxs-lookup"><span data-stu-id="95488-308">tooview hello output from hello [Evaluate Model][evaluate-model] module, click hello output port, and then select **Visualize**.</span></span>

<span data-ttu-id="95488-309">![Resultados de la evaluación de experimento Hola][evaluation-results]
</span><span class="sxs-lookup"><span data-stu-id="95488-309">![Evaluation results for hello experiment][evaluation-results]
</span></span><br/><span data-ttu-id="95488-310">
***Resultados de la evaluación de experimento Hola***</span><span class="sxs-lookup"><span data-stu-id="95488-310">
***Evaluation results for hello experiment***</span></span>

<span data-ttu-id="95488-311">Hola siguiendo las estadísticas se muestra para nuestro modelo:</span><span class="sxs-lookup"><span data-stu-id="95488-311">hello following statistics are shown for our model:</span></span>

- <span data-ttu-id="95488-312">**Desviación Media** (MAE): Hola promedio de errores absolutos (un *error* Hola diferencia entre Hola predecir el valor y el valor real de hello).</span><span class="sxs-lookup"><span data-stu-id="95488-312">**Mean Absolute Error** (MAE): hello average of absolute errors (an *error* is hello difference between hello predicted value and hello actual value).</span></span>
- <span data-ttu-id="95488-313">**Raíz del Error cuadrático significa** (RMSE): raíz cuadrada de Hola de Media de Hola de errores al cuadrado de predicciones realizadas en el conjunto de datos de prueba de Hola.</span><span class="sxs-lookup"><span data-stu-id="95488-313">**Root Mean Squared Error** (RMSE): hello square root of hello average of squared errors of predictions made on hello test dataset.</span></span>
- <span data-ttu-id="95488-314">**Error absoluto relativo**: Hola promedio de errores absoluta toohello relativo absoluto de la diferencia entre los valores reales y el promedio de Hola de todos los valores reales.</span><span class="sxs-lookup"><span data-stu-id="95488-314">**Relative Absolute Error**: hello average of absolute errors relative toohello absolute difference between actual values and hello average of all actual values.</span></span>
- <span data-ttu-id="95488-315">**Error cuadrático relativo**: promedio de Hola de errores al cuadrado relativo toohello cuadrado diferencia entre los valores reales de Hola y el promedio de Hola de todos los valores reales.</span><span class="sxs-lookup"><span data-stu-id="95488-315">**Relative Squared Error**: hello average of squared errors relative toohello squared difference between hello actual values and hello average of all actual values.</span></span>
- <span data-ttu-id="95488-316">**Coeficiente de determinación**: también se denomina hello **R cuadrado valor**, se trata de una métrica de estadística que indica el grado en que un modelo se adapta a los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="95488-316">**Coefficient of Determination**: Also known as hello **R squared value**, this is a statistical metric indicating how well a model fits hello data.</span></span>

<span data-ttu-id="95488-317">Para cada uno de los errores de hello estadísticas, menor es mejor.</span><span class="sxs-lookup"><span data-stu-id="95488-317">For each of hello error statistics, smaller is better.</span></span> <span data-ttu-id="95488-318">Un valor inferior indica que las predicciones de hello hacerlos coincidir con los valores reales de Hola.</span><span class="sxs-lookup"><span data-stu-id="95488-318">A smaller value indicates that hello predictions more closely match hello actual values.</span></span> <span data-ttu-id="95488-319">Para **coeficiente de determinación**, hello más cerca su valor es tooone (1.0), mejores predicciones de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="95488-319">For **Coefficient of Determination**, hello closer its value is tooone (1.0), hello better hello predictions.</span></span>

## <a name="final-experiment"></a><span data-ttu-id="95488-320">Experimento final</span><span class="sxs-lookup"><span data-stu-id="95488-320">Final experiment</span></span>

<span data-ttu-id="95488-321">experimento final Hola debe tener un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="95488-321">hello final experiment should look something like this:</span></span>

<span data-ttu-id="95488-322">![experimento final Hola][complete-linear-regression-experiment]
</span><span class="sxs-lookup"><span data-stu-id="95488-322">![hello final experiment][complete-linear-regression-experiment]
</span></span><br/><span data-ttu-id="95488-323">
***experimento final Hola***</span><span class="sxs-lookup"><span data-stu-id="95488-323">
***hello final experiment***</span></span>

## <a name="next-steps"></a><span data-ttu-id="95488-324">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="95488-324">Next steps</span></span>

<span data-ttu-id="95488-325">Ahora que ha completado el primer tutorial de aprendizaje de máquina hello y tienen su experimento configurado, puede seguir el modelo de hello tooimprove y, a continuación, implementarlo como un servicio web de predicción.</span><span class="sxs-lookup"><span data-stu-id="95488-325">Now that you've completed hello first machine learning tutorial and have your experiment set up, you can continue tooimprove hello model and then deploy it as a predictive web service.</span></span>

- <span data-ttu-id="95488-326">**Recorrer en el modelo de hello tooimprove tootry** -por ejemplo, puede cambiar las características de Hola que usar en la predicción.</span><span class="sxs-lookup"><span data-stu-id="95488-326">**Iterate tootry tooimprove hello model** - For example, you can change hello features you use in your prediction.</span></span> <span data-ttu-id="95488-327">O puede modificar las propiedades de Hola de hello [regresión lineal] [ linear-regression] algoritmo o intente un algoritmo diferente por completo.</span><span class="sxs-lookup"><span data-stu-id="95488-327">Or you can modify hello properties of hello [Linear Regression][linear-regression] algorithm or try a different algorithm altogether.</span></span> <span data-ttu-id="95488-328">Incluso puede agregar varios equipos al mismo tiempo los algoritmos tooyour experimento de aprendizaje y comparar dos de ellos utilizando hello [evaluar modelo] [ evaluate-model] módulo.</span><span class="sxs-lookup"><span data-stu-id="95488-328">You can even add multiple machine learning algorithms tooyour experiment at one time and compare two of them by using hello [Evaluate Model][evaluate-model] module.</span></span>
<span data-ttu-id="95488-329">Para obtener un ejemplo de cómo toocompare varios modelos en un experimento único, vea [comparación de regresores](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) en hello [Cortana Intelligence galería](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="95488-329">For an example of how toocompare multiple models in a single experiment, see [Compare Regressors](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span>

    > [!TIP]
    > <span data-ttu-id="95488-330">toocopy alguna iteración del experimento, use hello **SAVE AS** situado en la parte inferior de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="95488-330">toocopy any iteration of your experiment, use hello **SAVE AS** button at hello bottom of hello page.</span></span> <span data-ttu-id="95488-331">Puede ver todas las iteraciones de Hola de su experimento haciendo clic en **ver el historial de ejecución** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="95488-331">You can see all hello iterations of your experiment by clicking **VIEW RUN HISTORY** at hello bottom of hello page.</span></span> <span data-ttu-id="95488-332">Para más información, consulte [Administración de iteraciones de experimentos en Azure Machine Learning Studio][runhistory].</span><span class="sxs-lookup"><span data-stu-id="95488-332">For more details, see [Manage experiment iterations in Azure Machine Learning Studio][runhistory].</span></span>

[runhistory]: machine-learning-manage-experiment-iterations.md

- <span data-ttu-id="95488-333">**Implementar modelo Hola como un servicio web de predicción** : cuando esté satisfecho con el modelo, puede implementar como un toobe de servicio web utiliza los precios de automóviles toopredict mediante el uso de nuevos datos.</span><span class="sxs-lookup"><span data-stu-id="95488-333">**Deploy hello model as a predictive web service** - When you're satisfied with your model, you can deploy it as a web service toobe used toopredict automobile prices by using new data.</span></span> <span data-ttu-id="95488-334">Para más información, consulte [Implementar un servicio web Azure Machine Learning][publish].</span><span class="sxs-lookup"><span data-stu-id="95488-334">For more details, see [Deploy an Azure Machine Learning web service][publish].</span></span>

[publish]: machine-learning-publish-a-machine-learning-web-service.md

<span data-ttu-id="95488-335">¿Desea toolearn más?</span><span class="sxs-lookup"><span data-stu-id="95488-335">Want toolearn more?</span></span> <span data-ttu-id="95488-336">Para ver un tutorial más amplio y detallado del proceso de Hola de crear, entrenamiento, puntuación e implementar un modelo, vea [desarrollar una solución de predicción mediante aprendizaje automático de Azure][walkthrough].</span><span class="sxs-lookup"><span data-stu-id="95488-336">For a more extensive and detailed walkthrough of hello process of creating, training, scoring, and deploying a model, see [Develop a predictive solution by using Azure Machine Learning][walkthrough].</span></span>

[walkthrough]: machine-learning-walkthrough-develop-predictive-solution.md

<!-- Images -->
[sign-in-to-studio]: ./media/machine-learning-create-experiment/sign-in-to-studio.png
[rename-experiment]: ./media/machine-learning-create-experiment/rename-experiment.png
[visualize-auto-data]:./media/machine-learning-create-experiment/visualize-auto-data.png
[select-visualize]: ./media/machine-learning-create-experiment/select-visualize.png
[showing-excluded-column]:./media/machine-learning-create-experiment/showing-excluded-column.png
[set-remove-entire-row]:./media/machine-learning-create-experiment/set-remove-entire-row.png
[early-experiment-run]:./media/machine-learning-create-experiment/early-experiment-run.png
[select-columns-to-include]:./media/machine-learning-create-experiment/select-columns-to-include.png
[second-experiment-run]:./media/machine-learning-create-experiment/second-experiment-run.png
[connect-score-model]:./media/machine-learning-create-experiment/connect-score-model.png
[evaluation-results]:./media/machine-learning-create-experiment/evaluation-results.png
[complete-linear-regression-experiment]:./media/machine-learning-create-experiment/complete-linear-regression-experiment.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[type-automobile]:./media/machine-learning-create-experiment/type-automobile.png
[type-select-columns]:./media/machine-learning-create-experiment/type-select-columns.png
[launch-column-selector]:./media/machine-learning-create-experiment/launch-column-selector.png
[add-comment]:./media/machine-learning-create-experiment/add-comment.png
[connect-clean-to-select]:./media/machine-learning-create-experiment/connect-clean-to-select.png

[set-split-data-percentage]:./media/machine-learning-create-experiment/set-split-data-percentage.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[connect-train-model]:./media/machine-learning-create-experiment/connect-train-model.png
[select-price-column]:./media/machine-learning-create-experiment/select-price-column.png

[score-model-output]:./media/machine-learning-create-experiment/score-model-output.png

<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
