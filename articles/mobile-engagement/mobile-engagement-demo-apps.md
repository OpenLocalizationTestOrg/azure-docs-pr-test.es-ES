---
title: "aplicación de demostración de Mobile Engagement aaaAzure | Documentos de Microsoft"
description: "Describe dónde toodownload, cómo toouse y Hola ventajas del uso de Azure Mobile Engagement demostración de aplicación"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: f624d5aa-254b-4ad0-96a3-f00e6c3a2c97
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2016
ms.author: piyushjo
ms.openlocfilehash: 9ff0df0d21e1bad6aff573db49304a55593df1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-demo-app"></a>Aplicación de demostración de Azure Mobile Engagement
Hemos publicado una aplicación de demostración de Azure Mobile Engagement para **iOS**, **Android**, y **Windows** toohelp de plataformas que recursos útiles de toofind y obtener más información sobre Mobile Interacción.

aplicación Hello le ayuda a:

* Encontrar fácilmente vínculos útiles recursos de interacción de tooMobile como vídeos, documentación, foro de soporte técnico de hello, y que se solicita toogo tooraise característica.
* Notificaciones de ejemplo de experiencia que son compatibles con ideas de tooget de Mobile Engagement para sus propias aplicaciones móviles.
* Usar un toostudy de implementación de referencia cómo tooimplement Mobile Engagement en su aplicación. Puede aprender a:
  
  * Recopilar datos de análisis.
  * Implementar escenarios avanzados de notificación del tipo *Pantalla completa intersticial* o *Emergente*.
  * Implementar encuestas y sondeos.
  * Implementar escenarios de inserción silenciosa o inserción de datos.   

## <a name="app-installation"></a>Instalación de la aplicación
Esta aplicación está disponible en hello después de tiendas de aplicaciones:

* **Aplicación de demostración universal de Windows**:
  
  * Descargar la aplicación hello en hello [tienda de aplicaciones de Windows](https://www.microsoft.com/en-us/store/apps/azure-mobile-engagement/9nblggh4qmh2).
  * aplicación Hello se desarrolló como una aplicación Universal de Windows 10. está disponible en código fuente de Hello [GitHub](https://github.com/Azure/azure-mobile-engagement-app-windows).
* **Aplicación de demostración de iOS**:
  
  * Descargar la aplicación hello en hello [store de Apple](https://itunes.apple.com/us/app/azure%20mobile%20engagement/id1105090090).
  * se desarrolló la aplicación Hello en iOS Swift. está disponible en código fuente de Hello [GitHub](https://github.com/Azure/azure-mobile-engagement-app-ios).
* **Aplicación de demostración de Android**:
  
  * Descargar la aplicación hello en hello [Google Play store](https://play.google.com/store/apps/details?id=com.microsoft.azure.engagement).
  * está disponible en código fuente de Hello [GitHub](https://github.com/Azure/azure-mobile-engagement-app-android).

![Aplicación de demostración universal de Windows][1]

![aplicación de demostración de iOS][2]
![aplicación de demostración de Android][3]

## <a name="usage"></a>Uso
Puede usar esta aplicación Hola siguientes maneras:

**Descargar la aplicación hello en el dispositivo de vínculos de almacén de aplicación Hola (proporcionado anteriormente):**

> [!IMPORTANT]
> No necesita una cuenta de Azure y necesita tooconnect Hola aplicación tooa back. aplicación Hello funciona de forma independiente.
> 
> 

* Una vez que la aplicación hello en el dispositivo, puede ir a través de vínculos de hello en hello menú izquierda toofind Hola recursos útiles acerca de Mobile Engagement.
* Hemos agregado hello [fuentes RSS del servicio](https://aka.ms/azmerssfeed) en esta aplicación para que siempre esté informado actualizaciones de producto más recientes de Hola.
* También puede ir a través del tipo hello ejemplo notificación escenarios tooexperience Hola de notificaciones que son compatibles con Mobile Engagement para cada plataforma. Estas notificaciones se pueden experimentados localmente, es decir, puede hacer clic en botones de hello en tooshow de pantallas de Hola Hola experiencia de notificaciones, que es las notificaciones de hello toosending idénticos de plataforma de Mobile Engagement Hola.

![Menú de aplicación para Windows][4]

![Menú de aplicación para iOS][5]
![Menú de la aplicación para Android][6]

**Descargar código fuente de Hola de hello vínculos de GitHub (proporcionado anteriormente):**

* Una vez que haya descargado el código fuente de hello, ábralo en entorno de desarrollo respectivos de hello--XCode para iOS, Android Studio para Visual Studio para Windows y Android.
* A continuación deben seguir nuestra [pasos básicos de la integración de SDK](mobile-engagement-windows-store-dotnet-get-started.md) para que le pueda tooconnect esta tooits aplicación posee instancia de back-end de interacción móvil.
  * Necesita una cadena de conexión en la aplicación hello tooconfigure.
  * También necesita plataforma de notificación de inserción de hello tooconfigure para la aplicación.
* Observará que la aplicación hello propio está instrumentada con Mobile Engagement. Por lo tanto, que se abre la aplicación hello después de conectarse toohello back-end, podrá toosee capaz de sesión de usuario de hello, actividades, eventos y así sucesivamente, en hello **Monitor** ficha.
* También podrá toosend capaz de notificaciones toothis aplicación desde su propia instancia de Mobile Engagement, en lugar de usar notificaciones locales.
  
  * Aquí puede agregar un dispositivo como un dispositivo de prueba mediante el uso de hello **Get hello Id. de dispositivo** elemento de menú en la aplicación hello. Esto le proporciona un id. de dispositivo que, a continuación, registra como un dispositivo de prueba con la instancia de back-end de la plataforma.
    
    ![Id. de dispositivo en Windows][7]
    
    ![Id. de dispositivo en iOS][8]
    ![Id. de dispositivo en Android][9]

## <a name="key-features-of-hello-demo-app"></a>Características clave de aplicación de demostración de hello
* Como se mencionó anteriormente, con esta aplicación, tiene todos los recursos clave Hola para Mobile Engagement en la mano. Puede ir a través de vínculos de hello en el menú de la izquierda Hola.
* Puede experimentar notificaciones fuera de aplicación para cada plataforma. Estas notificaciones se pueden entregar como **solo notificación**, que simplemente haga clic en notificación Hola abrir una pantalla nativo de la aplicación hello hacia arriba (mediante el uso de **vinculación profunda**)--o como un **Web anuncio**, donde puede entregar contenido HTML adicional de hello terminar de Mobile Engagement volver toobe muestra cuando se hace clic en la notificación de Hola.
  
    ![Notificaciones fuera de la aplicación][29]
* En iOS, tener tooclose Hola aplicación toosee Hola sistema o aplicación de notificaciones de inserción. Puede mirar Hola aquí la implementación para agregar **botones de acción**, como Hola si son agregados toothis notificación de fuera de la aplicación para *comentarios* y *recurso compartido* (de modo que Hola usuario puede adoptar derecha de la acción de notificación de hello propio).
  
    ![Notificaciones fuera de la aplicación en iOS][11] ![Visualización de notificaciones fuera de la aplicación en iOS][14]
* En Android, opciones de hello admitidas están agregando texto multilínea (**texto grande**) o una imagen de notificación (**panorama**) toohello notificación, junto con hello **botones de acción** (como compatibles con iOS).
  
    ![Notificaciones fuera de la aplicación en Android][12] ![Visualización de notificaciones fuera de la aplicación en Android][15]
* En Windows 10, puede ver el aspecto de las notificaciones de hello en hello PC. Esta notificación también se presenta en Windows 10 hello **centro de notificaciones**. No hay compatibilidad para agregar **botones de acción** en el momento de hello en el SDK de Windows hello.
  
    ![Notificaciones fuera de la aplicación en Windows][10] ![Visualización fuera de la aplicación en Windows][13]
* Puede probar las notificaciones en aplicación para cada plataforma. Se trata de una experiencia de dos pasos donde se muestra primera una ventana de **notificación** . Al hacer clic en él, se abre una pantalla completa **anuncio**, tal y como se muestra en la siguiente captura de pantalla de Hola. contenido de Hola de este anuncio procede de la instancia de back-end de Mobile Engagement. Hola SDK dispone de plantillas de Hola para las notificaciones y los anuncios. Se pueden personalizar fácilmente, como se muestra en esta aplicación de demostración con adición de Hola de nuestro logotipo y el color de.  
  
    ![Notificaciones en aplicación en Windows][16]
  
    ![Notificaciones en aplicación en iOS][17]  ![Notificaciones en aplicación en Android][18]
  
    **iOS**, **Android**
* También puede usar hello **categoría** característica de Mobile Engagement toocustomize esta experiencia de forma predeterminada. En la aplicación de demostración de hello, hemos demostrado dos formas toochange Hola experiencia común de notificaciones de Hola. Tenga en cuenta que esta característica de categoría de hello no se admite todavía en hello SDK de Windows.
  
    **Pantalla completa intersticial:**
  
    ![Notificación en aplicación: categoría intersticial][30]
  
    ![Categoría intersticial en iOS][21]     ![Categoría intersticial en Android][22]
  
    **Notificación emergente:**
  
    ![Notificación en aplicación: categoría emergente][31]
  
    ![Notificación emergente en iOS][19]    ![Notificación emergente en Android][20]

**iOS**, **Android**

* Mobile Engagement también admite un tipo especializado de notificación de la aplicación denominada **Sondeos**. Esto le permite toosend los usuarios de aplicación de tooyour segmentada encuestas rápidas. Puede agregar preguntas y opciones para cada pregunta como en la siguiente captura de pantalla de Hola. Esto, a continuación, se muestren como un usuario de aplicación de toohello de notificación en la aplicación.   
  
    ![Notificaciones de sondeo][32]
  
    ![Encuesta sobre Windows][26]
  
    ![Encuesta sobre iOS][27]   ![Encuesta sobre Android][28]

**iOS**, **Android**

* Mobile Engagement también admite el envío de notificaciones de **inserción de datos** silenciosas. Con estas notificaciones, puede enviar datos desde su servicio (por ejemplo, datos JSON de hello en el siguiente ejemplo de Hola), que se pueden controlar en la aplicación y realizar alguna acción. Un ejemplo es cómo estamos cambiando selectivamente precio Hola de un elemento mediante el uso de notificaciones de inserción de datos.
  
    ![Notificación push de datos][33]
  
    ![Notificación push de datos en Windows][23]
  
    ![Notificación push de datos en iOS][24]  ![Notificación push de datos en Android][25]

**iOS**, **Android**

> [!NOTE]
> Encontrará instrucciones detalladas para cualquiera de estas notificaciones, haga clic en **haga clic aquí para obtener instrucciones sobre cómo toosend estas notificaciones de plataforma de Mobile Engagement** en cualquier pantalla de ejemplo de notificación.
> 
> 

[1]: ./media/mobile-engagement-demo-apps/home-windows.png
[2]: ./media/mobile-engagement-demo-apps/home-ios.png
[3]: ./media/mobile-engagement-demo-apps/home-android.png
[4]: ./media/mobile-engagement-demo-apps/menu-windows.png
[5]: ./media/mobile-engagement-demo-apps/menu-ios.png
[6]: ./media/mobile-engagement-demo-apps/menu-android.png
[7]: ./media/mobile-engagement-demo-apps/device-id-windows.png
[8]: ./media/mobile-engagement-demo-apps/device-id-ios.png
[9]: ./media/mobile-engagement-demo-apps/device-id-android.png
[10]: ./media/mobile-engagement-demo-apps/out-of-app-windows.png
[11]: ./media/mobile-engagement-demo-apps/out-of-app-ios.png
[12]: ./media/mobile-engagement-demo-apps/out-of-app-android.png
[13]: ./media/mobile-engagement-demo-apps/out-of-app-display-windows.png
[14]: ./media/mobile-engagement-demo-apps/out-of-app-display-ios.png
[15]: ./media/mobile-engagement-demo-apps/out-of-app-display-android.png
[16]: ./media/mobile-engagement-demo-apps/in-app-windows.png
[17]: ./media/mobile-engagement-demo-apps/in-app-ios.png
[18]: ./media/mobile-engagement-demo-apps/in-app-android.png
[19]: ./media/mobile-engagement-demo-apps/pop-up-ios.png
[20]: ./media/mobile-engagement-demo-apps/pop-up-android.png
[21]: ./media/mobile-engagement-demo-apps/interstitial-ios.png
[22]: ./media/mobile-engagement-demo-apps/interstitial-android.png
[23]: ./media/mobile-engagement-demo-apps/data-push-windows.png
[24]: ./media/mobile-engagement-demo-apps/data-push-ios.png
[25]: ./media/mobile-engagement-demo-apps/data-push-android.png
[26]: ./media/mobile-engagement-demo-apps/survey-windows.png
[27]: ./media/mobile-engagement-demo-apps/survey-ios.png
[28]: ./media/mobile-engagement-demo-apps/survey-android.png
[29]: ./media/mobile-engagement-demo-apps/out-of-app.png
[30]: ./media/mobile-engagement-demo-apps/in-app-interstitial.png
[31]: ./media/mobile-engagement-demo-apps/in-app-pop-up.png
[32]: ./media/mobile-engagement-demo-apps/notification-poll.png
[33]: ./media/mobile-engagement-demo-apps/notification-data-push.png
