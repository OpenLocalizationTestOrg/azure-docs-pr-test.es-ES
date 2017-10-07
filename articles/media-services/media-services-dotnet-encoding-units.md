---
title: "media de aaaScale procesamiento mediante la adición de unidades de codificación - Azure |  Documentos de Microsoft"
description: "Obtenga información acerca de cómo toohow tooadd unidades de codificación con .NET"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 33f7625a-966a-4f06-bc09-bccd6e2a42b5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;milangada;
ms.openlocfilehash: b9f71a6487c5d136319a38a1598d60edfaa81b9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-encoding-with-net-sdk"></a>¿Cómo tooscale codificación con el SDK de .NET
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-scale-media-processing.md)
> * [.NET](media-services-dotnet-encoding-units.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>Información general
> [!IMPORTANT]
> Que seguro Hola tooreview [Introducción](media-services-scale-media-processing-overview.md) tooget de tema para obtener más información acerca de cómo ampliar el medio de procesamiento de tema.
> 
> 

Hola toochange Hola reservado hello y tipo de número de unidad con .NET SDK, de unidades reservadas de codificación siguientes:

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds tooS1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a>Apertura de una incidencia de soporte técnico
De forma predeterminada, cada cuenta de servicios multimedia puede escalar tooup too25 codificación y 5 petición unidades reservadas de Streaming. Si desea solicitar un límite mayor, abra una incidencia de soporte técnico.

### <a name="open-a-support-ticket"></a>Abrir una incidencia de soporte técnico
tooopen una incidencia de soporte técnico Hola siguientes:

1. Haga clic en [Obtener soporte técnico](https://manage.windowsazure.com/?getsupport=true). Si no ha iniciado sesión, tendrá que ser solicitada tooenter sus credenciales.
2. Seleccione su suscripción.
3. En el tipo de soporte, seleccione "Técnico".
4. Haga clic en "Crear incidencia".
5. Seleccione "Servicios multimedia de Azure" en la lista de productos de hello presentados en la página siguiente de saludo.
6. Seleccione un "Tipo de problema" que sea pertinente en relación con su problema.
7. Haga clic en Continue.
8. Siga las instrucciones que aparecen en la página siguiente y, a continuación, escriba los detalles de su problema.
9. Haga clic en enviar vale de hello tooopen.

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

