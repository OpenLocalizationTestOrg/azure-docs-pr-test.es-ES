---
title: "Reentrenamiento de un servicio web clásico | Microsoft Docs"
description: "Obtenga información acerca de cómo volver a entrenar un modelo y actualizar el servicio web mediante programación para utilizar el modelo recién entrenado en el Aprendizaje automático de Azure."
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
ms.openlocfilehash: 3f9f4cd5ed36262845f7a3139073ccd4e49f472a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="retrain-a-classic-web-service"></a><span data-ttu-id="9781d-103">Reentrenamiento de un servicio web clásico</span><span class="sxs-lookup"><span data-stu-id="9781d-103">Retrain a Classic web service</span></span>
<span data-ttu-id="9781d-104">El servicio web predictivo que implementó es el punto de conexión de puntuación predeterminado.</span><span class="sxs-lookup"><span data-stu-id="9781d-104">The Predictive Web Service you deployed is the default scoring endpoint.</span></span> <span data-ttu-id="9781d-105">Los puntos de conexión predeterminados se mantienen sincronizados con los experimentos de entrenamiento y puntuación originales y, por tanto, el modelo entrenado de un punto de conexión predeterminado no se puede reemplazar.</span><span class="sxs-lookup"><span data-stu-id="9781d-105">Default endpoints are kept in sync with the original training and scoring experiments, and therefore the trained model for the default endpoint cannot be replaced.</span></span> <span data-ttu-id="9781d-106">Para reciclar el servicio web, debe agregar un nuevo punto de conexión al servicio web.</span><span class="sxs-lookup"><span data-stu-id="9781d-106">To retrain the web service, you must add a new endpoint to the web service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9781d-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9781d-107">Prerequisites</span></span>
<span data-ttu-id="9781d-108">Debe haber configurado un experimento de entrenamiento y un experimento predictivo tal como se muestra en los [modelos de reciclaje de Machine Learning mediante programación](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="9781d-108">You must have set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9781d-109">El experimento predictivo debe implementarse como un servicio web Machine Learning clásico.</span><span class="sxs-lookup"><span data-stu-id="9781d-109">The predictive experiment must be deployed as a Classic machine learning web service.</span></span> 
> 
> 

<span data-ttu-id="9781d-110">Para obtener más información sobre la implementación de servicios web, vea el artículo sobre [implementación de un servicio web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="9781d-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="add-a-new-endpoint"></a><span data-ttu-id="9781d-111">Adición de un nuevo punto de conexión</span><span class="sxs-lookup"><span data-stu-id="9781d-111">Add a new Endpoint</span></span>
<span data-ttu-id="9781d-112">El servicio web predictivo que implementó contiene un punto de conexión de puntuación predeterminado que se mantiene sincronizado con la formación original y el modelo entrenado de experimentos de puntuación.</span><span class="sxs-lookup"><span data-stu-id="9781d-112">The Predictive Web Service that you deployed contains a default scoring endpoint that is kept in sync with the original training and scoring experiments trained model.</span></span> <span data-ttu-id="9781d-113">Para actualizar el servicio web a un nuevo modelo entrenado, debe crear un nuevo punto de conexión para la puntuación.</span><span class="sxs-lookup"><span data-stu-id="9781d-113">To update your web service to with a new trained model, you must create a new scoring endpoint.</span></span> 

<span data-ttu-id="9781d-114">Para crear un nuevo punto de conexión de puntuación, en el servicio web predictivo que se puede actualizar con el modelo entrenado:</span><span class="sxs-lookup"><span data-stu-id="9781d-114">To create a new scoring endpoint, on the Predictive Web Service that can be updated with the trained model:</span></span>

> [!NOTE]
> <span data-ttu-id="9781d-115">Asegúrese de agregar el punto de conexión al servicio web predictivo y no al de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="9781d-115">Be sure you are adding the endpoint to the Predictive Web Service, not the Training Web Service.</span></span> <span data-ttu-id="9781d-116">Si ha implementado correctamente un servicio web predictivo y otro de entrenamiento, debería ver dos servicios web independientes.</span><span class="sxs-lookup"><span data-stu-id="9781d-116">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate web services listed.</span></span> <span data-ttu-id="9781d-117">El servicio web predictivo debe terminar con "[predictive exp.]".</span><span class="sxs-lookup"><span data-stu-id="9781d-117">The Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

<span data-ttu-id="9781d-118">Hay tres formas en que puede agregar un nuevo punto de conexión a un servicio web:</span><span class="sxs-lookup"><span data-stu-id="9781d-118">There are three ways in which you can add a new end point to a web service:</span></span>

1. <span data-ttu-id="9781d-119">De manera programática</span><span class="sxs-lookup"><span data-stu-id="9781d-119">Programmatically</span></span>
2. <span data-ttu-id="9781d-120">Uso del portal de servicios web de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="9781d-120">Use the Microsoft Azure Web Services portal</span></span>
3. <span data-ttu-id="9781d-121">Uso del Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="9781d-121">Use the Azure classic portal</span></span>

### <a name="programmatically-add-an-endpoint"></a><span data-ttu-id="9781d-122">Incorporación de un punto de conexión mediante programación</span><span class="sxs-lookup"><span data-stu-id="9781d-122">Programmatically add an endpoint</span></span>
<span data-ttu-id="9781d-123">También puede agregar puntos de conexión de puntuación mediante el código de ejemplo proporcionado en este [repositorio de GitHub](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="9781d-123">You can add scoring endpoints using the sample code provided in this [github repository](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span></span>

### <a name="use-the-microsoft-azure-web-services-portal-to-add-an-endpoint"></a><span data-ttu-id="9781d-124">Uso del portal de servicios web de Microsoft Azure para agregar un punto de conexión</span><span class="sxs-lookup"><span data-stu-id="9781d-124">Use the Microsoft Azure Web Services portal to add an endpoint</span></span>
1. <span data-ttu-id="9781d-125">En Machine Learning Studio, en la columna de navegación izquierda, haga clic en Servicios web.</span><span class="sxs-lookup"><span data-stu-id="9781d-125">In Machine Learning Studio, on the left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="9781d-126">En la parte inferior del panel de servicios web, haga clic en **Manage endpoints preview**(Administrar versión preliminar de puntos de conexión).</span><span class="sxs-lookup"><span data-stu-id="9781d-126">At the bottom of the web service dashboard, click **Manage endpoints preview**.</span></span>
3. <span data-ttu-id="9781d-127">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9781d-127">Click **Add**.</span></span>
4. <span data-ttu-id="9781d-128">Escriba un nombre y una descripción para el nuevo punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="9781d-128">Type a name and description for the new endpoint.</span></span> <span data-ttu-id="9781d-129">Seleccione el nivel de registro y si los datos de ejemplo están habilitados.</span><span class="sxs-lookup"><span data-stu-id="9781d-129">Select the logging level and whether sample data is enabled.</span></span> <span data-ttu-id="9781d-130">Para más información sobre los registros, vea [Habilitar el registro para los servicios web de Aprendizaje automático](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="9781d-130">For more information on logging, see [Enable logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>

### <a name="use-the-azure-classic-portal-to-add-an-endpoint"></a><span data-ttu-id="9781d-131">Uso del Portal de Azure clásico para agregar un punto de conexión</span><span class="sxs-lookup"><span data-stu-id="9781d-131">Use the Azure classic portal to add an endpoint</span></span>
1. <span data-ttu-id="9781d-132">Inicie sesión en el [Portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="9781d-132">Sign in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="9781d-133">Haga clic en **Aprendizaje automático**en el menú izquierdo.</span><span class="sxs-lookup"><span data-stu-id="9781d-133">In the left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="9781d-134">En Nombre, haga clic en el área de trabajo y, a continuación, haga clic en **Servicios web**.</span><span class="sxs-lookup"><span data-stu-id="9781d-134">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="9781d-135">En Nombre, haga clic en **Census Model [predictive exp.]** (Modelo de censo [exp. predictivo]).</span><span class="sxs-lookup"><span data-stu-id="9781d-135">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="9781d-136">Haga clic en **Agregar extremo**en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="9781d-136">At the bottom of the page, click **Add Endpoint**.</span></span> <span data-ttu-id="9781d-137">Para más información sobre la incorporación de puntos de conexión, consulte [Creación de puntos de conexión](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="9781d-137">For more information on adding endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span> 

## <a name="update-the-added-endpoints-trained-model"></a><span data-ttu-id="9781d-138">Actualización del modelo entrenado del punto de conexión agregado</span><span class="sxs-lookup"><span data-stu-id="9781d-138">Update the added endpoint’s Trained Model</span></span>
<span data-ttu-id="9781d-139">Para completar el proceso de reentrenamiento, debe actualizar el modelo entrenado del nuevo punto de conexión que ha agregado.</span><span class="sxs-lookup"><span data-stu-id="9781d-139">To complete the retraining process, you must update the trained model of the new endpoint that you added.</span></span>

* <span data-ttu-id="9781d-140">Si ha agregado el nuevo punto de conexión mediante el Portal de Azure clásico, puede hacer clic en su nombre y luego en el vínculo **UpdateResource** para obtener la dirección URL que necesitará para actualizar el modelo del punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="9781d-140">If you added the new endpoint using the classic Azure portal, you can click the new endpoint's name in the portal, then the **UpdateResource** link to get the URL you would need to update the endpoint's model.</span></span>
* <span data-ttu-id="9781d-141">Si agregó el punto de conexión mediante el código de ejemplo, esto incluye la ubicación de la dirección URL de ayuda identificada por el valor *HelpLocationURL* de la salida.</span><span class="sxs-lookup"><span data-stu-id="9781d-141">If you added the endpoint using the sample code, this includes location of the help URL identified by the *HelpLocationURL* value in the output.</span></span>

<span data-ttu-id="9781d-142">Para recuperar la dirección URL de la ruta de acceso:</span><span class="sxs-lookup"><span data-stu-id="9781d-142">To retrieve the path URL:</span></span>

1. <span data-ttu-id="9781d-143">Copie y pegue la URL en el explorador.</span><span class="sxs-lookup"><span data-stu-id="9781d-143">Copy and paste the URL into your browser.</span></span>
2. <span data-ttu-id="9781d-144">Haga clic en el vínculo Actualizar recurso.</span><span class="sxs-lookup"><span data-stu-id="9781d-144">Click the Update Resource link.</span></span>
3. <span data-ttu-id="9781d-145">Copie la dirección URL de POST de la solicitud PATCH.</span><span class="sxs-lookup"><span data-stu-id="9781d-145">Copy the POST URL of the PATCH request.</span></span> <span data-ttu-id="9781d-146">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9781d-146">For example:</span></span>
   
     <span data-ttu-id="9781d-147">PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span><span class="sxs-lookup"><span data-stu-id="9781d-147">PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span></span>

<span data-ttu-id="9781d-148">Ahora puede usar el modelo entrenado para actualizar el punto de conexión de puntuación que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9781d-148">You can now use the trained model to update the scoring endpoint that you created previously.</span></span>

<span data-ttu-id="9781d-149">El código de ejemplo siguiente muestra cómo utilizar *BaseLocation*, *RelativeLocation*, *SasBlobToken* y el valor de PATCH URL para actualizar el punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="9781d-149">The following sample code shows you how to use the *BaseLocation*, *RelativeLocation*, *SasBlobToken*, and PATCH URL to update the endpoint.</span></span>

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
                        RelativeLocation = "your endpoint relative location", //from the output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from the output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
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

<span data-ttu-id="9781d-150">Se puede obtener *apiKey* y *endpointUrl* para la llamada desde el panel del punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="9781d-150">The *apiKey* and the *endpointUrl* for the call can be obtained from endpoint dashboard.</span></span>

<span data-ttu-id="9781d-151">El valor del parámetro *Name* de *Resources* debe coincidir con el nombre del recurso del modelo entrenado guardado en el experimento predictivo.</span><span class="sxs-lookup"><span data-stu-id="9781d-151">The value of the *Name* parameter in *Resources* should match the Resource Name of the saved Trained Model in the predictive experiment.</span></span> <span data-ttu-id="9781d-152">Para obtener el nombre del recurso:</span><span class="sxs-lookup"><span data-stu-id="9781d-152">To get the Resource Name:</span></span>

1. <span data-ttu-id="9781d-153">Inicie sesión en el [Portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="9781d-153">Sign in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="9781d-154">Haga clic en **Aprendizaje automático**en el menú izquierdo.</span><span class="sxs-lookup"><span data-stu-id="9781d-154">In the left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="9781d-155">En Nombre, haga clic en el área de trabajo y, a continuación, haga clic en **Servicios web**.</span><span class="sxs-lookup"><span data-stu-id="9781d-155">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="9781d-156">En Nombre, haga clic en **Census Model [predictive exp.]** (Modelo de censo [exp. predictivo]).</span><span class="sxs-lookup"><span data-stu-id="9781d-156">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="9781d-157">Haga clic en el nuevo punto de conexión que ha agregado.</span><span class="sxs-lookup"><span data-stu-id="9781d-157">Click the new endpoint you added.</span></span>
6. <span data-ttu-id="9781d-158">En el panel del punto de conexión, haga clic en **Actualizar recurso**.</span><span class="sxs-lookup"><span data-stu-id="9781d-158">On the endpoint dashboard, click **Update Resource**.</span></span>
7. <span data-ttu-id="9781d-159">En la página de documentación de la API de actualización de recurso para el servicio web, encontrará el **nombre del recurso** en **Updatable Resources** (Recursos actualizables).</span><span class="sxs-lookup"><span data-stu-id="9781d-159">On the Update Resource API Documentation page for the web service, you can find the **Resource Name** under **Updatable Resources**.</span></span>

<span data-ttu-id="9781d-160">Si el token SAS expira antes de que termine de actualizar el punto de conexión, deberá realizar una operación GET con el identificador de trabajo para obtener un nuevo token.</span><span class="sxs-lookup"><span data-stu-id="9781d-160">If your SAS token expires before you finish updating the endpoint, you must perform a GET with the Job Id to obtain a fresh token.</span></span>

<span data-ttu-id="9781d-161">Si el código se ha ejecutado correctamente, el nuevo punto de conexión debería comenzar a utilizar el modelo reentrenado en aproximadamente 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="9781d-161">When the code has successfully run, the new endpoint should start using the retrained model in approximately 30 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="9781d-162">Resumen</span><span class="sxs-lookup"><span data-stu-id="9781d-162">Summary</span></span>
<span data-ttu-id="9781d-163">Mediante el uso de las API de reentrenamiento, puede actualizar el modelo entrenado de un servicio web predictivo habilitando escenarios como:</span><span class="sxs-lookup"><span data-stu-id="9781d-163">Using the Retraining APIs, you can update the trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="9781d-164">Reentrenamiento de modelos periódicos con nuevos datos.</span><span class="sxs-lookup"><span data-stu-id="9781d-164">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="9781d-165">Distribución de un modelo entre los clientes con el fin de permitirles reentrenar el modelo mediante sus propios datos.</span><span class="sxs-lookup"><span data-stu-id="9781d-165">Distribution of a model to customers with the goal of letting them retrain the model using their own data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9781d-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9781d-166">Next steps</span></span>
[<span data-ttu-id="9781d-167">Solución de problemas del reentrenamiento de un servicio web clásico de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="9781d-167">Troubleshooting the retraining of an Azure Machine Learning classic web service</span></span>](machine-learning-troubleshooting-retraining-models.md)

