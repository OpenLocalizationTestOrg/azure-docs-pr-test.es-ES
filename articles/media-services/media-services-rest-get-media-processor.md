---
title: "aaa cómo tooget una instancia de procesador multimedia mediante REST | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un tooencode de componente del procesador de multimedia, convertir el formato, cifrar o descifrar contenido multimedia para servicios multimedia de Azure."
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
ms.openlocfilehash: 9f423648ab73c90405c64895ce0f5b6a457862e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-a-media-processor-instance"></a><span data-ttu-id="0a06a-103">¿Cómo tooget una instancia de procesador multimedia</span><span class="sxs-lookup"><span data-stu-id="0a06a-103">How tooget a Media Processor instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0a06a-104">.NET</span><span class="sxs-lookup"><span data-stu-id="0a06a-104">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="0a06a-105">REST</span><span class="sxs-lookup"><span data-stu-id="0a06a-105">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="0a06a-106">Información general</span><span class="sxs-lookup"><span data-stu-id="0a06a-106">Overview</span></span>
<span data-ttu-id="0a06a-107">En los Servicios multimedia, un procesador multimedia es un componente que controla una tarea de procesamiento específica, como codificación, conversión de formato, cifrado o descifrado de contenido multimedia.</span><span class="sxs-lookup"><span data-stu-id="0a06a-107">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="0a06a-108">Suele crear un procesador multimedia cuando se crea una tarea tooencode, cifrar o convertir el formato de saludo del contenido multimedia.</span><span class="sxs-lookup"><span data-stu-id="0a06a-108">You typically create a media processor when you are creating a task tooencode, encrypt, or convert hello format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="0a06a-109">Procesadores de multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="0a06a-109">Azure media processors</span></span> 

<span data-ttu-id="0a06a-110">Hola tema siguiente proporciona listas de procesadores multimedia:</span><span class="sxs-lookup"><span data-stu-id="0a06a-110">hello following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="0a06a-111">Codificación de procesadores de multimedia</span><span class="sxs-lookup"><span data-stu-id="0a06a-111">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="0a06a-112">Procesadores de multimedia de Analytics</span><span class="sxs-lookup"><span data-stu-id="0a06a-112">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

>[!NOTE]
><span data-ttu-id="0a06a-113">Al obtener acceso a las entidades de Servicios multimedia, debe establecer los campos de encabezado específicos y los valores en las solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="0a06a-113">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="0a06a-114">Para obtener más información, consulte [Configuración del desarrollo de la API de REST de Servicios multimedia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="0a06a-114">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="0a06a-115">Conectar servicios de tooMedia</span><span class="sxs-lookup"><span data-stu-id="0a06a-115">Connect tooMedia Services</span></span>

<span data-ttu-id="0a06a-116">Para obtener información sobre cómo tooconnect toohello AMS API, consulte [Hola acceso API de servicios multimedia de Azure con autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="0a06a-116">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="0a06a-117">Después de conectarse correctamente toohttps://media.windows.net, recibirá una redirección 301 especificando otra URI de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="0a06a-117">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="0a06a-118">Debe realizar las llamadas subsiguientes toohello nuevo URI.</span><span class="sxs-lookup"><span data-stu-id="0a06a-118">You must make subsequent calls toohello new URI.</span></span>

## <a name="get-a-media-processor"></a><span data-ttu-id="0a06a-119">Obtención de un procesador multimedia</span><span class="sxs-lookup"><span data-stu-id="0a06a-119">Get a media processor</span></span>

<span data-ttu-id="0a06a-120">Hola después de la llamada de REST, muestra cómo tooget un procesador multimedia instancia por su nombre (en este caso, **Media Encoder estándar**).</span><span class="sxs-lookup"><span data-stu-id="0a06a-120">hello following REST call shows how tooget a media processor instance by name (in this case, **Media Encoder Standard**).</span></span> 

<span data-ttu-id="0a06a-121">Solicitud:</span><span class="sxs-lookup"><span data-stu-id="0a06a-121">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="0a06a-122">Respuesta:</span><span class="sxs-lookup"><span data-stu-id="0a06a-122">Response:</span></span>

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


## <a name="media-services-learning-paths"></a><span data-ttu-id="0a06a-123">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="0a06a-123">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0a06a-124">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="0a06a-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="0a06a-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0a06a-125">Next Steps</span></span>
<span data-ttu-id="0a06a-126">Ahora que sabe cómo tooget una instancia de procesador multimedia, vaya toohello [cómo tooEncode un activo](media-services-rest-get-started.md) tema que le mostrará cómo toouse Hola tooencode Media Encoder estándar a un recurso.</span><span class="sxs-lookup"><span data-stu-id="0a06a-126">Now that you know how tooget a media processor instance, go toohello [How tooEncode an Asset](media-services-rest-get-started.md) topic which will show you how toouse hello Media Encoder Standard tooencode an asset.</span></span>

