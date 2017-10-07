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
# <a name="add-sign-in-tooan-android-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a><span data-ttu-id="7d981-103">Agregar aplicación para Android tooan inicio de sesión mediante una biblioteca de terceros con API Graph con el punto de conexión de hello v2.0</span><span class="sxs-lookup"><span data-stu-id="7d981-103">Add sign-in tooan Android app using a third-party library with Graph API using hello v2.0 endpoint</span></span>
<span data-ttu-id="7d981-104">plataforma de identidad de Microsoft Hello usa estándares abiertos como OAuth2 y OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="7d981-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="7d981-105">Los desarrolladores pueden usar cualquier biblioteca que deseen toointegrate con nuestros servicios.</span><span class="sxs-lookup"><span data-stu-id="7d981-105">Developers can use any library they want toointegrate with our services.</span></span> <span data-ttu-id="7d981-106">toohelp a los desarrolladores usar nuestra plataforma con otras bibliotecas, hemos escrito algunos tutoriales como este uno toodemonstrate la plataforma de identidad de Microsoft de tooconfigure bibliotecas de otros fabricantes tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="7d981-106">toohelp developers use our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure third-party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="7d981-107">La mayoría de las bibliotecas que implementan [especificación de hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) toohello plataforma de identidad de Microsoft se pueden conectar.</span><span class="sxs-lookup"><span data-stu-id="7d981-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect toohello Microsoft identity platform.</span></span>

<span data-ttu-id="7d981-108">Con una aplicación Hola que crea en este tutorial, los usuarios pueden iniciar sesión en la organización de tootheir y, a continuación, buscar por sí mismos en su organización mediante Hola API Graph.</span><span class="sxs-lookup"><span data-stu-id="7d981-108">With hello application that this walkthrough creates, users can sign in tootheir organization and then search for themselves in their organization by using hello Graph API.</span></span>

<span data-ttu-id="7d981-109">Si es nuevo tooOAuth2 u OpenID Connect, gran parte de esta configuración de ejemplo puede que no tenga sentido tooyou.</span><span class="sxs-lookup"><span data-stu-id="7d981-109">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make sense tooyou.</span></span> <span data-ttu-id="7d981-110">Si este es el caso, es aconsejable que lea [Protocolos de la versión 2.0: Flujo de código de autorización de OAuth 2.0](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="7d981-110">We recommend that you read [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="7d981-111">Algunas características de la plataforma que tiene una expresión en Hola OAuth2 o estándares de OpenID Connect, como acceso condicional y administración de directivas de Intune, requieren toouse nuestro código abierto bibliotecas de identidad de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7d981-111">Some features of our platform that do have an expression in hello OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you toouse our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="7d981-112">el punto de conexión de Hello v2.0 no admite todas las características y escenarios de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7d981-112">hello v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="7d981-113">toodetermine si debe utilizar Hola v2.0 extremo, que conozca [v2.0 limitaciones](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="7d981-113">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-hello-code-from-github"></a><span data-ttu-id="7d981-114">Descargar código de hello desde GitHub</span><span class="sxs-lookup"><span data-stu-id="7d981-114">Download hello code from GitHub</span></span>
<span data-ttu-id="7d981-115">código de Hello para este tutorial se mantiene [en GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span><span class="sxs-lookup"><span data-stu-id="7d981-115">hello code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span></span>  <span data-ttu-id="7d981-116">toofollow a lo largo, puede [descargar el esqueleto de la aplicación hello como .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) o esqueleto de Hola de clon:</span><span class="sxs-lookup"><span data-stu-id="7d981-116">toofollow along, you can  [download hello app's skeleton as a .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

<span data-ttu-id="7d981-117">También se puede descargar el ejemplo de Hola y empezar a trabajar de forma inmediata:</span><span class="sxs-lookup"><span data-stu-id="7d981-117">You can also just download hello sample and get started right away:</span></span>

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="7d981-118">Registrar una aplicación</span><span class="sxs-lookup"><span data-stu-id="7d981-118">Register an app</span></span>
<span data-ttu-id="7d981-119">Crear una nueva aplicación en hello [portal de registro de aplicación](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), o siga Hola pasos detallados en [cómo una aplicación con el punto de conexión de hello v2.0 tooregister](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="7d981-119">Create a new app at hello [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow hello detailed steps at [How tooregister an app with hello v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="7d981-120">Asegúrese de que:</span><span class="sxs-lookup"><span data-stu-id="7d981-120">Make sure to:</span></span>

* <span data-ttu-id="7d981-121">Hola copia **identificador de la aplicación** que está asignado tooyour aplicación porque lo necesitará pronto.</span><span class="sxs-lookup"><span data-stu-id="7d981-121">Copy hello **Application Id** that's assigned tooyour app because you'll need it soon.</span></span>
* <span data-ttu-id="7d981-122">Agregar hello **Mobile** plataforma para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7d981-122">Add hello **Mobile** platform for your app.</span></span>

> <span data-ttu-id="7d981-123">Nota: portal de registro de aplicación Hola proporciona un **URI de redireccionamiento** valor.</span><span class="sxs-lookup"><span data-stu-id="7d981-123">Note: hello Application registration portal provides a **Redirect URI** value.</span></span> <span data-ttu-id="7d981-124">Sin embargo, en este ejemplo debe usar valor predeterminado de Hola de `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span><span class="sxs-lookup"><span data-stu-id="7d981-124">However, in this example you must use hello default value of `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span></span>
> 
> 

## <a name="download-hello-nxoauth2-third-party-library-and-create-a-workspace"></a><span data-ttu-id="7d981-125">Descargar la biblioteca de otro fabricante NXOAuth2 hello y crear un área de trabajo</span><span class="sxs-lookup"><span data-stu-id="7d981-125">Download hello NXOAuth2 third-party library and create a workspace</span></span>
<span data-ttu-id="7d981-126">En este tutorial, usará hello OIDCAndroidLib desde GitHub, que es una biblioteca de OAuth2 basada en hello código OpenID Connect de Google.</span><span class="sxs-lookup"><span data-stu-id="7d981-126">For this walkthrough, you will use hello OIDCAndroidLib from GitHub, which is an OAuth2 library based on hello OpenID Connect code of Google.</span></span> <span data-ttu-id="7d981-127">Implementa el perfil de aplicación nativa de Hola y es compatible con el extremo de autorización de saludo del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="7d981-127">It implements hello native application profile and supports hello authorization endpoint of hello user.</span></span> <span data-ttu-id="7d981-128">Éstos son todos los puntos de Hola que necesitará toointegrate a la plataforma de identidad de Microsoft de Hola.</span><span class="sxs-lookup"><span data-stu-id="7d981-128">These are all hello things that you'll need toointegrate with hello Microsoft identity platform.</span></span>

<span data-ttu-id="7d981-129">Clonar equipo tooyour de hello OIDCAndroidLib repositorio.</span><span class="sxs-lookup"><span data-stu-id="7d981-129">Clone hello OIDCAndroidLib repo tooyour computer.</span></span>

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![androidStudio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a><span data-ttu-id="7d981-131">Configuración del entorno de Android Studio</span><span class="sxs-lookup"><span data-stu-id="7d981-131">Set up your Android Studio environment</span></span>
1. <span data-ttu-id="7d981-132">Crear un nuevo proyecto de Android Studio y acepte los valores predeterminados de hello en el Asistente de Hola.</span><span class="sxs-lookup"><span data-stu-id="7d981-132">Create a new Android Studio project and accept hello defaults in hello wizard.</span></span>
   
    ![Creación de un nuevo proyecto de Android Studio](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![Dispositivos Android de destino](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![Agregar una actividad toomobile](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. <span data-ttu-id="7d981-136">tooset de los módulos de proyecto, mover ubicación del proyecto de hello clonar repositorio toohello.</span><span class="sxs-lookup"><span data-stu-id="7d981-136">tooset up your project modules, move hello cloned repo toohello project location.</span></span> <span data-ttu-id="7d981-137">También puede crear proyecto hello y, a continuación, clonarlo directamente toohello ubicación del proyecto.</span><span class="sxs-lookup"><span data-stu-id="7d981-137">You can also create hello project and then clone it directly toohello project location.</span></span>
   
    ![Módulos del proyecto](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. <span data-ttu-id="7d981-139">Abrir configuración de módulos de hello proyecto mediante el menú contextual de Hola o utilizando el método abreviado Ctrl + Alt + rincipales + S de Hola.</span><span class="sxs-lookup"><span data-stu-id="7d981-139">Open hello project modules settings by using hello context menu or by using hello Ctrl+Alt+Maj+S shortcut.</span></span>
   
    ![Configuración de los módulos del proyecto](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. <span data-ttu-id="7d981-141">Quite el módulo de aplicación de hello predeterminada porque solo se desea configuración Hola del contenedor de proyecto.</span><span class="sxs-lookup"><span data-stu-id="7d981-141">Remove hello default app module because you only want hello project container settings.</span></span>
   
    ![módulo de aplicación de Hello predeterminado](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. <span data-ttu-id="7d981-143">Importar módulos desde el proyecto actual de hello repositorio clonado toohello.</span><span class="sxs-lookup"><span data-stu-id="7d981-143">Import modules from hello cloned repo toohello current project.</span></span>
   
    <span data-ttu-id="7d981-144">![Proyecto de importación gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![crear una nueva página de módulo](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span><span class="sxs-lookup"><span data-stu-id="7d981-144">![Import gradle project](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![Create new module page](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span></span>
6. <span data-ttu-id="7d981-145">Repita estos pasos para hello `oidlib-sample` módulo.</span><span class="sxs-lookup"><span data-stu-id="7d981-145">Repeat these steps for hello `oidlib-sample` module.</span></span>
7. <span data-ttu-id="7d981-146">Comprobar las dependencias de oidclib hello en hello `oidlib-sample` módulo.</span><span class="sxs-lookup"><span data-stu-id="7d981-146">Check hello oidclib dependencies on hello `oidlib-sample` module.</span></span>
   
    ![dependencias de oidclib en el módulo de oidlib ejemplo de Hola](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. <span data-ttu-id="7d981-148">Haga clic en **Aceptar** y espere a que se inicie sincronización de gradle.</span><span class="sxs-lookup"><span data-stu-id="7d981-148">Click **OK** and wait for gradle sync.</span></span>
   
    <span data-ttu-id="7d981-149">El archivo settings.gradle debe ser similar a este:</span><span class="sxs-lookup"><span data-stu-id="7d981-149">Your settings.gradle should look like:</span></span>
   
    ![Captura de pantalla de settings.gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. <span data-ttu-id="7d981-151">Generar toomake de aplicación de ejemplo de Hola seguro ese ejemplo Hola ejecutando correctamente.</span><span class="sxs-lookup"><span data-stu-id="7d981-151">Build hello sample app toomake sure that hello sample running correctly.</span></span>
   
    <span data-ttu-id="7d981-152">No será capaz de toouse esto con Azure Active Directory todavía.</span><span class="sxs-lookup"><span data-stu-id="7d981-152">You won't be able toouse this with Azure Active Directory yet.</span></span> <span data-ttu-id="7d981-153">Necesitaremos tooconfigure algunos puntos de conexión en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="7d981-153">We'll need tooconfigure some endpoints first.</span></span> <span data-ttu-id="7d981-154">Se trata de tooensure no tiene un problemas Android Studio antes de empezar a personalizar la aplicación de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7d981-154">This is tooensure you don't have an Android Studio issues before we start customizing hello sample app.</span></span>
10. <span data-ttu-id="7d981-155">Compile y ejecute `oidlib-sample` como destino de hello en Android Studio.</span><span class="sxs-lookup"><span data-stu-id="7d981-155">Build and run `oidlib-sample` as hello target in Android Studio.</span></span>
    
    ![Progreso de la compilación oidlib-sample](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. <span data-ttu-id="7d981-157">Eliminar hello `app ` directorio que se dejó cuando quita el módulo de Hola de proyecto Hola porque Android Studio no se elimina, por motivos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="7d981-157">Delete hello `app ` directory that was left when you removed hello module from hello project because Android Studio doesn't delete it for safety.</span></span>
    
    ![Estructura del archivo que incluye el directorio de aplicación Hola](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. <span data-ttu-id="7d981-159">Abra hello **editar configuraciones** tooremove Hola ejecutar configuración de menú del que también se dejó cuando quita el módulo de Hola de proyecto Hola.</span><span class="sxs-lookup"><span data-stu-id="7d981-159">Open hello **Edit Configurations** menu tooremove hello run configuration that was also left when you removed hello module from hello project.</span></span>
    
    <span data-ttu-id="7d981-160">![Menú Editar configuración](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![Ejecutar configuración de aplicación](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span><span class="sxs-lookup"><span data-stu-id="7d981-160">![Edit configurations menu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
![Run configuration of app](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span></span>

## <a name="configure-hello-endpoints-of-hello-sample"></a><span data-ttu-id="7d981-161">Configurar los extremos de Hola de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="7d981-161">Configure hello endpoints of hello sample</span></span>
<span data-ttu-id="7d981-162">Ahora que tiene hello `oidlib-sample` ejecuta correctamente, editar algunos puntos de conexión tooget este trabajo con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7d981-162">Now that you have hello `oidlib-sample` running successfully, let's edit some endpoints tooget this working with Azure Active Directory.</span></span>

### <a name="configure-your-client-by-editing-hello-oidcclientconfxml-file"></a><span data-ttu-id="7d981-163">Configurar al cliente mediante la edición de archivos de hello oidc_clientconf.xml</span><span class="sxs-lookup"><span data-stu-id="7d981-163">Configure your client by editing hello oidc_clientconf.xml file</span></span>
1. <span data-ttu-id="7d981-164">Dado que usa OAuth2 flujos solo tooget un token y llamar a la API Graph hello, establecer cliente toodo OAuth2 de hello solo.</span><span class="sxs-lookup"><span data-stu-id="7d981-164">Because you are using OAuth2 flows only tooget a token and call hello Graph API, set hello client toodo OAuth2 only.</span></span> <span data-ttu-id="7d981-165">El uso de OIDC se tratará en un ejemplo posterior.</span><span class="sxs-lookup"><span data-stu-id="7d981-165">OIDC will come in a later example.</span></span>
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. <span data-ttu-id="7d981-166">Configure su ID de cliente que recibió del portal de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="7d981-166">Configure your client ID that you received from hello registration portal.</span></span>
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. <span data-ttu-id="7d981-167">A continuación, configure el URI de redirección con hello uno.</span><span class="sxs-lookup"><span data-stu-id="7d981-167">Configure your redirect URI with hello one below.</span></span>
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. <span data-ttu-id="7d981-168">Configurar los ámbitos que se necesita en orden tooaccess Hola API Graph.</span><span class="sxs-lookup"><span data-stu-id="7d981-168">Configure your scopes that you need in order tooaccess hello Graph API.</span></span>
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

<span data-ttu-id="7d981-169">Hola `User.Read` valor en `oidc_scopes` permite tooread Hola perfil básico Hola firmado en usuario.</span><span class="sxs-lookup"><span data-stu-id="7d981-169">hello `User.Read` value in `oidc_scopes` allows you tooread hello basic profile hello signed in user.</span></span>
<span data-ttu-id="7d981-170">Puede aprender más acerca de todos los ámbitos disponibles de hello en [ámbitos de permiso de Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).</span><span class="sxs-lookup"><span data-stu-id="7d981-170">You can learn more about all hello available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="7d981-171">Si quiere ver explicaciones sobre `openid` o `offline_access` como los ámbitos de OpenID Connect, consulte [Protocolos de la versión 2.0: Flujo de código de autorización de OAuth 2.0](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="7d981-171">If you'd like explanations about `openid` or `offline_access` as scopes in OpenID Connect, see [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md).</span></span>

### <a name="configure-your-client-endpoints-by-editing-hello-oidcendpointsxml-file"></a><span data-ttu-id="7d981-172">Configurar los extremos de cliente mediante la edición de archivos de hello oidc_endpoints.xml</span><span class="sxs-lookup"><span data-stu-id="7d981-172">Configure your client endpoints by editing hello oidc_endpoints.xml file</span></span>
* <span data-ttu-id="7d981-173">Abra hello `oidc_endpoints.xml` de archivos y que Hola siguientes cambios:</span><span class="sxs-lookup"><span data-stu-id="7d981-173">Open hello `oidc_endpoints.xml` file and make hello following changes:</span></span>
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

<span data-ttu-id="7d981-174">Nunca deben cambiar estos puntos de conexión si usa OAuth2 como protocolo.</span><span class="sxs-lookup"><span data-stu-id="7d981-174">These endpoints should never change if you are using OAuth2 as your protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="7d981-175">Hola extremos para `userInfoEndpoint` y `revocationEndpoint` no son compatibles actualmente con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7d981-175">hello endpoints for `userInfoEndpoint` and `revocationEndpoint` are currently not supported by Azure Active Directory.</span></span> <span data-ttu-id="7d981-176">Si deja junto con el valor de ejemplo.com Hola predeterminado, se le recordará que no están disponibles en el ejemplo de Hola :-)</span><span class="sxs-lookup"><span data-stu-id="7d981-176">If you leave these with hello default example.com value, you will be reminded that they are not available in hello sample :-)</span></span>
> 
> 

## <a name="configure-a-graph-api-call"></a><span data-ttu-id="7d981-177">Configuración de una llamada de API Graph</span><span class="sxs-lookup"><span data-stu-id="7d981-177">Configure a Graph API call</span></span>
* <span data-ttu-id="7d981-178">Abra hello `HomeActivity.java` de archivos y que Hola siguientes cambios:</span><span class="sxs-lookup"><span data-stu-id="7d981-178">Open hello `HomeActivity.java` file and make hello following changes:</span></span>
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

<span data-ttu-id="7d981-179">Aquí se muestra una llamada sencilla a la API Graph que devuelve nuestra información.</span><span class="sxs-lookup"><span data-stu-id="7d981-179">Here a simple Graph API call returns our information.</span></span>

<span data-ttu-id="7d981-180">Éstos son todos los cambios de Hola que necesita toodo.</span><span class="sxs-lookup"><span data-stu-id="7d981-180">Those are all hello changes that you need toodo.</span></span> <span data-ttu-id="7d981-181">Ejecute hello `oidlib-sample` aplicación y haga clic en **iniciar sesión en**.</span><span class="sxs-lookup"><span data-stu-id="7d981-181">Run hello `oidlib-sample` application, and click **Sign in**.</span></span>

<span data-ttu-id="7d981-182">Una vez haya autenticado correctamente, seleccione hello **solicitar el recurso protegido** botón tootest su toohello de llamada de API Graph.</span><span class="sxs-lookup"><span data-stu-id="7d981-182">After you've successfully authenticated, select hello **Request Protected Resource** button tootest your call toohello Graph API.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="7d981-183">Obtención de actualizaciones de seguridad para nuestro producto</span><span class="sxs-lookup"><span data-stu-id="7d981-183">Get security updates for our product</span></span>
<span data-ttu-id="7d981-184">Le recomendamos que tooget notificaciones acerca de los incidentes de seguridad visitando hello [TechCenter de seguridad](https://technet.microsoft.com/security/dd252948) y la suscripción tooSecurity asesoramiento alertas.</span><span class="sxs-lookup"><span data-stu-id="7d981-184">We encourage you tooget notifications about security incidents by visiting hello [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

