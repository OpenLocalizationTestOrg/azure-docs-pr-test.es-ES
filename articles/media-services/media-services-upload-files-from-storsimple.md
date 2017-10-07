---
title: archivos de aaaUpload en una cuenta de servicios multimedia de Azure de StorSimple de Azure | Documentos de Microsoft
description: "Este artículo ofrece una breve introducción a Azure StorSimple Data Manager. artículo de Hello también incluye vínculos tootutorials que le muestran cómo tooextract datos de StorSimple y cargarlo como activos tooan cuenta de servicios multimedia de Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1dd09328-262b-43ef-8099-73241b49a925
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/27/2017
ms.author: juliako
ms.openlocfilehash: 7e9712aa480106bbd5fcc63eaecf0418b24a8bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-an-azure-media-services-account-from-azure-storsimple"></a>Carga de archivos en una cuenta de Azure Media Services mediante Azure StorSimple

Este artículo ofrece una breve introducción a Azure StorSimple Data Manager. artículo de Hello también incluye vínculos tootutorials que le muestran cómo tooextract datos de StorSimple y cargar estos datos como activos tooan cuenta de servicios de multimedia de Azure (AMS).

> 
> [!NOTE]
> Azure StorSimple Data Manager actualmente está en versión preliminar privada. 
> 

## <a name="overview"></a>Información general

En Servicios multimedia, cargue los archivos digitales en un recurso. Hola activo puede contener vídeo, audio, imágenes, colecciones de miniaturas, texto realiza un seguimiento y subtítulos archivos (y Hola metadatos acerca de estos archivos.) Una vez que se cargan archivos de hello, el contenido está almacenado en forma segura en nube de Hola para su posterior procesamiento y transmisión por secuencias.

[StorSimple de Azure](https://docs.microsoft.com/azure/storsimple/) usa almacenamiento en nube como solución local de una extensión de hello y automáticamente de capas de datos a través de un almacenamiento local hello y almacenamiento en la nube. dispositivo de StorSimple de Hello dedupes y comprime los datos antes de enviarlo en la nube toohello lo que muy eficaz para el envío de nube de toohello de archivos de gran tamaño. Hola [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) servicio proporciona las API que permiten tooextract de datos de StorSimple y presentan como activos de AMS.

## <a name="get-started"></a>Primeros pasos

1. [Crear una cuenta de servicios multimedia](media-services-portal-create-account.md) en la que desea que los activos de hello tootransfer.
2. Registrarse para la vista previa de administrador de datos, como se describe en hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) artículo.
3. Cree una cuenta de StorSimple Data Manager.
4. Cree un trabajo de transformación de datos que, cuando se ejecute, extraiga datos de un dispositivo de StorSimple y los transfiera como recursos a una cuenta de AMS. 

    Cuando el trabajo de hello empieza a ejecutarse, se crea una cola de almacenamiento. Esta cola se rellena con mensajes de los blobs transformados a medida que están listos. nombre de Hola de esta cola es Hola igual que el nombre de Hola Hola de definición de trabajo. Puede usar este toodetermine de cola cuando como activo es listos y llamar a su toorun deseado de operación de servicios multimedia de ella. Por ejemplo, puede usar este tootrigger cola una función de Azure que tiene código de servicios multimedia necesario hello en ella.

## <a name="see-also"></a>Otras referencias

[Use Hola .net SDK tootrigger trabajos Hola Data Manager](../storsimple/storsimple-data-manager-dotnet-jobs.md)

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Pasos siguientes

Ahora puede codificar los recursos cargados. Para más información, consulte [Encode an asset using Media Encoder Standard with the Azure portal](media-services-portal-encode.md)(Codificación de recursos mediante el estándar de codificador multimedia con el Portal de Azure).
