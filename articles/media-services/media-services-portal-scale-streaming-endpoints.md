---
title: aaaScale streaming extremos con hello portal de Azure | Documentos de Microsoft
description: "Este tutorial le guiará por los pasos de Hola de ajuste de escala en los extremos de streaming con hello portal de Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1008b3a3-2fa1-4146-85bd-2cf43cd1e00e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: e466edf9232558b9e270f54ee2849cd9b22ad121
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scale-streaming-endpoints-with-hello-azure-portal"></a>Escalar los extremos de streaming con hello portal de Azure
## <a name="overview"></a>Información general

> [!NOTE]
> toocomplete este tutorial, necesita una cuenta de Azure. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

Los puntos de conexión de streaming **Premium** son adecuados para cargas de trabajo avanzadas y proporcionan una capacidad de ancho de banda dedicada y escalable. Los clientes que tienen un punto de conexión de streaming **Premium**, de forma predeterminada, obtienen una unidad de streaming (SU). Hola extremo de streaming puede ampliarse mediante la adición de SUs. Cada SU proporciona aplicaciones de toohello de capacidad de ancho de banda adicional. Para obtener más información acerca de los tipos de punto de conexión y la configuración de red CDN de transmisión por secuencias, vea hello [información general de transmisión por secuencias Endpoint](media-services-portal-manage-streaming-endpoints.md) tema.
 
Este tema se muestra cómo tooscale un extremo de streaming.

Para obtener más información acerca del precio, consulte la página sobre [información del precio de Servicios multimedia](http://go.microsoft.com/fwlink/?LinkId=275107).

## <a name="scale-streaming-endpoints"></a>Escalar puntos de conexión de streaming

número de hello toochange de unidades de streaming, Hola siguientes:

1. Hola [portal de Azure](https://portal.azure.com/), seleccione su cuenta de servicios multimedia de Azure.
2. Hola **configuración** ventana, seleccione **los extremos de Streaming**.
3. Haga clic en extremo de streaming de Hola que desea tooscale. 

    [!NOTE] Solo puede escalar puntos de conexión de streaming **Premium**.

4. Mover el número de Hola de hello control deslizante toospecify de unidades de streaming.

    ![punto de conexión de streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints3.png)

## <a name="next-steps"></a>Pasos siguientes
Consulte las rutas de aprendizaje de Servicios multimedia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

