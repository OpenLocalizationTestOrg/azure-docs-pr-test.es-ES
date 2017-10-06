---
title: "Paso 5: Implementar el servicio web de aprendizaje automático de hello | Documentos de Microsoft"
description: "Paso 5 de hello desarrollar un solución de predicción Tutorial: implementar un experimento de predicción en estudio de aprendizaje automático como un servicio web."
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
ms.openlocfilehash: 76391010972ed1450bbda8bfb2352c7b22b51ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-5-deploy-hello-azure-machine-learning-web-service"></a><span data-ttu-id="97eb4-103">Tutorial paso 5: Implementar el servicio web de aprendizaje automático de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="97eb4-103">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>
<span data-ttu-id="97eb4-104">Esto es Hola quinto paso del tutorial de hello, [desarrollar una solución de análisis predictivos en aprendizaje automático de Azure](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="97eb4-104">This is hello fifth step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="97eb4-105">Creación de un área de trabajo de Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="97eb4-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="97eb4-106">Carga de los datos existentes</span><span class="sxs-lookup"><span data-stu-id="97eb4-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="97eb4-107">Crear un experimento nuevo</span><span class="sxs-lookup"><span data-stu-id="97eb4-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="97eb4-108">Entrenar y evaluar modelos de Hola</span><span class="sxs-lookup"><span data-stu-id="97eb4-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. <span data-ttu-id="97eb4-109">**Implementar el servicio web de Hola**</span><span class="sxs-lookup"><span data-stu-id="97eb4-109">**Deploy hello web service**</span></span>
6. [<span data-ttu-id="97eb4-110">Servicio web de acceso Hola</span><span class="sxs-lookup"><span data-stu-id="97eb4-110">Access hello web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="97eb4-111">toogive otros una ocasión toouse Hola modelo predictivo, hemos desarrollado en este tutorial, nos podemos implementarlo como un servicio web en Azure.</span><span class="sxs-lookup"><span data-stu-id="97eb4-111">toogive others a chance toouse hello predictive model we've developed in this walkthrough, we can deploy it as a web service on Azure.</span></span>

<span data-ttu-id="97eb4-112">Toothis punto hemos sido experimentar con nuestro modelo de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="97eb4-112">Up toothis point we've been experimenting with training our model.</span></span> <span data-ttu-id="97eb4-113">Pero los servicio Hola implementado ya no queda toodo entrenamiento; será necesario toogenerate nuevas predicciones por entradas de usuario de hello según nuestro modelo de puntuación.</span><span class="sxs-lookup"><span data-stu-id="97eb4-113">But hello deployed service is no longer going toodo training - it's going toogenerate new predictions by scoring hello user's input based on our model.</span></span> <span data-ttu-id="97eb4-114">Por lo que vamos a toodo algunos tooconvert preparación esto experimentar de un ***entrenamiento*** experimentar tooa ***predictivo*** experimentar.</span><span class="sxs-lookup"><span data-stu-id="97eb4-114">So we're going toodo some preparation tooconvert this experiment from a ***training*** experiment tooa ***predictive*** experiment.</span></span> 

<span data-ttu-id="97eb4-115">Se trata de un proceso de tres pasos:</span><span class="sxs-lookup"><span data-stu-id="97eb4-115">This is a three-step process:</span></span>  

1. <span data-ttu-id="97eb4-116">Quite uno de los modelos de Hola</span><span class="sxs-lookup"><span data-stu-id="97eb4-116">Remove one of hello models</span></span>
2. <span data-ttu-id="97eb4-117">Convertir hello *experimento de entrenamiento* hemos creado en un *experimento predictivo*</span><span class="sxs-lookup"><span data-stu-id="97eb4-117">Convert hello *training experiment* we've created into a *predictive experiment*</span></span>
3. <span data-ttu-id="97eb4-118">Implementar experimento predictivo Hola como un servicio web</span><span class="sxs-lookup"><span data-stu-id="97eb4-118">Deploy hello predictive experiment as a web service</span></span>

## <a name="remove-one-of-hello-models"></a><span data-ttu-id="97eb4-119">Quite uno de los modelos de Hola</span><span class="sxs-lookup"><span data-stu-id="97eb4-119">Remove one of hello models</span></span>

<span data-ttu-id="97eb4-120">En primer lugar, necesitamos tootrim este experimento hacia abajo un poco.</span><span class="sxs-lookup"><span data-stu-id="97eb4-120">First, we need tootrim this experiment down a little.</span></span> <span data-ttu-id="97eb4-121">Actualmente tenemos dos modelos distintos en el experimento de hello, pero solamente queremos toouse un modelo cuando esto se implementa como un servicio web.</span><span class="sxs-lookup"><span data-stu-id="97eb4-121">We currently have two different models in hello experiment, but we only want toouse one model when we deploy this as a web service.</span></span>  

<span data-ttu-id="97eb4-122">Supongamos que hemos decidido ese modelo de árbol de hello impulsado realiza un rendimiento mejor que el modelo SVM de Hola.</span><span class="sxs-lookup"><span data-stu-id="97eb4-122">Let's say we've decided that hello boosted tree model performed better than hello SVM model.</span></span> <span data-ttu-id="97eb4-123">Por lo que Hola primera cosa toodo es quitar hello [máquina de vectores de soporte de dos clases] [ two-class-support-vector-machine] módulo y módulos de Hola que se utilizaron para entrenar a él.</span><span class="sxs-lookup"><span data-stu-id="97eb4-123">So hello first thing toodo is remove hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module and hello modules that were used for training it.</span></span> <span data-ttu-id="97eb4-124">Puede que desee toomake una copia del experimento de hello en primer lugar, haga clic en **Guardar como** final Hola de hello experimentar el lienzo.</span><span class="sxs-lookup"><span data-stu-id="97eb4-124">You may want toomake a copy of hello experiment first by clicking **Save As** at hello bottom of hello experiment canvas.</span></span>

<span data-ttu-id="97eb4-125">Necesitamos hello toodelete siguientes módulos:</span><span class="sxs-lookup"><span data-stu-id="97eb4-125">We need toodelete hello following modules:</span></span>  

* <span data-ttu-id="97eb4-126">[Two-Class Support Vector Machine][two-class-support-vector-machine] (Máquina de vectores de soporte de dos clases)</span><span class="sxs-lookup"><span data-stu-id="97eb4-126">[Two-Class Support Vector Machine][two-class-support-vector-machine]</span></span>
* <span data-ttu-id="97eb4-127">[Entrenar modelo] [ train-model] y [puntuar modelo] [ score-model] módulos que estaban conectado tooit</span><span class="sxs-lookup"><span data-stu-id="97eb4-127">[Train Model][train-model] and [Score Model][score-model] modules that were connected tooit</span></span>
* <span data-ttu-id="97eb4-128">[Normalize Data][normalize-data] (Normalizar datos) (ambos)</span><span class="sxs-lookup"><span data-stu-id="97eb4-128">[Normalize Data][normalize-data] (both of them)</span></span>
* <span data-ttu-id="97eb4-129">[Evaluar el modelo de] [ evaluate-model] (porque se haya terminado de evaluación de modelos de hello)</span><span class="sxs-lookup"><span data-stu-id="97eb4-129">[Evaluate Model][evaluate-model] (because we're finished evaluating hello models)</span></span>

<span data-ttu-id="97eb4-130">Seleccione cada módulo y presione la tecla SUPR de Hola o un módulo de Hola de menú contextual y seleccione **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="97eb4-130">Select each module and press hello Delete key, or right-click hello module and select **Delete**.</span></span> 

![Quita el modelo SVM de Hola][3a]

<span data-ttu-id="97eb4-132">Nuestro modelo debería tener ahora un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="97eb4-132">Our model should now look something like this:</span></span>

![Quita el modelo SVM de Hola][3]

<span data-ttu-id="97eb4-134">Ahora estamos listo toodeploy esto modelados con hello [árbol de decisión impulsado de dos clases][two-class-boosted-decision-tree].</span><span class="sxs-lookup"><span data-stu-id="97eb4-134">Now we're ready toodeploy this model using hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree].</span></span>

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a><span data-ttu-id="97eb4-135">Convertir el experimento de predicción de hello entrenamiento experimento tooa</span><span class="sxs-lookup"><span data-stu-id="97eb4-135">Convert hello training experiment tooa predictive experiment</span></span>

<span data-ttu-id="97eb4-136">tooget este modelo listo para la implementación, necesitamos tooconvert este experimento tooa predictivo experimento de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="97eb4-136">tooget this model ready for deployment, we need tooconvert this training experiment tooa predictive experiment.</span></span> <span data-ttu-id="97eb4-137">Esto implica tres pasos:</span><span class="sxs-lookup"><span data-stu-id="97eb4-137">This involves three steps:</span></span>

1. <span data-ttu-id="97eb4-138">Guardar el modelo de Hola se ha entrenado y, a continuación, reemplace nuestros módulos de entrenamiento</span><span class="sxs-lookup"><span data-stu-id="97eb4-138">Save hello model we've trained and then replace our training modules</span></span>
2. <span data-ttu-id="97eb4-139">Módulos de tooremove de experimento de Hola que eran necesarios únicamente para el entrenamiento de recorte</span><span class="sxs-lookup"><span data-stu-id="97eb4-139">Trim hello experiment tooremove modules that were only needed for training</span></span>
3. <span data-ttu-id="97eb4-140">Definir donde va a Aceptar proporcionados por el servicio web de Hola y donde genera la salida de hello</span><span class="sxs-lookup"><span data-stu-id="97eb4-140">Define where hello web service will accept input and where it generates hello output</span></span>

<span data-ttu-id="97eb4-141">Podríamos hacer esto manualmente, pero afortunadamente, los tres pasos pueden realizarse haciendo clic en **configurar el servicio de Web** final Hola del lienzo del experimento de hello (y seleccionando hello **predictivo servicio Web** opción).</span><span class="sxs-lookup"><span data-stu-id="97eb4-141">We could do this manually, but fortunately all three steps can be accomplished by clicking **Set Up Web Service** at hello bottom of hello experiment canvas (and selecting hello **Predictive Web Service** option).</span></span>

> [!TIP]
> <span data-ttu-id="97eb4-142">Si desea obtener más detalles sobre lo que ocurre cuando se convierte un tooa de experimento de entrenamiento predictivo experimentar, consulte [cómo tooprepare el modelo para la implementación en estudio de aprendizaje automático de Azure](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="97eb4-142">If you want more details on what happens when you convert a training experiment tooa predictive experiment, see [How tooprepare your model for deployment in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span></span>

<span data-ttu-id="97eb4-143">Al hacer clic en **Set Up Web Service**(Configurar servicio web), pasa lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="97eb4-143">When you click **Set Up Web Service**, several things happen:</span></span>

* <span data-ttu-id="97eb4-144">Hola entrenado es convertido tooa único **entrenado** módulo y almacenan en hello módulo paleta toohello izquierda de hello experimentar lienzo (puede encontrar en **modelos entrenados**)</span><span class="sxs-lookup"><span data-stu-id="97eb4-144">hello trained model is converted tooa single **Trained Model** module and stored in hello module palette toohello left of hello experiment canvas (you can find it under **Trained Models**)</span></span>
* <span data-ttu-id="97eb4-145">Se quitan los módulos que se utilizaron para el entrenamiento, en particular:</span><span class="sxs-lookup"><span data-stu-id="97eb4-145">Modules that were used for training are removed; specifically:</span></span>
  * <span data-ttu-id="97eb4-146">[Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] (Árbol de decisión ampliado de dos clases)</span><span class="sxs-lookup"><span data-stu-id="97eb4-146">[Two-Class Boosted Decision Tree][two-class-boosted-decision-tree]</span></span>
  * <span data-ttu-id="97eb4-147">[Train Model][train-model] (Entrenar modelo)</span><span class="sxs-lookup"><span data-stu-id="97eb4-147">[Train Model][train-model]</span></span>
  * <span data-ttu-id="97eb4-148">[Split Data][split] (Dividir datos)</span><span class="sxs-lookup"><span data-stu-id="97eb4-148">[Split Data][split]</span></span>
  * <span data-ttu-id="97eb4-149">en segundo lugar Hola [ejecutar Script de R] [ execute-r-script] módulo que se usa para los datos de prueba</span><span class="sxs-lookup"><span data-stu-id="97eb4-149">hello second [Execute R Script][execute-r-script] module that was used for test data</span></span>
* <span data-ttu-id="97eb4-150">modelo entrenado Hola guardado se agrega en el experimento de Hola</span><span class="sxs-lookup"><span data-stu-id="97eb4-150">hello saved trained model is added back into hello experiment</span></span>
* <span data-ttu-id="97eb4-151">**Entrada de servicio de Web** y **Web resultado del servicio** módulos se agregan (identifican donde los datos del usuario de hello introducirá modelo hello, así como qué datos se devuelven cuando se accede al servicio web de hello)</span><span class="sxs-lookup"><span data-stu-id="97eb4-151">**Web service input** and **Web service output** modules are added (these identify where hello user's data will enter hello model, and what data is returned, when hello web service is accessed)</span></span>

> [!NOTE]
> <span data-ttu-id="97eb4-152">Puede ver que el experimento de Hola se guarda en dos partes en pestañas que se han agregado en parte superior de hello del lienzo del experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="97eb4-152">You can see that hello experiment is saved in two parts under tabs that have been added at hello top of hello experiment canvas.</span></span> <span data-ttu-id="97eb4-153">Hello experimento de entrenamiento original está en la ficha de hello **experimento de entrenamiento**, y Hola recién creado experimento predictivo está por debajo del **experimento predictivo**.</span><span class="sxs-lookup"><span data-stu-id="97eb4-153">hello original training experiment is under hello tab **Training experiment**, and hello newly created predictive experiment is under **Predictive experiment**.</span></span> <span data-ttu-id="97eb4-154">experimento predictivo Hello es hello uno que se implementará como un servicio web.</span><span class="sxs-lookup"><span data-stu-id="97eb4-154">hello predictive experiment is hello one we'll deploy as a web service.</span></span>

<span data-ttu-id="97eb4-155">Es necesario un paso adicional tootake con este experimento determinado.</span><span class="sxs-lookup"><span data-stu-id="97eb4-155">We need tootake one additional step with this particular experiment.</span></span>
<span data-ttu-id="97eb4-156">Hemos agregado dos [ejecutar Script de R] [ execute-r-script] tooprovide módulos una ponderación función toohello datos.</span><span class="sxs-lookup"><span data-stu-id="97eb4-156">We added two [Execute R Script][execute-r-script] modules tooprovide a weighting function toohello data.</span></span> <span data-ttu-id="97eb4-157">Que era simplemente un truco que necesitábamos para el entrenamiento y pruebas, por lo que podemos realizar out esos módulos en el modelo final Hola.</span><span class="sxs-lookup"><span data-stu-id="97eb4-157">That was just a trick we needed for training and testing, so we can take out those modules in hello final model.</span></span>
<span data-ttu-id="97eb4-158">Estudio de aprendizaje automático quitado uno [ejecutar Script de R] [ execute-r-script] módulo cuando quita hello [división] [ split] módulo.</span><span class="sxs-lookup"><span data-stu-id="97eb4-158">Machine Learning Studio removed one [Execute R Script][execute-r-script] module when it removed hello [Split][split] module.</span></span> <span data-ttu-id="97eb4-159">Ahora podemos quitar Hola sí y conectar [Editor de metadatos] [ metadata-editor] directamente demasiado[puntuar modelo][score-model].</span><span class="sxs-lookup"><span data-stu-id="97eb4-159">Now we can remove hello other and connect [Metadata Editor][metadata-editor] directly too[Score Model][score-model].</span></span>    

<span data-ttu-id="97eb4-160">Nuestro experimento debería tener ahora un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="97eb4-160">Our experiment should now look like this:</span></span>  

![La puntuación del modelo entrenado Hola][4]  

> [!NOTE]
> <span data-ttu-id="97eb4-162">Quizás se pregunte por qué se deja el conjunto de datos de tarjeta de crédito de alemán de UCI de Hola en experimento predictivo Hola.</span><span class="sxs-lookup"><span data-stu-id="97eb4-162">You may be wondering why we left hello UCI German Credit Card Data dataset in hello predictive experiment.</span></span> <span data-ttu-id="97eb4-163">servicio de Hello va datos del usuario de tooscore hello, no Hola conjunto de datos original, por lo tanto ¿por qué dejar Hola conjunto de datos original en hello modelo?</span><span class="sxs-lookup"><span data-stu-id="97eb4-163">hello service is going tooscore hello user's data, not hello original dataset, so why leave hello original dataset in hello model?</span></span>
> 
> <span data-ttu-id="97eb4-164">Es cierto que servicio hello no necesita datos de tarjeta de crédito originales Hola.</span><span class="sxs-lookup"><span data-stu-id="97eb4-164">It's true that hello service doesn't need hello original credit card data.</span></span> <span data-ttu-id="97eb4-165">Pero debe esquema Hola de esos datos, que incluye información como el número de columnas hay y qué columnas son numéricos.</span><span class="sxs-lookup"><span data-stu-id="97eb4-165">But it does need hello schema for that data, which includes information such as how many columns there are and which columns are numeric.</span></span> <span data-ttu-id="97eb4-166">Esta información de esquema es datos del usuario de hello toointerpret necesarios.</span><span class="sxs-lookup"><span data-stu-id="97eb4-166">This schema information is necessary toointerpret hello user's data.</span></span> <span data-ttu-id="97eb4-167">Se deje estos componentes conectados para que hello puntuación módulo tiene esquema de conjunto de datos de hello cuando se está ejecutando el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="97eb4-167">We leave these components connected so that hello scoring module has hello dataset schema when hello service is running.</span></span> <span data-ttu-id="97eb4-168">no se usan datos de Hello, solo el esquema de Hola.</span><span class="sxs-lookup"><span data-stu-id="97eb4-168">hello data isn't used, just hello schema.</span></span>  
> 
> 

<span data-ttu-id="97eb4-169">Ejecute el experimento de hello una última vez (haga clic en **ejecutar**.) Si desea tooverify que Hola modelo sigue funcionando, haga clic en salida de hello de hello [puntuar modelo] [ score-model] módulo y seleccione **ver los resultados de**.</span><span class="sxs-lookup"><span data-stu-id="97eb4-169">Run hello experiment one last time (click **Run**.) If you want tooverify that hello model is still working, click hello output of hello [Score Model][score-model] module and select **View Results**.</span></span> <span data-ttu-id="97eb4-170">Puede ver que se muestran los datos originales de hello, junto con el valor de riesgo de crédito de hello ("etiquetas con puntuación") y Hola la puntuación del valor de probabilidad ("puntúan probabilidades".)</span><span class="sxs-lookup"><span data-stu-id="97eb4-170">You can see that hello original data is displayed, along with hello credit risk value ("Scored Labels") and hello scoring probability value ("Scored Probabilities".)</span></span> 

## <a name="deploy-hello-web-service"></a><span data-ttu-id="97eb4-171">Implementar el servicio web de Hola</span><span class="sxs-lookup"><span data-stu-id="97eb4-171">Deploy hello web service</span></span>
<span data-ttu-id="97eb4-172">Puede implementar Hola experimento como un servicio web de clásico o como un nuevo servicio web que se basa en el Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="97eb4-172">You can deploy hello experiment as either a Classic web service, or as a New web service that's based on Azure Resource Manager.</span></span>

### <a name="deploy-as-a-classic-web-service"></a><span data-ttu-id="97eb4-173">Implementación como servicio web clásico</span><span class="sxs-lookup"><span data-stu-id="97eb4-173">Deploy as a Classic web service</span></span>
<span data-ttu-id="97eb4-174">toodeploy un clásico web servicio derivado de nuestro experimento, haga clic en **implementar el servicio de Web** por debajo de hello lienzo y seleccione **implementar servicio Web [estándar]**.</span><span class="sxs-lookup"><span data-stu-id="97eb4-174">toodeploy a Classic web service derived from our experiment, click **Deploy Web Service** below hello canvas and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="97eb4-175">Estudio de aprendizaje automático implementa Hola experimento como un servicio web y le toohello panel para ese servicio web.</span><span class="sxs-lookup"><span data-stu-id="97eb4-175">Machine Learning Studio deploys hello experiment as a web service and takes you toohello dashboard for that web service.</span></span> <span data-ttu-id="97eb4-176">Desde esta página puede devolver toohello experimento (**ver instantánea** o **ver más reciente**) y ejecutar una prueba sencilla del servicio web de hello (vea **probar el servicio web de hello** a continuación).</span><span class="sxs-lookup"><span data-stu-id="97eb4-176">From this page you can return toohello experiment (**View snapshot** or **View latest**) and run a simple test of hello web service (see **Test hello web service** below).</span></span> <span data-ttu-id="97eb4-177">También hay información aquí para crear aplicaciones que pueden tener acceso a los servicio web de hello (más que en el paso siguiente de Hola de este tutorial).</span><span class="sxs-lookup"><span data-stu-id="97eb4-177">There is also information here for creating applications that can access hello web service (more on that in hello next step of this walkthrough).</span></span>

![Panel del servicio web][6]

<span data-ttu-id="97eb4-179">Puede configurar el servicio de hello haciendo clic en hello **configuración** ficha. Aquí puede modificar el nombre del servicio hello (es nombre de experimento Hola determinado de forma predeterminada) y escriba una descripción.</span><span class="sxs-lookup"><span data-stu-id="97eb4-179">You can configure hello service by clicking hello **CONFIGURATION** tab. Here you can modify hello service name (it's given hello experiment name by default) and give it a description.</span></span> <span data-ttu-id="97eb4-180">También se pueden proporcionar más etiquetas descriptivas Hola datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="97eb4-180">You can also give more friendly labels for hello input and output data.</span></span>  

![Configurar el servicio web de Hola][5]  

### <a name="deploy-as-a-new-web-service"></a><span data-ttu-id="97eb4-182">Implementación como servicio web nuevo</span><span class="sxs-lookup"><span data-stu-id="97eb4-182">Deploy as a New web service</span></span>

> [!NOTE] 
> <span data-ttu-id="97eb4-183">toodeploy un nuevo servicio web debe tener permisos suficientes en hello toowhich de suscripción que va a implementar Hola servicio web.</span><span class="sxs-lookup"><span data-stu-id="97eb4-183">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you are deploying hello web service.</span></span> <span data-ttu-id="97eb4-184">Para obtener más información, consulte [administrar un servicio web mediante el portal de servicios Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="97eb4-184">For more information, see [Manage a web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="97eb4-185">toodeploy un nuevo servicio web se deriva de nuestro experimento:</span><span class="sxs-lookup"><span data-stu-id="97eb4-185">toodeploy a New web service derived from our experiment:</span></span>

1. <span data-ttu-id="97eb4-186">Haga clic en **implementar el servicio de Web** por debajo de hello lienzo y seleccione **implementar [New] servicio Web**.</span><span class="sxs-lookup"><span data-stu-id="97eb4-186">Click **Deploy Web Service** below hello canvas and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="97eb4-187">Estudio de aprendizaje automático transfiere los servicios web de aprendizaje automático de Azure de toohello **implementar experimento** página.</span><span class="sxs-lookup"><span data-stu-id="97eb4-187">Machine Learning Studio transfers you toohello Azure Machine Learning web services **Deploy Experiment** page.</span></span>

2. <span data-ttu-id="97eb4-188">Escriba un nombre para el servicio web de Hola.</span><span class="sxs-lookup"><span data-stu-id="97eb4-188">Enter a name for hello web service.</span></span> 

3. <span data-ttu-id="97eb4-189">Para **Plan de precios**, puede seleccionar un plan de precios existente o seleccione "Crear nuevo" y conceda a Hola de nuevo plan de un nombre y una opción de plan mensual de hello select.</span><span class="sxs-lookup"><span data-stu-id="97eb4-189">For **Price Plan**, you can select an existing pricing plan, or select "Create new" and give hello new plan a name and select hello monthly plan option.</span></span> <span data-ttu-id="97eb4-190">plan de Hello niveles predeterminados toohello planes para la región predeterminada y el servicio web está implementado toothat región.</span><span class="sxs-lookup"><span data-stu-id="97eb4-190">hello plan tiers default toohello plans for your default region and your web service is deployed toothat region.</span></span>

4. <span data-ttu-id="97eb4-191">Haga clic en **Implementar**.</span><span class="sxs-lookup"><span data-stu-id="97eb4-191">Click **Deploy**.</span></span>

<span data-ttu-id="97eb4-192">Después de unos minutos, Hola **inicio rápido** se abre la página para el servicio web.</span><span class="sxs-lookup"><span data-stu-id="97eb4-192">After a few minutes, hello **Quickstart** page for your web service opens.</span></span>

<span data-ttu-id="97eb4-193">Puede configurar el servicio de hello haciendo clic en hello **configurar** ficha. Aquí puede modificar el servicio de hello título y escriba una descripción.</span><span class="sxs-lookup"><span data-stu-id="97eb4-193">You can configure hello service by clicking hello **Configure** tab. Here you can modify hello service title and give it a description.</span></span> 

<span data-ttu-id="97eb4-194">Hola tootest servicio web, haga clic en hello **prueba** pestaña (vea **probar el servicio web de hello** a continuación).</span><span class="sxs-lookup"><span data-stu-id="97eb4-194">tootest hello web service, click hello **Test** tab (see **Test hello web service** below).</span></span> <span data-ttu-id="97eb4-195">Para obtener información sobre cómo crear aplicaciones que pueden tener acceso a los servicio web de hello, haga clic en hello **Consume** pestaña (paso siguiente de hello en este tutorial entrarán en más detalle).</span><span class="sxs-lookup"><span data-stu-id="97eb4-195">For information on creating applications that can access hello web service, click hello **Consume** tab (hello next step in this walkthrough will go into more detail).</span></span>

> [!TIP]
> <span data-ttu-id="97eb4-196">Puede actualizar el servicio web de hello una vez que haya implementado.</span><span class="sxs-lookup"><span data-stu-id="97eb4-196">You can update hello web service after you've deployed it.</span></span> <span data-ttu-id="97eb4-197">Por ejemplo, si desea toochange el modelo, a continuación, puede editar el experimento de entrenamiento de Hola, ajustar los parámetros del modelo hello y haga clic en **implementar el servicio de Web**, seleccione **implementar servicio Web [estándar]** o  **Implementar el servicio Web [New]**.</span><span class="sxs-lookup"><span data-stu-id="97eb4-197">For example, if you want toochange your model, then you can edit hello training experiment, tweak hello model parameters, and click **Deploy Web Service**, selecting **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span> <span data-ttu-id="97eb4-198">Cuando implemente el experimento de Hola de nuevo, reemplaza el servicio web de hello, ahora con el modelo actualizado.</span><span class="sxs-lookup"><span data-stu-id="97eb4-198">When you deploy hello experiment again, it replaces hello web service, now using your updated model.</span></span>  
> 
> 

## <a name="test-hello-web-service"></a><span data-ttu-id="97eb4-199">Servicio web de Hola de prueba</span><span class="sxs-lookup"><span data-stu-id="97eb4-199">Test hello web service</span></span>

<span data-ttu-id="97eb4-200">Cuando se accede al servicio web de hello, datos del usuario de hello entra a través de hello **Web proporcionados por el servicio** módulo donde ha pasado toohello [puntuar modelo] [ score-model] módulo y puntuación.</span><span class="sxs-lookup"><span data-stu-id="97eb4-200">When hello web service is accessed, hello user's data enters through hello **Web service input** module where it's passed toohello [Score Model][score-model] module and scored.</span></span> <span data-ttu-id="97eb4-201">forma de Hello que hemos configurado experimento predictivo hello, modelo de hello espera datos en el mismo formato que el conjunto de datos de riesgo de crédito original de Hola de Hola.</span><span class="sxs-lookup"><span data-stu-id="97eb4-201">hello way we've set up hello predictive experiment, hello model expects data in hello same format as hello original credit risk dataset.</span></span>
<span data-ttu-id="97eb4-202">se devuelven resultados de Hola de toohello usuario de servicio web de Hola a través de hello **Web resultado del servicio** módulo.</span><span class="sxs-lookup"><span data-stu-id="97eb4-202">hello results are returned toohello user from hello web service through hello **Web service output** module.</span></span>

> [!TIP]
> <span data-ttu-id="97eb4-203">forma de Hello tenemos Hola predictivo experimento configurado, Hola todo da como resultado de hello [puntuar modelo] [ score-model] módulo se devuelven.</span><span class="sxs-lookup"><span data-stu-id="97eb4-203">hello way we have hello predictive experiment configured, hello entire results from hello [Score Model][score-model] module are returned.</span></span> <span data-ttu-id="97eb4-204">Esto incluye todos los datos de entrada de hello más valores de riesgo de crédito de Hola y Hola la puntuación de probabilidad.</span><span class="sxs-lookup"><span data-stu-id="97eb4-204">This includes all hello input data plus hello credit risk value and hello scoring probability.</span></span> <span data-ttu-id="97eb4-205">Pero puede devolver algo distinto si desea; por ejemplo, podría devolver solamente el valor de riesgo del crédito de Hola.</span><span class="sxs-lookup"><span data-stu-id="97eb4-205">But you can return something different if you want - for example, you could return just hello credit risk value.</span></span> <span data-ttu-id="97eb4-206">toodo, inserte un [proyectar columnas] [ project-columns] módulo entre [puntuar modelo] [ score-model] hello y **Web resultado del servicio** columnas tooeliminate que no desea Hola tooreturn de servicio web.</span><span class="sxs-lookup"><span data-stu-id="97eb4-206">toodo this, insert a [Project Columns][project-columns] module between [Score Model][score-model] and hello **Web service output** tooeliminate columns you don't want hello web service tooreturn.</span></span> 
> 
> 

<span data-ttu-id="97eb4-207">Puede probar un servidor web estándar de servicio en **estudio de aprendizaje automático** o en hello **servicios Web de Azure Machine Learning** portal.</span><span class="sxs-lookup"><span data-stu-id="97eb4-207">You can test a Classic web service either in **Machine Learning Studio** or in hello **Azure Machine Learning Web Services** portal.</span></span>
<span data-ttu-id="97eb4-208">Puede probar un nuevo servicio web solo en hello **servicios Web de aprendizaje de máquina** portal.</span><span class="sxs-lookup"><span data-stu-id="97eb4-208">You can test a New web service only in hello **Machine Learning Web Services** portal.</span></span>

> [!TIP]
> <span data-ttu-id="97eb4-209">Al realizar pruebas en el portal de servicios Web de Azure Machine Learning hello, puede tener portal Hola crear datos de ejemplo que puede usar tootest Hola respuesta de solicitud de servicio.</span><span class="sxs-lookup"><span data-stu-id="97eb4-209">When testing in hello Azure Machine Learning Web Services portal, you can have hello portal create sample data that you can use tootest hello Request-Response service.</span></span> <span data-ttu-id="97eb4-210">En hello **configurar** , seleccione "Sí" para **habilitado de datos de ejemplo?**.</span><span class="sxs-lookup"><span data-stu-id="97eb4-210">On hello **Configure** page, select "Yes" for **Sample Data Enabled?**.</span></span> <span data-ttu-id="97eb4-211">Cuando se abre la pestaña de hello solicitudes y respuestas de hello **prueba** página, portal de hello rellena los datos de ejemplo tomados de conjunto de datos de riesgo de crédito original de Hola.</span><span class="sxs-lookup"><span data-stu-id="97eb4-211">When you open hello Request-Response tab on hello **Test** page, hello portal fills in sample data taken from hello original credit risk dataset.</span></span>

### <a name="test-a-classic-web-service"></a><span data-ttu-id="97eb4-212">Prueba de un servicio web clásico</span><span class="sxs-lookup"><span data-stu-id="97eb4-212">Test a Classic web service</span></span>

<span data-ttu-id="97eb4-213">Puede probar un servicio web de clásico en estudio de aprendizaje automático o en el portal de servicios Web de aprendizaje de máquina de Hola.</span><span class="sxs-lookup"><span data-stu-id="97eb4-213">You can test a Classic web service in Machine Learning Studio or in hello Machine Learning Web Services portal.</span></span> 

#### <a name="test-in-machine-learning-studio"></a><span data-ttu-id="97eb4-214">Prueba en Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="97eb4-214">Test in Machine Learning Studio</span></span>

1. <span data-ttu-id="97eb4-215">En hello **panel** página de servicio web de hello, haga clic en hello **prueba** situado bajo **punto de conexión predeterminado**.</span><span class="sxs-lookup"><span data-stu-id="97eb4-215">On hello **DASHBOARD** page for hello web service, click hello **Test** button under **Default Endpoint**.</span></span> <span data-ttu-id="97eb4-216">Un cuadro de diálogo aparece y le pide de datos de entrada de hello para el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="97eb4-216">A dialog pops up and asks you for hello input data for hello service.</span></span> <span data-ttu-id="97eb4-217">Estos es Hola mismas columnas que aparecían en el conjunto de datos de riesgo de crédito original de Hola.</span><span class="sxs-lookup"><span data-stu-id="97eb4-217">These are hello same columns that appeared in hello original credit risk dataset.</span></span>  

2. <span data-ttu-id="97eb4-218">Escriba un conjunto de datos y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="97eb4-218">Enter a set of data and then click **OK**.</span></span> 

#### <a name="test-in-hello-machine-learning-web-services-portal"></a><span data-ttu-id="97eb4-219">Probar en el portal de servicios Web de aprendizaje de máquina de Hola</span><span class="sxs-lookup"><span data-stu-id="97eb4-219">Test in hello Machine Learning Web Services portal</span></span>

1. <span data-ttu-id="97eb4-220">En hello **panel** página de servicio web de hello, haga clic en hello **vista previa de prueba** vincular en **punto de conexión predeterminado**.</span><span class="sxs-lookup"><span data-stu-id="97eb4-220">On hello **DASHBOARD** page for hello web service, click hello **Test preview** link under **Default Endpoint**.</span></span> <span data-ttu-id="97eb4-221">página de prueba de Hello en el portal de servicios Web de Azure Machine Learning hello para el extremo del servicio web Hola se abre y le pide de datos de entrada de hello para el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="97eb4-221">hello test page in hello Azure Machine Learning Web Services portal for hello web service endpoint opens and asks you for hello input data for hello service.</span></span> <span data-ttu-id="97eb4-222">Estos es Hola mismas columnas que aparecían en el conjunto de datos de riesgo de crédito original de Hola.</span><span class="sxs-lookup"><span data-stu-id="97eb4-222">These are hello same columns that appeared in hello original credit risk dataset.</span></span>

2. <span data-ttu-id="97eb4-223">Haga clic en **Test Request-Response** (Probar solicitud-respuesta).</span><span class="sxs-lookup"><span data-stu-id="97eb4-223">Click **Test Request-Response**.</span></span> 

### <a name="test-a-new-web-service"></a><span data-ttu-id="97eb4-224">Prueba de un servicio web nuevo</span><span class="sxs-lookup"><span data-stu-id="97eb4-224">Test a New web service</span></span>

<span data-ttu-id="97eb4-225">Puede probar un nuevo servicio web solo en el portal de servicios Web de aprendizaje de máquina de Hola.</span><span class="sxs-lookup"><span data-stu-id="97eb4-225">You can test a New web service only in hello Machine Learning Web Services portal.</span></span>

1. <span data-ttu-id="97eb4-226">Hola [servicios Web de Azure Machine Learning](https://services.azureml.net/quickstart) portal, haga clic en **prueba** al principio de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="97eb4-226">In hello [Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal, click **Test** at hello top of hello page.</span></span> <span data-ttu-id="97eb4-227">Hola **prueba** se abre la página y puede escribir datos de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="97eb4-227">hello **Test** page opens and you can input data for hello service.</span></span> <span data-ttu-id="97eb4-228">campos de entrada de Hello mostrados corresponden columnas toohello que aparecían en el conjunto de datos de riesgo de crédito original de Hola.</span><span class="sxs-lookup"><span data-stu-id="97eb4-228">hello input fields displayed correspond toohello columns that appeared in hello original credit risk dataset.</span></span> 

2. <span data-ttu-id="97eb4-229">Escriba un conjunto de datos y, después, haga clic en **Test Request-Response**(Probar solicitud-respuesta).</span><span class="sxs-lookup"><span data-stu-id="97eb4-229">Enter a set of data and then click **Test Request-Response**.</span></span>

<span data-ttu-id="97eb4-230">Hola se muestran resultados de prueba de hello en lado derecho de Hola de página de hello en la columna de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="97eb4-230">hello results of hello test are displayed on hello right-hand side of hello page in hello output column.</span></span> 


## <a name="manage-hello-web-service"></a><span data-ttu-id="97eb4-231">Administrar el servicio web de Hola</span><span class="sxs-lookup"><span data-stu-id="97eb4-231">Manage hello web service</span></span>

### <a name="manage-a-classic-web-service-in-hello-azure-classic-portal"></a><span data-ttu-id="97eb4-232">Administrar un servicio web de clásico en hello portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="97eb4-232">Manage a Classic web service in hello Azure classic portal</span></span>

<span data-ttu-id="97eb4-233">Una vez haya implementado el servicio web de clásico, puede administrar de hello [portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="97eb4-233">Once you've deployed your Classic web service, you can manage it from hello [Azure classic portal](https://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="97eb4-234">Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="97eb4-234">Sign in toohello [Azure classic portal](https://manage.windowsazure.com)</span></span>
2. <span data-ttu-id="97eb4-235">En el panel de servicios de Microsoft Azure hello, haga clic en **aprendizaje automático**</span><span class="sxs-lookup"><span data-stu-id="97eb4-235">In hello Microsoft Azure services panel, click **MACHINE LEARNING**</span></span>
3. <span data-ttu-id="97eb4-236">Haga clic en el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="97eb4-236">Click your workspace</span></span>
4. <span data-ttu-id="97eb4-237">Haga clic en hello **servicios Web** ficha</span><span class="sxs-lookup"><span data-stu-id="97eb4-237">Click hello **Web services** tab</span></span>
5. <span data-ttu-id="97eb4-238">Haga clic en el servicio web de hello creamos</span><span class="sxs-lookup"><span data-stu-id="97eb4-238">Click hello web service we created</span></span>
6. <span data-ttu-id="97eb4-239">Haga clic en el punto de conexión de Hola "predeterminado"</span><span class="sxs-lookup"><span data-stu-id="97eb4-239">Click hello "default" endpoint</span></span>

<span data-ttu-id="97eb4-240">Desde aquí, puede hacer cosas como supervisar cómo realiza el servicio web de Hola y realizar ajustes de rendimiento cambiando el número de llamadas concurrentes Hola servicio puede controlar.</span><span class="sxs-lookup"><span data-stu-id="97eb4-240">From here, you can do things like monitor how hello web service is doing and make performance tweaks by changing how many concurrent calls hello service can handle.</span></span>

<span data-ttu-id="97eb4-241">Para obtener información, consulte:</span><span class="sxs-lookup"><span data-stu-id="97eb4-241">For more details, see:</span></span>

* [<span data-ttu-id="97eb4-242">Creación de extremos</span><span class="sxs-lookup"><span data-stu-id="97eb4-242">Creating Endpoints</span></span>](machine-learning-create-endpoint.md)
* [<span data-ttu-id="97eb4-243">Escalado del servicio web</span><span class="sxs-lookup"><span data-stu-id="97eb4-243">Scaling web service</span></span>](machine-learning-scaling-webservice.md)

### <a name="manage-a-classic-or-new-web-service-in-hello-azure-machine-learning-web-services-portal"></a><span data-ttu-id="97eb4-244">Administrar un nuevo servicio web en el portal de servicios Web de Azure Machine Learning Hola o clásico</span><span class="sxs-lookup"><span data-stu-id="97eb4-244">Manage a Classic or New web service in hello Azure Machine Learning Web Services portal</span></span>

<span data-ttu-id="97eb4-245">Una vez haya implementado el servicio web, ya sea clásico o nueva, se puede administrar desde hello [servicios Web de Microsoft Azure Machine Learning](https://services.azureml.net/quickstart) portal.</span><span class="sxs-lookup"><span data-stu-id="97eb4-245">Once you've deployed your web service, whether Classic or New, you can manage it from hello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal.</span></span>

<span data-ttu-id="97eb4-246">rendimiento de hello toomonitor del servicio web:</span><span class="sxs-lookup"><span data-stu-id="97eb4-246">toomonitor hello performance of your web service:</span></span>

1. <span data-ttu-id="97eb4-247">Inicie sesión en toohello [servicios Web de Microsoft Azure Machine Learning](https://services.azureml.net/quickstart) portal</span><span class="sxs-lookup"><span data-stu-id="97eb4-247">Sign in toohello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal</span></span>
2. <span data-ttu-id="97eb4-248">Haga clic en **Servicios web**.</span><span class="sxs-lookup"><span data-stu-id="97eb4-248">Click **Web services**</span></span>
3. <span data-ttu-id="97eb4-249">Haga clic en el servicio web.</span><span class="sxs-lookup"><span data-stu-id="97eb4-249">Click your web service</span></span>
4. <span data-ttu-id="97eb4-250">Haga clic en hello **panel**</span><span class="sxs-lookup"><span data-stu-id="97eb4-250">Click hello **Dashboard**</span></span>

- - -
<span data-ttu-id="97eb4-251">**Siguiente: [acceder al servicio web Hola](machine-learning-walkthrough-6-access-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="97eb4-251">**Next: [Access hello web service](machine-learning-walkthrough-6-access-web-service.md)**</span></span>

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
