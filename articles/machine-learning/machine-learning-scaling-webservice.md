---
title: "aaaHow tooincrease simultaneidad de un servicio web de aprendizaje automático de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooincrease simultaneidad de un aprendizaje automático de Azure de servicio web mediante la adición de puntos de conexión adicionales."
services: machine-learning
documentationcenter: 
author: neerajkh
manager: srikants
editor: cgronlun
keywords: "aprendizaje automático de azure, servicios web, operacionalización, escalado, punto de conexión, simultaneidad"
ms.assetid: c2c51d7f-fd2d-4f03-bc51-bf47e6969296
ms.service: machine-learning
ms.devlang: NA
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 01/23/2017
ms.author: neerajkh
ms.openlocfilehash: e2ad16ec766820a64f36c31232f6a33a79196af4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a><span data-ttu-id="985ee-104">Escalado de un servicio web de Azure Machine Learning mediante la incorporación de puntos de conexión adicionales</span><span class="sxs-lookup"><span data-stu-id="985ee-104">Scaling an Azure Machine Learning web service by adding additional endpoints</span></span>
> [!NOTE]
> <span data-ttu-id="985ee-105">En este tema se describe técnicas aplicables tooa **clásico** servicio Web de aprendizaje de máquina.</span><span class="sxs-lookup"><span data-stu-id="985ee-105">This topic describes techniques applicable tooa **Classic** Machine Learning Web service.</span></span> 
> 
> 

<span data-ttu-id="985ee-106">De forma predeterminada, cada servicio Web publicado es 20 solicitudes simultáneas de toosupport configurado y puede ser tan alto como 200 solicitudes simultáneas.</span><span class="sxs-lookup"><span data-stu-id="985ee-106">By default, each published Web service is configured toosupport 20 concurrent requests and can be as high as 200 concurrent requests.</span></span> <span data-ttu-id="985ee-107">Aunque Hola portal de Azure clásico proporciona una manera tooset este valor, aprendizaje automático de Azure optimiza automáticamente Hola configuración tooprovide Hola obtener el mejor rendimiento para el servicio web y se omite el valor de portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="985ee-107">While hello Azure classic portal provides a way tooset this value, Azure Machine Learning automatically optimizes hello setting tooprovide hello best performance for your web service and hello portal value is ignored.</span></span> 

<span data-ttu-id="985ee-108">Si tiene previsto toocall Hola API con una carga más elevada de será compatible con un valor de número máximo de llamadas simultáneas de 200, debe crear varios puntos de conexión en hello mismo servicio Web.</span><span class="sxs-lookup"><span data-stu-id="985ee-108">If you plan toocall hello API with a higher load than a Max Concurrent Calls value of 200 will support, you should create multiple endpoints on hello same Web service.</span></span> <span data-ttu-id="985ee-109">Acto seguido, podrá distribuir aleatoriamente la carga entre todos ellos.</span><span class="sxs-lookup"><span data-stu-id="985ee-109">You can then randomly distribute your load across all of them.</span></span>

<span data-ttu-id="985ee-110">Hola ajuste de escala de un servicio Web es una tarea común.</span><span class="sxs-lookup"><span data-stu-id="985ee-110">hello scaling of a Web service is a common task.</span></span> <span data-ttu-id="985ee-111">Algunas razones tooscale son toosupport más de 200 solicitudes simultáneas, aumentar la disponibilidad a través de varios puntos de conexión o proporcionar puntos de conexión independientes para el servicio web de Hola.</span><span class="sxs-lookup"><span data-stu-id="985ee-111">Some reasons tooscale are toosupport more than 200 concurrent requests, increase availability through multiple endpoints, or provide separate endpoints for hello web service.</span></span> <span data-ttu-id="985ee-112">Puede aumentar escala Hola agregando extremos adicionales en hello mismo servicio Web a través de [portal de Azure clásico](https://manage.windowsazure.com/) o hello [servicio Web de Azure Machine Learning](https://services.azureml.net/) portal.</span><span class="sxs-lookup"><span data-stu-id="985ee-112">You can increase hello scale by adding additional endpoints for hello same Web service through [Azure classic portal](https://manage.windowsazure.com/) or hello [Azure Machine Learning Web Service](https://services.azureml.net/) portal.</span></span>

<span data-ttu-id="985ee-113">Para obtener más información sobre la incorporación de puntos de conexión nuevos, consulte [Creación de puntos de conexión](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="985ee-113">For more information on adding new endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span>

<span data-ttu-id="985ee-114">Tenga en cuenta que con un recuento de alta simultaneidad puede ser perjudicial si no se está llamando a Hola API con una tasa alta según corresponda.</span><span class="sxs-lookup"><span data-stu-id="985ee-114">Keep in mind that using a high concurrency count can be detrimental if you're not calling hello API with a correspondingly high rate.</span></span> <span data-ttu-id="985ee-115">Podría ver los tiempos de espera esporádicas o picos de latencia de hello si coloca una carga relativamente baja en una API configurada para una carga elevada.</span><span class="sxs-lookup"><span data-stu-id="985ee-115">You might see sporadic timeouts and/or spikes in hello latency if you put a relatively low load on an API configured for high load.</span></span>

<span data-ttu-id="985ee-116">Hola que API sincrónicas se utilizan habitualmente en situaciones donde se desea una baja latencia.</span><span class="sxs-lookup"><span data-stu-id="985ee-116">hello synchronous APIs are typically used in situations where a low latency is desired.</span></span> <span data-ttu-id="985ee-117">Latencia aquí implica tiempo Hola toma para una solicitud de API de hello toocomplete y no en cuenta los retrasos de red.</span><span class="sxs-lookup"><span data-stu-id="985ee-117">Latency here implies hello time it takes for hello API toocomplete one request, and doesn't account for any network delays.</span></span> <span data-ttu-id="985ee-118">Supongamos que tiene una API con una latencia de 50 ms.</span><span class="sxs-lookup"><span data-stu-id="985ee-118">Let's say you have an API with a 50-ms latency.</span></span> <span data-ttu-id="985ee-119">toofully consumir capacidad disponible de hello con nivel de limitación de alto y el número máximo de llamadas simultáneas = 20, necesita toocall esta API 20 * 1000 / 400 = 50 veces por segundo.</span><span class="sxs-lookup"><span data-stu-id="985ee-119">toofully consume hello available capacity with throttle level High and Max Concurrent Calls = 20, you need toocall this API 20 * 1000 / 50 = 400 times per second.</span></span> <span data-ttu-id="985ee-120">Extender aún más, un número máximo de llamadas simultáneas de 200 permite toocall Hola API 4000 veces por segundo, suponiendo un 50-ms de latencia.</span><span class="sxs-lookup"><span data-stu-id="985ee-120">Extending this further, a Max Concurrent Calls of 200 allows you toocall hello API 4000 times per second, assuming a 50-ms latency.</span></span>

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png
