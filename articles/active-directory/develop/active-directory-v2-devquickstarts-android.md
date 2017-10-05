---
title: "Aplicación para Android de la versión 2.0 de Azure Active Directory | Microsoft Docs"
description: "Procedimiento para compilar una aplicación Android con la que los usuarios pueden iniciar sesión utilizando tanto su cuenta personal de Microsoft y sus cuentas profesionales o educativas, además de realizar llamadas a la API Graph mediante bibliotecas de terceros."
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
ms.openlocfilehash: c0a5a818c61f7af7ff04bf890b54e8364f3b21b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-android-app-using-a-third-party-library-with-graph-api-using-the-v20-endpoint"></a><span data-ttu-id="c78e0-103">Adición de inicio de sesión a una aplicación Android mediante una biblioteca de terceros con la API Graph mediante la versión 2.0 del punto de conexión</span><span class="sxs-lookup"><span data-stu-id="c78e0-103">Add sign-in to an Android app using a third-party library with Graph API using the v2.0 endpoint</span></span>
<span data-ttu-id="c78e0-104">La plataforma Microsoft Identity utiliza estándares abiertos como OAuth2 y OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="c78e0-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="c78e0-105">Los desarrolladores pueden usar la biblioteca que quieran integrar con nuestros servicios.</span><span class="sxs-lookup"><span data-stu-id="c78e0-105">Developers can use any library they want to integrate with our services.</span></span> <span data-ttu-id="c78e0-106">Para ayudar a los desarrolladores a utilizar nuestra plataforma con otras bibliotecas, hemos escrito algunos tutoriales como este para demostrar cómo configurar bibliotecas de terceros con el objetivo de conectarse a la plataforma Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="c78e0-106">To help developers use our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure third-party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="c78e0-107">La mayoría de las bibliotecas que implementan [la especificación OAuth2 RFC6749](https://tools.ietf.org/html/rfc6749) pueden conectarse a la plataforma Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="c78e0-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect to the Microsoft identity platform.</span></span>

<span data-ttu-id="c78e0-108">Con la aplicación que se crea en este tutorial, los usuarios podrán iniciar sesión en su organización y, después, buscarse en la organización mediante la API Graph.</span><span class="sxs-lookup"><span data-stu-id="c78e0-108">With the application that this walkthrough creates, users can sign in to their organization and then search for themselves in their organization by using the Graph API.</span></span>

<span data-ttu-id="c78e0-109">Si no está familiarizado con OAuth2 o con OpenID Connect, es posible que gran parte de esta configuración de ejemplo no le sea relevante.</span><span class="sxs-lookup"><span data-stu-id="c78e0-109">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make sense to you.</span></span> <span data-ttu-id="c78e0-110">Si este es el caso, es aconsejable que lea [Protocolos de la versión 2.0: Flujo de código de autorización de OAuth 2.0](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="c78e0-110">We recommend that you read [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="c78e0-111">Algunas características de nuestra plataforma mencionadas en los estándares OAuth2 u OpenID Connect, como el acceso condicional y la administración de directivas de Intune, deben usar nuestras bibliotecas de código abierto de Microsoft Azure Identity.</span><span class="sxs-lookup"><span data-stu-id="c78e0-111">Some features of our platform that do have an expression in the OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you to use our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="c78e0-112">No todas las características y escenarios de Azure Active Directory son compatibles con la versión 2.0 del punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="c78e0-112">The v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="c78e0-113">Para determinar si debe utilizar la versión 2.0 del punto de conexión, obtenga información sobre las [limitaciones de esta versión](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="c78e0-113">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-the-code-from-github"></a><span data-ttu-id="c78e0-114">Descargue el código desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="c78e0-114">Download the code from GitHub</span></span>
<span data-ttu-id="c78e0-115">El código de este tutorial se conserva [en GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span><span class="sxs-lookup"><span data-stu-id="c78e0-115">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span></span>  <span data-ttu-id="c78e0-116">Para continuar, puede [descargar el esqueleto de la aplicación como un archivo .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) o clonar el esqueleto:</span><span class="sxs-lookup"><span data-stu-id="c78e0-116">To follow along, you can  [download the app's skeleton as a .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

<span data-ttu-id="c78e0-117">También puede descargar el ejemplo y comenzar a trabajar inmediatamente:</span><span class="sxs-lookup"><span data-stu-id="c78e0-117">You can also just download the sample and get started right away:</span></span>

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="c78e0-118">Registrar una aplicación</span><span class="sxs-lookup"><span data-stu-id="c78e0-118">Register an app</span></span>
<span data-ttu-id="c78e0-119">Cree una nueva aplicación en el [Portal de registro de aplicaciones](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) o siga los pasos que se detallan en [Cómo registrar una aplicación con el punto de conexión v2.0](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="c78e0-119">Create a new app at the [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow the detailed steps at [How to register an app with the v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="c78e0-120">Asegúrese de que:</span><span class="sxs-lookup"><span data-stu-id="c78e0-120">Make sure to:</span></span>

* <span data-ttu-id="c78e0-121">Copie el **id. de aplicación** asignado a su aplicación, ya que lo necesitará pronto.</span><span class="sxs-lookup"><span data-stu-id="c78e0-121">Copy the **Application Id** that's assigned to your app because you'll need it soon.</span></span>
* <span data-ttu-id="c78e0-122">Agregar la plataforma **Móvil** a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c78e0-122">Add the **Mobile** platform for your app.</span></span>

> <span data-ttu-id="c78e0-123">Nota: El portal de registro de la aplicación proporciona un valor de **URI de redirección** .</span><span class="sxs-lookup"><span data-stu-id="c78e0-123">Note: The Application registration portal provides a **Redirect URI** value.</span></span> <span data-ttu-id="c78e0-124">Sin embargo, en este ejemplo debe utilizar el valor predeterminado de `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span><span class="sxs-lookup"><span data-stu-id="c78e0-124">However, in this example you must use the default value of `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span></span>
> 
> 

## <a name="download-the-nxoauth2-third-party-library-and-create-a-workspace"></a><span data-ttu-id="c78e0-125">Descarga de la biblioteca de terceros NXOAuth2 y creación de un área de trabajo</span><span class="sxs-lookup"><span data-stu-id="c78e0-125">Download the NXOAuth2 third-party library and create a workspace</span></span>
<span data-ttu-id="c78e0-126">Para este tutorial, usaremos OIDCAndroidLib desde GitHub, una biblioteca de OAuth2 basada en el código OpenID Connect de Google.</span><span class="sxs-lookup"><span data-stu-id="c78e0-126">For this walkthrough, you will use the OIDCAndroidLib from GitHub, which is an OAuth2 library based on the OpenID Connect code of Google.</span></span> <span data-ttu-id="c78e0-127">Implementa el perfil de la aplicación nativa y admite el punto de conexión de autorización del usuario.</span><span class="sxs-lookup"><span data-stu-id="c78e0-127">It implements the native application profile and supports the authorization endpoint of the user.</span></span> <span data-ttu-id="c78e0-128">Esto es todo lo que vamos a necesitar para integrarlo con la plataforma de Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="c78e0-128">These are all the things that you'll need to integrate with the Microsoft identity platform.</span></span>

<span data-ttu-id="c78e0-129">Clone el repositorio de OIDCAndroidLib en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c78e0-129">Clone the OIDCAndroidLib repo to your computer.</span></span>

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![androidStudio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a><span data-ttu-id="c78e0-131">Configuración del entorno de Android Studio</span><span class="sxs-lookup"><span data-stu-id="c78e0-131">Set up your Android Studio environment</span></span>
1. <span data-ttu-id="c78e0-132">Cree un nuevo proyecto de Android Studio y acepte los valores predeterminados en el asistente.</span><span class="sxs-lookup"><span data-stu-id="c78e0-132">Create a new Android Studio project and accept the defaults in the wizard.</span></span>
   
    ![Creación de un nuevo proyecto de Android Studio](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![Dispositivos Android de destino](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![Adición de una actividad a móviles](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. <span data-ttu-id="c78e0-136">Para configurar los módulos del proyecto, mueva el repositorio clonado a la ubicación del proyecto.</span><span class="sxs-lookup"><span data-stu-id="c78e0-136">To set up your project modules, move the cloned repo to the project location.</span></span> <span data-ttu-id="c78e0-137">También crear el proyecto y, después, clonarlo directamente en la ubicación del proyecto.</span><span class="sxs-lookup"><span data-stu-id="c78e0-137">You can also create the project and then clone it directly to the project location.</span></span>
   
    ![Módulos del proyecto](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. <span data-ttu-id="c78e0-139">Abra la configuración de los módulos del proyecto mediante el menú contextual o utilizando la combinación de teclas Ctrl+Alt+Mayús+S.</span><span class="sxs-lookup"><span data-stu-id="c78e0-139">Open the project modules settings by using the context menu or by using the Ctrl+Alt+Maj+S shortcut.</span></span>
   
    ![Configuración de los módulos del proyecto](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. <span data-ttu-id="c78e0-141">Quite el módulo de aplicación predeterminado, ya que solo se quiere la configuración del contenedor del proyecto.</span><span class="sxs-lookup"><span data-stu-id="c78e0-141">Remove the default app module because you only want the project container settings.</span></span>
   
    ![El módulo de aplicación predeterminado](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. <span data-ttu-id="c78e0-143">Ahora hay que importar los módulos del repositorio clonado al proyecto actual.</span><span class="sxs-lookup"><span data-stu-id="c78e0-143">Import modules from the cloned repo to the current project.</span></span>
   
    <span data-ttu-id="c78e0-144">![Proyecto de importación gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![crear una nueva página de módulo](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span><span class="sxs-lookup"><span data-stu-id="c78e0-144">![Import gradle project](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![Create new module page](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span></span>
6. <span data-ttu-id="c78e0-145">Repita estos pasos para el módulo `oidlib-sample` .</span><span class="sxs-lookup"><span data-stu-id="c78e0-145">Repeat these steps for the `oidlib-sample` module.</span></span>
7. <span data-ttu-id="c78e0-146">Compruebe las dependencias de oidclib en el módulo `oidlib-sample` .</span><span class="sxs-lookup"><span data-stu-id="c78e0-146">Check the oidclib dependencies on the `oidlib-sample` module.</span></span>
   
    ![Dependencias de oidclib en el módulo oidlib-sample](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. <span data-ttu-id="c78e0-148">Haga clic en **Aceptar** y espere a que se inicie sincronización de gradle.</span><span class="sxs-lookup"><span data-stu-id="c78e0-148">Click **OK** and wait for gradle sync.</span></span>
   
    <span data-ttu-id="c78e0-149">El archivo settings.gradle debe ser similar a este:</span><span class="sxs-lookup"><span data-stu-id="c78e0-149">Your settings.gradle should look like:</span></span>
   
    ![Captura de pantalla de settings.gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. <span data-ttu-id="c78e0-151">Compile la aplicación de ejemplo para asegurarse de que el ejemplo se ejecuta correctamente.</span><span class="sxs-lookup"><span data-stu-id="c78e0-151">Build the sample app to make sure that the sample running correctly.</span></span>
   
    <span data-ttu-id="c78e0-152">Todavía no podrá usarlo con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c78e0-152">You won't be able to use this with Azure Active Directory yet.</span></span> <span data-ttu-id="c78e0-153">Deberá configurar primero algunos puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="c78e0-153">We'll need to configure some endpoints first.</span></span> <span data-ttu-id="c78e0-154">Esto es para asegurarse de que no tiene problemas con Android Studio antes de empezar a personalizar la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c78e0-154">This is to ensure you don't have an Android Studio issues before we start customizing the sample app.</span></span>
10. <span data-ttu-id="c78e0-155">Compile y ejecute `oidlib-sample` como destino en Android Studio.</span><span class="sxs-lookup"><span data-stu-id="c78e0-155">Build and run `oidlib-sample` as the target in Android Studio.</span></span>
    
    ![Progreso de la compilación oidlib-sample](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. <span data-ttu-id="c78e0-157">Elimine el directorio `app ` que quedó al quitar el módulo del proyecto, ya que Android Studio no lo elimina por seguridad.</span><span class="sxs-lookup"><span data-stu-id="c78e0-157">Delete the `app ` directory that was left when you removed the module from the project because Android Studio doesn't delete it for safety.</span></span>
    
    ![Estructura del archivo que incluye el directorio de aplicación](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. <span data-ttu-id="c78e0-159">Abra el menú **Editar configuración** para quitar la configuración de ejecución que quedó al eliminar el módulo del proyecto.</span><span class="sxs-lookup"><span data-stu-id="c78e0-159">Open the **Edit Configurations** menu to remove the run configuration that was also left when you removed the module from the project.</span></span>
    
    <span data-ttu-id="c78e0-160">![Menú Editar configuración](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![Ejecutar configuración de aplicación](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span><span class="sxs-lookup"><span data-stu-id="c78e0-160">![Edit configurations menu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
![Run configuration of app](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span></span>

## <a name="configure-the-endpoints-of-the-sample"></a><span data-ttu-id="c78e0-161">Configuración de los puntos de conexión del ejemplo</span><span class="sxs-lookup"><span data-stu-id="c78e0-161">Configure the endpoints of the sample</span></span>
<span data-ttu-id="c78e0-162">Ahora que `oidlib-sample` se ejecuta correctamente, vamos a modificar algunos puntos de conexión para que funcionen con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c78e0-162">Now that you have the `oidlib-sample` running successfully, let's edit some endpoints to get this working with Azure Active Directory.</span></span>

### <a name="configure-your-client-by-editing-the-oidcclientconfxml-file"></a><span data-ttu-id="c78e0-163">Configuración del cliente modificando el archivo oidc_clientconf.xml</span><span class="sxs-lookup"><span data-stu-id="c78e0-163">Configure your client by editing the oidc_clientconf.xml file</span></span>
1. <span data-ttu-id="c78e0-164">Como estamos usando flujos de OAuth2 para obtener un token y llamar a la API Graph, vamos a configurar el cliente para que solo utilice OAuth2.</span><span class="sxs-lookup"><span data-stu-id="c78e0-164">Because you are using OAuth2 flows only to get a token and call the Graph API, set the client to do OAuth2 only.</span></span> <span data-ttu-id="c78e0-165">El uso de OIDC se tratará en un ejemplo posterior.</span><span class="sxs-lookup"><span data-stu-id="c78e0-165">OIDC will come in a later example.</span></span>
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. <span data-ttu-id="c78e0-166">Configure el id. de cliente que ha recibido en el portal de registro.</span><span class="sxs-lookup"><span data-stu-id="c78e0-166">Configure your client ID that you received from the registration portal.</span></span>
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. <span data-ttu-id="c78e0-167">Configure el URI de redireccionamiento con el siguiente código.</span><span class="sxs-lookup"><span data-stu-id="c78e0-167">Configure your redirect URI with the one below.</span></span>
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. <span data-ttu-id="c78e0-168">Configure los ámbitos que necesita para acceder a la API Graph.</span><span class="sxs-lookup"><span data-stu-id="c78e0-168">Configure your scopes that you need in order to access the Graph API.</span></span>
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

<span data-ttu-id="c78e0-169">El valor `User.Read` en `oidc_scopes` permite leer el perfil básico del usuario que ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="c78e0-169">The `User.Read` value in `oidc_scopes` allows you to read the basic profile the signed in user.</span></span>
<span data-ttu-id="c78e0-170">Puede obtener más información sobre todos los ámbitos disponibles en [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes)(Ámbitos de los permisos de Microsoft Graph).</span><span class="sxs-lookup"><span data-stu-id="c78e0-170">You can learn more about all the available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="c78e0-171">Si quiere ver explicaciones sobre `openid` o `offline_access` como los ámbitos de OpenID Connect, consulte [Protocolos de la versión 2.0: Flujo de código de autorización de OAuth 2.0](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="c78e0-171">If you'd like explanations about `openid` or `offline_access` as scopes in OpenID Connect, see [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md).</span></span>

### <a name="configure-your-client-endpoints-by-editing-the-oidcendpointsxml-file"></a><span data-ttu-id="c78e0-172">Configuración de los puntos de conexión de cliente modificando el archivo oidc_endpoints.xml</span><span class="sxs-lookup"><span data-stu-id="c78e0-172">Configure your client endpoints by editing the oidc_endpoints.xml file</span></span>
* <span data-ttu-id="c78e0-173">Abra el archivo `oidc_endpoints.xml` y realice los siguientes cambios:</span><span class="sxs-lookup"><span data-stu-id="c78e0-173">Open the `oidc_endpoints.xml` file and make the following changes:</span></span>
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

<span data-ttu-id="c78e0-174">Nunca deben cambiar estos puntos de conexión si usa OAuth2 como protocolo.</span><span class="sxs-lookup"><span data-stu-id="c78e0-174">These endpoints should never change if you are using OAuth2 as your protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="c78e0-175">Los puntos de conexión de `userInfoEndpoint` y `revocationEndpoint` no son compatibles actualmente con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c78e0-175">The endpoints for `userInfoEndpoint` and `revocationEndpoint` are currently not supported by Azure Active Directory.</span></span> <span data-ttu-id="c78e0-176">Si deja en ellos el valor predeterminado example.com, se le recordará que no estarán disponibles en el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c78e0-176">If you leave these with the default example.com value, you will be reminded that they are not available in the sample :-)</span></span>
> 
> 

## <a name="configure-a-graph-api-call"></a><span data-ttu-id="c78e0-177">Configuración de una llamada de API Graph</span><span class="sxs-lookup"><span data-stu-id="c78e0-177">Configure a Graph API call</span></span>
* <span data-ttu-id="c78e0-178">Abra el archivo `HomeActivity.java` y realice los siguientes cambios:</span><span class="sxs-lookup"><span data-stu-id="c78e0-178">Open the `HomeActivity.java` file and make the following changes:</span></span>
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

<span data-ttu-id="c78e0-179">Aquí se muestra una llamada sencilla a la API Graph que devuelve nuestra información.</span><span class="sxs-lookup"><span data-stu-id="c78e0-179">Here a simple Graph API call returns our information.</span></span>

<span data-ttu-id="c78e0-180">Estos son todos los cambios que tiene que realizar.</span><span class="sxs-lookup"><span data-stu-id="c78e0-180">Those are all the changes that you need to do.</span></span> <span data-ttu-id="c78e0-181">Ejecute aplicación `oidlib-sample` y haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="c78e0-181">Run the `oidlib-sample` application, and click **Sign in**.</span></span>

<span data-ttu-id="c78e0-182">Cuando se haya autenticado correctamente, haga clic en el botón **Request Protected Resource** (Solicitar recurso protegido) para probar la llamada a la API Graph.</span><span class="sxs-lookup"><span data-stu-id="c78e0-182">After you've successfully authenticated, select the **Request Protected Resource** button to test your call to the Graph API.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="c78e0-183">Obtención de actualizaciones de seguridad para nuestro producto</span><span class="sxs-lookup"><span data-stu-id="c78e0-183">Get security updates for our product</span></span>
<span data-ttu-id="c78e0-184">Le animamos a que obtenga notificaciones de los incidentes de seguridad que se produzcan; para ello, visite la página [TechCenter de seguridad](https://technet.microsoft.com/security/dd252948) y suscríbase a las alertas de documentos informativos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="c78e0-184">We encourage you to get notifications about security incidents by visiting the [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

