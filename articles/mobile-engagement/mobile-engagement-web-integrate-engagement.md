---
title: "integración con el SDK de Mobile Engagement Web aaaAzure | Documentos de Microsoft"
description: "Hola actualizaciones más recientes y procedimientos para hello Web SDK de Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: b5daa2a2-942b-489d-aa1d-568c3b25e56f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 02/29/2016
ms.author: piyushjo
ms.openlocfilehash: 99613b68b615bec4ddcfcc8e4e0133ce9d887bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a>Integración de Azure Mobile Engagement en una aplicación web
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

procedimientos de Hello en este artículo describen los análisis de Hola de manera más sencilla de hello tooactivate y las funciones de Azure Mobile Engagement en la aplicación web de supervisión.

Siga Hola pasos tooactivate Hola informes de registro que son necesario toocompute todas las estadísticas sobre los usuarios, sesiones, actividades, se bloquea y technicals. Para las estadísticas depende de la aplicación, como eventos y errores, trabajos, deberá activar manualmente los informes del registro mediante el uso de API de Azure Mobile Engagement Hola. Para obtener más información, consulte [cómo toouse Hola avanzada etiquetado API en una aplicación web de Mobile Engagement](mobile-engagement-web-use-engagement-api.md).

## <a name="introduction"></a>Introducción
[Descargar SDK de Azure Mobile Engagement Web hello](http://aka.ms/P7b453).
Hola Web de interacción móvil SDK se incluye como un único archivo de JavaScript, azure engagement.js, que tiene tooinclude en cada página de su sitio o aplicación web.

> [!IMPORTANT]
> Antes de ejecutar este script, debe ejecutar un script o que escriba tooconfigure Mobile Engagement para la aplicación de fragmento de código.
> 
> 

## <a name="browser-compatibility"></a>Compatibilidad con el explorador
Hola SDK de Mobile Engagement Web usa JSON nativo de codificación y descodificación, además de las solicitudes de AJAX de dominio toocross (depender de la especificación de W3C CORS Hola). Es compatible con hello siguientes exploradores:

* Microsoft Edge 12+
* Internet Explorer 10+
* Firefox 3.5+
* Chrome 4+
* Safari 6+
* Opera 12+

## <a name="configure-mobile-engagement"></a>Configuración de Mobile Engagement
Escribir un script que crea global `azureEngagement` objeto de JavaScript, como en el siguiente ejemplo de Hola. Como el sitio puede tener varias páginas, en el ejemplo se da por hecho que el script se incluye en cada página. En este ejemplo, se denomina objeto de JavaScript de hello `azure-engagement-conf.js`.

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

Hola `connectionString` valor de la aplicación se muestra en Hola portal de Azure.

> [!NOTE]
> `appVersionName` y `appVersionCode` son opcionales. Sin embargo, se recomienda configurarlos para que el análisis pueda procesar la información acerca de la versión.
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a>Incorporación de scripts de Mobile Engagement en las páginas
Agregar páginas de Mobile Engagement scripts tooyour de hello siguientes maneras:

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

O bien:

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a>Alias
Después de carga hello secuencia de comandos de SDK de Mobile Engagement Web, crea hello **interacción** alias tooaccess Hola API del SDK. No se puede usar esta configuración de SDK de alias toodefine Hola. El alias se usa como referencia en esta documentación.

Tenga en cuenta que si alias predeterminado de hello entra en conflicto con otra variable global de la página, puede volver a definir, en configuración de hello como se indica a continuación antes de cargarlos Hola SDK de Mobile Engagement Web:

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a>Informes básicos
Los informes básicos de Mobile Engagement incluyen estadísticas de nivel de sesión, tales como estadísticas sobre usuarios, sesiones, actividades y bloqueos.

### <a name="session-tracking"></a>Seguimiento de sesión
Las sesiones de Mobile Engagement se dividen en secuencias de actividades que se identifican por el nombre.

En un sitio web clásico, se recomienda declarar una actividad diferente en cada página del sitio. Para un sitio Web o aplicación web en qué Hola página actual nunca cambia, conviene tootrack actividades de hello en una escala más pequeña, como en la página de Hola.

Ya sea cierto, toostart o cambiar Hola actividad del usuario actual, llamada hello `engagement.agent.startActivity` función. Por ejemplo:

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

servidor de Mobile Engagement Hola termina automáticamente una sesión abierta en tres minutos después de cerrar la página de aplicación Hola.

También puede finalizar una sesión manualmente mediante una llamada a `engagement.agent.endActivity`. Esto establece hello too'Idle de actividad de usuario actual.'  sesión de Hello finalizará 10 segundos más tarde, a menos que un nuevo llamar demasiado`engagement.agent.startActivity` se reanuda la sesión de Hola.

Puede configurar retraso de 10 segundos de hello en objetos de interacción global hello, como sigue:

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end hello session as soon as endActivity is called

> [!NOTE]
> No se puede utilizar `engagement.agent.endActivity` en hello `onunload` devolución de llamada porque no se puede realizar llamadas de AJAX en esta fase.
> 
> 

## <a name="advanced-reporting"></a>Informes avanzados
Opcionalmente, si desea que los trabajos, los errores y eventos específicos de la aplicación de tooreport, deberá toouse Hola API de Mobile Engagement. Tiene acceso a API de Mobile Engagement hello mediante hello `engagement.agent` objeto.

Puede tener acceso a toda Hola capacidades en Mobile Engagement en hello Mobile Engagement API avanzadas. Hola API se detalla en el artículo hello [cómo toouse Hola avanzada etiquetado API en una aplicación web de Mobile Engagement](mobile-engagement-web-use-engagement-api.md).

## <a name="customize-hello-urls-used-for-ajax-calls"></a>Personalizar direcciones URL de hello usadas para las llamadas AJAX
Puede personalizar las direcciones URL que hello que usa el SDK de Mobile Engagement Web. Por ejemplo, tooredefine Hola dirección URL de registro (Hola SDK punto de conexión para el registro), se puede invalidar la configuración de hello similar a éste:

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

Si las funciones de dirección URL devuelven una cadena que comienza con `/`, `//`, `http://`, o `https://`, no se utiliza el esquema predeterminado de Hola. De forma predeterminada, Hola `https://` esquema se utiliza para las direcciones URL. Si desea que el esquema predeterminado de toocustomize hello, invalidar la configuración de hello, similar al siguiente:

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
