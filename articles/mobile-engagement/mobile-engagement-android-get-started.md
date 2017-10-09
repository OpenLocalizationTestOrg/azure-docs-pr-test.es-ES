---
title: "aaaGet partió Android aplicaciones de Azure Mobile Engagement"
description: "Obtenga información acerca de cómo toouse Azure Mobile Engagement con las notificaciones de inserción y de análisis para aplicaciones Android."
services: mobile-engagement
documentationcenter: android
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3c286c6d-cfef-4e3e-9b2c-715429fe82db
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e8c92607691104750cdf1c4f7639a041d8a7bcd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-android-apps"></a>Introducción a Azure Mobile Engagement para aplicaciones Android
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Este tema muestra cómo toouse Azure Mobile Engagement toounderstand el uso de la aplicación y cómo toosend insertar los usuarios de toosegmented de notificaciones de una aplicación Android.
Este tutorial muestra el escenario de difusión simple hello con Mobile Engagement. En él, creará una aplicación en blanco de Android que recopila datos básicos y recibe notificaciones de inserción con el Servicio de mensajería en la nube de Google (GCM).

## <a name="prerequisites"></a>Requisitos previos
Completar este tutorial requiere hello [Android Developer Tools](https://developer.android.com/sdk/index.html), que incluye el entorno de desarrollo integrado de Android Studio hello y plataforma de Android más reciente de Hola.

También requiere hello [Android SDK de Mobile Engagement](https://aka.ms/vq9mfn).

> [!IMPORTANT]
> toocomplete este tutorial, necesita una cuenta activa de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).
>
>

## <a name="set-up-mobile-engagement-for-your-android-app"></a>Configuración de Mobile Engagement para una aplicación Android
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="connect-your-app-toohello-mobile-engagement-backend"></a>Conectar el back-end de aplicación toohello Mobile Engagement
Este tutorial presenta una "la integración básica", que es Hola mínimo establecido toocollect requiere datos y enviar una notificación de inserción. Crear una aplicación básica con la integración de Android Studio toodemonstrate Hola.

Encontrará documentación de integración completa de Hola Hola [integración con el SDK de Mobile Engagement Android](mobile-engagement-android-sdk-overview.md).

### <a name="create-an-android-project"></a>Creación de un proyecto de Android
1. Iniciar **Android Studio**y en el menú emergente de hello, seleccione **iniciar un nuevo proyecto de Android Studio**.

    ![][1]
2. Especifique el nombre de la aplicación y el dominio de la compañía. Tome nota de los datos que especifique pues los necesitará más adelante. Haga clic en **Siguiente**.

    ![][2]
3. Seleccione el factor de forma de destino de Hola y el nivel de API y haga clic en **siguiente**.

   > [!NOTE]
   > Compromiso de Mobile requiere el nivel de API mínimo de 10 (2.3.3 Android).
   >
   >

    ![][3]
4. Seleccione **actividad en blanco** aquí, que es la única pantalla de bienvenida para esta aplicación y haga clic en **siguiente**.

    ![][4]
5. Por último, deje los valores predeterminados de hello tal y como está y haga clic en **finalizar**.

    ![][5]

Android Studio ahora crea la aplicación de demostración de hello en el que se integran Mobile Engagement.

### <a name="include-hello-sdk-library-in-your-project"></a>Incluir biblioteca del SDK de hello en el proyecto
1. Descargar hello [Android SDK de Mobile Engagement](https://aka.ms/vq9mfn).
2. Extraer carpeta tooa archivos para archivar faxes hello en el equipo.
3. Identificar Hola .jar biblioteca para la versión actual de Hola de este SDK y cópielo toohello Portapapeles.

      ![][6]
4. Navegue toohello **proyecto** sección (1) y pegue .jar hello en la carpeta de bibliotecas de hello (2).

      ![][7]
5. biblioteca de hello tooload, proyecto de Hola la sincronización.

      ![][8]

### <a name="connect-your-app-toomobile-engagement-backend-with-hello-connection-string"></a>Conectar el back-end de aplicación tooMobile interacción con hello cadena de conexión
1. Copie Hola siguientes líneas de código en la creación de la actividad de hello (debe realizarse solo en un lugar de la aplicación, normalmente actividad principal de hello). Para esta aplicación de ejemplo, abra hello MainActivity en src -> main -> carpeta de java y agregue Hola siguientes:

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
        EngagementAgent.getInstance(this).init(engagementConfiguration);
2. Resolver las referencias de hello presionando Alt + ENTRAR o agregando Hola siguiendo las instrucciones de importación:

        import com.microsoft.azure.engagement.EngagementAgent;
        import com.microsoft.azure.engagement.EngagementConfiguration;
3. Volver atrás toohello Portal de Azure clásico en la aplicación **información de conexión** Hola de página y copiar **cadena de conexión**.

      ![][9]
4. Pegue en hello `setConnectionString` parámetro, reemplazando la cadena completa de Hola se muestra en el siguiente código de hello:

        engagementConfiguration.setConnectionString("Endpoint=my-company-name.device.mobileengagement.windows.net;SdkKey=********************;AppId=*********");

### <a name="add-permissions-and-a-service-declaration"></a>Agregar permisos y una declaración de servicio
1. Agregar estos toohello permisos Manifest.xml del proyecto inmediatamente antes o después de hello `<application>` etiqueta:

        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
2. toodeclare Hola servicio del agente, agregue este código entre hello `<application>` y `</application>` etiquetas:

        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
3. En el código de hello que pegó, reemplace `"<Your application name>"` en etiqueta de hello, que se muestra en hello **configuración** menú donde puede ver los servicios que se ejecutan en el dispositivo de Hola. Por ejemplo puede agregar palabra Hola "Servicio" en esa etiqueta.

### <a name="send-a-screen-toomobile-engagement"></a>Enviar una interacción de pantalla tooMobile
toostart enviar datos y asegurarse de que los usuarios de hello están activos, debe enviar al menos un backend de interacción móvil toohello de pantalla (actividad).

Vaya demasiado**MainActivity.java** y agregue Hola después de la clase base de hello tooreplace de **MainActivity** demasiado**EngagementActivity**:

    public class MainActivity extends EngagementActivity {

> [!NOTE]
> Si la clase base no es *actividad*, consulte [avanzada Reporting Android](mobile-engagement-android-advanced-reporting.md) para saber cómo tooinherit partir de clases diferentes.
>
>

Comente Hola después de línea para este escenario de ejemplo simple:

    // setSupportActionBar(toolbar);

Si desea que hello tookeep `ActionBar` en la aplicación, consulte [avanzada Reporting Android](mobile-engagement-android-advanced-reporting.md).

## <a name="connect-app-with-real-time-monitoring"></a>Conectar la aplicación con la supervisión en tiempo real
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a name="enable-push-notifications-and-in-app-messaging"></a>Habilitación de las notificaciones push y la mensajería en aplicación
Durante una campaña, Mobile Engagement permite interactuar y llegar por REACH a los usuarios mediante notificaciones push y mensajería en la aplicación. Este módulo se denomina alcance en el portal de interacción móvil Hola.
Hola pasos de la sección configura su aplicación tooreceive ellos.

### <a name="copy-sdk-resources-in-your-project"></a>Copia de recursos SDK en el proyecto
1. Navegue Hola de contenido y copia de la descarga SDK tooyour back- **res** carpeta.

    ![][10]
2. Volver atrás tooAndroid Studio, seleccione hello **principal** directorio de los archivos de proyecto y, a continuación, péguelo recursos tooyour project de tooadd Hola.

    ![][11]

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

## <a name="next-steps"></a>Pasos siguientes
Vaya demasiado[SDK de Android](mobile-engagement-android-sdk-overview.md) tooget un conocimiento acerca de la integración con el SDK de hello detallado.

<!-- Images. -->
[1]: ./media/mobile-engagement-android-get-started/android-studio-new-project.png
[2]: ./media/mobile-engagement-android-get-started/android-studio-project-props.png
[3]: ./media/mobile-engagement-android-get-started/android-studio-project-props2.png
[4]: ./media/mobile-engagement-android-get-started/android-studio-add-activity.png
[5]: ./media/mobile-engagement-android-get-started/android-studio-activity-name.png
[6]: ./media/mobile-engagement-android-get-started/sdk-content.png
[7]: ./media/mobile-engagement-android-get-started/paste-jar.png
[8]: ./media/mobile-engagement-android-get-started/sync-project.png
[9]: ./media/mobile-engagement-android-get-started/app-connection-info-page.png
[10]: ./media/mobile-engagement-android-get-started/copy-resources.png
[11]: ./media/mobile-engagement-android-get-started/paste-resources.png
