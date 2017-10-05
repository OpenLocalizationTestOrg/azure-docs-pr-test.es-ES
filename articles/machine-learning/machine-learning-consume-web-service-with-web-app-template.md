---
title: "Consumo de un servicio web Machine Learning con una plantilla de aplicación web | Microsoft Docs"
description: "Use una plantilla de aplicación web en Azure Marketplace para consumir un servicio web predictivo en Aprendizaje automático de Azure."
keywords: "servicio web,operacionalización,API de REST,aprendizaje automático"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e0d71683-61b9-4675-8df5-09ddc2f0d92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;raymondl
ms.openlocfilehash: 95aa1fa23d83ec0dcd00870179167e803bafbd16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a><span data-ttu-id="e74d2-104">Consumo de un servicio web de Aprendizaje automático de Azure con una plantilla de aplicación web</span><span class="sxs-lookup"><span data-stu-id="e74d2-104">Consume an Azure Machine Learning web service with a web app template</span></span>

<span data-ttu-id="e74d2-105">Una vez que desarrolla su modelo predictivo y lo implementa como un servicio web de Azure con Estudio de aprendizaje automático o con herramientas como R o Python, puede tener acceso al modelo de operaciones con una API de REST.</span><span class="sxs-lookup"><span data-stu-id="e74d2-105">Once you've developed your predictive model and deployed it as an Azure web service using Machine Learning Studio, or using tools such as R or Python, you can access the operationalized model using a REST API.</span></span>

<span data-ttu-id="e74d2-106">Hay varias maneras de usar la API de REST y tener acceso al servicio web.</span><span class="sxs-lookup"><span data-stu-id="e74d2-106">There are a number of ways to consume the REST API and access the web service.</span></span> <span data-ttu-id="e74d2-107">Por ejemplo, puede escribir una aplicación en C#, R o Python con el código de ejemplo que se generó cuando implementó el servicio web (disponible en el [Portal Servicios web de Machine Learning](https://services.azureml.net/quickstart) o en el panel de servicios web en Machine Learning Studio).</span><span class="sxs-lookup"><span data-stu-id="e74d2-107">For example, you can write an application in C#, R, or Python using the sample code generated for you when you deployed the web service (available in the [Machine Learning Web Services Portal](https://services.azureml.net/quickstart) or in the web service dashboard in Machine Learning Studio).</span></span> <span data-ttu-id="e74d2-108">O bien, puede usar el libro de Microsoft Excel de ejemplo que se creó al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="e74d2-108">Or you can use the sample Microsoft Excel workbook created for you at the same time.</span></span>

<span data-ttu-id="e74d2-109">Pero la manera más rápida y fácil para tener acceso al servicio web es a través de las plantillas de aplicación web disponibles en [Marketplace de aplicaciones web de Azure](https://azure.microsoft.com/marketplace/web-applications/all/).</span><span class="sxs-lookup"><span data-stu-id="e74d2-109">But the quickest and easiest way to access your web service is through the Web App Templates available in the [Azure Web App Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="the-azure-machine-learning-web-app-templates"></a><span data-ttu-id="e74d2-110">Plantillas de aplicación web de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="e74d2-110">The Azure Machine Learning Web App Templates</span></span>
<span data-ttu-id="e74d2-111">Las plantillas de aplicación web disponibles en Azure Marketplace pueden crear una aplicación web personalizada que conoce los datos de entrada del servicio web y los resultados esperados.</span><span class="sxs-lookup"><span data-stu-id="e74d2-111">The web app templates available in the Azure Marketplace can build a custom web app that knows your web service's input data and expected results.</span></span> <span data-ttu-id="e74d2-112">Todo lo que necesita hacer es conceder el acceso de la aplicación web al servicio web y los datos, y la plantilla se encarga del resto.</span><span class="sxs-lookup"><span data-stu-id="e74d2-112">All you need to do is give the web app access to your web service and data, and the template does the rest.</span></span>

<span data-ttu-id="e74d2-113">Existen dos plantillas:</span><span class="sxs-lookup"><span data-stu-id="e74d2-113">Two templates are available:</span></span>

* [<span data-ttu-id="e74d2-114">Plantilla de aplicación web Request-Response Service de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="e74d2-114">Azure ML Request-Response Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [<span data-ttu-id="e74d2-115">Plantilla de aplicación web Batch Execution Service de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="e74d2-115">Azure ML Batch Execution Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

<span data-ttu-id="e74d2-116">Cada plantilla crea una aplicación de ASP.NET de ejemplo mediante el URI de la API y la clave para el servicio web y la implementa como un sitio web en Azure.</span><span class="sxs-lookup"><span data-stu-id="e74d2-116">Each template creates a sample ASP.NET application, using the API URI and Key for your web service, and deploys it as a web site to Azure.</span></span> <span data-ttu-id="e74d2-117">La plantilla Request-Response Service (RRS) crea una aplicación web que permite enviar una sola fila de datos al servicio web para obtener un resultado único.</span><span class="sxs-lookup"><span data-stu-id="e74d2-117">The Request-Response Service (RRS) template creates a web app that allows you to send a single row of data to the web service to get a single result.</span></span> <span data-ttu-id="e74d2-118">La plantilla Batch Execution Service (BES) crea una aplicación web que permite enviar muchas filas de datos para obtener varios resultados.</span><span class="sxs-lookup"><span data-stu-id="e74d2-118">The Batch Execution Service (BES) template creates a web app that allows you to send many rows of data to get multiple results.</span></span>

<span data-ttu-id="e74d2-119">No es necesaria ninguna codificación para usar estas plantillas.</span><span class="sxs-lookup"><span data-stu-id="e74d2-119">No coding is required to use these templates.</span></span> <span data-ttu-id="e74d2-120">Simplemente, proporcione el URI y la clave de API y la plantilla compilará la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e74d2-120">You just supply the API Key and URI, and the template builds the application for you.</span></span>

<span data-ttu-id="e74d2-121">Para obtener la clave de API y el URI de solicitud de un servicio web:</span><span class="sxs-lookup"><span data-stu-id="e74d2-121">To get the API key and Request URI for a web service:</span></span>

1. <span data-ttu-id="e74d2-122">En el [Portal Servicios web](https://services.azureml.net/quickstart), para un servicio web nuevo, haga clic en **Servicios web** en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="e74d2-122">In the [Web Services Portal](https://services.azureml.net/quickstart), for a New web service, click **Web Services** at the top.</span></span> <span data-ttu-id="e74d2-123">O bien, para un servicio web clásico, haga clic en **Servicios web clásicos**.</span><span class="sxs-lookup"><span data-stu-id="e74d2-123">Or for a Classic web service click **Classic Web Services**.</span></span>
2. <span data-ttu-id="e74d2-124">Haga clic en el servicio web al que desea tener acceso.</span><span class="sxs-lookup"><span data-stu-id="e74d2-124">Click the web service you want to access.</span></span>
3. <span data-ttu-id="e74d2-125">Para un servicio web clásico, haga clic en el punto de conexión al que desea tener acceso.</span><span class="sxs-lookup"><span data-stu-id="e74d2-125">For a Classic web service, click the endpoint you want to access.</span></span>
4. <span data-ttu-id="e74d2-126">Haga clic en **Consumir** en la parte superior.</span><span class="sxs-lookup"><span data-stu-id="e74d2-126">Click **Consume** at the top.</span></span>
5. <span data-ttu-id="e74d2-127">Copie la clave **principal** o **secundaria** y guárdela.</span><span class="sxs-lookup"><span data-stu-id="e74d2-127">Copy the **Primary** or **Secondary Key** and save it.</span></span>
6. <span data-ttu-id="e74d2-128">Si crea una plantilla de servicio de solicitud-respuesta (RRS), copie el URI de **solicitud-respuesta** y guárdelo.</span><span class="sxs-lookup"><span data-stu-id="e74d2-128">If you're creating a Request-Response Service (RRS) template, copy the **Request-Response** URI and save it.</span></span> <span data-ttu-id="e74d2-129">Si crea una plantilla de servicio de ejecución de lotes (BES), copie el URI de las **solicitudes de lote** y guárdelo.</span><span class="sxs-lookup"><span data-stu-id="e74d2-129">If you're creating a Batch Execution Service (BES) template, copy the **Batch Requests** URI and save it.</span></span>


## <a name="how-to-use-the-request-response-service-rrs-template"></a><span data-ttu-id="e74d2-130">Uso de la plantilla Request-Response Service (RRS)</span><span class="sxs-lookup"><span data-stu-id="e74d2-130">How to use the Request-Response Service (RRS) template</span></span>
<span data-ttu-id="e74d2-131">Siga estos pasos para usar la plantilla de aplicación web de RRS, tal como se indica en el diagrama siguiente.</span><span class="sxs-lookup"><span data-stu-id="e74d2-131">Follow these steps to use the RRS web app template, as shown in the following diagram.</span></span>

![Proceso para usar la plantilla web RRS][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. <span data-ttu-id="e74d2-133">Vaya a [Azure Portal](https://portal.azure.com), **Inicio de sesión**, haga clic en **Nuevo**, busque y seleccione **Azure ML Request-Response Service Web App** (Aplicación web de servicio Solicitud-respuesta de Azure ML) y luego haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e74d2-133">Go to the [Azure portal](https://portal.azure.com), **Login**, click **New**, search for and select **Azure ML Request-Response Service Web App**, then click **Create**.</span></span> 
   
   * <span data-ttu-id="e74d2-134">Asigne un nombre único a la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="e74d2-134">Give your web app a unique name.</span></span> <span data-ttu-id="e74d2-135">La dirección URL de la aplicación web será este nombre seguido de `.azurewebsites.net.` Por ejemplo, `http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="e74d2-135">The URL of the web app will be this name followed by `.azurewebsites.net.` For example, `http://carprediction.azurewebsites.net.`</span></span>
   * <span data-ttu-id="e74d2-136">Seleccione los servicios y la suscripción de Azure en los que se ejecuta el servicio web.</span><span class="sxs-lookup"><span data-stu-id="e74d2-136">Select the Azure subscription and services under which your web service is running.</span></span>
   * <span data-ttu-id="e74d2-137">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e74d2-137">Click **Create**.</span></span>
     
     ![Crear aplicación web][image5]

4. <span data-ttu-id="e74d2-139">Cuando Azure termine de implementar la aplicación web, haga clic en la **dirección URL** en la página de configuración de la aplicación web en Azure o escriba la dirección URL en un explorador web.</span><span class="sxs-lookup"><span data-stu-id="e74d2-139">When Azure has finished deploying the web app, click the **URL** on the web app settings page in Azure, or enter the URL in a web browser.</span></span> <span data-ttu-id="e74d2-140">Por ejemplo, `http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="e74d2-140">For example, `http://carprediction.azurewebsites.net.`</span></span>
5. <span data-ttu-id="e74d2-141">Cuando se ejecute la aplicación web por primera vez, le pedirá la **dirección URL del mensaje de API** y **clave de API**.</span><span class="sxs-lookup"><span data-stu-id="e74d2-141">When the web app first runs it will ask you for the **API Post URL** and **API Key**.</span></span>
   <span data-ttu-id="e74d2-142">Escriba los valores que guardó anteriormente (**URI de solicitud** y **Clave de API**, respectivamente).</span><span class="sxs-lookup"><span data-stu-id="e74d2-142">Enter the values you saved earlier (**Request URI** and **API Key**, respectively).</span></span>
     
     <span data-ttu-id="e74d2-143">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="e74d2-143">Click **Submit**.</span></span>
     
     ![Escriba el URI del mensaje y la clave de API][image6]

6. <span data-ttu-id="e74d2-145">La aplicación web muestra su página **Configuración de la aplicación web** con la configuración actual del servicio web.</span><span class="sxs-lookup"><span data-stu-id="e74d2-145">The web app displays its **Web App Configuration** page with the current web service settings.</span></span> <span data-ttu-id="e74d2-146">Aquí puede realizar cambios en la configuración usada por la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="e74d2-146">Here you can make changes to the settings used by the web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e74d2-147">El cambio de estas opciones solo las cambia para esta aplicación web.</span><span class="sxs-lookup"><span data-stu-id="e74d2-147">Changing the settings here only changes them for this web app.</span></span> <span data-ttu-id="e74d2-148">No cambia la configuración predeterminada del servicio web.</span><span class="sxs-lookup"><span data-stu-id="e74d2-148">It doesn't change the default settings of your web service.</span></span> <span data-ttu-id="e74d2-149">Por ejemplo, si cambia la **Descripción** aquí no cambia la descripción mostrada en el panel del servicio web en Estudio de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="e74d2-149">For example, if you change the **Description** here it doesn't change the description shown on the web service dashboard in Machine Learning Studio.</span></span>
   > 
   > 
   
    <span data-ttu-id="e74d2-150">Cuando termine, haga clic en **Guardar cambios** y, luego, haga clic en **Ir a la página principal**.</span><span class="sxs-lookup"><span data-stu-id="e74d2-150">When you're done, click **Save changes**, and then click **Go to Home Page**.</span></span>

7. <span data-ttu-id="e74d2-151">En la página principal puede escribir valores para enviar al servicio web.</span><span class="sxs-lookup"><span data-stu-id="e74d2-151">From the home page you can enter values to send to your web service.</span></span> <span data-ttu-id="e74d2-152">Cuando termine, haga clic en **Enviar** y se generará el resultado.</span><span class="sxs-lookup"><span data-stu-id="e74d2-152">Click **Submit** when you're done, and the result will be returned.</span></span>

<span data-ttu-id="e74d2-153">Si desea volver a la página **Configuración**, vaya a la página `setting.aspx` de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="e74d2-153">If you want to return to the **Configuration** page, go to the `setting.aspx` page of the web app.</span></span> <span data-ttu-id="e74d2-154">Por ejemplo: `http://carprediction.azurewebsites.net/setting.aspx.` le pedirá que vuelva a escribir la clave de API, lo que es necesario para tener acceso a la página y actualizar la configuración.</span><span class="sxs-lookup"><span data-stu-id="e74d2-154">For example: `http://carprediction.azurewebsites.net/setting.aspx.` You will be prompted to enter the API key again - you need that to access the page and update the settings.</span></span>

<span data-ttu-id="e74d2-155">Puede detener, reiniciar o eliminar la aplicación web en el Portal de Azure como cualquier otra aplicación web.</span><span class="sxs-lookup"><span data-stu-id="e74d2-155">You can stop, restart, or delete the web app in the Azure portal like any other web app.</span></span> <span data-ttu-id="e74d2-156">Mientras se esté ejecutando, puede ir a la dirección web de inicio y escribir los nuevos valores.</span><span class="sxs-lookup"><span data-stu-id="e74d2-156">As long as it is running you can browse to the home web address and enter new values.</span></span>

## <a name="how-to-use-the-batch-execution-service-bes-template"></a><span data-ttu-id="e74d2-157">Uso de la plantilla Batch Execution Service (BES)</span><span class="sxs-lookup"><span data-stu-id="e74d2-157">How to use the Batch Execution Service (BES) template</span></span>
<span data-ttu-id="e74d2-158">Puede usar la plantilla de aplicación web BES de la misma manera que la plantilla RRS, excepto que la aplicación web que se crea permite enviar varias filas de datos y recibir varios resultados.</span><span class="sxs-lookup"><span data-stu-id="e74d2-158">You can use the BES web app template in the same way as the RRS template, except that the web app that's created will allow you to submit multiple rows of data and receive multiple results.</span></span>

<span data-ttu-id="e74d2-159">Los valores de entrada de un servicio web de ejecución de lotes pueden provenir de Azure Storage o un archivo local; los resultados se almacenan en un contenedor de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="e74d2-159">The input values for a batch execution web service can come from Azure storage or a local file; the results are stored in an Azure storage container.</span></span>
<span data-ttu-id="e74d2-160">Por lo tanto, necesitará un contenedor de almacenamiento de Azure para guardar los resultados devueltos por la aplicación web, y deberá preparar los datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="e74d2-160">So, you'll need an Azure storage container to hold the results returned by the web app, and you'll need to get your input data ready.</span></span>

![Proceso para usar la plantilla web BES][image2]

1. <span data-ttu-id="e74d2-162">Siga el mismo procedimiento para crear la aplicación web de BES como lo hizo para la plantilla de RRS, excepto que debe ir a [Plantilla de aplicación web Servicio de ejecución de lotes de Azure ML](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) para abrir la plantilla BES en Azure Marketplace y haga clic en **Crear aplicación web**.</span><span class="sxs-lookup"><span data-stu-id="e74d2-162">Follow the same procedure to create the BES web app as for the RRS template, except go to [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) to open the BES template on Azure Marketplace and click **Create Web App**.</span></span>

2. <span data-ttu-id="e74d2-163">Para especificar dónde desea que se almacenen los resultados, escriba la información del contenedor de destino en la página principal de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="e74d2-163">To specify where you want the results stored, enter the destination container information on the web app home page.</span></span> <span data-ttu-id="e74d2-164">Especifique también dónde puede obtener los valores de entrada la aplicación web, en un archivo local o en un contenedor de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="e74d2-164">Also specify where the web app can get the input values, either in a local file or an Azure storage container.</span></span>
   <span data-ttu-id="e74d2-165">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="e74d2-165">Click **Submit**.</span></span>
   
    ![Información de almacenamiento][image7]

<span data-ttu-id="e74d2-167">La aplicación web mostrará una página con el estado del trabajo.</span><span class="sxs-lookup"><span data-stu-id="e74d2-167">The web app will display a page with job status.</span></span>
<span data-ttu-id="e74d2-168">Cuando se haya completado el trabajo, se le proporcionará la ubicación de los resultados en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="e74d2-168">When the job has completed you'll be given the location of the results in Azure blob storage.</span></span> <span data-ttu-id="e74d2-169">También tiene la opción de descargar los resultados en un archivo local.</span><span class="sxs-lookup"><span data-stu-id="e74d2-169">You also have the option of downloading the results to a local file.</span></span>

## <a name="for-more-information"></a><span data-ttu-id="e74d2-170">Para obtener más información</span><span class="sxs-lookup"><span data-stu-id="e74d2-170">For more information</span></span>
<span data-ttu-id="e74d2-171">Para obtener más información sobre...</span><span class="sxs-lookup"><span data-stu-id="e74d2-171">To learn more about...</span></span>

* <span data-ttu-id="e74d2-172">la creación de un experimento de aprendizaje automático con Estudio de aprendizaje automático, consulte [Creación del primer experimento en Estudio de aprendizaje automático de Azure](machine-learning-create-experiment.md)</span><span class="sxs-lookup"><span data-stu-id="e74d2-172">creating a machine learning experiment with Machine Learning Studio, see [Create your first experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md)</span></span>
* <span data-ttu-id="e74d2-173">cómo implementar el experimento de aprendizaje automático como un servicio web, consulte [Implementación de un servicio web de Aprendizaje automático de Azure](machine-learning-publish-a-machine-learning-web-service.md)</span><span class="sxs-lookup"><span data-stu-id="e74d2-173">how to deploy your machine learning experiment as a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md)</span></span>
* <span data-ttu-id="e74d2-174">otras formas de tener acceso al servicio web, consulte [Consumo de servicios web Azure Machine Learning](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="e74d2-174">other ways to access your web service, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md)</span></span>

[image1]: media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/machine-learning-consume-web-service-with-web-app-template/storage.png
