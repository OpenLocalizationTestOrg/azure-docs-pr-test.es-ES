---
title: "Paso 6: Acceder al servicio Web de aprendizaje de máquina Hola | Documentos de Microsoft"
description: "Paso 6 del programa Hola a desarrollar un solución de predicción Tutorial: obtener acceso a un servicio Web de aprendizaje de máquina de Azure activo."
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
ms.openlocfilehash: 211de0294092c6a6b5e6eb608d5d3b88107674c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-6-access-hello-azure-machine-learning-web-service"></a><span data-ttu-id="2acb5-103">Tutorial paso 6: Hola de acceso servicio web de aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="2acb5-103">Walkthrough Step 6: Access hello Azure Machine Learning web service</span></span>

<span data-ttu-id="2acb5-104">Éste es Hola último paso del tutorial de hello, [desarrollar una solución de análisis predictivos en aprendizaje automático de Azure](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="2acb5-104">This is hello last step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="2acb5-105">Creación de un área de trabajo de Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="2acb5-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="2acb5-106">Carga de los datos existentes</span><span class="sxs-lookup"><span data-stu-id="2acb5-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="2acb5-107">Crear un experimento nuevo</span><span class="sxs-lookup"><span data-stu-id="2acb5-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="2acb5-108">Entrenar y evaluar modelos de Hola</span><span class="sxs-lookup"><span data-stu-id="2acb5-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="2acb5-109">Implementar el servicio Web de Hola</span><span class="sxs-lookup"><span data-stu-id="2acb5-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. <span data-ttu-id="2acb5-110">**Acceder al servicio Web Hola**</span><span class="sxs-lookup"><span data-stu-id="2acb5-110">**Access hello Web service**</span></span>

- - -
<span data-ttu-id="2acb5-111">En el paso anterior de hello en este tutorial se implementa un servicio web que usa nuestro modelo de predicción de riesgo de crédito.</span><span class="sxs-lookup"><span data-stu-id="2acb5-111">In hello previous step in this walkthrough we deployed a web service that uses our credit risk prediction model.</span></span> <span data-ttu-id="2acb5-112">Ahora los usuarios son toosend capaz de datos tooit y reciban los resultados.</span><span class="sxs-lookup"><span data-stu-id="2acb5-112">Now users are able toosend data tooit and receive results.</span></span> 

<span data-ttu-id="2acb5-113">Hola servicio Web es un servicio web de Azure que puede recibir y devolver datos mediante las API de REST de una de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="2acb5-113">hello Web service is an Azure web service that can receive and return data using REST APIs in one of two ways:</span></span>  

* <span data-ttu-id="2acb5-114">**Solicitud/respuesta** : usuario Hola envía uno o más filas de crédito toohello de datos de servicio mediante un protocolo HTTP y Hola servicio responde con uno o varios conjuntos de resultados.</span><span class="sxs-lookup"><span data-stu-id="2acb5-114">**Request/Response** - hello user sends one or more rows of credit data toohello service by using an HTTP protocol, and hello service responds with one or more sets of results.</span></span>
* <span data-ttu-id="2acb5-115">**Ejecución por lotes** : usuario Hola almacena uno o más filas de datos de crédito en un Azure blob y, a continuación, envía el servicio de toohello de ubicación de blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="2acb5-115">**Batch Execution** - hello user stores one or more rows of credit data in an Azure blob and then sends hello blob location toohello service.</span></span> <span data-ttu-id="2acb5-116">puntuaciones de servicio de Hello que todas las filas de datos de Hola Hola blob de entrada, almacenes de hello da como resultado otro blob y devuelve Hola dirección URL de ese contenedor.</span><span class="sxs-lookup"><span data-stu-id="2acb5-116">hello service scores all hello rows of data in hello input blob, stores hello results in another blob, and returns hello URL of that container.</span></span>  

<span data-ttu-id="2acb5-117">Hola tooaccess de manera más rápida y sencilla un servicio web de clásico es a través de hello [Azure ML solicitudes y respuestas Web del servicio de aplicaciones](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) o [plantilla de aplicación Web de Azure ML lote ejecución servicio](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span><span class="sxs-lookup"><span data-stu-id="2acb5-117">hello quickest and easiest way tooaccess a Classic web service is through hello [Azure ML Request-Response Service Web App](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) or [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span></span>

<span data-ttu-id="2acb5-118">Estas plantillas de aplicación web pueden compilar una aplicación web personalizada que reconoce los datos de entrada del servicio web y lo que devolverá.</span><span class="sxs-lookup"><span data-stu-id="2acb5-118">These web app templates can build a custom web app that knows your web service's input data and what it will return.</span></span> <span data-ttu-id="2acb5-119">Todo lo que necesita toodo es proporcionar datos y servicio web de acceso tooyour y plantilla de Hola Hola rest.</span><span class="sxs-lookup"><span data-stu-id="2acb5-119">All you need toodo is provide access tooyour web service and data, and hello template does hello rest.</span></span>

<span data-ttu-id="2acb5-120">Para obtener más información sobre el uso de plantillas de aplicación web de hello, consulte [consumir un servicio Web de aprendizaje de máquina de Azure con una plantilla de aplicación web](machine-learning-consume-web-service-with-web-app-template.md).</span><span class="sxs-lookup"><span data-stu-id="2acb5-120">For more information on using hello web app templates, see [Consume an Azure Machine Learning Web service with a web app template](machine-learning-consume-web-service-with-web-app-template.md).</span></span>

<span data-ttu-id="2acb5-121">También puede desarrollar un servicio web de aplicación personalizada tooaccess hello mediante código de inicio que se proporcionan en R, C# y lenguajes de programación Python.</span><span class="sxs-lookup"><span data-stu-id="2acb5-121">You can also develop a custom application tooaccess hello web service using starter code provided for you in R, C#, and Python programming languages.</span></span>

<span data-ttu-id="2acb5-122">Puede encontrar detalles completos en [cómo tooconsume un servicio Web de aprendizaje de máquina de Azure](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="2acb5-122">You can find complete details in [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

