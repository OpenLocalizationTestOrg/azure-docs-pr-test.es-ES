---
title: aaaAzure Mobile Engagement Troubleshooting Guide - API
description: "Guías de solución de problemas de Azure Mobile Engagement - API"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3efc8a52-2b74-4917-b887-815ae8277474
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/04/2016
ms.author: piyushjo
ms.openlocfilehash: 5656b6f0f1aaf3e496a168c7cf09b307b9ab2a4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-api-issues"></a>Guía de solución de problemas de la API
los siguientes Hola son posibles problemas que pueden producirse con cómo los administradores interactúan con Azure Mobile Engagement a través de las API de Hola.

## <a name="syntax-issues"></a>Problemas de sintaxis
### <a name="issue"></a>Problema
* Errores de sintaxis mediante API de hello (o un comportamiento inesperado).

### <a name="causes"></a>Causas
* Problemas de sintaxis:
  * Que seguro toocheck Hola sintaxis de API específica de hello utilizas tooconfirm que Hola opción está disponible.
  * Un problema común con el uso de la API es tooconfuse Hola alcance de la API y Hola API de inserción (la mayoría de las tareas debe realizarse con hello API de cobertura en lugar de hello API de inserción). 
  * Otro problema común con integración con el SDK y el uso de API es hello tooconfuse clave de SDK y Hola clave de API.
  * Las secuencias de comandos que se conectan toohello API necesitan datos toosend al menos cada 10 minutos o conexión Hola agotará el tiempo (ser habitual sobre todo en secuencias de comandos de API de Monitor en escucha de datos). los tiempos de espera de tooprevent, tener el envío de secuencia de comandos un ping de XMPP cada sesión de Hola de 10 minutos tookeep activa con el servidor de Hola.

### <a name="see-also"></a>Otras referencias
* [Documentación de la API][Link 4]
* [Información del protocolo XMPP](http://xmpp.org/extensions/xep-0199.html)

## <a name="unable-toouse-hello-api-tooperform-hello-same-action-available-in-hello-azure-mobile-engagement-ui"></a>No se puede toouse Hola API tooperform Hola misma acción disponible en la interfaz de usuario de Azure Mobile Engagement Hola
### <a name="issue"></a>Problema
* Una acción que funciona de hello que no funciona la interfaz de usuario de Azure Mobile Engagement de hello relacionados con la API de Azure Mobile Engagement.

### <a name="causes"></a>Causas
* Confirmar que se puedan realizar Hola misma acción de interfaz de usuario de Azure Mobile Engagement hello muestra que se ha integrado correctamente esta característica de Azure Mobile Engagement con Hola SDK.

### <a name="see-also"></a>Otras referencias
* [Documentación de la interfaz de usuario][Link 1]

## <a name="error-messages"></a>Mensajes de error
### <a name="issue"></a>Problema
* Códigos de error mediante API de hello mostrada en tiempo de ejecución o en los registros.

### <a name="causes"></a>Causas
* A continuación se muestra una lista compuesta de números de códigos de estado de API comunes de referencia y de solución de problemas preliminar:
  
        200        Success.
        200        Account updated: device registered, associated, updated, or removed from hello current account.
        200        Returns a list of projects as a JSON object or an authentication token generated and returned in hello response’s body.
        201        Account created.
        400        Invalid parameter or validation exception (check payload for details). hello parameters provided toohello API or service are invalid. In this case, hello HTTP response will embed more details. Make sure tootest for hello MIME type of hello response as hello payload can either be plain text or a JSON object.
        401        Authentication error. No user is currently authenticated or connected (check hello AppID and SDK key).
        402        Billing lock. hello application is either off its quotas or is currently in a bad billing state.
        403        hello application is not enabled or hello specific API is disabled for this application.
        403        Unauthorized access toohello project or application, invalid access key (hello key must match hello one provided when created).
        403        Campaign specific errors: campaign must be finished (or has already been activated), hello suspend action can only be performed on an scheduled campaign, cannot finish a campaign that is not currently “in progress”, campaign must be “in progress” and hello campaign’s property named, manual Push must be set tootrue.
        403        hello email address is already associated tooanother account (a super user for instance). No authentication token will be generated.
        404        Application, device, campaign, or project identifier not found.
        404        Query parameter is invalid JSON or has a field with an unexpected value.
        404        hello email address is not associated with an account. Please create or update hello account first.
        405        Invalid HTTP method (GET, POST, etc.) or trying tooedit a read only segment (i.e. add or update or delete a criterion). A segment becomes read only after it has been computed for hello first time.
        409        Name already associated tooa different device ID or campaign.
        413        Too many device identifiers (current limit is 1,000), POST URL encoded entity is over 2MB, or hello period is too large toobe displayed (hello server didn’t retrieve hello analytics because hello user request is for a period that is too large).
        503        Analytics not available yet (hello requested information is not computed yet for an application).
        504        hello server was not able toohandle your request in a reasonable time (if you make multiple calls tooan API very quickly, try toomake one call at a time and spread hello calls out over time).

### <a name="see-also"></a>Consulte también
* [Documentación de API: para errores detallados en cada API específica][Link 4]

## <a name="silent-failures"></a>Errores silenciosos
### <a name="issue"></a>Problema
* Se produce un error en la acción de la API sin que se muestre ningún mensaje de error en el tiempo de ejecución o en los registros.

### <a name="causes"></a>Causas
* Muchos elementos se deshabilitará en hello interfaz de usuario de Azure Mobile Engagement si no se integra correctamente, pero se producirá un error en modo silencioso desde Hola API, por tanto, recuerde tootest Hola la misma funcionalidad de hello toosee de interfaz de usuario si funciona.
* Azure Mobile Engagement y muchas características avanzadas de Azure Mobile Engagement que está intentando toouse, toobe necesidad pasos independientes integra individualmente en su aplicación con hello SDK antes de utilizarlas.

### <a name="see-also"></a>Otras referencias
* [Guía de solución de problemas: SDK][Link 25]

<!--Link references-->
[Link 1]: mobile-engagement-user-interface-home.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/en-us/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/en-us/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/en-us/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

