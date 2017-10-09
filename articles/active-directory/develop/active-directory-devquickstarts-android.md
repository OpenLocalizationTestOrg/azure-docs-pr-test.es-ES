---
title: "aaaAzure AD Android Introducción | Documentos de Microsoft"
description: "¿Cómo toobuild una aplicación Android que se integra con Azure AD para inicio de sesión y llamadas a Azure AD había protegido API mediante OAuth."
services: active-directory
documentationcenter: android
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: da1ee39f-89d3-4d36-96f1-4eabbc662343
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 01/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1aedc8ff60874b405a182a4ccbfb2c8b4d9d3704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a>Integración de Azure AD en una aplicación Android
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> Probar la versión preliminar de Hola de nuestra nueva [portal para desarrolladores de](https://identity.microsoft.com/Docs/Android), que le ayudará a ponerse a trabajar con Azure AD en tan solo unos minutos. portal para desarrolladores de Hello le guiará a través del proceso de Hola de registrar una aplicación y la integración de Azure AD en el código. Cuando haya terminado, tendrá una aplicación sencilla que podrá autenticar a los usuarios del inquilino, así como un back-end con capacidad para aceptar tokens y realizar validaciones.
>
>

Si está desarrollando una aplicación de escritorio, Azure Active Directory (Azure AD) hace simple y sencillo para tooauthenticate los usuarios mediante sus cuentas de Active Directory local. También permite que su aplicación toosecurely consumir cualquier web API protegida por Azure AD, como Hola API de Office 365 u Hola API de Azure.

Para los clientes de Android que necesitan recursos tooaccess protegido, Azure AD proporciona Hola biblioteca de autenticación de Active Directory (ADAL). Hola único propósito de AAL es toomake más sencilla para los tokens de acceso de tooget de su aplicación. toodemonstrate lo fácil es, vamos a crear una aplicación Android lista de tareas que:

* Obtiene acceso a los tokens para llamar a una API de la lista de tareas mediante el uso de hello [protocolo de autenticación de OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Obtener listas de tareas pendientes de un usuario.
* Desconectar a los usuarios.

tooget iniciado, necesita a un inquilino de Azure AD en el que puede crear usuarios y registrar una aplicación. Si aún no tiene un inquilino, [Obtenga información acerca de cómo tooget uno](active-directory-howto-tenant.md).

## <a name="step-1-download-and-run-hello-nodejs-rest-api-todo-sample-server"></a>Paso 1: Descargue y ejecute el servidor de ejemplo de Hola tareas de API de REST de Node.js
ejemplo de Hola a tareas de API de REST de Node.js se escribe específicamente toowork en nuestro ejemplo existente para la creación de un API de REST de tareas pendientes de único inquilino para Azure AD. Se trata de un requisito previo para hello inicio rápido.

Para obtener información sobre cómo tooset este proceso, consulte nuestros ejemplos existentes en [Microsoft Azure Active Directory REST API de servicio de ejemplo para Node.js](active-directory-devquickstarts-webapi-nodejs.md).


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a>Paso 2: registre la API web con el inquilino de Azure AD
Active Directory permite agregar dos tipos de aplicaciones:

- Las API que ofrecen servicios toousers Web
- Aplicaciones (se ejecutan en web de Hola o en un dispositivo) que tienen acceso a los que las API web

En este paso, que se está registrando hello web API que se ejecutan localmente para probar este ejemplo. Normalmente, esta API web es un servicio REST que es una funcionalidad de oferta que desea que un tooaccess de aplicación. Azure AD puede ayudar a proteger cualquier punto de conexión.

Suponemos que está registrando Hola API de REST de tareas hace referencia a versiones anteriores. Pero esto funciona para cualquier API web en la que desea proteger toohelp de Active Directory de Azure.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En la barra superior de hello, haga clic en su cuenta. Hola **Directory** elija inquilino hello Azure AD en el que desea tooregister la aplicación.
3. Haga clic en **más servicios** en Hola panel izquierdo y, a continuación, seleccione **Azure Active Directory**.
4. Haga clic en **Registros de aplicaciones** y seleccione **Agregar**.
5. Escriba un nombre descriptivo para la aplicación hello (por ejemplo, **TodoListService**), seleccione **aplicación Web o API Web**y haga clic en **siguiente**.
6. Hola inicio de sesión en la dirección URL, escriba URL base Hola de ejemplo de Hola. De manera predeterminada, será `https://localhost:8080`.
7. Haga clic en **Aceptar** registro de hello toocomplete.
8. Mientras se encuentra en hello portal de Azure, ir a página de aplicación tooyour, buscar el valor de identificador de aplicación hello y cópiela. Lo necesitará más adelante cuando configure la aplicación.
9. De hello **configuración** -> **propiedades** página, actualizar la aplicación hello URI del Id.: Introduzca `https://<your_tenant_name>/TodoListService`. Reemplace `<your_tenant_name>` por nombre de hello del inquilino de Azure AD.

## <a name="step-3-register-hello-sample-android-native-client-application"></a>Paso 3: Registrar aplicación de Android Native Client de ejemplo de Hola
Debe registrar la aplicación web en este ejemplo. Esto permite que su toocommunicate de aplicación con API web recién registrado de Hola. Azure AD rechazará tooeven permitir su tooask de aplicación para inicio de sesión a menos que se registra. Que forma parte de la seguridad de hello del modelo de Hola.

Suponemos que está registrando la aplicación de ejemplo de Hola mencionado anteriormente. No obstante, este procedimiento sirve para cualquier aplicación que esté desarrollando.

> [!NOTE]
> Es posible que se pregunte por qué poner una aplicación y una API web en un mismo inquilino. Como posiblemente haya intuido, puede crear una aplicación con acceso a una API externa registrada en Azure AD desde otro inquilino. Si lo hace, sus clientes podrán solicita tooconsent toohello uso de hello API en la aplicación hello. La Biblioteca de autenticación de Active Directory para iOS se encarga de este consentimiento por usted. A medida que exploramos características más avanzadas, verá que se trata de una parte importante del conjunto de hello trabajo tooaccess necesarios Hola de APIs de Microsoft de Azure y Office, así como cualquier otro proveedor de servicio. Por ahora, ya ha registrado su API web y la aplicación sometida a Hola mismo inquilino, no verá las peticiones de consentimiento. Esto suele ser el caso de hello si está desarrollando una aplicación solo para su propio toouse de empresa.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En la barra superior de hello, haga clic en su cuenta. Hola **Directory** elija inquilino hello Azure AD en el que desea tooregister la aplicación.
3. Haga clic en **más servicios** en Hola panel izquierdo y, a continuación, seleccione **Azure Active Directory**.
4. Haga clic en **Registros de aplicaciones** y seleccione **Agregar**.
5. Escriba un nombre descriptivo para la aplicación hello (por ejemplo, **TodoListClient Android**), seleccione **aplicación cliente nativa**y haga clic en **siguiente**.
6. URI de redireccionamiento para hello, escriba `http://TodoListClient`. Haga clic en **Finalizar**
7. Página de aplicación Hola, buscar el valor de identificador de aplicación hello y cópiela. Lo necesitará más adelante cuando configure la aplicación.
8. De hello **configuración** página, seleccione **permisos necesarios** y seleccione **agregar**.  Busque y seleccione TodoListService, agregue hello **acceso TodoListService** permiso en **permisos delegados**y haga clic en **realiza**.

toobuild con Maven, puede usar pom.xml en el nivel superior de hello:

1. Clone este repositorio en el directorio que desee:

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. Siga los pasos de Hola Hola [tooset de requisitos previos del entorno de Maven para Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).
3. Configurar el emulador de hello con SDK 19.
4. Vaya a carpeta de raíz de toohello donde clonó repositorio Hola.
5. Ejecute este comando: `mvn clean install`
6. Cambiar directorio toohello inicio rápido muestra de Hola a:`cd samples\hello`
7. Ejecute este comando: `mvn android:deploy android:run`

   Debería ver la aplicación a partir de Hola.
8. Escriba tootry de credenciales de usuario de prueba.

Se van a enviar paquetes JAR junto a paquetes de saludo AAR.

## <a name="step-4-download-hello-android-adal-and-add-it-tooyour-eclipse-workspace"></a>Paso 4: Descargar Hola Android AAL y agregar área de trabajo de Eclipse tooyour
Que hemos hecho fácil para toohave varias opciones toouse ADAL en el proyecto de Android:

* Puede usar esta biblioteca de tooimport de código de origen de hello en Eclipse y vínculo tooyour una aplicación.
* Si usa Android Studio, puede usar Hola AAR paquete formato y referencia Hola archivos binarios.

### <a name="option-1-source-zip"></a>Opción 1: origen a través de ZIP
toodownload una copia del código fuente de hello, haga clic en **Download ZIP** en hello derecha de la página de Hola. También puede [descargarla desde GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).

### <a name="option-2-source-via-git"></a>Opción 2: origen a través de Git
código de origen de hello tooget de hello SDK mediante Git, escriba:

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a>Opción 3: binarios a través de Gradle
Puede obtener los archivos binarios de Hola de repositorio central de hello Maven. paquete de AAR Hola se puede incluir los siguientes en el proyecto en Android Studio:

```gradle
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
}
```

### <a name="option-4-aar-via-maven"></a>Opción 4: AAR a través de Maven
Si usas hello M2Eclipse complemento, puede especificar dependencias de hello en el archivo pom.xml:

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-hello-libs-folder"></a>Opción 5: Paquete JAR dentro de la carpeta de bibliotecas de Hola
Puede obtener archivo JAR de hello de repositorio de Maven hello y colóquelo en hello **bibliotecas** carpeta del proyecto. Necesita toocopy Hola requiere recursos tooyour project, porque no incluyen paquetes de saludo JAR.

## <a name="step-5-add-references-tooandroid-adal-tooyour-project"></a>Paso 5: Agregar proyecto de referencias tooAndroid tooyour ADAL
1. Agregue una referencia de proyecto de tooyour y especificarla como una biblioteca de Android. Si no está seguro cómo toodo esto, puede obtener más información sobre hello [sitio Android Studio](http://developer.android.com/tools/projects/projects-eclipse.html).
2. Agregar dependencia de proyecto de hello para la depuración en la configuración del proyecto.
3. Actualizar tooinclude de archivo AndroidManifest.xml del proyecto:

        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <application
            android:allowBackup="true"
            android:debuggable="true"
            android:icon="@drawable/ic_launcher"
            android:label="@string/app_name"
            android:theme="@style/AppTheme" >

            <activity
                android:name="com.microsoft.aad.adal.AuthenticationActivity"
                android:label="@string/title_login_hello_app" >
            </activity>
            ....
        <application/>

4. Cree una instancia de AuthenticationContext en la actividad principal. detalles de Hola de esta llamada son más allá del ámbito de Hola de este tema, pero puede empezar a trabajar examinando hello [ejemplo de Android Native Client](https://github.com/AzureADSamples/NativeClient-Android). En el siguiente ejemplo de Hola, SharedPreferences es la memoria caché predeterminada de Hola y entidad está en forma de Hola de `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. Copie este extremo de Hola de toohandle de bloque de código de AuthenticationActivity después de usuario de hello escribe las credenciales y recibe un código de autorización:

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. tooask para un token, defina una devolución de llamada:

        private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {

            @Override
            public void onError(Exception exc) {
                if (exc instanceof AuthenticationException) {
                    textViewStatus.setText("Cancelled");
                    Log.d(TAG, "Cancelled");
                } else {
                    textViewStatus.setText("Authentication error:" + exc.getMessage());
                    Log.d(TAG, "Authentication error:" + exc.getMessage());
                }
            }

            @Override
            public void onSuccess(AuthenticationResult result) {
                mResult = result;

                if (result == null || result.getAccessToken() == null
                        || result.getAccessToken().isEmpty()) {
                    textViewStatus.setText("Token is empty");
                    Log.d(TAG, "Token is empty");
                } else {
                    // request is successful
                    Log.d(TAG, "Status:" + result.getStatus() + " Expired:"
                            + result.getExpiresOn().toString());
                    textViewStatus.setText(PASSED);
                }
            }
        };

7. Por último, solicite un token mediante esa devolución de llamada:

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

Aquí se muestra una explicación de los parámetros de hello:

* *recursos* es necesaria y recursos de Hola que está tratando de tooaccess.
* *clientid* es necesario. Su valor procede de Azure AD.
* *RedirectUri* no es necesario toobe proporcionada para la llamada de acquireToken Hola. Se puede configurar como el nombre del paquete.
* *PromptBehavior* le ayuda a tooask para caché de credenciales tooskip hello y cookies.
* *devolución de llamada* se llama después de código de autorización de Hola se intercambia para un token. La devolución de llamada tiene un objeto de AuthenticationResult que tiene acceso al token, fecha de caducidad e información sobre el token del identificador.
* *acquireTokenSilent* es opcional. Puede llamarlo toohandle almacenamiento en caché y la actualización del token. También proporciona la versión de sincronización de Hola. Acepta *userId* como parámetro.

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

Mediante el uso de este tutorial, debe tener lo que necesita toosuccessfully integrar con Azure Active Directory. Para obtener más ejemplos de este trabajo, visite hello AzureADSamples / repositorio en GitHub.

## <a name="important-information"></a>Información importante
### <a name="customization"></a>Personalización
Los recursos de la aplicación pueden sobrescribir a los recursos del proyecto de la biblioteca. Esto sucede cuando la aplicación se está generando. Por este motivo, puede personalizar la autenticación actividad diseño Hola que quieras. Ser seguro tookeep Hola ID de controles de Hola que AAL usa (WebView).

### <a name="broker"></a>Agente
aplicación de Portal de empresa de Microsoft Intune Hello proporciona componentes de broker de Hola. se crea la cuenta de Hello en el Administrador de cuentas. tipo de cuenta de Hello es "com.microsoft.workaccount." El administrador de cuentas únicamente permite una sola cuenta SSO. Crea una cookie SSO para el usuario Hola después de completar el desafío de dispositivo de Hola para una de las aplicaciones de Hola.

AAL usa la cuenta del agente de Hola si se crea una cuenta de usuario en este autenticador y elige no tooskip lo. Puede omitir el usuario de broker de hello con:

   `AuthenticationSettings.Instance.setSkipBroker(true);`

Deberá tooregister un RedirectUri especial para el uso de broker. RedirectUri está en formato de Hola de `msauth://packagename/Base64UrlencodedSignature`. Puede obtener su RedirectUri de la aplicación mediante brokerRedirectPrint.ps1 de script de Hola u Hola API llamada mContext.getBrokerRedirectUri. firma de Hello es relacionado tooyour certificados de firma.

modelo de broker actual Hello es para un usuario. AuthenticationContext proporciona el usuario de broker de hello API método tooget Hola.

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

El manifiesto de aplicación debe tener Hola siguiendo las cuentas de administrador de cuentas de toouse de permisos. Para obtener más información, vea hello [información del Administrador de cuentas en el sitio de Android hello](http://developer.android.com/reference/android/accounts/AccountManager.html).

* GET_ACCOUNTS
* USE_CREDENTIALS
* MANAGE_ACCOUNTS

### <a name="authority-url-and-ad-fs"></a>AD FS y URL de la autoridad
Los servicios de federación de Active Directory (AD FS) no se reconoce como producción STS, por lo que necesita tooturn de detección de instancia y pase el valor false en el constructor de AuthenticationContext Hola.

dirección URL de la entidad emisora de Hello necesita una instancia de STS y un [nombre del inquilino](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).

### <a name="querying-cache-items"></a>Consulta de los elementos en caché
ADAL proporciona memoria caché predeterminada en SharedPreferences con algunas características sencillas para hacer consultas sobre los elementos en caché. Puede obtener de caché actual Hola de AuthenticationContext mediante:

    ITokenCacheStore cache = mContext.getCache();

También puede proporcionar la implementación de la memoria caché, si desea que toocustomize lo.

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a>Comportamiento de la petición
AAL proporciona un comportamiento de solicitud de toospecify de opción. PromptBehavior.Auto mostrará Hola interfaz de usuario si no es válido el token de actualización de Hola y se necesitan credenciales de usuario. PromptBehavior.Always se omita el uso de la memoria caché de Hola y mostrar siempre Hola interfaz de usuario.

### <a name="silent-token-request-from-cache-and-refresh"></a>Solicitud de token silenciosa desde la memoria caché y actualización
Una solicitud de token silenciosa no utiliza Hola emergente de la interfaz de usuario y no requiere una actividad. Devuelve un token de caché de hello si está disponible. Si expira el token de hello, este método intenta toorefresh lo. Si el token de actualización de hello está caducado o no correctamente, devuelve AuthenticationException.

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

También puede hacer una llamada de sincronización con este método. Puede establecer toocallback null o usar acquireTokenSilentSync.

### <a name="diagnostics"></a>Diagnóstico
Estas son las principales fuentes de Hola de información para diagnosticar problemas:

* Excepciones
* Registros
* Seguimientos de red

Tenga en cuenta que los identificadores de correlación son diagnósticos toohello central en la biblioteca de Hola. Puede establecer los identificadores de correlación en cada solicitud si desea toocorrelate una ADAL solicitar con otras operaciones en el código. Si no establece un identificador de correlación, ADAL generará uno aleatorio. Todos los mensajes de registro y llamadas de red, a continuación, se mostrarán con el identificador de correlación de Hola. Hola autogenerado Id. los cambios en cada solicitud.

#### <a name="exceptions"></a>Excepciones
Las excepciones son Hola primero diagnóstico. Intentamos tooprovide mensajes de error útiles. Si encuentra alguno que no sea útil, genere un caso y háganoslo saber. Proporcione también información sobre el dispositivo, por ejemplo, el modelo y el número de SDK.

#### <a name="logs"></a>Registros
Puede configurar Hola biblioteca toogenerate mensajes de registro que se puede usar toohelp diagnosticar problemas. Configurar el registro realizar Hola siguiente llamada a tooconfigure que AAL utilizará toohand desactivar cada mensaje del registro cuando se genera una devolución de llamada.

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this toolog file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

Se pueden escribir mensajes tooa archivo de registro personalizado, como se muestra en el siguiente código de hello. Por desgracia, no hay ninguna manera estándar de obtener los registros de un dispositivo. Hay algunos servicios que pueden ayudar con esta tarea. También puede inventar su propio, como servidor de tooa de archivo hello envío.

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

Estos son los niveles de registro de hello:
* Error (excepciones)
* Warn (advertencia)
* Info (información)
* Verbose (más detalles)

Establecer el nivel de registro de hello similar al siguiente:

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 Todos los mensajes de registro se envían toologcat, en las devoluciones de llamada de adición tooany registro personalizado.
Puede obtener un archivo de registro de tooa desde logcat como se indica a continuación:

    adb logcat > "C:\logmsg\logfile.txt"

 Para obtener más información acerca de los comandos de adb, vea hello [logcat información en el sitio de Android hello](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).

#### <a name="network-traces"></a>Seguimientos de red
Puede utilizar diversas herramientas toocapture Hola tráfico HTTP que genera AAL.  Esto es muy útil si está familiarizado con el protocolo OAuth Hola o si necesita tooprovide información de diagnóstico tooMicrosoft u otros canales de soporte técnico.

Fiddler es la herramienta de seguimiento de HTTP más sencilla de Hola. Siguientes de Hola de uso vínculos tooset, configúrelo toocorrectly registro AAL tráfico de red. Para obtener una herramienta de seguimiento como Fiddler o Charles toobe útil, debe configurarlo toorecord sin cifrar el tráfico SSL.  

> [!NOTE]
> Los seguimientos generados de esta manera pueden contener información altamente privilegiada, como tokens de acceso, nombres de usuario y contraseñas. Si utiliza cuentas de producción, no comparta esta información con terceras partes. Si necesita toosupply un toosomeone de seguimiento en la compatibilidad de orden tooget, reproduzca el problema de hello mediante una cuenta temporal con nombres de usuario y contraseñas que no le importa de uso compartido.

* Desde el sitio Web de Telerik hello: [configuración de seguridad de Fiddler para Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)
* En GitHub, consulte cómo [configurar reglas de Fiddler para ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler).

### <a name="dialog-mode"></a>Modo de diálogo
método de acquireToken de Hello sin actividad es compatible con un símbolo del sistema del cuadro de diálogo.

### <a name="encryption"></a>Cifrado
AAL cifra los tokens de Hola y almacén en SharedPreferences de forma predeterminada. Puede buscar en los detalles de Hola Hola StorageHelper clase toosee. Android introdujo el almacenamiento seguro de claves privadas AndroidKeyStore 4.3 (API18). ADAL lo utiliza para API 18 y las versiones posteriores. Si desea toouse AAL para las versiones inferiores de SDK, deberá tooprovide una clave secreta en AuthenticationSettings.INSTANCE.setSecretKey.

### <a name="oauth2-bearer-challenge"></a>Desafío de portador de Oauth2
Hola AuthenticationParameters clase proporciona funcionalidad tooget authorization_uri de hello desafío de portador de OAuth2.

### <a name="session-cookies-in-webview"></a>Cookies de sesión en WebView
Android WebView no borra las cookies de sesión después de cerrar la aplicación hello. Esto puede controlarse mediante el siguiente código de ejemplo:

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

Para obtener más información acerca de las cookies, consulte hello [CookieSyncManager información en el sitio de Android hello](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).

### <a name="resource-overrides"></a>Reemplazos de recursos
biblioteca ADAL de Hello incluye cadenas en inglés para los mensajes de ProgressDialog. La aplicación debe sobrescribirlas si desea ver las cadenas traducidas.

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a>Cuadro de diálogo NTLM
AAL versión 1.1.0 admite un cuadro de diálogo NTLM que se procesa a través de eventos de hello onReceivedHttpAuthRequest desde WebViewClient. Puede personalizar el diseño de Hola y cadenas para el cuadro de diálogo de Hola.

### <a name="cross-app-sso"></a>SSO entre aplicaciones
Obtenga información acerca de [cómo tooenable SSO de aplicación cruzado en Android mediante el uso de ADAL](active-directory-sso-android.md).  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
