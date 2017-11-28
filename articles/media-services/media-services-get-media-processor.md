---
title: "Cómo crear un procesador de multimedia mediante el SDK de Azure Media Services para .NET| Microsoft Docs"
description: "Aprenda a crear un componente de procesador de multimedia para codificar, cifrar, descifrar o convertir el formato de contenido multimedia para Servicios multimedia de Azure. Los ejemplos de código están escritos en C# y utilizan el SDK de Servicios multimedia para .NET."
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
ms.openlocfilehash: c2cbe41b71afa8acc184f9d7f4cfe94686de783e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-get-a-media-processor-instance"></a><span data-ttu-id="9f17b-104">Obtención de una instancia de procesador multimedia</span><span class="sxs-lookup"><span data-stu-id="9f17b-104">How to: Get a Media Processor Instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9f17b-105">.NET</span><span class="sxs-lookup"><span data-stu-id="9f17b-105">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="9f17b-106">REST</span><span class="sxs-lookup"><span data-stu-id="9f17b-106">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="9f17b-107">Información general</span><span class="sxs-lookup"><span data-stu-id="9f17b-107">Overview</span></span>
<span data-ttu-id="9f17b-108">En los Servicios multimedia, un procesador multimedia es un componente que controla una tarea de procesamiento específica, como codificación, conversión de formato, cifrado o descifrado de contenido multimedia.</span><span class="sxs-lookup"><span data-stu-id="9f17b-108">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="9f17b-109">Normalmente crea un procesador multimedia cuando crea una tarea para codificar, cifrar o convertir el formato de contenido multimedia.</span><span class="sxs-lookup"><span data-stu-id="9f17b-109">You typically create a media processor when you are creating a task to encode, encrypt, or convert the format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="9f17b-110">Procesadores de multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="9f17b-110">Azure media processors</span></span> 

<span data-ttu-id="9f17b-111">En el siguiente tema se proporcionan listas de procesadores de multimedia:</span><span class="sxs-lookup"><span data-stu-id="9f17b-111">The following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="9f17b-112">Codificación de procesadores de multimedia</span><span class="sxs-lookup"><span data-stu-id="9f17b-112">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="9f17b-113">Procesadores de multimedia de Analytics</span><span class="sxs-lookup"><span data-stu-id="9f17b-113">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

## <a name="get-media-processor"></a><span data-ttu-id="9f17b-114">Obtención de un procesador multimedia</span><span class="sxs-lookup"><span data-stu-id="9f17b-114">Get Media Processor</span></span>

<span data-ttu-id="9f17b-115">El siguiente método muestra cómo obtener una instancia del procesador multimedia.</span><span class="sxs-lookup"><span data-stu-id="9f17b-115">The following method shows how to get a media processor instance.</span></span> <span data-ttu-id="9f17b-116">El ejemplo de código supone el uso de una variable de nivel de módulo llamada **_context** para hacer referencia al contexto de servidor tal como se describe en la sección [Procedimientos: conexión con los Media Services mediante programación](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="9f17b-116">The code example assumes the use of a module-level variable named **_context** to reference the server context as described in the section [How to: Connect to Media Services Programmatically](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="9f17b-117">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="9f17b-117">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9f17b-118">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="9f17b-118">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="9f17b-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9f17b-119">Next Steps</span></span>
<span data-ttu-id="9f17b-120">Ahora que sabe cómo obtener una instancia de procesador multimedia, consulte el tema sobre la [codificación de un recurso](media-services-dotnet-encode-with-media-encoder-standard.md) , que le mostrará cómo utilizar el servicio Media Encoder estándar para codificar un recurso.</span><span class="sxs-lookup"><span data-stu-id="9f17b-120">Now that you know how to get a media processor instance, go to the [How to Encode an Asset](media-services-dotnet-encode-with-media-encoder-standard.md) topic which will show you how to use the Media Encoder Standard to encode an asset.</span></span>

