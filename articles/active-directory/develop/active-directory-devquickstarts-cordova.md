---
title: "aaaAzure AD Cordova Introducción | Documentos de Microsoft"
description: "Cómo toobuild una aplicación de Cordova que se integra con Azure AD para inicio de sesión y llama a las API de protegido por AD Azure mediante el uso de OAuth."
services: active-directory
documentationcenter: 
author: vibronet
manager: mbaldwin
editor: 
ms.assetid: b1a8d7bd-7ad6-44d5-8ccb-5255bb623345
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: vittorib
ms.custom: aaddev
ms.openlocfilehash: 573ed638c2180c5231648bcb8c49ceb6f53296f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a>Integración de Azure AD con una aplicación Apache Cordova
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Puede usar las aplicaciones de Apache Cordova toodevelop HTML5 y JavaScript que se pueden ejecutar en dispositivos móviles como aplicaciones nativas completas. Con Azure Active Directory (Azure AD), puede agregar aplicaciones de Cordova de tooyour de las capacidades de autenticación de empresarial.

Un complemento Cordova ajusta los SDK nativos de Azure AD en iOS, Android, la Tienda Windows y Windows Phone. Mediante el complemento, puede mejorar el inicio de sesión toosupport de aplicación con cuentas de Active Directory de Windows Server de los usuarios, obtener acceso tooOffice 365 y las API de Azure e incluso ayudar a proteger web personalizado propio de tooyour de llamadas API.

En este tutorial, usaremos Hola Apache Cordova complemento para la biblioteca de autenticación de Active Directory (ADAL) tooimprove una aplicación sencilla mediante la adición de hello siguientes características:

* Con solo unas líneas de código, autenticar a un usuario y obtener un token.
* Usar ese tooquery de API Graph de hello tooinvoke símbolo (token) de ese directorio y mostrar los resultados de Hola.  
* Utilizar autenticación de toominimize de caché de tokens AAL Hola solicita usuario Hola.

toomake esas mejoras, necesita:

1. Registrar una aplicación con Azure AD.
2. Agregue código tooyour aplicación toorequest tokens.
3. Agregar código toouse Hola token para consultar Hola API Graph y mostrar los resultados.
4. Crear proyecto de implementación de hello Cordova con todas las plataformas de hello desea tootarget, agregar complemento Cordova AAL hello y probar soluciones de hello en emuladores.

## <a name="prerequisites"></a>Requisitos previos
toocomplete este tutorial, necesita:

* Un inquilino de Azure AD que disponga de una cuenta con derechos de desarrollo de aplicaciones.
* Un entorno de desarrollo que ha configurado toouse Apache Cordova.  

Si tiene tanto ya configurado, tener acceso directamente toostep 1.

Si no tiene un inquilino de Azure AD, use hello [obtener instrucciones sobre cómo tooget uno](active-directory-howto-tenant.md).

Si no dispone de Apache Cordova configurado en su equipo, instalar Hola siguientes:

* [Git](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [Node.js](https://nodejs.org/download/)
* [Interfaz de línea de comandos Cordova](https://cordova.apache.org/) (se instala fácilmente mediante el administrador de paquetes NPM: `npm install -g cordova`)

Hola anterior instalaciones debería funcionar en hello PC y en hello Mac.

Cada plataforma de destino tiene diferentes requisitos previos:

* toobuild y ejecutar una aplicación para Tabletas de Windows o Windows Phone:
  * Instale [Visual Studio 2013 para Windows con la actualización 2 o posterior](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express u otra versión) o [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).

* toobuild y ejecutar una aplicación para iOS:

  * Instale Xcode 6.x o una versión posterior. Descargar de hello [sitio para desarrolladores de Apple](http://developer.apple.com/downloads) o hello [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).
  * Instale [ios-sim](https://www.npmjs.org/package/ios-sim). Puede usarlo toostart aplicaciones de iOS en el simulador de iOS desde la línea de comandos de Hola. (Se puede instalar fácilmente a través de terminal hello: `npm install -g ios-sim`.)
* toobuild y ejecutar una aplicación para Android:

  * Instale el [Kit de desarrollo de Java (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) o una versión posterior. Asegúrese de que `JAVA_HOME` (variable de entorno) se ha configurado correctamente según la ruta de acceso de la instalación de JDK toohello (por ejemplo, C:\Program Files\Java\jdk1.7.0_75).
  * Instalar [SDK de Android](http://developer.android.com/sdk/installing/index.html?pkg=tools) y agregue hello `<android-sdk-location>\tools` tooyour de ubicación (por ejemplo, C:\tools\Android\android-sdk\tools) `PATH` variable de entorno.
  * Abra el Administrador de Android SDK (por ejemplo, a través de hello terminal: `android`) e instalar:
    * *Android 5.0.1 (API 21)*
    * *Herramientas de compilación de SDK de Android*, versión 19.1.0 o posterior
    * *Repositorio compatible con Android* (extras)

  Hola SDK de Android no proporciona ninguna instancia del emulador predeterminada. Crear uno mediante la ejecución de `android avd` de hello terminal y, a continuación, seleccione **crear**, si desea que la aplicación de Android toorun hello en un emulador. Se recomienda un nivel de API de 19 o superior. Para obtener más información acerca de las opciones de creación y el emulador de Android hello, consulte [administrador AVD](http://developer.android.com/tools/help/avd-manager.html) en el sitio de hello Android.

## <a name="step-1-register-an-application-with-azure-ad"></a>Paso 1: Registro de una aplicación con Azure AD
Este paso es opcional. Este tutorial proporciona valores aprovisionados previamente que puede usar toosee Hola ejemplo en acción sin tener que realizar cualquier aprovisionamiento en su propio inquilino. Sin embargo, recomendamos que realice este paso y familiarizarse con el proceso de hello, ya que será necesaria al crear sus propias aplicaciones.

Azure AD emite tooonly tokens conocida las aplicaciones. Para poder usar Azure AD desde la aplicación, debe toocreate una entrada para él en el inquilino. tooregister una nueva aplicación en su inquilino:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En la barra superior de hello, haga clic en su cuenta. Hola **Directory** elija inquilino hello Azure AD en el que desea tooregister la aplicación.
3. Haga clic en **más servicios** en Hola panel izquierdo y, a continuación, seleccione **Azure Active Directory**.
4. Haga clic en **Registros de aplicaciones** y seleccione **Agregar**.
5. Siga las indicaciones de Hola y crear un **aplicación cliente nativa**. (Aunque las aplicaciones Cordova están basadas en HTML, aquí estamos creando una aplicación cliente nativa. Hola **aplicación cliente nativa** opción debe estar seleccionada o aplicación hello no funcionará.)
  * **Nombre** describe su toousers de aplicación.
  * **URI de redireccionamiento** es hello URI que se usa tooreturn tokens tooyour aplicación. Escriba **http://MyDirectorySearcherApp**.

Cuando termine de registro, Azure AD le asigna una aplicación de tooyour de Id. de aplicación exclusivo. Necesitará este valor en las secciones siguientes se Hola. Puede encontrarlo en pestaña de aplicación Hola de Hola que acaba de crear aplicaciones.

toorun `DirSearchClient Sample`, conceder Hola recién creado aplicación permiso tooquery hello Azure AD Graph API:

1. De hello **configuración** página, seleccione **permisos necesarios**y, a continuación, seleccione **agregar**.  
2. Para aplicaciones de Azure Active Directory de hello, seleccione **Microsoft Graph** como Hola API y agregar hello **obtener acceso al directorio de hello como usuario con sesión iniciada hello** permiso en **delegados Permisos**.  Esto permite que su Hola de tooquery aplicación API Graph para los usuarios.

## <a name="step-2-clone-hello-sample-app-repository"></a>Paso 2: Clonar el repositorio de aplicación de ejemplo de Hola
Desde el shell o la línea de comandos, escriba Hola siguiente comando:

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-hello-cordova-app"></a>Paso 3: Crear la aplicación de Cordova hello
Hay varias aplicaciones de Cordova toocreate de formas. En este tutorial, vamos a usar la interfaz de línea de comandos de hello Cordova (CLI).

1. Desde el shell o la línea de comandos, escriba Hola siguiente comando:

        cordova create DirSearchClient

   Ese comando crea la estructura de carpetas de Hola y scaffolding de proyecto de Cordova Hola.

2. Mover la nueva carpeta de DirSearchClient de toohello:

        cd .\DirSearchClient

3. Copiar el contenido de Hola Hola del proyecto de inicio en la subcarpeta de hello World Wide Web mediante un administrador de archivos u Hola siguiente comando en el shell:

  * Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`
  * Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`

4. Agregar lista aprobada de hello complemento. Esto es necesario para invocar Hola API Graph.

        cordova plugin add cordova-plugin-whitelist

5. Agregue todas las plataformas de Hola que desea toosupport. toohave un ejemplo funcional, deberá tooexecute al menos uno de hello siga los comandos. Tenga en cuenta que no puede tooemulate capaz de iOS en Windows o emular Windows en un equipo Mac.

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. Agregue hello AAL para el proyecto de complemento tooyour Cordova:

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-tooauthenticate-users-and-obtain-tokens-from-azure-ad"></a>Paso 4: Agregar código tooauthenticate usuarios y obtener tokens de Azure AD
aplicación de Hola que va a desarrollar en este tutorial proporcionará una característica de búsqueda de directorio sencillo. usuario Hola puede, a continuación, escriba el alias de Hola de cualquier usuario en el directorio de Hola y visualizar algunos atributos básicos. proyecto de inicio de Hello contiene la definición de Hola de interfaz de usuario básica de saludo de la aplicación hello (en www/index.html) y scaffolding de Hola que conecta los eventos de aplicación básico ciclos, enlaces de la interfaz de usuario y los resultados de la lógica de presentación (en www/js/index.js). Hello única tarea que queda para usted es tooadd Hola lógica que implementa las tareas de identidad.

Hello en primer lugar deberá toodo en el código es introducir los valores de protocolo de Hola que Azure AD usa para identificar la aplicación y Hola recursos de destino. Dichos valores serán solicitudes de token de hello tooconstruct usado más adelante. Inserte Hola siguiente fragmento de código al principio de hello del archivo de index.js de hello:

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

Hola `redirectUri` y `clientId` valores deben coincidir con los valores de hello que describen la aplicación en Azure AD. Los de hello encontrará **configurar** ficha Hola portal de Azure, tal como se describe en el paso 1 anteriormente en este tutorial.

> [!NOTE]
> Si ha optado por no registrar una nueva aplicación en su propio inquilino, simplemente puede pegar valores de hello preconfigurado tal cual. A continuación, puede ver ejecutando de ejemplo de Hola, aunque siempre se debe crear su propia entrada para las aplicaciones que están diseñadas para entornos de producción.

A continuación, agregue el código de la solicitud de token de Hola. Insertar Hola siguiente fragmento de código entre hello `search` y `renderData` definiciones:

```javascript
    // Shows hello user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
        });

    },
```
Examinemos esa función dividiéndola en dos partes principales.
Este ejemplo es toowork diseñada con todos los inquilinos, como opuesto toobeing había vinculada tooa uno determinado. Usa Hola "/ comunes" punto de conexión, que permite cualquier cuenta de hello tooenter de usuario en tiempo de autenticación y dirige el inquilino de hello solicitud toohello donde pertenece.

Esta primera parte del método hello inspecciona Hola caché AAL toosee si ya se almacena un token. Si es así, método hello usa a los inquilinos de Hola procedencia de token de Hola para reinicializar AAL. Esto es necesario tooavoid mensajes adicionales, porque Hola uso de "/ comunes" siempre da lugar a pedir Hola usuario tooenter una nueva cuenta.

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
segunda parte del método hello de Hello realiza la solicitud de token adecuado de Hola. Hola `acquireTokenSilentAsync` método pide AAL tooreturn un token de hello especificada recursos sin mostrar ninguna UX. Que puede producirse si caché Hola ya tiene un token de acceso adecuado almacenado, o si un token de actualización se puede usa tooget un nuevo token de acceso sin mostrar ningún mensaje. Si no lo consigue, se reviertan `acquireTokenAsync`--visiblemente que solicitará hello tooauthenticate de usuario.

```javascript
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
```
Ahora que tenemos token hello, finalmente podemos invocar Hola API Graph y realizar consultas de búsqueda de Hola que queremos. Insertar Hola siguiente fragmento de código siguiente hello `authenticate` definición:

```javascript
// Makes an API call tooreceive hello user list
    requestData: function (authResult, searchText) {
        var req = new XMLHttpRequest();
        var url = resourceUri + "/" + authResult.tenantId + "/users?api-version=" + graphApiVersion;
        url = searchText ? url + "&$filter=mailNickname eq '" + searchText + "'" : url + "&$top=10";

        req.open("GET", url, true);
        req.setRequestHeader('Authorization', 'Bearer ' + authResult.accessToken);

        req.onload = function(e) {
            if (e.target.status >= 200 && e.target.status < 300) {
                app.renderData(JSON.parse(e.target.response));
                return;
            }
            app.error('Data request failed: ' + e.target.response);
        };
        req.onerror = function(e) {
            app.error('Data request failed: ' + e.error);
        }

        req.send();
    },

```
archivos de punto de partida de Hello proporcionar experiencia del usuario simple para escribir el alias del usuario en un cuadro de texto. Este método utiliza ese valor tooconstruct una consulta, combinarla con el token de acceso de hello, enviar tooMicrosoft gráfico y analizar los resultados de Hola. Hola `renderData` método, ya está presente en el archivo de punto de partida de hello, se encarga de visualizar los resultados de Hola.

## <a name="step-5-run-hello-app"></a>Paso 5: Ejecutar la aplicación hello
La aplicación es toorun llegado el momento. Resulte sencillo: cuando se inicia la aplicación hello, escriba Hola alias del usuario de hello desea toolook y, a continuación, haga clic en botón Hola. Se le pedirá que se autentique. Tras la autenticación correcta y búsqueda correcta, se muestran los atributos de Hola de hello buscada usuario.

Las ejecuciones posteriores llevará a cabo búsqueda Hola sin mostrar ningún mensaje, gracias toohello presencia de hello previamente adquiere token en memoria caché.

pasos concretos de Hola para ejecutar la aplicación hello varían según la plataforma.

### <a name="windows-10"></a>Windows 10
   Tableta/PC: `cordova run windows --archs=x64 -- --appx=uap`

   Dispositivo móvil (requiere una tooa de dispositivo conectado PC de Windows 10 Mobile):`cordova run windows --archs=arm -- --appx=uap --phone`

   > [!NOTE]
   > Durante el saludo ejecuta por primera vez, podría se te pedirán toosign en una licencia de desarrollador. Para más información, consulte el artículo sobre la [licencia de desarrollador](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).

### <a name="windows-81-tabletpc"></a>Tableta/PC con Windows 8.1
   `cordova run windows`

   > [!NOTE]
   > Durante el saludo ejecuta por primera vez, podría se te pedirán toosign en una licencia de desarrollador. Para más información, consulte el artículo sobre la [licencia de desarrollador](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).

### <a name="windows-phone-81"></a>Windows Phone 8,1
   toorun en un dispositivo conectado:`cordova run windows --device -- --phone`

   toorun en el emulador de hello predeterminado:`cordova emulate windows -- --phone`

   Use `cordova run windows --list -- --phone` toosee todos los destinos disponibles y `cordova run windows --target=<target_name> -- --phone` toorun aplicación de hello en un emulador o dispositivo específico (por ejemplo, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).

### <a name="android"></a>Android
   toorun en un dispositivo conectado:`cordova run android --device`

   toorun en el emulador de hello predeterminado:`cordova emulate android`

   Asegúrese de que ha creado una instancia del emulador mediante el administrador AVD, tal y como se describió anteriormente en la sección "Requisitos previos" Hola.

   Use `cordova run android --list` toosee todos los destinos disponibles y `cordova run android --target=<target_name>` toorun aplicación de hello en un emulador o dispositivo específico (por ejemplo, `cordova run android --target="Nexus4_emulator"`).

### <a name="ios"></a>iOS
   toorun en un dispositivo conectado:`cordova run ios --device`

   toorun en el emulador de hello predeterminado:`cordova emulate ios`

   > [!NOTE]
   > Asegúrese de que tienen hello `ios-sim` toorun paquete instalado en el emulador de Hola. Para obtener más información, vea Hola "requisitos previos" sección.

    Use `cordova run ios --list` toosee all available targets and `cordova run ios --target=<target_name>` toorun hello application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` toosee additional build and run options.

## <a name="next-steps"></a>Pasos siguientes
Como referencia, está disponible en el ejemplo de Hola finalizado (sin los valores de configuración) [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).

Puede que ahora los escenarios de movimiento en toomore avanzada (y más interesantes). Es recomendable tootry: [proteger una API Web de Node.js con Azure AD](active-directory-devquickstarts-webapi-nodejs.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
