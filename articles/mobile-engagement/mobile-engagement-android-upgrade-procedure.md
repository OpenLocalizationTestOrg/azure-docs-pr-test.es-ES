---
title: "aaaAzure Mobile Engagement Android integración con el SDK"
description: "Procedimientos y actualizaciones más recientes para el SDK de Android para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 11618586-c709-49ca-bcd8-745323ff1af6
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: df5c82812fe0a242eaa5df8c906030237215b7eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-procedures"></a>Procedimientos de actualización
Si ya ha integrado una versión anterior de nuestro SDK en la aplicación, tener hello tooconsider siguientes puntos al actualizar Hola SDK.

Puede tener toofollow varios procedimientos si ejecutado varias versiones de hello SDK. Por ejemplo, si migra desde 1.4.0 too1.6.0 tiene toofirst siga Hola "de 1.4.0 too1.5.0" procedimiento, a continuación, Hola "de 1.5.0 too1.6.0" procedimiento.

Cualquier versión de Hola se actualiza desde, tiene hello tooreplace `mobile-engagement-VERSION.jar` con hello uno nuevo.

## <a name="from-420-too421"></a>Desde 4.2.0 too4.2.1
Este paso puede realizarse realmente en cualquier versión de Hola SDK, es una mejora de seguridad al integrar las actividades de alcance.

Ahora debe agregar `exported="false"` tooall alcance actividades.

Las actividades de cobertura deben ser ahora similares a esta en `AndroidManifest.xml`:

            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>
            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/html" />
              </intent-filter>
            </activity>
            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT" />
              </intent-filter>
            </activity>
            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
                <category android:name="android.intent.category.DEFAULT"/>
              </intent-filter>
            </activity>

## <a name="from-400-too410"></a>Desde 4.0.0 too4.1.0
Hola SDK ahora identificador nuevo modelo de permisos de M Android.

Si usa las características de ubicación o notificaciones de panorama general, lea [esta sección](mobile-engagement-android-integrate-engagement.md#android-m-permissions).

Además toohello al nuevo modelo de permisos, ahora se admite la configuración de características de ubicación en tiempo de ejecución.
Estamos siga siendo compatibles con parámetros para la ubicación del manifiesto de hello pero ahora está en desuso. las secciones siguientes de hello remove de configuración de en tiempo de ejecución de toouse, desde su ``AndroidManifest.xml``:

    <meta-data
      android:name="engagement:locationReport:lazyArea"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:background"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:fine"
      android:value="true"/>

y leer [Esto actualiza procedimiento](mobile-engagement-android-integrate-engagement.md#location-reporting) toouse configuración de tiempo de ejecución en su lugar.

## <a name="from-300-too400"></a>Desde 3.0.0 too4.0.0
### <a name="native-push"></a>Inserción nativa
Inserción nativa (GCM/ADM) ahora también se utiliza para las notificaciones en aplicación por lo que debe configurar credenciales de inserción nativa de Hola para cualquier tipo de campaña de inserción.

Si aún no lo hizo, siga [este procedimiento](mobile-engagement-android-integrate-engagement-reach.md#native-push).

### <a name="androidmanifestxml"></a>AndroidManifest.xml
Se modificó la integración de Reach en ``AndroidManifest.xml``.

Reemplazar esto:

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
      <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
        <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
      </intent-filter>
    </receiver>

Por

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
      <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
      </intent-filter>
    </receiver>
    <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
      <intent-filter>
        <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
      </intent-filter>
    </receiver>

Posiblemente, ahora hay una pantalla de carga al hacer clic en un anuncio (con texto y contenido web) o una encuesta.
Tienes tooadd esto para esos toowork campañas en 4.0.0:

    <activity
      android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity"
      android:theme="@android:style/Theme.Dialog">
      <intent-filter>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
        <category android:name="android.intent.category.DEFAULT"/>
      </intent-filter>
    </activity>

### <a name="resources"></a>Recursos
Incrustar Hola nueva `res/layout/engagement_loading.xml` archivo en el proyecto.

## <a name="from-240-too300"></a>De 2.4.0 too3.0.0
Hello siguiente describe cómo toomigrate una integración con el SDK de hello Capptain servicio ofrecido por Capptain SAS en una aplicación con la tecnología de Azure Mobile Engagement. Si va a migrar desde una versión anterior, consulte hello Capptain sitio web toomigrate too2.4.0 en primer lugar y, a continuación, aplicar Hola siguiendo el procedimiento.

> [!IMPORTANT]
> Capptain e interacción móvil son no Hola mismos servicios y Hola procedimiento que se indica a continuación solo destaca cómo toomigrate Hola aplicación cliente. Migrar Hola SDK en la aplicación hello no migrará los datos de hello Capptain toohello Mobile Engagement servidores.
> 
> 

### <a name="jar-file"></a>Archivo JAR
Sustituya `capptain.jar` por `mobile-engagement-VERSION.jar` en su carpeta `libs`.

### <a name="resource-files"></a>Archivos de recursos
Cada archivo de recursos que se proporciona (precedida por `capptain_`) se toobe reemplazado por hello nuevos (con el prefijo `engagement_`).

Si ha personalizado los archivos, tendrá que toore-aplicar la personalización en nuevos archivos de hello, **todos los identificadores de Hola Hola en archivos de recursos también ha cambiado el nombre**.

### <a name="application-id"></a>Identificador de aplicación
Ahora interacción usa un identificadores de conexión cadena tooconfigure Hola SDK como identificador de la aplicación hello.

Tiene toouse `EngagementAgent.init` método en la actividad del iniciador similar al siguiente:

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

cadena de conexión de Hello para la aplicación se muestra en el Portal de Azure.

Elimine cualquier llamada`CapptainAgent.configure` como `EngagementAgent.init` reemplaza a ese método.

Hola `appId` ya no se puede configurar mediante `AndroidManifest.xml`.

Quite esta sección de su `AndroidManifest.xml` si la tiene:

            <meta-data android:name="capptain:appId" android:value="<YOUR_APPID>"/>

### <a name="java-api"></a>API de Java
Cada clase de Java de nuestro SDK de llamada tooany tiene toobe cambiar el nombre; Por ejemplo, `CapptainAgent.getInstance(this)` debe cambiarse `EngagementAgent.getInstance(this)`, `extends CapptainActivity` debe cambiarse `extends EngagementActivity` etcetera...

Si se integra con los archivos de preferencias de agente de forma predeterminada, nombre de archivo predeterminado de hello es ahora `engagement.agent` y clave de hello es `engagement:agent`.

Al crear anuncios web, Hola Javascript enlazador es ahora `engagementReachContent`.

### <a name="androidmanifestxml"></a>AndroidManifest.xml
Ha ocurrido un lote de cambios, ya no se comparte el servicio de hello y una gran cantidad de destinatarios ya no son exportables.

declaración de servicio de Hello ahora es más sencillo; Quitar filtro de intención de Hola y todos los metadatos dentro de él y agregar `exportable=false`.

Además de todo lo que es la contratación de toouse cuyo nombre ha cambiado.

Ahora se parece a esto:

            <service
              android:name="com.microsoft.azure.engagement.service.EngagementService"
              android:exported="false"
              android:label="<Your application name>Service"
              android:process=":Engagement"/>

Cuando desee que los registros de pruebas tooenable, Hola metadatos ahora ha sido movido toohello etiqueta de la aplicación y se ha cambiado el nombre:

            <application>

              <meta-data android:name="engagement:log:test" android:value="true" />

              <service/>

            </application>

Todos los demás datos meta simplemente ha cambiado el nombre, esta es la lista completa de hello (evidentemente rename solo Hola que usas):

            <meta-data
              android:name="engagement:reportCrash"
              android:value="true"/>
            <meta-data
              android:name="engagement:sessionTimeout"
              android:value="10000"/>
            <meta-data
              android:name="engagement:burstThreshold"
              android:value="0"/>
            <meta-data
              android:name="engagement:connection:delay"
              android:value="0"/>
            <meta-data
              android:name="engagement:locationReport:lazyArea"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:background"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:fine"
              android:value="false"/>
            <meta-data
              android:name="engagement:agent:settings:name"
              android:value="engagement.agent"/>
            <meta-data
              android:name="engagement:agent:settings:mode"
              android:value="0"/>
            <meta-data
              android:name="engagement:gcm:sender"
              android:value="<YOUR_PROJECT_NUMBER>\n"/>
            <meta-data
              android:name="engagement:adm:register"
              android:value="true"/>
            <meta-data
              android:name="engagement:reach:notification:icon"
              android:value="<DRAWABLE_NAME_WITHOUT_EXTENSION>"/>

            <activity android:name="SomeActivityWithoutReachOverlay">
              <meta-data
                android:name="engagement:notification:overlay"
                android:value="false"/>
            </activity>

Seguimiento de Google Play y SmartAd se ha quitado del SDK sólo tiene tooremove esto sin reemplazo:

            <meta-data 
                android:name="capptain:track:installReferrerForwardList"
                android:value="com.class1,com.class2"/>
            <meta-data
                android:name="capptain:track:adservers"
                android:value="smartad" />

las actividades de cobertura de Hola se declaran ahora similar al siguiente:

            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/plain"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/html"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT"/>
              </intent-filter>
            </activity>

Si tiene actividades personalizadas de alcance, necesita ya sea solo toochange Hola acciones intención toomatch `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` o `com.microsoft.azure.engagement.reach.intent.action.POLL`.

Hello difusión receptores han cambiado de nombre, además de agregamos ahora `exported=false`. Esta es Hola lista completa de destinatarios de hello con nueva especificación de hello, (evidentemente rename solo Hola que usas):

            <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
              android:exported="false">
              <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
                <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver"
              android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION"/>
                <action android:name="com.google.android.c2dm.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
              android:permission="com.amazon.device.messaging.permission.SEND">
              <intent-filter>
                <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
                <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementConnectionReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.CONNECTED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.DISCONNECTED"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementMessageReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.MESSAGE"/>
              </intent-filter>
            </receiver>

Se ha quitado la seguimiento receptor, por lo que tendrá tooremove en esta sección:

          <receiver android:name="com.ubikod.capptain.android.sdk.track.CapptainTrackReceiver">
            <intent-filter>
              <action android:name="com.ubikod.capptain.intent.action.APPID_GOT" />
              <!-- possibly <action android:name="com.android.vending.INSTALL_REFERRER" /> -->
            </intent-filter>
          </receiver>

Tenga en cuenta que la declaración de Hola de su implementación de hello difusión receptor **EngagementMessageReceiver** ha cambiado en hello `AndroidManifest.xml`. Esto es porque Hola API toosend y quite XMPP arbitrario mensajes desde entidades XMPP arbitrarias y Hola API toosend y recibir mensajes entre los dispositivos se han quitado. Por lo tanto, también tiene hello toodelete siguiendo las devoluciones de llamada desde el **EngagementMessageReceiver** implementación:

            protected void onDeviceMessageReceived(android.content.Context context, java.lang.String deviceId, java.lang.String payload)

y

            protected void onXMPPMessageReceived(android.content.Context context, android.os.Bundle message)

luego elimine toda llamada en **EngagementAgent** para:

            sendMessageToDevice(java.lang.String deviceId, java.lang.String payload, java.lang.String packageName)

y

            sendXMPPMessage(android.os.Bundle msg)

### <a name="proguard"></a>Proguard
Configuración proguard puede verse afectado por la reconfiguración de marca, Hola ahora se parecido a las reglas:

            -dontwarn android.**
            -keep class android.support.v4.** { *; }

            -keep public class * extends android.os.IInterface
            -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
              <methods>;
            }

