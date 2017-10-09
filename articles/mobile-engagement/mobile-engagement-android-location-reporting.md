---
title: aaaLocation Reporting de Azure Mobile Engagement SDK de Android
description: "Describe cómo ubicación tooconfigure reporting de Azure Mobile Engagement SDK de Android"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6cab5ed1-b767-46ac-9f0b-48a4e249d88c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: c2cb097df2a77bee2d56ffe9509dc116548db408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="location-reporting-for-azure-mobile-engagement-android-sdk"></a>Informes de ubicación para el SDK de Android para Azure Mobile Engagement
> [!div class="op_single_selector"]
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

Este tema se describe cómo ubicación toodo reporting para su aplicación Android.

## <a name="prerequisites"></a>Requisitos previos
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="location-reporting"></a>Informes de ubicación
Si desea toobe ubicaciones notificado, necesita tooadd unas pocas líneas de configuración (entre hello `<application>` y `</application>` etiquetas).

### <a name="lazy-area-location-reporting"></a>Informes de ubicaciones de áreas diferidas
Informes de ubicación de área lenta permiten informes país hello, región y localidad asociados con los dispositivos. Este tipo de informe de ubicación sólo emplea ubicaciones de red (basadas en el identificador del teléfono móvil o en WIFI). área de dispositivo de Hola se notifica como máximo una vez por sesión. Hola GPS nunca se utiliza y, por tanto, este tipo de informe de ubicación tiene poca repercusión en batería Hola.

Áreas notificadas son toocompute usado geográfica estadísticas acerca de los usuarios, sesiones, eventos y errores. También se pueden usar como criterios en campañas de cobertura.

Habilitar ubicación de área lenta informes mediante el uso de la configuración de Hola que se mencionó anteriormente en este procedimiento:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

También deberá toospecify un permiso de ubicación. Este código usa el permiso ``COARSE`` :

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

Si la aplicación lo requiere, puede usar ``ACCESS_FINE_LOCATION`` en su lugar.

### <a name="real-time-location-reporting"></a>Informes de ubicación en tiempo real
Informes de ubicación en tiempo real permiten informes Hola de latitud y longitud asociada a dispositivos. Este tipo de informe de ubicación solo emplea ubicaciones de red basadas en el identificador del teléfono móvil o WiFi. Hola reporting solo está activa cuando la aplicación hello se ejecuta en primer plano (por ejemplo, durante una sesión).

Ubicaciones en tiempo real son *no* utiliza las estadísticas de toocompute. Su único propósito es el uso de Hola de tooallow de geovallado en tiempo real \<perímetro de audiencia de Reach\> criterio de campañas.

ubicación en tiempo real de tooenable informes, agregue una línea de código toowhere establece la cadena de conexión de interacción de hello en actividad del iniciador Hola. resultado de Hello es similar a Hola siguiente:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

        You also need toospecify a location permission. This code uses ``COARSE`` permission:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

        If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.

#### <a name="gps-based-reporting"></a>Informes basados en GPS
De forma predeterminada, los informes de ubicación en tiempo real solo emplean ubicaciones de red. tooenable Hola de GPS-based ubicaciones, que son mucho más precisa, usar el objeto de configuración de hello:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

También necesita hello tooadd después permiso si no se especifica:

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a>Informes en segundo plano
De forma predeterminada, el informes de ubicación en tiempo real sólo está activa cuando la aplicación hello se ejecuta en primer plano (por ejemplo, durante una sesión). Hola tooenable informes también en segundo plano, use este objeto de configuración:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> Cuando la aplicación hello se ejecuta en segundo plano, ubicaciones basadas en red solo se notifican, incluso si ha habilitado Hola GPS.
> 
> 

Si el usuario de Hola que su dispositivo reinicie, informes de ubicación de fondo de Hola se ha detenido. toomake reiniciará automáticamente al arrancar el sistema, agregue este código.

    <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
           android:exported="false">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
        </intent-filter>
    </receiver>

También necesita hello tooadd después permiso si no se especifica:

    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

## <a name="android-m-permissions"></a>Permisos de Android M
A partir de Android M, algunos permisos se administran en tiempo de ejecución y necesitan la aprobación del usuario.

Si su objetivo de nivel de API de Android 23, permisos de hello en tiempo de ejecución están desactivados de forma predeterminada para las nuevas instalaciones de aplicación. De lo contrario, se activan de forma predeterminada.

Puede habilitar o deshabilitar los permisos desde el menú de configuración del dispositivo de Hola. Al desactivar los permisos del menú del sistema Hola elimina procesos en segundo plano Hola de aplicación hello, que es un comportamiento del sistema y no tiene ningún efecto en la capacidad de inserción de tooreceive en segundo plano.

En el contexto de Hola de ubicación de Mobile Engagement reporting, los permisos de Hola que necesiten la aprobación en tiempo de ejecución son:

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`

Solicitar permisos de usuario de hello mediante un cuadro de diálogo estándar del sistema. Indicar si se aprueba el usuario hello, ``EngagementAgent`` tootake que cambian en cuenta en tiempo real. En caso contrario, cambio de hello es procesado Hola siguiente Hola usuario inicia Hola aplicación en tiempo de.

Este es un toouse de ejemplo de código en una actividad de los permisos de aplicación toorequest y el resultado de hello hacia delante, si es positivo demasiado``EngagementAgent``:

    @Override
    public void onCreate(Bundle savedInstanceState)
    {
      /* Other code... */

      /* Request permissions */
      requestPermissions();
    }

    @TargetApi(Build.VERSION_CODES.M)
    private void requestPermissions()
    {
      /* Avoid crashing if not on Android M */
      if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M)
      {
        /*
         * Request location permission, but this doesn't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }
