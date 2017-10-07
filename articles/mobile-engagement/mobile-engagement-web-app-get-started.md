---
title: aaaGet a trabajar con Azure Mobile Engagement para las aplicaciones Web | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Azure Mobile Engagement a las notificaciones de inserción y de análisis para las aplicaciones Web."
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04afe53a-4caf-4c80-bd75-20cc630cd75c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: js
ms.topic: hero-article
ms.date: 06/01/2016
ms.author: piyushjo
ms.openlocfilehash: a84c96cac13bf3b85e72aef55da5c91693e1766c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-web-apps"></a>Introducción a Azure Mobile Engagement para Web Apps
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Este tema muestra cómo toouse Azure Mobile Engagement toounderstand el uso de la aplicación Web.

> [!NOTE]
> servicio de Azure Mobile Engagement Hola se retirará de 2018 de marzo y actualmente solo los clientes de tooexisting disponible. Para más información, consulte [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Este tutorial requiere siguiente de hello:

* Visual Studio 2015, o cualquier otro editor que prefiera
* [SDK web](http://aka.ms/P7b453)

Este SDK Web está en vista previa y solo admite el análisis en el momento de Hola y todavía no admite notificaciones de inserción de explorador o de la aplicación de envío. 

> [!NOTE]
> toocomplete este tutorial, debe tener una cuenta activa de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).
> 
> 

## <a name="setup-mobile-engagement-for-your-web-app"></a>Configuración de Mobile Engagement para una aplicación web
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Conectar el back-end de aplicación toohello Mobile Engagement
Este tutorial presenta una "integración básica", que es Hola conjunto mínimo necesario toocollect datos.

Se creará una aplicación web básica con la integración de Visual Studio toodemonstrate Hola aunque puede seguir pasos de hello con cualquier aplicación web que se creó fuera de Visual Studio también. 

### <a name="create-a-new-web-app"></a>Creación de una aplicación web nueva
Hello siguientes pasos supone Hola uso de Visual Studio 2015 aunque Hola pasos son similares en versiones anteriores de Visual Studio. 

1. Inicie Visual Studio y en hello **inicio** pantalla, seleccione **nuevo proyecto**.
2. En el menú emergente de hello, seleccione **Web** -> **aplicación Web ASP.Net**. Rellene la aplicación hello **nombre**, **ubicación** y **nombre de la solución**y, a continuación, haga clic en **Aceptar**.
3. Hola **seleccione una plantilla de** ventana emergente, seleccione **vacía** en **ASP.Net 4.5 plantillas** y haga clic en **Aceptar**. 

Ahora ha creado un nuevo proyecto de aplicación Web en blanco en el que se integrará hello Web de Azure Mobile Engagement SDK.

### <a name="connect-your-app-toomobile-engagement-backend"></a>Conectar el backend de interacción de tooMobile de aplicación
1. Cree una carpeta nueva denominada **javascript** en la solución y agregue el archivo de Web SDK JS hello **engagement.js azure** en él. 
2. Agregar un nuevo archivo denominado **main.js** en esta carpeta de javascript con el siguiente código de hello. Asegúrese de cadena de conexión de hello tooupdate seguro. Esto `azureEngagement` objeto será tooaccess usa métodos Web SDK. 
   
        var azureEngagement = {
            debug: true,
            connectionString: 'xxxxx'
        };
   
    ![Visual Studio con archivos js][1]

## <a name="enable-real-time-monitoring"></a>Habilitación de la supervisión en tiempo real
En orden toostart enviando los datos y asegurarse de que los usuarios de hello activos, debe enviar al menos una actividad toohello Mobile Engagement back-end. Una actividad en el contexto de Hola de una aplicación web es una página web. 

1. Cree una nueva página denominada **home.html** en la solución y se establece como Hola a partir de página de la aplicación web. 
2. Incluir Hola dos archivos JavaScript que se agregó anteriormente en esta página agregando Hola siguientes dentro de la etiqueta body de Hola. 
   
        <script type="text/javascript" src="javascript/main.js"></script>
        <script type="text/javascript" src="javascript/azure-engagement.js"></script>
3. Actualizar Hola cuerpo etiqueta toocall EngagementAgent `startActivity` (método)
   
        <body onload="engagement.agent.startActivity('Home')">
4. Así será **home.html** .
   
        <html>
        <head>
            ...
        </head>
        <body onload="engagement.agent.startActivity('Home')">
            <script type="text/javascript" src="javascript/main.js"></script>
            <script type="text/javascript" src="javascript/azure-engagement.js"></script>
        </body>
        </html>

## <a name="connect-app-with-real-time-monitoring"></a>Conectar la aplicación con la supervisión en tiempo real
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

  ![][2]

## <a name="extend-analytics"></a>Ampliación del análisis
Aquí están actualmente disponibles con el SDK de Web que puede usar para el análisis de todos los métodos de hello:

1. Actividades y páginas web:
   
        engagement.agent.startActivity(name);
        engagement.agent.endActivity();
2. Eventos
   
        engagement.agent.sendEvent(name, extras);
3. Errors
   
        engagement.agent.sendError(name, extras);
4. Trabajos
   
        engagement.agent.startJob(name);
        engagement.agent.endJob(name);

<!-- Images. -->
[1]: ./media/mobile-engagement-web-app-get-started/visual-studio-solution-js.png
[2]: ./media/mobile-engagement-web-app-get-started/session.png

