---
title: 'Paso 2: Carga de datos en un experimento de Machine Learning | Microsoft Docs'
description: "Paso 2 del programa Hola a desarrollar un tutorial de solución de predicción: carga almacena datos públicos en estudio de aprendizaje automático de Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 9f4bc52e-9919-4dea-90ea-5cf7cc506d85
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 0ea21dcca2d0934ed06508560cf85cf31b48ce6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-2-upload-existing-data-into-an-azure-machine-learning-experiment"></a><span data-ttu-id="7ac95-103">Paso 2 del tutorial: Carga de los datos existentes en un experimento de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="7ac95-103">Walkthrough Step 2: Upload existing data into an Azure Machine Learning experiment</span></span>
<span data-ttu-id="7ac95-104">Esto es Hola segundo paso del tutorial de hello, [desarrollar una solución de análisis predictivos en aprendizaje automático de Azure](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="7ac95-104">This is hello second step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="7ac95-105">Creación de un área de trabajo de Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="7ac95-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. <span data-ttu-id="7ac95-106">**Carga de los datos existentes**</span><span class="sxs-lookup"><span data-stu-id="7ac95-106">**Upload existing data**</span></span>
3. [<span data-ttu-id="7ac95-107">Crear un experimento nuevo</span><span class="sxs-lookup"><span data-stu-id="7ac95-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="7ac95-108">Entrenar y evaluar modelos de Hola</span><span class="sxs-lookup"><span data-stu-id="7ac95-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="7ac95-109">Implementar el servicio Web de Hola</span><span class="sxs-lookup"><span data-stu-id="7ac95-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="7ac95-110">Acceder al servicio Web Hola</span><span class="sxs-lookup"><span data-stu-id="7ac95-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="7ac95-111">toodevelop un modelo de predicción de riesgo de crédito, es necesario que los datos que podemos usar tootrain y, a continuación, probar el modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7ac95-111">toodevelop a predictive model for credit risk, we need data that we can use tootrain and then test hello model.</span></span> <span data-ttu-id="7ac95-112">En este tutorial, usaremos Hola "Conjunto de datos UCI Statlog (datos de crédito alemana)" desde el repositorio de aprendizaje automático de UC Irvine Hola.</span><span class="sxs-lookup"><span data-stu-id="7ac95-112">For this walkthrough, we'll use hello "UCI Statlog (German Credit Data) Data Set" from hello UC Irvine Machine Learning repository.</span></span> <span data-ttu-id="7ac95-113">Puede encontrarlo aquí: </span><span class="sxs-lookup"><span data-stu-id="7ac95-113">You can find it here:</span></span>  
<span data-ttu-id="7ac95-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a></span><span class="sxs-lookup"><span data-stu-id="7ac95-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a></span></span>

<span data-ttu-id="7ac95-115">Vamos a usar con el nombre de archivo de hello **german.data**.</span><span class="sxs-lookup"><span data-stu-id="7ac95-115">We'll use hello file named **german.data**.</span></span> <span data-ttu-id="7ac95-116">Descargue este archivo tooyour el disco duro local.</span><span class="sxs-lookup"><span data-stu-id="7ac95-116">Download this file tooyour local hard drive.</span></span>  

<span data-ttu-id="7ac95-117">Hola **german.data** conjunto de datos contiene filas de 20 variables para los solicitantes de últimas 1000 de crédito.</span><span class="sxs-lookup"><span data-stu-id="7ac95-117">hello **german.data** dataset contains rows of 20 variables for 1000 past applicants for credit.</span></span> <span data-ttu-id="7ac95-118">Estas 20 variables representan Hola del conjunto de características (hello *vector de característica*), que proporciona características de identificación de los candidatos de crédito.</span><span class="sxs-lookup"><span data-stu-id="7ac95-118">These 20 variables represent hello dataset's set of features (hello *feature vector*), which provides identifying characteristics for each credit applicant.</span></span> <span data-ttu-id="7ac95-119">Una columna adicional en cada fila representa el riesgo de crédito calculados del solicitante de hello, con 700 candidatos identificados como un riesgo de crédito baja y 300 como un alto riesgo.</span><span class="sxs-lookup"><span data-stu-id="7ac95-119">An additional column in each row represents hello applicant's calculated credit risk, with 700 applicants identified as a low credit risk and 300 as a high risk.</span></span>

<span data-ttu-id="7ac95-120">sitio Web UCI Hola proporciona una descripción de los atributos de Hola de vector de característica de Hola para estos datos.</span><span class="sxs-lookup"><span data-stu-id="7ac95-120">hello UCI website provides a description of hello attributes of hello feature vector for this data.</span></span> <span data-ttu-id="7ac95-121">Entre estos figuran la información financiera, el historial crediticio, el estado de empleo e información personal.</span><span class="sxs-lookup"><span data-stu-id="7ac95-121">This includes financial information, credit history, employment status, and personal information.</span></span> <span data-ttu-id="7ac95-122">A cada solicitante se le ha dado una calificación binaria para indicar si son de riesgo de crédito alto o bajo.</span><span class="sxs-lookup"><span data-stu-id="7ac95-122">For each applicant, a binary rating has been given indicating whether they are a low or high credit risk.</span></span> 

<span data-ttu-id="7ac95-123">Usaremos esta tootrain un modelo de predicción de análisis de datos.</span><span class="sxs-lookup"><span data-stu-id="7ac95-123">We'll use this data tootrain a predictive analytics model.</span></span> <span data-ttu-id="7ac95-124">Cuando hayamos terminados, nuestro modelo debe ser capaz de tooaccept un vector de característica para un nuevo individuo y predecir si es un riesgo de crédito baja o alta.</span><span class="sxs-lookup"><span data-stu-id="7ac95-124">When we're done, our model should be able tooaccept a feature vector for a new individual and predict whether he or she is a low or high credit risk.</span></span>  

<span data-ttu-id="7ac95-125">Aquí hay un giro interesante.</span><span class="sxs-lookup"><span data-stu-id="7ac95-125">Here's an interesting twist.</span></span> <span data-ttu-id="7ac95-126">Hola descripción del conjunto de datos de hello en menciones de sitio Web de hello UCI lo que cuesta si se misclassify riesgo del crédito de una persona.</span><span class="sxs-lookup"><span data-stu-id="7ac95-126">hello description of hello dataset on hello UCI website mentions what it costs if we misclassify a person's credit risk.</span></span>
<span data-ttu-id="7ac95-127">Si el modelo Hola predice un riesgo de crédito alta para un usuario que es realmente un riesgo de crédito baja, modelo de hello ha realizado una clasificaciones incorrectas.</span><span class="sxs-lookup"><span data-stu-id="7ac95-127">If hello model predicts a high credit risk for someone who is actually a low credit risk, hello model has made a misclassification.</span></span>
<span data-ttu-id="7ac95-128">Pero clasificaciones incorrectas inversa de hello son cinco veces más costoso institución financiera de toohello: si el modelo de hello predice un riesgo de crédito baja para un usuario que es realmente un riesgo de crédito alta.</span><span class="sxs-lookup"><span data-stu-id="7ac95-128">But hello reverse misclassification is five times more costly toohello financial institution: if hello model predicts a low credit risk for someone who is actually a high credit risk.</span></span>

<span data-ttu-id="7ac95-129">Por lo tanto, es deseable tootrain nuestro modelo para que el costo de Hola de este último tipo de clasificaciones incorrectas es cinco veces mayor que clasifique mal Hola otra forma.</span><span class="sxs-lookup"><span data-stu-id="7ac95-129">So, we want tootrain our model so that hello cost of this latter type of misclassification is five times higher than misclassifying hello other way.</span></span>
<span data-ttu-id="7ac95-130">Toodo de una manera sencilla esto al modelo de hello en nuestro experimento de entrenamiento es duplicando (cinco veces) aquellas entradas que representan una persona con un riesgo de crédito alta.</span><span class="sxs-lookup"><span data-stu-id="7ac95-130">One simple way toodo this when training hello model in our experiment is by duplicating (five times) those entries that represent someone with a high credit risk.</span></span> <span data-ttu-id="7ac95-131">A continuación, si el modelo de hello misclassifies alguien como un riesgo de crédito baja cuando están realmente un alto riesgo, modelo Hola realiza esa misma clasificaciones de incorrectas cinco veces, una vez cada duplicado.</span><span class="sxs-lookup"><span data-stu-id="7ac95-131">Then, if hello model misclassifies someone as a low credit risk when they're actually a high risk, hello model does that same misclassification five times, once for each duplicate.</span></span> <span data-ttu-id="7ac95-132">Esto aumentará el costo de Hola de este error en los resultados de la formación de Hola.</span><span class="sxs-lookup"><span data-stu-id="7ac95-132">This will increase hello cost of this error in hello training results.</span></span>


## <a name="convert-hello-dataset-format"></a><span data-ttu-id="7ac95-133">Convertir el formato de conjunto de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="7ac95-133">Convert hello dataset format</span></span>
<span data-ttu-id="7ac95-134">Hola de conjunto de datos original utiliza un formato separado por el espacio en blanco.</span><span class="sxs-lookup"><span data-stu-id="7ac95-134">hello original dataset uses a blank-separated format.</span></span> <span data-ttu-id="7ac95-135">Estudio de aprendizaje automático funciona mejor con un archivo de valores separados por comas (CSV), por lo que se podrá convertir el conjunto de datos de hello reemplazando los espacios con comas.</span><span class="sxs-lookup"><span data-stu-id="7ac95-135">Machine Learning Studio works better with a comma-separated value (CSV) file, so we'll convert hello dataset by replacing spaces with commas.</span></span>  

<span data-ttu-id="7ac95-136">Estos datos no hay tooconvert de muchas maneras.</span><span class="sxs-lookup"><span data-stu-id="7ac95-136">There are many ways tooconvert this data.</span></span> <span data-ttu-id="7ac95-137">Una manera es mediante el uso de hello siguiente comando de Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7ac95-137">One way is by using hello following Windows PowerShell command:</span></span>   

    cat german.data | %{$_ -replace " ",","} | sc german.csv  

<span data-ttu-id="7ac95-138">Otra forma es mediante el uso de comando de sed Hola Unix:</span><span class="sxs-lookup"><span data-stu-id="7ac95-138">Another way is by using hello Unix sed command:</span></span>  

    sed 's/ /,/g' german.data > german.csv  

<span data-ttu-id="7ac95-139">En cualquier caso, hemos creado una versión separada por comas de los datos de hello en un archivo denominado **german.csv** que podemos usar en el experimento.</span><span class="sxs-lookup"><span data-stu-id="7ac95-139">In either case, we have created a comma-separated version of hello data in a file named **german.csv** that we can use in our experiment.</span></span>

## <a name="upload-hello-dataset-toomachine-learning-studio"></a><span data-ttu-id="7ac95-140">Cargar el conjunto de datos de hello tooMachine estudio de aprendizaje</span><span class="sxs-lookup"><span data-stu-id="7ac95-140">Upload hello dataset tooMachine Learning Studio</span></span>
<span data-ttu-id="7ac95-141">Una vez datos Hola formato tooCSV convertido, necesitamos tooupload en estudio de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="7ac95-141">Once hello data has been converted tooCSV format, we need tooupload it into Machine Learning Studio.</span></span> 

1. <span data-ttu-id="7ac95-142">Página principal de estudio de aprendizaje automático de hello abierto ([https://studio.azureml.net](https://studio.azureml.net)).</span><span class="sxs-lookup"><span data-stu-id="7ac95-142">Open hello Machine Learning Studio home page ([https://studio.azureml.net](https://studio.azureml.net)).</span></span> 

2. <span data-ttu-id="7ac95-143">Haga clic en el menú de hello ![menú][1] en la esquina superior izquierda de Hola de ventana hello, haga clic en **aprendizaje automático de Azure**, seleccione **Studio**e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="7ac95-143">Click hello menu ![Menu][1] in hello upper-left corner of hello window, click **Azure Machine Learning**, select **Studio**, and sign in.</span></span>

3. <span data-ttu-id="7ac95-144">Haga clic en **+ nuevo** final Hola de ventana hello.</span><span class="sxs-lookup"><span data-stu-id="7ac95-144">Click **+NEW** at hello bottom of hello window.</span></span>

4. <span data-ttu-id="7ac95-145">Seleccione **CONJUNTO DE DATOS**.</span><span class="sxs-lookup"><span data-stu-id="7ac95-145">Select **DATASET**.</span></span>

5. <span data-ttu-id="7ac95-146">Seleccione **DE ARCHIVO LOCAL**.</span><span class="sxs-lookup"><span data-stu-id="7ac95-146">Select **FROM LOCAL FILE**.</span></span>

    ![Adición de un conjunto de datos desde un archivo local][2]

6. <span data-ttu-id="7ac95-148">Hola **cargar un nuevo conjunto de datos** cuadro de diálogo, haga clic en **examinar** y buscar hello **german.csv** archivo que ha creado.</span><span class="sxs-lookup"><span data-stu-id="7ac95-148">In hello **Upload a new dataset** dialog, click **Browse** and find hello **german.csv** file you created.</span></span>

7. <span data-ttu-id="7ac95-149">Escriba un nombre para el conjunto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7ac95-149">Enter a name for hello dataset.</span></span> <span data-ttu-id="7ac95-150">En este tutorial, lo llamaremos "UCI German Credit Card Data".</span><span class="sxs-lookup"><span data-stu-id="7ac95-150">For this walkthrough, call it "UCI German Credit Card Data".</span></span>

8. <span data-ttu-id="7ac95-151">Para el tipo de datos, seleccione **Archivo CSV genérico sin encabezado (.nh.csv)**.</span><span class="sxs-lookup"><span data-stu-id="7ac95-151">For data type, select **Generic CSV File With no header (.nh.csv)**.</span></span>

9. <span data-ttu-id="7ac95-152">Agregue una descripción si así lo desea.</span><span class="sxs-lookup"><span data-stu-id="7ac95-152">Add a description if you’d like.</span></span>

10. <span data-ttu-id="7ac95-153">Haga clic en hello **Aceptar** marca de verificación.</span><span class="sxs-lookup"><span data-stu-id="7ac95-153">Click hello **OK** check mark.</span></span>  

    ![Carga el conjunto de datos de Hola][3]

<span data-ttu-id="7ac95-155">Esto carga los datos de hello en un módulo de conjunto de datos que podemos usar en un experimento.</span><span class="sxs-lookup"><span data-stu-id="7ac95-155">This uploads hello data into a dataset module that we can use in an experiment.</span></span>

<span data-ttu-id="7ac95-156">Puede administrar conjuntos de datos que ha cargado tooStudio haciendo clic en hello **conjuntos de datos** toohello de pestaña a la izquierda de la ventana de hello Studio.</span><span class="sxs-lookup"><span data-stu-id="7ac95-156">You can manage datasets that you've uploaded tooStudio by clicking hello **DATASETS** tab toohello left of hello Studio window.</span></span>

![Administración de conjuntos de datos][4]

<span data-ttu-id="7ac95-158">Para obtener más información sobre la importación de diversos tipos de datos a un experimento, consulte [Importar datos de entrenamiento en Azure Machine Learning Studio](machine-learning-data-science-import-data.md).</span><span class="sxs-lookup"><span data-stu-id="7ac95-158">For more information about importing other types of data into an experiment, see [Import your training data into Azure Machine Learning Studio](machine-learning-data-science-import-data.md).</span></span>

<span data-ttu-id="7ac95-159">**Siguiente: [Crear un experimento nuevo](machine-learning-walkthrough-3-create-new-experiment.md)**</span><span class="sxs-lookup"><span data-stu-id="7ac95-159">**Next: [Create a new experiment](machine-learning-walkthrough-3-create-new-experiment.md)**</span></span>

[1]: media/machine-learning-walkthrough-2-upload-data/menu.png
[2]: media/machine-learning-walkthrough-2-upload-data/add-dataset.png
[3]: media/machine-learning-walkthrough-2-upload-data/upload-dataset.png
[4]: media/machine-learning-walkthrough-2-upload-data/dataset-list.png
