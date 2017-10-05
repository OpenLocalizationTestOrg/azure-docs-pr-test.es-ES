---
title: Un experimento sencillo en Machine Learning Studio | Microsoft Docs
description: "Este tutorial de aprendizaje automático le guiará a través de un sencillo experimento de ciencia de datos. Podremos predecir el precio de un automóvil mediante un algoritmo de regresión."
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
ms.openlocfilehash: 0539e9d04c61d35de56a29d350c07654c095c576
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="machine-learning-tutorial-create-your-first-data-science-experiment-in-azure-machine-learning-studio"></a><span data-ttu-id="32caf-105">Tutorial de aprendizaje automático: creación del primer experimento de ciencia de datos en Estudio de aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="32caf-105">Machine learning tutorial: Create your first data science experiment in Azure Machine Learning Studio</span></span>

<span data-ttu-id="32caf-106">Si nunca ha usado **Azure Machine Learning Studio** antes, este tutorial le ayudará.</span><span class="sxs-lookup"><span data-stu-id="32caf-106">If you've never used **Azure Machine Learning Studio** before, this tutorial is for you.</span></span>

<span data-ttu-id="32caf-107">Le mostraremos cómo usar Studio por primera vez para crear un experimento de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="32caf-107">In this tutorial, we'll walk through how to use Studio for the first time to create a machine learning experiment.</span></span> <span data-ttu-id="32caf-108">En dicho experimento probaremos un modelo analítico que predice el precio de un automóvil en función de diferentes variables, como la marca y las especificaciones técnicas.</span><span class="sxs-lookup"><span data-stu-id="32caf-108">The experiment will test an analytical model that predicts the price of an automobile based on different variables such as make and technical specifications.</span></span>

> [!NOTE]
> <span data-ttu-id="32caf-109">En este tutorial se muestran los conceptos básicos de cómo arrastrar y colocar módulos en el experimento, conectarlos, ejecutar el experimento y examinar los resultados.</span><span class="sxs-lookup"><span data-stu-id="32caf-109">This tutorial shows you the basics of how to drag-and-drop modules onto your experiment, connect them together, run the experiment, and look at the results.</span></span> <span data-ttu-id="32caf-110">No vamos a explicar el tema general de aprendizaje automático o cómo seleccionar y usar los más de 100 algoritmos integrados y módulos de manipulación de datos incluidos en Studio.</span><span class="sxs-lookup"><span data-stu-id="32caf-110">We're not going to discuss the general topic of machine learning or how to select and use the 100+ built-in algorithms and data manipulation modules included in Studio.</span></span>
>
><span data-ttu-id="32caf-111">Si está familiarizado con el aprendizaje automático, la serie de vídeos [Ciencia de datos para principiantes](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) podría ser un buen lugar para comenzar.</span><span class="sxs-lookup"><span data-stu-id="32caf-111">If you're new to machine learning, the video series [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) might be a good place to start.</span></span> <span data-ttu-id="32caf-112">Esta serie de vídeos es una excelente introducción al aprendizaje automático mediante el uso de conceptos y lenguaje cotidianos.</span><span class="sxs-lookup"><span data-stu-id="32caf-112">This video series is a great introduction to machine learning using everyday language and concepts.</span></span>
>
><span data-ttu-id="32caf-113">Si está familiarizado con el aprendizaje automático pero busca información más general sobre Machine Learning Studio y los algoritmos de aprendizaje automático que contiene, aquí se indican algunos buenos recursos:</span><span class="sxs-lookup"><span data-stu-id="32caf-113">If you're familiar with machine learning, but you're looking for more general information about Machine Learning Studio, and the machine learning algorithms it contains, here are some good resources:</span></span>
>
- [<span data-ttu-id="32caf-114">¿Qué es Estudio de aprendizaje automático?</span><span class="sxs-lookup"><span data-stu-id="32caf-114">What is Machine Learning Studio?</span></span>](machine-learning-what-is-ml-studio.md) <span data-ttu-id="32caf-115">- Esta es una descripción de alto nivel de Studio.</span><span class="sxs-lookup"><span data-stu-id="32caf-115">- This is a high-level overview of Studio.</span></span>
- <span data-ttu-id="32caf-116">[Conceptos básicos de aprendizaje automático con ejemplos de algoritmos](machine-learning-basics-infographic-with-algorithm-examples.md): esta infografía es útil si quiere aprender más sobre los diferentes tipos de algoritmos de aprendizaje automático que se incluyen con Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="32caf-116">[Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md) - This infographic is useful if you want to learn more about the different types of machine learning algorithms included with Machine Learning Studio.</span></span>
- <span data-ttu-id="32caf-117">[Guía de aprendizaje automático](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1): esta guía incluye información similar a la infografía mencionada anteriormente, pero en formato interactivo.</span><span class="sxs-lookup"><span data-stu-id="32caf-117">[Machine Learning Guide](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) - This guide covers similar information as the infographic above, but in an interactive format.</span></span>
- <span data-ttu-id="32caf-118">[Hoja de referencia rápida de algoritmos de aprendizaje automático ](machine-learning-algorithm-cheat-sheet.md) y [Cómo elegir algoritmos para Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md): este póster descargable y el artículo que le acompaña tratan en profundidad los algoritmos de Studio.</span><span class="sxs-lookup"><span data-stu-id="32caf-118">[Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md) and [How to choose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md) - This downloadable poster and accompanying article discuss the Studio algorithms in depth.</span></span>
- <span data-ttu-id="32caf-119">[Machine Learning Studio: Algorithm and Module Help](https://msdn.microsoft.com/library/azure/dn905974.aspx) (Machine Learning Studio: ayuda de algoritmos y módulos): esta es la referencia completa para todos los módulos de Studio, incluidos los algoritmos de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="32caf-119">[Machine Learning Studio: Algorithm and Module Help](https://msdn.microsoft.com/library/azure/dn905974.aspx) - This is the complete reference for all Studio modules, including machine learning algorithms,</span></span>

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-does-machine-learning-studio-help"></a><span data-ttu-id="32caf-120">¿Cómo funciona la ayuda de Estudio de aprendizaje automático?</span><span class="sxs-lookup"><span data-stu-id="32caf-120">How does Machine Learning Studio help?</span></span>

<span data-ttu-id="32caf-121">Estudio de aprendizaje automático facilita la configuración de un experimento con módulos de arrastrar y colocar programados previamente con técnicas de modelado predictivo.</span><span class="sxs-lookup"><span data-stu-id="32caf-121">Machine Learning Studio makes it easy to set up an experiment using drag-and-drop modules preprogrammed with predictive modeling techniques.</span></span>

<span data-ttu-id="32caf-122">Mediante un área de trabajo visual e interactiva, se arrastran y colocan ***conjuntos de datos*** y ***módulos*** de análisis en un lienzo interactivo.</span><span class="sxs-lookup"><span data-stu-id="32caf-122">Using an interactive, visual workspace, you drag-and-drop ***datasets*** and analysis ***modules*** onto an interactive canvas.</span></span> <span data-ttu-id="32caf-123">Luego se conectan para formar un ***experimento*** que se ejecuta en Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="32caf-123">You connect them together to form an ***experiment*** that you run in Machine Learning Studio.</span></span>
<span data-ttu-id="32caf-124">Se ***crea un modelo***, ***se entrena***, se ***puntúa y se prueba***.</span><span class="sxs-lookup"><span data-stu-id="32caf-124">You ***create a model***, ***train the model***, and ***score and test the model***.</span></span>

<span data-ttu-id="32caf-125">Puede iterar en el modelo de diseño y editar el experimento y ejecutarlo hasta que le proporcione los resultados que busca.</span><span class="sxs-lookup"><span data-stu-id="32caf-125">You can iterate on your model design, editing the experiment and running it until it gives you the results you're looking for.</span></span> <span data-ttu-id="32caf-126">Cuando el modelo está listo, puede publicarlo como un ***servicio web*** para que otros puedan enviarle nuevos datos y obtener a cambio predicciones.</span><span class="sxs-lookup"><span data-stu-id="32caf-126">When your model is ready, you can publish it as a ***web service*** so that others can send it new data and get predictions in return.</span></span>

## <a name="open-machine-learning-studio"></a><span data-ttu-id="32caf-127">Apertura de Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="32caf-127">Open Machine Learning Studio</span></span>

<span data-ttu-id="32caf-128">Para empezar a trabajar con Studio, vaya a [https://studio.azureml.net](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="32caf-128">To get started with Studio, go to [https://studio.azureml.net](https://studio.azureml.net).</span></span> <span data-ttu-id="32caf-129">Si ya se ha registrado en Machine Learning Studio antes, haga clic en **Sign In** (Iniciar sesión).</span><span class="sxs-lookup"><span data-stu-id="32caf-129">If you’ve signed into Machine Learning Studio before, click **Sign In**.</span></span> <span data-ttu-id="32caf-130">De lo contrario, haga clic en **Sign up here** (Regístrese aquí) y elija entre opciones gratuitas y de pago.</span><span class="sxs-lookup"><span data-stu-id="32caf-130">Otherwise, click **Sign up here** and choose between free and paid options.</span></span>

<span data-ttu-id="32caf-131">![Iniciar sesión en Machine Learning Studio][sign-in-to-studio]
</span><span class="sxs-lookup"><span data-stu-id="32caf-131">![Sign in to Machine Learning Studio][sign-in-to-studio]
</span></span><br/><span data-ttu-id="32caf-132">
***Iniciar sesión en Machine Learning Studio***</span><span class="sxs-lookup"><span data-stu-id="32caf-132">
***Sign in to Machine Learning Studio***</span></span>

## <a name="five-steps-to-create-an-experiment"></a><span data-ttu-id="32caf-133">Cinco pasos para crear un experimento</span><span class="sxs-lookup"><span data-stu-id="32caf-133">Five steps to create an experiment</span></span>

<span data-ttu-id="32caf-134">En este tutorial de aprendizaje automático se enumeran los cinco pasos básicos que puede llevar a cabo para crear un experimento en Machine Learning Studio para crear, entrenar y puntuar el modelo:</span><span class="sxs-lookup"><span data-stu-id="32caf-134">In this machine learning tutorial, you'll follow five basic steps to build an experiment in Machine Learning Studio to create, train, and score your model:</span></span>

- <span data-ttu-id="32caf-135">**Crear un modelo**</span><span class="sxs-lookup"><span data-stu-id="32caf-135">**Create a model**</span></span>
    - <span data-ttu-id="32caf-136">[Paso 1: Obtener los datos]</span><span class="sxs-lookup"><span data-stu-id="32caf-136">[Step 1: Get data]</span></span>
    - <span data-ttu-id="32caf-137">[Paso 2: Preparar los datos]</span><span class="sxs-lookup"><span data-stu-id="32caf-137">[Step 2: Prepare the data]</span></span>
    - <span data-ttu-id="32caf-138">[Paso 3: Definir las características]</span><span class="sxs-lookup"><span data-stu-id="32caf-138">[Step 3: Define features]</span></span>
- <span data-ttu-id="32caf-139">**Entrenar el modelo**</span><span class="sxs-lookup"><span data-stu-id="32caf-139">**Train the model**</span></span>
    - <span data-ttu-id="32caf-140">[Paso 4: Elegir y aplicar un algoritmo de aprendizaje]</span><span class="sxs-lookup"><span data-stu-id="32caf-140">[Step 4: Choose and apply a learning algorithm]</span></span>
- <span data-ttu-id="32caf-141">**Puntuar y probar el modelo**</span><span class="sxs-lookup"><span data-stu-id="32caf-141">**Score and test the model**</span></span>
    - <span data-ttu-id="32caf-142">[Paso 5: Predecir los precios de los automóviles nuevos]</span><span class="sxs-lookup"><span data-stu-id="32caf-142">[Step 5: Predict new automobile prices]</span></span>

<span data-ttu-id="32caf-143">[Paso 1: Obtener los datos]: #step-1-get-data</span><span class="sxs-lookup"><span data-stu-id="32caf-143">[Step 1: Get data]: #step-1-get-data</span></span>
<span data-ttu-id="32caf-144">[Paso 2: Preparar los datos]: #step-2-prepare-the-data</span><span class="sxs-lookup"><span data-stu-id="32caf-144">[Step 2: Prepare the data]: #step-2-prepare-the-data</span></span>
<span data-ttu-id="32caf-145">[Paso 3: Definir las características]: #step-3-define-features</span><span class="sxs-lookup"><span data-stu-id="32caf-145">[Step 3: Define features]: #step-3-define-features</span></span>
<span data-ttu-id="32caf-146">[Paso 4: Elegir y aplicar un algoritmo de aprendizaje]: #step-4-choose-and-apply-a-learning-algorithm</span><span class="sxs-lookup"><span data-stu-id="32caf-146">[Step 4: Choose and apply a learning algorithm]: #step-4-choose-and-apply-a-learning-algorithm</span></span>
<span data-ttu-id="32caf-147">[Paso 5: Predecir los precios de los automóviles nuevos]: #step-5-predict-new-automobile-prices</span><span class="sxs-lookup"><span data-stu-id="32caf-147">[Step 5: Predict new automobile prices]: #step-5-predict-new-automobile-prices</span></span>

> [!TIP] 
> <span data-ttu-id="32caf-148">Puede encontrar una copia de trabajo del experimento siguiente en la [galería de Cortana Intelligence](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="32caf-148">You can find a working copy of the following experiment in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="32caf-149">Vaya a **[Your first data science experiment - Automobile price prediction](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)** (Su primer experimento de ciencia de los datos: predicción de los precios de automóviles) y haga clic en **Abrir en Studio** para descargar una copia del experimento en su área de trabajo de Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="32caf-149">Go to **[Your first data science experiment - Automobile price prediction](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)** and click **Open in Studio** to download a copy of the experiment into your Machine Learning Studio workspace.</span></span>


## <a name="step-1-get-data"></a><span data-ttu-id="32caf-150">Paso 1: Obtener los datos</span><span class="sxs-lookup"><span data-stu-id="32caf-150">Step 1: Get data</span></span>

<span data-ttu-id="32caf-151">Lo primero que necesita para ejecutar aprendizaje automático son datos.</span><span class="sxs-lookup"><span data-stu-id="32caf-151">The first thing you need to perform machine learning is data.</span></span>
<span data-ttu-id="32caf-152">Machine Learning Studio incluye varios conjuntos de datos que puede usar; otra opción es importarlos de diversos orígenes.</span><span class="sxs-lookup"><span data-stu-id="32caf-152">There are several sample datasets included with Machine Learning Studio that you can use, or you can import data from many sources.</span></span> <span data-ttu-id="32caf-153">En este ejemplo, usaremos el conjunto de datos de ejemplo, **Automobile price data (Raw)**, que se incluye en el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="32caf-153">For this example, we'll use the sample dataset, **Automobile price data (Raw)**, that's included in your workspace.</span></span>
<span data-ttu-id="32caf-154">Este conjunto de datos incluye entradas para diversos automóviles individuales, por ejemplo, información sobre la marca, el modelo, las especificaciones técnicas y el precio.</span><span class="sxs-lookup"><span data-stu-id="32caf-154">This dataset includes entries for various individual automobiles, including information such as make, model, technical specifications, and price.</span></span>

<span data-ttu-id="32caf-155">Aquí se muestra cómo obtener el conjunto de datos en el experimento.</span><span class="sxs-lookup"><span data-stu-id="32caf-155">Here's how to get the dataset into your experiment.</span></span>

1. <span data-ttu-id="32caf-156">Cree un experimento nuevo; para ello, haga clic en **+NUEVO** en la parte inferior de la ventana de Machine Learning Studio, seleccione **EXPERIMENTO** y luego **Experimento en blanco**.</span><span class="sxs-lookup"><span data-stu-id="32caf-156">Create a new experiment by clicking **+NEW** at the bottom of the Machine Learning Studio window, select **EXPERIMENT**, and then select **Blank Experiment**.</span></span>

2. <span data-ttu-id="32caf-157">El experimento recibe un nombre predeterminado que puede ver en la parte superior del lienzo.</span><span class="sxs-lookup"><span data-stu-id="32caf-157">The experiment is given a default name that you can see at the top of the canvas.</span></span> <span data-ttu-id="32caf-158">Seleccione este texto y cambie su nombre por algo significativo, por ejemplo, **predicción de precios de automóviles**.</span><span class="sxs-lookup"><span data-stu-id="32caf-158">Select this text and rename it to something meaningful, for example, **Automobile price prediction**.</span></span> <span data-ttu-id="32caf-159">No es necesario que el nombre sea único.</span><span class="sxs-lookup"><span data-stu-id="32caf-159">The name doesn't need to be unique.</span></span>

    ![Renombrar el experimento][rename-experiment]

2. <span data-ttu-id="32caf-161">A la izquierda del lienzo de experimentos, hay una paleta de conjuntos de datos y módulos.</span><span class="sxs-lookup"><span data-stu-id="32caf-161">To the left of the experiment canvas is a palette of datasets and modules.</span></span> <span data-ttu-id="32caf-162">Escriba **automobile** en el cuadro de búsqueda de la parte superior de esta paleta para encontrar el conjunto de datos llamado **Automobile price data (Raw)** (Datos de precios de automóviles [sin formato]).</span><span class="sxs-lookup"><span data-stu-id="32caf-162">Type **automobile** in the Search box at the top of this palette to find the dataset labeled **Automobile price data (Raw)**.</span></span> <span data-ttu-id="32caf-163">Arrastre este conjunto de datos al lienzo del experimento.</span><span class="sxs-lookup"><span data-stu-id="32caf-163">Drag this dataset to the experiment canvas.</span></span>

    <span data-ttu-id="32caf-164">![Buscar el conjunto de datos de automóvil y arrastrarlo hasta el lienzo del experimento][type-automobile]
    </span><span class="sxs-lookup"><span data-stu-id="32caf-164">![Find the automobile dataset and drag it onto the experiment canvas][type-automobile]
    </span></span><br/>
 <span data-ttu-id="32caf-165">***Busque el conjunto de datos de automóvil y arrástrela hasta el lienzo del experimento***</span><span class="sxs-lookup"><span data-stu-id="32caf-165">***Find the automobile dataset and drag it onto the experiment canvas***</span></span>

<span data-ttu-id="32caf-166">Para ver la apariencia de estos datos, haga clic en el puerto de salida, en la parte inferior del conjunto de datos de automóvil, y seleccione **Visualizar**.</span><span class="sxs-lookup"><span data-stu-id="32caf-166">To see what this data looks like, click the output port at the bottom of the automobile dataset, and then select **Visualize**.</span></span>

<span data-ttu-id="32caf-167">![Hacer clic en el puerto de salida y seleccionar "Visualizar"][select-visualize]
</span><span class="sxs-lookup"><span data-stu-id="32caf-167">![Click the output port and select "Visualize"][select-visualize]
</span></span><br/><span data-ttu-id="32caf-168">
***Hacer clic en el puerto de salida y seleccionar "Visualizar"***</span><span class="sxs-lookup"><span data-stu-id="32caf-168">
***Click the output port and select "Visualize"***</span></span>

> [!TIP]
> <span data-ttu-id="32caf-169">Los conjuntos de datos y los módulos tienen puertos de entrada y de salida representados por pequeños círculos: los puertos de entrada arriba y los puertos de salida abajo.</span><span class="sxs-lookup"><span data-stu-id="32caf-169">Datasets and modules have input and output ports represented by small circles - input ports at the top, output ports at the bottom.</span></span>
<span data-ttu-id="32caf-170">Para crear un flujo de datos a través del experimento, se conectará un puerto de salida de un módulo a un puerto de entrada de otro.</span><span class="sxs-lookup"><span data-stu-id="32caf-170">To create a flow of data through your experiment, you'll connect an output port of one module to an input port of another.</span></span>
<span data-ttu-id="32caf-171">En cualquier momento, puede hacer clic en el puerto de salida de un conjunto de datos o de un módulo para ver el aspecto de los datos en ese punto del flujo de datos.</span><span class="sxs-lookup"><span data-stu-id="32caf-171">At any time, you can click the output port of a dataset or module to see what the data looks like at that point in the data flow.</span></span>

<span data-ttu-id="32caf-172">En este conjunto de datos de ejemplo, cada instancia de un automóvil aparece como una fila y las variables asociadas a cada automóvil como columnas.</span><span class="sxs-lookup"><span data-stu-id="32caf-172">In this sample dataset, each instance of an automobile appears as a row, and the variables associated with each automobile appear as columns.</span></span> <span data-ttu-id="32caf-173">Dadas las variables para un automóvil determinado, vamos a intentar predecir el precio de la columna del extremo derecho (columna 26, llamada "precio").</span><span class="sxs-lookup"><span data-stu-id="32caf-173">Given the variables for a specific automobile, we're going to try to predict the price in far-right column (column 26, titled "price").</span></span>

<span data-ttu-id="32caf-174">![Ver los datos de automóviles en la ventana de visualización de datos][visualize-auto-data]
</span><span class="sxs-lookup"><span data-stu-id="32caf-174">![View the automobile data in the data visualization window][visualize-auto-data]
</span></span><br/><span data-ttu-id="32caf-175">
***Ver los datos de automóviles en la ventana de visualización de datos***</span><span class="sxs-lookup"><span data-stu-id="32caf-175">
***View the automobile data in the data visualization window***</span></span>

<span data-ttu-id="32caf-176">Cierre la ventana de visualización haciendo clic en la "**x**" en la esquina superior derecha.</span><span class="sxs-lookup"><span data-stu-id="32caf-176">Close the visualization window by clicking the "**x**" in the upper-right corner.</span></span>

## <a name="step-2-prepare-the-data"></a><span data-ttu-id="32caf-177">Paso 2: Preparar los datos</span><span class="sxs-lookup"><span data-stu-id="32caf-177">Step 2: Prepare the data</span></span>

<span data-ttu-id="32caf-178">Normalmente, un conjunto de datos requiere algún procesamiento previo antes de que se pueda analizar.</span><span class="sxs-lookup"><span data-stu-id="32caf-178">A dataset usually requires some preprocessing before it can be analyzed.</span></span> <span data-ttu-id="32caf-179">Por ejemplo, puede que haya observado los valores que faltan en las columnas de varias filas.</span><span class="sxs-lookup"><span data-stu-id="32caf-179">For example, you might have noticed the missing values present in the columns of various rows.</span></span> <span data-ttu-id="32caf-180">Estos valores que faltan se deben limpiar para que el modelo pueda analizar los datos de manera adecuada.</span><span class="sxs-lookup"><span data-stu-id="32caf-180">These missing values need to be cleaned so the model can analyze the data correctly.</span></span> <span data-ttu-id="32caf-181">En nuestro caso, quitaremos todas las filas que tengan valores ausentes.</span><span class="sxs-lookup"><span data-stu-id="32caf-181">In our case, we'll remove any rows that have missing values.</span></span> <span data-ttu-id="32caf-182">Además, la columna **normalized-losses** tiene una gran proporción de valores que faltan, por lo que excluiremos esa columna del modelo por completo.</span><span class="sxs-lookup"><span data-stu-id="32caf-182">Also, the **normalized-losses** column has a large proportion of missing values, so we'll exclude that column from the model altogether.</span></span>

> [!TIP]
> <span data-ttu-id="32caf-183">Limpiar los valores que faltan de los datos de entrada es un requisito previo para usar la mayoría de los módulos.</span><span class="sxs-lookup"><span data-stu-id="32caf-183">Cleaning the missing values from input data is a prerequisite for using most of the modules.</span></span>

<span data-ttu-id="32caf-184">Primero agregaremos un módulo que quite completamente la columna **normalized-losses** y luego agregaremos otro módulo que quite cualquier fila a la que le falten datos.</span><span class="sxs-lookup"><span data-stu-id="32caf-184">First we add a module that removes the **normalized-losses** column completely, and then we add another module that removes any row that has missing data.</span></span>

1. <span data-ttu-id="32caf-185">Escriba **seleccionar columnas** en el cuadro de búsqueda de la parte superior de la paleta de módulos, y busque [Select Columns in Dataset] (Seleccionar columnas en el conjunto de datos) [select-columns]; después, arrastre este módulo al lienzo del experimento.</span><span class="sxs-lookup"><span data-stu-id="32caf-185">Type **select columns** in the Search box at the top of the module palette to find the [Select Columns in Dataset][select-columns] module, then drag it to the experiment canvas.</span></span> <span data-ttu-id="32caf-186">Este módulo nos permite seleccionar las columnas de datos que queremos incluir o excluir del modelo.</span><span class="sxs-lookup"><span data-stu-id="32caf-186">This module allows us to select which columns of data we want to include or exclude in the model.</span></span>

2. <span data-ttu-id="32caf-187">Conecte el puerto de salida del conjunto de datos **Automobile price data (Raw)** al puerto de entrada del módulo [Select Columns in Dataset] (Seleccionar columnas en el conjunto de datos) [select-columns].</span><span class="sxs-lookup"><span data-stu-id="32caf-187">Connect the output port of the **Automobile price data (Raw)** dataset to the input port of the [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="32caf-188">![Agregar el módulo "Seleccionar columnas en el conjunto de datos" al lienzo del experimento y conectarlo][type-select-columns]
    </span><span class="sxs-lookup"><span data-stu-id="32caf-188">![Add the "Select Columns in Dataset" module to the experiment canvas and connect it][type-select-columns]
    </span></span><br/>
 <span data-ttu-id="32caf-189">***Agregar el módulo "Seleccionar columnas de conjunto de datos" al lienzo del experimento y conéctelo***</span><span class="sxs-lookup"><span data-stu-id="32caf-189">***Add the "Select Columns in Dataset" module to the experiment canvas and connect it***</span></span>

3. <span data-ttu-id="32caf-190">Haga clic en el módulo [Select Columns in Dataset] (Seleccionar columnas en el conjunto de datos) [select-columns] y haga clic en **Launch column selector** (Iniciar el selector de columnas) en el panel **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="32caf-190">Click the [Select Columns in Dataset][select-columns] module and click **Launch column selector** in the **Properties** pane.</span></span>

    - <span data-ttu-id="32caf-191">A la izquierda, haga clic en **Con reglas**</span><span class="sxs-lookup"><span data-stu-id="32caf-191">On the left, click **With rules**</span></span>
    - <span data-ttu-id="32caf-192">En **Empiezan por**, haga clic en **Todas las columnas**.</span><span class="sxs-lookup"><span data-stu-id="32caf-192">Under **Begin With**, click **All columns**.</span></span> <span data-ttu-id="32caf-193">Esto indica a [Select Columns in Dataset] (Seleccionar columnas en el conjunto de datos) [select-columns] que pase por todas las columnas (excepto las que se van a excluir).</span><span class="sxs-lookup"><span data-stu-id="32caf-193">This directs [Select Columns in Dataset][select-columns] to pass through all the columns (except those columns we're about to exclude).</span></span>
    - <span data-ttu-id="32caf-194">En los menús desplegables, seleccione **Excluir** y **nombres de columna** y luego haga clic en el cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="32caf-194">From the drop-downs, select **Exclude** and **column names**, and then click inside the text box.</span></span> <span data-ttu-id="32caf-195">A continuación, se mostrará una lista de columnas.</span><span class="sxs-lookup"><span data-stu-id="32caf-195">A list of columns is displayed.</span></span> <span data-ttu-id="32caf-196">Seleccione **normalized-losses**; se agregará al cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="32caf-196">Select **normalized-losses**, and it's added to the text box.</span></span>
    - <span data-ttu-id="32caf-197">Haga clic en el botón Aceptar con la marca de verificación para cerrar el selector de columnas (en la esquina inferior derecha).</span><span class="sxs-lookup"><span data-stu-id="32caf-197">Click the check mark (OK) button to close the column selector (on the lower-right).</span></span>

    <span data-ttu-id="32caf-198">![Iniciar el selector de columnas y excluir la columna "normalized-losses"][launch-column-selector]
    </span><span class="sxs-lookup"><span data-stu-id="32caf-198">![Launch the column selector and exclude the "normalized-losses" column][launch-column-selector]
    </span></span><br/>
 <span data-ttu-id="32caf-199">***Iniciar el selector de columnas y excluir la columna "pérdidas normalizadas"***</span><span class="sxs-lookup"><span data-stu-id="32caf-199">***Launch the column selector and exclude the "normalized-losses" column***</span></span>

    <span data-ttu-id="32caf-200">Ahora el panel de propiedades de **Select Columns in Dataset** (Seleccionar columnas en el conjunto de datos) indica que se pasará por todas las columnas del conjunto de datos excepto **normalized-losses**.</span><span class="sxs-lookup"><span data-stu-id="32caf-200">Now the properties pane for **Select Columns in Dataset** indicates that it will pass through all columns from the dataset except **normalized-losses**.</span></span>

    <span data-ttu-id="32caf-201">![El panel de propiedades muestra que la columna "normalized-losses" se ha excluido][showing-excluded-column]
    </span><span class="sxs-lookup"><span data-stu-id="32caf-201">![The properties pane shows that the "normalized-losses" column is excluded][showing-excluded-column]
    </span></span><br/>
 <span data-ttu-id="32caf-202">***El panel Propiedades muestra que se ha excluido la columna "pérdidas normalizadas"***</span><span class="sxs-lookup"><span data-stu-id="32caf-202">***The properties pane shows that the "normalized-losses" column is excluded***</span></span>

    > [!TIP]
    <span data-ttu-id="32caf-203">Puede agregar un comentario a un módulo; para ello, haga doble clic en el módulo y escriba texto.</span><span class="sxs-lookup"><span data-stu-id="32caf-203">You can add a comment to a module by double-clicking the module and entering text.</span></span> <span data-ttu-id="32caf-204">Esto puede ayudarle a ver de un vistazo lo que el módulo hace en el experimento.</span><span class="sxs-lookup"><span data-stu-id="32caf-204">This can help you see at a glance what the module is doing in your experiment.</span></span> <span data-ttu-id="32caf-205">En este caso, haga doble clic en el módulo [Select Columns in Dataset][select-columns] (Seleccionar columnas en el conjunto de datos) y escriba el comentario "Excluir normalized-losses".</span><span class="sxs-lookup"><span data-stu-id="32caf-205">In this case double-click the [Select Columns in Dataset][select-columns] module and type the comment "Exclude normalized losses."</span></span>
    >
    >


    <span data-ttu-id="32caf-206">![Hacer doble clic en un módulo para agregar un comentario][add-comment]
    </span><span class="sxs-lookup"><span data-stu-id="32caf-206">![Double-click a module to add a comment][add-comment]
    </span></span><br/>
 <span data-ttu-id="32caf-207">***Haga doble clic en un módulo para agregar un comentario***</span><span class="sxs-lookup"><span data-stu-id="32caf-207">***Double-click a module to add a comment***</span></span>

3. <span data-ttu-id="32caf-208">Arrastre el módulo [Clean Missing Data][clean-missing-data] (Limpiar los datos que faltan) al lienzo del experimento y conéctelo con el módulo [Select Columns in Dataset][select-columns] (Seleccionar columnas en el conjunto de datos).</span><span class="sxs-lookup"><span data-stu-id="32caf-208">Drag the [Clean Missing Data][clean-missing-data] module to the experiment canvas and connect it to the [Select Columns in Dataset][select-columns] module.</span></span> <span data-ttu-id="32caf-209">En el panel **Propiedades**, seleccione **Remove entire row** (Quitar la fila entera) en **Cleaning mode** (Modo de limpieza).</span><span class="sxs-lookup"><span data-stu-id="32caf-209">In the **Properties** pane, select **Remove entire row** under **Cleaning mode**.</span></span> <span data-ttu-id="32caf-210">Esto indica al módulo [Clean Missing Data] (Limpiar los datos que faltan) [clean-missing-data] que quite las filas que tienen valores que faltan para limpiar los datos.</span><span class="sxs-lookup"><span data-stu-id="32caf-210">This directs [Clean Missing Data][clean-missing-data] to clean the data by removing rows that have any missing values.</span></span> <span data-ttu-id="32caf-211">Haga doble clic en el módulo y escriba el comentario "Quitar las filas sin valor".</span><span class="sxs-lookup"><span data-stu-id="32caf-211">Double-click the module and type the comment "Remove missing value rows."</span></span>

    <span data-ttu-id="32caf-212">![Establecer el modo de limpieza en "Quitar la fila entera" para el módulo "Limpiar los datos que faltan"][set-remove-entire-row]
    </span><span class="sxs-lookup"><span data-stu-id="32caf-212">![Set the cleaning mode to "Remove entire row" for the "Clean Missing Data" module][set-remove-entire-row]
    </span></span><br/>
 <span data-ttu-id="32caf-213">***Establecer el modo de limpieza para "Quitar toda la fila" para el módulo "Limpiar datos que faltan"***</span><span class="sxs-lookup"><span data-stu-id="32caf-213">***Set the cleaning mode to "Remove entire row" for the "Clean Missing Data" module***</span></span>

4. <span data-ttu-id="32caf-214">Ejecute el experimento haciendo clic en **EJECUTAR** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="32caf-214">Run the experiment by clicking **RUN** at the bottom of the page.</span></span>

    <span data-ttu-id="32caf-215">Cuando el experimento finalice, todos los módulos tendrán una marca de verificación verde para indicar que se han completado correctamente.</span><span class="sxs-lookup"><span data-stu-id="32caf-215">When the experiment has finished running, all the modules have a green check mark to indicate that they finished successfully.</span></span> <span data-ttu-id="32caf-216">Observe también el estado **Ejecución finalizada** en la esquina superior derecha.</span><span class="sxs-lookup"><span data-stu-id="32caf-216">Notice also the **Finished running** status in the upper-right corner.</span></span>

<span data-ttu-id="32caf-217">![Después de ejecutarlo, el experimento debe tener un aspecto similar al siguiente][early-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="32caf-217">![After running it, the experiment should look something like this][early-experiment-run]
</span></span><br/><span data-ttu-id="32caf-218">
***Después de ejecutarlo, el experimento debe tener un aspecto similar al siguiente***</span><span class="sxs-lookup"><span data-stu-id="32caf-218">
***After running it, the experiment should look something like this***</span></span>

> [!TIP]
> <span data-ttu-id="32caf-219">¿Por qué ejecutamos el experimento ahora?</span><span class="sxs-lookup"><span data-stu-id="32caf-219">Why did we run the experiment now?</span></span> <span data-ttu-id="32caf-220">Al ejecutar el experimento, las definiciones de columna de nuestros datos pasan desde el conjunto de datos hasta los módulos [Select Columns in Dataset] (Seleccionar columnas en el conjunto de datos) [select-columns] y [Clean Missing Data] (Limpiar los datos que faltan) [clean-missing-data].</span><span class="sxs-lookup"><span data-stu-id="32caf-220">By running the experiment, the column definitions for our data pass from the dataset, through the [Select Columns in Dataset][select-columns] module, and through the [Clean Missing Data][clean-missing-data] module.</span></span> <span data-ttu-id="32caf-221">Esto significa que los módulos que conectamos a [Clean Missing Data] (Limpiar los datos que faltan) [clean-missing-data] tendrán también esta misma información.</span><span class="sxs-lookup"><span data-stu-id="32caf-221">This means that any modules we connect to [Clean Missing Data][clean-missing-data] will also have this same information.</span></span>

<span data-ttu-id="32caf-222">Todo lo que hemos hecho en el experimento hasta el momento es limpiar los datos.</span><span class="sxs-lookup"><span data-stu-id="32caf-222">All we have done in the experiment up to this point is clean the data.</span></span> <span data-ttu-id="32caf-223">Si quiere ver el conjunto de datos limpio, haga clic en el puerto de salida izquierdo del módulo [Clean Missing Data] (Limpiar los datos que faltan) [clean-missing-data] y seleccione **Visualizar**.</span><span class="sxs-lookup"><span data-stu-id="32caf-223">If you want to view the cleaned dataset, click the left output port of the [Clean Missing Data][clean-missing-data] module and select **Visualize**.</span></span> <span data-ttu-id="32caf-224">Observe que la columna **normalized-losses** ya no se incluye y que no hay valores que faltan.</span><span class="sxs-lookup"><span data-stu-id="32caf-224">Notice that the **normalized-losses** column is no longer included, and there are no missing values.</span></span>

<span data-ttu-id="32caf-225">Ahora los datos están limpios y ya puede especificar qué características se van a usar en el modelo predictivo.</span><span class="sxs-lookup"><span data-stu-id="32caf-225">Now that the data is clean, we're ready to specify what features we're going to use in the predictive model.</span></span>

## <a name="step-3-define-features"></a><span data-ttu-id="32caf-226">Paso 3: Definir las características</span><span class="sxs-lookup"><span data-stu-id="32caf-226">Step 3: Define features</span></span>

<span data-ttu-id="32caf-227">En el aprendizaje automático, las *características* son propiedades mensurables individuales de algo que le interesa.</span><span class="sxs-lookup"><span data-stu-id="32caf-227">In machine learning, *features* are individual measurable properties of something you’re interested in.</span></span> <span data-ttu-id="32caf-228">En nuestro conjunto de datos, cada fila representa un automóvil y cada columna es una característica de ese automóvil.</span><span class="sxs-lookup"><span data-stu-id="32caf-228">In our dataset, each row represents one automobile, and each column is a feature of that automobile.</span></span>

<span data-ttu-id="32caf-229">Encontrar un buen conjunto de funciones para la creación de un modelo de predicción requiere experimentación y conocimientos acerca del problema que desea resolver.</span><span class="sxs-lookup"><span data-stu-id="32caf-229">Finding a good set of features for creating a predictive model requires experimentation and knowledge about the problem you want to solve.</span></span> <span data-ttu-id="32caf-230">Algunas características son mejores para predecir el destino que otras.</span><span class="sxs-lookup"><span data-stu-id="32caf-230">Some features are better for predicting the target than others.</span></span> <span data-ttu-id="32caf-231">Además, algunas características tienen una correlación fuerte con otras y se pueden quitar.</span><span class="sxs-lookup"><span data-stu-id="32caf-231">Also, some features have a strong correlation with other features and can be removed.</span></span> <span data-ttu-id="32caf-232">Por ejemplo, city-mpg y highway-mpg están estrechamente relacionadas así que podemos mantener una y quitar la otra sin que tenga un impacto importante sobre la predicción.</span><span class="sxs-lookup"><span data-stu-id="32caf-232">For example, city-mpg and highway-mpg are closely related so we can keep one and remove the other without significantly affecting the prediction.</span></span>

<span data-ttu-id="32caf-233">Creemos un modelo que use un subconjunto de las funciones de nuestro conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="32caf-233">Let's build a model that uses a subset of the features in our dataset.</span></span> <span data-ttu-id="32caf-234">Puede volver más tarde y seleccionar diferentes características, ejecutar de nuevo el experimento y ver si obtiene mejores resultados.</span><span class="sxs-lookup"><span data-stu-id="32caf-234">You can come back later and select different features, run the experiment again, and see if you get better results.</span></span> <span data-ttu-id="32caf-235">Pero, para empezar, vamos a intentar las siguientes características:</span><span class="sxs-lookup"><span data-stu-id="32caf-235">But to start, let's try the following features:</span></span>

    make, body-style, wheel-base, engine-size, horsepower, peak-rpm, highway-mpg, price


1. <span data-ttu-id="32caf-236">Arrastre otro módulo [Select Columns in Dataset] (Seleccionar columnas en el conjunto de datos) [select-columns] al lienzo del experimento.</span><span class="sxs-lookup"><span data-stu-id="32caf-236">Drag another [Select Columns in Dataset][select-columns] module to the experiment canvas.</span></span> <span data-ttu-id="32caf-237">Conecte el puerto de salida izquierdo del módulo [Clean Missing Data] (Limpiar los datos que faltan) [clean-missing-data] a la entrada del módulo [Select Columns in Dataset] (Seleccionar columnas en el conjunto de datos) [select-columns].</span><span class="sxs-lookup"><span data-stu-id="32caf-237">Connect the left output port of the [Clean Missing Data][clean-missing-data] module to the input of the [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="32caf-238">![Conectar el módulo "Seleccionar columnas en el conjunto de datos" al módulo "Limpiar los datos que faltan"][connect-clean-to-select]
    </span><span class="sxs-lookup"><span data-stu-id="32caf-238">![Connect the "Select Columns in Dataset" module to the "Clean Missing Data" module][connect-clean-to-select]
    </span></span><br/>
 <span data-ttu-id="32caf-239">***Conecte el módulo "Seleccionar columnas de conjunto de datos" en el módulo "Limpiar datos que faltan"***</span><span class="sxs-lookup"><span data-stu-id="32caf-239">***Connect the "Select Columns in Dataset" module to the "Clean Missing Data" module***</span></span>

2. <span data-ttu-id="32caf-240">Haga doble clic en el módulo y escriba "Seleccionar funciones para la predicción".</span><span class="sxs-lookup"><span data-stu-id="32caf-240">Double-click the module and type "Select features for prediction."</span></span>

2. <span data-ttu-id="32caf-241">Haga clic en **Iniciar el selector de columnas** en el panel **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="32caf-241">Click **Launch column selector** in the **Properties** pane.</span></span>

3. <span data-ttu-id="32caf-242">Haga clic en **With rules**(Con reglas).</span><span class="sxs-lookup"><span data-stu-id="32caf-242">Click **With rules**.</span></span>

4. <span data-ttu-id="32caf-243">En **Empezar por**, haga clic en **No columns** (Ninguna columna).</span><span class="sxs-lookup"><span data-stu-id="32caf-243">Under **Begin With**, click **No columns**.</span></span> <span data-ttu-id="32caf-244">En la fila del filtro, seleccione **Incluir** y **nombres de columna** y seleccione nuestra lista de nombres de columna en el cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="32caf-244">In the filter row, select **Include** and **column names** and select our list of column names in the text box.</span></span> <span data-ttu-id="32caf-245">Esto indica al módulo que no pase por ninguna columna (características), a excepción de las especificadas.</span><span class="sxs-lookup"><span data-stu-id="32caf-245">This directs the module to not pass through any columns (features) except the ones that we specify.</span></span>

5. <span data-ttu-id="32caf-246">Haga clic en el botón de marca de verificación (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="32caf-246">Click the check mark (OK) button.</span></span>

    <span data-ttu-id="32caf-247">![Seleccionar las columnas (características) que se incluirán en la predicción][select-columns-to-include]
    </span><span class="sxs-lookup"><span data-stu-id="32caf-247">![Select the columns (features) to include in the prediction][select-columns-to-include]
    </span></span><br/>
 <span data-ttu-id="32caf-248">***Seleccione las columnas (funciones) que se incluirán en la predicción***</span><span class="sxs-lookup"><span data-stu-id="32caf-248">***Select the columns (features) to include in the prediction***</span></span>

<span data-ttu-id="32caf-249">Esto genera un conjunto de datos filtrado que contiene solo las características que queremos pasar al algoritmo de aprendizaje que usaremos en el siguiente paso.</span><span class="sxs-lookup"><span data-stu-id="32caf-249">This produces a filtered dataset containing only the features we want to pass to the learning algorithm we'll use in the next step.</span></span> <span data-ttu-id="32caf-250">Posteriormente puede volver e intentarlo de nuevo con una selección diferente de características.</span><span class="sxs-lookup"><span data-stu-id="32caf-250">Later, you can return and try again with a different selection of features.</span></span>

## <a name="step-4-choose-and-apply-a-learning-algorithm"></a><span data-ttu-id="32caf-251">Paso 4: Elegir y aplicar un algoritmo de aprendizaje</span><span class="sxs-lookup"><span data-stu-id="32caf-251">Step 4: Choose and apply a learning algorithm</span></span>

<span data-ttu-id="32caf-252">Ahora que los datos están listos, la construcción de un modelo predictivo consiste en entrenar y probar.</span><span class="sxs-lookup"><span data-stu-id="32caf-252">Now that the data is ready, constructing a predictive model consists of training and testing.</span></span> <span data-ttu-id="32caf-253">Usaremos nuestros datos para entrenar el modelo y luego probarlo para ver lo que se aproxima en sus predicciones de los precios.</span><span class="sxs-lookup"><span data-stu-id="32caf-253">We'll use our data to train the model, and then we'll test the model to see how closely it's able to predict prices.</span></span>
<!-- For now, don't worry about *why* we need to train and then test a model.-->

<span data-ttu-id="32caf-254">*Clasificación* y *regresión* son dos tipos de algoritmos de aprendizaje automático supervisado.</span><span class="sxs-lookup"><span data-stu-id="32caf-254">*Classification* and *regression* are two types of supervised machine learning algorithms.</span></span> <span data-ttu-id="32caf-255">La clasificación permite predecir una respuesta a partir de un conjunto definido de categorías, como el color (rojo, azul o verde).</span><span class="sxs-lookup"><span data-stu-id="32caf-255">Classification predicts an answer from a defined set of categories, such as a color (red, blue, or green).</span></span> <span data-ttu-id="32caf-256">La regresión se usa para predecir un número.</span><span class="sxs-lookup"><span data-stu-id="32caf-256">Regression is used to predict a number.</span></span>

<span data-ttu-id="32caf-257">Como queremos predecir un precio, que es un número, usaremos un modelo de regresión.</span><span class="sxs-lookup"><span data-stu-id="32caf-257">Because we want to predict price, which is a number, we'll use a regression algorithm.</span></span> <span data-ttu-id="32caf-258">En este ejemplo, vamos a usar un sencillo modelo de *regresión lineal*.</span><span class="sxs-lookup"><span data-stu-id="32caf-258">For this example, we'll use a simple *linear regression* model.</span></span>

> [!TIP]
> <span data-ttu-id="32caf-259">Para más información sobre los diferentes tipos de algoritmos de aprendizaje automático y cuándo usarlos, puede ver el primer vídeo de la serie Ciencia de datos para principiantes, [Las cinco preguntas a las que responde la ciencia de datos](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span><span class="sxs-lookup"><span data-stu-id="32caf-259">If you want to learn more about different types of machine learning algorithms and when to use them, you might view the first video in the Data Science for Beginners series, [The five questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span></span> <span data-ttu-id="32caf-260">También puede examinar la infografía [Conceptos básicos de aprendizaje automático con ejemplos de algoritmos](machine-learning-basics-infographic-with-algorithm-examples.md) o consultar la [Hoja de referencia rápida de algoritmos de aprendizaje automático](machine-learning-algorithm-cheat-sheet.md).</span><span class="sxs-lookup"><span data-stu-id="32caf-260">You might also look at the infographic [Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md), or check out the [Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md).</span></span>

<span data-ttu-id="32caf-261">Para entrenar el modelo le proporcionamos un conjunto de datos que incluye el precio.</span><span class="sxs-lookup"><span data-stu-id="32caf-261">We train the model by giving it a set of data that includes the price.</span></span> <span data-ttu-id="32caf-262">El modelo analiza los datos y busca correlaciones entre las características de un automóvil y su precio.</span><span class="sxs-lookup"><span data-stu-id="32caf-262">The model scans the data and look for correlations between an automobile's features and its price.</span></span> <span data-ttu-id="32caf-263">A continuación, probaremos el modelo; le daremos un conjunto de características de automóviles con los que estamos familiarizados y veremos si el modelo se acerca en la predicción del precio conocido.</span><span class="sxs-lookup"><span data-stu-id="32caf-263">Then we'll test the model - we'll give it a set of features for automobiles we're familiar with and see how close the model comes to predicting the known price.</span></span>

<span data-ttu-id="32caf-264">Usaremos nuestros datos para entrenar el modelo y probarlo, para lo cual los dividiremos en conjuntos de datos distintos, de entrenamiento y de prueba.</span><span class="sxs-lookup"><span data-stu-id="32caf-264">We'll use our data for both training the model and testing it by splitting the data into separate training and testing datasets.</span></span>

1. <span data-ttu-id="32caf-265">Seleccione y arrastre el módulo [Split Data][split] al lienzo del experimento y conéctelo al último módulo [Select Columns in Dataset] (Seleccionar columnas en el conjunto de datos) [select-columns].</span><span class="sxs-lookup"><span data-stu-id="32caf-265">Select and drag the [Split Data][split] module to the experiment canvas and connect it to the last [Select Columns in Dataset][select-columns] module.</span></span>

2. <span data-ttu-id="32caf-266">Haga clic en el módulo [Split Data][split] (Dividir datos) para seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="32caf-266">Click the [Split Data][split] module to select it.</span></span> <span data-ttu-id="32caf-267">Busque **Fraction of rows in the first output dataset** (Fracción de filas del primer conjunto de datos de salida) (en el panel **Propiedades** a la derecha de lienzo) y establézcalo en 0,75.</span><span class="sxs-lookup"><span data-stu-id="32caf-267">Find the **Fraction of rows in the first output dataset** (in the **Properties** pane to the right of the canvas) and set it to 0.75.</span></span> <span data-ttu-id="32caf-268">De esta manera, usaremos el 75 por ciento de los datos para entrenar el modelo y mantendremos el 25 por ciento para prueba (más adelante, puede experimentar con el uso de diferentes porcentajes).</span><span class="sxs-lookup"><span data-stu-id="32caf-268">This way, we'll use 75 percent of the data to train the model, and hold back 25 percent for testing (later, you can experiment with using different percentages).</span></span>

    <span data-ttu-id="32caf-269">![Establecer la fracción de división del módulo "Dividir datos" en 0,75][set-split-data-percentage]
    </span><span class="sxs-lookup"><span data-stu-id="32caf-269">![Set the split fraction of the "Split Data" module to 0.75][set-split-data-percentage]
    </span></span><br/>
 <span data-ttu-id="32caf-270">***Establece la fracción de división del módulo "Dividir datos" en 0,75***</span><span class="sxs-lookup"><span data-stu-id="32caf-270">***Set the split fraction of the "Split Data" module to 0.75***</span></span>

    > [!TIP]
    > <span data-ttu-id="32caf-271">Al cambiar el parámetro **Valor de inicialización aleatorio** , puede producir muestras aleatorias diferentes para entrenamiento y prueba.</span><span class="sxs-lookup"><span data-stu-id="32caf-271">By changing the **Random seed** parameter, you can produce different random samples for training and testing.</span></span> <span data-ttu-id="32caf-272">Este parámetro controla la inicialización del generador de números pseudoaleatorios.</span><span class="sxs-lookup"><span data-stu-id="32caf-272">This parameter controls the seeding of the pseudo-random number generator.</span></span>

2. <span data-ttu-id="32caf-273">Ejecute el experimento.</span><span class="sxs-lookup"><span data-stu-id="32caf-273">Run the experiment.</span></span> <span data-ttu-id="32caf-274">Cuando se ejecuta el experimento, los módulos [Select Columns in Dataset] (Seleccionar columnas en el conjunto de datos) [select-columns] y [Split Data] (Dividir datos) [split] pasan las definiciones de columna a los módulos que se agregarán a continuación.</span><span class="sxs-lookup"><span data-stu-id="32caf-274">When the experiment is run, the [Select Columns in Dataset][select-columns] and [Split Data][split] modules pass column definitions to the modules we'll be adding next.</span></span>  

3. <span data-ttu-id="32caf-275">Para seleccionar el algoritmo de aprendizaje, expanda la categoría **Aprendizaje automático** en la paleta de módulos situada a la izquierda del lienzo y luego expanda **Inicializar modelo**.</span><span class="sxs-lookup"><span data-stu-id="32caf-275">To select the learning algorithm, expand the **Machine Learning** category in the module palette to the left of the canvas, and then expand **Initialize Model**.</span></span> <span data-ttu-id="32caf-276">Se muestran varias categorías de módulos que se pueden usar para inicializar algoritmos de Aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="32caf-276">This displays several categories of modules that can be used to initialize machine learning algorithms.</span></span> <span data-ttu-id="32caf-277">Para este experimento, seleccione el módulo [Regresión lineal][linear-regression] en la categoría **Regresión** y arrástrelo al lienzo del experimento.</span><span class="sxs-lookup"><span data-stu-id="32caf-277">For this experiment, select the [Linear Regression][linear-regression] module under the **Regression** category, and drag it to the experiment canvas.</span></span>
<span data-ttu-id="32caf-278">(Otra forma de encontrar el módulo es escribir "regresión lineal" en el cuadro Buscar de la paleta.)</span><span class="sxs-lookup"><span data-stu-id="32caf-278">(You can also find the module by typing "linear regression" in the palette Search box.)</span></span>

4. <span data-ttu-id="32caf-279">Busque y arrastre el módulo [Train Model][train-model] (Entrenar modelo) al lienzo del experimento.</span><span class="sxs-lookup"><span data-stu-id="32caf-279">Find and drag the [Train Model][train-model] module to the experiment canvas.</span></span> <span data-ttu-id="32caf-280">Conecte la salida del módulo [Linear Regression][linear-regression] (Regresión lineal) a la entrada izquierda del módulo [Train Model][train-model] (Entrenar modelo), y conecte la salida de datos de entrenamiento (puerto izquierdo) del módulo [Split Data][split] (Dividir datos) a la entrada derecha del módulo [Train Model][train-model].</span><span class="sxs-lookup"><span data-stu-id="32caf-280">Connect the output of the [Linear Regression][linear-regression] module to the left input of the [Train Model][train-model] module, and connect the training data output (left port) of the [Split Data][split] module to the right input of the [Train Model][train-model] module.</span></span>

    <span data-ttu-id="32caf-281">![Conectar el módulo "Entrenar modelo" a los módulos "Regresión lineal" y "Dividir datos"][connect-train-model]
    </span><span class="sxs-lookup"><span data-stu-id="32caf-281">![Connect the "Train Model" module to both the "Linear Regression" and "Split Data" modules][connect-train-model]
    </span></span><br/>
 <span data-ttu-id="32caf-282">***Conecte el módulo "Entrenar modelo" a los módulos de los "Regresión lineal" y "División datos"***</span><span class="sxs-lookup"><span data-stu-id="32caf-282">***Connect the "Train Model" module to both the "Linear Regression" and "Split Data" modules***</span></span>

5. <span data-ttu-id="32caf-283">Haga clic en el módulo [Train Model][train-model] (Entrenar modelo), haga clic en **Launch column selector** (Iniciar el selector de columnas) en el panel **Propiedades** y, luego, seleccione la columna **price** (precio).</span><span class="sxs-lookup"><span data-stu-id="32caf-283">Click the [Train Model][train-model] module, click **Launch column selector** in the **Properties** pane, and then select the **price** column.</span></span> <span data-ttu-id="32caf-284">Este es el valor que nuestro modelo va a predecir.</span><span class="sxs-lookup"><span data-stu-id="32caf-284">This is the value that our model is going to predict.</span></span>

    <span data-ttu-id="32caf-285">Para seleccionar la columna **precio** en el selector de columnas, muévala de la lista **Columnas disponibles** a la lista **Columnas seleccionadas**.</span><span class="sxs-lookup"><span data-stu-id="32caf-285">You select the **price** column in the column selector by moving it from the **Available columns** list to the **Selected columns** list.</span></span>

    <span data-ttu-id="32caf-286">![Seleccionar la columna precio del módulo "Entrenar modelo"][select-price-column]
    </span><span class="sxs-lookup"><span data-stu-id="32caf-286">![Select the price column for the "Train Model" module][select-price-column]
    </span></span><br/>
 <span data-ttu-id="32caf-287">***Seleccione la columna de precio para el módulo "Entrenar modelo"***</span><span class="sxs-lookup"><span data-stu-id="32caf-287">***Select the price column for the "Train Model" module***</span></span>

6. <span data-ttu-id="32caf-288">Ejecute el experimento.</span><span class="sxs-lookup"><span data-stu-id="32caf-288">Run the experiment.</span></span>

<span data-ttu-id="32caf-289">Ahora tenemos un modelo de regresión entrenado que puede usarse para puntuar nuevos datos de automóviles para realizar predicciones de precios.</span><span class="sxs-lookup"><span data-stu-id="32caf-289">We now have a trained regression model that can be used to score new automobile data to make price predictions.</span></span>

<span data-ttu-id="32caf-290">![Tras la ejecución, el experimento debe tener este aspecto][second-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="32caf-290">![After running, the experiment should now look something like this][second-experiment-run]
</span></span><br/><span data-ttu-id="32caf-291">
***Tras la ejecución, el experimento debe tener este aspecto***</span><span class="sxs-lookup"><span data-stu-id="32caf-291">
***After running, the experiment should now look something like this***</span></span>

## <a name="step-5-predict-new-automobile-prices"></a><span data-ttu-id="32caf-292">Paso 5: Predecir los precios de los automóviles nuevos</span><span class="sxs-lookup"><span data-stu-id="32caf-292">Step 5: Predict new automobile prices</span></span>

<span data-ttu-id="32caf-293">Ahora que hemos entrenado el modelo usando el 75 % de nuestros datos, podemos usarlo para puntuar el otro 25 % de los datos y ver cómo funciona el modelo.</span><span class="sxs-lookup"><span data-stu-id="32caf-293">Now that we've trained the model using 75 percent of our data, we can use it to score the other 25 percent of the data to see how well our model functions.</span></span>

1. <span data-ttu-id="32caf-294">Busque y arrastre el módulo [Score Model] (Puntuar modelo) [score-model] al lienzo del experimento.</span><span class="sxs-lookup"><span data-stu-id="32caf-294">Find and drag the [Score Model][score-model] module to the experiment canvas.</span></span> <span data-ttu-id="32caf-295">Conecte la salida del módulo [Train Model][train-model] (Entrenar modelo) al puerto de entrada izquierdo de [Score Model] (Puntuar modelo) [score-model].</span><span class="sxs-lookup"><span data-stu-id="32caf-295">Connect the output of the [Train Model][train-model] module to the left input port of [Score Model][score-model].</span></span> <span data-ttu-id="32caf-296">Conecte la salida de datos de prueba (puerto derecho) del módulo [Split Data][split] (Dividir datos) al puerto de entrada derecho de [Score Model][score-model] (Puntuar modelo).</span><span class="sxs-lookup"><span data-stu-id="32caf-296">Connect the test data output (right port) of the [Split Data][split] module to the right input port of [Score Model][score-model].</span></span>

    <span data-ttu-id="32caf-297">![Conectar el módulo "Puntuar modelo" a los módulos "Entrenar modelo" y "Dividir datos"][connect-score-model]
    </span><span class="sxs-lookup"><span data-stu-id="32caf-297">![Connect the "Score Model" module to both the "Train Model" and "Split Data" modules][connect-score-model]
    </span></span><br/>
 <span data-ttu-id="32caf-298">***Conecte el módulo "Modelo de puntuación" a los módulos de los "Entrenar modelo" y "División datos"***</span><span class="sxs-lookup"><span data-stu-id="32caf-298">***Connect the "Score Model" module to both the "Train Model" and "Split Data" modules***</span></span>

2. <span data-ttu-id="32caf-299">Ejecute el experimento y vea la salida desde el módulo [Score Model][score-model] (Puntuar modelo); haga clic en el puerto de salida de [Score Model][score-model] (Puntuar modelo) y seleccione **Visualizar**.</span><span class="sxs-lookup"><span data-stu-id="32caf-299">Run the experiment and view the output from the [Score Model][score-model] module (click the output port of [Score Model][score-model] and select **Visualize**).</span></span> <span data-ttu-id="32caf-300">La salida muestra los valores previstos para el precio y los valores conocidos de los datos de prueba.</span><span class="sxs-lookup"><span data-stu-id="32caf-300">The output shows the predicted values for price and the known values from the test data.</span></span>  

    <span data-ttu-id="32caf-301">![Salida del módulo "Puntuar modelo"][score-model-output]
    </span><span class="sxs-lookup"><span data-stu-id="32caf-301">![Output of the "Score Model" module][score-model-output]
    </span></span><br/>
 <span data-ttu-id="32caf-302">***Salida del módulo "Modelo de puntuación"***</span><span class="sxs-lookup"><span data-stu-id="32caf-302">***Output of the "Score Model" module***</span></span>

3. <span data-ttu-id="32caf-303">Por último, probamos la calidad de los resultados.</span><span class="sxs-lookup"><span data-stu-id="32caf-303">Finally, we test the quality of the results.</span></span> <span data-ttu-id="32caf-304">Seleccione y arrastre el módulo [Evaluate Model][evaluate-model] (Evaluar modelo) al lienzo del experimento y conecte la salida del módulo [Score Model][score-model] (Puntuar modelo) a la entrada izquierda del módulo [Evaluate Model][evaluate-model] (Evaluar modelo).</span><span class="sxs-lookup"><span data-stu-id="32caf-304">Select and drag the [Evaluate Model][evaluate-model] module to the experiment canvas, and connect the output of the [Score Model][score-model] module to the left input of [Evaluate Model][evaluate-model].</span></span>

    > [!TIP]
    > <span data-ttu-id="32caf-305">Hay dos puertos de entrada en el módulo [Evaluate Model][evaluate-model] (Evaluar modelo) porque puede usarse para comparar dos modelos en paralelo.</span><span class="sxs-lookup"><span data-stu-id="32caf-305">There are two input ports on the [Evaluate Model][evaluate-model] module because it can be used to compare two models side by side.</span></span> <span data-ttu-id="32caf-306">Más adelante, puede agregar otro algoritmo al experimento y usar [Evaluate Model][evaluate-model] (Evaluar modelo) para ver cuál ofrece mejores resultados.</span><span class="sxs-lookup"><span data-stu-id="32caf-306">Later, you can add another algorithm to the experiment and use [Evaluate Model][evaluate-model] to see which one gives better results.</span></span>

4. <span data-ttu-id="32caf-307">Ejecute el experimento.</span><span class="sxs-lookup"><span data-stu-id="32caf-307">Run the experiment.</span></span>

<span data-ttu-id="32caf-308">Para ver la salida del módulo [Evaluate Model][evaluate-model] (Evaluar modelo), haga clic en el puerto de salida y seleccione **Visualize** (Visualizar).</span><span class="sxs-lookup"><span data-stu-id="32caf-308">To view the output from the [Evaluate Model][evaluate-model] module, click the output port, and then select **Visualize**.</span></span>

<span data-ttu-id="32caf-309">![Resultados de evaluación del experimento][evaluation-results]
</span><span class="sxs-lookup"><span data-stu-id="32caf-309">![Evaluation results for the experiment][evaluation-results]
</span></span><br/><span data-ttu-id="32caf-310">
***Resultados de evaluación del experimento***</span><span class="sxs-lookup"><span data-stu-id="32caf-310">
***Evaluation results for the experiment***</span></span>

<span data-ttu-id="32caf-311">Se muestran las siguientes estadísticas para nuestro modelo:</span><span class="sxs-lookup"><span data-stu-id="32caf-311">The following statistics are shown for our model:</span></span>

- <span data-ttu-id="32caf-312">**Desviación media** (MAE): la media de errores absolutos (un *error* es la diferencia entre el valor de predicción y el valor real).</span><span class="sxs-lookup"><span data-stu-id="32caf-312">**Mean Absolute Error** (MAE): The average of absolute errors (an *error* is the difference between the predicted value and the actual value).</span></span>
- <span data-ttu-id="32caf-313">**Raíz cuadrada de errores** (RMSE): la raíz cuadrada de la media de errores al cuadrado de las predicciones realizadas sobre el conjunto de datos de prueba.</span><span class="sxs-lookup"><span data-stu-id="32caf-313">**Root Mean Squared Error** (RMSE): The square root of the average of squared errors of predictions made on the test dataset.</span></span>
- <span data-ttu-id="32caf-314">**Error absoluto relativo**: la media de errores absolutos en relación con la diferencia absoluta entre los valores reales y la media de todos los valores reales.</span><span class="sxs-lookup"><span data-stu-id="32caf-314">**Relative Absolute Error**: The average of absolute errors relative to the absolute difference between actual values and the average of all actual values.</span></span>
- <span data-ttu-id="32caf-315">**Error al cuadrado relativo**: la media de errores al cuadrado en relación con la diferencia al cuadrado entre los valores reales y la media de todos los valores reales.</span><span class="sxs-lookup"><span data-stu-id="32caf-315">**Relative Squared Error**: The average of squared errors relative to the squared difference between the actual values and the average of all actual values.</span></span>
- <span data-ttu-id="32caf-316">**Coeficiente de determinación**: conocido también como **valor R cuadrado**, es una métrica estadística que indica cómo de bien se ajusta un modelo a los datos.</span><span class="sxs-lookup"><span data-stu-id="32caf-316">**Coefficient of Determination**: Also known as the **R squared value**, this is a statistical metric indicating how well a model fits the data.</span></span>

<span data-ttu-id="32caf-317">Para cada una de las estadísticas de errores, cuanto menor sea el valor, mejor.</span><span class="sxs-lookup"><span data-stu-id="32caf-317">For each of the error statistics, smaller is better.</span></span> <span data-ttu-id="32caf-318">Un valor inferior indica que las predicciones se adaptan más estrechamente a los valores reales.</span><span class="sxs-lookup"><span data-stu-id="32caf-318">A smaller value indicates that the predictions more closely match the actual values.</span></span> <span data-ttu-id="32caf-319">En **Coeficiente de determinación**, cuanto más cerca está el valor de uno (1,0), mejores son las predicciones.</span><span class="sxs-lookup"><span data-stu-id="32caf-319">For **Coefficient of Determination**, the closer its value is to one (1.0), the better the predictions.</span></span>

## <a name="final-experiment"></a><span data-ttu-id="32caf-320">Experimento final</span><span class="sxs-lookup"><span data-stu-id="32caf-320">Final experiment</span></span>

<span data-ttu-id="32caf-321">El experimento final debe tener un aspecto similar a este:</span><span class="sxs-lookup"><span data-stu-id="32caf-321">The final experiment should look something like this:</span></span>

<span data-ttu-id="32caf-322">![El experimento final][complete-linear-regression-experiment]
</span><span class="sxs-lookup"><span data-stu-id="32caf-322">![The final experiment][complete-linear-regression-experiment]
</span></span><br/><span data-ttu-id="32caf-323">
***El experimento final***</span><span class="sxs-lookup"><span data-stu-id="32caf-323">
***The final experiment***</span></span>

## <a name="next-steps"></a><span data-ttu-id="32caf-324">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="32caf-324">Next steps</span></span>

<span data-ttu-id="32caf-325">Ahora que ha completado el primer tutorial de aprendizaje automático y tiene su experimento configurado, puede continuar mejorando el modelo y luego implementarlo como un servicio web predictivo.</span><span class="sxs-lookup"><span data-stu-id="32caf-325">Now that you've completed the first machine learning tutorial and have your experiment set up, you can continue to improve the model and then deploy it as a predictive web service.</span></span>

- <span data-ttu-id="32caf-326">**Iterar para intentar mejorar el modelo**; por ejemplo, puede cambiar las características que usará en su predicción.</span><span class="sxs-lookup"><span data-stu-id="32caf-326">**Iterate to try to improve the model** - For example, you can change the features you use in your prediction.</span></span> <span data-ttu-id="32caf-327">O bien, puede modificar las propiedades del algoritmo [Linear Regression][linear-regression] (Regresión lineal) o probar un algoritmo completamente diferente.</span><span class="sxs-lookup"><span data-stu-id="32caf-327">Or you can modify the properties of the [Linear Regression][linear-regression] algorithm or try a different algorithm altogether.</span></span> <span data-ttu-id="32caf-328">Incluso puede agregar varios algoritmos de aprendizaje automático a la vez al experimento y comparar dos de ellos mediante el módulo [Evaluate Model][evaluate-model] (Evaluar modelo).</span><span class="sxs-lookup"><span data-stu-id="32caf-328">You can even add multiple machine learning algorithms to your experiment at one time and compare two of them by using the [Evaluate Model][evaluate-model] module.</span></span>
<span data-ttu-id="32caf-329">Para ver un ejemplo de cómo comparar varios modelos en un único experimento, consulte [Compare Regressors](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) (Comparar regresores) en la [galería de Cortana Intelligence](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="32caf-329">For an example of how to compare multiple models in a single experiment, see [Compare Regressors](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span>

    > [!TIP]
    > <span data-ttu-id="32caf-330">Para copiar cualquier iteración del experimento, use el botón **GUARDAR COMO** situado en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="32caf-330">To copy any iteration of your experiment, use the **SAVE AS** button at the bottom of the page.</span></span> <span data-ttu-id="32caf-331">Puede ver todas las iteraciones del experimento haciendo clic en **VER HISTORIAL DE EJECUCIÓN** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="32caf-331">You can see all the iterations of your experiment by clicking **VIEW RUN HISTORY** at the bottom of the page.</span></span> <span data-ttu-id="32caf-332">Para más información, consulte [Administración de iteraciones de experimentos en Azure Machine Learning Studio][runhistory].</span><span class="sxs-lookup"><span data-stu-id="32caf-332">For more details, see [Manage experiment iterations in Azure Machine Learning Studio][runhistory].</span></span>

[runhistory]: machine-learning-manage-experiment-iterations.md

- <span data-ttu-id="32caf-333">**Implementar el modelo como un servicio web predictivo**: si está satisfecho con su modelo, puede implementarlo como un servicio web a fin de usarlo para predecir precios de automóviles usando nuevos datos.</span><span class="sxs-lookup"><span data-stu-id="32caf-333">**Deploy the model as a predictive web service** - When you're satisfied with your model, you can deploy it as a web service to be used to predict automobile prices by using new data.</span></span> <span data-ttu-id="32caf-334">Para más información, consulte [Implementar un servicio web Azure Machine Learning][publish].</span><span class="sxs-lookup"><span data-stu-id="32caf-334">For more details, see [Deploy an Azure Machine Learning web service][publish].</span></span>

[publish]: machine-learning-publish-a-machine-learning-web-service.md

<span data-ttu-id="32caf-335">¿Quiere saber más?</span><span class="sxs-lookup"><span data-stu-id="32caf-335">Want to learn more?</span></span> <span data-ttu-id="32caf-336">Para ver un tutorial más amplio y detallado del proceso de crear, entrenar, puntuar e implementar un modelo, consulte [Desarrollar una solución predictiva mediante Azure Machine Learning][walkthrough].</span><span class="sxs-lookup"><span data-stu-id="32caf-336">For a more extensive and detailed walkthrough of the process of creating, training, scoring, and deploying a model, see [Develop a predictive solution by using Azure Machine Learning][walkthrough].</span></span>

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

<!-- temporarily switching GIFs to PNGs to remove animation --> 
[type-automobile]:./media/machine-learning-create-experiment/type-automobile.png
[type-select-columns]:./media/machine-learning-create-experiment/type-select-columns.png
[launch-column-selector]:./media/machine-learning-create-experiment/launch-column-selector.png
[add-comment]:./media/machine-learning-create-experiment/add-comment.png
[connect-clean-to-select]:./media/machine-learning-create-experiment/connect-clean-to-select.png

[set-split-data-percentage]:./media/machine-learning-create-experiment/set-split-data-percentage.png

<!-- temporarily switching GIFs to PNGs to remove animation --> 
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
