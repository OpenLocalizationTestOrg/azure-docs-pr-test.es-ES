---
title: 'Paso 6: Acceso al servicio web Machine Learning | Microsoft Docs'
description: "Paso 6 del tutorial Desarrollo de una solución predictiva: acceso a un servicio web activo de Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a65c89a-40ab-4673-8dd8-8eee0a150e3b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: d309f6c4749a80c81859b693a2bd5927e8fe0e54
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-6-access-the-azure-machine-learning-web-service"></a><span data-ttu-id="e6a7b-103">Paso 6 del tutorial: Acceso al servicio web de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="e6a7b-103">Walkthrough Step 6: Access the Azure Machine Learning web service</span></span>

<span data-ttu-id="e6a7b-104">Este es el último paso del tutorial [Desarrollo de una solución de análisis predictiva para la evaluación del riesgo de crédito en Aprendizaje automático de Azure](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="e6a7b-104">This is the last step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="e6a7b-105">Creación de un área de trabajo de Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="e6a7b-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="e6a7b-106">Carga de los datos existentes</span><span class="sxs-lookup"><span data-stu-id="e6a7b-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="e6a7b-107">Crear un experimento nuevo</span><span class="sxs-lookup"><span data-stu-id="e6a7b-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="e6a7b-108">Entrenamiento y evaluación de los modelos</span><span class="sxs-lookup"><span data-stu-id="e6a7b-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="e6a7b-109">Implementación del servicio web</span><span class="sxs-lookup"><span data-stu-id="e6a7b-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. <span data-ttu-id="e6a7b-110">**Acceso al servicio web**</span><span class="sxs-lookup"><span data-stu-id="e6a7b-110">**Access the Web service**</span></span>

- - -
<span data-ttu-id="e6a7b-111">En el paso anterior de este tutorial hemos implementado un servicio web que usa nuestro modelo de predicción del riesgo de crédito.</span><span class="sxs-lookup"><span data-stu-id="e6a7b-111">In the previous step in this walkthrough we deployed a web service that uses our credit risk prediction model.</span></span> <span data-ttu-id="e6a7b-112">Ahora los usuarios pueden enviar datos al servicio y recibir resultados.</span><span class="sxs-lookup"><span data-stu-id="e6a7b-112">Now users are able to send data to it and receive results.</span></span> 

<span data-ttu-id="e6a7b-113">El servicio web es un servicio web de Azure que puede recibir y devolver datos con las API de REST de una de estas dos maneras:</span><span class="sxs-lookup"><span data-stu-id="e6a7b-113">The Web service is an Azure web service that can receive and return data using REST APIs in one of two ways:</span></span>  

* <span data-ttu-id="e6a7b-114">**Solicitud/respuesta** : el usuario envía una o varias filas de datos de crédito al servicio mediante un protocolo HTTP, y el servicio responde con uno o más conjuntos de resultados.</span><span class="sxs-lookup"><span data-stu-id="e6a7b-114">**Request/Response** - The user sends one or more rows of credit data to the service by using an HTTP protocol, and the service responds with one or more sets of results.</span></span>
* <span data-ttu-id="e6a7b-115">**Ejecución de lotes** : el usuario almacena una o varias filas de datos de crédito en un blob de Azure y luego envía la ubicación del blob al servicio.</span><span class="sxs-lookup"><span data-stu-id="e6a7b-115">**Batch Execution** - The user stores one or more rows of credit data in an Azure blob and then sends the blob location to the service.</span></span> <span data-ttu-id="e6a7b-116">El servicio puntúa todas las filas de datos en el blob de entrada, almacena los resultados en otro blog y devuelve la dirección URL del contenedor.</span><span class="sxs-lookup"><span data-stu-id="e6a7b-116">The service scores all the rows of data in the input blob, stores the results in another blob, and returns the URL of that container.</span></span>  

<span data-ttu-id="e6a7b-117">La forma más fácil y rápida de acceder al servicio web clásico es a través de la [aplicación web del servicio de solicitud-respuesta de Azure ML](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) o la [plantilla de aplicación web del servicio de ejecución de lotes de Azure ML](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span><span class="sxs-lookup"><span data-stu-id="e6a7b-117">The quickest and easiest way to access a Classic web service is through the [Azure ML Request-Response Service Web App](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) or [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span></span>

<span data-ttu-id="e6a7b-118">Estas plantillas de aplicación web pueden compilar una aplicación web personalizada que reconoce los datos de entrada del servicio web y lo que devolverá.</span><span class="sxs-lookup"><span data-stu-id="e6a7b-118">These web app templates can build a custom web app that knows your web service's input data and what it will return.</span></span> <span data-ttu-id="e6a7b-119">Todo lo que necesita hacer es conceder acceso al servicio web y a los datos, y la plantilla se encarga del resto.</span><span class="sxs-lookup"><span data-stu-id="e6a7b-119">All you need to do is provide access to your web service and data, and the template does the rest.</span></span>

<span data-ttu-id="e6a7b-120">Para obtener más información sobre el uso de plantillas de aplicación web, consulte [Consumo de un servicio web de Azure Machine Learning con una plantilla de aplicación web](machine-learning-consume-web-service-with-web-app-template.md).</span><span class="sxs-lookup"><span data-stu-id="e6a7b-120">For more information on using the web app templates, see [Consume an Azure Machine Learning Web service with a web app template](machine-learning-consume-web-service-with-web-app-template.md).</span></span>

<span data-ttu-id="e6a7b-121">También puede desarrollar una aplicación personalizada para acceder al servicio web con código de inicio proporcionado en los lenguajes de programación R, C# y Python.</span><span class="sxs-lookup"><span data-stu-id="e6a7b-121">You can also develop a custom application to access the web service using starter code provided for you in R, C#, and Python programming languages.</span></span>

<span data-ttu-id="e6a7b-122">Puede encontrar detalles completos en [Cómo consumir un servicio web Azure Machine Learning](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="e6a7b-122">You can find complete details in [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

