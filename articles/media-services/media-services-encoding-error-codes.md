---
title: "códigos de error de codificación de servicios multimedia aaaAzure | Documentos de Microsoft"
description: "Este tema enumeran los códigos de error que se pueden devolver en caso de que se detectó un error durante la ejecución de la tarea de codificación de Hola..."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ce4e939f-5aee-41f9-859d-e4429815e9f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: b69b6abee797c40c9b8b8f23bf2398273c170e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="encoding-error-codes"></a><span data-ttu-id="a7d22-103">Códigos de error de Encoding</span><span class="sxs-lookup"><span data-stu-id="a7d22-103">Encoding error codes</span></span>

<span data-ttu-id="a7d22-104">Hello tabla siguiente enumeran los códigos de error que se pueden devolver en caso de que se detectó un error durante la ejecución de la tarea de codificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="a7d22-104">hello following table lists error codes that could be returned in case an error was encountered during hello encoding task execution.</span></span>  <span data-ttu-id="a7d22-105">tooget detalles del error en el código. NET, use hello [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) clase.</span><span class="sxs-lookup"><span data-stu-id="a7d22-105">tooget error details in your .NET code, use hello [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) class.</span></span> <span data-ttu-id="a7d22-106">tooget detalles del error en el código REST, usar hello [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) API de REST.</span><span class="sxs-lookup"><span data-stu-id="a7d22-106">tooget error details in your REST code, use hello [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST API.</span></span>

| <span data-ttu-id="a7d22-107">ErrorDetail.Code</span><span class="sxs-lookup"><span data-stu-id="a7d22-107">ErrorDetail.Code</span></span> | <span data-ttu-id="a7d22-108">Posibles causas de error</span><span class="sxs-lookup"><span data-stu-id="a7d22-108">Possible causes for error</span></span> |
| --- | --- |
| <span data-ttu-id="a7d22-109">Desconocido</span><span class="sxs-lookup"><span data-stu-id="a7d22-109">Unknown</span></span> |<span data-ttu-id="a7d22-110">Error desconocido al ejecutar la tarea hello</span><span class="sxs-lookup"><span data-stu-id="a7d22-110">Unknown error while executing hello task</span></span> |
| <span data-ttu-id="a7d22-111">ErrorDownloadingInputAssetMalformedContent</span><span class="sxs-lookup"><span data-stu-id="a7d22-111">ErrorDownloadingInputAssetMalformedContent</span></span> |<span data-ttu-id="a7d22-112">Categoría de errores en la que se incluyen errores en la descarga de recursos de entrada, como nombres de archivo no válidos, archivos de longitud cero, formatos incorrectos, etc.</span><span class="sxs-lookup"><span data-stu-id="a7d22-112">Category of errors that covers errors in downloading input asset such as bad file names, zero length files, incorrect formats and so on.</span></span> |
| <span data-ttu-id="a7d22-113">ErrorDownloadingInputAssetServiceFailure</span><span class="sxs-lookup"><span data-stu-id="a7d22-113">ErrorDownloadingInputAssetServiceFailure</span></span> |<span data-ttu-id="a7d22-114">Categoría de errores que se trata problemas en lado de servicio de hello - errores de red o almacenamiento de ejemplo mientras se descargaba.</span><span class="sxs-lookup"><span data-stu-id="a7d22-114">Category of errors that covers problems on hello service side - for example network or storage errors while downloading.</span></span> |
| <span data-ttu-id="a7d22-115">ErrorParsingConfiguration</span><span class="sxs-lookup"><span data-stu-id="a7d22-115">ErrorParsingConfiguration</span></span> |<span data-ttu-id="a7d22-116">Categoría de errores donde tarea <see cref="MediaTask.PrivateData"/> (configuración) no es válida, por ejemplo Hola configuración no es un sistema válido preestablecido o contiene un XML no válido.</span><span class="sxs-lookup"><span data-stu-id="a7d22-116">Category of errors where task <see cref="MediaTask.PrivateData"/> (configuration) is not valid, for example hello configuration is not a valid system preset or it contains invalid XML.</span></span> |
| <span data-ttu-id="a7d22-117">ErrorExecutingTaskMalformedContent</span><span class="sxs-lookup"><span data-stu-id="a7d22-117">ErrorExecutingTaskMalformedContent</span></span> |<span data-ttu-id="a7d22-118">Categoría de errores durante la ejecución de Hola de tarea hello donde problemas dentro de hello entrada archivos multimedia provocan un error.</span><span class="sxs-lookup"><span data-stu-id="a7d22-118">Category of errors during hello execution of hello task where issues inside hello input media files cause failure.</span></span> |
| <span data-ttu-id="a7d22-119">ErrorExecutingTaskUnsupportedFormat</span><span class="sxs-lookup"><span data-stu-id="a7d22-119">ErrorExecutingTaskUnsupportedFormat</span></span> |<span data-ttu-id="a7d22-120">Categoría de errores donde procesador de multimedia de hello no puede procesar archivos Hola proporcionados: media de formato no compatible o no coincide con la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="a7d22-120">Category of errors where hello media processor cannot process hello files provided - media format not supported, or does not match hello Configuration.</span></span> <span data-ttu-id="a7d22-121">Por ejemplo, al tratar de tooproduce una salida de solo audio desde un recurso que tiene solo vídeo</span><span class="sxs-lookup"><span data-stu-id="a7d22-121">For example, trying tooproduce an audio-only output from an asset that has only video</span></span> |
| <span data-ttu-id="a7d22-122">ErrorProcessingTask</span><span class="sxs-lookup"><span data-stu-id="a7d22-122">ErrorProcessingTask</span></span> |<span data-ttu-id="a7d22-123">Categoría de otros errores que Hola procesador multimedia se encuentra durante el procesamiento de Hola de tarea de Hola que están relacionados con toocontent.</span><span class="sxs-lookup"><span data-stu-id="a7d22-123">Category of other errors that hello media processor encounters during hello processing of hello task that are unrelated toocontent.</span></span> |
| <span data-ttu-id="a7d22-124">ErrorUploadingOutputAsset</span><span class="sxs-lookup"><span data-stu-id="a7d22-124">ErrorUploadingOutputAsset</span></span> |<span data-ttu-id="a7d22-125">Categoría de errores al cargar el recurso de salida de hello</span><span class="sxs-lookup"><span data-stu-id="a7d22-125">Category of errors when uploading hello output asset</span></span> |
| <span data-ttu-id="a7d22-126">ErrorCancelingTask</span><span class="sxs-lookup"><span data-stu-id="a7d22-126">ErrorCancelingTask</span></span> |<span data-ttu-id="a7d22-127">Categoría de errores de toocover de errores al intentar toocancel Hola tarea</span><span class="sxs-lookup"><span data-stu-id="a7d22-127">Category of errors toocover failures when attempting toocancel hello Task</span></span> |
| <span data-ttu-id="a7d22-128">TransientError</span><span class="sxs-lookup"><span data-stu-id="a7d22-128">TransientError</span></span> |<span data-ttu-id="a7d22-129">Categoría de errores toocover problemas transitorios (p. ej.</span><span class="sxs-lookup"><span data-stu-id="a7d22-129">Category of errors toocover transient issues (eg.</span></span> <span data-ttu-id="a7d22-130">ej., problemas de red temporales con Almacenamiento de Azure).</span><span class="sxs-lookup"><span data-stu-id="a7d22-130">temporary networking issues with Azure Storage)</span></span> |

<span data-ttu-id="a7d22-131">Ayuda de tooget de hello **servicios multimedia** equipo, abra un [incidencia de soporte técnico](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="a7d22-131">tooget help from hello **Media Services** team, open a [support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="a7d22-132">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="a7d22-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a7d22-133">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="a7d22-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="a7d22-134">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="a7d22-134">Related articles</span></span>
* [<span data-ttu-id="a7d22-135">Realización de tareas de codificación avanzadas mediante la personalización de valores preestablecidos de Media Encoder Estándar</span><span class="sxs-lookup"><span data-stu-id="a7d22-135">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="a7d22-136">Cuotas y limitaciones</span><span class="sxs-lookup"><span data-stu-id="a7d22-136">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
