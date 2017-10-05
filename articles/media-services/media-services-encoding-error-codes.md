---
title: "Códigos de error de codificación de Azure Media Services | Microsoft Docs"
description: "En este tema se indican los códigos de error que se podrían devolver en caso de que se encuentre un error durante la ejecución de la tarea de Encoding."
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
ms.openlocfilehash: f4fd2212d19f89148dde08c75c5a48cdd322d029
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="encoding-error-codes"></a><span data-ttu-id="11bad-103">Códigos de error de Encoding</span><span class="sxs-lookup"><span data-stu-id="11bad-103">Encoding error codes</span></span>

<span data-ttu-id="11bad-104">En la tabla siguiente se indican los códigos de error que se podrían devolver en caso de que se encuentre un error durante la ejecución de la tarea de codificación.</span><span class="sxs-lookup"><span data-stu-id="11bad-104">The following table lists error codes that could be returned in case an error was encountered during the encoding task execution.</span></span>  <span data-ttu-id="11bad-105">Para obtener detalles del error en el código .NET, use la clase [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) .</span><span class="sxs-lookup"><span data-stu-id="11bad-105">To get error details in your .NET code, use the [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) class.</span></span> <span data-ttu-id="11bad-106">Para obtener detalles del error en el código REST, use la API de REST [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) .</span><span class="sxs-lookup"><span data-stu-id="11bad-106">To get error details in your REST code, use the [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST API.</span></span>

| <span data-ttu-id="11bad-107">ErrorDetail.Code</span><span class="sxs-lookup"><span data-stu-id="11bad-107">ErrorDetail.Code</span></span> | <span data-ttu-id="11bad-108">Posibles causas de error</span><span class="sxs-lookup"><span data-stu-id="11bad-108">Possible causes for error</span></span> |
| --- | --- |
| <span data-ttu-id="11bad-109">Desconocido</span><span class="sxs-lookup"><span data-stu-id="11bad-109">Unknown</span></span> |<span data-ttu-id="11bad-110">Error desconocido al ejecutar la tarea</span><span class="sxs-lookup"><span data-stu-id="11bad-110">Unknown error while executing the task</span></span> |
| <span data-ttu-id="11bad-111">ErrorDownloadingInputAssetMalformedContent</span><span class="sxs-lookup"><span data-stu-id="11bad-111">ErrorDownloadingInputAssetMalformedContent</span></span> |<span data-ttu-id="11bad-112">Categoría de errores en la que se incluyen errores en la descarga de recursos de entrada, como nombres de archivo no válidos, archivos de longitud cero, formatos incorrectos, etc.</span><span class="sxs-lookup"><span data-stu-id="11bad-112">Category of errors that covers errors in downloading input asset such as bad file names, zero length files, incorrect formats and so on.</span></span> |
| <span data-ttu-id="11bad-113">ErrorDownloadingInputAssetServiceFailure</span><span class="sxs-lookup"><span data-stu-id="11bad-113">ErrorDownloadingInputAssetServiceFailure</span></span> |<span data-ttu-id="11bad-114">Categoría de errores en la que se incluyen problemas en el servicio, por ejemplo, errores de red o de almacenamiento durante la descarga.</span><span class="sxs-lookup"><span data-stu-id="11bad-114">Category of errors that covers problems on the service side - for example network or storage errors while downloading.</span></span> |
| <span data-ttu-id="11bad-115">ErrorParsingConfiguration</span><span class="sxs-lookup"><span data-stu-id="11bad-115">ErrorParsingConfiguration</span></span> |<span data-ttu-id="11bad-116">Categoría de errores en la que la tarea <see cref="MediaTask.PrivateData"/> (configuración) no es válida; por ejemplo, la configuración no es un valor preestablecido del sistema válido o contiene XML no válido.</span><span class="sxs-lookup"><span data-stu-id="11bad-116">Category of errors where task <see cref="MediaTask.PrivateData"/> (configuration) is not valid, for example the configuration is not a valid system preset or it contains invalid XML.</span></span> |
| <span data-ttu-id="11bad-117">ErrorExecutingTaskMalformedContent</span><span class="sxs-lookup"><span data-stu-id="11bad-117">ErrorExecutingTaskMalformedContent</span></span> |<span data-ttu-id="11bad-118">Categoría de errores durante la ejecución de la tarea en la que problemas en los archivos multimedia de entrada provocan errores.</span><span class="sxs-lookup"><span data-stu-id="11bad-118">Category of errors during the execution of the task where issues inside the input media files cause failure.</span></span> |
| <span data-ttu-id="11bad-119">ErrorExecutingTaskUnsupportedFormat</span><span class="sxs-lookup"><span data-stu-id="11bad-119">ErrorExecutingTaskUnsupportedFormat</span></span> |<span data-ttu-id="11bad-120">Categoría de errores en la que el procesador de contenido multimedia no puede procesar los archivos proporcionados: formato de contenido multimedia no compatible o que no coincide con la configuración.</span><span class="sxs-lookup"><span data-stu-id="11bad-120">Category of errors where the media processor cannot process the files provided - media format not supported, or does not match the Configuration.</span></span> <span data-ttu-id="11bad-121">Por ejemplo, intentar producir una salida de solo audio desde un activo que tenga solo vídeo.</span><span class="sxs-lookup"><span data-stu-id="11bad-121">For example, trying to produce an audio-only output from an asset that has only video</span></span> |
| <span data-ttu-id="11bad-122">ErrorProcessingTask</span><span class="sxs-lookup"><span data-stu-id="11bad-122">ErrorProcessingTask</span></span> |<span data-ttu-id="11bad-123">Categoría de otros errores que detecta el procesador de contenido multimedia durante el procesamiento de la tarea y que no están relacionados con el contenido.</span><span class="sxs-lookup"><span data-stu-id="11bad-123">Category of other errors that the media processor encounters during the processing of the task that are unrelated to content.</span></span> |
| <span data-ttu-id="11bad-124">ErrorUploadingOutputAsset</span><span class="sxs-lookup"><span data-stu-id="11bad-124">ErrorUploadingOutputAsset</span></span> |<span data-ttu-id="11bad-125">Categoría de errores al cargar el activo de salida.</span><span class="sxs-lookup"><span data-stu-id="11bad-125">Category of errors when uploading the output asset</span></span> |
| <span data-ttu-id="11bad-126">ErrorCancelingTask</span><span class="sxs-lookup"><span data-stu-id="11bad-126">ErrorCancelingTask</span></span> |<span data-ttu-id="11bad-127">Categoría de errores en la que se incluyen errores al intentar cancelar la tarea.</span><span class="sxs-lookup"><span data-stu-id="11bad-127">Category of errors to cover failures when attempting to cancel the Task</span></span> |
| <span data-ttu-id="11bad-128">TransientError</span><span class="sxs-lookup"><span data-stu-id="11bad-128">TransientError</span></span> |<span data-ttu-id="11bad-129">Categoría de errores en la que se incluyen problemas transitorios (p.</span><span class="sxs-lookup"><span data-stu-id="11bad-129">Category of errors to cover transient issues (eg.</span></span> <span data-ttu-id="11bad-130">ej., problemas de red temporales con Almacenamiento de Azure).</span><span class="sxs-lookup"><span data-stu-id="11bad-130">temporary networking issues with Azure Storage)</span></span> |

<span data-ttu-id="11bad-131">Para obtener ayuda del equipo de **Servicios multimedia** , abra una [incidencia de soporte técnico](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="11bad-131">To get help from the **Media Services** team, open a [support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="11bad-132">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="11bad-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="11bad-133">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="11bad-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="11bad-134">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="11bad-134">Related articles</span></span>
* [<span data-ttu-id="11bad-135">Realización de tareas de codificación avanzadas mediante la personalización de valores preestablecidos de Media Encoder Estándar</span><span class="sxs-lookup"><span data-stu-id="11bad-135">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="11bad-136">Cuotas y limitaciones</span><span class="sxs-lookup"><span data-stu-id="11bad-136">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
