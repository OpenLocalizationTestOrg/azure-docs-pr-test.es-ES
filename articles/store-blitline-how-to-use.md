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
# <a name="how-toouse-blitline-with-azure-and-azure-storage"></a>Cómo toouse Blitline con almacenamiento de Azure y Azure
Esta guía se explica cómo tooaccess Blitline servicios y cómo toosubmit trabajos tooBlitline.

## <a name="what-is-blitline"></a>¿Qué es Blitline?
Blitline es un servicio que proporciona el procesamiento de imagen de nivel empresarial en una fracción del precio de Hola que costaría toobuild de procesamiento de imágenes basado en la nube usted mismo.

hecho de Hello es que el procesamiento de imágenes se ha realizado una y otra vez, normalmente se vuelven a generar desde principio Hola hacia arriba para cada sitio Web. Sabemos esto porque las hemos generado un millón de veces. Un día decidimos que quizás era el momento de realizar el proceso para todos. Sabemos cómo toodo lo, toodo rápida y eficazmente y guardar todos los usuarios funciona en hello mientras tanto.

Para obtener más información, consulte [http://www.blitline.com](http://www.blitline.com).

## <a name="what-blitline-is-not"></a>¿Qué NO es Blitline?
tooclarify qué Blitline es útil para, es a menudo más fácil tooidentify qué Blitline no antes de continuar.

* Blitline no tiene imágenes de tooupload de widgets HTML. Debe tener imágenes disponibles públicamente o con permisos restringidos disponibles para Blitline tooreach.
* Blitline NO activa el procesamiento de imágenes, como Aviary.com.
* Blitline no acepta la carga de imágenes, no se pueden insertar su tooBlitline imágenes directamente. Debe insertarlas tooAzure almacenamiento o en otros lugares que blitline admite y, a continuación, indicar Blitline donde toogo obtenerlas.
* Blitline funciona de una forma totalmente paralela y NO realiza ningún procesamiento sincrónico. Esto significa que debe proporcionarnos una dirección URL postback_url para que podamos indicarle cuándo acabamos el procedimiento.

## <a name="create-a-blitline-account"></a>Creación de una cuenta Blitline
[!INCLUDE [blitline-signup](../includes/blitline-signup.md)]

## <a name="how-toocreate-a-blitline-job"></a>¿Cómo toocreate un trabajo Blitline
Blitline utiliza acciones de hello toodefine JSON que desee tootake en una imagen. JSON está compuesto por algunos campos simples.

ejemplo de Hola más simple es la siguiente:

        json : '{
       "application_id": "MY_APP_ID",
       "src" : "http://cdn.blitline.com/filters/boys.jpeg",
       "functions" : [ {
           "name": "resize_to_fit",
           "params" : { "width": 240, "height": 140 },
           "save" : { "image_identifier" : "external_sample_1" }
       } ]
    }'

Aquí tenemos JSON que se llevará a una imagen de "src" "... boys.jpeg" y, a continuación, cambiar el tamaño de esa imagen too240x140.

Identificador de la aplicación Hello es algo que encontrará en el **información de conexión** o **administrar** ficha en Azure. Es el identificador de secreto que le permite toorun trabajos Blitline.

Hola "Guardar" parámetro identifica la información sobre dónde desea tooput Hola imagen una vez que se han procesado. En este caso específico, no definimos ninguno. Si no se define ninguna ubicación, Blitline la almacenará localmente (o temporalmente) en una ubicación exclusiva de la nube. Es posible que pueda tooget que la ubicación de hello JSON devuelto por Blitline al realizar hello Blitline. identificador de la "imagen" Hello es necesario y se devuelve tooyou cuando tooidentify esta guarda la imagen.

También puede encontrar más información acerca de hello *funciones* admitimos aquí: <http://www.blitline.com/docs/functions>

También puede encontrar documentación sobre Hola opciones del trabajo: <http://www.blitline.com/docs/api>

Una vez que tenga su JSON es todo lo que necesita toodo **POST** lo demasiado`http://api.blitline.com/job`

Obtendrá un resultado JSON con una apariencia similar a la siguiente:

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


Esto indica que Blitline ha recibido la solicitud, coloca en una cola de procesamiento, y cuando se ha completado la imagen de hello estará disponible en: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_aplicación\_Id. /CK3f0xBF_2bV6wf7gEZE8w.jpg**

## <a name="how-toosave-an-image-tooyour-azure-storage-account"></a>¿Cómo toosave una cuenta de almacenamiento de Azure de imagen tooyour
Si tiene una cuenta de almacenamiento de Azure, puede tener fácilmente imágenes de Blitline inserción Hola procesado en el contenedor de Azure. Mediante la adición de un "azure_destination" Definir ubicación hello y los permisos de Blitline toopush a.

Aquí tiene un ejemplo:

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


Rellenando hello CAPITALIZED valores con su propio, puede enviar este toohttp://api.blitline.com/job JSON y se procesarán con un filtro de desenfoque hello "src" imagen y, a continuación, inserta tooyou destino de Azure.

### <a name="please-note"></a>Tenga en cuenta lo siguiente:
Hola SAS debe contener Hola SAS dirección url completa, incluidos filename Hola Hola del archivo de destino.

Ejemplo:

    http://blitline.blob.core.windows.net/sample/image.jpg?sr=b&sv=2012-02-12&st=2013-04-12T03%3A18%3A30Z&se=2013-04-12T04%3A18%3A30Z&sp=w&sig=Bte2hkkbwTT2sqlkkKLop2asByrE0sIfeesOwj7jNA5o%3D


También puede leer la edición más reciente de Hola de documentos de almacenamiento de Azure del Blitline [aquí](http://www.blitline.com/docs/azure_storage).

## <a name="next-steps"></a>Pasos siguientes
Visite blitline.com tooread sobre el resto de características:

* Documentos del punto de conexión de la API de Blitline <http://www.blitline.com/docs/api>
* Funciones de la API de Blitline <http://www.blitline.com/docs/functions>
* Ejemplos de la API de Blitline <http://www.blitline.com/docs/examples>
* Biblioteca Nuget de terceros <http://nuget.org/packages/Blitline.Net>

