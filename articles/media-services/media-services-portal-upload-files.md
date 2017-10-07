---
title: aaa"cargar archivos en una cuenta de servicios multimedia con hello portal de Azure | Documentos de Microsoft"
description: "Este tutorial le guiará por los pasos de Hola de carga de archivos en una cuenta de servicios multimedia con hello portal de Azure"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ad3dcea-95be-4711-9aae-a455a32434f6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 4ce1e133c72854532735ba7c72a43c92a75bc240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-azure-portal"></a>Cargar archivos en una cuenta de servicios multimedia mediante Hola portal de Azure
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-upload-files.md)
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> 
> [!NOTE]
> toocomplete este tutorial, necesita una cuenta de Azure. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 


En Servicios multimedia, cargue los archivos digitales en un recurso. Hola activo puede contener vídeo, audio, imágenes, colecciones de miniaturas, texto realiza un seguimiento y subtítulos archivos (y Hola metadatos acerca de estos archivos.) Una vez que se cargan archivos de hello, el contenido está almacenado en forma segura en nube de Hola para su posterior procesamiento y transmisión por secuencias.


## <a name="upload-files"></a>Carga de archivos

>[!NOTE]
>Hay un tamaño de archivo máximo de toohello límite admitido para el procesamiento de los servicios multimedia. Vea [esto](media-services-quotas-and-limitations.md) tema para obtener más información acerca de la limitación de tamaño de archivo de Hola.
>

1. Hola [portal de Azure](https://portal.azure.com/), seleccione su cuenta de servicios multimedia de Azure.
2. En hello **configuración** hoja, haga clic en **activos**.
   
    ![Carga de archivos](./media/media-services-portal-vod-get-started/media-services-upload.png)
3. Haga clic en hello **cargar** botón.
   
    Hola **cargar un recurso de vídeo** aparecerá la ventana.
   
   > [!NOTE]
   > No hay ninguna limitación de tamaño de archivo.
   > 
   > 
4. Examinar vídeo toohello deseado en el equipo, selecciónelo y haga clic en Aceptar.  
   
    inicia la carga de Hola y puede ver progreso de hello en nombre de archivo de Hola.  

Una vez completada la carga de hello, verá activo nuevo Hola enumerado en hello **activos** ventana. 

## <a name="next-steps"></a>Pasos siguientes
Ahora puede codificar los recursos cargados. Para más información, consulte [Encode an asset using Media Encoder Standard with the Azure portal](media-services-portal-encode.md)(Codificación de recursos mediante el estándar de codificador multimedia con Azure Portal).

También puede utilizar las funciones de Azure tootrigger un trabajo de codificación basado en un archivo que llegan en el contenedor de hello configurado. Para más información, consulte [este ejemplo](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

