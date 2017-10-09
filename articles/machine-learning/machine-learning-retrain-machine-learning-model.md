---
title: "un modelo de aprendizaje automático de aaaRetrain | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooretrain un modelo y actualización hello Web servicio toouse Hola recién entrenado en aprendizaje automático de Azure."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: d1cb6088-4f7c-4c32-94f2-f7523dad9059
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 342bb9954105339b4b634ff20968a64f4f9f750e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-machine-learning-model"></a><span data-ttu-id="e0c74-103">Reciclaje de un modelo de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e0c74-103">Retrain a Machine Learning Model</span></span>
<span data-ttu-id="e0c74-104">Como parte del proceso de Hola de puesta en marcha de modelos de aprendizaje automático en el aprendizaje automático de Azure, el modelo está entrenado y guardado.</span><span class="sxs-lookup"><span data-stu-id="e0c74-104">As part of hello process of operationalization of machine learning models in Azure Machine Learning, your model is trained and saved.</span></span> <span data-ttu-id="e0c74-105">También, a continuación, utilizarlo toocreate un servicio Web predicative.</span><span class="sxs-lookup"><span data-stu-id="e0c74-105">You then use it toocreate a predicative Web service.</span></span> <span data-ttu-id="e0c74-106">Hola servicio Web, a continuación, puede utilizarse en sitios web, paneles y aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="e0c74-106">hello Web service can then be consumed in web sites, dashboards, and mobile apps.</span></span> 

<span data-ttu-id="e0c74-107">Los modelos que crea mediante Aprendizaje automático no suelen ser estáticos.</span><span class="sxs-lookup"><span data-stu-id="e0c74-107">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="e0c74-108">Como los nuevos datos se convierte en disponibles o cuando consumidor Hola de hello API tiene su propio modelo de Hola de datos debe toobe volver a entrenar.</span><span class="sxs-lookup"><span data-stu-id="e0c74-108">As new data becomes available or when hello consumer of hello API has their own data hello model needs toobe retrained.</span></span> 

<span data-ttu-id="e0c74-109">El reentrenamiento puede producirse con frecuencia.</span><span class="sxs-lookup"><span data-stu-id="e0c74-109">Retraining may occur frequently.</span></span> <span data-ttu-id="e0c74-110">Con función de la API mediante programación de reciclaje de hello, mediante programación puede que volver a entrenar modelo de hello utilizando el servicio de Web de Hola de API de reciclaje y actualización Hola con hello recién entrenado.</span><span class="sxs-lookup"><span data-stu-id="e0c74-110">With hello Programmatic Retraining API feature, you can programmatically retrain hello model using hello Retraining APIs and update hello Web service with hello newly trained model.</span></span> 

<span data-ttu-id="e0c74-111">Este documento describe Hola reciclaje de proceso y muestra cómo toouse Hola reciclaje API.</span><span class="sxs-lookup"><span data-stu-id="e0c74-111">This document describes hello retraining process, and shows you how toouse hello Retraining APIs.</span></span>

## <a name="why-retrain-defining-hello-problem"></a><span data-ttu-id="e0c74-112">¿Por qué volver a entrenar: definir el problema de Hola</span><span class="sxs-lookup"><span data-stu-id="e0c74-112">Why retrain: defining hello problem</span></span>
<span data-ttu-id="e0c74-113">Como parte del aprendizaje automático de hello proceso de entrenamiento, se entrena un modelo utilizando un conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="e0c74-113">As part of hello machine learning training process, a model is trained using a set of data.</span></span> <span data-ttu-id="e0c74-114">Los modelos que crea mediante Aprendizaje automático no suelen ser estáticos.</span><span class="sxs-lookup"><span data-stu-id="e0c74-114">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="e0c74-115">Como los nuevos datos se convierte en disponibles o cuando consumidor Hola de hello API tiene su propio modelo de Hola de datos debe toobe volver a entrenar.</span><span class="sxs-lookup"><span data-stu-id="e0c74-115">As new data becomes available or when hello consumer of hello API has their own data hello model needs toobe retrained.</span></span>

<span data-ttu-id="e0c74-116">En estos casos, una API de programación proporciona una manera cómoda de tooallow se o hello consumidor de su toocreate API un cliente que puede, de forma puntual o regular, volver a entrenar modelo hello mediante sus propios datos.</span><span class="sxs-lookup"><span data-stu-id="e0c74-116">In these scenarios, a programmatic API provides a convenient way tooallow you or hello consumer of your APIs toocreate a client that can, on a one-time or regular basis, retrain hello model using their own data.</span></span> <span data-ttu-id="e0c74-117">A continuación, puede evaluar los resultados de Hola de reciclaje y actualizar hello Web servicio API toouse Hola recién entrenado.</span><span class="sxs-lookup"><span data-stu-id="e0c74-117">They can then evaluate hello results of retraining, and update hello Web service API toouse hello newly trained model.</span></span>

> [!NOTE]
> <span data-ttu-id="e0c74-118">Si tienes un experimento de aprendizaje existentes y el servicio Web nuevo, puede que desee toocheck out reciclaje una predicción Web existentes del servicio en lugar de la siguiente tutorial Hola mencionado en los pasos de la sección de Hola.</span><span class="sxs-lookup"><span data-stu-id="e0c74-118">If you have an existing Training Experiment and New Web service, you may want toocheck out Retrain an existing Predictive Web service instead of following hello walkthrough mentioned in hello following section.</span></span>
> 
> 

## <a name="end-to-end-workflow"></a><span data-ttu-id="e0c74-119">Flujo de trabajo de un extremo a otro</span><span class="sxs-lookup"><span data-stu-id="e0c74-119">End-to-end workflow</span></span>
<span data-ttu-id="e0c74-120">proceso de Hello implica Hola de los componentes siguientes: un experimento de entrenamiento y una predicción experimento publican como un servicio Web.</span><span class="sxs-lookup"><span data-stu-id="e0c74-120">hello process involves hello following components: A Training Experiment and a Predictive Experiment published as a Web service.</span></span> <span data-ttu-id="e0c74-121">tooenable reciclaje de un modelo entrenado, Hola experimento de entrenamiento debe publicarse como un servicio Web con salida de hello de un modelo entrenado.</span><span class="sxs-lookup"><span data-stu-id="e0c74-121">tooenable retraining of a trained model, hello Training Experiment must be published as a Web service with hello output of a trained model.</span></span> <span data-ttu-id="e0c74-122">Esto permite toohello modelo de acceso de API de reciclaje.</span><span class="sxs-lookup"><span data-stu-id="e0c74-122">This enables API access toohello model for retraining.</span></span> 

<span data-ttu-id="e0c74-123">Hola pasos aplica tooboth nuevo y clásico servicios Web:</span><span class="sxs-lookup"><span data-stu-id="e0c74-123">hello following steps apply tooboth New and Classic Web services:</span></span>

<span data-ttu-id="e0c74-124">Crear servicio Web de predicción inicial de hello:</span><span class="sxs-lookup"><span data-stu-id="e0c74-124">Create hello initial Predictive Web service:</span></span>

* <span data-ttu-id="e0c74-125">Crear un experimento de entrenamiento</span><span class="sxs-lookup"><span data-stu-id="e0c74-125">Create a training experiment</span></span>
* <span data-ttu-id="e0c74-126">Crear un experimento web predictivo</span><span class="sxs-lookup"><span data-stu-id="e0c74-126">Create a predictive web experiment</span></span>
* <span data-ttu-id="e0c74-127">Implementar un servicio web predictivo</span><span class="sxs-lookup"><span data-stu-id="e0c74-127">Deploy a predictive web service</span></span>

<span data-ttu-id="e0c74-128">Entrenar el modelo de servicio Web de hello:</span><span class="sxs-lookup"><span data-stu-id="e0c74-128">Retrain hello Web service:</span></span>

* <span data-ttu-id="e0c74-129">Actualizar tooallow de experimento de entrenamiento de reciclaje</span><span class="sxs-lookup"><span data-stu-id="e0c74-129">Update training experiment tooallow for retraining</span></span>
* <span data-ttu-id="e0c74-130">Implementar Hola reciclaje servicio web</span><span class="sxs-lookup"><span data-stu-id="e0c74-130">Deploy hello retraining web service</span></span>
* <span data-ttu-id="e0c74-131">Usar Hola servicio de ejecución por lotes código tooretrain Hola modelo</span><span class="sxs-lookup"><span data-stu-id="e0c74-131">Use hello Batch Execution Service code tooretrain hello model</span></span>

<span data-ttu-id="e0c74-132">Para ver un tutorial de hello pasos anteriores, consulte [aprendizaje automático de volver a entrenar modelos mediante programación](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="e0c74-132">For a walkthrough of hello preceding steps, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="e0c74-133">toodeploy un nuevo servicio web debe tener permisos suficientes en hello suscripción toowhich que implementar el servicio web de Hola.</span><span class="sxs-lookup"><span data-stu-id="e0c74-133">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="e0c74-134">Para obtener más información, vea [administrar un servicio Web mediante el portal de servicios Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="e0c74-134">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="e0c74-135">Si ha implementado un servicio web clásico:</span><span class="sxs-lookup"><span data-stu-id="e0c74-135">If you deployed a Classic Web Service:</span></span>

* <span data-ttu-id="e0c74-136">Crear un nuevo extremo de servicio Web de predicción Hola</span><span class="sxs-lookup"><span data-stu-id="e0c74-136">Create a new Endpoint on hello Predictive Web service</span></span>
* <span data-ttu-id="e0c74-137">Obtener la dirección URL de revisión de Hola y el código</span><span class="sxs-lookup"><span data-stu-id="e0c74-137">Get hello PATCH URL and code</span></span>
* <span data-ttu-id="e0c74-138">Use Hola URL PATCH toopoint Hola nuevo punto de conexión en hello volver a entrenar el modelo</span><span class="sxs-lookup"><span data-stu-id="e0c74-138">Use hello PATCH URL toopoint hello new Endpoint at hello retrained model</span></span> 

<span data-ttu-id="e0c74-139">Para ver un tutorial de hello pasos anteriores, consulte [entrenar el modelo de un servicio Web clásico](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="e0c74-139">For a walkthrough of hello preceding steps, see [Retrain a Classic Web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="e0c74-140">Si experimenta dificultades reciclaje de un servicio Web clásico, consulte [solución de problemas de hello reciclaje de un servicio Web clásico de Azure Machine Learning](machine-learning-troubleshooting-retraining-models.md).</span><span class="sxs-lookup"><span data-stu-id="e0c74-140">If you run into difficulties retraining a Classic Web service, see [Troubleshooting hello retraining of an Azure Machine Learning Classic Web service](machine-learning-troubleshooting-retraining-models.md).</span></span>

<span data-ttu-id="e0c74-141">Si ha implementado un nuevo servicio web:</span><span class="sxs-lookup"><span data-stu-id="e0c74-141">If you deployed a New Web service:</span></span>

* <span data-ttu-id="e0c74-142">Inicie sesión en tooyour cuenta de administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="e0c74-142">Sign in tooyour Azure Resource Manager account</span></span>
* <span data-ttu-id="e0c74-143">Obtener la definición de servicio Web de Hola</span><span class="sxs-lookup"><span data-stu-id="e0c74-143">Get hello Web service definition</span></span>
* <span data-ttu-id="e0c74-144">Exportar la definición del servicio Web de Hola como JSON</span><span class="sxs-lookup"><span data-stu-id="e0c74-144">Export hello Web Service Definition as JSON</span></span>
* <span data-ttu-id="e0c74-145">Actualizar Hola referencia toohello `ilearner` blob Hola JSON</span><span class="sxs-lookup"><span data-stu-id="e0c74-145">Update hello reference toohello `ilearner` blob in hello JSON</span></span>
* <span data-ttu-id="e0c74-146">Importar Hola JSON en una definición de servicio Web</span><span class="sxs-lookup"><span data-stu-id="e0c74-146">Import hello JSON into a Web Service Definition</span></span>
* <span data-ttu-id="e0c74-147">Actualizar el servicio Web de hello con la nueva definición del servicio Web</span><span class="sxs-lookup"><span data-stu-id="e0c74-147">Update hello Web service with new Web Service Definition</span></span>

<span data-ttu-id="e0c74-148">Para ver un tutorial de hello pasos anteriores, consulte [entrenar el modelo de un servicio Web nuevo mediante cmdlets de PowerShell de administración de aprendizaje de máquina de hello](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e0c74-148">For a walkthrough of hello preceding steps, see [Retrain a New Web service using hello Machine Learning Management PowerShell cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="e0c74-149">proceso de Hello para la configuración de reciclaje para un servicio Web clásico implica Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e0c74-149">hello process for setting up retraining for a Classic Web service involves hello following steps:</span></span>

![Descripción del proceso de reentrenamiento][1]

<span data-ttu-id="e0c74-151">proceso de Hello para la configuración de reciclaje para un servicio Web nuevo implica Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e0c74-151">hello process for setting up retraining for a New Web service involves hello following steps:</span></span>

![Descripción del proceso de reentrenamiento][7]

## <a name="other-resources"></a><span data-ttu-id="e0c74-153">Otros recursos</span><span class="sxs-lookup"><span data-stu-id="e0c74-153">Other Resources</span></span>
* [<span data-ttu-id="e0c74-154">Reciclaje y actualización de modelos de Azure Machine Learning con Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="e0c74-154">Retraining and Updating Azure Machine Learning models with Azure Data Factory</span></span>](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/)
* [<span data-ttu-id="e0c74-155">Creación de varios modelos de Machine Learning y puntos de conexión de servicio web a partir de un experimento mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0c74-155">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>](machine-learning-create-models-and-endpoints-with-powershell.md)
* <span data-ttu-id="e0c74-156">Hola [AML reciclaje modelos utilizando API](https://www.youtube.com/watch?v=wwjglA8xllg) vídeo muestra cómo crean modelos de aprendizaje automático de tooretrain aprendizaje automático de Azure con hello las API de reciclaje y PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0c74-156">hello [AML Retraining Models Using APIs](https://www.youtube.com/watch?v=wwjglA8xllg) video shows you how tooretrain Machine Learning models created in Azure Machine Learning using hello Retraining APIs and PowerShell.</span></span>

<!--image links-->
[1]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE01.png
[7]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE07.png

