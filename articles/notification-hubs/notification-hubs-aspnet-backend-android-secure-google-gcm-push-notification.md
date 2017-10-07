---
title: aaaSending Secure notificaciones Push con centros de notificaciones de Azure
description: "Obtenga información acerca de cómo toosend segura push aplicación Android tooan de notificaciones de Azure. Ejemplos de código escritos en Java y C#."
documentationcenter: android
keywords: push notification,push notifications,push messages,android push notifications
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: daf3de1c-f6a9-43c4-8165-a76bfaa70893
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: d07943c4691ed07acb987086228ef565e6281d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sending-secure-push-notifications-with-azure-notification-hubs"></a>Envío de notificaciones push seguras a los Centros de notificaciones de Azure
> [!div class="op_single_selector"]
> * [Windows Universal](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>Información general
> [!IMPORTANT]
> toocomplete este tutorial, debe tener una cuenta activa de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).
> 
> 

Compatibilidad con notificaciones de inserción de Microsoft Azure le permite tooaccess una infraestructura de mensaje de inserción de fácil de usar, varias plataformas y escala horizontal, que simplifica considerablemente la implementación de Hola de notificaciones de inserción para las aplicaciones de consumidor y empresa plataformas móviles.

A veces debido a restricciones de seguridad o tooregulatory, una aplicación podría querer tooinclude algo en la notificación de Hola que no se transmiten a través de la infraestructura de notificaciones de inserción estándar Hola. Este tutorial describe cómo tooachieve Hola misma experiencia mediante el envío de información confidencial a través de una conexión segura y autenticada entre dispositivos Android de cliente de Hola y Hola backend de la aplicación.

En un nivel alto, flujo de hello es como sigue:

1. Hola aplicación back-end:
   * Almacena la carga segura en la base de datos back-end.
   * Envía el Id. de Hola de este dispositivo Android de notificación toohello (se envía ninguna información segura).
2. aplicación Hello en dispositivo hello, al recibir la notificación de hello:
   * dispositivos Android Hola contacta con hello back-end que lo solicita Hola carga de seguridad.
   * aplicación Hello puede mostrar carga hello como una notificación en el dispositivo de Hola.

Es importante toonote que Hola anterior flujo (y en este tutorial), se da por supuesto ese dispositivo Hola almacena un token de autenticación en el almacenamiento local, después de hello usuario inicia sesión en. Esto garantiza una experiencia completamente sin problemas, como dispositivo de hello puede recuperar la carga de seguridad de la notificación de hello con este token. Si la aplicación no almacena tokens de autenticación en el dispositivo de hello, o si pueden haber expirado estos tokens, aplicación de dispositivo de hello, tras recibir la notificación de inserción de hello debe mostrar una notificación genérica preguntar aplicación Hola de hello usuario toolaunch. aplicación Hello, a continuación, autentica el usuario de Hola y muestra la carga de notificaciones de Hola.

Este tutorial muestra cómo las notificaciones de inserción toosend segura. Se basa en hello [informar a los usuarios](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) tutorial, por lo que debe completar los pasos de hello en este tutorial primero si no lo ha hecho ya.

> [!NOTE]
> En este tutorial se supone que se ha creado y configurado el Centro de notificaciones tal como se describe en [Introducción a los Centros de notificaciones (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-android-project"></a>Modificar el proyecto de Android Hola
Ahora que ha modificado su Hola solo de aplicación back-end toosend *identificador* de una notificación de inserción, tienen toochange su toohandle aplicación Android notificación y devolución de llamada su hello tooretrieve de back-end seguros toobe de mensaje que se muestra.
tooachieve este objetivo tiene toomake seguro de que la aplicación Android sabe cómo tooauthenticate con el back-end cuando recibe notificaciones de inserción de Hola.

Ahora modificaremos hello *inicio de sesión* flujo en el valor del encabezado de autenticación orden toosave Hola Hola comparten las preferencias de la aplicación. Mecanismos análogos pueden ser utilizado toostore cualquier token de autenticación (por ejemplo, tokens de OAuth) que Hola aplicación tendrá toouse sin necesidad de credenciales de usuario.

1. En el proyecto de aplicación de Android, agregar Hola siguientes constantes en parte superior de Hola de hello **MainActivity** clase:
   
        public static final String NOTIFY_USERS_PROPERTIES = "NotifyUsersProperties";
        public static final String AUTHORIZATION_HEADER_PROPERTY = "AuthorizationHeader";
2. Aún en hello **MainActivity** (clase), actualización hello `getAuthorizationHeader()` hello toocontain de método siguiente código:
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
   
            SharedPreferences sp = getSharedPreferences(NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            sp.edit().putString(AUTHORIZATION_HEADER_PROPERTY, basicAuthHeader).commit();
   
            return basicAuthHeader;
        }
3. Agregue los siguiente hello `import` las instrucciones en la parte superior de Hola de hello **MainActivity** archivo:
   
        import android.content.SharedPreferences;

Ahora cambiaremos controlador Hola que se llama cuando se recibe la notificación de Hola.

1. Hola **MyHandler** clase cambiar hello `OnReceive()` método toocontain:
   
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String secureMessageId = bundle.getString("secureId");
            retrieveNotification(secureMessageId);
        }
2. A continuación, agregue hello `retrieveNotification()` método, reemplazando el marcador de posición de hello `{back-end endpoint}` con punto de conexión de back-end de hello obtenido al implementar el back-end:
   
        private void retrieveNotification(final String secureMessageId) {
            SharedPreferences sp = ctx.getSharedPreferences(MainActivity.NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            final String authorizationHeader = sp.getString(MainActivity.AUTHORIZATION_HEADER_PROPERTY, null);
   
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
                        HttpUriRequest request = new HttpGet("{back-end endpoint}/api/notifications/"+secureMessageId);
                        request.addHeader("Authorization", "Basic "+authorizationHeader);
                        HttpResponse response = new DefaultHttpClient().execute(request);
                        if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                            Log.e("MainActivity", "Error retrieving secure notification" + response.getStatusLine().getStatusCode());
                            throw new RuntimeException("Error retrieving secure notification");
                        }
                        String secureNotificationJSON = EntityUtils.toString(response.getEntity());
                        JSONObject secureNotification = new JSONObject(secureNotificationJSON);
                        sendNotification(secureNotification.getString("Payload"));
                    } catch (Exception e) {
                        Log.e("MainActivity", "Failed tooretrieve secure notification - " + e.getMessage());
                        return e;
                    }
                    return null;
                }
            }.execute(null, null, null);
        }

Este método llama a su contenido usando credenciales de hello almacenadas en hello compartido preferencias y lo muestra como una notificación normal de notificación de Hola de tooretrieve de back-end de la aplicación. notificación de Hello busca toohello de usuario de aplicación exactamente igual que cualquier otra notificación de inserción.

Tenga en cuenta que es preferible toohandle casos de Hola de propiedad de encabezado de autenticación que falta o el rechazo por hello back-end. control específico de Hola de estos casos dependen principalmente de la experiencia del usuario de destino. Una opción es toodisplay una notificación con un mensaje genérico para la notificación de real de hello usuario tooauthenticate tooretrieve Hola.

## <a name="run-hello-application"></a>Ejecutar aplicación Hola
toorun Hola aplicación, Hola siguientes:

1. Asegúrese de que **AppBackend** se ha implementado en Azure. Si utiliza Visual Studio, ejecute hello **AppBackend** aplicación de API Web. Se mostrará una página web ASP.NET.
2. En Eclipse, ejecutar la aplicación hello en un emulador de dispositivo o hello Android físico.
3. En la aplicación hello Android interfaz de usuario, escriba un nombre de usuario y una contraseña. Pueden ser cualquier cadena, pero deben ser Hola el mismo valor.
4. En la aplicación hello Android interfaz de usuario, haga clic en **sesión**. A continuación, haga clic en **Enviar inserción**.

