---
title: "aaaHow toouse Blitline para el procesamiento de imagen - Guía de características de Azure"
description: "Obtenga información acerca de cómo toouse hello Blitline service tooprocess imágenes dentro de una aplicación de Azure."
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
ms.openlocfilehash: 328fd177e25f45f29f8ad8e142d02b46017a858e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blitline-with-azure-and-azure-storage"></a><span data-ttu-id="82b88-103">Cómo toouse Blitline con almacenamiento de Azure y Azure</span><span class="sxs-lookup"><span data-stu-id="82b88-103">How toouse Blitline with Azure and Azure Storage</span></span>
<span data-ttu-id="82b88-104">Esta guía se explica cómo tooaccess Blitline servicios y cómo toosubmit trabajos tooBlitline.</span><span class="sxs-lookup"><span data-stu-id="82b88-104">This guide will explain how tooaccess Blitline services and how toosubmit jobs tooBlitline.</span></span>

## <a name="what-is-blitline"></a><span data-ttu-id="82b88-105">¿Qué es Blitline?</span><span class="sxs-lookup"><span data-stu-id="82b88-105">What is Blitline?</span></span>
<span data-ttu-id="82b88-106">Blitline es un servicio que proporciona el procesamiento de imagen de nivel empresarial en una fracción del precio de Hola que costaría toobuild de procesamiento de imágenes basado en la nube usted mismo.</span><span class="sxs-lookup"><span data-stu-id="82b88-106">Blitline is a cloud-based image processing service that provides enterprise level image processing at a fraction of hello price that it would cost toobuild it yourself.</span></span>

<span data-ttu-id="82b88-107">hecho de Hello es que el procesamiento de imágenes se ha realizado una y otra vez, normalmente se vuelven a generar desde principio Hola hacia arriba para cada sitio Web.</span><span class="sxs-lookup"><span data-stu-id="82b88-107">hello fact is that image processing has been done over and over again, usually rebuilt from hello ground up for each and every website.</span></span> <span data-ttu-id="82b88-108">Sabemos esto porque las hemos generado un millón de veces.</span><span class="sxs-lookup"><span data-stu-id="82b88-108">We realize this because we’ve built them a million times too.</span></span> <span data-ttu-id="82b88-109">Un día decidimos que quizás era el momento de realizar el proceso para todos.</span><span class="sxs-lookup"><span data-stu-id="82b88-109">One day we decided that perhaps it‘s time we just do it for everyone.</span></span> <span data-ttu-id="82b88-110">Sabemos cómo toodo lo, toodo rápida y eficazmente y guardar todos los usuarios funciona en hello mientras tanto.</span><span class="sxs-lookup"><span data-stu-id="82b88-110">We know how toodo it, toodo it fast and efficiently, and save everyone work in hello meantime.</span></span>

<span data-ttu-id="82b88-111">Para obtener más información, consulte [http://www.blitline.com](http://www.blitline.com).</span><span class="sxs-lookup"><span data-stu-id="82b88-111">For more information, see [http://www.blitline.com](http://www.blitline.com).</span></span>

## <a name="what-blitline-is-not"></a><span data-ttu-id="82b88-112">¿Qué NO es Blitline?</span><span class="sxs-lookup"><span data-stu-id="82b88-112">What Blitline is NOT...</span></span>
<span data-ttu-id="82b88-113">tooclarify qué Blitline es útil para, es a menudo más fácil tooidentify qué Blitline no antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="82b88-113">tooclarify what Blitline is useful for, it is often easier tooidentify what Blitline does NOT do before moving forward.</span></span>

* <span data-ttu-id="82b88-114">Blitline no tiene imágenes de tooupload de widgets HTML.</span><span class="sxs-lookup"><span data-stu-id="82b88-114">Blitline does NOT have HTML widgets tooupload images.</span></span> <span data-ttu-id="82b88-115">Debe tener imágenes disponibles públicamente o con permisos restringidos disponibles para Blitline tooreach.</span><span class="sxs-lookup"><span data-stu-id="82b88-115">You must have images available publicly or with restricted permissions available for Blitline tooreach.</span></span>
* <span data-ttu-id="82b88-116">Blitline NO activa el procesamiento de imágenes, como Aviary.com.</span><span class="sxs-lookup"><span data-stu-id="82b88-116">Blitline does NOT do live image processing, like Aviary.com</span></span>
* <span data-ttu-id="82b88-117">Blitline no acepta la carga de imágenes, no se pueden insertar su tooBlitline imágenes directamente.</span><span class="sxs-lookup"><span data-stu-id="82b88-117">Blitline does NOT accept image uploads, you cannot push your images tooBlitline directly.</span></span> <span data-ttu-id="82b88-118">Debe insertarlas tooAzure almacenamiento o en otros lugares que blitline admite y, a continuación, indicar Blitline donde toogo obtenerlas.</span><span class="sxs-lookup"><span data-stu-id="82b88-118">You must push them tooAzure Storage or other places Blitline supports and then tell Blitline where toogo get them.</span></span>
* <span data-ttu-id="82b88-119">Blitline funciona de una forma totalmente paralela y NO realiza ningún procesamiento sincrónico.</span><span class="sxs-lookup"><span data-stu-id="82b88-119">Blitline is massively parallel and does NOT do any synchronous processing.</span></span> <span data-ttu-id="82b88-120">Esto significa que debe proporcionarnos una dirección URL postback_url para que podamos indicarle cuándo acabamos el procedimiento.</span><span class="sxs-lookup"><span data-stu-id="82b88-120">Meaning you must give us a postback_url and we can tell you when we are done processing.</span></span>

## <a name="create-a-blitline-account"></a><span data-ttu-id="82b88-121">Creación de una cuenta Blitline</span><span class="sxs-lookup"><span data-stu-id="82b88-121">Create a Blitline account</span></span>
[!INCLUDE [blitline-signup](../includes/blitline-signup.md)]

## <a name="how-toocreate-a-blitline-job"></a><span data-ttu-id="82b88-122">¿Cómo toocreate un trabajo Blitline</span><span class="sxs-lookup"><span data-stu-id="82b88-122">How toocreate a Blitline job</span></span>
<span data-ttu-id="82b88-123">Blitline utiliza acciones de hello toodefine JSON que desee tootake en una imagen.</span><span class="sxs-lookup"><span data-stu-id="82b88-123">Blitline uses JSON toodefine hello actions you want tootake on an image.</span></span> <span data-ttu-id="82b88-124">JSON está compuesto por algunos campos simples.</span><span class="sxs-lookup"><span data-stu-id="82b88-124">This JSON is composed of a few simple fields.</span></span>

<span data-ttu-id="82b88-125">ejemplo de Hola más simple es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="82b88-125">hello simplest example is as follows:</span></span>

        json : '{
       "application_id": "MY_APP_ID",
       "src" : "http://cdn.blitline.com/filters/boys.jpeg",
       "functions" : [ {
           "name": "resize_to_fit",
           "params" : { "width": 240, "height": 140 },
           "save" : { "image_identifier" : "external_sample_1" }
       } ]
    }'

<span data-ttu-id="82b88-126">Aquí tenemos JSON que se llevará a una imagen de "src" "... boys.jpeg" y, a continuación, cambiar el tamaño de esa imagen too240x140.</span><span class="sxs-lookup"><span data-stu-id="82b88-126">Here we have JSON that will take a "src" image "...boys.jpeg" and then resize that image too240x140.</span></span>

<span data-ttu-id="82b88-127">Identificador de la aplicación Hello es algo que encontrará en el **información de conexión** o **administrar** ficha en Azure.</span><span class="sxs-lookup"><span data-stu-id="82b88-127">hello Application ID is something you can find in your **CONNECTION INFO** or **MANAGE** tab on Azure.</span></span> <span data-ttu-id="82b88-128">Es el identificador de secreto que le permite toorun trabajos Blitline.</span><span class="sxs-lookup"><span data-stu-id="82b88-128">It is your secret identifier that allows you toorun jobs on Blitline.</span></span>

<span data-ttu-id="82b88-129">Hola "Guardar" parámetro identifica la información sobre dónde desea tooput Hola imagen una vez que se han procesado.</span><span class="sxs-lookup"><span data-stu-id="82b88-129">hello "save" parameter identifies information about where you want tooput hello image once we have processed it.</span></span> <span data-ttu-id="82b88-130">En este caso específico, no definimos ninguno.</span><span class="sxs-lookup"><span data-stu-id="82b88-130">In this trivial case, we haven't defined one.</span></span> <span data-ttu-id="82b88-131">Si no se define ninguna ubicación, Blitline la almacenará localmente (o temporalmente) en una ubicación exclusiva de la nube.</span><span class="sxs-lookup"><span data-stu-id="82b88-131">If no location is defined Blitline will store it locally (and temporarily) at a unique cloud location.</span></span> <span data-ttu-id="82b88-132">Es posible que pueda tooget que la ubicación de hello JSON devuelto por Blitline al realizar hello Blitline.</span><span class="sxs-lookup"><span data-stu-id="82b88-132">You will be able tooget that location from hello JSON returned by Blitline when you make hello Blitline.</span></span> <span data-ttu-id="82b88-133">identificador de la "imagen" Hello es necesario y se devuelve tooyou cuando tooidentify esta guarda la imagen.</span><span class="sxs-lookup"><span data-stu-id="82b88-133">hello "image" identifier is required and is returned tooyou when tooidentify this particular saved image.</span></span>

<span data-ttu-id="82b88-134">También puede encontrar más información acerca de hello *funciones* admitimos aquí: <http://www.blitline.com/docs/functions></span><span class="sxs-lookup"><span data-stu-id="82b88-134">You can find more information about hello *functions* we support here: <http://www.blitline.com/docs/functions></span></span>

<span data-ttu-id="82b88-135">También puede encontrar documentación sobre Hola opciones del trabajo: <http://www.blitline.com/docs/api></span><span class="sxs-lookup"><span data-stu-id="82b88-135">You can also find documentation about hello job options here: <http://www.blitline.com/docs/api></span></span>

<span data-ttu-id="82b88-136">Una vez que tenga su JSON es todo lo que necesita toodo **POST** lo demasiado`http://api.blitline.com/job`</span><span class="sxs-lookup"><span data-stu-id="82b88-136">Once you have your JSON all you need toodo is **POST** it too`http://api.blitline.com/job`</span></span>

<span data-ttu-id="82b88-137">Obtendrá un resultado JSON con una apariencia similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="82b88-137">You will get JSON back that looks something like this:</span></span>

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


<span data-ttu-id="82b88-138">Esto indica que Blitline ha recibido la solicitud, coloca en una cola de procesamiento, y cuando se ha completado la imagen de hello estará disponible en: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_aplicación\_Id. /CK3f0xBF_2bV6wf7gEZE8w.jpg**</span><span class="sxs-lookup"><span data-stu-id="82b88-138">This tells you that Blitline has recieved your request, it has put it in a processing queue, and when it has completed hello image will be available at: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_APP\_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg**</span></span>

## <a name="how-toosave-an-image-tooyour-azure-storage-account"></a><span data-ttu-id="82b88-139">¿Cómo toosave una cuenta de almacenamiento de Azure de imagen tooyour</span><span class="sxs-lookup"><span data-stu-id="82b88-139">How toosave an image tooyour Azure Storage account</span></span>
<span data-ttu-id="82b88-140">Si tiene una cuenta de almacenamiento de Azure, puede tener fácilmente imágenes de Blitline inserción Hola procesado en el contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="82b88-140">If you have an Azure Storage account, you can easily have Blitline push hello processed images into your Azure container.</span></span> <span data-ttu-id="82b88-141">Mediante la adición de un "azure_destination" Definir ubicación hello y los permisos de Blitline toopush a.</span><span class="sxs-lookup"><span data-stu-id="82b88-141">By adding an "azure_destination" you define hello location and permissions for Blitline toopush to.</span></span>

<span data-ttu-id="82b88-142">Aquí tiene un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="82b88-142">Here is an example:</span></span>

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


<span data-ttu-id="82b88-143">Rellenando hello CAPITALIZED valores con su propio, puede enviar este toohttp://api.blitline.com/job JSON y se procesarán con un filtro de desenfoque hello "src" imagen y, a continuación, inserta tooyou destino de Azure.</span><span class="sxs-lookup"><span data-stu-id="82b88-143">By filling in hello CAPITALIZED values with your own, you can submit this JSON toohttp://api.blitline.com/job and hello "src" image will be processed with a blur filter and then pushed tooyou Azure destination.</span></span>

### <a name="please-note"></a><span data-ttu-id="82b88-144">Tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="82b88-144">Please note:</span></span>
<span data-ttu-id="82b88-145">Hola SAS debe contener Hola SAS dirección url completa, incluidos filename Hola Hola del archivo de destino.</span><span class="sxs-lookup"><span data-stu-id="82b88-145">hello SAS must contain hello entire SAS url, including hello filename of hello destination file.</span></span>

<span data-ttu-id="82b88-146">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="82b88-146">Example:</span></span>

    http://blitline.blob.core.windows.net/sample/image.jpg?sr=b&sv=2012-02-12&st=2013-04-12T03%3A18%3A30Z&se=2013-04-12T04%3A18%3A30Z&sp=w&sig=Bte2hkkbwTT2sqlkkKLop2asByrE0sIfeesOwj7jNA5o%3D


<span data-ttu-id="82b88-147">También puede leer la edición más reciente de Hola de documentos de almacenamiento de Azure del Blitline [aquí](http://www.blitline.com/docs/azure_storage).</span><span class="sxs-lookup"><span data-stu-id="82b88-147">You can also read hello latest edition of Blitline's Azure Storage docs [here](http://www.blitline.com/docs/azure_storage).</span></span>

## <a name="next-steps"></a><span data-ttu-id="82b88-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="82b88-148">Next Steps</span></span>
<span data-ttu-id="82b88-149">Visite blitline.com tooread sobre el resto de características:</span><span class="sxs-lookup"><span data-stu-id="82b88-149">Visit blitline.com tooread about all our other features:</span></span>

* <span data-ttu-id="82b88-150">Documentos del punto de conexión de la API de Blitline <http://www.blitline.com/docs/api></span><span class="sxs-lookup"><span data-stu-id="82b88-150">Blitline API Endpoint Docs <http://www.blitline.com/docs/api></span></span>
* <span data-ttu-id="82b88-151">Funciones de la API de Blitline <http://www.blitline.com/docs/functions></span><span class="sxs-lookup"><span data-stu-id="82b88-151">Blitline API Functions <http://www.blitline.com/docs/functions></span></span>
* <span data-ttu-id="82b88-152">Ejemplos de la API de Blitline <http://www.blitline.com/docs/examples></span><span class="sxs-lookup"><span data-stu-id="82b88-152">Blitline API Examples <http://www.blitline.com/docs/examples></span></span>
* <span data-ttu-id="82b88-153">Biblioteca Nuget de terceros <http://nuget.org/packages/Blitline.Net></span><span class="sxs-lookup"><span data-stu-id="82b88-153">Third Part Nuget Library <http://nuget.org/packages/Blitline.Net></span></span>

