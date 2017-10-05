---
title: Conectarse a un servicio web Machine Learning | Microsoft Docs
description: "Mediante C# o Python, conéctese a un servicio web Azure Machine Learning mediante una clave de autorización."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 59b07bab-b60f-48c4-a385-a162e50ec7c2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: garye
ROBOTS: NOINDEX
redirect_url: machine-learning-consume-web-services
redirect_document_id: TRUE
ms.openlocfilehash: 0fc6c7e921b18eb14a95fb737d8fb5ab5cc7e687
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-an-azure-machine-learning-web-service"></a><span data-ttu-id="bf174-103">Conectarse a un servicio web de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="bf174-103">Connect to an Azure Machine Learning Web Service</span></span>
<span data-ttu-id="bf174-104">La experiencia del desarrollador de Azure Machine Learning es una API de servicio web para realizar predicciones a partir de datos de entrada en tiempo real o en modo por lotes.</span><span class="sxs-lookup"><span data-stu-id="bf174-104">The Azure Machine Learning developer experience is a Web service API to make predictions from input data in real time or in batch mode.</span></span> <span data-ttu-id="bf174-105">Use Azure Machine Learning Studio para crear predicciones e implementar un servicio web Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="bf174-105">You use Azure Machine Learning Studio to create predictions and deploy an Azure Machine Learning Web service.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="bf174-106">Para obtener información sobre cómo crear e implementar un servicio web Machine Learning con Machine Learning Studio:</span><span class="sxs-lookup"><span data-stu-id="bf174-106">To learn about how to create and deploy a Machine Learning Web service using Machine Learning Studio:</span></span>

* <span data-ttu-id="bf174-107">Para obtener un tutorial sobre cómo crear un experimento en Estudio de aprendizaje automático, consulte [Creación del primer experimento](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="bf174-107">For a tutorial on how to create an experiment in Machine Learning Studio, see [Create your first experiment](machine-learning-create-experiment.md).</span></span>
* <span data-ttu-id="bf174-108">Para obtener detalles sobre cómo implementar un servicio web, vea [Implementación de un servicio web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="bf174-108">For details on how to deploy a Web service, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="bf174-109">Para obtener más información sobre Aprendizaje automático, visite el [Centro de documentación de aprendizaje automático](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="bf174-109">For more information about Machine Learning in general, visit the [Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

## <a name="azure-machine-learning-web-service"></a><span data-ttu-id="bf174-110">Servicio web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="bf174-110">Azure Machine Learning Web service</span></span>
<span data-ttu-id="bf174-111">Con el servicio web Azure Machine Learning, una aplicación externa se comunica con un modelo de puntuación de flujo de trabajo de Machine Learning en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="bf174-111">With the Azure Machine Learning Web service, an external application communicates with a Machine Learning workflow scoring model in real time.</span></span> <span data-ttu-id="bf174-112">Una llamada al servicio web Machine Learning devuelve resultados de predicción a una aplicación externa.</span><span class="sxs-lookup"><span data-stu-id="bf174-112">A Machine Learning Web service call returns prediction results to an external application.</span></span> <span data-ttu-id="bf174-113">Para llamar a un servicio web Machine Learning, se pasa una clave de API que se crea cuando se implementa una predicción.</span><span class="sxs-lookup"><span data-stu-id="bf174-113">To make a Machine Learning Web service call, you pass an API key that is created when you deploy a prediction.</span></span> <span data-ttu-id="bf174-114">El servicio web Machine Learning se basa en REST, una opción popular de arquitectura para proyectos de programación web.</span><span class="sxs-lookup"><span data-stu-id="bf174-114">The Machine Learning Web service is based on REST, a popular architecture choice for web programming projects.</span></span>

<span data-ttu-id="bf174-115">Aprendizaje automático de Azure tiene dos tipos de servicios:</span><span class="sxs-lookup"><span data-stu-id="bf174-115">Azure Machine Learning has two types of services:</span></span>

* <span data-ttu-id="bf174-116">Servicio de solicitud y respuesta (RRS): servicio de latencia baja altamente escalable que proporciona una interfaz con los modelos sin estado creados e implementados desde el Estudio de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="bf174-116">Request-Response Service (RRS) – A low latency, highly scalable service that provides an interface to the stateless models created and deployed from the Machine Learning Studio.</span></span>
* <span data-ttu-id="bf174-117">Servicio de ejecución por lotes (BES): servicio asincrónico que puntúa un lote de registros de datos.</span><span class="sxs-lookup"><span data-stu-id="bf174-117">Batch Execution Service (BES) – An asynchronous service that scores a batch for data records.</span></span>

<span data-ttu-id="bf174-118">Para más información sobre los servicios web Machine Learning, consulte [Implementación de un servicio web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="bf174-118">For more information about Machine Learning Web services, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="get-an-azure-machine-learning-authorization-key"></a><span data-ttu-id="bf174-119">Obtener una clave de autorización de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="bf174-119">Get an Azure Machine Learning authorization key</span></span>
<span data-ttu-id="bf174-120">Al implementar el experimento, se generan claves de API para el servicio web.</span><span class="sxs-lookup"><span data-stu-id="bf174-120">When you deploy your experiment, API keys are generated for the Web service.</span></span> <span data-ttu-id="bf174-121">Puede recuperar las claves de varias ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="bf174-121">You can retrieve the keys from several locations.</span></span>

### <a name="from-the-microsoft-azure-machine-learning-web-services-portal"></a><span data-ttu-id="bf174-122">En el portal Servicios web Microsoft Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="bf174-122">From the Microsoft Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="bf174-123">Inicie sesión en el portal [Servicios web Microsoft Azure Machine Learning](https://services.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="bf174-123">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span>

<span data-ttu-id="bf174-124">Para recuperar la clave de API para un nuevo servicio web Machine Learning:</span><span class="sxs-lookup"><span data-stu-id="bf174-124">To retrieve the API key for a New Machine Learning Web service:</span></span>

1. <span data-ttu-id="bf174-125">En el portal de servicios web Azure Machine Learning, haga clic en la opción **Servicios web** del menú superior.</span><span class="sxs-lookup"><span data-stu-id="bf174-125">In the Azure Machine Learning Web Services portal, click **Web Services** the top menu.</span></span>
2. <span data-ttu-id="bf174-126">Haga clic en el servicio web del que quiere recuperar la clave.</span><span class="sxs-lookup"><span data-stu-id="bf174-126">Click the Web service for which you want to retrieve the key.</span></span>
3. <span data-ttu-id="bf174-127">En el menú superior, haga clic en **Consume**(Consumo).</span><span class="sxs-lookup"><span data-stu-id="bf174-127">On the top menu, click **Consume**.</span></span>
4. <span data-ttu-id="bf174-128">Copie y guarde la **clave principal**.</span><span class="sxs-lookup"><span data-stu-id="bf174-128">Copy and save the **Primary Key**.</span></span>

<span data-ttu-id="bf174-129">Para recuperar la clave de API para un servicio web Machine Learning clásico:</span><span class="sxs-lookup"><span data-stu-id="bf174-129">To retrieve the API key for a Classic Machine Learning Web service:</span></span>

1. <span data-ttu-id="bf174-130">En el portal Servicios web Azure Machine Learning, haga clic en la opción **Classic Web Services** (Servicios web clásicos) del menú superior.</span><span class="sxs-lookup"><span data-stu-id="bf174-130">In the Azure Machine Learning Web Services portal, click **Classic Web Services** the top menu.</span></span>
2. <span data-ttu-id="bf174-131">Haga clic en el servicio web que está usando.</span><span class="sxs-lookup"><span data-stu-id="bf174-131">Click the Web service with which you are working.</span></span>
3. <span data-ttu-id="bf174-132">Haga clic en el punto de conexión del que quiere recuperar la clave.</span><span class="sxs-lookup"><span data-stu-id="bf174-132">Click the endpoint for which you want to retrieve the key.</span></span>
4. <span data-ttu-id="bf174-133">En el menú superior, haga clic en **Consume**(Consumo).</span><span class="sxs-lookup"><span data-stu-id="bf174-133">On the top menu, click **Consume**.</span></span>
5. <span data-ttu-id="bf174-134">Copie y guarde la **clave principal**.</span><span class="sxs-lookup"><span data-stu-id="bf174-134">Copy and save the **Primary Key**.</span></span>

### <a name="classic-web-service"></a><span data-ttu-id="bf174-135">Servicio web clásico</span><span class="sxs-lookup"><span data-stu-id="bf174-135">Classic Web service</span></span>
 <span data-ttu-id="bf174-136">También puede obtener una clave para un servicio web clásico en Machine Learning Studio o el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="bf174-136">You can also retrieve a key for a Classic Web service from Machine Learning Studio or the Azure classic portal.</span></span>

#### <a name="machine-learning-studio"></a><span data-ttu-id="bf174-137">Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="bf174-137">Machine Learning Studio</span></span>
1. <span data-ttu-id="bf174-138">En Estudio de aprendizaje automático, haga clic en **SERVICIOS WEB** a la izquierda.</span><span class="sxs-lookup"><span data-stu-id="bf174-138">In Machine Learning Studio, click **WEB SERVICES** on the left.</span></span>
2. <span data-ttu-id="bf174-139">Haga clic en un servicio web.</span><span class="sxs-lookup"><span data-stu-id="bf174-139">Click a Web service.</span></span> <span data-ttu-id="bf174-140">La **clave de API** está en la pestaña **PANEL**.</span><span class="sxs-lookup"><span data-stu-id="bf174-140">The **API key** is on the **DASHBOARD** tab.</span></span>

#### <a name="azure-classic-portal"></a><span data-ttu-id="bf174-141">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="bf174-141">Azure classic portal</span></span>
1. <span data-ttu-id="bf174-142">Haga clic en **APRENDIZAJE AUTOMÁTICO** a la izquierda.</span><span class="sxs-lookup"><span data-stu-id="bf174-142">Click **MACHINE LEARNING** on the left.</span></span>
2. <span data-ttu-id="bf174-143">Haga clic en el área de trabajo en el que se encuentra el servicio web.</span><span class="sxs-lookup"><span data-stu-id="bf174-143">Click the workspace in which your Web service is located.</span></span>
3. <span data-ttu-id="bf174-144">Haga clic en **SERVICIOS WEB**.</span><span class="sxs-lookup"><span data-stu-id="bf174-144">Click **WEB SERVICES**.</span></span>
4. <span data-ttu-id="bf174-145">Haga clic en un servicio web.</span><span class="sxs-lookup"><span data-stu-id="bf174-145">Click a Web service.</span></span>
5. <span data-ttu-id="bf174-146">Haga clic en un extremo.</span><span class="sxs-lookup"><span data-stu-id="bf174-146">Click an endpoint.</span></span> <span data-ttu-id="bf174-147">La "CLAVE DE API" está inactiva en la parte inferior derecha.</span><span class="sxs-lookup"><span data-stu-id="bf174-147">The “API KEY” is down at the lower-right.</span></span>

## <span data-ttu-id="bf174-148"><a id="connect"></a>Conexión a un servicio web Machine Learning</span><span class="sxs-lookup"><span data-stu-id="bf174-148"><a id="connect"></a>Connect to a Machine Learning Web service</span></span>
<span data-ttu-id="bf174-149">Puede conectarse a un servicio web Machine Learning mediante cualquier lenguaje de programación que admita la respuesta y la solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="bf174-149">You can connect to a Machine Learning Web service using any programming language that supports HTTP request and response.</span></span> <span data-ttu-id="bf174-150">Puede ver ejemplos en C#, Python y R desde una página de ayuda de servicio web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="bf174-150">You can view examples in C#, Python, and R from a Machine Learning Web service help page.</span></span>

<span data-ttu-id="bf174-151">**Ayuda de la API de Machine Learning** Se crea una página de ayuda de API de Machine Learning al implementar un servicio web.</span><span class="sxs-lookup"><span data-stu-id="bf174-151">**Machine Learning API help** Machine Learning API help is created when you deploy a Web service.</span></span> <span data-ttu-id="bf174-152">Vea [Tutorial de Aprendizaje automático de Azure: Implementación de un servicio web](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="bf174-152">See [Azure Machine Learning Walkthrough- Deploy Web Service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
<span data-ttu-id="bf174-153">La ayuda de la API de Machine Learning contiene información sobre un servicio web de predicción.</span><span class="sxs-lookup"><span data-stu-id="bf174-153">The Machine Learning API help contains details about a prediction Web service.</span></span>

1. <span data-ttu-id="bf174-154">Haga clic en el servicio web que está usando.</span><span class="sxs-lookup"><span data-stu-id="bf174-154">Click the Web service with which you are working.</span></span>
2. <span data-ttu-id="bf174-155">Haga clic en el punto de conexión para el que desea ver la página de ayuda de la API.</span><span class="sxs-lookup"><span data-stu-id="bf174-155">Click the endpoint for which you want to view the API Help Page.</span></span>
3. <span data-ttu-id="bf174-156">En el menú superior, haga clic en **Consume**(Consumo).</span><span class="sxs-lookup"><span data-stu-id="bf174-156">On the top menu, click **Consume**.</span></span>
4. <span data-ttu-id="bf174-157">Haga clic en **API help page** (Página de ayuda de la API) en los puntos de conexión Solicitud-respuesta o Ejecución de lotes.</span><span class="sxs-lookup"><span data-stu-id="bf174-157">Click **API help page** under either the Request-Response or Batch Execution endpoints.</span></span>

<span data-ttu-id="bf174-158">**Para ver la ayuda de la API de Machine Learning para un servicio web nuevo**</span><span class="sxs-lookup"><span data-stu-id="bf174-158">**To view Machine Learning API help for a New Web service**</span></span>

<span data-ttu-id="bf174-159">En el portal Servicios web Azure Machine Learning:</span><span class="sxs-lookup"><span data-stu-id="bf174-159">In the Azure Machine Learning Web Services Portal:</span></span>

1. <span data-ttu-id="bf174-160">Haga clic en la opción de menú **SERVICIOS WEB** del menú superior.</span><span class="sxs-lookup"><span data-stu-id="bf174-160">Click **WEB SERVICES** on the top menu.</span></span>
2. <span data-ttu-id="bf174-161">Haga clic en el servicio web del que quiere recuperar la clave.</span><span class="sxs-lookup"><span data-stu-id="bf174-161">Click the Web service for which you want to retrieve the key.</span></span>

<span data-ttu-id="bf174-162">Haga clic en **Consume** (Consumo) para obtener los URI de los servicios de solicitud-respuesta y ejecución por lotes, además del código de ejemplo en C#, R y Python.</span><span class="sxs-lookup"><span data-stu-id="bf174-162">Click **Consume** to get the URIs for the Request-Reposonse and Batch Execution Services and Sample code in C#, R, and Python.</span></span>

<span data-ttu-id="bf174-163">Haga clic en **Swagger API** para obtener la documentación basada en Swagger de las API que se invocan desde los URI proporcionados.</span><span class="sxs-lookup"><span data-stu-id="bf174-163">Click **Swagger API** to get Swagger based documentation for the APIs called from the supplied URIs.</span></span>

### <a name="c-sample"></a><span data-ttu-id="bf174-164">Ejemplo de C#</span><span class="sxs-lookup"><span data-stu-id="bf174-164">C# Sample</span></span>
<span data-ttu-id="bf174-165">Para conectarse a un servicio web Machine Learning, use un elemento **HttpClient** que pase ScoreData.</span><span class="sxs-lookup"><span data-stu-id="bf174-165">To connect to a Machine Learning Web service, use an **HttpClient** passing ScoreData.</span></span> <span data-ttu-id="bf174-166">ScoreData contiene un FeatureVector, un vector de n dimensiones de características numéricos que representa el ScoreData.</span><span class="sxs-lookup"><span data-stu-id="bf174-166">ScoreData contains a FeatureVector, an n-dimensional vector of numerical features that represents the ScoreData.</span></span> <span data-ttu-id="bf174-167">Se autentica en el servicio de Aprendizaje automático con una clave API.</span><span class="sxs-lookup"><span data-stu-id="bf174-167">You authenticate to the Machine Learning service with an API key.</span></span>

<span data-ttu-id="bf174-168">Para conectarse a un servicio web Machine Learning, se debe instalar el paquete NuGet **Microsoft.AspNet.WebApi.Client**.</span><span class="sxs-lookup"><span data-stu-id="bf174-168">To connect to a Machine Learning Web service, the **Microsoft.AspNet.WebApi.Client** NuGet package must be installed.</span></span>

<span data-ttu-id="bf174-169">**Instalar Microsoft.AspNet.WebApi.Client NuGet en Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="bf174-169">**Install Microsoft.AspNet.WebApi.Client NuGet in Visual Studio**</span></span>

1. <span data-ttu-id="bf174-170">Publique el conjunto de datos de descarga de UCI: Servicio web de conjunto de datos de clase de contenido para adultos 2.</span><span class="sxs-lookup"><span data-stu-id="bf174-170">Publish the Download dataset from UCI: Adult 2 class dataset Web Service.</span></span>
2. <span data-ttu-id="bf174-171">Haga clic en **Herramientas** > **Administrador de paquetes NuGet** > **Consola del administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="bf174-171">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="bf174-172">Elija **Install-Package Microsoft.AspNet.WebApi.Client**.</span><span class="sxs-lookup"><span data-stu-id="bf174-172">Choose **Install-Package Microsoft.AspNet.WebApi.Client**.</span></span>

<span data-ttu-id="bf174-173">**Para ejecutar el ejemplo de código**</span><span class="sxs-lookup"><span data-stu-id="bf174-173">**To run the code sample**</span></span>

1. <span data-ttu-id="bf174-174">Publique el experimento "Ejemplo 1: descargar el conjunto de datos de UCI: conjunto de datos de clase de contenido para adultos 2", que forma parte de la colección de ejemplos de Aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="bf174-174">Publish "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of the Machine Learning sample collection.</span></span>
2. <span data-ttu-id="bf174-175">Asigne una clave de API con la clave de un servicio web.</span><span class="sxs-lookup"><span data-stu-id="bf174-175">Assign apiKey with the key from a Web service.</span></span> <span data-ttu-id="bf174-176">Consulte el apartado anterior **Obtener una clave de autorización de Aprendizaje automático de Azure** .</span><span class="sxs-lookup"><span data-stu-id="bf174-176">See **Get an Azure Machine Learning authorization key** above.</span></span>
3. <span data-ttu-id="bf174-177">Asigne la URI de servicio a la URI de solicitud.</span><span class="sxs-lookup"><span data-stu-id="bf174-177">Assign serviceUri with the Request URI.</span></span>

### <a name="python-sample"></a><span data-ttu-id="bf174-178">Ejemplo de Python</span><span class="sxs-lookup"><span data-stu-id="bf174-178">Python Sample</span></span>
<span data-ttu-id="bf174-179">Para conectarse a un servicio web Machine Learning, use la biblioteca **urllib2** que pasa ScoreData.</span><span class="sxs-lookup"><span data-stu-id="bf174-179">To connect to a Machine Learning Web service, use the **urllib2** library passing ScoreData.</span></span> <span data-ttu-id="bf174-180">ScoreData contiene un FeatureVector, un vector de n dimensiones de características numéricas que representa el ScoreData.</span><span class="sxs-lookup"><span data-stu-id="bf174-180">ScoreData contains a FeatureVector, an n-dimensional  vector of numerical features that represents the ScoreData.</span></span> <span data-ttu-id="bf174-181">Se autentica en el servicio de Aprendizaje automático con una clave API.</span><span class="sxs-lookup"><span data-stu-id="bf174-181">You authenticate to the Machine Learning service with an API key.</span></span>

<span data-ttu-id="bf174-182">**Para ejecutar el ejemplo de código**</span><span class="sxs-lookup"><span data-stu-id="bf174-182">**To run the code sample**</span></span>

1. <span data-ttu-id="bf174-183">Publique el experimento "Ejemplo 1: descargar el conjunto de datos de UCI: conjunto de datos de clase de contenido para adultos 2", que forma parte de la colección de ejemplos de Aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="bf174-183">Deploy "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of the Machine Learning sample collection.</span></span>
2. <span data-ttu-id="bf174-184">Asigne una clave de API con la clave de un servicio web.</span><span class="sxs-lookup"><span data-stu-id="bf174-184">Assign apiKey with the key from a Web service.</span></span> <span data-ttu-id="bf174-185">Vea la sección **Obtener una clave de autorización de Azure Machine Learning** casi al principio de este artículo.</span><span class="sxs-lookup"><span data-stu-id="bf174-185">See the **Get an Azure Machine Learning authorization key** section near the beginning of this article.</span></span>
3. <span data-ttu-id="bf174-186">Asigne la URI de servicio a la URI de solicitud.</span><span class="sxs-lookup"><span data-stu-id="bf174-186">Assign serviceUri with the Request URI.</span></span>

