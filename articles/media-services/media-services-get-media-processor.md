---
title: tooCreate aaaHow un procesador de medios mediante Hola SDK de servicios multimedia de Azure para .NET | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un tooencode de componente del procesador de multimedia, convertir el formato, cifrar o descifrar contenido multimedia para servicios multimedia de Azure. Ejemplos de código están escritos en C# y usar hello SDK de servicios multimedia para. NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: dbf9496f-c6f0-42a7-aa36-70f89dcb8ea2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: f133565cc1321d366013f17302adc8bc7585b251
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-get-a-media-processor-instance"></a><span data-ttu-id="e4d78-104">Obtención de una instancia de procesador multimedia</span><span class="sxs-lookup"><span data-stu-id="e4d78-104">How to: Get a Media Processor Instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e4d78-105">.NET</span><span class="sxs-lookup"><span data-stu-id="e4d78-105">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="e4d78-106">REST</span><span class="sxs-lookup"><span data-stu-id="e4d78-106">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="e4d78-107">Información general</span><span class="sxs-lookup"><span data-stu-id="e4d78-107">Overview</span></span>
<span data-ttu-id="e4d78-108">En los Servicios multimedia, un procesador multimedia es un componente que controla una tarea de procesamiento específica, como codificación, conversión de formato, cifrado o descifrado de contenido multimedia.</span><span class="sxs-lookup"><span data-stu-id="e4d78-108">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="e4d78-109">Suele crear un procesador multimedia cuando se crea una tarea tooencode, cifrar o convertir el formato de saludo del contenido multimedia.</span><span class="sxs-lookup"><span data-stu-id="e4d78-109">You typically create a media processor when you are creating a task tooencode, encrypt, or convert hello format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="e4d78-110">Procesadores de multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="e4d78-110">Azure media processors</span></span> 

<span data-ttu-id="e4d78-111">Hola tema siguiente proporciona listas de procesadores multimedia:</span><span class="sxs-lookup"><span data-stu-id="e4d78-111">hello following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="e4d78-112">Codificación de procesadores de multimedia</span><span class="sxs-lookup"><span data-stu-id="e4d78-112">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="e4d78-113">Procesadores de multimedia de Analytics</span><span class="sxs-lookup"><span data-stu-id="e4d78-113">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

## <a name="get-media-processor"></a><span data-ttu-id="e4d78-114">Obtención de un procesador multimedia</span><span class="sxs-lookup"><span data-stu-id="e4d78-114">Get Media Processor</span></span>

<span data-ttu-id="e4d78-115">Hola siguiendo el método muestra cómo tooget una instancia de procesador de multimedia.</span><span class="sxs-lookup"><span data-stu-id="e4d78-115">hello following method shows how tooget a media processor instance.</span></span> <span data-ttu-id="e4d78-116">ejemplo de código de Hello supone el uso de Hola de una variable de nivel de módulo con el nombre **_contexto** tooreference contexto de servidor hello tal y como se describe en la sección de hello [Cómo: conectar servicios mediante programación tooMedia](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="e4d78-116">hello code example assumes hello use of a module-level variable named **_context** tooreference hello server context as described in hello section [How to: Connect tooMedia Services Programmatically](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="e4d78-117">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="e4d78-117">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e4d78-118">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="e4d78-118">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="e4d78-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e4d78-119">Next Steps</span></span>
<span data-ttu-id="e4d78-120">Ahora que sabe cómo tooget una instancia de procesador multimedia, vaya toohello [cómo tooEncode un activo](media-services-dotnet-encode-with-media-encoder-standard.md) tema que le mostrará cómo toouse Hola tooencode Media Encoder estándar a un recurso.</span><span class="sxs-lookup"><span data-stu-id="e4d78-120">Now that you know how tooget a media processor instance, go toohello [How tooEncode an Asset](media-services-dotnet-encode-with-media-encoder-standard.md) topic which will show you how toouse hello Media Encoder Standard tooencode an asset.</span></span>

