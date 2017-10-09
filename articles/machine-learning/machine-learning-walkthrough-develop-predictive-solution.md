---
title: "solución de predicción aaaA de riesgo de crédito con aprendizaje automático | Documentos de Microsoft"
description: "Un tutorial detallado que muestra cómo toocreate una solución de análisis predictivos de crédito evaluación de riesgos en estudio de aprendizaje automático de Azure."
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
ms.openlocfilehash: 00ed39081e6952b8d03b37a8285d8dc3ddff2cb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-develop-a-predictive-analytics-solution-for-credit-risk-assessment-in-azure-machine-learning"></a><span data-ttu-id="67df9-104">Tutorial: Desarrollo de una solución de análisis predictiva para la evaluación del riesgo de crédito en Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="67df9-104">Walkthrough: Develop a predictive analytics solution for credit risk assessment in Azure Machine Learning</span></span>

<span data-ttu-id="67df9-105">En este tutorial, echamos un vistazo extendido en proceso de Hola de desarrollar una solución de análisis predictivos en estudio de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="67df9-105">In this walkthrough, we take an extended look at hello process of developing a predictive analytics solution in Machine Learning Studio.</span></span> <span data-ttu-id="67df9-106">Se desarrolla un modelo simple estudio de aprendizaje automático y, a continuación, implementarlo como un servicio web de aprendizaje automático de Azure donde modelo Hola puede realizar predicciones con los nuevos datos.</span><span class="sxs-lookup"><span data-stu-id="67df9-106">We develop a simple model in Machine Learning Studio, and then deploy it as an Azure Machine Learning web service where hello model can make predictions using new data.</span></span> 

<span data-ttu-id="67df9-107">En este tutorial, se presupone que usó Machine Learning Studio con anterioridad al menos una vez y que tiene ciertos conocimientos sobre los conceptos de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="67df9-107">This walkthrough assumes that you've used Machine Learning Studio at least once before, and that you have some understanding of machine learning concepts.</span></span> <span data-ttu-id="67df9-108">Pero no se asume de que sea un experto.</span><span class="sxs-lookup"><span data-stu-id="67df9-108">But it doesn't assume you're an expert in either.</span></span>

<span data-ttu-id="67df9-109">Si nunca ha utilizado **estudio de aprendizaje automático de Azure** antes, puede querer toostart con el tutorial de hello, [crear su primer ciencia de datos experimentar en estudio de aprendizaje automático de Azure](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="67df9-109">If you've never used **Azure Machine Learning Studio** before, you might want toostart with hello tutorial, [Create your first data science experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md).</span></span> <span data-ttu-id="67df9-110">Este tutorial le guiará por estudio de aprendizaje automático para hello primera vez.</span><span class="sxs-lookup"><span data-stu-id="67df9-110">That tutorial takes you through Machine Learning Studio for hello first time.</span></span> <span data-ttu-id="67df9-111">Muestra conceptos básicos de Hola de módulos de cómo toodrag y colocar en el experimento, conéctelos, ejecute el experimento de Hola y examine los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="67df9-111">It shows you hello basics of how toodrag-and-drop modules onto your experiment, connect them together, run hello experiment, and look at hello results.</span></span> <span data-ttu-id="67df9-112">Otra herramienta que puede resultar útil para obtener una introducción es un diagrama que ofrezca una visión general de las capacidades de Hola de estudio de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="67df9-112">Another tool that may be helpful for getting started is a diagram that gives an overview of hello capabilities of Machine Learning Studio.</span></span> <span data-ttu-id="67df9-113">Puede descargarlo e imprimirlo desde aquí: [Diagrama de información general de las funcionalidades de Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).</span><span class="sxs-lookup"><span data-stu-id="67df9-113">You can download and print it from here: [Overview diagram of Azure Machine Learning Studio capabilities](machine-learning-studio-overview-diagram.md).</span></span>
 
<span data-ttu-id="67df9-114">Si es nuevo campo toohello de máquina de aprendizaje en general, hay una serie de vídeos que podría ser útil tooyou.</span><span class="sxs-lookup"><span data-stu-id="67df9-114">If you're new toohello field of machine learning in general, there's a video series that might be helpful tooyou.</span></span> <span data-ttu-id="67df9-115">Se llama [ciencia de datos para principiantes](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) y puede ofrecerle un aprendizaje de toomachine introducción excelente utilizando lenguaje cotidiano y conceptos.</span><span class="sxs-lookup"><span data-stu-id="67df9-115">It's called [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) and it can give you a great introduction toomachine learning using everyday language and concepts.</span></span>


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
 

## <a name="hello-problem"></a><span data-ttu-id="67df9-116">problema de Hola</span><span class="sxs-lookup"><span data-stu-id="67df9-116">hello problem</span></span>

<span data-ttu-id="67df9-117">Supongamos que necesita toopredict riesgo del crédito de un individuo en función de información de Hola que le proporcionaron en una solicitud de crédito.</span><span class="sxs-lookup"><span data-stu-id="67df9-117">Suppose you need toopredict an individual's credit risk based on hello information they gave on a credit application.</span></span>  

<span data-ttu-id="67df9-118">La evaluación de riesgos de un crédito es un problema complejo, pero podemos simplificarlo un poco para usarlo en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="67df9-118">Credit risk assessment is a complex problem, but we can simplify it a bit for this walkthrough.</span></span> <span data-ttu-id="67df9-119">La usaremos como ejemplo de cómo puede crear una solución de análisis predictivo con Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="67df9-119">We'll use it as an example of how you can create a predictive analytics solution using Microsoft Azure Machine Learning.</span></span> <span data-ttu-id="67df9-120">toodo, utilizamos estudio de aprendizaje automático de Azure y un servicio web de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="67df9-120">toodo this, we use Azure Machine Learning Studio and a Machine Learning web service.</span></span>  

## <a name="hello-solution"></a><span data-ttu-id="67df9-121">solución de Hola</span><span class="sxs-lookup"><span data-stu-id="67df9-121">hello solution</span></span>

<span data-ttu-id="67df9-122">En este detallado tutorial, comenzamos con datos de riesgo de crédito y desarrollaremos y entrenaremos un modelo predictivo según esos datos.</span><span class="sxs-lookup"><span data-stu-id="67df9-122">In this detailed walkthrough, we start with publicly available credit risk data and develop and train a predictive model based on that data.</span></span> <span data-ttu-id="67df9-123">A continuación, implementamos modelo Hola como un servicio web para que pueda usar por otros usuarios para la evaluación del riesgo de crédito.</span><span class="sxs-lookup"><span data-stu-id="67df9-123">Then we deploy hello model as a web service so it can be used by others for credit risk assessment.</span></span>

<span data-ttu-id="67df9-124">toocreate esta solución de evaluación del riesgo de crédito, se siguen estos pasos:</span><span class="sxs-lookup"><span data-stu-id="67df9-124">toocreate this credit risk assessment solution, we follow these steps:</span></span>  

1. [<span data-ttu-id="67df9-125">Creación de un área de trabajo de Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="67df9-125">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="67df9-126">Carga de los datos existentes</span><span class="sxs-lookup"><span data-stu-id="67df9-126">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="67df9-127">Creación de un experimento</span><span class="sxs-lookup"><span data-stu-id="67df9-127">Create an experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="67df9-128">Entrenar y evaluar modelos de Hola</span><span class="sxs-lookup"><span data-stu-id="67df9-128">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="67df9-129">Implementar el servicio web de Hola</span><span class="sxs-lookup"><span data-stu-id="67df9-129">Deploy hello web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="67df9-130">Servicio web de acceso Hola</span><span class="sxs-lookup"><span data-stu-id="67df9-130">Access hello web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

> [!TIP] 
> <span data-ttu-id="67df9-131">Puede encontrar una copia de trabajo del experimento de Hola que desarrollamos en este tutorial Hola [Cortana Intelligence galería](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="67df9-131">You can find a working copy of hello experiment that we develop in this walkthrough in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="67df9-132">Vaya demasiado**[Tutorial: predicción de riesgo de crédito](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)**  y haga clic en **abierta en Studio** toodownload una copia del experimento de hello en el área de trabajo de estudio de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="67df9-132">Go too**[Walkthrough - Credit risk prediction](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)** and click **Open in Studio** toodownload a copy of hello experiment into your Machine Learning Studio workspace.</span></span>
> 
> <span data-ttu-id="67df9-133">En este tutorial se basa en una versión simplificada del experimento de ejemplo de Hola, [clasificación binaria: predicción de riesgo de crédito](http://go.microsoft.com/fwlink/?LinkID=525270), que también están disponibles en hello [galería](http://gallery.cortanaintelligence.com/).</span><span class="sxs-lookup"><span data-stu-id="67df9-133">This walkthrough is based on a simplified version of hello sample experiment, [Binary Classification: Credit risk prediction](http://go.microsoft.com/fwlink/?LinkID=525270), also available in hello [Gallery](http://gallery.cortanaintelligence.com/).</span></span>
