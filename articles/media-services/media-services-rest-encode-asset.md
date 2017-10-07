---
title: "aaaHow tooencode un recurso de Azure mediante el uso de medios codificador estándar | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Media Encoder estándar tooencode medios de contenido en servicios multimedia de Azure. Los ejemplos de código usan la API de REST."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2a7273c6-8a22-4f82-9bfe-4509ff32d4a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: b766bafded7ee98eda3e6ef149c31d5d8fe406fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencode-an-asset-by-using-media-encoder-standard"></a><span data-ttu-id="ac31e-104">¿Cómo tooencode un activo mediante el uso de medios codificador estándar</span><span class="sxs-lookup"><span data-stu-id="ac31e-104">How tooencode an asset by using Media Encoder Standard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ac31e-105">.NET</span><span class="sxs-lookup"><span data-stu-id="ac31e-105">.NET</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [<span data-ttu-id="ac31e-106">REST</span><span class="sxs-lookup"><span data-stu-id="ac31e-106">REST</span></span>](media-services-rest-encode-asset.md)
> * [<span data-ttu-id="ac31e-107">Portal</span><span class="sxs-lookup"><span data-stu-id="ac31e-107">Portal</span></span>](media-services-portal-encode.md)
>
>

## <a name="overview"></a><span data-ttu-id="ac31e-108">Información general</span><span class="sxs-lookup"><span data-stu-id="ac31e-108">Overview</span></span>
<span data-ttu-id="ac31e-109">toodeliver vídeo digital a través de Internet de hello, debe comprimir medios Hola.</span><span class="sxs-lookup"><span data-stu-id="ac31e-109">toodeliver digital video over hello Internet, you must compress hello media.</span></span> <span data-ttu-id="ac31e-110">Archivos de vídeo digital son grandes y pueden ser demasiado grande toodeliver a través de Internet de hello, o para toodisplay de dispositivos de los clientes correctamente.</span><span class="sxs-lookup"><span data-stu-id="ac31e-110">Digital video files are large and may be too big toodeliver over hello Internet, or for your customers’ devices toodisplay properly.</span></span> <span data-ttu-id="ac31e-111">La codificación es el proceso de Hola de compresión de vídeo y audio para que los clientes puedan ver los medios.</span><span class="sxs-lookup"><span data-stu-id="ac31e-111">Encoding is hello process of compressing video and audio so your customers can view your media.</span></span>

<span data-ttu-id="ac31e-112">Trabajos de codificación son una de las operaciones de procesamiento más habituales de hello en los servicios de multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="ac31e-112">Encoding jobs are one of hello most common processing operations in Azure Media Services.</span></span> <span data-ttu-id="ac31e-113">Crear archivos multimedia de codificación trabajos tooconvert desde una tooanother de codificación.</span><span class="sxs-lookup"><span data-stu-id="ac31e-113">You create encoding jobs tooconvert media files from one encoding tooanother.</span></span> <span data-ttu-id="ac31e-114">Al codificar, puede usar (estándar de codificador multimedia) de codificador integrado de servicios multimedia de Hola.</span><span class="sxs-lookup"><span data-stu-id="ac31e-114">When you encode, you can use hello Media Services built-in encoder (Media Encoder Standard).</span></span> <span data-ttu-id="ac31e-115">También puede usar un codificador proporcionado por un partner de Media Services.</span><span class="sxs-lookup"><span data-stu-id="ac31e-115">You can also use an encoder provided by a Media Services partner.</span></span> <span data-ttu-id="ac31e-116">Codificadores de terceros están disponibles a través de hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ac31e-116">Third-party encoders are available through hello Azure Marketplace.</span></span> <span data-ttu-id="ac31e-117">Puede especificar detalles de Hola de tareas de codificación mediante cadenas de valores preestablecidos definidas para el codificador o mediante el uso de archivos de configuración de valores predefinidos.</span><span class="sxs-lookup"><span data-stu-id="ac31e-117">You can specify hello details of encoding tasks by using preset strings defined for your encoder, or by using preset configuration files.</span></span> <span data-ttu-id="ac31e-118">toosee Hola tipos de valores predefinidos que están disponibles, consulte [valores preestablecidos de tarea para Media Encoder estándar](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="ac31e-118">toosee hello types of presets that are available, see [Task Presets for Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="ac31e-119">Cada trabajo puede tener uno o más tareas según el tipo de saludo de procesamiento que desea tooaccomplish.</span><span class="sxs-lookup"><span data-stu-id="ac31e-119">Each job can have one or more tasks depending on hello type of processing that you want tooaccomplish.</span></span> <span data-ttu-id="ac31e-120">A través de la API de REST de hello, puede crear trabajos y sus tareas relacionadas en una de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="ac31e-120">Through hello REST API, you can create jobs and their related tasks in one of two ways:</span></span>

* <span data-ttu-id="ac31e-121">Las tareas pueden definir en línea a través de la propiedad de navegación de las tareas de hello en entidades de trabajos.</span><span class="sxs-lookup"><span data-stu-id="ac31e-121">Tasks can be defined inline through hello Tasks navigation property on Job entities.</span></span>
* <span data-ttu-id="ac31e-122">Uso del procesamiento por lotes de OData.</span><span class="sxs-lookup"><span data-stu-id="ac31e-122">Use OData batch processing.</span></span>

<span data-ttu-id="ac31e-123">Se recomienda codificar siempre los archivos de origen en un conjunto de MP4 de velocidad de bits adaptativa y, a continuación, convertir el formato deseado de hello conjunto toohello mediante [empaquetado dinámico](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ac31e-123">We recommend that you always encode your source files into an adaptive bitrate MP4 set, and then convert hello set toohello desired format by using [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>

<span data-ttu-id="ac31e-124">Si su recurso de salida es el almacenamiento de cifrado, debe configurar la directiva de entrega del activo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ac31e-124">If your output asset is storage encrypted, you must configure hello asset delivery policy.</span></span> <span data-ttu-id="ac31e-125">Para obtener más información, consulte [Configuración de directivas de entrega de recursos](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="ac31e-125">For more information, see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="ac31e-126">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="ac31e-126">Considerations</span></span>

<span data-ttu-id="ac31e-127">Al obtener acceso a las entidades de Servicios multimedia, debe establecer los campos de encabezado específicos y los valores en las solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="ac31e-127">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="ac31e-128">Para obtener más información, consulte [Configuración del desarrollo de la API de REST de Servicios multimedia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="ac31e-128">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

<span data-ttu-id="ac31e-129">Antes de iniciar que hacen referencia a procesadores multimedia, compruebe que haya Hola Id. de procesador de medios correctos.</span><span class="sxs-lookup"><span data-stu-id="ac31e-129">Before you start referencing media processors, verify that you have hello correct media processor ID.</span></span> <span data-ttu-id="ac31e-130">Para obtener más información, consulte [Obtención de procesadores multimedia](media-services-rest-get-media-processor.md).</span><span class="sxs-lookup"><span data-stu-id="ac31e-130">For more information, see [Get media processors](media-services-rest-get-media-processor.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="ac31e-131">Conectar servicios de tooMedia</span><span class="sxs-lookup"><span data-stu-id="ac31e-131">Connect tooMedia Services</span></span>

<span data-ttu-id="ac31e-132">Para obtener información sobre cómo tooconnect toohello AMS API, consulte [Hola acceso API de servicios multimedia de Azure con autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="ac31e-132">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="ac31e-133">Después de conectarse correctamente toohttps://media.windows.net, recibirá una redirección 301 especificando otra URI de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="ac31e-133">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="ac31e-134">Debe realizar las llamadas subsiguientes toohello nuevo URI.</span><span class="sxs-lookup"><span data-stu-id="ac31e-134">You must make subsequent calls toohello new URI.</span></span>

## <a name="create-a-job-with-a-single-encoding-task"></a><span data-ttu-id="ac31e-135">Creación de un trabajo con una sola tarea de codificación</span><span class="sxs-lookup"><span data-stu-id="ac31e-135">Create a job with a single encoding task</span></span>
> [!NOTE]
> <span data-ttu-id="ac31e-136">Cuando se trabaja con API de REST de servicios multimedia de hello, hello siguientes consideraciones:</span><span class="sxs-lookup"><span data-stu-id="ac31e-136">When you're working with hello Media Services REST API, hello following considerations apply:</span></span>
>
> <span data-ttu-id="ac31e-137">Al obtener acceso a las entidades de Servicios multimedia, debe establecer los campos de encabezado específicos y los valores en las solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="ac31e-137">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="ac31e-138">Para obtener más información, consulte [Configuración del desarrollo de la API de REST de Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="ac31e-138">For more information, see [Setup for Media Services REST API development](media-services-rest-how-to-use.md).</span></span>
>
> <span data-ttu-id="ac31e-139">Después de conectarse correctamente toohttps://media.windows.net, recibirá una redirección 301 especificando otra URI de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="ac31e-139">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="ac31e-140">Debe realizar las llamadas subsiguientes toohello nuevo URI.</span><span class="sxs-lookup"><span data-stu-id="ac31e-140">You must make subsequent calls toohello new URI.</span></span> <span data-ttu-id="ac31e-141">Para obtener información sobre cómo tooconnect toohello AMS API, consulte [Hola acceso API de servicios multimedia de Azure con autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="ac31e-141">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
>
> <span data-ttu-id="ac31e-142">Cuando usa JSON y especifica toouse hello **__metadata** palabra clave en la solicitud de hello (por ejemplo, tooreferences un objeto vinculado), debe establecer hello **Accept** encabezado demasiado[formato JSON detallado ](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Aceptar: application/json; odata = detallado.</span><span class="sxs-lookup"><span data-stu-id="ac31e-142">When using JSON and specifying toouse hello **__metadata** keyword in hello request (for example, tooreferences a linked object), you must set hello **Accept** header too[JSON Verbose format](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accept: application/json;odata=verbose.</span></span>
>
>

<span data-ttu-id="ac31e-143">Hola de ejemplo siguiente muestra cómo toocreate y post un trabajo con una tarea establece tooencode un vídeo en una resolución y calidad específicas.</span><span class="sxs-lookup"><span data-stu-id="ac31e-143">hello following example shows you how toocreate and post a job with one task set tooencode a video at a specific resolution and quality.</span></span> <span data-ttu-id="ac31e-144">Al codificar con Media Encoder Standard, puede usar los valores preestablecidos de configuración de tareas especificados [aquí](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="ac31e-144">When you encode with Media Encoder Standard, you can use task configuration presets specified [here](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="ac31e-145">Solicitud:</span><span class="sxs-lookup"><span data-stu-id="ac31e-145">Request:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net

    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aaab7f15b-3136-4ddf-9962-e9ecb28fb9d2')"}}],  "Tasks" : [{"Configuration" : "Adaptive Streaming", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",  "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"}]}

<span data-ttu-id="ac31e-146">Respuesta:</span><span class="sxs-lookup"><span data-stu-id="ac31e-146">Response:</span></span>

    HTTP/1.1 201 Created

    . . .

### <a name="set-hello-output-assets-name"></a><span data-ttu-id="ac31e-147">Establece el nombre del recurso de salida de hello</span><span class="sxs-lookup"><span data-stu-id="ac31e-147">Set hello output asset's name</span></span>
<span data-ttu-id="ac31e-148">Hola de ejemplo siguiente muestra cómo tooset Hola atributo assetName:</span><span class="sxs-lookup"><span data-stu-id="ac31e-148">hello following example shows how tooset hello assetName attribute:</span></span>

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a><span data-ttu-id="ac31e-149">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="ac31e-149">Considerations</span></span>
* <span data-ttu-id="ac31e-150">Propiedades TaskBody deben usar el número de hello literal de toodefine XML de entrada o recursos de salida que se usan por tarea hello.</span><span class="sxs-lookup"><span data-stu-id="ac31e-150">TaskBody properties must use literal XML toodefine hello number of input, or output assets that are used by hello task.</span></span> <span data-ttu-id="ac31e-151">tema de la tarea Hello contiene Hola definición de esquemas XML para hello XML.</span><span class="sxs-lookup"><span data-stu-id="ac31e-151">hello task topic contains hello XML Schema Definition for hello XML.</span></span>
* <span data-ttu-id="ac31e-152">Hola definición TaskBody, cada interna valor <inputAsset> y <outputAsset> debe establecerse como JobInputAsset(value) o JobOutputAsset(value).</span><span class="sxs-lookup"><span data-stu-id="ac31e-152">In hello TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="ac31e-153">Una tarea puede tener varios recursos de salida.</span><span class="sxs-lookup"><span data-stu-id="ac31e-153">A task can have multiple output assets.</span></span> <span data-ttu-id="ac31e-154">Un elemento JobOutputAsset(x) solo se puede usar una vez como salida de una tarea en un trabajo.</span><span class="sxs-lookup"><span data-stu-id="ac31e-154">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="ac31e-155">Puede especificar JobInputAsset o JobOutputAsset como un recurso de entrada de una tarea.</span><span class="sxs-lookup"><span data-stu-id="ac31e-155">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="ac31e-156">Las tareas no pueden formar un ciclo.</span><span class="sxs-lookup"><span data-stu-id="ac31e-156">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="ac31e-157">valor del parámetro Hello que pasar tooJobInputAsset o JobOutputAsset representa el valor de índice de Hola para un activo.</span><span class="sxs-lookup"><span data-stu-id="ac31e-157">hello value parameter that you pass tooJobInputAsset or JobOutputAsset represents hello index value for an asset.</span></span> <span data-ttu-id="ac31e-158">recursos reales de Hola se definen en hello InputMediaAssets y OutputMediaAssets propiedades de navegación en la definición de la entidad de hello trabajo.</span><span class="sxs-lookup"><span data-stu-id="ac31e-158">hello actual assets are defined in hello InputMediaAssets and OutputMediaAssets navigation properties on hello job entity definition.</span></span>
* <span data-ttu-id="ac31e-159">Dado que los servicios multimedia se fundamentan en OData v3, Hola activos individuales en hello InputMediaAssets y OutputMediaAssets colecciones de propiedades de navegación se hace referencia a través de un "__metadata: uri" par nombre / valor.</span><span class="sxs-lookup"><span data-stu-id="ac31e-159">Because Media Services is built on OData v3, hello individual assets in hello InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
* <span data-ttu-id="ac31e-160">InputMediaAssets asigna tooone o más activos que creó en los servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="ac31e-160">InputMediaAssets maps tooone or more assets that you created in Media Services.</span></span> <span data-ttu-id="ac31e-161">Sistema de hello crea los OutputMediaAssets.</span><span class="sxs-lookup"><span data-stu-id="ac31e-161">OutputMediaAssets are created by hello system.</span></span> <span data-ttu-id="ac31e-162">Estos no hacen referencia a ningún recurso existente.</span><span class="sxs-lookup"><span data-stu-id="ac31e-162">They don't reference an existing asset.</span></span>
* <span data-ttu-id="ac31e-163">Los OutputMediaAssets puede llamarse mediante hello assetName atributo.</span><span class="sxs-lookup"><span data-stu-id="ac31e-163">OutputMediaAssets can be named by using hello assetName attribute.</span></span> <span data-ttu-id="ac31e-164">Si este atributo no está presente, el nombre de Hola de hello OutputMediaAsset es cualquier valor de texto interno de Hola de hello <outputAsset> elemento es con un sufijo de valor de nombre del trabajo de Hola o valor de Id. de trabajo de hello (en caso de hello donde no se ha definido la propiedad de nombre de hello).</span><span class="sxs-lookup"><span data-stu-id="ac31e-164">If this attribute is not present, then hello name of hello OutputMediaAsset is whatever hello inner text value of hello <outputAsset> element is with a suffix of either hello Job Name value, or hello Job Id value (in hello case where hello Name property isn't defined).</span></span> <span data-ttu-id="ac31e-165">Por ejemplo, si establece un valor para assetName demasiado "Sample" y, a continuación, Hola nombre OutputMediaAsset se establece la propiedad demasiado "Sample."</span><span class="sxs-lookup"><span data-stu-id="ac31e-165">For example, if you set a value for assetName too"Sample," then hello OutputMediaAsset Name property is set too"Sample."</span></span> <span data-ttu-id="ac31e-166">Sin embargo, si no ha configurado un valor para assetName, pero ha especificado el nombre del trabajo Hola demasiado "como NewJob" y, a continuación, Hola nombre OutputMediaAsset sería "JobOutputAsset (valor) _NewJob".</span><span class="sxs-lookup"><span data-stu-id="ac31e-166">However, if you didn't set a value for assetName, but did set hello job name too"NewJob," then hello OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob."</span></span>

## <a name="create-a-job-with-chained-tasks"></a><span data-ttu-id="ac31e-167">Creación de un trabajo con tareas encadenadas</span><span class="sxs-lookup"><span data-stu-id="ac31e-167">Create a job with chained tasks</span></span>
<span data-ttu-id="ac31e-168">En muchos escenarios de aplicación, los desarrolladores desean toocreate una serie de tareas de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="ac31e-168">In many application scenarios, developers want toocreate a series of processing tasks.</span></span> <span data-ttu-id="ac31e-169">En Servicios multimedia, puede crear una serie de tareas encadenadas.</span><span class="sxs-lookup"><span data-stu-id="ac31e-169">In Media Services, you can create a series of chained tasks.</span></span> <span data-ttu-id="ac31e-170">Cada tarea realiza distintos pasos de procesamiento diferentes y puede usar diferentes procesadores multimedia.</span><span class="sxs-lookup"><span data-stu-id="ac31e-170">Each task performs different processing steps and can use different media processors.</span></span> <span data-ttu-id="ac31e-171">tareas de Hello encadenada pueden entregar un activo de una tarea tooanother, realizar una secuencia lineal de tareas en activos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ac31e-171">hello chained tasks can hand off an asset from one task tooanother, performing a linear sequence of tasks on hello asset.</span></span> <span data-ttu-id="ac31e-172">Sin embargo, las tareas de hello realizadas en un trabajo no son toobe necesario en una secuencia.</span><span class="sxs-lookup"><span data-stu-id="ac31e-172">However, hello tasks performed in a job are not required toobe in a sequence.</span></span> <span data-ttu-id="ac31e-173">Cuando se crea una tarea encadenada, Hola encadenadas **ITask** objetos se crean en un único **IJob** objeto.</span><span class="sxs-lookup"><span data-stu-id="ac31e-173">When you create a chained task, hello chained **ITask** objects are created in a single **IJob** object.</span></span>

> [!NOTE]
> <span data-ttu-id="ac31e-174">Actualmente hay un límite de 30 tareas por trabajo.</span><span class="sxs-lookup"><span data-stu-id="ac31e-174">There is currently a limit of 30 tasks per job.</span></span> <span data-ttu-id="ac31e-175">Si necesita más de 30 tareas toochain, cree más de un trabajo de tareas de Hola de toocontain.</span><span class="sxs-lookup"><span data-stu-id="ac31e-175">If you need toochain more than 30 tasks, create more than one job toocontain hello tasks.</span></span>
>
>

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://testrest.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A910ffdc1-2e25-4b17-8a42-61ffd4b8914c')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          },
          {  
             "Configuration":"H264 Smooth Streaming 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-16\"?><taskBody><inputAsset>JobOutputAsset(0)</inputAsset><outputAsset>JobOutputAsset(1)</outputAsset></taskBody>"
          }
       ]
    }


### <a name="considerations"></a><span data-ttu-id="ac31e-176">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="ac31e-176">Considerations</span></span>
<span data-ttu-id="ac31e-177">tooenable encadenamiento de tareas:</span><span class="sxs-lookup"><span data-stu-id="ac31e-177">tooenable task chaining:</span></span>

* <span data-ttu-id="ac31e-178">Un trabajo debe tener al menos dos tareas.</span><span class="sxs-lookup"><span data-stu-id="ac31e-178">A job must have at least two tasks.</span></span>
* <span data-ttu-id="ac31e-179">Debe haber al menos una tarea cuya entrada sea salida de hello de otra tarea en el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ac31e-179">There must be at least one task whose input is hello output of another task in hello job.</span></span>

## <a name="use-odata-batch-processing"></a><span data-ttu-id="ac31e-180">Uso del procesamiento por lotes de OData</span><span class="sxs-lookup"><span data-stu-id="ac31e-180">Use OData batch processing</span></span>
<span data-ttu-id="ac31e-181">Hola de ejemplo siguiente muestra cómo toouse OData por lotes las toocreate de procesamiento de un trabajo y tareas.</span><span class="sxs-lookup"><span data-stu-id="ac31e-181">hello following example shows how toouse OData batch processing toocreate a job and tasks.</span></span> <span data-ttu-id="ac31e-182">Para obtener información sobre el procesamiento por lotes, consulte [Procesamiento por lotes del protocolo Open Data (OData)](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="ac31e-182">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

    POST https://media.windows.net/api/$batch HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: multipart/mixed; boundary=batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Accept: multipart/mixed
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net


    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Content-Type: multipart/mixed; boundary=changeset_122fb0a4-cd80-4958-820f-346309967e4d

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-ID: 1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {"Name" : "NewTestJob", "InputMediaAssets@odata.bind":["https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A2a22445d-1500-80c6-4b34-f1e5190d33c6')"]}

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/$1/Tasks HTTP/1.1
    Content-ID: 2
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
       "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
       "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"Custom output name\">JobOutputAsset(0)</outputAsset></taskBody>"
    }

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d--
    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e--



## <a name="create-a-job-by-using-a-jobtemplate"></a><span data-ttu-id="ac31e-183">Creación de un trabajo mediante una plantilla JobTemplate</span><span class="sxs-lookup"><span data-stu-id="ac31e-183">Create a job by using a JobTemplate</span></span>
<span data-ttu-id="ac31e-184">Cuando se procesan varios recursos mediante el uso de un conjunto común de tareas, utilice que una tarea de forma predeterminada de JobTemplate toospecify Hola presintonías u orden de hello tooset de tareas.</span><span class="sxs-lookup"><span data-stu-id="ac31e-184">When you process multiple assets by using a common set of tasks, use a JobTemplate toospecify hello default task presets, or tooset hello order of tasks.</span></span>

<span data-ttu-id="ac31e-185">Hola siguiente ejemplo muestra cómo toocreate una JobTemplate con una TaskTemplate que está había definido en línea.</span><span class="sxs-lookup"><span data-stu-id="ac31e-185">hello following example shows how toocreate a JobTemplate with a TaskTemplate that is defined inline.</span></span> <span data-ttu-id="ac31e-186">Hola TaskTemplate usa Hola Media Encoder estándar como archivo de recursos de hello MediaProcessor tooencode Hola.</span><span class="sxs-lookup"><span data-stu-id="ac31e-186">hello TaskTemplate uses hello Media Encoder Standard as hello MediaProcessor tooencode hello asset file.</span></span> <span data-ttu-id="ac31e-187">Sin embargo, también se pueden usar otros elementos MediaProcessor.</span><span class="sxs-lookup"><span data-stu-id="ac31e-187">However, other MediaProcessors can be used as well.</span></span>

    POST https://media.windows.net/API/JobTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewJobTemplate25", "JobTemplateBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><jobTemplate><taskBody taskTemplateId=\"nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789\"><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody></jobTemplate>", "TaskTemplates" : [{"Id" : "nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789", "Configuration" : "H264 Smooth Streaming 720p", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56", "Name" : "SampleTaskTemplate2", "NumberofInputAssets" : 1, "NumberofOutputAssets" : 1}] }


> [!NOTE]
> <span data-ttu-id="ac31e-188">A diferencia de otras entidades de servicios multimedia, debe definir un nuevo identificador GUID para cada TaskTemplate y colocarlo en taskTemplateId de Hola y la propiedad Id en el cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="ac31e-188">Unlike other Media Services entities, you must define a new GUID identifier for each TaskTemplate and place it in hello taskTemplateId and Id property in your request body.</span></span> <span data-ttu-id="ac31e-189">esquema de identificación de contenido de Hello debe seguir el esquema de hello descrito en identificar las entidades de servicios de multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="ac31e-189">hello content identification scheme must follow hello scheme described in Identify Azure Media Services Entities.</span></span> <span data-ttu-id="ac31e-190">Además, las plantillas de trabajo no se pueden actualizar.</span><span class="sxs-lookup"><span data-stu-id="ac31e-190">Also, JobTemplates cannot be updated.</span></span> <span data-ttu-id="ac31e-191">Por el contrario, debe crear una nueva con los cambios actualizados.</span><span class="sxs-lookup"><span data-stu-id="ac31e-191">Instead, you must create a new one with your updated changes.</span></span>
>
>

<span data-ttu-id="ac31e-192">Si se realiza correctamente, se devuelve Hola después de respuesta:</span><span class="sxs-lookup"><span data-stu-id="ac31e-192">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .


<span data-ttu-id="ac31e-193">Hola siguiente ejemplo se muestra cómo toocreate un trabajo que hace referencia a un identificador de JobTemplate:</span><span class="sxs-lookup"><span data-stu-id="ac31e-193">hello following example shows how toocreate a job that references a JobTemplate Id:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


<span data-ttu-id="ac31e-194">Si se realiza correctamente, se devuelve Hola después de respuesta:</span><span class="sxs-lookup"><span data-stu-id="ac31e-194">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .



## <a name="media-services-learning-paths"></a><span data-ttu-id="ac31e-195">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="ac31e-195">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ac31e-196">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="ac31e-196">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="ac31e-197">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ac31e-197">Next steps</span></span>
<span data-ttu-id="ac31e-198">Ahora que sabe cómo toocreate una tooencode trabajo un activo, consulte [cómo toocheck trabajo progreso con servicios multimedia](media-services-rest-check-job-progress.md).</span><span class="sxs-lookup"><span data-stu-id="ac31e-198">Now that you know how toocreate a job tooencode an asset, see [How toocheck job progress with Media Services](media-services-rest-check-job-progress.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="ac31e-199">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="ac31e-199">See also</span></span>
[<span data-ttu-id="ac31e-200">Obtención de una instancia de procesador multimedia</span><span class="sxs-lookup"><span data-stu-id="ac31e-200">Get Media Processors</span></span>](media-services-rest-get-media-processor.md)
