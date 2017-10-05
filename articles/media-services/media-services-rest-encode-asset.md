---
title: "Codificación de un recurso de Azure mediante Media Encoder Standard | Microsoft Docs"
description: "Aprenda a usar Media Encoder Standard para codificar el contenido multimedia en Azure Media Services. Los ejemplos de código usan la API de REST."
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
ms.openlocfilehash: 796f3b5a4dd56a0160986600cbbcf38faf8add56
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-encode-an-asset-by-using-media-encoder-standard"></a><span data-ttu-id="c8997-104">Codificación de un recurso mediante Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="c8997-104">How to encode an asset by using Media Encoder Standard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c8997-105">.NET</span><span class="sxs-lookup"><span data-stu-id="c8997-105">.NET</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [<span data-ttu-id="c8997-106">REST</span><span class="sxs-lookup"><span data-stu-id="c8997-106">REST</span></span>](media-services-rest-encode-asset.md)
> * [<span data-ttu-id="c8997-107">Portal</span><span class="sxs-lookup"><span data-stu-id="c8997-107">Portal</span></span>](media-services-portal-encode.md)
>
>

## <a name="overview"></a><span data-ttu-id="c8997-108">Información general</span><span class="sxs-lookup"><span data-stu-id="c8997-108">Overview</span></span>
<span data-ttu-id="c8997-109">Para entregar vídeo digital a través de Internet, debe comprimir los archivos multimedia.</span><span class="sxs-lookup"><span data-stu-id="c8997-109">To deliver digital video over the Internet, you must compress the media.</span></span> <span data-ttu-id="c8997-110">Los archivos de vídeo digital son grandes y pueden ser demasiado pesados para entregarlos a través de Internet o para que los dispositivos de sus clientes los muestren correctamente.</span><span class="sxs-lookup"><span data-stu-id="c8997-110">Digital video files are large and may be too big to deliver over the Internet, or for your customers’ devices to display properly.</span></span> <span data-ttu-id="c8997-111">La codificación es el proceso de compresión de vídeo y audio para que los clientes puedan ver el contenido multimedia.</span><span class="sxs-lookup"><span data-stu-id="c8997-111">Encoding is the process of compressing video and audio so your customers can view your media.</span></span>

<span data-ttu-id="c8997-112">Los trabajos de codificación son una de las operaciones de procesamiento más habituales en Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="c8997-112">Encoding jobs are one of the most common processing operations in Azure Media Services.</span></span> <span data-ttu-id="c8997-113">Los trabajos de codificación se crean para convertir archivos multimedia de una codificación a otra.</span><span class="sxs-lookup"><span data-stu-id="c8997-113">You create encoding jobs to convert media files from one encoding to another.</span></span> <span data-ttu-id="c8997-114">Al codificar, puede usar el codificador integrado en Servicios multimedia (Codificador multimedia estándar).</span><span class="sxs-lookup"><span data-stu-id="c8997-114">When you encode, you can use the Media Services built-in encoder (Media Encoder Standard).</span></span> <span data-ttu-id="c8997-115">También puede usar un codificador proporcionado por un partner de Media Services.</span><span class="sxs-lookup"><span data-stu-id="c8997-115">You can also use an encoder provided by a Media Services partner.</span></span> <span data-ttu-id="c8997-116">Los codificadores de terceros están disponibles a través de Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="c8997-116">Third-party encoders are available through the Azure Marketplace.</span></span> <span data-ttu-id="c8997-117">Puede especificar los detalles de las tareas de codificación mediante cadenas preestablecidas definidas para el codificador o mediante archivos de configuración preestablecidos.</span><span class="sxs-lookup"><span data-stu-id="c8997-117">You can specify the details of encoding tasks by using preset strings defined for your encoder, or by using preset configuration files.</span></span> <span data-ttu-id="c8997-118">Para consultar los tipos de valores preestablecidos disponibles, vea [Valores preestablecidos de tareas para el Codificador multimedia estándar](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="c8997-118">To see the types of presets that are available, see [Task Presets for Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="c8997-119">Cada trabajo puede tener una o más tareas según el tipo de procesamiento que desee llevar a cabo.</span><span class="sxs-lookup"><span data-stu-id="c8997-119">Each job can have one or more tasks depending on the type of processing that you want to accomplish.</span></span> <span data-ttu-id="c8997-120">A través de la API de REST, puede crear trabajos y sus tareas relacionadas en una de las dos maneras siguientes:</span><span class="sxs-lookup"><span data-stu-id="c8997-120">Through the REST API, you can create jobs and their related tasks in one of two ways:</span></span>

* <span data-ttu-id="c8997-121">Las tareas se pueden definir en línea mediante la propiedad de navegación Tasks en entidades Job.</span><span class="sxs-lookup"><span data-stu-id="c8997-121">Tasks can be defined inline through the Tasks navigation property on Job entities.</span></span>
* <span data-ttu-id="c8997-122">Uso del procesamiento por lotes de OData.</span><span class="sxs-lookup"><span data-stu-id="c8997-122">Use OData batch processing.</span></span>

<span data-ttu-id="c8997-123">Se recomienda codificar siempre los archivos fuente en un conjunto MP4 de velocidad de bits adaptable y, a continuación, convertirlo al formato deseado con el [empaquetado dinámico](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c8997-123">We recommend that you always encode your source files into an adaptive bitrate MP4 set, and then convert the set to the desired format by using [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>

<span data-ttu-id="c8997-124">Si el recurso de salida tiene el almacenamiento cifrado, asegúrese de configurar la directiva de entrega de recursos.</span><span class="sxs-lookup"><span data-stu-id="c8997-124">If your output asset is storage encrypted, you must configure the asset delivery policy.</span></span> <span data-ttu-id="c8997-125">Para obtener más información, consulte [Configuración de directivas de entrega de recursos](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="c8997-125">For more information, see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="c8997-126">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="c8997-126">Considerations</span></span>

<span data-ttu-id="c8997-127">Al obtener acceso a las entidades de Servicios multimedia, debe establecer los campos de encabezado específicos y los valores en las solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8997-127">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="c8997-128">Para obtener más información, consulte [Configuración del desarrollo de la API de REST de Servicios multimedia](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="c8997-128">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

<span data-ttu-id="c8997-129">Antes de empezar a hacer referencia a procesadores de multimedia, compruebe que dispone del identificador de procesador de multimedia correcto.</span><span class="sxs-lookup"><span data-stu-id="c8997-129">Before you start referencing media processors, verify that you have the correct media processor ID.</span></span> <span data-ttu-id="c8997-130">Para obtener más información, consulte [Obtención de procesadores multimedia](media-services-rest-get-media-processor.md).</span><span class="sxs-lookup"><span data-stu-id="c8997-130">For more information, see [Get media processors](media-services-rest-get-media-processor.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="c8997-131">Conexión con Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="c8997-131">Connect to Media Services</span></span>

<span data-ttu-id="c8997-132">Para obtener más información sobre cómo conectarse a la API de Azure Media Services, consulte [Acceso a la API de Azure Media Services con la autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="c8997-132">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="c8997-133">Después de conectarse correctamente a https://media.windows.net, recibirá una redirección 301 que especifica otro URI de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="c8997-133">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="c8997-134">Debe realizar las llamadas posteriores al nuevo URI.</span><span class="sxs-lookup"><span data-stu-id="c8997-134">You must make subsequent calls to the new URI.</span></span>

## <a name="create-a-job-with-a-single-encoding-task"></a><span data-ttu-id="c8997-135">Creación de un trabajo con una sola tarea de codificación</span><span class="sxs-lookup"><span data-stu-id="c8997-135">Create a job with a single encoding task</span></span>
> [!NOTE]
> <span data-ttu-id="c8997-136">Al trabajar con la API de REST de Media Services, se aplican las consideraciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="c8997-136">When you're working with the Media Services REST API, the following considerations apply:</span></span>
>
> <span data-ttu-id="c8997-137">Al obtener acceso a las entidades de Servicios multimedia, debe establecer los campos de encabezado específicos y los valores en las solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8997-137">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="c8997-138">Para obtener más información, consulte [Configuración del desarrollo de la API de REST de Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="c8997-138">For more information, see [Setup for Media Services REST API development](media-services-rest-how-to-use.md).</span></span>
>
> <span data-ttu-id="c8997-139">Después de conectarse correctamente a https://media.windows.net, recibirá una redirección 301 que especifica otro URI de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="c8997-139">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="c8997-140">Debe realizar las llamadas posteriores al nuevo URI.</span><span class="sxs-lookup"><span data-stu-id="c8997-140">You must make subsequent calls to the new URI.</span></span> <span data-ttu-id="c8997-141">Para más información sobre cómo conectarse a la API de Azure Media Services, vea [Acceso a Azure Media Services API con la autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="c8997-141">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
>
> <span data-ttu-id="c8997-142">Cuando se utiliza JSON y se especifica el uso de la palabra clave **__metadata** en la solicitud (por ejemplo, para referencias a un objeto vinculado), debe establecer el encabezado **Accept** en [formato JSON detallado](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accept: application/json;odata=verbose.</span><span class="sxs-lookup"><span data-stu-id="c8997-142">When using JSON and specifying to use the **__metadata** keyword in the request (for example, to references a linked object), you must set the **Accept** header to [JSON Verbose format](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accept: application/json;odata=verbose.</span></span>
>
>

<span data-ttu-id="c8997-143">En el ejemplo siguiente se muestra cómo crear y publicar un trabajo con un conjunto de tareas para codificar un vídeo con una resolución y calidad específicas.</span><span class="sxs-lookup"><span data-stu-id="c8997-143">The following example shows you how to create and post a job with one task set to encode a video at a specific resolution and quality.</span></span> <span data-ttu-id="c8997-144">Al codificar con Media Encoder Standard, puede usar los valores preestablecidos de configuración de tareas especificados [aquí](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="c8997-144">When you encode with Media Encoder Standard, you can use task configuration presets specified [here](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="c8997-145">Solicitud:</span><span class="sxs-lookup"><span data-stu-id="c8997-145">Request:</span></span>

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

<span data-ttu-id="c8997-146">Respuesta:</span><span class="sxs-lookup"><span data-stu-id="c8997-146">Response:</span></span>

    HTTP/1.1 201 Created

    . . .

### <a name="set-the-output-assets-name"></a><span data-ttu-id="c8997-147">Establecimiento del nombre del recurso de salida</span><span class="sxs-lookup"><span data-stu-id="c8997-147">Set the output asset's name</span></span>
<span data-ttu-id="c8997-148">En el ejemplo siguiente se muestra cómo establecer el atributo assetName:</span><span class="sxs-lookup"><span data-stu-id="c8997-148">The following example shows how to set the assetName attribute:</span></span>

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a><span data-ttu-id="c8997-149">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="c8997-149">Considerations</span></span>
* <span data-ttu-id="c8997-150">Las propiedades TaskBody deben usar archivos XML literales para definir el número de recursos de entrada o salida que se usarán en la tarea.</span><span class="sxs-lookup"><span data-stu-id="c8997-150">TaskBody properties must use literal XML to define the number of input, or output assets that are used by the task.</span></span> <span data-ttu-id="c8997-151">El tema Tarea incluye la definición de esquema XML para el archivo XML.</span><span class="sxs-lookup"><span data-stu-id="c8997-151">The task topic contains the XML Schema Definition for the XML.</span></span>
* <span data-ttu-id="c8997-152">En la definición de TaskBody, cada valor interno para <inputAsset> y <outputAsset> se debe establecer como JobInputAsset(value) o JobOutputAsset(value).</span><span class="sxs-lookup"><span data-stu-id="c8997-152">In the TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="c8997-153">Una tarea puede tener varios recursos de salida.</span><span class="sxs-lookup"><span data-stu-id="c8997-153">A task can have multiple output assets.</span></span> <span data-ttu-id="c8997-154">Un elemento JobOutputAsset(x) solo se puede usar una vez como salida de una tarea en un trabajo.</span><span class="sxs-lookup"><span data-stu-id="c8997-154">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="c8997-155">Puede especificar JobInputAsset o JobOutputAsset como un recurso de entrada de una tarea.</span><span class="sxs-lookup"><span data-stu-id="c8997-155">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="c8997-156">Las tareas no pueden formar un ciclo.</span><span class="sxs-lookup"><span data-stu-id="c8997-156">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="c8997-157">El parámetro de valor que se pasa a JobInputAsset o JobOutputAsset representa el valor de índice para un recurso.</span><span class="sxs-lookup"><span data-stu-id="c8997-157">The value parameter that you pass to JobInputAsset or JobOutputAsset represents the index value for an asset.</span></span> <span data-ttu-id="c8997-158">Los recursos reales se definen en las propiedades de navegación InputMediaAssets y OutputMediaAssets en la definición de la entidad Job.</span><span class="sxs-lookup"><span data-stu-id="c8997-158">The actual assets are defined in the InputMediaAssets and OutputMediaAssets navigation properties on the job entity definition.</span></span>
* <span data-ttu-id="c8997-159">Dado que Media Services se basa en OData v3, se hace referencia a los recursos individuales de las colecciones de propiedades de navegación InputMediaAssets y OutputMediaAssets a través de un par nombre-valor "__metadata : uri".</span><span class="sxs-lookup"><span data-stu-id="c8997-159">Because Media Services is built on OData v3, the individual assets in the InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
* <span data-ttu-id="c8997-160">InputMediaAssets se asigna a uno o más recursos que ha creado en Media Services.</span><span class="sxs-lookup"><span data-stu-id="c8997-160">InputMediaAssets maps to one or more assets that you created in Media Services.</span></span> <span data-ttu-id="c8997-161">El sistema crea OutputMediaAssets.</span><span class="sxs-lookup"><span data-stu-id="c8997-161">OutputMediaAssets are created by the system.</span></span> <span data-ttu-id="c8997-162">Estos no hacen referencia a ningún recurso existente.</span><span class="sxs-lookup"><span data-stu-id="c8997-162">They don't reference an existing asset.</span></span>
* <span data-ttu-id="c8997-163">Se puede asignar un nombre a OutputMediaAssets con el atributo assetName.</span><span class="sxs-lookup"><span data-stu-id="c8997-163">OutputMediaAssets can be named by using the assetName attribute.</span></span> <span data-ttu-id="c8997-164">Si este atributo no está presente, el nombre de OutputMediaAsset será el valor del texto interno del elemento <outputAsset> con un sufijo del valor Job Name o del valor Job Id (en el caso de que no se haya definido la propiedad Name).</span><span class="sxs-lookup"><span data-stu-id="c8997-164">If this attribute is not present, then the name of the OutputMediaAsset is whatever the inner text value of the <outputAsset> element is with a suffix of either the Job Name value, or the Job Id value (in the case where the Name property isn't defined).</span></span> <span data-ttu-id="c8997-165">Por ejemplo, si establece un valor para assetName como "Sample", se establece la propiedad de OutputMediaAsset Name en "Sample".</span><span class="sxs-lookup"><span data-stu-id="c8997-165">For example, if you set a value for assetName to "Sample," then the OutputMediaAsset Name property is set to "Sample."</span></span> <span data-ttu-id="c8997-166">Sin embargo, si no se ha definido un valor para assetName, pero se ha especificado el nombre del trabajo como "NewJob", OutputMediaAsset Name será "JobOutputAsset(value)_NewJob".</span><span class="sxs-lookup"><span data-stu-id="c8997-166">However, if you didn't set a value for assetName, but did set the job name to "NewJob," then the OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob."</span></span>

## <a name="create-a-job-with-chained-tasks"></a><span data-ttu-id="c8997-167">Creación de un trabajo con tareas encadenadas</span><span class="sxs-lookup"><span data-stu-id="c8997-167">Create a job with chained tasks</span></span>
<span data-ttu-id="c8997-168">En muchos escenarios de aplicaciones, los desarrolladores desean crear una serie de tareas de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="c8997-168">In many application scenarios, developers want to create a series of processing tasks.</span></span> <span data-ttu-id="c8997-169">En Servicios multimedia, puede crear una serie de tareas encadenadas.</span><span class="sxs-lookup"><span data-stu-id="c8997-169">In Media Services, you can create a series of chained tasks.</span></span> <span data-ttu-id="c8997-170">Cada tarea realiza distintos pasos de procesamiento diferentes y puede usar diferentes procesadores multimedia.</span><span class="sxs-lookup"><span data-stu-id="c8997-170">Each task performs different processing steps and can use different media processors.</span></span> <span data-ttu-id="c8997-171">Las tareas encadenadas pueden entregar un recurso de una tarea a otra, realizando una secuencia lineal de tareas en el recurso.</span><span class="sxs-lookup"><span data-stu-id="c8997-171">The chained tasks can hand off an asset from one task to another, performing a linear sequence of tasks on the asset.</span></span> <span data-ttu-id="c8997-172">Sin embargo, no es necesario que las tareas realizadas en un trabajo estén en una secuencia.</span><span class="sxs-lookup"><span data-stu-id="c8997-172">However, the tasks performed in a job are not required to be in a sequence.</span></span> <span data-ttu-id="c8997-173">Al crear una tarea encadenada, los objetos **ITask** encadenados se crean en un solo objeto **IJob**.</span><span class="sxs-lookup"><span data-stu-id="c8997-173">When you create a chained task, the chained **ITask** objects are created in a single **IJob** object.</span></span>

> [!NOTE]
> <span data-ttu-id="c8997-174">Actualmente hay un límite de 30 tareas por trabajo.</span><span class="sxs-lookup"><span data-stu-id="c8997-174">There is currently a limit of 30 tasks per job.</span></span> <span data-ttu-id="c8997-175">Si necesita encadenar más de 30 tareas, cree más de un trabajo para incluir las tareas.</span><span class="sxs-lookup"><span data-stu-id="c8997-175">If you need to chain more than 30 tasks, create more than one job to contain the tasks.</span></span>
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


### <a name="considerations"></a><span data-ttu-id="c8997-176">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="c8997-176">Considerations</span></span>
<span data-ttu-id="c8997-177">Para habilitar el encadenamiento de tareas:</span><span class="sxs-lookup"><span data-stu-id="c8997-177">To enable task chaining:</span></span>

* <span data-ttu-id="c8997-178">Un trabajo debe tener al menos dos tareas.</span><span class="sxs-lookup"><span data-stu-id="c8997-178">A job must have at least two tasks.</span></span>
* <span data-ttu-id="c8997-179">Debe haber al menos una tarea cuya entrada sea la salida de otra tarea del trabajo.</span><span class="sxs-lookup"><span data-stu-id="c8997-179">There must be at least one task whose input is the output of another task in the job.</span></span>

## <a name="use-odata-batch-processing"></a><span data-ttu-id="c8997-180">Uso del procesamiento por lotes de OData</span><span class="sxs-lookup"><span data-stu-id="c8997-180">Use OData batch processing</span></span>
<span data-ttu-id="c8997-181">En el ejemplo siguiente se muestra cómo usar el procesamiento por lotes de OData para crear un trabajo y tareas.</span><span class="sxs-lookup"><span data-stu-id="c8997-181">The following example shows how to use OData batch processing to create a job and tasks.</span></span> <span data-ttu-id="c8997-182">Para obtener información sobre el procesamiento por lotes, consulte [Procesamiento por lotes del protocolo Open Data (OData)](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="c8997-182">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

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



## <a name="create-a-job-by-using-a-jobtemplate"></a><span data-ttu-id="c8997-183">Creación de un trabajo mediante una plantilla JobTemplate</span><span class="sxs-lookup"><span data-stu-id="c8997-183">Create a job by using a JobTemplate</span></span>
<span data-ttu-id="c8997-184">Al procesar varios recursos usando un conjunto común de tareas, utilice una plantilla JobTemplate para especificar los valores preestablecidos de las tareas predeterminadas o establezca el orden de las tareas.</span><span class="sxs-lookup"><span data-stu-id="c8997-184">When you process multiple assets by using a common set of tasks, use a JobTemplate to specify the default task presets, or to set the order of tasks.</span></span>

<span data-ttu-id="c8997-185">En el ejemplo siguiente se muestra cómo crear una plantilla JobTemplate con una plantilla TaskTemplate definida en línea.</span><span class="sxs-lookup"><span data-stu-id="c8997-185">The following example shows how to create a JobTemplate with a TaskTemplate that is defined inline.</span></span> <span data-ttu-id="c8997-186">La plantilla TaskTemplate usa Media Encoder Standard como elemento MediaProcessor para codificar el archivo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c8997-186">The TaskTemplate uses the Media Encoder Standard as the MediaProcessor to encode the asset file.</span></span> <span data-ttu-id="c8997-187">Sin embargo, también se pueden usar otros elementos MediaProcessor.</span><span class="sxs-lookup"><span data-stu-id="c8997-187">However, other MediaProcessors can be used as well.</span></span>

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
> <span data-ttu-id="c8997-188">A diferencia de otras entidades de Servicios multimedia, debe definir un nuevo identificador GUID para cada plantilla de tarea y colocarlo en el identificador de la plantilla de tarea y en la propiedad Id en el cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="c8997-188">Unlike other Media Services entities, you must define a new GUID identifier for each TaskTemplate and place it in the taskTemplateId and Id property in your request body.</span></span> <span data-ttu-id="c8997-189">El esquema de identificación de contenido debe seguir el esquema descrito en Identificación de entidades de Servicios multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="c8997-189">The content identification scheme must follow the scheme described in Identify Azure Media Services Entities.</span></span> <span data-ttu-id="c8997-190">Además, las plantillas de trabajo no se pueden actualizar.</span><span class="sxs-lookup"><span data-stu-id="c8997-190">Also, JobTemplates cannot be updated.</span></span> <span data-ttu-id="c8997-191">Por el contrario, debe crear una nueva con los cambios actualizados.</span><span class="sxs-lookup"><span data-stu-id="c8997-191">Instead, you must create a new one with your updated changes.</span></span>
>
>

<span data-ttu-id="c8997-192">Si se realiza correctamente, se devuelve la respuesta siguiente:</span><span class="sxs-lookup"><span data-stu-id="c8997-192">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .


<span data-ttu-id="c8997-193">En el ejemplo siguiente se muestra cómo crear un trabajo que hace referencia a un identificador de plantilla JobTemplate:</span><span class="sxs-lookup"><span data-stu-id="c8997-193">The following example shows how to create a job that references a JobTemplate Id:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


<span data-ttu-id="c8997-194">Si se realiza correctamente, se devuelve la respuesta siguiente:</span><span class="sxs-lookup"><span data-stu-id="c8997-194">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .



## <a name="media-services-learning-paths"></a><span data-ttu-id="c8997-195">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="c8997-195">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c8997-196">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="c8997-196">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="c8997-197">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c8997-197">Next steps</span></span>
<span data-ttu-id="c8997-198">Ahora que sabe cómo crear un trabajo para codificar un recurso, consulte [Comprobación del progreso del trabajo con Media Services](media-services-rest-check-job-progress.md).</span><span class="sxs-lookup"><span data-stu-id="c8997-198">Now that you know how to create a job to encode an asset, see [How to check job progress with Media Services](media-services-rest-check-job-progress.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="c8997-199">Consulte también</span><span class="sxs-lookup"><span data-stu-id="c8997-199">See also</span></span>
[<span data-ttu-id="c8997-200">Obtención de una instancia de procesador multimedia</span><span class="sxs-lookup"><span data-stu-id="c8997-200">Get Media Processors</span></span>](media-services-rest-get-media-processor.md)
