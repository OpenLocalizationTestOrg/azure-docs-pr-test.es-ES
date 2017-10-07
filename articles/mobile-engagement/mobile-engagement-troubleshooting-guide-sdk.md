---
title: aaaAzure Mobile Engagement Troubleshooting Guide - SDK
description: "Solución de problemas de integración de SDK en Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: de265cf1-2f88-43ef-8616-156ada5be7b6
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1c082b81d898f4bdb47b8efe6cfbacfd83fe9279
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-sdk-integration-issues"></a>Guía de solución de problemas de la integración de SDK
los siguientes Hola son posibles problemas que pueden producirse con cómo se integra Azure Mobile Engagement en la aplicación.

## <a name="sdk-issues-discovered-by-a-failure-in-another-area-of-your-application"></a>Problemas SDK descubiertos por un error en otra área de la aplicación
### <a name="issue"></a>Problema
* Error de colección de datos de interfaz de usuario (en el análisis, supervisión, segmentación o paneles).
* Errores de inserción (las inserciones no funcionan en la aplicación, fuera de la aplicación o en ambos).
* Fallos de función avanzados (no funcionan el seguimiento, la geolocalización o las inserciones específicas de plataforma).
* Errores de la API (las API fallan a menudo de manera silenciosa sin que se muestren mensajes de error).
* Errores del servicio (ninguno de los Azure Mobile Engagement funciona para su aplicación).

### <a name="causes"></a>Causas
* Un error en la aplicación (por ejemplo, un error de recopilación de datos de interfaz de usuario, error de inserción, fallos de las funciones avanzadas, error de la API, bloqueos de la aplicación o servicio aparente detectará la mayoría de los problemas que deben toobe resuelto con hello Azure Mobile Engagement SDK interrupción).  
* Si una característica determinada de Azure Mobile Engagement nunca ha funcionado en la aplicación antes, deberá toocomplete la integración de Hola. 
* Si una característica determinada de Azure Mobile Engagement estaba funcionando y detiene, deberá tooupgrade toohello última versión hello Azure Mobile Engagement SDK. Recuerde que hay una versión diferente de hello Azure Mobile Engagement SDK para cada plataforma compatible con Azure Mobile Engagement (Android, iOS, Windows y Windows Phone).

#### <a name="sdk-integration"></a>Integración de SDK
* Azure Mobile Engagement no integrado correctamente en el SDK (análisis).
* Cobertura no integrada correctamente en SDK (inserciones dentro y fuera de la aplicación).
* Certificado caducado o PROD frente a DEV incorrecto (únicamente iOS).
* GCM o ADM incorrectamente integrado en el SDK (solo en Android - Inserciones específicas del servicio).
* Seguimiento incorrectamente integrado en el SDK (instalar el seguimiento de la tienda).
* Ubicación diferida o ubicación de GPS incorrectamente integrada en el SDK (orientación mediante ubicación geográfica).

**Consulte también:**

* [Documentación del SDK - Guías de integración][Link 5] 
* [Guía de solución de problemas - Push][Link 23]

#### <a name="sdk-upgrade"></a>Actualización del SDK
* Tenga problemas de tooresolve tooupgrade SDK con versiones anteriores de hello SDK (toonewer a menudo relacionados versiones de sistema operativo del dispositivo hello).
* Desinstale todas las versiones anteriores de la aplicación desde el dispositivo y vuelva a instalar la versión más reciente de saludo de la aplicación, Hola volver a registrar el identificador de dispositivo de hello tooconfirm de interfaz de usuario de Azure Mobile Engagement que el dispositivo está utilizando la versión más reciente de saludo de la aplicación.

**Consulte también:**

* [Documentación del SDK - Notas de la versión](http://go.microsoft.com/fwlink/?LinkId= 525554) 
* [Documentación del SDK - Guía de actualización](http://go.microsoft.com/fwlink/?LinkId= 525554)

#### <a name="sdk-other"></a>Otros errores del SDK
* Los errores en el manifiesto de aplicación "AndroidManifest.xml" pueden producir Azure Mobile Engagement no toowork (solo Android).
* Un problema común con integración con el SDK y el uso de API es hello tooconfuse clave de SDK y Hola clave de API.

**Consulte también:**

* [Conceptos - Glosario][Link 6]

## <a name="advanced-coding-issues"></a>Problemas de codificación avanzados
### <a name="issue"></a>Problema
* Código específico de plataforma no relacionada directamente tooAzure que Mobile Engagement puede causar problemas en Windows Phone, iOS y Android.

### <a name="causes"></a>Causas
* Muchos problemas de codificación con Azure Mobile Engagement avanzados causados por plataforma escrito incorrectamente código específico no relacionada directamente tooAzure Mobile Engagement. Necesitará la plataforma de tooconsult documentación toohello específico que está desarrollando para además tooAzure documentación de Mobile Engagement (Android, iOS, Web, Windows y Windows Phone).
* Configurar no correctamente "categorías", impide que vincular desde una ubicación de tooanother notificación dentro o fuera de la aplicación hello (solo Android). 
* Si no se configura "UIKit.framework" demasiado "opcional" en el código de iOS, se muestra un "Error no encontrado"Symbol"o se bloquea en los dispositivos más antiguos de iOS (solo iOS).
* Certificados expirados o no correctamente mediante Hola desarrollo o una versión Prod de cert hello, inserción de causas problemas (solo iOS).
* No hay algunos plataforma tooa inherente de limitaciones que no se puede controlar Azure Mobile Engagement (por ejemplo, cómo Hola system center sirve para fuera de la aplicación inserta en iOS y Android).
* Azure Mobile Engagement publica una lista completa de paquetes de hello interno utilizado por Azure Mobile Engagement para iOS y Android como referencia. Tenga en cuenta que algunas características de Azure Mobile Engagement son toohello específico de la plataforma (Android, iOS, Web, Windows y Windows Phone).

### <a name="see-also"></a>Otras referencias
* [Guía de solución de problemas - Push][Link 23] 
* [Documentación del SDK - Notas de la versión][Link 5]
* [Documentación del SDK - Guía de actualización][Link 5]

## <a name="application-crashes"></a>Bloqueos de la aplicación
### <a name="issue"></a>Problema
* La aplicación se bloquea en el dispositivo de los usuarios de finales de Hola.

### <a name="causes"></a>Causas
* Información de bloqueo puede verse en hello *interfaz de usuario de análisis de* o hello *API de análisis*
* Puede encontrar Hola Id. de dispositivo del dispositivo de prueba y tomar Hola misma acción que provocó su toocrash de aplicación para un usuario final toohelp identificar la causa de Hola de su bloqueo.
* Problemas conocidos con hello Azure Mobile Engagement SDK que generan las aplicaciones toocrash a veces se resuelven mediante la actualización toohello la versión más reciente de hello SDK. Asegúrese de seguro toocheck Hola notas acerca de la plataforma al investigar los bloqueos.

### <a name="see-also"></a>Otras referencias
* [Documentación del SDK - Notas de la versión][Link 5]
* [Documentación del SDK - Guía de actualización][Link 5]

## <a name="app-store-upload-failures"></a>Fallos de carga de la tienda de aplicaciones
### <a name="issue"></a>Problema
* Errores relacionados con la versión más reciente de hello toouploading de su aplicación tooApple, Google o almacén de aplicación de Windows hello.

### <a name="causes"></a>Causas
* Aplicación a veces almacena bloquear las aplicaciones con ciertas características habilitadas (p. ej. Hola Store de Apple impide el uso de Hola de IDFV en las aplicaciones de almacén de Hola y almacén de hello GooglePlay evita Hola de uso compartido de información entre las aplicaciones de la aplicación). 
* Asegúrese de que ha activado notas de la versión de Hola acerca de la plataforma y la versión actual de hello SDK si tiene dificultades para cargar un almacén de toohello de aplicación.

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
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

