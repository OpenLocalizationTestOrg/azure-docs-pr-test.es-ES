---
title: media de aaaScale procesamiento mediante Hola portal de Azure | Documentos de Microsoft
description: "Este tutorial le guiará por los pasos de Hola de escalado medios procesamiento mediante Hola portal de Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: e500f733-68aa-450c-b212-cf717c0d15da
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: 89240c6f7579b8795e7b47f2b1c398b1d5477e20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-reserved-unit-type"></a>Tipo de unidad de cambio Hola reservado
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encoding-units.md)
> * [Portal](media-services-portal-scale-media-processing.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>Información general

Una cuenta de servicios multimedia está asociada a un tipo de unidad reservada, que determina la velocidad de hello con la que se procesan los medios de las tareas de procesamiento. Puede elegir entre como consecuencia de hello reservado los tipos de unidad: **S1**, **S2**, o **S3**. Por ejemplo, hello mismo trabajo de codificación se ejecuta con mayor rapidez cuando se usa hello **S2** tipo de unidad reservada comparar toohello **S1** tipo.

Además toospecifying Hola reservado del tipo de unidad, puede especificar su cuenta con tooprovision **unidades reservadas** (RUs). número de Hola de RUs aprovisionados determina número Hola de tareas multimedia que se pueden procesar simultáneamente en una cuenta determinada.

>[!NOTE]
>Las unidades reservadas sirven para establecer paralelismos en todo el procesamiento multimedia, incluida la indexación de trabajos mediante Azure Media Indexer. Sin embargo, a diferencia de la codificación, la indexación de los trabajos no se procesará más rápido con unidades reservadas de mayor rapidez.

> [!IMPORTANT]
> Que seguro Hola tooreview [Introducción](media-services-scale-media-processing-overview.md) tooget de tema para obtener más información acerca de cómo ampliar el medio de procesamiento de tema.
> 
> 

## <a name="scale-media-processing"></a>Escalar el procesamiento multimedia
toochange Hola reservado hello y tipo de número de unidad de unidades reservadas, Hola siguientes:

1. Hola [portal de Azure](https://portal.azure.com/), seleccione su cuenta de servicios multimedia de Azure.
2. Hola **configuración** ventana, seleccione **unidades reservadas de multimedia**.
   
    número de hello toochange de unidades reservadas para hello seleccionado el tipo de unidad reservada, use hello **unidades de medios servida** control deslizante.
   
    Hola toochange **tipo de unidad reservada**, presione S1, S2 o S3.
   
    ![Página de procesadores](./media/media-services-portal-scale-media-processing/media-services-scale-media-processing.png)
3. Hola presione Guardar botón toosave los cambios.
   
    unidades reservadas de Hola se asignan cuando se presiona guardar.

## <a name="next-steps"></a>Pasos siguientes
Consulte las rutas de aprendizaje de Servicios multimedia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

