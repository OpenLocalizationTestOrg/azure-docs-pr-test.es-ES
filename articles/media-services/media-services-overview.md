---
title: "información general de servicios multimedia de aaaAzure | Documentos de Microsoft"
description: "En este tema se proporciona información general de Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7a5e9723-c379-446b-b4d6-d0e41bd7d31f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/04/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 81f9f4d9ff75effea30c10fd09449e9d2025f377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-overview"></a><span data-ttu-id="53800-103">Introducción a Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="53800-103">Azure Media Services overview</span></span> 

<span data-ttu-id="53800-104">Servicios de multimedia de Microsoft Azure es una plataforma extensible basada en la nube que permite a los desarrolladores toobuild medios escalable administración y entrega de las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="53800-104">Microsoft Azure Media Services is an extensible cloud-based platform that enables developers toobuild scalable media management and delivery applications.</span></span> <span data-ttu-id="53800-105">Servicios multimedia se basa en las API de REST que permiten toosecurely cargar, almacenar, codificar y empaquetar contenido de audio o vídeo a petición y en vivo streaming entrega toovarious para clientes de (por ejemplo, televisión, PC y dispositivos móviles).</span><span class="sxs-lookup"><span data-stu-id="53800-105">Media Services is based on REST APIs that enable you toosecurely upload, store, encode, and package video or audio content for both on-demand and live streaming delivery toovarious clients (for example, TV, PC, and mobile devices).</span></span>

<span data-ttu-id="53800-106">Puede crear flujos de trabajo de un extremo a otro usando solamente Media Services.</span><span class="sxs-lookup"><span data-stu-id="53800-106">You can build end-to-end workflows using entirely Media Services.</span></span> <span data-ttu-id="53800-107">También puede elegir toouse componentes de terceros para algunas partes del flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="53800-107">You can also choose toouse third-party components for some parts of your workflow.</span></span> <span data-ttu-id="53800-108">Por ejemplo, codifique mediante un codificador de terceros.</span><span class="sxs-lookup"><span data-stu-id="53800-108">For example, encode using a third-party encoder.</span></span> <span data-ttu-id="53800-109">A continuación, cargue, proteja, empaquete y entregue con Media Services.</span><span class="sxs-lookup"><span data-stu-id="53800-109">Then, upload, protect, package, deliver using Media Services.</span></span>

<span data-ttu-id="53800-110">Puede elegir toostream su contenido en vivo o entregar contenido a petición.</span><span class="sxs-lookup"><span data-stu-id="53800-110">You can choose toostream your content live or deliver content on-demand.</span></span> <span data-ttu-id="53800-111">tema de Hello también incluye vínculos a temas relevantes de tooother.</span><span class="sxs-lookup"><span data-stu-id="53800-111">hello topic also links tooother relevant topics.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="53800-112">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="53800-112">Media Services learning paths</span></span>
<span data-ttu-id="53800-113">Puede ver las rutas de aprendizaje de Azure Media Services aquí:</span><span class="sxs-lookup"><span data-stu-id="53800-113">You can view AMS learning paths here:</span></span>

* [<span data-ttu-id="53800-114">Flujo de trabajo de streaming en vivo de Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="53800-114">AMS Live Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-live/)
* [<span data-ttu-id="53800-115">Flujo de trabajo de streaming a petición de AMS</span><span class="sxs-lookup"><span data-stu-id="53800-115">AMS on-Demand Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-on-demand/)

## <a name="prerequisites"></a><span data-ttu-id="53800-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="53800-116">Prerequisites</span></span>

<span data-ttu-id="53800-117">toostart con servicios multimedia de Azure, como tener Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="53800-117">toostart using Azure Media Services, you should have hello following:</span></span>

* <span data-ttu-id="53800-118">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="53800-118">An Azure account.</span></span> <span data-ttu-id="53800-119">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="53800-119">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="53800-120">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="53800-120">For details, see [Azure Free Trial](https://azure.microsoft.com).</span></span>
* <span data-ttu-id="53800-121">Una cuenta de Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="53800-121">An Azure Media Services account.</span></span> <span data-ttu-id="53800-122">Para obtener más información, consulte [Creación de una cuenta](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="53800-122">For more information, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="53800-123">(Opcional) Configurar el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="53800-123">(Optional) Set up development environment.</span></span> <span data-ttu-id="53800-124">Elija .NET o API de REST para el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="53800-124">Choose .NET or REST API for your development environment.</span></span> <span data-ttu-id="53800-125">Para obtener más información, consulte [Configuración del entorno](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="53800-125">For more information, see [Set up environment](media-services-dotnet-how-to-use.md).</span></span>

    <span data-ttu-id="53800-126">Además, obtenga información acerca de cómo demasiado[conectarse mediante programación tooAMS API](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="53800-126">Also, learn how too[connect  programmatically tooAMS API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
* <span data-ttu-id="53800-127">Un punto de conexión de streaming estándar o premium en estado iniciado.</span><span class="sxs-lookup"><span data-stu-id="53800-127">A standard or premium streaming endpoint in started state.</span></span>  <span data-ttu-id="53800-128">Para más información, consulte [Administración de puntos de conexión de streaming](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="53800-128">For more information, see [Managing streaming endpoints](media-services-portal-manage-streaming-endpoints.md)</span></span>

## <a name="sdks-and-tools"></a><span data-ttu-id="53800-129">SDK y herramientas</span><span class="sxs-lookup"><span data-stu-id="53800-129">SDKs and tools</span></span>

<span data-ttu-id="53800-130">soluciones de servicios multimedia de toobuild, puede utilizar:</span><span class="sxs-lookup"><span data-stu-id="53800-130">toobuild Media Services solutions, you can use:</span></span>

* [<span data-ttu-id="53800-131">API de REST de Media Services</span><span class="sxs-lookup"><span data-stu-id="53800-131">Media Services REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)
* <span data-ttu-id="53800-132">Uno de los SDK de cliente disponibles hello:</span><span class="sxs-lookup"><span data-stu-id="53800-132">One of hello available client SDKs:</span></span>
    * <span data-ttu-id="53800-133">[SDK de Servicios multimedia de Azure para .NET](https://github.com/Azure/azure-sdk-for-media-services)</span><span class="sxs-lookup"><span data-stu-id="53800-133">[Azure Media Services SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services),</span></span>
    * <span data-ttu-id="53800-134">[SDK de Azure para Java](https://github.com/Azure/azure-sdk-for-java)</span><span class="sxs-lookup"><span data-stu-id="53800-134">[Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java),</span></span>
    * <span data-ttu-id="53800-135">[SDK de Azure para PHP](https://github.com/Azure/azure-sdk-for-php)</span><span class="sxs-lookup"><span data-stu-id="53800-135">[Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php),</span></span>
    * <span data-ttu-id="53800-136">[Azure Media Services para Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (es decir, una versión de un SDK de Node.js que no sea de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="53800-136">[Azure Media Services for Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (This is a non-Microsoft version of a Node.js SDK.</span></span> <span data-ttu-id="53800-137">Se mantiene por una Comunidad y actualmente no tiene una cobertura del 100% de hello AMS APIs).</span><span class="sxs-lookup"><span data-stu-id="53800-137">It is maintained by a community and currently does not have a 100% coverage of hello AMS APIs).</span></span>
* <span data-ttu-id="53800-138">Herramientas existentes:</span><span class="sxs-lookup"><span data-stu-id="53800-138">Existing tools:</span></span>
    * [<span data-ttu-id="53800-139">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="53800-139">Azure portal</span></span>](https://portal.azure.com/)
    * <span data-ttu-id="53800-140">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (El Explorador de Azure Media Services (AMSE) es una aplicación Winforms/C# para Windows)</span><span class="sxs-lookup"><span data-stu-id="53800-140">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Explorer (AMSE) is a Winforms/C# application for Windows)</span></span>

## <a name="concepts-and-overview"></a><span data-ttu-id="53800-141">Introducción y conceptos</span><span class="sxs-lookup"><span data-stu-id="53800-141">Concepts and overview</span></span>
<span data-ttu-id="53800-142">Para conocer los conceptos de Azure Media Services, consulte [Conceptos](media-services-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="53800-142">For Azure Media Services concepts, see [Concepts](media-services-concepts.md).</span></span>

<span data-ttu-id="53800-143">Para un cómo-tooseries que le presenta componentes principales de hello tooall de servicios multimedia de Azure, consulte [tutoriales paso a paso de Azure Media Services](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series).</span><span class="sxs-lookup"><span data-stu-id="53800-143">For a how-tooseries that introduces you tooall hello main components of Azure Media Services, see [Azure Media Services Step-by-Step tutorials](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series).</span></span> <span data-ttu-id="53800-144">Esta serie tiene una buena información general sobre conceptos y realiza las tareas de hello AMSE herramienta toodemonstrate AMS.</span><span class="sxs-lookup"><span data-stu-id="53800-144">This series has a great overview of concepts and it uses hello AMSE tool toodemonstrate AMS tasks.</span></span> <span data-ttu-id="53800-145">La herramienta AMSE es una herramienta de Windows.</span><span class="sxs-lookup"><span data-stu-id="53800-145">AMSE tool is a Windows tool.</span></span> <span data-ttu-id="53800-146">Esta herramienta es compatible con la mayoría de las tareas de hello puede lograr mediante programación con [AMS SDK para .NET](https://github.com/Azure/azure-sdk-for-media-services), [Azure SDK para Java](https://github.com/Azure/azure-sdk-for-java), o [Azure SDK para PHP](https://github.com/Azure/azure-sdk-for-php).</span><span class="sxs-lookup"><span data-stu-id="53800-146">This tool supports most of hello tasks you can achieve programmatically with [AMS SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services), [Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java), or  [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php).</span></span>

## <a name="supported-scenarios-and-availability-of-media-services-across-data-centers"></a><span data-ttu-id="53800-147">Escenarios admitidos y disponibilidad de Media Services en centros de datos</span><span class="sxs-lookup"><span data-stu-id="53800-147">Supported scenarios and availability of Media Services across data centers</span></span>

<span data-ttu-id="53800-148">Para más información, consulte [Scenarios and availability of Media Services features across datacenters](scenarios-and-availability.md) (Escenarios y disponibilidad de Media Services en centros de datos).</span><span class="sxs-lookup"><span data-stu-id="53800-148">For detailed information, see [AMS scenarios and availability of features and services across data centers](scenarios-and-availability.md).</span></span>

## <a name="service-level-agreement-sla"></a><span data-ttu-id="53800-149">Contrato de nivel de servicio (SLA)</span><span class="sxs-lookup"><span data-stu-id="53800-149">Service Level Agreement (SLA)</span></span>

* <span data-ttu-id="53800-150">Garantizamos la disponibilidad del 99,9% de las transacciones de API de REST para la codificación de Media Services.</span><span class="sxs-lookup"><span data-stu-id="53800-150">For Media Services Encoding, we guarantee 99.9% availability of REST API transactions.</span></span>
* <span data-ttu-id="53800-151">Para el streaming, atenderemos correctamente las solicitudes de servicio con una garantía de disponibilidad del 99,9 % para el contenido multimedia existente cuando se adquiera un punto de conexión de streaming estándar o premium.</span><span class="sxs-lookup"><span data-stu-id="53800-151">For Streaming, we will successfully service requests with a 99.9% availability guarantee for existing media content when a standard or premium streaming endpoint is purchased.</span></span>
* <span data-ttu-id="53800-152">Para los canales de Live, se garantiza que ejecuta canales no tenga conectividad externa al menos un 99,9% de tiempo de Hola.</span><span class="sxs-lookup"><span data-stu-id="53800-152">For Live Channels, we guarantee that running Channels will have external connectivity at least 99.9% of hello time.</span></span>
* <span data-ttu-id="53800-153">Para la protección de contenido, se garantiza que se correctamente completará las solicitudes de clave al menos un 99,9% de tiempo de Hola.</span><span class="sxs-lookup"><span data-stu-id="53800-153">For Content Protection, we guarantee that we will successfully fulfill key requests at least 99.9% of hello time.</span></span>
* <span data-ttu-id="53800-154">De indizador, se procesará correctamente las solicitudes de tarea del indizador que se procesa con una codificación reservado unidad 99,9% de tiempo de Hola.</span><span class="sxs-lookup"><span data-stu-id="53800-154">For Indexer, we will successfully service Indexer Task requests processed with an Encoding Reserved Unit 99.9% of hello time.</span></span>

<span data-ttu-id="53800-155">Para obtener más información, consulte el [Contrato de nivel de servicio (SLA) de Microsoft Azure](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="53800-155">For more information, see [Microsoft Azure SLA](https://azure.microsoft.com/support/legal/sla/).</span></span>

<span data-ttu-id="53800-156">Para obtener información acerca de la disponibilidad en centros de datos, vea hello [Avaiability](scenarios-and-availability.md#availability) sección.</span><span class="sxs-lookup"><span data-stu-id="53800-156">For information about availability in datacenters, see hello [Avaiability](scenarios-and-availability.md#availability) section.</span></span>

## <a name="support"></a><span data-ttu-id="53800-157">Soporte técnico</span><span class="sxs-lookup"><span data-stu-id="53800-157">Support</span></span>

<span data-ttu-id="53800-158">[Soporte técnico de Azure](https://azure.microsoft.com/support/options/) proporciona opciones de soporte técnico para Azure, incluido Media Services.</span><span class="sxs-lookup"><span data-stu-id="53800-158">[Azure Support](https://azure.microsoft.com/support/options/) provides support options for Azure, including Media Services.</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="53800-159">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="53800-159">Provide feedback</span></span>

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
