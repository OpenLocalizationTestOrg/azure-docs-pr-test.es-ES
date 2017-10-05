---
title: "Obtención de un procesador de multimedia mediante REST | Microsoft Docs"
description: Aprenda a crear un componente de procesador de multimedia para codificar, cifrar, descifrar o convertir el formato de contenido multimedia para Servicios multimedia de Azure.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f9ff1997-0da6-4528-aaed-792837e5be41
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 4ad90ad979c5bd74fc55155098c88d5c13cb12e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-get-a-media-processor-instance"></a><span data-ttu-id="13be1-103">Obtención de una instancia del procesador de multimedia</span><span class="sxs-lookup"><span data-stu-id="13be1-103">How to get a Media Processor instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="13be1-104">.NET</span><span class="sxs-lookup"><span data-stu-id="13be1-104">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="13be1-105">REST</span><span class="sxs-lookup"><span data-stu-id="13be1-105">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="13be1-106">Información general</span><span class="sxs-lookup"><span data-stu-id="13be1-106">Overview</span></span>
<span data-ttu-id="13be1-107">En los Servicios multimedia, un procesador multimedia es un componente que controla una tarea de procesamiento específica, como codificación, conversión de formato, cifrado o descifrado de contenido multimedia.</span><span class="sxs-lookup"><span data-stu-id="13be1-107">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="13be1-108">Normalmente crea un procesador multimedia cuando crea una tarea para codificar, cifrar o convertir el formato de contenido multimedia.</span><span class="sxs-lookup"><span data-stu-id="13be1-108">You typically create a media processor when you are creating a task to encode, encrypt, or convert the format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="13be1-109">Procesadores de multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="13be1-109">Azure media processors</span></span> 

<span data-ttu-id="13be1-110">En el siguiente tema se proporcionan listas de procesadores de multimedia:</span><span class="sxs-lookup"><span data-stu-id="13be1-110">The following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="13be1-111">Codificación de procesadores de multimedia</span><span class="sxs-lookup"><span data-stu-id="13be1-111">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="13be1-112">Procesadores de multimedia de Analytics</span><span class="sxs-lookup"><span data-stu-id="13be1-112">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

>[!NOTE]
><span data-ttu-id="13be1-113">Al obtener acceso a las entidades de Servicios multimedia, debe establecer los campos de encabezado específicos y los valores en las solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="13be1-113">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="13be1-114">Para obtener más información, consulte [Configuración del desarrollo de la API de REST de Servicios multimedia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="13be1-114">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="13be1-115">Conexión con Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="13be1-115">Connect to Media Services</span></span>

<span data-ttu-id="13be1-116">Para obtener más información sobre cómo conectarse a la API de Azure Media Services, consulte [Acceso a la API de Azure Media Services con la autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="13be1-116">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="13be1-117">Después de conectarse correctamente a https://media.windows.net, recibirá una redirección 301 que especifica otro URI de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="13be1-117">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="13be1-118">Debe realizar las llamadas posteriores al nuevo URI.</span><span class="sxs-lookup"><span data-stu-id="13be1-118">You must make subsequent calls to the new URI.</span></span>

## <a name="get-a-media-processor"></a><span data-ttu-id="13be1-119">Obtención de un procesador multimedia</span><span class="sxs-lookup"><span data-stu-id="13be1-119">Get a media processor</span></span>

<span data-ttu-id="13be1-120">La siguiente llamada REST muestra cómo obtener una instancia de procesador multimedia por nombre (en este caso, **Codificador multimedia estándar**).</span><span class="sxs-lookup"><span data-stu-id="13be1-120">The following REST call shows how to get a media processor instance by name (in this case, **Media Encoder Standard**).</span></span> 

<span data-ttu-id="13be1-121">Solicitud:</span><span class="sxs-lookup"><span data-stu-id="13be1-121">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="13be1-122">Respuesta:</span><span class="sxs-lookup"><span data-stu-id="13be1-122">Response:</span></span>

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "Description":"Media Encoder Standard",
             "Name":"Media Encoder Standard",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="13be1-123">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="13be1-123">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="13be1-124">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="13be1-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="13be1-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="13be1-125">Next Steps</span></span>
<span data-ttu-id="13be1-126">Ahora que sabe cómo obtener una instancia de procesador multimedia, consulte el tema sobre la [codificación de un recurso](media-services-rest-get-started.md) , que le mostrará cómo utilizar el servicio Media Encoder estándar para codificar un recurso.</span><span class="sxs-lookup"><span data-stu-id="13be1-126">Now that you know how to get a media processor instance, go to the [How to Encode an Asset](media-services-rest-get-started.md) topic which will show you how to use the Media Encoder Standard to encode an asset.</span></span>

