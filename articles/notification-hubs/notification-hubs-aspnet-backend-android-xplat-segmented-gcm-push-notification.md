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
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="9cc1b-103">Usar toosend centros de notificaciones noticias de última hora</span><span class="sxs-lookup"><span data-stu-id="9cc1b-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="9cc1b-104">Información general</span><span class="sxs-lookup"><span data-stu-id="9cc1b-104">Overview</span></span>
<span data-ttu-id="9cc1b-105">Este tema muestra cómo toouse centros de notificaciones de Azure toobroadcast importantes noticias notificaciones tooan aplicación Android.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooan Android app.</span></span> <span data-ttu-id="9cc1b-106">Cuando haya finalizado, se puede tooregister puede romper la categorías de noticias que le interesen y recibir notificaciones de inserción solo para esas categorías.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-106">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="9cc1b-107">Este escenario es un patrón común para muchas aplicaciones donde las notificaciones tienen toogroups toobe enviado de los usuarios que previamente se han declarado el interés en ellos, por ejemplo, aplicaciones de ventiladores de música, etcetera, lector RSS.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-107">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="9cc1b-108">Escenarios de difusión se habilitan mediante la inclusión de uno o varios *etiquetas* al crear un registro en el centro de notificaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="9cc1b-109">Cuando se envían las notificaciones tooa etiqueta, todos los dispositivos que se han registrado para la etiqueta de hello recibirá notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-109">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="9cc1b-110">Dado que las etiquetas son simplemente cadenas, no tiene toobe aprovisionado de antemano.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-110">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="9cc1b-111">Para obtener más información acerca de las etiquetas, consulte demasiado[notificación centros de enrutamiento y expresiones de etiqueta](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="9cc1b-111">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9cc1b-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9cc1b-112">Prerequisites</span></span>
<span data-ttu-id="9cc1b-113">En este tema se basa en la aplicación hello que creó en [empezar a trabajar con los centros de notificaciones][get-started].</span><span class="sxs-lookup"><span data-stu-id="9cc1b-113">This topic builds on hello app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="9cc1b-114">Antes de comenzar este tutorial, debe haber completado la [Introducción a Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="9cc1b-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="9cc1b-115">Agregar categoría selección toohello aplicación</span><span class="sxs-lookup"><span data-stu-id="9cc1b-115">Add category selection toohello app</span></span>
<span data-ttu-id="9cc1b-116">Hola primer paso es tooadd Hola UI elementos tooyour principal actividad existente que permiten Hola usuario tooselect categorías tooregister.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-116">hello first step is tooadd hello UI elements tooyour existing main activity that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="9cc1b-117">categorías de Hello seleccionadas por el usuario se almacenan en el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-117">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="9cc1b-118">Cuando se inicia la aplicación hello, se crea un registro de dispositivos en el centro de notificaciones con las categorías de hello seleccionado como etiquetas.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-118">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="9cc1b-119">Abra el archivo res/layout/activity_main.xml y sustituya el contenido de hello con siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="9cc1b-119">Open your res/layout/activity_main.xml file, and substitute hello content with hello following:</span></span>
   
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
2. <span data-ttu-id="9cc1b-120">Abra el archivo res/values/strings.xml y agregue Hola siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="9cc1b-120">Open your res/values/strings.xml file and add hello following lines:</span></span>
   
        <string name="button_subscribe">Subscribe</string>
        <string name="label_world">World</string>
        <string name="label_politics">Politics</string>
        <string name="label_business">Business</string>
        <string name="label_technology">Technology</string>
        <string name="label_science">Science</string>
        <string name="label_sports">Sports</string>
   
    <span data-ttu-id="9cc1b-121">El diseño gráfico main_activity.xml ahora debe tener un aspecto similar a este:</span><span class="sxs-lookup"><span data-stu-id="9cc1b-121">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
3. <span data-ttu-id="9cc1b-122">Ahora cree una clase **notificaciones** en hello en el mismo paquete como su **MainActivity** clase.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-122">Now create a class **Notifications** in hello same package as your **MainActivity** class.</span></span>
   
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
   
    <span data-ttu-id="9cc1b-123">Esta clase usa categorías de hello almacenamiento local toostore Hola de noticias que este dispositivo tiene tooreceive.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-123">This class uses hello local storage toostore hello categories of news that this device has tooreceive.</span></span> <span data-ttu-id="9cc1b-124">También contiene métodos tooregister para estas categorías.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-124">It also contains methods tooregister for these categories.</span></span>
4. <span data-ttu-id="9cc1b-125">En la clase **MainActivity**, elimine los campos privados para **NotificationHub** y **GoogleCloudMessaging** y agregue un campo para **Notifications**:</span><span class="sxs-lookup"><span data-stu-id="9cc1b-125">In your **MainActivity** class remove your private fields for **NotificationHub** and **GoogleCloudMessaging**, and add a field for **Notifications**:</span></span>
   
        // private GoogleCloudMessaging gcm;
        // private NotificationHub hub;
        private Notifications notifications;
5. <span data-ttu-id="9cc1b-126">A continuación, en hello **onCreate** método remove Hola inicialización de hello **concentrador** hello y campo **registerWithNotificationHubs** método.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-126">Then, in hello **onCreate** method, remove hello initialization of hello **hub** field and hello **registerWithNotificationHubs** method.</span></span> <span data-ttu-id="9cc1b-127">A continuación, agregue Hola siguiendo las líneas que inicializar una instancia de hello **notificaciones** clase.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-127">Then add hello following lines which initialize an instance of hello **Notifications** class.</span></span> 

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            MyHandler.mainActivity = this;

            NotificationsManager.handleNotifications(this, SENDER_ID,
                    MyHandler.class);

            notifications = new Notifications(this, SENDER_ID, HubName, HubListenConnectionString);

            notifications.subscribeToCategories(notifications.retrieveCategories());
        }

    <span data-ttu-id="9cc1b-128">`HubName`y `HubListenConnectionString` ya debería estar configurado con hello `<hub name>` y `<connection string with listen access>` marcadores de posición con la notificación concentrador hello y nombre de cadena de conexión para *DefaultListenSharedAccessSignature* obtenido versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-128">`HubName` and `HubListenConnectionString` should already be set with hello `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>

    > [AZURE.NOTE] <span data-ttu-id="9cc1b-129">Dado que las credenciales que se distribuyen con una aplicación cliente no son generalmente seguras, debe distribuir solo clave hello para el acceso de escucha con la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-129">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="9cc1b-130">Escuchar habilita el acceso que no se puede modificar su tooregister de aplicación para notificaciones, pero los registros existentes y no se enviarán las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-130">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="9cc1b-131">clave de acceso completa de Hola se usa en un servicio seguro back-end para enviar notificaciones y cambiar los registros existentes.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-131">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>


1. <span data-ttu-id="9cc1b-132">A continuación, agregue Hola siguiendo importa y `subscribe` Hola de toohandle método suscribirse botón click (evento):</span><span class="sxs-lookup"><span data-stu-id="9cc1b-132">Then, add hello following imports and `subscribe` method toohandle hello subscribe button click event:</span></span>
   
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
   
    <span data-ttu-id="9cc1b-133">Este método crea una lista de categorías y se utiliza hello **notificaciones** clase toostore lista de hello en el almacenamiento local de Hola y registrar las etiquetas correspondientes Hola con el centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-133">This method creates a list of categories and uses hello **Notifications** class toostore hello list in hello local storage and register hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="9cc1b-134">Cuando se cambian las categorías, se vuelve a crear el registro de hello con nuevas categorías de Hola.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-134">When categories are changed, hello registration is recreated with hello new categories.</span></span>

<span data-ttu-id="9cc1b-135">La aplicación ahora es capaz de toostore un conjunto de categorías en el almacenamiento local en el dispositivo de Hola y registrar con el centro de notificaciones de hello siempre que los cambios de usuarios Hola Hola selección de categorías.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-135">Your app is now able toostore a set of categories in local storage on hello device and register with hello notification hub whenever hello user changes hello selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="9cc1b-136">Registro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="9cc1b-136">Register for notifications</span></span>
<span data-ttu-id="9cc1b-137">Estos pasos se registran con el centro de notificaciones de Hola durante el inicio con las categorías de Hola que han sido almacenados en el almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-137">These steps register with hello notification hub on startup using hello categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="9cc1b-138">Dado que identificador hello asignado por Google (GCM Cloud Messaging) puede cambiar en cualquier momento, se deben registrar para notificaciones con frecuencia tooavoid errores de notificación.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-138">Because hello registrationId assigned by Google Cloud Messaging (GCM) can change at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="9cc1b-139">En este ejemplo se registra para la notificación cada vez que inicia la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-139">This example registers for notification every time that hello app starts.</span></span> <span data-ttu-id="9cc1b-140">Para las aplicaciones que se ejecutan con frecuencia, más de una vez al día, puede probablemente Omitir ancho de banda de registro toopreserve si ha pasado menos de un día desde el registro de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-140">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
> 
> 

1. <span data-ttu-id="9cc1b-141">Agregar Hola siguiente código al final de Hola de hello **onCreate** método Hola **MainActivity** clase:</span><span class="sxs-lookup"><span data-stu-id="9cc1b-141">Add hello following code at hello end of hello **onCreate** method in hello **MainActivity** class:</span></span>
   
        notifications.subscribeToCategories(notifications.retrieveCategories());
   
    <span data-ttu-id="9cc1b-142">Esto garantiza que cada vez que inicia la aplicación hello recupera categorías Hola desde el almacenamiento local y solicita un registro para estas categorías.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-142">This makes sure that every time hello app starts it retrieves hello categories from local storage and requests a registeration for these categories.</span></span> 
2. <span data-ttu-id="9cc1b-143">A continuación, actualice hello `onStart()` método de hello `MainActivity` clase como sigue:</span><span class="sxs-lookup"><span data-stu-id="9cc1b-143">Then update hello `onStart()` method of hello `MainActivity` class as follows:</span></span>
   
    <span data-ttu-id="9cc1b-144">@Override protected void onStart() {</span><span class="sxs-lookup"><span data-stu-id="9cc1b-144">@Override  protected void onStart() {</span></span>
   
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
    <span data-ttu-id="9cc1b-145">}</span><span class="sxs-lookup"><span data-stu-id="9cc1b-145">}</span></span>
   
    <span data-ttu-id="9cc1b-146">Esto actualiza la actividad principal de hello basada en estado de Hola de categorías guardadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-146">This updates hello main activity based on hello status of previously saved categories.</span></span>

<span data-ttu-id="9cc1b-147">aplicación Hello ahora está completa y puede almacenar un conjunto de categorías en hello dispositivo almacenamiento local usa tooregister con el centro de notificaciones de hello siempre que los cambios de usuarios Hola Hola selección de categorías.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-147">hello app is now complete and can store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello user changes hello selection of categories.</span></span> <span data-ttu-id="9cc1b-148">A continuación, definimos un back-end que puede enviar la aplicación de toothis de notificaciones de categoría.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-148">Next, we will define a backend that can send category notifications toothis app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="9cc1b-149">Envío de notificaciones con etiquetas</span><span class="sxs-lookup"><span data-stu-id="9cc1b-149">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="9cc1b-150">Ejecutar aplicación hello y generar notificaciones</span><span class="sxs-lookup"><span data-stu-id="9cc1b-150">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="9cc1b-151">En Android Studio, compile la aplicación hello e inícielo en un dispositivo o emulador.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-151">In Android Studio, build hello app and start it on a device or emulator.</span></span>
   
    <span data-ttu-id="9cc1b-152">Tenga en cuenta que interfaz de usuario proporciona un conjunto de la aplicación hello alterna que le permite elegir Hola categorías toosubscribe a.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-152">Note that hello app UI provides a set of toggles that lets you choose hello categories toosubscribe to.</span></span>
2. <span data-ttu-id="9cc1b-153">Habilite uno o más elementos de alternancia de las categorías y, a continuación, haga clic en **Suscribirse**.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-153">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="9cc1b-154">aplicación Hello convierte categorías Hola seleccionado en las etiquetas y solicita un nuevo registro de dispositivo para etiquetas de hello seleccionada del centro de notificaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-154">hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span> <span data-ttu-id="9cc1b-155">Hello categorías registrados se devuelve y se muestran en una notificación del sistema.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-155">hello registered categories are returned and displayed in a toast notification.</span></span>
3. <span data-ttu-id="9cc1b-156">Enviar una notificación de nuevo mediante la ejecución de la aplicación de consola .NET de hello.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-156">Send a new notification by running hello .NET Console app.</span></span>  <span data-ttu-id="9cc1b-157">Como alternativa, puede enviar notificaciones de plantilla etiquetadas con ficha de depuración de Hola de su centro de notificaciones de hello [Portal clásico de Azure].</span><span class="sxs-lookup"><span data-stu-id="9cc1b-157">Alternatively, you can send tagged template notifications using hello debug tab of your notification hub in hello [Azure Classic Portal].</span></span>
   
    <span data-ttu-id="9cc1b-158">Las notificaciones para las categorías de hello seleccionado aparecen como notificaciones del sistema.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-158">Notifications for hello selected categories appear as toast notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9cc1b-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9cc1b-159">Next steps</span></span>
<span data-ttu-id="9cc1b-160">En este tutorial hemos visto cómo toobroadcast noticias de última hora por categoría.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-160">In this tutorial we learned how toobroadcast breaking news by category.</span></span> <span data-ttu-id="9cc1b-161">Considere la posibilidad de completar uno de hello tutoriales que indican errores de otros escenarios avanzados de centros de notificaciones:</span><span class="sxs-lookup"><span data-stu-id="9cc1b-161">Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="9cc1b-162">[Utilice noticias de última hora de toobroadcast localizado de los centros de notificaciones]</span><span class="sxs-lookup"><span data-stu-id="9cc1b-162">[Use Notification Hubs toobroadcast localized breaking news]</span></span>
  
    <span data-ttu-id="9cc1b-163">Obtenga información acerca de cómo hello tooexpand interrumpir el envío de noticias aplicación tooenable localizar las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="9cc1b-163">Learn how tooexpand hello breaking news app tooenable sending localized notifications.</span></span>

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
