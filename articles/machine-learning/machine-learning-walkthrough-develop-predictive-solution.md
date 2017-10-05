---
title: "Una solución predictiva para el riesgo de crédito con Machine Learning | Microsoft Docs"
description: "Un tutorial detallado que muestra cómo crear una solución de análisis predictiva para la evaluación del riesgo de crédito en Estudio de aprendizaje automático de Azure"
keywords: "riesgo de crédito, solución de análisis predictivo, evaluación de riesgos"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 43300854-a14e-4cd2-9bb1-c55c779e0e93
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: e1af999b2fde8ffa2a0ffd1b88230f0aaab32b37
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-develop-a-predictive-analytics-solution-for-credit-risk-assessment-in-azure-machine-learning"></a><span data-ttu-id="f612b-104">Tutorial: Desarrollo de una solución de análisis predictiva para la evaluación del riesgo de crédito en Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="f612b-104">Walkthrough: Develop a predictive analytics solution for credit risk assessment in Azure Machine Learning</span></span>

<span data-ttu-id="f612b-105">En este tutorial se explica con detalle el proceso de desarrollo de una solución de análisis predictivo en Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="f612b-105">In this walkthrough, we take an extended look at the process of developing a predictive analytics solution in Machine Learning Studio.</span></span> <span data-ttu-id="f612b-106">Desarrollaremos un modelo simple en Machine Learning Studio y lo implementaremos como un servicio web Azure Machine Learning, donde podrá realizar predicciones utilizando datos nuevos.</span><span class="sxs-lookup"><span data-stu-id="f612b-106">We develop a simple model in Machine Learning Studio, and then deploy it as an Azure Machine Learning web service where the model can make predictions using new data.</span></span> 

<span data-ttu-id="f612b-107">En este tutorial, se presupone que usó Machine Learning Studio con anterioridad al menos una vez y que tiene ciertos conocimientos sobre los conceptos de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="f612b-107">This walkthrough assumes that you've used Machine Learning Studio at least once before, and that you have some understanding of machine learning concepts.</span></span> <span data-ttu-id="f612b-108">Pero no se asume de que sea un experto.</span><span class="sxs-lookup"><span data-stu-id="f612b-108">But it doesn't assume you're an expert in either.</span></span>

<span data-ttu-id="f612b-109">Si nunca ha utilizado **Azure Machine Learning Studio**, sería conveniente que realizara primero el tutorial [Creación del primer experimento de ciencia de datos en Azure Machine Learning Studio](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="f612b-109">If you've never used **Azure Machine Learning Studio** before, you might want to start with the tutorial, [Create your first data science experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md).</span></span> <span data-ttu-id="f612b-110">Este tutorial lo guiará por primera vez por Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="f612b-110">That tutorial takes you through Machine Learning Studio for the first time.</span></span> <span data-ttu-id="f612b-111">Aquí se muestran los conceptos básicos de cómo arrastrar y colocar módulos en el experimento, conectarlos, ejecutar el experimento y examinar los resultados.</span><span class="sxs-lookup"><span data-stu-id="f612b-111">It shows you the basics of how to drag-and-drop modules onto your experiment, connect them together, run the experiment, and look at the results.</span></span> <span data-ttu-id="f612b-112">Otra herramienta que puede resultar útil para comenzar es un diagrama que muestra información general sobre las funcionalidades de Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="f612b-112">Another tool that may be helpful for getting started is a diagram that gives an overview of the capabilities of Machine Learning Studio.</span></span> <span data-ttu-id="f612b-113">Puede descargarlo e imprimirlo desde aquí: [Diagrama de información general de las funcionalidades de Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).</span><span class="sxs-lookup"><span data-stu-id="f612b-113">You can download and print it from here: [Overview diagram of Azure Machine Learning Studio capabilities](machine-learning-studio-overview-diagram.md).</span></span>
 
<span data-ttu-id="f612b-114">Si es su primera vez en el campo del aprendizaje automático en general, hay una serie de vídeos que puede resultarle útil.</span><span class="sxs-lookup"><span data-stu-id="f612b-114">If you're new to the field of machine learning in general, there's a video series that might be helpful to you.</span></span> <span data-ttu-id="f612b-115">La serie se llama [Ciencia de datos para principiantes](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) y le puede brindar una excelente introducción al aprendizaje automático con un lenguaje y conceptos de uso diario.</span><span class="sxs-lookup"><span data-stu-id="f612b-115">It's called [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) and it can give you a great introduction to machine learning using everyday language and concepts.</span></span>


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
 

## <a name="the-problem"></a><span data-ttu-id="f612b-116">El problema</span><span class="sxs-lookup"><span data-stu-id="f612b-116">The problem</span></span>

<span data-ttu-id="f612b-117">Suponga que necesita predecir el riesgo de crédito de un individuo en función de la información que se proporcionó en una solicitud de crédito.</span><span class="sxs-lookup"><span data-stu-id="f612b-117">Suppose you need to predict an individual's credit risk based on the information they gave on a credit application.</span></span>  

<span data-ttu-id="f612b-118">La evaluación de riesgos de un crédito es un problema complejo, pero podemos simplificarlo un poco para usarlo en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="f612b-118">Credit risk assessment is a complex problem, but we can simplify it a bit for this walkthrough.</span></span> <span data-ttu-id="f612b-119">La usaremos como ejemplo de cómo puede crear una solución de análisis predictivo con Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f612b-119">We'll use it as an example of how you can create a predictive analytics solution using Microsoft Azure Machine Learning.</span></span> <span data-ttu-id="f612b-120">Para hacerlo, usamos Azure Machine Learning Studio y un servicio web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f612b-120">To do this, we use Azure Machine Learning Studio and a Machine Learning web service.</span></span>  

## <a name="the-solution"></a><span data-ttu-id="f612b-121">La solución</span><span class="sxs-lookup"><span data-stu-id="f612b-121">The solution</span></span>

<span data-ttu-id="f612b-122">En este detallado tutorial, comenzamos con datos de riesgo de crédito y desarrollaremos y entrenaremos un modelo predictivo según esos datos.</span><span class="sxs-lookup"><span data-stu-id="f612b-122">In this detailed walkthrough, we start with publicly available credit risk data and develop and train a predictive model based on that data.</span></span> <span data-ttu-id="f612b-123">Luego, implementaremos el modelo como servicio web para que otros usuarios puedan usarlo para una evaluación de riesgos de crédito.</span><span class="sxs-lookup"><span data-stu-id="f612b-123">Then we deploy the model as a web service so it can be used by others for credit risk assessment.</span></span>

<span data-ttu-id="f612b-124">Para crear esta solución de evaluación de riesgos de crédito, seguiremos estos pasos:</span><span class="sxs-lookup"><span data-stu-id="f612b-124">To create this credit risk assessment solution, we follow these steps:</span></span>  

1. [<span data-ttu-id="f612b-125">Creación de un área de trabajo de Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="f612b-125">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="f612b-126">Carga de los datos existentes</span><span class="sxs-lookup"><span data-stu-id="f612b-126">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="f612b-127">Creación de un experimento</span><span class="sxs-lookup"><span data-stu-id="f612b-127">Create an experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="f612b-128">Entrenamiento y evaluación de los modelos</span><span class="sxs-lookup"><span data-stu-id="f612b-128">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="f612b-129">Implementación del servicio web</span><span class="sxs-lookup"><span data-stu-id="f612b-129">Deploy the web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="f612b-130">Acceso al servicio web</span><span class="sxs-lookup"><span data-stu-id="f612b-130">Access the web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

> [!TIP] 
> <span data-ttu-id="f612b-131">Puede encontrar una copia de trabajo del experimento que desarrollamos en este tutorial en la [galería de Cortana Intelligence](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="f612b-131">You can find a working copy of the experiment that we develop in this walkthrough in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="f612b-132">Vaya a **[Walkthrough - Credit risk prediction](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)** (Tutorial: predicción de riesgos de crédito) y haga clic en **Abrir en Studio** para descargar una copia del experimento al área de trabajo de Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="f612b-132">Go to **[Walkthrough - Credit risk prediction](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)** and click **Open in Studio** to download a copy of the experiment into your Machine Learning Studio workspace.</span></span>
> 
> <span data-ttu-id="f612b-133">Este tutorial se basa en una versión simplificada del experimento de ejemplo, [Clasificación binaria: predicción de riesgos de crédito](http://go.microsoft.com/fwlink/?LinkID=525270), también disponible en la [galería](http://gallery.cortanaintelligence.com/).</span><span class="sxs-lookup"><span data-stu-id="f612b-133">This walkthrough is based on a simplified version of the sample experiment, [Binary Classification: Credit risk prediction](http://go.microsoft.com/fwlink/?LinkID=525270), also available in the [Gallery](http://gallery.cortanaintelligence.com/).</span></span>
