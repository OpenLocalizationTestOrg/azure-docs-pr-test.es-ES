---
title: "Búsqueda de Azure de aaaAdding tooBlob almacenamiento | Documentos de Microsoft"
description: "Crear un índice en el código mediante Hola API de REST de HTTP de búsqueda de Azure."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
ms.service: search
ms.topic: article
ms.date: 05/04/2017
ms.author: ashmaka
ms.openlocfilehash: a3801790067bf169693b500e83799286b7387a77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="searching-blob-storage-with-azure-search"></a>Búsqueda en Blob Storage con Azure Search

La búsqueda a través de saludo diversos tipos de contenido almacenado en el almacenamiento de blobs de Azure, puede ser un problema difícil toosolve. Sin embargo, puede indizar y buscar Hola contenido de los Blobs en tan solo unos clics mediante la búsqueda de Azure. Para buscar en Blob Storage, es necesario aprovisionar un servicio de Azure Search. Hola distintos límites de servicio y los niveles de búsqueda de Azure de precios pueden encontrarse en hello [página de precios](https://aka.ms/azspricing).

## <a name="what-is-azure-search"></a>¿Qué es Azure Search?
[Búsqueda de Azure](https://aka.ms/whatisazsearch) es una solución de búsqueda que facilita el proceso de búsqueda de texto completo de los desarrolladores tooadd sólida experimenta tooweb y aplicaciones móviles. Como servicio, búsqueda de Azure quita Hola necesidad toomanage cualquier infraestructura de búsqueda durante la oferta de un [tiempo de actividad del 99,9% SLA](https://aka.ms/azuresearchsla).

Con una compatibilidad avanzada con 56 idiomas, Azure Search puede analizar el contenido y controlar de forma inteligente las construcciones específicas del idioma. Búsqueda de Azure también proporciona una experiencia de usuario de búsqueda de hello herramientas toobuild. Resulta sencillo tooadd características como la navegación por facetas, sugerencias de búsqueda de escritura anticipada y posicionamiento interfaces toouser resaltado con búsqueda de Azure. toolearn acerca de las características de búsqueda de Azure, puede leer del servicio de hello [documentación](https://aka.ms/azsearchdocs).

## <a name="crack-open-and-search-through-hello-content-of-enterprise-document-formats"></a>Ruptura abierto y la búsqueda a través de contenido de Hola de formatos de documentos de empresa
Con compatibilidad para [documento extracción](https://aka.ms/azsblobindexer) en almacenamiento de blobs de Azure, búsqueda de Azure puede indizar el contenido de hello una variedad de tipos de archivo almacenados en blobs:
- PDF
- Microsoft Office: DOC/DOCX, XLSX/XLS, PPTX/PPT y MSG (correos electrónicos de Outlook)
- HTML
- Texto sin formato

Mediante la extracción de texto y los metadatos de estos tipos de archivo, es fácil toosearch a través de varios formatos de archivo con un documentos más relevantes de consulta única toofind Hola independientemente del tipo. Al indizar Hola metadatos hello y contenido de documentos de Microsoft Office, PDF y mensajes de correo electrónico, es posible toobuild una solución de administración de contenido empresarial sólidas con el almacenamiento de blobs y búsqueda de Azure.

## <a name="search-through-your-blob-metadata"></a>Buscar en los metadatos del blob
Un escenario común que hace más fácil toosort a través de blobs de cualquier tipo de contenido es tooindex Hola blob personalizada definida por el usuario, metadatos, así como Hola propiedades del sistema para cada uno de los blobs. De este modo, información para cada blob se indiza independientemente del tipo de saludo del documento en el blob de hello, por lo que se puede ordenar fácilmente y la faceta a través de todo el contenido del almacenamiento de blobs.

[Obtenga más información sobre la indexación de metadatos del blob.](https://aka.ms/azsblobmetadataindexing)

## <a name="image-search"></a>Búsqueda de imágenes
Búsqueda de texto completo de la búsqueda de Azure, la navegación por facetas y capacidades de ordenación ahora pueden toohello aplicado metadatos de las imágenes almacenadas en blobs.

Si estas imágenes se procesan previamente mediante hello [equipo Vision API](https://www.microsoft.com/cognitive-services/computer-vision-api) de servicios de Microsoft cognitivos es contenido visual que hello tooindex posibles se encuentra en cada imagen incluido el reconocimiento de escritura a mano y reconocimiento óptico de caracteres. Estamos trabajando para agregar las imágenes de OCR y otras capacidades de procesamiento directamente tooAzure búsqueda, si está interesado en estas funcionalidades envíe una solicitud en nuestra [UserVoice](https://aka.ms/azsuv) o [envíenos un correo electrónico](mailto:azscustquestions@microsoft.com).

## <a name="index-and-search-through-json-blobs"></a>Indexar y buscar en blobs JSON
Búsqueda de Azure puede ser el contenido de tooextract configurado estructurado que se encuentra en los blobs que contienen JSON. Búsqueda de Azure puede leer los blobs JSON y analizar el contenido de hello estructurado en campos correspondientes de Hola de un documento de búsqueda de Azure. Búsqueda de Azure también puede tomar los blobs que contienen una matriz de objetos JSON y asignan cada documento de búsqueda de Azure de elemento tooa independiente.

Tenga en cuenta que el análisis de JSON no es actualmente configurable a través del portal de Hola. [Obtenga más información sobre el análisis de JSON en Azure Search.](https://aka.ms/azsjsonblobindexing)

## <a name="quick-start"></a>Inicio rápido
Búsqueda de Azure puede agregarse tooblobs directamente desde la hoja de portal de almacenamiento de blobs de Hola.

![](./media/search-blob-storage-integration/blob-blade.png)

Al hacer clic en la opción "Agregar búsqueda de Azure" Hola, inicia un flujo donde puede seleccionar un servicio de búsqueda de Azure existente o crear un nuevo servicio. Si crea un servicio, saldrá de la experiencia del portal de su cuenta de almacenamiento. Necesitará toore-navegue hoja de portal toohello almacenamiento y vuelva a seleccionar la opción de "Búsqueda de Azure agregar" hello, donde puede seleccionar servicio existente de Hola.

### <a name="next-steps"></a>Pasos siguientes
Obtener más información sobre Hola Blob indizador de búsqueda de Azure en hello completa [documentación](https://aka.ms/azsblobindexer).
