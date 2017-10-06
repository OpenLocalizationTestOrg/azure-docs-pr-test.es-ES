---
title: "aaaHow tooconsume un servicio Web de aprendizaje de máquina de Azure | Documentos de Microsoft"
description: "Una vez que se implementa un servicio de aprendizaje automático, servicio Web RESTFul que debe ponerse a disposición de hello puede utilizarse como servicio de solicitudes y respuestas en tiempo real o como un servicio de ejecución por lotes."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 804f8211-9437-4982-98e9-ca841b7edf56
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 06/02/2017
ms.author: garye
ms.openlocfilehash: 19095604169e5af1daed12c17ba66258233178bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconsume-an-azure-machine-learning-web-service"></a><span data-ttu-id="acb47-103">¿Cómo tooconsume un servicio Web de aprendizaje de máquina de Azure</span><span class="sxs-lookup"><span data-stu-id="acb47-103">How tooconsume an Azure Machine Learning Web service</span></span>

<span data-ttu-id="acb47-104">Una vez que implementa un modelo de predicción de aprendizaje automático de Azure como un servicio Web, puede usar una API de REST toosend lo datos y obtener predicciones.</span><span class="sxs-lookup"><span data-stu-id="acb47-104">Once you deploy an Azure Machine Learning predictive model as a Web service, you can use a REST API toosend it data and get predictions.</span></span> <span data-ttu-id="acb47-105">Puede enviar datos de hello en tiempo real o en modo por lotes.</span><span class="sxs-lookup"><span data-stu-id="acb47-105">You can send hello data in real-time or in batch mode.</span></span>

<span data-ttu-id="acb47-106">Puede encontrar más información sobre cómo toocreate e implementar un servicio Web de aprendizaje de máquina mediante el estudio de aprendizaje automático aquí:</span><span class="sxs-lookup"><span data-stu-id="acb47-106">You can find more information about how toocreate and deploy a Machine Learning Web service using Machine Learning Studio here:</span></span>

* <span data-ttu-id="acb47-107">Para obtener un tutorial sobre cómo toocreate un experimento en estudio de aprendizaje automático, consulte [crear su primer experimento](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="acb47-107">For a tutorial on how toocreate an experiment in Machine Learning Studio, see [Create your first experiment](machine-learning-create-experiment.md).</span></span>
* <span data-ttu-id="acb47-108">Para obtener más información acerca de cómo toodeploy un servicio Web, consulte [implementar un servicio Web de aprendizaje de máquina](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="acb47-108">For details on how toodeploy a Web service, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="acb47-109">Para obtener más información acerca de aprendizaje automático, por lo general, visite hello [centro de documentación de aprendizaje de máquina](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="acb47-109">For more information about Machine Learning in general, visit hello [Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview"></a><span data-ttu-id="acb47-110">Información general</span><span class="sxs-lookup"><span data-stu-id="acb47-110">Overview</span></span>
<span data-ttu-id="acb47-111">Con hello servicio Web de aprendizaje de máquina de Azure, una aplicación externa se comunica con un modelo de puntuación de flujo de trabajo de aprendizaje automático en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="acb47-111">With hello Azure Machine Learning Web service, an external application communicates with a Machine Learning workflow scoring model in real time.</span></span> <span data-ttu-id="acb47-112">Una llamada de servicio Web de aprendizaje de máquina devuelve resultados de predicción tooan de aplicación externa.</span><span class="sxs-lookup"><span data-stu-id="acb47-112">A Machine Learning Web service call returns prediction results tooan external application.</span></span> <span data-ttu-id="acb47-113">toomake una llamada de servicio Web de aprendizaje de máquina, se pasa una clave de API que se crea al implementar una predicción.</span><span class="sxs-lookup"><span data-stu-id="acb47-113">toomake a Machine Learning Web service call, you pass an API key that is created when you deploy a prediction.</span></span> <span data-ttu-id="acb47-114">Hola servicio Web de aprendizaje de máquina está basado en REST, una opción de arquitectura populares para proyectos de programación web.</span><span class="sxs-lookup"><span data-stu-id="acb47-114">hello Machine Learning Web service is based on REST, a popular architecture choice for web programming projects.</span></span>

<span data-ttu-id="acb47-115">Aprendizaje automático de Azure tiene dos tipos de servicios:</span><span class="sxs-lookup"><span data-stu-id="acb47-115">Azure Machine Learning has two types of services:</span></span>

* <span data-ttu-id="acb47-116">Servicio de respuesta de solicitud (RR): una latencia baja, el servicio altamente escalable que ofrece una interfaz toohello sin estado modelos creado e implementado de hello estudio de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="acb47-116">Request-Response Service (RRS) – A low latency, highly scalable service that provides an interface toohello stateless models created and deployed from hello Machine Learning Studio.</span></span>
* <span data-ttu-id="acb47-117">Servicio de ejecución por lotes (BES): servicio asincrónico que puntúa un lote de registros de datos.</span><span class="sxs-lookup"><span data-stu-id="acb47-117">Batch Execution Service (BES) – An asynchronous service that scores a batch for data records.</span></span>

<span data-ttu-id="acb47-118">Para más información sobre los servicios web Machine Learning, consulte [Implementación de un servicio web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="acb47-118">For more information about Machine Learning Web services, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="get-an-azure-machine-learning-authorization-key"></a><span data-ttu-id="acb47-119">Obtener una clave de autorización de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="acb47-119">Get an Azure Machine Learning authorization key</span></span>
<span data-ttu-id="acb47-120">Cuando se implementa el experimento, se generan claves de API para hello servicio Web.</span><span class="sxs-lookup"><span data-stu-id="acb47-120">When you deploy your experiment, API keys are generated for hello Web service.</span></span> <span data-ttu-id="acb47-121">Puede recuperar las claves de Hola desde varias ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="acb47-121">You can retrieve hello keys from several locations.</span></span>

### <a name="from-hello-microsoft-azure-machine-learning-web-services-portal"></a><span data-ttu-id="acb47-122">Desde el portal de servicios Web de Microsoft Azure Machine Learning Hola</span><span class="sxs-lookup"><span data-stu-id="acb47-122">From hello Microsoft Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="acb47-123">Inicie sesión en toohello [servicios Web de Microsoft Azure Machine Learning](https://services.azureml.net) portal.</span><span class="sxs-lookup"><span data-stu-id="acb47-123">Sign in toohello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span>

<span data-ttu-id="acb47-124">clave de API hello tooretrieve para un servicio Web de aprendizaje de máquina nueva:</span><span class="sxs-lookup"><span data-stu-id="acb47-124">tooretrieve hello API key for a New Machine Learning Web service:</span></span>

1. <span data-ttu-id="acb47-125">En el portal de servicios Web de Azure Machine Learning hello, haga clic en **servicios Web** menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="acb47-125">In hello Azure Machine Learning Web Services portal, click **Web Services** hello top menu.</span></span>
2. <span data-ttu-id="acb47-126">Haga clic en el servicio Web de hello para el que desea que clave de hello tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="acb47-126">Click hello Web service for which you want tooretrieve hello key.</span></span>
3. <span data-ttu-id="acb47-127">En el menú superior de hello, haga clic en **usar**.</span><span class="sxs-lookup"><span data-stu-id="acb47-127">On hello top menu, click **Consume**.</span></span>
4. <span data-ttu-id="acb47-128">Copie y guarde hello **Primary Key**.</span><span class="sxs-lookup"><span data-stu-id="acb47-128">Copy and save hello **Primary Key**.</span></span>

<span data-ttu-id="acb47-129">clave de API de hello tooretrieve para un servicio Web de aprendizaje de máquina clásico:</span><span class="sxs-lookup"><span data-stu-id="acb47-129">tooretrieve hello API key for a Classic Machine Learning Web service:</span></span>

1. <span data-ttu-id="acb47-130">En el portal de servicios Web de Azure Machine Learning hello, haga clic en **servicios Web clásico** menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="acb47-130">In hello Azure Machine Learning Web Services portal, click **Classic Web Services** hello top menu.</span></span>
2. <span data-ttu-id="acb47-131">Haga clic en el servicio Web de hello con el que está trabajando.</span><span class="sxs-lookup"><span data-stu-id="acb47-131">Click hello Web service with which you are working.</span></span>
3. <span data-ttu-id="acb47-132">Haga clic en el punto de conexión de hello para el que desea que clave de hello tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="acb47-132">Click hello endpoint for which you want tooretrieve hello key.</span></span>
4. <span data-ttu-id="acb47-133">En el menú superior de hello, haga clic en **usar**.</span><span class="sxs-lookup"><span data-stu-id="acb47-133">On hello top menu, click **Consume**.</span></span>
5. <span data-ttu-id="acb47-134">Copie y guarde hello **Primary Key**.</span><span class="sxs-lookup"><span data-stu-id="acb47-134">Copy and save hello **Primary Key**.</span></span>

### <a name="classic-web-service"></a><span data-ttu-id="acb47-135">Servicio web clásico</span><span class="sxs-lookup"><span data-stu-id="acb47-135">Classic Web service</span></span>
 <span data-ttu-id="acb47-136">También puede recuperar una clave para un servicio Web clásico de estudio de aprendizaje automático o hello portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="acb47-136">You can also retrieve a key for a Classic Web service from Machine Learning Studio or hello Azure classic portal.</span></span>

#### <a name="machine-learning-studio"></a><span data-ttu-id="acb47-137">Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="acb47-137">Machine Learning Studio</span></span>
1. <span data-ttu-id="acb47-138">En estudio de aprendizaje automático, haga clic en **servicios WEB** de hello izquierda.</span><span class="sxs-lookup"><span data-stu-id="acb47-138">In Machine Learning Studio, click **WEB SERVICES** on hello left.</span></span>
2. <span data-ttu-id="acb47-139">Haga clic en un servicio web.</span><span class="sxs-lookup"><span data-stu-id="acb47-139">Click a Web service.</span></span> <span data-ttu-id="acb47-140">Hola **clave de API** en hello **panel** ficha.</span><span class="sxs-lookup"><span data-stu-id="acb47-140">hello **API key** is on hello **DASHBOARD** tab.</span></span>

#### <a name="azure-classic-portal"></a><span data-ttu-id="acb47-141">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="acb47-141">Azure classic portal</span></span>
1. <span data-ttu-id="acb47-142">Haga clic en **aprendizaje automático** de hello izquierda.</span><span class="sxs-lookup"><span data-stu-id="acb47-142">Click **MACHINE LEARNING** on hello left.</span></span>
2. <span data-ttu-id="acb47-143">Haga clic en el área de trabajo de hello en el que se encuentra el servicio Web.</span><span class="sxs-lookup"><span data-stu-id="acb47-143">Click hello workspace in which your Web service is located.</span></span>
3. <span data-ttu-id="acb47-144">Haga clic en **SERVICIOS WEB**.</span><span class="sxs-lookup"><span data-stu-id="acb47-144">Click **WEB SERVICES**.</span></span>
4. <span data-ttu-id="acb47-145">Haga clic en un servicio web.</span><span class="sxs-lookup"><span data-stu-id="acb47-145">Click a Web service.</span></span>
5. <span data-ttu-id="acb47-146">Haga clic en un extremo.</span><span class="sxs-lookup"><span data-stu-id="acb47-146">Click an endpoint.</span></span> <span data-ttu-id="acb47-147">Hola "Clave de API" está inactivo en hello inferior derecha.</span><span class="sxs-lookup"><span data-stu-id="acb47-147">hello “API KEY” is down at hello lower-right.</span></span>

## <span data-ttu-id="acb47-148"><a id="connect"></a>Conectar el servicio Web de aprendizaje de máquina tooa</span><span class="sxs-lookup"><span data-stu-id="acb47-148"><a id="connect"></a>Connect tooa Machine Learning Web service</span></span>
<span data-ttu-id="acb47-149">Puede conectarse tooa servicio Web de aprendizaje de máquina mediante cualquier lenguaje de programación que admita la respuesta y solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="acb47-149">You can connect tooa Machine Learning Web service using any programming language that supports HTTP request and response.</span></span> <span data-ttu-id="acb47-150">Puede ver ejemplos en C#, Python y R desde una página de ayuda de servicio web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="acb47-150">You can view examples in C#, Python, and R from a Machine Learning Web service help page.</span></span>

<span data-ttu-id="acb47-151">**Ayuda de la API de Machine Learning** Se crea una página de ayuda de API de Machine Learning al implementar un servicio web.</span><span class="sxs-lookup"><span data-stu-id="acb47-151">**Machine Learning API help** Machine Learning API help is created when you deploy a Web service.</span></span> <span data-ttu-id="acb47-152">Vea [Tutorial de Aprendizaje automático de Azure: Implementación de un servicio web](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="acb47-152">See [Azure Machine Learning Walkthrough- Deploy Web Service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
<span data-ttu-id="acb47-153">Hola ayuda de API de aprendizaje de máquina contiene detalles acerca de una servicio Web de predicción.</span><span class="sxs-lookup"><span data-stu-id="acb47-153">hello Machine Learning API help contains details about a prediction Web service.</span></span>

1. <span data-ttu-id="acb47-154">Haga clic en el servicio Web de hello con el que está trabajando.</span><span class="sxs-lookup"><span data-stu-id="acb47-154">Click hello Web service with which you are working.</span></span>
2. <span data-ttu-id="acb47-155">Haga clic en el punto de conexión de hello para el que desea tooview Hola página de Ayuda de API.</span><span class="sxs-lookup"><span data-stu-id="acb47-155">Click hello endpoint for which you want tooview hello API Help Page.</span></span>
3. <span data-ttu-id="acb47-156">En el menú superior de hello, haga clic en **usar**.</span><span class="sxs-lookup"><span data-stu-id="acb47-156">On hello top menu, click **Consume**.</span></span>
4. <span data-ttu-id="acb47-157">Haga clic en **página de Ayuda de API** en hello solicitud-respuesta o puntos de conexión de la ejecución por lotes.</span><span class="sxs-lookup"><span data-stu-id="acb47-157">Click **API help page** under either hello Request-Response or Batch Execution endpoints.</span></span>

<span data-ttu-id="acb47-158">**Ayuda de API de aprendizaje de máquina de tooview para un servicio Web nuevo**</span><span class="sxs-lookup"><span data-stu-id="acb47-158">**tooview Machine Learning API help for a New Web service**</span></span>

<span data-ttu-id="acb47-159">Hola Portal de servicios de Web de aprendizaje de máquina de Azure:</span><span class="sxs-lookup"><span data-stu-id="acb47-159">In hello Azure Machine Learning Web Services Portal:</span></span>

1. <span data-ttu-id="acb47-160">Haga clic en **servicios WEB** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="acb47-160">Click **WEB SERVICES** on hello top menu.</span></span>
2. <span data-ttu-id="acb47-161">Haga clic en el servicio Web de hello para el que desea que clave de hello tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="acb47-161">Click hello Web service for which you want tooretrieve hello key.</span></span>

<span data-ttu-id="acb47-162">Haga clic en **Consume** tooget Hola URI hello Reposonse de solicitud y servicios de ejecución por lotes y código de ejemplo en C#, R y Python.</span><span class="sxs-lookup"><span data-stu-id="acb47-162">Click **Consume** tooget hello URIs for hello Request-Reposonse and Batch Execution Services and Sample code in C#, R, and Python.</span></span>

<span data-ttu-id="acb47-163">Haga clic en **Swagger API** tooget Swagger documentación en función de hello las API que se llama desde Hola proporcionado URI.</span><span class="sxs-lookup"><span data-stu-id="acb47-163">Click **Swagger API** tooget Swagger based documentation for hello APIs called from hello supplied URIs.</span></span>

### <a name="c-sample"></a><span data-ttu-id="acb47-164">Ejemplo de C#</span><span class="sxs-lookup"><span data-stu-id="acb47-164">C# Sample</span></span>
<span data-ttu-id="acb47-165">tooconnect tooa servicio Web de aprendizaje de máquina, utilice un **HttpClient** pasar ScoreData.</span><span class="sxs-lookup"><span data-stu-id="acb47-165">tooconnect tooa Machine Learning Web service, use an **HttpClient** passing ScoreData.</span></span> <span data-ttu-id="acb47-166">ScoreData contiene un FeatureVector, un vector de n dimensiones de características numéricos que representa hello ScoreData.</span><span class="sxs-lookup"><span data-stu-id="acb47-166">ScoreData contains a FeatureVector, an n-dimensional vector of numerical features that represents hello ScoreData.</span></span> <span data-ttu-id="acb47-167">Servicio de aprendizaje automático de toohello, autenticarse con una clave de API.</span><span class="sxs-lookup"><span data-stu-id="acb47-167">You authenticate toohello Machine Learning service with an API key.</span></span>

<span data-ttu-id="acb47-168">Hola tooconnect tooa servicio Web de aprendizaje de máquina, **Microsoft.AspNet.WebApi.Client** debe estar instalado el paquete de NuGet.</span><span class="sxs-lookup"><span data-stu-id="acb47-168">tooconnect tooa Machine Learning Web service, hello **Microsoft.AspNet.WebApi.Client** NuGet package must be installed.</span></span>

<span data-ttu-id="acb47-169">**Instalar Microsoft.AspNet.WebApi.Client NuGet en Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="acb47-169">**Install Microsoft.AspNet.WebApi.Client NuGet in Visual Studio**</span></span>

1. <span data-ttu-id="acb47-170">Publicar el conjunto de datos de descarga de Hola de UCI: conjunto de datos de clase de 2 para adultos servicio Web.</span><span class="sxs-lookup"><span data-stu-id="acb47-170">Publish hello Download dataset from UCI: Adult 2 class dataset Web Service.</span></span>
2. <span data-ttu-id="acb47-171">Haga clic en **Herramientas** > **Administrador de paquetes NuGet** > **Consola del administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="acb47-171">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="acb47-172">Elija **Install-Package Microsoft.AspNet.WebApi.Client**.</span><span class="sxs-lookup"><span data-stu-id="acb47-172">Choose **Install-Package Microsoft.AspNet.WebApi.Client**.</span></span>

<span data-ttu-id="acb47-173">**ejemplo de código de hello toorun**</span><span class="sxs-lookup"><span data-stu-id="acb47-173">**toorun hello code sample**</span></span>

1. <span data-ttu-id="acb47-174">Publicar "ejemplo 1: descargar el conjunto de datos de UCI: conjunto de datos de contenido para adultos 2 clase" experimento, parte de la colección de aprendizaje automático de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="acb47-174">Publish "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of hello Machine Learning sample collection.</span></span>
2. <span data-ttu-id="acb47-175">Asignar apiKey con clave de Hola desde un servicio Web.</span><span class="sxs-lookup"><span data-stu-id="acb47-175">Assign apiKey with hello key from a Web service.</span></span> <span data-ttu-id="acb47-176">Consulte el apartado anterior **Obtener una clave de autorización de Aprendizaje automático de Azure** .</span><span class="sxs-lookup"><span data-stu-id="acb47-176">See **Get an Azure Machine Learning authorization key** above.</span></span>
3. <span data-ttu-id="acb47-177">Asignar serviceUri con hello URI de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="acb47-177">Assign serviceUri with hello Request URI.</span></span>

### <a name="python-sample"></a><span data-ttu-id="acb47-178">Ejemplo de Python</span><span class="sxs-lookup"><span data-stu-id="acb47-178">Python Sample</span></span>
<span data-ttu-id="acb47-179">tooconnect tooa servicio Web de aprendizaje de máquina, utilice hello **urllib2** biblioteca pasar ScoreData.</span><span class="sxs-lookup"><span data-stu-id="acb47-179">tooconnect tooa Machine Learning Web service, use hello **urllib2** library passing ScoreData.</span></span> <span data-ttu-id="acb47-180">ScoreData contiene un FeatureVector, un vector de n dimensiones de características numéricos que representa hello ScoreData.</span><span class="sxs-lookup"><span data-stu-id="acb47-180">ScoreData contains a FeatureVector, an n-dimensional  vector of numerical features that represents hello ScoreData.</span></span> <span data-ttu-id="acb47-181">Servicio de aprendizaje automático de toohello, autenticarse con una clave de API.</span><span class="sxs-lookup"><span data-stu-id="acb47-181">You authenticate toohello Machine Learning service with an API key.</span></span>

<span data-ttu-id="acb47-182">**ejemplo de código de hello toorun**</span><span class="sxs-lookup"><span data-stu-id="acb47-182">**toorun hello code sample**</span></span>

1. <span data-ttu-id="acb47-183">Implementar "ejemplo 1: descargar el conjunto de datos de UCI: conjunto de datos de contenido para adultos 2 clase" experimento, parte de la colección de aprendizaje automático de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="acb47-183">Deploy "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of hello Machine Learning sample collection.</span></span>
2. <span data-ttu-id="acb47-184">Asignar apiKey con clave de Hola desde un servicio Web.</span><span class="sxs-lookup"><span data-stu-id="acb47-184">Assign apiKey with hello key from a Web service.</span></span> <span data-ttu-id="acb47-185">Vea hello **obtener una clave de autorización de aprendizaje automático de Azure** sección principio Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="acb47-185">See hello **Get an Azure Machine Learning authorization key** section near hello beginning of this article.</span></span>
3. <span data-ttu-id="acb47-186">Asignar serviceUri con hello URI de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="acb47-186">Assign serviceUri with hello Request URI.</span></span>

