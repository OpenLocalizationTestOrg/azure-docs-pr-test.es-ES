---
title: "aaaAzure Mobile Engagement Android integración con el SDK"
description: "Procedimientos y actualizaciones más recientes para el SDK de Android para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ec3fab3-35ec-458e-bf41-6cdd69e3fa44
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 06/27/2016
ms.author: piyushjo
ms.openlocfilehash: 4ab6143771bdc0758a548abb529d6bde98fc0e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-android"></a>Cómo tooIntegrate interacción a en Android
> [!IMPORTANT]
> Debe seguir el procedimiento de integración de hello descrito en hello cómo documentar tooIntegrate interacción en Android antes de seguir a esta guía.
> 
> 

## <a name="standard-integration"></a>Integración estándar

Copie los archivos de recursos de alcance de hello SDK en el proyecto:

* Copie los archivos de Hola de hello `res/layout` carpeta ofrece Hola SDK en hello `res/layout` carpeta de la aplicación.
* Copie los archivos de Hola de hello `res/drawable` carpeta ofrece Hola SDK en hello `res/drawable` carpeta de la aplicación.

Edite su archivo `AndroidManifest.xml`:

* Agregar pasos de la sección de hello (entre hello `<application>` y `</application>` etiquetas):
  
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
          <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver" android:exported="false">
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
* Notificaciones de tooreplay sistema este permiso que no se ha hecho clic en el arranque (en caso contrario, se conservará en el disco pero no se mostrarán ya, tiene en realidad tooinclude esto).
  
          <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
* Especificar un icono que se usa para notificaciones (tanto en la aplicación y del sistema), copiando y editando los pasos de la sección de hello (entre hello `<application>` y `</application>` etiquetas):
  
          <meta-data android:name="engagement:reach:notification:icon" android:value="<name_of_icon_WITHOUT_file_extension_and_WITHOUT_'@drawable/'>" />

> [!IMPORTANT]
> Esta sección es **obligatoria** si planifica utilizar notificaciones del sistema al crear campañas de cobertura. Android impide que se muestren las notificaciones del sistema sin iconos. Por lo que si se omite en esta sección, los usuarios finales no será capaz de tooreceive ellos.
> 
> 

* Si creas las campañas con notificaciones del sistema con la idea global, necesita hello tooadd los siguientes permisos (después de hello `</application>` etiqueta) si no se especifica:
  
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
          <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
  
  * En Android M y si la aplicación está destinada al nivel de API Android 23 o superior, el permiso ``WRITE_EXTERNAL_STORAGE`` requiere la aprobación del usuario. Lea [esta sección](mobile-engagement-android-integrate-engagement.md#android-m-permissions).
* Para las notificaciones del sistema que también puede especificar en hello alcancen campaña si dispositivo Hola debe sonar o Vibrar. Para toowork, tendrá que declaran Hola después permiso toomake (después de hello `</application>` etiqueta):
  
          <uses-permission android:name="android.permission.VIBRATE" />
  
  Sin este permiso, Android, impide que las notificaciones del sistema que no se muestre si ha seleccionado anillo de Hola o hello Vibrar opción en el Administrador de campaña alcanzar Hola.

## <a name="native-push"></a>Inserción nativa:
Ahora que ha configurado el módulo de Reach, debe tooconfigure nativo toobe tooreceive capaz de hello las campañas de inserción en el dispositivo de Hola.

Se admiten dos servicios en Android:

* Dispositivos de Google Play: Use [Google Cloud Messaging] por hello siguiente [cómo guía tooIntegrate GCM con interacción](mobile-engagement-android-gcm-integrate.md) guía.
* Dispositivos de Amazon: Use [Amazon Device Messaging] por hello siguiente [cómo guía tooIntegrate ADM con interacción](mobile-engagement-android-adm-integrate.md) guía.

Si desea que tootarget dispositivos de Amazon y Google Play, su posibles toohave todos los datos 1 AndroidManifest.xml/APK para el desarrollo. Pero, al enviar tooAmazon, puede rechazar la aplicación si encuentra el código de GCM.

En ese caso, debe usar varios APK.

**La aplicación está ahora listo tooreceive y presentación alcanzan las campañas!**

## <a name="how-toohandle-data-push"></a>Cómo inserción datos toohandle
### <a name="integration"></a>Integración
Si desea que su aplicación toobe pueda inserta tooreceive datos de cobertura, tendrá que toocreate una subclase de `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` y hacer referencia a él en hello `AndroidManifest.xml` archivo (entre hello `<application>` o `</application>` etiquetas):

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

A continuación, puede invalidar hello `onDataPushStringReceived` y `onDataPushBase64Received` las devoluciones de llamada. Aquí tiene un ejemplo:

            public class MyDataPushReceiver extends EngagementReachDataPushReceiver
            {
              @Override
              protected Boolean onDataPushStringReceived(Context context, String category, String body)
              {
                Log.d("tmp", "String data push message received: " + body);
                return true;
              }

              @Override
              protected Boolean onDataPushBase64Received(Context context, String category, byte[] decodedBody, String encodedBody)
              {
                Log.d("tmp", "Base64 data push message received: " + encodedBody);
                // Do something useful with decodedBody like updating an image view
                return true;
              }
            }

### <a name="category"></a>Categoría
parámetro de categoría de Hello es opcional cuando se crea una campaña de inserción de datos y permite que los datos de toofilter inserta. Esto es útil si tiene varios receptores difusión de administración de los diferentes tipos de inserciones de datos, o si desea toopush diferentes tipos de `Base64` tooidentify de datos y quiere que su tipo antes del análisis de ellos.

### <a name="callbacks-return-parameter"></a>Parámetro de devolución de devoluciones de llamada
Estas son algunas directrices tooproperly identificador hello parámetro devuelto de `onDataPushStringReceived` y `onDataPushBase64Received`:

* Debe devolver un receptor de difusión `null` de devolución de llamada de hello si no sabe cómo insertar toohandle datos. Debe usar Hola categoría toodetermine si el receptor difusión debe controlar la inserción de datos de Hola o no.
* Uno de hello difusión receptor debe devolver `true` en devolución de llamada de hello si acepta la inserción de datos de Hola.
* Uno de hello difusión receptor debe devolver `false` en devolución de llamada de hello si se reconoce la inserción de datos de hello, pero descarta por cualquier motivo. Por ejemplo, devolver `false` cuando Hola recibido datos no son válidos.
* Si una difusión receptor devuelve `true` mientras otro uno devuelve `false` para hello misma inserción de datos, el comportamiento de hello no está definido, nunca debe hacerlo.

tipo de valor devuelto de Hola se usa solo para las estadísticas de cobertura de hello:

* `Replied`se incrementa si uno de los receptores de difusión de hello devuelve cualquiera `true` o `false`.
* `Actioned`se incrementa sólo si uno de hello difusión receptores devueltos `true`.

## <a name="how-toocustomize-campaigns"></a>Cómo las campañas de toocustomize
las campañas de toocustomize, puede modificar diseños de hello proporcionados Hola Reach SDK.

Debe mantener todos los identificadores de hello usados en los diseños de Hola y mantener Hola tipos de vistas de Hola que utiliza un identificador, especialmente para las vistas de texto y las vistas de la imagen. Algunas vistas son solo usa toohide o muestran las áreas, por lo que se puede cambiar su tipo. Compruebe código fuente de hello si piensa toochange tipo de saludo de una vista en los diseños de hello proporcionado.

### <a name="notifications"></a>Notificaciones
Existen dos tipos de notificaciones: notificaciones del sistema y notificaciones en aplicación, las que usan distintos archivos de diseño.

#### <a name="system-notifications"></a>Notificaciones del sistema
notificaciones del sistema toocustomize necesita hello toouse **categorías**. También puede avanzar demasiado[categorías](#categories).

#### <a name="in-app-notifications"></a>Notificación en aplicación
De forma predeterminada, una notificación en la aplicación es una vista que es toohello agregados dinámicamente actual actividad usuario gracias toohello Android método de interfaz `addContentView()`. Esto se denomina superposición de notificaciones. Superposiciones de notificación son excelentes para una integración rápida porque no requieren toomodify cualquier diseño de la aplicación.

visión de hello toomodify de sus superposiciones de notificación, simplemente puede modificar archivo hello `engagement_notification_area.xml` tooyour necesita.

> [!NOTE]
> archivo hello `engagement_notification_overlay.xml` es uno que sea utilizado toocreate Hola una superposición de notificación, incluye el archivo hello `engagement_notification_area.xml`. También se puede personalizar toosuit sus necesidades (por ejemplo, para colocar el área de notificación de hello en superposición de hello).
> 
> 

##### <a name="include-notification-layout-as-part-of-an-activity-layout"></a>Incluya el diseño de la notificación como parte de un diseño de actividad
Las superposiciones son ideales para lograr una integración rápida, pero puede ser poco conveniente o tener efectos secundarios en casos especiales. sistema de superposición de Hello puede personalizarse en un nivel de actividad, lo que efectos secundarios de tooprevent fácil para actividades especiales.

Puede decidir tooinclude nuestro diseño de notificación en la toohello gracias de diseño existente Android **incluyen** instrucción. Hello aquí te mostramos un ejemplo de una modificación `ListActivity` diseño que simplemente contienen un `ListView`.

**Antes de la integración de Engagement :**

            <?xml version="1.0" encoding="utf-8"?>
            <ListView
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@android:id/list"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" />

**Después de la integración de Engagement :**

            <?xml version="1.0" encoding="utf-8"?>
            <LinearLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="vertical"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <ListView
                android:id="@android:id/list"
                android:layout_width="fill_parent"
                android:layout_height="fill_parent"
                android:layout_weight="1" />

              <include layout="@layout/engagement_notification_area" />

            </LinearLayout>

En este ejemplo se agrega un contenedor primario porque diseño original de hello usando una vista de lista como elemento de nivel superior de Hola. También hemos agregado `android:layout_weight="1"` toobe capaz tooadd una vista por debajo de una vista de lista configurado con `android:layout_height="fill_parent"`.

Hola interacción Reach SDK detecta automáticamente ese diseño de notificación de Hola se incluye en esta actividad y no agregará una superposición para esta actividad.

> [!TIP]
> Si usas un ListActivity en la aplicación, una superposición de cobertura visible no podrá reaccionando elementos tooclicked en la vista de lista de hello ya. Este es un problema conocido. toowork solucionar este problema se recomienda tooembed diseño de notificación de hello en su propio diseño de la actividad de lista como en el ejemplo anterior de Hola.
> 
> 

##### <a name="disabling-application-notification-per-activity"></a>Deshabilitación de notificación de aplicación por actividad
Si no desea hello toobe de superposición agrega tooyour actividad y, si no incluye el diseño de la notificación de hello en un diseño propio, puede deshabilitar la superposición de Hola para esta actividad en hello `AndroidManifest.xml` agregando un `meta-data` sección, como en los siguientes Hola ejemplo:

            <activity android:name="SplashScreenActivity">
              <meta-data android:name="engagement:notification:overlay" android:value="false"/>
            </activity>

#### <a name="categories"></a> Categorías
Cuando se modifica Hola proporcionada diseños, modificar aspecto de Hola de todas las notificaciones. Las categorías permiten toodefine que distintos destino busca (posiblemente comportamientos) para las notificaciones. Las categorías pueden especificarse cuando se crea una campaña de cobertura. Tenga en cuenta que las categorías también permiten personalizar anuncios y sondeos, aspectos que se describen más adelante en este documento.

tooregister un controlador de categoría para las notificaciones, debe tooadd una llamada cuando se inicializa la aplicación hello.

> [!IMPORTANT]
> Lea la advertencia Hola sobre el atributo de android: proceso de hello \<android-sdk-en proceso de contratación\> Hola cómo tooIntegrate interacción en tema Android antes de continuar.
> 
> 

Hello en el ejemplo siguiente se supone que reconoce la advertencia anterior hello y utilice una subclase de `EngagementApplication`:

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), "myCategory");
              }
            }

Hola `MyNotifier` objeto es la implementación de Hola de controlador de categoría de notificación de Hola. Es cualquier implementación de hello `EngagementNotifier` interfaz o una subclase de la implementación predeterminada de hello: `EngagementDefaultNotifier`.

Tenga en cuenta que Hola notificador mismo puede controlar varias categorías, puede registrar similar al siguiente:

            reachAgent.registerNotifier(new MyNotifier(this), "myCategory", "myAnotherCategory");

implementación de categoría de tooreplace Hola predeterminada, puede registrar su implementación como en el siguiente ejemplo de Hola:

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), Intent.CATEGORY_DEFAULT); // "android.intent.category.DEFAULT"
              }
            }

categoría de Hello actual utilizada en un controlador se pasa como un parámetro en la mayoría de los métodos se pueden reemplazar en `EngagementDefaultNotifier`.

Se transmite como un parámetro `String` o de manera indirecta en un objeto `EngagementReachContent` que tiene un método `getCategory()`.

Puede cambiar la mayor parte del proceso de creación de notificación de hello mediante la redefinición de métodos en `EngagementDefaultNotifier`, para una personalización más avanzada sentirse tootake libre un vistazo en la documentación técnica de Hola y en código fuente de Hola.

##### <a name="in-app-notifications"></a>Notificación en aplicación
Si solo desea diseños alternativos de toouse para una categoría específica, puede hacerlo como en el siguiente ejemplo de Hola:

            public class MyNotifier extends EngagementDefaultNotifier
            {
              public MyNotifier(Context context)
              {
                super(context);
              }

              @Override
              protected int getOverlayLayoutId(String category)
              {
                return R.layout.my_notification_overlay;
              }


              @Override
              public Integer getOverlayViewId(String category)
              {
                return R.id.my_notification_overlay;
              }

              @Override
              public Integer getInAppAreaId(String category)
              {
                return R.id.my_notification_area;
              }
            }

**Ejemplo de `my_notification_overlay.xml` :**

            <?xml version="1.0" encoding="utf-8"?>
            <RelativeLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@+id/my_notification_overlay"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <include layout="@layout/my_notification_area" />

            </RelativeLayout>

Como puede ver, identificador de la vista de hello superposición es diferente de estándar de hello uno. Es importante que cada diseño utilice un identificador único para las superposiciones.

**Ejemplo de `my_notification_area.xml` :**

            <?xml version="1.0" encoding="utf-8"?>
            <merge
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <RelativeLayout
                android:id="@+id/my_notification_area"
                android:layout_width="fill_parent"
                android:layout_height="64dp"
                android:layout_alignParentTop="true"
                android:background="#B000">

                <LinearLayout
                  android:orientation="horizontal"
                  android:layout_width="fill_parent"
                  android:layout_height="fill_parent"
                  android:gravity="center_vertical">

                  <ImageView
                    android:id="@+id/engagement_notification_icon"
                    android:layout_width="48dp"
                    android:layout_height="48dp" />

                  <LinearLayout
                    android:id="@+id/engagement_notification_text"
                    android:orientation="vertical"
                    android:layout_width="fill_parent"
                    android:layout_height="fill_parent"
                    android:layout_weight="1"
                    android:gravity="center_vertical">

                    <TextView
                      android:id="@+id/engagement_notification_title"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:singleLine="true"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Medium" />

                    <TextView
                      android:id="@+id/engagement_notification_message"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:maxLines="2"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Small" />

                  </LinearLayout>

                  <ImageView
                    android:id="@+id/engagement_notification_image"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:adjustViewBounds="true" />

                  <ImageButton
                    android:id="@+id/engagement_notification_close_area"
                    android:visibility="invisible"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:src="@android:drawable/btn_dialog"
                    android:background="#0F00" />

                </LinearLayout>

                <ImageButton
                  android:id="@+id/engagement_notification_close"
                  android:layout_width="wrap_content"
                  android:layout_height="fill_parent"
                  android:layout_alignParentRight="true"
                  android:src="@android:drawable/btn_dialog"
                  android:background="#0F00" />

              </RelativeLayout>

            </merge>

Como puede ver, identificador de la vista de área de notificación de hello es diferente de estándar de hello uno. Es importante que cada diseño utilice un identificador único para las áreas de notificación.

Este sencillo ejemplo de categoría hace que las notificaciones de aplicación (o en la aplicación) aparece en la parte superior de Hola de pantalla de bienvenida. No se cambió identificadores estándar Hola usados en el área de notificación de hello propio.

Si desea que toochange que, tener hello tooredefine `EngagementDefaultNotifier.prepareInAppArea` método. Se recomienda toolook en la documentación técnica de Hola y en código fuente de Hola de `EngagementNotifier` y `EngagementDefaultNotifier` si desea que este nivel de personalización avanzada.

##### <a name="system-notifications"></a>Notificaciones del sistema
Extendiendo `EngagementDefaultNotifier`, puede invalidar `onNotificationPrepared` notificación de hello tooalter que se preparó implementación predeterminada de Hola.

Por ejemplo:

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content)
              throws RuntimeException
            {
              if ("ongoing".equals(content.getCategory()))
                notification.flags |= Notification.FLAG_ONGOING_EVENT;
              return true;
            }

En este ejemplo realiza una notificación del sistema para un contenido que se muestra como un evento en curso cuando se utiliza la categoría "en curso" Hola.

Si desea que hello toobuild `Notification` objeto desde el principio, puede devolver `false` toohello método y llame al método `notify` usted mismo en hello `NotificationManager`. En ese caso es importante que mantenga un `contentIntent`, `deleteIntent` y Hola utilizado por el identificador de notificación `EngagementReachReceiver`.

El siguiente es un ejemplo de una implementación de ese tipo correcta:

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content) throws RuntimeException
            {
              /* Required fields */
              NotificationCompat.Builder builder = new NotificationCompat.Builder(mContext)
                .setSmallIcon(notification.icon)              // icon is mandatory
                .setContentIntent(notification.contentIntent) // keep content intent
                .setDeleteIntent(notification.deleteIntent);  // keep delete intent

              /* Your customization */
              // builder.set...

              /* Dismiss option can be managed only after build */
              Notification myNotification = builder.build();
              if (!content.isNotificationCloseable())
                myNotification.flags |= Notification.FLAG_NO_CLEAR;

              /* Notify here instead of super class */
              NotificationManager manager = (NotificationManager) mContext.getSystemService(Context.NOTIFICATION_SERVICE);
              manager.notify(getNotificationId(content), myNotification); // notice hello call tooget hello right identifier

              /* Return false, we notify ourselves */
              return false;
            }

##### <a name="notification-only-announcements"></a>Anuncios solo de notificación
Hello administración de hello haga clic en una anuncio solo puede personalizarse mediante la invalidación de notificación `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` hello toomodify preparado `Intent`. Con este método permite marcas de hello tootune fácilmente.

Por ejemplo tooadd hello `SINGLE_TOP` marca:

            @Override
            protected Intent onNotifAnnouncementIntentPrepared(EngagementNotifAnnouncement notifAnnouncement,
              Intent intent)
            {
              intent.addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
              return intent;
            }

Para los usuarios de contratación heredados, tenga en cuenta que las notificaciones del sistema sin ninguna acción dirección URL ahora se inicia aplicación hello si estaba en segundo plano, por lo que puede llamar a este método con un anuncio sin dirección URL de acción. Debe considerar al personalizar la intención de Hola.

También puede implementar `EngagementNotifier.executeNotifAnnouncementAction` desde cero.

##### <a name="notification-life-cycle"></a>Ciclo de vida de notificación
Cuando se usa la categoría predeterminada de hello, se llaman a algunos métodos de ciclo de vida en hello `EngagementReachInteractiveContent` tooreport estadísticas y actualización Hola campaña el estado del objeto:

* Cuando se muestra en la aplicación o colocar en la barra de estado de hello notificación de hello, Hola `displayNotification` se llama al método (que notifica estadísticas) por `EngagementReachAgent` si `handleNotification` devuelve `true`.
* Si se descarta la notificación de hello, Hola `exitNotification` método se llama, se notifica la estadística y ahora se pueden procesar las campañas siguientes.
* Si se hace clic en la notificación de hello, `actionNotification` es llama, se notifican estadísticas y se inicia el intento de hello asociado.

Si la implementación de `EngagementNotifier` omisiones Hola comportamiento predeterminado, tendrá toocall estos métodos de ciclo de vida por usted mismo. Hello en los ejemplos siguientes muestra algunos casos donde se omite el comportamiento predeterminado de hello:

* No se extienden `EngagementDefaultNotifier`, por ejemplo, se implementa el control de categoría desde cero.
* Para las notificaciones del sistema, reemplazó hello `onNotificationPrepared` y modificado `contentIntent` o `deleteIntent` en hello `Notification` objeto.
* Para las notificaciones de la aplicación, reemplazó `prepareInAppArea`, ser al menos seguro toomap `actionNotification` tooone de los controles de I.U.

> [!NOTE]
> Si `handleNotification` inicia una excepción, Hola contenido se elimina y `dropContent` se llama. Esto se informa en las estadísticas y ahora es posible procesar las siguientes campañas.
> 
> 

### <a name="announcements-and-polls"></a>Anuncios y sondeos
#### <a name="layouts"></a>Diseños
Puede modificar hello `engagement_text_announcement.xml`, `engagement_web_announcement.xml` y `engagement_poll.xml` archivos toocustomize anuncios de texto, sondeos y anuncios de web.

Estos archivos comparten dos diseños comunes para el área de título de Hola y área del botón Hola. diseño de Hola de título de hello es `engagement_content_title.xml` y utiliza Hola epónimo archivos con estas características para el fondo de Hola. Hello diseño de botones de acción y salir de hello es `engagement_button_bar.xml` y utiliza Hola epónimo archivos con estas características para el fondo de Hola.

En un sondeo, Hola diseño pregunta y sus opciones son exagerar dinámicamente mediante varias veces hello `engagement_question.xml` archivo de diseño para resolver dudas de Hola y Hola `engagement_choice.xml` archivo de opciones de Hola.

#### <a name="categories"></a>Categorías
##### <a name="alternate-layouts"></a>Diseños alternativos
Al igual que las notificaciones, categoría de la campaña de hello puede ser toohave usado diseños alternativos para los sondeos y anuncios.

Por ejemplo, toocreate una categoría de un anuncio de texto, puede ampliar `EngagementTextAnnouncementActivity` y hacer referencia a él hello `AndroidManifest.xml` archivo:

            <activity android:name="com.your_company.MyCustomTextAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>

Tenga en cuenta esa categoría de hello en el intento de Hola se utiliza el filtro de diferencia de hello toomake con actividad de anuncio de Hola predeterminada.

Hola Reach SDK usa actividad derecho de hello sistema intención tooresolve Hola para una categoría específica y recurre en la categoría de hello predeterminado si no se pudo resolver Hola.

Tendrá que tooimplement `MyCustomTextAnnouncementActivity`, si simplemente desea toochange Hola diseño (pero mantener Hola mismos identificadores de vista), solo tienen clase de hello toodefine como en el siguiente ejemplo de Hola:

            public class MyCustomTextAnnouncementActivity extends EngagementTextAnnouncementActivity
            {
              @Override
              protected String getLayoutName()
              {
                return "my_text_announcement";  // tell super class toouse R.layout.my_text_announcement
              }
            }

categoría de tooreplace Hola predeterminada de los anuncios de texto, reemplace simplemente `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` por su implementación.

Los anuncios web y los sondeos se pueden personalizar de manera similar.

Para anuncios web también puede extender `EngagementWebAnnouncementActivity` y declarar su actividad en hello `AndroidManifest.xml` al igual que en el siguiente ejemplo de Hola:

            <activity android:name="com.your_company.MyCustomWebAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/html" />    <!-- only difference with text announcements in hello intent is hello data mime type -->
              </intent-filter>
            </activity>

Para los sondeos puede ampliar `EngagementPollActivity` y declarar su hello en `AndroidManifest.xml` como en el siguiente ejemplo de Hola:

            <activity android:name="com.your_company.MyCustomPollActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="my_category" />
              </intent-filter>
            </activity>

##### <a name="implementation-from-scratch"></a>Implementación desde cero
Puede implementar categorías de tus actividades de anuncio (y sondeo) sin tener que ampliar uno de hello `Engagement*Activity` las clases proporcionadas por Hola Reach SDK. Esto es útil por ejemplo si desea toodefine un diseño que no usa Hola mismo vistas como diseños estándar Hola.

Al igual que para la personalización avanzada de notificación, se recomienda toolook en el código fuente de Hola de implementación estándar de Hola.

Estas son algunas cosas tookeep en mente: alcance iniciará actividad hello con un propósito específico (filtro intención de correspondiente toohello) junto con un parámetro adicional que es el identificador de contenido de Hola.

tooretrieve Hola objeto de contenido que contienen campos de Hola que especificó al crear Hola de campaña en el sitio web de Hola puede hacer esto:

            public class MyCustomTextAnnouncement extends EngagementActivity
            {
              private EngagementAnnouncement mContent;

              @Override
              protected void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);

                /* Get content */
                mContent = EngagementReachAgent.getInstance(this).getContent(getIntent());
                if (mContent == null)
                {
                  /* If problem with content, exit */
                  finish();
                  return;
                }

                setContentView(R.layout.my_text_announcement);

                /* Configure views by querying fields on mContent */
                // ...
              }
            }

Para las estadísticas, debería notificar es mostrar el contenido de Hola Hola `onResume` eventos:

            @Override
            protected void onResume()
            {
             /* Mark hello content displayed */
             mContent.displayContent(this);
             super.onResume();
            }

A continuación, no olvide toocall o `actionContent(this)` o `exitContent(this)` en el objeto de contenido de hello antes de actividad hello entra en segundo plano.

Si no llama a `actionContent` o `exitContent`, no se envían las estadísticas (es decir, ningún análisis en campaña Hola) y más importante aún, Hola campañas siguientes no será informadas hasta que se reinicie el proceso de la aplicación hello.

Orientación u otros cambios de configuración puede realizar Hola código difícil toodetermine si actividad hello entra en segundo plano o no, Hola hace de implementación estándar seguro contenido Hola se notifica como salido si usuario Hola deja actividad hello (ya sea mediante la al presionar `HOME` o `BACK`) pero no si cambia la orientación de Hola.

Aquí es parte interesante de Hola de implementación de hello:

            @Override
            protected void onUserLeaveHint()
            {
              finish();
            }

            @Override
            protected void onPause()
            {
              if (isFinishing() && mContent != null)
              {
                /*
                 * Exit content on exit, this is has no effect if another process method has already been
                 * called so we don't have toocheck anything here.
                 */
                mContent.exitContent(this);
              }
              super.onPause();
            }

Como puede ver, si llama a `actionContent(this)` , a continuación, finaliza la actividad de hello, `exitContent(this)` puede llamar de forma segura sin tener ningún efecto.

[here]:http://developer.android.com/tools/extras/support-library.html#Downloading
[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html
[Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html
