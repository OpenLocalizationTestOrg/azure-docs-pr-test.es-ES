---
title: "aaaAzure notificación centros de informar a los usuarios para Android con back-end de .NET"
description: "Obtenga información acerca de cómo toosend push toousers de notificaciones en Azure. Ejemplos de código escritos en Java para Android"
documentationcenter: android
services: notification-hubs
author: ysxu
manager: erikre
editor: 
ms.assetid: ae0e17a8-9d2b-496e-afd2-baa151370c25
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: b042d2e6fb7f7c861c378526a8a0d59ab75beef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-for-android-with-net-backend"></a><span data-ttu-id="c3c49-104">Notificaciones de Azure Notification Hubs a los usuarios de Android con back-end de .NET</span><span class="sxs-lookup"><span data-stu-id="c3c49-104">Azure Notification Hubs Notify Users for Android with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="c3c49-105">Información general</span><span class="sxs-lookup"><span data-stu-id="c3c49-105">Overview</span></span>
<span data-ttu-id="c3c49-106">Compatibilidad de la notificación de inserción en Azure permite tooaccess una fácil de usar, multiplataforma y la infraestructura de inserción de escala horizontal, que simplifica considerablemente la implementación de Hola de notificaciones de inserción para las aplicaciones de consumidor y empresa para dispositivos móviles plataformas.</span><span class="sxs-lookup"><span data-stu-id="c3c49-106">Push notification support in Azure enables you tooaccess an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="c3c49-107">Este tutorial muestra cómo toouse centros de notificaciones de Azure toosend push usuario de aplicación específica de tooa de notificaciones en un dispositivo específico.</span><span class="sxs-lookup"><span data-stu-id="c3c49-107">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa specific app user on a specific device.</span></span> <span data-ttu-id="c3c49-108">Un back-end de ASP.NET WebAPI es tooauthenticate usa clientes y las notificaciones de toogenerate, como se muestra en el tema de la Guía de hello [registrar desde su aplicación de back-end](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span><span class="sxs-lookup"><span data-stu-id="c3c49-108">An ASP.NET WebAPI backend is used tooauthenticate clients and toogenerate notifications, as shown in hello guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span> <span data-ttu-id="c3c49-109">Este tutorial se basa en el centro de notificaciones de Hola que creó en hello [Introducción a centros de notificaciones (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="c3c49-109">This tutorial builds on hello notification hub that you created in hello [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="c3c49-110">En este tutorial se supone que se ha creado y configurado el Centro de notificaciones tal como se describe en [Introducción a los Centros de notificaciones (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c3c49-110">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="create-hello-android-project"></a><span data-ttu-id="c3c49-111">Crear proyecto de Android hello</span><span class="sxs-lookup"><span data-stu-id="c3c49-111">Create hello Android Project</span></span>
<span data-ttu-id="c3c49-112">Hola siguiente paso es aplicación de Android toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="c3c49-112">hello next step is toocreate hello Android application.</span></span>

1. <span data-ttu-id="c3c49-113">Siga hello [Introducción a centros de notificaciones (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) toocreate tutorial y configurar las notificaciones de inserción de aplicación tooreceive de GCM.</span><span class="sxs-lookup"><span data-stu-id="c3c49-113">Follow hello [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial toocreate and configure your app tooreceive push notifications from GCM.</span></span>
2. <span data-ttu-id="c3c49-114">Abra su **res/layout/activity_main.xml** archivo, reemplace Hola con hello siguiendo las definiciones de contenido.</span><span class="sxs-lookup"><span data-stu-id="c3c49-114">Open your **res/layout/activity_main.xml** file, replace hello with hello following content definitions.</span></span>
   
    <span data-ttu-id="c3c49-115">Esto agrega nuevos controles de EditText para iniciar sesión como usuario.</span><span class="sxs-lookup"><span data-stu-id="c3c49-115">This adds new EditText controls for logging in as a user.</span></span> <span data-ttu-id="c3c49-116">Además, se agrega un campo para una etiqueta de nombre de usuario que formará parte de las notificaciones que envíe:</span><span class="sxs-lookup"><span data-stu-id="c3c49-116">Also a field is added for a username tag that will be part of notifications you send:</span></span>
   
        <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
            xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent"
            android:layout_height="match_parent" android:paddingLeft="@dimen/activity_horizontal_margin"
            android:paddingRight="@dimen/activity_horizontal_margin"
            android:paddingTop="@dimen/activity_vertical_margin"
            android:paddingBottom="@dimen/activity_vertical_margin" tools:context=".MainActivity">
   
        <EditText
            android:id="@+id/usernameText"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:ems="10"
            android:hint="@string/usernameHint"
            android:layout_above="@+id/passwordText"
            android:layout_alignParentEnd="true" />
        <EditText
            android:id="@+id/passwordText"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:ems="10"
            android:hint="@string/passwordHint"
            android:inputType="textPassword"
            android:layout_above="@+id/buttonLogin"
            android:layout_alignParentEnd="true" />
        <Button
            android:id="@+id/buttonLogin"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/loginButton"
            android:onClick="login"
            android:layout_above="@+id/toggleButtonGCM"
            android:layout_centerHorizontal="true"
            android:layout_marginBottom="24dp" />
        <ToggleButton
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textOn="WNS on"
            android:textOff="WNS off"
            android:id="@+id/toggleButtonWNS"
            android:layout_toLeftOf="@id/toggleButtonGCM"
            android:layout_centerVertical="true" />
        <ToggleButton
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textOn="GCM on"
            android:textOff="GCM off"
            android:id="@+id/toggleButtonGCM"
            android:checked="true"
            android:layout_centerHorizontal="true"
            android:layout_centerVertical="true" />
        <ToggleButton
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textOn="APNS on"
            android:textOff="APNS off"
            android:id="@+id/toggleButtonAPNS"
            android:layout_toRightOf="@id/toggleButtonGCM"
            android:layout_centerVertical="true" />
        <EditText
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/editTextNotificationMessageTag"
            android:layout_below="@id/toggleButtonGCM"
            android:layout_centerHorizontal="true"
            android:hint="@string/notification_message_tag_hint" />
        <EditText
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/editTextNotificationMessage"
            android:layout_below="@+id/editTextNotificationMessageTag"
            android:layout_centerHorizontal="true"
            android:hint="@string/notification_message_hint" />
        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/send_button"
            android:id="@+id/sendbutton"
            android:onClick="sendNotificationButtonOnClick"
            android:layout_below="@+id/editTextNotificationMessage"
            android:layout_centerHorizontal="true" />
        </RelativeLayout>
3. <span data-ttu-id="c3c49-117">Abra su **res/values/strings.xml** archivo y reemplazar hello `send_button` definición por siguiente Hola líneas esa cadena de hello redefine para hello `send_button` y agregue las cadenas de hello otros controles:</span><span class="sxs-lookup"><span data-stu-id="c3c49-117">Open your **res/values/strings.xml** file and replace hello `send_button` definition with hello following lines that redefine hello string for hello `send_button` and add strings for hello other controls:</span></span>
   
        <string name="usernameHint">Username</string>
        <string name="passwordHint">Password</string>
        <string name="loginButton">1. Log in</string>
        <string name="send_button">2. Send Notification</string>
        <string name="notification_message_tag_hint">
            Recipient username tag
        </string>
   
    <span data-ttu-id="c3c49-118">El diseño gráfico main_activity.xml ahora debe tener un aspecto similar a este:</span><span class="sxs-lookup"><span data-stu-id="c3c49-118">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
4. <span data-ttu-id="c3c49-119">Crear una nueva clase denominada **RegisterClient** en hello en el mismo paquete como su `MainActivity` clase.</span><span class="sxs-lookup"><span data-stu-id="c3c49-119">Create a new class named **RegisterClient** in hello same package as your `MainActivity` class.</span></span> <span data-ttu-id="c3c49-120">Usar código de hello debajo para el nuevo archivo de clase Hola.</span><span class="sxs-lookup"><span data-stu-id="c3c49-120">Use hello code below for hello new class file.</span></span>
   
        import java.io.IOException;
        import java.io.UnsupportedEncodingException;
        import java.util.Set;
   
        import org.apache.http.HttpResponse;
        import org.apache.http.HttpStatus;
        import org.apache.http.client.ClientProtocolException;
        import org.apache.http.client.HttpClient;
        import org.apache.http.client.methods.HttpPost;
        import org.apache.http.client.methods.HttpPut;
        import org.apache.http.client.methods.HttpUriRequest;
        import org.apache.http.entity.StringEntity;
        import org.apache.http.impl.client.DefaultHttpClient;
        import org.apache.http.util.EntityUtils;
        import org.json.JSONArray;
        import org.json.JSONException;
        import org.json.JSONObject;
   
        import android.content.Context;
        import android.content.SharedPreferences;
        import android.util.Log;
   
        public class RegisterClient {
            private static final String PREFS_NAME = "ANHSettings";
            private static final String REGID_SETTING_NAME = "ANHRegistrationId";
            private String Backend_Endpoint;
            SharedPreferences settings;
            protected HttpClient httpClient;
            private String authorizationHeader;
   
            public RegisterClient(Context context, String backendEnpoint) {
                super();
                this.settings = context.getSharedPreferences(PREFS_NAME, 0);
                httpClient =  new DefaultHttpClient();
                Backend_Endpoint = backendEnpoint + "/api/register";
            }
   
            public String getAuthorizationHeader() {
                return authorizationHeader;
            }
   
            public void setAuthorizationHeader(String authorizationHeader) {
                this.authorizationHeader = authorizationHeader;
            }
   
            public void register(String handle, Set<String> tags) throws ClientProtocolException, IOException, JSONException {
                String registrationId = retrieveRegistrationIdOrRequestNewOne(handle);
   
                JSONObject deviceInfo = new JSONObject();
                deviceInfo.put("Platform", "gcm");
                deviceInfo.put("Handle", handle);
                deviceInfo.put("Tags", new JSONArray(tags));
   
                int statusCode = upsertRegistration(registrationId, deviceInfo);
   
                if (statusCode == HttpStatus.SC_OK) {
                    return;
                } else if (statusCode == HttpStatus.SC_GONE){
                    settings.edit().remove(REGID_SETTING_NAME).commit();
                    registrationId = retrieveRegistrationIdOrRequestNewOne(handle);
                    statusCode = upsertRegistration(registrationId, deviceInfo);
                    if (statusCode != HttpStatus.SC_OK) {
                        Log.e("RegisterClient", "Error upserting registration: " + statusCode);
                        throw new RuntimeException("Error upserting registration");
                    }
                } else {
                    Log.e("RegisterClient", "Error upserting registration: " + statusCode);
                    throw new RuntimeException("Error upserting registration");
                }
            }
   
            private int upsertRegistration(String registrationId, JSONObject deviceInfo)
                    throws UnsupportedEncodingException, IOException,
                    ClientProtocolException {
                HttpPut request = new HttpPut(Backend_Endpoint+"/"+registrationId);
                request.setEntity(new StringEntity(deviceInfo.toString()));
                request.addHeader("Authorization", "Basic "+authorizationHeader);
                request.addHeader("Content-Type", "application/json");
                HttpResponse response = httpClient.execute(request);
                int statusCode = response.getStatusLine().getStatusCode();
                return statusCode;
            }
   
            private String retrieveRegistrationIdOrRequestNewOne(String handle) throws ClientProtocolException, IOException {
                if (settings.contains(REGID_SETTING_NAME))
                    return settings.getString(REGID_SETTING_NAME, null);
   
                HttpUriRequest request = new HttpPost(Backend_Endpoint+"?handle="+handle);
                request.addHeader("Authorization", "Basic "+authorizationHeader);
                HttpResponse response = httpClient.execute(request);
                if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                    Log.e("RegisterClient", "Error creating registrationId: " + response.getStatusLine().getStatusCode());
                    throw new RuntimeException("Error creating Notification Hubs registrationId");
                }
                String registrationId = EntityUtils.toString(response.getEntity());
                registrationId = registrationId.substring(1, registrationId.length()-1);
   
                settings.edit().putString(REGID_SETTING_NAME, registrationId).commit();
   
                return registrationId;
            }
        }
   
    <span data-ttu-id="c3c49-121">Este componente implementa Hola REST llamadas toocontact necesario Hola aplicación back-end, en orden tooregister las notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="c3c49-121">This component implements hello REST calls required toocontact hello app backend, in order tooregister for push notifications.</span></span> <span data-ttu-id="c3c49-122">También localmente almacena hello *registrationIds* creado por hello centro de notificaciones como se detalla en [registrar desde su aplicación de back-end](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span><span class="sxs-lookup"><span data-stu-id="c3c49-122">It also locally stores hello *registrationIds* created by hello Notification Hub as detailed in [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span> <span data-ttu-id="c3c49-123">Tenga en cuenta que usa un token de autorización almacenado en almacenamiento local al hacer clic en hello **sesión** botón.</span><span class="sxs-lookup"><span data-stu-id="c3c49-123">Note that it uses an authorization token stored in local storage when you click hello **Log in** button.</span></span>
5. <span data-ttu-id="c3c49-124">En su `MainActivity` clase quite o marque como comentario el campo privado para `NotificationHub`, y agregar un campo para hello `RegisterClient` clase y una cadena para el punto de conexión de su servidor ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c3c49-124">In your `MainActivity` class remove or comment out your private field for `NotificationHub`, and add a field for hello `RegisterClient` class and a string for your ASP.NET backend's endpoint.</span></span> <span data-ttu-id="c3c49-125">Ser seguro tooreplace `<Enter Your Backend Endpoint>` con hello obtenida anteriormente el punto de conexión real de back-end.</span><span class="sxs-lookup"><span data-stu-id="c3c49-125">Be sure tooreplace `<Enter Your Backend Endpoint>` with hello your actual backend endpoint obtained previously.</span></span> <span data-ttu-id="c3c49-126">Por ejemplo: `http://mybackend.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="c3c49-126">For example, `http://mybackend.azurewebsites.net`.</span></span>

        //private NotificationHub hub;
        private RegisterClient registerClient;
        private static final String BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";


1. <span data-ttu-id="c3c49-127">En su `MainActivity` (clase), en hello `onCreate` método, quite o marque como comentario la inicialización Hola de hello `hub` hello y campo llaman toohello `registerWithNotificationHubs` método.</span><span class="sxs-lookup"><span data-stu-id="c3c49-127">In your `MainActivity` class, in hello `onCreate` method, remove or comment out hello initialization of hello `hub` field and hello call toohello `registerWithNotificationHubs` method.</span></span> <span data-ttu-id="c3c49-128">A continuación, agregue código tooinitialize una instancia de hello `RegisterClient` clase.</span><span class="sxs-lookup"><span data-stu-id="c3c49-128">Then add code tooinitialize an instance of hello `RegisterClient` class.</span></span> <span data-ttu-id="c3c49-129">método Hello debe contener Hola siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="c3c49-129">hello method should contain hello following lines:</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
   
            MyHandler.mainActivity = this;
            NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);
            gcm = GoogleCloudMessaging.getInstance(this);
   
            //hub = new NotificationHub(HubName, HubListenConnectionString, this);
            //registerWithNotificationHubs();
   
            registerClient = new RegisterClient(this, BACKEND_ENDPOINT);
   
            setContentView(R.layout.activity_main);
        }
2. <span data-ttu-id="c3c49-130">En su `MainActivity` clase, eliminar o marque como comentario todo hello `registerWithNotificationHubs` método.</span><span class="sxs-lookup"><span data-stu-id="c3c49-130">In your `MainActivity` class, delete or comment out hello entire `registerWithNotificationHubs` method.</span></span> <span data-ttu-id="c3c49-131">No se usará en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="c3c49-131">It will not be used in this tutorial.</span></span>
3. <span data-ttu-id="c3c49-132">Agregue los siguiente hello `import` instrucciones tooyour **MainActivity.java** archivo.</span><span class="sxs-lookup"><span data-stu-id="c3c49-132">Add hello following `import` statements tooyour **MainActivity.java** file.</span></span>
   
        import android.widget.Button;
        import java.io.UnsupportedEncodingException;
        import android.content.Context;
        import java.util.HashSet;
        import android.widget.Toast;
        import org.apache.http.client.ClientProtocolException;
        import java.io.IOException;
        import org.apache.http.HttpStatus;
4. <span data-ttu-id="c3c49-133">A continuación, agregue Hola después Hola de métodos toohandle **sesión** click del botón eventos y enviar notificaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="c3c49-133">Then, add hello following methods toohandle hello **Log in** button click event and sending push notifications.</span></span>
   
        @Override
        protected void onStart() {
            super.onStart();
            Button sendPush = (Button) findViewById(R.id.sendbutton);
            sendPush.setEnabled(false);
        }
   
        public void login(View view) throws UnsupportedEncodingException {
            this.registerClient.setAuthorizationHeader(getAuthorizationHeader());
   
            final Context context = this;
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
                        String regid = gcm.register(SENDER_ID);
                        registerClient.register(regid, new HashSet<String>());
                    } catch (Exception e) {
                        DialogNotify("MainActivity - Failed tooregister", e.getMessage());
                        return e;
                    }
                    return null;
                }
   
                protected void onPostExecute(Object result) {
                    Button sendPush = (Button) findViewById(R.id.sendbutton);
                    sendPush.setEnabled(true);
                    Toast.makeText(context, "Logged in and registered.",
                            Toast.LENGTH_LONG).show();
                }
            }.execute(null, null, null);
        }
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
            return basicAuthHeader;
        }
   
        /**
         * This method calls hello ASP.NET WebAPI backend toosend hello notification message
         * toohello platform notification service based on hello pns parameter.
         *
         * @param pns     hello platform notification service toosend hello notification message to. Must
         *                be one of hello following ("wns", "gcm", "apns").
         * @param userTag hello tag for hello user who will receive hello notification message. This string
         *                must not contain spaces or special characters.
         * @param message hello notification message string. This string must include hello double quotes
         *                toobe used as JSON content.
         */
        public void sendPush(final String pns, final String userTag, final String message)
                throws ClientProtocolException, IOException {
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
   
                        String uri = BACKEND_ENDPOINT + "/api/notifications";
                        uri += "?pns=" + pns;
                        uri += "&to_tag=" + userTag;
   
                        HttpPost request = new HttpPost(uri);
                        request.addHeader("Authorization", "Basic "+ getAuthorizationHeader());
                        request.setEntity(new StringEntity(message));
                        request.addHeader("Content-Type", "application/json");
   
                        HttpResponse response = new DefaultHttpClient().execute(request);
   
                        if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                            DialogNotify("MainActivity - Error sending " + pns + " notification",
                                response.getStatusLine().toString());
                            throw new RuntimeException("Error sending notification");
                        }
                    } catch (Exception e) {
                        DialogNotify("MainActivity - Failed toosend " + pns + " notification ", e.getMessage());
                        return e;
                    }
   
                    return null;
                }
            }.execute(null, null, null);
        }

    <span data-ttu-id="c3c49-134">Hola `login` controlador para hello **sesión** botón genera un mediante símbolo (token) de la autenticación básica en hello entrada nombre de usuario y una contraseña (tenga en cuenta que esto representa cualquier token que se utiliza el esquema de autenticación), a continuación utiliza `RegisterClient`back-end de toocall hello para el registro.</span><span class="sxs-lookup"><span data-stu-id="c3c49-134">hello `login` handler for hello **Log in** button generates a basic authentication token using on hello input username and password (note that this represents any token your authentication scheme uses), then it uses `RegisterClient` toocall hello backend for registration.</span></span>

    <span data-ttu-id="c3c49-135">Hola `sendPush` llamadas de método hello back-end tootrigger un usuario de toohello notificación seguros basado en etiqueta de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3c49-135">hello `sendPush` method calls hello backend tootrigger a secure notification toohello user based on hello user tag.</span></span> <span data-ttu-id="c3c49-136">Hello notificación de plataforma de servicio que `sendPush` destinos depende de hello `pns` cadena que se pasa.</span><span class="sxs-lookup"><span data-stu-id="c3c49-136">hello platform notification service that `sendPush` targets depends on hello `pns` string passed in.</span></span>

1. <span data-ttu-id="c3c49-137">En su `MainActivity` (clase), actualización hello `sendNotificationButtonOnClick` Hola de método toocall `sendPush` método con del usuario de hello selecciona servicios de notificación de plataforma como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="c3c49-137">In your `MainActivity` class, update hello `sendNotificationButtonOnClick` method toocall hello `sendPush` method with hello user's selected platform notification services as follows.</span></span>
   
       /**
        * Send Notification button click handler. This method sends hello push notification
        * message tooeach platform selected.
        *
        * @param v hello view
        */
       public void sendNotificationButtonOnClick(View v)
               throws ClientProtocolException, IOException {
   
           String nhMessageTag = ((EditText) findViewById(R.id.editTextNotificationMessageTag))
                   .getText().toString();
           String nhMessage = ((EditText) findViewById(R.id.editTextNotificationMessage))
                   .getText().toString();
   
           // JSON String
           nhMessage = "\"" + nhMessage + "\"";
   
           if (((ToggleButton)findViewById(R.id.toggleButtonWNS)).isChecked())
           {
               sendPush("wns", nhMessageTag, nhMessage);
           }
           if (((ToggleButton)findViewById(R.id.toggleButtonGCM)).isChecked())
           {
               sendPush("gcm", nhMessageTag, nhMessage);
           }
           if (((ToggleButton)findViewById(R.id.toggleButtonAPNS)).isChecked())
           {
               sendPush("apns", nhMessageTag, nhMessage);
           }
       }

## <a name="run-hello-application"></a><span data-ttu-id="c3c49-138">Ejecutar aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="c3c49-138">Run hello Application</span></span>
1. <span data-ttu-id="c3c49-139">Ejecute la aplicación hello en un dispositivo o un emulador con Android Studio.</span><span class="sxs-lookup"><span data-stu-id="c3c49-139">Run hello application on a device or an emulator using Android Studio.</span></span>
2. <span data-ttu-id="c3c49-140">En la aplicación Android hello, escriba un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="c3c49-140">In hello Android app, enter a username and password.</span></span> <span data-ttu-id="c3c49-141">Ambos deben ser Hola mismo valor de cadena y no debe contener espacios ni caracteres especiales.</span><span class="sxs-lookup"><span data-stu-id="c3c49-141">They must both be hello same string value and they must not contain spaces or special characters.</span></span>
3. <span data-ttu-id="c3c49-142">En la aplicación Android hello, haga clic en **sesión**.</span><span class="sxs-lookup"><span data-stu-id="c3c49-142">In hello Android app, click **Log in**.</span></span> <span data-ttu-id="c3c49-143">Espere que aparezca un mensaje de aviso que indique que **se ha iniciado la sesión y se ha registrado**.</span><span class="sxs-lookup"><span data-stu-id="c3c49-143">Wait for a toast message that states **Logged in and registered**.</span></span> <span data-ttu-id="c3c49-144">Esto le permitirá hello **enviar notificación** botón.</span><span class="sxs-lookup"><span data-stu-id="c3c49-144">This will enable hello **Send Notification** button.</span></span>
   
    ![][A2]
4. <span data-ttu-id="c3c49-145">Haga clic en tooenable de botones de alternancia de hello todas las plataformas donde haya ejecutado la aplicación hello y un usuario registrado.</span><span class="sxs-lookup"><span data-stu-id="c3c49-145">Click hello toggle buttons tooenable all platforms where you have ran hello app and registered a user.</span></span>
5. <span data-ttu-id="c3c49-146">Escriba nombre de usuario de Hola que recibirá el mensaje de notificación de saludo.</span><span class="sxs-lookup"><span data-stu-id="c3c49-146">Enter hello user's name that will receive hello notification message.</span></span> <span data-ttu-id="c3c49-147">Ese usuario debe registrarse para recibir notificaciones en dispositivos de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3c49-147">That user must be registered for notifications on hello target devices.</span></span>
6. <span data-ttu-id="c3c49-148">Escriba un mensaje para hello tooreceive de usuario como un mensaje de notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="c3c49-148">Enter a message for hello user tooreceive as a push notification message.</span></span>
7. <span data-ttu-id="c3c49-149">Haga clic en **Enviar notificación**.</span><span class="sxs-lookup"><span data-stu-id="c3c49-149">Click **Send Notification**.</span></span>  <span data-ttu-id="c3c49-150">Cada dispositivo que tiene un registro con la etiqueta de nombre de usuario correspondiente Hola recibirá notificación de inserción de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3c49-150">Each device that has a registration with hello matching username tag will receive hello push notification.</span></span>

[A1]: ./media/notification-hubs-aspnet-backend-android-notify-users/android-notify-users.png
[A2]: ./media/notification-hubs-aspnet-backend-android-notify-users/android-notify-users-enter-password.png