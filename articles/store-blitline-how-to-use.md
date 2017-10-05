---
title: "Cómo usar Blitline para el procesamiento de imágenes - Guía de funciones de Azure"
description: "Obtenga información acerca de cómo usar el servicio de Blitline para procesar imágenes dentro de una aplicación de Azure."
services: 
documentationcenter: .net
author: blitline-dev
manager: jason@blitline.com
editor: jason@blitline.com
ms.assetid: 6c711248-0e52-4895-ba9e-8395628de924
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2014
ms.author: support@blitline.com
ms.openlocfilehash: 1d90599e028b3407a513b04b878e3aefc39928a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-blitline-with-azure-and-azure-storage"></a><span data-ttu-id="49005-103">Cómo usar Blitline con Azure y Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="49005-103">How to use Blitline with Azure and Azure Storage</span></span>
<span data-ttu-id="49005-104">Esta guía explica cómo obtener acceso a los servicios Blitline y cómo enviar trabajos a Blitline.</span><span class="sxs-lookup"><span data-stu-id="49005-104">This guide will explain how to access Blitline services and how to submit jobs to Blitline.</span></span>

## <a name="what-is-blitline"></a><span data-ttu-id="49005-105">¿Qué es Blitline?</span><span class="sxs-lookup"><span data-stu-id="49005-105">What is Blitline?</span></span>
<span data-ttu-id="49005-106">Blitline es un servicio de procesamiento de imágenes basado en la nube que ofrece un procesamiento de imágenes de nivel empresarial por una fracción del precio que le costaría realizar la generación por su cuenta.</span><span class="sxs-lookup"><span data-stu-id="49005-106">Blitline is a cloud-based image processing service that provides enterprise level image processing at a fraction of the price that it would cost to build it yourself.</span></span>

<span data-ttu-id="49005-107">En realidad, el procesamiento de imágenes se realiza una y otra vez. Normalmente se vuelve a generar desde el principio en cada sitio web.</span><span class="sxs-lookup"><span data-stu-id="49005-107">The fact is that image processing has been done over and over again, usually rebuilt from the ground up for each and every website.</span></span> <span data-ttu-id="49005-108">Sabemos esto porque las hemos generado un millón de veces.</span><span class="sxs-lookup"><span data-stu-id="49005-108">We realize this because we’ve built them a million times too.</span></span> <span data-ttu-id="49005-109">Un día decidimos que quizás era el momento de realizar el proceso para todos.</span><span class="sxs-lookup"><span data-stu-id="49005-109">One day we decided that perhaps it‘s time we just do it for everyone.</span></span> <span data-ttu-id="49005-110">Sabemos cómo hacerlo, de forma rápida y eficaz, y guardar el trabajo de todos a la vez.</span><span class="sxs-lookup"><span data-stu-id="49005-110">We know how to do it, to do it fast and efficiently, and save everyone work in the meantime.</span></span>

<span data-ttu-id="49005-111">Para obtener más información, consulte [http://www.blitline.com](http://www.blitline.com).</span><span class="sxs-lookup"><span data-stu-id="49005-111">For more information, see [http://www.blitline.com](http://www.blitline.com).</span></span>

## <a name="what-blitline-is-not"></a><span data-ttu-id="49005-112">¿Qué NO es Blitline?</span><span class="sxs-lookup"><span data-stu-id="49005-112">What Blitline is NOT...</span></span>
<span data-ttu-id="49005-113">Para aclarar para qué sirve Blitline, normalmente es más sencillo identificar qué NO hace Blitline antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="49005-113">To clarify what Blitline is useful for, it is often easier to identify what Blitline does NOT do before moving forward.</span></span>

* <span data-ttu-id="49005-114">Blitline NO dispone de widgets HTML para cargar imágenes.</span><span class="sxs-lookup"><span data-stu-id="49005-114">Blitline does NOT have HTML widgets to upload images.</span></span> <span data-ttu-id="49005-115">Debe tener imágenes disponibles públicamente o con permisos restringidos disponibles para que los consiga Blitline.</span><span class="sxs-lookup"><span data-stu-id="49005-115">You must have images available publicly or with restricted permissions available for Blitline to reach.</span></span>
* <span data-ttu-id="49005-116">Blitline NO activa el procesamiento de imágenes, como Aviary.com.</span><span class="sxs-lookup"><span data-stu-id="49005-116">Blitline does NOT do live image processing, like Aviary.com</span></span>
* <span data-ttu-id="49005-117">Blitline NO acepta cargas de imágenes y no puede insertar imágenes en Blitline directamente.</span><span class="sxs-lookup"><span data-stu-id="49005-117">Blitline does NOT accept image uploads, you cannot push your images to Blitline directly.</span></span> <span data-ttu-id="49005-118">Debe insertarlas en Almacenamiento de Azure o en otros lugares compatibles con Blitline y luego indicar a Blitline el lugar donde conseguirlas.</span><span class="sxs-lookup"><span data-stu-id="49005-118">You must push them to Azure Storage or other places Blitline supports and then tell Blitline where to go get them.</span></span>
* <span data-ttu-id="49005-119">Blitline funciona de una forma totalmente paralela y NO realiza ningún procesamiento sincrónico.</span><span class="sxs-lookup"><span data-stu-id="49005-119">Blitline is massively parallel and does NOT do any synchronous processing.</span></span> <span data-ttu-id="49005-120">Esto significa que debe proporcionarnos una dirección URL postback_url para que podamos indicarle cuándo acabamos el procedimiento.</span><span class="sxs-lookup"><span data-stu-id="49005-120">Meaning you must give us a postback_url and we can tell you when we are done processing.</span></span>

## <a name="create-a-blitline-account"></a><span data-ttu-id="49005-121">Creación de una cuenta Blitline</span><span class="sxs-lookup"><span data-stu-id="49005-121">Create a Blitline account</span></span>
[!INCLUDE [blitline-signup](../includes/blitline-signup.md)]

## <a name="how-to-create-a-blitline-job"></a><span data-ttu-id="49005-122">Creación de un trabajo Blitline</span><span class="sxs-lookup"><span data-stu-id="49005-122">How to create a Blitline job</span></span>
<span data-ttu-id="49005-123">Blitline usa JSON para definir las acciones que desea realizar en una imagen.</span><span class="sxs-lookup"><span data-stu-id="49005-123">Blitline uses JSON to define the actions you want to take on an image.</span></span> <span data-ttu-id="49005-124">JSON está compuesto por algunos campos simples.</span><span class="sxs-lookup"><span data-stu-id="49005-124">This JSON is composed of a few simple fields.</span></span>

<span data-ttu-id="49005-125">El ejemplo más simple es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="49005-125">The simplest example is as follows:</span></span>

        json : '{
       "application_id": "MY_APP_ID",
       "src" : "http://cdn.blitline.com/filters/boys.jpeg",
       "functions" : [ {
           "name": "resize_to_fit",
           "params" : { "width": 240, "height": 140 },
           "save" : { "image_identifier" : "external_sample_1" }
       } ]
    }'

<span data-ttu-id="49005-126">Aquí tenemos el elemento JSON que tomará una imagen "src" "...boys.jpeg" y, a continuación, cambiará el tamaño de la imagen a 240x140.</span><span class="sxs-lookup"><span data-stu-id="49005-126">Here we have JSON that will take a "src" image "...boys.jpeg" and then resize that image to 240x140.</span></span>

<span data-ttu-id="49005-127">Puede encontrar el identificador de la aplicación en la pestaña **INFORMACIÓN DE CONEXIÓN** o **ADMINISTRAR** de Azure.</span><span class="sxs-lookup"><span data-stu-id="49005-127">The Application ID is something you can find in your **CONNECTION INFO** or **MANAGE** tab on Azure.</span></span> <span data-ttu-id="49005-128">Se trata del identificador secreto que le permite ejecutar trabajos en Blitline.</span><span class="sxs-lookup"><span data-stu-id="49005-128">It is your secret identifier that allows you to run jobs on Blitline.</span></span>

<span data-ttu-id="49005-129">El parámetro "save" identifica información sobre dónde desea colocar la imagen una vez que se haya procesado.</span><span class="sxs-lookup"><span data-stu-id="49005-129">The "save" parameter identifies information about where you want to put the image once we have processed it.</span></span> <span data-ttu-id="49005-130">En este caso específico, no definimos ninguno.</span><span class="sxs-lookup"><span data-stu-id="49005-130">In this trivial case, we haven't defined one.</span></span> <span data-ttu-id="49005-131">Si no se define ninguna ubicación, Blitline la almacenará localmente (o temporalmente) en una ubicación exclusiva de la nube.</span><span class="sxs-lookup"><span data-stu-id="49005-131">If no location is defined Blitline will store it locally (and temporarily) at a unique cloud location.</span></span> <span data-ttu-id="49005-132">Podrá obtener esa ubicación desde el JSON devuelto por Blitline cuando realice el trabajo Blitline.</span><span class="sxs-lookup"><span data-stu-id="49005-132">You will be able to get that location from the JSON returned by Blitline when you make the Blitline.</span></span> <span data-ttu-id="49005-133">El identificador "image" es obligatorio y se devuelve cuando se identifica esta imagen guardada en concreto.</span><span class="sxs-lookup"><span data-stu-id="49005-133">The "image" identifier is required and is returned to you when to identify this particular saved image.</span></span>

<span data-ttu-id="49005-134">Puede obtener más información sobre las *funciones* que ofrecemos aquí: <http://www.blitline.com/docs/functions>.</span><span class="sxs-lookup"><span data-stu-id="49005-134">You can find more information about the *functions* we support here: <http://www.blitline.com/docs/functions></span></span>

<span data-ttu-id="49005-135">También puede encontrar información sobre las opciones de trabajo aquí: <http://www.blitline.com/docs/api>.</span><span class="sxs-lookup"><span data-stu-id="49005-135">You can also find documentation about the job options here: <http://www.blitline.com/docs/api></span></span>

<span data-ttu-id="49005-136">Una vez que disponga de JSON, lo único que tiene que hacer es **PUBLICARLO** en `http://api.blitline.com/job`.</span><span class="sxs-lookup"><span data-stu-id="49005-136">Once you have your JSON all you need to do is **POST** it to `http://api.blitline.com/job`</span></span>

<span data-ttu-id="49005-137">Obtendrá un resultado JSON con una apariencia similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="49005-137">You will get JSON back that looks something like this:</span></span>

    {
     "results":
         {"images":
            [{
              "image_identifier":"external_sample_1",
              "s3_url":"https://s3.amazonaws.com/dev.blitline/2011110722/YOUR_APP_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg"
            }],
          "job_id":"4eb8c9f72a50ee2a9900002f"
         }
    }


<span data-ttu-id="49005-138">Esto indica que Blitline ha recibido la solicitud, la ha puesto en la cola de procesamiento y, cuando se haya completado, la imagen estará disponible en: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_APP\_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg**</span><span class="sxs-lookup"><span data-stu-id="49005-138">This tells you that Blitline has recieved your request, it has put it in a processing queue, and when it has completed the image will be available at: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_APP\_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg**</span></span>

## <a name="how-to-save-an-image-to-your-azure-storage-account"></a><span data-ttu-id="49005-139">Almacenamiento de una imagen en la cuenta de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="49005-139">How to save an image to your Azure Storage account</span></span>
<span data-ttu-id="49005-140">Si dispone de una cuenta de Almacenamiento de Azure, puede hacer que Blitline inserte las imágenes procesadas en el contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="49005-140">If you have an Azure Storage account, you can easily have Blitline push the processed images into your Azure container.</span></span> <span data-ttu-id="49005-141">Si agrega "azure_destination", defina la ubicación y los permisos de inserción de Blitline.</span><span class="sxs-lookup"><span data-stu-id="49005-141">By adding an "azure_destination" you define the location and permissions for Blitline to push to.</span></span>

<span data-ttu-id="49005-142">Aquí tiene un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="49005-142">Here is an example:</span></span>

    job : '{
      "application_id": "YOUR_APP_ID",
      "src" : "http://www.google.com/logos/2011/houdini11-hp.jpg",
         "functions" : [{
         "name": "blur",
         "save" : {
             "image_identifier" : "YOUR_IMAGE_IDENTIFIER",
             "azure_destination" : {
                 "account_name" : "YOUR_AZURE_CONTAINER_NAME",
                 "shared_access_signature" : "SAS_THAT_GIVES_BLITLINE_PERMISSION_TO_WRITE_THIS_OBJECT_TO_CONTAINER",
               }
           }
         }]
       }'


<span data-ttu-id="49005-143">Si completa los valores en MAYÚSCULAS por su cuenta, puede enviar JSON a http://api.blitline.com/job y la imagen "src" se procesará con un filtro de desenfoque y, a continuación, se insertará en un destino de Azure.</span><span class="sxs-lookup"><span data-stu-id="49005-143">By filling in the CAPITALIZED values with your own, you can submit this JSON to http://api.blitline.com/job and the "src" image will be processed with a blur filter and then pushed to you Azure destination.</span></span>

### <a name="please-note"></a><span data-ttu-id="49005-144">Tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="49005-144">Please note:</span></span>
<span data-ttu-id="49005-145">SAS debe contener la dirección URL completa de SAS, incluido el nombre de archivo del archivo de destino.</span><span class="sxs-lookup"><span data-stu-id="49005-145">The SAS must contain the entire SAS url, including the filename of the destination file.</span></span>

<span data-ttu-id="49005-146">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="49005-146">Example:</span></span>

    http://blitline.blob.core.windows.net/sample/image.jpg?sr=b&sv=2012-02-12&st=2013-04-12T03%3A18%3A30Z&se=2013-04-12T04%3A18%3A30Z&sp=w&sig=Bte2hkkbwTT2sqlkkKLop2asByrE0sIfeesOwj7jNA5o%3D


<span data-ttu-id="49005-147">También puede consultar la última edición de los documentos de Almacenamiento de Azure de Blitline [aquí](http://www.blitline.com/docs/azure_storage).</span><span class="sxs-lookup"><span data-stu-id="49005-147">You can also read the latest edition of Blitline's Azure Storage docs [here](http://www.blitline.com/docs/azure_storage).</span></span>

## <a name="next-steps"></a><span data-ttu-id="49005-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="49005-148">Next Steps</span></span>
<span data-ttu-id="49005-149">Visite blitline.com para conocer toda la información sobre otras características:</span><span class="sxs-lookup"><span data-stu-id="49005-149">Visit blitline.com to read about all our other features:</span></span>

* <span data-ttu-id="49005-150">Documentos del punto de conexión de la API de Blitline <http://www.blitline.com/docs/api></span><span class="sxs-lookup"><span data-stu-id="49005-150">Blitline API Endpoint Docs <http://www.blitline.com/docs/api></span></span>
* <span data-ttu-id="49005-151">Funciones de la API de Blitline <http://www.blitline.com/docs/functions></span><span class="sxs-lookup"><span data-stu-id="49005-151">Blitline API Functions <http://www.blitline.com/docs/functions></span></span>
* <span data-ttu-id="49005-152">Ejemplos de la API de Blitline <http://www.blitline.com/docs/examples></span><span class="sxs-lookup"><span data-stu-id="49005-152">Blitline API Examples <http://www.blitline.com/docs/examples></span></span>
* <span data-ttu-id="49005-153">Biblioteca Nuget de terceros <http://nuget.org/packages/Blitline.Net></span><span class="sxs-lookup"><span data-stu-id="49005-153">Third Part Nuget Library <http://nuget.org/packages/Blitline.Net></span></span>

