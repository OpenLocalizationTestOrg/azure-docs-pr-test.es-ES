---
title: "aaaAzure Mobile Engagement Android integración con el SDK"
description: "Procedimientos y actualizaciones más recientes para el SDK de Android para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a5487793-1a12-4f6c-a1cf-587c5a671e6b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4f79936ea0fa6102023dec2b4682032a4a81fa9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-on-android"></a>¿Cómo tooIntegrate interacción en Android
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

Este procedimiento describe las funciones de la aplicación Android de supervisión y análisis hello más sencilla forma tooactivate Engagement.

> [!IMPORTANT]
> El nivel mínimo de la API del SDK de Android debe ser 10 o superior (Android 2.3.3 o superior).
> 
> 

Hola pasos es que toocompute necesita un suficiente informe de hello tooactivates de los registros de todas las estadísticas relacionadas con los usuarios, sesiones, actividades, se bloquea y Technicals. Hola de registros necesita un informe toocompute otras estadísticas como trabajos, errores y eventos deben realizarse manualmente mediante la API de interacción de Hola (vea [cómo toouse Hola avanzada Mobile Engagement etiquetado API en sus Android](mobile-engagement-android-use-engagement-api.md) desde estos las estadísticas son dependientes de la aplicación.

## <a name="embed-hello-engagement-sdk-and-service-into-your-android-project"></a>No inserte Hola Engagement SDK y el servicio en su proyecto de Android
Descarga Hola SDK de Android de [aquí](https://aka.ms/vq9mfn) obtener `mobile-engagement-VERSION.jar` y colóquelos en hello `libs` carpeta del proyecto de Android (crear carpeta de bibliotecas de hello si aún no existe).

> [!IMPORTANT]
> Si compila el paquete de aplicación con ProGuard, deberá tookeep algunas clases. Puede usar Hola siguiente fragmento de código de configuración:
> 
> -keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
> 
> <methods>; }
> 
> 

Especifique la cadena de conexión de interacción por Hola que realiza la llamada siguiente método en la actividad del iniciador hello:

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

cadena de conexión de Hello para la aplicación se muestra en el Portal de Azure.

* Si no se especifica, agregue los siguientes permisos Android de hello (antes de hello `<application>` etiqueta):
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* Agregar pasos de la sección de hello (entre hello `<application>` y `</application>` etiquetas):
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* Cambio `<Your application name>` por su nombre de saludo de la aplicación.

> [!TIP]
> Hola `android:label` atributo permite toochoose Hola nombre de servicio de contratación de hello tal y como aparecerá toohello los usuarios finales en la pantalla de bienvenida "Ejecutar servicios" de su teléfono. Es recomendable tooset este atributo demasiado`"<Your application name>Service"` (p. ej. `"AcmeFunGameService"`).
> 
> 

Hola especificando `android:process` atributo garantiza que ese servicio de contratación de Hola se ejecutará en su propio proceso (ejecutando interacción Hola mismo proceso cuando la aplicación hará que el subproceso de interfaz de usuario/main potencialmente responde a una menor).

> [!NOTE]
> Cualquier código que se coloque en `Application.onCreate()` y otras devoluciones de llamada de la aplicación se ejecutará para los procesos de todas las de su aplicación, incluido el servicio de contratación de Hola. Puede tener efectos secundarios no deseados (por ejemplo, las asignaciones de memoria innecesario y subprocesos de proceso Hola Engagement, receptores de difusión duplicados o servicios).
> 
> 

Si invalida `Application.onCreate()`, resulta hello tooadd recomendado siguiente fragmento de código al principio de Hola de su `Application.onCreate()` función:

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

Puede hacer lo mismo para Hola `Application.onTerminate()`, `Application.onLowMemory()` y `Application.onConfigurationChanged(...)`.

También puede extender `EngagementApplication` en lugar de extender `Application`: Hola de devolución de llamada `Application.onCreate()` Hola comprobación del proceso y llamadas `Application.onApplicationProcessCreate()` solo si proceso actual de hello es no Hola uno Hola interacción servicio de hospedaje, hello mismas reglas se aplican para Hola otras devoluciones de llamada.

## <a name="basic-reporting"></a>Informes básicos
### <a name="recommended-method-overload-your-activity-classes"></a>Método recomendado: sobrecargar las clases `Activity`
En informe de hello pedido tooactivate de todos los registros de hello requiere interacción toocompute usuarios, sesiones, actividades, bloqueos y las estadísticas técnicas, tiene todos los toomake su `*Activity` subclases heredan de hello correspondiente `Engagement*Activity` clases (por ejemplo, si se extiende la actividad heredada `ListActivity`, asegúrese de extiende `EngagementListActivity`).

**Sin Engagement:**

            package com.company.myapp;

            import android.app.Activity;
            import android.os.Bundle;

            public class MyApp extends Activity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

**Con Engagement:**

            package com.company.myapp;

            import com.microsoft.azure.engagement.activity.EngagementActivity;
            import android.os.Bundle;

            public class MyApp extends EngagementActivity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

> [!IMPORTANT]
> Cuando se usa `EngagementListActivity` o `EngagementExpandableListActivity`, asegúrese de que todas las llamadas demasiado`requestWindowFeature(...);` se realiza antes de la llamada de hello demasiado`super.onCreate(...);`, en caso contrario, se producirá un bloqueo.
> 
> 

Puede encontrar estas clases en hello `src` carpeta y puede copiarlos en el proyecto. clases de Hello también están en hello **JavaDoc**.

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a>Método alternativo: llamar a `startActivity()` y `endActivity()` manualmente
Si no puede o no desea que toooverload su `Activity` clases, en su lugar, puede iniciar y finalizar las actividades mediante una llamada a `EngagementAgent`de métodos directamente.

> [!IMPORTANT]
> Hola SDK de Android nunca llama hello `endActivity()` método, incluso cuando se cierra la aplicación hello (en Android, las aplicaciones no son realmente nunca cerradas). Por lo tanto, es *alta* recomienda hello toocall `startActivity()` método Hola `onResume` devolución de llamada de *todos los* sus actividades y hello `endActivity()` método Hola `onPause()` devolución de llamada de *todos los* sus actividades. Se trata de toobe de manera única de hello seguro de que no se perderá las sesiones. Si una sesión se ha filtrado, Hola servicio interacción nunca se desconectará de backend de interacción de hello (ya que servicio Hola permanece conectado mientras está pendiente una sesión).
> 
> 

Aquí tiene un ejemplo:

            public class MyActivity extends Some3rdPartyActivity
            {
              @Override
              protected void onResume()
              {
                super.onResume();
                String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at hello end.
                EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
              }

              @Override
              protected void onPause()
              {
                super.onPause();
                EngagementAgent.getInstance(this).endActivity();
              }
            }

Este toohello muy similar en el ejemplo se `EngagementActivity` clase y sus variantes, cuyo código fuente se proporciona en hello `src` carpeta.

## <a name="test"></a>Prueba
Ahora compruebe la integración mediante la ejecución su aplicación móvil en un dispositivo o emulador y comprobar que registra una sesión en la pestaña Monitor de Hola.

las secciones siguientes se Hola son opcionales.

## <a name="location-reporting"></a>Informes de ubicación
Si desea toobe ubicaciones notificado, necesita tooadd unas pocas líneas de configuración (entre hello `<application>` y `</application>` etiquetas).

### <a name="lazy-area-location-reporting"></a>Informes de ubicaciones de áreas diferidas
Informes de ubicación de área lenta permiten país de hello tooreport, región y localidad asociado toodevices. Este tipo de informe de ubicación sólo emplea ubicaciones de red (basadas en el identificador del teléfono móvil o en WIFI). área de dispositivo de Hola se notifica como máximo una vez por sesión. Hello GPS nunca se utiliza, y, por tanto, este tipo de informe de ubicación tiene muy pocas (no toosay ningún) impacto en la batería de Hola.

Áreas notificadas son toocompute usado geográfica estadísticas acerca de los usuarios, sesiones, eventos y errores. También se pueden usar como criterios en campañas de cobertura.

ubicación de área lenta tooenable reporting, puede hacerlo mediante la configuración de Hola se mencionó anteriormente en este procedimiento:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

También necesita hello tooadd después permiso si no se especifica:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

O bien, puede seguir usando ``ACCESS_FINE_LOCATION`` si ya lo usa en la aplicación.

### <a name="real-time-location-reporting"></a>Informes de ubicación en tiempo real
Informes de ubicación en tiempo real permiten asociada de latitud y tooreport hello toodevices. De forma predeterminada, este tipo de informes de ubicación sólo usa ubicaciones de red (basadas en el identificador de la celda o Wi-Fi) y reporting Hola solo está activa cuando la aplicación hello se ejecuta en primer plano (es decir, durante una sesión).

Ubicaciones de tiempo real son *no* utiliza las estadísticas de toocompute. Su único propósito es el uso de Hola de tooallow de barrera geográfica en tiempo real \<perímetro de audiencia de Reach\> criterio de campañas.

ubicación en tiempo real de tooenable reporting, puede hacerlo mediante la configuración de Hola se mencionó anteriormente en este procedimiento:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

También necesita hello tooadd después permiso si no se especifica:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

O bien, puede seguir usando ``ACCESS_FINE_LOCATION`` si ya lo usa en la aplicación.

#### <a name="gps-based-reporting"></a>Informes basados en GPS
De forma predeterminada, los informes de ubicación en tiempo real solo emplean ubicaciones de red. uso de hello tooenable de GPS basadas ubicaciones (que son mucho más precisas), use el objeto de configuración de hello:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

También necesita hello tooadd después permiso si no se especifica:

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a>Informes en segundo plano
De forma predeterminada, el informes de ubicación en tiempo real sólo está activa cuando la aplicación hello se ejecuta en primer plano (es decir, durante una sesión). tooenable Hola reporting también en segundo plano, use el objeto de configuración de hello:

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> Cuando la aplicación hello se ejecuta en segundo plano, se notifican únicas ubicaciones a basados en red, incluso si ha habilitado Hola GPS.
> 
> 

informes de ubicación de fondo de Hola se detendrá si el usuario de hello su dispositivo reinicia, puede agregar este toomake reiniciará automáticamente al arrancar el sistema:

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

También necesita hello tooadd después permiso si no se especifica:

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a>Permisos de Android M
A partir de Android M, algunos permisos se administran en tiempo de ejecución y se necesita la aprobación del usuario.

permisos de Hello en tiempo de ejecución se desactivará de forma predeterminada para las nuevas instalaciones de aplicación si el destino es el nivel de API de Android 23. De lo contrario, se activan de forma predeterminada.

usuario de Hello puede habilitar o deshabilitar los permisos desde el menú de configuración del dispositivo de Hola. Al desactivar los permisos en el menú de sistema elimina procesos en segundo plano de la aplicación hello, esto es un comportamiento del sistema y no tiene ningún efecto en la capacidad de inserción de tooreceive en segundo plano.

En el contexto de Hola de Mobile Engagement, permisos de Hola que necesiten la aprobación en tiempo de ejecución son:

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* `WRITE_EXTERNAL_STORAGE` (solo cuando el destino es la API de Android nivel 23)

almacenamiento externo de Hola se usa solo para la característica de panorama general de alcance. Si encuentra pidiendo a los usuarios este toobe permiso potencialmente perjudiciales, se puede quitar si se usa solo para Mobile Engagement, pero al costo de Hola de deshabilitar la característica de imagen grande.

Para las características de la ubicación de hello, debe solicitar toouser permisos mediante un cuadro de diálogo estándar del sistema. Si se aprueba el usuario hello, necesita tootell ``EngagementAgent`` tootake que cambian en cuenta en tiempo real (cambio de hello en caso contrario será procesado Hola siguiente Hola usuario inicia Hola aplicación en tiempo de).

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
         * Request location permission, but this won't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

        /* Only if you want tookeep features using external storage */
        if (checkSelfPermission(android.Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.WRITE_EXTERNAL_STORAGE }, 1);
      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }

## <a name="advanced-reporting"></a>Informes avanzados
Opcionalmente, si desea eventos específicos de aplicación tooreport, errores y trabajos, debe toouse Hola API de interacción a través de métodos de Hola de hello `EngagementAgent` clase. Un objeto de esta clase puede ser recuperó por llamada hello `EngagementAgent.getInstance()` método estático.

permite todas las capacidades avanzadas de contratación toouse Hello API de contratación y se detalla cómo Hola tooUse la API de interacción en Android (así como en la documentación técnica de Hola de hello `EngagementAgent` clase).

## <a name="advanced-configuration-in-androidmanifestxml"></a>Configuración avanzada (en AndroidManifest.xml)
### <a name="wake-locks"></a>Reactivar bloqueos
Si desea toobe seguro de que se envían las estadísticas en tiempo real cuando el uso de Wi-Fi o cuando la pantalla de bienvenida está desactivada, agregar Hola después permiso opcional:

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a>Informe de bloqueos
Si desea que los informes de bloqueo toodisable, agregue esta (entre hello `<application>` y `</application>` etiquetas):

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a>Umbral de ráfaga
De forma predeterminada, los registros de informes del servicio de contratación de hello en tiempo real. Si la aplicación informa de los registros con mucha frecuencia, es mejor toobuffer Hola registros y tooreport usarlas todos a la vez en una base de tiempo regular (Esto se denomina hello "modo de ráfaga"). toodo, por lo tanto, agregue esta (entre hello `<application>` y `</application>` etiquetas):

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

Hello el modo de ráfaga incremente ligeramente batería Hola vida pero tiene un impacto en hello Monitor de contratación: duración de las sesiones y los trabajos de todos los será redondeado toohello ráfaga umbral (por lo tanto, las sesiones y trabajos más cortos que el umbral de ráfaga de hello puede no estar visible). Es recomendable toouse ya no es un umbral de ráfaga de 30000 (30 s).

### <a name="session-timeout"></a>Tiempo de espera de sesión
De forma predeterminada, una sesión es 10s finaliza después del final de Hola de su última actividad (que normalmente se produce al presionar Hola inicio o hacer copia de clave, por teléfono de hello establecer inactivo o saltar a otra aplicación). Se trata de tooavoid una división de sesión cada vez que lo utiliza Hola salir y devolver rápidamente la aplicación de toohello (que puede ocurrir cuando recoge una imagen, comprobar una notificación, etcetera.). Puede que desee toomodify este parámetro. toodo, por lo tanto, agregue esta (entre hello `<application>` y `</application>` etiquetas):

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a>Deshabilitación de los informes de registro
### <a name="using-a-method-call"></a>Mediante una llamada al método
Si desea enviar registros de toostop de interacción, puede llamar:

            EngagementAgent.getInstance(context).setEnabled(false);

Esta llamada es persistente: usa un archivo de preferencias compartido.

Si la interacción está activa cuando se llama a esta función, puede tardar 1 minuto para hello toostop de servicio. Sin embargo no inicie la próxima vez que inicia la aplicación hello servicio hello en hello todos los.

Puede habilitar el registro de reporting nuevo mediante una llamada a Hola la misma función con `true`.

### <a name="integration-in-your-own-preferenceactivity"></a>Integración en su propia `PreferenceActivity`
En lugar de llamar a esta función, también puede integrar este valor directamente en su `PreferenceActivity` existente.

Puede configurar toouse de contratación sus preferencias de archivo (con el modo deseado de hello) de hello `AndroidManifest.xml` de archivos con `application meta-data`:

* Hola `engagement:agent:settings:name` clave es toodefine usado Hola nombre de archivo de preferencias compartidas hello.
* Hola `engagement:agent:settings:mode` clave es modo de hello toodefine utilizado del archivo de preferencias compartidas hello, debe usar hello mismo modo que en su `PreferenceActivity`. modo de saludo se debe pasar como un número: Si usas una combinación de marcas de constantes en el código, compruebe el valor total de Hola.

Interacción siempre usar hello `engagement:key` booleano clave en el archivo de preferencias de Hola para administrar esta configuración.

Hola siguiendo el ejemplo de `AndroidManifest.xml` muestra Hola valores predeterminados:

            <application>
                [...]
                <meta-data
                  android:name="engagement:agent:settings:name"
                  android:value="engagement.agent" />
                <meta-data
                  android:name="engagement:agent:settings:mode"
                  android:value="0" />

A continuación, puede agregar un `CheckBoxPreference` en el diseño de preferencias como Hola sigue uno:

            <CheckBoxPreference
              android:key="engagement:enabled"
              android:defaultValue="true"
              android:title="Use Engagement"
              android:summaryOn="Engagement is enabled."
              android:summaryOff="Engagement is disabled." />

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
