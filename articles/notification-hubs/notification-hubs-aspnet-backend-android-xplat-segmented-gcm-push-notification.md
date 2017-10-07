---
title: Tutorial de noticias importantes de concentradores - aaaNotification de Android
description: "Obtenga información acerca de cómo toouse centros de notificaciones de Bus de servicio de Azure toosend principales de dispositivos de tooAndroid de notificaciones de noticias."
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 3c23cb80-9d35-4dde-b26d-a7bfd4cb8f81
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: e6eb41bec95c67d7dc059f560194966d04400494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a>Usar toosend centros de notificaciones noticias de última hora
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Información general
Este tema muestra cómo toouse centros de notificaciones de Azure toobroadcast importantes noticias notificaciones tooan aplicación Android. Cuando haya finalizado, se puede tooregister puede romper la categorías de noticias que le interesen y recibir notificaciones de inserción solo para esas categorías. Este escenario es un patrón común para muchas aplicaciones donde las notificaciones tienen toogroups toobe enviado de los usuarios que previamente se han declarado el interés en ellos, por ejemplo, aplicaciones de ventiladores de música, etcetera, lector RSS.

Escenarios de difusión se habilitan mediante la inclusión de uno o varios *etiquetas* al crear un registro en el centro de notificaciones de Hola. Cuando se envían las notificaciones tooa etiqueta, todos los dispositivos que se han registrado para la etiqueta de hello recibirá notificación de Hola. Dado que las etiquetas son simplemente cadenas, no tiene toobe aprovisionado de antemano. Para obtener más información acerca de las etiquetas, consulte demasiado[notificación centros de enrutamiento y expresiones de etiqueta](notification-hubs-tags-segment-push-message.md).

## <a name="prerequisites"></a>Requisitos previos
En este tema se basa en la aplicación hello que creó en [empezar a trabajar con los centros de notificaciones][get-started]. Antes de comenzar este tutorial, debe haber completado la [Introducción a Notification Hubs][get-started].

## <a name="add-category-selection-toohello-app"></a>Agregar categoría selección toohello aplicación
Hola primer paso es tooadd Hola UI elementos tooyour principal actividad existente que permiten Hola usuario tooselect categorías tooregister. categorías de Hello seleccionadas por el usuario se almacenan en el dispositivo de Hola. Cuando se inicia la aplicación hello, se crea un registro de dispositivos en el centro de notificaciones con las categorías de hello seleccionado como etiquetas.

1. Abra el archivo res/layout/activity_main.xml y sustituya el contenido de hello con siguiente hello:
   
        <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
            xmlns:tools="http://schemas.android.com/tools"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:paddingBottom="@dimen/activity_vertical_margin"
            android:paddingLeft="@dimen/activity_horizontal_margin"
            android:paddingRight="@dimen/activity_horizontal_margin"
            android:paddingTop="@dimen/activity_vertical_margin"
            tools:context="com.example.breakingnews.MainActivity"
            android:orientation="vertical">
   
                <CheckBox
                    android:id="@+id/worldBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_world" />
                <CheckBox
                    android:id="@+id/politicsBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_politics" />
                <CheckBox
                    android:id="@+id/businessBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_business" />
                <CheckBox
                    android:id="@+id/technologyBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_technology" />
                <CheckBox
                    android:id="@+id/scienceBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_science" />
                <CheckBox
                    android:id="@+id/sportsBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_sports" />
                <Button
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:onClick="subscribe"
                    android:text="@string/button_subscribe" />
        </LinearLayout>
2. Abra el archivo res/values/strings.xml y agregue Hola siguientes líneas:
   
        <string name="button_subscribe">Subscribe</string>
        <string name="label_world">World</string>
        <string name="label_politics">Politics</string>
        <string name="label_business">Business</string>
        <string name="label_technology">Technology</string>
        <string name="label_science">Science</string>
        <string name="label_sports">Sports</string>
   
    El diseño gráfico main_activity.xml ahora debe tener un aspecto similar a este:
   
    ![][A1]
3. Ahora cree una clase **notificaciones** en hello en el mismo paquete como su **MainActivity** clase.
   
        import java.util.HashSet;
        import java.util.Set;
   
        import android.content.Context;
        import android.content.SharedPreferences;
        import android.os.AsyncTask;
        import android.util.Log;
        import android.widget.Toast;
   
        import com.google.android.gms.gcm.GoogleCloudMessaging;
        import com.microsoft.windowsazure.messaging.NotificationHub;
   
        public class Notifications {
            private static final String PREFS_NAME = "BreakingNewsCategories";
            private GoogleCloudMessaging gcm;
            private NotificationHub hub;
            private Context context;
            private String senderId;
   
            public Notifications(Context context, String senderId, String hubName, 
                                    String listenConnectionString) {
                this.context = context;
                this.senderId = senderId;
   
                gcm = GoogleCloudMessaging.getInstance(context);
                hub = new NotificationHub(hubName, listenConnectionString, context);
            }
   
            public void storeCategoriesAndSubscribe(Set<String> categories)
            {
                SharedPreferences settings = context.getSharedPreferences(PREFS_NAME, 0);
                settings.edit().putStringSet("categories", categories).commit();
                subscribeToCategories(categories);
            }
   
            public Set<String> retrieveCategories() {
                SharedPreferences settings = context.getSharedPreferences(PREFS_NAME, 0);
                return settings.getStringSet("categories", new HashSet<String>());
            }
   
            public void subscribeToCategories(final Set<String> categories) {
                new AsyncTask<Object, Object, Object>() {
                    @Override
                    protected Object doInBackground(Object... params) {
                        try {
                            String regid = gcm.register(senderId);
   
                            String templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";
   
                            hub.registerTemplate(regid,"simpleGCMTemplate", templateBodyGCM, 
                                categories.toArray(new String[categories.size()]));
                        } catch (Exception e) {
                            Log.e("MainActivity", "Failed tooregister - " + e.getMessage());
                            return e;
                        }
                        return null;
                    }
   
                    protected void onPostExecute(Object result) {
                        String message = "Subscribed for categories: "
                                + categories.toString();
                        Toast.makeText(context, message,
                                Toast.LENGTH_LONG).show();
                    }
                }.execute(null, null, null);
            }
   
        }
   
    Esta clase usa categorías de hello almacenamiento local toostore Hola de noticias que este dispositivo tiene tooreceive. También contiene métodos tooregister para estas categorías.
4. En la clase **MainActivity**, elimine los campos privados para **NotificationHub** y **GoogleCloudMessaging** y agregue un campo para **Notifications**:
   
        // private GoogleCloudMessaging gcm;
        // private NotificationHub hub;
        private Notifications notifications;
5. A continuación, en hello **onCreate** método remove Hola inicialización de hello **concentrador** hello y campo **registerWithNotificationHubs** método. A continuación, agregue Hola siguiendo las líneas que inicializar una instancia de hello **notificaciones** clase. 

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            MyHandler.mainActivity = this;

            NotificationsManager.handleNotifications(this, SENDER_ID,
                    MyHandler.class);

            notifications = new Notifications(this, SENDER_ID, HubName, HubListenConnectionString);

            notifications.subscribeToCategories(notifications.retrieveCategories());
        }

    `HubName`y `HubListenConnectionString` ya debería estar configurado con hello `<hub name>` y `<connection string with listen access>` marcadores de posición con la notificación concentrador hello y nombre de cadena de conexión para *DefaultListenSharedAccessSignature* obtenido versiones anteriores.

    > [AZURE.NOTE] Dado que las credenciales que se distribuyen con una aplicación cliente no son generalmente seguras, debe distribuir solo clave hello para el acceso de escucha con la aplicación cliente. Escuchar habilita el acceso que no se puede modificar su tooregister de aplicación para notificaciones, pero los registros existentes y no se enviarán las notificaciones. clave de acceso completa de Hola se usa en un servicio seguro back-end para enviar notificaciones y cambiar los registros existentes.


1. A continuación, agregue Hola siguiendo importa y `subscribe` Hola de toohandle método suscribirse botón click (evento):
   
        import android.widget.CheckBox;
        import java.util.HashSet;
        import java.util.Set;
   
        public void subscribe(View sender) {
            final Set<String> categories = new HashSet<String>();
   
            CheckBox world = (CheckBox) findViewById(R.id.worldBox);
            if (world.isChecked())
                categories.add("world");
            CheckBox politics = (CheckBox) findViewById(R.id.politicsBox);
            if (politics.isChecked())
                categories.add("politics");
            CheckBox business = (CheckBox) findViewById(R.id.businessBox);
            if (business.isChecked())
                categories.add("business");
            CheckBox technology = (CheckBox) findViewById(R.id.technologyBox);
            if (technology.isChecked())
                categories.add("technology");
            CheckBox science = (CheckBox) findViewById(R.id.scienceBox);
            if (science.isChecked())
                categories.add("science");
            CheckBox sports = (CheckBox) findViewById(R.id.sportsBox);
            if (sports.isChecked())
                categories.add("sports");
   
            notifications.storeCategoriesAndSubscribe(categories);
        }
   
    Este método crea una lista de categorías y se utiliza hello **notificaciones** clase toostore lista de hello en el almacenamiento local de Hola y registrar las etiquetas correspondientes Hola con el centro de notificaciones. Cuando se cambian las categorías, se vuelve a crear el registro de hello con nuevas categorías de Hola.

La aplicación ahora es capaz de toostore un conjunto de categorías en el almacenamiento local en el dispositivo de Hola y registrar con el centro de notificaciones de hello siempre que los cambios de usuarios Hola Hola selección de categorías.

## <a name="register-for-notifications"></a>Registro de notificaciones
Estos pasos se registran con el centro de notificaciones de Hola durante el inicio con las categorías de Hola que han sido almacenados en el almacenamiento local.

> [!NOTE]
> Dado que identificador hello asignado por Google (GCM Cloud Messaging) puede cambiar en cualquier momento, se deben registrar para notificaciones con frecuencia tooavoid errores de notificación. En este ejemplo se registra para la notificación cada vez que inicia la aplicación hello. Para las aplicaciones que se ejecutan con frecuencia, más de una vez al día, puede probablemente Omitir ancho de banda de registro toopreserve si ha pasado menos de un día desde el registro de hello anterior.
> 
> 

1. Agregar Hola siguiente código al final de Hola de hello **onCreate** método Hola **MainActivity** clase:
   
        notifications.subscribeToCategories(notifications.retrieveCategories());
   
    Esto garantiza que cada vez que inicia la aplicación hello recupera categorías Hola desde el almacenamiento local y solicita un registro para estas categorías. 
2. A continuación, actualice hello `onStart()` método de hello `MainActivity` clase como sigue:
   
    @Override protected void onStart() {
   
        super.onStart();
        isVisible = true;
   
        Set<String> categories = notifications.retrieveCategories();
   
        CheckBox world = (CheckBox) findViewById(R.id.worldBox);
        world.setChecked(categories.contains("world"));
        CheckBox politics = (CheckBox) findViewById(R.id.politicsBox);
        politics.setChecked(categories.contains("politics"));
        CheckBox business = (CheckBox) findViewById(R.id.businessBox);
        business.setChecked(categories.contains("business"));
        CheckBox technology = (CheckBox) findViewById(R.id.technologyBox);
        technology.setChecked(categories.contains("technology"));
        CheckBox science = (CheckBox) findViewById(R.id.scienceBox);
        science.setChecked(categories.contains("science"));
        CheckBox sports = (CheckBox) findViewById(R.id.sportsBox);
        sports.setChecked(categories.contains("sports"));
    }
   
    Esto actualiza la actividad principal de hello basada en estado de Hola de categorías guardadas anteriormente.

aplicación Hello ahora está completa y puede almacenar un conjunto de categorías en hello dispositivo almacenamiento local usa tooregister con el centro de notificaciones de hello siempre que los cambios de usuarios Hola Hola selección de categorías. A continuación, definimos un back-end que puede enviar la aplicación de toothis de notificaciones de categoría.

## <a name="sending-tagged-notifications"></a>Envío de notificaciones con etiquetas
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a>Ejecutar aplicación hello y generar notificaciones
1. En Android Studio, compile la aplicación hello e inícielo en un dispositivo o emulador.
   
    Tenga en cuenta que interfaz de usuario proporciona un conjunto de la aplicación hello alterna que le permite elegir Hola categorías toosubscribe a.
2. Habilite uno o más elementos de alternancia de las categorías y, a continuación, haga clic en **Suscribirse**.
   
    aplicación Hello convierte categorías Hola seleccionado en las etiquetas y solicita un nuevo registro de dispositivo para etiquetas de hello seleccionada del centro de notificaciones de Hola. Hello categorías registrados se devuelve y se muestran en una notificación del sistema.
3. Enviar una notificación de nuevo mediante la ejecución de la aplicación de consola .NET de hello.  Como alternativa, puede enviar notificaciones de plantilla etiquetadas con ficha de depuración de Hola de su centro de notificaciones de hello [Portal clásico de Azure].
   
    Las notificaciones para las categorías de hello seleccionado aparecen como notificaciones del sistema.

## <a name="next-steps"></a>Pasos siguientes
En este tutorial hemos visto cómo toobroadcast noticias de última hora por categoría. Considere la posibilidad de completar uno de hello tutoriales que indican errores de otros escenarios avanzados de centros de notificaciones:

* [Utilice noticias de última hora de toobroadcast localizado de los centros de notificaciones]
  
    Obtenga información acerca de cómo hello tooexpand interrumpir el envío de noticias aplicación tooenable localizar las notificaciones.

<!-- Images. -->
[A1]: ./media/notification-hubs-aspnet-backend-android-breaking-news/android-breaking-news1.PNG

<!-- URLs.-->
[get-started]: notification-hubs-android-push-notification-google-gcm-get-started.md
[Utilice noticias de última hora de toobroadcast localizado de los centros de notificaciones]: /manage/services/notification-hubs/breaking-news-localized-dotnet/
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Portal clásico de Azure]: https://manage.windowsazure.com
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
