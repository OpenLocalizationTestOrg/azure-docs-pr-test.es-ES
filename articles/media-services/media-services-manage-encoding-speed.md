---
title: "velocidad de administrar aaa y la simultaneidad de la codificación con servicios multimedia de Azure | Documentos de Microsoft"
description: "En este artículo se proporciona una breve introducción sobre cómo puede administrar la velocidad y la simultaneidad de las trabajos y las tareas de codificación con Azure Media Services."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 676313f8-a158-4e3a-a99b-2c29a341ecc9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: da52a6278a3d3b084dbf5a594db37df8447bb944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a>Administración de la velocidad y la simultaneidad de la codificación

En este artículo se proporciona una breve introducción sobre cómo puede administrar la velocidad y la simultaneidad de las trabajos y las tareas de codificación.

## <a name="overview"></a>Información general

En los servicios multimedia, un **tipo de unidad reservada** determina la velocidad de hello con la que se procesan los medios de las tareas de procesamiento. Puede elegir entre como consecuencia de hello reservado los tipos de unidad: **S1**, **S2**, o **S3**. Por ejemplo, hello mismo trabajo de codificación se ejecuta con mayor rapidez cuando se usa hello **S2** tipo de unidad reservada comparar toohello **S1** tipo. Hola [ajuste de escala en unidades de codificación](media-services-scale-media-processing-overview.md) tema muestra una tabla que le ayuda a tomar la decisión al elegir entre distintas velocidades de codificación.

Además toospecifying Hola reservado del tipo de unidad, puede especificar su cuenta con tooprovision **unidades reservadas**. número de Hola de unidades reservadas aprovisionadas determina número Hola de tareas multimedia que se pueden procesar simultáneamente en una cuenta determinada. Por ejemplo, si su cuenta tiene cinco unidades reservadas, se ejecutarán simultáneamente siempre y tareas de cinco medios como hay toobe de tareas que se procesan. las tareas restantes de Hello esperarán en cola de Hola y se procesarán de manera secuencial cuando finaliza una tarea en ejecución. Si una cuenta no tiene ninguna unidad reservada aprovisionada, las tareas se elegirán de manera secuencial. En este caso, Hola de tiempo entre la finalización de una tarea de espera y hello siguiente que empieza dependerá disponibilidad Hola de recursos de sistema de Hola.

Para obtener información detallada y ejemplos que muestran cómo tooscale unidades de codificación, vea [esto](media-services-scale-media-processing-overview.md) tema.

## <a name="next-step"></a>Paso siguiente

[Escalar unidades de codificación](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

