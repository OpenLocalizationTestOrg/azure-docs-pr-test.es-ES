---
title: aaaGet Started with Azure Mobile Engagement para Xamarin.Android
description: "Obtenga información acerca de cómo toouse Azure Mobile Engagement con las notificaciones de inserción para las aplicaciones de Xamarin.Android y análisis."
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: fb68cf98-08a2-41b5-8e59-757469de3fe7
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/16/2016
ms.author: piyushjo
ms.openlocfilehash: 9d584fea8e8153d511258cf9b6f87f31dac6aeca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a>Introducción a Azure Mobile Engagement para aplicaciones Xamarin.Android
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Este tema muestra cómo toouse Azure Mobile Engagement toounderstand el uso de la aplicación y cómo toosend insertar los usuarios de toosegmented de notificaciones de una aplicación Xamarin.Android.
Este tutorial muestra el escenario de difusión simple hello con Mobile Engagement. En él, creará una aplicación vacía de Xamarin.Android que recopile datos básicos y reciba notificaciones push con Google Cloud Messaging (GCM).

> [!NOTE]
> servicio de Azure Mobile Engagement Hola se retirará de 2018 de marzo y actualmente solo los clientes de tooexisting disponible. Para más información, consulte [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Este tutorial requiere siguiente de hello:

* [Xamarin Studio](http://xamarin.com/studio). También puede utilizar Visual Studio con Xamarin, pero en este tutorial se usa Xamarin Studio. Consulte [Configuración e instalación](https://msdn.microsoft.com/library/mt613162.aspx)para obtener instrucciones.
* [SDK de Mobile Engagement Xamarin](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> toocomplete este tutorial, debe tener una cuenta activa de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).
> 
> 

## <a id="setup-azme"></a>Configuración de Mobile Engagement para una aplicación Android
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Conectar el back-end de aplicación toohello Mobile Engagement
Este tutorial presenta una "la integración básica", que es Hola mínimo establecido toocollect requiere datos y enviar una notificación de inserción. 

Se creará una aplicación básica con la integración de Xamarin Studio toodemonstrate Hola.

### <a name="create-a-new-xamarinandroid-project"></a>Creación de un nuevo proyecto de Xamarin.Android
1. Iniciar **Xamarin Studio** vaya demasiado**archivo** -> **New** -> **solución** 
   
    ![][1]
2. Seleccione **aplicación Android** , a continuación, compruebe que el idioma de hello seleccionado es **C#** y haga clic en **siguiente**.
   
    ![][2]
3. Rellene hello **nombre de la aplicación** hello y **identificador de la organización**. Asegúrese de que toocheckmark **servicios de Google Play** y, a continuación, haga clic en **siguiente**. 
   
    ![][3]
4. Hola de actualización **nombre del proyecto**, **nombre de la solución** y **ubicación** si es necesario y haga clic en **crear**.
   
    ![][4]

Xamarin Studio creará la aplicación hello en el que se integrará Mobile Engagement. 

### <a name="connect-your-app-toomobile-engagement-backend"></a>Conectar el backend de interacción de tooMobile de aplicación
1. Haga clic en hello **paquetes** carpeta de windows de la solución de Hola y seleccione **agregar paquetes...**
   
    ![][5]
2. Busque hello **Xamarin SDK de Microsoft Azure Mobile Engagement** y agregar soluciones tooyour.  
   
    ![][6]
3. Abra **MainActivity.cs** y agregue Hola siguientes instrucciones using:
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. Hola `OnCreate` método, agregue Hola después de la conexión de hello tooinitialize con Mobile Engagement back-end. Asegúrese de que tooadd su **ConnectionString**. 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a>Agregar permisos y una declaración de servicio
1. Abra hello **Manifest.xml** archivo bajo la carpeta Propiedades de Hola. Seleccione la ficha origen para que actualizar origen XML de hello directamente.
2. Agregar estos toohello permisos Manifest.xml (que se pueden encontrar en hello **propiedades** carpeta) de su proyecto inmediatamente antes o después de hello `<application>` etiqueta:
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. Agregue siguiente Hola entre hello `<application>` y `</application>` etiquetas de servicio del agente de Hola toodeclare:
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. En el código de hello que acaba de pegar, reemplace `"<Your application name>"` en etiqueta Hola. Esto se muestra en hello **configuración** menú donde los usuarios pueden ver los servicios que se ejecutan en el dispositivo de Hola. Por ejemplo puede agregar palabra Hola "Servicio" en esa etiqueta.

### <a name="send-a-screen-toomobile-engagement"></a>Enviar una interacción de pantalla tooMobile
En orden toostart enviando los datos y asegurarse de que los usuarios de hello están activos, debe enviar al menos una pantalla toohello Mobile Engagement back-end. Para hacer esto-Asegúrese de que hello `MainActivity` hereda de `EngagementActivity` en lugar de `Activity`.

    public class MainActivity : EngagementActivity

Como alternativa, si no puede heredar de `EngagementActivity`, deberá agregar los métodos `.StartActivity` y `.EndActivity` en `OnResume` y `OnPause`, respectivamente.  

        protected override void OnResume()
            {
                EngagementAgent.StartActivity(EngagementAgentUtils.BuildEngagementActivityName(Java.Lang.Class.FromType(this.GetType())), null);
                base.OnResume();             
            }

            protected override void OnPause()
            {
                EngagementAgent.EndActivity();
                base.OnPause();            
            }

## <a id="monitor"></a>Conexión de la aplicación con la supervisión en tiempo real
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Habilitación de notificaciones push y mensajería en la aplicación
Mobile Engagement le permite toointeract con y llegar a los usuarios con las notificaciones de inserción y en mensajería desde la aplicación en el contexto de Hola de campañas. Este módulo se denomina alcance en el portal de interacción móvil Hola.
Hola siguientes secciones configura su aplicación tooreceive ellos.

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[1]: ./media/mobile-engagement-xamarin-android-get-started/1.png
[2]: ./media/mobile-engagement-xamarin-android-get-started/2.png
[3]: ./media/mobile-engagement-xamarin-android-get-started/3.png
[4]: ./media/mobile-engagement-xamarin-android-get-started/4.png
[5]: ./media/mobile-engagement-xamarin-android-get-started/5.png
[6]: ./media/mobile-engagement-xamarin-android-get-started/6.png
