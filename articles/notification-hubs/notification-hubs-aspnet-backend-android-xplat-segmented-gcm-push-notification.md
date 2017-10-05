---
title: "Tutorial de noticias de última hora en los Centros de notificaciones: Android"
description: "Obtenga información acerca del uso de Centros de notificaciones del Bus de servicio de Azure para enviar notificaciones de noticias de última hora en dispositivos Android."
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
ms.openlocfilehash: 76ec01c874fceedab7d76b2ef58e4b45b5489f58
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="06902-103">Uso de los Centros de notificaciones para enviar noticias de última hora</span><span class="sxs-lookup"><span data-stu-id="06902-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="06902-104">Información general</span><span class="sxs-lookup"><span data-stu-id="06902-104">Overview</span></span>
<span data-ttu-id="06902-105">Este tema muestra cómo puede usar los Centros de notificaciones de Azure para difundir notificaciones de noticias de última hora en una aplicación Android.</span><span class="sxs-lookup"><span data-stu-id="06902-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to an Android app.</span></span> <span data-ttu-id="06902-106">Cuando lo complete, podrá registrar las categorías de noticias de última hora en las que esté interesado y recibir solo notificaciones de inserción para esas categorías.</span><span class="sxs-lookup"><span data-stu-id="06902-106">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="06902-107">Este escenario es un patrón común para muchas aplicaciones en las que las notificaciones tienen que enviarse a grupos de usuarios que han mostrado previamente interés en ellas, por ejemplo, lectores RSS, aplicaciones para aficionados a la música, etc.</span><span class="sxs-lookup"><span data-stu-id="06902-107">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="06902-108">Los escenarios de difusión se habilitan mediante la inclusión de una o más *etiquetas* cuando se crea un registro en el Centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="06902-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="06902-109">Cuando las notificaciones se envían a una etiqueta, todos los dispositivos registrados para la etiqueta recibirán la notificación.</span><span class="sxs-lookup"><span data-stu-id="06902-109">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="06902-110">Puesto que las etiquetas son cadenas simples, no tendrán que aprovisionarse antes.</span><span class="sxs-lookup"><span data-stu-id="06902-110">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="06902-111">Para información sobre las etiquetas, consulte [Expresiones de etiqueta y enrutamiento de los Centros de notificaciones](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="06902-111">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06902-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="06902-112">Prerequisites</span></span>
<span data-ttu-id="06902-113">Este tema se basa en la aplicación que creó en [Introducción a Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="06902-113">This topic builds on the app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="06902-114">Antes de comenzar este tutorial, debe haber completado la [Introducción a Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="06902-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="06902-115">Adición de una selección de categorías a la aplicación</span><span class="sxs-lookup"><span data-stu-id="06902-115">Add category selection to the app</span></span>
<span data-ttu-id="06902-116">El primer paso es agregar los elementos de la interfaz de usuario a la actividad principal existente que permiten al usuario seleccionar las categorías para registrar.</span><span class="sxs-lookup"><span data-stu-id="06902-116">The first step is to add the UI elements to your existing main activity that enable the user to select categories to register.</span></span> <span data-ttu-id="06902-117">Las categorías seleccionadas por un usuario se almacenan en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="06902-117">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="06902-118">Cuando la aplicación se inicia, se crea un registro de dispositivos en el Centro de notificaciones con las categorías seleccionadas como etiquetas.</span><span class="sxs-lookup"><span data-stu-id="06902-118">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="06902-119">Abra el archivo res/layout/activity_main.xml y sustituya el contenido por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="06902-119">Open your res/layout/activity_main.xml file, and substitute the content with the following:</span></span>
   
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
2. <span data-ttu-id="06902-120">Abra el archivo res/values/strings.xml y agregue las líneas siguientes:</span><span class="sxs-lookup"><span data-stu-id="06902-120">Open your res/values/strings.xml file and add the following lines:</span></span>
   
        <string name="button_subscribe">Subscribe</string>
        <string name="label_world">World</string>
        <string name="label_politics">Politics</string>
        <string name="label_business">Business</string>
        <string name="label_technology">Technology</string>
        <string name="label_science">Science</string>
        <string name="label_sports">Sports</string>
   
    <span data-ttu-id="06902-121">El diseño gráfico main_activity.xml ahora debe tener un aspecto similar a este:</span><span class="sxs-lookup"><span data-stu-id="06902-121">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
3. <span data-ttu-id="06902-122">Cree ahora una clase **Notifications** en el mismo paquete que la clase **MainActivity**.</span><span class="sxs-lookup"><span data-stu-id="06902-122">Now create a class **Notifications** in the same package as your **MainActivity** class.</span></span>
   
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
                            Log.e("MainActivity", "Failed to register - " + e.getMessage());
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
   
    <span data-ttu-id="06902-123">Esta clase usa el almacenamiento local para almacenar las categorías de noticias que este dispositivo ha de recibir.</span><span class="sxs-lookup"><span data-stu-id="06902-123">This class uses the local storage to store the categories of news that this device has to receive.</span></span> <span data-ttu-id="06902-124">También contiene métodos para registrar estas categorías.</span><span class="sxs-lookup"><span data-stu-id="06902-124">It also contains methods to register for these categories.</span></span>
4. <span data-ttu-id="06902-125">En la clase **MainActivity**, elimine los campos privados para **NotificationHub** y **GoogleCloudMessaging** y agregue un campo para **Notifications**:</span><span class="sxs-lookup"><span data-stu-id="06902-125">In your **MainActivity** class remove your private fields for **NotificationHub** and **GoogleCloudMessaging**, and add a field for **Notifications**:</span></span>
   
        // private GoogleCloudMessaging gcm;
        // private NotificationHub hub;
        private Notifications notifications;
5. <span data-ttu-id="06902-126">Luego, en el método **onCreate**, quite la inicialización del campo **hub** y el método **registerWithNotificationHubs**.</span><span class="sxs-lookup"><span data-stu-id="06902-126">Then, in the **onCreate** method, remove the initialization of the **hub** field and the **registerWithNotificationHubs** method.</span></span> <span data-ttu-id="06902-127">Agregue después las siguientes líneas que inicializan una instancia de la clase **Notifications** .</span><span class="sxs-lookup"><span data-stu-id="06902-127">Then add the following lines which initialize an instance of the **Notifications** class.</span></span> 

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            MyHandler.mainActivity = this;

            NotificationsManager.handleNotifications(this, SENDER_ID,
                    MyHandler.class);

            notifications = new Notifications(this, SENDER_ID, HubName, HubListenConnectionString);

            notifications.subscribeToCategories(notifications.retrieveCategories());
        }

    <span data-ttu-id="06902-128">`HubName` y `HubListenConnectionString` deberían estar ya establecidos con los marcadores de posición `<hub name>` y `<connection string with listen access>` por el nombre del centro de notificaciones y la cadena de conexión de *DefaultListenSharedAccessSignature* que obtuvo anteriormente.</span><span class="sxs-lookup"><span data-stu-id="06902-128">`HubName` and `HubListenConnectionString` should already be set with the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>

    > [AZURE.NOTE] <span data-ttu-id="06902-129">Puesto que las credenciales que se distribuyen con una aplicación de cliente no son normalmente seguras, solo debe distribuir la clave para el acceso de escucha con la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="06902-129">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="06902-130">El acceso de escucha permite a la aplicación el registro de notificaciones, pero los registros existentes no pueden modificarse y las notificaciones no se pueden enviar.</span><span class="sxs-lookup"><span data-stu-id="06902-130">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="06902-131">La clave de acceso completo se usa en un servicio back-end protegido para el envío de notificaciones y el cambio de registros existentes.</span><span class="sxs-lookup"><span data-stu-id="06902-131">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>


1. <span data-ttu-id="06902-132">Luego agregue las siguientes importaciones y el método `subscribe` para controlar el evento Click del botón para suscribir:</span><span class="sxs-lookup"><span data-stu-id="06902-132">Then, add the following imports and `subscribe` method to handle the subscribe button click event:</span></span>
   
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
   
    <span data-ttu-id="06902-133">Este método crea una lista de categorías y usa la clase **Notifications** para almacenar la lista en el almacenamiento local y registrar las etiquetas correspondientes en el centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="06902-133">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span></span> <span data-ttu-id="06902-134">Cuando se modifican las categorías, el registro vuelve a crearse con las nuevas categorías.</span><span class="sxs-lookup"><span data-stu-id="06902-134">When categories are changed, the registration is recreated with the new categories.</span></span>

<span data-ttu-id="06902-135">La aplicación ahora puede almacenar un conjunto de categorías en el almacenamiento local en el dispositivo y registrarse en el Centro de notificaciones siempre que el usuario cambie la selección de categorías.</span><span class="sxs-lookup"><span data-stu-id="06902-135">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="06902-136">Registro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="06902-136">Register for notifications</span></span>
<span data-ttu-id="06902-137">Estos pasos permiten registrar el Centro de notificaciones en el inicio mediante las categorías que se han almacenado en el almacén local.</span><span class="sxs-lookup"><span data-stu-id="06902-137">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="06902-138">Dado que el identificador de registro asignado por el servicio de mensajería en la nube de Google (GCM) puede cambiar en cualquier momento, debe registrarse para recibir notificaciones frecuentemente para evitar errores de notificación.</span><span class="sxs-lookup"><span data-stu-id="06902-138">Because the registrationId assigned by Google Cloud Messaging (GCM) can change at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="06902-139">En este ejemplo se registra la notificación cada vez que se inicia la aplicación.</span><span class="sxs-lookup"><span data-stu-id="06902-139">This example registers for notification every time that the app starts.</span></span> <span data-ttu-id="06902-140">En las aplicaciones que se ejecutan con frecuencia, más de una vez al día, es posible que pueda omitir el registro para conservar el ancho de banda si pasa menos de un día del registro previo.</span><span class="sxs-lookup"><span data-stu-id="06902-140">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
> 
> 

1. <span data-ttu-id="06902-141">Agregue el siguiente código al final del método **onCreate** en la clase **MainActivity**:</span><span class="sxs-lookup"><span data-stu-id="06902-141">Add the following code at the end of the **onCreate** method in the **MainActivity** class:</span></span>
   
        notifications.subscribeToCategories(notifications.retrieveCategories());
   
    <span data-ttu-id="06902-142">De esta forma, se garantiza que cada vez que la aplicación se inicia, se recuperan las categorías del almacenamiento local y se solicita un registro de estas categorías.</span><span class="sxs-lookup"><span data-stu-id="06902-142">This makes sure that every time the app starts it retrieves the categories from local storage and requests a registeration for these categories.</span></span> 
2. <span data-ttu-id="06902-143">Después actualice el método `onStart()` de la clase `MainActivity` de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="06902-143">Then update the `onStart()` method of the `MainActivity` class as follows:</span></span>
   
    <span data-ttu-id="06902-144">@Override protected void onStart() {</span><span class="sxs-lookup"><span data-stu-id="06902-144">@Override  protected void onStart() {</span></span>
   
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
    <span data-ttu-id="06902-145">}</span><span class="sxs-lookup"><span data-stu-id="06902-145">}</span></span>
   
    <span data-ttu-id="06902-146">De esta forma se actualiza la actividad principal según el estado de las categorías guardadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="06902-146">This updates the main activity based on the status of previously saved categories.</span></span>

<span data-ttu-id="06902-147">La aplicación está ahora completa y puede almacenar un conjunto de categorías en el almacenamiento local del dispositivo usado para registrarse en el Centro de notificaciones cuando el usuario cambie la selección de categorías.</span><span class="sxs-lookup"><span data-stu-id="06902-147">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span></span> <span data-ttu-id="06902-148">A continuación, definiremos un back-end que pueda enviar notificaciones de categorías a esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="06902-148">Next, we will define a backend that can send category notifications to this app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="06902-149">Envío de notificaciones con etiquetas</span><span class="sxs-lookup"><span data-stu-id="06902-149">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="06902-150">Ejecución de la aplicación y generación de notificaciones</span><span class="sxs-lookup"><span data-stu-id="06902-150">Run the app and generate notifications</span></span>
1. <span data-ttu-id="06902-151">En Android Studio, cree la aplicación e iníciela en un dispositivo o emulador.</span><span class="sxs-lookup"><span data-stu-id="06902-151">In Android Studio, build the app and start it on a device or emulator.</span></span>
   
    <span data-ttu-id="06902-152">Tenga en cuenta que la interfaz de usuario de la aplicación ofrece un conjunto de elementos de alternancia que le permite seleccionar las categorías a las que suscribirse.</span><span class="sxs-lookup"><span data-stu-id="06902-152">Note that the app UI provides a set of toggles that lets you choose the categories to subscribe to.</span></span>
2. <span data-ttu-id="06902-153">Habilite uno o más elementos de alternancia de las categorías y, a continuación, haga clic en **Suscribirse**.</span><span class="sxs-lookup"><span data-stu-id="06902-153">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="06902-154">La aplicación convierte las categorías seleccionadas en etiquetas y solicita un nuevo registro de dispositivo para las etiquetas seleccionadas al Centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="06902-154">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span> <span data-ttu-id="06902-155">Se devuelven las categorías registradas y se muestran en una notificación del sistema.</span><span class="sxs-lookup"><span data-stu-id="06902-155">The registered categories are returned and displayed in a toast notification.</span></span>
3. <span data-ttu-id="06902-156">Envíe una notificación nueva ejecutando la aplicación de la consola. NET.</span><span class="sxs-lookup"><span data-stu-id="06902-156">Send a new notification by running the .NET Console app.</span></span>  <span data-ttu-id="06902-157">También puede enviar notificaciones de plantilla con etiqueta mediante la pestaña Depurar del centro de notificaciones en el [Portal de Azure clásico].</span><span class="sxs-lookup"><span data-stu-id="06902-157">Alternatively, you can send tagged template notifications using the debug tab of your notification hub in the [Azure Classic Portal].</span></span>
   
    <span data-ttu-id="06902-158">Las notificaciones para las categorías seleccionadas aparecen como notificaciones del sistema.</span><span class="sxs-lookup"><span data-stu-id="06902-158">Notifications for the selected categories appear as toast notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06902-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="06902-159">Next steps</span></span>
<span data-ttu-id="06902-160">En este tutorial hemos aprendido cómo difundir noticias de última hora por categoría.</span><span class="sxs-lookup"><span data-stu-id="06902-160">In this tutorial we learned how to broadcast breaking news by category.</span></span> <span data-ttu-id="06902-161">Considere la posibilidad de llevar a cabo uno de los siguientes tutoriales que destacan otros escenarios de Centros de notificaciones avanzados:</span><span class="sxs-lookup"><span data-stu-id="06902-161">Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="06902-162">[Uso de los Centros de notificaciones para difundir noticias de última hora localizadas]</span><span class="sxs-lookup"><span data-stu-id="06902-162">[Use Notification Hubs to broadcast localized breaking news]</span></span>
  
    <span data-ttu-id="06902-163">Conozca cómo expandir la aplicación de noticias de última hora para habilitar el envío de notificaciones localizadas.</span><span class="sxs-lookup"><span data-stu-id="06902-163">Learn how to expand the breaking news app to enable sending localized notifications.</span></span>

<!-- Images. -->
[A1]: ./media/notification-hubs-aspnet-backend-android-breaking-news/android-breaking-news1.PNG

<!-- URLs.-->
[get-started]: notification-hubs-android-push-notification-google-gcm-get-started.md
<span data-ttu-id="06902-164">[Uso de los Centros de notificaciones para difundir noticias de última hora localizadas]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span><span class="sxs-lookup"><span data-stu-id="06902-164">[Use Notification Hubs to broadcast localized breaking news]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span></span>
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
<span data-ttu-id="06902-165">[Portal de Azure clásico]: https://manage.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="06902-165">[Azure Classic Portal]: https://manage.windowsazure.com</span></span>
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
