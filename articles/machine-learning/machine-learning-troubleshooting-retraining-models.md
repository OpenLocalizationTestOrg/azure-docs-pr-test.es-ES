---
title: "Solución de problemas de reciclaje de un servicio web clásico Azure Machine Learning | Microsoft Docs"
description: Identifique y corrija los problemas comunes que se encuentran al volver a entrenar el modelo para un servicio web Azure Machine Learning.
services: machine-learning
documentationcenter: 
author: VDonGlover
manager: raymondl
editor: 
ms.assetid: 75cac53c-185c-437d-863a-5d66d871921e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: fc36499ebff88c86635228ff899c85e9166aabed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-the-retraining-of-an-azure-machine-learning-classic-web-service"></a><span data-ttu-id="1b078-103">Solución de problemas de reentrenamiento de un servicio web clásico de Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1b078-103">Troubleshooting the retraining of an Azure Machine Learning Classic Web service</span></span>
## <a name="retraining-overview"></a><span data-ttu-id="1b078-104">Información general sobre reentrenamiento</span><span class="sxs-lookup"><span data-stu-id="1b078-104">Retraining overview</span></span>
<span data-ttu-id="1b078-105">Cuando se implementa un experimento predictivo, tal como servicio web de puntuación, es un modelo estático.</span><span class="sxs-lookup"><span data-stu-id="1b078-105">When you deploy a predictive experiment as a scoring web service it is a static model.</span></span> <span data-ttu-id="1b078-106">Cuando hay nuevos datos disponibles o cuando el consumidor de la API tiene sus propios datos, el modelo debe volver a entrenarse.</span><span class="sxs-lookup"><span data-stu-id="1b078-106">As new data becomes available or when the consumer of the API has their own data, the model needs to be retrained.</span></span> 

<span data-ttu-id="1b078-107">Para ver un tutorial completo del proceso de reentrenamiento de un servicio web clásico, consulte [Reentrenamiento mediante programación de modelos de Machine Learning](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="1b078-107">For a complete walkthrough of the retraining process of a Classic Web service, see [Retrain Machine Learning Models Programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

## <a name="retraining-process"></a><span data-ttu-id="1b078-108">Proceso de reentrenamiento</span><span class="sxs-lookup"><span data-stu-id="1b078-108">Retraining process</span></span>
<span data-ttu-id="1b078-109">Cuando tiene que volver a entrenar el servicio web, debe agregar algunos elementos adicionales:</span><span class="sxs-lookup"><span data-stu-id="1b078-109">When you need to retrain the Web service, you must add some additional pieces:</span></span>

* <span data-ttu-id="1b078-110">Un servicio web implementado desde el experimento de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="1b078-110">A Web service deployed from the Training Experiment.</span></span> <span data-ttu-id="1b078-111">El experimento debe tener un módulo de **salida de servicio web** conectado a la salida del módulo **Entrenar modelo**.</span><span class="sxs-lookup"><span data-stu-id="1b078-111">The experiment must have a **Web Service Output** module attached to the output of the **Train Model** module.</span></span>  
  
    ![Asocie la salida del servicio web al modelo entrenado.][image1]
* <span data-ttu-id="1b078-113">Un nuevo punto de conexión agregado a su servicio web de puntuación.</span><span class="sxs-lookup"><span data-stu-id="1b078-113">A new endpoint added to your scoring Web service.</span></span>  <span data-ttu-id="1b078-114">Puede agregar el punto de conexión mediante programación usando el código de ejemplo al que se hace referencia en el tema Volver a entrenar modelos de aprendizaje automático mediante programación, o mediante el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="1b078-114">You can add the endpoint programmatically using the sample code referenced in the Retrain Machine Learning models programmatically topic or through the Azure classic portal.</span></span>

<span data-ttu-id="1b078-115">Después, para entrenar el modelo puede usar el código C# de ejemplo de la página de Ayuda de la API del servicio web de aprendizaje.</span><span class="sxs-lookup"><span data-stu-id="1b078-115">You can then use the sample C# code from the Training Web Service's API help page to retrain model.</span></span> <span data-ttu-id="1b078-116">Cuando haya evaluado los resultados y esté satisfecho con ellos, actualice el servicio web de puntuación con el modelo entrenado para que use el nuevo punto de conexión agregado.</span><span class="sxs-lookup"><span data-stu-id="1b078-116">Once you have evaluated the results and are satisfied with them, you update the trained model scoring web service using the new endpoint that you added.</span></span>

<span data-ttu-id="1b078-117">Con todos los elementos en su lugar, estos son los pasos principales que debe seguir para reentrenar el modelo:</span><span class="sxs-lookup"><span data-stu-id="1b078-117">With all the pieces in place, the major steps you must take to retrain the model are as follows:</span></span>

1. <span data-ttu-id="1b078-118">Llame al servicio web de entrenamiento: la llamada se realiza al servicio de ejecución por lotes (BES, Batch Execution Service), no al servicio de solicitud-respuesta (RRS, Request-Response Service).</span><span class="sxs-lookup"><span data-stu-id="1b078-118">Call the Training Web Service:  The call is to the Batch Execution Service (BES), not the Request Response Service (RRS).</span></span> <span data-ttu-id="1b078-119">Puede usar el código C# de ejemplo en la página de ayuda de la API para realizar la llamada.</span><span class="sxs-lookup"><span data-stu-id="1b078-119">You can use the sample C# code on the API help page to make the call.</span></span> 
2. <span data-ttu-id="1b078-120">Busque los valores de *BaseLocation*, *RelativeLocation* y *SasBlobToken*: estos valores se devuelven en el resultado de la llamada al servicio web de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="1b078-120">Find the values for the *BaseLocation*, *RelativeLocation*, and *SasBlobToken*: These values are returned in the output from your call to the Training Web Service.</span></span> 
   <span data-ttu-id="1b078-121">![muestra de la salida de la ejemplo de reentrenamiento y los valores de BaseLocation, RelativeLocation y SasBlobToken.][image6]</span><span class="sxs-lookup"><span data-stu-id="1b078-121">![showing the output of the retraining sample and the BaseLocation, RelativeLocation, and  SasBlobToken values.][image6]</span></span>
3. <span data-ttu-id="1b078-122">Actualice el punto de conexión agregado en el servicio web de puntuación con el nuevo modelo entrenado: use el código de ejemplo proporcionado en el tema Volver a entrenar modelos de aprendizaje automático mediante programación para actualizar el nuevo punto de conexión que agregó al modelo de puntuación con el modelo recién entrenado en el servicio web de aprendizaje.</span><span class="sxs-lookup"><span data-stu-id="1b078-122">Update the added endpoint from the scoring web service with the new trained model: Using the sample code provided in the Retrain Machine Learning models programmatically, update the new endpoint you added to the scoring model with the newly trained model from the Training Web Service.</span></span>

## <a name="common-obstacles"></a><span data-ttu-id="1b078-123">Obstáculos más comunes</span><span class="sxs-lookup"><span data-stu-id="1b078-123">Common obstacles</span></span>
### <a name="check-to-see-if-you-have-the-correct-patch-url"></a><span data-ttu-id="1b078-124">Compruebe si el valor de PATCH URL es el correcto</span><span class="sxs-lookup"><span data-stu-id="1b078-124">Check to see if you have the correct PATCH URL</span></span>
<span data-ttu-id="1b078-125">El valor de PATCH URL que use deberá ser el único asociado con el nuevo punto de conexión de puntuación que agregó al servicio web de puntuación.</span><span class="sxs-lookup"><span data-stu-id="1b078-125">The PATCH URL you are using must be the one associated with the new scoring endpoint you added to the scoring Web service.</span></span> <span data-ttu-id="1b078-126">Hay varias maneras de obtener el valor de PATCH URL:</span><span class="sxs-lookup"><span data-stu-id="1b078-126">There are a number of ways to obtain the PATCH URL:</span></span>

<span data-ttu-id="1b078-127">**Opción 1: De forma programada**</span><span class="sxs-lookup"><span data-stu-id="1b078-127">**Option 1: Programatically**</span></span>

<span data-ttu-id="1b078-128">Para obtener valor de PATCH URL correcto:</span><span class="sxs-lookup"><span data-stu-id="1b078-128">To get the correct PATCH URL:</span></span>

1. <span data-ttu-id="1b078-129">Ejecute el código de ejemplo [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) .</span><span class="sxs-lookup"><span data-stu-id="1b078-129">Run the [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>
2. <span data-ttu-id="1b078-130">En la salida de AddEndpoint, busque el valor *HelpLocation* y copie la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="1b078-130">From the output of AddEndpoint, find the *HelpLocation* value and copy the URL.</span></span>
   
   ![HelpLocation en la salida del ejemplo de addEndpoint.][image2]
3. <span data-ttu-id="1b078-132">Pegue la dirección URL en un explorador para ir a una página que ofrece vínculos de ayuda para el servicio web.</span><span class="sxs-lookup"><span data-stu-id="1b078-132">Paste the URL into a browser to navigate to a page that provides help links for the Web service.</span></span>
4. <span data-ttu-id="1b078-133">Haga clic en el vínculo **Actualizar recurso** para abrir la página de ayuda sobre aplicación de revisiones.</span><span class="sxs-lookup"><span data-stu-id="1b078-133">Click the **Update Resource** link to open the patch help page.</span></span>

<span data-ttu-id="1b078-134">**Opción 2: Usar el Portal de Azure clásico**</span><span class="sxs-lookup"><span data-stu-id="1b078-134">**Option 2: Use the Azure classic portal**</span></span>

1. <span data-ttu-id="1b078-135">Inicie sesión en el [Portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="1b078-135">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="1b078-136">Vaya a la pestaña Aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="1b078-136">Open the Machine Learning tab.</span></span> 
   <span data-ttu-id="1b078-137">![Pestaña Machine Learning.][image4]</span><span class="sxs-lookup"><span data-stu-id="1b078-137">![Machine leaning tab.][image4]</span></span>
3. <span data-ttu-id="1b078-138">Haga clic en el nombre del área de trabajo y, luego, en **Servicios web**.</span><span class="sxs-lookup"><span data-stu-id="1b078-138">Click your workspace name, then **Web Services**.</span></span>
4. <span data-ttu-id="1b078-139">Haga clic en el servicio web de puntuación con el que está trabajando.</span><span class="sxs-lookup"><span data-stu-id="1b078-139">Click the scoring Web service you are working with.</span></span> <span data-ttu-id="1b078-140">(Si no modificó el nombre predeterminado del servicio web, terminará en [Scoring Exp.]).</span><span class="sxs-lookup"><span data-stu-id="1b078-140">(If you did not modify the default name of the web service, it will end in [Scoring Exp.].)</span></span>
5. <span data-ttu-id="1b078-141">Haga clic en **Agregar extremo**.</span><span class="sxs-lookup"><span data-stu-id="1b078-141">Click **Add Endpoint**.</span></span>
6. <span data-ttu-id="1b078-142">Una vez agregado el punto de conexión, haga clic en su nombre.</span><span class="sxs-lookup"><span data-stu-id="1b078-142">After the endpoint is added, click the endpoint name.</span></span> <span data-ttu-id="1b078-143">Después, haga clic en **Actualizar recurso** para abrir la página de ayuda sobre aplicación de revisiones.</span><span class="sxs-lookup"><span data-stu-id="1b078-143">Then click **Update Resource** to open the patching help page.</span></span>

> [!NOTE]
> <span data-ttu-id="1b078-144">Si ha agregado el punto de conexión al servicio web de entrenamiento en lugar de al predictivo, verá el siguiente mensaje de error al hacer clic en el vínculo **Actualizar recurso**: Lo sentimos, pero esta característica no se admite ni está disponible en este contexto.</span><span class="sxs-lookup"><span data-stu-id="1b078-144">If you have added the endpoint to the Training Web Service instead of the Predictive Web Service, you will receive the following error when you click the **Update Resource** link: Sorry, but this feature is not supported or available in this context.</span></span> <span data-ttu-id="1b078-145">Este servicio web no tiene ningún recurso actualizable.</span><span class="sxs-lookup"><span data-stu-id="1b078-145">This Web Service has no updatable resources.</span></span> <span data-ttu-id="1b078-146">Sentimos las molestias. Estamos trabajando en mejorar este flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="1b078-146">We apologize for the inconvenience and are working on improving this workflow.</span></span>
> 
> 

![Panel del nuevo punto de conexión.][image3]

<span data-ttu-id="1b078-148">La página de ayuda sobre PATCH contiene el valor de PATCH URL que debe usar y proporciona un código de ejemplo que puede usar para realizar la llamada.</span><span class="sxs-lookup"><span data-stu-id="1b078-148">The PATCH help page contains the PATCH URL you must use and provides sample code you can use to call it.</span></span>

![PATCH URL.][image5]

### <a name="check-to-see-that-you-are-updating-the-correct-scoring-endpoint"></a><span data-ttu-id="1b078-150">Compruebe que está actualizando el punto de conexión de puntuación correcto.</span><span class="sxs-lookup"><span data-stu-id="1b078-150">Check to see that you are updating the correct scoring endpoint</span></span>
* <span data-ttu-id="1b078-151">No aplique revisiones al servicio web de entrenamiento: la operación de revisión debe realizarse en el servicio web de puntuación.</span><span class="sxs-lookup"><span data-stu-id="1b078-151">Do not patch the Training Web Service: The patch operation must be performed on the scoring Web service.</span></span>
* <span data-ttu-id="1b078-152">No aplique revisiones al punto de conexión predeterminado en el servicio web: la operación de revisión debe realizarse en el nuevo punto de conexión del servicio web de puntuación que agregó.</span><span class="sxs-lookup"><span data-stu-id="1b078-152">Do not patch the default endpoint on Web service: The patch operation must be performed on the new scoring Web service endpoint that you added.</span></span>

<span data-ttu-id="1b078-153">Para comprobar en qué servicio web está el punto de conexión, visite el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="1b078-153">You can verify which Web service the endpoint is on by visiting the Azure classic portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="1b078-154">Asegúrese de agregar el punto de conexión al servicio web predictivo y no al de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="1b078-154">Be sure you are adding the endpoint to the Predictive Web Service, not the Training Web Service.</span></span> <span data-ttu-id="1b078-155">Si ha implementado correctamente un servicio web predictivo y otro de formación, debería ver dos servicios web independientes.</span><span class="sxs-lookup"><span data-stu-id="1b078-155">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate Web services listed.</span></span> <span data-ttu-id="1b078-156">El servicio web predictivo debe terminar con "[predictive exp.]".</span><span class="sxs-lookup"><span data-stu-id="1b078-156">The Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

1. <span data-ttu-id="1b078-157">Inicie sesión en el [Portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="1b078-157">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="1b078-158">Vaya a la pestaña Aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="1b078-158">Open the Machine Learning tab.</span></span> 
   <span data-ttu-id="1b078-159">![Interfaz de usuario del área de trabajo de Machine Learning.][image4]</span><span class="sxs-lookup"><span data-stu-id="1b078-159">![Machine learning workspace UI.][image4]</span></span>
3. <span data-ttu-id="1b078-160">Seleccione su área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="1b078-160">Select your workspace.</span></span>
4. <span data-ttu-id="1b078-161">Haga clic en **Servicios web**.</span><span class="sxs-lookup"><span data-stu-id="1b078-161">Click **Web Services**.</span></span>
5. <span data-ttu-id="1b078-162">Seleccione su servicio web predictivo.</span><span class="sxs-lookup"><span data-stu-id="1b078-162">Select your Predictive Web Service.</span></span>
6. <span data-ttu-id="1b078-163">Compruebe que el nuevo punto de conexión se agregó al servicio web.</span><span class="sxs-lookup"><span data-stu-id="1b078-163">Verify that your new endpoint was added to the Web service.</span></span>

### <a name="check-the-workspace-that-your-web-service-is-in-to-ensure-it-is-in-the-correct-region"></a><span data-ttu-id="1b078-164">Compruebe el área de trabajo donde está en el servicio web para asegurarse de que está en la región correcta.</span><span class="sxs-lookup"><span data-stu-id="1b078-164">Check the workspace that your web service is in to ensure it is in the correct region</span></span>
1. <span data-ttu-id="1b078-165">Inicie sesión en el [Portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="1b078-165">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="1b078-166">Seleccione Aprendizaje automático en el menú.</span><span class="sxs-lookup"><span data-stu-id="1b078-166">Select Machine Learning from the menu.</span></span>
   <span data-ttu-id="1b078-167">![Interfaz de usuario de la región de Machine Learning.][image4]</span><span class="sxs-lookup"><span data-stu-id="1b078-167">![Machine learning region UI.][image4]</span></span>
3. <span data-ttu-id="1b078-168">Compruebe la ubicación del área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="1b078-168">Verify the location of your workspace.</span></span>

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
