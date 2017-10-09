---
title: "aaaRetrain un servicio web de clásico | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooprogrammatically volver a entrenar un modelo y actualización hello web servicio toouse Hola recién entrenado en aprendizaje automático de Azure."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: e36e1961-9e8b-4801-80ef-46d80b140452
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: d3ba21ed75f02868535cb2fcac607643303a9554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-classic-web-service"></a><span data-ttu-id="69d5a-103">Reentrenamiento de un servicio web clásico</span><span class="sxs-lookup"><span data-stu-id="69d5a-103">Retrain a Classic web service</span></span>
<span data-ttu-id="69d5a-104">Hola predictivo servicio Web implementa es predeterminado Hola la puntuación del punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="69d5a-104">hello Predictive Web Service you deployed is hello default scoring endpoint.</span></span> <span data-ttu-id="69d5a-105">Puntos de conexión predeterminados se mantienen sincronizada con hello originales de entrenamiento y puntuación experimentos y, por tanto, hello entrenado para el punto de conexión de hello predeterminado no se puede reemplazar.</span><span class="sxs-lookup"><span data-stu-id="69d5a-105">Default endpoints are kept in sync with hello original training and scoring experiments, and therefore hello trained model for hello default endpoint cannot be replaced.</span></span> <span data-ttu-id="69d5a-106">servicio web de tooretrain hello, debe agregar un nuevo servicio web de toohello de punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="69d5a-106">tooretrain hello web service, you must add a new endpoint toohello web service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="69d5a-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="69d5a-107">Prerequisites</span></span>
<span data-ttu-id="69d5a-108">Debe haber configurado un experimento de entrenamiento y un experimento predictivo tal como se muestra en los [modelos de reciclaje de Machine Learning mediante programación](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="69d5a-108">You must have set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="69d5a-109">experimento predictivo Hola debe implementarse como un servicio web de aprendizaje de automático de clásico.</span><span class="sxs-lookup"><span data-stu-id="69d5a-109">hello predictive experiment must be deployed as a Classic machine learning web service.</span></span> 
> 
> 

<span data-ttu-id="69d5a-110">Para obtener más información sobre la implementación de servicios web, vea el artículo sobre [implementación de un servicio web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="69d5a-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="add-a-new-endpoint"></a><span data-ttu-id="69d5a-111">Adición de un nuevo punto de conexión</span><span class="sxs-lookup"><span data-stu-id="69d5a-111">Add a new Endpoint</span></span>
<span data-ttu-id="69d5a-112">Hola predictivo servicio Web que ha implementado contiene un punto de conexión que se mantiene en sincronización con entrenamiento original de Hola y puntuación entrenado de experimentos de puntuación predeterminado.</span><span class="sxs-lookup"><span data-stu-id="69d5a-112">hello Predictive Web Service that you deployed contains a default scoring endpoint that is kept in sync with hello original training and scoring experiments trained model.</span></span> <span data-ttu-id="69d5a-113">tooupdate el servicio web, toowith un nuevo modelo entrenado, debe crear un nuevo extremo de puntuación.</span><span class="sxs-lookup"><span data-stu-id="69d5a-113">tooupdate your web service toowith a new trained model, you must create a new scoring endpoint.</span></span> 

<span data-ttu-id="69d5a-114">un nuevo extremo de puntuación, en hello predictivo servicio Web que se pueden actualizar con entrenado Hola toocreate:</span><span class="sxs-lookup"><span data-stu-id="69d5a-114">toocreate a new scoring endpoint, on hello Predictive Web Service that can be updated with hello trained model:</span></span>

> [!NOTE]
> <span data-ttu-id="69d5a-115">Asegúrese de que está agregando Hola extremo toohello predictivo servicio Web, servicio Web de aprendizaje y no Hola.</span><span class="sxs-lookup"><span data-stu-id="69d5a-115">Be sure you are adding hello endpoint toohello Predictive Web Service, not hello Training Web Service.</span></span> <span data-ttu-id="69d5a-116">Si ha implementado correctamente un servicio web predictivo y otro de entrenamiento, debería ver dos servicios web independientes.</span><span class="sxs-lookup"><span data-stu-id="69d5a-116">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate web services listed.</span></span> <span data-ttu-id="69d5a-117">Hola predictivo servicio Web debe terminar con "[exp predictiva.]".</span><span class="sxs-lookup"><span data-stu-id="69d5a-117">hello Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

<span data-ttu-id="69d5a-118">Hay tres formas en que puede agregar un nuevo servicio web de tooa de punto de conexión:</span><span class="sxs-lookup"><span data-stu-id="69d5a-118">There are three ways in which you can add a new end point tooa web service:</span></span>

1. <span data-ttu-id="69d5a-119">De manera programática</span><span class="sxs-lookup"><span data-stu-id="69d5a-119">Programmatically</span></span>
2. <span data-ttu-id="69d5a-120">Usar el portal de servicios Web de Microsoft Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="69d5a-120">Use hello Microsoft Azure Web Services portal</span></span>
3. <span data-ttu-id="69d5a-121">Usar hello portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="69d5a-121">Use hello Azure classic portal</span></span>

### <a name="programmatically-add-an-endpoint"></a><span data-ttu-id="69d5a-122">Incorporación de un punto de conexión mediante programación</span><span class="sxs-lookup"><span data-stu-id="69d5a-122">Programmatically add an endpoint</span></span>
<span data-ttu-id="69d5a-123">Puede agregar extremos de puntuación mediante código de ejemplo de Hola proporcionado en este [repositorio de github](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="69d5a-123">You can add scoring endpoints using hello sample code provided in this [github repository](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span></span>

### <a name="use-hello-microsoft-azure-web-services-portal-tooadd-an-endpoint"></a><span data-ttu-id="69d5a-124">Usar Hola servicios Web de Microsoft Azure portal tooadd un punto de conexión</span><span class="sxs-lookup"><span data-stu-id="69d5a-124">Use hello Microsoft Azure Web Services portal tooadd an endpoint</span></span>
1. <span data-ttu-id="69d5a-125">En estudio de aprendizaje automático, en la columna de navegación izquierdo de hello, haga clic en servicios Web.</span><span class="sxs-lookup"><span data-stu-id="69d5a-125">In Machine Learning Studio, on hello left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="69d5a-126">En hello parte inferior del panel de servicio de hello web, haga clic en **vista previa de los puntos de conexión de administrar**.</span><span class="sxs-lookup"><span data-stu-id="69d5a-126">At hello bottom of hello web service dashboard, click **Manage endpoints preview**.</span></span>
3. <span data-ttu-id="69d5a-127">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="69d5a-127">Click **Add**.</span></span>
4. <span data-ttu-id="69d5a-128">Escriba un nombre y una descripción para el nuevo punto de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="69d5a-128">Type a name and description for hello new endpoint.</span></span> <span data-ttu-id="69d5a-129">Seleccione el nivel de registro de hello y si los datos de ejemplo está habilitado.</span><span class="sxs-lookup"><span data-stu-id="69d5a-129">Select hello logging level and whether sample data is enabled.</span></span> <span data-ttu-id="69d5a-130">Para más información sobre los registros, vea [Habilitar el registro para los servicios web de Aprendizaje automático](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="69d5a-130">For more information on logging, see [Enable logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>

### <a name="use-hello-azure-classic-portal-tooadd-an-endpoint"></a><span data-ttu-id="69d5a-131">Usar hello tooadd portal clásico un punto de conexión de Azure</span><span class="sxs-lookup"><span data-stu-id="69d5a-131">Use hello Azure classic portal tooadd an endpoint</span></span>
1. <span data-ttu-id="69d5a-132">Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="69d5a-132">Sign in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="69d5a-133">En el menú de la izquierda hello, haga clic en **aprendizaje automático**.</span><span class="sxs-lookup"><span data-stu-id="69d5a-133">In hello left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="69d5a-134">En Nombre, haga clic en el área de trabajo y, a continuación, haga clic en **Servicios web**.</span><span class="sxs-lookup"><span data-stu-id="69d5a-134">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="69d5a-135">En Nombre, haga clic en **Census Model [predictive exp.]** (Modelo de censo [exp. predictivo]).</span><span class="sxs-lookup"><span data-stu-id="69d5a-135">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="69d5a-136">En la parte inferior de Hola de página de hello, haga clic en **Agregar extremo**.</span><span class="sxs-lookup"><span data-stu-id="69d5a-136">At hello bottom of hello page, click **Add Endpoint**.</span></span> <span data-ttu-id="69d5a-137">Para más información sobre la incorporación de puntos de conexión, consulte [Creación de puntos de conexión](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="69d5a-137">For more information on adding endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span> 

## <a name="update-hello-added-endpoints-trained-model"></a><span data-ttu-id="69d5a-138">Hola de actualización agrega entrenado del punto de conexión</span><span class="sxs-lookup"><span data-stu-id="69d5a-138">Update hello added endpoint’s Trained Model</span></span>
<span data-ttu-id="69d5a-139">proceso de reconversión de hello toocomplete, debe actualizar entrenado Hola de hello nuevo punto de conexión que agregó.</span><span class="sxs-lookup"><span data-stu-id="69d5a-139">toocomplete hello retraining process, you must update hello trained model of hello new endpoint that you added.</span></span>

* <span data-ttu-id="69d5a-140">Si ha agregado Hola nuevo punto de conexión mediante el portal de Azure clásico hello, puede haga clic en nombre de hello nuevo del punto de conexión en el portal de Hola y luego Hola **UpdateResource** tooget dirección URL de hello necesitaría modelo tooupdate Hola del punto de conexión del vínculo.</span><span class="sxs-lookup"><span data-stu-id="69d5a-140">If you added hello new endpoint using hello classic Azure portal, you can click hello new endpoint's name in hello portal, then hello **UpdateResource** link tooget hello URL you would need tooupdate hello endpoint's model.</span></span>
* <span data-ttu-id="69d5a-141">Si ha agregado el punto de conexión de hello mediante código de ejemplo de Hola, esta información incluye la ubicación de dirección URL de la Ayuda de hello identificado por hello *HelpLocationURL* valor de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="69d5a-141">If you added hello endpoint using hello sample code, this includes location of hello help URL identified by hello *HelpLocationURL* value in hello output.</span></span>

<span data-ttu-id="69d5a-142">dirección URL de la ruta de acceso de hello del tooretrieve:</span><span class="sxs-lookup"><span data-stu-id="69d5a-142">tooretrieve hello path URL:</span></span>

1. <span data-ttu-id="69d5a-143">Copie y pegue la dirección URL de hello en el explorador.</span><span class="sxs-lookup"><span data-stu-id="69d5a-143">Copy and paste hello URL into your browser.</span></span>
2. <span data-ttu-id="69d5a-144">Haga clic en el vínculo del recurso de actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="69d5a-144">Click hello Update Resource link.</span></span>
3. <span data-ttu-id="69d5a-145">Copiar dirección URL de POST de solicitud de revisión de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="69d5a-145">Copy hello POST URL of hello PATCH request.</span></span> <span data-ttu-id="69d5a-146">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="69d5a-146">For example:</span></span>
   
     <span data-ttu-id="69d5a-147">PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span><span class="sxs-lookup"><span data-stu-id="69d5a-147">PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span></span>

<span data-ttu-id="69d5a-148">Ahora puede usar hello tooupdate Hola entrenado que la puntuación del punto de conexión que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="69d5a-148">You can now use hello trained model tooupdate hello scoring endpoint that you created previously.</span></span>

<span data-ttu-id="69d5a-149">Hola siguiendo el ejemplo de código muestra cómo hello toouse *BaseLocation*, *RelativeLocation*, *SasBlobToken*y el punto de conexión de dirección URL PATCH tooupdate Hola.</span><span class="sxs-lookup"><span data-stu-id="69d5a-149">hello following sample code shows you how toouse hello *BaseLocation*, *RelativeLocation*, *SasBlobToken*, and PATCH URL tooupdate hello endpoint.</span></span>

    private async Task OverwriteModel()
    {
        var resourceLocations = new
        {
            Resources = new[]
            {
                new
                {
                    Name = "Census Model [trained model]",
                    Location = new AzureBlobDataReference()
                    {
                        BaseLocation = "https://esintussouthsus.blob.core.windows.net/",
                        RelativeLocation = "your endpoint relative location", //from hello output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from hello output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
                    }
                }
            }
        };

        using (var client = new HttpClient())
        {
            client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", apiKey);

            using (var request = new HttpRequestMessage(new HttpMethod("PATCH"), endpointUrl))
            {
                request.Content = new StringContent(JsonConvert.SerializeObject(resourceLocations), System.Text.Encoding.UTF8, "application/json");
                HttpResponseMessage response = await client.SendAsync(request);

                if (!response.IsSuccessStatusCode)
                {
                    await WriteFailedResponse(response);
                }

                // Do what you want with a successful response here.
            }
        }
    }

<span data-ttu-id="69d5a-150">Hola *apiKey* hello y *endpointUrl* de llamada de hello puede obtenerse de panel de punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="69d5a-150">hello *apiKey* and hello *endpointUrl* for hello call can be obtained from endpoint dashboard.</span></span>

<span data-ttu-id="69d5a-151">Hola valo hello *nombre* parámetro en *recursos* debe Hola de coincidencia de nombre de recurso de hello Guardar modelo entrenado en experimento predictivo Hola.</span><span class="sxs-lookup"><span data-stu-id="69d5a-151">hello value of hello *Name* parameter in *Resources* should match hello Resource Name of hello saved Trained Model in hello predictive experiment.</span></span> <span data-ttu-id="69d5a-152">Hola tooget nombre de recurso:</span><span class="sxs-lookup"><span data-stu-id="69d5a-152">tooget hello Resource Name:</span></span>

1. <span data-ttu-id="69d5a-153">Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="69d5a-153">Sign in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="69d5a-154">En el menú de la izquierda hello, haga clic en **aprendizaje automático**.</span><span class="sxs-lookup"><span data-stu-id="69d5a-154">In hello left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="69d5a-155">En Nombre, haga clic en el área de trabajo y, a continuación, haga clic en **Servicios web**.</span><span class="sxs-lookup"><span data-stu-id="69d5a-155">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="69d5a-156">En Nombre, haga clic en **Census Model [predictive exp.]** (Modelo de censo [exp. predictivo]).</span><span class="sxs-lookup"><span data-stu-id="69d5a-156">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="69d5a-157">Haga clic en nuevo extremo de Hola que agregó.</span><span class="sxs-lookup"><span data-stu-id="69d5a-157">Click hello new endpoint you added.</span></span>
6. <span data-ttu-id="69d5a-158">En el panel de punto de conexión de hello, haga clic en **recurso de actualización**.</span><span class="sxs-lookup"><span data-stu-id="69d5a-158">On hello endpoint dashboard, click **Update Resource**.</span></span>
7. <span data-ttu-id="69d5a-159">En la página de documentación de API de recursos de actualización de hello para el servicio web de hello, puede buscar hello **nombre de recurso** en **recursos actualizables**.</span><span class="sxs-lookup"><span data-stu-id="69d5a-159">On hello Update Resource API Documentation page for hello web service, you can find hello **Resource Name** under **Updatable Resources**.</span></span>

<span data-ttu-id="69d5a-160">Si el token SAS expira antes de que termine de actualizar el punto de conexión de hello, debe realizar una operación GET con el Id. de trabajo de hello tooobtain un nuevo token.</span><span class="sxs-lookup"><span data-stu-id="69d5a-160">If your SAS token expires before you finish updating hello endpoint, you must perform a GET with hello Job Id tooobtain a fresh token.</span></span>

<span data-ttu-id="69d5a-161">Cuando se ejecutó correctamente el código de hello, nuevo punto de conexión de hello debe empezar a utilizar Hola volver a entrenar modelo en 30 segundos aproximadamente.</span><span class="sxs-lookup"><span data-stu-id="69d5a-161">When hello code has successfully run, hello new endpoint should start using hello retrained model in approximately 30 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="69d5a-162">Resumen</span><span class="sxs-lookup"><span data-stu-id="69d5a-162">Summary</span></span>
<span data-ttu-id="69d5a-163">Usar Hola reciclaje API, puede actualizar entrenado Hola de un servicio Web predictivos que permite escenarios como:</span><span class="sxs-lookup"><span data-stu-id="69d5a-163">Using hello Retraining APIs, you can update hello trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="69d5a-164">Reentrenamiento de modelos periódicos con nuevos datos.</span><span class="sxs-lookup"><span data-stu-id="69d5a-164">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="69d5a-165">Distribución de un modelo toocustomers con el objetivo de Hola de lo que permite volver a entrenar modelo hello mediante sus propios datos.</span><span class="sxs-lookup"><span data-stu-id="69d5a-165">Distribution of a model toocustomers with hello goal of letting them retrain hello model using their own data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69d5a-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="69d5a-166">Next steps</span></span>
[<span data-ttu-id="69d5a-167">Solución de problemas de hello reciclaje de un servicio web clásico de aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="69d5a-167">Troubleshooting hello retraining of an Azure Machine Learning classic web service</span></span>](machine-learning-troubleshooting-retraining-models.md)

