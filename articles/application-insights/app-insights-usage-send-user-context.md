---
title: uso de tooenable de contexto de usuario de aaaSending experiencias en Azure Application Insights | Documentos de Microsoft
description: "Realice un seguimiento de cómo los usuarios navegan por el servicio mediante la asignación a cada uno de ellos de una cadena de identificador única y persistente en Application Insights."
services: application-insights
documentationcenter: 
author: abgreg
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: csharp
ms.topic: article
ms.date: 08/02/2017
ms.author: bwren
ms.openlocfilehash: 0e6c2348f53a3ea970060334179b0dd070925e82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
#  <a name="sending-user-context-tooenable-usage-experiences-in-azure-application-insights"></a>Uso de tooenable de contexto de usuario envío experiencias en Azure Application Insights

## <a name="tracking-users"></a>Seguimiento de usuarios

Application Insights permite toomonitor y realizar un seguimiento de los usuarios a través de un conjunto de herramientas de uso del producto: 
* [Usuarios, sesiones, eventos](https://docs.microsoft.com/azure/application-insights/app-insights-usage-segmentation)
* [Embudos](https://docs.microsoft.com/azure/application-insights/usage-funnels)
* [Retención](https://docs.microsoft.com/azure/application-insights/app-insights-usage-retention)
* Cohortes
* [Libros](https://docs.microsoft.com/azure/application-insights/app-insights-usage-workbooks)

En orden tootrack lo que un usuario realiza por tiempo, Application Insights necesita un identificador para cada usuario o la sesión. Incluya estos identificadores en cada evento personalizado o vista de página.
- Usuarios, embudos, retención y cohortes: incluya el identificador de usuario.
- Sesiones: incluya el identificador de sesión.

Si la aplicación se integra con hello [SDK de JavaScript](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), es un seguimiento automático de Id. de usuario.

## <a name="choosing-user-ids"></a>Elección de los identificadores de usuario

Id. de usuario debe conservarse en tootrack de sesiones de usuario el comportan de los usuarios con el tiempo. Hay varios enfoques para conservar Hola identificador.
- Una definición de un usuario que ya tiene en su servicio.
- Si el servicio de Hola tiene explorador tooa de acceso, puede pasar una cookie con un Id. explorador hello en ella. Id. de Hola se conservará para siempre que la cookie de hello permanezca en el explorador del usuario de Hola.
- Si es necesario, puede utilizar un nuevo identificador de cada sesión, pero se limitarán los resultados de hello acerca de los usuarios. Por ejemplo, no será capaz de toosee cómo cambia el comportamiento de un usuario con el tiempo.

Hola identificador debe ser un Guid u otra cadena tooidentify lo suficientemente compleja como cada usuario forma única. Por ejemplo, podría ser un número aleatorio largo.

Si identificador hello contiene información de identificación personal sobre el usuario de hello, no es un tooApplication de toosend visión de valor adecuado como un identificador de usuario. Puede enviar un Id. como un [autenticado Id. de usuario](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), pero no cumple requisito de Id. de usuario de Hola para escenarios de uso.

## <a name="aspnet-apps-set-user-context-in-an-itelemetryinitializer"></a>Aplicaciones ASP.NET: Establecimiento del contexto de usuario en un inicializador de telemetría

Crear un inicializador de telemetría, tal y como se describe en detalle [aquí](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer)y establezca Hola Context.User.Id y Hola Context.Session.Id.

Este ejemplo establece el identificador de tooan de Id. de usuario de Hola que expira después de la sesión de Hola. Si es posible, use un identificador de usuario que se conserve entre sesiones.

*C#*

```C#

    using System;
    using System.Web;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that sets hello user ID.
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            // For a full experience, track each user across sessions. For an incomplete view of user 
            // behavior within a session, store user ID on hello HttpContext Session.
            // Set hello user ID if we haven't done so yet.
            if (HttpContext.Current.Session["UserId"] == null)
            {
                HttpContext.Current.Session["UserId"] = Guid.NewGuid();
            }

            // Set hello user id on hello Application Insights telemetry item.
            telemetry.Context.User.Id = (string)HttpContext.Current.Session["UserId"];

            // Set hello session id on hello Application Insights telemetry item.
            telemetry.Context.Session.Id = HttpContext.Current.Session.SessionID;
        }
      }
    }
```

## <a name="next-steps"></a>Pasos siguientes
- uso de tooenable experimenta, empezar a enviar [eventos personalizados](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) o [página vistas](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Si ya envía eventos personalizados o las vistas de página, explorar Hola uso herramientas toolearn cómo los usuarios utilizar el servicio.
    * [Información general del uso](app-insights-usage-overview.md)
    * [Usuarios, sesiones y eventos](app-insights-usage-segmentation.md)
    * [Embudos](usage-funnels.md)
    * [Retención](app-insights-usage-retention.md)
    * [Libros](app-insights-usage-workbooks.md)
