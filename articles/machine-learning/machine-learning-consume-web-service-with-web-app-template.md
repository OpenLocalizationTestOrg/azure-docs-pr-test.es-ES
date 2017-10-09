---
title: "un servicio web de aprendizaje automático con una plantilla de aplicación web aaaConsume | Documentos de Microsoft"
description: "Usar una plantilla de aplicación web en Azure Marketplace tooconsume un servicio web de predicción en aprendizaje automático de Azure."
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
ms.openlocfilehash: 1199377bead470807d58ca7f7a667175cbb88450
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a><span data-ttu-id="cedf5-104">Consumo de un servicio web de Aprendizaje automático de Azure con una plantilla de aplicación web</span><span class="sxs-lookup"><span data-stu-id="cedf5-104">Consume an Azure Machine Learning web service with a web app template</span></span>

<span data-ttu-id="cedf5-105">Una vez haya desarrollado el modelo de predicción e implementarla como un servicio web de Azure con estudio de aprendizaje automático, o mediante herramientas como R o Python, puede tener acceso mediante una API de REST de modelo operaciones Hola.</span><span class="sxs-lookup"><span data-stu-id="cedf5-105">Once you've developed your predictive model and deployed it as an Azure web service using Machine Learning Studio, or using tools such as R or Python, you can access hello operationalized model using a REST API.</span></span>

<span data-ttu-id="cedf5-106">Hay varias maneras de tooconsume Hola API de REST de servicio y acceso hello web.</span><span class="sxs-lookup"><span data-stu-id="cedf5-106">There are a number of ways tooconsume hello REST API and access hello web service.</span></span> <span data-ttu-id="cedf5-107">Por ejemplo, puede escribir una aplicación en C#, R, o código generado automáticamente cuando implementa el servicio web de Hola de ejemplo de Python con hello (disponible en hello [Portal de servicios Web de aprendizaje de máquina](https://services.azureml.net/quickstart) o en el panel de servicio web de hello en Estudio de aprendizaje automático).</span><span class="sxs-lookup"><span data-stu-id="cedf5-107">For example, you can write an application in C#, R, or Python using hello sample code generated for you when you deployed hello web service (available in hello [Machine Learning Web Services Portal](https://services.azureml.net/quickstart) or in hello web service dashboard in Machine Learning Studio).</span></span> <span data-ttu-id="cedf5-108">O bien puede usar el libro de Microsoft Excel de ejemplo de Hola creado para usted en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="cedf5-108">Or you can use hello sample Microsoft Excel workbook created for you at hello same time.</span></span>

<span data-ttu-id="cedf5-109">Pero Hola tooaccess de forma más rápida y más fácil su servicio web es a través de plantillas de aplicación de hello Web disponibles en hello [Marketplace de aplicaciones Web de Azure](https://azure.microsoft.com/marketplace/web-applications/all/).</span><span class="sxs-lookup"><span data-stu-id="cedf5-109">But hello quickest and easiest way tooaccess your web service is through hello Web App Templates available in hello [Azure Web App Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-azure-machine-learning-web-app-templates"></a><span data-ttu-id="cedf5-110">Hola plantillas de aplicaciones de Web de aprendizaje de máquina de Azure</span><span class="sxs-lookup"><span data-stu-id="cedf5-110">hello Azure Machine Learning Web App Templates</span></span>
<span data-ttu-id="cedf5-111">plantillas de aplicación de Hello web disponibles en hello Azure Marketplace pueden compilar una aplicación web personalizada que conoce los datos de entrada de su servicio web y los resultados esperados.</span><span class="sxs-lookup"><span data-stu-id="cedf5-111">hello web app templates available in hello Azure Marketplace can build a custom web app that knows your web service's input data and expected results.</span></span> <span data-ttu-id="cedf5-112">Todo lo que necesita toodo es proporcionar datos y servicio web de tooyour de acceso de aplicación de hello web y plantilla de Hola Hola rest.</span><span class="sxs-lookup"><span data-stu-id="cedf5-112">All you need toodo is give hello web app access tooyour web service and data, and hello template does hello rest.</span></span>

<span data-ttu-id="cedf5-113">Existen dos plantillas:</span><span class="sxs-lookup"><span data-stu-id="cedf5-113">Two templates are available:</span></span>

* [<span data-ttu-id="cedf5-114">Plantilla de aplicación web Request-Response Service de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="cedf5-114">Azure ML Request-Response Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [<span data-ttu-id="cedf5-115">Plantilla de aplicación web Batch Execution Service de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="cedf5-115">Azure ML Batch Execution Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

<span data-ttu-id="cedf5-116">Cada plantilla crea una aplicación de ASP.NET de ejemplo, mediante Hola URI de API y la clave para el servicio web e implementa como un tooAzure de sitio web.</span><span class="sxs-lookup"><span data-stu-id="cedf5-116">Each template creates a sample ASP.NET application, using hello API URI and Key for your web service, and deploys it as a web site tooAzure.</span></span> <span data-ttu-id="cedf5-117">plantilla de servicio de solicitud-respuesta (RR) de Hello crea una aplicación web que le permite toosend una sola fila de datos toohello web servicio tooget un único resultado.</span><span class="sxs-lookup"><span data-stu-id="cedf5-117">hello Request-Response Service (RRS) template creates a web app that allows you toosend a single row of data toohello web service tooget a single result.</span></span> <span data-ttu-id="cedf5-118">plantilla de servicio de ejecución de lotes (BES) de Hello crea una aplicación web que le permite toosend muchas filas de datos tooget varios resultados.</span><span class="sxs-lookup"><span data-stu-id="cedf5-118">hello Batch Execution Service (BES) template creates a web app that allows you toosend many rows of data tooget multiple results.</span></span>

<span data-ttu-id="cedf5-119">Ninguna codificación es necesario toouse estas plantillas.</span><span class="sxs-lookup"><span data-stu-id="cedf5-119">No coding is required toouse these templates.</span></span> <span data-ttu-id="cedf5-120">Basta con proporcionar Hola clave de API y el URI y plantilla Hola compila la aplicación hello automáticamente.</span><span class="sxs-lookup"><span data-stu-id="cedf5-120">You just supply hello API Key and URI, and hello template builds hello application for you.</span></span>

<span data-ttu-id="cedf5-121">clave de API de hello tooget y URI de la solicitud para un servicio web:</span><span class="sxs-lookup"><span data-stu-id="cedf5-121">tooget hello API key and Request URI for a web service:</span></span>

1. <span data-ttu-id="cedf5-122">Hola [Portal de servicios Web](https://services.azureml.net/quickstart), para un nuevo servicio web, haga clic en **servicios Web** en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="cedf5-122">In hello [Web Services Portal](https://services.azureml.net/quickstart), for a New web service, click **Web Services** at hello top.</span></span> <span data-ttu-id="cedf5-123">O bien, para un servicio web clásico, haga clic en **Servicios web clásicos**.</span><span class="sxs-lookup"><span data-stu-id="cedf5-123">Or for a Classic web service click **Classic Web Services**.</span></span>
2. <span data-ttu-id="cedf5-124">Haga clic en el servicio de web de Hola que desee tooaccess.</span><span class="sxs-lookup"><span data-stu-id="cedf5-124">Click hello web service you want tooaccess.</span></span>
3. <span data-ttu-id="cedf5-125">Para un servicio web clásico, haga clic en punto de conexión de hello desea tooaccess.</span><span class="sxs-lookup"><span data-stu-id="cedf5-125">For a Classic web service, click hello endpoint you want tooaccess.</span></span>
4. <span data-ttu-id="cedf5-126">Haga clic en **Consume** en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="cedf5-126">Click **Consume** at hello top.</span></span>
5. <span data-ttu-id="cedf5-127">Hola copia **principal** o **clave secundaria** y guárdelo.</span><span class="sxs-lookup"><span data-stu-id="cedf5-127">Copy hello **Primary** or **Secondary Key** and save it.</span></span>
6. <span data-ttu-id="cedf5-128">Si está creando una plantilla de servicio de solicitud-respuesta (RR), copie hello **solicitud-respuesta** URI y guárdelo.</span><span class="sxs-lookup"><span data-stu-id="cedf5-128">If you're creating a Request-Response Service (RRS) template, copy hello **Request-Response** URI and save it.</span></span> <span data-ttu-id="cedf5-129">Si está creando una plantilla de servicio de ejecución de lotes (BES), copie hello **solicitudes por lotes** URI y guárdelo.</span><span class="sxs-lookup"><span data-stu-id="cedf5-129">If you're creating a Batch Execution Service (BES) template, copy hello **Batch Requests** URI and save it.</span></span>


## <a name="how-toouse-hello-request-response-service-rrs-template"></a><span data-ttu-id="cedf5-130">¿Cómo toouse Hola plantilla de servicio de solicitud-respuesta (RR)</span><span class="sxs-lookup"><span data-stu-id="cedf5-130">How toouse hello Request-Response Service (RRS) template</span></span>
<span data-ttu-id="cedf5-131">Siga estos plantilla pasos toouse Hola RR web app, como se muestra en hello siguiente diagrama.</span><span class="sxs-lookup"><span data-stu-id="cedf5-131">Follow these steps toouse hello RRS web app template, as shown in hello following diagram.</span></span>

![Plantilla de proceso toouse RR web][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. <span data-ttu-id="cedf5-133">Vaya toohello [portal de Azure](https://portal.azure.com), **inicio de sesión**, haga clic en **New**, busque y seleccione **Azure ML solicitudes y respuestas Web del servicio de aplicaciones**, a continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="cedf5-133">Go toohello [Azure portal](https://portal.azure.com), **Login**, click **New**, search for and select **Azure ML Request-Response Service Web App**, then click **Create**.</span></span> 
   
   * <span data-ttu-id="cedf5-134">Asigne un nombre único a la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="cedf5-134">Give your web app a unique name.</span></span> <span data-ttu-id="cedf5-135">dirección URL de Hola de aplicación web de hello será este nombre seguido de `.azurewebsites.net.` por ejemplo,`http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="cedf5-135">hello URL of hello web app will be this name followed by `.azurewebsites.net.` For example, `http://carprediction.azurewebsites.net.`</span></span>
   * <span data-ttu-id="cedf5-136">Seleccione Hola suscripción de Azure y servicios en la que se ejecuta el servicio web.</span><span class="sxs-lookup"><span data-stu-id="cedf5-136">Select hello Azure subscription and services under which your web service is running.</span></span>
   * <span data-ttu-id="cedf5-137">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="cedf5-137">Click **Create**.</span></span>
     
     ![Crear una aplicación web][image5]

4. <span data-ttu-id="cedf5-139">Cuando Azure ha terminado de implementar la aplicación web de hello, haga clic en hello **URL** Hola página de configuración de aplicación web en Azure, o escriba la dirección URL de hello en un explorador web.</span><span class="sxs-lookup"><span data-stu-id="cedf5-139">When Azure has finished deploying hello web app, click hello **URL** on hello web app settings page in Azure, or enter hello URL in a web browser.</span></span> <span data-ttu-id="cedf5-140">Por ejemplo: `http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="cedf5-140">For example, `http://carprediction.azurewebsites.net.`</span></span>
5. <span data-ttu-id="cedf5-141">Cuando Hola aplicación de web primero se ejecuta le pedirá hello **URL de entrada de la API** y **clave de API**.</span><span class="sxs-lookup"><span data-stu-id="cedf5-141">When hello web app first runs it will ask you for hello **API Post URL** and **API Key**.</span></span>
   <span data-ttu-id="cedf5-142">Escriba los valores de hello guardó anteriormente (**URI de solicitud** y **clave de API**, respectivamente).</span><span class="sxs-lookup"><span data-stu-id="cedf5-142">Enter hello values you saved earlier (**Request URI** and **API Key**, respectively).</span></span>
     
     <span data-ttu-id="cedf5-143">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="cedf5-143">Click **Submit**.</span></span>
     
     ![Escriba el URI del mensaje y la clave de API][image6]

6. <span data-ttu-id="cedf5-145">Hola de aplicación web se muestra su **configuración de la aplicación Web** página con la configuración del servicio web actual Hola.</span><span class="sxs-lookup"><span data-stu-id="cedf5-145">hello web app displays its **Web App Configuration** page with hello current web service settings.</span></span> <span data-ttu-id="cedf5-146">Aquí puede realizar cambios toohello configuración de aplicación web de hello.</span><span class="sxs-lookup"><span data-stu-id="cedf5-146">Here you can make changes toohello settings used by hello web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="cedf5-147">Estas opciones de hello solo si se cambia su para esta aplicación web.</span><span class="sxs-lookup"><span data-stu-id="cedf5-147">Changing hello settings here only changes them for this web app.</span></span> <span data-ttu-id="cedf5-148">Configuración predeterminada de Hola de su servicio web no cambia.</span><span class="sxs-lookup"><span data-stu-id="cedf5-148">It doesn't change hello default settings of your web service.</span></span> <span data-ttu-id="cedf5-149">Por ejemplo, si cambia hello **descripción** aquí no cambia la descripción de Hola se muestra en el panel de servicio web de hello en estudio de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="cedf5-149">For example, if you change hello **Description** here it doesn't change hello description shown on hello web service dashboard in Machine Learning Studio.</span></span>
   > 
   > 
   
    <span data-ttu-id="cedf5-150">Cuando haya terminado, haga clic en **guardar cambios**y, a continuación, haga clic en **vaya tooHome página**.</span><span class="sxs-lookup"><span data-stu-id="cedf5-150">When you're done, click **Save changes**, and then click **Go tooHome Page**.</span></span>

7. <span data-ttu-id="cedf5-151">De hello página principal que puede escribir valores de servicio web de toosend tooyour.</span><span class="sxs-lookup"><span data-stu-id="cedf5-151">From hello home page you can enter values toosend tooyour web service.</span></span> <span data-ttu-id="cedf5-152">Haga clic en **enviar** cuando haya terminado, y se devolverá el resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="cedf5-152">Click **Submit** when you're done, and hello result will be returned.</span></span>

<span data-ttu-id="cedf5-153">Si desea que tooreturn toohello **configuración** página, vaya toohello `setting.aspx` página de aplicación web de hello.</span><span class="sxs-lookup"><span data-stu-id="cedf5-153">If you want tooreturn toohello **Configuration** page, go toohello `setting.aspx` page of hello web app.</span></span> <span data-ttu-id="cedf5-154">Por ejemplo: `http://carprediction.azurewebsites.net/setting.aspx.` podrá volver a clave de API de hello tooenter solicitadas: necesita que tooaccess Hola página y actualizar la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="cedf5-154">For example: `http://carprediction.azurewebsites.net/setting.aspx.` You will be prompted tooenter hello API key again - you need that tooaccess hello page and update hello settings.</span></span>

<span data-ttu-id="cedf5-155">Puede detener, reiniciar o eliminar la aplicación web de Hola Hola portal de Azure como cualquier otra aplicación web.</span><span class="sxs-lookup"><span data-stu-id="cedf5-155">You can stop, restart, or delete hello web app in hello Azure portal like any other web app.</span></span> <span data-ttu-id="cedf5-156">Mientras se está ejecutando puede buscar direcciones web principal de toohello y escribir nuevos valores.</span><span class="sxs-lookup"><span data-stu-id="cedf5-156">As long as it is running you can browse toohello home web address and enter new values.</span></span>

## <a name="how-toouse-hello-batch-execution-service-bes-template"></a><span data-ttu-id="cedf5-157">¿Cómo toouse Hola plantilla de servicio de ejecución de lotes (BES)</span><span class="sxs-lookup"><span data-stu-id="cedf5-157">How toouse hello Batch Execution Service (BES) template</span></span>
<span data-ttu-id="cedf5-158">Puede usar hello BES plantilla de aplicación web en hello mismo excepto forma como plantilla de Hola RR, dicha aplicación Hola que se crea, podrá toosubmit varias filas de datos y recibir varios resultados.</span><span class="sxs-lookup"><span data-stu-id="cedf5-158">You can use hello BES web app template in hello same way as hello RRS template, except that hello web app that's created will allow you toosubmit multiple rows of data and receive multiple results.</span></span>

<span data-ttu-id="cedf5-159">los valores de entrada de Hola para un servicio web de ejecución de lotes pueden proceder de almacenamiento de Azure o un archivo local; Hola resultados se almacenan en un contenedor de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="cedf5-159">hello input values for a batch execution web service can come from Azure storage or a local file; hello results are stored in an Azure storage container.</span></span>
<span data-ttu-id="cedf5-160">Por lo tanto, será necesario un toohold del contenedor de almacenamiento de Azure Hola resultados devueltos por la aplicación web de hello, y deberá tooget los datos de entrada listo.</span><span class="sxs-lookup"><span data-stu-id="cedf5-160">So, you'll need an Azure storage container toohold hello results returned by hello web app, and you'll need tooget your input data ready.</span></span>

![Procesar toouse BES plantilla web][image2]

1. <span data-ttu-id="cedf5-162">Seguimiento Hola mismo Hola de toocreate procedimiento BES web app para la plantilla de RR hello, excepto go demasiado[plantilla de aplicación Web de Azure ML lote ejecución servicio](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen Hola plantilla BES en Azure Marketplace y haga clic en **crear aplicación Web** .</span><span class="sxs-lookup"><span data-stu-id="cedf5-162">Follow hello same procedure toocreate hello BES web app as for hello RRS template, except go too[Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen hello BES template on Azure Marketplace and click **Create Web App**.</span></span>

2. <span data-ttu-id="cedf5-163">toospecify donde desea que los resultados de hello almacenados, escriba la información del contenedor de destino de Hola en la página de inicio de aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="cedf5-163">toospecify where you want hello results stored, enter hello destination container information on hello web app home page.</span></span> <span data-ttu-id="cedf5-164">Especificar donde la aplicación web de hello puede obtener valores de entrada de hello, en un archivo local o en un contenedor de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="cedf5-164">Also specify where hello web app can get hello input values, either in a local file or an Azure storage container.</span></span>
   <span data-ttu-id="cedf5-165">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="cedf5-165">Click **Submit**.</span></span>
   
    ![Información de almacenamiento][image7]

<span data-ttu-id="cedf5-167">aplicación web de Hello mostrará una página con el estado del trabajo.</span><span class="sxs-lookup"><span data-stu-id="cedf5-167">hello web app will display a page with job status.</span></span>
<span data-ttu-id="cedf5-168">Cuando se haya completado el trabajo de Hola se le ofrecerán ubicación Hola de resultados de hello en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="cedf5-168">When hello job has completed you'll be given hello location of hello results in Azure blob storage.</span></span> <span data-ttu-id="cedf5-169">También tiene opción de Hola de descarga de archivos local de hello resultados tooa.</span><span class="sxs-lookup"><span data-stu-id="cedf5-169">You also have hello option of downloading hello results tooa local file.</span></span>

## <a name="for-more-information"></a><span data-ttu-id="cedf5-170">Para obtener más información</span><span class="sxs-lookup"><span data-stu-id="cedf5-170">For more information</span></span>
<span data-ttu-id="cedf5-171">más información acerca de toolearn...</span><span class="sxs-lookup"><span data-stu-id="cedf5-171">toolearn more about...</span></span>

* <span data-ttu-id="cedf5-172">la creación de un experimento de aprendizaje automático con Estudio de aprendizaje automático, consulte [Creación del primer experimento en Estudio de aprendizaje automático de Azure](machine-learning-create-experiment.md)</span><span class="sxs-lookup"><span data-stu-id="cedf5-172">creating a machine learning experiment with Machine Learning Studio, see [Create your first experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md)</span></span>
* <span data-ttu-id="cedf5-173">toodeploy experimentar el aprendizaje automático como un servicio web, vea [implementar un servicio web de aprendizaje automático de Azure](machine-learning-publish-a-machine-learning-web-service.md)</span><span class="sxs-lookup"><span data-stu-id="cedf5-173">how toodeploy your machine learning experiment as a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md)</span></span>
* <span data-ttu-id="cedf5-174">otras maneras tooaccess el servicio web, vea [cómo tooconsume un servicio Web de aprendizaje de máquina de Azure](machine-learning-consume-web-services.md)</span><span class="sxs-lookup"><span data-stu-id="cedf5-174">other ways tooaccess your web service, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md)</span></span>

[image1]: media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/machine-learning-consume-web-service-with-web-app-template/storage.png
