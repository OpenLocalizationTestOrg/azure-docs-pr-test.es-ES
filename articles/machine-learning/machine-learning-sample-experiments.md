---
title: "Copia de experimentos de ejemplo de aprendizaje automático (Azure) | Microsoft Docs"
description: "Aprenda a usar experimentos de ejemplo de aprendizaje automático para crear nuevos experimentos con la Galería de Cortana Intelligence y Microsoft Azure Machine Learning."
keywords: "ejemplos de aprendizaje automático, ejemplo de experimento, ejemplo de aprendizaje automático"
services: machine-learning
documentationcenter: 
author: cjgronlund
manager: jhubbard
editor: cgronlun
ms.assetid: 81e6c1d8-682c-4db3-bfd5-d7bfb1150ff3
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/28/2017
ms.author: cgronlun
ms.openlocfilehash: 55f9bd2ed0d555a14d31bf3d262707d65bd70244
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="copy-example-experiments-to-create-new-machine-learning-experiments"></a><span data-ttu-id="f7d20-104">Copia de experimentos de ejemplo para crear nuevos experimentos de aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="f7d20-104">Copy example experiments to create new machine learning experiments</span></span>
<span data-ttu-id="f7d20-105">Aprenda cómo comenzar con experimentos de ejemplo desde la [Galería de Cortana Intelligence](https://gallery.cortanaintelligence.com/) en lugar de crear experimentos de aprendizaje automático desde cero.</span><span class="sxs-lookup"><span data-stu-id="f7d20-105">Learn how to start with example experiments from [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) instead of creating machine learning experiments from scratch.</span></span> <span data-ttu-id="f7d20-106">Puede usar los ejemplos para crear su propia solución de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="f7d20-106">You can use the examples to build your own machine learning solution.</span></span>

<span data-ttu-id="f7d20-107">En la galería hay experimentos de ejemplo creados por el equipo Microsoft Azure Machine Learning, así como ejemplos compartidos por la comunidad de Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f7d20-107">The gallery has example experiments by the Microsoft Azure Machine Learning team as well as examples shared by the Machine Learning community.</span></span> <span data-ttu-id="f7d20-108">También puede plantear preguntas o publicar comentarios acerca de experimentos.</span><span class="sxs-lookup"><span data-stu-id="f7d20-108">You also can ask questions or post comments about experiments.</span></span>

<span data-ttu-id="f7d20-109">Para ver cómo usar la galería, vea el vídeo de 3 minutos [Copia del trabajo de otras personas para realizar ciencia de datos](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) de la serie [Ciencia de datos para principiantes](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span><span class="sxs-lookup"><span data-stu-id="f7d20-109">To see how to use the gallery, watch the 3-minute video [Copy other people's work to do data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) from the series [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="find-an-experiment-to-copy-in-cortana-intelligence-gallery"></a><span data-ttu-id="f7d20-110">Busque un experimento para copiar en la Galería de Cortana Intelligence</span><span class="sxs-lookup"><span data-stu-id="f7d20-110">Find an experiment to copy in Cortana Intelligence Gallery</span></span>
<span data-ttu-id="f7d20-111">Para ver qué experimentos hay disponibles, vaya a la [galería](https://gallery.cortanaintelligence.com/) y haga clic en **Experiments** (Experimentos) en la parte superior de la página.</span><span class="sxs-lookup"><span data-stu-id="f7d20-111">To see what experiments are available, go to the [Gallery](https://gallery.cortanaintelligence.com/) and click **Experiments** at the top of the page.</span></span>

### <a name="find-the-newest-or-most-popular-experiments"></a><span data-ttu-id="f7d20-112">Busque los experimentos más recientes o más populares</span><span class="sxs-lookup"><span data-stu-id="f7d20-112">Find the newest or most popular experiments</span></span>
<span data-ttu-id="f7d20-113">En esta página puede ver experimentos **agregados recientemente** (Recently added), desplazarse hacia abajo para averiguar **qué es popular** (What's popular) o consultar los **experimentos populares de Microsoft** (Popular Microsoft experiments) más recientes.</span><span class="sxs-lookup"><span data-stu-id="f7d20-113">On this page, you can see **Recently added** experiments, or scroll down to look at **What's popular** or the latest **Popular Microsoft experiments**.</span></span>

### <a name="look-for-an-experiment-that-meets-specific-requirements"></a><span data-ttu-id="f7d20-114">Busque un experimento que cumpla los requisitos específicos</span><span class="sxs-lookup"><span data-stu-id="f7d20-114">Look for an experiment that meets specific requirements</span></span>
<span data-ttu-id="f7d20-115">Para examinar todos los experimentos:</span><span class="sxs-lookup"><span data-stu-id="f7d20-115">To browse all experiments:</span></span>

1. <span data-ttu-id="f7d20-116">Haga clic en **Browse all** (Examinar todo) en la parte superior de la página.</span><span class="sxs-lookup"><span data-stu-id="f7d20-116">Click **Browse all** at the top of the page.</span></span>
2. <span data-ttu-id="f7d20-117">En el lado izquierdo, en **Refine by** (Refinar por) de la sección **Categories** (Categorías), seleccione **Experiment** (Experimento) para ver los experimentos de la galería.</span><span class="sxs-lookup"><span data-stu-id="f7d20-117">On the left-hand side, under **Refine by** in the **Categories** section, select **Experiment** to see all the experiments in the Gallery.</span></span>
3. <span data-ttu-id="f7d20-118">Puede encontrar los experimentos que cumplan con sus requisitos de las siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="f7d20-118">You can find experiments that meet your requirements a couple different ways:</span></span>
   * <span data-ttu-id="f7d20-119">**Seleccione los filtros de la izquierda.**</span><span class="sxs-lookup"><span data-stu-id="f7d20-119">**Select filters on the left.**</span></span> <span data-ttu-id="f7d20-120">Por ejemplo, para examinar experimentos que usan un algoritmo de detección de anomalías basada en PCA, haciendo seleccionado **Experiment** (Experimento) en **Categories** (Categorías), haga clic en **Show all** (Mostrar todo).</span><span class="sxs-lookup"><span data-stu-id="f7d20-120">For example, to browse experiments that use a PCA-based anomaly detection algorithm: With **Experiment** selected under **Categories**, click **Show all**.</span></span> <span data-ttu-id="f7d20-121">A continuación, en **Algorithms Used** (Algoritmos usados), elija **PCA-Based Anomaly Detection** (Detección de anomalías basada en PCA).</span><span class="sxs-lookup"><span data-stu-id="f7d20-121">Then, under **Algorithms Used**, choose **PCA-Based Anomaly Detection**.</span></span> <br></br><span data-ttu-id="f7d20-122">
     ![Filtros de selección](./media/machine-learning-sample-experiments/refine-the-view.png)</span><span class="sxs-lookup"><span data-stu-id="f7d20-122">
![Select filters](./media/machine-learning-sample-experiments/refine-the-view.png)</span></span>
   * <span data-ttu-id="f7d20-123">**Utilice el cuadro de búsqueda.**</span><span class="sxs-lookup"><span data-stu-id="f7d20-123">**Use the search box.**</span></span> <span data-ttu-id="f7d20-124">Por ejemplo, para buscar experimentos aportados por Microsoft relacionados con el reconocimiento de dígitos que usen un algoritmo de máquina de vectores de soporte de dos clases, escriba "digit recognition" (reconocimiento de dígitos) en el cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="f7d20-124">For example, to find experiments contributed by Microsoft related to digit recognition that use a two-class support vector machine algorithm, enter "digit recognition" in the search box.</span></span> <span data-ttu-id="f7d20-125">A continuación, seleccione los filtros **Experiment** (Experimento), **Microsoft content only** (Solo contenido de Microsoft) y **Two-Class Support Vector Machine** (Máquina de vectores de soporte de dos clases):</span><span class="sxs-lookup"><span data-stu-id="f7d20-125">Then, select the filters **Experiment**, **Microsoft content only**, and **Two-Class Support Vector Machine**:</span></span><br></br><span data-ttu-id="f7d20-126">
     ![Utilice el cuadro de búsqueda](./media/machine-learning-sample-experiments/search-for-experiments.png)</span><span class="sxs-lookup"><span data-stu-id="f7d20-126">
![Use the search box](./media/machine-learning-sample-experiments/search-for-experiments.png)</span></span>
4. <span data-ttu-id="f7d20-127">Haga clic en un experimento para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="f7d20-127">Click an experiment to learn more about it.</span></span>
5. <span data-ttu-id="f7d20-128">Para ejecutar o modificar el experimento, haga clic en **Open in Studio** (Abrir en Estudio) en la página del experimento.</span><span class="sxs-lookup"><span data-stu-id="f7d20-128">To run and/or modify the experiment, click **Open in Studio** on the experiment's page.</span></span> <br></br>

    ![Experimento de ejemplo](./media/machine-learning-sample-experiments/example-experiment.png)

    > [!NOTE]
    > <span data-ttu-id="f7d20-130">Cuando abra un experimento en Machine Learning Studio por primera vez, puede probarlo de forma gratuita o comprar una suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="f7d20-130">When you open an experiment in Machine Learning Studio for the first time, you can try it for free or buy an Azure subscription.</span></span> [<span data-ttu-id="f7d20-131">Vea información sobre la diferencia entre la prueba gratuita de Machine Learning Studio y el servicio de pago</span><span class="sxs-lookup"><span data-stu-id="f7d20-131">Learn about the Machine Learning Studio free trial vs. paid service</span></span>](https://azure.microsoft.com/pricing/details/machine-learning/)
    >
    >

## <a name="create-a-new-experiment-using-an-example-as-a-template"></a><span data-ttu-id="f7d20-132">Creación de un nuevo experimento usando un ejemplo como plantilla</span><span class="sxs-lookup"><span data-stu-id="f7d20-132">Create a new experiment using an example as a template</span></span>
<span data-ttu-id="f7d20-133">También puede crear un nuevo experimento en Machine Learning Studio tomando un ejemplo de la galería como plantilla.</span><span class="sxs-lookup"><span data-stu-id="f7d20-133">You also can create a new experiment in Machine Learning Studio using a Gallery example as a template.</span></span>

1. <span data-ttu-id="f7d20-134">Inicie sesión con las credenciales de su cuenta de Microsoft en [Studio](https://studio.azureml.net) y haga clic en **Nuevo** para crear un experimento.</span><span class="sxs-lookup"><span data-stu-id="f7d20-134">Sign in with your Microsoft account credentials to the [Studio](https://studio.azureml.net), and then click **New** to create an experiment.</span></span>
2. <span data-ttu-id="f7d20-135">Examine el contenido de ejemplo y haga clic en uno.</span><span class="sxs-lookup"><span data-stu-id="f7d20-135">Browse through the example content and click one.</span></span>

<span data-ttu-id="f7d20-136">Se crea un nuevo experimento en su área de trabajo de Machine Learning Studio tomando como plantilla el experimento de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="f7d20-136">A new experiment is created in your Machine Learning Studio workspace using the example experiment as a template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7d20-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f7d20-137">Next steps</span></span>
* [<span data-ttu-id="f7d20-138">Importación de datos desde varios orígenes</span><span class="sxs-lookup"><span data-stu-id="f7d20-138">Import data from various sources</span></span>](machine-learning-data-science-import-data.md)
* [<span data-ttu-id="f7d20-139">Tutorial rápido para el lenguaje R en Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f7d20-139">Quickstart tutorial for the R language in Machine Learning</span></span>](machine-learning-r-quickstart.md)
* [<span data-ttu-id="f7d20-140">Implementación de un servicio web Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f7d20-140">Deploy a Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)
