---
title: "servicio web de aaaTroubleshoot reciclaje un clásico de aprendizaje de máquina de Azure | Documentos de Microsoft"
description: "Identifique y corrija comunes detectó problemas cuando se reciclaje modelo Hola para un servicio Web de aprendizaje de máquina de Azure."
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
ms.openlocfilehash: 2b6a78eaba161877106dccdc23437b5e454fca7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-retraining-of-an-azure-machine-learning-classic-web-service"></a><span data-ttu-id="ba4d2-103">Solución de problemas de hello reciclaje de un servicio Web clásico de aprendizaje de máquina de Azure</span><span class="sxs-lookup"><span data-stu-id="ba4d2-103">Troubleshooting hello retraining of an Azure Machine Learning Classic Web service</span></span>
## <a name="retraining-overview"></a><span data-ttu-id="ba4d2-104">Información general sobre reentrenamiento</span><span class="sxs-lookup"><span data-stu-id="ba4d2-104">Retraining overview</span></span>
<span data-ttu-id="ba4d2-105">Cuando se implementa un experimento predictivo, tal como servicio web de puntuación, es un modelo estático.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-105">When you deploy a predictive experiment as a scoring web service it is a static model.</span></span> <span data-ttu-id="ba4d2-106">Como los nuevos datos se convierte en disponibles o al consumidor de Hola de hello API tiene sus propios datos, modelo de hello necesita toobe volver a entrenar.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-106">As new data becomes available or when hello consumer of hello API has their own data, hello model needs toobe retrained.</span></span> 

<span data-ttu-id="ba4d2-107">Para obtener un tutorial completo de hello reciclaje de procesos de un servicio Web clásico, consulte [volver a entrenar máquina aprendizaje modelos mediante programación](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="ba4d2-107">For a complete walkthrough of hello retraining process of a Classic Web service, see [Retrain Machine Learning Models Programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

## <a name="retraining-process"></a><span data-ttu-id="ba4d2-108">Proceso de reentrenamiento</span><span class="sxs-lookup"><span data-stu-id="ba4d2-108">Retraining process</span></span>
<span data-ttu-id="ba4d2-109">Cuando necesite tooretrain Hola servicio Web, debe agregar algunos elementos adicionales:</span><span class="sxs-lookup"><span data-stu-id="ba4d2-109">When you need tooretrain hello Web service, you must add some additional pieces:</span></span>

* <span data-ttu-id="ba4d2-110">Un servicio Web que se implementan a partir de hello experimento de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-110">A Web service deployed from hello Training Experiment.</span></span> <span data-ttu-id="ba4d2-111">debe tener el experimento de Hello un **resultado del servicio Web** módulo adjunta toohello salida de hello **entrenar modelo** módulo.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-111">hello experiment must have a **Web Service Output** module attached toohello output of hello **Train Model** module.</span></span>  
  
    ![Adjuntar Hola salida toohello entrenar modelo para servicios web.][image1]
* <span data-ttu-id="ba4d2-113">Un nuevo extremo agregado tooyour la puntuación del servicio Web.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-113">A new endpoint added tooyour scoring Web service.</span></span>  <span data-ttu-id="ba4d2-114">Puede agregar punto de conexión de hello mediante programación utilizando el código de ejemplo de Hola hace referencia en hello aprendizaje automático de volver a entrenar modelos mediante programación tema o a través de hello portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-114">You can add hello endpoint programmatically using hello sample code referenced in hello Retrain Machine Learning models programmatically topic or through hello Azure classic portal.</span></span>

<span data-ttu-id="ba4d2-115">A continuación, puede usar Hola ejemplo C# código a partir API ayuda página tooretrain modelo del servicio Web de hello entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-115">You can then use hello sample C# code from hello Training Web Service's API help page tooretrain model.</span></span> <span data-ttu-id="ba4d2-116">Una vez que se evalúa los resultados de Hola y esté satisfecho con ellas, actualizar modelo entrenado Hola la puntuación del servicio web mediante Hola nuevo punto de conexión que agregó.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-116">Once you have evaluated hello results and are satisfied with them, you update hello trained model scoring web service using hello new endpoint that you added.</span></span>

<span data-ttu-id="ba4d2-117">Con todas las piezas de hello en su lugar, pasos principales de Hola que debe seguir modelo de hello tooretrain son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="ba4d2-117">With all hello pieces in place, hello major steps you must take tooretrain hello model are as follows:</span></span>

1. <span data-ttu-id="ba4d2-118">Llame al servicio Web de aprendizaje de hello: llamada hello es toohello servicio de ejecución de lotes (BES), no Hola servicio de respuesta de solicitud (RR).</span><span class="sxs-lookup"><span data-stu-id="ba4d2-118">Call hello Training Web Service:  hello call is toohello Batch Execution Service (BES), not hello Request Response Service (RRS).</span></span> <span data-ttu-id="ba4d2-119">Puede usar código C# de ejemplo Hola en llamada de API de hello ayuda página toomake Hola.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-119">You can use hello sample C# code on hello API help page toomake hello call.</span></span> 
2. <span data-ttu-id="ba4d2-120">Buscar valores de hello para hello *BaseLocation*, *RelativeLocation*, y *SasBlobToken*: estos valores se devuelven en la salida de hello desde la Web de aprendizaje de llamada toohello Servicio.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-120">Find hello values for hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken*: These values are returned in hello output from your call toohello Training Web Service.</span></span> 
   <span data-ttu-id="ba4d2-121">![Mostrar la salida de hello de hello reciclaje hello y muestra los valores de BaseLocation, RelativeLocation y SasBlobToken.][image6]</span><span class="sxs-lookup"><span data-stu-id="ba4d2-121">![showing hello output of hello retraining sample and hello BaseLocation, RelativeLocation, and  SasBlobToken values.][image6]</span></span>
3. <span data-ttu-id="ba4d2-122">Hola de actualización agrega punto de conexión de Hola la puntuación del servicio web con hello nuevo modelo entrenado: usar código de ejemplo de Hola Hola aprendizaje automático de volver a entrenar modelos mediante programación, actualizar nuevo extremo de hello agregado toohello puntuar modelo con hello recientemente modelo entrenado de hello servicio Web de aprendizaje.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-122">Update hello added endpoint from hello scoring web service with hello new trained model: Using hello sample code provided in hello Retrain Machine Learning models programmatically, update hello new endpoint you added toohello scoring model with hello newly trained model from hello Training Web Service.</span></span>

## <a name="common-obstacles"></a><span data-ttu-id="ba4d2-123">Obstáculos más comunes</span><span class="sxs-lookup"><span data-stu-id="ba4d2-123">Common obstacles</span></span>
### <a name="check-toosee-if-you-have-hello-correct-patch-url"></a><span data-ttu-id="ba4d2-124">Consulte toosee si tiene Hola corregir la dirección URL de revisión</span><span class="sxs-lookup"><span data-stu-id="ba4d2-124">Check toosee if you have hello correct PATCH URL</span></span>
<span data-ttu-id="ba4d2-125">Hola URL PATCH utilizas debe ser Hola asociado Hola nuevo extremo de puntuación que agregó toohello la puntuación del servicio Web.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-125">hello PATCH URL you are using must be hello one associated with hello new scoring endpoint you added toohello scoring Web service.</span></span> <span data-ttu-id="ba4d2-126">Hay una serie de formas tooobtain Hola PATCH URL:</span><span class="sxs-lookup"><span data-stu-id="ba4d2-126">There are a number of ways tooobtain hello PATCH URL:</span></span>

<span data-ttu-id="ba4d2-127">**Opción 1: De forma programada**</span><span class="sxs-lookup"><span data-stu-id="ba4d2-127">**Option 1: Programatically**</span></span>

<span data-ttu-id="ba4d2-128">Hola tooget corríjala PATCH:</span><span class="sxs-lookup"><span data-stu-id="ba4d2-128">tooget hello correct PATCH URL:</span></span>

1. <span data-ttu-id="ba4d2-129">Ejecute hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-129">Run hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>
2. <span data-ttu-id="ba4d2-130">En la salida de hello de AddEndpoint, observa hello *HelpLocation* valor y copie la dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-130">From hello output of AddEndpoint, find hello *HelpLocation* value and copy hello URL.</span></span>
   
   ![HelpLocation en la salida de hello de ejemplo de Hola a addEndpoint.][image2]
3. <span data-ttu-id="ba4d2-132">Pegue la dirección de URL de hello en una página de tooa de toonavigate de explorador que proporciona los vínculos de ayuda para el servicio Web de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-132">Paste hello URL into a browser toonavigate tooa page that provides help links for hello Web service.</span></span>
4. <span data-ttu-id="ba4d2-133">Haga clic en hello **recurso de actualización** página de Ayuda de revisión de vínculo tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-133">Click hello **Update Resource** link tooopen hello patch help page.</span></span>

<span data-ttu-id="ba4d2-134">**Opción 2: Usar hello portal de Azure clásico**</span><span class="sxs-lookup"><span data-stu-id="ba4d2-134">**Option 2: Use hello Azure classic portal**</span></span>

1. <span data-ttu-id="ba4d2-135">Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="ba4d2-135">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="ba4d2-136">Pestaña de aprendizaje automático de hello abierto. ![Pestaña Machine Learning.][image4]</span><span class="sxs-lookup"><span data-stu-id="ba4d2-136">Open hello Machine Learning tab. ![Machine leaning tab.][image4]</span></span>
3. <span data-ttu-id="ba4d2-137">Haga clic en el nombre del área de trabajo y, luego, en **Servicios web**.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-137">Click your workspace name, then **Web Services**.</span></span>
4. <span data-ttu-id="ba4d2-138">Haga clic en hello la puntuación del servicio Web que está trabajando.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-138">Click hello scoring Web service you are working with.</span></span> <span data-ttu-id="ba4d2-139">(Si no ha modificado el nombre predeterminado de hello del servicio web de hello, termina en [puntuación Exp].)</span><span class="sxs-lookup"><span data-stu-id="ba4d2-139">(If you did not modify hello default name of hello web service, it will end in [Scoring Exp.].)</span></span>
5. <span data-ttu-id="ba4d2-140">Haga clic en **Agregar extremo**.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-140">Click **Add Endpoint**.</span></span>
6. <span data-ttu-id="ba4d2-141">Después de agrega el punto de conexión de hello, haga clic en el nombre del extremo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-141">After hello endpoint is added, click hello endpoint name.</span></span> <span data-ttu-id="ba4d2-142">A continuación, haga clic en **recurso de actualización** tooopen Hola página de Ayuda de aplicación de revisiones.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-142">Then click **Update Resource** tooopen hello patching help page.</span></span>

> [!NOTE]
> <span data-ttu-id="ba4d2-143">Si ha agregado Hola extremo toohello servicio Web de aprendizaje en lugar de hello predictivo servicio Web, recibirá el mensaje Hola tras error al hacer clic en hello **recurso de actualización** vínculo: lo sentimos, pero no se admite esta característica o está disponible en este contexto.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-143">If you have added hello endpoint toohello Training Web Service instead of hello Predictive Web Service, you will receive hello following error when you click hello **Update Resource** link: Sorry, but this feature is not supported or available in this context.</span></span> <span data-ttu-id="ba4d2-144">Este servicio web no tiene ningún recurso actualizable.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-144">This Web Service has no updatable resources.</span></span> <span data-ttu-id="ba4d2-145">Nos disculpamos molestias hello y está trabajando en la mejora de este flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-145">We apologize for hello inconvenience and are working on improving this workflow.</span></span>
> 
> 

![Panel del nuevo punto de conexión.][image3]

<span data-ttu-id="ba4d2-147">página de Ayuda de revisión de Hello contiene Hola dirección URL de aplicar la revisión que se debe usar y proporciona código de ejemplo que puede usar toocall lo.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-147">hello PATCH help page contains hello PATCH URL you must use and provides sample code you can use toocall it.</span></span>

![PATCH URL.][image5]

### <a name="check-toosee-that-you-are-updating-hello-correct-scoring-endpoint"></a><span data-ttu-id="ba4d2-149">Toosee de comprobación que se está actualizando el extremo de puntuación correcta Hola</span><span class="sxs-lookup"><span data-stu-id="ba4d2-149">Check toosee that you are updating hello correct scoring endpoint</span></span>
* <span data-ttu-id="ba4d2-150">No aplicar la revisión Hola servicio Web de aprendizaje: operación de revisión de hello debe realizarse en hello la puntuación del servicio Web.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-150">Do not patch hello Training Web Service: hello patch operation must be performed on hello scoring Web service.</span></span>
* <span data-ttu-id="ba4d2-151">No aplicar la revisión extremo predeterminado de hello en el servicio Web: operación de revisión de hello debe realizarse en Hola de nuevo la puntuación del extremo del servicio Web que agregó.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-151">Do not patch hello default endpoint on Web service: hello patch operation must be performed on hello new scoring Web service endpoint that you added.</span></span>

<span data-ttu-id="ba4d2-152">Puede comprobar qué extremo de hello del servicio Web está activado de hello visitando portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-152">You can verify which Web service hello endpoint is on by visiting hello Azure classic portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="ba4d2-153">Asegúrese de que está agregando Hola extremo toohello predictivo servicio Web, servicio Web de aprendizaje y no Hola.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-153">Be sure you are adding hello endpoint toohello Predictive Web Service, not hello Training Web Service.</span></span> <span data-ttu-id="ba4d2-154">Si ha implementado correctamente un servicio web predictivo y otro de formación, debería ver dos servicios web independientes.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-154">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate Web services listed.</span></span> <span data-ttu-id="ba4d2-155">Hola predictivo servicio Web debe terminar con "[exp predictiva.]".</span><span class="sxs-lookup"><span data-stu-id="ba4d2-155">hello Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

1. <span data-ttu-id="ba4d2-156">Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="ba4d2-156">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="ba4d2-157">Pestaña de aprendizaje automático de hello abierto. ![Interfaz de usuario del área de trabajo de Machine Learning.][image4]</span><span class="sxs-lookup"><span data-stu-id="ba4d2-157">Open hello Machine Learning tab. ![Machine learning workspace UI.][image4]</span></span>
3. <span data-ttu-id="ba4d2-158">Seleccione su área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-158">Select your workspace.</span></span>
4. <span data-ttu-id="ba4d2-159">Haga clic en **Servicios web**.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-159">Click **Web Services**.</span></span>
5. <span data-ttu-id="ba4d2-160">Seleccione su servicio web predictivo.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-160">Select your Predictive Web Service.</span></span>
6. <span data-ttu-id="ba4d2-161">Compruebe que el nuevo punto de conexión se ha agregado el servicio Web de toohello.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-161">Verify that your new endpoint was added toohello Web service.</span></span>

### <a name="check-hello-workspace-that-your-web-service-is-in-tooensure-it-is-in-hello-correct-region"></a><span data-ttu-id="ba4d2-162">Compruebe el área de trabajo de Hola que el servicio web está en tooensure que se encuentra en la región correcta Hola</span><span class="sxs-lookup"><span data-stu-id="ba4d2-162">Check hello workspace that your web service is in tooensure it is in hello correct region</span></span>
1. <span data-ttu-id="ba4d2-163">Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="ba4d2-163">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="ba4d2-164">Seleccione aprendizaje automático en el menú de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-164">Select Machine Learning from hello menu.</span></span>
   <span data-ttu-id="ba4d2-165">![Interfaz de usuario de la región de Machine Learning.][image4]</span><span class="sxs-lookup"><span data-stu-id="ba4d2-165">![Machine learning region UI.][image4]</span></span>
3. <span data-ttu-id="ba4d2-166">Compruebe la ubicación de hello del área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="ba4d2-166">Verify hello location of your workspace.</span></span>

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
