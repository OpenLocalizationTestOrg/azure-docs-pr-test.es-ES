---
title: "Paso 5: implementación del servicio web Machine Learning | Microsoft Docs"
description: "Paso 5 del tutorial Desarrollo de una solución predictiva: implementación de un experimento predictivo en Estudio de aprendizaje automático como servicio web."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 3fca74a3-c44b-4583-a218-c14c46ee5338
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: cec1bcceea158a20742c7019a266dcefaac4c9cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-5-deploy-the-azure-machine-learning-web-service"></a><span data-ttu-id="91a85-103">Paso 5 del tutorial: Implementar el servicio web de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="91a85-103">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span></span>
<span data-ttu-id="91a85-104">Este es el quinto paso del tutorial [Desarrollo de una solución de análisis predictiva para la evaluación del riesgo de crédito en Aprendizaje automático de Azure](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="91a85-104">This is the fifth step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="91a85-105">Creación de un área de trabajo de Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="91a85-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="91a85-106">Carga de los datos existentes</span><span class="sxs-lookup"><span data-stu-id="91a85-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="91a85-107">Crear un experimento nuevo</span><span class="sxs-lookup"><span data-stu-id="91a85-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="91a85-108">Entrenamiento y evaluación de los modelos</span><span class="sxs-lookup"><span data-stu-id="91a85-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. <span data-ttu-id="91a85-109">**Implementación del servicio web**</span><span class="sxs-lookup"><span data-stu-id="91a85-109">**Deploy the web service**</span></span>
6. [<span data-ttu-id="91a85-110">Acceso al servicio web</span><span class="sxs-lookup"><span data-stu-id="91a85-110">Access the web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="91a85-111">Para permitir que otros usuarios puedan usar el modelo predictivo desarrollado en este tutorial, se puede implementar como un servicio web en Azure.</span><span class="sxs-lookup"><span data-stu-id="91a85-111">To give others a chance to use the predictive model we've developed in this walkthrough, we can deploy it as a web service on Azure.</span></span>

<span data-ttu-id="91a85-112">Hasta ahora hemos estado experimentando con el entrenamiento de nuestro modelo.</span><span class="sxs-lookup"><span data-stu-id="91a85-112">Up to this point we've been experimenting with training our model.</span></span> <span data-ttu-id="91a85-113">Sin embargo, el servicio implementado ya no va a realizar el entrenamiento: va a generar nuevas predicciones mediante la puntuación de la entrada del usuario en función de nuestro modelo.</span><span class="sxs-lookup"><span data-stu-id="91a85-113">But the deployed service is no longer going to do training - it's going to generate new predictions by scoring the user's input based on our model.</span></span> <span data-ttu-id="91a85-114">Por lo tanto, hay que realizar unos cuantos preparativos para convertir este experimento de ***entrenamiento*** en un experimento ***predictivo***.</span><span class="sxs-lookup"><span data-stu-id="91a85-114">So we're going to do some preparation to convert this experiment from a ***training*** experiment to a ***predictive*** experiment.</span></span> 

<span data-ttu-id="91a85-115">Se trata de un proceso de tres pasos:</span><span class="sxs-lookup"><span data-stu-id="91a85-115">This is a three-step process:</span></span>  

1. <span data-ttu-id="91a85-116">Eliminación de uno de los modelos</span><span class="sxs-lookup"><span data-stu-id="91a85-116">Remove one of the models</span></span>
2. <span data-ttu-id="91a85-117">Conversión del *experimento de entrenamiento* que hemos creado en un *experimento predictivo*</span><span class="sxs-lookup"><span data-stu-id="91a85-117">Convert the *training experiment* we've created into a *predictive experiment*</span></span>
3. <span data-ttu-id="91a85-118">Implementar el experimento predictivo como servicio web</span><span class="sxs-lookup"><span data-stu-id="91a85-118">Deploy the predictive experiment as a web service</span></span>

## <a name="remove-one-of-the-models"></a><span data-ttu-id="91a85-119">Eliminación de uno de los modelos</span><span class="sxs-lookup"><span data-stu-id="91a85-119">Remove one of the models</span></span>

<span data-ttu-id="91a85-120">En primer lugar, debemos reducir este experimento un poco.</span><span class="sxs-lookup"><span data-stu-id="91a85-120">First, we need to trim this experiment down a little.</span></span> <span data-ttu-id="91a85-121">Actualmente, hay dos modelos distintos en el experimento, pero solo queremos usar uno al implementar esto como un servicio web.</span><span class="sxs-lookup"><span data-stu-id="91a85-121">We currently have two different models in the experiment, but we only want to use one model when we deploy this as a web service.</span></span>  

<span data-ttu-id="91a85-122">Pongamos que decidimos que el modelo de árbol ampliado ofrece un rendimiento mayor que el modelo SVM.</span><span class="sxs-lookup"><span data-stu-id="91a85-122">Let's say we've decided that the boosted tree model performed better than the SVM model.</span></span> <span data-ttu-id="91a85-123">Por tanto, lo primero que se debe hacer es eliminar el módulo [Two-Class Support Vector Machine][two-class-support-vector-machine] (Máquina de vectores de soporte de dos clases) y los módulos que se usaron para entrenarlo.</span><span class="sxs-lookup"><span data-stu-id="91a85-123">So the first thing to do is remove the [Two-Class Support Vector Machine][two-class-support-vector-machine] module and the modules that were used for training it.</span></span> <span data-ttu-id="91a85-124">Puede que desee hacer una copia del experimento antes; para ello, haga clic en **Guardar como** en la parte inferior del lienzo de experimento.</span><span class="sxs-lookup"><span data-stu-id="91a85-124">You may want to make a copy of the experiment first by clicking **Save As** at the bottom of the experiment canvas.</span></span>

<span data-ttu-id="91a85-125">Es necesario eliminar los siguientes módulos:</span><span class="sxs-lookup"><span data-stu-id="91a85-125">We need to delete the following modules:</span></span>  

* <span data-ttu-id="91a85-126">[Two-Class Support Vector Machine][two-class-support-vector-machine] (Máquina de vectores de soporte de dos clases)</span><span class="sxs-lookup"><span data-stu-id="91a85-126">[Two-Class Support Vector Machine][two-class-support-vector-machine]</span></span>
* <span data-ttu-id="91a85-127">Módulos [Train Model][train-model] (Entrenar modelo) y [Score Model][score-model] (Puntuar modelo) conectados a él</span><span class="sxs-lookup"><span data-stu-id="91a85-127">[Train Model][train-model] and [Score Model][score-model] modules that were connected to it</span></span>
* <span data-ttu-id="91a85-128">[Normalize Data][normalize-data] (Normalizar datos) (ambos)</span><span class="sxs-lookup"><span data-stu-id="91a85-128">[Normalize Data][normalize-data] (both of them)</span></span>
* <span data-ttu-id="91a85-129">[Evaluate Model][evaluate-model] (Evaluar modelo) (porque se ha terminado de evaluar los modelos)</span><span class="sxs-lookup"><span data-stu-id="91a85-129">[Evaluate Model][evaluate-model] (because we're finished evaluating the models)</span></span>

<span data-ttu-id="91a85-130">Seleccione cada módulo y presione la tecla Supr o haga clic con el botón derecho en el módulo y seleccione **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="91a85-130">Select each module and press the Delete key, or right-click the module and select **Delete**.</span></span> 

![Modelo de SVM con elementos quitados][3a]

<span data-ttu-id="91a85-132">Nuestro modelo debería tener ahora un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="91a85-132">Our model should now look something like this:</span></span>

![Modelo de SVM con elementos quitados][3]

<span data-ttu-id="91a85-134">Ahora ya estamos listos para implementar este modelo con el [Árbol de decisión ampliado de dos clases][two-class-boosted-decision-tree].</span><span class="sxs-lookup"><span data-stu-id="91a85-134">Now we're ready to deploy this model using the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree].</span></span>

## <a name="convert-the-training-experiment-to-a-predictive-experiment"></a><span data-ttu-id="91a85-135">Convertir un experimento de entrenamiento en experimento predictivo</span><span class="sxs-lookup"><span data-stu-id="91a85-135">Convert the training experiment to a predictive experiment</span></span>

<span data-ttu-id="91a85-136">Para tener este modelo listo para la implementación, tenemos que convertir este experimento de entrenamiento en un experimento de predicción.</span><span class="sxs-lookup"><span data-stu-id="91a85-136">To get this model ready for deployment, we need to convert this training experiment to a predictive experiment.</span></span> <span data-ttu-id="91a85-137">Esto implica tres pasos:</span><span class="sxs-lookup"><span data-stu-id="91a85-137">This involves three steps:</span></span>

1. <span data-ttu-id="91a85-138">Guardar el modelo que se ha entrenado y sustituir nuestros módulos de aprendizaje</span><span class="sxs-lookup"><span data-stu-id="91a85-138">Save the model we've trained and then replace our training modules</span></span>
2. <span data-ttu-id="91a85-139">Recortar el experimento para quitar los módulos que fueron necesarios solo para el entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="91a85-139">Trim the experiment to remove modules that were only needed for training</span></span>
3. <span data-ttu-id="91a85-140">Definir el lugar en el que el servicio web aceptará la entrada y en el que generará la salida</span><span class="sxs-lookup"><span data-stu-id="91a85-140">Define where the web service will accept input and where it generates the output</span></span>

<span data-ttu-id="91a85-141">Se puede hacer manualmente, pero afortunadamente, para realizar estos tres pasos, basta con hacer clic en la opción **Set Up Web Service** (Configurar servicio web) de la parte inferior del lienzo del experimento (y seleccionar la opción **Predictive web Service** [Servicio web predictivo]).</span><span class="sxs-lookup"><span data-stu-id="91a85-141">We could do this manually, but fortunately all three steps can be accomplished by clicking **Set Up Web Service** at the bottom of the experiment canvas (and selecting the **Predictive Web Service** option).</span></span>

> [!TIP]
> <span data-ttu-id="91a85-142">Si desea obtener más detalles sobre lo que ocurre cuando convierte un experimento de entrenamiento en uno de predicción, consulte el artículo sobre la [preparación del modelo de implementación en Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="91a85-142">If you want more details on what happens when you convert a training experiment to a predictive experiment, see [How to prepare your model for deployment in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span></span>

<span data-ttu-id="91a85-143">Al hacer clic en **Set Up Web Service**(Configurar servicio web), pasa lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="91a85-143">When you click **Set Up Web Service**, several things happen:</span></span>

* <span data-ttu-id="91a85-144">El modelo entrenado se convierte en un único módulo **Trained Model** (Modelo entrenado) y se guarda en la paleta de módulos que se encuentra a la izquierda del lienzo de experimento (se encuentra en **Modelos entrenados**).</span><span class="sxs-lookup"><span data-stu-id="91a85-144">The trained model is converted to a single **Trained Model** module and stored in the module palette to the left of the experiment canvas (you can find it under **Trained Models**)</span></span>
* <span data-ttu-id="91a85-145">Se quitan los módulos que se utilizaron para el entrenamiento, en particular:</span><span class="sxs-lookup"><span data-stu-id="91a85-145">Modules that were used for training are removed; specifically:</span></span>
  * <span data-ttu-id="91a85-146">[Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] (Árbol de decisión ampliado de dos clases)</span><span class="sxs-lookup"><span data-stu-id="91a85-146">[Two-Class Boosted Decision Tree][two-class-boosted-decision-tree]</span></span>
  * <span data-ttu-id="91a85-147">[Train Model][train-model] (Entrenar modelo)</span><span class="sxs-lookup"><span data-stu-id="91a85-147">[Train Model][train-model]</span></span>
  * <span data-ttu-id="91a85-148">[Split Data][split] (Dividir datos)</span><span class="sxs-lookup"><span data-stu-id="91a85-148">[Split Data][split]</span></span>
  * <span data-ttu-id="91a85-149">El segundo módulo [Execute R Script][execute-r-script] (Ejecutar script R) que se usó para probar los datos</span><span class="sxs-lookup"><span data-stu-id="91a85-149">the second [Execute R Script][execute-r-script] module that was used for test data</span></span>
* <span data-ttu-id="91a85-150">El modelo entrenado guardado se vuelve a agregar al experimento.</span><span class="sxs-lookup"><span data-stu-id="91a85-150">The saved trained model is added back into the experiment</span></span>
* <span data-ttu-id="91a85-151">Se agregan los módulos **Web service input** (Entrada al servicio web) y **Web service output** (Salida de servicio web), que identifican dónde los datos del usuario especificarán el modelo y qué datos se devolverán, cuando se accede al servicio web.</span><span class="sxs-lookup"><span data-stu-id="91a85-151">**Web service input** and **Web service output** modules are added (these identify where the user's data will enter the model, and what data is returned, when the web service is accessed)</span></span>

> [!NOTE]
> <span data-ttu-id="91a85-152">Puede ver que el experimento se guarda en dos partes en pestañas que se han agregado en la parte superior del lienzo del experimento.</span><span class="sxs-lookup"><span data-stu-id="91a85-152">You can see that the experiment is saved in two parts under tabs that have been added at the top of the experiment canvas.</span></span> <span data-ttu-id="91a85-153">El experimento de entrenamiento original está en la pestaña **Experimento de entrenamiento**, y el experimento de predicción recién creado está en **Experimento predictivo**.</span><span class="sxs-lookup"><span data-stu-id="91a85-153">The original training experiment is under the tab **Training experiment**, and the newly created predictive experiment is under **Predictive experiment**.</span></span> <span data-ttu-id="91a85-154">El experimento predictivo es el que se va a implementar como un servicio web.</span><span class="sxs-lookup"><span data-stu-id="91a85-154">The predictive experiment is the one we'll deploy as a web service.</span></span>

<span data-ttu-id="91a85-155">Necesitamos realizar un paso adicional con este experimento concreto.</span><span class="sxs-lookup"><span data-stu-id="91a85-155">We need to take one additional step with this particular experiment.</span></span>
<span data-ttu-id="91a85-156">Se han agregado dos módulos [Execute R Script][execute-r-script] (Ejecutar script R) para proporcionar una función de ponderación a los datos.</span><span class="sxs-lookup"><span data-stu-id="91a85-156">We added two [Execute R Script][execute-r-script] modules to provide a weighting function to the data.</span></span> <span data-ttu-id="91a85-157">Era simplemente un truco necesario para el entrenamiento y las pruebas, por lo que es posible quitar dichos módulos en el modelo final.</span><span class="sxs-lookup"><span data-stu-id="91a85-157">That was just a trick we needed for training and testing, so we can take out those modules in the final model.</span></span>
<span data-ttu-id="91a85-158">Machine Learning Studio quitó un módulo [Execute R Script][execute-r-script] (Ejecutar script R) cuando quitó el módulo [Split][split] (Dividir).</span><span class="sxs-lookup"><span data-stu-id="91a85-158">Machine Learning Studio removed one [Execute R Script][execute-r-script] module when it removed the [Split][split] module.</span></span> <span data-ttu-id="91a85-159">Ahora se puede quitar el otro y conectar [Editor de metadatos][metadata-editor] directamente a [Score Model][score-model] (Puntuar modelo).</span><span class="sxs-lookup"><span data-stu-id="91a85-159">Now we can remove the other and connect [Metadata Editor][metadata-editor] directly to [Score Model][score-model].</span></span>    

<span data-ttu-id="91a85-160">Nuestro experimento debería tener ahora un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="91a85-160">Our experiment should now look like this:</span></span>  

![Scoring the trained model][4]  

> [!NOTE]
> <span data-ttu-id="91a85-162">Quizás se pregunte por qué hemos dejado el conjunto de datos de los datos de datos de tarjeta de crédito alemana de UCI en el experimento predictivo.</span><span class="sxs-lookup"><span data-stu-id="91a85-162">You may be wondering why we left the UCI German Credit Card Data dataset in the predictive experiment.</span></span> <span data-ttu-id="91a85-163">El servicio va a utilizar los datos del usuario, no el conjunto de datos original; entonces, ¿por qué se deja el conjunto de datos original en el modelo?</span><span class="sxs-lookup"><span data-stu-id="91a85-163">The service is going to score the user's data, not the original dataset, so why leave the original dataset in the model?</span></span>
> 
> <span data-ttu-id="91a85-164">Es cierto que el servicio no necesita los datos originales de la tarjeta de crédito.</span><span class="sxs-lookup"><span data-stu-id="91a85-164">It's true that the service doesn't need the original credit card data.</span></span> <span data-ttu-id="91a85-165">Pero sí necesita el esquema para esos datos, que incluye información como la cantidad de columnas que hay y cuáles son numéricas.</span><span class="sxs-lookup"><span data-stu-id="91a85-165">But it does need the schema for that data, which includes information such as how many columns there are and which columns are numeric.</span></span> <span data-ttu-id="91a85-166">Esta información del esquema es necesaria para interpretar los datos del usuario.</span><span class="sxs-lookup"><span data-stu-id="91a85-166">This schema information is necessary to interpret the user's data.</span></span> <span data-ttu-id="91a85-167">Dejamos estos componentes conectados para que el módulo de puntuación tenga el esquema del conjunto de datos cuando el servicio se esté ejecutando.</span><span class="sxs-lookup"><span data-stu-id="91a85-167">We leave these components connected so that the scoring module has the dataset schema when the service is running.</span></span> <span data-ttu-id="91a85-168">No se utilizan los datos, sino solamente el esquema.</span><span class="sxs-lookup"><span data-stu-id="91a85-168">The data isn't used, just the schema.</span></span>  
> 
> 

<span data-ttu-id="91a85-169">Ejecute el experimento por última vez (haga clic en **Ejecutar**). Si desea comprobar que el modelo sigue funcionando, haga clic en la salida del módulo [Score Model][score-model] (Puntuar modelo) y seleccione **Ver resultados**.</span><span class="sxs-lookup"><span data-stu-id="91a85-169">Run the experiment one last time (click **Run**.) If you want to verify that the model is still working, click the output of the [Score Model][score-model] module and select **View Results**.</span></span> <span data-ttu-id="91a85-170">Puede ver que aparecen los datos originales, junto con el valor de riesgo de crédito (las "etiquetas puntuadas") y el valor de probabilidad de la puntuación (las "probabilidades puntuadas").</span><span class="sxs-lookup"><span data-stu-id="91a85-170">You can see that the original data is displayed, along with the credit risk value ("Scored Labels") and the scoring probability value ("Scored Probabilities".)</span></span> 

## <a name="deploy-the-web-service"></a><span data-ttu-id="91a85-171">Implementación del servicio web</span><span class="sxs-lookup"><span data-stu-id="91a85-171">Deploy the web service</span></span>
<span data-ttu-id="91a85-172">Puede implementar el experimento como un servicio web clásico o como un servicio web nuevo basado en Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="91a85-172">You can deploy the experiment as either a Classic web service, or as a New web service that's based on Azure Resource Manager.</span></span>

### <a name="deploy-as-a-classic-web-service"></a><span data-ttu-id="91a85-173">Implementación como servicio web clásico</span><span class="sxs-lookup"><span data-stu-id="91a85-173">Deploy as a Classic web service</span></span>
<span data-ttu-id="91a85-174">Para implementar un servicio web clásico derivado de nuestro experimento, haga clic en **Deploy Web Service** (Implementar servicio web) debajo del lienzo y seleccione **Deploy Web Service [Classic]** (Implementar servicio web [clásico]).</span><span class="sxs-lookup"><span data-stu-id="91a85-174">To deploy a Classic web service derived from our experiment, click **Deploy Web Service** below the canvas and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="91a85-175">Estudio de aprendizaje automático implementa el experimento como servicio web y lo remite al panel del servicio web.</span><span class="sxs-lookup"><span data-stu-id="91a85-175">Machine Learning Studio deploys the experiment as a web service and takes you to the dashboard for that web service.</span></span> <span data-ttu-id="91a85-176">Desde esta página, puede volver al experimento (**View snapshot** [Ver instantánea] o **View latest** [Ver más reciente]) y ejecutar una prueba sencilla del servicio web (consulte la sección **Prueba del servicio web** a continuación).</span><span class="sxs-lookup"><span data-stu-id="91a85-176">From this page you can return to the experiment (**View snapshot** or **View latest**) and run a simple test of the web service (see **Test the web service** below).</span></span> <span data-ttu-id="91a85-177">También hay información aquí para crear aplicaciones que puedan acceder al servicio web (más información al respecto en el siguiente paso de este tutorial).</span><span class="sxs-lookup"><span data-stu-id="91a85-177">There is also information here for creating applications that can access the web service (more on that in the next step of this walkthrough).</span></span>

![Panel del servicio web][6]

<span data-ttu-id="91a85-179">Puede configurar el servicio haciendo clic en la pestaña **CONFIGURACIÓN** .</span><span class="sxs-lookup"><span data-stu-id="91a85-179">You can configure the service by clicking the **CONFIGURATION** tab.</span></span> <span data-ttu-id="91a85-180">Aquí puede modificar el nombre del servicio (recibe de manera predeterminada el nombre del experimento) y proporcionarle una descripción.</span><span class="sxs-lookup"><span data-stu-id="91a85-180">Here you can modify the service name (it's given the experiment name by default) and give it a description.</span></span> <span data-ttu-id="91a85-181">También puede poner etiquetas más descriptivas para los datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="91a85-181">You can also give more friendly labels for the input and output data.</span></span>  

![Configurar el servicio web][5]  

### <a name="deploy-as-a-new-web-service"></a><span data-ttu-id="91a85-183">Implementación como servicio web nuevo</span><span class="sxs-lookup"><span data-stu-id="91a85-183">Deploy as a New web service</span></span>

> [!NOTE] 
> <span data-ttu-id="91a85-184">Para implementar un servicio web nuevo, debe tener permisos suficientes en la suscripción en la que lo implementa.</span><span class="sxs-lookup"><span data-stu-id="91a85-184">To deploy a New web service you must have sufficient permissions in the subscription to which you are deploying the web service.</span></span> <span data-ttu-id="91a85-185">Para obtener más información, consulte [Administración de un servicio web mediante el portal Servicios web Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="91a85-185">For more information, see [Manage a web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="91a85-186">Para implementar un servicio web nuevo derivado del experimento:</span><span class="sxs-lookup"><span data-stu-id="91a85-186">To deploy a New web service derived from our experiment:</span></span>

1. <span data-ttu-id="91a85-187">Haga clic en **Deploy Web Service** (Implementar servicio web) debajo del lienzo y seleccione **Deploy Web Service [New]** (Implementar servicio web [nuevo]).</span><span class="sxs-lookup"><span data-stu-id="91a85-187">Click **Deploy Web Service** below the canvas and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="91a85-188">Machine Learning Studio lo lleva a la página de **implementación de experimentos** del portal Servicios web Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="91a85-188">Machine Learning Studio transfers you to the Azure Machine Learning web services **Deploy Experiment** page.</span></span>

2. <span data-ttu-id="91a85-189">Escriba un nombre para el servicio web.</span><span class="sxs-lookup"><span data-stu-id="91a85-189">Enter a name for the web service.</span></span> 

3. <span data-ttu-id="91a85-190">Para **Plan de precios**, puede seleccionar un plan de precios existente, o seleccionar "Crear nuevo" y asignar un nombre al nuevo plan y seleccionar la opción de plan mensual.</span><span class="sxs-lookup"><span data-stu-id="91a85-190">For **Price Plan**, you can select an existing pricing plan, or select "Create new" and give the new plan a name and select the monthly plan option.</span></span> <span data-ttu-id="91a85-191">Los niveles de los planes predeterminados son los de la región predeterminada, y el servicio web se implementa en dicha región.</span><span class="sxs-lookup"><span data-stu-id="91a85-191">The plan tiers default to the plans for your default region and your web service is deployed to that region.</span></span>

4. <span data-ttu-id="91a85-192">Haga clic en **Implementar**.</span><span class="sxs-lookup"><span data-stu-id="91a85-192">Click **Deploy**.</span></span>

<span data-ttu-id="91a85-193">Después algunos minutos, se abre la página **Inicio rápido** del servicio web.</span><span class="sxs-lookup"><span data-stu-id="91a85-193">After a few minutes, the **Quickstart** page for your web service opens.</span></span>

<span data-ttu-id="91a85-194">Puede configurar el servicio haciendo clic en la pestaña **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="91a85-194">You can configure the service by clicking the **Configure** tab.</span></span> <span data-ttu-id="91a85-195">Aquí puede modificar el título del servicio y escribir una descripción.</span><span class="sxs-lookup"><span data-stu-id="91a85-195">Here you can modify the service title and give it a description.</span></span> 

<span data-ttu-id="91a85-196">Para probar el servicio web, haga clic en la pestaña **Probar** (vea la sección **Prueba del servicio web** a continuación).</span><span class="sxs-lookup"><span data-stu-id="91a85-196">To test the web service, click the **Test** tab (see **Test the web service** below).</span></span> <span data-ttu-id="91a85-197">Para obtener información sobre cómo crear aplicaciones que puedan acceder al servicio web, haga clic en la pestaña **Consumir** (en el siguiente paso de este tutorial puede encontrar más información).</span><span class="sxs-lookup"><span data-stu-id="91a85-197">For information on creating applications that can access the web service, click the **Consume** tab (the next step in this walkthrough will go into more detail).</span></span>

> [!TIP]
> <span data-ttu-id="91a85-198">Puede actualizar el servicio web después de haberlo implementado.</span><span class="sxs-lookup"><span data-stu-id="91a85-198">You can update the web service after you've deployed it.</span></span> <span data-ttu-id="91a85-199">Por ejemplo, si desea cambiar el modelo, edite el experimento de entrenamiento, ajuste los parámetros del modelo, haga clic en **Deploy Web Service** (Implementar servicio web) y seleccione **Deploy Web Service [Classic]** (Implementar servicio web [clásico]) o **Deploy Web Service [New]** (Implementar servicio web [nuevo]).</span><span class="sxs-lookup"><span data-stu-id="91a85-199">For example, if you want to change your model, then you can edit the training experiment, tweak the model parameters, and click **Deploy Web Service**, selecting **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span> <span data-ttu-id="91a85-200">Cuando implementa el experimento de nuevo, este sustituye al servicio web, ahora con el modelo actualizado.</span><span class="sxs-lookup"><span data-stu-id="91a85-200">When you deploy the experiment again, it replaces the web service, now using your updated model.</span></span>  
> 
> 

## <a name="test-the-web-service"></a><span data-ttu-id="91a85-201">Prueba del servicio web</span><span class="sxs-lookup"><span data-stu-id="91a85-201">Test the web service</span></span>

<span data-ttu-id="91a85-202">Cuando se accede al servicio web, los datos del usuario se escriben a través del módulo **Web service input** (Entrada al servicio web), donde se pasan al módulo [Score Model][score-model] (Puntuar modelo) y se puntúan.</span><span class="sxs-lookup"><span data-stu-id="91a85-202">When the web service is accessed, the user's data enters through the **Web service input** module where it's passed to the [Score Model][score-model] module and scored.</span></span> <span data-ttu-id="91a85-203">Según se ha configurado el experimento predictivo, el modelo espera los datos en el mismo formato que el conjunto de datos de riesgo de crédito original.</span><span class="sxs-lookup"><span data-stu-id="91a85-203">The way we've set up the predictive experiment, the model expects data in the same format as the original credit risk dataset.</span></span>
<span data-ttu-id="91a85-204">Los resultados se devuelven al usuario desde el servicio web a través del módulo **Web service output** (Salida del servicio web).</span><span class="sxs-lookup"><span data-stu-id="91a85-204">The results are returned to the user from the web service through the **Web service output** module.</span></span>

> [!TIP]
> <span data-ttu-id="91a85-205">La forma en que se configura el experimento predictivo permitirá que se devuelvan los resultados desde el módulo [Score Model][score-model] (Puntuar modelo).</span><span class="sxs-lookup"><span data-stu-id="91a85-205">The way we have the predictive experiment configured, the entire results from the [Score Model][score-model] module are returned.</span></span> <span data-ttu-id="91a85-206">Esto incluye todos los datos de entrada además del valor de riesgo de crédito y la probabilidad de puntuación.</span><span class="sxs-lookup"><span data-stu-id="91a85-206">This includes all the input data plus the credit risk value and the scoring probability.</span></span> <span data-ttu-id="91a85-207">Pero puede devolver algo distinto si lo desea; por ejemplo, podría devolver solamente el valor de riesgo de crédito.</span><span class="sxs-lookup"><span data-stu-id="91a85-207">But you can return something different if you want - for example, you could return just the credit risk value.</span></span> <span data-ttu-id="91a85-208">Para ello, inserte un módulo [Columnas del proyecto][project-columns] entre [Puntuar modelo][score-model] y **Web service output** (Salida del servicio web) para eliminar aquellas columnas que no desea que devuelva el servicio web.</span><span class="sxs-lookup"><span data-stu-id="91a85-208">To do this, insert a [Project Columns][project-columns] module between [Score Model][score-model] and the **Web service output** to eliminate columns you don't want the web service to return.</span></span> 
> 
> 

<span data-ttu-id="91a85-209">Puede probar el servicio web clásico en **Machine Learning Studio** o en el portal **Servicios web Azure Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="91a85-209">You can test a Classic web service either in **Machine Learning Studio** or in the **Azure Machine Learning Web Services** portal.</span></span>
<span data-ttu-id="91a85-210">Puede probar un servicio web nuevo en el portal **Servicios web Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="91a85-210">You can test a New web service only in the **Machine Learning Web Services** portal.</span></span>

> [!TIP]
> <span data-ttu-id="91a85-211">Al realizar pruebas en el portal Servicios web Azure Machine Learning, puede habilitar el portal para que cree datos de ejemplo que se puedan usar para probar el servicio de solicitud-respuesta.</span><span class="sxs-lookup"><span data-stu-id="91a85-211">When testing in the Azure Machine Learning Web Services portal, you can have the portal create sample data that you can use to test the Request-Response service.</span></span> <span data-ttu-id="91a85-212">En la página **Configurar**, seleccione "Yes" (Sí) para **Sample Data Enabled?** (¿Datos de ejemplo habilitados?).</span><span class="sxs-lookup"><span data-stu-id="91a85-212">On the **Configure** page, select "Yes" for **Sample Data Enabled?**.</span></span> <span data-ttu-id="91a85-213">Al abrir la pestaña Solicitud-respuesta en la página **Probar**, el portal rellena los datos de ejemplo obtenidos del conjunto de datos de riesgo de crédito original.</span><span class="sxs-lookup"><span data-stu-id="91a85-213">When you open the Request-Response tab on the **Test** page, the portal fills in sample data taken from the original credit risk dataset.</span></span>

### <a name="test-a-classic-web-service"></a><span data-ttu-id="91a85-214">Prueba de un servicio web clásico</span><span class="sxs-lookup"><span data-stu-id="91a85-214">Test a Classic web service</span></span>

<span data-ttu-id="91a85-215">Puede probar un servicio web clásico en Machine Learning Studio o en el portal Servicios web Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="91a85-215">You can test a Classic web service in Machine Learning Studio or in the Machine Learning Web Services portal.</span></span> 

#### <a name="test-in-machine-learning-studio"></a><span data-ttu-id="91a85-216">Prueba en Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="91a85-216">Test in Machine Learning Studio</span></span>

1. <span data-ttu-id="91a85-217">En la página **PANEL** del servicio web, haga clic en el botón **Probar** de **Default Endpoint** (Punto de conexión predeterminado).</span><span class="sxs-lookup"><span data-stu-id="91a85-217">On the **DASHBOARD** page for the web service, click the **Test** button under **Default Endpoint**.</span></span> <span data-ttu-id="91a85-218">Aparecerá un cuadro de diálogo que le pide los datos de entrada del servicio.</span><span class="sxs-lookup"><span data-stu-id="91a85-218">A dialog pops up and asks you for the input data for the service.</span></span> <span data-ttu-id="91a85-219">Se trata de las mismas columnas que aparecieron en el conjunto de datos original de riesgo de crédito original.</span><span class="sxs-lookup"><span data-stu-id="91a85-219">These are the same columns that appeared in the original credit risk dataset.</span></span>  

2. <span data-ttu-id="91a85-220">Escriba un conjunto de datos y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="91a85-220">Enter a set of data and then click **OK**.</span></span> 

#### <a name="test-in-the-machine-learning-web-services-portal"></a><span data-ttu-id="91a85-221">Prueba en el portal Servicios web Machine Learning</span><span class="sxs-lookup"><span data-stu-id="91a85-221">Test in the Machine Learning Web Services portal</span></span>

1. <span data-ttu-id="91a85-222">En la página **PANEL** del servicio web, haga clic en el botón **Test preview** (Vista preliminar de la prueba) de **Default Endpoint** (Punto de conexión predeterminado).</span><span class="sxs-lookup"><span data-stu-id="91a85-222">On the **DASHBOARD** page for the web service, click the **Test preview** link under **Default Endpoint**.</span></span> <span data-ttu-id="91a85-223">La página de prueba del portal Servicios web Azure Machine Learning para el punto de conexión del servicio web se abrirá y le pedirá los datos de entrada para el servicio.</span><span class="sxs-lookup"><span data-stu-id="91a85-223">The test page in the Azure Machine Learning Web Services portal for the web service endpoint opens and asks you for the input data for the service.</span></span> <span data-ttu-id="91a85-224">Se trata de las mismas columnas que aparecieron en el conjunto de datos original de riesgo de crédito original.</span><span class="sxs-lookup"><span data-stu-id="91a85-224">These are the same columns that appeared in the original credit risk dataset.</span></span>

2. <span data-ttu-id="91a85-225">Haga clic en **Test Request-Response** (Probar solicitud-respuesta).</span><span class="sxs-lookup"><span data-stu-id="91a85-225">Click **Test Request-Response**.</span></span> 

### <a name="test-a-new-web-service"></a><span data-ttu-id="91a85-226">Prueba de un servicio web nuevo</span><span class="sxs-lookup"><span data-stu-id="91a85-226">Test a New web service</span></span>

<span data-ttu-id="91a85-227">Puede probar un servicio web nuevo en el portal Servicios web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="91a85-227">You can test a New web service only in the Machine Learning Web Services portal.</span></span>

1. <span data-ttu-id="91a85-228">En el portal [Servicios web Azure Machine Learning](https://services.azureml.net/quickstart), haga clic en **Probar** en la parte superior de la página.</span><span class="sxs-lookup"><span data-stu-id="91a85-228">In the [Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal, click **Test** at the top of the page.</span></span> <span data-ttu-id="91a85-229">Se abrirá la página **Prueba** y podrá escribir datos para el servicio.</span><span class="sxs-lookup"><span data-stu-id="91a85-229">The **Test** page opens and you can input data for the service.</span></span> <span data-ttu-id="91a85-230">Los campos de entrada que se muestran corresponden a las columnas que aparecieron en el conjunto de datos original de riesgo de crédito.</span><span class="sxs-lookup"><span data-stu-id="91a85-230">The input fields displayed correspond to the columns that appeared in the original credit risk dataset.</span></span> 

2. <span data-ttu-id="91a85-231">Escriba un conjunto de datos y, después, haga clic en **Test Request-Response**(Probar solicitud-respuesta).</span><span class="sxs-lookup"><span data-stu-id="91a85-231">Enter a set of data and then click **Test Request-Response**.</span></span>

<span data-ttu-id="91a85-232">Los resultados de la prueba se muestran en el lado derecho de la página en la columna de salida.</span><span class="sxs-lookup"><span data-stu-id="91a85-232">The results of the test are displayed on the right-hand side of the page in the output column.</span></span> 


## <a name="manage-the-web-service"></a><span data-ttu-id="91a85-233">Administración del servicio web</span><span class="sxs-lookup"><span data-stu-id="91a85-233">Manage the web service</span></span>

### <a name="manage-a-classic-web-service-in-the-azure-classic-portal"></a><span data-ttu-id="91a85-234">Administración de un servicio web clásico en el Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="91a85-234">Manage a Classic web service in the Azure classic portal</span></span>

<span data-ttu-id="91a85-235">Cuando se haya implementado el servicio web clásico, podrá administrarlo desde el [Portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="91a85-235">Once you've deployed your Classic web service, you can manage it from the [Azure classic portal](https://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="91a85-236">Inicie sesión en el [Portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="91a85-236">Sign in to the [Azure classic portal](https://manage.windowsazure.com)</span></span>
2. <span data-ttu-id="91a85-237">En el panel Servicios de Microsoft Azure, haga clic en **MACHINE LEARNING**.</span><span class="sxs-lookup"><span data-stu-id="91a85-237">In the Microsoft Azure services panel, click **MACHINE LEARNING**</span></span>
3. <span data-ttu-id="91a85-238">Haga clic en el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="91a85-238">Click your workspace</span></span>
4. <span data-ttu-id="91a85-239">Haga clic en la pestaña **Servicios web**.</span><span class="sxs-lookup"><span data-stu-id="91a85-239">Click the **Web services** tab</span></span>
5. <span data-ttu-id="91a85-240">Haga clic en el servicio web creado.</span><span class="sxs-lookup"><span data-stu-id="91a85-240">Click the web service we created</span></span>
6. <span data-ttu-id="91a85-241">Haga clic en el punto de conexión "predeterminado".</span><span class="sxs-lookup"><span data-stu-id="91a85-241">Click the "default" endpoint</span></span>

<span data-ttu-id="91a85-242">Desde aquí, puede hacer tareas como supervisar el funcionamiento del servicio web y realizar ajustes de rendimiento cambiando el volumen de llamadas simultáneas que el servicio puede controlar.</span><span class="sxs-lookup"><span data-stu-id="91a85-242">From here, you can do things like monitor how the web service is doing and make performance tweaks by changing how many concurrent calls the service can handle.</span></span>

<span data-ttu-id="91a85-243">Para obtener información, consulte:</span><span class="sxs-lookup"><span data-stu-id="91a85-243">For more details, see:</span></span>

* [<span data-ttu-id="91a85-244">Creación de extremos</span><span class="sxs-lookup"><span data-stu-id="91a85-244">Creating Endpoints</span></span>](machine-learning-create-endpoint.md)
* [<span data-ttu-id="91a85-245">Escalado del servicio web</span><span class="sxs-lookup"><span data-stu-id="91a85-245">Scaling web service</span></span>](machine-learning-scaling-webservice.md)

### <a name="manage-a-classic-or-new-web-service-in-the-azure-machine-learning-web-services-portal"></a><span data-ttu-id="91a85-246">Administración de un servicio web nuevo o clásico en el portal Servicios web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="91a85-246">Manage a Classic or New web service in the Azure Machine Learning Web Services portal</span></span>

<span data-ttu-id="91a85-247">Cuando se haya implementado el servicio web, ya sea clásico o nuevo, podrá administrarlo desde el portal [Servicios web Microsoft Azure Machine Learning](https://services.azureml.net/quickstart).</span><span class="sxs-lookup"><span data-stu-id="91a85-247">Once you've deployed your web service, whether Classic or New, you can manage it from the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal.</span></span>

<span data-ttu-id="91a85-248">Para supervisar el rendimiento del servicio web, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="91a85-248">To monitor the performance of your web service:</span></span>

1. <span data-ttu-id="91a85-249">Inicie sesión en el portal [Servicios web Microsoft Azure Machine Learning](https://services.azureml.net/quickstart).</span><span class="sxs-lookup"><span data-stu-id="91a85-249">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal</span></span>
2. <span data-ttu-id="91a85-250">Haga clic en **Servicios web**.</span><span class="sxs-lookup"><span data-stu-id="91a85-250">Click **Web services**</span></span>
3. <span data-ttu-id="91a85-251">Haga clic en el servicio web.</span><span class="sxs-lookup"><span data-stu-id="91a85-251">Click your web service</span></span>
4. <span data-ttu-id="91a85-252">Haga clic en **Panel**.</span><span class="sxs-lookup"><span data-stu-id="91a85-252">Click the **Dashboard**</span></span>

- - -
<span data-ttu-id="91a85-253">**Siguiente: [Acceso al servicio web](machine-learning-walkthrough-6-access-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="91a85-253">**Next: [Access the web service](machine-learning-walkthrough-6-access-web-service.md)**</span></span>

[3]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3.png
[3a]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3a.png
[4]: ./media/machine-learning-walkthrough-5-publish-web-service/publish4.png
[5]: ./media/machine-learning-walkthrough-5-publish-web-service/publish5.png
[6]: ./media/machine-learning-walkthrough-5-publish-web-service/publish6.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[metadata-editor]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[project-columns]: https://msdn.microsoft.com/en-us/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
