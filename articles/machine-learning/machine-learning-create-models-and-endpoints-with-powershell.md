---
title: "Creación de varios modelos a partir de un experimento | Microsoft Docs"
description: "Use PowerShell para crear varios modelos de Aprendizaje automático y puntos de conexión de servicio web con el mismo algoritmo pero con conjuntos de datos de entrenamiento distintos."
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1076b8eb-5a0d-4ac5-8601-8654d9be229f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: garye;haining
ms.openlocfilehash: 21d8c1ee0877df8d317d5a14131dc574fa5303c4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-many-machine-learning-models-and-web-service-endpoints-from-one-experiment-using-powershell"></a><span data-ttu-id="5b0f4-103">Creación de varios modelos de aprendizaje automático y puntos de conexión de servicio web a partir de un experimento mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b0f4-103">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>
<span data-ttu-id="5b0f4-104">Este es un problema común del aprendizaje automático: quiere crear muchos modelos que tienen el mismo flujo de trabajo de entrenamiento y utilizan el mismo algoritmo, pero tienen conjuntos de datos de entrenamiento distintos como entrada.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-104">Here's a common machine learning problem: You want to create many models that have the same training workflow and use the same algorithm, but have different training datasets as input.</span></span> <span data-ttu-id="5b0f4-105">Este artículo muestra cómo hacer esto a escala en Estudio de aprendizaje automático de Azure simplemente con un solo experimento.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-105">This article shows you how to do this at scale in Azure Machine Learning Studio using just a single experiment.</span></span>

<span data-ttu-id="5b0f4-106">Por ejemplo, digamos que posee una empresa de franquicias de alquiler de bicicletas global.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-106">For example, let's say you own a global bike rental franchise business.</span></span> <span data-ttu-id="5b0f4-107">Desea crear un modelo de regresión para predecir la demanda de alquiler basada en datos históricos.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-107">You want to build a regression model to predict the rental demand based on historic data.</span></span> <span data-ttu-id="5b0f4-108">Tiene 1000 ubicaciones de alquiler en todo el mundo y ha recopilado un conjunto de datos para cada ubicación que incluye características importantes como fecha, hora, meteorología y tráfico que son específicas de cada ubicación.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-108">You have 1,000 rental locations across the world and you've collected a dataset for each location that includes important features such as date, time, weather, and traffic that are specific to each location.</span></span>

<span data-ttu-id="5b0f4-109">Puede entrenar el modelo una vez usando una versión combinada de todos los conjuntos de datos en todas las ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-109">You could train your model once using a merged version of all the datasets across all locations.</span></span> <span data-ttu-id="5b0f4-110">Pero dado que cada una de las ubicaciones tiene un entorno único, un mejor enfoque sería entrenar el modelo de regresión por separado mediante el conjunto de datos de cada ubicación.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-110">But because each of your locations has a unique environment, a better approach would be to train your regression model separately using the dataset for each location.</span></span> <span data-ttu-id="5b0f4-111">De este modo, cada modelo entrenado podría tener en cuenta los diferentes tamaños de tienda, el volumen, la geografía, la población, el entorno de tráfico preparado para bicicletas, *etc*.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-111">That way, each trained model could take into account the different store sizes, volume, geography, population, bike-friendly traffic environment, *etc.*.</span></span>

<span data-ttu-id="5b0f4-112">Ese puede que sea el mejor enfoque, pero no desea crear 1000 experimentos de entrenamiento en Aprendizaje automático de Azure cada uno de los cuales representando una ubicación única.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-112">That may be the best approach, but you don't want to create 1,000 training experiments in Azure Machine Learning with each one representing a unique location.</span></span> <span data-ttu-id="5b0f4-113">Además de ser una tarea abrumadora, también parece bastante ineficaz, ya que cada experimento tendría exactamente los mismos componentes, excepto el conjunto de datos de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-113">Besides being an overwhelming task, it's also seems pretty inefficient since each experiment would have all the same components except for the training dataset.</span></span>

<span data-ttu-id="5b0f4-114">Por suerte, podemos lograrlo con la [API para volver a entrenar de Aprendizaje automático de Azure](machine-learning-retrain-models-programmatically.md) y automatizando la tarea con [PowerShell de Aprendizaje automático de Azure](machine-learning-powershell-module.md).</span><span class="sxs-lookup"><span data-stu-id="5b0f4-114">Fortunately, we can accomplish this by using the [Azure Machine Learning retraining API](machine-learning-retrain-models-programmatically.md) and automating the task with [Azure Machine Learning PowerShell](machine-learning-powershell-module.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5b0f4-115">Para que nuestro ejemplo se ejecute más rápido, reduciremos el número de ubicaciones de 1000 a 10.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-115">To make our sample run faster, we'll reduce the number of locations from 1,000 to 10.</span></span> <span data-ttu-id="5b0f4-116">Pero se aplican los mismos principios y procedimientos a 1000 ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-116">But the same principles and procedures apply to 1,000 locations.</span></span> <span data-ttu-id="5b0f4-117">La única diferencia es que si desea entrenar con 1000 conjuntos de datos, probablemente piense en ejecutar los siguientes scripts de PowerShell en paralelo.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-117">The only difference is that if you want to train from 1,000 datasets you probably want to think of running the following PowerShell scripts in parallel.</span></span> <span data-ttu-id="5b0f4-118">Cómo hacerlo queda fuera del ámbito de este artículo, pero puede encontrar ejemplos de subprocesamiento múltiple de PowerShell en Internet.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-118">How to do that is beyond the scope of this article, but you can find examples of PowerShell multi-threading on the Internet.</span></span>  
> 
> 

## <a name="set-up-the-training-experiment"></a><span data-ttu-id="5b0f4-119">Configuración del experimento de entrenamiento</span><span class="sxs-lookup"><span data-stu-id="5b0f4-119">Set up the training experiment</span></span>
<span data-ttu-id="5b0f4-120">Vamos a usar un [experimento de entrenamiento](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) de ejemplo que ya hemos creado en la [Galería de Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="5b0f4-120">We're going to use an example [training experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) that we've already created in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="5b0f4-121">Abra este experimento en su área de trabajo [Estudio de aprendizaje automático de Azure](https://studio.azureml.net) .</span><span class="sxs-lookup"><span data-stu-id="5b0f4-121">Open this experiment in your [Azure Machine Learning Studio](https://studio.azureml.net) workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="5b0f4-122">Para seguir este ejemplo, puede que le interese usar un área de trabajo estándar en lugar de un área de trabajo gratis.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-122">In order to follow along with this example, you may want to use a standard workspace rather than a free workspace.</span></span> <span data-ttu-id="5b0f4-123">Crearemos un punto de conexión para cada cliente (para un total de 10 puntos de conexión) y que requerirá un área de trabajo estándar, ya que un área de trabajo gratis se limitado a 3 puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-123">We'll be creating one endpoint for each customer - for a total of 10 endpoints - and that will require a standard workspace since a free workspace is limited to 3 endpoints.</span></span> <span data-ttu-id="5b0f4-124">Si solo tiene un área de trabajo gratis, solo tiene que modificar los scripts siguientes para permitir solo 3 ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-124">If you only have a free workspace, just modify the scripts below to allow for only 3 locations.</span></span>
> 
> 

<span data-ttu-id="5b0f4-125">El experimento usa un módulo **Importar datos** para importar el conjunto de datos de entrenamiento *customer001.csv* desde una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-125">The experiment uses an **Import Data** module to import the training dataset *customer001.csv* from an Azure storage account.</span></span> <span data-ttu-id="5b0f4-126">Supongamos que hemos recopilado los conjuntos de datos de entrenamiento de todas las ubicaciones de alquiler de bicicletas y los hemos almacenado en la misma ubicación de Blob Storage con nombres de archivo que van desde *rentalloc001.csv* a *rentalloc10.csv*.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-126">Let's assume we have collected training datasets from all bike rental locations and stored them in the same blob storage location with file names ranging from *rentalloc001.csv* to *rentalloc10.csv*.</span></span>

![imagen](./media/machine-learning-create-models-and-endpoints-with-powershell/reader-module.png)

<span data-ttu-id="5b0f4-128">Tenga en cuenta que se ha agregado el módulo **Web Service Output** (Resultados de servicio web) al módulo **Train Model** (Entrenar modelo).</span><span class="sxs-lookup"><span data-stu-id="5b0f4-128">Note that a **Web Service Output** module has been added to the **Train Model** module.</span></span>
<span data-ttu-id="5b0f4-129">Cuando este experimento se implementa como un servicio web, el punto de conexión asociado a esa salida devolverá el modelo entrenado con el formato de un archivo .ilearner.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-129">When this experiment is deployed as a web service, the endpoint associated with that output will return the trained model in the format of a .ilearner file.</span></span>

<span data-ttu-id="5b0f4-130">Observe también que configuramos un parámetro de servicio web para la dirección URL que el módulo **Importar datos** utiliza.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-130">Also note that we set up a web service parameter for the URL that the **Import Data** module uses.</span></span> <span data-ttu-id="5b0f4-131">Esto nos permite utilizar el parámetro para especificar conjuntos de datos de entrenamiento individuales para entrenar el modelo para cada ubicación.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-131">This allows us to use the parameter to specify individual training datasets to train the model for each location.</span></span>
<span data-ttu-id="5b0f4-132">Podríamos haber hecho esto de otras maneras; por ejemplo, podríamos haber usado una consulta SQL con un parámetro de servicio web para obtener datos de una base de datos SQL Azure o se podría haber usado un módulo **Web Service Input** (Entrada del servicio web) para pasar un conjunto de datos al servicio web.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-132">There are other ways we could have done this, such as using a SQL query with a web service parameter to get data from a SQL Azure database, or simply using a  **Web Service Input** module to pass in a dataset to the web service.</span></span>

![imagen](./media/machine-learning-create-models-and-endpoints-with-powershell/web-service-output.png)

<span data-ttu-id="5b0f4-134">Ahora, vamos a ejecutar este experimento de entrenamiento utilizando el valor predeterminado *rental001.csv* como el conjunto de datos de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-134">Now, let's run this training experiment using the default value *rental001.csv* as the training dataset.</span></span> <span data-ttu-id="5b0f4-135">Si ve los resultados del módulo **Evaluate** (Evaluar), después de hacer clic en los resultados y seleccionar **Visualize** (Visualizar), verá que obtenemos un rendimiento aceptable de *AUC* = 0,91.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-135">If you view the output of the **Evaluate** module (click the output and select **Visualize**), you can see we get a decent performance of *AUC* = 0.91.</span></span> <span data-ttu-id="5b0f4-136">En este momento, estamos listos para implementar un servicio web fuera de este experimento de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-136">At this point, we're ready to deploy a web service out of this training experiment.</span></span>

## <a name="deploy-the-training-and-scoring-web-services"></a><span data-ttu-id="5b0f4-137">Implementación del entrenamiento y puntuación de servicios web</span><span class="sxs-lookup"><span data-stu-id="5b0f4-137">Deploy the training and scoring web services</span></span>
<span data-ttu-id="5b0f4-138">Para implementar el servicio web de entrenamiento, haga clic en el botón **Set Up Web Service** (Configurar servicio web) situado debajo del lienzo del experimento y seleccione **Deploy Web Service** (Implementar servicio web).</span><span class="sxs-lookup"><span data-stu-id="5b0f4-138">To deploy the training web service, click the **Set Up Web Service** button below the experiment canvas and select **Deploy Web Service**.</span></span> <span data-ttu-id="5b0f4-139">Llame a este servicio web "Bike Rental Training" (Entrenamiento para alquiler de bicicletas).</span><span class="sxs-lookup"><span data-stu-id="5b0f4-139">Call this web service ""Bike Rental Training".</span></span>

<span data-ttu-id="5b0f4-140">Ahora debemos implementar el servicio web de puntuación.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-140">Now we need to deploy the scoring web service.</span></span>
<span data-ttu-id="5b0f4-141">Para ello, podemos hacer clic en **Set Up Web Service** (Configurar servicio web) bajo el lienzo y seleccionar **Predictive Web Service** (Servicio web predictivo).</span><span class="sxs-lookup"><span data-stu-id="5b0f4-141">To do this, we can click **Set Up Web Service** below the canvas and select **Predictive Web Service**.</span></span> <span data-ttu-id="5b0f4-142">Esto crear un experimento de puntuación.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-142">This creates a scoring experiment.</span></span>
<span data-ttu-id="5b0f4-143">Necesitamos realizar algunos ajustes menores para que funcione como un servicio web, como puede ser eliminar la columna de etiquetas "cnt" de los datos de entrada y limitar la salida a solo el identificador de instancia y el valor predicho correspondiente.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-143">We'll need to make a few minor adjustments to make it work as a web service, such as removing the label column "cnt" from the input data and limiting the output to only the instance id and the corresponding predicted value.</span></span>

<span data-ttu-id="5b0f4-144">Para ahorrarse ese trabajo, puede simplemente abrir el [experimento predictivo](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) en la galería que ya se ha preparado.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-144">To save yourself that work, you can simply open the [predictive experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) in the Gallery that's already been prepared.</span></span>

<span data-ttu-id="5b0f4-145">Para implementar el servicio web, ejecute el experimento predictivo y luego haga clic en el botón **Deploy Web Service** (Implementar servicio web) bajo el lienzo.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-145">To deploy the web service, run the predictive experiment, then click the **Deploy Web Service** button below the canvas.</span></span> <span data-ttu-id="5b0f4-146">Asigne el nombre "Bike Rental Scoring" (Puntuación de alquiler de bicicletas) al servicio web de puntuación.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-146">Name the scoring web service "Bike Rental Scoring"".</span></span>

## <a name="create-10-identical-web-service-endpoints-with-powershell"></a><span data-ttu-id="5b0f4-147">Creación de 10 puntos de conexión de servicio web idénticos con PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b0f4-147">Create 10 identical web service endpoints with PowerShell</span></span>
<span data-ttu-id="5b0f4-148">Este servicio web incluye un punto de conexión predeterminado.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-148">This web service comes with a default endpoint.</span></span> <span data-ttu-id="5b0f4-149">Pero no estamos más interesados en el punto de conexión predeterminado, ya que no se puede actualizar.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-149">But we're not as interested in the default endpoint since it can't be updated.</span></span> <span data-ttu-id="5b0f4-150">Lo que necesitamos hacer es crear 10 puntos de conexión adicionales, uno para cada ubicación.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-150">What we need to do is to create 10 additional endpoints, one for each location.</span></span> <span data-ttu-id="5b0f4-151">Haremos esto con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-151">We'll do this with PowerShell.</span></span>

<span data-ttu-id="5b0f4-152">En primer lugar, configure nuestro entorno de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5b0f4-152">First, we set up our PowerShell environment:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume the default configuration file exists and is properly set to point to the valid Workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

<span data-ttu-id="5b0f4-153">Después, ejecute el siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5b0f4-153">Then, run the following PowerShell command:</span></span>

    # Create 10 endpoints on the scoring web service.
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpointName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

<span data-ttu-id="5b0f4-154">Ahora hemos creado 10 puntos de conexión y todos ellos contienen el mismo modelo entrenado en *customer001.csv*.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-154">Now we've created 10 endpoints and they all contain the same trained model trained on *customer001.csv*.</span></span> <span data-ttu-id="5b0f4-155">Puede verlos en el Portal de administración de Azure.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-155">You can view them in the Azure Management Portal.</span></span>

![imagen](./media/machine-learning-create-models-and-endpoints-with-powershell/created-endpoints.png)

## <a name="update-the-endpoints-to-use-separate-training-datasets-using-powershell"></a><span data-ttu-id="5b0f4-157">Actualización de los puntos de conexión para usar conjuntos de datos de entrenamiento independientes mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b0f4-157">Update the endpoints to use separate training datasets using PowerShell</span></span>
<span data-ttu-id="5b0f4-158">El siguiente paso consiste en actualizar los puntos de conexión con modelos entrenados excepcionalmente en datos individuales de cada cliente.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-158">The next step is to update the endpoints with models uniquely trained on each customer's individual data.</span></span> <span data-ttu-id="5b0f4-159">Pero primero necesitamos generar estos modelos desde el servicio web **Bike Rental Training** (Entrenamiento para alquiler de bicicletas).</span><span class="sxs-lookup"><span data-stu-id="5b0f4-159">But first we need to produce these models from the **Bike Rental Training** web service.</span></span> <span data-ttu-id="5b0f4-160">Volvamos al servicio web **Bike Rental Training** (Entrenamiento para alquiler de bicicletas).</span><span class="sxs-lookup"><span data-stu-id="5b0f4-160">Let's go back to the **Bike Rental Training** web service.</span></span> <span data-ttu-id="5b0f4-161">Es necesario llamar a su punto de conexión BES 10 veces con 10 conjuntos de datos de entrenamiento distintos para generar 10 modelos diferentes.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-161">We need to call its BES endpoint 10 times with 10 different training datasets in order to produce 10 different models.</span></span> <span data-ttu-id="5b0f4-162">Vamos a usar el cmdlet de PowerShell **InovkeAmlWebServiceBESEndpoint** para hacerlo.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-162">We'll use the **InovkeAmlWebServiceBESEndpoint** PowerShell cmdlet to do this.</span></span>

<span data-ttu-id="5b0f4-163">También debe proporcionar credenciales para su cuenta de almacenamiento de blobs en `$configContent`, es decir, los campos `AccountName`, `AccountKey` y `RelativeLocation`.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-163">You will also need to provide credentials for your blob storage account into `$configContent`, namely, at the fields `AccountName`, `AccountKey` and `RelativeLocation`.</span></span> <span data-ttu-id="5b0f4-164">El `AccountName` puede ser uno de los nombres de cuenta, como se muestra en el **Portal de administración de Azure clásico** (pestaña*Almacenamiento* ).</span><span class="sxs-lookup"><span data-stu-id="5b0f4-164">The `AccountName` can be one of your account names, as seen in the **Classic Azure Management Portal** (*Storage* tab).</span></span> <span data-ttu-id="5b0f4-165">Cuando haga clic en una cuenta de almacenamiento, su `AccountKey` puede encontrarse presionando el botón **Administrar claves de acceso** , situado en la parte inferior, y copiando la *clave de acceso principal*.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-165">Once you click on a storage account, its `AccountKey` can be found by pressing the **Manage Access Keys** button at the bottom and copying the *Primary Access Key*.</span></span> <span data-ttu-id="5b0f4-166">El campo `RelativeLocation` es la ruta de acceso relativa al almacenamiento donde se almacenará un nuevo modelo.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-166">The `RelativeLocation` is the path relative to your storage where a new model will be stored.</span></span> <span data-ttu-id="5b0f4-167">Por ejemplo, la ruta de acceso `hai/retrain/bike_rental/` en el script siguiente señala a un contenedor denominado `hai` y `/retrain/bike_rental/` son subcarpetas.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-167">For instance, the path `hai/retrain/bike_rental/` in the script below points to a container named `hai`, and `/retrain/bike_rental/` are subfolders.</span></span> <span data-ttu-id="5b0f4-168">Actualmente, no puede crear subcarpetas a través del portal de interfaz de usuario, pero hay [varios exploradores de Almacenamiento de Azure](../storage/common/storage-explorers.md) que le permiten hacerlo.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-168">Currently, you cannot create subfolders through the portal UI, but there are [several Azure Storage Explorers](../storage/common/storage-explorers.md) that allow you to do so.</span></span> <span data-ttu-id="5b0f4-169">Se recomienda crear un contenedor en el almacenamiento para almacenar los nuevos modelos entrenados (archivos .ilearner) de esta forma: en la página de almacenamiento, haga clic en el botón **Agregar** de la parte inferior y asigne el nombre `retrain` al botón.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-169">It is recommended that you create a new container in your storage to store the new trained models (.ilearner files) as follows: from your storage page, click on the **Add** button at the bottom and name it `retrain`.</span></span> <span data-ttu-id="5b0f4-170">En resumen, los cambios necesarios para el siguiente script se refieren a `AccountName`, `AccountKey` y `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).</span><span class="sxs-lookup"><span data-stu-id="5b0f4-170">In summary, the necassary changes to the script below pertain to `AccountName`, `AccountKey` and `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).</span></span>

    # Invoke the retraining API 10 times
    # This is the default (and the only) endpoint on the training web service
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

> [!NOTE]
> <span data-ttu-id="5b0f4-171">El punto de conexión BES es el único modo admitido para esta operación.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-171">The BES endpoint is the only supported mode for this operation.</span></span> <span data-ttu-id="5b0f4-172">RRS no se puede usar para generar modelos entrenados.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-172">RRS cannot be used for producing trained models.</span></span>
> 
> 

<span data-ttu-id="5b0f4-173">Como puede ver anteriormente, en lugar de construir 10 archivos JSON de configuración de trabajos BES diferentes, creamos la cadena de configuración dinámicamente en su lugar y la introducimos en el parámetro *jobConfigString* del cmdlet **InvokeAmlWebServceBESEndpoint** , puesto que no es realmente necesario mantener una copia en disco.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-173">As you can see above, instead of constructing 10 different BES job configuration json files, we dynamically create the config string instead and feed it to the *jobConfigString* parameter of the **InvokeAmlWebServceBESEndpoint** cmdlet, since there is really no need to keep a copy on disk.</span></span>

<span data-ttu-id="5b0f4-174">Si todo va bien, después de un tiempo verá 10 archivos .ilearner (de *model001.ilearner* a *model010.ilearner*) en la cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-174">If everything goes well, after a while you should see 10 .ilearner files, from *model001.ilearner* to *model010.ilearner*, in your Azure storage account.</span></span> <span data-ttu-id="5b0f4-175">Ahora ya estamos listos para actualizar nuestros 10 puntos de conexión del servicio web de puntuación con estos modelos mediante el cmdlet de PowerShell **Patch AmlWebServiceEndpoint** .</span><span class="sxs-lookup"><span data-stu-id="5b0f4-175">Now we're ready to update our 10 scoring web service endpoints with these models using the **Patch-AmlWebServiceEndpoint** PowerShell cmdlet.</span></span> <span data-ttu-id="5b0f4-176">Recuerde una vez más que solo podemos revisar los puntos de conexión no predeterminados mediante programación creados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-176">Remember again that we can only patch the non-default endpoints we programmatically created earlier.</span></span>

    # Patch the 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '<my_blob_sas_token>'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }

<span data-ttu-id="5b0f4-177">Esto se debe ejecutar bastante rápido.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-177">This should run fairly quickly.</span></span> <span data-ttu-id="5b0f4-178">Cuando la ejecución finalice, habremos creado correctamente 10 puntos de conexión de servicio web predictivos, de manera que cada uno de ellos contendrá un modelo entrenado excepcionalmente en el conjunto de datos específico a una ubicación de alquiler, todo ello a partir de un solo experimento de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-178">When the execution finishes, we'll have successfully created 10 predictive web service endpoints, each containing a trained model uniquely trained on the dataset specific to a rental location, all from a single training experiment.</span></span> <span data-ttu-id="5b0f4-179">Para comprobarlo, intente llamar a estos puntos de conexión mediante el cmdlet **InvokeAmlWebServiceRRSEndpoint** , ofreciéndoles los mismos datos de entrada; debe ver diferentes resultados de predicción, ya que los modelos se entrenan con conjuntos de entrenamiento distintos.</span><span class="sxs-lookup"><span data-stu-id="5b0f4-179">To verify this, you can try calling these endpoints using the **InvokeAmlWebServiceRRSEndpoint** cmdlet, providing them with the same input data, and you should expect to see different prediction results since the models are trained with different training sets.</span></span>

## <a name="full-powershell-script"></a><span data-ttu-id="5b0f4-180">Script de PowerShell completo</span><span class="sxs-lookup"><span data-stu-id="5b0f4-180">Full PowerShell script</span></span>
<span data-ttu-id="5b0f4-181">Este es el listado del código fuente completo:</span><span class="sxs-lookup"><span data-stu-id="5b0f4-181">Here's the listing of the full source code:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume the default configuration file exists and properly set to point to the valid workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

    # Create 10 endpoints on the scoring web service
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpontName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

    # Invoke the retraining API 10 times to produce 10 regression models in .ilearner format
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

    # Patch the 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '?test'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }
