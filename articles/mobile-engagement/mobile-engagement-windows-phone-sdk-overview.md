---
title: "aaaAzure Mobile Engagement Windows Phone Silverlight información general del SDK | Documentos de Microsoft"
description: "Información general de Windows Phone Silverlight SDK de Azure Mobile Engagement hello"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0e3d2420-0509-4952-8891-392e3dad9aaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 11/03/2016
ms.author: piyushjo
ms.openlocfilehash: ff2febed2202127e0538373ebbabe674993ce39d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-overview-for-azure-mobile-engagement"></a>Introducción al SDK de Windows Phone Silverlight para Azure Mobile Engagement
Empiece aquí detalles de hello tooget acerca de cómo toointegrate Azure Mobile Engagement en un Windows Phone Silverlight App. Si desea que toogive que un bloque try en primer lugar, asegúrese de que complete nuestro [tutorial de 15 minutos](mobile-engagement-windows-phone-get-started.md).

Haga clic en hello toosee [contenido de SDK](mobile-engagement-windows-phone-sdk-content.md)

## <a name="integration-procedures"></a>Procedimientos de integración
1. Empiece aquí: [cómo toointegrate Mobile Engagement en la aplicación de Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
2. Para las notificaciones: [cómo toointegrate alcance (notificaciones) en la aplicación de Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement-reach.md)
3. Implementación del plan de etiqueta: [cómo toouse Hola avanzada Mobile Engagement etiquetado API en la aplicación de Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md)

## <a name="release-notes"></a>Notas de la versión
###<a name="331-11032016"></a>3.3.1 (03/11/2016)
Parte del programa Hola a *MicrosoftAzure.MobileEngagement* paquete Nuget **v3.4.1**

* Mejoras de estabilidad.

Para la versión anterior, consulte hello [completar notas de la versión](mobile-engagement-windows-phone-release-notes.md)

## <a name="upgrade-procedures"></a>Procedimientos de actualización
Si ya ha integrado una versión anterior de nuestro SDK en la aplicación, tener hello tooconsider siguientes puntos al actualizar Hola SDK.

Puede tener toofollow varios procedimientos si ejecutado varias versiones de hello SDK. Vea Hola completa [actualizar procedimientos](mobile-engagement-windows-phone-upgrade-procedure.md). Por ejemplo, si migra desde 0.10.1 too0.11.0 tiene toofirst siga Hola "de 0.9.0 too0.10.1" procedimiento, a continuación, Hola "de 0.10.1 too0.11.0" procedimiento.

### <a name="from-200-too330"></a>Desde 2.0.0 too3.3.0
#### <a name="test-logs"></a>Registros de prueba
Registros de la consola producidos por hello SDK ahora pueden habilitada, deshabilitada o filtrado. toocustomize, propiedad de hello actualización `EngagementAgent.Instance.TestLogEnabled` tooone del valor de hello disponible de hello `EngagementTestLogLevel` enumeración, por ejemplo:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="upgrade-from-older-versions"></a>Actualizar de versiones anteriores
Consulte [Procedimientos de actualización](mobile-engagement-windows-phone-upgrade-procedure.md)

