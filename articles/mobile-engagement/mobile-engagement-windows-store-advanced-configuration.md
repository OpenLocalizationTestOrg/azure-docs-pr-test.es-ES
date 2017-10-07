---
title: "Configuración de Windows Universal aplicaciones Engagement SDK aaaAdvanced"
description: "Opciones de configuración para Azure Mobile Engagement con aplicaciones universales de Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6d85dd5d-ac07-43ba-bbe4-e91c3a17690b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 23bd05012bc25d438d8d4985a112280bed0292b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-windows-universal-apps-engagement-sdk"></a>Configuración avanzada del SDK de Engagement para aplicaciones universales de Windows
> [!div class="op_single_selector"]
> * [Windows universal](mobile-engagement-windows-store-advanced-configuration.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-configuration.md)
> 
> 

Este procedimiento describe cómo tooconfigure distintas opciones de configuración para las aplicaciones de Azure Mobile Engagement Android.

## <a name="prerequisites"></a>Requisitos previos
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="advanced-configuration"></a>Configuración avanzada
### <a name="disable-automatic-crash-reporting"></a>Deshabilitar los informes automáticos de bloqueo
Puede deshabilitar Hola automática de informes de errores característica de contratación. Cuando se produzca una excepción no controlada, Engagement no hará nada.

> [!WARNING]
> Si deshabilita esta característica, cuando se produce un bloqueo no controlado en la aplicación, interacción no envía el bloqueo de hello **AND** no cierra la sesión de Hola y trabajos.
> 
> 

bloqueo automático toodisable reporting, personalizar la configuración según la forma de Hola se declaró:

#### <a name="from-engagementconfigurationxml-file"></a>Desde el archivo `EngagementConfiguration.xml`
Establecer un informe de bloqueo demasiado`false` entre `<reportCrash>` y `</reportCrash>` etiquetas.

#### <a name="from-engagementconfiguration-object-at-run-time"></a>Desde el objeto `EngagementConfiguration` en tiempo de ejecución
Establecer toofalse de bloqueo de informe mediante el objeto EngagementConfiguration.

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="disable-real-time-reporting"></a>Deshabilitar los informes en tiempo real
De forma predeterminada, los registros de informes del servicio de contratación de hello en tiempo real. Si la aplicación informa de los registros con frecuencia, es mejor toobuffer Hola registros y tooreport usarlas todos a la vez en una base de tiempo regulares. Esto se denomina "modo de ráfaga".

toodo por lo tanto, llame al método hello:

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

Hola argumento es un valor en **milisegundos**. Siempre que lo desee registro en tiempo real de tooreactivate hello, llamar a método de hello sin ningún parámetro, o con el valor de hello 0.

El modo de ráfaga ligeramente aumenta la duración de la batería de hello pero tiene un impacto en el Monitor de interacción de hello: duración de las sesiones y los trabajos de todos los son toohello redondeado ráfaga umbral (por lo tanto, las sesiones y trabajos más cortos que el umbral de ráfaga de hello puede no estar visible). Se recomienda usar un umbral de ráfaga inferior a 30 000 (30 segundos). Registros guardados son elementos de too300 limitado. Si el envío es demasiado largo, puede perder algunos registros.

> [!WARNING]
> umbral de ráfaga de Hello no puede ser configurado tooa período menor que uno en segundo lugar. Si lo hace, Hola SDK muestra un seguimiento con error de Hola y restablece automáticamente el valor predeterminado de toohello, cero segundos. Este desencadenadores Hola SDK tooreport Hola registra en tiempo real.
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview
