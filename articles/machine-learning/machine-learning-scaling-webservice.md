---
title: "Ampliación de la simultaneidad en servicios web de Azure Machine Learning | Microsoft Docs"
description: "Aprenda a ampliar la simultaneidad en los servicios web de Azure Machine Learning incorporando puntos de conexión adicionales."
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
ms.openlocfilehash: 013354515d841003c912ac0338690dd975a79ef7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a><span data-ttu-id="927f2-104">Escalado de un servicio web de Azure Machine Learning mediante la incorporación de puntos de conexión adicionales</span><span class="sxs-lookup"><span data-stu-id="927f2-104">Scaling an Azure Machine Learning web service by adding additional endpoints</span></span>
> [!NOTE]
> <span data-ttu-id="927f2-105">En este tema se describen técnicas que se aplican a un servicio web Machine Learning **clásico**.</span><span class="sxs-lookup"><span data-stu-id="927f2-105">This topic describes techniques applicable to a **Classic** Machine Learning Web service.</span></span> 
> 
> 

<span data-ttu-id="927f2-106">De manera predeterminada, cada servicio web publicado está configurado para admitir 20 solicitudes simultáneas y 200 solicitudes simultáneas como máximo.</span><span class="sxs-lookup"><span data-stu-id="927f2-106">By default, each published Web service is configured to support 20 concurrent requests and can be as high as 200 concurrent requests.</span></span> <span data-ttu-id="927f2-107">Aunque el Portal de Azure clásico ofrece una manera de establecer este valor, Azure Machine Learning optimiza automáticamente este valor con el fin de brindar el mejor rendimiento para el servicio web, por lo que se omite el valor del portal.</span><span class="sxs-lookup"><span data-stu-id="927f2-107">While the Azure classic portal provides a way to set this value, Azure Machine Learning automatically optimizes the setting to provide the best performance for your web service and the portal value is ignored.</span></span> 

<span data-ttu-id="927f2-108">Si tiene previsto llamar a la API con una carga mayor que un máximo de 200 llamadas simultáneas, debe crear varios puntos de conexión en el mismo servicio web.</span><span class="sxs-lookup"><span data-stu-id="927f2-108">If you plan to call the API with a higher load than a Max Concurrent Calls value of 200 will support, you should create multiple endpoints on the same Web service.</span></span> <span data-ttu-id="927f2-109">Acto seguido, podrá distribuir aleatoriamente la carga entre todos ellos.</span><span class="sxs-lookup"><span data-stu-id="927f2-109">You can then randomly distribute your load across all of them.</span></span>

<span data-ttu-id="927f2-110">El escalado de un servicio web es una tarea común.</span><span class="sxs-lookup"><span data-stu-id="927f2-110">The scaling of a Web service is a common task.</span></span> <span data-ttu-id="927f2-111">Algunos de los motivos para ello son admitir más de 200 solicitudes simultáneas, aumentar la disponibilidad a través de varios puntos de conexión u ofrecer puntos de conexión independientes para el servicio web.</span><span class="sxs-lookup"><span data-stu-id="927f2-111">Some reasons to scale are to support more than 200 concurrent requests, increase availability through multiple endpoints, or provide separate endpoints for the web service.</span></span> <span data-ttu-id="927f2-112">Puede aumentar la escala agregando más puntos de conexión para el mismo servicio web a través del [Portal de Azure clásico](https://manage.windowsazure.com/) o del portal [Servicio web Azure Machine Learning](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="927f2-112">You can increase the scale by adding additional endpoints for the same Web service through [Azure classic portal](https://manage.windowsazure.com/) or the [Azure Machine Learning Web Service](https://services.azureml.net/) portal.</span></span>

<span data-ttu-id="927f2-113">Para obtener más información sobre la incorporación de puntos de conexión nuevos, consulte [Creación de puntos de conexión](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="927f2-113">For more information on adding new endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span>

<span data-ttu-id="927f2-114">Tenga en cuenta que usar un recuento de simultaneidad alto puede ser perjudicial si no se llama a la API con una tasa elevada en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="927f2-114">Keep in mind that using a high concurrency count can be detrimental if you're not calling the API with a correspondingly high rate.</span></span> <span data-ttu-id="927f2-115">Puede que vea tiempos de espera esporádicos o picos de latencia si pone una carga relativamente baja en una API configurada para una carga elevada.</span><span class="sxs-lookup"><span data-stu-id="927f2-115">You might see sporadic timeouts and/or spikes in the latency if you put a relatively low load on an API configured for high load.</span></span>

<span data-ttu-id="927f2-116">Las API sincrónicas se usan normalmente en situaciones en las que se desea una latencia baja.</span><span class="sxs-lookup"><span data-stu-id="927f2-116">The synchronous APIs are typically used in situations where a low latency is desired.</span></span> <span data-ttu-id="927f2-117">Latencia aquí implica el tiempo que tarda la API en completar una solicitud, sin contar los retrasos de red.</span><span class="sxs-lookup"><span data-stu-id="927f2-117">Latency here implies the time it takes for the API to complete one request, and doesn't account for any network delays.</span></span> <span data-ttu-id="927f2-118">Supongamos que tiene una API con una latencia de 50 ms.</span><span class="sxs-lookup"><span data-stu-id="927f2-118">Let's say you have an API with a 50-ms latency.</span></span> <span data-ttu-id="927f2-119">Para utilizar totalmente la capacidad disponible con nivel de limitación alto y un número máximo de llamadas simultáneas de 20, debe llamar a esta API 20 * 1000/50 = 400 veces por segundo.</span><span class="sxs-lookup"><span data-stu-id="927f2-119">To fully consume the available capacity with throttle level High and Max Concurrent Calls = 20, you need to call this API 20 * 1000 / 50 = 400 times per second.</span></span> <span data-ttu-id="927f2-120">Al ampliar esto aún más, un número máximo de llamadas simultáneas de 200 le permitirá llamar a la API 4000 veces por segundo, si presuponemos que la latencia es de 50 ms.</span><span class="sxs-lookup"><span data-stu-id="927f2-120">Extending this further, a Max Concurrent Calls of 200 allows you to call the API 4000 times per second, assuming a 50-ms latency.</span></span>

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png
