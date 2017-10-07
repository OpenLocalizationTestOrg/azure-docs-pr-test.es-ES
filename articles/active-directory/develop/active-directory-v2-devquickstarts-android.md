---
title: "aplicación de Android v2.0 aaaAzure Active Directory | Documentos de Microsoft"
description: "¿Cómo toobuild una aplicación Android que inicia sesión a los usuarios con personal cuenta Microsoft y trabajo o escolares y llamadas Hola API Graph mediante el uso de bibliotecas de terceros."
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 16294c07-f27d-45c9-833f-7dbb12083794
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1dd40bd3bcea28c629abce09abaed66b38774162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-android-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a>Agregar aplicación para Android tooan inicio de sesión mediante una biblioteca de terceros con API Graph con el punto de conexión de hello v2.0
plataforma de identidad de Microsoft Hello usa estándares abiertos como OAuth2 y OpenID Connect. Los desarrolladores pueden usar cualquier biblioteca que deseen toointegrate con nuestros servicios. toohelp a los desarrolladores usar nuestra plataforma con otras bibliotecas, hemos escrito algunos tutoriales como este uno toodemonstrate la plataforma de identidad de Microsoft de tooconfigure bibliotecas de otros fabricantes tooconnect toohello. La mayoría de las bibliotecas que implementan [especificación de hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) toohello plataforma de identidad de Microsoft se pueden conectar.

Con una aplicación Hola que crea en este tutorial, los usuarios pueden iniciar sesión en la organización de tootheir y, a continuación, buscar por sí mismos en su organización mediante Hola API Graph.

Si es nuevo tooOAuth2 u OpenID Connect, gran parte de esta configuración de ejemplo puede que no tenga sentido tooyou. Si este es el caso, es aconsejable que lea [Protocolos de la versión 2.0: Flujo de código de autorización de OAuth 2.0](active-directory-v2-protocols-oauth-code.md).

> [!NOTE]
> Algunas características de la plataforma que tiene una expresión en Hola OAuth2 o estándares de OpenID Connect, como acceso condicional y administración de directivas de Intune, requieren toouse nuestro código abierto bibliotecas de identidad de Microsoft Azure.
> 
> 

el punto de conexión de Hello v2.0 no admite todas las características y escenarios de Azure Active Directory.

> [!NOTE]
> toodetermine si debe utilizar Hola v2.0 extremo, que conozca [v2.0 limitaciones](active-directory-v2-limitations.md).
> 
> 

## <a name="download-hello-code-from-github"></a>Descargar código de hello desde GitHub
código de Hello para este tutorial se mantiene [en GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).  toofollow a lo largo, puede [descargar el esqueleto de la aplicación hello como .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) o esqueleto de Hola de clon:

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

También se puede descargar el ejemplo de Hola y empezar a trabajar de forma inmediata:

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a>Registrar una aplicación
Crear una nueva aplicación en hello [portal de registro de aplicación](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), o siga Hola pasos detallados en [cómo una aplicación con el punto de conexión de hello v2.0 tooregister](active-directory-v2-app-registration.md).  Asegúrese de que:

* Hola copia **identificador de la aplicación** que está asignado tooyour aplicación porque lo necesitará pronto.
* Agregar hello **Mobile** plataforma para la aplicación.

> Nota: portal de registro de aplicación Hola proporciona un **URI de redireccionamiento** valor. Sin embargo, en este ejemplo debe usar valor predeterminado de Hola de `https://login.microsoftonline.com/common/oauth2/nativeclient`.
> 
> 

## <a name="download-hello-nxoauth2-third-party-library-and-create-a-workspace"></a>Descargar la biblioteca de otro fabricante NXOAuth2 hello y crear un área de trabajo
En este tutorial, usará hello OIDCAndroidLib desde GitHub, que es una biblioteca de OAuth2 basada en hello código OpenID Connect de Google. Implementa el perfil de aplicación nativa de Hola y es compatible con el extremo de autorización de saludo del usuario de Hola. Éstos son todos los puntos de Hola que necesitará toointegrate a la plataforma de identidad de Microsoft de Hola.

Clonar equipo tooyour de hello OIDCAndroidLib repositorio.

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![androidStudio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a>Configuración del entorno de Android Studio
1. Crear un nuevo proyecto de Android Studio y acepte los valores predeterminados de hello en el Asistente de Hola.
   
    ![Creación de un nuevo proyecto de Android Studio](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![Dispositivos Android de destino](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![Agregar una actividad toomobile](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. tooset de los módulos de proyecto, mover ubicación del proyecto de hello clonar repositorio toohello. También puede crear proyecto hello y, a continuación, clonarlo directamente toohello ubicación del proyecto.
   
    ![Módulos del proyecto](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. Abrir configuración de módulos de hello proyecto mediante el menú contextual de Hola o utilizando el método abreviado Ctrl + Alt + rincipales + S de Hola.
   
    ![Configuración de los módulos del proyecto](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. Quite el módulo de aplicación de hello predeterminada porque solo se desea configuración Hola del contenedor de proyecto.
   
    ![módulo de aplicación de Hello predeterminado](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. Importar módulos desde el proyecto actual de hello repositorio clonado toohello.
   
    ![Proyecto de importación gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![crear una nueva página de módulo](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)
6. Repita estos pasos para hello `oidlib-sample` módulo.
7. Comprobar las dependencias de oidclib hello en hello `oidlib-sample` módulo.
   
    ![dependencias de oidclib en el módulo de oidlib ejemplo de Hola](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. Haga clic en **Aceptar** y espere a que se inicie sincronización de gradle.
   
    El archivo settings.gradle debe ser similar a este:
   
    ![Captura de pantalla de settings.gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. Generar toomake de aplicación de ejemplo de Hola seguro ese ejemplo Hola ejecutando correctamente.
   
    No será capaz de toouse esto con Azure Active Directory todavía. Necesitaremos tooconfigure algunos puntos de conexión en primer lugar. Se trata de tooensure no tiene un problemas Android Studio antes de empezar a personalizar la aplicación de ejemplo de Hola.
10. Compile y ejecute `oidlib-sample` como destino de hello en Android Studio.
    
    ![Progreso de la compilación oidlib-sample](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. Eliminar hello `app ` directorio que se dejó cuando quita el módulo de Hola de proyecto Hola porque Android Studio no se elimina, por motivos de seguridad.
    
    ![Estructura del archivo que incluye el directorio de aplicación Hola](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. Abra hello **editar configuraciones** tooremove Hola ejecutar configuración de menú del que también se dejó cuando quita el módulo de Hola de proyecto Hola.
    
    ![Menú Editar configuración](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![Ejecutar configuración de aplicación](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)

## <a name="configure-hello-endpoints-of-hello-sample"></a>Configurar los extremos de Hola de ejemplo de Hola
Ahora que tiene hello `oidlib-sample` ejecuta correctamente, editar algunos puntos de conexión tooget este trabajo con Azure Active Directory.

### <a name="configure-your-client-by-editing-hello-oidcclientconfxml-file"></a>Configurar al cliente mediante la edición de archivos de hello oidc_clientconf.xml
1. Dado que usa OAuth2 flujos solo tooget un token y llamar a la API Graph hello, establecer cliente toodo OAuth2 de hello solo. El uso de OIDC se tratará en un ejemplo posterior.
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. Configure su ID de cliente que recibió del portal de registro de hello.
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. A continuación, configure el URI de redirección con hello uno.
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. Configurar los ámbitos que se necesita en orden tooaccess Hola API Graph.
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

Hola `User.Read` valor en `oidc_scopes` permite tooread Hola perfil básico Hola firmado en usuario.
Puede aprender más acerca de todos los ámbitos disponibles de hello en [ámbitos de permiso de Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).

Si quiere ver explicaciones sobre `openid` o `offline_access` como los ámbitos de OpenID Connect, consulte [Protocolos de la versión 2.0: Flujo de código de autorización de OAuth 2.0](active-directory-v2-protocols-oauth-code.md).

### <a name="configure-your-client-endpoints-by-editing-hello-oidcendpointsxml-file"></a>Configurar los extremos de cliente mediante la edición de archivos de hello oidc_endpoints.xml
* Abra hello `oidc_endpoints.xml` de archivos y que Hola siguientes cambios:
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

Nunca deben cambiar estos puntos de conexión si usa OAuth2 como protocolo.

> [!NOTE]
> Hola extremos para `userInfoEndpoint` y `revocationEndpoint` no son compatibles actualmente con Azure Active Directory. Si deja junto con el valor de ejemplo.com Hola predeterminado, se le recordará que no están disponibles en el ejemplo de Hola :-)
> 
> 

## <a name="configure-a-graph-api-call"></a>Configuración de una llamada de API Graph
* Abra hello `HomeActivity.java` de archivos y que Hola siguientes cambios:
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

Aquí se muestra una llamada sencilla a la API Graph que devuelve nuestra información.

Éstos son todos los cambios de Hola que necesita toodo. Ejecute hello `oidlib-sample` aplicación y haga clic en **iniciar sesión en**.

Una vez haya autenticado correctamente, seleccione hello **solicitar el recurso protegido** botón tootest su toohello de llamada de API Graph.

## <a name="get-security-updates-for-our-product"></a>Obtención de actualizaciones de seguridad para nuestro producto
Le recomendamos que tooget notificaciones acerca de los incidentes de seguridad visitando hello [TechCenter de seguridad](https://technet.microsoft.com/security/dd252948) y la suscripción tooSecurity asesoramiento alertas.

